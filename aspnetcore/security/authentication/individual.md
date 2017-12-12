---
title: "基于使用单个用户帐户创建的项目的文章"
author: rick-anderson
description: "本文档列出了一些文章基于使用单个用户帐户创建的项目。"
keywords: "ASP.NET 核心，授权，IAuthorizationService"
ms.author: riande
manager: wpickett
ms.date: 11/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/individual
ms.openlocfilehash: 1864625e0ad6b4ec6fc2ada3fa7d93edec91b633
ms.sourcegitcommit: 037d3900f739dbaa2ba14158e3d7dc81478952ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="articles-based-on-projects-created-with-individual-user-accounts"></a><span data-ttu-id="2d883-104">基于使用单个用户帐户创建的项目的文章</span><span class="sxs-lookup"><span data-stu-id="2d883-104">Articles based on projects created with individual user accounts</span></span>

<span data-ttu-id="2d883-105">ASP.NET 核心标识包含在 Visual Studio 中使用"单个用户帐户"选项的项目模板中。</span><span class="sxs-lookup"><span data-stu-id="2d883-105">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="2d883-106">中使用的.NET 核心 CLI 中可用的身份验证模板`-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="2d883-106">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new razor -au Individual
```

<span data-ttu-id="2d883-107">以下文章演示了如何使用 ASP.NET Core 使用单个用户帐户的模板中生成的代码：</span><span class="sxs-lookup"><span data-stu-id="2d883-107">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="2d883-108">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="2d883-108">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="2d883-109">ASP.NET Core 中的帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="2d883-109">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="2d883-110">使用受授权的用户数据创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="2d883-110">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)