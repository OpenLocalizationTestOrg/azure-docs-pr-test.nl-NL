---
title: aaaMultiple IP-adressen voor virtuele machines in Azure - sjabloon | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met een Azure Resource Manager-sjabloon.
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Meerdere IP-adressen toewijzen toovirtual machines met een Azure Resource Manager-sjabloon

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Dit artikel wordt uitgelegd hoe toocreate een virtuele machine (VM) via hello Azure Resource Manager deployment model met een Resource Manager-sjabloon. Meerdere openbare en particuliere IP-adressen kunnen niet worden toegewezen toohello dezelfde NIC bij het implementeren van een virtuele machine via het klassieke implementatiemodel Hallo. meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Beschrijving van sjabloon

Implementeren van een sjabloon kunt u tooquickly en Azure-resources consistent te maken met andere configuratie-waarden. Lees Hallo [overzicht voor Resource Manager-sjabloon](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel als u niet bekend met Azure Resource Manager-sjablonen bent. Hallo [implementeren van een virtuele machine met meerdere IP-adressen](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) sjabloon worden gebruikt in dit artikel.

<a name="resources"></a>Implementatie Hallo-sjabloon maakt Hallo resources te volgen:

|Resource|Naam|Beschrijving|
|---|---|---|
|Netwerkinterface|*myNic1*|Hallo drie IP-configuraties beschreven in Hallo scenario sectie van dit artikel worden gemaakt en toegewezen toothis NIC.|
|Openbare IP-adres resource|2 worden gemaakt: *myPublicIP* en *myPublicIP2*|Deze resources statische openbare IP-adressen zijn toegewezen en zijn toegewezen toohello *IPConfig 1* en *IPConfig 2* IP-configuraties in Hallo scenario beschreven.|
|VM|*myVM1*|Een standaard DS3 VM.|
|Virtueel netwerk|*myVNet1*|Een virtueel netwerk met één subnet met de naam *mySubnet*.|
|Storage-account|Unieke toohello implementatie|Een opslagaccount.|

<a name="parameters"></a>Bij het Hallo-sjabloon implementeren, moet u waarden voor Hallo volgende parameters opgeven:

|Naam|Beschrijving|
|---|---|
|adminUsername|Gebruikersnaam van de beheerder. Hallo-gebruikersnaam moet voldoen aan [gebruikersnaam van Azure-vereisten](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Beheerderswachtwoord wachtwoord Hallo moet voldoen aan [Azure wachtwoordvereisten](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|DNS-naam voor PublicIPAddressName1. Hallo DNS-naam wordt tooone van Hallo openbare IP-adressen toegewezen toohello VM opgelost. Hallo naam moet uniek zijn binnen hello Azure regio (locatie), hebt u Hallo virtuele machine in.|
|dnsLabelPrefix1|DNS-naam voor PublicIPAddressName2. Hallo DNS-naam wordt tooone van Hallo openbare IP-adressen toegewezen toohello VM opgelost. Hallo naam moet uniek zijn binnen hello Azure regio (locatie), hebt u Hallo virtuele machine in.|
|OSVersion|Hallo Windows of Linux-versie voor Hallo VM. Hallo-besturingssysteem is een volledig patches Hallo gegeven van de geselecteerde versie van Windows of Linux-installatiekopie.|
|imagePublisher|Hallo Windows of Linux installatiekopie-uitgever Hallo geselecteerd VM.|
|imageOffer|Hallo Windows of Linux-afbeelding voor Hallo geselecteerd VM.|

Elk Hallo-resources die zijn geïmplementeerd door Hallo-sjabloon is geconfigureerd met verschillende standaardinstellingen. U kunt deze instellingen via een van de volgende methoden Hallo bekijken:

- **Hallo-sjabloon weergeven op GitHub:** als u bekend met sjablonen bent, kunt u bekijken Hallo instellingen binnen Hallo [sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Hallo instellingen na de implementatie weergeven:** als u niet bekend met sjablonen bent, kunt u met behulp van de stappen in een van de volgende secties Hallo Hallo-sjabloon implementeren en bekijk vervolgens Hallo instellingen na de implementatie.

U kunt hello Azure-portal, PowerShell of hello Azure-opdrachtregelinterface (CLI) toodeploy Hallo sjabloon gebruiken. Alle methoden produceren Hallo hetzelfde resultaat. toodeploy hello sjabloon volledige Hallo stappen in een Hallo uit te voeren:

## <a name="deploy-using-hello-azure-portal"></a>Implementeren met behulp van hello Azure-portal

toodeploy hello sjabloon met gebruik van hello Azure-portal voltooid Hallo volgende stappen:

1. Hallo-sjabloon, wijzig desgewenst. Hallo sjabloon implementeert Hallo bronnen en instellingen in Hallo [resources](#resources) sectie van dit artikel. meer informatie over sjablonen toolearn en hoe tooauthor ze, leest hello [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)artikel.
2. Hallo-sjabloon implementeren met een van de volgende methoden Hallo:
    - **Selecteer Hallo-sjabloon in Hallo-portal:** voltooid Hallo stappen voor het Hallo [resources met aangepaste sjabloon implementeren](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) artikel. Kies Hallo vooraf bestaande sjabloon met de naam *101 vm-meerdere ipconfig*.
    - **Rechtstreeks:** klikt u op Hallo knop tooopen Hallo-sjabloon rechtstreeks in Hallo-portal te volgen:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Ongeacht Hallo methode u kiest, moet u toosupply waarden voor Hallo [parameters](#parameters) eerder in dit artikel worden vermeld. Nadat Hallo VM is geïmplementeerd, verbinding toohello VM en voeg Hallo persoonlijke IP-adressen toohello besturingssysteem u geïmplementeerd door te voeren Hallo stappen voor het Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

## <a name="deploy-using-powershell"></a>Implementeren met behulp van PowerShell

toodeploy hello sjabloon met behulp van PowerShell, volledige Hallo stappen te volgen:

1. Hallo-sjabloon implementeren via Hallo stappen in Hallo [implementeren van een sjabloon met PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) artikel. Hallo artikel beschrijft meerdere opties voor het implementeren van een sjabloon. Als u ervoor kiest met behulp van Hallo toodeploy `-TemplateUri parameter`, Hallo URI voor deze sjabloon is *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Als u ervoor kiest met behulp van Hallo toodeploy `-TemplateFile` parameter, inhoud van de kopie Hallo Hallo [sjabloonbestand](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) vanuit GitHub in een nieuw bestand op uw computer. Wijzig de sjablooninhoud hello, desgewenst. Hallo sjabloon implementeert Hallo bronnen en instellingen in Hallo [resources](#resources) sectie van dit artikel. meer informatie over sjablonen toolearn en hoe tooauthor ze, leest hello [Azure Resource Manager-sjablonen samenstellen ](../azure-resource-manager/resource-group-authoring-templates.md)artikel.

    Ongeacht de Hallo optie u toodeploy Hallo sjabloon met kiest, moet u waarden voor Hallo parameterwaarden die worden vermeld in Hallo opgeven [parameters](#parameters) sectie van dit artikel. Als u toosupply parameters in met behulp van een parameterbestand kiest, kopieert u de inhoud Hallo Hallo [parameterbestand](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) vanuit GitHub in een nieuw bestand op uw computer. Wijzig de waarden Hallo in Hallo-bestand. Gebruik Hallo-bestand dat u als waarde voor Hallo Hallo gemaakt `-TemplateParameterFile` parameter.

    toodetermine geldige waarden voor Hallo OSVersion, ImagePublisher en imageOffer parameters, stappen voor voltooid Hallo Hallo [navigeren door en selecteer Windows-VM-installatiekopieën artikel](../virtual-machines/windows/cli-ps-findimage.md) artikel.

    >[!TIP]
    >Als u niet zeker weet of een dnslabelprefix beschikbaar is, voert u Hallo `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` opdracht toofind uit. Als deze beschikbaar is, Hallo opdracht retourneert `True`.

2. Nadat Hallo VM is geïmplementeerd, verbinding toohello VM en voeg Hallo persoonlijke IP-adressen toohello besturingssysteem u geïmplementeerd door te voeren Hallo stappen voor het Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

## <a name="deploy-using-hello-azure-cli"></a>Implementeren met behulp van hello Azure CLI

toodeploy Hallo-sjabloon met gebruik van hello Azure CLI 1.0, volledige Hallo stappen te volgen:

1. Hallo-sjabloon implementeren via Hallo stappen in Hallo [implementeren van een sjabloon met hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) artikel. Hallo beschreven meerdere opties voor het implementeren van Hallo-sjabloon. Als u ervoor kiest met behulp van Hallo toodeploy `--template-uri` (-f), Hallo URI voor deze sjabloon is *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Als u ervoor kiest met behulp van Hallo toodeploy `--template-file` (-f) parameter, inhoud van de kopie Hallo Hallo [sjabloonbestand](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) vanuit GitHub in een nieuw bestand op uw computer. Wijzig de sjablooninhoud hello, desgewenst. Hallo sjabloon implementeert Hallo bronnen en instellingen in Hallo [resources](#resources) sectie van dit artikel. meer informatie over sjablonen toolearn en hoe tooauthor ze, leest hello [Azure Resource Manager-sjablonen samenstellen ](../azure-resource-manager/resource-group-authoring-templates.md)artikel.

    Ongeacht de Hallo optie u toodeploy Hallo sjabloon met kiest, moet u waarden voor Hallo parameterwaarden die worden vermeld in Hallo opgeven [parameters](#parameters) sectie van dit artikel. Als u toosupply parameters in met behulp van een parameterbestand kiest, kopieert u de inhoud Hallo Hallo [parameterbestand](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) vanuit GitHub in een nieuw bestand op uw computer. Wijzig de waarden Hallo in Hallo-bestand. Gebruik Hallo-bestand dat u als waarde voor Hallo Hallo gemaakt `--parameters-file` (-e) parameter.

    toodetermine geldige waarden voor Hallo OSVersion, ImagePublisher en imageOffer parameters, stappen voor voltooid Hallo Hallo [navigeren door en selecteer Windows-VM-installatiekopieën artikel](../virtual-machines/windows/cli-ps-findimage.md) artikel.

2. Nadat Hallo VM is geïmplementeerd, verbinding toohello VM en voeg Hallo persoonlijke IP-adressen toohello besturingssysteem u geïmplementeerd door te voeren Hallo stappen voor het Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
