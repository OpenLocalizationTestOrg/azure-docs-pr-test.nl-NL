---
title: aaaContinuous integratie in VS-Team Services met behulp van Azure Resource Group projecten | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van doorlopende integratie in Visual Studio Team Services met behulp van Azure Resource Group-implementatie in Visual Studio-projecten.
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Doorlopende integratie in Visual Studio Team Services met behulp van Azure Resource Group implementatieprojecten
een Azure-sjabloon toodeploy, u taken uitvoeren in verschillende stadia: maken, testen, kopie tooAzure (ook wel 'Fasering' genoemd) en de sjabloon implementeert. Er zijn twee verschillende manieren toodeploy sjablonen tooVisual Studio Team Services (VS Team Services). Beide methoden Hallo dezelfde resultaten opleveren, dus kies Hallo die het beste past bij uw werkstroom.

1. Een definitie van één stap tooyour build met Hallo PowerShell-script dat opgenomen in het implementatieproject Azure-resourcegroep van hello (implementeren AzureResourceGroup.ps1) toevoegen. Hallo script artefacten kopieert en vervolgens implementeert Hallo-sjabloon.
2. Voeg dat meerdere tegenover Team Services bouwen stappen elkaar uitvoeren van een taak fase.

In dit artikel wordt gedemonstreerd beide opties. de eerste optie Hallo heeft Hallo voordeel gebruik Hallo hetzelfde script gebruikt door ontwikkelaars in Visual Studio en het geven van de consistentie in het hele levenscyclus Hallo. de tweede optie Hallo biedt een handige alternatieve toohello ingebouwde script. Beide procedures wordt ervan uitgegaan dat u hebt al een implementatieproject voor Visual Studio in VS-teamservices ingecheckt.

## <a name="copy-artifacts-tooazure"></a>Artefacten tooAzure kopiëren
Als u alle artefacten die nodig zijn voor de sjabloonimplementatie, moet u ongeacht Hallo scenario Azure Resource Manager toegang toothem geven. Deze artefacten kunnen u de volgende bestanden:

* Geneste sjablonen
* Configuratiescripts en DSC-scripts
* Binaire bestanden van toepassingen

### <a name="nested-templates-and-configuration-scripts"></a>Geneste sjablonen en configuratiescripts
Wanneer u het Hallo-sjablonen die worden geleverd door Visual Studio gebruikt (of gebouwd met Visual Studio codefragmenten) Hallo PowerShell-script bereidt niet alleen Hallo artefacten, het Hallo-URI voor Hallo bronnen voor verschillende implementaties ook parameterizes. Hallo-script en vervolgens kopieert Hallo artefacten tooa beveiligde container in Azure, maakt u een SaS-token voor die container en stuurt vervolgens deze gegevens over toohello sjabloonimplementatie. Zie [sjabloonimplementatie met een maakt](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn informatie over geneste sjablonen.  Wanneer u taken in de VS Team Services, moet u Hallo juiste taken voor uw sjabloonimplementatie selecteren en indien nodig, parameterwaarden doorgeven van Hallo stap toohello sjabloonimplementatie voor fasering.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Doorlopende implementatie in VS-teamservices ingesteld
toocall hello PowerShell-script in VS-Team Services, moet u tooupdate de definitie van de build. In het kort zijn Hallo stappen: 

1. De definitie van de build Hallo bewerken.
2. Azure autorisatie in VS-teamservices instellen.
3. De stap van een Azure PowerShell-build die verwijst naar de PowerShell-script in hello Azure-resourcegroep implementatieproject Hallo toevoegen.
4. Hallo-waarde van Hallo *- ArtifactsStagingDirectory* toowork parameter aan een project is ingebouwd in VS-Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Gedetailleerd overzicht optie 1
Hallo doorlopen volgende procedures Hallo stappen nodig tooconfigure continue implementatie in VS-Team Services met behulp van een enkele taak waarvoor Hallo PowerShell-script wordt uitgevoerd in uw project. 

1. Bewerk de definitie van de VS Team Services bouwen en toevoegen van een Azure PowerShell build stap. Kies Hallo build definitie onder Hallo **bouwen definities** categorie en kies vervolgens Hallo **bewerken** koppeling.
   
   ![De definitie van de build bewerken][0]
2. Voeg een nieuwe **Azure PowerShell** stap toohello build definitie bouwen en kies vervolgens Hallo **build-stap toevoegen...** te klikken.
   
   ![Build stap toevoegen][1]
3. Kies Hallo **implementeren taak** categorie, selecteer Hallo **Azure PowerShell** taak en kies vervolgens de **toevoegen** knop.
   
   ![Taken toevoegen][2]
4. Kies Hallo **Azure PowerShell** stap bouwen en vul vervolgens de waarden.
   
   1. Als u al een Azure-service-eindpunt toegevoegd tooVS Team Services, kiest u Hallo-abonnement in Hallo **Azure-abonnement** vervolgkeuzelijst vak en klikt u vervolgens overslaan toohello volgende sectie. 
      
      Als u geen een Azure-service-eindpunt in VS-Team Services, moet u tooadd een. Deze subsectie doorloopt u Hallo-proces. Als uw Azure-account gebruikt een Microsoft-account (zoals Hotmail), moet u Hallo stappen tooget na een Service-Principal-verificatie uitvoeren.
   2. Kies Hallo **beheren** koppelen van de volgende toohello **Azure-abonnement** keuzelijst met invoervak.
      
      ![Azure-abonnementen beheren][3]
   3. Kies **Azure** in Hallo **nieuwe Service-eindpunt** keuzelijst met invoervak.
      
      ![Nieuwe service-eindpunt][4]
   4. In Hallo **Azure-abonnement toevoegen** dialoogvenster, selecteer Hallo **Service-Principal** optie.
      
      ![Service-principal optie][5]
   5. Toevoegen van uw Azure-abonnement informatie toohello **Azure-abonnement toevoegen** in het dialoogvenster. U moet tooprovide Hallo volgende items:
      
      * Abonnements-Id
      * De naam van abonnement
      * Service-Principal-Id
      * Service-Principal-sleutel
      * Tenant-Id
   6. Voeg een naam van uw keuze toohello **abonnement** naamvak. Deze waarde wordt weergegeven in hello later **Azure-abonnement** vervolgkeuzelijst in VS-Team Services. 
   7. Als u uw Azure-abonnement-ID niet weet, kunt u een van de volgende opdrachten tooretrieve Hallo deze.
      
      Gebruik voor PowerShell-scripts:
      
      `Get-AzureRmSubscription`
      
      Gebruik voor Azure CLI:
      
      `azure account show`
   8. tooget een Service-Principal-ID, Service-Principal-sleutel en Tenant-ID, volgt u de procedure Hallo in [een Active Directory-toepassing en service-principal maken met portal](resource-group-create-service-principal-portal.md) of [verifiëren met een service-principal Azure Resource Manager](resource-group-authenticate-service-principal.md).
   9. Add Hallo Service-Principal-ID, Service-Principal-sleutel en het Tenant-ID-waarden toohello **Azure-abonnement toevoegen** dialoogvenster vak en klik vervolgens op Hallo **OK** knop.
      
      U hebt nu een geldige Service Principal toouse toorun hello Azure PowerShell-script.
5. De definitie van de build Hallo bewerken en kies Hallo **Azure PowerShell** stap bouwen. Selecteer Hallo-abonnement in Hallo **Azure-abonnement** keuzelijst met invoervak. (Als het Hallo-abonnement niet wordt weergegeven, kiest u Hallo **vernieuwen** knop volgende Hallo **beheren** koppeling.) 
   
   ![Azure PowerShell opbouwtaak configureren][8]
6. Geef een pad toohello implementeren AzureResourceGroup.ps1 PowerShell-script. toodo, kies Hallo weglatingsteken (...) knop volgende toohello **scriptpad** toohello implementeren AzureResourceGroup.ps1 PowerShell-script in Hallo Ga **Scripts** map van uw project, selecteer en kies vervolgens Hallo **OK** knop.    
   
   ![Pad tooscript selecteren][9]
7. Nadat u Hallo script hebt geselecteerd, Hallo pad toohello script bijwerken zodat deze wordt uitgevoerd vanaf Hallo Build.StagingDirectory (dezelfde directory Hallo die *ArtifactsLocation* is ingesteld op). U kunt dit doen door toe te voegen "$(Build.StagingDirectory)/ ' toohello begin van Hallo scriptpad.
   
    ![Pad tooscript bewerken][10]
8. In Hallo **scriptparameters** Voer Hallo parameters (op één regel) te volgen. Wanneer u Hallo script in Visual Studio uitvoert, kunt u zien hoe tegenover maakt gebruik van parameters in Hallo Hallo **uitvoer** venster. U kunt dit gebruiken als een beginpunt voor het instellen van de parameterwaarden Hallo in uw build-stap.
   
   | Parameter | Beschrijving |
   | --- | --- |
   | -ResourceGroupLocation |geografische locatie waarde waar Hallo resourcegroep zich bevindt, zoals Hallo **eastus** of **'VS-Oost'**. (Toevoegen tussen enkele aanhalingstekens als Hallo naam een spatie.) Zie [Azure-gebieden](https://azure.microsoft.com/en-us/regions/) voor meer informatie. |
   | -ResourceGroupName |Hallo-naam van resourcegroep Hallo gebruikt voor deze implementatie. |
   | -UploadArtifacts |Deze parameter, indien aanwezig, wordt die artefacten die toobe moeten geüpload tooAzure van Hallo lokaal systeem. U hoeft alleen tooset deze switch als de sjabloonimplementatie van uw extra artefacten vereist die u wilt toostage met Hallo PowerShell-script (zoals configuratiescripts of geneste sjablonen). |
   | -StorageAccountName |Hallo-naam van de opslagaccount Hallo gebruikt toostage artefacten voor deze implementatie. Deze parameter wordt alleen gebruikt als u bij het Faseren van artefacten voor implementatie. Als deze parameter wordt opgegeven, wordt een nieuw opslagaccount gemaakt als Hallo-script niet tijdens een eerdere implementatie gemaakt is. Als het Hallo-parameter wordt opgegeven, wordt opslagaccount Hallo moet al bestaan. |
   | -StorageAccountResourceGroupName |Hallo-naam van resourcegroep Hallo Hallo storage-account gekoppeld. Deze parameter is alleen vereist als u een waarde voor Hallo StorageAccountName parameter opgeven. |
   | -Sjabloonbestand |Hallo pad toohello sjabloonbestand in implementatieproject voor hello Azure-resourcegroep. Gebruik een pad voor deze parameter op die locatie Hallo PowerShell-script in plaats van een absoluut pad relatief toohello tooenhance flexibiliteit. |
   | -TemplateParametersFile |Hallo pad toohello parameterbestand in implementatieproject voor hello Azure-resourcegroep. Gebruik een pad voor deze parameter op die locatie Hallo PowerShell-script in plaats van een absoluut pad relatief toohello tooenhance flexibiliteit. |
   | -ArtifactStagingDirectory |Deze parameter kunt Hallo PowerShell-script weet Hallo-map van waaruit de binaire bestanden van het project Hallo moeten worden gekopieerd. Hallo-standaardwaarde gebruikt door Hallo PowerShell-script, overschrijft deze waarde. Voor VS Team Services gebruikt, stelt u Hallo-waarde in op: - ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   Hier volgt een voorbeeld van een script argumenten (line verbroken voor de leesbaarheid):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Wanneer u klaar bent, Hallo **scriptparameters** vak moet eruitzien als Hallo volgende lijst:
   
   ![Scriptargumenten][11]
9. Nadat u hebt toegevoegd om alle vereiste items toohello Azure PowerShell bouwen stap hello, kiest u Hallo **wachtrij** knop toobuild Hallo project te bouwen. Hallo **bouwen** scherm toont Hallo-uitvoer van Hallo PowerShell-script.

### <a name="detailed-walkthrough-for-option-2"></a>Optie 2 gedetailleerd overzicht
Hallo doorlopen volgende procedures Hallo stappen nodig tooconfigure continue implementatie in VS-teamservices Hallo ingebouwde taken gebruiken.

1. Bewerk uw tegenover Team Services build definitie tooadd twee nieuwe build stappen. Kies Hallo build definitie onder Hallo **bouwen definities** categorie en kies vervolgens Hallo **bewerken** koppeling.
   
   ![Build-definition bewerken][12]
2. Add Hallo nieuwe bouwen stappen toohello build definitie met Hallo **build-stap toevoegen...** te klikken.
   
   ![Build stap toevoegen][13]
3. Kies Hallo **implementeren** taakcategorie, selecteer Hallo **Azure bestandskopie** taak en kies vervolgens de **toevoegen** knop.
   
   ![Azure bestandskopie taak toevoegen][14]
4. Kies Hallo **Azure Resource Group Deployment** taak en kies vervolgens de **toevoegen** knop en vervolgens **sluiten** hello **taak catalogus**.
   
   ![Azure Resource Group Deployment taak toevoegen][15]
5. Kies Hallo **Azure bestandskopie** taak en de waarden in te vullen.
   
   Als u al een Azure-service-eindpunt toegevoegd tooVS Team Services, kiest u Hallo-abonnement in Hallo **Azure-abonnement** keuzelijst met invoervak. Als u niet een abonnement hebt, raadpleegt u [optie 1](#detailed-walkthrough-for-option-1) voor instructies over het instellen van een van in VS-teamservices.
   
   * Bron - Voer **$(Build.StagingDirectory)**
   * Azure verbindingstype - Selecteer **Azure Resource Manager**
   * Azure RM-abonnement - Selecteer Hallo abonnement voor Hallo storage-account u wilt dat toouse in Hallo **Azure-abonnement** keuzelijst met invoervak. Als het Hallo-abonnement niet wordt weergegeven, kiest u Hallo **vernieuwen** knop volgende Hallo **beheren** koppeling.
   * Doeltype - Selecteer **Azure Blob**
   * RM Storage-Account - Selecteer Hallo storage account u wilt dat toouse voor het Faseren van artefacten
   * Containernaam - Hallo naam invoeren van de container Hallo gewenst toouse voor fasering; elke naam zijn geldige container kan, maar één toegewezen toothis build definitie gebruiken
   
   Voor de uitvoerwaarden Hallo:
   
   * Storage-Container URI - Voer **artifactsLocation**
   * Storage-Container SAS-Token - Voer **artifactsLocationSasToken**
   
   ![De taak Azure bestand kopiëren configureren][16]
6. Kies Hallo **Azure Resource Group Deployment** stap bouwen en vul vervolgens de waarden.
   
   * Azure verbindingstype - Selecteer **Azure Resource Manager**
   * Azure RM-abonnement - abonnement voor de implementatie in Hallo Selecteer Hallo **Azure-abonnement** keuzelijst met invoervak. Dit is meestal Hallo hetzelfde abonnement worden gebruikt in de vorige stap Hallo
   * Actie - Selecteer **maken of bijwerken resourcegroep**
   * Resourcegroep - Selecteer een resourcegroep of Hallo-naam van een nieuwe resourcegroep voor Hallo-implementatie
   * Locatie - Selecteer Hallo-locatie voor de resourcegroep Hallo
   * Sjabloon: Voer Hallo pad en naam van Hallo sjabloon toobe geïmplementeerd voorafgaand **$(Build.StagingDirectory)**, bijvoorbeeld: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Sjabloonparameters - Hallo pad en naam van Hallo parameters toobe gebruikt, voer voorafgaand **$(Build.StagingDirectory)**, bijvoorbeeld: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Sjabloonparameters overschrijven: Voer of kopiëren en plakken van Hallo code te volgen:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Azure-resourcegroep implementatie taak configureren][17]
7. Nadat u alle vereiste Hallo items hebt toegevoegd, Hallo build definitie opslaan en kies **wachtrij nieuwe build** Hallo bovenaan.

## <a name="next-steps"></a>Volgende stappen
Lees [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md) toolearn meer informatie over Azure Resource Manager en Azure-resourcegroepen.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
