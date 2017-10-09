---
title: aaaResource Manager en Service Management (klassiek) implementatiemodi | Microsoft Docs
description: Meer informatie over Hallo verschillen tussen Resource Manager en het klassieke implementatiemodel.
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
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Azure-implementatiemodellen
Hello Azure-platform is in de overgangsfase.  Of u nieuwe tooAzure of alleen met het jaar, het is belangrijk toounderstand enkele belangrijke wijzigingen Hallo we doorvoeren toohello platform tijdens deze overgang.

Alle Azure-resources bieden ondersteuning voor een of beide Hallo implementatiemodellen te volgen:

* **Resource Manager:** dit Hallo nieuwste implementatiemodel voor Azure-resources is. De meeste nieuwere resources bieden al ondersteuning voor dit implementatiemodel en uiteindelijk alle resources wordt.   
* **Klassieke:** dit model wordt ondersteund door de meeste bestaande Azure-resources vandaag. Nieuwe resources toegevoegd tooAzure biedt geen ondersteuning voor dit model.

Hallo-documentatie voor elk Azure-resource-informatie welke service het model kan worden gemaakt met.

## <a name="why-does-this-matter"></a>Waarom wordt deze kwestie?
Het is van belang voor Hallo volgende redenen:

* Hello Azure-platformfuncties waarmee u verschillen tussen deze twee modellen.  Bijvoorbeeld, resources die zijn gemaakt met behulp van Hallo Resource Manager-implementatiemodel (of alleen Resource Manager) kunnen worden gemaakt met [Azure Resource Manager-sjablonen](azure-resource-manager/resource-group-overview.md#template-deployment), terwijl dit niet resources die zijn gemaakt met de Hallo klassieke implementatiemodel.
* Azure-resource afzonderlijke functies Hallo of gedrag worden verschillende tussen de twee modellen Hallo of bestaan alleen in een model of andere Hallo.  Verkeer voor taakverdeling over virtuele machines die zijn gemaakt met de Hallo klassieke implementatiemodel is bijvoorbeeld *impliciete* omdat virtuele machines deel van een Azure Cloud Service uitmaken en wordt automatisch taakverdeling in virtuele machines binnen een cloudservice. Virtuele machines die zijn gemaakt met Resource Manager zijn geen leden van een cloudservice en moet een afzonderlijke Azure Load Balancer-resource *expliciet* tooload saldo verkeer over meerdere virtuele machines gemaakt.  
* Hoe u maken, configureren en beheren van uw Azure-resources is verschil is tussen deze twee modellen.
* Resources die zijn gemaakt met een implementatiemodel kunnen niet per se samenwerken met bronnen die zijn gemaakt met een andere implementatiemodel. Azure Virtual Machines is gemaakt met een implementatiemodel kan bijvoorbeeld alleen worden verbonden tooAzure virtuele netwerken die worden gemaakt met behulp van Hallo hetzelfde implementatiemodel.    

Elk van de implementatiemodellen Hallo onderliggende is een application programming interface (API) voor elke resource.  Er is een [Resource Manager-API](https://msdn.microsoft.com/library/azure/dn948464.aspx) Hallo Resource Manager-implementatiemodel en een [Service Management API](https://msdn.microsoft.com/library/azure/ee460799.aspx) voor Hallo klassieke implementatiemodel. Code toointeract met deze API's kunnen ontwikkelaars *rechtstreeks*.  

IT-professionals echter meestal communiceren met deze API's *indirect* met behulp van een grafische portal in een webbrowser, met behulp van Azure PowerShell cmdlets op een Windows-computer of met behulp van hello Azure-opdrachtregelinterface (CLI) op ofwel een Windows-, OS X- of Linux-computer. Alle drie deze indirecte methoden die worden gebruikt door de IT-Professional Hallo communiceren rechtstreeks met de Hallo API's. Dit betekent dat wanneer nieuwe functionaliteit geïntroduceerd toohello Azure wordt platform of bronnen is altijd direct beschikbaar via Hallo API eerst met de indirecte methoden Hallo krijgt ondersteuning voor Hallo nieuwe resources en functies nadat Hallo API beschikbaar is gemaakt.  

Hallo in de volgende secties wordt uitgelegd hoe Azure-resources zijn geconfigureerd met behulp van de verschillende implementatiemodellen Hallo via Hallo drie indirecte methoden.

## <a name="portals"></a>Portals
Azure heeft twee portals:

* **[Azure-portal](https://manage.windowsazure.com):** als u Azure hebt met een tijdje, hebt u deze portal gebruikt. Het gebruikte toocreate is en oudere Azure-resources die ondersteuning bieden voor het klassieke implementatiemodel Hallo configureren. Toocreate worden gebruikt kan of dat alleen ondersteuning voor Resource Manager-resources configureren. 
* **[Azure preview-portal](https://azure.microsoft.com/overview/preview-portal/):** als u een nieuwere Azure-resource, hebt u waarschijnlijk deze portal gebruikt. Het gebruikte toocreate worden en sommige Azure-resources configureren. U uiteindelijk kunnen toocreate en alle Azure-resources configureren met het. Voor bepaalde bronnen die ondersteuning bieden voor beide implementatiemodellen, deze portal worden de gebruikte toocreate en configureren van een resource met een implementatiemodel. 

Sommige resources en de functies worden alleen gemaakt en geconfigureerd in een portal of Hallo andere. Sommige resources of functies (nog) kunnen niet worden gemaakt of geconfigureerd in de portal en kunnen alleen worden geconfigureerd met PowerShell, CLI of beide Hallo. Hallo-documentatie voor elk Azure-resource details met de methode die kunnen worden gemaakt met. 

## <a name="powershell"></a>PowerShell
Met [PowerShell](/powershell/azureps-cmdlets-docs) kunt u een opdrachtregel of de auteur van scripts toocreate gebruiken en vanaf een computer met Windows Azure-resources configureren.  Afzonderlijke Azure-resources hebt [Resource Manager-cmdlets](/powershell/azure/overview), [Service Management-cmdlets](/powershell/azure/overview?view=azuresmps-3.7.0), of beide.  Sommige resources en functies kunnen alleen worden gemaakt en/of geconfigureerd met PowerShell of CLI Hallo. Hallo-resource, afhankelijk van wanneer met Resource Manager PowerShell-cmdlets wellicht hebt u twee opties voor het maken en configureren van Azure-resources:

* **PowerShell-cmdlets:** u kunt maken en configureren van elke Azure-resource afzonderlijk met Hallo-cmdlets voor elke resource. U kunt dit doen vanaf een opdrachtregel of door meerdere opdrachten in een PowerShell-script dat kan worden opgeslagen en -versie.
* **PowerShell-cmdlets met een Azure Resource Manager-sjabloon:** kunt u PowerShell toocreate Azure-resources met behulp van een Azure Resource Manager-sjabloon. Sjablonen kunnen worden opgeslagen en samengestelde. Hallo voor meer informatie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md) artikel. Verschillende [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) bestaan voor algemene oplossingen die kunnen worden gedownload en te worden gewijzigd.

## <a name="cli"></a>CLI
U kunt maken en configureren van Windows-, OS X- of Linux-computers met CLI hello Azure-resources.  Lees Hallo [installeren hello Azure CLI](cli-install-nodejs.md) artikel tooinstall Hallo CLI op uw besturingssysteem naar keuze. Zoals PowerShell, zijn er verschillende opdrachten die moeten worden gebruikt, afhankelijk van of u resources met behulp van [Resource Manager](xplat-cli-azure-resource-manager.md) of Hallo [klassieke (Service Management)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) implementatiemodellen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Begrijpen hoe te[sjablonen ontwerpen](best-practices-resource-manager-design-templates.md).

