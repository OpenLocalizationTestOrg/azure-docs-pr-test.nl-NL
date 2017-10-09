---
title: aaaBuild een IoT-oplossing met behulp van de Stream Analytics | Microsoft Docs
description: Zelfstudie voor Hallo Stream Analytics IoT-oplossing van een scenario tolhuisje aan de slag
keywords: IOT-oplossing, vensterfuncties
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Een IoT-oplossing bouwen met behulp van de Stream Analytics
## <a name="introduction"></a>Inleiding
In deze zelfstudie leert u hoe toouse Azure Stream Analytics tooget realtime inzicht in uw gegevens. Ontwikkelaars kunnen eenvoudig gegevensstromen, zoals Klik streams logboeken en gebeurtenissen die door de apparaten worden gegenereerd met historische records of verwijzing gegevens tooderive zakelijke inzichten combineren. Als een volledig beheerde, realtime stroom berekening service die wordt gehost in Microsoft Azure, biedt Azure Stream Analytics ingebouwde tolerantie, lage latentie en schaalbaarheid tooget u up en wordt uitgevoerd in minuten.

Na het voltooien van deze zelfstudie, kunt u zich kunt:

* Maak uzelf bekend met hello Azure Stream Analytics-portal.
* Configureren en implementeren van een streaming-taak.
* Bewoordingen aan echte problemen en ze op te lossen met behulp van Hallo Stream Analytics query language.
* Ontwikkel streaming van oplossingen voor uw klanten met behulp van de Stream Analytics met vertrouwen.
* Gebruik hello controle en logboekregistratie ervaring tootroubleshoot problemen.

## <a name="prerequisites"></a>Vereisten
U wordt moet Hallo na vereisten toocomplete in deze zelfstudie:

* meest recente versie van Hallo [Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017 2015 of Hallo gratis [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* Een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/)
* Administratorbevoegdheden op Hallo-computer
* Het downloaden van de [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) van Hallo Microsoft Download Center
* Optioneel: De broncode voor Hallo TollApp gebeurtenis generator in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Scenario Inleiding: "Hallo, Tolstation!"
Een station tolstation is een algemene verschijnsel. Tijdens deze veel autowegen bruggen en tunnels tussen Hallo wereld. Elk station tolstation heeft meerdere tolstation stands. Bij handmatige stands stoppen u toopay hello tolstation tooan daarmee gepaard gaande. Een sensor boven op elke stand scant op geautomatiseerde stands een RFID-kaart is aangebrachte toohello voorruit van uw vehicle verwerkt als u Hallo tolstation stand doorgeven. Het is gemakkelijk toovisualize Hallo passage door middel van deze stations tolstation als een stroom gebeurtenissen waarover interessante bewerkingen kunnen worden uitgevoerd.

![Afbeelding van auto's op een tolstation stands](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Binnenkomende gegevens
Deze zelfstudie werkt met twee streams gegevens. Sensoren in Hallo-ingang is geïnstalleerd en afsluiten van Hallo tolstation stations produceren Hallo eerste stroom. tweede Hallo-stroom is een statische lookup gegevensset die vehicle registratiegegevens heeft.

### <a name="entry-data-stream"></a>Gegevensstroom van vermelding
gegevensstroom Hallo-vermelding bevat informatie over auto's wanneer deze stations tolstation binnengaat.

| TollID | EntryTime | LicensePlate | Status | Maken | Model | VehicleType | VehicleWeight | Gratis | Label |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |7001 JNB |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |1007 BNJ |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4 x 4 |1 |0 |6 |321987654 |

Hier volgt een korte beschrijving van Hallo kolommen:

| Kolom | Beschrijving |
| --- | --- |
| TollID |Hallo tolstation stand-ID die een unieke identificatie van een stand tolstation |
| EntryTime |Hallo-datum en tijd van de vermelding van het Hallo vehicle toohello tolstation stand in UTC |
| LicensePlate |Hallo sofi-nummer van Hallo vehicle |
| Status |Een status in de Verenigde Staten |
| Maken |Hallo fabrikant van Hallo auto |
| Model |Hallo modelnummer van Hallo auto |
| VehicleType |1 voor passagiers voertuigen of 2 voor commerciële voertuigen |
| WeightType |Toegestaan gewicht in ton; 0 voor passagiers voertuigen |
| Gratis |Hallo tolstation waarde in USD |
| Label |Hallo e-tags op Hallo auto die betaling automatiseert. lege waar Hallo betaling handmatig is uitgevoerd |

### <a name="exit-data-stream"></a>De gegevensstroom afsluiten
Hallo afsluiten gegevensstroom bevat informatie over auto's Hallo tolstation station verlaten.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |7001 JNB |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |1007 BNJ |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Hier volgt een korte beschrijving van Hallo kolommen:

| Kolom | Beschrijving |
| --- | --- |
| TollID |Hallo tolstation stand-ID die een unieke identificatie van een stand tolstation |
| ExitTime |Hallo-datum en tijd van af te sluiten van Hallo vehicle van tolstation stand in UTC |
| LicensePlate |Hallo sofi-nummer van Hallo vehicle |

### <a name="commercial-vehicle-registration-data"></a>De registratiegegevens commerciële vehicle
Hallo-zelfstudie maakt gebruik van een momentopname van een registratiedatabase commerciële vehicle verwerkt.

| LicensePlate | Registratie-id | Verlopen |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| 1005 BACK |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Hier volgt een korte beschrijving van Hallo kolommen:

| Kolom | Beschrijving |
| --- | --- |
| LicensePlate |Hallo sofi-nummer van Hallo vehicle |
| Registratie-id |Hallo vehicle van registratie-ID |
| Verlopen |de registratiestatus van Hallo vehicle Hallo: 0 of vehicle registratie actief is, is 1 als de registratie is verlopen |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Hallo-omgeving instellen voor Azure Stream Analytics
toocomplete in deze zelfstudie hebt u een Microsoft Azure-abonnement nodig. Microsoft biedt een gratis proefversie van Microsoft Azure-services.

Als u geen Azure-account hebt, kunt u [aanvragen van een gratis evaluatieversie](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign voor een gratis proefversie, moet u een mobiel apparaat dat u kunt tekstberichten en een geldige creditcard ontvangen.
> 
> 

Zorg ervoor dat toofollow Hallo stappen in 'Opschonen van uw Azure-account' Hallo-sectie op Hallo einde van dit artikel, zodat u optimaal gebruik van uw Azure-krediet Hallo kunt maken.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Vereist voor de zelfstudie hello Azure-resources inrichten
Deze zelfstudie vereist twee event hubs tooreceive *vermelding* en *sluiten* gegevensstromen. Azure SQL Database worden de resultaten Hallo van Hallo Stream Analytics-taken. Azure Storage worden opgeslagen referentiegegevens over vehicle registraties.

U kunt gebruiken Hallo Setup.ps1 script in Hallo TollApp map op GitHub toocreate alle vereiste resources. In Hallo belang van de tijd, is het raadzaam dat u het uitvoert. Als u wilt meer informatie over hoe tooconfigure deze bronnen in hello Azure-portal verwijzen toolearn toohello 'Zelfstudie resources in Azure-portal configureren' bijlage.

Download en sla Hallo ondersteunende [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) map en bestanden.

Open een **Microsoft Azure PowerShell** venster *als beheerder*. Als u nog geen Azure PowerShell, volgt u de instructies Hallo in [installeren en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall deze.

Omdat Windows wordt automatisch geblokkeerd .ps1-, dll- en .exe-bestanden, moet u tooset Hallo uitvoeringsbeleid voordat u Hallo-script uitvoeren. Zorg ervoor dat hello Azure PowerShell-venster wordt uitgevoerd *als beheerder*. Voer **Set-ExecutionPolicy unrestricted**. Wanneer u wordt gevraagd, typt u **Y**.

![Schermopname van 'Set-ExecutionPolicy unrestricted' uitgevoerd in Azure PowerShell-venster](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Voer **Get-ExecutionPolicy** toomake ervoor dat de opdracht Hallo gewerkt.

![Schermopname van 'Get-ExecutionPolicy' uitgevoerd in Azure PowerShell-venster](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Ga toohello-map met Hallo scripts en generator-toepassing.

![Schermopname van 'cd .\TollApp\TollApp' in hello Azure PowerShell-venster](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Type **.\\ Setup.ps1** tooset van uw Azure-account maken en alle vereiste bronnen configureren en starten toogenerate gebeurtenissen. Hallo script willekeurig neemt over een toocreate regio uw resources. een regio tooexplicitly opgeven, kunt u Hallo doorgeven **-locatie** parameter zoals Hallo volgt in:

**. \\Setup.ps1-locatie 'VS-midden'**

![Schermafbeelding van pagina hello Azure aanmelden](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

Hallo-script wordt geopend Hallo **aanmelden** pagina voor Microsoft Azure. Voer de referenties van uw account.

> [!NOTE]
> Als uw account toegang toomultiple abonnementen heeft, kunt u zich gestelde tooenter Hallo abonnementsnaam wilt u toouse voor Hallo zelfstudie.
> 
> 

Hallo-script kan toorun van enkele minuten duren. Nadat deze is voltooid, worden Hallo uitvoer moet eruitzien als Hallo volgende schermopname.

![Schermopname van het resultaat van het Hallo-script van hello Azure PowerShell-venster](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

U ziet ook een ander venster die vergelijkbaar toohello volgende schermopname. Deze toepassing is het verzenden van gebeurtenissen tooAzure Event Hubs, die is vereist toorun Hallo zelfstudie. Dus geen stop de toepassing hello of dit venster sluiten totdat u klaar bent met het Hallo-zelfstudie.

![Schermopname van 'Verzenden event hub gegevens'](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

U moet kunnen toosee uw resources in Azure-portal nu. Ga te<https://portal.azure.com>, en meld u aan met referenties van uw account. Houd er rekening mee dat momenteel bepaalde functionaliteit maakt gebruik van de klassieke portal Hallo. Deze stappen worden duidelijk vermeld.

### <a name="azure-event-hubs"></a>Azure Event Hubs
Klik in hello Azure-portal, op **meer services** op Hallo Hallo management linker deelvenster onderaan. Type **Event hubs** in Hallo veld en klikt u op **Event hubs**. Hiermee wordt een nieuwe browser venster toodisplay Hallo gestart **SERVICE BUS** gebied in Hallo **klassieke portal**. Hier ziet u Hallo Event Hub is gemaakt door Hallo Setup.ps1 script.

![Service Bus](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Klik op Hallo die met begint *tolldata*. Klik op Hallo **EVENT HUBS** tabblad. Ziet u twee event hubs met de naam *vermelding* en *sluiten* gemaakt in deze naamruimte.

![Event Hubs-tabblad in de klassieke portal Hallo](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Azure Storage-container
1. Ga terug toohello tabblad in uw browser openen tooAzure-portal. Klik op **opslag** op de linkerkant van hello Azure portal toosee hello Azure Storage-container die wordt gebruikt in de zelfstudie Hallo Hallo.
   
    ![Opslag menu-item](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Klik op Hallo die beginnen met *tolldata*. Klik op Hallo **CONTAINERS** tabblad toosee Hallo gemaakt container.
   
    ![Tabblad containers in hello Azure-portal](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Klik op Hallo **tolldata** container toosee Hallo JSON-bestand met de registratiegegevens vehicle geüpload.
   
    ![Schermopname van Hallo registration.json bestand in container Hallo](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Azure SQL Database
1. Ga terug toohello Azure-portal op Hallo eerste tabblad dat in de browser Hallo is geopend. Klik op **SQL-DATABASES** op Hallo linkerkant van hello Azure portal toosee Hallo SQL-database die wordt gebruikt in de zelfstudie Hallo en klikt u op **tolldatadb**.
   
    ![Schermopname van Hallo SQL-database gemaakt](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Het Hallo-servernaam kopiëren zonder Hallo-poortnummer (*servername*. database.windows.net bijvoorbeeld).
    ![Schermopname van Hallo SQL database-database gemaakt](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Verbinding maken met toohello database vanuit Visual Studio
Gebruik Visual Studio tooaccess queryresultaten in Hallo Uitvoerdatabase.

Verbinding maken met toohello SQL-database (Hallo doel) vanuit Visual Studio:

1. Open Visual Studio en klik vervolgens op **extra** > **tooDatabase verbinding**.
2. Als u wordt gevraagd, klikt u op **Microsoft SQL Server** als gegevensbron.
   
    ![Het dialoogvenster gegevensbron wijzigen](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. In Hallo **servernaam** veld, plak Hallo-naam die u hebt gekopieerd in de vorige sectie Hallo uit hello Azure-portal (dat wil zeggen, *servername*. database.windows.net).
4. Klik op **SQL Server-verificatie gebruiken**.
5. Voer **tolladmin** in Hallo **gebruikersnaam** veld en **123toll!** in Hallo **wachtwoord** veld.
6. Klik op **Selecteer of voer een databasenaam**, en selecteer **TollDataDB** als Hallo-database.
   
    ![Het dialoogvenster verbinding toevoegen](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Klik op **OK**.
8. Open in Server Explorer.
   
    ![Server Explorer](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Zie vier tabellen in Hallo TollDataDB database.
   
    ![Tabellen in Hallo TollDataDB database](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Gebeurtenis generator: TollApp-voorbeeldproject
Hallo PowerShell-script wordt automatisch toosend gebeurtenissen met behulp van Hallo TollApp voorbeeldprogramma toepassing wordt gestart. U hoeft niet tooperform eventuele extra stappen.

Als u geïnteresseerd in de implementatiegegevens bent, kunt u de broncode Hallo Hallo TollApp toepassing vinden in GitHub [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Schermopname van voorbeeldcode weergegeven in Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken
1. In hello Azure-portal, klikt u op Hallo groen plusteken in Hallo linkerbovenhoek van Hallo pagina toocreate nieuwe Stream Analytics-taak. Selecteer **Intelligence en analyse** en klik vervolgens op **Stream Analytics-taak**.
   
    ![Knop Nieuw](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Geef de taaknaam van een, het valideren van Hallo abonnement juist is en maak vervolgens een nieuwe resourcegroep in Hallo dezelfde regio bevinden als Hallo Event hub-opslag (is standaard Zuid-centraal VS voor Hallo script).
3. Klik op **pincode toodashboard** en vervolgens **maken** Hallo Hallo pagina onderaan in.
   
    ![Optie voor Stream Analytics-taak maken](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Invoerbronnen definiëren
1. Hallo-taak wordt gemaakt en geopend Hallo taak pagina. U kunt ook op Hallo analytics-taak gemaakt op Hallo-portaldashboard.

2. Klik op Hallo **invoer** toodefine Hallo brongegevens tabblad.
   
    ![Hallo invoer tabblad](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Klik op **invoer toevoegen**.
   
    ![Hallo een invoer-optie toevoegen](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Voer **EntryStream** als **INVOERALIAS**.
5. Brontype is **gegevensstroom**
6. Bron is **Event hub**.
7. **Service bus-naamruimte** moet Hallo TollData in Hallo vervolgkeuzelijst.
8. **Naam Event hub** te moet worden ingesteld**vermelding**.
9. **Naam Event hub beleid*is **RootManageSharedAccessKey** (Hallo standaardwaarde).
10. Selecteer **JSON** voor **GEBEURTENIS SERIALISATIE-indeling** en **UTF8** voor **codering**.
   
    Uw instellingen, ziet er als:
   
    ![Event hub-instellingen](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Klik op **maken** Hallo Hallo pagina toofinish Hallo wizard onderaan in.
    
    Nu dat u Hallo vermelding stroom hebt gemaakt, wordt u Hallo volgt dezelfde stappen toocreate Hallo afsluiten stream. Ervoor tooenter waarden zijn als op de volgende schermafbeelding Hallo.
    
    ![Instellingen voor Hallo afsluiten stroom](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    U hebt twee invoer streams gedefinieerd:
    
    ![Invoer streams gedefinieerd in hello Azure-portal](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Vervolgens voegt u de gegevensinvoer verwijzing voor Hallo blob-bestand met de registratiegegevens auto.
11. Klik op **toevoegen**, en volg Hallo hetzelfde proces voor Hallo stroom invoer maar selecteren **REFERENTIEGEGEVENS** in plaats van **gegevensstroom** en Hallo **invoer Alias**  is **registratie**.

12. Storage-account die met begint **tolldata**. Hallo-containernaam moet **tolldata**, en Hallo **pad PATROON** moet **registration.json**. Deze naam is hoofdlettergevoelig en moet **kleine**.
    
    ![Instellingen voor de opslag blog](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Klik op **maken** toofinish Hallo-wizard.

Nu worden alle invoer gedefinieerd.

## <a name="define-output"></a>Uitvoer definiëren
1. Selecteer op Hallo Stream Analytics-taak overzichtsvenster **uitvoer**.
   
    ![tabblad uitvoer en de optie 'Add uitvoer' Hallo](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Klik op **Add**.
3. Set Hallo **uitvoeraliassen** too'output' en vervolgens **Sink** te**SQL-database**.
3. Selecteer Hallo-servernaam die is gebruikt in Hallo 'Connect tooDatabase vanuit Visual Studio' sectie Hallo artikel. Hallo-databasenaam is **TollDataDB**.
4. Voer **tolladmin** in Hallo **gebruikersnaam** veld **123toll!** in Hallo **wachtwoord** veld en **TollDataRefJoin** in Hallo **tabel** veld.
   
    ![SQL Database-instellingen](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Klik op **Create**.

## <a name="azure-stream-analytics-query"></a>Azure Stream analytics query
Hallo **QUERY** tabblad bevat een SQL-query of transformaties Hallo binnenkomende gegevens.

![Een query toohello Query tabblad toegevoegd](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Deze zelfstudie probeert verschillende bedrijfsvragen die zijn gerelateerd tootoll gegevens en constructies Stream Analytics query's die kunnen worden gebruikt in Azure Stream Analytics tooprovide tooanswer geen relevant antwoord.

Voordat u uw eerste Stream Analytics-taak, gaan we enkele scenario's en Hallo-querysyntaxis verkennen.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Inleiding tooAzure querytaal van Stream Analytics
- - -
Stel dat u nodig hebt toocount Hallo aantal voertuigen dat een tolstation stand invoeren. Omdat dit een continue stroom van gebeurtenissen, hebt u toodefine een 'periode van tijd." Laten we wijzigen Hallo vraag toobe 'hoeveel voertuigen Geef een tolstation stand elke drie minuten?'. Dit is meestal waarnaar wordt verwezen tooas hello tumbling count.

Bekijk hello Azure Stream Analytics query waarmee deze vraag worden beantwoord:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Zoals u ziet, Azure Stream Analytics maakt gebruik van een querytaal die lijkt op SQL en enkele extensies toospecify tijd gerelateerde aspecten van Hallo query toegevoegd.

Lees voor meer informatie over [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructies die worden gebruikt in query Hallo van MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Azure Stream Analytics query's testen
Nu u uw eerste Azure Stream Analytics query hebt geschreven, is het tijd tootest deze met behulp van bestanden met voorbeeldgegevens in de map TollApp van Hallo pad bevindt:

**.. \\TollApp\\TollApp\\gegevens**

Deze map bevat de volgende bestanden Hallo:

* Entry.JSON
* Exit.JSON
* Registration.JSON

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Vraag 1: Het aantal voertuigen een tolstation stand
1. Open hello Azure-portal en ga tooyour gemaakt Azure Stream Analytics-taak. Klik op Hallo **QUERY** tabblad en plak de query uit de vorige sectie Hallo.

2. toovalidate deze query op de voorbeeldgegevens, Hallo uploadgegevens in Hallo EntryStream invoer door te klikken op Hallo... symbool en het selecteren van **voorbeeldgegevens uit bestand uploaden**.

    ![Schermopname van Hallo Entry.json bestand](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. In Hallo deelvenster verschijnt Selecteer Hallo-bestand (Entry.json) op uw lokale computer en klik op **OK**. Hallo **Test** pictogram wordt nu verlichten en worden geklikt.
   
    ![Schermopname van Hallo Entry.json bestand](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Valideren dat Hallo-uitvoer van Hallo-query is zoals verwacht:
   
    ![Resultaten van Hallo-test](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Vraag 2: De totale tijd voor elke toopass auto via Hallo tolstation stand rapporteren
Hallo gemiddelde tijd die zijn voor een auto-toopass via Hallo tolstation vereist helpt tooassess Hallo efficiëntie van het Hallo-proces en Hallo klantervaring.

totale tijd toofind hello, moet u toojoin hello EntryTime stream met Hallo ExitTime-stroom. U doet u mee aan Hallo stromen voor TollId en LicencePlate kolommen. Hallo **JOIN** operator moet u tijdelijke eenheidsprofiel toospecify die beschrijft Hallo aanvaardbare tijd verschil tussen Hallo die lid zijn van gebeurtenissen. U gaat gebruiken **DATEDIFF** toospecify gebeurtenissen moet langer zijn dan 15 minuten van elkaar werken. U wordt ook van toepassing hello **DATEDIFF** functie tooexit en vermelding tijden toocompute Hallo werkelijke tijd waarop een auto in Hallo doorbrengt tolbruggen station. Houd er rekening mee Hallo verschil van het gebruik van Hallo **DATEDIFF** wanneer het wordt gebruikt in een **Selecteer** instructie in plaats van een **JOIN** voorwaarde.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest deze query, update Hallo-query op Hallo **QUERY** voor Hallo-taak. Hallo-testbestand voor toevoegen **ExitStream** net als bij **EntryStream** hierboven is opgegeven.
   
2. Klik op **Test**.

3. Selecteer Hallo selectievakje tootest Hallo query en bekijkt hello uitvoer:
   
    ![Uitvoer van Hallo-test](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Vraag 3: Alle commerciële voertuigen met verlopen registratie rapporteren
Azure Stream Analytics kunt statische momentopnamen van gegevens toojoin met tijdelijke gegevensstromen gebruiken. toodemonstrate deze mogelijkheid, gebruik Hallo Voorbeeldvraag te volgen.

Als een commerciële-medium is geregistreerd bij Hallo tolstation bedrijf, kan het Hallo tolstation stand passeren zonder te zijn gestopt voor inspectie. Gebruikt u registratie commerciële Vehicle lookup table tooidentify alle commerciële voertuigen die registraties zijn verlopen.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

een query met behulp van referentiegegevens tootest, moet u een invoerbron toodefine voor Hallo verwijzingsgegevens, die u al hebt gedaan.

tootest deze query plakken Hallo query in Hallo **QUERY** tabblad **Test**, en geef Hallo twee invoerbronnen en Hallo registratie voorbeeldgegevens en klikt u op **Test**.  
   
![Uitvoer van Hallo-test](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Hallo Stream Analytics-taak starten
Nu is het tijd toofinish Hallo configuratie en start Hallo taak. Hallo query opslaan van de vraag 3, die wordt uitvoer dat overeenkomt met schema Hallo Hallo produceren **TollDataRefJoin** uitvoertabel.

Ga toohello taak **DASHBOARD**, en klik op **START**.

![Schermafbeelding van de startknop Hallo in Hallo taak dashboard](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Hallo in het dialoogvenster dat wordt geopend wijzigen Hallo **START uitvoer** tijd te**aangepaste tijd**. Hallo uur tooone uur vóór de huidige tijd Hallo wijzigen. Deze wijziging zorgt ervoor dat alle gebeurtenissen van Hallo event hub worden verwerkt sinds het begin van toogenerate Hallo gebeurtenissen aan begin van de zelfstudie Hallo Hallo. Klik nu op Hallo **Start** knop toostart Hallo taak.

![Selectie van aangepaste tijd](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Taak starten Hallo kan enkele minuten duren. U ziet op het hoogste niveau pagina Hallo Hallo status voor Stream Analytics.

![Schermafbeelding van de status van taak Hallo Hallo](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Controleer de resultaten in Visual Studio
1. Open Visual Studio Server Explorer en met de rechtermuisknop op Hallo **TollDataRefJoin** tabel.
2. Klik op **tabelgegevens weergeven** toosee Hallo uitvoer van de taak.
   
    ![Selectie van 'Tabelgegevens weergeven' in Server Explorer](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Azure Stream Analytics uitbreiden met taken
Azure Stream Analytics is ontworpen tooelastically schalen zodat deze kan grote hoeveelheden gegevens verwerken. Hello Azure Stream Analytics query kunt gebruiken een **PARTITION BY** component tootell Hallo systeem dat in deze stap wordt uitgebreid. **PartitionId** is een speciale kolom die het systeem Hallo toomatch Hallo partitie-ID van Hallo-invoer (event hub) wordt toegevoegd.

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Hallo huidige taak stoppen, update Hallo-query in Hallo **QUERY** tabblad en open Hallo **instellingen** stemmen in Hallo taak dashboard. Klik op **Scale**.
   
    **STREAMING-eenheden** definiëren Hallo hoeveelheid rekenkracht die taak Hallo kan ontvangen.
2. Wijziging Hallo voor vervolgkeuzelijst van 1 6.
   
    ![Schermopname van het selecteren van 6 streaming-eenheden](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Ga toohello **uitvoer** tabblad en Hallo-naam van de SQL-tabel hello te wijzigen**TollDataTumblingCountPartitioned**.

Als u Hallo taak start nu kunt Azure Stream Analytics werk verdelen over meer computerresources en een betere doorvoer behalen. Houd er rekening mee dat Hallo TollApp toepassing ook gebeurtenissen gepartitioneerd door TollId verzendt.

## <a name="monitor"></a>Bewaken
Hallo **MONITOR** gebied bevat statistieken over Hallo taak uitgevoerd. Eerste keer dat de configuratie is vereist toouse Hallo storage-account in Hallo dezelfde regio (naam tolstation zoals Hallo rest van dit document).   

![Schermopname van monitor](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

U hebt toegang tot **activiteitenlogboeken** vanuit Hallo taak dashboard **instellingen** ook gebied.


## <a name="conclusion"></a>Conclusie
Deze zelfstudie geïntroduceerd toohello Azure Stream Analytics-service. Deze gedemonstreerd hoe Hallo tooconfigure invoer en uitvoer voor Stream Analytics-taak. Met behulp van Hallo Tolstation gegevens scenario Hallo zelfstudie voorkomende problemen die ontstaan in de ruimte Hallo van gegevens in beweging en hoe ze kunnen worden opgelost met eenvoudige SQL-achtige query's in Azure Stream Analytics uitgelegd. Hallo-zelfstudie beschreven SQL extensie constructs voor het werken met tijdelijke gegevens. Deze hebt u geleerd hoe toojoin gegevensstromen, hoe tooenrich Hallo gegevensstroom met statische referentiegegevens en hoe tooscale uit een query tooachieve hogere doorvoer.

Hoewel deze zelfstudie een goede inleiding biedt, is het niet voltooid door middel van. U vindt meer querypatronen met Hallo SAQL taal op [voorbeelden voor het algemene gebruikspatronen van de Stream Analytics Query](stream-analytics-stream-analytics-query-patterns.md).
Raadpleeg toohello [onlinedocumentatie](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn meer informatie over Azure Stream Analytics.

## <a name="clean-up-your-azure-account"></a>Opschonen van uw Azure-account
1. Stop Hallo Stream Analytics-taak in hello Azure-portal.
   
    Hallo Setup.ps1 script maakt twee event hubs en een SQL-database. Hallo instructies help die resources achter Hallo Hallo-zelfstudie opschonen te volgen.
2. Typ in een PowerShell-venster **.\\ CleanUp.ps1** toostart Hallo script waarmee bronnen die worden gebruikt in de zelfstudie Hallo worden verwijderd.
   
   > [!NOTE]
   > Resources worden aangeduid met de naam van de Hallo. Zorg ervoor dat u elk item zorgvuldig controleren vóór de verwijdering te bevestigen.
   > 
   > 


