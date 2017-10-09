---
title: 'MyDriving Azure IoT-voorbeeld: samenstellen | Microsoft Docs'
description: Een app die is een uitgebreide demonstratie van het bouwen tooarchitect een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Bouw en implementeer Hallo MyDriving oplossing tooyour omgeving
MyDriving is een Internet der dingen (IoT)-oplossing die u verzamelt gegevens uit uw auto, verwerkt met behulp van machine learning en geeft deze op uw mobiele telefoon. Hallo back-end bestaat uit diverse services geleverd door Microsoft Azure. Hallo-clients kunnen Android, iOS of Windows 10 Phone zijn.

Wij Hallo MyDriving oplossing toogive u snel aan de slag bij het maken van uw eigen IoT-systeem. Van Hallo [MyDriving opslagplaats op GitHub](https://github.com/Azure-Samples/MyDriving), krijgt u Azure Resource Manager scripts toodeploy Hallo back-end-architectuur in uw eigen Azure-account. Vanaf dat moment kunt u Hallo verschillende services configureren, Hallo query's toosuit uw eigen gegevens wijzigen en enzovoort. U vindt deze scripts--samen met de code voor de mobiele app hello, hello Azure App Service API-project en meer--in Hallo MyDriving opslagplaats.

Als u Hallo app nog niet hebt geprobeerd, bekijkt hello [Get-handleiding](iot-solution-get-started.md).

Er is een gedetailleerd overzicht van Hallo-architectuur in Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs). Kortom, er zijn verschillende dat we ingesteld toocreate een vergelijkbaar project:

* Een **clientapp** wordt uitgevoerd op Android, iOS en Windows 10 Phone-telefoons. We gebruiken Hallo Xamarin platform tooshare veel van Hallo code, die is opgeslagen op GitHub onder `src/MobileApp`. Hallo-app voert daadwerkelijk twee afzonderlijke functies uit:
  * Deze organisatiebeveiligingstokens telemetrie uit Hallo on-board diagnostics (OBD)-apparaat en een eigen locatie service toohello systeem cloud back-end.
  * Het is een gebruikersinterface waarin gebruikers kunnen zoeken over hun reizen opgenomen weg.
* Een **cloudservice** Hallo weg reis gegevens in real-time opgenomen en verwerkt deze. Hallo belangrijkste werk voor het maken van deze service is toochoose, voorzien en bekabelen van tal van Azure-services. Sommige onderdelen Hallo vereist scripts toofilter en proces Hallo binnenkomende gegevens. We gebruiken een Azure Resource Manager-sjabloon tooconfigure alle Hallo delen.
* Een **mobiele service app** Hallo webservice achter Hallo gebruikersinterface onderdeel van de app Hallo-apparaat is. De belangrijkste taak is tooquery Hallo-database opgeslagen, verwerkt gegevens. De code op GitHub onder is `src/MobileAppService`.
* **Visual Studio met Xamarin** is onze ontwikkelomgeving. Xamarin dat bestaat als een onderdeel van de Visual Studio en als een zelfstandige integrated development environment (IDE), wordt gebruikt toobuild Hallo platformoverschrijdende apparaatcode. toobuild hello iOS code is noodzakelijk toohave een exemplaar van het Xamarin uitgevoerd op een OS X-machine. Indien nodig, kan deze worden uitgevoerd als een agent, beheerd vanuit Visual Studio.
* **Testen van de eenheden** Hallo apparaat apps in Xamarin-Testcloud wordt uitgevoerd.
* **GitHub** is Hallo opslagplaats waar we alle Hallo code, scripts en sjablonen opslaat.
* **Visual Studio Team Services** is een cloudservice die is gebruikt toomanage Hallo continue bouwen en testen van Hallo web service en apparaat-apps.
* **HockeyApp** gebruikte toodistribute releases van Hallo apparaatcode is. Verzamelt ook crashes en gebruik rapporten en feedback van gebruikers.
* **Visual Studio Application Insights** monitors Hallo mobiele web-service.

Dus gaan we kijken hoe we ingesteld dat alle. 

> [!NOTE] 
> Veel van de volgende stappen uit Hallo zijn optioneel.
>
>

## <a name="sign-up-for-accounts"></a>Aanmelden voor accounts
* [Visual Studio Developer Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Dit gratis programma biedt eenvoudige toegang toomany ontwikkelhulpprogramma's en services, zoals Visual Studio, Visual Studio Team Services en Azure. Dit biedt u een creditcard $25 per maand op Azure voor twaalf maanden. Dit omvat ook abonnementen tooPluralsight trainings- en Xamarin universiteit. U kunt ook aanmelden afzonderlijk voor gratis lagen van [Azure](https://azure.com) en [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), maar deze geen Azure-tegoed.
* [HockeyApp](https://rink.hockeyapp.net/) (optioneel), voor het beheren van de test-distributie van mobiele apps en het verzamelen van telemetrie.
* [Xamarin](https://xamarin.com/) (vereist), voor het bouwen van de mobiele app Hallo en actieve foutopsporing wordt uitgevoerd en tests op [Xamarin-Testcloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (optioneel), toocreate gratis openbare opslagplaatsen voor uw eigen code (persoonlijke opslagplaatsen betaald). U kunt ook Hallo basisniveau in Visual Studio Team Services voor privé-opslagplaatsen.
* [Power BI](https://powerbi.microsoft.com/) (optioneel) toocreate uitgebreide afbeeldingen van gegevens over het hele systeem Hallo.

> [!NOTE]
> U hoeft niet met een account tooaccess Hallo MyDriving code in GitHub [GitHub MyDriving-opslagplaats Hallo](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Ontwikkelingsprogramma's installeren
Hallo volgende instellingen zijn voor het ontwikkelen van de volledige oplossing Hallo: een iOS-, Android- en Windows 10 Mobile platformoverschrijdende-app met een Azure back-end.

Als alternatief kunt u Xamarin Studio in Mac of Windows toodevelop Hallo mobile apps als u niet werken op Hallo Azure back-end.

Er is een [langere beschrijving van deze installatie](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Windows-ontwikkelcomputer
Hallo centrale hulpprogramma in Windows is Visual Studio voor het werken met Hallo MyDriving app voor Android en Windows, Hallo-App Service API-project en microservice-extensies.

Xamarin, Git emulators en andere onderdelen nuttig zijn alle geïntegreerd met Visual Studio.

Installeren:

* [Visual Studio met Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (elke editie--Community is gratis).
* [SQLite voor Universal Windows Platform](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Toobuild hello Windows 10 Mobile-code vereist.
* [Azure SDK voor Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Biedt u Hallo SDK voor apps in Azure, samen met de opdrachtregelprogramma's voor het beheren van Azure wordt uitgevoerd.
* [Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Vereiste toobuild hello [microservice](../service-fabric/service-fabric-get-started.md) extensie.

Zorg ervoor dat u de juiste Visual Studio-serverextensies Hallo hebt. Controleer of onder **extra**, ziet u **Android, iOS, Xamarin...** . Als dit niet het geval is, Visual Studio niet openen, zoekt u Xamarin en volg Hallo prompts tooinstall deze. Controleer ook of **Git voor Windows** is geïnstalleerd. Als deze niet in de Visual Studio, zoeken en volg Hallo prompts tooinstall deze. 

### <a name="mac-development-machine"></a>Mac-ontwikkelcomputer
Hallo Mac (Yosemite of hoger) is vereist als u wilt dat toodevelop voor iOS. Hoewel we Visual Studio met Xamarin op Windows-toodevelop gebruiken en alle Hallo code beheren, Xamarin maakt gebruik van een agent is geïnstalleerd op een Mac in volgorde toobuild en aanmelding Hallo iOS-code.

![Voor Windows ontwikkelen en bouwen op Mac](./media/iot-solution-build-system/image1.png)

(Als alternatief kunt u Xamarin Studio rechtstreeks op Hallo Mac toodevelop platformoverschrijdende apps.)

U hoeft niet Hallo Mac als u niet tooinclude iOS als doelplatform wilt.

Installeren:

* [Xamarin Studio voor iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). U kunt ook Visual Studio en Xamarin op een Mac met een virtuele Windows-computer instellen. Zie [-installatie, installatie en verificaties voor Mac-gebruikers](https://msdn.microsoft.com/library/mt488770.aspx) op MSDN.
* [Azure ontwikkelingsprogramma's](https://azure.microsoft.com/downloads/) (optioneel).

Inschakelen van externe aanmelding op Hallo Mac. Open **Systeemvoorkeuren** > **delen**, en selecteer vervolgens **externe aanmelding**.

Wanneer u een iOS-project in Visual Studio in Windows opent, wordt Hallo Xamarin-invoegtoepassing u gevraagd voor ID Hallo Hallo Mac.

## <a name="fetch-hello-github-repository"></a>Hallo GitHub-opslagplaats ophalen
Ophalen van een lokale kopie van [GitHub MyDriving-opslagplaats Hallo](https://github.com/Azure-Samples/MyDriving) met behulp van Hallo **ZIP downloaden** knop in GitHub, Visual Studio of een andere Git-client.

Pak Hallo tooa map met een korte padnaam, zoals C:\\code.

U kunt ook als u wilt dat tookeep up toodate met of tooour code bijdragen, Hallo opslagplaats klonen als volgt:

**GIT kloon https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Een Bing maps API-sleutel ophalen
[Registreren voor een Bing kaarten-API-sleutel](https://msdn.microsoft.com/library/ff428642.aspx).

U moet dit in 22 in regel tooreplace `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Hallo demo-app bouwen
Deze oplossingen openen in Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Krijgt u de aanwijzingen voor het:

* Vertrouwen van sommige mogelijk onbetrouwbare projecten. Kies tooopen ze als u wilt dat toogo vooruit.
* Modus voor ontwikkelaars instellen als u op een nieuwe Windows 10-computer werkt.
* Geef uw Xamarin-referenties.
* Verbinding maken met toohello Xamarin Mac. Als u een Mac hebt, klik met de rechtermuisknop Hallo iOS in Visual Studio-project en selecteer vervolgens **Unload project**.

Hallo-oplossing opnieuw maakt.

Hebt u problemen bij het bouwen, probeert u Hallo oplossingen tooquirks die we hebben gevonden:

* *VINLookupApplication project niet laden*: Controleer of u Hallo geïnstalleerd [Azure SDK voor Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Service Fabric-project niet onderhouden*: eerst Hallo interface projecten bouwen en controleer of u Hallo Service Fabric SDK geïnstalleerd.
* *Android-app niet onderhouden*:
  
  * Open **extra** > **Android** > **Android SDK Manager**, en zorg ervoor dat Android 6 (API 23) / Platform SDK is geïnstalleerd.
  * Deze map te verwijderen en vervolgens opnieuw maken:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Tooknow hello code ophalen
Hallo-oplossing, hebt u:

* Azure-extensies: Service Fabric.
* Azure HDInsight: Scripts voor het verwerken van reis gegevens in Azure.
* Mobiele Apps: apps Hallo apparaten.
* MobileAppsService/MyDrivingService: Hallo web terug eindigen.
* Power BI: Hallo rapportdefinitie.
* Scripts:
  
  * Resource Manager: sjablonen toobuild hello Azure-resources.
  * PowerShell: Scripts toorun Hallo Resource Manager-sjablonen.
  * Azure SQL Database: Foutopsporing databases.
* SQL Database: CreateTables: schemadefinities.
* Azure Stream Analytics: Een query die transformatie Hallo binnenkomende gegevensstroom.

## <a name="run-hello-apps-in-development-mode"></a>Hallo-apps uitvoeren in de Ontwikkelingsmodus
Onderneem actie toorun Hallo-apps, op basis van het Hallo-apparaat dat u gebruikt:

* Back-end: MyDrivingService instellen als opstartproject Hallo en druk op F5 toorun Hallo back-end-webservice. Een browserweergave van Hallo API aanbieding wordt geopend.
* Mobiele clients: Hallo [mobiele apps zijn ontwikkeld in Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: Zie voor meer informatie [Android foutopsporing in Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: Zie voor meer informatie [foutopsporing in iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: Zie voor meer informatie [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Hallo mobiele app tooHockeyApp uploaden
HockeyApp beheert Hallo distributie van uw Android, iOS of Windows-app tootest gebruikers verwittigen van gebruikers met nieuwe releases. Verzamelt ook nuttig foutenrapporten, feedback van gebruikers met schermafbeeldingen en meetgegevens voor softwaregebruik.

[Start met uploaden van](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) uw build-app. Meld u vervolgens aan te[HockeyApp](https://rink.hockeyapp.net) van uw ontwikkelcomputer. Klik op dashboard Hallo voor ontwikkelaars, **nieuwe App**, en sleep Hallo gebouwd bestanden naar Hallo-venster. (Later kunt u automatiseren uw service build toodo dit.)

U kunt nu in uw app-dashboard.

![Overzichtstabblad op Hallo app-dashboard](./media/iot-solution-build-system/image2.png)

Hallo proces herhalen voor elk platform dat uw app wordt uitgevoerd op. Vervolgens kunt u doen Hallo volgende:

* Gebruik Hallo [app-ID](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) van Hallo dashboard toosend crashgegevens en feedback van uw app. Werk in MyDriving, Hallo-id's in src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Testgebruikers uitnodigen](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Krijgt u een URL-toorecruit testers gebruikers. Ze je kunnen toosign voor uw team worden, Hallo-app downloaden en u feedback sturen.
* Als u liever een meer geopende bètaversie, stelt u Hallo distributie toopublic. Klik op **App beheren** > **distributie** > **downloaden = openbare**. Iedereen kan nu uw app downloaden en u feedback verzenden en ze ziet een melding wanneer u een nieuwe versie plaatsen. U kunt sommige foutenrapporten van deze te ophalen.
  
   ![Teams op Hallo-dashboard](./media/iot-solution-build-system/image3.png)
* [Koppeling crash rapporten tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Klik op **App beheren** > **Visual Studio teamservices**. HockeyApp kunt automatisch werkitems in Team Services maken wanneer er foutenrapporten of wanneer feedback wordt ontvangen.

Lees meer op Hallo [HockeyApp site](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Test Hallo mobiele app op Xamarin-Testcloud
[Xamarin-Testcloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) UI testen op echte apparaten in de cloud Hallo automatiseert. Met behulp van Hallo NUnit framework, kunt u tests die uw app via de gebruikersinterface Hallo uitvoeren schrijven.

toouse Xamarin, als u Hallo opnemen [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK in uw app wordt geleverd als een NuGet-pakket. U vindt deze in Hallo demo-app en is opgenomen bij het maken van nieuwe Testprojecten Hello Xamarin-sjablonen.

![Waar toofind Hallo platformoverschrijdende SDK op Hallo-interface](./media/iot-solution-build-system/image4.png)

Een voorbeeldproject van de test is opgenomen in de app in de opslagplaats Hallo Hallo. In [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), zoek onder [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Als u een build voor Visual Studio Team Services gebruikt, is het eenvoudig toowrite Xamarin UI eenheid test en ze worden uitgevoerd als onderdeel van uw build.

## <a name="deploy-azure-services"></a>Azure-services implementeren
een automatische implementatie van Azure-services en services van de build Team Services, tooperform verwijzen toohello gedetailleerde instructies in **scripts/README.md**.

Microsoft Azure biedt een schat aan verschillende services waarmee u toobuild cloud-toepassingen kunt. Hoewel veel kunnen worden gebruikt (zoals App Service of Web-Apps) afzonderlijk, ze zijn op hun best wanneer ze met elkaar bent verbonden tooform een geïntegreerd systeem die we gebruiken in MyDriving.

Het is mogelijk toocreate en Azure-services handmatig verbinding, maar het is veel sneller en betrouwbaarder toouse Azure Resource Manager-sjablonen. [Resource Manager](../azure-resource-manager/resource-group-overview.md) automatiseert het Hallo-implementatie van een oplossing bronnen en Hallo onderlinge verbindingen tussen hen maken.

U vindt Hallo-sjabloon voor Hallo MyDriving systeem in Hallo GitHub-opslagplaats onder [scripts/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Het biedt een uitgebreide en beknopt overzicht van hoe verschillende services in onze architectuur Hallo onderling verbonden. Kunnen al deze in Hallo in detail uitgelegd [MyDriving handleiding](http://aka.ms/mydrivingdocs), maar u veel meer door te lezen via Hallo sjabloon zelf.

> [!NOTE]
> De meeste Azure-services hebben een bijbehorende kosten, afhankelijk van Hallo prijscategorie. Als u nieuwe tooAzure bent, kunt u [gratis uitproberen](https://azure.microsoft.com/free/). Als u niet van plan toouse bepaalde onderdelen in Hallo MyDriving systeem bent, worden echter zeker tooremove ze tooavoid steeds kosten. Hallo bevat 'Schatting operationele kosten' later in dit artikel een overzicht van de typische service onkosten.
> 
> 

### <a name="edit-hello-template"></a>Hallo-sjabloon bewerken
toocustomize uw implementatie mogelijk tooremove onnodige onderdelen of tooadd anderen, moet u eerst een kopieën maken van het scenario voor\_complete.params.json en scenario\_complete.json in welke wijzigingen toomake.

U kunt Hallo scenario\_complete.params.json bestand toooverride verschillende, zoals Hallo service SKU of Hallo opslagreplicatietype, standaardwaarden zoals beschreven in de volgende tabel Hallo. standaardwaarden Hallo selecteren Hallo laagste kosten opties.

| **Parameter** | **Beschrijving** | **Standaardwaarde** |
| --- | --- | --- |
| IoT-Hub SKU |Laag voor de service Azure IoT Hub |F1 |
| Opslagaccounttype |Opslagreplicatietype |Standaard-LRS |
| SQL-Servicedoelstelling |Gelijktijdigheid sleuf verbruik |DW100 |
| Hosting Plan SKU |Service-plan voor App Service |F1 |

In scenario\_complete.json:

* Zoek naar 'baseName' en tooa-naam die u wilt wijzigen.
* Zoek naar 'Maken'. Elk van deze secties maakt een resource.
* SqlServerAdminLogin en sqlServerAdminPassword toosuitable waarden instellen.
* Voordat u een sectie die u een resource maakt verwijdert, moet u controleren of er afhankelijke services door te zoeken naar de naam elders in Hallo-bestand. Denk eraan dat elke sectie maakt u een service bevat een *dependsOn* sectie waarin de afhankelijkheden ervan.

Hier volgt welke Hallo-sjabloon configureert. Informatie vindt u in Hallo [handleiding](http://aka.ms/mydrivingdocs).

| **Service** | **Beschrijving en details** |
| --- | --- |
| Opslagaccounts |Hallo-sjabloon maakt drie accounts: |
| -Een SQL-database die ontvangt geaggregeerde telemetrie van Stream Analytics en fungeert als Hallo back-uparchief voor Azure App Service-tabellen die deze gegevens via de API-eindpunten beschikbaar. | |
| -Blob opslag, stelt u historische gegevens uit een andere Stream Analytics-taak toobe verwerkt door HDInsight samen. | |
| -Een SQL-database die door HDInsight worden verwerkt voor gebruik met Power BI resultaten ontvangt. | |
| Azure IoT Hub |Hiermee stelt u een wederzijdse verbinding tooeach aangesloten apparaat. In Hallo MyDriving oplossing fungeert mobiele app Hallo als een veld gateway toosend gegevens tooAzure IoT Hub. Azure IoT Hub en fungeert als een invoer tooStream Analytics. |
| Azure Event Hubs |Uitvoer voor een Stream Analytics-taak die in de wachtrij Hallo geplaatst uitvoer tooextensions die zijn gemaakt met Azure Service Fabric. |
| Azure SQL Data Warehouse | |
| Stream Analytics-taken |In- en uitgangen verbinden met een query, namelijk gebruikte tooaggregate real-time en historische gegevens voor het Hallo-App Service-API's, Azure Machine Learning, uitbreidingen en Power BI. |
| Machine Learning-werkruimte |Omvat experimenten, R-code en API-service. |
| Azure Data Factory |Geplande Machine Learning retraining. |
| Hosting service Fabric-plan |Voor uitbreidingen. |
| App Service ("mam") |Hosts Hallo Mobile Apps-API-project met eindpunten voor de mobiele app Hallo. Hallo API-code moet geïmplementeerde tooApp Service vanuit Visual Studio. |
| Regels voor waarschuwingen |Verzendt dat u e-als Hallo app antwoorden duiden op fouten. |
| Application Insights |Voor het bewaken van de prestaties van Hallo-API's in App Service. U hebt tooconfigure Hallo verbinding in Visual Studio. |
| Azure Key Vault |Voor het opslaan van certificaat Hallo web service-cluster. |

### <a name="run-hello-template"></a>Hallo sjabloon uitvoeren
In **scripts/README.md**, er zijn gedetailleerde instructies voor het actieve Hallo-sjabloon.

tooprovision deze services in uw eigen Azure-account met behulp van script hello, doe hello te volgen:

* PowerShell gebruiken:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *locatie* Hallo is [Azure-locatie](https://azure.microsoft.com/regions/), zoals `North Europe` of `West US`. Gebruik `Get-AzureLocation` toofind een lijst met beschikbare locaties.
  * *resourceGroupName* is Hallo-naam die u wilt dat toogive toohello groep die alle Hallo resources deel van uitmaakt. Wanneer u klaar bent met de Hallo resources, kunt u ze allemaal tegelijk verwijderen door deze groep te verwijderen.
* Voer DeploymentScripts/Bash/deploy.sh met Bash.
* Open en Hallo Visual Studio-oplossing DeploymentScripts/VS/DeployARM.sln bouwen.

Houd er rekening mee dat elke keer Hallo-sjabloon wordt uitgevoerd, wordt een nieuwe set resources gemaakt onder een andere naam. toodelete hello resources, Ga toohello portal en Hallo resourcegroep verwijderen.

Als het Hallo-script voor een of andere reden mislukt, kunt u het opnieuw uitvoeren.

Hallo script kunt u de optie van de configuratie van doorlopende integratie in Visual Studio Team Services Hallo. Als u een Team Services-project hebt ingesteld, hebt u een URL: https://yourAccountName.visualstudio.com. Voer de volledige URL Hallo wanneer u wordt gevraagd. U kunt daarvoor een nieuwe of bestaande naam voor een Team Services-project.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Instellen van de build en definities in Visual Studio Team Services testen
We gebruiken Team Services op dit project voornamelijk voor de build en functies testen. Maar, biedt ook ondersteuning voor uitstekende samenwerking, zoals Taakbeheer met kanbanborden, code-revisie geïntegreerd met taken en bronbeheer en geregeld bouwt. Het is geïntegreerd met andere hulpprogramma's zoals GitHub, Xamarin HockeyApp en natuurlijk Visual Studio. U kunt toegang tot dit via Hallo webinterface of Visual Studio, indien dit handiger op elk moment.

Hallo stappen voor het Hallo-build en release definities gebruiken diverse invoegtoepassing services die beschikbaar in Hallo Team Services zijn [Marketplace](https://marketplace.visualstudio.com/VSTS). Er zijn services die wordt aangeroepen builds door Xamarin-, Android- en andere leveranciers en die verbinding maken met tooHockeyApp in toorun opdrachtregels voor toevoeging toobasic hulpprogramma's of bestanden kopiëren.

![Opties in het Team Services bouwen](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definities bouwen
We hebben build definities voor elk van de belangrijkste doelen Hallo. We hebben ook variaties voor functie- en regressie testen. Dat geeft ons:

* MyDriving.Services (back-end-web-app voor de mobiele app Hallo Hallo)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-functie
  * MyDriving.Xamarin.Android regressie
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-functie
  * MyDriving.Xamarin.iOS regressie
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-functie
  * MyDriving.Xamarin.UWP regressie

Als u wilt dat toosee Hallo volledige details van de configuratie, raadpleegt u de sectie 4.7 Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs), 'Build en Release-configuratie.' Deze Hallo volgen algemene patroon. Hallo-script:

1. Hiermee herstelt u Hallo NuGet-pakket. We bewaren niet gecompileerde code in Hallo-opslagplaats, zodat de eerste stappen Hallo van elke build toorestore Hallo vereist NuGet-pakketten.
2. Hallo licentie activeert. Hallo build wordt uitgevoerd in de cloud Hallo, dus indien een licentie--moet in het bijzonder voor Hallo Xamarin bouwen service--we hebben tooactivate onze licentie op het huidige build machine Hallo. Vervolgens wordt deze onmiddellijk daarna tooallow deactiveren deze toobe gebruikt op een andere computer.
3. Met behulp van de relevante service Hallo is gebaseerd. We Xamarin builds voor mobiele apps hello gebruiken en Visual Studio builds voor Hallo back-end-webservice.
4. Tests is gebaseerd.
5. Voert testen uit. We Hallo mobiele app tests worden uitgevoerd in Xamarin-Testcloud.
6. Hallo build resultaat toohello-doellocatie publiceert.

Hallo-trigger voor de belangrijkste builds Hallo ingesteld toocontinuous integratie. Dat wil zeggen, Hallo build uitgevoerd telkens wanneer de code is ingeschakeld in de hoofdvertakking toohello.

![Interface waar Hallo trigger is de set toocontinuous integratie](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definities van release
Release-definities worden ingesteld in veel Hallo dezelfde manier.

Voor de webservice hello instellen we implementatie als een Azure-web-app:

![Interface voor het instellen van de implementatie als een Azure-web-app](./media/iot-solution-build-system/image7.png)

En we Hallo release trigger toocontinuous implementatie instellen. Dat wil zeggen, elke inchecken gevolgd door een geslaagde build resulteert in een update toohello web-app.

![Interface voor het instellen van Hallo release trigger toocontinuous implementatie](./media/iot-solution-build-system/image8.png)

We implementeren tooHockeyApp voor mobiele apps:

![Interface voor het implementeren van een mobiele app tooHockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Telemetrie verkennen met behulp van Application Insights
[Application Insights](../application-insights/app-insights-overview.md) telemetrie over Hallo prestaties en het gebruik van uw webservices worden verzameld. Hallo Application Insights-SDK verzendt telemetrie van Hallo service toohello Application Insights-resource in Azure.

Blader toohello Application Insights-resource die Hallo-sjabloon instellen. Daar vindt u diagrammen van Hallo prestaties van uw [mobiele App Service-project](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Deze serveraanvragen en reactietijden, fouten, weergeven en uitzondering telt. Er zijn ook grafieken van afhankelijkheid responstijden--dat wil zeggen aanroepen toohello database en tooREST API's zoals Machine Learning. Als er problemen met de prestaties, zult u kunnen toosee welk onderdeel van uw systeem veroorzaken.

![Voorbeeld van grafiek](./media/iot-solution-build-system/image11.png)

Als u hebt een webservice die u handmatig hebt ingesteld, van eenvoudige tooget Hallo dezelfde grafieken. Klik op Hallo blade web-service op **extra** > **extensies** > **toevoegen**. Selecteer **Application Insights**.

![Interface voor het selecteren van Application Insights tooget Hallo grafieken](./media/iot-solution-build-system/image12.png)

Hallo-functie werkt door het instrumenteren van uw toepassing Hello Application Insights-SDK.

U kunt aangepaste telemetrie (of dat een toepassing die ergens buiten Azure wordt uitgevoerd) toevoegen door [Application Insights-SDK toe te voegen Hallo](../application-insights/app-insights-asp-net.md) tijdens ontwikkeling. Dit is nuttig toolog metrische gegevens die afhankelijk van toepassing op Hallo, zoals gebruikers gemiddelde reis lengte of Totaalaantal kilometers zijn. In Visual Studio met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Application Insights toevoegen**.

![Interface voor aangepaste telemetrie voor Application Insights toevoegen tooadd selecteren](./media/iot-solution-build-system/image10.png)

Application Insights wordt waarschuwingsmails sturen als er vreemde aantal mislukte reacties. U kunt ook uw eigen waarschuwingen op verschillende metrische gegevens, zoals responstijden instellen.

Alleen toobe ervoor dat uw web-service altijd up-to-date is en wordt uitgevoerd, kunt u instellen [beschikbaarheidstests](../application-insights/app-insights-monitor-web-app-availability.md). Deze tests ping uw site vanuit verschillende locaties Hallo wereld om de 15 minuten. U ontvangt een e-mailbericht opnieuw, als er een probleem toobe lijkt.

## <a name="estimate-operational-costs"></a>Schatting maken van de operationele kosten
Het is opmerkelijk goedkope toorun een app in zoals deze op kleine schaal. Veel van Hallo services hebben gratis instapmodellen lagen, zodat ontwikkeling en kleinschalige bewerking weinig kosten. En uw eigen apps niet beschikken over alle functies van de Hallo gedemonstreerd in MyDriving toouse.

Hier volgt een ruwe schatting van onze kosten bij het instellen van de configuratie van Hallo-ontwikkeling voor MyDriving. We enkele alternatieven die we hebben ook Opmerking *niet* gebruiken. Deze informatie kan nuttig zijn als u een schatting maken van uw eigen kosten.

We gaan ervan uit:

* Een team van niet meer dan vijf (plus observeren belanghebbenden).
* Uitgevoerd over een maand.
* 100 gebruikers met vier reizen per dag.

> [!NOTE]
> Als u nieuwe tooAzure er is een [gratis account](https://azure.microsoft.com/free/).
> 
> 

| **Onderdeel-service** | **Opmerkingen bij de** | **Kosten per maand** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) met [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Cross-platform dev-omgeving |Visual Studio Community. (Moet [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) voor [Xamarin.Forms](https://xamarin.com/forms), toodesign platformoverschrijdende uit één codebasis.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Wederzijdse gegevens verbinding toodevices |8000 berichten + 0,5 KB/bericht vrij te geven. |$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Stroom van grote hoeveelheden gegevens verwerken |De kosten van $0,031 per eenheid per uur, streaming terwijl ingeschakeld. U kiest Hallo aantal streaming-eenheden die u wilt. meer tooscale up. |$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Adaptieve reacties |seat-$10/maand. <br/>                                                                                                                                                                                 + 3 uur experiment \* $1 / experimenteren uur. <br/>                                                                                                                                                           + 3.5 uur API CPU \* $2 / productie CPU uur. <br/>                                                                                                                                                          API-CPU-tijd wordt ervan uitgegaan 5 min. per dag retraining, hoewel dit zou toename met meer invoergegevens.                   <br/>                                                                                                                                                                     + 2 min. per dag score berekenen tooprocess 400 reizen per dag. |$20 |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Host voor mobiele back-end |Laag B1--productie web-apps. |$56 |
| [Visual Studio teamservices](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Bouwen, testen van eenheden en releasebeheer; Taakbeheer |Persoonlijke agents vijf gebruikers. |$0 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Bewaking van prestaties en het gebruik van web-services en sites |Gratis laag. |$0 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Distributie van de verzameling van feedback, gebruik en crashgegevens plus beta-apps |Twee gratis apps voor nieuwe gebruikers.<br/> $30/ daaropvolgende maand. |$0 |
| [Xamarin](https://store.xamarin.com/)<br/> Code op een uniform platform voor meerdere apparaten |Gratis proefversie. <br/>$25 per maand daarna. |$0 |
| [SQL-Database](https://azure.microsoft.com/pricing/details/sql-database/) voor Azure App Service |Basisstaffel; model van één database. |$5 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (optioneel) |Een lokaal cluster worden uitgevoerd. |$0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Veelzijdige geeft en het onderzoek van gestroomd en statische gegevens |Gratis laag: 1 GB, 10.000 rijen per uur, dagelijks vernieuwd. <br/> $10/gebruiker/maand voor [hogere limieten](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), meer verbindingsopties, samenwerking. |$0 |
| [Storage](https://azure.microsoft.com/pricing/details/storage/) |L (lokaal redundant) &lt; 100 G $0.024/GB. |$3 |
| [Data Factory](https://azure.microsoft.com/pricing/details/data-factory/) |$0,60 per activiteit \* (FOC 8 tot en met 5). |$2 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  De cluster op aanvraag voor het dagelijkse retraining |Drie A3 knooppunten op $0,32 per uur 1 uur per dag * 31 dagen. |$30 |
| [Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) |Basic met doorvoereenheid $11/ maand + $0,028 inkomend. |$11 |
| OBD-dongle | |$12 |
| **Totaal** | |**$157** |

Zie voor meer informatie:

* Samenvatting van [Azure servicequota en limieten](../azure-subscription-service-limits.md#iot-hub-limits)
* Azure [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Stuur ons uw feedback
Omdat we MyDriving toohelp aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker toohear van u over hoe goed werkt. Laat ons weten als:

* U ondervindt problemen of uitdagingen.
* Er is een extensiepunt waaruit zou geschikte tooyour scenario.
* U vindt een efficiëntere manier tooaccomplish bepaalde behoeften.
* U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.

feedback over toogive bestand een probleem op GitHub of een opmerking hieronder laat (en-us edition).

We hopen toohearing van u!

## <a name="next-steps"></a>Volgende stappen
Hallo wordt aangeraden [MyDriving handleiding](http://aka.ms/mydrivingdocs), dit is een uitgebreide beschrijving van Hallo ontwerp van Hallo systeem en de bijbehorende onderdelen.

