---
title: aaaCreate een functie-app van hello Azure Portal | Microsoft Docs
description: Een nieuwe functie-app maken in Azure App Service vanuit Hallo-portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="99559-103">Een functie-app maken vanuit hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="99559-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="99559-104">Apps van Azure functie maakt gebruik van hello Azure App Service-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="99559-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="99559-105">Dit onderwerp leest u hoe toocreate een functie-app in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="99559-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="99559-106">Een functie-app is Hallo-container die als host fungeert voor Hallo uitvoering van afzonderlijke functies.</span><span class="sxs-lookup"><span data-stu-id="99559-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="99559-107">Wanneer u een functie-app in Hallo hosting App Service-abonnement maakt, kan uw app in de functie alle Hallo functies van App Service kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99559-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="99559-108">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="99559-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="99559-109">Wanneer u een functie-app maakt, Geef een geldige **appnaam**, die kunnen alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="99559-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="99559-110">Het onderstrepingsteken (**_**) is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="99559-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="99559-111">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="99559-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="99559-112">De naam van uw opslagaccount moet uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="99559-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="99559-113">Nadat Hallo functie-app is gemaakt, kunt u afzonderlijke functies in een of meer verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="99559-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="99559-114">Functies maken [met behulp van de portal Hallo](functions-create-first-azure-function.md#create-function), [continue implementatie](functions-continuous-deployment.md), of door [uploaden met FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="99559-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="99559-115">Service-plannen</span><span class="sxs-lookup"><span data-stu-id="99559-115">Service plans</span></span>

<span data-ttu-id="99559-116">Azure Functions heeft twee verschillende serviceplannen: verbruik plannings- en App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="99559-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="99559-117">rekencapaciteit Hallo verbruik plan automatisch toegewezen wanneer uw code wordt uitgevoerd, kan worden geschaald-out als nodig toohandle laden, en vervolgens kan worden geschaald in wanneer de code wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99559-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="99559-118">Hallo App Service-abonnement geeft de functie app toegang tooall Hallo faciliteiten van App Service.</span><span class="sxs-lookup"><span data-stu-id="99559-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="99559-119">Als de functie-app wordt gemaakt en kan niet op dit moment worden gewijzigd, moet u uw service-abonnement kiezen.</span><span class="sxs-lookup"><span data-stu-id="99559-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="99559-120">Zie voor meer informatie [Kies een Azure-functies die als host fungeert voor plan](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="99559-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="99559-121">Als u van plan bent toorun JavaScript-functies op een App Service-abonnement, moet u een plan met minder cores kiezen.</span><span class="sxs-lookup"><span data-stu-id="99559-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="99559-122">Zie voor meer informatie, Hallo [verwijzing in JavaScript voor functies](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="99559-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="99559-123">Opslagvereisten voor account</span><span class="sxs-lookup"><span data-stu-id="99559-123">Storage account requirements</span></span>

<span data-ttu-id="99559-124">Wanneer u een functie-app in App Service, moet u maken of tooa voor algemene doeleinden Azure Storage-account koppelen die ondersteuning biedt voor opslag voor blobs, wachtrijen en tabellen.</span><span class="sxs-lookup"><span data-stu-id="99559-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="99559-125">Intern functies opslagruimte gebruikt voor bewerkingen zoals het beheren van triggers en functies die logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="99559-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="99559-126">Sommige opslagaccounts bieden geen ondersteuning voor wachtrijen en tabellen, zoals alleen-blob storage-accounts, Azure Premium-opslag en opslagaccounts waarvoor ZRS-replicatie.</span><span class="sxs-lookup"><span data-stu-id="99559-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="99559-127">Deze accounts worden gefilterd van Hallo Opslagaccount blade bij het maken van een functie-app.</span><span class="sxs-lookup"><span data-stu-id="99559-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="99559-128">Wanneer u Hallo verbruik hosting plan, wordt de functie code en binding configuratiebestanden worden opgeslagen in Azure File storage in Hallo belangrijkste storage-account.</span><span class="sxs-lookup"><span data-stu-id="99559-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="99559-129">Wanneer u de belangrijkste opslagaccount Hallo verwijdert, wordt deze inhoud is verwijderd en kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="99559-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="99559-130">toolearn meer informatie over opslagaccounttypen, Zie [Introducing hello Azure Storage-Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="99559-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="99559-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99559-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



