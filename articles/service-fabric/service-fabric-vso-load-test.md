---
title: aaaLoad uw toepassing testen met behulp van Visual Studio Team Services | Microsoft Docs
description: Meer informatie over hoe toostress uw Azure Service Fabric-toepassingen testen met behulp van Visual Studio Team Services.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Uw toepassing werklast testen met behulp van Visual Studio Team Services
Dit artikel laat zien hoe toouse Microsoft Visual Studio load test functies toostress testen voor een toepassing. Maakt gebruik van een Azure Service Fabric stateful service back-end en een webfront-end staatloze service. Hallo is voorbeeldtoepassing gebruikt hier een locatie in een vliegtuig simulator. U opgeven dat een vliegtuig-ID, de vertrektijd en de bestemming. Hallo back-end van de toepassing hello aanvragen verwerkt en Hallo-front-end wordt weergegeven in een kaart Hallo vliegtuig die overeenkomt met de Hallo criteria.

Hallo illustreert volgende diagram Hallo Service Fabric-toepassing die u gaat testen.

![Diagram van een vliegtuig Hallo-locatie voorbeeldtoepassing][0]

## <a name="prerequisites"></a>Vereisten
Voordat u aan de slag, hebt u toodo Hallo volgende nodig:

* Maak een Visual Studio Team Services-account. U kunt een gratis verkrijgen op [Visual Studio Team Services](https://www.visualstudio.com).
* Ontvangen en Visual Studio 2013 of Visual Studio 2015 te installeren. Dit artikel wordt Visual Studio 2015 Enterprise edition gebruikt, maar Visual Studio 2013 en andere edities moeten op dezelfde manier werken.
* Implementeer uw toepassing tooa staging-omgeving. Zie [hoe toodeploy toepassingen tooa externe cluster met Visual Studio](service-fabric-publish-app-remote-cluster.md) voor informatie over deze.
* Inzicht in uw toepassing gebruikspatroon. Deze informatie is gebruikte toosimulate Hallo load patroon.
* Hallo-doel voor het testen van uw belasting te begrijpen. Dit helpt u bij het interpreteren en analyseren van de resultaten bekijkt hello laden.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Maken en Hallo Webprestatie- en belastingstest project uitvoeren
### <a name="create-a-web-performance-and-load-test-project"></a>Een Web-prestatie- en belastingstest-project maken
1. Open Visual Studio 2015. Kies **bestand** > **nieuw** > **Project** op Hallo menubalk tooopen hello **nieuw Project** in het dialoogvenster.
2. Vouw Hallo **Visual C#** knooppunt en kies **Test** > **Webprestatie- en belastingstest project**. Geef een naam op Hallo-project en kies vervolgens Hallo **OK** knop.

    ![Schermopname van dialoogvenster Hallo-nieuw Project][1]

    Hier ziet u een nieuw Webprestatie- en belastingstest project in Solution Explorer.

    ![Schermopname van Solution Explorer toont Hallo nieuw project][2]

### <a name="record-a-web-performance-test"></a>Neem een WebTest prestaties
1. Open Hallo .webtest project.
2. Kies Hallo **toevoegen Recording** pictogram toostart een opnamesessie in uw browser.

    ![Schermopname van Hallo opname toevoegen-pictogram in een browser][3]

    ![Schermafdruk van knop voor Hallo opnemen in een browser][4]
3. Blader toohello Service Fabric-toepassing. Hallo opname Configuratiescherm Hallo webaanvragen moet worden weergegeven.

    ![Schermopname van webaanvragen in Hallo Configuratiescherm opnemen][5]
4. Een reeks acties die u verwacht Hallo gebruikers tooperform dat uitvoeren. Deze acties worden gebruikt als een patroon toogenerate Hallo belasting.
5. Wanneer u bent klaar, kiest u Hallo **stoppen** knop toostop opnemen.

    ![Schermafdruk van knop voor stoppen Hallo][6]

    Hallo .webtest-project in Visual Studio moet een reeks aanvragen hebt vastgelegd. Dynamische parameters worden automatisch vervangen. Op dit moment kunt u extra, herhaalde afhankelijkheid verzoeken die geen deel uitmaken van uw testscenario verwijderen.
6. Sla Hallo-project en kies vervolgens Hallo **uitvoeren testen** opdracht toorun Hallo webprestaties lokaal testen en te controleren of alles correct werkt.

    ![Schermopname van het Hallo opdracht Test uitvoeren][7]

### <a name="parameterize-hello-web-performance-test"></a>Hallo prestaties WebTest voorzien
U kunt Hallo prestaties WebTest parameter converteren van de WebTest prestaties tooa gecodeerd en vervolgens bewerken Hallo-code. U kunt als alternatief kunt Hallo web prestaties test tooa gegevenslijst binden zodat hello test Hallo-gegevens doorlopen. Zie [genereren en voer een gecodeerde WebTest prestaties](https://msdn.microsoft.com/library/ms182552.aspx) voor meer informatie over hoe tooconvert Hallo web prestaties test tooa test gecodeerd. Zie [toevoegen van een prestatietest data source tooa web](https://msdn.microsoft.com/library/ms243142.aspx) voor meer informatie over hoe toobind gegevens tooa web-prestaties testen.

In dit voorbeeld hebt we Hallo prestaties test tooa gecodeerde WebTest converteren zodat u kunt Hallo vliegtuig ID door een gegenereerde GUID vervangen en meer aanvragen toosend vlucht toodifferent locaties toevoegen.

### <a name="create-a-load-test-project"></a>Een load-test-project maken
Een load-testproject bestaat uit een of meer scenario's beschreven door Hallo prestaties WebTest en testen van eenheden, samen met de instellingen voor extra belasting van de opgegeven testen. Hallo stappen te volgen tonen hoe een load toocreate project testen:

1. Kies in het snelmenu Hallo van uw project Webprestatie- en belastingstest, **toevoegen** > **belastingstest**. In Hallo **Load testen** wizard Hallo kiezen **volgende** knop instellingen van tooconfigure Hallo testen.
2. In Hallo **patroon laden** sectie, kiest u of u wilt een constante gebruikersbelasting of een stap belasting, die met een paar gebruikers begint en toeneemt Hallo gebruikers gedurende een bepaalde periode.

    Als u een goede schatting van de hoeveelheid gebruikersbelasting Hallo hebt en wilt toosee hoe het huidige systeem Hallo uitvoert, kiest u **constante laden**. Als het doel toolearn is of Hallo system consistent onder verschillende belasting voert, kiest u **stap Load**.
3. In Hallo **testen combinatie** sectie, kiest u Hallo **toevoegen** knop en selecteer vervolgens Hallo testen die u wilt dat tooinclude in Hallo belastingtest uit. U kunt Hallo **distributie** kolom toospecify Hallo percentage van totale tests uitvoeren voor elke test.
4. In Hallo **instellingen uitvoeren** sectie, Hallo load testduur opgeven.

   > [!NOTE]
   > Hallo **testen iteraties** optie is beschikbaar alleen bij het uitvoeren van een load-test lokaal met Visual Studio.
   >
   >
5. In Hallo **locatie** sectie van **instellingen uitvoeren**, geef Hallo locatie waarbij load test aanvragen worden gegenereerd. Hallo-wizard wordt u mogelijk gevraagd toolog in tooyour Team Services-account. Meld u bij en kies vervolgens een geografische locatie. Wanneer u bent klaar, kiest u Hallo **voltooien** knop.
6. Nadat Hallo load test is gemaakt, opent u het Hallo .loadtest project en kies Hallo huidige uitgevoerd instelling, zoals **instellingen uitvoeren** > **Settings1 uitvoeren [actieve]**. Hallo uitvoeren instellingen wordt geopend in Hallo **eigenschappen** venster.
7. In Hallo **resultaten** sectie Hallo **instellingen uitvoeren** eigenschappenvenster, Hallo **Timing Details opslag** instelling hebt **geen** als de standaardwaarde. Deze waarde te wijzigen**alle afzonderlijke Details** tooget meer informatie over de resultaten bekijkt hello laden. Zie [laden testen](https://www.visualstudio.com/load-testing.aspx) voor meer informatie over hoe tooconnect tooVisual Studio Team Services en voer een werklast test.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Hallo load test uitvoeren met behulp van Visual Studio Team Services
Kies Hallo **Load testen uitvoeren** opdracht toostart Hallo test uitvoeren.

![Schermopname van het Hallo opdracht Load Test uitvoeren][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Weergeven en analyseren van Hallo load testresultaten
Als Hallo laden van de voortgang van de test, informatie over de prestaties van Hallo grafiek moeten worden weergegeven. Hier ziet u iets dergelijks toohello grafiek te volgen.

![Schermopname van Prestatiegrafiek voor load testresultaten][9]

1. Kies Hallo **Download rapport** koppeling bij Hallo Hallo pagina bovenaan. Nadat het Hallo-rapport wordt gedownload, kiest u Hallo **rapport weergeven** knop.

    Op Hallo **grafiek** tabblad kunt u diagrammen voor verschillende prestatiemeteritems zien. Op Hallo **samenvatting** tabblad hello algemene resultaten worden weergegeven. Hallo **tabellen** tabblad Hallo totaal aantal geslaagde en mislukte load tests ziet.
2. Kies Hallo aantal koppelingen op Hallo **Test** > **mislukt** en Hallo **fouten** > **aantal** kolommen toosee foutgegevens.

    Hallo **Detail** tabblad ziet u virtuele gebruikers- en informatie over scenario's voor mislukte aanvragen. Deze gegevens kan nuttig zijn als Hallo load test meerdere scenario's bevat.

Zie [resultaten voor het laden van testen analyseren in Hallo grafieken weergave Hallo testen Analyzer laden](https://www.visualstudio.com/load-testing.aspx) resultaten voor meer informatie over het weergeven van de belasting te testen.

## <a name="automate-your-load-test"></a>Uw test load automatiseren
Visual Studio Team Services laden Test biedt API's toohelp u load tests beheren en analyseren van resultaten in een Team Services-account. Zie [Cloud Load testen Rest-API's](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
* [Controle en diagnose van services in de instellingen voor een lokale computer-ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
