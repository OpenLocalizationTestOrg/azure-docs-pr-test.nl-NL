---
title: Virtuele-Machineschaalset met Visual Studio aaaDeploy | Microsoft Docs
description: Virtuele-Machineschaalsets met Visual Studio en het Resource Manager-sjabloon implementeren
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Hoe toocreate een virtuele-Machineschaalset met Visual Studio
Dit artikel laat zien hoe toodeploy een Azure virtuele-Machineschaalset instelt met behulp van een Visual Studio Resource Group-implementatie.

[Azure virtuele-Machineschaalsets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is een resource Azure Compute toodeploy en beheren van een verzameling van soortgelijke virtuele machines met automatisch schalen en taakverdeling. U kunt inrichten en implementeren van virtuele-Machineschaalsets met [Azure Resource Manager-sjablonen](https://github.com/Azure/azure-quickstart-templates). Azure Resource Manager-sjablonen kunnen worden geïmplementeerd met behulp van de REST van de Azure CLI, PowerShell, en ook rechtstreeks vanuit Visual Studio. Visual Studio biedt een set van voorbeeld-sjablonen die kunnen worden geïmplementeerd als onderdeel van een implementatie van Azure Resource Group-project.

Azure Resource Group-implementaties zijn een manier toogroup en publiceren van een verzameling Azure gerelateerde resources in een met één implementatiebewerking. Voor meer informatie over deze hier: [maken en implementeren van Azure-resourcegroepen met Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Vereisten
tooget gestart met het implementeren van virtuele-Machineschaalsets in Visual Studio, moet u de volgende Hallo:

* Visual Studio 2013 of hoger
* Azure SDK 2.7, 2.8 of 2.9

>[!NOTE]
>Deze instructies wordt ervan uitgegaan dat u met behulp van Visual Studio met [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Een Project maken
1. Maak een nieuw project in Visual Studio door te kiezen **bestand | Nieuwe | Project**.
   
    ![Nieuw bestand][file_new]

2. Onder **Visual C# | Cloud**, kies **Azure Resource Manager** toocreate een project voor het implementeren van een Azure Resource Manager-sjabloon.
   
    ![Project maken][create_project]

3. Selecteer Hallo Linux of Windows Scale ingesteld Virtuelemachinesjabloon in Hallo lijst met sjablonen.
   
   ![Sjabloon selecteren][select_Template]

4. U ziet PowerShell-scripts voor implementatie, een Azure Resource Manager-sjabloon en een parameterbestand voor virtuele-Machineschaalset Hallo wanneer het project is gemaakt.
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a>Aanpassen van uw project
Nu kunt u Hallo sjabloon toocustomize laden voor de behoeften van uw toepassing, zoals VM-extensie-eigenschappen toevoegen of bewerken van regels voor taakverdeling. Hallo Scale ingesteld Virtuelemachinesjablonen zijn standaard geconfigureerde toodeploy hello AzureDiagnostics uitbreiding, waardoor het eenvoudig tooadd automatisch schalen regels. Ook implementeert u een load balancer met een openbaar IP-adres geconfigureerd met binnenkomende NAT-regels. 

Hallo load balancer kunt u verbinding maken met de VM-instanties toohello met SSH (Linux) of RDP (Windows). Hallo front-endpoort bereik begint met 50000. Voor linux dit betekent dat wanneer u SSH tooport 50000, bent u gerouteerde tooport 22 van Hallo eerste VM in het Hallo-Schaalset. Verbinding maken met tooport 50001 is gerouteerde tooport 22 Hallo tweede VM enzovoort.

 Een goede manier tooedit uw sjablonen met Visual Studio is toouse Hallo JSON-overzicht tooorganize Hallo parameters, variabelen en bronnen. Met kennis over Hallo kan schema Visual Studio wijzen fouten in uw sjabloon voordat u deze implementeert.

![JSON Explorer][json_explorer]

## <a name="deploy-hello-project"></a>Hallo-project implementeert
1. Implementeer hello Azure Resource Manager-sjabloon toocreate Hallo virtuele-Machineschaalset resource. Met de rechtermuisknop op het projectknooppunt Hallo en kies **implementeren | Nieuwe implementatie**.
   
    ![Sjabloon implementeren][5deploy_Template]
    
2. Selecteer uw abonnement in Hallo 'Implementeren tooResource groep' dialoogvenster.
   
    ![Sjabloon implementeren][6deploy_Template]

3. Hier kunt u een Azure-resourcegroep toodeploy de sjabloon wilt maken.
   
    ![Nieuwe resourcegroep][new_resource]

4. Klik vervolgens op **Parameters bewerken** tooenter-parameters die zijn doorgegeven tooyour sjabloon. Geef Hallo gebruikersnaam en wachtwoord voor Hallo besturingssysteem, die vereist toocreate Hallo-implementatie is. Als er geen PowerShell-hulpprogramma's voor Visual Studio is geïnstalleerd, is het raadzaam toocheck **wachtwoorden opslaan** tooavoid een verborgen PowerShell opdrachtregel vragen of gebruik [keyvault ondersteuning](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Parameters bewerken][edit_parameters]

5. Klik nu op **implementeren**. Hallo **uitvoer** venster bevat Hallo implementatie uitgevoerd. Opmerking Hallo actie uitvoeren van Hallo **implementeren AzureResourceGroup.ps1** script.
   
   ![Venster Output][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>De virtuele-Machineschaalset verkennen
Als het Hallo-implementatie is voltooid, kunt u bekijken Hallo nieuwe virtuele-Machineschaalset in Visual Studio Hallo **Cloud Explorer** (vernieuwen Hallo lijst). Cloud Explorer kunt u Azure-resources in Visual Studio tijdens het ontwikkelen van toepassingen beheren. U kunt ook bekijken uw virtuele-Machineschaalset in Hallo [Azure-portal](https://portal.azure.com) en [Azure Resource Explorer](https://resources.azure.com/).

![Cloud Explorer][cloud_explorer]

 Hallo-portal biedt de beste manier Hallo toovisually beheren van uw Azure-infrastructuur met een webbrowser, terwijl Azure Resource Explorer biedt een eenvoudige manier tooexplore en fouten opsporen in Azure-resources, geeft een venster in Hallo 'exemplaar weergeven' en ook weer met PowerShell opdrachten voor u bekijkt hello-bronnen.

## <a name="next-steps"></a>Volgende stappen
Als u virtuele-Machineschaalsets met Visual Studio hebt geïmplementeerd, kunt u verder aanpassen uw project toosuit de toepassingsvereisten van uw. Bijvoorbeeld automatisch schalen configureren door het toevoegen van een **Insights** resource, infrastructuur tooyour sjabloon (zoals zelfstandige virtuele machines) toevoegen of implementeren van toepassingen met behulp van de aangepaste scriptextensie Hallo. Goed voorbeeld sjablonen kunnen u vinden in Hallo [Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates) GitHub-opslagplaats (zoek 'vmss').

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
