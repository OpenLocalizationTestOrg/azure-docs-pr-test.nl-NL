---
title: aaaProvision en microservices zoals verwacht in Azure implementeren
description: "Meer informatie over hoe een toepassing toodeploy bestaat uit microservices in Azure App Service als één eenheid en in een voorspelbare wijze met JSON resource group-sjablonen en PowerShell-scripts."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Inrichten en microservices zoals verwacht in Azure implementeren
Deze zelfstudie laat zien hoe tooprovision en implementeer een toepassing die bestaat uit [microservices](https://en.wikipedia.org/wiki/Microservices) in [Azure App Service](/services/app-service/) als één eenheid en in een voorspelbare wijze JSON resource group-sjablonen en PowerShell-scripts. 

Bij het inrichten en implementeren van hoge schaalbaarheid toepassingen die zijn samengesteld van maximaal losgekoppelde microservices, zijn herhaalbaarheid en voorspelbaarheid cruciaal toosuccess. [Azure App Service](/services/app-service/) kunt u toocreate microservices met web-apps, mobiele apps, API-apps en logic apps. [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kunt u toomanage alle Hallo microservices als een eenheid, samen met bronafhankelijkheden zoals instellingen voor beheer en de bron. U kunt nu ook dergelijke toepassing met behulp van JSON-sjablonen en eenvoudig PowerShell-scripts implementeren. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Wat u doet
In de zelfstudie hello implementeert u een toepassing die gebruikmaakt van:

* Twee web-apps (dat wil zeggen twee microservices)
* Een back-end SQL-Database
* App-instellingen, verbindingsreeksen en bronbeheer
* Application insights, waarschuwingen, instellingen voor automatisch schalen

## <a name="tools-you-will-use"></a>Hulpprogramma's die u wilt gebruiken
In deze zelfstudie gebruikt u Hallo hulpprogramma's te volgen. Omdat het geen uitgebreide bespreking van de hulpprogramma's, ik ben toostick toohello end-to-end scenario gaat en net bieden u een tooeach korte inleiding en waar u meer informatie over deze kunt vinden. 

### <a name="azure-resource-manager-templates-json"></a>Azure Resource Manager-sjablonen (JSON)
Telkens wanneer u een web-app in Azure App Service maakt, Azure Resource Manager gebruikt bijvoorbeeld een JSON-sjabloon toocreate Hallo hele resourcegroep met de Hallo onderdeel resources. Een complexe sjabloon van Hallo [Azure Marketplace](/marketplace) zoals Hallo [schaalbare WordPress](/marketplace/partners/wordpress/scalablewordpress/) app Hallo MySQL-database, opslagaccounts, Hallo App Service-abonnement, Hallo web-app zelf, waarschuwingsregels, app kunt opnemen instellingen, instellingen voor automatisch schalen en meer en alle deze sjablonen zijn beschikbaar tooyou via PowerShell. Voor informatie over hoe toodownload en gebruik deze sjablonen zien [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).

Zie voor meer informatie over hello Azure Resource Manager-sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>2.6 Azure SDK voor Visual Studio
Hallo bevat nieuwste SDK verbeteringen toohello sjabloonondersteuning voor Resource Manager-in Hallo JSON-editor. U kunt deze tooquickly een resource group-sjabloon maken vanaf het begin of open een bestaande JSON-sjabloon (zoals een gedownloade gallery-sjabloon) voor wijziging, Hallo parameterbestand vullen en zelfs implementeren Hallo resourcegroep rechtstreeks van een Azure Resourcegroep oplossing.

Zie voor meer informatie [2.6 van de Azure SDK voor Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 of hoger
Vanaf versie 0.8.0, bevat hello Azure PowerShell-installatie hello Azure Resource Manager-module in toevoeging toohello Azure-module. Deze nieuwe module kunt u tooscript Hallo implementatie van resourcegroepen.

Zie voor meer informatie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Azure Resource Explorer
Dit [voorbeeldfunctie](https://resources.azure.com) kunt u tooexplore Hallo JSON definities van alle Hallo resourcegroepen in uw abonnement en Hallo afzonderlijke resources. In Hallo-hulpprogramma kunt u Hallo JSON definities van een resource te bewerken, verwijderen van de gehele hiërarchie van resources en maken van nieuwe resources.  Hallo informatie direct beschikbaar is in dit hulpprogramma is erg handig voor het ontwerpen van een sjabloon omdat hier u wat ziet u nodig hebt tooset voor een bepaald type resource, hello eigenschappen corrigeren waarden, enzovoort. U kunt zelfs uw resourcegroep maken in Hallo [Azure Portal](https://portal.azure.com/), Controleer de definities van JSON in Hallo explorer hulpprogramma toohelp templatize u Hallo resourcegroep.

### <a name="deploy-tooazure-button"></a>TooAzure implementatieknop
Als u GitHub voor broncodebeheer gebruikt, kunt u plaatsen een [implementeren tooAzure knop](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) in de Leesmij-bestand. MD, waardoor een directe implementatie UI tooAzure. Terwijl u dit voor een eenvoudige web-app doen kunt, kunt u deze tooenable een hele resourcegroep implementeren door het plaatsen van een bestand azuredeploy.json in de hoofdmap van de opslagplaats Hallo uitbreiden. Deze JSON-bestand dat Hallo resource group-sjabloon bevat, wordt gebruikt door Hallo implementeren tooAzure knop toocreate Hallo met resourcegroep. Zie voor een voorbeeld Hallo [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) voorbeeld, gaat u in deze zelfstudie.

## <a name="get-hello-sample-resource-group-template"></a>Resource Hallo-groep voorbeeldsjabloon ophalen
Nu gaan we aan de juiste tooit.

1. Navigeer toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) voorbeeld-App Service.
2. Klik in de readme.md, **tooAzure implementeren**.
3. U bent toohello ondernomen [implementeren naar azure](https://deploy.azure.com) site en gestelde tooinput implementatieparameters. U ziet dat de meeste van Hallo velden zijn gevuld met naam van de opslagplaats Hallo en sommige willekeurige tekenreeksen voor u. U kunt alle Hallo velden wijzigen als u wilt, maar Hallo alleen dingen die u hebt tooenter beheerdersrechten Hallo SQL Server-aanmelding en Hallo wachtwoord en klik vervolgens op **volgende**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Klik vervolgens op **implementeren** toostart Hallo-implementatieproces. Zodra het Hallo-proces wordt uitgevoerd toocompletion, klikt u op Hallo http://todoapp*XXXX*. azurewebsites.net koppeling toobrowse Hallo toepassing is geïmplementeerd. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hallo UI zou enigszins traag zijn als u eerst tooit bladert omdat Hallo apps alleen worden gestart, maar zelf te overtuigen dat het een toepassing volledig functioneel is.
5. Klik op Hallo terug op de pagina voor het implementeren van Hallo **beheren** toosee Hallo nieuwe toepassing in Azure Portal Hallo koppelen.
6. In Hallo **Essentials** dropdown, klikt u op Hallo resource group-koppeling. Opmerking ook die Hallo web-app al is verbonden toohello GitHub-opslagplaats onder **extern Project**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. In de resourcegroepblade hello, houd er rekening mee dat er al twee web-apps en één SQL-Database in de resourcegroep Hallo zijn.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Alles wat u hebt gezien in enkele korte minuten is een volledig geïmplementeerde twee-microservice-toepassing, met alle Hallo onderdelen, afhankelijkheden, instellingen, database en continue publicatie ingesteld door een geautomatiseerde orchestration in Azure Resource Manager. Dit alles is uitgevoerd door twee dingen:

* Hallo implementeren tooAzure knop
* azuredeploy.JSON in Hallo opslagplaats hoofdmap

U kunt deze dezelfde toepassing implementeren tientallen, honderden of duizenden malen en Hallo exact dezelfde configuratie elke keer hebben. Hallo herhaalbaarheid en Hallo voorspelbaarheid van deze benadering kunt u toodeploy hoge-toepassingen met gemak en betrouwbaarheid.

## <a name="examine-or-edit-azuredeployjson"></a>Bekijk AZUREDEPLOY (of bewerken). JSON
Nu gaan we kijken hoe Hallo GitHub-opslagplaats is ingesteld. U Hallo JSON-editor gebruikt in hello Azure .NET SDK, dus als u nog niet hebt geïnstalleerd [Azure .NET SDK 2.6](/downloads/), dat nu doen.

1. Kloon Hallo [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats met uw favoriete git-hulpprogramma. In onderstaande Hallo schermafbeelding, ben ik dit doen in Hallo Team Explorer in Visual Studio 2013.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Open azuredeploy.json in Visual Studio in de hoofdmap van de opslagplaats hello. Als u het JSON-overzichtsvenster Hallo niet ziet, moet u tooinstall Azure .NET SDK.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Ik ben niet gaat toodescribe elk detail van Hallo JSON-indeling, maar Hallo [meer bronnen](#resources) sectie bevat koppelingen voor het leren van Hallo resource groep sjabloontaal. NET ga ik hier tooshow u Hallo interessante functies die u kunnen helpen bij het maken van uw eigen aangepaste sjabloon voor app-implementatie aan de slag.

### <a name="parameters"></a>Parameters
Kijk eens naar Hallo parameters sectie toosee dat de meeste van deze parameters welke Hallo zijn **tooAzure implementeren** knop tooinput wordt u gevraagd. Hallo site achter Hallo **tooAzure implementeren** knop Hallo invoer UI gevuld met Hallo gedefinieerde parameters in azuredeploy.json. Deze parameters worden gebruikt in de resourcedefinities Hallo zoals resourcenamen, eigenschapswaarden, enz.

### <a name="resources"></a>Resources
In knooppunt Hallo-bronnen ziet u dat 4 op het hoogste niveau resources zijn gedefinieerd, met inbegrip van een SQL Server-exemplaar, een App Service-plan en twee web-apps. 

#### <a name="app-service-plan"></a>App Service-plan
Laten we beginnen met een eenvoudige hoofdniveau resource in Hallo JSON. Klik op Hallo App Service-abonnement met de naam in JSON-overzicht hello, **[hostingPlanName]** toohighlight Hallo bijbehorende JSON-code. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Houd er rekening mee dat Hallo `type` element geeft Hallo-tekenreeks voor een App Service-abonnement (het is wel een serverfarm een lange, lange tijd geleden), en andere elementen en eigenschappen worden ingevuld met behulp van Hallo gedefinieerde parameters in JSON-bestand Hallo en deze bron heeft geen alle ingesloten resources.

> [!NOTE]
> U ziet ook dat Hallo de waarde van `apiVersion` vertelt Azure welke versie van Hallo REST-API toouse Hallo JSON resourcedefinitie met, maar kan beïnvloeden hoe Hallo resource moet worden opgemaakt in Hallo `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Klik op Hallo SQL Server-bron met de naam **SQLServer** in Hallo JSON-overzicht.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Opmerking Hallo volgen over Hallo gemarkeerd JSON-code:

* Hallo-gebruik van parameters zorgt ervoor dat Hallo gemaakt zijn met de naam en bronnen op een manier die zorgt ervoor dat ze consistent zijn met elkaar zijn geconfigureerd.
* Hallo SQLServer resource heeft twee ingesloten resources, elk een andere waarde voor `type`.
* Hallo genest bronnen binnen `“resources”: […]`, waarbij Hallo-database en Hallo firewallregels zijn gedefinieerd, hebben een `dependsOn` element waarmee wordt aangegeven Hallo bron-ID van Hallo hoofdniveau SQLServer resource. Dit vertelt Azure Resource Manager 'voordat u deze resource die andere resources moet al bestaan; maken en als die andere resource is gedefinieerd in de sjabloon hello, maakt u dat een eerst'.
  
  > [!NOTE]
  > Voor gedetailleerde informatie over het toouse hello `resourceId()` werkt, Zie [Azure Resource Manager-sjabloonfuncties](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* effect van Hallo Hallo `dependsOn` -element is dat Azure Resource Manager weten kunt welke resources parallel kunnen worden gemaakt en welke resources moeten opeenvolgend worden gemaakt. 

#### <a name="web-app"></a>Web-app
Nu gaan we toohello Werkelijke web-apps zelf, die gecompliceerder zijn. Klik op Hallo [variables('apiSiteName')] web-app in Hallo JSON-overzicht toohighlight de JSON-code. U zult zien dat dingen zijn het veel meer interessant. Voor dit doel bespreken ik Hallo functies, één voor één:

##### <a name="root-resource"></a>Basis-resource
Hallo-web-app, is afhankelijk van twee verschillende bronnen. Dit betekent dat Azure Resource Manager Hallo web-app wordt maken nadat beide Hallo App Service-abonnement en Hallo SQL Server-exemplaar worden gemaakt.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>App-instellingen
Hallo app-instellingen zijn ook gedefinieerd als een geneste resource.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

In Hallo `properties` element voor `config/appsettings`, hebt u twee appinstellingen in de indeling Hallo `“<name>” : “<value>”`.

* `PROJECT`is een [KUDU instelling](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) die vertelt Azure-implementatie welke toouse project in een meerdere project Visual Studio-oplossing. Leest u hoe broncodebeheer is geconfigureerd, maar omdat Hallo ToDoApp code zich in een meerdere project Visual Studio-oplossing, moet deze instelling.
* `clientUrl`is gewoon een instelling van die toepassing hello code app gebruikt.

##### <a name="connection-strings"></a>Verbindingsreeksen
Hallo-verbindingsreeksen zijn ook gedefinieerd als een geneste resource.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

In Hallo `properties` element voor `config/connectionstrings`, elke verbindingsreeks ook is gedefinieerd als een combinatie van naam: waarde, met specifieke notatie Hallo `“<name>” : {“value”: “…”, “type”: “…”}`. Voor Hallo `type` element mogelijke waarden zijn `MySql`, `SQLServer`, `SQLAzure`, en `Custom`.

> [!TIP]
> Uitvoeren voor een definitieve lijst van de tekenreeks verbindingstypen Hallo Hallo-opdracht in Azure PowerShell te volgen: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Resourcebeheer
instellingen voor bronbeheer Hallo zijn ook gedefinieerd als een geneste resource. Azure Resource Manager gebruikt deze continue publiceren van bronnen tooconfigure (Zie voorbehoud op `IsManualIntegration` later) en ook tookick uitschakelen Hallo-implementatie van toepassingscode automatisch tijdens de verwerking van Hallo van Hallo JSON-bestand.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`en `branch` moet vrij intuïtieve en toohello Git-opslagplaats en Hallo naam van Hallo vertakking toopublish van moet verwijzen. Deze worden opnieuw, gedefinieerd door de invoerparameters. 

Let op Hallo `dependsOn` element dat in de toevoeging toohello web-app-resource zelf, `sourcecontrols/web` ook afhankelijk van `config/appsettings` en `config/connectionstrings`. Dit is omdat zodra `sourcecontrols/web` is geconfigureerd, hello Azure implementatieproces wordt automatisch geprobeerd toodeploy, bouwen en toepassingscode hello te starten. Daarom heeft invoegen van deze afhankelijkheid kunt u ervoor zorgen die toepassing hello toegang toohello vereist app-instellingen en verbindingsreeksen voordat Hallo toepassingscode wordt uitgevoerd. 

> [!NOTE]
> U ziet ook dat `IsManualIntegration` te is ingesteld`true`. Deze eigenschap is in deze zelfstudie nodig omdat u niet uw eigendom Hallo GitHub-opslagplaats en dus kan geen daadwerkelijk machtiging tooAzure tooconfigure continue publiceren vanaf verlenen [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (dat wil zeggen push automatische opslagplaats updates tooAzure). U kunt de standaardwaarde Hallo `false` voor Hallo opgegeven bibliotheek alleen als u van de eigenaar van het Hallo GitHub referenties hebt geconfigureerd in Hallo [Azure-portal](https://portal.azure.com/) voordat. Met andere woorden, als u bron besturingselement tooGitHub of BitBucket hebt ingesteld voor een app in Hallo [Azure Portal](https://portal.azure.com/) voorheen werd door gebruik te maken van uw referenties, vervolgens Azure wordt Hallo referenties onthouden en ze gebruiken wanneer u een app van implementeren GitHub of BitBucket in toekomstige Hallo. Echter, als u dit nog niet hebt gedaan, Hallo JSON-sjabloon mislukt de implementatie van wanneer Azure Resource Manager probeert de instellingen voor bronbeheer tooconfigure Hallo van web-app omdat deze niet kan op GitHub of BitBucket met referenties Hallo opslagplaats eigenaar aanmelden.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Hallo JSON-sjabloon met de geïmplementeerde resourcegroep vergelijken
Hier, doorloopt u de blades alle Hallo van web-app in Hallo [Azure Portal](https://portal.azure.com/), maar er is een ander hulpprogramma dat net zoals handig als niet meer. Ga toohello [Azure Resource Explorer](https://resources.azure.com) voorbeeldfunctie waarmee u een JSON-weergave van alle Hallo resourcegroepen in uw abonnementen, omdat ze werkelijk bestaan in hello Azure back-end. U ziet ook hoe Hallo-resourcegroep van JSON-hiërarchie in Azure komt overeen met de Hallo hiërarchie in Hallo sjabloonbestand dat toocreate gebruikt deze.

Bijvoorbeeld, wanneer ik toohello gaat [Azure Resource Explorer](https://resources.azure.com) hulpprogramma en vouw de knooppunten Hallo in Verkenner hello, ik ziet Hallo-resourcegroep en Hallo hoofdniveau resources die worden verzameld onder hun respectieve resourcetypen.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Als u de web-app tooa detailanalyse, moet u kunnen toosee web app configuration details vergelijkbare toohello onderstaande schermafbeelding:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Opnieuw hello ingesloten resources moet een hiërarchie vergelijkbaar toothose in uw bestand JSON-sjabloon en ziet u Hallo app-instellingen, verbindingsreeksen, enzovoort, juist in Hallo JSON deelvenster worden weergegeven. Hallo afwezigheid van instellingen kan wijzen op een probleem met uw JSON-bestand en kunt u uw JSON-sjabloonbestand oplossen.

## <a name="deploy-hello-resource-group-template-yourself"></a>Implementeren van Hallo resource group-sjabloon
Hallo **tooAzure implementeren** knop is een goede, maar kunt u toodeploy Hallo resource group-sjabloon in azuredeploy.json alleen als u hebt al azuredeploy.json tooGitHub gepusht. Hello Azure .NET SDK biedt ook Hallo hulpmiddelen voor toodeploy u elk bestand JSON-sjabloon rechtstreeks vanuit uw lokale computer. toodo deze, Hallo stappen hieronder:

1. Klik in Visual Studio **bestand** > **nieuw** > **Project**.
2. Klik op **Visual C#** > **Cloud** > **Azure-resourcegroep**, klikt u vervolgens op **OK**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. In **Azure-sjabloon selecteren**, selecteer **lege sjabloon** en klik op **OK**.
4. Sleep azuredeploy.json naar Hallo **sjabloon** map van het nieuwe project.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. Open in Solution Explorer azuredeploy.json Hallo gekopieerd.
6. Alleen voor Hallo mogelijk te houden van Hallo demonstratie, gaan we toevoegen sommige standaard Application Insight resources tooour JSON-bestand, door te klikken op **Resource toevoegen**. Als u alleen geïnteresseerd bent in JSON-bestand Hallo implementeren, gaat u verder toohello stappen implementeren.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Selecteer **Application Insights voor Web-Apps**, Controleer of een bestaande App Service-plan en web app is geselecteerd en klik vervolgens op **toevoegen**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   U hebt nu kunnen toosee worden diverse nieuwe bronnen, afhankelijk van het Hallo-resource en wat het doet, afhankelijk van beide Hallo App Service plan of Hallo web-app zijn. Deze resources niet zijn ingeschakeld in hun bestaande definitie en u gaat toochange die.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. Klik in de JSON-overzicht hello, op **appInsights automatisch schalen** toohighlight de JSON-code. Dit is Hallo schalen van de instelling voor uw App Service-abonnement.
9. In Hallo gemarkeerde JSON-code, zoek Hallo `location` en `enabled` eigenschappen en ze te stellen zoals hieronder wordt weergegeven.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. Klik in de JSON-overzicht hello, **CPUHigh appInsights** toohighlight de JSON-code. Dit is een waarschuwing.
11. Zoek Hallo `location` en `isEnabled` eigenschappen en ze te stellen zoals hieronder wordt weergegeven. Hello dezelfde voor Hallo andere drie waarschuwingen (paarse bollen).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. U bent nu klaar toodeploy. Met de rechtermuisknop op het Hallo-project en selecteer **implementeren** > **nieuwe implementatie**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Meld u aan bij uw Azure-account als u dat nog niet hebt gedaan.
14. Selecteer een bestaande resourcegroep in uw abonnement of maak een nieuwe één, selecteer **azuredeploy.json**, en klik vervolgens op **Parameters bewerken**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    U zult nu kunnen tooedit alle Hallo parameters die zijn gedefinieerd in Hallo sjabloonbestand in een tabel nice. Parameters die standaardwaarden definiëren al hun standaardwaarden en parameters die een lijst van toegestane waarden te definiëren als opgegeven waarin dropdowns worden weergegeven.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Vul alle Hallo leeg parameters en gebruik Hallo [GitHub-repo-adres voor ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) in **repoUrl**. Klik vervolgens op **opslaan**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > Automatisch schalen is een functie die wordt aangeboden op **standaard** laag of hoger en plan niveau waarschuwingen zijn functies die worden aangeboden **Basic** servicetier of hoger, moet u tooset hello **sku** parameter te**standaard** of **Premium** in volgorde toosee al uw nieuwe App Insights resources lichte up.
    > 
    > 
16. Klik op **implementeren**. Als u hebt geselecteerd **wachtwoorden opslaan**, Hallo wachtwoord wordt opgeslagen in het parameterbestand Hallo **als tekst zonder opmaak**. Anders wordt u gevraagd tooinput Hallo databasewachtwoord tijdens het implementatieproces Hallo.

Dat is alles. Nu u alleen toogo toohello hoeft [Azure Portal](https://portal.azure.com/) en Hallo [Azure Resource Explorer](https://resources.azure.com) hulpprogramma toosee Hallo nieuwe waarschuwingen en instellingen voor automatisch schalen toegevoegd tooyour JSON-toepassing geïmplementeerd.

De stappen in deze sectie u hoofdzakelijk Hallo volgende doen:

1. Voorbereide Hallo-sjabloonbestand
2. Een parameter bestand toogo gemaakt met Hallo-sjabloonbestand
3. Geïmplementeerde Hallo sjabloonbestand met Hallo parameterbestand

de laatste stap Hallo eenvoudig doet u door een PowerShell-cmdlet. toosee Visual Studio heeft wanneer deze uw toepassing, open Scripts\Deploy-AzureResourceGroup.ps1 geïmplementeerd. Er is veel code er maar ik ben toohighlight NET gaan alle Hallo-relevante code, moet u toodeploy Hallo sjabloonbestand met Hallo parameterbestand.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

laatste cmdlet Hallo `New-AzureResourceGroup`, is Hallo die daadwerkelijk Hallo-actie uitvoert. Dit alles moet tooyou dat aan de hand van de Hallo van tooling, betrekkelijk eenvoudig toodeploy is demonstreren uw cloud toepassing zoals verwacht. Telkens wanneer u Hallo cmdlet uitvoeren op Hallo Hallo dezelfde sjabloon met dezelfde parameterbestand, gaat u tooget Hallo hetzelfde resultaat.

## <a name="summary"></a>Samenvatting
In DevOps zijn herhaalbaarheid en voorspelbaarheid sleutels tooany geslaagde implementatie van een toepassing met hoge schaalbaarheid van microservices bestaan. In deze zelfstudie maakt hebt u een toepassing twee microservice tooAzure geïmplementeerd als één resourcegroep hello Azure Resource Manager-sjabloon. In het ideale geval, heeft deze gegeven u Hallo kennis die u nodig hebt in volgorde toostart converteren van uw toepassing in Azure in een sjabloon en kunt inrichten en implementeren deze zoals verwacht. 

## <a name="next-steps"></a>Volgende stappen
Ontdek hoe u kunt te[flexibele methoden toepassen en uw toepassing microservices continu publiceren met gemak](app-service-agile-software-development.md) en technieken voor toepassingsimplementatie zoals geavanceerde [zeker implementatie](app-service-web-test-in-production-controlled-test-flight.md) eenvoudig.

<a name="resources"></a>

## <a name="more-resources"></a>Meer bronnen
* [Taal van Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure Resource Manager-sjabloonfuncties](../azure-resource-manager/resource-group-template-functions.md)
* [Implementeer een toepassing met Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Implementaties van de resourcegroep in Azure oplossen](../azure-resource-manager/resource-manager-common-deployment-errors.md)

