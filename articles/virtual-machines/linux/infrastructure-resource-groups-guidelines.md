---
title: Resourcegroepen voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor het implementeren van resourcegroepen in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 452acde571164a3ab4ce2dcccf99d2aed90361fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Azure resource group richtlijnen voor virtuele Linux-machines 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het logisch bouwen van uw omgeving en de groep van alle onderdelen van resourcegroepen.

## <a name="implementation-guidelines-for-resource-groups"></a>Richtlijnen voor de implementatie voor resourcegroepen
Beslissingen te nemen:

* Gaat u naar het bouwen van resourcegroepen, door de kernonderdelen van infrastructuur of door de implementatie van de volledige toepassing?
* Moet u de toegang beperken tot resourcegroepen toegangsbeheer op basis van rollen gebruiken?

Taken:

* Wat kernonderdelen van de infrastructuur en resourcegroepen, u moet speciale definiëren.
* Bekijk het implementeren van Resource Manager-sjablonen voor consistente, reproduceerbare implementaties.
* Definieer welke gebruikersrollen voor toegang tot u nodig hebt voor het beheren van toegang tot de resourcegroepen.
* Maak de set met behulp van de naamconventie resourcegroepen. U kunt de Azure CLI of portal gebruiken.

## <a name="resource-groups"></a>Resourcegroepen
In Azure groepeert u logisch gerelateerde resources zoals opslagaccounts, virtuele netwerken en virtuele machines (VM's) te implementeren, beheren en deze als één entiteit te handhaven. Deze aanpak kunt u gemakkelijker om toepassingen te implementeren terwijl de bijbehorende resources samen vanuit het perspectief van een management of andere gebruikers om toegang te verlenen aan die groep van resources. De namen van resourcegroepen kunnen maximaal 90 tekens lang zijn. Voor een uitgebreider inzicht van resourcegroepen, vindt u de [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Een belangrijke functie aan resourcegroepen is de mogelijkheid om te bouwen van uw omgeving met een JSON-bestand dat de opslag, netwerken, declareert en bronnen berekenen. U kunt ook alle gerelateerde aangepaste scripts of configuraties toe te passen definiëren. Met behulp van deze JSON-sjablonen, kunt u consistent reproduceerbare implementaties maken voor uw toepassingen. Deze benadering kunt u bij het bouwen van een omgeving in ontwikkeling en gebruik vervolgens dezelfde sjabloon voor het maken van een productie-implementatie of vice versa. Lees voor een beter begrip over met behulp van sjablonen, [het overzicht van de sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md) die u begeleidt bij elke stap van het opzetten van een JSON-sjabloon.

Er zijn twee verschillende benaderingen die u bij het ontwerpen van uw omgeving met resourcegroepen kunt uitvoeren:

* Resourcegroepen voor de implementatie van elke toepassing die de storage-accounts, virtuele netwerken en subnetten, virtuele machines combineert, load balancers, enzovoort.
* Gecentraliseerde resourcegroepen die uw core virtuele netwerk en de subnetten of de opslag accounts bevatten. Uw toepassingen zijn in hun eigen resourcegroepen die alleen virtuele machines, load balancers, netwerkinterfaces, enzovoort bevatten.

Als u scale-out, gecentraliseerde resourcegroepen voor uw virtuele netwerken en subnetten maken het makkelijker wordt om samen te stellen netwerkverbindingen cross-premises voor hybride verbinding opties. Er is een alternatieve methode voor elke toepassing hebben hun eigen virtuele netwerk waarvoor de configuratie en het onderhoud. [Toegangsbeheer op basis van rollen](../../active-directory/role-based-access-control-what-is.md) bieden een gedetailleerde manier om toegang aan brongroepen te beheren. Voor productietoepassingen, kunt u de gebruikers die toegang deze bronnen tot mogelijk bepalen of voor de infrastructuur core resources beperkt u alleen infrastructuur engineers mee kunt werken. Uw toepassingseigenaars hebben alleen toegang tot de toepassingsonderdelen in de resourcegroep en niet de kern van het Azure-infrastructuur van uw omgeving. U kunt de gebruikers die toegang tot de resources nodig hebt en ontwerpen van uw resourcegroepen dienovereenkomstig bij het ontwerpen van uw omgeving. 

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

