---
title: 身份验证
description: 支持的身份验证模块列表
published: true
date: 2023-03-16T08:45:000Z
tags: auth, 身份验证
editor: markdown
dateCreated: 2023-01-08T10:33:13.500Z
---

身份验证模块允许安全和简单的登录。

在管理区，您可以启用最适合您的身份验证策略，可以同时启用多种策略。例如，您可以允许用户使用其Google、Facebook或GitHub账户登录。

需要注意的是，默认的 **本地** 验证策略需要供全局管理员登录使用，无法被禁用。

大多数验证策略都需要进行一些配置。您可以查看下面的链接来获取配置指导。

# Modules

- [Auth0](/auth/auth0)
- [Azure AD](/auth/azure)
- CAS
- [Discord](/auth/discord)
- [Dropbox](/auth/dropbox)
- [Facebook](/auth/facebook)
- Firebase
- [GitHub](/auth/github)
- [Google](/auth/google)
- [Keycloak OpenID Connect](/auth/keycloak)
- [LDAP / Active Directory](/auth/ldap)
- [本地](/auth/local)
- Microsoft
- Generic OpenID / OAuth2
- [Okta](/auth/okta)
- [SAML 2.0](/auth/saml)
- [Slack](/auth/slack)
- [Twitch](/auth/twitch)
{.links-list}

# 开放注册

**默认情况下，新用户无权访问任何内容。** 新用户必须由管理员预先授权，或使用开放注册纳入现有用户组。

后者大大简化了新用户的注册流程。您可以根据每个身份验证策略启用开放注册。

## 配置

在身份验证模块配置页面上，启用**开放注册**选项。

作为可选措施，您可以设定一个域名白名单，这样只有指定域的用户可以注册。要启用这项措施，您需要输入一组域名，例如： `company.com`，然后按下 <kbd>Enter</kbd> 键。对所有需要授权的域重复这个操作。

最后，选择一个新用户首次登录会被自动分配到的用户组。

点击**应用**来保存这项设置。

# 两步验证

> 此功能只在 **2.5 及以上版本** 可用。
{.is-info}

两步验证（2FA）为用户帐户添加了一层额外保护。它将你知道的东西（你的密码）与你拥有的东西（*手机、指纹、安全钥匙等*）结合在一起。

即使恶意用户获取了您的密码，他们也无法登录，因为他们没有“第二身份验证要素”。

## 开始配置

两步验证可以对所有用户启用，也可以对每个用户分别配置。

### 全局启用

要强制所有用户启用两步验证，转到**管理区**并点击侧边栏中的**安全**选项。

启用 **强制两步验证** 选项并点击**应用**。

所有用户都将在下次登录时被要求为他们的账户设定两步验证。

### 对特定用户启用

在**管理区**，点击侧边栏中的**用户**选项。

选择要启用两步验证的用户，并点击**两步验证**这一列的开关使其变为**启用**状态。

该用户会在下次登录时被要求为他的账户设置两步验证。

> 目前，只有管理员才能为用户启用两步验证。未来将支持让用户自行启用两步验证。
{.is-info}

## 支持的验证方法

- **OTP (一次性密码)** <i class="mdi mdi-check green--text"></i>
	- TOTP *(Authy, Google Authenticator, Microsoft Authenticator)*{.caption} <i class="mdi mdi-check green--text"></i>
- **WebAuthn** <i class="mdi mdi-clock-outline orange--text"></i> *(计划之后支持)*{.caption .orange--text .text--darken-3}
	- Windows Hello
  - FIDO2 *(Yubikey 5)*{.caption}
  - FIDO U2F *(Yubikey 4 and earlier, Google Titan Key)*{.caption}
- **短信验证码** <i class="mdi mdi-close red--text"></i> *(由于此方法**不安全**且不可靠，不计划在将来提供支持。)*{.caption .red--text}

# 自定义登录流程

在**管理区** > **安全** 中，您可以修改登录流程对用户的呈现方式。

## 登录页背景图

您可以为登录页设置另外的背景图。在相应设置项中输入图像的完整路径即可*(.jpg / .png)*。

> 需要注意的是，如果您直接向wiki上传图片，您需要保证Guest用户组有权访问对应路径！建议您将图片上传到专门的目录，并授予Guest用户组对该目录路径的`read:assets`权限。
{.is-warning}

## 跳过登录界面

当使用社交网络 *（如：谷歌认证）* 作为登录服务提供商时，你可能希望直接跳过登录界面，将用户直接跳转到登录服务提供商的界面以加快登录流程。

> 在这项设置启用的情况下，您仍然可以通过在登录URL后加上`?all=1`来访问登陆界面。 *(如： `https://wiki.example.com/login?all=1`)*
{.is-info}

## 隐藏本地登录

如果您启用了多个身份验证提供程序，但希望隐藏默认的本地提供程序，则可以启用此选项来隐藏它。

> 在这项设置启用的情况下，您仍然可以通过在登录URL后加上`?all=1`来显示本地登录。 *(如： `https://wiki.example.com/login?all=1`)*
{.is-info}
