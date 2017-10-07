---
title: aaaResolve gegevens tijdverschil problemen met behulp van Azure Data Lake Tools voor Visual Studio | Microsoft Docs
description: Het oplossen van problemen die gegevens tijdverschil mogelijke oplossingen met behulp van Azure Data Lake Tools voor Visual Studio.
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Gegevens tijdverschil problemen oplossen met behulp van Azure Data Lake Tools voor Visual Studio

## <a name="what-is-data-skew"></a>Wat is er gegevens leiden tot onjuiste?

Kort gezegd, is gegevens tijdverschil een overmatig vertegenwoordigde waarde. Stel dat u hebt toegewezen 50 btw-onderzoekers tooaudit btw berekent, één examinator voor elke status van de Verenigde Staten. Hallo Wyoming examinator, heeft omdat er Hallo populatie klein is, weinig toodo. In Californië, echter wordt Hallo examinator opgeslagen erg druk is vanwege de grote bevolking Hallo-staat.
    ![Voorbeeld van gegevens tijdverschil probleem](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

In ons scenario is Hallo gegevens ongelijkmatig verdeeld over alle btw-onderzoekers, wat betekent dat sommige onderzoekers meer dan andere moeten werken. In uw eigen baan, moet u vaak situaties zoals Hallo btw examinator voorbeeld hier ervaren. Één hoekpunt opgehaald in meer technische voorwaarden veel meer gegevens dan de peers, een situatie die Hallo hoekpunt werken meer dan Hallo anderen en die uiteindelijk vertraagt een hele taak maakt. Wat is er slechter, mislukken Hallo taak, omdat de hoekpunten, bijvoorbeeld een beperking 5 uur runtime en een beperking 6 GB geheugen.

## <a name="resolving-data-skew-problems"></a>Het oplossen van problemen met gegevens tijdverschil

Met behulp van Azure Data Lake Tools voor Visual Studio kunt u vaststellen of de taak een probleem gegevens tijdverschil heeft. Als er een probleem is, kunt u deze kunt oplossen door de Hallo-oplossingen in deze sectie.

## <a name="solution-1-improve-table-partitioning"></a>Oplossing 1: Verbeteren Tabelpartities

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Optie 1: Filter Hallo vervormd sleutelwaarde van tevoren

Als het heeft geen invloed op uw bedrijfslogica, kunt u van tevoren Hallo hogere frequentie waarden filteren. Bijvoorbeeld, als er een groot aantal 000 000 000 in kolom GUID, raadzaam niet tooaggregate die waarde. Voordat u cumulatieve, kunt u ' WHERE GUID! '000 000 000' = ' toofilter Hallo hoge frequentie waarde.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Optie 2: Kies een andere partitie of distributie-sleutel

In het voorgaande voorbeeld Hallo als u wilt dat alleen toocheck Hallo btw-audit werkbelasting alle via land Hallo, u kunt Hallo gegevensdistributie verbeteren door het Hallo-id-nummer als uw sleutel te selecteren. Verzamelen van een andere partitie of distributiesleutel soms beter kunt verdelen Hallo gegevens, maar moet u ervoor dat deze keuze niet van invloed op uw bedrijfslogica toomake. Bijvoorbeeld: toocalculate Hallo btw som voor elke status kunt u toodesignate _status_ als partitiesleutel Hallo. Als u tooexperience dit probleem doorgaat, probeert u optie 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Optie 3: Meer partitie of distributie sleutels toevoegen

In plaats van alleen _status_ als een partitiesleutel, kunt u meer dan één sleutel gebruiken voor het partitioneren. Overweeg bijvoorbeeld _postcode_ als een extra partitie sleutel tooreduce gegevens partitie groottes en Hallo gegevens beter verdelen.

### <a name="option-4-use-round-robin-distribution"></a>Optie 4: Round-robin distributie gebruiken

Als u niet een geschikte sleutel voor partitie en distributie vinden, kunt u proberen toouse round-robin distributie. Round-robin distributie worden alle rijen gelijk behandeld en worden ze willekeurig in bijbehorende buckets geplaatst. Hallo-gegevens opgehaald gelijkmatig worden verdeeld, maar een nadeel van het ook zo de prestaties van de taak voor bepaalde bewerkingen plaats informatie verliest. Bovendien, als u aggregatie voor Hallo asymmetrische sleutel toch doet, bewaard Hallo gegevens tijdverschil probleem. toolearn meer informatie over round-robin distributie Zie Hallo U-SQL-tabel distributies sectie [CREATE TABLE (U-SQL): het maken van een tabel met Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Oplossing 2: Het queryplan Hallo verbeteren

### <a name="option-1-use-hello-create-statistics-statement"></a>Optie 1: De instructie CREATE STATISTICS hello gebruiken

U-SQL biedt de instructie CREATE STATISTICS hello in tabellen. Deze instructie biedt meer informatie toohello queryoptimalisatie over Hallo gegevenskenmerken, zoals distributie waarde, die zijn opgeslagen in een tabel. Voor de meeste query's genereert Hallo queryoptimalisatie al Hallo nodig statistieken voor een hoge kwaliteit queryplan. In sommige gevallen moet u mogelijk tooimprove queryprestaties met het maken van aanvullende statistieken met statistieken maken of te wijzigen Hallo queryontwerp. Zie voor meer informatie, Hallo [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) pagina.

Codevoorbeeld:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Statistische gegevens wordt niet automatisch bijgewerkt. Als u gegevens in een tabel Hallo zonder Hallo statistieken worden opnieuw gemaakt bijwerkt, zou kunnen Hallo queryprestaties afnemen.

### <a name="option-2-use-skewfactor"></a>Optie 2: SKEWFACTOR gebruiken

Als u toosum Hallo belasting voor elke status wilt, moet u GROEPEREN op status, een benadering die niet Hallo gegevens tijdverschil probleem voorkomen. U kunt echter een hint gegevens opgeven in uw query tooidentify gegevens leiden tot sleutels onjuiste zodat Hallo optimaliseren een uitvoeringsplan voor u voorbereiden kunt.

Meestal kunt u Hallo parameter instellen als 0,5 en 1, met 0,5, wat betekent dat niet veel zware tijdverschil scheeftrekken en 1 betekenis. Aangezien Hallo-hint is van invloed op uitvoeringsplan optimalisatie voor de huidige instructie Hallo en alle downstream-instructies, moet u ervoor tooadd Hallo hint voordat potentiële Hallo vervormd key-wise aggregatie.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Codevoorbeeld:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Optie 3: ROWCOUNT gebruiken  
Bovendien tooSKEWFACTOR voor specifieke vervormd-sleutel join gevallen, als u weet dat Hallo andere rijenset gekoppelde is klein, kunt u instellen dat Hallo optimaliseren door toe te voegen een ROWCOUNT-hint in Hallo U-SQL-instructie voor samenvoegen. Op deze manier optimaliseren kunt ervoor kiezen een toohelp broadcast join-strategie voor de prestaties verbeteren. Let erop dat ROWCOUNT Hallo gegevens tijdverschil probleem niet is opgelost, maar aanvullende hulp kunnen worden aangeboden.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Codevoorbeeld:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Oplossing 3: Hallo gebruiker gedefinieerde reducer en combiner verbeteren

U kunt een gebruiker gedefinieerde operator toodeal met ingewikkeld proces logica soms schrijven en een goed geschreven reducer en combiner mogelijk een probleem gegevens tijdverschil in sommige gevallen beperken.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Optie 1: Een reducer recursieve indien mogelijk gebruiken

Een door de gebruiker gedefinieerde reducer wordt standaard uitgevoerd in de modus voor niet-recursieve, wat betekent dat de hoeveelheid werk voor een sleutel die wordt gedistribueerd in een enkel hoekpunt. Maar als uw gegevens is vervormd, Hallo grote gegevenssets mogelijk verwerkt in een enkel hoekpunt en lange tijd worden uitgevoerd.

tooimprove prestaties, kunt u een kenmerk toevoegen in uw code toodefine reducer toorun in de recursieve modus. Vervolgens Hallo grote gegevenssets worden gedistribueerde toomultiple hoekpunten en parallel, die uw taak sneller worden uitgevoerd.

een niet-recursieve reducer toorecursive toochange, moet u ervoor dat de algoritme associatieve toomake. Bijvoorbeeld Hallo som is associatieve en Hallo mediaan is niet. Ook moet u ervoor dat Hallo invoer en uitvoer voor reducer Hallo behoudt toomake hetzelfde schema.

Kenmerk van recursieve reducer:

    [SqlUserDefinedReducer(IsRecursive = true)]

Codevoorbeeld:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Optie 2: Rijniveau combiner modus gebruiken, indien mogelijk

Vergelijkbare toohello ROWCOUNT hint op voor specifieke vervormd sleutel join gevallen, combiner modus probeert toodistribute grote vervormd-sleutelwaarde sets toomultiple hoekpunten zodat Hallo werk gelijktijdig kan worden uitgevoerd. Gegevens tijdverschil problemen kan niet worden omgezet in combiner modus, maar aanvullende hulp voor grote vervormd-sleutelwaarde sets kunnen worden aangeboden.

Standaard is Hallo combiner modus volledig, wat betekent dat Hallo rij ingestelde links en rechts rijenset kan niet worden gescheiden. Instelling Hallo-modus als rechts-links/interne kunnen rijniveau join. Hallo systeem scheidt Hallo overeenkomende rij sets en ze worden verdeeld over meerdere hoekpunten die parallel worden uitgevoerd. Voordat u Hallo combiner modus configureren, let er tooensure die overeenkomstige rij sets Hallo kan worden gescheiden.

volgende Hallo voorbeeld ziet u een rijenset gescheiden links. Elke rij van de uitvoer, is afhankelijk van één rij invoer van Hallo links en mogelijk afhankelijk is van alle rijen uit Hallo Hallo met dezelfde sleutelwaarde. Als u links Hallo combiner modus instelt, wordt Hallo systeem scheidt Hallo grote linkerkant-rijenset in kleine netwerken en wijst deze toomultiple hoekpunten.

![Afbeelding van combiner-modus](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Als u Hallo verkeerde combiner modus instelt, Hallo combinatie is minder efficiënt en Hallo resultaten mis zijn.

De kenmerken van combiner modus:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links (en mogelijk alle rijen uit Hallo Hallo met dezelfde sleutelwaarde).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): elke rij van de uitvoer is afhankelijk van één rij invoer van de juiste hello (en mogelijk alle rijen uit Hallo links Hello dezelfde sleutelwaarde).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links en Hallo Hallo met dezelfde waarde.

Codevoorbeeld:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
