---
title: "与 EF 核心-迁移-4 的 8 razor 页"
author: rick-anderson
description: "在本教程中，你启动使用 EF 核心迁移功能来管理的 ASP.NET 核心 MVC 应用程序中的数据模型更改。"
keywords: "ASP.NET Core, Entity Framework Core, 迁移"
ms.author: riande
manager: wpickett
ms.date: 10/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/migrations
ms.openlocfilehash: 8549fc522bcd05a5755a449cd6d4b655f00d998b
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="migrations---ef-core-with-razor-pages-tutorial-4-of-8"></a><span data-ttu-id="2c7ab-104">迁移的 EF 核心 Razor 页教程 (8 的第 4)</span><span class="sxs-lookup"><span data-stu-id="2c7ab-104">Migrations - EF Core with Razor Pages tutorial (4 of 8)</span></span>

<span data-ttu-id="2c7ab-105">通过[Tom Dykstra](https://github.com/tdykstra)， [Jon P Smith](https://twitter.com/thereformedprog)，和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2c7ab-105">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="2c7ab-106">在本教程中，使用 EF 核心迁移功能用于管理数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-106">In this tutorial, the EF Core migrations feature for managing data model changes is used.</span></span>

<span data-ttu-id="2c7ab-107">如果你遇到无法解决的问题，请下载[对此阶段已完成应用程序](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-107">If you run into problems you can't solve, download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="2c7ab-108">当开发新的应用程序时、 数据模型经常更改。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-108">When a new app is developed, the data model changes frequently.</span></span> <span data-ttu-id="2c7ab-109">每次将模型更改，该模型获取与数据库不同步。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-109">Each time the model changes, the model gets out of sync with the database.</span></span> <span data-ttu-id="2c7ab-110">通过配置实体框架可以创建数据库，如果它不存在开始本教程。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-110">This tutorial started by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="2c7ab-111">每个数据模型更改的时间：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-111">Each time the data model changes:</span></span>

* <span data-ttu-id="2c7ab-112">数据库已被删除。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-112">The DB is dropped.</span></span>
* <span data-ttu-id="2c7ab-113">EF 创建一个与型号匹配的新。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-113">EF creates a new one that matches the model.</span></span>
* <span data-ttu-id="2c7ab-114">应用程序设定种子使用测试数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-114">The app seeds the DB with test data.</span></span>

<span data-ttu-id="2c7ab-115">使数据库保持与数据模型同步到此方法适用也直到应用程序部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-115">This approach to keeping the DB in sync with the data model works well until you deploy the app to production.</span></span> <span data-ttu-id="2c7ab-116">当在生产环境中运行应用程序时，它通常将需要维护的数据存储。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-116">When the app is running in production, it is usually storing data that needs to be maintained.</span></span> <span data-ttu-id="2c7ab-117">应用程序无法启动一个测试数据库每次更改 （如添加新列）。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-117">The app can't start with a test DB each time a change is made (such as adding a new column).</span></span> <span data-ttu-id="2c7ab-118">EF 核心迁移功能启用 EF 核心以更新数据库架构，而不是创建新的 DB，从而解决了此问题。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-118">The EF Core Migrations feature solves this problem by enabling EF Core to update the DB schema instead of creating a new DB.</span></span>

<span data-ttu-id="2c7ab-119">而不是删除并重新创建数据库，在数据模型更改时，迁移架构更新，并保留现有数据。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-119">Rather than dropping and recreating the DB when the data model changes, migrations updates the schema and retains existing data.</span></span>

## <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="2c7ab-120">用于进行迁移的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="2c7ab-120">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="2c7ab-121">若要使用迁移，使用**程序包管理器控制台**(PMC) 或命令行界面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-121">To work with migrations, use the **Package Manager Console** (PMC) or the command-line interface (CLI).</span></span> <span data-ttu-id="2c7ab-122">这些教程介绍如何使用 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-122">These tutorials show how to use CLI commands.</span></span> <span data-ttu-id="2c7ab-123">有关 PMC 信息位于[本教程末尾](#pmc)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-123">Information about the PMC is at [the end of this tutorial](#pmc).</span></span>

<span data-ttu-id="2c7ab-124">中提供了命令行界面 (CLI) 的 EF 核心工具[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-124">The EF Core tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="2c7ab-125">若要安装此包，将其添加到`DotNetCliToolReference`中的集合*.csproj*文件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-125">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file, as shown.</span></span> <span data-ttu-id="2c7ab-126">**注意：**必须编辑安装此程序包*.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-126">**Note:** This package must be installed by editing the *.csproj* file.</span></span> <span data-ttu-id="2c7ab-127">`install-package`命令或包管理器 GUI 不能用于安装此包。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-127">The`install-package` command or the package manager GUI cannot be used to install this package.</span></span> <span data-ttu-id="2c7ab-128">编辑*.csproj*通过右键单击中的项目名称的文件**解决方案资源管理器**并选择**编辑 ContosoUniversity.csproj**。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-128">Edit the *.csproj* file by right-clicking the project name in **Solution Explorer** and selecting **Edit ContosoUniversity.csproj**.</span></span>

<span data-ttu-id="2c7ab-129">以下标记显示已更新*.csproj*使用 EF 核心 CLI 工具突出显示的文件：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-129">The following markup shows the updated *.csproj* file with the EF Core CLI tools highlighted:</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
<span data-ttu-id="2c7ab-130">前面的示例中的版本号是当前在撰写本教程时。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-130">The version numbers in the preceding example were current when the tutorial was written.</span></span> <span data-ttu-id="2c7ab-131">为其他包中找到的 EF 核心 CLI 工具中使用相同版本。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-131">Use the same version for the EF Core CLI tools found in the other packages.</span></span>

## <a name="change-the-connection-string"></a><span data-ttu-id="2c7ab-132">更改连接字符串</span><span class="sxs-lookup"><span data-stu-id="2c7ab-132">Change the connection string</span></span>

<span data-ttu-id="2c7ab-133">在*appsettings.json*文件中，将连接字符串中数据库的名称更改为 ContosoUniversity2。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-133">In the *appsettings.json* file, change the name of the DB in the connection string to ContosoUniversity2.</span></span>

[!code-json[Main](intro/samples/cu/appsettings2.json?range=1-4)]

<span data-ttu-id="2c7ab-134">更改连接字符串中的数据库名称，则会导致创建新数据库的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-134">Changing the DB name in the connection string causes the first migration to create a new DB.</span></span> <span data-ttu-id="2c7ab-135">创建新数据库，因为具有该名称不存在。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-135">A new DB is created because one with that name does not exist.</span></span> <span data-ttu-id="2c7ab-136">更改连接字符串不是必需的迁移入门知识。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-136">Changing the connection string isn't required for getting started with migrations.</span></span>

<span data-ttu-id="2c7ab-137">更改数据库名称的替代方法删除数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-137">An alternative to changing the DB name is deleting the DB.</span></span> <span data-ttu-id="2c7ab-138">使用**SQL Server 对象资源管理器**(SSOX) 或`database drop`CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-138">Use **SQL Server Object Explorer** (SSOX) or the `database drop` CLI command:</span></span>

 ```console
 dotnet ef database drop
 ```

<span data-ttu-id="2c7ab-139">以下部分说明如何运行 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-139">The following section explains how to run CLI commands.</span></span>

## <a name="create-an-initial-migration"></a><span data-ttu-id="2c7ab-140">创建初始迁移</span><span class="sxs-lookup"><span data-stu-id="2c7ab-140">Create an initial migration</span></span>

<span data-ttu-id="2c7ab-141">生成项目。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-141">Build the project.</span></span>

<span data-ttu-id="2c7ab-142">打开命令窗口并导航到项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-142">Open a command window and navigate to the project folder.</span></span> <span data-ttu-id="2c7ab-143">项目文件夹包含*Startup.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-143">The project folder contains the *Startup.cs* file.</span></span>

<span data-ttu-id="2c7ab-144">在命令窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-144">Enter the following in the command window:</span></span>

```console
dotnet ef migrations add InitialCreate
```

<span data-ttu-id="2c7ab-145">命令窗口显示类似于以下信息：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-145">The command window displays information similar to the following:</span></span>

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="2c7ab-146">如果迁移失败，出现消息"*无法访问文件...ContosoUniversity.dll 由于另一个进程正在使用。*"</span><span class="sxs-lookup"><span data-stu-id="2c7ab-146">If the migration fails with the message "*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*"</span></span> <span data-ttu-id="2c7ab-147">显示：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-147">is displayed:</span></span>

* <span data-ttu-id="2c7ab-148">停止 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-148">Stop IIS Express.</span></span>

   * <span data-ttu-id="2c7ab-149">退出并重新启动 Visual Studio 中，或</span><span class="sxs-lookup"><span data-stu-id="2c7ab-149">Exit and restart Visual Studio, or</span></span>
   * <span data-ttu-id="2c7ab-150">在 Windows 系统任务栏中找到的 IIS Express 图标。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-150">Find the IIS Express icon in the Windows System Tray.</span></span>
   * <span data-ttu-id="2c7ab-151">右键单击 IIS Express 图标，并依次**ContosoUniversity > 停止站点**。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-151">Right-click the IIS Express icon, and then click **ContosoUniversity > Stop Site**.</span></span>

<span data-ttu-id="2c7ab-152">如果错误消息"生成失败。"</span><span class="sxs-lookup"><span data-stu-id="2c7ab-152">If the error message "Build failed."</span></span> <span data-ttu-id="2c7ab-153">将显示，重新运行该命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-153">is displayed, run the command again.</span></span> <span data-ttu-id="2c7ab-154">如果你收到此错误，将在本教程的底部保留注释。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-154">If you get this error, leave a note at the bottom of this tutorial.</span></span>

### <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="2c7ab-155">检查向上和向下方法</span><span class="sxs-lookup"><span data-stu-id="2c7ab-155">Examine the Up and Down methods</span></span>

<span data-ttu-id="2c7ab-156">EF 核心命令`migrations add`生成代码以创建从 DB。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-156">The EF Core command `migrations add` generated code to create the DB from.</span></span> <span data-ttu-id="2c7ab-157">此迁移代码位于*迁移\<时间戳 > _InitialCreate.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-157">This migrations code is in the *Migrations\<timestamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="2c7ab-158">`Up`方法`InitialCreate`类创建到数据模型的实体集对应的数据库表。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-158">The `Up` method of the `InitialCreate` class creates the DB tables that correspond to the data model entity sets.</span></span> <span data-ttu-id="2c7ab-159">`Down`方法删除它们，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-159">The `Down` method deletes them, as shown in the following example:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

<span data-ttu-id="2c7ab-160">迁移调用`Up`方法以实现迁移的数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-160">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="2c7ab-161">当你输入命令回滚更新，迁移调用`Down`方法。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-161">When you enter a command to roll back the update, migrations calls the `Down` method.</span></span>

<span data-ttu-id="2c7ab-162">前面的代码适用于初始迁移。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-162">The preceding code is for the initial migration.</span></span> <span data-ttu-id="2c7ab-163">该代码时，将创建`migrations add InitialCreate`命令已运行。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-163">That code was created when the `migrations add InitialCreate` command was run.</span></span> <span data-ttu-id="2c7ab-164">迁移 name 参数 (如在示例中的"InitialCreate") 用于文件名称。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-164">The migration name parameter ("InitialCreate" in the example) is used for the file name.</span></span> <span data-ttu-id="2c7ab-165">该迁移的名称可以是任何有效的文件名称。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-165">The migration name can be any valid file name.</span></span> <span data-ttu-id="2c7ab-166">最好选择的单词或短语，总结了中迁移正在进行的内容。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-166">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="2c7ab-167">例如，添加了一个部门表的迁移可能会调用"AddDepartmentTable。"</span><span class="sxs-lookup"><span data-stu-id="2c7ab-167">For example, a migration that added a department table might be called "AddDepartmentTable."</span></span>

<span data-ttu-id="2c7ab-168">如果创建初始迁移和 DB 退出：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-168">If the initial migration is created and the DB exits:</span></span>

* <span data-ttu-id="2c7ab-169">生成数据库创建代码。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-169">The DB creation code is generated.</span></span>
* <span data-ttu-id="2c7ab-170">数据库创建代码不需要运行，因为数据库已与匹配的数据模型。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-170">The DB creation code doesn't need to run because the DB already matches the data model.</span></span> <span data-ttu-id="2c7ab-171">如果运行的 DB 创建代码，它不执行任何更改，因为数据库已与数据模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-171">If the The DB creation code is run, it doesn't make any changes because the DB already matches the data model.</span></span>

<span data-ttu-id="2c7ab-172">应用程序部署到新的环境中，必须运行数据库创建代码以创建数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-172">When the app is deployed to a new environment, the DB creation code must be run to create the DB.</span></span>

<span data-ttu-id="2c7ab-173">以前的连接字符串已更改为使用数据库的新名称。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-173">Previously the connection string was changed to use a new name for the DB.</span></span> <span data-ttu-id="2c7ab-174">指定的数据库不存在，因此迁移创建数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-174">The specified DB doesn't exist, so migrations creates the DB.</span></span>

### <a name="examine-the-data-model-snapshot"></a><span data-ttu-id="2c7ab-175">检查数据模型快照</span><span class="sxs-lookup"><span data-stu-id="2c7ab-175">Examine the data model snapshot</span></span>

<span data-ttu-id="2c7ab-176">迁移创建*快照*中的当前数据库架构的*Migrations/SchoolContextModelSnapshot.cs*:</span><span class="sxs-lookup"><span data-stu-id="2c7ab-176">Migrations creates a *snapshot* of the current DB schema in *Migrations/SchoolContextModelSnapshot.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot1.cs?name=snippet_Truncate)]

<span data-ttu-id="2c7ab-177">以代码表示为当前的数据库架构，因为 EF 核心没有与创建迁移的数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-177">Because the current DB schema is represented in code, EF Core doesn't have to interact with the DB to create migrations.</span></span> <span data-ttu-id="2c7ab-178">当添加迁移时，EF 核心确定通过比较快照文件的数据模型更改的内容。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-178">When you add a migration, EF Core determines what changed by comparing the data model to the snapshot file.</span></span> <span data-ttu-id="2c7ab-179">仅当有更新数据库时，EF 核心与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-179">EF Core interacts with the DB only when it has to update the DB.</span></span>

<span data-ttu-id="2c7ab-180">快照文件必须与创建它的迁移同步。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-180">The snapshot file must be in sync with the migrations that created it.</span></span> <span data-ttu-id="2c7ab-181">无法通过删除名为的文件中删除迁移*\<时间戳 > _\<migrationname >.cs*。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-181">A migration can't be removed by deleting the file named *\<timestamp>_\<migrationname>.cs*.</span></span> <span data-ttu-id="2c7ab-182">如果删除该文件时，将剩余的迁移将与数据库快照文件不同步。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-182">If that file is deleted, the remaining migrations are out of sync with the DB snapshot file.</span></span> <span data-ttu-id="2c7ab-183">若要删除上次添加的迁移，使用[dotnet ef 迁移删除](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove)命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-183">To delete the last migration added, use the [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) command.</span></span>

## <a name="remove-ensurecreated"></a><span data-ttu-id="2c7ab-184">删除 EnsureCreated</span><span class="sxs-lookup"><span data-stu-id="2c7ab-184">Remove EnsureCreated</span></span>

<span data-ttu-id="2c7ab-185">对于早期的开发，`EnsureCreated`命令未使用。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-185">For early development, the `EnsureCreated` command was used.</span></span> <span data-ttu-id="2c7ab-186">在本教程中，使用迁移。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-186">In this tutorial, migrations is used.</span></span> <span data-ttu-id="2c7ab-187">`EnsureCreated`具有以下 limatitions:</span><span class="sxs-lookup"><span data-stu-id="2c7ab-187">`EnsureCreated` has the following limatitions:</span></span>

* <span data-ttu-id="2c7ab-188">绕过迁移并创建数据库和架构。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-188">Bypasses migrations and creates the DB and schema.</span></span>
* <span data-ttu-id="2c7ab-189">不会创建迁移表。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-189">Does not create a migrations table.</span></span>
* <span data-ttu-id="2c7ab-190">可以*不*迁移与一起使用。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-190">Can *not* be used with migrations.</span></span>
* <span data-ttu-id="2c7ab-191">专为测试或快速原型制作，其中数据库是删除并重新创建频繁。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-191">Is designed for testing or rapid prototyping where the DB is dropped and re-created frequently.</span></span>

<span data-ttu-id="2c7ab-192">删除以下行从`DbInitializer`:</span><span class="sxs-lookup"><span data-stu-id="2c7ab-192">Remove the following line from `DbInitializer`:</span></span>

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a><span data-ttu-id="2c7ab-193">适用于在开发过程中数据库的迁移</span><span class="sxs-lookup"><span data-stu-id="2c7ab-193">Apply the migration to the DB in development</span></span>

<span data-ttu-id="2c7ab-194">在命令窗口中，输入以下命令以创建数据库和表。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-194">In the command window, enter the following to create the DB and tables.</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="2c7ab-195">注意： 如果`update`命令将返回"生成失败"。 错误：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-195">Note: If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="2c7ab-196">再次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-196">Run the command again.</span></span>
* <span data-ttu-id="2c7ab-197">如果再次失败，退出 Visual Studio，然后运行`update`命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-197">If it fails again, exit Visual Studio and then run the `update` command.</span></span>
* <span data-ttu-id="2c7ab-198">将保留在页面底部的消息。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-198">Leave a message at the bottom of the page.</span></span>

<span data-ttu-id="2c7ab-199">该命令的输出是类似于`migrations add`命令输出。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-199">The output from the command is similar to the `migrations add` command output.</span></span> <span data-ttu-id="2c7ab-200">在上述命令中，显示的 SQL 命令的设置数据库的日志。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-200">In the preceding command, logs for the SQL commands that set up the DB are displayed.</span></span> <span data-ttu-id="2c7ab-201">在下面的示例输出中，大部分日志被省略：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-201">Most of the logs are omitted in the following sample output:</span></span>

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

<span data-ttu-id="2c7ab-202">若要减少的日志消息中的详细信息级别可以更改中的日志级别*appsettings。Development.json*文件。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-202">To reduce the level of detail in log messages, can change the log levels in the *appsettings.Development.json* file.</span></span> <span data-ttu-id="2c7ab-203">有关详细信息，请参阅[简介日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-203">For more information, see [Introduction to logging](xref:fundamentals/logging/index).</span></span>

<span data-ttu-id="2c7ab-204">使用**SQL Server 对象资源管理器**检查数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-204">Use **SQL Server Object Explorer** to inspect the DB.</span></span> <span data-ttu-id="2c7ab-205">请注意添加`__EFMigrationsHistory`表。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-205">Notice the addition of an `__EFMigrationsHistory` table.</span></span> <span data-ttu-id="2c7ab-206">`__EFMigrationsHistory`表将跟踪的哪些迁移已应用于数据库。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-206">The `__EFMigrationsHistory` table keeps track of which migrations have been applied to the DB.</span></span> <span data-ttu-id="2c7ab-207">查看中的数据`__EFMigrationsHistory`表，它显示为第一次迁移一个行。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-207">View the data in the `__EFMigrationsHistory` table, it shows one row for the first migration.</span></span> <span data-ttu-id="2c7ab-208">在 CLI 输出上例中的最后一个日志显示创建此行的 INSERT 语句。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-208">The last log in the preceding CLI output example shows the INSERT statement that creates this row.</span></span>

<span data-ttu-id="2c7ab-209">运行应用程序并验证一切就绪。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-209">Run the app and verify that everything works.</span></span>

## <a name="appling-migrations-in-production"></a><span data-ttu-id="2c7ab-210">在生产环境中的 appling 迁移</span><span class="sxs-lookup"><span data-stu-id="2c7ab-210">Appling migrations in production</span></span>

<span data-ttu-id="2c7ab-211">我们建议生产应用程序应**不**调用[Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)在应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-211">We recommend production apps should **not** call [Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) at application startup.</span></span> <span data-ttu-id="2c7ab-212">`Migrate`不应从服务器场中的应用程序调用。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-212">`Migrate` should not be called from an app in server farm.</span></span> <span data-ttu-id="2c7ab-213">例如，如果应用已部署，向外扩展 （应用程序的多个实例正在运行） 的云。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-213">For example, if the app has been cloud deployed with scale-out (multiple instances of the app are running).</span></span>

<span data-ttu-id="2c7ab-214">应作为的一部分，部署，且以可控方式完成数据库迁移。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-214">Database migration should be done as part of deployment, and in a controlled way.</span></span> <span data-ttu-id="2c7ab-215">生产数据库迁移方法包括：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-215">Production database migration approaches include:</span></span>

* <span data-ttu-id="2c7ab-216">使用迁移来创建 SQL 脚本，并在部署中使用的 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-216">Using migrations to create SQL scripts and using the SQL scripts in deployment.</span></span>
* <span data-ttu-id="2c7ab-217">运行`dotnet ef database update`从受控的环境。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-217">Running `dotnet ef database update` from a controlled environment.</span></span>

<span data-ttu-id="2c7ab-218">EF 核心使用`__MigrationsHistory`表以查看任何迁移需要运行。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-218">EF Core uses the `__MigrationsHistory` table to see if any migrations need to run.</span></span> <span data-ttu-id="2c7ab-219">如果数据库是最新，则运行无需迁移。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-219">If the DB is up to date, no migration is run.</span></span>

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a><span data-ttu-id="2c7ab-220">命令行界面 (CLI) vs。程序包管理器控制台 (PMC)</span><span class="sxs-lookup"><span data-stu-id="2c7ab-220">Command-line interface (CLI) vs. Package Manager Console (PMC)</span></span>

<span data-ttu-id="2c7ab-221">EF 核心工具，用于管理迁移是从可用：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-221">The EF Core tooling for managing migrations is available from:</span></span>

* <span data-ttu-id="2c7ab-222">.NET 核心 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-222">.NET Core CLI commands.</span></span>
* <span data-ttu-id="2c7ab-223">在 Visual Studio 的 PowerShell cmdlet**程序包管理器控制台**(PMC) 窗口。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-223">The PowerShell cmdlets in the Visual Studio **Package Manager Console** (PMC) window.</span></span>

<span data-ttu-id="2c7ab-224">本教程演示如何使用 CLI，一些开发人员喜欢使用 PMC。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-224">This tutorial shows how to use the CLI, some developers prefer using the PMC.</span></span>

<span data-ttu-id="2c7ab-225">PMC 的 EF 核心命令处于[Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools)包。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-225">The EF Core commands for the PMC are in the [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) package.</span></span> <span data-ttu-id="2c7ab-226">此包包含在[Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage，因此你不必安装它。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-226">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="2c7ab-227">**重要说明：**这不的是通过编辑的 cli 安装与相同的包*.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-227">**Important:** This is not the same package as the one you install for the CLI by editing the *.csproj* file.</span></span> <span data-ttu-id="2c7ab-228">此名称以结尾`Tools`，与中结束的 CLI 包名称不同`Tools.DotNet`。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-228">The name of this one ends in `Tools`, unlike the CLI package name which ends in `Tools.DotNet`.</span></span>

<span data-ttu-id="2c7ab-229">有关 CLI 命令的详细信息，请参阅[.NET 核心 CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-229">For more information about the CLI commands, see [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="2c7ab-230">有关 PMC 命令的详细信息，请参阅[Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-230">For more information about the PMC commands, see [Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c7ab-231">疑难解答</span><span class="sxs-lookup"><span data-stu-id="2c7ab-231">Troubleshooting</span></span>

<span data-ttu-id="2c7ab-232">下载[对此阶段已完成应用程序](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-232">Download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="2c7ab-233">应用程序生成以下异常：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-233">The app generates the following exception:</span></span>

```text
`SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

<span data-ttu-id="2c7ab-234">解决方案： 运行`dotnet ef database update`</span><span class="sxs-lookup"><span data-stu-id="2c7ab-234">Solution: Run `dotnet ef database update`</span></span>

<span data-ttu-id="2c7ab-235">如果`update`命令将返回"生成失败"。 错误：</span><span class="sxs-lookup"><span data-stu-id="2c7ab-235">If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="2c7ab-236">再次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-236">Run the command again.</span></span>
* <span data-ttu-id="2c7ab-237">将保留在页面底部的消息。</span><span class="sxs-lookup"><span data-stu-id="2c7ab-237">Leave a message at the bottom of the page.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2c7ab-238">[上一页](xref:data/ef-rp/sort-filter-page)
[下一页](xref:data/ef-rp/complex-data-model)</span><span class="sxs-lookup"><span data-stu-id="2c7ab-238">[Previous](xref:data/ef-rp/sort-filter-page)
[Next](xref:data/ef-rp/complex-data-model)</span></span>
