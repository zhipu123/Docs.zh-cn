---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: "滑块控件使用自动回发 (VB) |Microsoft 文档"
author: wenz
description: "AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。 它是可以进行滑块自动过帐..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: fedd3ff947c6f5d5d4d00791087e9fd825fdf9d3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="7f645-104">滑块控件使用自动回发 (VB)</span><span class="sxs-lookup"><span data-stu-id="7f645-104">Using the Slider Control With Auto-Postback (VB)</span></span>
====================
<span data-ttu-id="7f645-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7f645-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7f645-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7f645-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="7f645-107">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="7f645-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="7f645-108">它是可以进行滑块有些一次将其值更改。</span><span class="sxs-lookup"><span data-stu-id="7f645-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="7f645-109">概述</span><span class="sxs-lookup"><span data-stu-id="7f645-109">Overview</span></span>

<span data-ttu-id="7f645-110">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="7f645-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="7f645-111">它是可以进行滑块有些一次将其值更改。</span><span class="sxs-lookup"><span data-stu-id="7f645-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="7f645-112">步骤</span><span class="sxs-lookup"><span data-stu-id="7f645-112">Steps</span></span>

<span data-ttu-id="7f645-113">为了使滑块更改时自动回发，两个文本框内需要的特性`AutoPostBack="true"`： 文本框将成为滑块本身，并包含滑块的位置的文本框。</span><span class="sxs-lookup"><span data-stu-id="7f645-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="7f645-114">下面是该所需的标记：</span><span class="sxs-lookup"><span data-stu-id="7f645-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="7f645-115">`SliderExtender` ASP.NET AJAX 控件工具包中的控件将滑块功能分配给两个文本框中：</span><span class="sxs-lookup"><span data-stu-id="7f645-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="7f645-116">其他标签元素以后可用于通知的回发用户：</span><span class="sxs-lookup"><span data-stu-id="7f645-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="7f645-117">最后，`ScriptManager`控件的 ASP.NET AJAX 加载控件工具包工作所需的 JavaScript:</span><span class="sxs-lookup"><span data-stu-id="7f645-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="7f645-118">现在返回; 发布滑块在服务器端，可能捕获到此事件，并采取行动中：</span><span class="sxs-lookup"><span data-stu-id="7f645-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]


<span data-ttu-id="7f645-119">[![将滑块移动触发回发](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7f645-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="7f645-120">将滑块移动触发回发 ([单击以查看实际尺寸的图像](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7f645-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>


<span data-ttu-id="7f645-121">[![然后，此更改的日期写入标签中](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7f645-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="7f645-122">然后，此更改的日期写入标签中 ([单击以查看实际尺寸的图像](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7f645-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="7f645-123">[上一页](databinding-the-slider-control-cs.md)
[下一页](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7f645-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
