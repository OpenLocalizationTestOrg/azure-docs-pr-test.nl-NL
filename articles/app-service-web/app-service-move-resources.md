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
# <a name="supported-move-configurations"></a>Ondersteunde Move-configuraties
U kunt Azure-Web-App-resources met behulp van Hallo verplaatsen [Resource Manager verplaatsen Resources API](../azure-resource-manager/resource-group-move-resources.md).

Azure Web Apps ondersteunt momenteel Hallo verplaatsen scenario's te volgen:

* Hallo volledige inhoud van een resourcegroep (web-apps, app service-abonnementen en certificaten) verplaatsen tooanother resourcegroep. 
   > [!Note]
   > Hallo bestemming resourcegroep mag niet Microsoft.Web bronnen in dit scenario.

* Afzonderlijke web apps tooa andere resourcegroep verplaatsen tijdens het hosten van ze nog steeds in de huidige app service-abonnement (Hallo-app service plan blijft in de oude resourcegroep Hallo).


