---
title: "ASP.NET Core 中的数据保护"
author: rick-anderson
description: "此文档充当各 ASP.NET Core 数据保护主题的目录。"
keywords: "ASP.NET Core, 数据保护"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 1f402da8-1052-4970-9835-9f9f16a02dbc
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/index
ms.openlocfilehash: 8b42e65bb6121355120a6f4fbe8cd4d1fea153de
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="efd62-104">ASP.NET Core 中的数据保护：使用者 API、配置、扩展性 API 和实现</span><span class="sxs-lookup"><span data-stu-id="efd62-104">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="efd62-105">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="efd62-105">Introduction to Data Protection</span></span>](introduction.md)

* [<span data-ttu-id="efd62-106">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="efd62-106">Getting Started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="efd62-107">使用者 API</span><span class="sxs-lookup"><span data-stu-id="efd62-107">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="efd62-108">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="efd62-108">Consumer APIs Overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="efd62-109">目标字符串</span><span class="sxs-lookup"><span data-stu-id="efd62-109">Purpose Strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="efd62-110">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="efd62-110">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="efd62-111">密码哈希</span><span class="sxs-lookup"><span data-stu-id="efd62-111">Password Hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="efd62-112">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="efd62-112">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="efd62-113">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="efd62-113">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="efd62-114">配置</span><span class="sxs-lookup"><span data-stu-id="efd62-114">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="efd62-115">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="efd62-115">Configuring Data Protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="efd62-116">默认设置</span><span class="sxs-lookup"><span data-stu-id="efd62-116">Default Settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="efd62-117">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="efd62-117">Machine Wide Policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="efd62-118">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="efd62-118">Non DI Aware Scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="efd62-119">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="efd62-119">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="efd62-120">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="efd62-120">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="efd62-121">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="efd62-121">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="efd62-122">其他 API</span><span class="sxs-lookup"><span data-stu-id="efd62-122">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="efd62-123">实现</span><span class="sxs-lookup"><span data-stu-id="efd62-123">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="efd62-124">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="efd62-124">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="efd62-125">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="efd62-125">Subkey Derivation and Authenticated Encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="efd62-126">上下文标头</span><span class="sxs-lookup"><span data-stu-id="efd62-126">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="efd62-127">密钥管理</span><span class="sxs-lookup"><span data-stu-id="efd62-127">Key Management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="efd62-128">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="efd62-128">Key Storage Providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="efd62-129">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="efd62-129">Key Encryption At Rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="efd62-130">密钥永久性和更改设置</span><span class="sxs-lookup"><span data-stu-id="efd62-130">Key Immutability and Changing Settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="efd62-131">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="efd62-131">Key Storage Format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="efd62-132">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="efd62-132">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="efd62-133">兼容性</span><span class="sxs-lookup"><span data-stu-id="efd62-133">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="efd62-134">在应用程序之间共享 cookie</span><span class="sxs-lookup"><span data-stu-id="efd62-134">Sharing cookies between applications</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="efd62-135">在 ASP.NET 中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="efd62-135">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
