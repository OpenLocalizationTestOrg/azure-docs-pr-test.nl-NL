---
title: aaaVisual Studio Azure resource group projecten | Microsoft Docs
description: Visual Studio toocreate een Azure-resourcegroepproject te gebruiken en Hallo resources tooAzure implementeren.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Azure-resourcegroepen maken en implementeren met Visual Studio
Met Visual Studio en Hallo [Azure SDK](https://azure.microsoft.com/downloads/), kunt u een project waarvoor uw infrastructuur en code tooAzure implementeert. U kunt bijvoorbeeld Hallo webhost, website en database definiëren voor uw app, en die infrastructuur samen met de Hallo code implementeren. U kunt ook een virtuele machine, een virtueel netwerk en een opslagaccount opgeven en die infrastructuur implementeren in combinatie met een script dat wordt uitgevoerd op de virtuele machine. Hallo **Azure-resourcegroep** implementatieproject kunt u toodeploy alle Hallo nodig resources in één herhaalbare bewerking. Zie voor meer informatie over het implementeren en beheren van uw resources [Overzicht van Azure Resource Manager](resource-group-overview.md).

Azure-resourcegroepprojecten bevatten Azure Resource Manager JSON-sjablonen, waarin Hallo-resources die u tooAzure implementeert. toolearn over Hallo elementen van de Resource Manager-sjabloon hello, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md). Visual Studio kunt u tooedit deze sjablonen en voorziet in hulpprogramma's die werken met sjablonen te vereenvoudigen.

In dit artikel gaat u een web-app en SQL Database implementeren. Hallo stappen zijn echter bijna Hallo dezelfde voor elk type resource. U kunt net zo eenvoudig een Virtuele Machine en de bijbehorende resources implementeren. Visual Studio biedt veel verschillende startsjablonen om te implementeren in algemene scenario's.

In dit artikel wordt Visual Studio 2017 gebruikt. Als u Visual Studio 2015 Update 2 en Microsoft Azure SDK voor .NET 2.9 gebruiken, of Visual Studio 2013 met Azure SDK 2.9 uw ervaring grotendeels Hallo dezelfde. Kunt u versies van hello Azure SDK versie 2.6 of hoger. uw ervaring van de gebruikersinterface Hallo mogelijk anders dan Hallo-gebruikersinterface wordt weergegeven in dit artikel. Wordt aangeraden dat u de meest recente versie Hallo Hallo installeert [Azure SDK](https://azure.microsoft.com/downloads/) voordat u Hallo stappen begint. 

## <a name="create-azure-resource-group-project"></a>Een Azure-resourcegroepproject maken
In deze procedure maakt u een Azure Resource Group-project met het sjabloon **Web app + SQL**.

1. Ga in Visual Studio naar **Bestand**, **Nieuw project**. Kies vervolgens **C#** of **Visual Basic**. Kies vervolgens **Cloud** en het project **Azure-resourcegroep**.
   
    ![Project voor cloudimplementatie](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Hallo sjabloon kiezen die u wilt dat toodeploy tooAzure Resource Manager. Er zijn diverse opties beschikbaar op basis van Hallo type project u aankondiging wilt toodeploy. Kies voor dit artikel Hallo **webtoepassing + SQL** sjabloon.
   
    ![Een sjabloon selecteren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    Hallo sjabloon dat u kiest is slechts een beginpunt; u kunt toevoegen en verwijderen van resources toofulfill uw scenario.
   
   > [!NOTE]
   > Visual Studio haalt een lijst met beschikbare sjablonen online op. Hallo lijst wordt gewijzigd.
   > 
   > 
   
    Visual Studio maakt een project voor resourcegroepimplementatie voor Hallo web-app en SQL-database.
3. toosee wat u hebt gemaakt, zoekt u naar op Hallo-knooppunt in het implementatieproject Hallo.
   
    ![knooppunten weergegeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Omdat we Hallo-webtoepassing + SQL-sjabloon voor dit voorbeeld kiest, ziet u de volgende bestanden Hallo: 
   
   | Bestandsnaam | Beschrijving |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Een PowerShell-script waarmee PowerShell-opdrachten toodeploy tooAzure Resource Manager aanroept.<br />**Opmerking** Visual Studio gebruikt deze PowerShell-script toodeploy uw sjabloon. Wijzigingen die u aanbrengt toothis script-implementatie in Visual Studio beïnvloeden, dus wees voorzichtig. |
   | WebSiteSQLDatabase.json |Hallo Resource Manager-sjabloon waarmee Hallo-infrastructuur die u wilt implementeren tooAzure en Hallo-parameters die kunt u opgeven tijdens de implementatie worden gedefinieerd. Het definieert ook Hallo afhankelijkheden tussen Hallo resources zo Resource Manager Hallo resources in de juiste volgorde Hallo implementeert. |
   | WebSiteSQLDatabase.parameters.json |Een parameterbestand die nodig is voor de sjabloon Hallo waarden bevat. U doorgeven in parameter waarden toocustomize elke implementatie. |
   
    Alle resourcegroepimplementatieprojecten bevatten deze algemene bestanden. Andere projecten bevatten mogelijk extra bestanden toosupport andere functies.

## <a name="customize-hello-resource-manager-template"></a>Hallo Resource Manager-sjabloon aanpassen
U kunt een implementatieproject aanpassen door het wijzigen van Hallo JSON-sjablonen die Hallo-bronnen die u wilt dat toodeploy beschrijven. JSON staat voor JavaScript Object Notation en is een geserialiseerde gegevensindeling waarmee eenvoudig toowork met. Hallo JSON-bestanden een schema dat u verwijst naar Hallo boven aan elk bestand gebruikt. Als u toounderstand Hallo schema wilt, kunt u downloaden en analyseren. Hallo schema wordt gedefinieerd welke elementen zijn geldige, hello typen en indelingen voor velden, mogelijke waarden van de opsommingswaarden hello, enzovoort. toolearn over Hallo elementen van de Resource Manager-sjabloon hello, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

open toowork van uw sjabloon **WebSiteSQLDatabase.json**.

Hallo Visual Studio editor biedt hulpprogramma's voor u met het bewerken van resourcemanager-sjabloon Hallo tooassist. Hallo **JSON-overzicht** venster kunt u eenvoudig toosee Hallo-elementen gedefinieerd in de sjabloon.

![JSON-overzicht weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Wanneer u een Hallo-elementen in Hallo overzicht, neemt u toothat deel van de sjabloon Hallo en markeert u Hallo JSON overeenkomt.

![door JSON navigeren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

U kunt een resource toevoegen door beide te selecteren Hallo **Resource toevoegen** knop boven Hallo Hallo JSON overzichtsvenster of door met de rechtermuisknop op **resources** en het selecteren van **nieuwe Resource toevoegen**.

![resource toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Voor deze zelfstudie selecteert u **Opslagaccount** en geeft u het een naam. Geef een naam op die niet meer dan elf tekens (alleen cijfers en kleine letters) omvat.

![opslag toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

U ziet dat niet alleen Hallo resource is toegevoegd, maar ook een parameter voor Hallo storage-account en een variabele voor naam van de Hallo van Hallo storage-account invoeren.

![overzicht weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Hallo **storageType** -parameter is vooraf gedefinieerd met de toegestane typen en een standaardtype. U kunt deze waarden laten staan of ze bewerken voor uw scenario. Als u niet dat iemand anders wilt toodeploy een **Premium_LRS** storage-account via dit sjabloon verwijderen uit Hallo typen toegestaan. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio biedt ook intellisense toohelp u begrijpt welke eigenschappen beschikbaar zijn bij het Hallo-sjabloon bewerken. Tooedit hello eigenschappen voor uw App Service-abonnement, gaat u toohello **HostingPlan** resource, en voeg een waarde voor Hallo **eigenschappen**. U ziet dat intellisense Hallo beschikbare waarden worden weergegeven en wordt een beschrijving van die waarde.

![IntelliSense weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

U kunt instellen **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Hallo resourcegroep project tooAzure implementeren
U bent nu klaar toodeploy uw project. Wanneer u een Azure-resourcegroepproject implementeert, implementeert u deze tooan Azure-resourcegroep. Hallo-resourcegroep is een logische groepering van resources die een gemeenschappelijk levenscyclus delen.

1. Kies in het snelmenu Hallo van projectknooppunt Hallo-implementatie, **implementeren** > **nieuw**.
   
    ![Het menu-item Implementeren, Nieuwe implementatie](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Hallo **tooResource groep implementeren** dialoogvenster wordt weergegeven.
   
    ![Dialoogvenster groep tooResource implementeren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. In Hallo **resourcegroep** vervolgkeuzelijst, kiest u een bestaande resourcegroep of maak een nieuwe. toocreate een resourcegroep of open Hallo **resourcegroep** dropdown vak en kies **nieuw**.
   
    ![Dialoogvenster groep tooResource implementeren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Hallo **resourcegroep maken** dialoogvenster wordt weergegeven. Geef uw groep een naam en locatie en selecteer Hallo **maken** knop.
   
    ![Dialoogvenster Resourcegroep maken](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Hallo-parameters voor de implementatie van Hallo bewerken door te selecteren van Hallo **Parameters bewerken** knop.
   
    ![Knop Parameters bewerken](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Geef waarden op voor Hallo leeg parameters en selecteer Hallo **opslaan** knop. Hallo leeg parameters zijn **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, en **databaseName**.
   
    **hostingPlanName** geeft een naam voor Hallo [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **administratorLogin** Hallo gebruikersnaam voor Hallo SQL Server-beheerder. Gebruik geen veelvoorkomende beheerdersnamen als **sa** of **admin**. 
   
    Hallo **administratorLoginPassword** Hiermee geeft u een wachtwoord voor SQL Server-beheerder. Hallo **wachtwoorden opslaan als tekst zonder opmaak in het parameterbestand Hallo** optie is niet beveiligen; daarom deze optie niet selecteert. Aangezien het Hallo-wachtwoord wordt niet opgeslagen als tekst zonder opmaak, moet u op tooprovide dit wachtwoord opnieuw tijdens de implementatie. 
   
    **databaseName** geeft een naam voor Hallo database toocreate. 
   
    ![Dialoogvenster Parameters bewerken](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Kies Hallo **implementeren** knop toodeploy Hallo project tooAzure. Een PowerShell-console wordt geopend buiten Hallo Visual Studio-exemplaar. Voer SQL Server-beheerderswachtwoord Hallo in Hallo PowerShell-console wanneer u wordt gevraagd. **De PowerShell-console kan worden verborgen achter andere items of geminimaliseerd in de taakbalk Hallo.** Deze console zoekt en selecteert u het tooprovide Hallo wachtwoord.
   
   > [!NOTE]
   > Visual Studio gevraagd tooinstall hello Azure PowerShell-cmdlets. U moet hello Azure PowerShell cmdlets toosuccessfully resourcegroepen implementeren. Installeer ze als dit gevraagd wordt.
   > 
   > 
6. Hallo-implementatie kan enkele minuten duren. In Hallo **uitvoer** windows hello status van implementatie Hallo weergegeven. Wanneer het Hallo-implementatie is voltooid, geeft laatste Hallo-bericht met iets soortgelijks als in de implementatie:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. Open in een browser Hallo [Azure-portal](https://portal.azure.com/) en meld u aan tooyour-account. toosee hello resourcegroep, selecteer **resourcegroepen** en Hallo-resourcegroep geïmplementeerd.
   
    ![groep selecteren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Ziet u alle resources voor Hallo geïmplementeerd. U ziet dat Hallo-naam van Hallo storage-account is niet precies welke u hebt opgegeven bij het toevoegen van die bron. Hallo-opslagaccount moet uniek zijn. Hallo sjabloon voegt automatisch een tekenreeks met tekens toohello naam opgegeven tooprovide een unieke naam op. 
   
    ![resources weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Als u wijzigingen aanbrengen en tooredeploy uw project, kiest u Hallo bestaande resourcegroep in het snelmenu Hallo van Azure-resourcegroepproject. Kies in het snelmenu hello, **implementeren**, en kies vervolgens Hallo-resourcegroep die u hebt geïmplementeerd.
   
    ![Azure-resourcegroep geïmplementeerd](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Code implementeren in uw infrastructuur
Op dit moment wordt u Hallo infrastructuur voor uw app hebt geïmplementeerd, maar er is geen daadwerkelijke code is geïmplementeerd met Hallo-project. Dit artikel laat zien hoe toodeploy een web-app en SQL Database tabellen tijdens de implementatie. Als u een virtuele Machine in plaats van een web-app implementeert, wilt u toorun code op Hallo machine als onderdeel van de implementatie. Hallo-proces voor het implementeren van code voor een web-app of voor het instellen van een virtuele Machine bijna is identiek Hallo.

1. Toevoegen van een project tooyour Visual Studio-oplossing. Met de rechtermuisknop op het Hallo-oplossing en selecteer **toevoegen** > **nieuw Project**.
   
    ![project toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Voeg een **ASP.NET-webtoepassing** toe. 
   
    ![webtoepassing toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Selecteer **MVC**.
   
    ![MVC selecteren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Nadat Visual Studio de web-app maakt, ziet u beide projecten in Hallo-oplossing.
   
    ![projecten weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Nu moet u ervoor dat uw resourcegroepproject is op de hoogte van het nieuwe project Hallo toomake. Ga terug tooyour resourcegroepproject (AzureResourceGroup1). Klik met de rechtermuisknop op **Verwijzingen** en selecteer **Verwijzing toevoegen**.
   
    ![verwijzing toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Selecteer Hallo web-app-project dat u hebt gemaakt.
   
    ![verwijzing toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Hallo web-app-project toohello resourcegroepproject koppelen door een verwijzing toe te voegen en automatisch drie sleuteleigenschappen ingesteld. U ziet deze eigenschappen in Hallo **eigenschappen** venster voor het Hallo-verwijzing.
   
      ![verwijzing bekijken](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Hallo-eigenschappen zijn:
   
   * Hallo **aanvullende eigenschappen** hello webimplementatiepakket faseringslocatie die toohello Azure Storage wordt gepusht bevat. Houd er rekening mee Hallo-map (ExampleApp) en de bestandsnaam (pakket.zip). U moet tooknow deze waarden omdat u ze als parameters bij het implementeren van Hallo app opgeven. 
   * Hallo **bestandspad toevoegen** bevat Hallo pad waar het Hallo-pakket wordt gemaakt. Hallo **doelen** Hallo opdrachten die implementatie wordt uitgevoerd. 
   * de standaardwaarde van Hallo **bouwen; Pakket** maakt het mogelijk Hallo implementatie toobuild en maken van een webtoepassingspakket (pakket.zip).  
     
     U hoeft niet een publicatieprofiel zoals Hallo implementatie Hallo benodigde informatie opgehaald van Hallo eigenschappen toocreate Hallo pakket.
7. Ga terug tooWebSiteSQLDatabase.json en voeg een resource toohello sjabloon.
   
    ![resource toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Selecteer deze keer **Webimplementatie voor Web Apps**. 
   
    ![webimplementatie toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. De resourcegroep voor resource groep project toohello implementeren. Deze keer zijn er enkele nieuwe parameters. U hoeft geen waarden voor tooprovide **_artifactsLocation** of **_artifactsLocationSasToken** omdat deze waarden door Visual Studio automatisch gegenereerd. Maar u hebt tooset Hallo map en bestandsnaam toohello pad dat het implementatiepakket Hallo bevat (weergegeven als **ExampleAppPackageFolder** en **ExampleAppPackageFileName** in Hallo na installatiekopie ). Hallo-waarden die u eerder in gezien Hallo verwijzingseigenschappen bevatten (**ExampleApp** en **pakket.zip**).
   
    ![webimplementatie toevoegen](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Voor Hallo **opslagaccountartefact**, selecteer Hallo een geïmplementeerd met deze resourcegroep.
10. Nadat het Hallo-implementatie is voltooid, selecteert u uw web-app in Hallo-portal. Hallo URL toobrowse toohello site selecteren.
    
     ![naar site bladeren](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. U ziet dat er Hallo standaard ASP.NET-app is geïmplementeerd.
    
     ![geïmplementeerde app weergeven](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Volgende stappen
* toolearn over het beheren van uw resources via de portal hello, Zie [Using hello Azure portal toomanage uw Azure-resources](resource-group-portal.md).
* toolearn meer informatie over sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

