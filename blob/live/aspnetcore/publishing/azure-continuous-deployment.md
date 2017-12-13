---
title: "使用 Visual Studio 和 Git 持续部署到 Azure"
author: rick-anderson
description: "了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure App Service 以实现持续部署。"
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 2707c7a8-2350-4304-9856-fda58e5c0a16
ms.technology: aspnet
ms.prod: asp.net-core
uid: publishing/azure-continuous-deployment
ms.openlocfilehash: f7ea2e76fdee19a3d964e42053f0060a0a505e5b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="continuous-deployment-to-azure-for-aspnet-core-with-visual-studio-and-git"></a><span data-ttu-id="49f57-104">使用 Visual Studio 和 Git 将 ASP.NET Core 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="49f57-104">Continuous deployment to Azure for ASP.NET Core, with Visual Studio and Git</span></span>

<span data-ttu-id="49f57-105">作者：[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="49f57-105">By [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="49f57-106">本教程演示如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用持续部署将其从 Visual Studio 部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="49f57-106">This tutorial shows you how to create an ASP.NET Core web app using Visual Studio and deploy it from Visual Studio to Azure App Service using continuous deployment.</span></span> 

<span data-ttu-id="49f57-107">另请参阅 [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)（使用 VSTS 生成并通过持续部署发布到 Azure Web 应用），其中演示如何使用 Visual Studio Team Services 为 [Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/) 配置持续交付 (CD) 工作流。</span><span class="sxs-lookup"><span data-stu-id="49f57-107">See also [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic), which shows how to configure a continuous delivery (CD) workflow for [Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/) using Visual Studio Team Services.</span></span> <span data-ttu-id="49f57-108">Team Services 中的 Azure 持续交付简化了用于将应用更新发布到 Azure App Service 的可靠部署管道的设置。</span><span class="sxs-lookup"><span data-stu-id="49f57-108">Azure Continuous Delivery in Team Services simplifies setting up a robust deployment pipeline to publish updates for your app to Azure App Service.</span></span> <span data-ttu-id="49f57-109">可以从 Azure 门户配置管道以生成、运行测试、部署到过渡槽，然后部署到生产。</span><span class="sxs-lookup"><span data-stu-id="49f57-109">The pipeline can be configured from the Azure portal to build, run tests, deploy to a staging slot,  and then deploy to production.</span></span>

> [!NOTE]
> <span data-ttu-id="49f57-110">若要完成本教程，需要一个 Microsoft Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="49f57-110">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="49f57-111">如果没有帐户，可[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)或[注册免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="49f57-111">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49f57-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="49f57-112">Prerequisites</span></span>

<span data-ttu-id="49f57-113">本教程假定已经安装以下各组件：</span><span class="sxs-lookup"><span data-stu-id="49f57-113">This tutorial assumes you have already installed the following:</span></span>

* [<span data-ttu-id="49f57-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49f57-114">Visual Studio</span></span>](https://www.visualstudio.com)

* <span data-ttu-id="49f57-115">[ASP.NET Core](https://www.microsoft.com/net/download/core)（运行时和工具）</span><span class="sxs-lookup"><span data-stu-id="49f57-115">[ASP.NET Core](https://www.microsoft.com/net/download/core) (runtime and tooling)</span></span>

* <span data-ttu-id="49f57-116">用于 Windows 的 [Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="49f57-116">[Git](https://git-scm.com/downloads) for Windows</span></span>

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="49f57-117">创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="49f57-117">Create an ASP.NET Core web app</span></span>

1. <span data-ttu-id="49f57-118">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="49f57-118">Start Visual Studio.</span></span>

2. <span data-ttu-id="49f57-119">从“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="49f57-119">From the **File** menu, select **New** > **Project**.</span></span>

3. <span data-ttu-id="49f57-120">选择“ASP.NET Core Web 应用程序”项目模板。</span><span class="sxs-lookup"><span data-stu-id="49f57-120">Select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="49f57-121">它出现在“已安装” > “模板” > “Visual C#” > “.NET Core”下。</span><span class="sxs-lookup"><span data-stu-id="49f57-121">It appears under **Installed** > **Templates** > **Visual C#** > **.NET Core**.</span></span> <span data-ttu-id="49f57-122">将项目命名为 `SampleWebAppDemo`。</span><span class="sxs-lookup"><span data-stu-id="49f57-122">Name the project `SampleWebAppDemo`.</span></span> <span data-ttu-id="49f57-123">选择“创建新 Git 存储库”选项，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="49f57-123">Select the **Create new Git respository** option and click **OK**.</span></span>

   ![“新建项目”对话框](azure-continuous-deployment/_static/01-new-project.png)

4. <span data-ttu-id="49f57-125">在“新建 ASP.NET Core 项目”对话框中，选择 ASP.NET Core 的“空”模板，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="49f57-125">In the **New ASP.NET Core Project** dialog, select the ASP.NET Core **Empty** template, then click **OK**.</span></span>

   ![“新建 ASP.NET 项目”对话框](azure-continuous-deployment/_static/02-web-site-template.png)

>[!NOTE]
    ><span data-ttu-id="49f57-127">.NET Core 的最新版本为 2.0</span><span class="sxs-lookup"><span data-stu-id="49f57-127">Most recent release of .NET Core is 2.0</span></span>

### <a name="running-the-web-app-locally"></a><span data-ttu-id="49f57-128">本地运行 Web 应用</span><span class="sxs-lookup"><span data-stu-id="49f57-128">Running the web app locally</span></span>

1. <span data-ttu-id="49f57-129">Visual Studio 完成创建应用后，请选择“调试” -> “启动调试”以运行该应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-129">Once Visual Studio finishes creating the app, run the app by selecting **Debug** -> **Start Debugging**.</span></span> <span data-ttu-id="49f57-130">作为替代方法，也可以按 F5。</span><span class="sxs-lookup"><span data-stu-id="49f57-130">As an alternative, you can press **F5**.</span></span>

   <span data-ttu-id="49f57-131">可能需要一些时间对 Visual Studio 和新应用进行初始化。</span><span class="sxs-lookup"><span data-stu-id="49f57-131">It may take time to initialize Visual Studio and the new app.</span></span> <span data-ttu-id="49f57-132">完成后，浏览器将显示正在运行的应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-132">Once it is complete, the browser will show the running app.</span></span>

   ![显示正在运行的应用程序（显示“Hello World!”）的浏览器窗口](azure-continuous-deployment/_static/04-browser-runapp.png)

2. <span data-ttu-id="49f57-134">查看完正在运行的 Web 应用后，关闭浏览器，然后单击 Visual Studio 工具栏中的“停止调试”图标以停止应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-134">After reviewing the running Web app, close the browser and click the "Stop Debugging" icon in the toolbar of Visual Studio to stop the app.</span></span>

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="49f57-135">在 Azure 门户中创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="49f57-135">Create a web app in the Azure Portal</span></span>

<span data-ttu-id="49f57-136">以下步骤将演示如何在 Azure 门户中创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-136">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="49f57-137">登录到 [Azure 门户](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="49f57-137">Log in to the [Azure Portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="49f57-138">点击门户左上方的“新建”</span><span class="sxs-lookup"><span data-stu-id="49f57-138">TAP **NEW** at the top left of the Portal</span></span>
3. <span data-ttu-id="49f57-139">点击“Web + 移动” > “Web 应用”</span><span class="sxs-lookup"><span data-stu-id="49f57-139">TAP **Web + Mobile** > **Web App**</span></span>

    ![Microsoft Azure 门户：“新建”按钮：Marketplace 下的“Web + 移动”：“特别推荐的应用”下的“Web 应用”按钮](azure-continuous-deployment/_static/05-azure-newwebapp.png)

4.  <span data-ttu-id="49f57-141">在“Web 应用”边栏选项卡中，输入“应用服务名称”的唯一值。</span><span class="sxs-lookup"><span data-stu-id="49f57-141">In the **Web App** blade, enter a unique value for the **App Service Name**.</span></span>

    ![“Web 应用”边栏选项卡](azure-continuous-deployment/_static/06-azure-newappblade.png)

    >[!NOTE]
    ><span data-ttu-id="49f57-143">“应用服务名称”的名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="49f57-143">The **App Service Name** name needs to be unique.</span></span> <span data-ttu-id="49f57-144">尝试输入名称时，门户将强制执行此规则。</span><span class="sxs-lookup"><span data-stu-id="49f57-144">The portal will enforce this rule when you attempt to enter the name.</span></span> <span data-ttu-id="49f57-145">在输入一个不同的值后，需要为在本教程中每次出现的“SampleWebAppDemo”替换该值。</span><span class="sxs-lookup"><span data-stu-id="49f57-145">After you enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span>

    &nbsp;
    
    <span data-ttu-id="49f57-146">另外，在“Web 应用”边栏选项卡中，选择现有“应用服务计划/位置”或新建一个。</span><span class="sxs-lookup"><span data-stu-id="49f57-146">Also in the **Web App** blade, select an existing **App Service Plan/Location** or create a new one.</span></span> <span data-ttu-id="49f57-147">如果创建新的计划，请选择定价层、位置和其他选项。</span><span class="sxs-lookup"><span data-stu-id="49f57-147">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="49f57-148">有关应用服务计划的详细信息，请参阅 [Azure App Service 计划深入概述](https://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/)。</span><span class="sxs-lookup"><span data-stu-id="49f57-148">For more information on App Service plans, [Azure App Service plans in-depth overview](https://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/).</span></span>

5.  <span data-ttu-id="49f57-149">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="49f57-149">Click **Create**.</span></span> <span data-ttu-id="49f57-150">Azure 将预配并启动 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-150">Azure will provision and start your web app.</span></span>

    ![Azure 门户：示例 Web 应用演示 01 Essentials 边栏选项卡](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="49f57-152">为新 Web 应用启用 Git 发布</span><span class="sxs-lookup"><span data-stu-id="49f57-152">Enable Git publishing for the new web app</span></span>

<span data-ttu-id="49f57-153">Git 是一个分布式版本控制系统，可用来部署 Azure App Service Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-153">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="49f57-154">将为 Web 应用编写的代码将存储到本地 Git 存储库中，并通过推送到远程存储库将代码部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="49f57-154">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>

1. <span data-ttu-id="49f57-155">如果尚未登录，请先登录 [Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="49f57-155">Log into the [Azure Portal](https://portal.azure.com), if you're not already logged in.</span></span>

2. <span data-ttu-id="49f57-156">单击“应用服务”查看与 Azure 订阅关联的应用服务列表。</span><span class="sxs-lookup"><span data-stu-id="49f57-156">Click **App Services** to view a list of the app services associated with your Azure subscription.</span></span>

3. <span data-ttu-id="49f57-157">选择在本教程的前一部分中创建的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-157">Select the web app you created in the previous section of this tutorial.</span></span>

4. <span data-ttu-id="49f57-158">在“部署”边栏选项卡中，选择“部署选项” > “选择源” > “本地 Git 存储库”。</span><span class="sxs-lookup"><span data-stu-id="49f57-158">In the **Deployment** blade, select **Deployment options** > **Choose Source** > **Local Git Repository**.</span></span>

   ![“设置”边栏选项卡：“部署源”边栏选项卡：“选择源”边栏选项卡](azure-continuous-deployment/_static/deployment-options.png)

5. <span data-ttu-id="49f57-160">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="49f57-160">Click **OK**.</span></span>

6. <span data-ttu-id="49f57-161">如果事先未设置部署凭据用于发布 Web 应用或其他应用服务应用，请立即设置：</span><span class="sxs-lookup"><span data-stu-id="49f57-161">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>

   * <span data-ttu-id="49f57-162">单击“设置” > “部署凭据”。</span><span class="sxs-lookup"><span data-stu-id="49f57-162">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="49f57-163">“设置部署凭据”边栏选项卡将显示。</span><span class="sxs-lookup"><span data-stu-id="49f57-163">The **Set deployment credentials** blade will be displayed.</span></span>

   * <span data-ttu-id="49f57-164">创建用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="49f57-164">Create a user name and password.</span></span>  <span data-ttu-id="49f57-165">稍后设置 Git 时需要此密码。</span><span class="sxs-lookup"><span data-stu-id="49f57-165">You'll need this password later when setting up Git.</span></span>

   * <span data-ttu-id="49f57-166">单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="49f57-166">Click **Save**.</span></span>

7. <span data-ttu-id="49f57-167">在“Web 应用”边栏选项卡中，单击“设置” > “属性”。</span><span class="sxs-lookup"><span data-stu-id="49f57-167">In the **Web App** blade, click **Settings** > **Properties**.</span></span> <span data-ttu-id="49f57-168">将部署到的远程 Git 存储库的 URL 会显示在“GIT URL”下。</span><span class="sxs-lookup"><span data-stu-id="49f57-168">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>

8. <span data-ttu-id="49f57-169">复制“GIT URL”的值，稍后将在本教程中用到。</span><span class="sxs-lookup"><span data-stu-id="49f57-169">Copy the **GIT URL** value for later use in the tutorial.</span></span>

   ![Azure 门户：应用程序“属性”边栏选项卡](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="49f57-171">将 Web 应用发布到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="49f57-171">Publish your web app to Azure App Service</span></span>

<span data-ttu-id="49f57-172">在本部分中，将使用 Visual Studio 创建本地 Git 存储库并从该存储库推送到 Azure 以部署 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-172">In this section, you will create a local Git repository using Visual Studio and push from that repository to Azure to deploy your web app.</span></span> <span data-ttu-id="49f57-173">涉及到的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="49f57-173">The steps involved include the following:</span></span>

   * <span data-ttu-id="49f57-174">使用 GIT URL 值添加远程存储库设置，以将本地存储库部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="49f57-174">Add the remote repository setting using your GIT URL value, so you can deploy your local repository to Azure.</span></span>

   * <span data-ttu-id="49f57-175">提交项目更改。</span><span class="sxs-lookup"><span data-stu-id="49f57-175">Commit your project changes.</span></span>

   * <span data-ttu-id="49f57-176">将项目更改从本地存储库推送到 Azure.上的远程存储库。</span><span class="sxs-lookup"><span data-stu-id="49f57-176">Push your project changes from your local repository to your remote repository on Azure.</span></span>

&nbsp;
   
1.  <span data-ttu-id="49f57-177">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="49f57-177">In **Solution Explorer** right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="49f57-178">“团队资源管理器”将显示。</span><span class="sxs-lookup"><span data-stu-id="49f57-178">The **Team Explorer** will be displayed.</span></span>

    ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/10-team-explorer.png)

2.  <span data-ttu-id="49f57-180">在“团队资源管理器”中，选择“主页”（主页图标）>“设置” > “存储库设置”。</span><span class="sxs-lookup"><span data-stu-id="49f57-180">In **Team Explorer**, select the **Home** (home icon) > **Settings** > **Repository Settings**.</span></span>

3.  <span data-ttu-id="49f57-181">在“存储库设置”的“远程”部分中选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="49f57-181">In the **Remotes** section of the **Repository Settings** select **Add**.</span></span> <span data-ttu-id="49f57-182">“添加远程”对话框将显示。</span><span class="sxs-lookup"><span data-stu-id="49f57-182">The **Add Remote** dialog box will be displayed.</span></span>

4.  <span data-ttu-id="49f57-183">将远程的“名称”设置为“Azure-SampleApp”。</span><span class="sxs-lookup"><span data-stu-id="49f57-183">Set the **Name** of the remote to **Azure-SampleApp**.</span></span>

5.  <span data-ttu-id="49f57-184">将“提取”的值设置为在本教程前面部分从 Azure 复制的“Git URL”。</span><span class="sxs-lookup"><span data-stu-id="49f57-184">Set the value for **Fetch** to the **Git URL** that you copied from Azure earlier in this tutorial.</span></span> <span data-ttu-id="49f57-185">请注意，此 URL 是以 .git 结尾的。</span><span class="sxs-lookup"><span data-stu-id="49f57-185">Note that this is the URL that ends with **.git**.</span></span>

    ![“编辑远程”对话框](azure-continuous-deployment/_static/11-add-remote.png)

    >[!NOTE]
    ><span data-ttu-id="49f57-187">作为替代方法，可以通过打开“命令窗口”、更改为项目目录并输入命令从“命令窗口”指定远程存储库。</span><span class="sxs-lookup"><span data-stu-id="49f57-187">As an alternative, you can specify the remote repository from the **Command Window** by opening the **Command Window**, changing to your project directory, and entering the command.</span></span> <span data-ttu-id="49f57-188">例如：`git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`</span><span class="sxs-lookup"><span data-stu-id="49f57-188">For example:`git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`</span></span>

6.  <span data-ttu-id="49f57-189">选择“主页”（主页图标）>“设置” > “全局设置”。</span><span class="sxs-lookup"><span data-stu-id="49f57-189">Select the **Home** (home icon) > **Settings** > **Global Settings**.</span></span> <span data-ttu-id="49f57-190">请确保已设置了姓名和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="49f57-190">Make sure you have your name and your email address set.</span></span> <span data-ttu-id="49f57-191">可能还需要选择“更新”。</span><span class="sxs-lookup"><span data-stu-id="49f57-191">You may also need to select **Update**.</span></span>

7.  <span data-ttu-id="49f57-192">选择“主页” > “更改”以返回到“更改”视图。</span><span class="sxs-lookup"><span data-stu-id="49f57-192">Select **Home** > **Changes** to return to the **Changes** view.</span></span>

8.  <span data-ttu-id="49f57-193">输入提交消息，如“初始推送 #1”，然后单击“提交”。</span><span class="sxs-lookup"><span data-stu-id="49f57-193">Enter a commit message, such as **Initial Push #1** and click **Commit**.</span></span> <span data-ttu-id="49f57-194">此操作将本地创建“提交”。</span><span class="sxs-lookup"><span data-stu-id="49f57-194">This action will create a *commit* locally.</span></span> <span data-ttu-id="49f57-195">接下来，需要与 Azure 进行同步。</span><span class="sxs-lookup"><span data-stu-id="49f57-195">Next, you need to *sync* with Azure.</span></span>

    ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/12-initial-commit.png)

    >[!NOTE]
    ><span data-ttu-id="49f57-197">作为替代方法，可以通过打开“命令窗口”、更改为项目目录并输入 git 命令从“命令窗口”提交更改。</span><span class="sxs-lookup"><span data-stu-id="49f57-197">As an alternative, you can commit your changes from the **Command Window** by opening the **Command Window**, changing to your project directory, and entering the git commands.</span></span> <span data-ttu-id="49f57-198">例如: </span><span class="sxs-lookup"><span data-stu-id="49f57-198">For example:</span></span>
    >
    >`git add .`
    >
    >`git commit -am "Initial Push #1"`

9.  <span data-ttu-id="49f57-199">选择“主页” > “同步” > “操作” > “打开命令提示符”。</span><span class="sxs-lookup"><span data-stu-id="49f57-199">Select **Home** > **Sync** > **Actions** > **Open Command Prompt**.</span></span> <span data-ttu-id="49f57-200">命令提示符将针对项目目录打开。</span><span class="sxs-lookup"><span data-stu-id="49f57-200">The command prompt will open to your project directory.</span></span>

10.  <span data-ttu-id="49f57-201">在命令窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="49f57-201">Enter the following command in the command window:</span></span>

    `git push -u Azure-SampleApp master`

11.  <span data-ttu-id="49f57-202">输入之前在 Azure 中创建的 Azure“部署凭据”密码。</span><span class="sxs-lookup"><span data-stu-id="49f57-202">Enter your Azure **deployment credentials** password that you created earlier in Azure.</span></span>

    >[!NOTE]
    ><span data-ttu-id="49f57-203">输入时密码将不可见。</span><span class="sxs-lookup"><span data-stu-id="49f57-203">Your password will not be visible as you enter it.</span></span>

    <span data-ttu-id="49f57-204">此命令将启动将本地项目文件推送到 Azure 的进程。</span><span class="sxs-lookup"><span data-stu-id="49f57-204">This command will start the process of pushing your local project files to Azure.</span></span> <span data-ttu-id="49f57-205">上述命令的输出以部署成功的消息结尾。</span><span class="sxs-lookup"><span data-stu-id="49f57-205">The output from the above command ends with a message that deployment was successful.</span></span>
        
    ```
    remote: Finished successfully.
    remote: Running post deployment command(s)...
    remote: Deployment successful.
    To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
    * [new branch]      master -> master
    Branch master set up to track remote branch master from Azure-SampleApp.
    ```
    > [!NOTE]
    > <span data-ttu-id="49f57-206">如果需要协作处理项目，则应考虑在推送到 Azure 时推送到 [GitHub](https://github.com)。</span><span class="sxs-lookup"><span data-stu-id="49f57-206">If you need to collaborate on a project, you should consider pushing to [GitHub](https://github.com) in between pushing to Azure.</span></span>
 
### <a name="verify-the-active-deployment"></a><span data-ttu-id="49f57-207">验证活动的部署</span><span class="sxs-lookup"><span data-stu-id="49f57-207">Verify the Active Deployment</span></span>

<span data-ttu-id="49f57-208">可以验证是否已成功将 Web 应用从本地环境传输到了 Azure。</span><span class="sxs-lookup"><span data-stu-id="49f57-208">You can verify that you successfully transferred the web app from your local environment to Azure.</span></span> <span data-ttu-id="49f57-209">你将看到列出的成功部署。</span><span class="sxs-lookup"><span data-stu-id="49f57-209">You'll see the listed successful deployment.</span></span>

1. <span data-ttu-id="49f57-210">在 [Azure 门户](https://portal.azure.com)中，选择 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-210">In the [Azure Portal](https://portal.azure.com), select your web app.</span></span> <span data-ttu-id="49f57-211">然后，选择“部署” > “部署选项”。</span><span class="sxs-lookup"><span data-stu-id="49f57-211">Then, select **Deployment** > **Deployment options**.</span></span>

   ![Azure 门户：“设置”边栏选项卡：显示成功部署的“部署”边栏选项卡](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a><span data-ttu-id="49f57-213">在 Azure 中运行此应用</span><span class="sxs-lookup"><span data-stu-id="49f57-213">Run the app in Azure</span></span>

<span data-ttu-id="49f57-214">在将 Web 应用部署到 Azure 后就可以运行此应用了。</span><span class="sxs-lookup"><span data-stu-id="49f57-214">Now that you have deployed your web app to Azure, you can run the app.</span></span>

<span data-ttu-id="49f57-215">有两种方法可以做到这一点：</span><span class="sxs-lookup"><span data-stu-id="49f57-215">This can be done in two ways:</span></span>

* <span data-ttu-id="49f57-216">在 Azure 门户中，找到 Web 应用的“Web 应用”边栏选项卡，然后单击“浏览”在默认浏览器中查看应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-216">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app in your default browser.</span></span>

* <span data-ttu-id="49f57-217">打开浏览器并输入 Web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="49f57-217">Open a browser and enter the URL for your web app.</span></span> <span data-ttu-id="49f57-218">例如: </span><span class="sxs-lookup"><span data-stu-id="49f57-218">For example:</span></span>

  `http://SampleWebAppDemo.azurewebsites.net`

## <a name="update-your-web-app-and-republish"></a><span data-ttu-id="49f57-219">更新 Web 应用并重新发布</span><span class="sxs-lookup"><span data-stu-id="49f57-219">Update your web app and republish</span></span>

<span data-ttu-id="49f57-220">对本地代码进行更改后，可以重新发布。</span><span class="sxs-lookup"><span data-stu-id="49f57-220">After you make changes to your local code, you can republish.</span></span>

1.  <span data-ttu-id="49f57-221">在 Visual Studio 的“解决方案资源管理器”中，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="49f57-221">In **Solution Explorer** of Visual Studio, open the *Startup.cs* file.</span></span>

2.  <span data-ttu-id="49f57-222">在 `Configure` 方法中，修改 `Response.WriteAsync` 方法，使它显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="49f57-222">In the `Configure` method, modify the `Response.WriteAsync` method so that it appears as follows:</span></span>

    ```aspx-cs
    await context.Response.WriteAsync("Hello World! Deploy to Azure.");
    ```
3.  <span data-ttu-id="49f57-223">将保存更改到 Startup.cs。</span><span class="sxs-lookup"><span data-stu-id="49f57-223">Save changes to *Startup.cs*.</span></span>

4.  <span data-ttu-id="49f57-224">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="49f57-224">In **Solution Explorer**, right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="49f57-225">“团队资源管理器”将显示。</span><span class="sxs-lookup"><span data-stu-id="49f57-225">The **Team Explorer** will be displayed.</span></span>

5.  <span data-ttu-id="49f57-226">输入提交消息，如：</span><span class="sxs-lookup"><span data-stu-id="49f57-226">Enter a commit message, such as:</span></span>

    ```none
    Update #2
    ```

6.  <span data-ttu-id="49f57-227">按“提交”按钮以提交项目更改。</span><span class="sxs-lookup"><span data-stu-id="49f57-227">Press the **Commit** button to commit the project changes.</span></span>

7.  <span data-ttu-id="49f57-228">选择“主页” > “同步” > “操作” > “推送”。</span><span class="sxs-lookup"><span data-stu-id="49f57-228">Select **Home** > **Sync** > **Actions** > **Push**.</span></span>

>[!NOTE]
><span data-ttu-id="49f57-229">作为替代方法，可以通过打开“命令窗口”、更改为项目目录并输入 git 命令从“命令窗口”推送更改。</span><span class="sxs-lookup"><span data-stu-id="49f57-229">As an alternative, you can push your changes from the **Command Window** by opening the **Command Window**, changing to your project directory, and entering a git command.</span></span> <span data-ttu-id="49f57-230">例如: </span><span class="sxs-lookup"><span data-stu-id="49f57-230">For example:</span></span>
>
>`git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a><span data-ttu-id="49f57-231">在 Azure 中查看更新的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="49f57-231">View the updated web app in Azure</span></span>

<span data-ttu-id="49f57-232">通过从 Azure 门户中的“Web 应用”边栏选项卡选择“浏览”，或通过打开浏览器并输入 Web 应用的 URL 以查看更新的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="49f57-232">View your updated web app by selecting **Browse** from the web app blade in the Azure Portal or by opening a browser and entering the URL for your web app.</span></span> <span data-ttu-id="49f57-233">例如: </span><span class="sxs-lookup"><span data-stu-id="49f57-233">For example:</span></span>

   `http://SampleWebAppDemo.azurewebsites.net`

## <a name="additional-resources"></a><span data-ttu-id="49f57-234">其他资源</span><span class="sxs-lookup"><span data-stu-id="49f57-234">Additional Resources</span></span>

* [<span data-ttu-id="49f57-235">发布和部署</span><span class="sxs-lookup"><span data-stu-id="49f57-235">Publishing and Deployment</span></span>](index.md)

* [<span data-ttu-id="49f57-236">项目 Kudu</span><span class="sxs-lookup"><span data-stu-id="49f57-236">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
