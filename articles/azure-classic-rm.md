---
title: Resource Manager en Service Management (klassiek) implementatiemodi | Microsoft Docs
description: Meer informatie over de verschillen tussen Resource Manager en het klassieke implementatiemodel.
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: 0f451efa239dd36d82229f01cc385d6df46654f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-deployment-models"></a>Azure-implementatiemodellen
De Azure-platform is in de overgangsfase.  Of u niet vertrouwd met Azure bent of u hebt gebruikt het jaar, is het belangrijk te weten van enkele van de belangrijkste wijzigingen die we om het platform tijdens deze overgang doorvoeren.

Alle Azure-resources bieden ondersteuning voor een of beide van de volgende implementatiemodellen:

* **Resource Manager:** dit is het nieuwste implementatiemodel voor Azure-resources. De meeste nieuwere resources bieden al ondersteuning voor dit implementatiemodel en uiteindelijk alle resources wordt.   
* **Klassieke:** dit model wordt ondersteund door de meeste bestaande Azure-resources vandaag. Nieuwe resources toegevoegd aan Azure biedt geen ondersteuning voor dit model.

De documentatie voor elk Azure-resource-informatie welke service het model kan worden gemaakt met.

## <a name="why-does-this-matter"></a>Waarom wordt deze kwestie?
Het is van belang om de volgende redenen:

* De Azure-platform-functies waarmee u verschillen tussen deze twee modellen.  Bijvoorbeeld, de resources die zijn gemaakt met behulp van de Resource Manager-implementatiemodel (of alleen Resource Manager) kunnen worden gemaakt met [Azure Resource Manager-sjablonen](azure-resource-manager/resource-group-overview.md#template-deployment), terwijl dit niet resources die zijn gemaakt met het klassieke implementatiemodel.
* De Azure-resource afzonderlijke functies of gedragingen worden verschillende tussen de twee modellen of bestaan alleen in één model of de andere.  Verkeer voor taakverdeling over virtuele machines die zijn gemaakt met het klassieke implementatiemodel is bijvoorbeeld *impliciete* omdat virtuele machines deel van een Azure Cloud Service uitmaken en wordt automatisch taakverdeling in virtuele machines binnen een cloudservice. Virtuele machines die zijn gemaakt met Resource Manager zijn geen leden van een cloudservice en moet een afzonderlijke Azure Load Balancer-resource *expliciet* samengesteld en taken te verdelen voor verkeer over meerdere virtuele machines.  
* Hoe u maken, configureren en beheren van uw Azure-resources is verschil is tussen deze twee modellen.
* Resources die zijn gemaakt met een implementatiemodel kunnen niet per se samenwerken met bronnen die zijn gemaakt met een andere implementatiemodel. Azure Virtual Machines is gemaakt met een implementatiemodel kan bijvoorbeeld alleen worden verbonden met virtuele netwerken van Azure die zijn gemaakt met behulp van hetzelfde implementatiemodel.    

Elk van de implementatiemodellen onderliggende is een application programming interface (API) voor elke resource.  Er is een [Resource Manager-API](https://msdn.microsoft.com/library/azure/dn948464.aspx) voor het Resource Manager-implementatiemodel en een [Service Management API](https://msdn.microsoft.com/library/azure/ee460799.aspx) voor het klassieke implementatiemodel. Ontwikkelaars kunnen code schrijven om te communiceren met deze API's *rechtstreeks*.  

IT-professionals echter meestal communiceren met deze API's *indirect* met behulp van een grafische portal in een webbrowser, met behulp van Azure PowerShell-cmdlets op een Windows-computer of met behulp van de Azure-opdrachtregelinterface (CLI) op een Windows , OS X- of Linux-computer. Alle drie deze indirecte methoden die worden gebruikt door de IT-Professional communiceren rechtstreeks met de API's. Dit betekent dat wanneer nieuwe functionaliteit wordt toegevoegd aan de Azure-platform of resources, het altijd direct beschikbaar via de API eerst met de indirecte methoden ondersteuning voor de nieuwe resources en de functies krijgt is nadat de API beschikbaar is gemaakt.  

De volgende secties wordt uitgelegd hoe Azure-resources met behulp van de verschillende implementatiemodellen via de drie indirecte methoden zijn geconfigureerd.

## <a name="portals"></a>Portals
Azure heeft twee portals:

* **[Azure-portal](https://manage.windowsazure.com):** als u Azure hebt met een tijdje, hebt u deze portal gebruikt. Deze wordt gebruikt voor het maken en oudere Azure-resources die ondersteuning bieden voor het klassieke implementatiemodel configureren. U kunt deze niet gebruiken om te maken of configureren van de resources die alleen ondersteuning voor Resource Manager. 
* **[Azure preview-portal](https://azure.microsoft.com/overview/preview-portal/):** als u een nieuwere Azure-resource, hebt u waarschijnlijk deze portal gebruikt. Het kan worden gebruikt voor het maken en configureren van Azure-resources. Uiteindelijk zult u maken en alle Azure-resources configureren met het. Voor bepaalde bronnen die ondersteuning bieden voor beide implementatiemodellen, kan deze portal worden gebruikt voor het maken en configureren van een resource met een implementatiemodel. 

Sommige resources en functies kunnen alleen worden gemaakt en geconfigureerd in één portal of de andere. Sommige resources of functies (nog) kunnen niet worden gemaakt of geconfigureerd in de portal en kan alleen worden geconfigureerd met PowerShell of de CLI. Welke methode kan worden gemaakt met details over de documentatie voor elk Azure-resource. 

## <a name="powershell"></a>PowerShell
Met [PowerShell](/powershell/azureps-cmdlets-docs) kunt u scripts maken en configureren van een computer met Windows Azure-resources maken of een opdrachtregel gebruiken.  Afzonderlijke Azure-resources hebt [Resource Manager-cmdlets](/powershell/azure/overview), [Service Management-cmdlets](/powershell/azure/overview?view=azuresmps-3.7.0), of beide.  Sommige resources en functies kunnen alleen worden gemaakt en/of geconfigureerd met behulp van PowerShell of de CLI. Afhankelijk van de resource bij gebruik van Resource Manager PowerShell-cmdlets wellicht hebt u twee opties voor het maken en configureren van Azure-resources:

* **PowerShell-cmdlets:** u kunt maken en configureren van elke Azure-resource afzonderlijk met de cmdlets voor elke resource. U kunt dit doen vanaf een opdrachtregel of door meerdere opdrachten in een PowerShell-script dat kan worden opgeslagen en -versie.
* **PowerShell-cmdlets met een Azure Resource Manager-sjabloon:** u kunt PowerShell gebruiken voor het maken van Azure-resources met een Azure Resource Manager-sjabloon. Sjablonen kunnen worden opgeslagen en samengestelde. Meer informatie de [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md) artikel. Verschillende [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) bestaan voor algemene oplossingen die kunnen worden gedownload en te worden gewijzigd.

## <a name="cli"></a>CLI
U kunt maken en configureren van Azure-resources van Windows-, OS X- of Linux-computers met behulp van de CLI.  Lees de [Azure CLI installeren](cli-install-nodejs.md) artikel de CLI installeren op uw besturingssysteem naar keuze. Zoals PowerShell, zijn er verschillende opdrachten die moeten worden gebruikt, afhankelijk van of u resources met behulp van [Resource Manager](xplat-cli-azure-resource-manager.md) of de [klassieke (Service Management)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) implementatiemodellen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Begrijpen hoe [sjablonen ontwerpen](best-practices-resource-manager-design-templates.md).

