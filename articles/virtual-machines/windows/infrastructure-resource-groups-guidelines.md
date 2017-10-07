---
title: aaaResource groepen voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van resourcegroepen in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>Azure resource group richtlijnen voor het Windows-VM 's

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op inzicht in hoe toologically bouwen van uw omgeving en de groep van alle onderdelen van Hallo van resourcegroepen.

## <a name="implementation-guidelines-for-resource-groups"></a>Richtlijnen voor de implementatie voor resourcegroepen
Beslissingen te nemen:

* Gaat u toobuild uit resourcegroepen door Hallo infrastructuur kernonderdelen of door de implementatie van de volledige toepassing?
* Moet u toorestrict toegang tooResource groepen met behulp van toegangsbeheer op basis van rollen?

Taken:

* Wat kernonderdelen van de infrastructuur en resourcegroepen, u moet speciale definiëren.
* Bekijk hoe tooimplement Resource Manager-sjablonen voor consistente, reproduceerbare implementaties.
* Definieer welke gebruikersrollen toegang u voor het beheren van moet toegang tot tooResource groepen.
* Hallo set maken van resourcegroepen met behulp van de naamconventie. U kunt Azure PowerShell of Hallo portal gebruiken.

## <a name="resource-groups"></a>Resourcegroepen
In Azure, u logisch groeperen van gerelateerde resources zoals opslagaccounts, virtuele netwerken en virtuele machines (VM's) toodeploy, beheren en deze als één entiteit te handhaven. Deze aanpak kunt u gemakkelijker toodeploy toepassingen terwijl alle Hallo houden resources samen van een perspectief management of toogrant anderen verwante toegang toothat groep resources. De namen van resourcegroepen kunnen maximaal 90 tekens lang zijn. Lees voor een uitgebreider inzicht van resourcegroepen Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Een belangrijke functie tooResource groepen is mogelijkheid toobuild uit uw omgeving met behulp van sjablonen. Een sjabloon is gewoon een JSON-bestand die wordt gedeclareerd Hallo opslag, netwerken, en bronnen berekenen. U kunt ook alle gerelateerde aangepaste scripts of configuraties tooapply definiëren. Met behulp van deze sjablonen, kunt u consistent reproduceerbare implementaties maken voor uw toepassingen. Deze aanpak kunt u eenvoudig toobuild uit een omgeving in ontwikkeling en gebruik vervolgens die dezelfde sjabloon toocreate een productie-implementatie of vice versa. Lees voor een beter inzicht te krijgen met behulp van sjablonen, [overzicht sjabloon Hallo](../../azure-resource-manager/resource-manager-template-walkthrough.md) die u begeleidt bij elke stap van Hallo opzetten van een sjabloon.

Er zijn twee verschillende benaderingen die u bij het ontwerpen van uw omgeving met resourcegroepen kunt uitvoeren:

* Resourcegroepen voor de implementatie van elke toepassing die Hallo opslagaccounts, virtuele netwerken en subnetten, virtuele machines combineert, load balancers, enzovoort.
* Gecentraliseerde resourcegroepen die uw core virtuele netwerk en de subnetten of de opslag accounts bevatten. Uw toepassingen zijn in hun eigen resourcegroepen die alleen virtuele machines, load balancers, netwerkinterfaces, enzovoort bevatten.

Als u uitschalen, gecentraliseerde resourcegroepen voor uw virtuele netwerken maken en subnetten maakt het eenvoudiger toobuild netwerkverbindingen cross-premises voor hybride verbinding opties. Er is een alternatieve methode Hallo voor elke toepassing toohave hun eigen virtuele netwerk waarvoor de configuratie en het onderhoud.  [Toegangsbeheer op basis van rollen](../../active-directory/role-based-access-control-what-is.md) bieden een gedetailleerde manier toocontrol toegang tooResource groepen. Voor productietoepassingen, kunt u Hallo-gebruikers die toegang deze bronnen tot mogelijk bepalen of voor Hallo core infrastructuurresources kunt u alleen infrastructuur engineers toowork met hen beperken. Uw toepassingseigenaars hebben alleen toegang toohello toepassingsonderdelen in de resourcegroep en geen Hallo core Azure-infrastructuur van uw omgeving. Overweeg het Hallo-gebruikers die toegang tot toohello bronnen nodig hebt en ontwerpen van uw resourcegroepen dienovereenkomstig bij het ontwerpen van uw omgeving. 

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

