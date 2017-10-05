---
title: Web-App Resources verplaatsen naar een andere resourcegroep
description: Beschrijft de scenario's waarin kunt u Web-Apps en App-Services van een resourcegroep naar een andere.
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
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="15c82-103">Ondersteunde Move-configuraties</span><span class="sxs-lookup"><span data-stu-id="15c82-103">Supported Move Configurations</span></span>
<span data-ttu-id="15c82-104">Kunt u Web-App van Azure-resources met behulp van de [Resource Manager verplaatsen Resources API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="15c82-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="15c82-105">Azure Web Apps biedt momenteel ondersteuning voor de volgende move-scenario's:</span><span class="sxs-lookup"><span data-stu-id="15c82-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="15c82-106">De volledige inhoud van een resourcegroep (web-apps, app service-abonnementen en certificaten) naar een andere resourcegroep verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="15c82-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="15c82-107">De resourcegroep voor de bestemming kan geen Microsoft.Web bronnen in dit scenario bevatten.</span><span class="sxs-lookup"><span data-stu-id="15c82-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="15c82-108">Afzonderlijke web-apps naar een andere resourcegroep verplaatsen tijdens het hosten van ze nog steeds in de huidige app service-abonnement (het app service-abonnement blijft in de oude resourcegroep).</span><span class="sxs-lookup"><span data-stu-id="15c82-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


