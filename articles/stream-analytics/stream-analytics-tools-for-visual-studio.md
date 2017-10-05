---
title: Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken | Microsoft Docs
description: Zelfstudie voor de Azure Stream Analytics-Tools voor Visual Studio aan de slag
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken
## <a name="introduction"></a>Inleiding
In deze zelfstudie leert u hoe u met Azure Stream Analytics-Tools voor Visual Studio maken, ontwerpen, lokaal testen, beheren en fouten opsporen in uw Stream Analytics-taken. 

Na het voltooien van deze zelfstudie, kunt u zich kunt:
* Tijd om uzelf bekend met Stream Analytics-hulpprogramma's voor Visual Studio.
* Configureren en implementeren van een Stream Analytics-taak.
* Test uw taak lokaal met lokale voorbeeldgegevens.
* Gebruik controle met het oplossen van problemen.
* Bestaande taken exporteren naar projecten.

## <a name="prerequisites"></a>Vereisten
Voor het voltooien van deze zelfstudie moet aan de volgende vereisten worden voldaan:
* Voltooi de stappen die worden voorafgegaan door 'Een Stream Analytics-taak maken' de [een IoT-oplossing bouwen met behulp van de Stream Analytics-zelfstudie](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Gebruik Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012. Enterprise (Ultimate/Premium), Professional en Community-edities worden ondersteund. Express edition wordt niet ondersteund. Visual Studio 2017 wordt niet ondersteund. 
* Gebruik de Azure SDK voor .NET versie 2.7.1 of hoger. U kunt dit installeren met het [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).
* Installeer de [Stream Analytics-hulpprogramma's voor Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Een Stream Analytics-project maken
1. Klik in Visual Studio de **bestand** menu en selecteer **nieuw Project**. 

2. Selecteer in de lijst met sjablonen aan de linkerkant **Stream Analytics** en klik vervolgens op **Azure Stream Analytics toepassing**.

3. Voer het project **naam**, **locatie**, en **oplossingsnaam** als voor andere projecten.

    ![Nieuw Project-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Een **Tolstation** project is gegenereerd op **Solution Explorer**.

    ![Tolstation project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a>Kies het juiste abonnement
1. Klik in Visual Studio de **weergave** menu en open **Server Explorer**.

2. Meld u aan met uw Azure-Account. 

## <a name="define-the-input-sources"></a>De invoerbronnen definiëren
1.  In **Solution Explorer**, vouw de **invoer** knooppunt en wijzig de naam **Input.json** naar **EntryStream.json**. Dubbelklik op **EntryStream.json**.
2.  De **invoer Alias** is nu **EntryStream**. De ingevoerde alias is in het query-script gebruikt. 
3.  In **brontype**, selecteer **gegevensstroom**.
4.  In **bron**, selecteer **Event Hub**.
5.  In **Service Bus Namespace**, selecteer de **TollData** optie.
6.  In **naam Event Hub**, selecteer **vermelding**.
7.  In **Event Hub-beleidsnaam**, selecteer **RootManageSharedAccessKey** (de standaardwaarde).
8.  In **gebeurtenis serialisatie-indeling**, selecteer **Json**. 
9.  In **codering**, selecteer **UTF8**. Uw instellingen moeten eruitzien als in de volgende schermafbeelding:

    ![Invoer-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Klik op om de wizard **opslaan**. U kunt nu een andere invoer bron voor het maken van de stroom afsluiten toevoegen. Met de rechtermuisknop op de **invoer** uit en selecteer **Nieuw Item**.

    ![Nieuw Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Selecteer in het venster **Azure Stream Analytics invoer**, en wijzig de **naam** naar **ExitStream.json**. Klik op **Add**.

    ![Venster Nieuw Item toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Dubbelklik op **ExitStream.json** in het project en volg dezelfde stappen als u voor de post-stroom heeft. Voer **sluiten** voor de **naam Event Hub** zoals weergegeven in de volgende schermafbeelding:

    ![ExitStream venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    U hebt nu twee invoer streams gedefinieerd:

    ![Toegang naar en uitgang invoer stromen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Voeg vervolgens de gegevensinvoer verwijzing voor het blob-bestand dat de registratiegegevens auto bevat.

13. Met de rechtermuisknop op de **invoer** knooppunt in het project en volg dezelfde stappen als bij de invoer van de stroom. In **invoer Alias**, voer **registratie**, en in **brontype**, selecteer **referentiegegevens**.

    ![Registratie-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. In **Opslagaccount**, selecteer de **tolldata** optie. In **Container**, selecteer **tolldata**, en in **pad patroon**, voer **registration.json**. Deze naam is hoofdlettergevoelig en moet in kleine letters.
15. Klik op om de wizard **opslaan**.

Nu zijn de invoer gedefinieerd.

## <a name="define-the-output"></a>De uitvoer definiëren
1.  In **Solution Explorer**, vouw de **invoer** knooppunt en dubbelklik op **Output.json**.

2.  In **Uitvoeraliassen**, voer **uitvoer**. 
3.  In **Sink**, selecteer **SQL-Database**.
4.  In **Database**, selecteer **TollDataDB**.
5.  In **gebruikersnaam**, voer **tolladmin**. 
6.  In **wachtwoord**, voer **123toll!**.
7.  In **tabel**, voer **TollDataRefJoin**.
8.  Klik op **Opslaan**.

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Een Stream Analytics query maken
Deze zelfstudie probeert verschillende bedrijven vragen die zijn gerelateerd aan gegevens tolbruggen te beantwoorden. Dit wordt ook Stream Analytics query's die kunnen worden gebruikt in de Stream Analytics relevante beantwoorden.
Voordat u uw eerste Stream Analytics-taak, gaan we een eenvoudig scenario en de querysyntaxis verkennen.

### <a name="introduction-to-the-stream-analytics-query-language"></a>Inleiding tot de Stream Analytics query language
Stel dat u moet het aantal voertuigen die een tolstation stand invoeren. Omdat dit voorbeeld een continue stroom van gebeurtenissen is, hebt u voor het definiëren van een bepaalde periode. Wijzig de vraag om 'hoeveel voertuigen Geef een tolstation stand elke drie minuten?' Deze manier om gegevens te tellen wordt vaak aangeduid als het aantal daling.

Bekijk de Stream Analytics query waarmee deze vraag worden beantwoord:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Stream Analytics maakt gebruik van een querytaal die lijkt op SQL en enkele uitbreidingen om op te geven tijd gerelateerde aspecten van de query toegevoegd.

Zie voor meer informatie [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructies die worden gebruikt in de query van MSDN.

Nu u uw eerste Stream Analytics query hebt geschreven, is het tijd om deze te testen. Gebruik de bestanden met voorbeeldgegevens zich in de map TollApp in het volgende pad:

.. \TollApp\TollApp\Data

Deze map bevat de volgende bestanden:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a>Het aantal voertuigen een tolstation stand tellen
Dubbelklik in het project op **Script.asaql** openen van het script in de **Query-Editor**. Kopieer en plak het script in de vorige sectie in de editor. De Query-Editor biedt ondersteuning voor IntelliSense syntaxiskleuren en de markering van de fout.

![Query-Editor](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Stream Analytics query's lokaal testen

1. Compileren van de query om te zien of er een syntaxisfout, met de rechtermuisknop op het project en selecteer **bouwen**. 

2. Voor het valideren van deze query op de voorbeeldgegevens, kunt u lokale voorbeeldgegevens. Met de rechtermuisknop op de invoer en selecteer **lokale invoer toevoegen**.

    ![Lokale invoer toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Selecteer de voorbeeldgegevens van uw lokale pad in het pop-upvenster. Klik op **Opslaan**.

    ![Lokale invoer venster toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Een bestand met de naam **local_EntryStream.json** wordt automatisch toegevoegd aan de map van uw invoer.

    ![Bestand toegevoegd aan de map invoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. In de **Query-Editor**, klikt u op **lokaal uitvoeren**. Of u kunt ook op F5 drukken.

    ![Lokaal uitvoeren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Lokaal uitvoeren van uitvoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Druk op een willekeurige toets om weer te geven van de uitvoer in de **ASA lokale uitvoeren resultaat** venster in Visual Studio. 

    ![Venster ASA lokale uitvoeren resultaat](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Klik op **geopende resultaat map** om te controleren van de uitvoerbestanden beide in CSV en JSON-indeling.

    ![Open resultaat map uitvoer](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a>Voorbeeld van de invoergegevens
U kunt ook invoer voorbeeldgegevens uit invoerbronnen naar een lokaal bestand. 
1. Met de rechtermuisknop op het configuratiebestand van de invoer en selecteer **voorbeeldgegevens**. 

   ![Voorbeeldgegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    U kunt alleen de event hub of -IoT-hub steekproef nemen nu. Andere bronnen worden niet ondersteund.

2. Geef het lokale pad gebruikt voor het opslaan van de voorbeeldgegevens in het pop-upvenster. Klik op **voorbeeld**.

    ![Venster van de gegevens voorbeeld](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    U ziet de voortgang in de **uitvoer** venster. 

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a>Verzenden van een Stream Analytics-query naar Azure
1. In de **Query-Editor**, klikt u op **verzenden naar Azure** in de scripteditor.

    ![Verzenden naar Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Selecteer **maken van een nieuwe Azure Stream Analytics-taak**. Voer de **taaknaam**, en selecteer de juiste **abonnement**. Klik op **indienen**.

    ![Venster van de taak verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Een taak starten
Nu dat de taak is gemaakt, wordt de taakweergave wordt automatisch geopend. 
1. De taak starten, klikt u op de **groene pijl** knop.

    ![Een taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. De standaardinstelling selecteren en op **Start**.
 
    ![Venster van de taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    De taak **Status** wijzigingen in **met**, en **invoer gebeurtenissen** en **Uitvoergebeurtenissen** worden weergegeven.

    ![Uitvoeringsstatus in Taakoverzicht](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a>De resultaten controleren in Visual Studio
1. Open in Visual Studio **Server Explorer** met de rechtermuisknop op de **TollDataRefJoin** tabel.
2. Selecteer **tabelgegevens weergeven** om te zien van de uitvoer van de taak.
   
    ![Selectie van de tabelgegevens weergeven in Server Explorer](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a>De taak metrische gegevens weergeven
Een aantal statistieken basic taak kunt u vinden in **taak metrische gegevens**. 

![Venster van de taak metrische gegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a>Lijst van de taak in Server Explorer
In **Server Explorer**, klikt u op **Stream Analytics-taken** en klik vervolgens op **vernieuwen**. De taak wordt weergegeven onder **Stream Analytics-taken**.

![Stream Analytics-taken die worden vermeld in Server Explorer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a>De taakweergave openen
De als taakweergave wilt openen, vouw het knooppunt van uw project en dubbelklik op de **taakweergave** knooppunt.

![Knooppunt van de taak weergeven](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a>Exporteren van een bestaande taak aan een project
Er zijn twee manieren kunt u een bestaande taak exporteren naar een project.

In **Server Explorer**, met de rechtermuisknop op het taakknooppunt in de **Stream Analytics-taken** uit en selecteer **exporteren naar nieuwe Stream Analytics-Project**.

![Exporteren naar nieuwe Stream Analytics-Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

Het project is gegenereerd op **Solution Explorer**.

![Project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
U ook kunt gebruiken de Project-weergave, en klik op **genereren Project**.

![Genereren van Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Bekende problemen en beperkingen
 
- Er is geen ondersteuning voor Power BI-uitvoer en Azure Date Lake Store-uitvoer.
- Er is geen editor-ondersteuning voor het toevoegen of wijzigen van de gebruiker gedefinieerde functies van JavaScript.

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tot Azure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met behulp van Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
