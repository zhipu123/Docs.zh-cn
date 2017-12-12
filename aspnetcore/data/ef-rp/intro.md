---
title: "包含实体框架核心技术-8 的教程 1 razor 页面"
author: rick-anderson
description: "演示如何创建使用实体框架核心的 Razor 页面应用程序"
keywords: "ASP.NET 核心，实体框架核心，教程"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/intro
ms.openlocfilehash: d3bcf9aaf7fa809825a0ba8631ee52d3860b090d
ms.sourcegitcommit: 05e798c9bac7b9e9983599afb227ef393905d023
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a><span data-ttu-id="7fd16-104">开始使用 Razor 页和使用 Visual Studio (第 1 个 8) 的实体框架核心</span><span class="sxs-lookup"><span data-stu-id="7fd16-104">Getting started with Razor Pages and Entity Framework Core using Visual Studio (1 of 8)</span></span>

<span data-ttu-id="7fd16-105">通过[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7fd16-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7fd16-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework (EF) 核心 2.0 和 Visual Studio 2017 ASP.NET 核心 2.0 MVC web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7fd16-106">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="7fd16-107">该示例应用是一个用于 fictional Contoso 大学网站。</span><span class="sxs-lookup"><span data-stu-id="7fd16-107">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="7fd16-108">它包括诸如学生许可、 过程创建和教师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="7fd16-108">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="7fd16-109">此页是一系列教程说明如何生成 Contoso 大学示例应用程序中的第一个。</span><span class="sxs-lookup"><span data-stu-id="7fd16-109">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="7fd16-110">下载或查看已完成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7fd16-110">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="7fd16-111">[下载说明](xref:tutorials/index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-111">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fd16-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="7fd16-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="7fd16-113">疑难解答</span><span class="sxs-lookup"><span data-stu-id="7fd16-113">Troubleshooting</span></span>

<span data-ttu-id="7fd16-114">如果你遇到无法解决的问题，通常可以通过比较你的代码查找解决方案[完成阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)或[已完成的项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-114">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) or [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span></span> <span data-ttu-id="7fd16-115">有关常见错误以及如何解决这些列表，请参阅[最后一个教程系列中的故障排除部分](xref:data/ef-mvc/advanced#common-errors)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-115">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="7fd16-116">如果没有找到你那里需要你可以将问题发布到为 StackOverflow.com [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core)或[EF 核心](https://stackoverflow.com/questions/tagged/entity-framework-core)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-116">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="7fd16-117">这一系列教程的基础上早期教程中执行哪些操作。</span><span class="sxs-lookup"><span data-stu-id="7fd16-117">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="7fd16-118">请考虑在每个成功的教程完成后保存项目的副本。</span><span class="sxs-lookup"><span data-stu-id="7fd16-118">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="7fd16-119">如果遇到问题时，便可以通过从以前的教程，而不是追溯到开头。</span><span class="sxs-lookup"><span data-stu-id="7fd16-119">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="7fd16-120">或者，你可以下载[完成阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)并重新使用已完成的阶段开始。</span><span class="sxs-lookup"><span data-stu-id="7fd16-120">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="7fd16-121">Contoso 大学 web 应用</span><span class="sxs-lookup"><span data-stu-id="7fd16-121">The Contoso University web app</span></span>

<span data-ttu-id="7fd16-122">这些教程中生成该应用是基本大学网站。</span><span class="sxs-lookup"><span data-stu-id="7fd16-122">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="7fd16-123">用户可以查看和更新学生、 课程中和教师信息。</span><span class="sxs-lookup"><span data-stu-id="7fd16-123">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="7fd16-124">以下是几个在本教程创建的屏幕。</span><span class="sxs-lookup"><span data-stu-id="7fd16-124">Here are a few of the screens created in the tutorial.</span></span>

![学生索引页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

<span data-ttu-id="7fd16-127">什么由内置模板生成即将此站点的用户界面样式。</span><span class="sxs-lookup"><span data-stu-id="7fd16-127">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="7fd16-128">教程的重点是 EF 核心具有 Razor 页面，ui 部分除外。</span><span class="sxs-lookup"><span data-stu-id="7fd16-128">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="7fd16-129">创建 Razor 页的 web 应用</span><span class="sxs-lookup"><span data-stu-id="7fd16-129">Create a Razor Pages web app</span></span>

* <span data-ttu-id="7fd16-130">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="7fd16-130">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="7fd16-131">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7fd16-131">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="7fd16-132">将项目**ContosoUniversity**。</span><span class="sxs-lookup"><span data-stu-id="7fd16-132">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="7fd16-133">务必要将项目*ContosoUniversity*因此命名空间与匹配时代码复制/粘贴。</span><span class="sxs-lookup"><span data-stu-id="7fd16-133">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="7fd16-134">![新建 ASP.NET Core Web 应用程序](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="7fd16-134">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="7fd16-135">在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="7fd16-135">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="7fd16-136">![Web 应用程序（Razor 页面）](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="7fd16-136">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="7fd16-137">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在运行（不附加调试器）</span><span class="sxs-lookup"><span data-stu-id="7fd16-137">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="7fd16-138">设置站点样式</span><span class="sxs-lookup"><span data-stu-id="7fd16-138">Set up the site style</span></span>

<span data-ttu-id="7fd16-139">少量的更改将设置为站点菜单、 布局和主页。</span><span class="sxs-lookup"><span data-stu-id="7fd16-139">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="7fd16-140">打开*Pages/_Layout.cshtml*并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="7fd16-140">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="7fd16-141">将每个匹配项的"ContosoUniversity"更改为"Contoso 大学。"</span><span class="sxs-lookup"><span data-stu-id="7fd16-141">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="7fd16-142">有三个匹配项。</span><span class="sxs-lookup"><span data-stu-id="7fd16-142">There are three occurrences.</span></span>

* <span data-ttu-id="7fd16-143">添加菜单项**学生**，**课程**，**教师**，和**部门**，并删除**联系人**菜单项。</span><span class="sxs-lookup"><span data-stu-id="7fd16-143">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="7fd16-144">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="7fd16-144">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-39,47&range=1-50)]

<span data-ttu-id="7fd16-145">在*Views/Home/Index.cshtml*，将文件的内容替换为以下代码以将有关 ASP.NET 和 MVC 的文本替换为此应用相关的文本：</span><span class="sxs-lookup"><span data-stu-id="7fd16-145">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="7fd16-146">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="7fd16-146">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="7fd16-147">在以下教程中创建的选项卡显示主页：</span><span class="sxs-lookup"><span data-stu-id="7fd16-147">The home page is displayed with tabs created in the following tutorials:</span></span>

![Contoso 大学主页](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="7fd16-149">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="7fd16-149">Create the data model</span></span>

<span data-ttu-id="7fd16-150">创建 Contoso 大学应用的实体类。</span><span class="sxs-lookup"><span data-stu-id="7fd16-150">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="7fd16-151">使用以下三个实体启动：</span><span class="sxs-lookup"><span data-stu-id="7fd16-151">Start with the following three entities:</span></span>

![课程注册学生数据模型关系图](intro/_static/data-model-diagram.png)

<span data-ttu-id="7fd16-153">之间的一对多关系`Student`和`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-153">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="7fd16-154">之间的一对多关系`Course`和`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-154">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="7fd16-155">一名学生可以在任意数量的课程中注册。</span><span class="sxs-lookup"><span data-stu-id="7fd16-155">A student can enroll in any number of courses.</span></span> <span data-ttu-id="7fd16-156">课程可以有任意数量的学生在其中注册。</span><span class="sxs-lookup"><span data-stu-id="7fd16-156">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="7fd16-157">在以下部分中，创建为这些实体的每个类。</span><span class="sxs-lookup"><span data-stu-id="7fd16-157">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="7fd16-158">学生实体</span><span class="sxs-lookup"><span data-stu-id="7fd16-158">The Student entity</span></span>

![学生实体关系图](intro/_static/student-entity.png)

<span data-ttu-id="7fd16-160">创建*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7fd16-160">Create a *Models* folder.</span></span> <span data-ttu-id="7fd16-161">在*模型*文件夹中，创建一个名为的类文件*Student.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-161">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="7fd16-162">`ID`属性变为对应于此类数据库 (DB) 表的主键列。</span><span class="sxs-lookup"><span data-stu-id="7fd16-162">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="7fd16-163">默认情况下，EF 核心将解释一个属性，名为`ID`或`classnameID`为主键。</span><span class="sxs-lookup"><span data-stu-id="7fd16-163">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="7fd16-164">`Enrollments`属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="7fd16-164">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="7fd16-165">导航属性链接到与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-165">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="7fd16-166">在这种情况下，`Enrollments`属性`Student entity`包含的所有`Enrollment`与该订阅相关的实体`Student`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-166">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="7fd16-167">例如，如果数据库中的学生行有两个相关注册行`Enrollments`导航属性包含这两个`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-167">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="7fd16-168">相关`Enrollment`行是包含该学生的主键值中的行`StudentID`列。</span><span class="sxs-lookup"><span data-stu-id="7fd16-168">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="7fd16-169">例如，假设学生 id = 1 有两个行`Enrollment`表。</span><span class="sxs-lookup"><span data-stu-id="7fd16-169">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="7fd16-170">`Enrollment`表包含两个行`StudentID`= 1。</span><span class="sxs-lookup"><span data-stu-id="7fd16-170">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="7fd16-171">`StudentID`是中的外键`Enrollment`指定中的学生的表`Student`表。</span><span class="sxs-lookup"><span data-stu-id="7fd16-171">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="7fd16-172">如果导航属性可以具有多个实体，导航属性必须是列表类型，如`ICollection<T>`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-172">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="7fd16-173">`ICollection<T>`可以指定，或如类型`List<T>`或`HashSet<T>`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-173">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="7fd16-174">当`ICollection<T>`是使用，EF 核心创建`HashSet<T>`默认情况下的集合。</span><span class="sxs-lookup"><span data-stu-id="7fd16-174">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="7fd16-175">包含多个实体的导航属性来自于多对多和一个对多关系。</span><span class="sxs-lookup"><span data-stu-id="7fd16-175">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="7fd16-176">注册实体</span><span class="sxs-lookup"><span data-stu-id="7fd16-176">The Enrollment entity</span></span>

![注册实体关系图](intro/_static/enrollment-entity.png)

<span data-ttu-id="7fd16-178">在*模型*文件夹中，创建*Enrollment.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-178">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="7fd16-179">`EnrollmentID`属性是为主键。</span><span class="sxs-lookup"><span data-stu-id="7fd16-179">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="7fd16-180">此实体使用`classnameID`模式而不是`ID`如`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-180">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="7fd16-181">通常，开发人员选择一个模式并使用整个数据模型。</span><span class="sxs-lookup"><span data-stu-id="7fd16-181">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="7fd16-182">在更高版本的教程中，没有类名的情况下使用 ID 将显示以便更加轻松地在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="7fd16-182">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="7fd16-183">`Grade`属性是`enum`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-183">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="7fd16-184">后问号`Grade`类型声明指示`Grade`属性可以为 null。</span><span class="sxs-lookup"><span data-stu-id="7fd16-184">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="7fd16-185">为 null 的等级不从零个年级不同--null 意味着一个等级而言未知的或未尚未分配。</span><span class="sxs-lookup"><span data-stu-id="7fd16-185">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="7fd16-186">`StudentID`属性是一个外键，且相应的导航属性为`Student`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-186">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="7fd16-187">`Enrollment`实体是与一个相关联`Student`实体，因此该属性包含单个`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-187">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="7fd16-188">`Student`实体区别`Student.Enrollments`导航属性，其中包含多个`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-188">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="7fd16-189">`CourseID`属性是一个外键，且相应的导航属性为`Course`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-189">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="7fd16-190">`Enrollment`实体是与一个相关联`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-190">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="7fd16-191">EF 核心作为外键解释属性，如果它名为`<navigation property name><primary key property name>`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-191">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="7fd16-192">例如，`StudentID`为`Student`导航属性，因为`Student`实体的主键是`ID`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-192">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="7fd16-193">外键属性还可以进行命名`<primary key property name>`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-193">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="7fd16-194">例如，`CourseID`由于`Course`实体的主键是`CourseID`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-194">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="7fd16-195">课程实体</span><span class="sxs-lookup"><span data-stu-id="7fd16-195">The Course entity</span></span>

![课程实体关系图](intro/_static/course-entity.png)

<span data-ttu-id="7fd16-197">在*模型*文件夹中，创建*Course.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-197">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="7fd16-198">`Enrollments`属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="7fd16-198">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="7fd16-199">A`Course`可以与任意数量的相关实体`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-199">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="7fd16-200">`DatabaseGenerated`属性允许应用程序以指定为主键，而不是具有数据库生成它。</span><span class="sxs-lookup"><span data-stu-id="7fd16-200">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="7fd16-201">创建 SchoolContext 数据库上下文</span><span class="sxs-lookup"><span data-stu-id="7fd16-201">Create the SchoolContext DB context</span></span>

<span data-ttu-id="7fd16-202">协调 EF 核心功能为给定的数据模型的主类是 DB 上下文类。</span><span class="sxs-lookup"><span data-stu-id="7fd16-202">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="7fd16-203">数据上下文派生自`Microsoft.EntityFrameworkCore.DbContext`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-203">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="7fd16-204">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-204">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="7fd16-205">在此项目中类命名为`SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-205">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="7fd16-206">在项目文件夹中，创建名为的文件夹*数据*。</span><span class="sxs-lookup"><span data-stu-id="7fd16-206">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="7fd16-207">在*数据*文件夹创建*SchoolContext.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-207">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="7fd16-208">此代码将创建`DbSet`每个实体集的属性。</span><span class="sxs-lookup"><span data-stu-id="7fd16-208">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="7fd16-209">在 EF 核心术语：</span><span class="sxs-lookup"><span data-stu-id="7fd16-209">In EF Core terminology:</span></span>

* <span data-ttu-id="7fd16-210">实体集通常对应于数据库表。</span><span class="sxs-lookup"><span data-stu-id="7fd16-210">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="7fd16-211">实体对应于表中的行。</span><span class="sxs-lookup"><span data-stu-id="7fd16-211">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="7fd16-212">`DbSet<Enrollment>`和`DbSet<Course>`可以省略。</span><span class="sxs-lookup"><span data-stu-id="7fd16-212">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="7fd16-213">EF 核心或希伯来语它们隐式`Student`实体引用`Enrollment`实体，与`Enrollment`实体引用`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="7fd16-213">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="7fd16-214">对于本教程中，保留`DbSet<Enrollment>`和`DbSet<Course>`中`SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-214">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="7fd16-215">EF 核心创建数据库后，创建具有名称相同的表`DbSet`属性名称。</span><span class="sxs-lookup"><span data-stu-id="7fd16-215">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="7fd16-216">为集合的属性名将采用通常复数形式 （学生而不是学生）。</span><span class="sxs-lookup"><span data-stu-id="7fd16-216">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="7fd16-217">开发人员不同意有关表名称是否应采用复数形式。</span><span class="sxs-lookup"><span data-stu-id="7fd16-217">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="7fd16-218">有关这些教程中，覆盖默认行为是在 DbContext 中指定单数表名称。</span><span class="sxs-lookup"><span data-stu-id="7fd16-218">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="7fd16-219">若要指定单数表名称，添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-219">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="7fd16-220">上下文注册依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="7fd16-220">Register the context with dependency injection</span></span>

<span data-ttu-id="7fd16-221">ASP.NET 核心包括[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-221">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="7fd16-222">在应用程序启动过程的依赖关系注入注册服务 （例如 EF 核心 DB 上下文中）。</span><span class="sxs-lookup"><span data-stu-id="7fd16-222">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="7fd16-223">需要这些服务 （如 Razor 页） 的组件提供了这些服务通过构造函数参数。</span><span class="sxs-lookup"><span data-stu-id="7fd16-223">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="7fd16-224">在教程后面部分显示了获取的数据库上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="7fd16-224">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="7fd16-225">若要注册`SchoolContext`作为一种服务，打开*Startup.cs*，并添加到突出显示的行`ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="7fd16-225">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="7fd16-226">连接字符串的名称均在通过传递给上下文上调用的方法`DbContextOptionsBuilder`对象。</span><span class="sxs-lookup"><span data-stu-id="7fd16-226">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="7fd16-227">以进行本地开发， [ASP.NET 核心配置系统](xref:fundamentals/configuration/index)读取中的连接字符串*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="7fd16-227">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="7fd16-228">添加`using`语句`ContosoUniversity.Data`和`Microsoft.EntityFrameworkCore`命名空间。</span><span class="sxs-lookup"><span data-stu-id="7fd16-228">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="7fd16-229">生成项目。</span><span class="sxs-lookup"><span data-stu-id="7fd16-229">Build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="7fd16-230">打开*appsettings.json*文件并添加连接字符串，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="7fd16-230">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="7fd16-231">前面提到的连接字符串使用`ConnectRetryCount=0`以防止[SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework)从挂起。</span><span class="sxs-lookup"><span data-stu-id="7fd16-231">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="7fd16-232">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="7fd16-232">SQL Server Express LocalDB</span></span>

<span data-ttu-id="7fd16-233">连接字符串指定 SQL Server LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-233">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="7fd16-234">LocalDB 是 SQL Server Express 数据库引擎的轻量级版本，用于应用程序开发，不生产环境中使用。</span><span class="sxs-lookup"><span data-stu-id="7fd16-234">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="7fd16-235">LocalDB 按需启动并在用户模式下运行，因此没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="7fd16-235">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="7fd16-236">默认情况下，创建 LocalDB *.mdf* DB 文件中`C:/Users/<user>`目录。</span><span class="sxs-lookup"><span data-stu-id="7fd16-236">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="7fd16-237">添加代码以初始化使用测试数据的数据库</span><span class="sxs-lookup"><span data-stu-id="7fd16-237">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="7fd16-238">EF 核心创建空数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-238">EF Core creates an empty DB.</span></span> <span data-ttu-id="7fd16-239">在本部分中，*种子*方法编写要测试数据填充它。</span><span class="sxs-lookup"><span data-stu-id="7fd16-239">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="7fd16-240">在*数据*文件夹中，创建名为的新类文件*DbInitializer.cs*并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fd16-240">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="7fd16-241">代码将检查数据库中是否存在任何学生。</span><span class="sxs-lookup"><span data-stu-id="7fd16-241">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="7fd16-242">如果在数据库中不有任何学生，数据库设置种子值使用测试数据。</span><span class="sxs-lookup"><span data-stu-id="7fd16-242">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="7fd16-243">它将测试数据加载到数组而不是`List<T>`集合来优化性能。</span><span class="sxs-lookup"><span data-stu-id="7fd16-243">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="7fd16-244">`EnsureCreated`方法自动创建的数据库上下文 DB。</span><span class="sxs-lookup"><span data-stu-id="7fd16-244">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="7fd16-245">如果 DB 存在，`EnsureCreated`返回而不修改数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-245">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="7fd16-246">在*Program.cs*，修改`Main`方法来执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7fd16-246">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="7fd16-247">从依赖关系注入容器获取 DB 上下文实例。</span><span class="sxs-lookup"><span data-stu-id="7fd16-247">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="7fd16-248">调用 seed 方法，将上下文传递到它。</span><span class="sxs-lookup"><span data-stu-id="7fd16-248">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="7fd16-249">Seed 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="7fd16-249">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="7fd16-250">下面的代码演示更新*Program.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="7fd16-250">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="7fd16-251">第一次运行该应用程序，数据库是创建并使用测试数据设定种子。</span><span class="sxs-lookup"><span data-stu-id="7fd16-251">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="7fd16-252">更新数据模型时：</span><span class="sxs-lookup"><span data-stu-id="7fd16-252">When the data model is updated:</span></span>
* <span data-ttu-id="7fd16-253">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-253">Delete the DB.</span></span>
* <span data-ttu-id="7fd16-254">更新的 seed 方法。</span><span class="sxs-lookup"><span data-stu-id="7fd16-254">Update the seed method.</span></span>
* <span data-ttu-id="7fd16-255">运行应用并创建新的植入的 DB。</span><span class="sxs-lookup"><span data-stu-id="7fd16-255">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="7fd16-256">在更高版本的教程中，在数据模型更改，而无需删除并重新创建数据库时，被更新数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-256">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="7fd16-257">添加基架工具</span><span class="sxs-lookup"><span data-stu-id="7fd16-257">Add scaffold tooling</span></span>

<span data-ttu-id="7fd16-258">在本部分中，包管理器控制台 (PMC) 用于添加的 Visual Studio web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="7fd16-258">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="7fd16-259">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="7fd16-259">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="7fd16-260">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="7fd16-260">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="7fd16-261">在包管理器控制台 (PMC) 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7fd16-261">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="7fd16-262">前一个命令将 NuGet 包添加到 *.csproj 文件中：</span><span class="sxs-lookup"><span data-stu-id="7fd16-262">The previous command adds the NuGet packages to the *.csproj file:</span></span>

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="7fd16-263">基架模型</span><span class="sxs-lookup"><span data-stu-id="7fd16-263">Scaffold the model</span></span>

* <span data-ttu-id="7fd16-264">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="7fd16-264">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="7fd16-265">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7fd16-265">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
<span data-ttu-id="7fd16-266">如果生成以下错误：</span><span class="sxs-lookup"><span data-stu-id="7fd16-266">If the following error is generated:</span></span>

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

<span data-ttu-id="7fd16-267">再次运行该命令并保留在页面底部的注释。</span><span class="sxs-lookup"><span data-stu-id="7fd16-267">Run the command again and leave a comment at the bottom of the page.</span></span>

<span data-ttu-id="7fd16-268">生成项目。</span><span class="sxs-lookup"><span data-stu-id="7fd16-268">Build the project.</span></span> <span data-ttu-id="7fd16-269">生成将生成如下所示的错误：</span><span class="sxs-lookup"><span data-stu-id="7fd16-269">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="7fd16-270">全局更改`_context.Student`到`_context.Students`(即，将"s"添加到`Student`)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-270">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="7fd16-271">7 匹配项的发现和更新。</span><span class="sxs-lookup"><span data-stu-id="7fd16-271">7 occurrences are found and updated.</span></span> <span data-ttu-id="7fd16-272">我们希望修复[此 bug](https://github.com/aspnet/Scaffolding/issues/633)下一个版本中。</span><span class="sxs-lookup"><span data-stu-id="7fd16-272">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="7fd16-273">测试应用</span><span class="sxs-lookup"><span data-stu-id="7fd16-273">Test the app</span></span>

<span data-ttu-id="7fd16-274">运行应用并选择**学生**链接。</span><span class="sxs-lookup"><span data-stu-id="7fd16-274">Run the app and select the **Students** link.</span></span> <span data-ttu-id="7fd16-275">具体取决于浏览器宽度，**学生**链接将显示在页面顶部。</span><span class="sxs-lookup"><span data-stu-id="7fd16-275">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="7fd16-276">如果**学生**链接不可见，请单击右上角中的导航图标。</span><span class="sxs-lookup"><span data-stu-id="7fd16-276">If the **Students** link is not visible, click the navigation icon in the upper right corner.</span></span>

![窄的 Contoso 大学主页](intro/_static/home-page-narrow.png)

<span data-ttu-id="7fd16-278">测试**创建**，**编辑**，和**详细信息**链接。</span><span class="sxs-lookup"><span data-stu-id="7fd16-278">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="7fd16-279">查看数据库</span><span class="sxs-lookup"><span data-stu-id="7fd16-279">View the DB</span></span>

<span data-ttu-id="7fd16-280">当启动应用程序时，`DbInitializer.Initialize`调用`EnsureCreated`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-280">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="7fd16-281">`EnsureCreated`检测到如果 DB 存在，并且如有必要将创建一个。</span><span class="sxs-lookup"><span data-stu-id="7fd16-281">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="7fd16-282">如果 DB 中, 不有任何学生`Initialize`方法将添加学生。</span><span class="sxs-lookup"><span data-stu-id="7fd16-282">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="7fd16-283">打开**SQL Server 对象资源管理器**(SSOX) 从**视图**Visual Studio 中的菜单。</span><span class="sxs-lookup"><span data-stu-id="7fd16-283">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="7fd16-284">在 SSOX 中，单击**(localdb) \MSSQLLocalDB > 数据库 > ContosoUniversity1**。</span><span class="sxs-lookup"><span data-stu-id="7fd16-284">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="7fd16-285">展开**表**节点。</span><span class="sxs-lookup"><span data-stu-id="7fd16-285">Expand the **Tables** node.</span></span>

<span data-ttu-id="7fd16-286">右键单击**学生**表，然后单击**查看数据**以查看创建的列和插入到表的行。</span><span class="sxs-lookup"><span data-stu-id="7fd16-286">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="7fd16-287">*.Mdf*和*.ldf* DB 文件位于*C:\Users\<yourusername >*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7fd16-287">The *.mdf* and *.ldf* DB files are in the *C:\Users\<yourusername>* folder.</span></span>

<span data-ttu-id="7fd16-288">`EnsureCreated`称为应用程序启动，允许以下工作流：</span><span class="sxs-lookup"><span data-stu-id="7fd16-288">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="7fd16-289">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd16-289">Delete the DB.</span></span>
* <span data-ttu-id="7fd16-290">更改数据库架构 (例如，添加`EmailAddress`字段)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-290">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="7fd16-291">运行应用。</span><span class="sxs-lookup"><span data-stu-id="7fd16-291">Run the app.</span></span>

<span data-ttu-id="7fd16-292">`EnsureCreated`创建与 DB`EmailAddress`列。</span><span class="sxs-lookup"><span data-stu-id="7fd16-292">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="7fd16-293">约定</span><span class="sxs-lookup"><span data-stu-id="7fd16-293">Conventions</span></span>

<span data-ttu-id="7fd16-294">为了使 EF 核心以创建完整数据库编写量是代码的最小因为使用的约定，或者使 EF 核心的假设。</span><span class="sxs-lookup"><span data-stu-id="7fd16-294">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="7fd16-295">名称`DbSet`属性用作表名。</span><span class="sxs-lookup"><span data-stu-id="7fd16-295">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="7fd16-296">未被引用的实体`DbSet`属性，实体类名称用作表名称。</span><span class="sxs-lookup"><span data-stu-id="7fd16-296">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="7fd16-297">实体属性名称用于列名称。</span><span class="sxs-lookup"><span data-stu-id="7fd16-297">Entity property names are used for column names.</span></span>

* <span data-ttu-id="7fd16-298">ID 或 classnameID 命名的实体属性被识别为主键属性。</span><span class="sxs-lookup"><span data-stu-id="7fd16-298">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="7fd16-299">如果它名为属性将被解释为外键属性 *<navigation property name> <primary key property name>*  (例如，`StudentID`为`Student`以来的导航属性`Student`实体的主键是`ID`).</span><span class="sxs-lookup"><span data-stu-id="7fd16-299">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="7fd16-300">可以命名外键属性 *<primary key property name>*  (例如，`EnrollmentID`由于`Enrollment`实体的主键是`EnrollmentID`)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-300">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="7fd16-301">可以重写常规行为。</span><span class="sxs-lookup"><span data-stu-id="7fd16-301">Conventional behavior can be overridden.</span></span> <span data-ttu-id="7fd16-302">例如，表名称可以显式指定，本教程中前面所示。</span><span class="sxs-lookup"><span data-stu-id="7fd16-302">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="7fd16-303">可以显式设置的列名称。</span><span class="sxs-lookup"><span data-stu-id="7fd16-303">The column names can be explicitly set.</span></span> <span data-ttu-id="7fd16-304">可以显式设置主键和外键。</span><span class="sxs-lookup"><span data-stu-id="7fd16-304">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="7fd16-305">异步代码</span><span class="sxs-lookup"><span data-stu-id="7fd16-305">Asynchronous code</span></span>

<span data-ttu-id="7fd16-306">异步编程是 ASP.NET Core 和 EF 核心的默认模式。</span><span class="sxs-lookup"><span data-stu-id="7fd16-306">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="7fd16-307">Web 服务器具有有限的数量的线程可用，并且在高负载情况下的所有可用线程可能正在使用。</span><span class="sxs-lookup"><span data-stu-id="7fd16-307">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="7fd16-308">在这种情况，服务器无法处理新请求，直到线程会被释放。</span><span class="sxs-lookup"><span data-stu-id="7fd16-308">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="7fd16-309">与同步代码，多个线程可能会占用时它们实际上不执行任何操作，因为它们正在等待 I/O 完成。</span><span class="sxs-lookup"><span data-stu-id="7fd16-309">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="7fd16-310">与异步代码时进程正在等待 I/O 完成，将其线程被释放服务器用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="7fd16-310">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="7fd16-311">因此，异步代码启用更有效地使用服务器资源，并启用该服务器以处理更多流量不会延迟。</span><span class="sxs-lookup"><span data-stu-id="7fd16-311">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="7fd16-312">异步代码会在运行时引入的少量开销。</span><span class="sxs-lookup"><span data-stu-id="7fd16-312">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="7fd16-313">低流量情况下，性能命中可以忽略不计，时的高流量情况下，此潜在的性能改进非常大量。</span><span class="sxs-lookup"><span data-stu-id="7fd16-313">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="7fd16-314">在下面的代码中，`async`关键字，`Task<T>`返回值，`await`关键字，和`ToListAsync`方法使代码异步执行。</span><span class="sxs-lookup"><span data-stu-id="7fd16-314">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="7fd16-315">`async`关键字告知编译器对：</span><span class="sxs-lookup"><span data-stu-id="7fd16-315">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="7fd16-316">生成方法体的部分的回调。</span><span class="sxs-lookup"><span data-stu-id="7fd16-316">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="7fd16-317">自动创建[任务](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7)返回的对象。</span><span class="sxs-lookup"><span data-stu-id="7fd16-317">Automatically create the [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that is returned.</span></span> <span data-ttu-id="7fd16-318">有关详细信息，请参阅[任务返回类型](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-318">For more information, see [Task Return Type](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="7fd16-319">隐式返回类型`Task`表示正在进行的工作。</span><span class="sxs-lookup"><span data-stu-id="7fd16-319">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="7fd16-320">`await`关键字会导致编译器拆分为两个部分的方法。</span><span class="sxs-lookup"><span data-stu-id="7fd16-320">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="7fd16-321">第一部分结尾以异步方式启动该操作。</span><span class="sxs-lookup"><span data-stu-id="7fd16-321">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="7fd16-322">第二部分被放入操作完成时调用的回调方法。</span><span class="sxs-lookup"><span data-stu-id="7fd16-322">The second part is put into a callback method that is called when the operation completes.</span></span>

* <span data-ttu-id="7fd16-323">`ToListAsync`是的异步版本`ToList`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="7fd16-323">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="7fd16-324">编写异步代码，使用 EF 核心时考虑的一些事项：</span><span class="sxs-lookup"><span data-stu-id="7fd16-324">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="7fd16-325">以异步方式执行导致查询或命令发送到数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="7fd16-325">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="7fd16-326">这包括`ToListAsync`， `SingleOrDefaultAsync`， `FirstOrDefaultAsync`，和`SaveChangesAsync`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-326">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="7fd16-327">它不包括只需更改的语句`IQueryable`，如`var students = context.Students.Where(s => s.LastName == "Davolio")`。</span><span class="sxs-lookup"><span data-stu-id="7fd16-327">It does not include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="7fd16-328">EF 核心上下文不线程安全： 请勿尝试执行并行的多个操作。</span><span class="sxs-lookup"><span data-stu-id="7fd16-328">An EF Core context is not threaded safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="7fd16-329">若要充分利用异步代码的性能优势，请验证库包 （如分页），是否它们调用将查询发送到数据库的 EF 核心方法中使用异步。</span><span class="sxs-lookup"><span data-stu-id="7fd16-329">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="7fd16-330">有关在.NET 中的异步编程的详细信息，请参阅[异步概述](https://docs.microsoft.com/dotnet/articles/standard/async)。</span><span class="sxs-lookup"><span data-stu-id="7fd16-330">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="7fd16-331">在下一步的教程中，基本的 CRUD （创建、 读取、 更新、 删除） 操作进行检查。</span><span class="sxs-lookup"><span data-stu-id="7fd16-331">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="7fd16-332">下一篇</span><span class="sxs-lookup"><span data-stu-id="7fd16-332">Next</span></span>](xref:data/ef-rp/crud)
