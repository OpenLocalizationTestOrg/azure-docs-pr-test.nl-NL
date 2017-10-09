---
title: aaaView en gebruiken van een virtuele machine van Azure Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure Resource Manager-sjabloon van een virtuele machine toocreate andere virtuele machines
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Een virtuele machine van Azure Resource Manager-sjabloon gebruiken

Wanneer u een virtuele machine (VM) zijn maken in DevTest Labs via Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), kunt u hello Azure Resource Manager-sjabloon bekijken voordat u Hallo VM opslaat. Hallo sjabloon kan vervolgens worden gebruikt als een basis-toocreate meer lab virtuele machines met dezelfde instellingen Hallo.

Dit artikel wordt beschreven hoe tooview Resource Manager-sjabloon Hallo bij het maken van een virtuele machine en hoe toodeploy deze later tooautomate maken van Hallo dezelfde virtuele machine.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Multi-VM versus één VM-resourcemanager-sjablonen
Er zijn twee manieren toocreate virtuele machines in DevTest Labs met een Resource Manager-sjabloon: Hallo Microsoft.DevTestLab/labs/virtualmachines resource inrichten of Hallo Microsoft.Commpute/virtualmachines resource inrichten. Elke wordt gebruikt in verschillende scenario's en andere machtigingen zijn vereist.

- Resource Manager-sjablonen die gebruikmaken van een resourcetype Microsoft.DevTestLab/labs/virtualmachines (zoals opgegeven in Hallo 'resource'-eigenschap in de sjabloon Hallo) kunnen afzonderlijke lab virtuele machines inrichten. Elke virtuele machine vervolgens wordt weergegeven als één item in de lijst met Hallo DevTest Labs virtuele machines:

   ![Lijst met virtuele machines als één items in de lijst met virtuele machines van Hallo DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Dit type Resource Manager-sjabloon kan worden ingericht via hello Azure PowerShell-opdracht **New-AzureRmResourceGroupDeployment** of via Azure CLI-opdracht Hallo **az implementatie maken** . Het vereist administrator-machtigingen zodat gebruikers die zijn toegewezen aan een gebruikersrol DevTest Labs Hallo-implementatie kunnen niet uitvoeren. 

- Resource Manager-sjablonen die gebruikmaken van een resourcetype Microsoft.Compute/virtualmachines kunnen meerdere virtuele machines inrichten als één enkele omgeving in de lijst met Hallo DevTest Labs virtuele machines:

   ![Lijst met virtuele machines als één items in de lijst met virtuele machines van Hallo DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Virtuele machines in dezelfde omgeving samen kan worden beheerd Hallo en share Hallo dezelfde levenscyclus. Gebruikers die zijn toegewezen aan een gebruikersrol DevTest Labs kan omgevingen met behulp van deze sjablonen, zolang Hallo beheerder Hallo lab heeft geconfigureerd op deze manier kunnen maken.

Hallo rest van dit artikel wordt beschreven Resource Manager-sjablonen die Mirosoft.DevTestLab/labs/virtualmachines gebruiken. Deze worden gebruikt door het lab admins tooautomate lab maken van virtuele machines (bijvoorbeeld claimable VM's) of gouden installatiekopie generatie (bijvoorbeeld installatiekopie factory).

[Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) veel richtlijnen en suggesties toohelp biedt u Azure Resource Manager-sjablonen die betrouwbare en eenvoudige toouse zijn maken.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Weergeven en opslaan van een virtuele machine Resource Manager-sjabloon
1. Volg de stappen Hallo in [maakt van uw eerste virtuele machine in een lab](devtest-lab-create-first-vm.md) toobegin maken van een virtuele machine.
1. Geef informatie op Hallo vereist voor uw virtuele machine en alle artefacten die u voor deze virtuele machine wilt toevoegen.
1. Aan de onderkant van de Hallo van Hallo configureren instellingenvenster, kies **weergave ARM-sjabloon**.

   ![Knop voor ARM-sjabloon weergeven](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Kopiëren en opslaan van Hallo Resource Manager-sjabloon toouse hoger toocreate een andere virtuele machine.

   ![Resource manager-sjabloon toosave voor later gebruik](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Nadat u Hallo Resource Manager-sjabloon hebt opgeslagen, moet u de sectie van de parameters Hallo van Hallo sjabloon bijwerken voordat u deze kunt gebruiken. U kunt een parameter.json dat net Hallo parameters buiten Hallo werkelijke Resource Manager-sjabloon aanpast maken. 

![Een JSON-bestand met parameters aanpassen](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Een Resource Manager-sjabloon toocreate een virtuele machine implementeren
Nadat u hebt opgeslagen van Resource Manager-sjabloon en het is afgestemd op uw behoeften, kunt u het maken van tooautomate VM. [Implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) wordt beschreven hoe toouse Azure PowerShell met Resource Manager-sjablonen toodeploy uw tooAzure resources. [Implementeren van resources met Resource Manager-sjablonen en Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) wordt beschreven hoe toouse Azure CLI met Resource Manager-sjablonen toodeploy uw tooAzure resources.

> [!NOTE]
> Alleen een gebruiker met machtigingen van de eigenaar lab kunt virtuele machines maken van een Resource Manager-sjabloon met behulp van Azure PowerShell. Als u wilt maken van VM tooautomate met een Resource Manager-sjabloon en u alleen gebruikersmachtigingen hebt, kunt u Hallo [ **az lab vm maken** opdracht in Hallo CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[multi-VM-omgevingen maken met Resource Manager-sjablonen](devtest-lab-create-environment-from-arm.md).
* Verken meer snel starten-Resource Manager-sjablonen voor het automatiseren van DevTest Labs van Hallo [openbare DevTest Labs GitHub-repo-](https://github.com/Azure/azure-quickstart-templates).
