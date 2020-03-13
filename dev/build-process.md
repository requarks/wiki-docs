---
title: Build Process
description: Reproducable build process of Wiki.js
published: true
date: 2020-03-13T23:53:00.326Z
tags: 
---

# Build & Deployment Flow

All builds are done via Azure DevOps and can be [viewed online](https://dev.azure.com/requarks/wiki/_build?definitionId=9).

Every commit generates a new build and increments the build number by one *(MAJOR.MINOR.BUILD)*.

The following processes are documented for understanding how the builds are produced. They are not meant to be used as a deployment method for production usage. Please use the prebuilt packages / images [as detailed in the docs](/install) instead.

# Build Process

## Task 1 - Disable dev Flag

Using the **Command Line** task:

```bash
sudo apt-get install jq -y
mv package.json pkg-temp.json
jq -r '.dev |= false' pkg-temp.json > package.json
rm pkg-temp.json
```

## Task 2 - Set Build Version

Using the [Version JSON File](https://github.com/rfennell/AzurePipelines/wiki/Version-Assemblies-and-Packages-Tasks) task, inject the `version` field in `package.json` with value `$(Build.BuildNumber)`

## Task 3 - Compile Assets

Using the **Docker** task, build and push the image `requarks/wiki`, with tag `canary` using Dockerfile `dev/build/Dockerfile`

## Task 4 - Extract Compiled Assets

Using the **Command Line** task:

```bash
docker create --name wiki requarks/wiki:canary
docker cp wiki:/wiki $(Build.StagingDirectory)
docker rm wiki
rm $(Build.StagingDirectory)/wiki/config.yml
rm $(Build.StagingDirectory)/wiki/wait.sh
cp $(System.DefaultWorkingDirectory)/config.sample.yml $(Build.StagingDirectory)/wiki/config.sample.yml
find $(Build.StagingDirectory)/wiki/ -printf "%P\n" | tar -czf wiki-js.tar.gz --no-recursion -C $(Build.StagingDirectory)/wiki/ -T -
```

## Task 5 - Publish Artifact

Using the **Publish build artifacts** task, publish the `wiki-js.tar.gz` file as artifact `drop` to Azure Pipelines.

# Release Process

When the latest build is selected for release, the following steps are executed in Azure DevOps:

## BETA

```bash
docker pull requarks/wiki:canary
docker tag requarks/wiki:canary requarks/wiki:beta
docker push requarks/wiki:beta
```

The artifacts from the build are also published as a **GitHub Release** using the associated source version + tag. An auto-generated changelog listing all commits since the last release is added as content. The release is set as **Pre-release**.

The following assets, coming from the build artifacts, are attached to the release:
```
$(System.DefaultWorkingDirectory)/_build/drop/*.tar.gz
$(System.DefaultWorkingDirectory)/_build/drop-win/*.tar.gz
```

Upon completion, the release pipeline is gated until manual approval.

## GA

```bash
docker pull requarks/wiki:beta

curl -LJO https://static.requarks.io/semver
chmod +x semver

MAJOR=`./semver get major $(Build.BuildNumber)`
MINOR=`./semver get minor $(Build.BuildNumber)`
MAJORMINOR="$MAJOR.$MINOR"

echo "Using major $MAJOR and minor $MINOR..."

docker tag requarks/wiki:beta requarks/wiki:$(Build.BuildNumber)
docker tag requarks/wiki:beta requarks/wiki:$MAJOR
docker tag requarks/wiki:beta requarks/wiki:$MAJORMINOR
docker tag requarks/wiki:beta requarks/wiki:latest

docker push requarks/wiki:$(Build.BuildNumber)
docker push requarks/wiki:$MAJOR
docker push requarks/wiki:$MAJORMINOR
docker push requarks/wiki:latest
```

The GitHub Release is also modified to remove the Pre-Release flag.