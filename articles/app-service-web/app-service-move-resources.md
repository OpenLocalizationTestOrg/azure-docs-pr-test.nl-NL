---
title: aaaMove bronnen voor Web-App tooanother resourcegroep
description: Hallo-scenario's waarin u Web-Apps en App-Services van een resourcegroep tooanother verplaatsen kunt beschrijft.
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="12b2d-103">Ondersteunde Move-configuraties</span><span class="sxs-lookup"><span data-stu-id="12b2d-103">Supported Move Configurations</span></span>
<span data-ttu-id="12b2d-104">U kunt Azure-Web-App-resources met behulp van Hallo verplaatsen [Resource Manager verplaatsen Resources API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="12b2d-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="12b2d-105">Azure Web Apps ondersteunt momenteel Hallo verplaatsen scenario's te volgen:</span><span class="sxs-lookup"><span data-stu-id="12b2d-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="12b2d-106">Hallo volledige inhoud van een resourcegroep (web-apps, app service-abonnementen en certificaten) verplaatsen tooanother resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="12b2d-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="12b2d-107">Hallo bestemming resourcegroep mag niet Microsoft.Web bronnen in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="12b2d-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="12b2d-108">Afzonderlijke web apps tooa andere resourcegroep verplaatsen tijdens het hosten van ze nog steeds in de huidige app service-abonnement (Hallo-app service plan blijft in de oude resourcegroep Hallo).</span><span class="sxs-lookup"><span data-stu-id="12b2d-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


