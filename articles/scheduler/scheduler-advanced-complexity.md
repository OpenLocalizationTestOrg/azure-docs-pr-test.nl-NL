---
title: aaaHow tooBuild complexe schema's en geavanceerde terugkeerpatronen met Azure Scheduler
description: Hoe tooBuild plant u complexe en geavanceerde terugkeerpatronen met Azure Scheduler
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Hoe tooBuild plant u complexe en geavanceerde terugkeerpatronen met Azure Scheduler
## <a name="overview"></a>Overzicht
Hallo-kern van een Azure Scheduler-taak is Hallo *planning*. Hallo planning bepaalt wanneer en hoe Hallo Scheduler Hallo-taak uitvoert.

Azure Scheduler kunt u toospecify verschillende eenmalige en terugkerende planningen voor een taak. *Eenmalige* planningen effectief eenmaal op een opgegeven periode – is gestart, zijn *terugkerende* schema's die slechts één keer worden uitgevoerd. Terugkerende planningen geactiveerd op een vooraf vastgestelde frequentie.

Met deze flexibiliteit kunt Azure Scheduler u ondersteuning voor een groot aantal bedrijfsscenario's:

* Opruimen van periodieke gegevens – bijvoorbeeld dagelijks verwijderen voor alle tweets ouder is dan 3 maanden
* Het archiveren – bijvoorbeeld elke maand, push factuur geschiedenis toobackup service
* Aanvragen voor externe gegevens – bijvoorbeeld pull elke 15 minuten,-weerrapport door nieuwe ski van NOAA
* Afbeelding van verwerking – bijvoorbeeld elke weekdag tijdens de daluren, gebruikt u cloud computing toocompress afbeeldingen geüpload die dag

In dit artikel doorlopen we voorbeeld taken die u met Azure Scheduler maken kunt. We bieden Hallo JSON-gegevens die worden beschreven van het schema. Als u Hallo [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx), kunt u deze dezelfde JSON voor [maken van een Azure Scheduler-taak](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
Hallo die veel voorbeelden in dit onderwerp ziet Hallo breedte van de scenario's die ondersteuning biedt voor Azure Scheduler. Ruime zin is laten deze voorbeelden zien hoe toocreate schema's voor veel gedrag patronen, met inbegrip van toepassingsgroepen onderstaande Hallo:

* Eenmaal uitvoeren op een bepaalde datum en tijd
* Uitvoeren en een aantal expliciete keer herhaald
* Direct uitgevoerd en herhaald
* Voer en herhaald elke  *n*  minuten, uren, dagen, weken of maanden, beginnend bij een bepaalde tijd
* Voer en herhaald in wekelijkse of maandelijkse frequentie, maar alleen op bepaalde dagen, specifieke dagen van de week of specifieke dagen van maand
* Voer en op meerdere keren in een periode – bijvoorbeeld laatste vrijdag en maandag van elke maand of op 5:15 uur en 17:15:00 uur elke dag herhaald

## <a name="dates-and-datetimes"></a>Datum en tijd
Datums in Azure Scheduler-taken Volg Hallo [ISO 8601-specificatie](http://en.wikipedia.org/wiki/ISO_8601) en bevatten alleen Hallo datum.

Voer de datum / tijd-verwijzingen in Azure Scheduler-taken Hallo [ISO 8601-specificatie](http://en.wikipedia.org/wiki/ISO_8601) en zowel datum en tijd onderdelen bevatten. Een datum / tijd waarvoor geen een UTC-afwijking wordt aangenomen dat toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Procedure: JSON en REST-API gebruiken voor het maken van planningen
een eenvoudige planning met toocreate Hallo [Azure Scheduler REST API](https://msdn.microsoft.com/library/mt629143), eerste [registreren van uw abonnement met een resourceprovider](https://msdn.microsoft.com/library/azure/dn790548.aspx) (Hallo providernaam voor de planner is  *Microsoft.Scheduler*), vervolgens [maken van een taakverzameling](https://msdn.microsoft.com/library/mt629159.aspx), en tot slot [maken van een taak](https://msdn.microsoft.com/library/mt629145.aspx). Wanneer u een taak maakt, kunt u de planning en een terugkeerpatroon met een JSON zoals Hallo een overgenomen hieronder kunt opgeven:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Overzicht: Taak Schema basisbeginselen
Hallo volgende tabel biedt een overzicht van Hallo belangrijke elementen gerelateerde toorecurrence en in een taak plannen:

| **De naam van de JSON** | **Beschrijving** |
|:--- |:--- |
| ***startTime*** |*startTime* is een datum / tijd. Voor eenvoudige planningen *startTime* is het eerste exemplaar Hallo en Hallo taak gaat voor complexe schema's niet eerder dan *startTime*. |
| ***terugkeerpatroon*** |Hallo *terugkeerpatroon* object geeft terugkeerpatroon regels voor Hallo taak en Hallo terugkeerpatroon Hallo taak wordt uitgevoerd waarbij. Hallo planningsterugkeerobject ondersteunt Hallo elementen *frequentie, interval, endTime, count,* en *planning*. Als *terugkeerpatroon* is gedefinieerd, *frequentie* is vereist; andere elementen van Hallo *terugkeerpatroon* zijn optioneel. |
| ***frequentie*** |Hallo *frequentie* Hallo frequentie eenheid welke Hallo taak terugkeert type string. Ondersteunde waarden zijn *'minuut', 'uur', 'day', 'week'* of *"maand".* |
| ***interval*** |Hallo *interval* een positief geheel getal is en geeft hello-interval voor Hallo *frequentie* waarmee wordt bepaald hoe vaak hello taak wordt uitgevoerd. Bijvoorbeeld, als *interval* 3 en *frequentie* ' week ' hello taak herhaald om de drie weken. Azure Scheduler ondersteunt maximaal *interval* 18 maanden voor maandelijkse frequentie, 78 weken voor de frequentie wekelijks of 548 dagen voor de frequentie van dagelijkse. Voor de uur- en minuut frequentie Hallo ondersteund bereik is 1 < = *interval* < = 1000. |
| ***Eindtijd*** |Hallo *endTime* tekenreeks Hallo datum / tijd-voorbij welke Hallo taak dient niet te worden uitgevoerd. Het is niet geldig toohave een *endTime* in de afgelopen Hallo. Als er geen *endTime* of count wordt opgegeven, Hallo taak oneindig wordt uitgevoerd. Beide *endTime* en *aantal* kan niet worden opgenomen voor Hallo dezelfde taak. |
| ***aantal*** |<p>Hallo *aantal* een positief geheel getal (groter dan nul) waarmee Hallo aantal keer dat deze taak voordat wordt voltooid uitvoeren moet.</p><p>Hallo *aantal* vertegenwoordigt Hallo aantal keren Hallo-taak wordt uitgevoerd voordat er bepaald wordt voltooid. Bijvoorbeeld: voor een taak die dagelijks wordt uitgevoerd met *aantal* 5 en de begindatum van maandag, Hallo-taak is voltooid na uitvoering op vrijdag. Als Hallo start datum valt in de afgelopen hello, Hallo eerste uitvoering wordt berekend op basis van Hallo Aanmaaktijd.</p><p>Als er geen *endTime* of *aantal* is opgegeven, Hallo taak oneindig wordt uitgevoerd. Beide *endTime* en *aantal* kan niet worden opgenomen voor Hallo dezelfde taak.</p> |
| ***planning*** |Een taak met een opgegeven frequentie wijzigt het terugkeerpatroon op basis van een terugkerende planning. Een *planning* bevat wijzigingen die op basis van de minuten, uren, weekdagen, dagen van de maand en weeknummer. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Overzicht: De taak Schema standaardwaarden, limieten en voorbeelden
Dit overzicht we Bespreek elk van deze elementen in detail.

| **De naam van de JSON** | **Waardetype** | **Vereist?** | **Standaardwaarde** | **Geldige waarden** | **Voorbeeld** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |Tekenreeks |Nee |Geen |Datums en tijden volgens ISO 8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***terugkeerpatroon*** |Object |Nee |Geen |Recurrence-object |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequentie*** |Tekenreeks |Ja |Geen |'minuut', 'uur', 'day', 'week', 'maand' |<code>"frequency" : "hour"</code> |
| ***interval*** |Aantal |Nee |1 |1 too1000. |<code>"interval":10</code> |
| ***Eindtijd*** |Tekenreeks |Nee |Geen |Datum / tijd-waarde waarmee een tijd in toekomstige Hallo |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***aantal*** |Aantal |Nee |Geen |>= 1 |<code>"count": 5</code> |
| ***planning*** |Object |Nee |Geen |Schedule-object |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Deep Dive: *startTime*
Hallo volgende tabel opnamen hoe *startTime* bepaalt hoe een taak wordt uitgevoerd.

| **de waarde startTime** | **Geen terugkeerpatroon** | **Terugkeerpatroon. Er is geen schema** | **Terugkeerpatroon met planning** |
|:--- |:--- |:--- |:--- |
| **Er is geen begintijd** |Eenmaal onmiddellijk uitvoeren |Eenmaal onmiddellijk uitvoeren. Bij een volgende uitvoering op basis van het berekenen van de laatste uitvoertijd uitvoeren |<p>Eenmaal onmiddellijk uitvoeren</p><p>Volgende uitvoeringen worden op basis van de terugkeerplanning uitgevoerd</p> |
| **De begintijd in het verleden** |Eenmaal onmiddellijk uitvoeren |<p>Eerste toekomstige uitvoeringstijd berekenen na de begintijd liggen, en op dat moment worden uitgevoerd</p><p>Bij een volgende uitvoering op basis van oncalculating uitvoeren vanaf laatste uitvoeringstijd</p><p>Zie het voorbeeld na deze tabel voor een nadere uitleg</p> |<p>Taak gestart *niet sooner dan* Hallo begintijd opgegeven. de eerste instantie Hallo is gebaseerd op Hallo planning berekend op basis van de begintijd Hallo</p><p>Volgende uitvoeringen worden op basis van de terugkeerplanning uitgevoerd</p> |
| **De begintijd in de toekomst, of op dit moment** |Eenmaal op de opgegeven begintijd uitvoeren |<p>Eenmaal op de opgegeven begintijd uitvoeren</p><p>Bij een volgende uitvoering op basis van het berekenen van de laatste uitvoertijd uitvoeren</p> |<p>Taak gestart *niet sooner dan* Hallo begintijd opgegeven. de eerste instantie Hallo is gebaseerd op Hallo planning berekend op basis van de begintijd Hallo</p><p>Volgende uitvoeringen worden op basis van de terugkeerplanning uitgevoerd</p> |

We bekijken een voorbeeld van wat er gebeurt wanneer *startTime* Hallo vroeger, wordt met *terugkeerpatroon* , maar er is geen *planning*.  Wordt ervan uitgegaan dat Hallo huidige tijd is 2015-04-08 13:00 *startTime* 2015-04-07 14:00 en *terugkeerpatroon* is elke 2 dagen (gedefinieerd met *frequentie*: dag en *interval*: 2.) Houd er rekening mee dat Hallo *startTime* zich in de afgelopen Hallo en vindt plaats voordat de huidige tijd Hallo

In deze omstandigheden Hallo *eerste uitvoering* 2015-04-09 worden om 14:00 uur\. Hallo Scheduler engine berekent instanties van de uitvoering van de begintijd Hallo.  Alle instanties in de afgelopen Hallo verwijderd. Hallo-engine gebruikt de volgende Hallo-exemplaar dat zich in toekomstige Hallo voordoet.  Dus in dit geval *startTime* 2015-04-07 op 14:00 uur is, waardoor de Hallo volgende exemplaar is 2 dagen na deze periode kan die 2015-04-09 op 14:00 uur.

Houd er rekening mee dat de eerste uitvoering Hallo Hallo zou zijn hetzelfde, zelfs als Hallo startTime 2015-04-05 14:00 of 2015-04-01 14:00\. Na de eerste uitvoering hello, een volgende uitvoering wordt berekend op basis van Hallo gepland – zodat u deze zou op 2015-04-11 op 14:00 uur, vervolgens 2015-04-13 op 14:00 uur, vervolgens 2015-04-15 op 14:00 uur, enzovoort.

Ten slotte wanneer een taak heeft een planning als uren en/of minuten zijn niet ingesteld in Hallo planning, ze toohello standaarduren en/of minuten van de eerste uitvoering hello, respectievelijk.

## <a name="deep-dive-schedule"></a>Deep Dive: *planning*
Enerzijds een *planning* kunt *limiet* Hallo aantal uitvoeringen van de taak.  Bijvoorbeeld, als een taak met een frequentie "maand" heeft een *planning* die wordt uitgevoerd op enige dag 31, Hallo-taak wordt uitgevoerd in alleen deze maanden waarvoor een 31<sup>st</sup> dag.

Op Hallo daarentegen een *planning* kunt ook *Vouw* Hallo aantal uitvoeringen van de taak. Bijvoorbeeld, als een taak met een frequentie "maand" heeft een *planning* dat wordt uitgevoerd op dagen van de maand 1 en 2 Hallo-taak wordt uitgevoerd op Hallo 1<sup>st</sup> en 2<sup>nd</sup> dagen van maand Hallo in plaats van slechts één keer een maand.

Als meerdere schema-elementen zijn opgegeven, is het Hallo-volgorde van de evaluatie van Hallo grootste toosmallest – weeknummer, maand, dag,, weekdag, uur en minuut.

Hallo volgende tabel beschrijft *planning* elementen in detail.

| **De naam van de JSON** | **Beschrijving** | **Geldige waarden** |
|:--- |:--- |:--- |
| **minuten** |Minuten van Hallo uur op welke Hallo taak wordt uitgevoerd |<ul><li>Geheel getal, of</li><li>Matrix van gehele getallen</li></ul> |
| **uren** |Uur van Hallo dag op welke Hallo taak wordt uitgevoerd |<ul><li>Geheel getal, of</li><li>Matrix van gehele getallen</li></ul> |
| **Weekdagen** |Dagen van Hallo week Hallo taak wordt uitgevoerd. Kan alleen worden opgegeven met de frequency wekelijks. |<ul><li>"Maandag", "Dinsdag", "Woensdag", "Donderdag", "Vrijdag", "Zaterdag" of "Zondag"</li><li>Matrix van elk Hallo hierboven waarden (maximale grootte van de matrix 7)</li></ul>*Niet* hoofdlettergevoelig |
| **monthlyOccurrences** |Bepaalt welke dagen van Hallo maand Hallo taak wordt uitgevoerd. Kan alleen worden opgegeven met de frequency maandelijks. |<ul><li>Matrix van monthlyOccurrence objecten:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *dag* Hallo dag van Hallo week Hallo taak wordt uitgevoerd is, bijvoorbeeld {zondag} is elke zondag van Hallo maand. Vereist.</p><p>Het aantal exemplaren is *exemplaar* van Hallo dag tijdens Hallo maand, bijvoorbeeld {zondag, -1} is laatste zondag van de maand Hallo Hallo. Optioneel.</p> |
| **maanddagen** |Dag van Hallo maand Hallo taak wordt uitgevoerd. Kan alleen worden opgegeven met de frequency maandelijks. |<ul><li>Een waarde < = -1 en > =-31.</li><li>Een willekeurige waarde > = 1 en < = 31.</li><li>Een matrix met bovenstaande waarden</li></ul> |

## <a name="examples-recurrence-schedules"></a>Voorbeelden: Terugkerende schema 's
Hallo volgen verschillende voorbeelden van terugkerende planningen – gericht op Hallo planning object en de onderliggende elementen.

Hallo planningen hieronder alle wordt ervan uitgegaan dat Hallo *interval* too1 is ingesteld\. Bovendien moet een aannemen Hallo Hallo juiste frequentie in overeenstemming toowhat wordt *planning* – bijvoorbeeld een kan niet gebruiken frequentie 'day' en 'maanddagen' wijziging in Hallo planning. Deze beperkingen zijn hierboven beschreven.

| **Voorbeeld** | **Beschrijving** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Op 5 uur uitgevoerd elke dag. Azure Scheduler komt overeen met elke waarde in 'hours' waarbij elke waarde in 'minutes', één voor één, toocreate een lijst met alle Hallo tijden op welke Hallo taak toobe is uitgevoerd. |
| <code>{"minutes":[15], "hours":[5]}</code> |Op 5:15 uur uitgevoerd elke dag |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Uitvoeren op 5:15 uur en 17:15:00 uur elke dag |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Uitvoeren op 5:15 uur, 5:45 uur 17:15:00 uur en 17:45 uur elke dag |
| <code>{"minutes":[0,15,30,45]}</code> |Elke 15 minuten wordt uitgevoerd |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Elk uur uitgevoerd. Deze taak elk uur wordt uitgevoerd. Hallo minuut wordt beheerd door Hallo *startTime*, als er een is opgegeven of als niets wordt opgegeven door de aanmaaktijd Hallo. Bijvoorbeeld, als Hallo start tijd of Aanmaaktijd (afhankelijk van wat van toepassing) 12:25 uur is, Hallo taak worden uitgevoerd op 00:25, 01:25 02:25,..., 23:25. Hallo planning is gelijkwaardig toohaving een taak met *frequentie* van 'uur' een *interval* van 1, maar er is geen *planning*. Hallo verschil is dat dit schema kan worden gebruikt met andere *frequentie* en *interval* toocreate andere taken te. Bijvoorbeeld, als hello *frequentie* zijn "maand", Hallo schema uitgevoerd slechts één keer per maand in plaats van elke dag als *frequentie* zijn "dag" |
| <code>{minutes:[0]}</code> |Elk uur op Hallo uur uitgevoerd. Deze taak wordt ook uitgevoerd voor elk uur, maar ook op Hallo uur (bijvoorbeeld 12: 00 A.M., 1 uur 2 uur, enz.) Dit is gelijkwaardig tooa taak met de frequentie van een "uur", een startTime met nul minuten en zonder schema als Hallo frequentie zijn 'day', maar als de frequentie Hallo 'week' of 'maand', Hallo planning respectievelijk slechts één dag een week of maand, één dag zou uitvoeren. |
| <code>{"minutes":[15]}</code> |Op 15 minuten worden uitgevoerd uit het verleden uur elk uur. Wordt elk uur uitgevoerd vanaf 00:15, 01:15, 02,15, enz. en eindigt om 22:15 en 23:15. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Uitvoeren op 17: 00 uur op zaterdag elke Week |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uitvoeren op 17: 00 uur op maandag, woensdag en vrijdag elke Week |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uitvoeren op 17:15:00 uur en 17:45 uur op maandag, woensdag en vrijdag elke Week |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uitvoeren op 5 uur en 17: 00 uur op maandag, woensdag en vrijdag elke Week |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uitvoeren op 5:15 uur, 5:45 uur 17:15:00 uur en 17:45 uur op maandag, woensdag en vrijdag elke Week |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Wordt elke 15 minuten uitgevoerd op weekdagen |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Elke 15 minuten wordt uitgevoerd op weekdagen tussen 9: 00 uur en 4:45 uur |
| <code>{"weekDays":["sunday"]}</code> |Uitvoeren op zondag tijdens het starten |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Uitvoeren op dinsdag en donderdag tijdens het starten |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Uitvoeren om 6.00 uur op Hallo 28 dag van elke maand (ervan uitgaande dat de frequentie van de maand) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Op Hallo laatste dag van de maand hello om 6.00 uur uitgevoerd. Als u een taak op Hallo toorun laatste dag van een maand wilt, gebruik dan -1 in plaats van de dag 28, 29, 30 of 31. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Eerste en laatste dag van elke maand om 6.00 uur worden uitgevoerd op Hallo |
| <code>{monthDays":[1,-1]}</code> |Uitvoeren op Hallo eerste en laatste dag van elke maand op tijd starten |
| <code>{monthDays":[1,14]}</code> |Uitvoeren op Hallo eerste en Fourteenth dag van elke maand op tijd starten |
| <code>{monthDays":[2]}</code> |Voer op Hallo tweede dag Hallo maand begintijd |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Voer op de eerste vrijdag van elke maand om 05: 00 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: De gegevens worden uitgevoerd op de eerste vrijdag van elke maand tijdens het starten |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Voer op de derde vrijdag uit einde van de maand, elke maand, tijdens het starten |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Op de eerste en laatste vrijdag van elke maand 5:15 uur uitvoeren |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Voer op de eerste en laatste vrijdag van elke maand tijdens het starten |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Voer op vijfde vrijdag van elke maand tijdens het starten. Als er geen vijfde vrijdag in een maand, dit wordt niet uitgevoerd, omdat het geplande toorun op alleen vijfde vrijdag. U overweegt -1 gebruik in plaats van 5 voor Hallo-exemplaar, als u wilt dat toorun Hallo-taak op Hallo laatste vrijdag van Hallo maand plaatsvinden. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Om de 15 minuten worden uitgevoerd op de laatste vrijdag van Hallo maand |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Uitvoeren op 5:15 uur, 5:45 uur 17:15:00 uur en 17:45 uur op Hallo 3e woensdag van elke maand |

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

