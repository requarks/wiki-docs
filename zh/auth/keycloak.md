---
title: Keycloak
description: 身份验证模块
published: true
date: 2023-01-29T10:37:51.960Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:22.614Z
---

# Keycloak
[Keycloak](https://keycloak.org) 是一个用于现代应用程序和服务的开源身份和访问管理解决方案。

## 相关信息
- [Keycloak OIDC Endpoints](https://www.keycloak.org/docs/latest/server_admin/#keycloak-server-oidc-uri-endpoints)
- [Keycloak OIDC 客户端](https://www.keycloak.org/docs/latest/server_admin/#_clients)

## 配置
### 在Wiki.js中创建Keycloak登录策略实例
1. 在您wiki的管理区中，点击左侧导航栏中的`身份验证`。
2. 点击 `+ 创建策略`, 下滑并选中 `Keycloak`
3. 到页面底部，复制/记录 `回调 URL / 重定向 URI`
4. 保持此页面/标签页打开。我们将在设置Keyclock客户端后填写其余内容

### 创建Keycloak客户端
1. 在Keycloak管理页面中，转到`客户端`菜单，并点击右侧的`创建`按钮。
2. 输入一个**客户端ID**, 例如 `wikijs` (我们后面会用到这个 `客户端ID` )
3. 选择 **openid-connect** 为 `客户端协议`
4. 将您wiki的域名填入**根URL** (例如 `https://wiki.example.com`)
5. 点击 **保存**
6. 修改 **访问类型** 为 `confidential`
7. 输入 **合法重定向URIs**, 也就是Wiki.js里的 `回调 URL / 重定向 URI` (例： `https://wiki.example.com/login/d03f689b-0dd0-44d6-90ca-6386ec41d799/callback`, 或仅输入路径 `/login/{GUID}/callback`)
8. 将 **基准URL** 设为与 `根URL` 相同
9. 将 **Web源** 设为 `+`, 这意味着使用`合法重定向URI`中的URI。
10. 现在点击页面底部的 **保存**
11. 转到 **凭据** 标签页并复制 `密钥` (这个我们后面也会用到)

### 在Wiki.js中配置Keycloak登录策略
1. 如果你之前没有保留第一步中的标签页， 请进入您wiki的管理区，点击左侧导航栏中的`身份验证`。
2. 点击**Keycloak**
3. 填入**Host**, 即您Keyclock服务端的域名 (包含协议头) (例如: `https://keycloak.example.com`)
4. 填入**Realm**, 即您在Keycloak中使用的realm (默认为: `master`)
5. 填入**客户端Id**, 即Keycloak中的 `客户端ID`
6. 填入**客户端密钥**, 即Keycloak中的 `密钥`
7. 填入**身份认证 Endpoint URL**, 即 `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/auth`
8. 填入**Token URL**, 即 `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/token`
9. 填入**用户信息URL**, 即 `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/userinfo`
10. 如果您希望用户在从Wiki.js注销的同时从Keyclock注销，请启用`注销时从Keyclock注销`
11. 输入`登出Endpoint URL`, 即 `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/logout`
12. 启用 **开放注册** 来启用Keyclok登录按钮, 为首次通过Keycloak登录的用户自动创建wiki账户。 
13. 记得在**分配到用户组**列表中添加一个至少具有读权限的用户组。
14. 点击右上角的 `应用` 并尝试登陆

### 无缝登录
如果登录策略配置正确，您可以在左侧导航菜单的`安全`选项卡下启用`跳过登录界面`。
请确保Keycloak在`身份认证`选项卡下的登录服务提供者列表的顶部。

![](https://static.requarks.io/logo/keycloak.svg =x50){.align-abstopright}