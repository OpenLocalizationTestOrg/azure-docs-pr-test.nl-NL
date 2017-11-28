---
title: aaaUsing hello REST-API tooaccess Azure Mobile Engagement Service API 's
description: Hierin wordt beschreven hoe toouse Hallo Mobile Engagement REST-API's tooaccess Azure Mobile Engagement Service API 's
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="a0d7f-103">Met behulp van REST tooaccess Azure Mobile Engagement Service API 's</span><span class="sxs-lookup"><span data-stu-id="a0d7f-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="a0d7f-104">Azure Mobile Engagement biedt Hallo [REST-API van Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) u toomanage apparaten/te pushen Reach-campagnes enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="a0d7f-105">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="a0d7f-106">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="a0d7f-107">Als u toouse Hallo REST-API's niet rechtstreeks wilt, bieden we ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) die u met gebruiken kunt hulpprogramma's voor toogenerate SDK's voor uw voorkeurstaal.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="a0d7f-108">Aangeraden wordt Hallo [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma toogenerate uw SDK uit onze Swagger-bestand.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="a0d7f-109">We hebben een .NET SDK gemaakt op een vergelijkbare manier waarmee u kunt toointeract met deze API's met behulp van een C#-wrapper en u hebt geen toodo Hallo verificatie token onderhandeling en uzelf te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="a0d7f-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="a0d7f-110">Zie [Service API .NET SDK-voorbeeld](mobile-engagement-dotnet-sdk-service-api.md) toolearn hoe toouse .net SDK Hallo voor API</span><span class="sxs-lookup"><span data-stu-id="a0d7f-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
