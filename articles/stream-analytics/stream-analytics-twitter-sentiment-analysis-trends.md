---
title: aaaReal tijd Twitter-gevoel analyse met Azure Stream Analytics | Microsoft Docs
description: Meer informatie over hoe toouse Stream Analytics voor analyse van realtime Twitter-gevoel. Stapsgewijze richtlijnen van gebeurtenis generatie toodata in een live dashboard.
keywords: het trendanalyse realtime twitter, gevoel analyse, analyse van sociale media, trend analysis-voorbeeld
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Real-time Twitter-gevoel analyse in Azure Stream Analytics

Meer informatie over hoe een gevoel analysis-oplossing voor sociale media analytics doordat realtime toobuild gebeurtenissen Twitter in Azure Event Hubs. Vervolgens kunt u een Azure Stream Analytics query tooanalyze Hallo gegevens en de archieven Hallo resultaten voor later gebruik of gebruik een dashboard en [Power BI](https://powerbi.com/) tooprovide inzichten in realtime.

Sociale media analytics-hulpprogramma's waarmee organisaties kunnen begrijpen trends onderwerpen. Trends onderwerpen zijn onderwerpen en houding die een groot aantal berichten in sociale media hebt. Gevoel analyse, ook wel genoemd *advies analysemodel*, maakt gebruik van sociale media analytics extra toodetermine houding ten opzichte van een product, idee, enzovoort. 

Trendgrafiek van realtime Twitter is een goed voorbeeld van een hulpprogramma voor analyse, omdat Hallo hashtag abonnementsmodel kunt u toolisten toospecific trefwoorden (hashtags) en gevoel analyse van de feed Hallo ontwikkelen.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Scenario: Sociale media gevoel analyse in realtime

Een bedrijf met een website nieuws media is geïnteresseerd in een voordeel ten opzichte van de concurrenten krijgen door de inhoud van de site die onmiddellijk relevante tooits lezers. analyse van sociale media Hallo bedrijf gebruikt op onderwerpen die relevant tooreaders zijn als volgt realtime gevoel analyse van gegevens van Twitter.

onderwerpen over trends in realtime op Twitter, tooidentify Hallo bedrijf behoeften realtime analyses over Hallo tweet volume en gevoel voor belangrijke onderwerpen. Hallo nodig is met andere woorden, een gevoel analysis analytics-engine die gebaseerd op deze sociale media feed.

## <a name="prerequisites"></a>Vereisten
In deze zelfstudie gebruikt u een clienttoepassing die is verbonden tooTwitter en zoekt tweets waarvoor bepaalde hashtags (die u kunt instellen). In volgorde toorun toepassing hello en analyseren van Hallo tweets met Azure Streaming Analytics, moet u de volgende Hallo hebben:

* Een Azure-abonnement
* Een Twitter-account 
* Een Twitter-toepassing en Hallo [OAuth-toegangstoken](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) voor die toepassing. We bieden op hoog niveau instructies voor het toocreate later een Twitter-toepassing.
* Hallo TwitterWPFClient toepassing, wat Hallo Twitter leest-feed. tooget deze toepassing, download Hallo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) bestand van GitHub en pak vervolgens Hallo-pakket naar een map op uw computer. Als u wilt dat toosee Hallo broncode en Hallo toepassing uitvoert in een foutopsporingsprogramma, u de broncode Hallo van krijgt [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Maken van een event hub voor Streaming Analytics invoer

Hallo-voorbeeldtoepassing gebeurtenissen gegenereerd en stuurt ze tooan Azure event hub. Azure event hubs zijn Hallo voorkeurs-methode van gebeurtenis opname voor Stream Analytics. Zie voor meer informatie, Hallo [documentatie van Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Een event hub-naamruimte en event hub maken
In deze procedure maakt u eerst een event hub-naamruimte maken en vervolgens voegt u toe een event hub toothat naamruimte. Event hub-naamruimten worden gebruikt toologically groep gerelateerde gebeurtenis bus exemplaren. 

1. Meld u bij toohello Azure-portal en klikt u op **nieuw** > **Internet der dingen** > **Event Hub**. 

2. In Hallo **naamruimte maken** blade, voer de naam van een naamruimte zoals `<yourname>-socialtwitter-eh-ns`. Kunt u een naam voor de naamruimte hello, maar Hallo-naam moet geldig zijn voor een URL en deze uniek zijn binnen Azure. 
    
3. Selecteer een abonnement maken of een resourcegroep kiezen, en klikt u op **maken**. 

    ![Een event hub-naamruimte maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Wanneer het Hallo-naamruimte is voltooid implementeren, vinden Hallo event hub naamruimte in uw lijst met Azure-resources. 

5. Klik op de nieuwe naamruimte Hallo en op Hallo naamruimte Blade  **+ &nbsp;Event Hub**. 

    ![Hallo toevoegen Event Hub knop voor het maken van nieuwe event hub ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Naam Hallo nieuwe event hub `socialtwitter-eh`. U kunt een andere naam gebruiken. Als u dit doet, noteer, omdat u de naam van de hello later nodig. U hoeft niet tooset andere opties voor Hallo event hub.

    ![Blade voor het maken van nieuwe event hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Klik op **Create**.


### <a name="grant-access-toohello-event-hub"></a>Verleen toegang toohello event hub

Voordat een proces gegevens tooan event hub verzendt kan, moet Hallo event hub een beleid waarmee u de juiste toegang hebben. Hallo toegangsbeleid produceert een verbindingsreeks die autorisatie-informatie bevat.

1.  Klik op Hallo gebeurtenis naamruimte blade **Event Hubs** en klik vervolgens op Hallo-naam van uw nieuwe event hub.

2.  Klik op Hallo event hubblade **gedeeld toegangsbeleid** en klik vervolgens op  **+ &nbsp;toevoegen**.

    >[!NOTE]
    >Zorg ervoor dat u werkt met Hallo event hub niet Hallo event hub naamruimte.

3.  Een beleid met de naam toevoegen `socialtwitter-access` en voor **Claim**, selecteer **beheren**.

    ![Blade voor een nieuwe event hub-beleid maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Klik op **Create**.

5.  Nadat Hallo beleid is geïmplementeerd, klikt u op het Hallo-lijst met beleidsregels voor gedeelde toegang.

6.  Hallo-zoekvak met het label **CONNECTION STRING-primaire sleutel** en klik op Hallo kopie knop volgende toohello-verbindingsreeks. 
    
    ![Kopiëren van primaire verbindingssleutel tekenreeks Hallo van Hallo-beleid](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Hallo-verbindingsreeks in een teksteditor plakken. U moet deze verbindingsreeks voor de volgende sectie hello, nadat u een aantal kleine wijzigingen tooit.

    Hallo-verbindingsreeks ziet er als volgt:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    U ziet dat Hallo-verbindingsreeks meerdere sleutel / waarde-paren bevat, gescheiden door puntkomma's: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, en `EntityPath`.  

    > [!NOTE]
    > Voor beveiliging zijn onderdelen van de verbindingsreeks Hallo in Hallo voorbeeld verwijderd.

8.  Verwijder in de teksteditor Hallo Hallo `EntityPath` paar uit de verbindingsreeks hello (Vergeet niet tooremove Hallo puntkomma voorafgaande). Wanneer u bent klaar, uitziet de verbindingsreeks Hallo:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Configureren en starten van de toepassing hello Twitter-client
Hallo-clienttoepassing opgehaald tweet gebeurtenissen rechtstreeks vanuit Twitter. In volgorde toodo doet, moet machtigingen toocall Hallo Twitter Streaming-API's. tooconfigure dat toestemming hebben, u een toepassing maakt in Twitter, dat wordt gegenereerd unieke referenties (zoals een OAuth-token). Vervolgens kunt u Hallo client toepassing toouse deze referenties wanneer het API-aanroepen maakt. 

### <a name="create-a-twitter-application"></a>Een Twitter-toepassing maken
Als u nog geen een Twitter-toepassing die u voor deze zelfstudie gebruiken kunt, kunt u een maken. U moet al een Twitter-account hebben.

> [!NOTE]
> de exacte stappen Hallo in Twitter voor het maken van een toepassing en het Hallo-sleutels, geheimen en -token ophalen kan worden gewijzigd. Als u deze instructies niet overeenkomen met wat u ziet op Hallo Twitter-site, raadpleegt u toohello Twitter-documentatie voor ontwikkelaars.

1. Ga toohello [Twitter application management-pagina](https://apps.twitter.com/). 

2. Maak een nieuwe toepassing. 

    * Geef een geldige URL voor Hallo-website-URL. Er geen toobe een live site. (U kunt niet alleen opgeven `localhost`.)
    * Hallo callback veld leeg laten. Hallo-clienttoepassing die u voor deze zelfstudie gebruiken vereist geen retouraanroepen.

    ![Maken van een toepassing in Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Wijzig eventueel Hallo Toepassingsmachtigingen tooread alleen-lezen.

4. Wanneer de toepassing hello wordt gemaakt, gaat u toohello **sleutels en toegangstokens** pagina.

5. Klik op Hallo knop toogenerate een toegangstoken en toegang token geheim.

Bewaar deze informatie bij de hand hebt, hebt u deze in de volgende procedure Hallo.

>[!NOTE]
>Hallo-sleutels en geheimen voor Hallo Twitter-toepassing biedt toegang tooyour Twitter-account. Deze informatie als vertrouwelijk te behandelen, dezelfde Hallo als u uw wachtwoord Twitter. Bijvoorbeeld: deze informatie in een toepassing dat u tooothers geeft niet insluiten. 


### <a name="configure-hello-client-application"></a>Hallo-clienttoepassing configureren
Er is een clienttoepassing die verbinding via de tooTwitter gegevens maakt gemaakt [Twitter van Streaming-API's](https://dev.twitter.com/streaming/overview) toocollect tweet gebeurtenissen over een specifieke set van onderwerpen. Hallo-toepassing hello gebruikt [Sentiment140](http://help.sentiment140.com/) open-source hulpprogramma waarmee toegewezen Hallo gevoel waarde tooeach tweet te volgen:

* 0 = negatief
* 2 = neutral
* 4 = positief

Nadat het Hallo tweet gebeurtenissen een gevoel-waarde is toegewezen, zijn ze geduwd toohello event hub die u eerder hebt gemaakt.

Voordat de toepassing hello wordt uitgevoerd, is er bepaalde gegevens van u, zoals Hallo Twitter-sleutels en Hallo event hub-verbindingsreeks. U kunt opgeven dat Hallo configuratie-informatie op de volgende manieren:

* Voer de toepassing hello en gebruik vervolgens van de toepassing hello UI tooenter Hallo sleutels, geheimen en verbindingsreeks. Als u dit doet, Hallo configuratie-informatie wordt gebruikt voor de huidige sessie, maar het is niet opgeslagen.
* Bewerken van de toepassing hello .config-bestand en er set Hallo-waarden. Deze aanpak Hallo configuratie-informatie blijft bestaan, maar het betekent ook dat deze potentieel gevoelige informatie wordt opgeslagen als tekst zonder opmaak op uw computer.

Hallo volgende procedure worden beide benaderingen. 

1. Zorg ervoor dat u hebt gedownload en uitgepakt Hallo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) toepassing, zoals vermeld in het Hallo-vereisten.

2. tooset hello waarden tijdens runtime (en alleen voor de huidige sessie Hallo) uitvoeren Hallo `TwitterWPFClient.exe` toepassing. Wanneer de toepassing hello wordt gevraagd, voert u Hallo volgende waarden:

    * Hallo Twitter consumentsleutel (API-sleutel).
    * Hallo Twitter consumentgeheim (geheim API).
    * Hallo Access Token Twitter.
    * Hallo Access Token geheim Twitter.
    * Hallo verbindingsreeksgegevens die u eerder hebt opgeslagen. Zorg ervoor dat u het Hallo-verbindingsreeks dat u Hallo verwijderd `EntityPath` sleutel-waardepaar uit.
    * Hallo Twitter sleutelwoorden die u wilt dat toodetermine gevoel voor.

   ![TwitterWpfClient toepassing uitgevoerd, worden weergegeven met verborgen instellingen](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. tooset hello waarden permanent, een editor tooopen hello TwitterWpfClient.exe.config tekstbestand gebruiken. Klik dan in Hallo `<appSettings>` element dit doen:

    * Stel `oauth_consumer_key` toohello Twitter consumentsleutel (API-sleutel). 
    * Stel `oauth_consumer_secret` toohello Twitter consumentgeheim (geheim API).
    * Stel `oauth_token` toohello Access Token Twitter.
    * Stel `oauth_token_secret` toohello Access Token geheim Twitter.

    Verderop in Hallo `<appSettings>` element, deze wijzigingen aanbrengen:

    * Stel `EventHubName` naam toohello event hub (dat wil zeggen toohello waarde van Hallo entiteit pad).
    * Stel `EventHubNameConnectionString` toohello-verbindingsreeks. Zorg ervoor dat u het Hallo-verbindingsreeks dat u Hallo verwijderd `EntityPath` sleutel-waardepaar uit.

    Hallo `<appSettings>` sectie eruit Hallo voorbeeld te volgen. (Voor duidelijkheid en beveiliging we sommige regels ingepakt en bepaalde tekens verwijderd.)

    ![TwitterWpfClient toepassingsconfiguratiebestand in een teksteditor Hallo Twitter-sleutels en geheimen en Hallo event hub verbindingsinformatie weergeven](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Als u al Hallo toepassing niet starten, nu TwitterWpfClient.exe uitvoeren. 

5. Klik op Hallo groene knop toocollect sociale gevoel. U ziet Tweet gebeurtenissen met de Hallo **CreatedAt**, **onderwerp**, en **SentimentScore** waarden tooyour event hub worden verzonden.

    ![TwitterWpfClient-toepassing wordt uitgevoerd, met een overzicht van tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Als u fouten ziet en u een stream met tweets weergegeven in de onderste deel Hallo van Hallo-venster niet ziet, Controleer Hallo sleutels en geheimen. Controleer ook de verbindingsreeks hello (Zorg ervoor dat deze geen Hallo bevat `EntityPath` sleutel en waarde.)


## <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken

Nu dat tweet gebeurtenissen streaming in realtime van Twitter, kunt u instellen een Stream Analytics-taak tooanalyze deze gebeurtenissen in realtime.

1. Klik in hello Azure-portal, op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.

2. Naam Hallo taak `socialtwitter-sa-job` en een abonnement, resourcegroep en locatie opgeven.

    Het is een goed idee tooplace Hallo taak en Hallo event hub in Hallo dezelfde regio voor optimale prestaties en doet dat niet u tootransfer gegevens tussen regio's betaalt.

    ![Er wordt een nieuwe Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Klik op **Create**.

    Hallo-taak is gemaakt en Hallo portal geeft taakdetails weer.


## <a name="specify-hello-job-input"></a>Geef Hallo taak voor invoer

1. In de Stream Analytics-taak onder **taak topologie** in Hallo midden van de blade taak hello, klikt u op **invoer**. 

2. In Hallo **invoer** blade, klikt u op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:

    * **Invoeralias**: Gebruik de naam van Hallo `TwitterStream`. Als u een andere naam gebruikt, noteer het omdat u deze later nodig.
    * **Gegevensbrontype**: Selecteer **gegevensstroom**.
    * **Bron**: Selecteer **Event hub**.
    * **Optie importeren**: Selecteer **gebruik event hub uit het huidige abonnement**. 
    * **Service bus-naamruimte**: Selecteer Hallo event hub naamruimte die u eerder hebt gemaakt (`<yourname>-socialtwitter-eh-ns`).
    * **Event hub**: Selecteer Hallo event hub die u eerder hebt gemaakt (`socialtwitter-eh`).
    * **Naam Event hub beleid**: Selecteer Hallo-beleid dat u eerder hebt gemaakt (`socialtwitter-access`).

    ![Nieuwe invoer voor Streaming Analytics-taak maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Klik op **Create**.


## <a name="specify-hello-job-query"></a>Hallo taak query opgeven

Stream Analytics ondersteunt een eenvoudig, declaratief querymodel die transformaties beschrijft. toolearn meer informatie over het Hallo-taal, Zie Hallo [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Deze zelfstudie helpt u bij het ontwerpen en testen van meerdere query's via Twitter-gegevens.

toocompare hello aantal vermeldingen tussen onderwerpen, kunt u een [tumblingvenster](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget Hallo aantal vermeldingen onderwerp elke vijf seconden.

1. Sluit Hallo **invoer** blade als u dat nog niet gedaan hebt.

2. Klik op Hallo taakblade Hallo **Query** vak. Azure bevat Hallo invoer en uitvoer die zijn geconfigureerd voor Hallo taak en kunnen u een query maken die u kunt de invoerstroom Hallo transformeren toohello uitvoer worden verzonden.

3. Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd. 

3. In Hallo **Query** blade, klikt u op Hallo punten volgende toohello `TwitterStream` invoer- en selecteer vervolgens **voorbeeldgegevens uit de invoer**.

    ![Menu Opties toouse voorbeeldgegevens voor Hallo Streaming Analytics-job vermelding met 'Voorbeeldgegevens uit invoer' geselecteerd](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Hiermee opent u een blade die u opgeven hoeveel sample data tooget kunt, gedefinieerd in termen van hoe lang tooread Hallo stream invoeren.

4. Stel **minuten** too3 en klik vervolgens op **OK**. 
    
    ![Opties voor de invoerstroom hello, een steekproef met '3 minuten' geselecteerd.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure 3 minuten aan gegevens uit de invoerstroom Hallo voorbeelden en waarschuwt u als voorbeeldgegevens Hallo gereed is. (Dit duurt even.) 

    Hallo voorbeeldgegevens worden tijdelijk opgeslagen en is beschikbaar tijdens het Hallo-query-venster geopend. Als u Hallo query-venster sluit, Hallo voorbeeldgegevens wordt verwijderd en u een nieuwe set met voorbeeldgegevens toocreate hebt. 

5. Hallo-query in Hallo code-editor toohello volgende wijzigen:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Als niet `TwitterStream` als Hallo alias voor Hallo invoer vervangen door uw alias voor `TwitterStream` in Hallo-query.  

    Deze query gebruikt Hallo **TIMESTAMP BY** sleutelwoord toospecify een tijdstempelveld in Hallo nettolading toobe gebruikt in Hallo tijdelijke berekeningen. Als dit veld niet wordt opgegeven, wordt Hallo windowing bewerking uitgevoerd met behulp van Hallo hoelang elke gebeurtenis is ontvangen op Hallo event hub. Meer informatie in de sectie Hallo 'aankomsttijd tegenover tijd Application' van [Stream Analytics Query verwijzing](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Deze query ook toegang tot krijgt een tijdstempel voor Hallo einde van elke venster met Hallo **System.Timestamp** eigenschap.

5. Klik op **Test**. Hallo-query wordt uitgevoerd tegen Hallo-gegevens die u door actieve.
    
6. Klik op **Opslaan**. Dit bespaart Hallo query als onderdeel van Hallo Streaming Analytics-taak. (Deze kunt Hallo voorbeeldgegevens niet opslaan.)


## <a name="experiment-using-different-fields-from-hello-stream"></a>Experimenteren met verschillende velden van Hallo stream 

Hallo bevat volgende tabel Hallo velden die deel van Hallo streaming JSON-gegevens uitmaken. U kunt gratis tooexperiment in Hallo query-editor.

|JSON-eigenschap | Definitie|
|--- | ---|
|CreatedAt | Hallo-tijd die tweet Hallo is gemaakt|
|Onderwerp | Hallo-onderwerp dat overeenkomt met de Hallo opgegeven trefwoord|
|SentimentScore | Hallo gevoel score uit Sentiment140|
|Auteur | Hallo Twitter-ingang die Hallo tweet wordt verzonden|
|Tekst | Hallo volledige hoofdtekst van Hallo tweet|


## <a name="create-an-output-sink"></a>Uitvoerlocatie maken

U hebt nu een stroom gebeurtenissen, een event hub invoer tooingest gebeurtenissen en een query tooperform een transformatie gedefinieerd via Hallo-stroom. de laatste stap Hallo is toodefine uitvoerlocatie voor Hallo-taak.  

In deze zelfstudie maakt schrijven u Hallo geaggregeerd tweet gebeurtenissen van Hallo taak query tooAzure Blob-opslag.  U kunt ook uw resultaten tooAzure SQL-Database, Azure Table storage, Event Hubs push of, afhankelijk van uw toepassing moet Power BI.

## <a name="specify-hello-job-output"></a>Hallo taakuitvoer opgeven

1. In Hallo **taak topologie** sectie, klikt u op Hallo **uitvoer** vak. 

2. In Hallo **uitvoer** blade, klikt u op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:

    * **Uitvoeraliassen**: Gebruik de naam van Hallo `TwitterStream-Output`. 
    * **Sink**: Selecteer **Blob storage**.
    * **Opties voor het importeren**: Selecteer **gebruik blob storage uit het huidige abonnement**.
    * **Storage-account**. Selecteer **een nieuw opslagaccount maken.**
    * **Storage-account** (tweede vak). Voer `YOURNAMEsa`, waarbij `YOURNAME` uw naam of een andere unieke tekenreeks is. Hallo-naam kan gebruiken die alleen kleine letters en cijfers en deze uniek zijn binnen Azure. 
    * **Container**. Voer `socialtwitter`.
    Hallo opslagaccountnaam- en containernaam zijn gebruikte samen tooprovide een URI voor Hallo blob storage als volgt: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    !['Nieuw uitvoer' blade voor Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Klik op **Create**. 

    Azure storage-account Hallo maakt en genereert een sleutel automatisch. 

5. Sluit Hallo **uitvoer** blade. 


## <a name="start-hello-job"></a>Hallo taak starten

Een taak invoer-, query- en uitvoer zijn opgegeven. U bent klaar toostart Hallo Stream Analytics-taak.

1. Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd. 

2. Klik op Hallo taakblade **Start**.

    ![Hallo Stream Analytics-taak starten](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. In Hallo **starttaak** blade voor **taakuitvoer begintijd**, selecteer **nu** en klik vervolgens op **Start**. 

    ![Blade 'Start de taak' voor Hallo Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure waarschuwt u als Hallo-taak is gestart en Hallo taak blade Hallo status wordt weergegeven als **met**.

    ![Actieve taak](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Uitvoer weergeven voor gevoel analyse

Nadat uw taak eenmaal is gestart en Hallo realtime Twitter-stroom wordt verwerkt, kunt u de uitvoer voor analyse gevoel Hallo kunt weergeven.

U kunt een hulpprogramma zoals [Azure Opslagverkenner](https://http://storageexplorer.com/) of [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview uw taakuitvoerbestand in realtime. Hier kunt u [Power BI](https://powerbi.com/) tooextend uw toepassing tooinclude een aangepaste dashboard, zoals een weergegeven in de volgende schermafbeelding Hallo Hallo:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Maken van een andere query tooidentify trends onderwerpen

Een andere query kunt u toounderstand Twitter-gevoel is gebaseerd op een [Verschuivend venster](https://msdn.microsoft.com/library/azure/dn835051.aspx). tooidentify trends onderwerpen, die u zoeken naar onderwerpen die via een drempelwaarde voor vermeldingen in een opgegeven tijdsduur.

Oog op Hallo van deze zelfstudie wordt zoeken u naar onderwerpen die worden vermeld meer dan 20 keer in Hallo laatste 5 seconden.

1. Klik op Hallo taakblade **stoppen** toostop Hallo taak. 

2. In Hallo **taak topologie** sectie, klikt u op Hallo **Query** vak. 

3. Hallo query toohello volgende wijzigen:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Klik op **Opslaan**.

5. Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd. 

6. Klik op **Start** toorestart Hallo taak met de nieuwe query Hallo.


## <a name="get-support"></a>Ondersteuning krijgen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
