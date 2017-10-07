---
title: aaaAutomatically scale rekenknooppunten in een Azure Batch-pool | Microsoft Docs
description: Automatische schaling van inschakelen op een groep cloud toodynamically Hallo aantal rekenknooppunten in de pool Hallo aanpassen.
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Een automatische schaling formule voor het schalen van rekenknooppunten in een Batch-pool maken

Azure Batch kan pools op basis van de parameters die u definieert automatisch schalen. Met automatisch schalen Batch dynamisch knooppunten tooa pool wordt toegevoegd als taak eisen toename en rekenknooppunten wordt verwijderd als ze afnemen. U kunt zowel tijd en geld opslaan door het aantal rekenknooppunten gebruikt door de Batch-toepassing hello automatisch aan te passen. 

Inschakelen van automatisch schalen op een pool van rekenknooppunten door te koppelen aan een *formule voor automatisch schalen* die u definieert. Hallo Batch-service gebruikt Hallo automatisch schalen formule toodetermine Hallo aantal rekenknooppunten die vereist tooexecute zijn uw workload. Knooppunten kunnen worden toegewezen knooppunten COMPUTE of [prioriteit Laag knooppunten](batch-low-pri-vms.md). Batch reageert tooservice metrische gegevens die regelmatig wordt verzameld. Met deze metrische gegevens Batch aangepast Hallo aantal rekenknooppunten in Hallo-groep op basis van de formule en met een configureerbare interval.

U kunt inschakelen automatische schaling tijdens het maken van een groep of op een bestaande toepassingen. U kunt ook een bestaande formule op een groep die is geconfigureerd voor automatisch schalen wijzigen. Batch kunt u tooevaluate formules voordat het toewijzen van toopools en toomonitor Hallo-status van de automatische schaling wordt uitgevoerd.

Dit artikel wordt beschreven Hallo verschillende entiteiten die gezamenlijk uw formules automatisch schalen, met inbegrip van variabelen, operators, bewerkingen en functies. Bespreken we hoe tooobtain verschillende compute resource en taak metrische gegevens in Batch. U kunt deze metrische gegevens tooadjust aantal van de knooppunten van de groep op basis van gebruiks- en resourcestatus gebruiken. Vervolgens wordt beschreven hoe een formule tooconstruct en schakel automatisch vergroten / verkleinen op een groep met behulp van beide Hallo Batch REST en .NET API's. Ten slotte voltooien we met een paar voorbeeld formules.

> [!IMPORTANT]
> Wanneer u een Batch-account maakt, kunt u Hallo [accountconfiguratie](batch-api-basics.md#account), waarmee wordt bepaald of groepen in een Batch-service-abonnement (Hallo standaard), of in uw gebruikerabonnement zijn toegewezen. Als u uw Batch-account hebt gemaakt met de Batch-Service standaardconfiguratie hello, is uw account beperkt tooa kunt u het maximum aantal kernen die kunnen worden gebruikt voor verwerking. Hallo Batch-service schaalt rekenknooppunten alleen up toothat core limiet. Om deze reden kan Hallo Batch-service niet Hallo doelaantal rekenknooppunten die zijn opgegeven met een formule voor automatisch schalen bereikt. Zie [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor informatie over het weergeven en uw accountquota verhogen.
>
>Als u uw account hebt gemaakt met de configuratie van de gebruikerabonnement Hallo, vervolgens deelt uw account in Hallo kerngeheugenquotum voor Hallo-abonnement. Zie [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) (Limieten voor Virtuele Machines) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md) (Azure-abonnement en servicelimieten, -quota en -beperkingen) voor meer informatie.
>
>

## <a name="automatic-scaling-formulas"></a>Automatische schaling formules
Een formule voor automatisch schalen is een string-waarde die u definieert die een of meer instructies bevat. Hallo-formule voor automatisch schalen van tooa pool is toegewezen [autoScaleFormula] [ rest_autoscaleformula] element (Batch REST) of [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] de eigenschap (Batch .NET). Hallo Batch-service gebruikt uw formule toodetermine Hallo doelaantal rekenknooppunten in de groep Hallo voor de volgende interval hello wordt verwerkt. Hallo formule tekenreeks mag niet meer dan 8 KB, up too100 instructies die worden gescheiden door puntkomma's en kunnen regeleinden en -opmerkingen bevatten kunt opnemen.

U kunt automatische schaling formules beschouwen als een Batch automatisch schalen 'taal'. Formule-instructies zijn gratis ingedeelde expressies die zowel de service gedefinieerde variabelen (variabelen die zijn gedefinieerd door Hallo Batch-service) als de gebruiker gedefinieerde variabelen (variabelen die u definieert) kunnen opnemen. Ze kunnen verschillende bewerkingen op deze waarden uitvoeren met behulp van de ingebouwde typen, operators en functies. Een instructie duurt bijvoorbeeld Hallo formulier te volgen:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Formules bevatten doorgaans meerdere instructies die bewerkingen uitvoeren op waarden die zijn verkregen in de vorige instructies. Bijvoorbeeld, eerst we een waarde voor aanvragen `variable1`, geeft u het tooa functie toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Deze instructies opnemen in uw formule tooarrive automatisch schalen op een doel-nummer van rekenknooppunten. Toegewezen knooppunten en knooppunten met lage prioriteit hebben hun eigen doelinstellingen zodat u kunt een doel voor elk type knooppunt definiëren. Een formule voor automatisch schalen kan een doelwaarde voor speciale knooppunten of een doelwaarde voor prioriteit Laag knooppunten bevatten.

Hallo doelaantal knooppunten mogelijk hogere en lagere of gelijk zijn aan het huidige aantal knooppunten van dat type in de groep Hallo HALLO hallo. Batch evalueert formule voor een pool automatisch schalen met een bepaald interval (Zie [automatisch vergroten / verkleinen intervallen](#automatic-scaling-interval)). Batch aangepast Hallo doelaantal van elk type van de knooppunten in Hallo groep toohello waarde waarmee de formule voor automatisch schalen op Hallo moment van evaluatie.

### <a name="sample-autoscale-formula"></a>Formule voor automatisch schalen

Hier volgt een voorbeeld van een formule voor automatisch schalen die aangepast toowork voor de meeste scenario's worden kan. Hallo variabelen `startingNumberOfVMs` en `maxNumberofVMs` in Hallo voorbeeldformule worden aangepaste tooyour behoeften. Deze formule schaalt toegewezen knooppunten, maar het gewijzigde tooapply tooscale prioriteit laag ook knooppunten kan worden. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Met deze formule voor automatisch schalen Hallo van toepassingen in eerste instantie gemaakt met een enkele virtuele machine. Hallo `$PendingTasks` metriek definieert Hallo aantal taken die uitgevoerd of in de wachtrij zijn. Hallo formule Hallo gemiddelde aantal in behandeling zijnde taken vindt in Hallo afgelopen 180 seconden en stelt Hallo `$TargetDedicatedNodes` variabele dienovereenkomstig. Hallo formule zorgt ervoor dat Hallo doelaantal knooppunten toegewezen nooit meer dan 25 virtuele machines. Als nieuwe taken worden verzonden, wordt automatisch Hallo groep groeit. Als taken zijn voltooid, virtuele machines worden gratis één voor één en formule voor automatisch schalen Hallo Hallo groep wordt verkleind.

## <a name="variables"></a>Variabelen
U kunt beide **service gedefinieerde** en **gebruiker gedefinieerde** variabelen in formules automatisch schalen. Hallo service gedefinieerde variabelen zijn ingebouwd in toohello Batch-service. Sommige service gedefinieerde variabelen zijn alleen-lezen en sommige alleen-lezen zijn. Gebruiker gedefinieerde variabelen zijn variabelen die u definieert. In Hallo voorbeeldformule weergegeven in de vorige sectie hello, `$TargetDedicatedNodes` en `$PendingTasks` service gedefinieerde variabelen zijn. Variabelen `startingNumberOfVMs` en `maxNumberofVMs` zijn van de gebruiker gedefinieerde variabelen.

> [!NOTE]
> Service gedefinieerde variabelen worden altijd voorafgegaan door een dollarteken ($). Hallo dollarteken is voor de gebruiker gedefinieerde variabelen, optioneel.
>
>

Hallo volgende tabellen ziet u beide lezen-schrijven en alleen-lezen-variabelen die zijn gedefinieerd door Hallo Batch-service.

U kunt ophalen en het instellen van de Hallo waarden van deze service gedefinieerde variabelen toomanage Hallo aantal rekenknooppunten in een groep:

| Lees-/ service gedefinieerde variabelen | Beschrijving |
| --- | --- |
| $TargetDedicatedNodes |Hallo doelaantal toegewezen rekenknooppunten voor Hallo van toepassingen. Hallo aantal toegewezen knooppunten is opgegeven als een doel omdat een groep van toepassingen mogelijk niet altijd worden bereikt Hallo gewenst aantal knooppunten. Als Hallo doelaantal knooppunten toegewezen wordt gewijzigd door een evaluatie met automatisch schalen voordat Hallo groep Hallo initiële doel heeft bereikt en Hallo van toepassingen mogelijk Hallo doel niet bereiken. <br /><br /> Een groep in een account dat is gemaakt met Hallo Batch-Service-configuratie kan niet het doel bereiken als Hallo doel een Batch-account knooppunt of core-quota overschrijdt. Een groep in een account dat is gemaakt met de configuratie van de Hallo-abonnement van de gebruiker kan het doel niet bereiken als doel Hallo Hallo gedeeld kerngeheugenquotum voor Hallo abonnement overschrijdt.|
| $TargetLowPriorityNodes |Hallo doelaantal prioriteit Laag rekenknooppunten voor Hallo van toepassingen. Hallo aantal knooppunten dat prioriteit laag is opgegeven als een doel omdat een groep van toepassingen mogelijk niet altijd worden bereikt Hallo gewenst aantal knooppunten. Als Hallo doelaantal knooppunten prioriteit laag wordt gewijzigd door een evaluatie met automatisch schalen voordat Hallo groep Hallo initiële doel heeft bereikt en Hallo van toepassingen mogelijk Hallo doel niet bereiken. Een pool kan ook niet het doel bereiken als Hallo doel een Batch-account knooppunt of core-quota overschrijdt. <br /><br /> Zie voor meer informatie op prioriteit Laag rekenknooppunten [met lage prioriteit virtuele machines, met Batch (Preview)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |Hallo-actie die optreedt wanneer de rekenknooppunten worden verwijderd uit een groep. Mogelijke waarden zijn:<ul><li>**requeue**--taken onmiddellijk beëindigd en weer in de taakwachtrij Hallo plaatst, zodat ze opnieuw worden gepland.<li>**beëindigen**--taken onmiddellijk beëindigd en worden deze verwijderd uit de wachtrij Hallo.<li>**taskcompletion**--wacht voor actief toofinish taken en Hallo knooppunt uit Hallo van toepassingen verwijdert.<li>**retaineddata**--wacht op alle Hallo lokale taak bewaard gegevens op Hallo knooppunt toobe opgeruimd voordat het Hallo-knooppunt wordt verwijderd uit het Hallo-groep.</ul> |

U kunt Hallo-waarde van deze service gedefinieerde variabelen toomake aanpassingen die zijn gebaseerd op metrische gegevens van de Batch-service Hallo krijgen:

| Alleen-lezen service gedefinieerde variabelen | Beschrijving |
| --- | --- |
| $CPUPercent |Hallo gemiddelde percentage van CPU-gebruik. |
| $WallClockSeconds |Hallo aantal seconden verbruikt. |
| $MemoryBytes |Hallo gemiddelde aantal megabytes gebruikt. |
| $DiskBytes |Hallo gemiddelde aantal gigabytes op Hallo lokale schijven gebruikt. |
| $DiskReadBytes |Hallo aantal gelezen bytes. |
| $DiskWriteBytes |Hallo aantal geschreven bytes. |
| $DiskReadOps |aantal gelezen schijfbewerkingen Hallo uitgevoerd. |
| $DiskWriteOps |Hallo aantal schijf schrijfbewerkingen uitgevoerd. |
| $NetworkInBytes |Hallo aantal binnenkomende bytes. |
| $NetworkOutBytes |Hallo aantal uitgaande bytes. |
| $SampleNodeCount |Hallo aantal rekenknooppunten. |
| $ActiveTasks |Hallo aantal taken die gereed tooexecute zijn, maar nog niet zijn uitgevoerd. Hallo $ActiveTasks aantal bevat alle taken die zijn Hallo actieve status heeft en waarvan afhankelijkheden is voldaan. Alle taken die zich in de actieve status Hallo maar waarvan afhankelijkheden niet is voldaan, worden uitgesloten van Hallo $ActiveTasks count.|
| $RunningTasks |Hallo aantal taken actief is. |
| $PendingTasks |Hallo som van $ActiveTasks en $RunningTasks. |
| $SucceededTasks |Hallo aantal taken dat voltooid is. |
| $FailedTasks |Hallo aantal taken dat is mislukt. |
| $CurrentDedicatedNodes |Hallo Huidig aantal toegewezen rekenknooppunten. |
| $CurrentLowPriorityNodes |Huidig aantal prioriteit Laag Hallo rekenknooppunten, met inbegrip van alle knooppunten die verschoven zijn. |
| $PreemptedNodeCount | Hallo aantal knooppunten in het Hallo-groep die zich in een status verschoven. |

> [!TIP]
> Hallo alleen-lezen, service gedefinieerde variabelen die worden weergegeven in de vorige tabel Hallo zijn *objecten* die verschillende methoden tooaccess gegevens die zijn gekoppeld aan elk bieden. Zie voor meer informatie [verkrijgen voorbeeldgegevens](#getsampledata) verderop in dit artikel.
>
>

## <a name="types"></a>Typen
Deze typen worden ondersteund in een formule:

* dubbele
* doubleVec
* doubleVecList
* Tekenreeks
* tijdstempel--tijdstempel is een samengestelde structuur die Hallo volgende leden bevat:

  * jaar
  * maand (1-12)
  * dag (1-31)
  * werkdag (Hallo-indeling van het nummer; bijvoorbeeld: 1 voor maandag)
  * uur (in 24-uurs notatie, bijvoorbeeld: 13 betekent 1 uur)
  * minuten (00-59)
  * tweede (00-59)
* TimeInterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Bewerkingen
Deze bewerkingen zijn toegestaan op Hallo-typen die worden vermeld in de vorige sectie Hallo.

| Bewerking | Ondersteunde operators | Resultaattype |
| --- | --- | --- |
| dubbele *operator* dubbele |+, -, *, / |dubbele |
| dubbele *operator* timeinterval |* |TimeInterval |
| doubleVec *operator* dubbele |+, -, *, / |doubleVec |
| doubleVec *operator* doubleVec |+, -, *, / |doubleVec |
| TimeInterval *operator* dubbele |*, / |TimeInterval |
| TimeInterval *operator* timeinterval |+, - |TimeInterval |
| TimeInterval *operator* tijdstempel |+ |tijdstempel |
| tijdstempel *operator* timeinterval |+ |tijdstempel |
| tijdstempel *operator* tijdstempel |- |TimeInterval |
| *operator*dubbele |-, ! |dubbele |
| *operator*timeinterval |- |TimeInterval |
| dubbele *operator* dubbele |<, <=, ==, >=, >, != |dubbele |
| tekenreeks *operator* tekenreeks |<, <=, ==, >=, >, != |dubbele |
| tijdstempel *operator* tijdstempel |<, <=, ==, >=, >, != |dubbele |
| TimeInterval *operator* timeinterval |<, <=, ==, >=, >, != |dubbele |
| dubbele *operator* dubbele |&&, &#124;&#124; |dubbele |

Bij het testen van een Double-waarde met een ternaire operator (`double ? statement1 : statement2`), niet nul is **true**, en nul is **false**.

## <a name="functions"></a>Functies
Deze vooraf gedefinieerde **functies** zijn beschikbaar voor toouse bij het definiëren van een formule voor automatisch schalen.

| Functie | Retourtype | Beschrijving |
| --- | --- | --- |
| Avg(doubleVecList) |dubbele |Retourneert Hallo gemiddelde waarde van alle waarden in Hallo doubleVecList. |
| Len(doubleVecList) |dubbele |Retourneert Hallo de lengte van Hallo-vector is gemaakt van Hallo doubleVecList. |
| LG(Double) |dubbele |Retourneert Hallo logboek grondtal 2 Hallo dubbele. |
| LG(doubleVecList) |doubleVec |Hallo component-wise logboek retourneert grondtal 2 van Hallo doubleVecList. Een vec(double) moet expliciet voor Hallo-parameter worden doorgegeven. Anders wordt Hallo dubbele lg(double) versie verondersteld. |
| ln(Double) |dubbele |Retourneert Hallo natuurlijke logboek van dubbele Hallo. |
| ln(doubleVecList) |doubleVec |Hallo component-wise logboek retourneert grondtal 2 van Hallo doubleVecList. Een vec(double) moet expliciet voor Hallo-parameter worden doorgegeven. Anders wordt Hallo dubbele lg(double) versie verondersteld. |
| log(Double) |dubbele |Retourneert Hallo logboek grondtal 10 van Hallo dubbele. |
| log(doubleVecList) |doubleVec |Hallo component-wise logboek retourneert grondtal 10 van Hallo doubleVecList. Een vec(double) moet expliciet voor Hallo enkele dubbele parameter worden doorgegeven. Anders wordt Hallo dubbele log(double) versie verondersteld. |
| Max(doubleVecList) |dubbele |Retourneert Hallo de maximumwaarde in Hallo doubleVecList. |
| min(doubleVecList) |dubbele |Retourneert Hallo de minimumwaarde in Hallo doubleVecList. |
| norm(doubleVecList) |dubbele |Retourneert Hallo twee-norm van Hallo-vector is gemaakt van Hallo doubleVecList. |
| percentiel (v doubleVec, dubbele p) |dubbele |Retourneert Hallo percentiel element van het Hallo-vector v. |
| ASELECT() |dubbele |Retourneert een willekeurige waarde tussen 0,0 en 1,0 liggen. |
| Range(doubleVecList) |dubbele |Retourneert Hallo verschil tussen Hallo min en max-waarden in Hallo doubleVecList. |
| Std(doubleVecList) |dubbele |Retourneert Hallo de standaarddeviatie van de steekproef van waarden in Hallo doubleVecList Hallo. |
| Stop() | |Evaluatie van Hallo automatisch schalen expressie stopt. |
| SUM(doubleVecList) |dubbele |Retourneert Hallo de som van alle onderdelen van de Hallo van Hallo doubleVecList. |
| tijd (string, dateTime = "") |tijdstempel |Retourneert de tijdstempel Hallo Hallo huidige tijd als er geen parameters worden doorgegeven of tijdstempel van een datum/tijd-tekenreeks Hallo Hallo als deze wordt doorgegeven. Ondersteunde datum-/ tijdindelingen zijn W3C-DTF- en RFC 1123. |
| waarde opnemen (v doubleVec, dubbele i) |dubbele |Retourneert de waarde Hallo van Hallo-element dat is op locatie i in vector v, met een startIndex gelijk is aan nul. |

Sommige Hallo-functies die worden beschreven in de vorige tabel Hallo kan een lijst accepteren als een argument. Hallo door komma's gescheiden lijst is een combinatie van *dubbele* en *doubleVec*. Bijvoorbeeld:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Hallo *doubleVecList* waarde is geconverteerd tooa één *doubleVec* voordat de evaluatie. Bijvoorbeeld, als `v = [1,2,3]`, klikt u vervolgens het aanroepen van `avg(v)` gelijkwaardige toocalling is `avg(1,2,3)`. Het aanroepen van `avg(v, 7)` is gelijkwaardig toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Voorbeeldgegevens downloaden
Automatisch schalen formules fungeren op metrische gegevens (voorbeelden) die wordt geleverd door Hallo Batch-service. Een formule groeit of krimpt poolgrootte op basis van Hallo die wordt verkregen van Hallo-service. Hallo service gedefinieerde variabelen die zijn beschreven zijn eerder objecten die verschillende methoden tooaccess-gegevens die is gekoppeld aan dit object te bieden. Hallo ziet volgende expressie u bijvoorbeeld een aanvraag tooget Hallo laatste vijf minuten van CPU-gebruik:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Methode | Beschrijving |
| --- | --- |
| GetSample() |Hallo `GetSample()` methode retourneert een vector van voorbeelden van gegevens.<br/><br/>Een voorbeeld is 30 seconden metrische gegevens. Voorbeelden zijn met andere woorden, elke 30 seconden opgehaald. Maar zoals hieronder aangegeven, er is een vertraging tussen wanneer een voorbeeld van een worden verzameld en wanneer het beschikbaar tooa formule is. Als zodanig kunnen niet alle voorbeelden voor een bepaalde periode niet beschikbaar voor evaluatie van een formule.<ul><li>`doubleVec GetSample(double count)`<br/>Geeft het aantal steekproeven tooobtain van de meest recente Hallo-voorbeelden die zijn verzameld Hallo.<br/><br/>`GetSample(1)`retourneert de laatste beschikbare voorbeeld Hallo. Metrische gegevens zoals `$CPUPercent`, maar dit mag niet worden gebruikt omdat het onmogelijk tooknow *wanneer* Hallo voorbeeld is verzameld. Kan het zijn recente of vanwege problemen met het systeem, kan het veel ouder zijn. Het is beter in dergelijke gevallen toouse een tijdsinterval zoals hieronder wordt weergegeven.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Hiermee geeft u een tijdsbestek voor het verzamelen van voorbeeldgegevens. Eventueel ook wordt hiermee aangegeven Hallo percentage van de voorbeelden die beschikbaar zijn in Hallo tijdsbestek aangevraagd.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`Voorbeelden van 20 zou worden geretourneerd als alle voorbeelden voor laatste 10 minuten Hallo aanwezig in Hallo CPUPercent geschiedenis zijn. Als Hallo laatste minuut van de geschiedenis niet beschikbaar is echter zou alleen 18 voorbeelden worden geretourneerd. In dit geval:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`mislukken omdat slechts 90 procent van Hallo voorbeelden beschikbaar zijn.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`zou slagen.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Hiermee geeft u een tijdsbestek voor het verzamelen van gegevens met een begintijd en eindtijd.<br/><br/>Zoals eerder vermeld, is er een vertraging tussen wanneer een voorbeeld van een worden verzameld en wanneer het beschikbaar tooa formule is. Houd rekening met deze vertraging wanneer u Hallo `GetSample` methode. Zie `GetSamplePercent` hieronder. |
| GetSamplePeriod() |Hallo periode van voorbeelden die zijn uitgevoerd retourneert in een historische voorbeeldgegevensset. |
| Count() |Retourneert Hallo totale aantal steekproeven in Hallo metrische geschiedenis. |
| HistoryBeginTime() |Retourneert Hallo tijdstempel van Hallo oudste beschikbaar steekproef voor Hallo metriek. |
| GetSamplePercent() |Retourneert Hallo percentage van de voorbeelden die beschikbaar voor een bepaald tijdsinterval zijn. Bijvoorbeeld:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Omdat Hallo `GetSample` methode mislukt als Hallo percentage van de voorbeelden die zijn geretourneerd, kleiner dan Hallo is `samplePercent` opgegeven, kunt u Hallo `GetSamplePercent` methode toocheck eerste. Vervolgens kunt u een alternatieve actie uitvoeren onvoldoende voorbeelden aanwezig zijn, zonder automatische schaling evaluatie Hallo stoppen. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Voorbeelden en voorbeeld percentage Hallo *GetSample()* methode
Hallo hoofdbewerking van een formule voor automatisch schalen is tooobtain taken en resources metrische gegevens en past u de poolgrootte op basis van die gegevens. Hierdoor is het belangrijk toohave een duidelijk beeld van de wisselwerking tussen de formules automatisch schalen met metrische gegevens (voorbeelden).

**Voorbeelden**

Hallo Batch-service wordt regelmatig duurt voorbeelden van taken en resources metrische gegevens en maakt u ze beschikbaar tooyour automatisch schalen formules. Deze voorbeelden worden elke 30 seconden door Hallo Batch-service geregistreerd. Er is echter meestal een vertraging tussen wanneer deze voorbeelden zijn vastgelegd, en wanneer ze worden beschikbaar gesteld te (en kunnen worden gelezen door) automatisch schalen formules. Bovendien vanwege toovarious factoren zoals netwerk- of andere problemen infrastructuur, steekproeven mogelijk niet geregistreerd voor een bepaalde interval.

**Percentage van de steekproef**

Wanneer `samplePercent` toohello wordt doorgegeven `GetSample()` methode of Hallo `GetSamplePercent()` methode wordt aangeroepen, _procent_ verwijst tooa vergelijking tussen Hallo mogelijke totale aantal voorbeelden die zijn vastgelegd door Hallo Batch-service en Hallo aantal voorbeelden die de formule voor automatisch schalen beschikbaar tooyour zijn.

We bekijken een timespan 10 minuten als voorbeeld. Omdat voorbeelden worden elke 30 seconden binnen een timespan 10 minuten vastgelegd, zou Hallo maximum aantal voorbeelden die zijn vastgelegd door de Batch 20 steekproeven (2 per minuut) zijn. Echter, vanwege toohello inherente latentie Hallo reporting mechanisme en andere problemen in Azure, kunnen er alleen 15 voorbeelden die beschikbaar tooyour automatisch schalen formule voor het lezen zijn. Ja, bijvoorbeeld voor deze periode 10 minuten alleen 75% van totaal aantal steekproeven vastgelegd Hallo mogelijk beschikbaar tooyour formule.

**GetSample() en voorbeeld-bereiken**

Automatisch schalen formules worden gaat toobe groeit en uw pools verkleinen &mdash; knooppunten toe te voegen of te verwijderen van knooppunten. Omdat knooppunten geld kosten, wilt u tooensure met formules een intelligente methode van de analyse op basis van voldoende gegevens. Daarom raden we u een trending-type-analyse gebruiken in uw formules. Dit type groeit en uw pools op basis van een bereik van verzamelde steekproeven verkleind.

toodo dus gebruiken `GetSample(interval look-back start, interval look-back end)` tooreturn een vector van voorbeelden:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Wanneer Hallo boven de regel wordt geëvalueerd door de Batch, wordt een reeks voorbeelden als vector van waarden. Bijvoorbeeld:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Zodra u Hallo vector van voorbeelden hebt verzameld, vervolgens kunt u functies zoals `min()`, `max()`, en `avg()` tooderive zinvolle waarden uit Hallo verzameld bereik.

Voor extra beveiliging kunt u een formule-evaluatie toofail afdwingen als minder dan een bepaald percentage van het voorbeeld beschikbaar voor een bepaalde periode is. Wanneer u een formule-evaluatie toofail afdwingt, vertelt u Batch toocease verdere evaluatie van de formule Hallo Hallo opgegeven percentage van de voorbeelden is niet beschikbaar als. In dit geval worden niet gewijzigd toohello poolgrootte. toospecify vereist percentage van de voorbeelden voor Hallo evaluatie toosucceed, dit opgeven als de derde parameter te Hallo`GetSample()`. Hier wordt een vereiste van 75 procent van de voorbeelden is opgegeven:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Omdat er een vertraging optreden in de steekproef beschikbaarheid, is het belangrijk tooalways Geef een periode met een uiterlijk-back-begintijd die ouder is dan een minuut. Het duurt ongeveer een minuut voor voorbeelden toopropagate via Hallo-systeem, dus voorbeelden in Hallo bereik `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` mogelijk niet beschikbaar. Nogmaals, kunt u Hallo percentage parameter van `GetSample()` tooforce een bepaalde voorbeeld percentage vereiste.

> [!IMPORTANT]
> We **aangeraden** die u hebt **voorkomen relying *alleen* op `GetSample(1)` in formules automatisch schalen**. Dit komt doordat `GetSample(1)` in wezen zegt toohello Batch-service, "Geef me Hallo laatste steekproef die u hebt, niet van belang hoe lang geleden u opgehaald." Omdat dit slechts een enkele voorbeeld is en kan een oudere voorbeeld, mogelijk vertegenwoordiger van grotere afbeelding Hallo van recente taak of resource staat niet meer. Als u gebruik maakt van `GetSample(1)`en zorg ervoor dat het deel van een grotere instructie uitmaakt niet Hallo alleen gegevenspunt dat afhankelijk is van de formule.
>
>

## <a name="metrics"></a>Metrische gegevens
U kunt zowel de bron- als de taak metrische gegevens gebruiken wanneer u bij het definiëren van een formule. U aanpassen Hallo doelaantal toegewezen knooppunten in het Hallo-groep op basis van Hallo metrische gegevens die u ophalen en evalueren. Zie Hallo [variabelen](#variables) sectie hierboven voor meer informatie over elke metriek.

<table>
  <tr>
    <th>Gegevens</th>
    <th>Beschrijving</th>
  </tr>
  <tr>
    <td><b>Resource</b></td>
    <td><p>Metrische gegevens voor resources zijn gebaseerd op Hallo CPU, Hallo bandbreedte, geheugengebruik Hallo van rekenknooppunten en Hallo aantal knooppunten.</p>
        <p> Deze service gedefinieerde variabelen zijn handig voor het uitvoeren van aanpassingen op basis van het aantal knooppunten:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Deze service gedefinieerde variabelen zijn nuttig voor het uitvoeren van aanpassingen op basis van knooppunt Resourcegebruik:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Taak</b></td>
    <td><p>Taak metrische gegevens op basis van Hallo status van taken, zoals actief, in behandeling, en voltooid. Hallo zijn volgende service gedefinieerde variabelen handig voor groepsgrootte aanpassingen op basis van de taak metrische gegevens:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Schrijven van een formule voor automatisch schalen
U een formule voor automatisch schalen verder door de instructies die gebruikmaken van Hallo hierboven onderdelen vormen en vervolgens deze instructies naar een volledige formule combineren. In deze sectie maken we een formule voor het automatisch schalen van voorbeeld die een echte vergroten/verkleinen beslissingen kunt uitvoeren.

Eerst laten we Hallo vereisten definiëren voor onze nieuwe formule voor automatisch schalen. Hallo formule moet het volgende doen:

1. Hallo doelaantal knooppunten in een pool speciale berekenings verhogen als hoog CPU-gebruik.
2. Hallo doelaantal knooppunten in een pool speciale berekenings afnemen als CPU-gebruik laag is.
3. Maximum aantal toegewezen knooppunten too400 Hallo altijd beperken.

tooincrease hello aantal knooppunten hoog CPU-gebruik tijdens het Hallo-instructie die de gebruiker gedefinieerde variabele vult definiëren (`$totalDedicatedNodes`) met een waarde die is 110 procent van Hallo Huidig doelaantal toegewezen knooppunten, maar alleen als Hallo minimale gemiddelde CPU-gebruik tijdens het Hallo was de laatste tien minuten dan 70 procent. Gebruik anders Hallo-waarde voor het huidige aantal toegewezen knooppunten Hallo.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

te*verkleinen* aantal toegewezen knooppunten Hallo tijdens het lage CPU-gebruik, volgende instructie in onze formule sets Hallo Hallo dezelfde `$totalDedicatedNodes` variabele too90 procent van Hallo Huidig doelaantal toegewezen knooppunten als hello gemiddelde CPU-gebruik in Hallo is afgelopen 60 minuten onder 20 procent. Gebruik anders de huidige waarde van Hallo `$totalDedicatedNodes` die we ingevuld in bovenstaande Hallo-instructie.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Hallo doelaantal speciale berekenings-knooppunten maximaal 400 tooa nu beperken:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Dit is de volledige formule Hallo:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Een pool automatisch schalen ingeschakeld maken met .NET

een groep met automatisch schalen die zijn ingeschakeld in .NET toocreate als volgt te werk:

1. Maak Hallo-adresgroep met [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Set Hallo [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) eigenschap te`true`.
3. Set Hallo [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) eigenschap met de formule voor automatisch schalen.
4. (Optioneel) Set Hallo [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) eigenschap (de standaardwaarde is 15 minuten).
5. Hallo-adresgroep met doorvoeren [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) of [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Hallo maakt volgende codefragment een groep voor automatisch schalen die zijn ingeschakeld in .NET. Hallo stelt van pool automatisch schalen formule Hallo doelaantal knooppunten toegewezen too5 op maandag en 1 op om de dag van week Hallo. Hallo [automatisch vergroten/verkleinen interval](#automatic-scaling-interval) is too30 minuten ingesteld. In deze en andere codefragmenten C# in dit artikel Hallo `myBatchClient` is een goed geïnitialiseerd exemplaar van Hallo [BatchClient] [ net_batchclient] klasse.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Wanneer u een groep automatisch schalen ingeschakeld maakt, geef geen Hallo _targetDedicatedComputeNodes_ parameter of Hallo _targetLowPriorityComputeNodes_ parameter op Hallo aanroepen te **CreatePool**. Geef in plaats daarvan Hallo **AutoScaleEnabled** en **AutoScaleFormula** eigenschappen op Hallo van toepassingen. Hallo-waarden voor deze eigenschappen bepalen Hallo doelaantal van elk type knooppunt. Bovendien toomanually vergroten of verkleinen van een groep automatisch schalen is ingeschakeld (bijvoorbeeld met [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), eerste **uitschakelen** automatisch schalen op Hallo groep en vervolgens het formaat.
>
>

Bovendien tooBatch .NET, kunt u een van de andere Hallo [Batch-SDK's](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell-cmdlets](batch-powershell-cmdlets-get-started.md), en Hallo [Batch CLI](batch-cli-get-started.md)tooconfigure automatisch schalen.


### <a name="automatic-scaling-interval"></a>Interval voor automatisch schalen
Standaard aangepast Hallo Batch-service een groepsgrootte tooits volgens de formule voor automatisch schalen om de 15 minuten. Dit interval kan worden geconfigureerd met behulp van Hallo groepseigenschappen te volgen:

* [CloudPool.AutoScaleEvaluationInterval] [ net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval] [ rest_autoscaleinterval] (REST-API)

Hallo minimuminterval is vijf minuten en maximale Hallo is 168 uur. Als een interval buiten dit bereik is opgegeven, geeft Hallo Batch-service een fout Ongeldige aanvraag (400).

> [!NOTE]
> Automatisch schalen is niet op dit moment beoogde toorespond toochanges in minder dan een minuut, maar in plaats daarvan is tooadjust Hallo grootte van uw pool geleidelijk bedoeld als u een werkbelasting worden uitgevoerd.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Automatisch schalen op een bestaande toepassingen inschakelen

Elke Batch-SDK biedt een manier tooenable automatisch schalen. Bijvoorbeeld:

* [BatchClient.PoolOperations.EnableAutoScaleAsync] [ net_enableautoscaleasync] (Batch .NET)
* [Inschakelen van automatisch schalen op een pool] [ rest_enableautoscale] (REST-API)

Wanneer u automatisch schalen op een bestaande pool inschakelt, houd er rekening mee Hallo volgende punten:

* Als automatische schaling is momenteel uitgeschakeld op Hallo van toepassingen wanneer u automatisch schalen Hallo aanvraag tooenable verzendt, moet u een formule voor automatisch schalen die geldige opgeven wanneer u Hallo aanvraag verzendt. U kunt optioneel een evaluatie-interval voor automatisch schalen opgeven. Als u een interval niet opgeeft, wordt de standaardwaarde Hallo van 15 minuten gebruikt.
* Als voor automatisch schalen die momenteel is ingeschakeld op Hallo van toepassingen, kunt u een formule voor automatisch schalen, een evaluatie-interval of beide opgeven. U moet ten minste één van deze eigenschappen opgeven.

  * Als u een nieuwe evaluatie interval voor automatisch schalen opgeeft, bestaande evaluatieplanning hello wordt gestopt en er wordt een nieuw schema gestart. Hallo nieuwe planning start tijdstip is Hallo op welke Hallo aanvraag tooenable automatisch schalen is uitgegeven.
  * Als u beide hello automatisch schalen formule of evaluatie-interval weglaat, blijft Hallo Batch-service toouse Hallo huidige waarde van de instelling.

> [!NOTE]
> Als u de waarden voor Hallo opgegeven *targetDedicatedComputeNodes* of *targetLowPriorityComputeNodes* parameters Hallo **CreatePool** methode wanneer u Hallo gemaakt groep van toepassingen in .NET, of voor Hallo vergelijkbare parameters in een andere taal, worden deze waarden worden genegeerd tijdens het Hallo automatisch vergroten / verkleinen formule wordt geëvalueerd.
>
>

Dit C#-codefragment maakt gebruik van Hallo [Batch .NET] [ net_api] bibliotheek tooenable automatisch schalen op een bestaande toepassingen:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Bijwerken van een formule voor automatisch schalen

op een bestaande automatisch schalen ingeschakeld toepassingen, aanroep Hallo bewerking tooenable automatisch schalen opnieuw met de nieuwe formule Hallo tooupdate Hallo-formule. Bijvoorbeeld, als u automatisch schalen is al ingeschakeld op `myexistingpool` wanneer Hallo na .NET-code wordt uitgevoerd, de formule voor automatisch schalen is vervangen door Hallo inhoud van `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Hallo-update-interval voor automatisch schalen

tooupdate hello automatisch schalen evaluatie-interval van een bestaande automatisch schalen ingeschakeld pool, aanroep Hallo bewerking tooenable automatisch schalen opnieuw met een nieuwe hello-interval. Bijvoorbeeld: tooset Hallo automatisch schalen evaluatie interval too60 minuten voor een pool die al automatisch schalen in .NET is ingeschakeld:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Evalueren van een formule voor automatisch schalen

U kunt een formule evalueren voordat dit wordt toegepast tooa van toepassingen. Op deze manier kunt u Hallo formule toosee hoe de instructies evalueren voordat u Hallo formule in productie plaatsen testen.

tooevaluate een formule voor automatisch schalen, moet u eerst automatisch schalen op Hallo van toepassingen met een geldige formule inschakelen. tootest een formule in een groep die nog geen automatisch schalen is ingeschakeld, gebruik Hallo één regel formule `$TargetDedicatedNodes = 0` wanneer u automatisch schalen voor het eerst inschakelt. Gebruik vervolgens een Hallo tooevaluate Hallo formule gewenste tootest te volgen:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) of [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Deze methoden Batch .NET vereisen Hallo-ID van een bestaande pool en een tekenreeks met de formule voor automatisch schalen-tooevaluate Hallo.

* [Evalueren van een formule voor automatisch schalen](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    Geef Hallo pool-ID in Hallo URI in deze aanvraag REST-API en de formule voor automatisch schalen in Hallo Hallo *autoScaleFormula* element van het Hallo-aanvraagtekst. Hallo-antwoord van Hallo-bewerking bevat informatie over de fout die mogelijk gerelateerde toohello formule.

In deze [Batch .NET] [ net_api] codefragment, we een formule voor automatisch schalen evalueren. Als Hallo van toepassingen geen automatisch schalen die zijn ingeschakeld heeft, wordt dit inschakelen eerst.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Geslaagde evaluatie van Hallo formule weergegeven in dit codefragment van de resultaten van vergelijkbaar met:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Informatie ophalen over automatisch schalen die wordt uitgevoerd

tooensure die de formule uitvoert als het is raadzaam dat u regelmatig Hallo resultaten controleren van Hallo automatisch schalen wordt uitgevoerd waarmee Batch wordt uitgevoerd op uw pool werd verwacht. toodo dus ophalen (of vernieuwen) een verwijzing toohello pool en bekijk het Hallo-eigenschappen van de laatste automatisch schalen die wordt uitgevoerd.

Hallo in Batch .NET [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) eigenschap heeft verschillende eigenschappen die informatie geven over Hallo nieuwste automatische schaling uitgevoerd op Hallo van toepassingen worden uitgevoerd:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

Hallo in Hallo REST-API, [informatie ophalen over een pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) aanvraag retourneert informatie over het Hallo-toepassingen, waaronder Hallo nieuwste automatische schaling uitgevoerd van de informatie in Hallo [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) eigenschap.

Hallo volgende C#-codefragment maakt gebruik van Hallo Batch .NET-bibliotheek tooprint informatie over Hallo laatste automatisch schalen uitvoeren op de groep _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Voorbeeld van uitvoer Hallo voorgaande codefragment:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Voorbeeld voor automatisch schalen formules
Bekijken we enkele formules die verschillende manieren tooadjust Hallo hoeveelheid rekenresources in een pool weergeven.

### <a name="example-1-time-based-adjustment"></a>Voorbeeld 1: Op basis van tijd aanpassing
Stel dat u wilt dat tooadjust Hallo-groepsgrootte op basis van de dag van week Hallo Hallo en het tijdstip van de dag. Dit voorbeeld toont hoe tooincrease of afname Hallo aantal knooppunten in Hallo groep dienovereenkomstig.

Hallo formule verkrijgt eerst Hallo huidige tijd. Als dit een weekdag (1-5 is) en binnen werkuren (8 AM too6 PM), Hallo doel groepsgrootte too20 knooppunten is ingesteld. Anders wordt deze ingesteld too10 knooppunten.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Voorbeeld 2: Taakgebaseerde aanpassing
Hallo-groepsgrootte wordt aangepast op basis van het aantal taken in de wachtrij Hallo Hallo in dit voorbeeld. Alle opmerkingen en regeleinden zijn acceptabel in formule tekenreeksen.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Voorbeeld 3: Accounting voor parallelle taken
In dit voorbeeld wordt aangepast op basis van het aantal taken Hallo Hallo-groepsgrootte. Deze formule houdt ook account Hallo [MaxTasksPerComputeNode] [ net_maxtasks] waarde die is ingesteld voor Hallo van toepassingen. Deze methode is handig in situaties waar [parallelle uitvoering van de taak](batch-parallel-node-tasks.md) is ingeschakeld op uw pool.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Voorbeeld 4: De grootte van een eerste groep van toepassingen instellen
Het aantal knooppunten in dit voorbeeld toont een C# code codefragment met een formule voor automatisch schalen die ingesteld Hallo groep grootte tooa opgegeven voor een eerste periode. Vervolgens wordt deze aangepast Hallo poolgrootte op basis van het aantal uitgevoerd Hallo en actieve taken na de initiële Hallo-periode is verstreken.

Hallo formule in het volgende codefragment Hallo:

* Hallo initiële adresgroep instellen grootte toofour knooppunten.
* Niet aangepast Hallo groepsgrootte binnen Hallo eerste 10 minuten van de levenscyclus van Hallo pool.
* Na 10 minuten verkrijgt Hallo max-waarde van Hallo nummer van het uitvoeren en actieve taken binnen Hallo afgelopen 60 minuten.
  * Als beide waarden zijn 0 (waarmee wordt aangegeven dat er geen taken uitgevoerd of is actief in Hallo laatste 60 minuten zijn), is de poolgrootte Hallo too0 ingesteld.
  * Als een waarde groter dan nul is, worden niet gewijzigd.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Volgende stappen
* [Azure Batch compute Resourcegebruik met gelijktijdige knooppunt taken maximaliseren](batch-parallel-node-tasks.md) bevat details over hoe u meerdere taken tegelijkertijd op Hallo van rekenknooppunten in uw groep uitvoeren kunt. Bovendien tooautoscaling, deze functie kunt toolower taak duur voor sommige werkbelastingen, u geld besparen.
* Voor een andere efficiëntie booster, moet u ervoor zorgen dat uw Batch-toepassing-query's Batch-service in de meeste optimaal Hallo Hallo. Zie [hello Azure Batch-service efficiënt Query](batch-efficient-list-queries.md) toolearn hoe toolimit Hallo hoeveelheid gegevens die over de kabel Hallo als u een query Hallo status van mogelijk duizenden compute-knooppunten of taken.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
