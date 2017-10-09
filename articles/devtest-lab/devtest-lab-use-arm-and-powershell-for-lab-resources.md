---
title: aaaCreate of wijzigen van automatisch in PowerShell met Azure Resource Manager-sjablonen labs | Microsoft Docs
description: Meer informatie over hoe toouse Azure Resource Manager-sjablonen met PowerShell toocreate of labs automatisch in een DevTest lab wijzigen
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Maken of wijzigen van labs automatisch met Azure Resource Manager-sjablonen en PowerShell

DevTest Labs biedt tal van sjablonen voor Azure Resource Manager en PowerShell-scripts die kunnen helpen u snel en automatisch maken van nieuwe labs of wijzig bestaande labs en vervolgens implementeert deze resources.

In dit artikel begeleidt u bij Hallo proces van het gebruik van deze sjablonen en scripts tooautomate Hallo maken, wijzigen en implementeren van uw labs. In dit artikel ziet u ook waar u meer informatie over hoe toouse PowerShell tooperform enkele algemene in DevTest Labs taken kan vinden.

## <a name="step-1-gather-your-templates-and-scripts"></a>Stap 1: Uw sjablonen en scripts verzamelen
U kunt vinden en-klare [Azure Resource Manager-sjablonen](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) en [PowerShell-scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) op onze openbare [Github-opslagplaats](https://github.com/Azure/azure-devtestlab). Gebruik deze als-is, of pas ze aan uw behoeften en op te slaan in uw eigen [persoonlijke Git-opslagplaats](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Stap 2: Uw Azure Resource Manager-sjabloon wijzigen
U kunt Hallo stappen op [maken van uw eerste Azure Resource Manager-sjabloon](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) als u een sjabloon voordat nooit hebt gemaakt.

Bovendien [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) veel richtlijnen en suggesties toohelp biedt u Azure Resource Manager-sjablonen die betrouwbare en eenvoudige toouse zijn maken. Normaal gesproken gebruikt u een variant van een van de Hallo benaderingen of voorbeelden opgegeven en wijzigen van de sjabloon voor uw behoeften.

## <a name="step-3-deploy-resources-with-powershell"></a>Stap 3: Implementatie van resources met PowerShell
Nadat u uw sjablonen en scripts hebt aangepast, volgt u Hallo stappen nodig te[implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). Hallo artikel bevat algemene informatie over het gebruik van Azure PowerShell met Azure Resource Manager-sjablonen toodeploy uw tooAzure resources.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Algemene taken die u kunt uitvoeren in DevTest labs met behulp van PowerShell
Er zijn veel andere veelvoorkomende taken die u automatiseren kunt met behulp van PowerShell. Hallo volgende secties van Hallo documentatie worden Hallo stappen vereist tooperform deze taken.

* [Een aangepaste installatiekopie maken van een VHD-bestand met behulp van PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Uploaden van de VHD-bestand toolab storage-account met behulp van PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Toevoegen van een externe gebruiker tooa lab met behulp van PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Maakt een lab aangepaste rol met behulp van PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe toocreate een [persoonlijke Git-opslagplaats](devtest-lab-add-artifact-repo.md) waar u uw aangepaste sjablonen of scripts wilt opslaan.
* Hallo verkennen [Azure Resource Manager-sjablonen uit Azure sjabloon snelstartgalerie](https://github.com/Azure/azure-quickstart-templates).
