---
title: Met behulp van de REST-API voor toegang tot Azure Mobile Engagement Service API 's
description: Hierin wordt beschreven hoe u de Mobile Engagement REST-API's gebruiken voor toegang tot Azure Mobile Engagement Service API 's
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="56943-103">Met behulp van de REST voor toegang tot Azure Mobile Engagement Service API 's</span><span class="sxs-lookup"><span data-stu-id="56943-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="56943-104">Azure Mobile Engagement biedt de [REST-API van Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) kunt beheren apparaten/te pushen Reach-campagnes enzovoort.</span><span class="sxs-lookup"><span data-stu-id="56943-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="56943-105">De Azure Mobile Engagement-service wordt in maart 2018 beëindigd en is momenteel alleen beschikbaar voor bestaande klanten.</span><span class="sxs-lookup"><span data-stu-id="56943-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="56943-106">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="56943-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="56943-107">Als u niet rechtstreeks gebruik van de REST API's wilt, bieden we ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) waarmee u met hulpprogramma's kunt voor het genereren van SDK's voor uw voorkeurstaal.</span><span class="sxs-lookup"><span data-stu-id="56943-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="56943-108">Wordt u aangeraden de [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma voor het genereren van de SDK van onze Swagger-bestand.</span><span class="sxs-lookup"><span data-stu-id="56943-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="56943-109">We hebben een .NET-SDK op een vergelijkbare manier waarmee u communiceren met deze API's met behulp van een C#-wrapper gemaakt en u hoeft te doen de token verificatie-onderhandeling en vernieuw zelf.</span><span class="sxs-lookup"><span data-stu-id="56943-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="56943-110">Zie [Service API .NET SDK-voorbeeld](mobile-engagement-dotnet-sdk-service-api.md) voor informatie over het gebruik van de .net SDK voor API</span><span class="sxs-lookup"><span data-stu-id="56943-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>
