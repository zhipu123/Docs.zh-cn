---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: "迭代 #1 – 创建应用程序 (VB) |Microsoft 文档"
author: microsoft
description: "在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和 D...."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 11d3d4f174207f5370849fdf4517f272b4b6bc6b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="iteration-1--create-the-application-vb"></a><span data-ttu-id="07863-104">迭代 #1 – 创建应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="07863-104">Iteration #1 – Create the Application (VB)</span></span>
====================
<span data-ttu-id="07863-105">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="07863-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="07863-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="07863-106">Download Code</span></span>](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> <span data-ttu-id="07863-107">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="07863-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="07863-108">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="07863-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="07863-109">生成联系人管理 ASP.NET MVC 应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="07863-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="07863-110">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="07863-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="07863-111">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="07863-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="07863-112">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="07863-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="07863-114">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="07863-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="07863-115">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="07863-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="07863-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="07863-117">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="07863-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="07863-118">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="07863-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="07863-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="07863-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="07863-120">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="07863-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="07863-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="07863-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="07863-122">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="07863-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="07863-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="07863-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="07863-124">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="07863-125">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="07863-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="07863-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="07863-127">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="07863-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="07863-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="07863-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="07863-129">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="07863-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="07863-130">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="07863-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="07863-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="07863-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="07863-132">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="07863-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="07863-133">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="07863-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="07863-134">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="07863-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="07863-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="07863-135">This Iteration</span></span>

<span data-ttu-id="07863-136">在此第一次迭代中，我们生成的基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="07863-137">目标是中的最快和最简单的方法可能生成联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="07863-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="07863-138">在更高版本迭代中，我们改进应用程序的设计。</span><span class="sxs-lookup"><span data-stu-id="07863-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="07863-139">联系人管理器应用程序是一个基本的数据库驱动应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="07863-140">应用程序可用于创建新的联系人、 编辑现有联系人和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="07863-141">在此迭代中，我们将完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="07863-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="07863-142">ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="07863-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="07863-143">创建一个数据库来存储我们联系人</span><span class="sxs-lookup"><span data-stu-id="07863-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="07863-144">生成用于我们的 Microsoft 实体框架的数据库的模型类</span><span class="sxs-lookup"><span data-stu-id="07863-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="07863-145">创建控制器操作和视图，以使我们以列出所有数据库中的联系人</span><span class="sxs-lookup"><span data-stu-id="07863-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="07863-146">创建控制器操作和使我们能够在数据库中创建新联系人的视图</span><span class="sxs-lookup"><span data-stu-id="07863-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="07863-147">创建控制器操作和使我们能够编辑现有联系人数据库中的视图</span><span class="sxs-lookup"><span data-stu-id="07863-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="07863-148">创建控制器操作和使我们能够删除现有联系人数据库中的视图</span><span class="sxs-lookup"><span data-stu-id="07863-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="07863-149">软件必备项</span><span class="sxs-lookup"><span data-stu-id="07863-149">Software Prerequisites</span></span>

<span data-ttu-id="07863-150">在 ASP.NET MVC 应用程序，你必须具有 Visual Studio 2008 或 （Visual Web Developer 是不包括所有 Visual Studio 的高级功能的 Visual Studio 的免费版本） 在计算机上安装的 Visual Web Developer 2008。</span><span class="sxs-lookup"><span data-stu-id="07863-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="07863-151">你可以从以下地址下载 Visual Studio 2008 试用版，或者 Visual Web Developer 中：</span><span class="sxs-lookup"><span data-stu-id="07863-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[<span data-ttu-id="07863-152">https://www.asp.net/downloads/essential/</span><span class="sxs-lookup"><span data-stu-id="07863-152">https://www.asp.net/downloads/essential/</span></span>](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="07863-153">对于使用 Visual Web Developer 的 ASP.NET MVC 应用程序，你必须安装的 Visual Web Developer Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="07863-153">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="07863-154">不带 Service Pack 1，无法创建 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="07863-154">Without Service Pack 1, you cannot create Web Application Projects.</span></span>


<span data-ttu-id="07863-155">ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="07863-155">ASP.NET MVC framework.</span></span> <span data-ttu-id="07863-156">你可以从以下地址下载 ASP.NET MVC framework:</span><span class="sxs-lookup"><span data-stu-id="07863-156">You can download the ASP.NET MVC framework from the following address:</span></span>

[<span data-ttu-id="07863-157">https://www.asp.net/mvc</span><span class="sxs-lookup"><span data-stu-id="07863-157">https://www.asp.net/mvc</span></span>](../../../index.md)

<span data-ttu-id="07863-158">在本教程中，我们可以使用 Microsoft 实体框架访问数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-158">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="07863-159">实体框架将包含在.NET Framework 3.5 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="07863-159">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="07863-160">你可以从以下位置下载此 service pack:</span><span class="sxs-lookup"><span data-stu-id="07863-160">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="07863-161">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;-4a83-b309-53b7b77edf78&displaylang = en</span><span class="sxs-lookup"><span data-stu-id="07863-161">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="07863-162">作为执行每个这些下载逐个的替代方法，可以利用 Web 平台安装程序 (Web PI)。</span><span class="sxs-lookup"><span data-stu-id="07863-162">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="07863-163">你可以从以下地址下载 Web PI:</span><span class="sxs-lookup"><span data-stu-id="07863-163">You can download the Web PI from the following address:</span></span>

[<span data-ttu-id="07863-164">https://www.asp.net/downloads/essential/</span><span class="sxs-lookup"><span data-stu-id="07863-164">https://www.asp.net/downloads/essential/</span></span>](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="07863-165">ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="07863-165">ASP.NET MVC Project</span></span>

<span data-ttu-id="07863-166">ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="07863-166">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="07863-167">启动 Visual Studio，然后选择菜单选项**文件、 新项目**。</span><span class="sxs-lookup"><span data-stu-id="07863-167">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="07863-168">**新项目**对话框 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="07863-168">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="07863-169">选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="07863-169">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="07863-170">命名新项目*ContactManager* ，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="07863-170">Name your new project *ContactManager* and click the OK button.</span></span>


<span data-ttu-id="07863-171">请确保你具有从顶部的下拉列表中选择的.NET Framework 3.5 角**新项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="07863-171">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="07863-172">否则，将出现获胜 t 的 ASP.NET MVC Web 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="07863-172">Otherwise, the ASP.NET MVC Web Application template won t appear.</span></span>


<span data-ttu-id="07863-173">[![新项目对话框](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="07863-173">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span></span>

<span data-ttu-id="07863-174">**图 01**: 的新项目对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="07863-174">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-vb/_static/image2.png))</span></span>


<span data-ttu-id="07863-175">ASP.NET MVC 应用程序，**创建单元测试项目**此时将显示对话框。</span><span class="sxs-lookup"><span data-stu-id="07863-175">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="07863-176">可以使用此对话框以指示你想要创建并将单元测试项目添加到你的解决方案创建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-176">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="07863-177">虽然我们获胜 t 会生成此迭代中的单元测试，则应选择选项**是，创建单元测试项目**由于我们计划在后续迭代中添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="07863-177">Although we won t be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="07863-178">首次创建新的 ASP.NET MVC 项目中添加的测试项目是比创建 ASP.NET MVC 项目后添加的测试项目容易得多。</span><span class="sxs-lookup"><span data-stu-id="07863-178">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="07863-179">因为 Visual Web Developer 不支持测试项目，则无法获得创建单元测试项目对话框，使用 Visual Web Developer 时。</span><span class="sxs-lookup"><span data-stu-id="07863-179">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>


<span data-ttu-id="07863-180">[![新项目对话框](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="07863-180">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span></span>

<span data-ttu-id="07863-181">**图 02**: 创建单元测试项目对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="07863-181">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image4.png))</span></span>


<span data-ttu-id="07863-182">Visual Studio 解决方案资源管理器窗口中显示的 ASP.NET MVC 应用程序 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="07863-182">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="07863-183">如果 don t 看到解决方案资源管理器窗口，然后通过选择菜单选项可打开此窗口**视图、 解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="07863-183">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="07863-184">请注意，该解决方案包含两个项目： ASP.NET MVC 项目和测试项目。</span><span class="sxs-lookup"><span data-stu-id="07863-184">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="07863-185">ASP.NET MVC 项目命名为 ContactManager 和测试项目命名为 ContactManager.Tests。</span><span class="sxs-lookup"><span data-stu-id="07863-185">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>


<span data-ttu-id="07863-186">[![新项目对话框](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="07863-186">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span></span>

<span data-ttu-id="07863-187">**图 03**: 解决方案资源管理器窗口 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="07863-187">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image6.png))</span></span>


## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="07863-188">删除项目示例文件</span><span class="sxs-lookup"><span data-stu-id="07863-188">Deleting the Project Sample Files</span></span>

<span data-ttu-id="07863-189">ASP.NET MVC 项目模板包括用于控制器和视图的示例文件。</span><span class="sxs-lookup"><span data-stu-id="07863-189">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="07863-190">在创建新的 ASP.NET MVC 应用程序之前, 应删除这些文件。</span><span class="sxs-lookup"><span data-stu-id="07863-190">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="07863-191">你可以通过右键单击文件或文件夹并选择菜单选项删除文件和文件夹在解决方案资源管理器窗口中的**删除**。</span><span class="sxs-lookup"><span data-stu-id="07863-191">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="07863-192">你需要从 ASP.NET MVC 项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="07863-192">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="07863-193">\Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="07863-193">\Controllers\HomeController.vb</span></span>

- <span data-ttu-id="07863-194">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="07863-194">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="07863-195">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="07863-195">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="07863-196">而且，你需要从测试项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="07863-196">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="07863-197">\Controllers\HomeControllerTest.vb</span><span class="sxs-lookup"><span data-stu-id="07863-197">\Controllers\HomeControllerTest.vb</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="07863-198">创建数据库</span><span class="sxs-lookup"><span data-stu-id="07863-198">Creating the Database</span></span>

<span data-ttu-id="07863-199">联系人管理器应用程序是一个数据库驱动的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-199">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="07863-200">我们使用数据库来存储的联系信息。</span><span class="sxs-lookup"><span data-stu-id="07863-200">We use a database to store the contact information.</span></span>

<span data-ttu-id="07863-201">与任何现代的数据库，包括 Microsoft SQL Server、 Oracle、 MySQL 和 IBM DB2 数据库的 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="07863-201">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="07863-202">在本教程中，我们使用 Microsoft SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-202">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="07863-203">在安装 Visual Studio 时，将向你提供的安装 Microsoft SQL Server Express，是免费版的 Microsoft SQL Server 数据库的选项。</span><span class="sxs-lookup"><span data-stu-id="07863-203">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="07863-204">通过右键单击应用程序创建新数据库\_在解决方案资源管理器窗口并选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="07863-204">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="07863-205">在**添加新项**对话框中，选择**数据**类别和**SQL Server 数据库**模板 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="07863-205">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="07863-206">将新数据库 ContactManagerDB.mdf，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="07863-206">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>


<span data-ttu-id="07863-207">[![新项目对话框](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="07863-207">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span></span>

<span data-ttu-id="07863-208">**图 04**： 创建新的 Microsoft SQL Server Express 数据库 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="07863-208">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image8.png))</span></span>


<span data-ttu-id="07863-209">创建新的数据库后，数据库将出现在应用程序\_在解决方案资源管理器窗口中的数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="07863-209">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="07863-210">双击 ContactManager.mdf 文件以打开服务器资源管理器窗口，然后连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-210">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="07863-211">服务器资源管理器窗口调用在 Microsoft Visual Web Developer 的情况下的数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="07863-211">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>


<span data-ttu-id="07863-212">服务器资源管理器窗口可用于创建新的数据库对象，如数据库表、 视图、 触发器和存储的过程。</span><span class="sxs-lookup"><span data-stu-id="07863-212">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="07863-213">右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="07863-213">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="07863-214">此数据库表设计器显示 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="07863-214">The Database Table Designer appears (see Figure 5).</span></span>


<span data-ttu-id="07863-215">[![新项目对话框](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="07863-215">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span></span>

<span data-ttu-id="07863-216">**图 05**： 数据库表设计器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="07863-216">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image10.png))</span></span>


<span data-ttu-id="07863-217">我们需要创建包含以下各列的表：</span><span class="sxs-lookup"><span data-stu-id="07863-217">We need to create a table that contains the following columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="07863-218">**列名称**</span><span class="sxs-lookup"><span data-stu-id="07863-218">**Column Name**</span></span> | <span data-ttu-id="07863-219">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="07863-219">**Data Type**</span></span> | <span data-ttu-id="07863-220">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="07863-220">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="07863-221">Id</span><span class="sxs-lookup"><span data-stu-id="07863-221">Id</span></span> | <span data-ttu-id="07863-222">int</span><span class="sxs-lookup"><span data-stu-id="07863-222">int</span></span> | <span data-ttu-id="07863-223">false</span><span class="sxs-lookup"><span data-stu-id="07863-223">false</span></span> |
| <span data-ttu-id="07863-224">FirstName</span><span class="sxs-lookup"><span data-stu-id="07863-224">FirstName</span></span> | <span data-ttu-id="07863-225">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="07863-225">nvarchar(50)</span></span> | <span data-ttu-id="07863-226">false</span><span class="sxs-lookup"><span data-stu-id="07863-226">false</span></span> |
| <span data-ttu-id="07863-227">LastName</span><span class="sxs-lookup"><span data-stu-id="07863-227">LastName</span></span> | <span data-ttu-id="07863-228">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="07863-228">nvarchar(50)</span></span> | <span data-ttu-id="07863-229">false</span><span class="sxs-lookup"><span data-stu-id="07863-229">false</span></span> |
| <span data-ttu-id="07863-230">电话</span><span class="sxs-lookup"><span data-stu-id="07863-230">Phone</span></span> | <span data-ttu-id="07863-231">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="07863-231">nvarchar(50)</span></span> | <span data-ttu-id="07863-232">false</span><span class="sxs-lookup"><span data-stu-id="07863-232">false</span></span> |
| <span data-ttu-id="07863-233">电子邮件</span><span class="sxs-lookup"><span data-stu-id="07863-233">Email</span></span> | <span data-ttu-id="07863-234">nvarchar （255)</span><span class="sxs-lookup"><span data-stu-id="07863-234">nvarchar(255)</span></span> | <span data-ttu-id="07863-235">false</span><span class="sxs-lookup"><span data-stu-id="07863-235">false</span></span> |


<span data-ttu-id="07863-236">第一列，Id 列中，是非常特殊。</span><span class="sxs-lookup"><span data-stu-id="07863-236">The first column, the Id column, is special.</span></span> <span data-ttu-id="07863-237">你需要将 Id 列标记为标识列和主键列。</span><span class="sxs-lookup"><span data-stu-id="07863-237">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="07863-238">指示列是标识列，通过展开列属性 （查找底部的图 6） 和滚动到标识规范属性。</span><span class="sxs-lookup"><span data-stu-id="07863-238">You indicate that a column is an Identity column by expanding Column Properites (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="07863-239">设置**（是标识）**属性值**是**。</span><span class="sxs-lookup"><span data-stu-id="07863-239">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="07863-240">通过选择列并单击带有密钥的图标的按钮可将列标记为主键列中。</span><span class="sxs-lookup"><span data-stu-id="07863-240">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="07863-241">某列被标记为主键列后，列旁边将显示一个图标的密钥 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="07863-241">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="07863-242">完成创建表后，单击保存按钮 （带有软盘图标的按钮） 以保存新的表。</span><span class="sxs-lookup"><span data-stu-id="07863-242">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="07863-243">将新表命名*联系人*。</span><span class="sxs-lookup"><span data-stu-id="07863-243">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="07863-244">后创建的联系人数据库表的完成，应将某些记录添加到表中。</span><span class="sxs-lookup"><span data-stu-id="07863-244">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="07863-245">右键单击服务器资源管理器窗口中的联系人表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="07863-245">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="07863-246">在出现的网格中输入一个或多个联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-246">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="07863-247">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="07863-247">Creating the Data Model</span></span>

<span data-ttu-id="07863-248">ASP.NET MVC 应用程序包含模型、 视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-248">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="07863-249">我们首先创建一个表示联系人表，我们在上一节中创建的模型类。</span><span class="sxs-lookup"><span data-stu-id="07863-249">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="07863-250">在本教程中，我们可以使用 Microsoft 实体框架自动从数据库生成模型类。</span><span class="sxs-lookup"><span data-stu-id="07863-250">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="07863-251">ASP.NET MVC framework 未绑定到以任何方式 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="07863-251">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="07863-252">与其他数据库访问技术包括 NHibernate，LINQ to SQL 中或 ADO.NET，可以使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="07863-252">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>


<span data-ttu-id="07863-253">请按照下列步骤以创建数据模型类：</span><span class="sxs-lookup"><span data-stu-id="07863-253">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="07863-254">右击解决方案资源管理器窗口中的 Models 文件夹并选择**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="07863-254">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="07863-255">**添加新项**对话框 （请参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="07863-255">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="07863-256">选择**数据**类别和**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="07863-256">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="07863-257">命名你的数据模型*ContactManagerModel.edmx*单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="07863-257">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="07863-258">出现实体数据模型向导 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="07863-258">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="07863-259">在**选择模型内容**步骤中，选择**从数据库生成**（请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="07863-259">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="07863-260">在**选择你的数据连接**步骤，选择 ContactManagerDB.mdf 数据库，然后输入名称*ContactManagerDBEntities* （请参阅图 8） 的实体连接设置。</span><span class="sxs-lookup"><span data-stu-id="07863-260">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="07863-261">在**选择数据库对象**步骤中，选中复选框标记为的表 （请参阅图 9）。</span><span class="sxs-lookup"><span data-stu-id="07863-261">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="07863-262">数据模型将包括 （仅仅是一个，Contacts 表没有） 查看数据库中包含的所有表。</span><span class="sxs-lookup"><span data-stu-id="07863-262">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="07863-263">输入的命名空间*模型*。</span><span class="sxs-lookup"><span data-stu-id="07863-263">Enter the namespace *Models*.</span></span> <span data-ttu-id="07863-264">单击完成按钮以完成向导。</span><span class="sxs-lookup"><span data-stu-id="07863-264">Click the Finish button to complete the wizard.</span></span>


<span data-ttu-id="07863-265">[![新项目对话框](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="07863-265">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span></span>

<span data-ttu-id="07863-266">**图 06**: 添加新项对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="07863-266">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image12.png))</span></span>


<span data-ttu-id="07863-267">[![新项目对话框](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="07863-267">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span></span>

<span data-ttu-id="07863-268">**图 07**： 选择模型内容 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="07863-268">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image14.png))</span></span>


<span data-ttu-id="07863-269">[![新项目对话框](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="07863-269">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span></span>

<span data-ttu-id="07863-270">**图 08**： 选择你的数据连接 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="07863-270">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image16.png))</span></span>


<span data-ttu-id="07863-271">[![新项目对话框](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="07863-271">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span></span>

<span data-ttu-id="07863-272">**图 09**： 选择数据库对象 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="07863-272">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image18.png))</span></span>


<span data-ttu-id="07863-273">完成实体数据模型向导后，将显示实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="07863-273">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="07863-274">设计器为每个要建模的表显示相对应的类。</span><span class="sxs-lookup"><span data-stu-id="07863-274">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="07863-275">你应看到一个名为联系人的类。</span><span class="sxs-lookup"><span data-stu-id="07863-275">You should see one class named Contacts.</span></span>

<span data-ttu-id="07863-276">实体数据模型向导生成基于数据库的表名称的类名称。</span><span class="sxs-lookup"><span data-stu-id="07863-276">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="07863-277">几乎总是需要更改由向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="07863-277">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="07863-278">右键单击设计器中的联系人类，然后选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="07863-278">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="07863-279">将类的名称从联系人 （复数形式） 更改为联系人 （单个）。</span><span class="sxs-lookup"><span data-stu-id="07863-279">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="07863-280">更改类名称后，类应该如下图 10。</span><span class="sxs-lookup"><span data-stu-id="07863-280">After you change the class name, the class should appear like Figure 10.</span></span>


<span data-ttu-id="07863-281">[![新项目对话框](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="07863-281">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span></span>

<span data-ttu-id="07863-282">**图 10**: 联系人类 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="07863-282">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image20.png))</span></span>


<span data-ttu-id="07863-283">此时，我们已创建我们的数据库模型。</span><span class="sxs-lookup"><span data-stu-id="07863-283">At this point, we have created our database model.</span></span> <span data-ttu-id="07863-284">我们可以使用联系人类来表示我们的数据库中的特定联系人记录。</span><span class="sxs-lookup"><span data-stu-id="07863-284">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="07863-285">创建主控制器</span><span class="sxs-lookup"><span data-stu-id="07863-285">Creating the Home Controller</span></span>

<span data-ttu-id="07863-286">下一步是创建我们主控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-286">The next step is to create our Home controller.</span></span> <span data-ttu-id="07863-287">Home 控制器是在 ASP.NET MVC 应用程序中调用的默认控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-287">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="07863-288">通过右键单击解决方案资源管理器窗口中的 Controllers 文件夹并选择菜单选项创建主页控制器类**添加、 控制器**（请参阅图 11）。</span><span class="sxs-lookup"><span data-stu-id="07863-288">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="07863-289">请注意该复选框标记为**添加用于创建、 更新和详细信息的方案的操作方法**。</span><span class="sxs-lookup"><span data-stu-id="07863-289">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="07863-290">请确保单击前选中此复选框，**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="07863-290">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>


<span data-ttu-id="07863-291">[![新项目对话框](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="07863-291">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span></span>

<span data-ttu-id="07863-292">**图 11**： 添加主控制器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="07863-292">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image22.png))</span></span>


<span data-ttu-id="07863-293">创建主控制器时，获取类列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="07863-293">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="07863-294">**列表 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="07863-294">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a><span data-ttu-id="07863-295">列出联系人</span><span class="sxs-lookup"><span data-stu-id="07863-295">Listing the Contacts</span></span>

<span data-ttu-id="07863-296">为了在联系人数据库表中显示的记录，我们需要创建 index （） 操作和索引视图。</span><span class="sxs-lookup"><span data-stu-id="07863-296">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="07863-297">Home 控制器已包含 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="07863-297">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="07863-298">我们需要修改此方法，使其类似列出 2 所示。</span><span class="sxs-lookup"><span data-stu-id="07863-298">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="07863-299">**列出 2-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="07863-299">**Listing 2 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

<span data-ttu-id="07863-300">请注意，列出 2 中的主页控制器类包含名为的私有字段\_实体。</span><span class="sxs-lookup"><span data-stu-id="07863-300">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="07863-301">\_实体字段表示实体数据模型中。</span><span class="sxs-lookup"><span data-stu-id="07863-301">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="07863-302">我们使用\_实体字段以与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="07863-302">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="07863-303">Index （） 方法返回表示联系人的所有联系人数据库表中的视图。</span><span class="sxs-lookup"><span data-stu-id="07863-303">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="07863-304">表达式\_实体。ContactSet.ToList() 泛型列表的形式返回联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="07863-304">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="07863-305">现在我们制作了索引控制器中，我们接下来需要创建索引视图。</span><span class="sxs-lookup"><span data-stu-id="07863-305">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="07863-306">在创建索引视图之前, 编译你的应用程序通过选择菜单选项**生成，生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="07863-306">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="07863-307">始终应在将视图添加以使模型类的列表中显示之前编译你的项目**添加视图**对话框。</span><span class="sxs-lookup"><span data-stu-id="07863-307">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="07863-308">你创建索引视图，请右键单击 index （） 方法并选择菜单选项**添加视图**（请参阅图 12）。</span><span class="sxs-lookup"><span data-stu-id="07863-308">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="07863-309">选择此菜单选项将打开**添加视图**对话框 （请参阅图 13）。</span><span class="sxs-lookup"><span data-stu-id="07863-309">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>


<span data-ttu-id="07863-310">[![新项目对话框](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="07863-310">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span></span>

<span data-ttu-id="07863-311">**图 12**： 添加索引视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="07863-311">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image24.png))</span></span>


<span data-ttu-id="07863-312">在**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="07863-312">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="07863-313">选择视图数据类 ContactManager.Contact 和查看内容列表。</span><span class="sxs-lookup"><span data-stu-id="07863-313">Select the View data class ContactManager.Contact and the View content List.</span></span> <span data-ttu-id="07863-314">选择这些选项生成的视图，显示的联系人记录的列表。</span><span class="sxs-lookup"><span data-stu-id="07863-314">Selecting these options generates a view that displays a list of Contact records.</span></span>


<span data-ttu-id="07863-315">[![新项目对话框](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="07863-315">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span></span>

<span data-ttu-id="07863-316">**图 13**: 添加视图对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="07863-316">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image26.png))</span></span>


<span data-ttu-id="07863-317">当你单击**添加**生成按钮，列出 3 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="07863-317">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="07863-318">请注意&lt;%@ 页 %&gt;文件的顶部显示的指令。</span><span class="sxs-lookup"><span data-stu-id="07863-318">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="07863-319">索引视图继承自 ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt;类。</span><span class="sxs-lookup"><span data-stu-id="07863-319">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="07863-320">换而言之，在视图中的模型类表示联系人实体的列表。</span><span class="sxs-lookup"><span data-stu-id="07863-320">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="07863-321">索引视图的正文包含的 foreach 循环中循环访问每个模型类表示的联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-321">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="07863-322">HTML 表中显示的联系人类的每个属性的值。</span><span class="sxs-lookup"><span data-stu-id="07863-322">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="07863-323">**列出 3-Views\Home\Index.aspx （未修改）**</span><span class="sxs-lookup"><span data-stu-id="07863-323">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

<span data-ttu-id="07863-324">我们需要一个对进行修改的索引视图。</span><span class="sxs-lookup"><span data-stu-id="07863-324">We need to make one modification to the Index view.</span></span> <span data-ttu-id="07863-325">因为我们不创建详细信息视图，我们可以移除的详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="07863-325">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="07863-326">查找并从索引视图中删除以下代码：</span><span class="sxs-lookup"><span data-stu-id="07863-326">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="07863-327">{.id = 项。Id}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="07863-327">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="07863-328">修改索引视图后，你可以运行联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-328">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="07863-329">选择启动调试菜单选项调试，或只需按 F5。</span><span class="sxs-lookup"><span data-stu-id="07863-329">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="07863-330">首次运行该应用程序，您会得到对话框图 14 中。</span><span class="sxs-lookup"><span data-stu-id="07863-330">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="07863-331">选择选项**修改 Web.config 文件以启用调试**，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="07863-331">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>


<span data-ttu-id="07863-332">[![新项目对话框](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="07863-332">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span></span>

<span data-ttu-id="07863-333">**图 14**： 启用调试 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="07863-333">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image28.png))</span></span>


<span data-ttu-id="07863-334">默认情况下，返回索引视图。</span><span class="sxs-lookup"><span data-stu-id="07863-334">The Index view is returned by default.</span></span> <span data-ttu-id="07863-335">此视图将列出所有联系人数据库表中的数据 （请参阅图 15）。</span><span class="sxs-lookup"><span data-stu-id="07863-335">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>


<span data-ttu-id="07863-336">[![新项目对话框](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="07863-336">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span></span>

<span data-ttu-id="07863-337">**图 15**: 索引视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="07863-337">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image30.png))</span></span>


<span data-ttu-id="07863-338">请注意索引视图包括带有标签视图底部创建新的链接。</span><span class="sxs-lookup"><span data-stu-id="07863-338">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="07863-339">在下一部分中，你将了解如何创建新的联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-339">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="07863-340">创建新的联系人</span><span class="sxs-lookup"><span data-stu-id="07863-340">Creating New Contacts</span></span>

<span data-ttu-id="07863-341">若要使用户能够创建新的联系人，我们需要将两个 create （） 操作添加到 Home 控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-341">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="07863-342">我们需要创建一个返回用于创建新联系人的 HTML 窗体的 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="07863-342">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="07863-343">我们需要创建执行实际的数据库插入新联系人的第二个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="07863-343">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="07863-344">我们需要将添加到 Home 控制器的新 create （） 方法包含在清单 4。</span><span class="sxs-lookup"><span data-stu-id="07863-344">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="07863-345">**列出 4-Controllers\HomeController.vb （使用创建方法）**</span><span class="sxs-lookup"><span data-stu-id="07863-345">**Listing 4 - Controllers\HomeController.vb (with Create methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

<span data-ttu-id="07863-346">可以仅由 HTTP POST 调用第二个 create （） 方法时，可以使用 HTTP GET 调用第一个 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="07863-346">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="07863-347">换而言之，仅当发布 HTML 窗体时，可以调用第二个 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="07863-347">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="07863-348">第一种 create （） 方法只返回一个包含用于创建新联系人的 HTML 窗体视图。</span><span class="sxs-lookup"><span data-stu-id="07863-348">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="07863-349">第二个 create （） 方法是更有意义： 它向数据库添加新联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-349">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="07863-350">请注意，第二个 create （） 方法已被修改以接受联系人类的实例。</span><span class="sxs-lookup"><span data-stu-id="07863-350">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="07863-351">从 HTML 窗体发布窗体值绑定到此联系人类由 ASP.NET MVC 框架自动。</span><span class="sxs-lookup"><span data-stu-id="07863-351">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="07863-352">从 HTML 创建窗体的每个窗体字段分配给联系人参数的属性。</span><span class="sxs-lookup"><span data-stu-id="07863-352">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="07863-353">请注意，使用 [绑定] 特性修饰的联系人参数。</span><span class="sxs-lookup"><span data-stu-id="07863-353">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="07863-354">[绑定] 属性用于从绑定中排除的联系人 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="07863-354">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="07863-355">由于 Id 属性表示标识属性，我们不 t 想要设置的 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="07863-355">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="07863-356">在 create （） 方法的正文中，实体框架用于向数据库中插入新的联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-356">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="07863-357">新的联系人添加到联系人的现有设置和 savechanges （） 方法调用以将这些更改推送回基础数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-357">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="07863-358">你可以生成一个 HTML 表单，通过右键单击任一两个 create （） 方法并选择菜单选项创建新的联系人的**添加视图**（请参阅图 16）。</span><span class="sxs-lookup"><span data-stu-id="07863-358">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>


<span data-ttu-id="07863-359">[![新项目对话框](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="07863-359">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span></span>

<span data-ttu-id="07863-360">**图 16**： 添加 Create 视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="07863-360">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image32.png))</span></span>


<span data-ttu-id="07863-361">在**添加视图**对话框中，选择**ContactManager.Contact**类和**创建**视图内容的选项 （请参阅图 17）。</span><span class="sxs-lookup"><span data-stu-id="07863-361">In the **Add View** dialog, select the **ContactManager.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="07863-362">当你单击**添加**按钮，自动生成的视图创建。</span><span class="sxs-lookup"><span data-stu-id="07863-362">When you click the **Add** button, a Create view is generated automatically.</span></span>


<span data-ttu-id="07863-363">[![新项目对话框](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="07863-363">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span></span>

<span data-ttu-id="07863-364">**图 17**： 看到分解的页 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image34.png))</span><span class="sxs-lookup"><span data-stu-id="07863-364">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image34.png))</span></span>


<span data-ttu-id="07863-365">创建视图包含联系人类的属性的每个窗体字段。</span><span class="sxs-lookup"><span data-stu-id="07863-365">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="07863-366">创建视图的代码包括在列出 5。</span><span class="sxs-lookup"><span data-stu-id="07863-366">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="07863-367">**列出 5-Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="07863-367">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

<span data-ttu-id="07863-368">修改 create （） 方法并添加创建视图后，你可以运行联系人管理器应用程序并创建新的联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-368">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="07863-369">单击**新建**显示在索引视图，以便导航到创建视图的链接。</span><span class="sxs-lookup"><span data-stu-id="07863-369">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="07863-370">你应看到图 18 中的视图。</span><span class="sxs-lookup"><span data-stu-id="07863-370">You should see the view in Figure 18.</span></span>


<span data-ttu-id="07863-371">[![新项目对话框](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="07863-371">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span></span>

<span data-ttu-id="07863-372">**图 18**: Create View ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="07863-372">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image36.png))</span></span>


## <a name="editing-contacts"></a><span data-ttu-id="07863-373">编辑联系人</span><span class="sxs-lookup"><span data-stu-id="07863-373">Editing Contacts</span></span>

<span data-ttu-id="07863-374">添加编辑联系人记录的功能是添加用于创建新的联系人记录功能非常相似。</span><span class="sxs-lookup"><span data-stu-id="07863-374">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="07863-375">首先，我们需要将两个新的编辑方法添加到 Home 控制器类。</span><span class="sxs-lookup"><span data-stu-id="07863-375">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="07863-376">这些新 edit （） 方法包含在列出 6。</span><span class="sxs-lookup"><span data-stu-id="07863-376">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="07863-377">**列出 6-Controllers\HomeController.vb （与编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="07863-377">**Listing 6 - Controllers\HomeController.vb (with Edit methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

<span data-ttu-id="07863-378">第一种 edit （） 方法调用一个 HTTP GET 操作。</span><span class="sxs-lookup"><span data-stu-id="07863-378">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="07863-379">Id 参数传递给此方法，它表示正在编辑的联系人记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="07863-379">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="07863-380">实体框架将用于检索联系人相匹配的 id。返回一个包含用于编辑记录 HTML 窗体视图。</span><span class="sxs-lookup"><span data-stu-id="07863-380">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="07863-381">第二个 edit （） 方法来执行实际更新到数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-381">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="07863-382">此方法作为参数接受联系人类的实例。</span><span class="sxs-lookup"><span data-stu-id="07863-382">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="07863-383">ASP.NET MVC framework 窗体字段从编辑窗体与此类将自动绑定。</span><span class="sxs-lookup"><span data-stu-id="07863-383">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="07863-384">请注意不要 t [绑定] 属性包括在编辑的联系人 （我们需要 Id 属性的值） 时。</span><span class="sxs-lookup"><span data-stu-id="07863-384">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="07863-385">实体框架用于将已修改的联系人保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="07863-385">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="07863-386">必须先从数据库检索原始的联系人。</span><span class="sxs-lookup"><span data-stu-id="07863-386">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="07863-387">接下来，实体框架 ApplyPropertyChanges() 方法调用可记录对联系人的更改。</span><span class="sxs-lookup"><span data-stu-id="07863-387">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="07863-388">最后，调用实体框架 savechanges （） 方法以持久保存到基础数据库更改。</span><span class="sxs-lookup"><span data-stu-id="07863-388">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="07863-389">你可以生成包含编辑窗体通过右键单击 edit （） 方法并选择添加视图菜单选项的视图。</span><span class="sxs-lookup"><span data-stu-id="07863-389">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="07863-390">在添加视图对话框中，选择**ContactManager.Models.Contact**类和**编辑**查看内容 （请参阅图 19）。</span><span class="sxs-lookup"><span data-stu-id="07863-390">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>


<span data-ttu-id="07863-391">[![新项目对话框](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="07863-391">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span></span>

<span data-ttu-id="07863-392">**图 19**： 添加一个编辑视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="07863-392">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image38.png))</span></span>


<span data-ttu-id="07863-393">单击添加按钮时，自动生成新的编辑视图。</span><span class="sxs-lookup"><span data-stu-id="07863-393">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="07863-394">生成的 HTML 窗体包含字段对应于每个联系人类 （请参阅列出 7） 的属性。</span><span class="sxs-lookup"><span data-stu-id="07863-394">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="07863-395">**列出 7-Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="07863-395">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="07863-396">删除联系人</span><span class="sxs-lookup"><span data-stu-id="07863-396">Deleting Contacts</span></span>

<span data-ttu-id="07863-397">如果你想要删除联系人，则需要将两个 delete （） 操作添加到 Home 控制器类。</span><span class="sxs-lookup"><span data-stu-id="07863-397">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="07863-398">第一个 delete （） 操作显示一个删除确认窗体。</span><span class="sxs-lookup"><span data-stu-id="07863-398">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="07863-399">第二个 delete （） 操作执行实际的删除。</span><span class="sxs-lookup"><span data-stu-id="07863-399">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="07863-400">更高版本，在迭代 #7 中，我们修改联系人管理器以便它支持 Ajax 删除一个步骤。</span><span class="sxs-lookup"><span data-stu-id="07863-400">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>


<span data-ttu-id="07863-401">列出 8 中包含两个新的 delete （） 方法。</span><span class="sxs-lookup"><span data-stu-id="07863-401">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="07863-402">**列出 8-Controllers\HomeController.vb （删除方法）**</span><span class="sxs-lookup"><span data-stu-id="07863-402">**Listing 8 - Controllers\HomeController.vb (Delete methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

<span data-ttu-id="07863-403">第一个 delete （） 方法返回用于从数据库中删除联系人记录的确认窗体 （请参阅 Figure20）。</span><span class="sxs-lookup"><span data-stu-id="07863-403">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="07863-404">第二个 delete （） 方法执行对数据库的实际删除操作。</span><span class="sxs-lookup"><span data-stu-id="07863-404">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="07863-405">从数据库中检索原始联系人后，在调用的实体框架 DeleteObject() 和 savechanges （） 方法来执行数据库删除。</span><span class="sxs-lookup"><span data-stu-id="07863-405">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>


<span data-ttu-id="07863-406">[![新项目对话框](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="07863-406">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span></span>

<span data-ttu-id="07863-407">**图 20**： 删除确认视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="07863-407">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image40.png))</span></span>


<span data-ttu-id="07863-408">我们需要修改索引视图，以使其包含一个链接，以便删除 （请参阅图 21） 的联系人记录。</span><span class="sxs-lookup"><span data-stu-id="07863-408">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="07863-409">你需要将以下代码添加到同一个表包含的单元格的编辑链接：</span><span class="sxs-lookup"><span data-stu-id="07863-409">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="07863-410">{.id = 项。Id}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="07863-410">{.id = item.Id})%&gt;</span></span>


<span data-ttu-id="07863-411">[![新项目对话框](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="07863-411">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span></span>

<span data-ttu-id="07863-412">**图 21**： 索引视图编辑链接 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image42.png))</span><span class="sxs-lookup"><span data-stu-id="07863-412">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image42.png))</span></span>


<span data-ttu-id="07863-413">接下来，我们需要创建的删除确认视图。</span><span class="sxs-lookup"><span data-stu-id="07863-413">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="07863-414">右键单击主页控制器类中的 delete （） 方法并选择添加视图菜单选项。</span><span class="sxs-lookup"><span data-stu-id="07863-414">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="07863-415">（请参阅图 22） 时出现添加视图对话框。</span><span class="sxs-lookup"><span data-stu-id="07863-415">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="07863-416">与不同的列表、 创建和编辑视图中，对于添加视图对话框中不包含用于创建删除视图的选项。</span><span class="sxs-lookup"><span data-stu-id="07863-416">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="07863-417">相反，选择**ContactManager.Models.Contact**数据类和**空**查看内容。</span><span class="sxs-lookup"><span data-stu-id="07863-417">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="07863-418">选择空视图内容的选项将需要我们自行创建视图。</span><span class="sxs-lookup"><span data-stu-id="07863-418">Selecting the Empty view content option will require us to create the view ourselves.</span></span>


<span data-ttu-id="07863-419">[![新项目对话框](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="07863-419">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span></span>

<span data-ttu-id="07863-420">**图 22**： 添加的删除确认视图 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="07863-420">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image44.png))</span></span>


<span data-ttu-id="07863-421">删除视图的内容包含在列出 9。</span><span class="sxs-lookup"><span data-stu-id="07863-421">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="07863-422">此视图包含窗体，其中确认是否特定联系人应删除 （请参阅图 21）。</span><span class="sxs-lookup"><span data-stu-id="07863-422">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="07863-423">**列出 9-Views\Home\Delete.aspx**</span><span class="sxs-lookup"><span data-stu-id="07863-423">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="07863-424">更改默认控制器的名称</span><span class="sxs-lookup"><span data-stu-id="07863-424">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="07863-425">它可能会打扰您用于使用联系人我们控制器类的名称名为 HomeController 类。</span><span class="sxs-lookup"><span data-stu-id="07863-425">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="07863-426">不应 t 控制器命名为 ContactController？</span><span class="sxs-lookup"><span data-stu-id="07863-426">Shouldn t the controller be named ContactController?</span></span>

<span data-ttu-id="07863-427">此问题问题很容易修复。</span><span class="sxs-lookup"><span data-stu-id="07863-427">This issue is easy enough to fix.</span></span> <span data-ttu-id="07863-428">首先，我们需要重构 Home 控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="07863-428">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="07863-429">在 Visual Studio 代码编辑器中打开 HomeController 类、 右键单击类的名称，然后选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="07863-429">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Rename**.</span></span> <span data-ttu-id="07863-430">选择此菜单选项将打开重命名对话框。</span><span class="sxs-lookup"><span data-stu-id="07863-430">Selecting this menu option opens the Rename dialog.</span></span>


<span data-ttu-id="07863-431">[![新项目对话框](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="07863-431">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span></span>

<span data-ttu-id="07863-432">**图 23**： 重构的控制器名称 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image46.png))</span><span class="sxs-lookup"><span data-stu-id="07863-432">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image46.png))</span></span>


<span data-ttu-id="07863-433">[![新项目对话框](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="07863-433">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span></span>

<span data-ttu-id="07863-434">**图 24**： 使用重命名对话框 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image48.png))</span><span class="sxs-lookup"><span data-stu-id="07863-434">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image48.png))</span></span>


<span data-ttu-id="07863-435">如果重命名控制器类时，Visual Studio 将更新视图文件夹中的文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="07863-435">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="07863-436">Visual Studio 将到 \Views\Contact 文件夹中重命名 \Views\Home 文件夹。</span><span class="sxs-lookup"><span data-stu-id="07863-436">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="07863-437">进行此更改后，你的应用程序将不再有一个主控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-437">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="07863-438">运行你的应用程序时，你将获得图 25 的错误页。</span><span class="sxs-lookup"><span data-stu-id="07863-438">When you run your application, you'll get the error page in Figure 25.</span></span>


<span data-ttu-id="07863-439">[![新项目对话框](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="07863-439">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span></span>

<span data-ttu-id="07863-440">**图 25**： 无默认控制器 ([单击以查看实际尺寸的图像](iteration-1-create-the-application-vb/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="07863-440">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image50.png))</span></span>


<span data-ttu-id="07863-441">我们需要更新要使用而不是主控制器的联系控制器的 Global.asax 文件中的默认路由。</span><span class="sxs-lookup"><span data-stu-id="07863-441">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="07863-442">打开 Global.asax 文件并修改默认路由 （请参阅列出 10） 使用的默认控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-442">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="07863-443">**列出 10-Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="07863-443">**Listing 10 - Global.asax.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

<span data-ttu-id="07863-444">进行这些更改之后，联系人管理器将正确运行。</span><span class="sxs-lookup"><span data-stu-id="07863-444">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="07863-445">现在，它将使用作为默认控制器的联系控制器类。</span><span class="sxs-lookup"><span data-stu-id="07863-445">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="07863-446">摘要</span><span class="sxs-lookup"><span data-stu-id="07863-446">Summary</span></span>

<span data-ttu-id="07863-447">在此第一次迭代中，我们创建一个基本的联系人管理器应用程序中的最快方法可能。</span><span class="sxs-lookup"><span data-stu-id="07863-447">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="07863-448">我们利用 Visual Studio 自动生成我们控制器和视图的初始代码。</span><span class="sxs-lookup"><span data-stu-id="07863-448">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="07863-449">我们还利用实体框架可以自动生成我们数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="07863-449">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="07863-450">目前，我们可以列表、 创建、 编辑和删除与联系人管理器应用程序的联系人记录。</span><span class="sxs-lookup"><span data-stu-id="07863-450">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="07863-451">换而言之，我们可以执行所有数据库驱动的 web 应用程序所需的基本数据库操作。</span><span class="sxs-lookup"><span data-stu-id="07863-451">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="07863-452">遗憾的是，我们的应用程序具有一些问题。</span><span class="sxs-lookup"><span data-stu-id="07863-452">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="07863-453">第一个，我不愿意再不得不承认，联系人管理器应用程序不是最具吸引力的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07863-453">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="07863-454">它需要进行一些设计工作。</span><span class="sxs-lookup"><span data-stu-id="07863-454">It needs some design work.</span></span> <span data-ttu-id="07863-455">在下一个迭代中，我们将了解如何更改的默认视图母版页和级联样式表，以提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="07863-455">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="07863-456">其次，我们已不实现任何窗体验证。</span><span class="sxs-lookup"><span data-stu-id="07863-456">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="07863-457">例如，没有任何可以阻止你提交创建联系人窗体而无需任何窗体字段中输入值。</span><span class="sxs-lookup"><span data-stu-id="07863-457">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="07863-458">此外，你可以输入无效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="07863-458">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="07863-459">我们首先为处理独特窗体验证迭代 #3 中的问题。</span><span class="sxs-lookup"><span data-stu-id="07863-459">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="07863-460">最后，并且最重要的是，联系人管理器应用程序的当前迭代无法轻松地修改或维护。</span><span class="sxs-lookup"><span data-stu-id="07863-460">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="07863-461">例如，数据库访问逻辑被融入右控制器操作。</span><span class="sxs-lookup"><span data-stu-id="07863-461">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="07863-462">这意味着，我们无法修改数据访问代码，而无需修改我们控制器。</span><span class="sxs-lookup"><span data-stu-id="07863-462">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="07863-463">在更高版本迭代中，我们将探讨我们可以实现以更具弹性，若要更改联系人管理器的软件设计模式。</span><span class="sxs-lookup"><span data-stu-id="07863-463">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="07863-464">[上一页](iteration-7-add-ajax-functionality-cs.md)
[下一页](iteration-2-make-the-application-look-nice-vb.md)</span><span class="sxs-lookup"><span data-stu-id="07863-464">[Previous](iteration-7-add-ajax-functionality-cs.md)
[Next](iteration-2-make-the-application-look-nice-vb.md)</span></span>
