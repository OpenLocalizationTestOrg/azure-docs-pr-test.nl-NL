---
title: aaaPower BI-dashboard op Azure Stream Analytics | Microsoft Docs
description: Gebruik een realtime streaming Power BI-dashboard toogather business intelligence en analyseren van grote hoeveelheden gegevens uit een Stream Analytics-taak.
keywords: dashboard met analytische, realtime dashboard
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics en Power BI: een realtime analytics-dashboard voor het streamen van gegevens
Azure Stream Analytics kunt u profiteren van een van de hulpprogramma's voor bedrijfsinformatie, voorloopspaties Hallo tootake [Microsoft Power BI](https://powerbi.com/). In dit artikel leert u hoe hulpprogramma's voor bedrijfsinformatie te maken met behulp van Power BI als uitvoer voor uw Azure Stream Analytics-taken. U leert ook hoe toocreate en gebruiken van een realtime dashboard.

In dit artikel wordt voortgezet vanaf Hallo Stream Analytics [realtime-fraudedetectie](stream-analytics-real-time-fraud-detection.md) zelfstudie. Het is gebaseerd op Hallo-werkstroom gemaakt in deze zelfstudie en voegt een Power BI zodat u kunt visualiseren frauduleuze telefoongesprekken die zijn gedetecteerd door een Streaming Analytics-taak uitvoeren. 

U kunt bekijken [video](https://www.youtube.com/watch?v=SGUpT-a99MA) die dit scenario laat zien.


## <a name="prerequisites"></a>Vereisten

Zorg voordat u begint, hebt u de volgende Hallo:

* Een Azure-account.
* Een account voor Power BI. U kunt een werk- of een schoolaccount gebruiken.
* Een voltooide versie van Hallo [realtime-fraudedetectie](stream-analytics-real-time-fraud-detection.md) zelfstudie. Hallo-zelfstudie omvat een app die fictieve telefoongesprek metagegevens genereert. In de zelfstudie hello, een event hub maken en verzenden Hallo streaming telefoongesprek gegevens toohello event hub. U een query schrijven waarmee frauduleuze aanroepen detecteert (aanroepen vanuit dezelfde number op Hallo Hallo dezelfde periode in verschillende locaties). 


## <a name="add-power-bi-output"></a>Power BI-uitvoer toevoegen
In Hallo realtime fraude detectie zelfstudie Hallo uitvoer tooAzure blobopslag verzonden. In deze sectie voegt u een uitvoer die informatie tooPower BI verzendt.

1. Open in hello Azure-portal, Hallo Streaming Analytics-taak die u eerder hebt gemaakt. Als u de voorgestelde naam Hallo gebruikt, Hallo taak heet `sa_frauddetection_job_demo`.

2. Selecteer Hallo **uitvoer** in het midden van Hallo taak dashboard Hallo vak en selecteer vervolgens **+ toevoegen**.

3. Voor **Uitvoeraliassen**, voer `CallStream-PowerBI`. U kunt een andere naam gebruiken. Als u dit doet, noteer, omdat u de naam van de hello later nodig. 

4. Onder **Sink**, selecteer **Power BI**.

   ![Maken van een uitvoer voor Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Klik op **autoriseren**.

    Een venster wordt geopend waarin u uw Azure-referenties voor een werk- of schoolaccount account kunt opgeven. 

    ![Geef referenties voor toegang tot tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Geef uw referenties. Let en wanneer u uw referenties invoeren, geeft u bent ook beschermd machtiging toohello Streaming Analytics-taak tooaccess uw Power BI-gebied.

7. Wanneer u wordt teruggeleid toohello **nieuwe uitvoer** blade Voer Hallo volgende informatie:

    * **Werkruimte groep**: Selecteer een werkruimte in uw Power BI-tenant waar u toocreate Hallo gegevensset.
    * **Naam van DataSet**: Voer `sa-dataset`. U kunt een andere naam gebruiken. Als u dit doet, noteer deze later.
    * **Tabelnaam**: Voer `fraudulent-calls`. Power BI-uitvoer van de Stream Analytics-taken zijn op dit moment slechts één tabel in een dataset.

    ![PBI-werkruimte](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Als Power BI een gegevensset heeft en tabel met dezelfde naam als Hallo Hallo die u opgeeft in de Stream Analytics-taak hello, worden bestaande toepassingsgroepen hallo overschreven.
    > U wordt aangeraden dat u niet expliciet deze gegevensset en de tabel in uw Power BI-account maakt. Ze worden automatisch gemaakt wanneer u uw Stream Analytics-taak start en Hallo taak gemalen uitvoer naar Power BI begint. Als de taak query geen resultaten oplevert, Hallo gegevensset en de tabel niet gemaakt.
    >

8. Klik op **Create**.

Hallo gegevensset is gemaakt met Hallo volgende instellingen:

* **defaultRetentionPolicy: BasicFIFO**: gegevens zijn FIFO, met een maximum van 200.000 rijen.
* **defaultMode: pushStreaming**: Hallo dataset ondersteunt streaming tegels en traditionele op basis van een rapport visuele elementen (ook push).

U kunt op dit moment gegevenssets maken met andere vlaggen.

Zie voor meer informatie over Power BI-gegevenssets Hallo [Power BI REST-API](https://msdn.microsoft.com/library/mt203562.aspx) verwijzing.


## <a name="write-hello-query"></a>Hallo-query schrijven

1. Sluit Hallo **uitvoer** blade en return toohello taakblade.

2. Klik op Hallo **Query** vak. 

3. Voer Hallo query te volgen. Deze query is vergelijkbaar toohello zelf join-query die u in Hallo fraudedetectie zelfstudie hebt gemaakt. Hallo verschil is dat deze query verzendt resultaten toohello nieuwe uitvoer u hebt gemaakt (`CallStream-PowerBI`). 

    >[!NOTE]
    >Als u hebt niet de naam Hallo invoer `CallStream` vervangen door uw naam in de zelfstudie voor het detecteren van fraude van Hallo `CallStream` in Hallo **FROM** en **JOIN** componenten in Hallo-query.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Klik op **Opslaan**.


## <a name="test-hello-query"></a>Hallo-testquery
Deze sectie is optioneel maar aanbevolen. 

1. Als Hallo TelcoStreaming app niet wordt uitgevoerd, start u deze met de volgende stappen:

    * Open een opdrachtvenster.
    * Ga toohello map waarin Hallo telcogenerator.exe en telcodatagen.exe.config gewijzigde bestanden zijn.
    * Hallo volgende opdracht uitvoeren:

            telcodatagen.exe 1000 .2 2

2. In Hallo **Query** blade, klikt u op Hallo punten volgende toohello `CallStream` invoer- en selecteer vervolgens **voorbeeldgegevens uit de invoer**.

3. U wilt opgeven dat drie minuten aan gegevens en klik op **OK**. Wacht totdat u een bericht dat Hallo gegevens steekproefgewijs verkregen.

4. Klik op **Test** en zorg ervoor dat u resultaten krijgt.


## <a name="run-hello-job"></a>Hallo-taak uitvoeren

1. Zorg ervoor dat Hallo TelcoStreaming app wordt uitgevoerd.

2. Sluit Hallo **Query** blade.

3. Klik op Hallo taakblade **Start**.

    ![Hallo Stream Analytics-taak starten](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Uw Streaming Analytics-taak wordt gestart frauduleuze aanroepen in de stroom voor inkomende hello zoekt. Hallo taak ook Hallo gegevensset en de tabel in Power BI maakt en begint met het verzenden van gegevens over Hallo frauduleuze aanroepen toothem.


## <a name="create-hello-dashboard-in-power-bi"></a>Hallo-dashboard maken in Power BI

1. Ga te[Powerbi.com](https://powerbi.com) en meld u aan met uw werk of school-account. Als Hallo Stream Analytics-taak query worden de resultaten, ziet u dat uw gegevensset al is gemaakt:

    ![Streaming gegevensset in Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. Klik in de werkruimte op  **+ &nbsp;maken**.

    ![Hallo-knop maken klikt in Power BI-werkruimte](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Maak een nieuw dashboard en noem deze `Fraudulent Calls`.

    ![Een dashboard maken en hieraan een naam in Power BI-werkruimte](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Bovenaan Hallo Hallo-venster, klikt u op **toevoegen tegel**, selecteer **aangepaste STREAMINGGEGEVENS**, en klik vervolgens op **volgende**.

    ![Aangepaste gegevensset streaming](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. Onder **uw DATSETS**, selecteer uw gegevensset en klik vervolgens op **volgende**.

    ![Uw streaminggegevensset](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. Onder **visualisatie Type**, selecteer **kaart**, en klik vervolgens in Hallo **velden** selecteert **fraudulentcalls**.

    ![Details van de visualisatie voor nieuwe tegel](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Klik op **Volgende**.

8. Vul in de tegel-gegevens, zoals een titel en subtitel.

    ![Titel en subtitel voor nieuwe tegel](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Klik op **Toepassen**.

    U hebt nu een teller fraude.

    ![Fraude teller](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Volg Hallo stappen opnieuw tooadd een tegel (te beginnen bij stap 4). Deze tijd Hallo te volgen:

    * Als u krijgt te**visualisatie Type**, selecteer **lijndiagram**. 
    * Een as toevoegen en selecteer **windowend**. 
    * Een waarde toevoegen en selecteer **fraudulentcalls**.
    * Voor **tijd venster toodisplay**, selecteer Hallo van afgelopen 10 minuten.

    ![Tegel lijndiagram maken](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Klik op **volgende**, het toevoegen van een titel en subtitel en klikt u op **toepassen**.

    Hallo Power BI-dashboard kunt u nu twee weergaven van gegevens over frauduleuze aanroepen als gedetecteerd in Hallo gegevensstromen.

    ![Klaar met Power BI-dashboard met twee tegels voor frauduleuze aanroepen](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Meer informatie over Power BI

Deze zelfstudie laat zien hoe toocreate alleen enkele soorten visualisaties voor een dataset. Power BI kunt u andere klant hulpprogramma's voor bedrijfsinformatie voor uw organisatie te maken. Zie voor meer ideeën Hallo resources te volgen:

* Voor een ander voorbeeld van een Power BI-dashboard bekijkt hello [aan de slag met Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.
* Taak voor meer informatie over het configureren van Streaming Analytics uitvoer tooPower BI en u Power BI-groepen bekijken Hallo [Power BI](stream-analytics-define-outputs.md#power-bi) sectie Hallo [Stream Analytics levert](stream-analytics-define-outputs.md) artikel. 
* Zie voor meer informatie over het gebruik van Power BI in het algemeen [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Meer informatie over de beperkingen en best practices
Op dit moment kunnen Power BI ongeveer één keer per seconde worden aangeroepen. Streaming visuele elementen ondersteuning bieden voor pakketten van 15 KB. Daarna streaming visuele elementen mislukken (maar push blijft toowork). Vanwege deze beperkingen Power BI gepaard meest natuurlijk toocases waar Azure Stream Analytics een aanzienlijke hoeveelheid gegevens laden beperken biedt. U wordt aangeraden een tumblingvenster of Hopping venster tooensure gegevens-push is maximaal één push per seconde is en of uw query belandt binnen Hallo doorvoer vereisten.

Kunt u Hallo vergelijking toocompute Hallo waarde toogive na het venster (in seconden):

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Bijvoorbeeld:

* U hebt 1000 apparaten verzenden van gegevens met een interval van één seconde.
* U gebruikt Hallo Power BI Pro SKU die ondersteuning biedt voor 1.000.000 rijen per uur.
* Wilt u toopublish Hallo hoeveelheid gemiddelde gegevens per apparaat tooPower BI.

Als gevolg hiervan wordt het Hallo vergelijking:

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

In deze configuratie kunt u Hallo oorspronkelijke query toohello volgende wijzigen:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Verificatie vernieuwen
Als het Hallo-wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd, moet u tooreauthenticate uw Power BI-account. Als Azure multi-factor Authentication is geconfigureerd op de tenant van uw Azure Active Directory (Azure AD), moet u ook toorenew Power BI autorisatie elke twee weken. Als u niet verlengt, kan er problemen zoals een gebrek aan taakuitvoer of een `Authenticate user error` in Hallo bewerkingslogboeken.

Als een taak wordt gestart nadat het Hallo-token is verlopen, een fout optreedt en Hallo taak mislukt. tooresolve dit probleem stoppen Hallo-taak die wordt uitgevoerd, en gaat u tooyour Power BI-uitvoer. tooavoid gegevensverlies, selecteer Hallo **vernieuwen autorisatie** koppelen en start de taak in Hallo **laatste tijd geëindigd**.

Nadat het Hallo-autorisatie is vernieuwd met Power BI, een groene waarschuwing wordt weergegeven in Hallo autorisatie gebied tooreflect Hallo probleem is opgelost.

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Naslaginformatie over Azure Stream Analytics Management REST-API](https://msdn.microsoft.com/library/azure/dn835031.aspx)
