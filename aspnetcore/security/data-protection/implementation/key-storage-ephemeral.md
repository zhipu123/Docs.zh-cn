---
title: "临时数据保护提供程序"
author: rick-anderson
description: "本文档介绍了 ASP.NET 核心暂时数据保护提供程序实现详细信息。"
keywords: "ASP.NET 核心，数据保护、 暂时的提供程序"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: af6ea1d0-0d9d-41df-a870-5dda24978e2f
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: 51d4aaa3a669763c2e388a8186ebeaec6b57e77a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="ephemeral-data-protection-providers"></a><span data-ttu-id="1a166-104">临时数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="1a166-104">Ephemeral data protection providers</span></span>

<a name="data-protection-implementation-key-storage-ephemeral"></a>

<span data-ttu-id="1a166-105">有的方案： 应用程序需要的 throwaway `IDataProtectionProvider`。</span><span class="sxs-lookup"><span data-stu-id="1a166-105">There are scenarios where an application needs a throwaway `IDataProtectionProvider`.</span></span> <span data-ttu-id="1a166-106">例如，开发人员可能只需在一次性的控制台应用程序中，进行试验或应用程序本身是暂时性 （已编写脚本或单元测试项目）。</span><span class="sxs-lookup"><span data-stu-id="1a166-106">For example, the developer might just be experimenting in a one-off console application, or the application itself is transient (it's scripted or a unit test project).</span></span> <span data-ttu-id="1a166-107">若要支持这些方案[Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/)包包括一种类型`EphemeralDataProtectionProvider`。</span><span class="sxs-lookup"><span data-stu-id="1a166-107">To support these scenarios the [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) package includes a type `EphemeralDataProtectionProvider`.</span></span> <span data-ttu-id="1a166-108">此类型提供的基本实现`IDataProtectionProvider`其密钥的存储库保留仅在内存中和不写出到任何后备存储。</span><span class="sxs-lookup"><span data-stu-id="1a166-108">This type provides a basic implementation of `IDataProtectionProvider` whose key repository is held solely in-memory and isn't written out to any backing store.</span></span>

<span data-ttu-id="1a166-109">每个实例`EphemeralDataProtectionProvider`使用其自身唯一的主密钥。</span><span class="sxs-lookup"><span data-stu-id="1a166-109">Each instance of `EphemeralDataProtectionProvider` uses its own unique master key.</span></span> <span data-ttu-id="1a166-110">因此，如果`IDataProtector`处`EphemeralDataProtectionProvider`生成受保护的负载，该负载仅受等效`IDataProtector`(给定相同[目的](../consumer-apis/purpose-strings.md#data-protection-consumer-apis-purposes)链) 位于同一个取得 root 权限`EphemeralDataProtectionProvider`实例。</span><span class="sxs-lookup"><span data-stu-id="1a166-110">Therefore, if an `IDataProtector` rooted at an `EphemeralDataProtectionProvider` generates a protected payload, that payload can only be unprotected by an equivalent `IDataProtector` (given the same [purpose](../consumer-apis/purpose-strings.md#data-protection-consumer-apis-purposes) chain) rooted at the same `EphemeralDataProtectionProvider` instance.</span></span>

<span data-ttu-id="1a166-111">下面的示例演示如何实例化`EphemeralDataProtectionProvider`并使用它来保护和取消保护数据。</span><span class="sxs-lookup"><span data-stu-id="1a166-111">The following sample demonstrates instantiating an `EphemeralDataProtectionProvider` and using it to protect and unprotect data.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
