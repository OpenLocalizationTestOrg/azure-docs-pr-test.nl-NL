---
title: 'MyDriving Azure IoT-voorbeeld: samenstellen | Microsoft Docs'
description: Maken van een app die is een uitgebreide demonstratie van het bouwen van een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
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
ms.openlocfilehash: c4b19cc76ca11f606ca8af6b0f3277b5aa46ac5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="build-and-deploy-the-mydriving-solution-to-your-environment"></a>Bouwen en implementeren van de oplossing MyDriving aan uw omgeving
MyDriving is een Internet der dingen (IoT)-oplossing die u verzamelt gegevens uit uw auto, verwerkt met behulp van machine learning en geeft deze op uw mobiele telefoon. De back-end bestaat uit diverse services geleverd door Microsoft Azure. De clients kunnen worden Android, iOS of Windows 10-telefoons.

De oplossing MyDriving zodat u snel aan de slag bij het maken van uw eigen IoT-systeem is gemaakt. Van de [MyDriving opslagplaats op GitHub](https://github.com/Azure-Samples/MyDriving), kunt u Azure Resource Manager-scripts voor het implementeren van de back-end-architectuur in uw eigen Azure-account krijgen. U kunt vanaf dat moment opnieuw configureren van de andere services, wijzig de query's om aan de behoeften van uw eigen gegevens, enzovoort. U vindt deze scripts--samen met de code voor de mobiele app, het Azure App Service API-project en meer--in de opslagplaats MyDriving.

Als u de app nog niet hebt geprobeerd, bekijkt u de [Get-handleiding](iot-solution-get-started.md).

Er is een gedetailleerd overzicht van de architectuur in de [MyDriving handleiding](http://aka.ms/mydrivingdocs). Kortom zijn er enkele softwareonderdelen die wij instellen om een soortgelijke project te maken:

* Een **clientapp** wordt uitgevoerd op Android, iOS en Windows 10 Phone-telefoons. We gebruiken de Xamarin-platform voor het delen van veel van de code die is opgeslagen op GitHub onder `src/MobileApp`. De app daadwerkelijk voert twee afzonderlijke functies uit:
  * Deze organisatiebeveiligingstokens telemetrie van het apparaat ingebouwde diagnostische gegevens (OBD) en van de eigen Locatieservice naar back-end van het systeem.
  * Het is een gebruikersinterface waarin gebruikers kunnen zoeken over hun reizen opgenomen weg.
* Een **cloudservice** opgenomen van de gegevens onderweg reis in realtime en verwerkt deze. Het belangrijkste werk voor het maken van deze service is, kiest voorzien en bekabelen van tal van Azure-services. Sommige van de onderdelen vereist scripts te filteren en proces de inkomende gegevens. We gebruiken een Azure Resource Manager-sjabloon voor het configureren van alle onderdelen.
* Een **mobiele service app** is de webservice achter het deel van de gebruikersinterface van de app voor het apparaat. De belangrijkste taak is om te zoeken in de database opgeslagen, verwerkt gegevens. De code op GitHub onder is `src/MobileAppService`.
* **Visual Studio met Xamarin** is onze ontwikkelomgeving. Xamarin dat bestaat als een onderdeel van de Visual Studio en als een zelfstandige integrated development environment (IDE), wordt gebruikt voor het bouwen van de apparaatcode voor meerdere platforms. Als de iOS-code, is het nodig zijn voor een exemplaar van het Xamarin uitgevoerd op een OS X-machine. Indien nodig, kan deze worden uitgevoerd als een agent, beheerd vanuit Visual Studio.
* **Testen van de eenheden** van het apparaat-apps in Xamarin-Testcloud wordt uitgevoerd.
* **GitHub** is de opslagplaats waar we de code, scripts en sjablonen opslaat.
* **Visual Studio Team Services** is een cloudservice die wordt gebruikt voor het beheren van de continue bouwen en testen van de web-service en apparaat-apps.
* **HockeyApp** wordt gebruikt voor het distribueren van de versies van de apparaatcode. Verzamelt ook crashes en gebruik rapporten en feedback van gebruikers.
* **Visual Studio Application Insights** bewaakt de mobiele web-service.

Dus gaan we kijken hoe we ingesteld dat alle. 

> [!NOTE] 
> Veel van de volgende stappen zijn optioneel.
>
>

## <a name="sign-up-for-accounts"></a>Aanmelden voor accounts
* [Visual Studio Developer Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Dit gratis programma biedt eenvoudige toegang tot veel hulpprogramma's voor ontwikkelaars en -services, waaronder Visual Studio, Visual Studio Team Services en Azure. Dit biedt u een creditcard $25 per maand op Azure voor twaalf maanden. Dit omvat ook abonnementen op Pluralsight trainings- en Xamarin universiteit. U kunt ook aanmelden afzonderlijk voor gratis lagen van [Azure](https://azure.com) en [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), maar deze geen Azure-tegoed.
* [HockeyApp](https://rink.hockeyapp.net/) (optioneel), voor het beheren van de test-distributie van mobiele apps en het verzamelen van telemetrie.
* [Xamarin](https://xamarin.com/) (vereist), voor het bouwen van de mobiele app en foutopsporing wordt uitgevoerd en tests uitgevoerd op [Xamarin-Testcloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (optioneel), vrije openbare opslagplaatsen voor uw eigen code (persoonlijke opslagplaatsen betaald) maken. U kunt ook het basisniveau gebruiken in Visual Studio Team Services voor privé-opslagplaatsen.
* [Power BI](https://powerbi.microsoft.com/) (optioneel), uitgebreide visualisaties van gegevens maken in het hele systeem.

> [!NOTE]
> U hoeft niet een GitHub-account voor toegang tot de code MyDriving in [de GitHub MyDriving-opslagplaats](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Ontwikkelingsprogramma's installeren
De volgende instellingen zijn voor het ontwikkelen van de volledige oplossing: een iOS-, Android- en Windows 10 Mobile platformoverschrijdende-app met een Azure back-end.

Als alternatief kunt u Xamarin Studio in Mac of Windows voor het ontwikkelen van de mobiele apps als u niet werken op de Azure back-end.

Er is een [langere beschrijving van deze installatie](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Windows-ontwikkelcomputer
Het centrale hulpprogramma in Windows is Visual Studio voor het werken met de MyDriving-app voor Android en Windows, de App Service API-project en microservice-extensies.

Xamarin, Git emulators en andere onderdelen nuttig zijn alle geïntegreerd met Visual Studio.

Installeren:

* [Visual Studio met Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (elke editie--Community is gratis).
* [SQLite voor Universal Windows Platform](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Vereist voor het bouwen van de Windows 10 Mobile-code.
* [Azure SDK voor Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Biedt u de SDK voor apps in Azure, samen met de opdrachtregelprogramma's voor het beheren van Azure wordt uitgevoerd.
* [Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Vereist voor het bouwen de [microservice](../service-fabric/service-fabric-get-started.md) extensie.

Zorg ervoor dat u de juiste Visual Studio-extensies hebben. Controleer of onder **extra**, ziet u **Android, iOS, Xamarin...** . Als dat niet het geval is, Visual Studio niet openen, doorzoeken voor Xamarin en volg de aanwijzingen om deze te installeren. Controleer ook of **Git voor Windows** is geïnstalleerd. Als dat niet het geval is, wordt in Visual Studio, zoekt u het en volg de aanwijzingen om deze te installeren. 

### <a name="mac-development-machine"></a>Mac-ontwikkelcomputer
De Mac (Yosemite of hoger) is vereist als u wilt ontwikkelen voor iOS. Hoewel we Visual Studio met Xamarin in Windows te ontwikkelen en beheren van alle code gebruiken, gebruikt Xamarin een agent is geïnstalleerd op een Mac wilt bouwen en meld u aan de iOS-code.

![Voor Windows ontwikkelen en bouwen op Mac](./media/iot-solution-build-system/image1.png)

(Als alternatief kunt u Xamarin Studio rechtstreeks op de Mac om platformoverschrijdende apps te ontwikkelen.)

U hoeft niet op de Mac als u niet wilt laten iOS als doelplatform.

Installeren:

* [Xamarin Studio voor iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). U kunt ook Visual Studio en Xamarin op een Mac met een virtuele Windows-computer instellen. Zie [-installatie, installatie en verificaties voor Mac-gebruikers](https://msdn.microsoft.com/library/mt488770.aspx) op MSDN.
* [Azure ontwikkelingsprogramma's](https://azure.microsoft.com/downloads/) (optioneel).

Inschakelen van externe aanmelding op de Mac. Open **Systeemvoorkeuren** > **delen**, en selecteer vervolgens **externe aanmelding**.

Wanneer u een iOS-project in Visual Studio in Windows opent, wordt de invoegtoepassing Xamarin u gevraagd voor de ID van de Mac.

## <a name="fetch-the-github-repository"></a>Ophalen van de GitHub-opslagplaats
Ophalen van een lokale kopie van [de GitHub MyDriving-opslagplaats](https://github.com/Azure-Samples/MyDriving) met behulp van de **ZIP downloaden** knop in GitHub, Visual Studio of een andere Git-client.

Pak het bestand naar een map met een korte padnaam, zoals C:\\code.

U kunt ook als u wilt up-to-date te houden met of bijdragen aan onze code, de opslagplaats klonen als volgt:

**GIT kloon https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Een Bing maps API-sleutel ophalen
[Registreren voor een Bing kaarten-API-sleutel](https://msdn.microsoft.com/library/ff428642.aspx).

U moet dit vervangen in regel 22 in `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-the-demo-app"></a>De demo-app bouwen
Deze oplossingen openen in Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Krijgt u de aanwijzingen voor het:

* Vertrouwen van sommige mogelijk onbetrouwbare projecten. Kies om deze te openen als u wilt doorgaan.
* Modus voor ontwikkelaars instellen als u op een nieuwe Windows 10-computer werkt.
* Geef uw Xamarin-referenties.
* Verbinding maken met de Xamarin-Mac. Als u een Mac hebt, met de rechtermuisknop op het iOS-project in Visual Studio en selecteer vervolgens **Unload project**.

De oplossing opnieuw worden opgebouwd.

Als u problemen ondervindt bij het bouwen, probeert u de oplossingen quirks die we hebben gevonden:

* *VINLookupApplication project niet laden*: Controleer of u geïnstalleerd de [Azure SDK voor Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Service Fabric-project niet onderhouden*: eerst de interface-projecten bouwen en controleer of u de Service Fabric SDK geïnstalleerd.
* *Android-app niet onderhouden*:
  
  * Open **extra** > **Android** > **Android SDK Manager**, en zorg ervoor dat Android 6 (API 23) / Platform SDK is geïnstalleerd.
  * Deze map te verwijderen en vervolgens opnieuw maken:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-to-know-the-code"></a>Kennismaking met de code
In de oplossing vindt u het:

* Azure-extensies: Service Fabric.
* Azure HDInsight: Scripts voor het verwerken van reis gegevens in Azure.
* Mobiele Apps: De apparaat-apps.
* MobileAppsService/MyDrivingService: Het web terug eindigen.
* Power BI: Definitie van het rapport.
* Scripts:
  
  * Resource Manager: sjablonen voor het bouwen van de Azure-resources.
  * PowerShell: Scripts worden uitgevoerd van de Resource Manager-sjablonen.
  * Azure SQL Database: Foutopsporing databases.
* SQL Database: CreateTables: schemadefinities.
* Azure Stream Analytics: Query's die de gegevensstroom inkomende te transformeren.

## <a name="run-the-apps-in-development-mode"></a>De apps worden uitgevoerd in de Ontwikkelingsmodus
Onderneem actie om uit te voeren van de apps, op basis van het apparaat dat u gebruikt:

* Back-end: MyDrivingService instellen als opstartproject en druk op F5 om uit te voeren van de back-end-webservice. Een browserweergave van de API-vermelding wordt geopend.
* Mobiele clients: de [mobiele apps zijn ontwikkeld in Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: Zie voor meer informatie [Android foutopsporing in Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: Zie voor meer informatie [foutopsporing in iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: Zie voor meer informatie [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-the-mobile-app-to-hockeyapp"></a>De mobiele app uploaden naar HockeyApp
HockeyApp beheert de distributie van uw Android, iOS of Windows-app voor het testen van gebruikers, het verwittigen van gebruikers met nieuwe releases. Verzamelt ook nuttig foutenrapporten, feedback van gebruikers met schermafbeeldingen en meetgegevens voor softwaregebruik.

[Start met uploaden van](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) uw build-app. Meld u vervolgens, bij [HockeyApp](https://rink.hockeyapp.net) van uw ontwikkelcomputer. Klik op het dashboard voor ontwikkelaars **nieuwe App**, en sleep de gemaakte bestanden naar het venster. (Later kunt u automatiseren uw buildservice om dit te doen.)

U kunt nu in uw app-dashboard.

![Overzichtstabblad op het app-dashboard](./media/iot-solution-build-system/image2.png)

Het proces herhalen voor elk platform dat uw app wordt uitgevoerd op. Vervolgens kunt u het volgende doen:

* Gebruik de [app-ID](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) vanuit het dashboard crashgegevens en feedback verzenden vanuit uw app. Werk in MyDriving, de id's in src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Testgebruikers uitnodigen](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). U ophalen een URL naar het werven testers gebruikers. Deze persoon zich aanmelden voor uw team, de app downloaden en u feedback sturen.
* Als u liever een meer geopende bètaversie, stelt u de distributie naar openbaar. Klik op **App beheren** > **distributie** > **downloaden = openbare**. Iedereen kan nu uw app downloaden en u feedback verzenden en ze ziet een melding wanneer u een nieuwe versie plaatsen. U kunt sommige foutenrapporten van deze te ophalen.
  
   ![Teams op het dashboard](./media/iot-solution-build-system/image3.png)
* [Foutenrapporten koppelen aan Visual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Klik op **App beheren** > **Visual Studio teamservices**. HockeyApp kunt automatisch werkitems in Team Services maken wanneer er foutenrapporten of wanneer feedback wordt ontvangen.

Meer informatie op de [HockeyApp site](https://hockeyapp.net).

## <a name="test-the-mobile-app-on-xamarin-test-cloud"></a>Testen van de mobiele app op Xamarin-Testcloud
[Xamarin-Testcloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatiseert UI testen op echte apparaten in de cloud. Met behulp van het framework NUnit schrijven u tests die uw app via de gebruikersinterface uitvoeren.

Voor het gebruik van Xamarin, die u neemt de [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK in uw app wordt geleverd als een NuGet-pakket. U vindt deze in de demo-app en is opgenomen wanneer u nieuwe Testprojecten met de Xamarin-sjablonen maakt.

![Waar vind ik de platformoverschrijdende SDK op de interface](./media/iot-solution-build-system/image4.png)

Een voorbeeldproject van de test is opgenomen in de app in de opslagplaats. In [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), zoek onder [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Als u een build voor Visual Studio Team Services gebruikt, is het gemakkelijk te schrijven Xamarin UI eenheidstests en ze worden uitgevoerd als onderdeel van uw build.

## <a name="deploy-azure-services"></a>Azure-services implementeren
Raadpleeg de gedetailleerde instructies in om uit te voeren een automatische implementatie van Azure-services en build-services Team Services, **scripts/README.md**.

Microsoft Azure biedt een schat aan andere services die u gebruiken kunt om cloudtoepassingen te bouwen. Hoewel veel kunnen afzonderlijk (zoals App Service of Web-Apps) worden gebruikt, zijn ze op hun best wanneer ze zijn verbonden met een geïntegreerde systeem, zoals dat we gebruiken in MyDriving formulier.

Het is mogelijk te maken en Azure-services handmatig verbinding, maar het is veel sneller en betrouwbaarder gebruik van Azure Resource Manager-sjablonen. [Resource Manager](../azure-resource-manager/resource-group-overview.md) automatiseert de implementatie van een oplossing resources en de onderlinge verbindingen tussen hen maken.

U vindt de sjabloon voor het systeem MyDriving in de GitHub-opslagplaats onder [scripts/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Het biedt een uitgebreide en beknopt overzicht van hoe de andere services in onze architectuur onderling verbonden. We uitleggen al deze beschreven in de [MyDriving handleiding](http://aka.ms/mydrivingdocs), maar veel meer door te lezen via de sjabloon zelf.

> [!NOTE]
> De meeste Azure-services hebben een bijbehorende kosten, afhankelijk van de prijscategorie. Als u geen ervaring met Azure, kunt u [gratis uitproberen](https://azure.microsoft.com/free/). Echter, als u niet dat bepaalde onderdelen in het systeem MyDriving gebruiken wilt, moet verwijderen, om de kosten vermijden. De sectie 'Schatting maken van de operationele kosten' verderop in dit artikel biedt een overzicht van de typische service onkosten.
> 
> 

### <a name="edit-the-template"></a>De sjabloon bewerken
Voor het aanpassen van uw implementatie mogelijk overbodige om onderdelen te verwijderen of toevoegen van anderen, moet u eerst een kopieën van scenario\_complete.params.json en scenario\_complete.json waarin wijzigingen aanbrengen.

U kunt het scenario\_complete.params.json-bestand voor het onderdrukken van verschillende standaardwaarden, zoals de SKU-service of het replicatietype, zoals beschreven in de volgende tabel. De standaardwaarden selecteren de laagste kosten-opties.

| **Parameter** | **Beschrijving** | **Standaardwaarde** |
| --- | --- | --- |
| IoT-Hub SKU |Laag voor de service Azure IoT Hub |F1 |
| Opslagaccounttype |Opslagreplicatietype |Standaard-LRS |
| SQL-Servicedoelstelling |Gelijktijdigheid sleuf verbruik |DW100 |
| Hosting Plan SKU |Service-plan voor App Service |F1 |

In scenario\_complete.json:

* Zoek naar 'baseName' en wijzig dit in een naam die u liever.
* Zoek naar 'Maken'. Elk van deze secties maakt een resource.
* SqlServerAdminLogin en sqlServerAdminPassword geschikte waarden instellen.
* Voordat u een sectie die u een resource maakt verwijdert, moet u controleren of er afhankelijke services door te zoeken naar de naam ervan ergens anders in het bestand. Denk eraan dat elke sectie maakt u een service bevat een *dependsOn* sectie waarin de afhankelijkheden ervan.

Dit is wat de sjabloon configureert. Informatie vindt u in de [handleiding](http://aka.ms/mydrivingdocs).

| **Service** | **Beschrijving en details** |
| --- | --- |
| Opslagaccounts |De sjabloon maakt drie accounts: |
| -Een SQL-database die ontvangt geaggregeerde telemetrie van Stream Analytics en fungeert als de back-uparchief voor Azure App Service-tabellen die deze gegevens via de API-eindpunten beschikbaar. | |
| -Blob opslag, stelt u historische gegevens uit een andere Stream Analytics-taak kan worden verwerkt door HDInsight samen. | |
| -Een SQL-database die door HDInsight worden verwerkt voor gebruik met Power BI resultaten ontvangt. | |
| Azure IoT Hub |Een verbinding tot stand wederzijdse op elk aangesloten apparaat. In de oplossing MyDriving fungeert de mobiele app als een veldgateway gegevens verzenden naar Azure IoT Hub. Azure IoT Hub en fungeert als invoer voor Stream Analytics. |
| Azure Event Hubs |Uitvoer voor een Stream Analytics-taak die de uitvoer naar uitbreidingen die zijn gemaakt met Azure Service Fabric in de wachtrij geplaatst. |
| Azure SQL Data Warehouse | |
| Stream Analytics-taken |In- en uitgangen verbinden met een query die wordt gebruikt voor het cumuleren van zowel real-time en historische gegevens voor de App Service-API's, Azure Machine Learning, uitbreidingen en Power BI. |
| Machine Learning-werkruimte |Omvat experimenten, R-code en API-service. |
| Azure Data Factory |Geplande Machine Learning retraining. |
| Hosting service Fabric-plan |Voor uitbreidingen. |
| App Service ("mam") |Als host fungeert voor de mobiele Apps API-project met eindpunten voor de mobiele app. De API-code moet worden geïmplementeerd in App Service vanuit Visual Studio. |
| Regels voor waarschuwingen |Verzendt dat u e-als de app-antwoorden duiden op fouten. |
| Application Insights |Voor het bewaken van de prestaties van de API in App Service. U moet de verbinding wordt geconfigureerd in Visual Studio. |
| Azure Key Vault |Voor het opslaan van het certificaat voor web service-cluster. |

### <a name="run-the-template"></a>Voer de sjabloon
In **scripts/README.md**, er zijn gedetailleerde instructies voor het uitvoeren van de sjabloon.

Voor het inrichten van deze services in uw eigen Azure-account met behulp van het script, doe het volgende:

* PowerShell gebruiken:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *locatie* is de [Azure-locatie](https://azure.microsoft.com/regions/), zoals `North Europe` of `West US`. Gebruik `Get-AzureLocation` aan een lijst met beschikbare locaties.
  * *resourceGroupName* is de naam die u wilt geven aan de groep waartoe alle resources moeten behoren. Wanneer u klaar bent met de resources, kunt u ze allemaal tegelijk verwijderen door deze groep te verwijderen.
* Voer DeploymentScripts/Bash/deploy.sh met Bash.
* Open en bouwen van de Visual Studio-oplossing DeploymentScripts/VS/DeployARM.sln.

Houd er rekening mee dat elke keer dat de sjabloon die wordt uitgevoerd, wordt een nieuwe set resources gemaakt onder een andere naam. U verwijdert de resources, gaat u naar de portal en de resourcegroep verwijderen.

Als het script voor een of andere reden mislukt, kunt u het opnieuw uitvoeren.

Het script geeft u de optie van de configuratie van doorlopende integratie in Visual Studio Team Services. Als u een Team Services-project hebt ingesteld, hebt u een URL: https://yourAccountName.visualstudio.com. Voer de volledige URL als u wordt gevraagd. U kunt daarvoor een nieuwe of bestaande naam voor een Team Services-project.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Instellen van de build en definities in Visual Studio Team Services testen
We gebruiken Team Services op dit project voornamelijk voor de build en functies testen. Maar, biedt ook ondersteuning voor uitstekende samenwerking, zoals Taakbeheer met kanbanborden, code-revisie geïntegreerd met taken en bronbeheer en geregeld bouwt. Het is geïntegreerd met andere hulpprogramma's zoals GitHub, Xamarin HockeyApp en natuurlijk Visual Studio. U kunt toegang tot dit via de web-interface of Visual Studio, indien dit handiger op elk moment.

De stappen in de definities van build en release gebruikt tal van invoegtoepassing services die beschikbaar in de Team Services zijn [Marketplace](https://marketplace.visualstudio.com/VSTS). Naast eenvoudige hulpprogramma's voor opdrachtregels worden uitgevoerd of kopiëren van bestanden, zijn er services die wordt aangeroepen builds door Xamarin-, Android- en andere leveranciers en die verbinding maken met HockeyApp.

![Opties in het Team Services bouwen](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definities bouwen
We hebben build definities voor elk van de belangrijkste doelen. We hebben ook variaties voor functie- en regressie testen. Dat geeft ons:

* MyDriving.Services (de back-end-web-app voor de mobiele app)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-functie
  * MyDriving.Xamarin.Android regressie
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-functie
  * MyDriving.Xamarin.iOS regressie
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-functie
  * MyDriving.Xamarin.UWP regressie

Als u zien van de volledige details van de configuratie wilt, raadpleegt u de sectie 4.7 van de [MyDriving handleiding](http://aka.ms/mydrivingdocs), 'Build en Release-configuratie.' Ze volgen de algemene patroon. Het script:

1. Hiermee herstelt u het NuGet-pakket. We bewaren niet gecompileerde code in de opslagplaats, zodat de eerste stappen van elke build zijn de vereiste NuGet-pakketten.
2. De licentie activeert. De build wordt uitgevoerd in de cloud, zodat indien een licentie--moet met name voor de Xamarin-build-service--we hebben onze licentie op de huidige build-machine te activeren. Vervolgens wordt deze deactiveren onmiddellijk daarna zodat deze kan worden gebruikt op een andere computer.
3. Met behulp van de desbetreffende service is gebaseerd. We gebruiken Xamarin builds voor mobiele apps en Visual Studio maakt voor de back-end-webservice.
4. Tests is gebaseerd.
5. Voert testen uit. We de tests voor de mobiele app in Xamarin-Testcloud uitgevoerd.
6. Het resultaat van de build publiceert naar de doellocatie.

De trigger voor de belangrijkste builds is ingesteld op continue integratie. Dat wil zeggen, de build uitgevoerd telkens wanneer de code wordt ingecheckt bij de hoofdvertakking.

![Interface waarvan de trigger is ingesteld op doorlopende integratie](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definities van release
Release-definities worden ingesteld op ongeveer dezelfde manier.

Voor de webservice instellen we implementatie als een Azure-web-app:

![Interface voor het instellen van de implementatie als een Azure-web-app](./media/iot-solution-build-system/image7.png)

En we de release-trigger voor continue implementatie instellen. Dat wil zeggen, elke inchecken gevolgd door een geslaagde build resulteert in een update naar de web-app.

![Interface voor het instellen van de release-trigger voor continue implementatie](./media/iot-solution-build-system/image8.png)

We implementeren naar HockeyApp voor mobiele apps:

![Interface voor het implementeren van een mobiele app naar HockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Telemetrie verkennen met behulp van Application Insights
[Application Insights](../application-insights/app-insights-overview.md) telemetrie over de prestaties en het gebruik van uw webservices worden verzameld. De Application Insights-SDK verzendt telemetrie van de service naar de Application Insights-resource in Azure.

Blader naar de Application Insights-resource die de sjabloon is ingesteld. Daar vindt u op de grafieken van de prestaties van uw [mobiele App Service-project](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Deze serveraanvragen en reactietijden, fouten, weergeven en uitzondering telt. Er zijn ook grafieken van afhankelijkheid responstijden--dat wil zeggen, aanroepen naar de database en REST-API's zoals Machine Learning. Als er problemen met de prestaties, kunt u zult kunnen zien welk onderdeel van uw systeem veroorzaken.

![Voorbeeld van grafiek](./media/iot-solution-build-system/image11.png)

Als u een webservice die u handmatig hebt ingesteld hebt, is het verkrijgen van de dezelfde grafieken. Klik op de blade web-service op **extra** > **extensies** > **toevoegen**. Selecteer **Application Insights**.

![Interface voor het selecteren van Application Insights om op te halen van de grafieken](./media/iot-solution-build-system/image12.png)

De functie werkt door het instrumenteren van uw toepassing met de Application Insights-SDK.

U kunt aangepaste telemetrie (of dat een toepassing die ergens buiten Azure wordt uitgevoerd) toevoegen door [Application Insights-SDK toevoegen](../application-insights/app-insights-asp-net.md) tijdens ontwikkeling. Dit is handig voor logboek-metrische gegevens die afhankelijk van de toepassing, zoals gebruikers gemiddelde reis lengte of Totaalaantal kilometers zijn. In Visual Studio met de rechtermuisknop op het project en selecteer vervolgens **Application Insights toevoegen**.

![Interface voor het selecteren van Application Insights toevoegen aan het toevoegen van aangepaste telemetrie](./media/iot-solution-build-system/image10.png)

Application Insights wordt waarschuwingsmails sturen als er vreemde aantal mislukte reacties. U kunt ook uw eigen waarschuwingen op verschillende metrische gegevens, zoals responstijden instellen.

Alleen om ervoor te zorgen dat uw web-service is altijd up-to-date en wordt uitgevoerd, kunt u instellen [beschikbaarheidstests](../application-insights/app-insights-monitor-web-app-availability.md). Deze tests ping uw site vanuit verschillende locaties over de hele wereld om de 15 minuten. U krijgt een e-mailbericht opnieuw als blijkt te zijn van een probleem.

## <a name="estimate-operational-costs"></a>Schatting maken van de operationele kosten
Het is opmerkelijk goedkope een app in zoals deze op kleine schaal uitvoert. Veel van de services hebben gratis instapmodellen lagen, zodat de ontwikkeling en kleinschalige bewerking weinig kosten. En uw eigen apps niet beschikken over alle functies in MyDriving gedemonstreerd gebruiken.

Hier volgt een ruwe schatting van onze kosten bij het instellen van de configuratie van de ontwikkeling voor MyDriving. We enkele alternatieven die we hebben ook Opmerking *niet* gebruiken. Deze informatie kan nuttig zijn als u een schatting maken van uw eigen kosten.

We gaan ervan uit:

* Een team van niet meer dan vijf (plus observeren belanghebbenden).
* Uitgevoerd over een maand.
* 100 gebruikers met vier reizen per dag.

> [!NOTE]
> Als u geen ervaring met Azure, er is een [gratis account](https://azure.microsoft.com/free/).
> 
> 

| **Onderdeel-service** | **Opmerkingen bij de** | **Kosten per maand** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) met [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Cross-platform dev-omgeving |Visual Studio Community. (Moet [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) voor [Xamarin.Forms](https://xamarin.com/forms), voor het ontwerpen van cross-platform van één codebasis.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Wederzijdse gegevensverbinding met apparaten |8000 berichten + 0,5 KB/bericht vrij te geven. |$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Stroom van grote hoeveelheden gegevens verwerken |De kosten van $0,031 per eenheid per uur, streaming terwijl ingeschakeld. Kies van het aantal streaming-eenheden die u wilt. meer worden uitgebreid. |$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Adaptieve reacties |seat-$10/maand. <br/>                                                                                                                                                                                 + 3 uur experiment \* $1 / experimenteren uur. <br/>                                                                                                                                                           + 3.5 uur API CPU \* $2 / productie CPU uur. <br/>                                                                                                                                                          API-CPU-tijd wordt ervan uitgegaan 5 min. per dag retraining, hoewel dit zou toename met meer invoergegevens.                   <br/>                                                                                                                                                                     + 2 min. per dag score berekenen voor het verwerken van 400 reizen per dag. |$20 |
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
Omdat we MyDriving om te helpen aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker graag van u over hoe goed werkt. Laat ons weten als:

* U ondervindt problemen of uitdagingen.
* Er is een extensiepunt zou om het meest geschikt is voor uw scenario.
* U vindt een efficiëntere manier voor het uitvoeren van bepaalde behoeften.
* U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.

Als u feedback geven, een probleem op GitHub bestand of een opmerking hieronder laat (en-us edition).

We hopen graag van u!

## <a name="next-steps"></a>Volgende stappen
Het is raadzaam de [MyDriving handleiding](http://aka.ms/mydrivingdocs), dit is een uitgebreide beschrijving van het ontwerp van het systeem en de bijbehorende onderdelen.

