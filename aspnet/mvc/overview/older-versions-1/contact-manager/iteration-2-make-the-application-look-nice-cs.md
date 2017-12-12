---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: "迭代 #2 – 使应用程序，看上去很好的 (C#) |Microsoft 文档"
author: microsoft
description: "在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 10379f5321773155aaff4c384d8e0716d7e0e874
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="iteration-2--make-the-application-look-nice-c"></a><span data-ttu-id="0889a-103">迭代 #2 – 使应用程序，看上去很好的 (C#)</span><span class="sxs-lookup"><span data-stu-id="0889a-103">Iteration #2 – Make the application look nice (C#)</span></span>
====================
<span data-ttu-id="0889a-104">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0889a-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0889a-105">下载代码</span><span class="sxs-lookup"><span data-stu-id="0889a-105">Download Code</span></span>](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> <span data-ttu-id="0889a-106">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="0889a-106">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="0889a-107">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="0889a-107">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="0889a-108">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="0889a-108">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="0889a-109">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="0889a-109">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="0889a-110">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-110">We build the application over multiple iterations.</span></span> <span data-ttu-id="0889a-111">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-111">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="0889a-112">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="0889a-112">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="0889a-113">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-113">Iteration #1 - Create the application.</span></span> <span data-ttu-id="0889a-114">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="0889a-114">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="0889a-115">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="0889a-115">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="0889a-116">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="0889a-116">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="0889a-117">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="0889a-117">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="0889a-118">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="0889a-118">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="0889a-119">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="0889a-119">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="0889a-120">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="0889a-120">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="0889a-121">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="0889a-121">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="0889a-122">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-122">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="0889a-123">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-123">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="0889a-124">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="0889a-124">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="0889a-125">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="0889a-125">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="0889a-126">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="0889a-126">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="0889a-127">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="0889a-127">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="0889a-128">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="0889a-128">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="0889a-129">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="0889a-129">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="0889a-130">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="0889a-130">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="0889a-131">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="0889a-131">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="0889a-132">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="0889a-132">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="0889a-133">此迭代</span><span class="sxs-lookup"><span data-stu-id="0889a-133">This Iteration</span></span>

<span data-ttu-id="0889a-134">此迭代的目的是提高联系人管理器应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="0889a-134">The goal of this iteration is to improve the appearance of the Contact Manager application.</span></span> <span data-ttu-id="0889a-135">当前，联系人管理器使用默认 ASP.NET MVC 视图母版页和级联样式表 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="0889a-135">Currently, the Contact Manager uses the default ASP.NET MVC view master page and cascading style sheet (see Figure 1).</span></span> <span data-ttu-id="0889a-136">这些不要看起来不正常，但我不想要看起来正像每个其他 ASP.NET MVC 网站的联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="0889a-136">These don t look bad, but I don t want the Contact Manager to look just like every other ASP.NET MVC website.</span></span> <span data-ttu-id="0889a-137">我想要将这些文件替换为自定义文件。</span><span class="sxs-lookup"><span data-stu-id="0889a-137">I want to replace these files with custom files.</span></span>


<span data-ttu-id="0889a-138">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-138">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span></span>

<span data-ttu-id="0889a-139">**图 01**: ASP.NET MVC 应用程序的默认外观 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-139">**Figure 01**: The default appearance of an ASP.NET MVC Application ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span></span>


<span data-ttu-id="0889a-140">在此迭代中，我讨论两种方法来改进我们的应用程序的可视设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-140">In this iteration, I discuss two approaches to improving the visual design of our application.</span></span> <span data-ttu-id="0889a-141">首先，我向你演示如何充分利用 ASP.NET MVC 设计库以下载可用的 ASP.NET MVC 设计模板。</span><span class="sxs-lookup"><span data-stu-id="0889a-141">First, I show you how to take advantage of the ASP.NET MVC Design gallery to download a free ASP.NET MVC design template.</span></span> <span data-ttu-id="0889a-142">ASP.NET MVC 设计库，可创建专业人员的 web 应用程序不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="0889a-142">The ASP.NET MVC Design gallery enables you to create a professional web application without doing any work.</span></span>

<span data-ttu-id="0889a-143">我决定不使用模板从 ASP.NET MVC 设计库联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-143">I decided to not use a template from the ASP.NET MVC Design gallery for the Contact Manager application.</span></span> <span data-ttu-id="0889a-144">相反，我必须由专业人员设计公司的自定义设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-144">Instead, I had a custom design created by a professional design firm.</span></span> <span data-ttu-id="0889a-145">在本教程的第二个阶段，我将说明我专业人员设计公司，以创建最终的 ASP.NET MVC 设计的工作方式。</span><span class="sxs-lookup"><span data-stu-id="0889a-145">In the second part of this tutorial, I explain how I worked with a professional design company to create the final ASP.NET MVC design.</span></span>

## <a name="the-aspnet-mvc-design-gallery"></a><span data-ttu-id="0889a-146">ASP.NET MVC 设计库</span><span class="sxs-lookup"><span data-stu-id="0889a-146">The ASP.NET MVC Design Gallery</span></span>

<span data-ttu-id="0889a-147">ASP.NET MVC 设计库是由 Microsoft 提供的可用资源。</span><span class="sxs-lookup"><span data-stu-id="0889a-147">The ASP.NET MVC Design Gallery is a free resource provided by Microsoft.</span></span> <span data-ttu-id="0889a-148">ASP.NET MVC 库位于以下地址：</span><span class="sxs-lookup"><span data-stu-id="0889a-148">The ASP.NET MVC Gallery is located at the following address:</span></span>

[<span data-ttu-id="0889a-149">https://www.asp.net/mvc/gallery</span><span class="sxs-lookup"><span data-stu-id="0889a-149">https://www.asp.net/mvc/gallery</span></span>](https://www.asp.net/mvc/gallery)

<span data-ttu-id="0889a-150">ASP.NET MVC 设计库承载专门为使用 ASP.NET MVC 项目中创建的免费网站设计的集合。</span><span class="sxs-lookup"><span data-stu-id="0889a-150">The ASP.NET MVC Design Gallery hosts a collection of free website designs that were created specifically for using in an ASP.NET MVC project.</span></span> <span data-ttu-id="0889a-151">设计上载由社区的成员。</span><span class="sxs-lookup"><span data-stu-id="0889a-151">Designs are uploaded by members of the community.</span></span> <span data-ttu-id="0889a-152">库的访问者可以对其最喜欢的设计进行投票 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="0889a-152">Visitors to the Gallery can vote for their favorite designs (see Figure 2).</span></span>


<span data-ttu-id="0889a-153">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-153">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span></span>

<span data-ttu-id="0889a-154">**图 02**: ASP.NET MVC 设计库 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-154">**Figure 02**: The ASP.NET MVC Design Gallery ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span></span>


<span data-ttu-id="0889a-155">当我撰写本教程中，库中最常用的设计是由 David Hauser 命名年 10 月的设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-155">As I write this tutorial, the most popular design in the gallery is a design named October by David Hauser.</span></span> <span data-ttu-id="0889a-156">你可以通过完成以下步骤为这种设计用于 ASP.NET MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="0889a-156">You can use this design for an ASP.NET MVC project by completing the following steps:</span></span>

1. <span data-ttu-id="0889a-157">单击**下载**按钮 October.zip 文件下载到你的计算机。</span><span class="sxs-lookup"><span data-stu-id="0889a-157">Click the **Download** button to download the October.zip file to your computer.</span></span>
2. <span data-ttu-id="0889a-158">右键单击下载的 October.zip 文件，然后单击**解除阻止**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="0889a-158">Right-click the downloaded October.zip file and click the **Unblock** button (see Figure 3).</span></span>
3. <span data-ttu-id="0889a-159">将文件提取到名为年 10 月的文件夹。</span><span class="sxs-lookup"><span data-stu-id="0889a-159">Unzip the file to a folder named October.</span></span>
4. <span data-ttu-id="0889a-160">从包含在年 10 月文件夹 DesignTemplate 文件夹中选择的所有文件，右键单击文件，然后选择菜单选项**复制**。</span><span class="sxs-lookup"><span data-stu-id="0889a-160">Select all of the files from the DesignTemplate folder contained in the October folder, right-click the files, and select the menu option **Copy**.</span></span>
5. <span data-ttu-id="0889a-161">右键单击 Visual Studio 解决方案资源管理器窗口中的 ContactManager 项目节点并选择菜单选项**粘贴**（请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="0889a-161">Right-click the ContactManager project node in the Visual Studio Solution Explorer window and select the menu option **Paste** (see Figure 4).</span></span>
6. <span data-ttu-id="0889a-162">选择 Visual Studio 菜单选项**编辑、 查找和替换，快速替换**和替换*[MyProjectName]*与*ContactManager* （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="0889a-162">Select the Visual Studio menu option **Edit, Find and Replace, Quick Replace** and replace *[MyProjectName]* with *ContactManager* (see Figure 5).</span></span>


<span data-ttu-id="0889a-163">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-163">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span></span>

<span data-ttu-id="0889a-164">**图 03**： 取消阻止文件从 web 下载 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-164">**Figure 03**: Unblocking a file downloaded from the web ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span></span>


<span data-ttu-id="0889a-165">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-165">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span></span>

<span data-ttu-id="0889a-166">**图 04**： 覆盖在解决方案资源管理器中的文件 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-166">**Figure 04**: Overwriting files in the Solution Explorer ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span></span>


<span data-ttu-id="0889a-167">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-167">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span></span>

<span data-ttu-id="0889a-168">**图 05**: [ProjectName] 替换为 ContactManager ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-168">**Figure 05**: Replacing [ProjectName] with ContactManager ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span></span>


<span data-ttu-id="0889a-169">完成这些步骤后，web 应用程序将使用新的设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-169">After you complete these steps, your web application will use the new design.</span></span> <span data-ttu-id="0889a-170">在图 6 中页演示年 10 月设计的联系人管理器应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="0889a-170">The page in Figure 6 illustrates the appearance of the Contact Manager application with the October design.</span></span>


<span data-ttu-id="0889a-171">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-171">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span></span>

<span data-ttu-id="0889a-172">**图 06**: ContactManager 年 10 月模板 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-172">**Figure 06**: ContactManager with the October template ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span></span>


## <a name="creating-a-custom-aspnet-mvc-design"></a><span data-ttu-id="0889a-173">创建自定义 ASP.NET MVC 设计</span><span class="sxs-lookup"><span data-stu-id="0889a-173">Creating a Custom ASP.NET MVC Design</span></span>

<span data-ttu-id="0889a-174">ASP.NET MVC 设计库具有不同的设计样式很好选择。</span><span class="sxs-lookup"><span data-stu-id="0889a-174">The ASP.NET MVC Design Gallery has a good selection of different design styles.</span></span> <span data-ttu-id="0889a-175">库为你提供了一种自定义的 ASP.NET MVC 应用程序的外观的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="0889a-175">The Gallery provides you with a painless way to customize the appearance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="0889a-176">而且，当然，库中包含的完全免费而言优势巨大。</span><span class="sxs-lookup"><span data-stu-id="0889a-176">And, of course, the Gallery has the big advantage of being completely free.</span></span>

<span data-ttu-id="0889a-177">但是，你可能需要创建你的网站的完全唯一设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-177">However, you might need to create a completely unique design for your website.</span></span> <span data-ttu-id="0889a-178">在这种情况下，最好使用网站设计公司。</span><span class="sxs-lookup"><span data-stu-id="0889a-178">In that case, it makes sense to work with a website design company.</span></span> <span data-ttu-id="0889a-179">我决定采用此方法为联系人管理器应用程序的设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-179">I decided to take this approach for the design for the Contact Manager application.</span></span>

<span data-ttu-id="0889a-180">我压缩向上联系人管理器从迭代 #1，并发送到设计公司的项目。</span><span class="sxs-lookup"><span data-stu-id="0889a-180">I zipped up the Contact Manager from Iteration #1 and sent the project to the design company.</span></span> <span data-ttu-id="0889a-181">它们不归 Visual Studio （耻辱在其上 ！），但这不是 t 会出现问题。</span><span class="sxs-lookup"><span data-stu-id="0889a-181">They did not own Visual Studio (shame on them!), but that didn t present a problem.</span></span> <span data-ttu-id="0889a-182">它们是可以从免费下载 Microsoft Visual Web Developer [https://www.asp.net](https://www.asp.net)网站，然后打开 Visual Web Developer 中的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-182">They were able to download Microsoft Visual Web Developer for free from the [https://www.asp.net](https://www.asp.net) website and open the Contact Manager application in Visual Web Developer.</span></span> <span data-ttu-id="0889a-183">在几天，它们必须生成图 7 中的设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-183">In a couple of days, they had produced the design in Figure 7.</span></span>


<span data-ttu-id="0889a-184">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-184">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span></span>

<span data-ttu-id="0889a-185">**图 07**: ASP.NET MVC 联系人管理器设计 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-185">**Figure 07**: The ASP.NET MVC Contact Manager Design ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span></span>


<span data-ttu-id="0889a-186">新设计由两个主要文件组成： 新的级联样式表文件和新视图母版页文件。</span><span class="sxs-lookup"><span data-stu-id="0889a-186">The new design consisted of two main files: a new cascading style sheet file and a new view master page file.</span></span> <span data-ttu-id="0889a-187">视图的母版页包含的布局和共享中的 ASP.NET MVC 应用程序视图的内容。</span><span class="sxs-lookup"><span data-stu-id="0889a-187">A view master page contains the layout and shared content for views in an ASP.NET MVC application.</span></span> <span data-ttu-id="0889a-188">例如，视图的母版页包括标头、 导航选项卡和页脚显示在图 7。</span><span class="sxs-lookup"><span data-stu-id="0889a-188">For example, the view master page includes the header, navigation tabs, and footer that appear in Figure 7.</span></span> <span data-ttu-id="0889a-189">我使用从设计公司中，新的 Site.Master 文件覆盖现有 Site.Master 视图母版页 Views\Shared 文件夹中</span><span class="sxs-lookup"><span data-stu-id="0889a-189">I overwrote the existing Site.Master view master page in the Views\Shared folder with the new Site.Master file from the design company,</span></span>

<span data-ttu-id="0889a-190">设计公司还创建一个新的级联样式表和一组的映像。</span><span class="sxs-lookup"><span data-stu-id="0889a-190">The design company also created a new cascading style sheet and set of images.</span></span> <span data-ttu-id="0889a-191">我的内容文件夹中放置这些新文件，并覆盖现有的 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="0889a-191">I placed these new files in the Content folder and overwrote the existing Site.css file.</span></span> <span data-ttu-id="0889a-192">应将所有静态内容放在内容文件夹。</span><span class="sxs-lookup"><span data-stu-id="0889a-192">You should place all static content in the Content folder.</span></span>

<span data-ttu-id="0889a-193">请注意，新设计的联系人管理器中包含图像编辑和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="0889a-193">Notice that the new design for the Contact Manager includes images for editing and deleting contacts.</span></span> <span data-ttu-id="0889a-194">联系人的 HTML 表中每个联系人旁边将显示编辑和删除映像。</span><span class="sxs-lookup"><span data-stu-id="0889a-194">An Edit and Delete image appear next to each contact in the HTML table of contacts.</span></span>

<span data-ttu-id="0889a-195">最初，这些链接在呈现的 HTML。ActionLink() 帮助器如下：</span><span class="sxs-lookup"><span data-stu-id="0889a-195">Originally, these links that were rendered with the HTML.ActionLink() helper like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

<span data-ttu-id="0889a-196">Html.ActionLink() 方法不支持 （方法 HTML 编码出于安全原因此链接文本） 的映像。</span><span class="sxs-lookup"><span data-stu-id="0889a-196">The Html.ActionLink() method does not support images (the method HTML encodes the link text for security reasons).</span></span> <span data-ttu-id="0889a-197">因此，我可以对 Html.ActionLink() 的调用替换对 Url.Action() 如下的调用：</span><span class="sxs-lookup"><span data-stu-id="0889a-197">Therefore, I replaced the calls to Html.ActionLink() with calls to Url.Action() like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

<span data-ttu-id="0889a-198">Html.ActionLink() 方法呈现整个 HTML 超链接。</span><span class="sxs-lookup"><span data-stu-id="0889a-198">The Html.ActionLink() method renders an entire HTML hyperlink.</span></span> <span data-ttu-id="0889a-199">Url.Action() 方法中，另一方面，呈现只而无需 URL &lt;&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="0889a-199">The Url.Action() method, on the other hand, renders just the URL without the &lt;a&gt; tag.</span></span>

<span data-ttu-id="0889a-200">此外，请注意，新的设计包括选定的和未选定的选项卡。</span><span class="sxs-lookup"><span data-stu-id="0889a-200">Notice, furthermore, that the new design includes both selected and unselected tabs.</span></span> <span data-ttu-id="0889a-201">例如，在图 8:**创建新联系人**选择选项卡和**我的联系人**不选择选项卡。</span><span class="sxs-lookup"><span data-stu-id="0889a-201">For example, in Figure 8, the **Create New Contact** tab is selected and the **My Contacts** tab is not selected.</span></span>


<span data-ttu-id="0889a-202">[![新项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="0889a-202">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span></span>

<span data-ttu-id="0889a-203">**图 08**： 选中和取消选中选项卡 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="0889a-203">**Figure 08**: Selected and unselected tabs([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span></span>


<span data-ttu-id="0889a-204">若要支持呈现选定和未选定的选项卡，我创建了名为 MenuItemHelper 的自定义 HTML 帮助。</span><span class="sxs-lookup"><span data-stu-id="0889a-204">To support rendering both selected and unselected tabs, I created a custom HTML helper named the MenuItemHelper.</span></span> <span data-ttu-id="0889a-205">此帮助器方法呈现或者&lt;li&gt;标记或&lt;li 类 ="所选"&gt;具体取决于当前控制器和操作是否与传递给帮助器的控制器和操作名称对应的标记。</span><span class="sxs-lookup"><span data-stu-id="0889a-205">This helper method renders either a &lt;li&gt; tag or a &lt;li class="selected"&gt; tag depending on whether the current controller and action corresponds to the controller and action name passed to the helper.</span></span> <span data-ttu-id="0889a-206">MenuItemHelper 的代码包含在清单 1。</span><span class="sxs-lookup"><span data-stu-id="0889a-206">The code for the MenuItemHelper is contained in Listing 1.</span></span>

<span data-ttu-id="0889a-207">**列表 1-Helpers\MenuItemHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="0889a-207">**Listing 1 - Helpers\MenuItemHelper.cs**</span></span>

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

<span data-ttu-id="0889a-208">MenuItemHelper 在内部使用 TagBuilder 类来生成&lt;li&gt; HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="0889a-208">The MenuItemHelper uses the TagBuilder class internally to build the &lt;li&gt; HTML tag.</span></span> <span data-ttu-id="0889a-209">TagBuilder 类是当需要生成新的 HTML 标记时可以使用一个非常有用的实用程序类。</span><span class="sxs-lookup"><span data-stu-id="0889a-209">The TagBuilder class is a very useful utility class that you can use whenever you need to build up a new HTML tag.</span></span> <span data-ttu-id="0889a-210">它包括用于添加属性、 添加 CSS 类、 生成 Id，和修改标记的方法内部 HTML。</span><span class="sxs-lookup"><span data-stu-id="0889a-210">It includes methods for adding attributes, adding CSS classes, generating Ids, and modifying the tag s inner HTML.</span></span>

## <a name="summary"></a><span data-ttu-id="0889a-211">摘要</span><span class="sxs-lookup"><span data-stu-id="0889a-211">Summary</span></span>

<span data-ttu-id="0889a-212">在此迭代中，我们改进我们的 ASP.NET MVC 应用程序的可视设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-212">In this iteration, we improved the visual design of our ASP.NET MVC application.</span></span> <span data-ttu-id="0889a-213">首先，已引入到 ASP.NET MVC 设计库。</span><span class="sxs-lookup"><span data-stu-id="0889a-213">First, you were introduced to the ASP.NET MVC Design Gallery.</span></span> <span data-ttu-id="0889a-214">您学习了如何从你可以在 ASP.NET MVC 应用程序中使用 ASP.NET MVC 设计库下载免费设计模板。</span><span class="sxs-lookup"><span data-stu-id="0889a-214">You learned how to download free design templates from the ASP.NET MVC Design Gallery that you can use in your ASP.NET MVC applications.</span></span>

<span data-ttu-id="0889a-215">接下来，我们讨论了通过修改默认级联样式表文件和母版视图中页面文件，你就可以创建自定义设计。</span><span class="sxs-lookup"><span data-stu-id="0889a-215">Next, we discussed how you can create a custom design by modifying the default cascading style sheet file and master view page file.</span></span> <span data-ttu-id="0889a-216">为了支持新的设计，我们必须对我们的联系人管理器应用程序进行少量更改。</span><span class="sxs-lookup"><span data-stu-id="0889a-216">In order to support the new design, we had to make some minor changes to our Contact Manager application.</span></span> <span data-ttu-id="0889a-217">例如，我们将添加名为显示选定和未选定的选项卡 MenuItemHelper 的新 HTML 帮助。</span><span class="sxs-lookup"><span data-stu-id="0889a-217">For example, we added a new HTML helper named the MenuItemHelper that displays selected and unselected tabs.</span></span>

<span data-ttu-id="0889a-218">在下一步的迭代中，我们解决的验证非常重要的主题。</span><span class="sxs-lookup"><span data-stu-id="0889a-218">In the next iteration, we tackle the very important subject of validation.</span></span> <span data-ttu-id="0889a-219">以便用户无法未首先提供所需的值，如人员 s 情况下创建一个新的联系人和姓氏，我们将验证代码添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="0889a-219">We add validation code to our application so that a user cannot create a new contact without supplying required values such as a person s first and last name.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="0889a-220">[上一页](iteration-1-create-the-application-cs.md)
[下一页](iteration-3-add-form-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="0889a-220">[Previous](iteration-1-create-the-application-cs.md)
[Next](iteration-3-add-form-validation-cs.md)</span></span>
