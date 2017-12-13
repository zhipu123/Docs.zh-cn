---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: "将应用发布到 Azure 的 Azure App Service |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: 08994815cb339800619caacdcb8d717e9986f9d5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="9e6db-102">将应用发布到 Azure 的 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9e6db-102">Publish the App to Azure Azure App Service</span></span>
====================
<span data-ttu-id="9e6db-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9e6db-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9e6db-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="9e6db-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="9e6db-105">作为最后一步中，将发布到 Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e6db-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="9e6db-106">在解决方案资源管理器，右键单击该项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="9e6db-107">单击**发布**时，将调用**发布 Web**对话框。</span><span class="sxs-lookup"><span data-stu-id="9e6db-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="9e6db-108">如果你选中**云中的主机**当你首次创建项目，然后连接并已配置设置。</span><span class="sxs-lookup"><span data-stu-id="9e6db-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="9e6db-109">在这种情况下，只需单击**设置**选项卡上，并检查&quot;执行 Code First 迁移&quot;。</span><span class="sxs-lookup"><span data-stu-id="9e6db-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="9e6db-110">(如果未检查**云中的主机**开头，然后按照中的步骤[下一节](#new-website)。)</span><span class="sxs-lookup"><span data-stu-id="9e6db-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="9e6db-111">若要将应用部署，请单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="9e6db-112">你可以查看中的发布进度**Web 发布活动**窗口。</span><span class="sxs-lookup"><span data-stu-id="9e6db-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="9e6db-113">(从**视图**菜单上，选择**其他窗口**，然后选择**Web 发布活动**。)</span><span class="sxs-lookup"><span data-stu-id="9e6db-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="9e6db-114">当 Visual Studio 完成部署应用程序时，默认浏览器将自动打开到已部署网站的 URL，且你创建的应用程序现在运行在云中。</span><span class="sxs-lookup"><span data-stu-id="9e6db-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="9e6db-115">浏览器地址栏中的 URL 显示正在从 Internet 加载该站点。</span><span class="sxs-lookup"><span data-stu-id="9e6db-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="9e6db-116">将部署到新网站</span><span class="sxs-lookup"><span data-stu-id="9e6db-116">Deploying to a New Website</span></span>

<span data-ttu-id="9e6db-117">如果你没有检查**云中的主机**时首先创建项目时，你可以立即配置新的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e6db-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="9e6db-118">在解决方案资源管理器，右键单击该项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="9e6db-119">选择**配置文件**选项卡，单击**Microsoft Azure 网站**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="9e6db-120">如果当前未登录到 Azure，将提示您登录。</span><span class="sxs-lookup"><span data-stu-id="9e6db-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="9e6db-121">在**现有网站**对话框中，单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="9e6db-122">输入站点名称。</span><span class="sxs-lookup"><span data-stu-id="9e6db-122">Enter a site name.</span></span> <span data-ttu-id="9e6db-123">选择你的 Azure 订阅和区域。</span><span class="sxs-lookup"><span data-stu-id="9e6db-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="9e6db-124">下**数据库服务器**，选择**创建新服务器**，或选择现有的服务器。</span><span class="sxs-lookup"><span data-stu-id="9e6db-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="9e6db-125">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="9e6db-126">单击**设置**选项卡上，并检查&quot;执行 Code First 迁移&quot;。</span><span class="sxs-lookup"><span data-stu-id="9e6db-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="9e6db-127">然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="9e6db-127">Then click **Publish**.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="9e6db-128">上一篇</span><span class="sxs-lookup"><span data-stu-id="9e6db-128">Previous</span></span>](part-9.md)
