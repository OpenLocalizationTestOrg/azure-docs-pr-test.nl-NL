---
title: Log Analytics aaaAzure zoeken verwijzing | Microsoft Docs
description: Hallo logboekanalyse zoeken verwijzing Hallo zoektaal worden beschreven en Hallo algemene query syntaxis-opties die u gebruiken kunt wanneer u gegevens zoeken en filteren van expressies toohelp Beperk uw zoekopdracht.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Log Analytics verwijzing zoeken

>[!NOTE]
> Dit artikel wordt beschreven logboek zoekopdrachten met het huidige querytaal Hallo in logboekanalyse.  Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en u dient te raadplegen[Naslaggids voor de nieuwe taal Hallo Hallo](https://go.microsoft.com/fwlink/?linkid=856079).

Hallo beschrijft sectie van de volgende documentatie over zoektaal Hallo algemene query syntaxis-opties die u gebruiken kunt wanneer u gegevens zoeken en filteren van expressies toohelp Beperk uw zoekopdracht. Hierin worden ook opdrachten die u, tootake actie op Hallo-gegevens opgehaald gebruiken kunt.

U kunt lezen over Hallo velden geretourneerd in zoekopdrachten en Hallo facetten waarmee u lees meer over vergelijkbare categorieën van gegevens in Hallo [veld zoeken en facet verwijzen naar de sectie](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Algemene querysyntaxis
Hallo-syntaxis voor algemene query's is als volgt:

```
filterExpression | command1 | command2 …
```

Hallo filterexpressie (`filterExpression`) Hallo 'where'-voorwaarde voor Hallo query definieert. Hallo opdrachten toohello resultaten geretourneerd door de query Hallo van toepassing. Meerdere opdrachten moeten worden gescheiden door Hallo sluisteken (|).

### <a name="general-syntax-examples"></a>Voorbeelden van de algemene syntaxis
Voorbeelden:

```
system
```

Deze query retourneert resultaten met Hallo word *system* in elk veld dat is geïndexeerd voor volledige tekst of voorwaarden zoeken.

> [!NOTE]
> Niet alle velden op deze manier worden geïndexeerd, maar de meest voorkomende tekstuele velden (zoals beschrijvingen en namen) meestal Hallo zijn.
>
>

```
system error
```

Deze query retourneert resultaten die Hallo woorden bevatten *system* en *fout*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Deze query retourneert resultaten die Hallo woorden bevatten *system* en *fout*. Vervolgens worden de resultaten Hallo gesorteerd op Hallo *ManagementGroupName* veld (in oplopende volgorde), en vervolgens op Hallo *TimeGenerated* veld (in aflopende volgorde). Het duurt enige Hallo eerste 10 resultaten.

> [!IMPORTANT]
> Alle veldnamen Hallo en Hallo waarden voor de tekenreeks en tekstvelden Hallo zijn hoofdlettergevoelig.
>
>

## <a name="filter-expressions"></a>Filterexpressies
Hallo volgende subsecties worden uitgelegd Hallo filterexpressies.

### <a name="string-literals"></a>Letterlijke tekenreeks
Een letterlijke tekenreeks is een tekenreeks die niet wordt herkend door Hallo parser als een sleutelwoord of een vooraf gedefinieerde gegevenstype (bijvoorbeeld een getal of een datum).

Voorbeelden:

```
These all are string literals
```

Deze query zoekt naar resultaten die exemplaren van alle vijf woorden bevatten. een zoekopdracht complexe tekenreeks tooperform plaatst u Hallo tekenreeks tussen aanhalingstekens. Bijvoorbeeld:

```
"Windows Server"
```

Dit retourneert alleen resultaten met de exacte overeenkomsten voor *Windows Server*.

### <a name="numbers"></a>Cijfers
Hallo-parser ondersteunt Hallo decimal integer en syntaxis van de drijvende-nummer voor numerieke velden.

Voorbeelden:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Datums en tijden
Elk onderdeel van de gegevens in Hallo systeem heeft een *TimeGenerated* eigenschap Hallo oorspronkelijke datum en tijd van de record Hallo vertegenwoordigt. Bepaalde typen gegevens kunnen aanvullende datum- en tijdvelden hebben (bijvoorbeeld *LastModified*).

Hallo tijdlijn **grafiek/tijd** selector in Azure-logboekanalyse toont een distributie van resultaten gedurende een bepaalde periode (volgens toohello huidige query wordt uitgevoerd). Dit is gebaseerd op Hallo *TimeGenerated* veld. Datum en tijd velden hebben een specifieke tekenreeks-indeling die kan worden gebruikt in query's toorestrict Hallo query tooa bepaald tijdsbestek. U kunt ook de syntaxis toorefer toorelative tijdsintervallen (bijvoorbeeld ' tussen drie dagen geleden en 2 uur geleden').

Hallo volgen geldig vormen van de syntaxis voor datums en tijden:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Bijvoorbeeld:

```
TimeGenerated:2013-10-01T12:20
```

Hallo vorige opdracht retourneert alleen de records met een *TimeGenerated* waarde exact 12:20 op 1 oktober 2013.

Hallo-parser ook Hallo symbool datum/tijd-waarden ondersteunt, nu. (Het lijkt onwaarschijnlijk dat dit geen resultaten leidt tot omdat gegevens niet worden aanbrengen via Hallo-systeem dat snelle.)

Deze voorbeelden zijn toouse bouwstenen voor relatieve en absolute datums. Hallo in de volgende drie subsecties, ziet u hoe toouse in meer geavanceerde filters, met voorbeelden die de relatieve datumbereiken gebruiken.

### <a name="datetime-math"></a>Math datum/tijd
Hallo datum/tijd rekenkundige operatoren toooffset gebruiken of afronden Hallo datum/tijd-waarde, met behulp van eenvoudige datum/tijd-berekeningen.

Syntaxis:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Operator | Beschrijving |
| --- | --- |
| / |Rondt datum/tijd toohello opgegeven eenheid. Bijvoorbeeld, nu / dag Rondt de huidige datum/tijd-toomidnight Hallo Hallo huidige dag. |
| + of - |Offsets datum/tijd door Hallo opgegeven aantal eenheden. Bijvoorbeeld, nu + 1 uur worden verschoven Hallo huidige datum/tijd van één uur vooruit. 2013-10-01T12:00-10 dagen worden verschoven Hallo Date-waarde terug 10 dagen. |

U kunt Hallo datum/tijd rekenkundige operatoren elkaar koppelen. Bijvoorbeeld:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Hallo bevat volgende tabel Hallo ondersteund datum/tijd-eenheden.

| Datum/tijd-eenheid | Beschrijving |
| --- | --- |
| JAAR, JAAR |Rondt toocurrent jaar of verschuivingen door Hallo opgegeven aantal jaren. |
| MAAND MAANDEN |Rondt toocurrent maand of verschuivingen door Hallo opgegeven aantal maanden. |
| DAG, DAGEN, DATUM |Rondt toocurrent dag van de maand Hallo of verschuivingen door Hallo opgegeven aantal dagen. |
| UUR, UREN |Rondt toocurrent uur of verschuivingen door Hallo opgegeven aantal uren. |
| MINUUT, MINUTEN |Rondt toocurrent minuut of verschuivingen door Hallo opgegeven aantal minuten. |
| TEN TWEEDE SECONDEN |Rondt toocurrent tweede of worden verschoven Hallo opgegeven aantal seconden. |
| MILLISECONDE MILLISECONDEN MILLI, MILLIS |Rondt toocurrent milliseconde of verschuivingen door Hallo opgegeven tijd in milliseconden. |

### <a name="field-facets"></a>Veld facetten
U kunt met behulp van veld facetten Hallo zoekcriterium voor specifieke velden en hun precieze waarden opgeven. Dit wijkt af van het schrijven van query's 'vrije tekst' voor verschillende voorwaarden in de gehele index Hallo. U hebt al gezien deze techniek in verschillende voorgaande voorbeelden. Hallo hieronder vindt u complexere voorbeelden.

**Syntaxis**

```
field:value
```

```
field=value
```

**Beschrijving**

Zoekopdrachten Hallo veld voor het Hallo-specifieke waarde. Hallo-waarde is een letterlijke tekenreeks, getal, of datum en tijd.

Bijvoorbeeld:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Syntaxis**

*veld > waarde*

*veld < waarde*

*veld > = waarde*

*veld < = waarde*

*veld! = waarde*

**Beschrijving**

Biedt vergelijkingen.

Bijvoorbeeld:

```
TimeGenerated>NOW+2HOURS
```

**Syntaxis**

```
field:[from..to]
```

**Beschrijving**

Biedt bereik facetten.

Bijvoorbeeld:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Hallo **IN** sleutelwoord kunt u tooselect uit een lijst met waarden. Afhankelijk van Hallo syntaxis die u gebruikt, kan dit een eenvoudige lijst met waarden die u opgeeft, of een lijst met waarden van een aggregatie worden.

Syntaxis 1:

```
field IN {value1,value2,value3,...}
```

Deze syntaxis kunt u alle waarden in een eenvoudige lijst tooinclude.



Voorbeelden:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Syntaxis 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Deze syntaxis kunt u toocreate een aggregatie. U kunt vervolgens Hallo lijst met waarden feed vanuit die verwijst naar een andere outer (primaire) zoeken die er ongeveer voor gebeurtenissen met deze waarde uitziet. U doen dit door Hallo binnenste zoeken insluitende accolades en de resultaten als mogelijke waarden voor een veld in Hallo buitenste zoeken met behulp van de IN-operator Hallo voeding.

Interne query-voorbeeld: *computers momenteel ontbrekende beveiligingsupdates* Hello aggregatie query te volgen:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

Hallo laatste querybewerking waarmee wordt gezocht naar *alle Windows-gebeurtenissen voor computers die momenteel ontbrekende beveiligingsupdates* lijkt op Hallo volgende:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contains
Hallo **bevat** sleutelwoord kunt u toofilter voor records met een veld dat een opgegeven tekenreeks bevat. Dit is hoofdlettergevoelig, werkt alleen met tekenreeksvelden en mag escape-tekens bevatten.

Syntaxis:

```
field:contains("string")
```

Voorbeeld:

```
Type:contains("Event")
```

Dit resulteert in records met een type dat Hallo tekenreeks bevat 'Gebeurtenis'. Voorbeelden zijn onder meer **gebeurtenis**, **SecurityEvent**, en **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Reguliere expressies
U kunt een zoekcriterium voor een veld met een reguliere expressie opgeven met behulp van Hallo **Regex** sleutelwoord. Zie voor een volledige beschrijving van Hallo syntaxis kunt u in reguliere expressies [met reguliere expressies toofilter logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches-regex.md).

Syntaxis:

```
field:Regex("Regular Expression")
```

Voorbeeld:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Logische operators
Hallo query talen ondersteunen Hallo logische operators (*en*, *of*, en *niet*) en hun C-stijl-aliassen (*&&*,  *||* , en *!*respectievelijk). U kunt deze operators haakjes toogroup.

Voorbeelden:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

U kunt de logische operator Hallo voor Hallo op het hoogste niveau filter argumenten weglaten. In dit geval wordt Hallo AND-operator verondersteld.

| Filterexpressie | Gelijkwaardige te|
| --- | --- |
| systeemfout |systeem en opstaan |
| systeem 'Windows Server' of ernst: 1 |systeem- en ('Windows Server' of ernst: 1) |

### <a name="wildcarding"></a>Gebruik van jokertekens
Hallo-querytaal ondersteunt het gebruik van hello ( \* ) teken te vertegenwoordigen een of meer tekens voor een waarde in een query.

Voorbeeld:

 Alle computers met 'SQL' niet vinden in het Hallo-naam, bijvoorbeeld 'Redmond SQL'.

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> Op dit moment worden niet jokertekens gebruikt binnen offertes. Bijvoorbeeld, het Hallo-bericht `"*This text*"` Hallo overweegt (\*) gebruikt als een letterlijke waarde (\*) teken.


## <a name="commands"></a>Opdrachten


Hallo opdrachten toepassing toohello resultaten die door Hallo query zijn geretourneerd. Gebruik Hallo pipe (|) teken tooapply een opdracht toohello resultaten opgehaald. Meerdere opdrachten moeten worden gescheiden door sluisteken Hallo.

> [!NOTE]
> Namen van opdrachten kunnen worden geschreven in hoofdletters of kleine letters, in tegenstelling tot het Hallo-veldnamen en Hallo-gegevens.
>
>

### <a name="sort"></a>Sorteren
Syntaxis:

    sort field1 asc|desc, field2 asc|desc, …

Resultaten worden gesorteerd Hallo op bepaalde velden. Hallo asc/desc achtervoegsel toosort Hallo resultaten in oplopende of aflopende volgorde is optioneel. Als dit wordt weggelaten, Hallo *asc* sorteervolgorde wordt verondersteld. Voor Hallo **TimeGenerated** veld *desc* wordt uitgegaan van sorteervolgorde, zodat deze de meest recente resultaten Hallo eerst standaard retourneert.

### <a name="toplimit"></a>Top/limiet
Syntaxis:

    top number


    limit number
Limieten Hallo antwoord toohello bovenste N resultaten.

Voorbeeld:

    Type:Alert errors detected | top 10

Retourneert Hallo top 10 van overeenkomende resultaten.

### <a name="skip"></a>Overslaan
Syntaxis:

    skip number

Slaat het Hallo aantal resultaten weergegeven.

Voorbeeld:

    Type:Alert errors detected | top 10 | skip 200

Retourneert de bovenste 10 overeenkomende resultaten vanaf resultaat 200.

### <a name="select"></a>Selecteer
Syntaxis:

    select field1, field2, ...

Beperkt resultaten toohello velden die u kiest.

Voorbeeld:

    Type:Alert errors detected | select Name, Severity

Limieten Hallo velden van de geretourneerde resultaten te*naam* en *ernst*.

### <a name="measure"></a>meting
Hallo *meting* opdracht gebruikte tooapply statistische functies toohello onbewerkte zoekresultaten is. Dit is zeer nuttig tooget *groeperen op* weergaven over Hallo-gegevens. Als u Hallo meting opdracht, wordt een tabel met cumulatieve resultaten weergegeven in logboekanalyse zoeken.

**Syntaxis:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Hallo resultaten door aggregeert *groupField*, en meetwaarden worden geaggregeerd Hallo berekend op basis van *aggregatedField*.

| Statistische functie van meting | Beschrijving |
| --- | --- |
| *de statistische functie* |Hallo-naam van de statistische functie hello (hoofdlettergevoelig). Hallo volgende statistische functies worden ondersteund: aantal, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, percentiel ## of PCT ## (## is een getal tussen 1 en 99). |
| *aggregatedField* |Hallo-veld dat is worden geaggregeerd. Dit veld is optioneel voor de statistische functie COUNT hello, maar heeft toobe een bestaand numeriek veld voor de som, MAX, MIN, AVG, STDEV, percentiel ## of PCT ## (## is een getal tussen 1 en 99). Hallo aggregatedField kan ook Hallo worden **uitbreiden** ondersteunde functies. |
| *fieldAlias* |Hallo (optioneel) alias voor Hallo cumulatieve waarde berekend. Als niet wordt opgegeven, is Hallo veldnaam **AggregatedValue**. |
| *groupField* |Hallo-naam van Hallo-veld dat Hallo resultaatset worden gegroepeerd per. |
| *Interval* |de tijdsinterval Hallo Hallo indeling:**nnnNAME**. **nnn**Hallo positief geheel getal is. **NAAM** Hallo interval naam. Het interval namen zijn hoofdlettergevoelig en omvatten: MILLISECONDE [S] [S] seconde minuut [S] [S] uur dag [S] [S] maand en jaar [S]. |

optie voor Hallo interval kan alleen worden gebruikt in velden voor datum/tijd-groep (zoals *TimeGenerated* en *TimeCreated*). Op dit moment is dit niet wordt afgedwongen door Hallo-service, maar veld zonder datum/tijd die wordt doorgegeven toohello back-end zorgt ervoor dat een runtime-fout. Wanneer Hallo schemavalidatie is geïmplementeerd, weigert Hallo service API query's die gebruikmaken van velden zonder datum/tijd voor interval voor aggregatie. huidige Hallo *meting* implementatie ondersteunt groepering interval voor een statistische functie.

Als Hallo BY-component wordt weggelaten, maar een interval dat is opgegeven (als een tweede syntaxis), Hallo *TimeGenerated* veld wordt aangenomen dat standaard.

Voorbeelden:

**Voorbeeld 1**

    Type:Alert | measure count() as Count by ObjectId

Groepen Hallo waarschuwingen per *ObjectID*, en het aantal waarschuwingen voor elke groep Hallo berekent. Hallo cumulatieve waarde geretourneerd als Hallo *aantal* veld (alias).

**Voorbeeld 2**

    Type:Alert | measure count() interval 1HOUR

Groepen Hallo waarschuwingen door 1 uur met behulp van Hallo *TimeGenerated* veld en retourneert Hallo aantal waarschuwingen in elk interval.

**Voorbeeld 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Hetzelfde als het vorige voorbeeld hello, maar met een alias geaggregeerd veld (*AlertsPerHour*).

**Voorbeeld 4**

    * | meting count() door TimeCreated interval 5DAYS

Hallo resultaten met behulp van Hallo gegroepeerd 5 dagintervallen *TimeCreated* veld en retourneert Hallo aantal resultaten in elk interval.

**Voorbeeld 5**

    Type:Alert | measure max(Severity) by WorkflowName

Groepen Hallo waarschuwingen met de naam van de werkbelasting en retourneert Hallo maximale ernst van waarschuwing waarde voor elke werkstroom.

**Voorbeeld 6**

    Type:Alert | measure min(Severity) by WorkflowName

Hetzelfde als het vorige voorbeeld hello, maar met Hallo *min* functie geaggregeerd.

**Voorbeeld 7**

    Type:Perf | measure avg(CounterValue) by Computer

Perf gegroepeerd op de computer en berekent de gemiddelde hello (Gem.).

**Voorbeeld 8**

    Type:Perf | measure sum(CounterValue) by Computer

Hetzelfde als het vorige voorbeeld hello, maar gebruikt *som*.

**Voorbeeld 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Hetzelfde als het vorige voorbeeld hello, maar gebruikt *stddev*.

**Voorbeeld 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Hetzelfde als het vorige voorbeeld hello, maar gebruikt *percentile70*.

**Voorbeeld 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Hetzelfde als het vorige voorbeeld hello, maar gebruikt *pct70*. Houd er rekening mee dat *PCT ##* is alleen een alias voor *percentiel ##* functie.

**Voorbeeld 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Perf eerst gegroepeerd op de Computer en vervolgens CounterName en berekent Hallo gemiddelde (Gem.).

**Voorbeeld 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Hiermee haalt u Hallo bovenste vijf werkstromen met Hallo kunt u het maximum aantal waarschuwingen.

**Voorbeeld 14**

    * | meting countdistinct(Computer) per Type

Telt het aantal unieke computers melden voor elk Type Hallo.

**Voorbeeld 15**

    * | meting countdistinct(Computer) Interval 1 uur

Telt het aantal unieke computers melden voor elk uur Hallo.

**Voorbeeld 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

Percentage processortijd door Computer groepen en retourneert Hallo gemiddelde voor elk uur.

**Voorbeeld 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

W3CIISLog gegroepeerd op methode en retourneert Hallo maximale voor elke 5 minuten.

**Voorbeeld 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Groepen % processortijd van de computer, en retourneert Hallo minimum, gemiddelde 75e percentiel en maximum voor elk uur.

**Voorbeeld 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Groepen percentage processortijd eerst op de computer en vervolgens op exemplaar naam en retourneert Hallo minimum, gemiddelde, 75e percentiel en de maximale voor elk uur.

**Voorbeeld 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Berekent de Hallo maximum van schrijfbewerkingen per minuut voor elke schijf op uw computer.

### <a name="where"></a>waar
Syntaxis:

```
**where** AggregatedValue>20
```

Kan alleen worden gebruikt na een *meting* opdracht toofurther filter Hallo geaggregeerd resulteert dat Hallo *meting* aggregatiefunctie heeft geproduceerd.

Voorbeelden:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Ontdubbeling
Syntaxis:

    Dedup FieldName

Retourneert de eerste Hallo-document vinden voor elke unieke waarde van het opgegeven veld Hallo.

Voorbeeld:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

In dit voorbeeld retourneert één gebeurtenis (laatste gebeurtenis Hallo) per EventID.

### <a name="join"></a>Koppelen
Joins Hallo resultaten van twee query's tooform één resultaatset.  Ondersteunt meerdere join-typen die zijn beschreven in Hallo Volg tabel.

| Type samenvoeging | Beschrijving |
|:--|:--|
| interne | Alleen records met een overeenkomende waarde in beide query's retourneren. |
| buitenste | Alle records van beide query's worden geretourneerd.  |
| Links  | Alle records uit links query en overeenkomende records uit de juiste query retourneren. |


- Joins bieden momenteel geen ondersteuning voor query's met Hallo **IN** sleutelwoord, Hallo **meting** opdracht of Hallo **uitbreiden** opdracht als deze is bedoeld voor een veld van de juiste query Hallo.
- U kunt slechts één veld momenteel opnemen in een join.
- Een enkele zoekactie mag niet meer dan één join inhouden.

**Syntaxis**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Voorbeelden**

tooillustrate hello verschillende join-typen, u kunt lid worden van een gegevenstype verzameld van een aangepaste logboek MyBackup_CL aangeroepen met Hallo heartbeat voor elke computer.  Deze gegevenstypen hebben Hallo volgt gegevens.

`Type = MyBackup_CL`

| TimeGenerated | Computer | LastBackupStatus |
|:---|:---|:---|
| 4/20/2017 01:26:32.137 AM | Srv01.contoso.com | Geslaagd |
| 4/20/2017 02:13:12.381 AM | SRV02.contoso.com | Geslaagd |
| 4/20/2017 02:13:12.381 AM | srv03.contoso.com | Fout |

`Type = Hearbeat`(Alleen een subset van de velden die worden weergegeven)

| TimeGenerated | Computer | ComputerIP |
|:---|:---|:---|
| 21-4/2017 12:01:34.482 PM | Srv01.contoso.com | 10.10.100.1 |
| 21-4/2017 12:02:21.916 PM | SRV02.contoso.com | 10.10.100.2 |
| 21-4/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>inner join

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Retourneert Hallo volgen records als Hallo computer veld overeenkomt met voor beide gegevenstypen.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Geslaagd | 21-4/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| SRV02.contoso.com | 4/20/2017 02:13:12.381 AM | Geslaagd | 21-4/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |


#### <a name="outer-join"></a>outer join

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Retourneert Hallo records voor beide gegevenstypen te volgen.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Geslaagd  | 21-4/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| SRV02.contoso.com | 4/20/2017 02:14:12.381 AM | Geslaagd  | 21-4/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 01:33:35.974 AM | Fout  | 21-4/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 21-4/2017 12:01:47.373 PM | 10.10.100.2 | Heartbeat |



#### <a name="left-join"></a>linker join

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Retourneert de volgende records uit MyBackup_CL met een overeenkomende velden uit de Heartbeat Hallo.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Geslaagd | 21-4/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| SRV02.contoso.com | 4/20/2017 02:13:12.381 AM | Geslaagd | 21-4/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 02:13:12.381 AM | Fout | | | |


### <a name="extend"></a>Breid uit
Hiermee kunt u toocreate runtime-velden in query's. Houd er rekening mee dat de runtime-velden kunnen niet worden gebruikt met Hallo meting opdracht tooperform aggregatie.

**Voorbeeld 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Toont gewogen score aanbeveling voor aanbevelingen voor SQL-evaluatie.

**Voorbeeld 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Geeft de waarde van het prestatiemeteritem in kB in plaats van bytes.

**Voorbeeld 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Kan worden geschaald Hallo waarde van WireData TotalBytes, zodat alle resultaten tussen 0 en 100 liggen zijn.

**Voorbeeld 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Labels Perf teller waarden bevat die kleiner is dan 50 procent als laag en anderen zo hoog.

**Voorbeeld 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Berekent de Hallo maximum van schrijfbewerkingen per minuut voor elke schijf op uw computer.

**Ondersteunde functies**

| Functie | Beschrijving | Syntaxisvoorbeelden |
| --- | --- | --- |
| ABS |Retourneert Hallo absolute waarde van Hallo opgegeven waarde of functie. |`abs(x)` <br> `abs(-5)` |
| BOOGCOS |Retourneert de arccosinus van een waarde of een functie. |`acos(x)` |
| en |Retourneert de waarde true en alleen als alle van de operands tootrue evalueren. |`and(not(exists(popularity)),exists(price))` |
| ASIN |Retourneert de arcsinus van een waarde of een functie. |`asin(x)` |
| BOOGTAN |Retourneert de arctangens van een waarde of een functie. |`atan(x)` |
| BOOGTAN2 |Hallo hoek ten gevolge van Hallo conversie van Hallo vierkant coördinaten x, y-coördinaten voor toopolar retourneert. |`atan2(x,y)` |
| cbrt |Hoofdmap van de kubus. |`cbrt(x)` |
| ceil |Rondt up tooan geheel getal. |`ceil(x)`  <br> `ceil(5.6)`Retourneert 6 |
| CO 's |Retourneert de cosinus van een hoek. |`cos(x)` |
| COSH |Retourneert de hyperbolische cosinus van een hoek. |`cosh(x)` |
| def |Afkorting voor standaard. Retourneert Hallo de waarde van veld"'. Als Hallo veld niet bestaat, retourneert Hallo standaardwaarde opgegeven en de eerste waarde Hallo oplevert waar: `exists()==true`. |`def(rating,5)`. Deze functie def() resultaat Hallo classificatie, of als er geen classificatie is opgegeven in Hallo document, 5. <br> `def(myfield, 1.0)`is gelijk te`if(exists(myfield),myfield,1.0)`. |
| graden |Converteert radialen toodegrees. |`deg(x)` |
| div |`div(x,y)`verdeelt x y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| distributie |Retourneert Hallo afstand tussen twee aanvalsvectoren, (punten) in een n-dimensionale ruimte. Duurt in Hallo power, plus twee of meer exemplaren van ValueSource en berekent de afstand tussen de twee vectoren Hallo Hallo. Elke ValueSource moet een getal zijn. Er moet een even aantal exemplaren van ValueSource doorgegeven en Hallo-methode wordt ervan uitgegaan dat eerste helft Hallo Hallo eerste vector vertegenwoordigen en de tweede helft Hallo Hallo tweede vector vertegenwoordigen. |`dist(2, x, y, 0, 0)`Berekent de Hallo Euclidean afstand tussen (0,0) en (x, y) voor elk document. <br> `dist(1, x, y, 0, 0)`Berekent de Hallo Manhattan (taxi) afstand tussen (0,0) en (x, y) voor elk document. <br> `dist(2,,x,y,z,0,0,0)`Euclidean afstand tussen (0,0,0) en (x, y, z) voor elk document.<br>`dist(1,x,y,z,e,f,g)`Afstand tussen Manhattan (x, y, z) en (e, f, g), waarbij elke letter veldnaam is. |
| Er bestaat |Retourneert waar als een lid van Hallo veld bestaat. |`exists(author)`Retourneert TRUE zijn voor elk document dat in Hallo 'auteur' veld een waarde bevat.<br>`exists(query(price:5.00))`Retourneert ' True ' als 'price' overeenkomt, '5,00'. |
| EXP |Retourneert Euler van getal verheven toopower x. |`exp(x)` |
| Floor |Rondt af naar beneden tooan geheel getal. |`floor(x)`  <br> `floor(5.6)`Retourneert 5 |
| hypo |Retourneert sqrt(sum(pow(x,2),pow(y,2))) zonder tussenliggende overloop of negatieve overloop. |`hypo(x,y)`  <br> ` |
| Als |Hiermee kunt voorwaardelijke functie query's. In `if(test,value1,value2)`, test of verwijst deze tooa logische waarde of expressie waarvan de retourneert een logische waarde (TRUE of FALSE). `value1`Hallo-waarde geretourneerd door de functie Hallo als test TRUE oplevert. `value2`Hallo-waarde geretourneerd door de functie Hallo als test FALSE oplevert. Een expressie kan een functie die Boole-waarden levert zijn. Het kan ook een functie retourneren numerieke waarden, waarin de case-waarde 0 wordt geïnterpreteerd als onwaar of retourneren tekenreeksen, in welk geval lege tekenreeks wordt geïnterpreteerd als onwaar zijn. |`if(termfreq(cat,'electronics'),popularity,42)`Deze functie controleert elk document toosee als het Hallo-term 'electronics' in hello cat veld bevat. Als dit het geval is, klikt u vervolgens Hallo Hallo populariteit veld waarde geretourneerd. Anders wordt de waarde van 42 Hallo is geretourneerd. |
| Lineair |Implements `m*x+c`, m en c constanten zijn waarbij x staat voor een willekeurige functie. Dit is gelijkwaardig te`sum(product(m,x),c)`, maar enigszins efficiënter zoals deze is geïmplementeerd als een enkele functie. |`linear(x,m,c) linear(x,2,4)`retourneert`2*x+4` |
| Rg |Retourneert Hallo natuurlijke logboek van Hallo opgegeven functie. |`ln(x)` |
| Logboek |Retourneert Hallo logboek grondtal 10 van Hallo opgegeven functie. |`log(x)   log(sum(x,100))` |
| Kaart |Alle waarden van een invoer x-functie die min en max, inclusief toohello opgegeven doel vallen wordt toegewezen. Hallo argumenten min en max moeten constanten zijn. Hallo argumenten doel en standaard zijn constanten of functies. Als Hallo-waarde van x niet tussen min en max ligt, wordt de waarde van beide Hallo van x geretourneerd of een standaardwaarde wordt geretourneerd als de opgegeven als een argument van 5e. |`map(x,min,max,target) map(x,0,0,1)`Eventuele waarden van 0 too1 gewijzigd. Dit kan nuttig zijn bij het verwerken van standaardwaarden 0 zijn.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Eventuele waarden tussen 0 en 100 too1 en alle andere waarden te-1 gewijzigd.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Wijzigt een waarden tussen 0 en 100 toox + 599 en andere waarden toofrequency van Hallo term 'solr' hello veld tekst. |
| Maximum aantal |Retourneert de maximale numerieke waarde van meerdere geneste functies of constanten die worden opgegeven als argumenten Hallo: `max(x,y,...)`. maximale Hallo-functie kan ook nuttig zijn voor 'bottoming out' een andere functie of veld op sommige opgegeven constante.  Gebruik Hallo `field(myfield,max)` syntaxis voor het selecteren van de maximale waarde Hallo van één veld met meerdere waarden. |`max(myfield,myotherfield,0)` |
| min. |Retourneert de minimale numerieke waarde van meerdere geneste functies van de constanten die worden opgegeven als argumenten Hallo: `min(x,y,...)`. de functie min Hallo kan ook nuttig voor het ontwikkelen van een 'bovengrens' op een functie met een constante zijn. Gebruik Hallo `field(myfield,min)` syntaxis voor het selecteren van de minimale waarde Hallo van één veld met meerdere waarden. |`min(myfield,myotherfield,0)` |
| Mod |Hallo modulus van Hallo functie x door Hallo functie y berekent. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| MS |Retourneert de milliseconden van verschil tussen de argumenten. Datums zijn relatieve toohello Unix- of POSIX tijd epoche, middernacht, 1 januari 1970 UTC. Argumenten kunnen Hallo-naam van een geïndexeerde TrieDateField of datum math op basis van een constante datum of nu. `ms()`is gelijk te`ms(NOW)`, aantal milliseconden dat sinds het Hallo-epoche. `ms(a)`retourneert het aantal milliseconden Hallo sinds het Hallo-epoche Hallo argument vertegenwoordigt. `ms(a,b)`retourneert het aantal milliseconden Hallo die b vindt plaats voordat een, namelijk `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| niet |Hallo logisch genegeerde waarde Hallo ingepakt functie. |`not(exists(author))`GELDT alleen wanneer `exists(author)` is ingesteld op false. |
| of |Een logische splitsing. |`or(value1,value2)`De waarde TRUE wanneer beide value1 of value2 is ingesteld op true. |
| Pow |Verhoogt Hallo opgegeven base toohello opgegeven macht. `pow(x,y)`Verheft x toohello macht y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Hallo dezelfde als sqrt. |
| Product |Retourneert Hallo product van meerdere waarden of functies, die zijn opgegeven in een door komma's gescheiden lijst. `mul(...)`kan ook worden gebruikt als een alias voor deze functie. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Een wederzijdse werkt met `recip(x,m,a,b)` implementeren `a/(m*x+b)`, waarbij m a en b zijn constanten en x staat voor een willekeurig complexe functie. Wanneer een b zijn gelijk en x > = 0, deze functie heeft een maximale waarde van 1 zakt x toeneemt. Hallo-waarde van een b samen resulteert in een verplaatsing van Hallo gehele functie tooa houden deel uit van de curve Hallo. Deze eigenschappen kunnen ervoor zorgen dat dit een ideaal werkt voor versterking van meer recente documenten, waarbij x `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| RAD |Converteert graden tooradians. |`rad(x)` |
| afdrukken |Rondt toohello dichtstbijzijnde integer. |`rint(x)`  <br> `rint(5.6)`Retourneert 6 |
| sin |Retourneert de sinus van een hoek. |`sin(x)` |
| SINH |Retourneert de hyperbolische sinus van een hoek. |`sinh(x)` |
| Schaal |Schaalt waarden van de functie Hallo x, zodat ze liggen tussen Hallo opgegeven minTarget en maxTarget liggen. de huidige implementatie Hallo passeert alle Hallo functie waarden tooobtain Hallo min en max, zodat deze de juiste schaal Hallo kunt selecteren. Hallo huidige implementatie kan niet worden onderscheiden wanneer documenten zijn verwijderd, of de documenten die geen waarde. 0,0 waarden wordt gebruikt voor deze aanvragen. Dit betekent dat als waarden gewoonlijk alle groter zijn dan 0,0 zijn, een nog steeds met 0,0 eindigen kan zoals Hallo min-waarde toomap uit. In dergelijke gevallen een geschikte `map()` functie kan worden gebruikt als een tijdelijke oplossing toochange 0,0 tooa waarde in Hallo echte bereik, zoals hier wordt weergegeven:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Kan worden geschaald Hallo waarden van x, zodat alle waarden tussen 1 en 2 liggen zijn. |
| SQRT |Retourneert de vierkantswortel van Hallo Hallo opgegeven waarde of functie. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Berekent de Hallo afstand tussen de twee tekenreeksen. Hallo Lucene spellen checker StringDistance interface gebruikt en ondersteunt alle Hallo-implementaties die beschikbaar zijn in dit pakket. Ook kunt toepassingen tooplug in hun eigen via Solr van resource mogelijkheden laden. strdist duurt `(string1, string2, distance measure)`. Mogelijke waarden voor de afstand meting zijn:<ul><li>jw: Jaro Winkler</li><li>bewerken: afstand Levenstein of bewerken</li><li>ngram: Hallo NGramDistance, indien opgegeven, kan eventueel doorgeven in Hallo ngram grootte te. De standaardwaarde is 2.</li><li>FQN: Volledig gekwalificeerde naam voor een implementatie van Hallo StringDistance interface klasse. Moet een niet-arg constructor hebben.</li></ul> |`strdist("SOLR",id,edit)` |
| Sub |Retourneert de x-y van `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Som |Retourneert Hallo de som van meerdere waarden of functies, die zijn opgegeven in een door komma's gescheiden lijst. `add(...)`kan worden gebruikt als een alias voor deze functie. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Retourneert het aantal keren Hallo term wordt weergegeven in het veld Hallo van dat document Hallo. |termfreq(Text,'memory') |
| Tan |Retourneert de tangens van een hoek. |`tan(x)` |
| TANH |Retourneert de hyperbolische tangens van een hoek. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Het veld en facet verwijzing zoeken
Wanneer u logboek toofind zoekgegevens gebruikt, worden de resultaten weergegeven verschillende veld en facetten. Sommige Hallo gegevens mogelijk niet erg beschrijvende weergegeven. Gebruik Hallo informatie toohelp u begrijpt Hallo resultaten te volgen.

| Veld | Zoektype | Beschrijving |
| --- | --- | --- |
| TenantId |Alle |Toopartition gegevens gebruikt. |
| TimeGenerated |Alle |Toodrive hello tijdlijn timeselectors (in de zoekopdracht en andere schermen) gebruikt. Dit vertegenwoordigt wanneer Hallo gegevensitem is gegenereerd (doorgaans op Hallo agent). Hallo tijd wordt uitgedrukt in de ISO-indeling en is altijd UTC. In geval van typen die zijn gebaseerd op bestaande instrumentation (dat wil zeggen, de gebeurtenissen in een logboek) Hallo is dit meestal Hallo echt tijd dat die Hallo vermelding/regel/logboekrecord is vastgelegd. Voor een aantal Hallo Hallo andere typen die via management packs of in de cloud hello (bijvoorbeeld aanbevelingen of waarschuwingen), worden geproduceerd tijd vertegenwoordigt een ander. Dit is de tijd Hallo wanneer deze nieuwe gegevensitem met een momentopname van een configuratie van sommige sorteren is verzameld, of een aanbeveling/waarschuwing is gemaakt op basis van deze. |
| Gebeurtenis-id |Gebeurtenis |Gebeurtenis-id in het gebeurtenislogboek van Windows hello. |
| Gebeurtenislogboek |Gebeurtenis |Gebeurtenislogboek waar Hallo gebeurtenis is vastgelegd door Windows. |
| EventLevelName |Gebeurtenis |Kritieke/waarschuwing/informatie/geslaagd |
| eventLevel |Gebeurtenis |Numerieke waarde voor kritieke/waarschuwing/informatie/succes (EventLevelName in plaats daarvan gebruiken voor query's eenvoudiger/beter leesbaar). |
| SourceSystem |Alle |Waar Hallo gegevens vandaan (bijvoegen in termen van modus toohello service). Voorbeelden zijn Microsoft System Center Operations Manager en Azure Storage. |
| Objectnaam |PerfHourly |Naam van het prestatieobject Windows. |
| InstanceName |PerfHourly |Windowsnaam van het exemplaar. |
| CounteName |PerfHourly |Naam Prestatiemeter Windows. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Weergavenaam van het Hallo-object door een prestatieverzamelingsregel in Operations Manager zijn gericht. Kan ook Hallo weergavenaam van Hallo object gedetecteerd door operationeel inzicht, of op basis van welke Hallo waarschuwing is gegenereerd. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Weergavenaam van de bovenliggende Hallo van Hallo bovenliggende (in een dubbele hosting-relatie) van Hallo object gericht door een prestatieverzamelingsregel in Operations Manager. Kan ook Hallo weergavenaam van Hallo object gedetecteerd door operationeel inzicht, of op basis van welke Hallo waarschuwing is gegenereerd. |
| Computer |De meeste typen |De naam van de computer die gegevens Hallo behoort. |
| Apparaatnaam |ProtectionStatus |Computergegevens naam Hallo behoort te (zelfde als 'Computer'). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Threat status rang is een numerieke representatie van Hallo threat status. Vergelijkbare tooHTTP reactiecodes, Hallo ranking heeft onderbrekingen tussen de Hallo cijfers (daarom geen bedreigingen is 150 en niet 100 of 0), waardoor er ruimte overblijft tooadd nieuwe statussen. Hallo voornemen is voor een updatepakket van threat status en beveiligingsstatus tooshow Hallo slechtste toestand die computer Hallo Hallo geselecteerde periode heeft voorgedaan. Hallo cijfers rangschikken Hallo status veranderen, zodat u naar Hallo-record met de hoogste nummer Hallo zoeken kunt. |
| ThreatStatus |ProtectionStatus |Beschrijving van ThreatStatus, 1:1 met ThreatStatusRank toegewezen. |
| TypeofProtection |ProtectionStatus |Antimalware-product dat is gedetecteerd in het Hallo-computer: none, Microsoft Malware-hulpprogramma, Forefront, enzovoort. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |HealthService-ID voor de agent van deze computer. |
| HealthServiceId |De meeste typen |HealthService-ID voor de agent van deze computer. |
| ManagementGroupName |De meeste typen |Naam beheergroep voor agents met Operations Manager zijn gekoppeld. Anders is null/leeg. |
| objectType |ConfigurationObject |Typ (zoals in Operations Manager management pack-type/klasse) voor dit object, door logboekanalyse configuratie assessment gedetecteerd. |
| UpdateTitle |RequiredUpdate |Naam van het Hallo-update die is gevonden niet is geïnstalleerd. |
| PublishDate |RequiredUpdate |Wanneer Hallo-update is gepubliceerd op Microsoft Update. |
| Server |RequiredUpdate |Computergegevens naam Hallo behoort te (zelfde als 'Computer'). |
| Product |RequiredUpdate |Product dat Hallo update van toepassing op. |
| UpdateClassification |RequiredUpdate |Type update (bijvoorbeeld updatepakket of service pack). |
| KBID |RequiredUpdate |KB-artikel-ID die deze best practice of update beschrijft. |
| WorkflowName |ConfigurationAlert |Naam van het Hallo-regel of monitor die Hallo waarschuwing geproduceerd. |
| Ernst |ConfigurationAlert |Ernst van waarschuwing Hallo. |
| Prioriteit |ConfigurationAlert |De prioriteit van waarschuwing Hallo. |
| IsMonitorAlert |ConfigurationAlert |Is deze waarschuwing gegenereerd door een monitor (true) of een regel (ONWAAR)? |
| AlertParameters |ConfigurationAlert |De XML met Hallo parameters van Hallo logboekanalyse waarschuwing. |
| Context |ConfigurationAlert |De XML met Hallo context van Hallo logboekanalyse waarschuwing. |
| Workload |ConfigurationAlert |Technologie of werkbelasting die Hallo waarschuwing verwijst naar. |
| AdvisorWorkload |Aanbeveling |Technologie of werkbelasting die aanbeveling Hallo verwijst naar. |
| Beschrijving |ConfigurationAlert |Beschrijving van waarschuwing (korte). |
| DaysSinceLastUpdate |UpdateAgent |Hoeveel dagen geleden (relatieve tooTimeGenerated van deze record) deze agent het een update van Windows Server Update Service (WSUS) of Microsoft Update installeren? |
| DaysSinceLastUpdateBucket |UpdateAgent |Op basis van DaysSinceLastUpdate, een categorisatie in tijd buckets van hoe lang geleden een computer installatie van de vorige updates vanaf WSUS of Microsoft Update. |
| AutomaticUpdateEnabled |UpdateAgent |Automatische updates controleren in- of uitgeschakeld voor deze agent? |
| AutomaticUpdateValue |UpdateAgent |Automatische updates controleren of set tooautomatically downloaden en installeren, alleen downloaden of alleen controleren? |
| WindowsUpdateAgentVersion |UpdateAgent |Het versienummer van Hallo Microsoft Update-agent. |
| WSUSServer |UpdateAgent |Welke WSUS-server is gericht voor deze update-agent? |
| OSVersion |UpdateAgent |Versie van besturingssysteem Hallo deze update-agent wordt uitgevoerd op. |
| Naam |Aanbeveling, ConfigurationObjectProperty |Naam/functie van Hallo aanbeveling of de naam van de eigenschap Hallo van logboekanalyse configuratie bepalen. |
| Waarde |ConfigurationObjectProperty |De waarde van een eigenschap van logboekanalyse configuratie bepalen. |
| KBLink |Aanbeveling |URL toohello KB-artikel die deze aanbevolen procedure of update beschrijft. |
| RecommendationStatus |Aanbeveling |Aanbevelingen zijn Hallo enkele typen waarvan de records bijgewerkte, niet de zojuist toegevoegde toohello search-index ophalen. Deze status wordt gewijzigd of Hallo aanbeveling wordt actief/openen, of als logboekanalyse detecteert is opgelost. |
| RenderedDescription |Gebeurtenis |Beschrijving (opnieuw gebruikte tekst met ingevulde parameters) van een Windows-gebeurtenis weergegeven. |
| ParameterXml |Gebeurtenis |De XML met Hallo-parameters in gegevenssectie Hallo van een Windows-gebeurtenis (zoals te zien in Logboeken). |
| EventData |Gebeurtenis |De XML met Hallo hele gegevenssectie van een Windows-gebeurtenis (zoals te zien in Logboeken). |
| Bron |Gebeurtenis |Het gebeurtenislogboek die Hallo gebeurtenis heeft gegenereerd. |
| Culture |Gebeurtenis |Categorie van de gebeurtenis hello, rechtstreeks vanuit de Windows-gebeurtenislogboek Hallo. |
| Gebruikersnaam |Gebeurtenis |Gebruikersnaam van Hallo Windows-gebeurtenis (meestal NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Gemiddelde waarde voor aggregatie op uurbasis Hallo van een prestatiemeteritem. |
| Min |PerfHourly |De minimumwaarde in per uur hello-interval van een prestaties teller Uurlijkse aggregatie. |
| Max. |PerfHourly |Maximale waarde in per uur hello-interval van een prestaties teller Uurlijkse aggregatie. |
| Percentile95 |PerfHourly |Hallo 95e percentielwaarde voor elk uur hello-interval van een prestaties teller Uurlijkse aggregatie. |
| SampleCount |PerfHourly |Voorbeelden van de teller hoeveel prestatie Onverwerkt gebruikte tooproduce dit per uur zijn record samenvoegen. |
| Threat |ProtectionStatus |De naam van malware. |
| StorageAccount |W3CIISLog |Azure Storage-account Hallo logboek is gelezen uit. |
| AzureDeploymentID |W3CIISLog |Azure-implementatie-ID van Hallo cloud service Hallo logboek behoort. |
| Rol |W3CIISLog |Rol van logboek-hello Azure cloud service Hallo behoort. |
| RoleInstance |W3CIISLog |RoleInstance Hallo Azure rol die Hallo logboek behoort. |
| sSiteName |W3CIISLog |IIS-website met logboek Hallo behoort too(metabase notation); Hallo s-sitename veld in de oorspronkelijke logboek Hallo. |
| sComputerName |W3CIISLog |Hallo s-computername veld in de oorspronkelijke logboek Hallo. |
| sIP |W3CIISLog |Server IP-adres Hallo HTTP-aanvraag is geadresseerd aan. Hallo s-IP-veld in de oorspronkelijke logboek Hallo. |
| csMethod |W3CIISLog |HTTP-methode (bijvoorbeeld GET/POST) is gebruikt door de client Hallo Hallo HTTP-aanvraag. Hallo cs-methode in de oorspronkelijke logboek Hallo. |
| Overschrijving |W3CIISLog |Client IP-adres Hallo HTTP-aanvraag van afkomstig is. Hallo c-IP-veld in de oorspronkelijke logboek Hallo. |
| csUserAgent |W3CIISLog |HTTP-gebruikersagent gedeclareerd door de client hello (browser of anderszins). cs-user-agent in de oorspronkelijke logboek Hallo Hallo. |
| scStatus |W3CIISLog |HTTP-statuscode (bijvoorbeeld: 200/403/500) geretourneerd door Hallo server toohello-client. Hallo cs-status in de oorspronkelijke logboek Hallo. |
| timeTaken |W3CIISLog |Hoe lang (in milliseconden) duurde die aanvraag Hallo toocomplete. Hallo timetaken veld in de oorspronkelijke logboek Hallo. |
| csUriStem |W3CIISLog |Relatieve URI (zonder hostadres, die is, / zoeken) die is aangevraagd. Hallo cs uristem veld in de oorspronkelijke logboek Hallo. |
| csUriQuery |W3CIISLog |URI-query. URI-query's zijn alleen nodig voor dynamische pagina's, zoals ASP-pagina's, zodat dit veld meestal een koppelteken voor statische's bevat. |
| sPort |W3CIISLog |Serverpoort die Hallo HTTP-aanvraag is verzonden, te (en dat IIS luistert naar, aangezien deze opgepikt). |
| csUserName |W3CIISLog |Naam van gebruiker geverifieerd als de aanvraag Hallo geverifieerde en niet-anonieme. |
| csVersion |W3CIISLog |HTTP-Protocol versie gebruikt in Hallo-aanvraag (bijvoorbeeld HTTP/1.1). |
| csCookie |W3CIISLog |Informatie van de cookie. |
| csReferer |W3CIISLog |Site die het laatst heeft bezocht Hallo-gebruiker. Deze website bevat een koppeling toohello huidige site. |
| csHost |W3CIISLog |Host-header (bijvoorbeeld www.mysite.com) die is aangevraagd. |
| scSubStatus |W3CIISLog |Fout-substatuscode geregistreerd. |
| scWin32Status |W3CIISLog |Windows-statuscode geregistreerd. |
| csBytes |W3CIISLog |Bytes verzonden in de aanvraag Hallo van Hallo client toohello server. |
| scBytes |W3CIISLog |Bytes terug in antwoord Hallo vanaf Hallo server toohello client geretourneerd. |
| ConfigChangeType |Configuratiewijziging |Type wijziging (bijvoorbeeld WindowsServices/Software). |
| ChangeCategory |Configuratiewijziging |De categorie van Hallo wijzigen (toegevoegde-Modified/verwijderd). |
| SoftwareType |Configuratiewijziging |Type software (Update/toepassing). |
| SoftwareName |Configuratiewijziging |Naam van het Hallo-software (alleen van toepassing toosoftware wijzigingen). |
| Uitgever |Configuratiewijziging |Leverancier die Hallo software (alleen van toepassing toosoftware wijzigingen publiceert). |
| SvcChangeType |Configuratiewijziging |Type wijziging die is toegepast op een Windows-service (status/StartupType/pad/ServiceAccount). Dit is alleen van toepassing tooWindows-servicewijzigingen. |
| SvcDisplayName |Configuratiewijziging |Weergavenaam van het Hallo-service die is gewijzigd. |
| SvcName |Configuratiewijziging |Naam van het Hallo-service die is gewijzigd. |
| SvcState |Configuratiewijziging |Nieuwe (huidige) status van Hallo-service. |
| SvcPreviousState |Configuratiewijziging |Vorige bekende status van Hallo-service (alleen van toepassing als de status van service gewijzigd). |
| SvcStartupType |Configuratiewijziging |Opstarttype van service. |
| SvcPreviousStartupType |Configuratiewijziging |Vorige opstarttype (alleen van toepassing als opstarttype gewijzigd). |
| SvcAccount |Configuratiewijziging |Service-account. |
| SvcPreviousAccount |Configuratiewijziging |Vorige serviceaccount (alleen van toepassing als serviceaccount gewijzigd). |
| SvcPath |Configuratiewijziging |Pad toohello uitvoerbaar van Hallo Windows-service. |
| SvcPreviousPath |Configuratiewijziging |Vorige pad van het uitvoerbare bestand voor Windows-service (alleen van toepassing als deze gewijzigd) Hallo Hallo. |
| SvcDescription |Configuratiewijziging |Beschrijving van het Hallo-service. |
| Vorige |Configuratiewijziging |Eerdere status van deze software (geïnstalleerde/niet geïnstalleerde vorige versie). |
| Huidige |Configuratiewijziging |Meest recente toestand van deze software (geïnstalleerde/niet-geïnstalleerde/huidige versie). |

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over logboek zoekacties:

* Raken met [Meld zoekopdrachten](log-analytics-log-searches.md) tooview gedetailleerde informatie verzameld door oplossingen.
* Gebruik [aangepaste velden in logboekanalyse](log-analytics-custom-fields.md) tooextend logboek zoekopdrachten.
