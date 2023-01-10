---
title: Users, Groups & Permissions
description: Manage access to your wiki
published: true
date: 2023-01-10T03:21:58.201Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:33:27.804Z
---

虽然一个好的wiki是任何人都可以贡献新内容的地方，但最好将某些部分和特定操作限制在您选定的用户中。

Wiki.js拥有强大的权限系统，可以精细控制用户能看到的内容和能执行的操作。

# 概述

Wiki.js的权限系统基于4个概念设计：

- **用户组**
- **用户**
- **权限**
- **页面规则**
{.grid-list}

一个用户组包含数个用户、一组权限和一组页面规则。

![diag-permissions.jpg](/assets/diagrams/diag-permissions.webp =1000x){.decor-shadow .radius-4}

**用户** 可以属于 **一个或多个** 用户组。

**用户组** 规定用户能看到的内容和能执行的操作。 它通过两个概念来实现这一点： **全局权限** 和 **页面规则**.

**全局权限** 授权用户执行特定操作。例如，全局权限 `read:pages` 允许用户访问页面，而全局权限 `write:assets` 允许用户上传图片和文件。 这些全局权限起总开关的作用，以 **允许或拒绝** 用户在wiki上执行特定操作。

全局权限可以有效控制用户可以执行的操作，但它不能控制权限被应用在**在哪些地方**。 比如，你有可能想要一名用户能查看在 `/cities` 目录下的页面， 但不能查看在 `/secret` 目录下的页面。 这就是 **页面规则** 发挥作用的地方。

**页面规则** 确定全局权限的生效范围。

---

**让我们用下面的例子来解释：**
*我们想让用户组 XYZ 下的用户可以查看路径 `/cities/montreal` 的页面和资源*

需要设定如下的页面规则：

- 允许或拒绝: `允许`
- 权限: `read:pages, read:assets`
- 匹配规则: `路径精确匹配...`
- 匹配值: `/cities/montreal`
{.grid-list}

![ss-pagerule-ex1.png](/assets/examples/ss-pagerule-ex1.webp =1000x)

将上述内容汇总起来，这个用户组需要被这样设置：

- 拥有数名用户
- 启用全局权限 `read:pages` 和 `read:assets`
- 有一条权限为 `允许` `read:pages, read:assets`，使用匹配规则为 `路径精确匹配`... `/cities/montreal` 的页面规则。

---

***规则的应用顺序是？***

规则按精确度应用。更精确的路径的页面规则将覆盖之前的页面规则。

比如, 应用于`/geography/countries`的页面规则将覆盖应用于`/geography`的页面规则。

当两条规则精确度相同（目录的层数相同）时，将按照如下顺序从低优先级到高优先级确定规则：
- 路径开头匹配... *(优先级最低)*{.caption}
- 路径结尾匹配...
- 路径通配符匹配...
- 路径精确匹配... *(优先级最高)*{.caption}

当两条页面规则的精确度和匹配规则均相同时, `拒绝` 规则将默认覆盖 `允许` 规则.

***默认的权限行为是？***

除非您明确对某一权限添加一条 `允许` 规则, 它将始终被默认拒绝. 因此, 不分配权限等同于对所有权限设定 `拒绝` 规则. 因此, `拒绝` 规则只需覆盖之前的（同优先级或更低优先级的） `允许` 规则（上面我们就是这么规定的）。 如果您并没有在相同或更低的优先级上设定`允许`规则，您就不需要在这一优先级上设定`拒绝`规则。

***有了页面规则，为什么你还要设计全局权限？***

某些操作不与任何特定路径相关联。例如，创建用户或管理组的能力。全局权限还可以让管理员快速查看用户组可以做什么，而不必查看一堆页面规则来查看是否应用了权限。在不修改任何页面规则的情况下，全局删除对特定操作的访问也更容易。

***我可以定义具有未在全局权限中启用的权限的页面规则吗？***

不行。全局权限始终优先于页面规则。如果未启用全局权限，页面规则将无效。

***如果我希望用户在所有位置都能使用全局权限，我是否还需要定义页面规则？***

是，但只有内容权限需要您这么做。您需要定义至少一个针对相关内容权限的页面规则，并使用`路径开头匹配`规则并配以空白值。


# 用户组

你可以在 **管理区** 点击侧边栏的 **用户组** 选项来管理用户组。

有两个用户组是系统预先定义好的，不能被删除：

- **Administrators**
- **Guests**
{.grid-list}

你可以在用户组列表中通过锁🔒图标认出它们。您只能向 **Administrators** 用户组增加或删除用户，不能修改其它内容。**Guests**用户组只能被拥有管理员权限的用户编辑。


# 用户

你可以在 **管理区** 点击侧边栏的 **用户** 选项来管理用户组。

## 创建新用户

点击 **创建新用户** 按钮以弹出创建用户的对话框。

选择要创建用户的认证服务 **提供者**。当提供者被设为 本地认证 时，你将在数据库
Select the authentication **Provider** to use for the user to be created. When selecting the **Local** authentication provider, you are creating a new user that lives uniquely in the database. For all other providers, a reference to the external service will be kept in the database to identify the user during login.

Fill in the details about the user:

![ui-user-create.png](/assets/ui/ui-user-create.png =450x){.radius-4 .decor-shadow}

**Tip:** You can click the dice icon to automatically generate a strong random password.

> **You must assign the user to at least 1 group.** Otherwise, they will not be able to access anything.
{.is-warning}

Click **Create and Close** to create the user. You can also click **Create** to create another user afterwards.


## Edit User

From the **Users** list, click on the user you want to edit.

Click the **pencil** icon next to the field(s) you want to edit. Click the **Update User** button, located at the top-right corner of the page to apply the modifications.

### Deactivate / Activate User

You can disable access to an account, without deleting it, by deactivating the user account. To do so, click on the **Actions** button and select **Deactivate**. The user will no longer be able to login.

Select **Activate** to enable access again.

### Manually Verify User

If the user was unable to verify their account or didn't receive the verification email, you can manually verify the action by clicking the **Actions** button and select **Set as Verified**.

## Delete User

While it's possible to delete an account, it's not recommended. It's always preferrable to deactivate the user instead.

To delete a user, select the account from the **Users** list, click the **Actions** button and select **Delete**. Confirm that you want to delete the account to proceed.

> Note that the **Guest** account cannot be deleted and some of its fields are locked.
{.is-info}

# Guides

## Private Wiki

To make your wiki completely private and require authentication in order to view any page, simply modify the **Guest** group in the **Administration Area -> Groups** section. Either change the default **Page Rule** from **Allow** to **Deny**, or remove all global permissions on the account. Both methods will result in the same behavior.

## Departments

To give a private space to each department of your company, create a **group** for each.

For each group, add a **Page Rule** with access to **path starting with...** a specific subfolder (e.g. `/accounting`, `/marketing`, etc.).

> Note that you cannot use 2 letters paths. Therefore, paths like `/hr` or `/it` will not work as they are reserved for languages.
{.is-warning}

Starting in Wiki.js **2.5**, you can redirect users directly to their subfolder upon login, instead of the homepage. In earlier versions, you should give read access to the `/home` path (using **Path matches exactly...** match) as this is the landing page for all users upon login.

![](https://a.icons8.com/kkjevabe/OINR8w/svg.svg){.align-abstopright}
