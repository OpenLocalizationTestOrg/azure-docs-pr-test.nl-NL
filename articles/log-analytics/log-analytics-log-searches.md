---
title: aaaFind gegevens met logboek van zoekopdrachten in Azure Log Analytics | Microsoft Docs
description: Logboek zoekopdrachten kunnen u toocombine en correleren machinegegevens uit meerdere bronnen binnen uw omgeving.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Gegevens met behulp van logboek zoekopdrachten in logboekanalyse zoeken

>[!NOTE]
> Dit artikel wordt beschreven logboek zoekopdrachten met het huidige querytaal Hallo in logboekanalyse.  Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en u dient te raadplegen[Understanding logboek zoekt in logboekanalyse (nieuw)](log-analytics-log-search-new.md).


Hallo-kern van logboekanalyse is Hallo logboek zoekfunctie waarmee u toocombine en correleren machinegegevens uit meerdere bronnen binnen uw omgeving. Oplossingen worden ook aangedreven door logboek zoeken toobring u metrische gegevens om een bepaald probleemgebied gedraaid.

Op de zoekpagina hello, kunt u een query maken en vervolgens wanneer u zoekt, kunt u filteren Hallo resultaten met facet besturingselementen. U kunt ook tootransform geavanceerde query's, te filteren en rapport maken op de resultaten.

Algemene logboek zoekquery's weergegeven op de meeste oplossing's. U kunt in de gehele Hallo OMS-console tegels klikt u op of inzoomen in tooother items tooview details over Hallo item met logboek zoeken.

In deze zelfstudie doorlopen we voorbeelden toocover alle Hallo basisbeginselen wanneer u logboek zoeken gebruikt.

We beginnen met eenvoudige, praktische voorbeelden en klik vervolgens op deze bouwen zodat u kunt een goed begrip van praktische gebruiksdoeleinden over hoe toouse Hallo syntaxis tooextract Hallo inzichten u van Hallo-gegevens wilt ophalen.

Nadat u nagegaan wat de zoektechnieken hebt, kunt u controleren Hallo [logboekanalyse Meld zoeken verwijzing](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Basic-filters gebruiken
Hallo eerst te beginnen tooknow die Hallo eerste deel uitmaakt van een zoekopdracht, voordat een ' | ' verticale pipe-teken is altijd een *filter*. U kunt dit beschouwen als een WHERE-component in TSQL--bepaalt *wat* subset van gegevens toopull buiten Hallo OMS-gegevensarchief. Zoeken in het gegevensarchief Hallo is grotendeels over het opgeven van Hallo kenmerken van Hallo-gegevens die u tooextract, wilt dus is het natuurlijke dat een query met Hallo WHERE-component beginnen wilt.

Hallo meest eenvoudige filters kunt u zijn *trefwoorden*, zoals 'fout' of 'out' of een computernaam op. Deze typen van eenvoudige query's in het algemeen diverse vormen retourneren van gegevens binnen Hallo dezelfde resultaatset. Dit komt doordat Log Analytics uit verschillende *typen* van gegevens in Hallo-systeem.

### <a name="tooconduct-a-simple-search"></a>een eenvoudige zoekopdrachten tooconduct
1. Klik in de OMS-portal Hallo **logboek zoeken**.  
    ![tegel Search](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Typ in Hallo queryveld `error` en klik vervolgens op **Search**.  
    ![Fout bij zoeken](./media/log-analytics-log-searches/oms-search-error.png)  
    Bijvoorbeeld Hallo query voor `error` in Hallo geretourneerd de volgende afbeelding 100.000 **gebeurtenis** records (verzameld door Log-beheer), 18 **ConfigurationAlert** records (gegenereerd door de configuratie Beoordeling) en 12 **ConfigurationChange** records (vastgelegd door Hallo bijhouden).   
    ![zoekresultaten](./media/log-analytics-log-searches/oms-search-results01.png)  

Deze filters zijn niet echt objectklassen typen. *Type* is slechts een label of een eigenschap of een tekenreeks/naam/categorie, die is gekoppeld tooa gegevensitem. Een aantal documenten in Hallo system zijn gelabeld als **Type: ConfigurationAlert** en sommige zijn gelabeld als **Type: Perf**, of **gebeurtenistype:**, enzovoort. Elke zoekresultaat, document, record of vermelding geeft alle onbewerkte Hallo-eigenschappen en hun waarden voor elk van deze onderdelen van gegevens en kunt u deze namen veld toospecify in Hallo filter als u wilt dat tooretrieve alleen Hallo records waar Hallo veld heeft die gegeven waarde.

*Type* is gewoon een veld dat alle records hebt, is niet anders dan een ander veld. Dit is vastgesteld op basis van het Hallo-waarde van veld Hallo-Type. Deze record heeft een andere vorm of vorm. Incidenteel, **Type = Perf**, of **Type gebeurtenis =** is ook moet u toolearn tooquery prestatiegegevens of gebeurtenissen Hallo-syntaxis.

U kunt een dubbele punt (:) of een gelijkteken (=) na Hallo veldnaam en voor Hallo waarde gebruiken. **Gebeurtenistype:** en **Type gebeurtenis =** vergelijkbaar zijn met het betekenis, kunt u Hallo u liever stijl.

Dus als hello typt = Perf records hebben een veld met de naam 'CounterName' en vervolgens kunt u een query die lijkt op `Type=Perf CounterName="% Processor Time"`.

Hiermee krijgt u alleen Hallo prestatiegegevens als naam Prestatiemeter Hallo is '% processortijd'.

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch voor prestatiegegevens van processor time
* Typ in het Hallo-zoekveld query`Type=Perf CounterName="% Processor Time"`

U kunt ook niet meer specifiek en **InstanceName = _ 'Totaal'** in Hallo-query die een Windows-prestatiemeteritem is. U kunt ook een facet en een andere selecteren **veldwaarde:**. Hallo-filter wordt automatisch tooyour filter toegevoegd op Hallo query-balk. U kunt dit zien in Hallo installatiekopie te volgen. Er wordt aangegeven waar tooclick tooadd **InstanceName: '_Totaal'** toohello query zonder iets te typen.

![facet zoeken](./media/log-analytics-log-searches/oms-search-facet.png)

Er wordt nu uw query`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

In dit voorbeeld wordt er geen toospecify **Type = Perf** tooget toothis resultaat. Omdat Hallo velden CounterName en InstanceName bestaan alleen voor records van het Type = Perf, Hallo-query is specifiek genoeg tooreturn Hallo als langer vorige een Hallo dezelfde resultaten:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Dit komt doordat alle Hallo filters in Hallo query worden geëvalueerd als *en* met elkaar. Effectief hello meer velden u toohello criteria toevoegen, krijgt u minder specifiek en verfijnd resultaten.

Bijvoorbeeld Hallo query `Type=Event EventLog="Windows PowerShell"` is identiek te`Type=Event AND EventLog="Windows PowerShell"`. Retourneert alle gebeurtenissen die zijn aangemeld en verzameld uit Hallo Windows PowerShell-gebeurtenislogboek. Als u een filter meerdere keren toevoegen door te selecteren herhaaldelijk Hallo dezelfde beperkingsfacet, klikt u vervolgens Hallo probleem puur cosmetisch--het Hallo zoekbalk bruikbaar mogelijk blijft, maar nog steeds retourneert Hallo dezelfde resultaten Hallo impliciete AND-operator is er altijd is.

U kunt eenvoudig hello impliciete AND-operator met behulp van een niet-operator expliciet omkeren. Bijvoorbeeld:

`Type:Event NOT(EventLog:"Windows PowerShell")`of de bijbehorende equivalent `Type=Event EventLog!="Windows PowerShell"` alle gebeurtenissen van andere logboeken die geen Windows PowerShell-logboek Hallo retourneren.

Of u kunt andere Booleaanse operator gebruikt, zoals 'Of'. Hallo volgende query retourneert records met welke Hallo EventLog een toepassing of het systeem is.

```
EventLog=Application OR EventLog=System
```

Hallo hierboven query gebruikt, krijgt u vermeldingen voor beide logboeken in Hallo dezelfde set leiden.

Echter, als u hello of door Hallo impliciete en in plaats verwijdert, vervolgens hello volgende query wordt geen queryplan geen resultaten omdat er een logboekvermelding die deel uitmaakt van tooBOTH Logboeken niet. Elke logboekvermelding is tooonly een van twee Hallo-Logboeken geschreven.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Aanvullende filters gebruiken
Hallo retourneert volgende query vermeldingen voor 2 gebeurtenislogboeken voor alle Hallo-computers die gegevens verzonden.

```
EventLog=Application OR EventLog=System
```

![zoekresultaten](./media/log-analytics-log-searches/oms-search-results03.png)

Selecteer een van de Hallo velden of filters wordt Hallo query tooa specifieke computer, met uitzondering van alle andere protocollen beperken. de resulterende query Hallo zou lijken op Hallo volgende.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Dit volgende gelijkwaardige toohello, is vanwege Hallo impliciete AND.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Elke query wordt geëvalueerd in Hallo expliciete volgorde. Opmerking Hallo haakje.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Net als Hallo gebeurtenislogboek veld, kunt u alleen gegevens voor een set specifieke computers ophalen door toe te voegen of. Bijvoorbeeld:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Op deze manier deze query return na Hallo **% CPU-tijd** voor Hallo slechts twee computers geselecteerde.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Veldtypen
Wanneer u filters maakt, moet u Hallo verschillen bij het werken met verschillende typen velden die zijn geretourneerd door het logboek zoekopdrachten begrijpen.

**De doorzoekbare velden** weergeven in blauw weergegeven in de zoekresultaten.  U kunt de doorzoekbare velden in voorwaarden specifieke toohello zoekveld zoals Hallo volgende gebruiken:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**Vrije tekst doorzoekbare velden** grijs in de zoekresultaten worden weergegeven.  Ze kunnen niet worden gebruikt met voorwaarden specifieke toohello zoekveld zoals doorzoekbare velden.  Ze worden alleen bij het uitvoeren van een query op alle gebieden zoals Hallo volgende doorzocht.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Booleaanse operators
Met datetime en numerieke velden, kunt u zoeken naar waarden die *groter is dan*, *minder dan*, en *kleiner dan of gelijk*. U kunt eenvoudig operators zoals >, <>, =, < =,! = in Hallo query zoekbalk.

U kunt een specifiek gebeurtenislogboek opvragen voor een bepaalde periode. Bijvoorbeeld, wordt Hallo afgelopen 24 uur uitgedrukt Hello symbool expressie te volgen.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>met behulp van een Booleaanse operator toosearch
* Typ in het Hallo-zoekveld query`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![zoeken met Booleaanse waarde](./media/log-analytics-log-searches/oms-search-boolean.png)

Hoewel u kunt beheren tijdsinterval grafisch Hallo en meestal kunt u toodo, zijn er voordelen tooincluding een tijdfilter rechtstreeks in het Hallo-query. Bijvoorbeeld: dit goed werkt met dashboards waar u tijd voor elke tegel, ongeacht Hallo Hallo kunt negeren *globale* tijd selector op Hallo dashboardpagina. Zie voor meer informatie [tijd belangrijk is in het Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Bij het filteren door de tijd, houd er rekening mee dat u resultaten voor Hallo krijgen *snijpunt* Hallo twee perioden: Hallo hebt opgegeven in Hallo OMS-portal (S1) en Hallo hebt opgegeven in het Hallo-query (S2).

![snijpunt](./media/log-analytics-log-searches/oms-search-intersection.png)

Dit betekent dat, als hello perioden elkaar niet overlappen, bijvoorbeeld in Hallo OMS-portal waar u desgewenst **deze week** en in Hallo query waarin u definiëren **afgelopen week**, is er geen snijpunt en u won't alle resultaten krijgen.

Vergelijkingsoperators voor Hallo TimeGenerated veld gebruikt, zijn ook nuttig zijn in andere gevallen. Bijvoorbeeld, met numerieke velden.

Bijvoorbeeld opgegeven dat van de beoordeling van de configuratie waarschuwingen Hallo ernstwaarden volgende hebben:

* 0 = informatie
* 1 = waarschuwing
* 2 = kritiek

U kunt doorzoeken op waarschuwingen en kritieke waarschuwingen en informatieve netwerken met de volgende query Hallo ook uitsluiten:

```
Type=ConfigurationAlert  Severity>=1
```


U kunt ook query's bereik gebruiken. Dit betekent dat u Hallo begin en einde bereik van waarden in een reeks kunt opgeven. Bijvoorbeeld, als u wilt dat gebeurtenissen uit Operations Manager-gebeurtenislogboek Hallo waar hello EventID is too2100 groter dan of gelijk zijn, maar niet groter zijn dan 2199, en vervolgens Hallo na query wilt retourneren.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> moet u de syntaxis van de Hallo bereik is Hallo dubbele punt (:) veldwaarde: scheidingsteken en *niet* Hallo gelijkteken (=). Zet de boven- en ondergrenzen einde Hallo van Hallo-bereik tussen vierkante haken en scheiden met twee punten (.).
>
>

## <a name="manipulate-search-results"></a>Zoekresultaten manipuleren
Wanneer u gegevens zoekt, gaat u wilt toorefine uw zoekopdracht en een goede beheerniveau Hallo resultaten hebben. Wanneer resultaten worden opgehaald, kunt u opdrachten tootransform toepassen ze.

Opdrachten in logboekanalyse zoekopdrachten *moet* Volg na het teken van Hallo verticale pipe (|). Een filter moet altijd Hallo eerste deel van een queryreeks. Hallo-gegevensset waarmee u samenwerkt definieert en vervolgens 'doorgesluisd' de resultaten in een opdrachtregel. U kunt vervolgens Hallo pipe tooadd aanvullende opdrachten gebruiken. Dit is los vergelijkbare toohello Windows PowerShell-pijplijn.

In het algemeen Hallo logboekanalyse zoektaal toofollow PowerShell stijl en richtlijnen toomake probeert it vergelijkbare toohello IT-professionals en tooease Hallo leerproces.

Opdrachten hebben namen van termen, zodat u kunt in één oogopslag zien wat ze doen.  

### <a name="sort"></a>Sorteren
Hallo sorteren opdracht kunt u toodefine Hallo sorteervolgorde op een of meer velden. Zelfs als u niet, standaard gebruikt, wordt een tijd aflopende volgorde afgedwongen. de meest recente resultaten Hallo zijn altijd boven Hallo zoekresultaten. Dit betekent dat wanneer u een zoekopdracht met uitvoert `Type=Event EventID=1234` wat daadwerkelijk wordt uitgevoerd voor u is:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Dat is omdat het Hallo-type van de gebruikerservaring die u bekend met in Logboeken bent. Bijvoorbeeld, in de logboeken van Windows hello.

U kunt sorteren toochange Hallo manier resultaten worden geretourneerd. Hallo volgende voorbeelden laten zien hoe dit werkt.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello eenvoudige voorbeelden hierboven ziet u hoe opdrachten werken--ze Hallo vorm van Hallo resultaten gefilterd als resultaat gegeven Hallo wijzigen.

### <a name="limit-and-top"></a>Limiet en boven
Een andere minder bekende opdracht is een LIMIET. De limiet is een PowerShell-achtige term. De limiet is identiek toohello bovenste opdracht. Hallo volgende query's Hallo dezelfde resultaten geretourneerd.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>met behulp van de bovenste toosearch
* Typ in het Hallo-zoekveld query`Type=Event EventID=600 | Top 1`   
    ![Zoek boven](./media/log-analytics-log-searches/oms-search-top.png)

In het Hallo-afbeelding hierboven, zijn er 358 duizend records met gebeurtenis-id = 600. Hallo velden, facetten en filters op Hallo links altijd informatie weergeven over Hallo resultaten geretourneerd *door Hallo filter gedeelte* van Hallo query, die deel uitmaakt Hallo voordat een pipe-teken. Hallo **resultaten** deelvenster alleen resultaat Hallo meest recente 1, omdat Hallo voorbeeldopdracht vorm en getransformeerd Hallo resultaten.

### <a name="select"></a>Selecteer
Hallo SELECT-opdracht gedraagt zich als Select-Object in PowerShell. Het resultaat gefilterde resultaten die niet beschikt over alle hun oorspronkelijke eigenschappen. In plaats daarvan wordt geselecteerd Hallo alleen eigenschappen die u opgeeft.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun een zoeken met de Hallo select-opdracht
1. Typ in zoeken `Type=Event` en klik vervolgens op **Search**.
2. Klik op **+ meer** in een Hallo resultaten tooview alle Hallo-eigenschappen die Hallo resultaten hebben.
3. Selecteer een aantal van deze expliciet en hello wijzigingen in query's te`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![Selecteer zoeken](./media/log-analytics-log-searches/oms-search-select.png)

Met deze opdracht is bijzonder nuttig wanneer u zoeken dat uitvoer toocontrol wilt en kiest alleen Hallo delen van gegevens die echt belangrijk voor uw onderzoek, die vaak geen volledige Hallo-record. Dit is ook handig wanneer de records van verschillende typen hebben *sommige* algemene eigenschappen, maar niet *alle* van hun eigenschappen gelden. De uitvoer genereren die meer toe op een tabel lijkt of geschikt voor tooa CSV-bestand exporteren en vervolgens massaged in Excel.

## <a name="use-hello-measure-command"></a>Hallo meting opdracht gebruiken
METING is een van de meest veelzijdige opdrachten Hallo in logboekanalyse zoekopdrachten. Hiermee kunt u tooapply statistische *functies* tooyour gegevens en statistische resultaten gegroepeerd op een bepaald veld. Er zijn meerdere statistische functies die ondersteuning biedt voor meting.

### <a name="measure-count"></a>Meting count()
Hallo eerste statistische functie toowork met en een van de eenvoudigste toounderstand Hallo Hallo is *count()* functie.

Resultaat is van een zoekopdracht zoals `Type=Event`, ook wel facetten op Hallo linkerkant zoekresultaten filters weer. Hallo filters zien een verdeling van waarden met een bepaald veld voor de Hallo resultaten in Hallo-zoekopdracht uitgevoerd.

![zoeken maateenheid count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Bijvoorbeeld in Hallo bovenstaande u afbeelding ziet Hallo **Computer** veld en geeft aan dat in de Hallo bijna 739 duizend gebeurtenissen in de resultaten hello, 68 uniek en anders waarden voor Hallo **Computer** het veld in deze records. Hallo-tegel bevat alleen Hallo bovenste 5 die zich Hallo meest voorkomende 5 waarden die zijn geschreven in Hallo **Computer** velden), gesorteerd op Hallo aantal documenten dat die specifieke waarde in het veld bevatten. In het Hallo-afbeelding ziet u dat-tussen deze gebeurtenissen bijna 369 duizend – 90 duizend afkomstig zijn van Hallo OpsInsights04.contoso.com computer, 83 duizend van Hallo DB03.contoso.com computer, enzovoort.

Wat gebeurt er als u wilt dat toosee alle waarden, omdat het Hallo-tegel alleen toont alleen Hallo top 5?

Dat is de meting van welke Hallo opdracht kunt doen met de Hallo count() functie. Deze functie heeft geen parameters gebruikt. U zojuist hebt waarop u toogroup door – Hallo wilt Hallo-veld opgeven **Computer** veld in dit geval:

`Type=Event | Measure count() by Computer`

![zoeken maateenheid count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Echter **Computer** is slechts een veld gebruikt *in* elke stukje informatie: Er zijn geen relationele databases die zijn betrokken, en er is geen afzonderlijke **Computer** overal object. NET Hallo waarden *in* Hallo gegevens kunt beschrijven welke entiteit gegenereerd deze, en een aantal andere kenmerken en aspecten van de gegevens in Hallo Hallo daarom term *facet*. U kunt echter alleen ook groeperen op andere velden. Omdat de oorspronkelijke resultaten Hallo bijna 739 duizend gebeurtenissen die zijn doorgesluisd naar Hallo meting opdracht ook een veld met de naam **EventID**, u kunt toepassen Hallo dezelfde techniek toogroup door dat veld en krijgt u een aantal gebeurtenissen dat door de gebeurtenis-id:

```
Type=Event | Measure count() by EventID
```

Als u niet bent geïnteresseerd in Hallo record zelf aantal die een specifieke waarde bevatten, maar in plaats daarvan als u alleen een lijst met Hallo zelf waarden, kunt u toevoegen een *Selecteer* opdracht aan Hallo einde van deze en selecteer Hallo eerste kolom:

```
Type=Event | Measure count() by EventID | Select EventID
```

Vervolgens kunt u meer geavanceerde ophalen en vóór sorteren Hallo resulteert in het Hallo-query of hoeft u alleen op Hallo kolommen in Hallo raster te.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch met behulp van de maateenheid count
* Typ in het Hallo-zoekveld query`Type=Event | Measure count() by EventID`
* Append `| Select EventID` toohello einde van Hallo-query.
* Ten slotte toevoegen `| Sort EventID asc` toohello einde van Hallo-query.

Er zijn een aantal belangrijke punten toonotice en leg de nadruk op:

Eerst Hallo u ziet geen zijn resultaten oorspronkelijke onbewerkte resultaten Hallo meer. In plaats daarvan zijn ze cumulatieve resultaten – in wezen groepen van de resultaten. Dit geen probleem, maar moet u weten dat u bent interactie met een heel andere vorm van gegevens die afwijkt van Hallo oorspronkelijke onbewerkte vorm die wordt gemaakt op Hallo snel als gevolg van Hallo aggregatie/statistische functie.

Tweede, **aantal meten** retourneert Hallo momenteel alleen top 100 verschillende resultaten. Deze limiet niet van toepassing toohello andere statistische functies. U hebt dus meestal toouse een nauwkeurigere filter eerste toosearch nodig voor specifieke items voordat u een meting count() toepassen.

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Hallo max en min-functies gebruiken met Hallo meting opdracht
Er zijn verschillende scenario's waarbij **meting Max()** en **meting zijn** zijn nuttig. Echter, omdat elke functie tegengestelde laten we van elkaar hebt Max() zien en u kunt experimenteren met zijn zelf.

Als u een query voor beveiligingsgebeurtenissen, hebben ze een **niveau** eigenschap die kan verschillen. Bijvoorbeeld:

```
Type=SecurityEvent
```

![zoeken maatregel telling starten](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Als u tooview Hallo hoogste waarde voor alle Hallo beveiliging wilt kunt gebeurtenissen krijgt een gemeenschappelijke Computer Hallo group by-veld, u

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![maximale computer zoeken meting](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Die wordt weergegeven voor Hallo-computers waarop **niveau** records, de meeste van deze hebben ten minste 8, niveau veel had een niveau van 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![maximale zoektijd meting gegenereerd computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Deze functie werkt goed samen met de getallen, maar het werkt ook met DateTime-velden. Laatste is handig toocheck voor Hallo of de meest recente tijdstempel van elk deel van de gegevens die zijn geïndexeerd voor elke computer. Bijvoorbeeld: wanneer is het meest recente beveiligingsgebeurtenis Hallo gerapporteerd voor elke computer?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>De functie Avg. hello gebruiken met Hallo meting opdracht
Hallo Avg() statistische functie gebruikt in combinatie met een meting kunt u toocalculate Hallo gemiddelde waarde van een veld en groep resulteert door Hallo dezelfde of een ander veld. Dit is handig in tal van gevallen, zoals de prestatiegegevens.

We beginnen met de prestatiegegevens. Houd er rekening mee dat OMS momenteel prestatiemeteritems voor Windows- en Linux-machines verzamelt.

toosearch voor *alle* prestatiegegevens, de meest eenvoudige query Hallo is:

```
Type=Perf
```

![Gem. start zoeken](./media/log-analytics-log-searches/oms-search-avg01.png)

Hallo eerste wat u kunt zien is dat Log Analytics u drie perspectieven ziet: lijst ziet u waarin de werkelijke records Hallo achter Hallo grafieken. Tabel waarin een tabellarische weergave van gegevens van prestatiemeteritems; metrische gegevens en geeft en grafieken voor Hallo prestatiemeteritems.

In Hallo afbeelding hierboven zijn er twee sets met velden die zijn gemarkeerd die wijzen op Hallo volgende:

* de eerste set Hallo identificeert naam Windows Prestatiemeter, objectnaam en exemplaarnaam in Hallo queryfilter. Dit zijn Hallo velden die u waarschijnlijk meest worden gebruikt als facetten/filters
* **Tegenwaarde** Hallo werkelijke waarde van Hallo teller. In dit voorbeeld Hallo-waarde is *75*.
* **TimeGenerated** 12:51, in 24-uurs tijdnotatie is.

Hier volgt een overzicht van Hallo metrische gegevens in een grafiek.

![Gem. start zoeken](./media/log-analytics-log-searches/oms-search-avg02.png)

Na het lezen over Hallo Perf record shape en hebben meer informatie over andere zoektechnieken, kunt u meting Avg() tooaggregate gebruiken dit soort numerieke gegevens.

Hier volgt een voorbeeld van een eenvoudige:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Gem. samplevalue zoeken](./media/log-analytics-log-searches/oms-search-avg03.png)

In dit voorbeeld selecteert u Hallo totale CPU-tijd prestatiemeteritem en gemiddelde per Computer. Als u wilt dat toonarrow omlaag uw resultaten tooonly Hallo laatste 6 uur, kunt u Hallo tijd filterbesturingselement gebruiken of Geef in de query als volgt:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>met behulp van de functie Avg. Hallo met Hallo meting opdracht toosearch
* Typ in het Hallo-query in het zoekvak `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

U kunt aggregeren en correleren van gegevens *over* computers. Stel bijvoorbeeld dat u hebt een set van hosts in een bepaald soort farm waar elk knooppunt is gelijk tooany andere en ze alleen alle Hallo hetzelfde type werk en load moet ongeveer in evenwicht doen. U kunt hun items die in een gaan Hello volgende opvragen en gemiddelden ophalen voor de gehele farm Hallo kan ophalen. U kunt starten door te kiezen Hallo computers Hello voorbeeld te volgen:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Nu dat u Hallo computers hebt, wilt u ook alleen tooselect twee prestatie-indicatoren (KPI's): % CPU-gebruik en % vrije schijfruimte. Zo, dat deel van het Hallo-query wordt:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

U kunt nu computers en prestatiemeteritems toevoegen Hello voorbeeld te volgen:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Omdat u een zeer specifieke selectie hebt, Hallo **Avg() meten** opdracht kunt terugkeren Hallo gemiddelde niet door de computer, maar in de farm hello, gewoon door groepering door CounterName. Bijvoorbeeld:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Hiermee krijgt u een handig compacte weergave van een aantal KPI's voor uw omgeving.

![groepering van Search Gem.](./media/log-analytics-log-searches/oms-search-avg04.png)

U kunt eenvoudig hello zoekquery gebruiken in een dashboard. U kan bijvoorbeeld Hallo zoekopdracht opslaan en een dashboard maken vanuit deze met de naam *Web Farm KPI's*. toolearn meer over het gebruik van dashboards, Zie [maken van een aangepast dashboard in logboekanalyse](log-analytics-dashboards.md).

![Search-dashboard, Gem.](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>De functie sum Hallo met Hallo meting opdracht gebruiken
de functie sum Hallo is soortgelijke tooother functies van Hallo meting opdracht. U ziet een voorbeeld over hoe toouse sum-functie op Hallo [W3C IIS-logboeken zoeken in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

U kunt Max() en zijn met de getallen, datums en tijden en tekenreeksen. Met tekenreeksen, ze alfabetische volgorde worden gesorteerd en u eerste en laatste.

U kunt de bladwijzers echter niet gebruiken met iets anders dan numerieke velden. Dit geldt ook tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Hallo percentielfunctie met Hallo meting opdracht gebruiken
Hallo percentielfunctie is vergelijkbaar tooAvg() of bladwijzers in die u het alleen voor numerieke velden gebruiken kunt. U kunt percentiel tussen 1 too99 op een numeriek veld gebruiken. U kunt ook beide **percentiel** en **pct** opdrachten. Hier volgen enkele voorbeelden:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Hallo gebruiken wanneer de opdracht
Hallo waarbij opdracht werkt als een filter, maar deze kan worden toegepast in Hallo pijplijn toofurther filter geaggregeerd resultaten die zijn gemaakt door een opdracht meting – als tegengestelde tooraw resultaten die zijn gefilterd op Hallo begin van een query.

Bijvoorbeeld:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

U kunt een andere pipe toevoegen ' | ' teken en het Hallo waar opdracht tooonly computers waarvan gemiddelde CPU hoger is dan 80% met krijgen Hallo volgende voorbeeld:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Als u bekend met de Microsoft System Center - Operations Manager bent, kunt u Hallo zien wanneer de opdracht in termen van management pack. Als voorbeeld Hallo was van een regel, Hallo eerste deel van de query Hallo worden Hallo gegevensbron en Hallo waar opdracht detectie van conditie voor Hallo zou zijn.

U kunt query hello gebruiken als een tegel in **mijn Dashboard**, als een monitor van sorteerbewerkingen toosee wanneer computer CPU's zijn te veel gebruikt. toolearn meer informatie over dashboards, Zie [maken van een aangepast dashboard in logboekanalyse](log-analytics-dashboards.md). U kunt ook maken en dashboards met Hallo mobiele app gebruiken. Zie voor meer informatie [OMS mobiele App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). In Hallo onder twee tegels Hallo volgende afbeelding ziet u Hallo monitor een lijst weergegeven en als een getal. In wezen altijd gewenste Hallo nummer toobe nul en Hallo lijst toobe leeg. Anders geeft een meldingsvoorwaarde aan. Indien nodig, kunt u deze tootake kijken welke computers zijn onder druk.

![mobiele dashboard](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Hallo gebruiken in de operator
Hallo *IN* -operator, samen met *NOT IN* kunt u toouse subsearches die zoekopdrachten met een andere zoekopdracht als argument. Ze zijn opgenomen in de accolades {} binnen een andere *primaire* of *buitenste* zoeken. Hallo-resultaat van een subsearch, vaak een lijst met verschillende resultaten, wordt vervolgens gebruikt als argument voor de primaire zoekactie.

U kunt subsearches toomatch subsets van uw gegevens dat u een beschrijving kan niet rechtstreeks in een zoekexpressie, maar die kunnen worden gegenereerd vanuit een zoekopdracht kunt gebruiken. Bijvoorbeeld, als u geïnteresseerd bent in het gebruik van een zoekopdracht toofind alle gebeurtenissen uit *computers met ontbrekende beveiligingsupdates*, moet u een subsearch die eerst dat identificeert toodesign *computers met ontbrekende beveiligingsupdates*  voordat er gebeurtenissen behoren toothose hosts.

Ja, u kan express *computers momenteel ontbreekt vereiste beveiligingsupdates* Hello query te volgen:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Zodra u Hallo lijst hebt, kunt u Hallo zoeken als een binnenste zoeken toofeed Hallo lijst van computers in een buitenste (primaire) zoeken die wordt gezocht naar gebeurtenissen voor deze computers. U doen dit door Hallo binnenste zoeken insluitende accolades en de resultaten als mogelijke waarden voor een filterveld in buitenste Hallo-search met behulp van de IN-operator Hallo voeding. Hallo query zou zijn vergelijkbaar met:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Kennisgeving Hallo tijd filter dat wordt gebruikt in de interne zoekopdracht Hallo omdat Hallo System Update-evaluatie maakt een momentopname van alle computers ook elke 24 uur. U maken Hallo binnenste query meer licht en nauwkeurige, zoekt alleen naar een dag. Hallo buitenste zoeken in plaats daarvan maakt gebruik van Tijdselectie Hallo Hallo-gebruikersinterface, ophalen van gebeurtenissen van Hallo afgelopen 7 dagen. Zie [Booleaanse operators](#boolean-operators) voor meer informatie over tijd operators.

Omdat u echt alleen gebruik Hallo resultaten van de binnenste zoekopdracht Hallo als de filterwaarde van een voor een outer Hallo, kunt u opdrachten in een buitenste zoeken Hallo nog steeds toepassen. U kunt bijvoorbeeld nog steeds groep Hallo hierboven gebeurtenissen met een andere meting-opdracht:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in03-revised.png)

In het algemeen wilt u dat uw interne query tooexecute snel omdat logboekanalyse aan servicezijde time-outs voor het en ook tooreturn een kleine hoeveelheid resultaten heeft. Als interne query Hallo meer resultaten oplevert, Hallo resultatenlijst afgekapt, die kan veroorzaken Hallo buitenste zoeken tooreturn onjuiste resultaten.

Een andere regel is die Hallo binnenste zoekopdracht moet momenteel tooprovide *geaggregeerde* resultaten. Met andere woorden, deze moet bevatten een *meting* opdracht; u kan niet op dit moment onbewerkte resultaten in een buitenste zoekopdracht feed.

Ook kan er slechts één IN-operator en het laatste filter Hallo in Hallo-query moet worden. Meerdere IN operators kunnen niet worden of zou – hierdoor in principe kan meerdere subsearches uitgevoerd: Hallo belangrijk punt wordt die slechts één sub/interne zoekopdracht is mogelijk dat elke buitenste zoeken.

Zelfs met deze limieten IN kunnen veel soorten gecorreleerde zoekopdrachten en kunt u toodefine iets dergelijks toogroups zoals computers, gebruikers of bestanden – ongeacht Hallo velden in uw gegevens bevatten. Hier vindt u meer voorbeelden:

**Alle updates ontbreken van computers waarop automatische updates-instelling wordt uitgeschakeld**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Alle foutgebeurtenissen van computers met SQL Server (= waar SQL-analyse is uitgevoerd)**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Alle beveiligingsgebeurtenissen van computers die domeincontrollers (= waar AD analyse is uitgevoerd)**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Die andere accounts zich aangemeld hebben toohello dezelfde computers waarbij BACONLAND\jochan account heeft aangemeld?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Gebruik afzonderlijke opdracht Hallo
Als de naam van de Hallo wordt voorgesteld, biedt deze opdracht een lijst met verschillende waarden voor een veld. Het is verrassend eenvoudige maar wel handig. Hallo die dezelfde kan worden verkregen met meting count() opdracht ook, zoals hieronder wordt weergegeven.

```
Type=Event | Measure count() by Computer
```

![Voorbeeld van de opdracht DISTINCT zoeken](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Als u geïnteresseerd bent in een lijst van de afzonderlijke waarden en niet Hallo aantal documenten waarvoor die waarden, kan vervolgens DISTINCT evenwel schonere en gemakkelijker tooread uitvoer en kortere syntaxis, zoals hieronder wordt weergegeven.

```
Type=Event | Distinct Computer
```
![Voorbeeld van de opdracht DISTINCT zoeken](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Hallo countdistinct functie gebruiken met Hallo meting opdracht
Hallo countdistinct functie telt Hallo aantal afzonderlijke waarden in elke groep. Het kan bijvoorbeeld worden gebruikt toocount Hallo aantal unieke computers melden voor elk Type:

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Hallo meting interval opdracht gebruiken
Met bijna Realtime prestatiegegevens verzamelen, kunt u verzamelen en visualiseren van elk prestatiemeteritem in logboekanalyse. Gewoon invoeren Hallo query **Type: Perf** duizenden metrische grafieken op basis van Hallo aantal items en servers in uw omgeving Log Analytics wordt geretourneerd. Met metrische aggregatie op aanvraag, kunt u bekijken op Hallo algemene metrische gegevens in uw omgeving op een hoog niveau en diepgaand naar meer gedetailleerde gegevens als nodig is voor.

Stel dat u wilt dat tooknow wat Hallo gemiddelde CPU is voor alle computers. Bekijkt hello gemiddelde CPU voor elke computer mogelijk niet meer nuttig zijn omdat resultaten kunnen ophalen vloeiend moeten worden gemaakt. toolook naar meer informatie, u kunt samenvoegen in uw resultaat in een kleinere tijd venster segmenten gedownload en zoek een tijdreeks over verschillende dimensies. Bijvoorbeeld, kunt u uitvoeren Hallo per uur gemiddelde CPU-gebruik op alle computers als volgt:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![gemiddelde interval meting](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Standaard worden deze resultaten worden weergegeven in een lijndiagram met meerdere reeksen interactieve.  Dit diagram ondersteunt reeks schakelen (met y-as schaling aanpassen), zoomen en aanwijzen.  Hallo weergave tabeloptie nog steeds beschikbaar voor het weergeven van Hallo onbewerkte gegevens, indien nodig.

U kunt ook andere velden groeperen. In dit voorbeeld ik zoek alle Hallo % prestatiemeteritems voor een specifieke computer en tooknow wat is er elk uur 70 percentielen Hallo van elke teller wilt:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Een ding toonote is deze query's zijn niet beperkt tooperformance tellers. U kunt deze toepassen tooany metriek. In dit voorbeeld zoek ik op de W3C-IIS-logboeken. Ik wil tooknow wat Hallo maximale tijd die nodig is tijdens een interval van 5 minuten voor het verwerken van elke aanvraag is:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Gebruik van meerdere statistische functies in één query
U kunt meerdere cumulatieve componenten opgeven in de opdracht van een meting.  Elk criterium kan alias onafhankelijk zijn.  Als er geen een alias Hallo resulterende opgegeven is veldnaam zich Hallo statistische functie die is gebruikt (dat wil zeggen ' avg(CounterValue)' voor avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Hier volgt nog een voorbeeld:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over logboek zoekopdrachten:

* Gebruik [aangepaste velden in logboekanalyse](log-analytics-custom-fields.md) tooextend logboek zoekopdrachten.
* Bekijk Hallo [logboekanalyse Meld zoeken verwijzing](log-analytics-search-reference.md) tooview alle Hallo velden en beschikbaar zijn in logboekanalyse facetten zoeken.
