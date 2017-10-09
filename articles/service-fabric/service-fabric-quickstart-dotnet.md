---
title: een .NET Service Fabric-toepassing in Azure aaaCreate | Microsoft Docs
description: Maak een .NET-toepassing voor Azure Hallo Service Fabric-voorbeeld gebruikt snel starten.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Een .NET-Service Fabric-toepassing maken in Azure
Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u schaalbare en betrouwbare microservices en containers implementeert en beheert. 

Deze snelstartgids toont hoe toodeploy uw eerste .NET application tooService Fabric. Wanneer u klaar bent, hebt u een stemtoepassing met een ASP.NET Core web-front-die stemmende resultaten worden opgeslagen in een stateful back-end-service in Hallo-cluster.

![Schermafbeelding van de toepassing](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

Met behulp van deze toepassing u leert hoe:
> [!div class="checklist"]
> * Een toepassing maken met .NET- en Service Fabric
> * ASP.NET core gebruiken als een webfront-end
> * Opslaan van toepassingsgegevens in een stateful service
> * Fouten opsporen in uw toepassing lokaal
> * Hallo toepassing tooa cluster in Azure implementeren
> * Scale-out Hallo-toepassing op meerdere knooppunten
> * Een rolling upgrade van de toepassing uitvoeren

## <a name="prerequisites"></a>Vereisten
toocomplete deze snelstartgids:
1. [Installeer Visual Studio 2017](https://www.visualstudio.com/) Hello **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.
2. [Git installeren](https://git-scm.com/)
3. [Hallo Microsoft Azure Service Fabric SDK installeren](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. Voer Hallo opdracht tooenable Visual Studio toodeploy toohello lokale Service Fabric-cluster te volgen:
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a>Hallo voorbeeld downloaden
In een opdrachtvenster Hallo na de opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer worden uitgevoerd.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
Met de rechtermuisknop op Hallo Visual Studio-pictogram in het Menu Start Hallo en kies **als administrator uitvoeren**. In de volgorde tooattach Hallo foutopsporingsprogramma tooyour services moet u toorun Visual Studio als beheerder.

Open Hallo **Voting.sln** Visual Studio-oplossing uit Hallo opslagplaats u gekloond.

Druk op-toepassing hello toodeploy **F5**.

> [!NOTE]
> Hallo maakt eerst u uitvoeren en implementeren van de toepassing hello, Visual Studio een lokaal cluster voor foutopsporing. Deze bewerking kan enige tijd duren. status van het Hallo-cluster maken wordt weergegeven in Visual Studio-uitvoervenster Hallo.

Wanneer het Hallo-implementatie is voltooid, een browser starten en open deze pagina: `http://localhost:8080` -Hallo webfront-end van de toepassing hello.

![Front-toepassing](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

U kunt nu een set opties voor uw stem toevoegen en begin met het maken van stemmen. Hallo-toepassing wordt uitgevoerd en alle gegevens worden opgeslagen in het Service Fabric-cluster zonder Hallo nodig is voor een aparte database.

## <a name="walk-through-hello-voting-sample-application"></a>Hallo stemmen voorbeeldtoepassing doorlopen
Hallo stemmen toepassing bestaat uit twee services:
- Web-front-service (VotingWeb): een ASP.NET Core web-front-endservice die webpagina Hallo fungeert en zichtbaar gemaakt web-API's toocommunicate met Hallo back-endservice.
- Back-end-service (VotingData)-Core van een ASP.NET-webservice, die zichtbaar gemaakt die een API toostore Hallo stem in een betrouwbare woordenlijst resulteert op schijf persistent.

![Diagram van de toepassing](./media/service-fabric-quickstart-dotnet/application-diagram.png)

Wanneer u stemmen in Hallo toepassing hello volgende gebeurtenissen:
1. Een JavaScript verzendt Hallo stem aanvraag toohello web API in Hallo web-front-service als een HTTP PUT-aanvraag.

2. Hallo-web-front-service gebruikt een toolocate proxy en doorsturen van een HTTP PUT-aanvraag toohello back-endservice.

3. Hallo back-endservice Hallo inkomende aanvraag duurt en winkels Hallo bijgewerkt resulteren in een betrouwbare woordenlijst die gerepliceerde toomultiple knooppunten binnen Hallo cluster opgehaald en opgeslagen op schijf. Alle Hallo toepassingsgegevens wordt opgeslagen in Hallo-cluster, zodat er geen database nodig is.

## <a name="debug-in-visual-studio"></a>Fouten opsporen in Visual Studio
Als u fouten opspoort toepassing in Visual Studio, gebruikt u een lokaal cluster van de Service Fabric-ontwikkeling. U hebt uw foutopsporing ervaring tooyour scenario Hallo optie tooadjust. In deze toepassing opgeslagen gegevens in onze back-end-service met behulp van een betrouwbare woordenlijst. Visual Studio Hiermee verwijdert u de toepassing hello per standaard wanneer u Hallo foutopsporingsprogramma stopt. Verwijderen van de toepassing hello zorgt ervoor dat de gegevens Hallo in Hallo back-end service tooalso worden verwijderd. toopersist hello gegevens tussen foutopsporingssessies, kunt u Hallo **toepassing foutopsporingsmodus** als eigenschap op Hallo **Voting** -project in Visual Studio.

toolook op wat er gebeurt in Hallo code voltooid Hallo stappen te volgen:
1. Open Hallo **VotesController.cs** bestands- en stel een onderbrekingspunt in Hallo web-API's **plaatsen** methode (regel 47) - u kunt zoeken naar Hallo-bestand in Hallo Solution Explorer in Visual Studio.

2. Open Hallo **VoteDataController.cs** bestands- en stel een onderbrekingspunt in deze web-API **plaatsen** methode (line 50).

3. Ga terug toohello browser en klik op een optie of toevoegen van een nieuwe stemmende optie. U onderbrekingspunt Hallo eerste in Hallo web front-end van api-controller.
    - Dit is waar Hallo JavaScript in browser Hallo verzendt u een aanvraag toohello web API-controller in Hallo front-end-service.
    
    ![Stem front-end-Service toevoegen](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - Eerst we Hallo URL toohello ReverseProxy opstellen voor onze back-endservice **(1)**.
    - Vervolgens we Hallo HTTP PUT-aanvraag toohello ReverseProxy sturen **(2)**.
    - Ten slotte hello wordt teruggeplaatst antwoord Hallo van Hallo back-endservice toohello client **(3)**.

4. Druk op **F5** toocontinue
    - U bent nu op Hallo break punt in Hallo back-endservice.
    
    ![Stem Back-End-Service toevoegen](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - In de eerste regel in de methode Hallo Hallo **(1)** gebruiken we Hallo `StateManager` tooget of toevoegen van een betrouwbare woordenlijst aangeroepen `counts`.
    - Alle interacties met waarden in een betrouwbare woordenlijst vereisen een transactie, deze met de instructie **(2)** die transactie maakt.
    - In de transactie hello, werk we vervolgens Hallo-waarde van relevante Hallo-sleutel voor uw stem optie Hallo en doorvoeracties Hallo bewerking **(3)**. Zodra het Hallo doorvoeren retourneert methode, Hallo gegevens wordt bijgewerkt in de woordenlijst Hallo en tooother knooppunten in cluster Hallo gerepliceerd. Hallo gegevens worden nu veilig opgeslagen in de cluster Hallo en Hallo back-endservice failover tooother knooppunten, nog steeds Hallo gegevens beschikbaar.
5. Druk op **F5** toocontinue

toostop hello foutopsporingssessie, drukt u op **Shift + F5**.

## <a name="deploy-hello-application-tooazure"></a>Hallo toepassing tooAzure implementeren
toodeploy hello toepassing tooa cluster in Azure, u kunt ofwel toocreate uw eigen cluster of gebruik een Cluster van derden.

Partijen clusters zijn gratis, tijdelijke Service Fabric clusters gehost op Azure en uitgevoerd door Hallo Service Fabric-team waar iedereen toepassingen implementeren en meer informatie over het Hallo-platform. tooget toegang tooa partij Cluster [Hallo instructies](http://aka.ms/tryservicefabric). 

Zie voor meer informatie over het maken van uw eigen cluster [Uw eerste Service Fabric-cluster maken op Azure](service-fabric-get-started-azure-cluster.md).

> [!Note]
> Hallo-web-front-service is geconfigureerd toolisten op poort 8080 voor binnenkomend verkeer. Zorg ervoor dat de poort is geopend in het cluster. Als u Hallo partij Cluster gebruikt, is deze poort is geopend.
>

### <a name="deploy-hello-application-using-visual-studio"></a>Hallo-toepassing met Visual Studio implementeren
Nu dat de toepassing hello klaar is, kunt u het cluster tooa rechtstreeks vanuit Visual Studio implementeren.

1. Met de rechtermuisknop op **Voting** Hallo in Solution Explorer en kiest u **publiceren**. Hallo publiceren dialoogvenster wordt weergegeven.

    ![Het dialoogvenster Publiceren](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. Type in Hallo verbindingseindpunt van Hallo-cluster op Hallo **verbindingseindpunt** veld en klikt u op **publiceren**. Wanneer u zich registreren voor Hallo partij Cluster, vindt u in Hallo browser Hallo verbindingseindpunt. -bijvoorbeeld `winh1x87d1d.westus.cloudapp.azure.com:19000`.

3. Open een browser en typ in het adres van de cluster Hallo - bijvoorbeeld `http://winh1x87d1d.westus.cloudapp.azure.com`. U ziet nu Hallo-toepassing in Hallo-cluster in Azure wordt uitgevoerd.

![Front-toepassing](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>Toepassingen en services voor schalen in een cluster
Service Fabric-services kunnen eenvoudig worden geschaald over een tooaccommodate cluster voor een wijziging in Hallo belasting op Hallo-services. U schaalt een service door Hallo aantal exemplaren in Hallo cluster wordt uitgevoerd te wijzigen. U hebt meerdere manieren schalen van uw services, kunt u scripts of opdrachten van PowerShell of CLI van de Fabric-Service (sfctl). In dit voorbeeld gebruiken we Service Fabric Explorer.

Service Fabric Explorer wordt uitgevoerd in alle Service Fabric-clusters en toegankelijk is vanuit een browser door te bladeren toohello clusters HTTP-poort (19080), bijvoorbeeld `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.

Hallo tooscale web-front-endservice, Hallo volgende stappen:

1. Open Service Fabric Explorer in het cluster - bijvoorbeeld: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
2. Klik op Hallo weglatingsteken (drie punten) volgende toohello **fabric: / Voting/VotingWeb** knooppunt in de treeview Hallo en kies **Scale Service**.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    U kunt nu tooscale Hallo aantal exemplaren van Hallo web-front-service.

3. Hallo nummer te wijzigen**2** en klik op **Scale Service**.
4. Klik op Hallo **fabric: / Voting/VotingWeb** knooppunt in Hallo structuurweergave en Hallo partitie knooppunt (vertegenwoordigd door een GUID zijn).

    ![Service Fabric Explorer Scale-Service](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    U ziet nu dat Hallo-service twee instanties heeft, en in de structuurweergave Hallo u welke knooppunten Hallo instanties worden uitgevoerd ziet op.

Door deze taak eenvoudig beheer verdubbeld we Hallo bronnen beschikbaar voor de front-end-service tooprocess gebruiker werklast. Het is belangrijk toounderstand die u hoeft niet meerdere exemplaren van een service toohave het op betrouwbare wijze uitgevoerd. Als de service is mislukt, Service Fabric, zorgt dat een nieuwe service-exemplaar in Hallo cluster wordt uitgevoerd.

## <a name="perform-a-rolling-application-upgrade"></a>Een rolling upgrade van de toepassing uitvoeren
Bij het implementeren van nieuwe updates tooyour toepassing implementeert Service Fabric Hallo update op een veilige manier. Rolling upgrades biedt u geen uitvaltijd tijdens het bijwerken of het terugdraaien van de geautomatiseerde moeten fouten optreden.

tooupgrade toepassing hello, Hallo te volgen:

1. Open Hallo **Index.cshtml** bestand in Visual Studio - u kunt zoeken naar Hallo-bestand in Hallo Solution Explorer in Visual Studio.
2. Hallo koppen op Hallo pagina wijzigen door sommige tekst - bijvoorbeeld toe te voegen.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. Hallo-bestand opslaan.
4. Met de rechtermuisknop op **Voting** Hallo in Solution Explorer en kiest u **publiceren**. Hallo publiceren dialoogvenster wordt weergegeven.
5. Klik op Hallo **Manifest versie** knop toochange Hallo versie van het Hallo-service en toepassing.
6. Hallo-versie wijzigen van Hallo **Code** element onder **VotingWebPkg** te '2.0.0' bijvoorbeeld en op **opslaan**.

    ![Dialoogvenster van de versie wijzigen](./media/service-fabric-quickstart-dotnet/change-version.png)
7. In Hallo **Service Fabric-toepassing publiceren** dialoogvenster selectievakje Hallo Upgrade Hallo toepassing selectievakje en klikt u op **publiceren**.

    ![Dialoogvenster publiceren instelling upgraden](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. Open uw browser en blader toohello clusteradres op poort 19080 - bijvoorbeeld `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
9. Klik op Hallo **toepassingen** knooppunt in de structuurweergave hello, en vervolgens **Upgrades uitgevoerd** in het rechterdeelvenster Hallo. U ziet hoe Hallo upgrade totaliseert via Hallo upgradedomeinen in uw cluster ervoor te zorgen dat elk domein in orde is voordat u doorgaat toohello naast.
    ![Upgrade weergeven in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)

    Service Fabric maakt upgrades veilig door Wacht twee minuten na de upgrade Hallo-service op elk knooppunt in het Hallo-cluster. Hallo volledige update tootake ongeveer 8 minuten verwacht.

10. Tijdens het Hallo-upgrade wordt uitgevoerd, kunt u nog steeds Hallo-toepassing. Omdat er twee exemplaren van Hallo-service in Hallo cluster wordt uitgevoerd, kunnen sommige met uw verzoeken, een bijgewerkte versie van de toepassing hello, krijgen terwijl anderen mogelijk nog steeds de oude versie van de Hallo.

## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u de volgende zaken geleerd:

> [!div class="checklist"]
> * Een toepassing maken met .NET- en Service Fabric
> * ASP.NET core gebruiken als een webfront-end
> * Opslaan van toepassingsgegevens in een stateful service
> * Fouten opsporen in uw toepassing lokaal
> * Hallo toepassing tooa cluster in Azure implementeren
> * Scale-out Hallo-toepassing op meerdere knooppunten
> * Een rolling upgrade van de toepassing uitvoeren

toolearn meer informatie over Service Fabric en .NET, kijk eens naar deze zelfstudie:
> [!div class="nextstepaction"]
> [.NET-toepassing op Service Fabric](service-fabric-tutorial-create-dotnet-app.md)