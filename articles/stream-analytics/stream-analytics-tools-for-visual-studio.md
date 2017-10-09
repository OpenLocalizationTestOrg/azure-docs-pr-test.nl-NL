---
title: aaaUse Azure Stream Analytics-Tools voor Visual Studio | Microsoft Docs
description: Zelfstudie voor hello Azure Stream Analytics-Tools voor Visual Studio aan de slag
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
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken
## <a name="introduction"></a>Inleiding
In deze zelfstudie leert u hoe toouse Azure Stream Analytics-Tools voor Visual Studio-toocreate ontwerpen, lokaal testen, beheren en fouten opsporen in uw Stream Analytics-taken. 

Na het voltooien van deze zelfstudie, kunt u zich kunt:
* Tijd om uzelf bekend met Stream Analytics-hulpprogramma's voor Visual Studio.
* Configureren en implementeren van een Stream Analytics-taak.
* Test uw taak lokaal met lokale voorbeeldgegevens.
* Gebruik controle tootroubleshoot problemen.
* Bestaande taken tooprojects exporteren.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:
* Hallo-stappen die worden voorafgegaan door 'Een Stream Analytics-taak maken' in hello voltooien [een IoT-oplossing bouwen met behulp van de Stream Analytics-zelfstudie](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Gebruik Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012. Enterprise (Ultimate/Premium), Professional en Community-edities worden ondersteund. Express edition wordt niet ondersteund. Visual Studio 2017 wordt niet ondersteund. 
* Gebruik hello Azure SDK voor .NET versie 2.7.1 of hoger. Installeren met behulp van Hallo [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).
* Hallo installeren [Stream Analytics-Tools voor Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Een Stream Analytics-project maken
1. Klik in Visual Studio op Hallo **bestand** menu en selecteer **nieuw Project**. 

2. Selecteer in Hallo sjablonen lijst aan de linkerkant Hallo **Stream Analytics** en klik vervolgens op **Azure Stream Analytics toepassing**.

3. Voer Hallo project **naam**, **locatie**, en **oplossingsnaam** als voor andere projecten.

    ![Nieuw Project-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Een **Tolstation** project is gegenereerd op **Solution Explorer**.

    ![Tolstation project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Kies het juiste abonnement Hallo
1. Klik in Visual Studio op Hallo **weergave** menu en open **Server Explorer**.

2. Meld u aan met uw Azure-Account. 

## <a name="define-hello-input-sources"></a>Hallo invoerbronnen definiëren
1.  In **Solution Explorer**, vouw Hallo **invoer** knooppunt en wijzig de naam **Input.json** te**EntryStream.json**. Dubbelklik op **EntryStream.json**.
2.  Hallo **invoer Alias** is nu **EntryStream**. Hallo invoer alias wordt gebruikt in Hallo query script. 
3.  In **brontype**, selecteer **gegevensstroom**.
4.  In **bron**, selecteer **Event Hub**.
5.  In **Service Bus Namespace**, selecteer Hallo **TollData** optie.
6.  In **naam Event Hub**, selecteer **vermelding**.
7.  In **Event Hub-beleidsnaam**, selecteer **RootManageSharedAccessKey** (Hallo standaardwaarde).
8.  In **gebeurtenis serialisatie-indeling**, selecteer **Json**. 
9.  In **codering**, selecteer **UTF8**. Uw instellingen moeten eruitzien als Hallo schermafbeelding te volgen:

    ![Invoer-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. wizard toofinish hello, klikt u op **opslaan**. U kunt nu een andere invoerbron toocreate Hallo afsluiten stroom toevoegen. Klik met de rechtermuisknop Hallo **invoer** uit en selecteer **Nieuw Item**.

    ![Nieuw Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Selecteer in het venster Hallo **Azure Stream Analytics invoer**, en wijzig Hallo **naam** te**ExitStream.json**. Klik op **Add**.

    ![Venster Nieuw Item toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Dubbelklik op **ExitStream.json** in Hallo-project en volg Hallo dezelfde stappen als bij Hallo vermelding stroom. Ervoor tooenter worden **sluiten** voor Hallo **naam Event Hub** zoals weergegeven in de volgende schermafbeelding Hallo:

    ![ExitStream venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    U hebt nu twee invoer streams gedefinieerd:

    ![Toegang naar en uitgang invoer stromen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Voeg vervolgens de gegevensinvoer verwijzing voor Hallo blob-bestand met de registratiegegevens auto.

13. Klik met de rechtermuisknop Hallo **invoer** knooppunt in het Hallo-project en klik vervolgens op Hallo van Volg dezelfde stappen als bij Hallo stroom invoer. In **invoer Alias**, voer **registratie**, en in **brontype**, selecteer **referentiegegevens**.

    ![Registratie-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. In **Opslagaccount**, selecteer Hallo **tolldata** optie. In **Container**, selecteer **tolldata**, en in **pad patroon**, voer **registration.json**. Deze naam is hoofdlettergevoelig en moet in kleine letters.
15. wizard toofinish hello, klikt u op **opslaan**.

Nu worden alle Hallo invoer gedefinieerd.

## <a name="define-hello-output"></a>Hallo-uitvoer definiëren
1.  In **Solution Explorer**, vouw Hallo **invoer** knooppunt en dubbelklik op **Output.json**.

2.  In **Uitvoeraliassen**, voer **uitvoer**. 
3.  In **Sink**, selecteer **SQL-Database**.
4.  In **Database**, selecteer **TollDataDB**.
5.  In **gebruikersnaam**, voer **tolladmin**. 
6.  In **wachtwoord**, voer **123toll!**.
7.  In **tabel**, voer **TollDataRefJoin**.
8.  Klik op **Opslaan**.

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Een Stream Analytics query maken
Deze zelfstudie probeert tooanswer verschillende bedrijfsvragen gerelateerde tootoll gegevens zijn. Dit wordt ook Stream Analytics query's die kunnen worden gebruikt in de Stream Analytics tooprovide relevante antwoorden.
Voordat u uw eerste Stream Analytics-taak, we gaan een eenvoudige scenario en Hallo-querysyntaxis te verkennen.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Inleiding toohello querytaal van Stream Analytics
Stel dat u nodig hebt toocount Hallo aantal voertuigen dat een tolstation stand invoeren. Omdat dit voorbeeld een continue stroom van gebeurtenissen is, hebt u toodefine een periode. Hallo vraag toobe 'hoeveel voertuigen Geef een tolstation stand elke drie minuten?' wijzigen Deze manier toocount gegevens vaak wordt aangeduid tooas Hallo daling aantal.

Bekijkt hello Stream Analytics query waarmee deze vraag worden beantwoord:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Stream Analytics maakt gebruik van een querytaal die lijkt op SQL en enkele extensies toospecify tijd gerelateerde aspecten van Hallo query toegevoegd.

Zie voor meer informatie [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructies die worden gebruikt in query Hallo van MSDN.

Nu u uw eerste Stream Analytics query hebt geschreven, is het tijd tootest deze. Hallo voorbeeldbestanden zich in de map TollApp in in het pad naar hello gebruiken:

.. \TollApp\TollApp\Data

Deze map bevat de volgende bestanden Hallo:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Het aantal voertuigen een tolstation stand Hallo tellen
Dubbelklik in het Hallo-project op **Script.asaql** tooopen Hallo script in Hallo **Query-Editor**. Kopieer en plak Hallo script in de vorige sectie Hallo in Hallo-editor. Hallo Query-Editor biedt ondersteuning voor IntelliSense syntaxiskleuren en Hallo fout markering.

![Query-Editor](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Stream Analytics query's lokaal testen

1. toocompile hello query toosee als er een syntaxisfout, met de rechtermuisknop op het Hallo-project en selecteer **bouwen**. 

2. toovalidate deze query tegen voorbeeldgegevens, kunt u lokale voorbeeldgegevens. Met de rechtermuisknop op het Hallo-invoer en selecteer **lokale invoer toevoegen**.

    ![Lokale invoer toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Selecteer in het pop-upvenster Hallo, Hallo voorbeeldgegevens vanaf uw lokale pad. Klik op **Opslaan**.

    ![Lokale invoer venster toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Een bestand met de naam **local_EntryStream.json** tooyour invoer map automatisch wordt toegevoegd.

    ![Toegevoegde tooinputs bestandsmap](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. In Hallo **Query-Editor**, klikt u op **lokaal uitvoeren**. Of u kunt ook op Hallo F5 drukken.

    ![Lokaal uitvoeren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Lokaal uitvoeren van uitvoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Druk op belangrijke tooview Hallo uitvoer in Hallo **ASA lokale uitvoeren resultaat** venster in Visual Studio. 

    ![Venster ASA lokale uitvoeren resultaat](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Klik op **geopende resultaat map** toocheck Hallo uitvoerbestanden beide in CSV en JSON-indeling.

    ![Open resultaat map uitvoer](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Voorbeeld Hallo invoergegevens
U kunt ook invoer voorbeeldgegevens vanuit het lokale bestand voor invoerbronnen tooa. 
1. Met de rechtermuisknop op Hallo invoer config-bestand en selecteer **voorbeeldgegevens**. 

   ![Voorbeeldgegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    U kunt alleen de event hub of -IoT-hub steekproef nemen nu. Andere bronnen worden niet ondersteund.

2. Voer in het pop-upvenster hello, Hallo lokaal pad gebruikt toosave Hallo-voorbeeldgegevens. Klik op **voorbeeld**.

    ![Venster van de gegevens voorbeeld](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    U kunt de voortgang Hallo in Hallo bekijken **uitvoer** venster. 

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Verzenden van een Stream Analytics query tooAzure
1. In Hallo **Query-Editor**, klikt u op **indienen tooAzure** in de Hallo scripteditor.

    ![TooAzure verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Selecteer **maken van een nieuwe Azure Stream Analytics-taak**. Voer Hallo **taaknaam**, en selecteer Hallo juist **abonnement**. Klik op **indienen**.

    ![Venster van de taak verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Een taak starten
Nu dat de taak is gemaakt, wordt Hallo taakweergave automatisch geopend. 
1. Hallo toostart taak, klikt u op Hallo **groene pijl** knop.

    ![Een taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. De standaardinstelling Hallo selecteren en op **Start**.
 
    ![Venster van de taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    Hallo taak **Status** wijzigingen te**met**, en **invoer gebeurtenissen** en **Uitvoergebeurtenissen** worden weergegeven.

    ![Uitvoeringsstatus in Taakoverzicht](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Resultaten van de Hallo in Visual Studio
1. Open in Visual Studio **Server Explorer** en klik met de rechtermuisknop Hallo **TollDataRefJoin** tabel.
2. Selecteer **tabelgegevens weergeven** toosee Hallo uitvoer van de taak.
   
    ![Selectie van de tabelgegevens weergeven in Server Explorer](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Metrische gegevens weergeven Hallo taak
Een aantal statistieken basic taak kunt u vinden in **taak metrische gegevens**. 

![Venster van de taak metrische gegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Lijst Hallo taak in Server Explorer
In **Server Explorer**, klikt u op **Stream Analytics-taken** en klik vervolgens op **vernieuwen**. Hallo-taak wordt weergegeven onder **Stream Analytics-taken**.

![Stream Analytics-taken die worden vermeld in Server Explorer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Open Hallo taak weergeven
tooopen hello taak weergeven, vouwt u het taakknooppunt en dubbelklikt u op Hallo **taakweergave** knooppunt.

![Knooppunt van de taak weergeven](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Een bestaande taak tooa project exporteren
Er zijn twee manieren kunt u een bestaand taak tooa project exporteren.

In **Server Explorer**, klik met de rechtermuisknop Hallo taakknooppunt in Hallo **Stream Analytics-taken** uit en selecteer **tooNew Stream Analytics Project exporteren**.

![TooNew Stream Analytics Project exporteren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

Hallo-project is gegenereerd op **Solution Explorer**.

![Project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
U ook kunt gebruiken Hallo taak weergeven en klik op **genereren Project**.

![Genereren van Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Bekende problemen en beperkingen
 
- Er is geen ondersteuning voor Power BI-uitvoer en Azure Date Lake Store-uitvoer.
- Er is geen editor-ondersteuning voor het toevoegen of wijzigen van de gebruiker gedefinieerde functies van JavaScript.

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met behulp van Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
