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
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a>Met behulp van REST tooaccess Azure Mobile Engagement Service API 's
Azure Mobile Engagement biedt Hallo [REST-API van Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) u toomanage apparaten/te pushen Reach-campagnes enzovoort.

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

Als u toouse Hallo REST-API's niet rechtstreeks wilt, bieden we ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) die u met gebruiken kunt hulpprogramma's voor toogenerate SDK's voor uw voorkeurstaal. Aangeraden wordt Hallo [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma toogenerate uw SDK uit onze Swagger-bestand. We hebben een .NET SDK gemaakt op een vergelijkbare manier waarmee u kunt toointeract met deze API's met behulp van een C#-wrapper en u hebt geen toodo Hallo verificatie token onderhandeling en uzelf te vernieuwen. Zie [Service API .NET SDK-voorbeeld](mobile-engagement-dotnet-sdk-service-api.md) toolearn hoe toouse .net SDK Hallo voor API
