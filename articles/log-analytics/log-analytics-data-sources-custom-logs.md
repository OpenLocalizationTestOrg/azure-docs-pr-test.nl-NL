---
title: aangepaste aaaCollect wordt geregistreerd in OMS Log Analytics | Microsoft Docs
description: Log Analytics kunt verzamelen van gebeurtenissen uit tekstbestanden op Windows- en Linux-computers.  In dit artikel wordt beschreven hoe een nieuwe aangepaste logboek toodefine en details van Hallo records ze in Hallo OMS-opslagplaats maken.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Aangepaste logboeken in Log Analytics
Hallo aangepaste logboeken van de gegevensbron in Log Analytics kunt u toocollect gebeurtenissen uit tekstbestanden op Windows- en Linux-computers. Veel toepassingen logboekbestanden informatie tootext in plaats van standaard logboekregistratieservices zoals Windows-gebeurtenislogboek of Syslog.  Zodra verzameld, kunt u elke record in logboek in tooindividual velden met Hallo Hallo parseren [aangepaste velden](log-analytics-custom-fields.md) functie van logboekanalyse.

![Aangepaste logboekgegevens verzameld](media/log-analytics-data-sources-custom-logs/overview.png)

Hallo-logboek bestanden toobe verzameld moet overeenkomen met de Hallo criteria te volgen.

- Hallo logboek moet hebben één vermelding per regel of een tijdstempel die overeenkomt met een van de volgende Hallo aan begin van elke vermelding hello indelingen gebruiken.

    JJJJ-MM-DD: MM: SS<br>M/D/JJJJ UU: MM: SS AM/PM <br>Ma DD JJJJ: mm: ss

- Hallo-logboekbestand mag geen circulaire updates toestaan waar Hallo-bestand wordt overschreven met nieuwe gegevens.
- Hallo-logboekbestand moet gebruiken ASCII- of UTF-8-codering.  Andere indelingen zoals UTF-16 worden niet ondersteund.

>[!NOTE]
>Als er dubbele vermeldingen in het logboekbestand hello, worden ze logboekanalyse verzamelen.  Hallo zoekresultaten wordt wel inconsistente waar Hallo filterresultaten meer gebeurtenissen dan Hallo resultaattelling weergeven.  Dit is belangrijk dat u Hallo logboek toodetermine valideren als dit probleem wordt veroorzaakt door Hallo-toepassing die wordt deze gemaakt en indien mogelijk oplossen voordat u de definitie van de verzameling aangepaste logboek Hallo maakt.  
>
  
## <a name="defining-a-custom-log"></a>Een aangepast logboek definiëren
Hallo te volgen procedure toodefine een aangepaste logboekbestand gebruiken.  Schuif toohello einde van dit artikel voor een overzicht van een steekproef van een aangepaste logboekbestanden toe te voegen.

### <a name="step-1-open-hello-custom-log-wizard"></a>Step 1. Hallo aangepast logboek Wizard openen
Hallo aangepaste logboek Wizard wordt uitgevoerd in Hallo OMS-portal en kunt u een nieuwe aangepaste logboek toocollect toodefine.

1. Hallo OMS-portal, ga te**instellingen**.
2. Klik op **gegevens** en vervolgens **aangepaste logboeken**.
3. Standaard zijn alle configuratiewijzigingen tooall agents automatisch gepusht.  Voor Linux-agents, wordt een configuratiebestand toohello Fluentd gegevensverzamelaar verzonden.  Als u toomodify dit bestand handmatig op elke Linux-agent wenst, schakelt u Hallo vak *toepassen onder configuratie toomy Linux-machines*.
4. Klik op **toevoegen +** tooopen Hallo aangepast logboek Wizard.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Stap 2. Uploaden en een voorbeeldlogboek te parseren
Begint u met een steekproef van het aangepaste logboek Hallo uploaden.  Hallo-wizard parseren en Hallo vermeldingen weergegeven in dit bestand voor u toovalidate.  Log Analytics maakt gebruik van Hallo scheidingsteken dat u tooidentify elke record opgeeft.

**Nieuwe regel** Hallo standaardscheidingsteken is en wordt gebruikt voor de logboekbestanden met één vermelding per regel.  Als Hallo regel met een datum en tijd in een van de beschikbare indelingen Hallo begint en vervolgens kunt u een **tijdstempel** scheidingsteken die ondersteuning biedt voor vermeldingen die meer dan één regel omvatten.

Als een tijdstempel scheidingsteken wordt gebruikt, wordt Hallo TimeGenerated eigenschap van elke record in OMS worden ingevuld met Hallo datum/tijd voor deze vermelding in het logboekbestand Hallo opgegeven.  Als een nieuwe regel scheidingsteken wordt gebruikt, wordt TimeGenerated gevuld met de datum en tijd of Log Analytics Hallo vermelding verzameld.

> [!NOTE]
> Log Analytics behandelt momenteel Hallo datum/tijd verzameld van een logboek met behulp van een timestamp-scheidingsteken als UTC.  Dit is binnenkort gewijzigde toouse Hallo tijdzone op Hallo-agent.
>
>

1. Klik op **Bladeren** en blader tooa-voorbeeldbestand.  Let op deze knop kan mogelijk worden gelabeld **bestand kiezen** in sommige browsers.
2. Klik op **Volgende**.
3. Hallo aangepast logboek Wizard gaat uploaden Hallo bestands- en Hallo records die wordt geïdentificeerd.
4. Hallo scheidingsteken dat wordt gebruikt tooidentify een nieuwe record en selecteer Hallo scheidingsteken waarmee beste Hallo records in het logboekbestand wijzigen.
5. Klik op **Volgende**.

### <a name="step-3-add-log-collection-paths"></a>Stap 3. Paden van logboekverzamelingen toevoegen
U moet een of meer paden definiëren op Hallo agent waar Hallo aangepaste logboekgegevens kunnen worden gevonden.  Kunt u ofwel bieden een specifiek pad en naam voor het logboekbestand Hallo of kunt u een pad opgeven met een jokerteken voor Hallo-naam.  Dit biedt ondersteuning voor toepassingen die een nieuw bestand maken elke dag of wanneer een bestand een bepaalde grootte heeft bereikt.  U kunt ook meerdere paden opgeven voor één logboekbestand.

Bijvoorbeeld, een toepassing mogelijk maken een logboekbestand per dag met Hallo datum die is opgenomen in het Hallo-naam als in log20100316.txt. Een patroon voor een dergelijke logboek is mogelijk *logboek\*.txt* waarvoor tooany logboekbestand na de toepassing hello zou gelden de naamgeving van schema.

Hallo volgende tabel bevat voorbeelden van geldige patronen toospecify verschillende logboekbestanden.

| Beschrijving | Pad |
|:--- |:--- |
| Alle bestanden in *C:\Logs* met .txt-extensie op Windows-agent |C:\Logs\\\*.txt |
| Alle bestanden in *C:\Logs* met een naam die begint met het logboek en een txt-extensie op Windows-agent |C:\Logs\log\*.txt |
| Alle bestanden in */var/log/audit* met .txt-extensie op Linux-agent |/var/log/audit/*.txt |
| Alle bestanden in */var/log/audit* met een naam die begint met het logboek en een txt-extensie op Linux-agent |/var/log/audit/log\*.txt |

1. Selecteer Windows of Linux toospecify welke padindeling van het dat u toevoegt.
2. Typ in het Hallo-pad en klik op Hallo  **+**  knop.
3. Hallo proces herhalen voor elke extra paden.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Stap 4. Geef een naam en beschrijving voor het Hallo-logboek
Hallo wordt naam die u opgeeft gebruikt voor Hallo Logboektype zoals hierboven is beschreven.  Het wordt altijd eindig met _CL toodistinguish als een aangepast logboek.

1. Typ een naam voor Hallo logboek.  Hallo  **\_CL** achtervoegsel automatisch wordt geleverd.
2. Voeg een optionele **beschrijving**.
3. Klik op **volgende** toosave Hallo aangepaste logboekdefinitie.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Stap 5. Valideren dat de aangepaste logboeken Hallo worden verzameld
Het kan Hallo initiële gegevens uit een nieuwe aangepaste logboek tooappear in logboekanalyse tooan uur duren.  Start het verzamelen van gegevens van Hallo logboeken gevonden in Hallo pad opgegeven van Hallo dat u gedefinieerde Hallo aangepaste aan te melden.  Het Hallo-vermeldingen die u tijdens het maken van aangepaste logboek Hallo hebt geüpload niet behoudt, maar er al een bestaande vermeldingen in logboekbestanden Hallo die wordt gezocht naar verzamelt.

Zodra logboekanalyse verzamelen van het aangepaste logboek hello start, is de records worden beschikbaar met een zoekopdracht logboek.  Gebruik Hallo de naam die u hebt gegeven aangepaste logboekgegevens als Hallo Hallo **Type** in uw query.

> [!NOTE]
> Als Hallo RawData-eigenschap in Hallo zoeken ontbreekt, kunt u tooclose moet en Open uw browser.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Stap 6. De aangepaste logboekvermeldingen Hallo parseren
Hallo gehele logboekvermelding worden opgeslagen in één eigenschap aangeroepen **RawData**.  Wilt u waarschijnlijk tooseparate Hallo verschillende soorten informatie in elk item in afzonderlijke eigenschappen in de record Hallo opgeslagen.  U dit doen met Hallo [aangepaste velden](log-analytics-custom-fields.md) functie van logboekanalyse.

Gedetailleerde stappen voor het parseren van de aangepaste logboekvermelding Hallo worden niet hier beschreven.  Raadpleeg toohello [aangepaste velden](log-analytics-custom-fields.md) documentatie voor deze informatie.

## <a name="disabling-a-custom-log"></a>Een aangepast logboek uitschakelen
U kunt de definitie van een aangepaste logboek niet verwijderen, zodra deze is gemaakt, maar u deze uitschakelen kunt door het verwijderen van alle de paden van de verzameling.

1. Hallo OMS-portal, ga te**instellingen**.
2. Klik op **gegevens** en vervolgens **aangepaste logboeken**.
3. Klik op **Details** volgende toohello aangepaste logboek definitie toodisable.
4. Hallo verzameling paden voor de definitie van de aangepaste logboek Hallo verwijderen.

## <a name="data-collection"></a>Gegevensverzameling
Log Analytics worden nieuwe gegevens worden verzameld uit elk aangepast logboek ongeveer elke 5 minuten.  Hallo-agent wordt plaats registreren in elk logboekbestand die worden verzameld uit.  Hallo-agent voor een bepaalde periode offline gaat, klikt u vervolgens verzamelt Log Analytics vermeldingen van waar het laatst werd afgebroken, zelfs als deze vermeldingen zijn gemaakt terwijl de agent Hallo offline was.

Hallo volledige inhoud van Hallo logboekvermelding tooa één eigenschap aangeroepen worden geschreven **RawData**.  U kunt dit parseren naar meerdere eigenschappen die kunnen worden geanalyseerd en afzonderlijk worden doorzocht door te definiëren [aangepaste velden](log-analytics-custom-fields.md) nadat u het aangepaste logboek Hallo hebt gemaakt.

## <a name="custom-log-record-properties"></a>Eigenschappen van aangepaste record
Aangepaste logboekrecords hebben een type met de naam van het logboek Hallo die u voorzien en eigenschappen in de volgende tabel Hallo Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| TimeGenerated |Datum en tijd waarop Hallo record is verzameld door logboekanalyse.  Als het Hallo-logboek een scheidingsteken wordt gebruikt op basis van tijd is dit Hallo tijd verzameld van Hallo vermelding. |
| SourceSystem |Agent Hallo recordtype is verzameld. <br> OpsManager – Windows-agent, ofwel direct verbinding maken of System Center Operations Manager <br> Linux – alle Linux-agents |
| RawData |Volledige tekst van Hallo verzameld vermelding. |
| ManagementGroupName |De naam van de beheergroep Hallo voor System Center Operations beheren agents.  Dit is voor andere agents AOI -\<werkruimte-ID\> |

## <a name="log-searches-with-custom-log-records"></a>Logboek van zoekopdrachten met aangepaste logboekrecords
Records van aangepaste logboeken worden opgeslagen in de OMS-opslagplaats Hallo net als records uit een andere gegevensbron.  Hebben ze een type dat overeenkomt met Hallo-naam die u opgeeft wanneer u Hallo logboek, definieert zodat u de eigenschap Type Hallo in uw zoekopdracht tooretrieve records die van een specifieke logboekbestanden worden verzameld gebruiken kunt.

Hallo bevat volgende tabel voorbeelden van logboek-zoekopdrachten die records uit de aangepaste logboeken ophalen.

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type MyApp_CL = |Alle gebeurtenissen van een aangepaste benoemde MyApp_CL worden geregistreerd. |
| Type = MyApp_CL Severity_CF fout = |Alle gebeurtenissen van een aangepaste benoemde MyApp_CL worden geregistreerd met een waarde van *fout* in een aangepast veld met de naam *Severity_CF*. |

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.

> | Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| MyApp_CL |Alle gebeurtenissen van een aangepaste benoemde MyApp_CL worden geregistreerd. |
| MyApp_CL &#124; waar Severity_CF == "error" |Alle gebeurtenissen van een aangepaste benoemde MyApp_CL worden geregistreerd met een waarde van *fout* in een aangepast veld met de naam *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Overzicht van het toevoegen van een aangepaste logboek voorbeeld
Hallo volgende sectie wordt uitgelegd een voorbeeld van een aangepaste logboek te maken.  Hallo voorbeeldlogboek worden verzameld heeft een afzonderlijke vermelding op elke regel moet beginnen met een datum en tijd en vervolgens door komma's gescheiden velden voor de code, status en het bericht.  Enkele voorbeelden van vermeldingen worden hieronder weergegeven.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Uploaden en een voorbeeldlogboek te parseren
We bieden een van de logboekbestanden Hallo en ziet Hallo-gebeurtenissen die zullen worden verzameld.  In dit geval is de nieuwe regel een voldoende scheidingsteken.  Als een afzonderlijke vermelding in Hallo logboek echter meerdere regels omvatten kan, zou een timestamp-scheidingsteken toobe gebruikt moet.

![Uploaden en een voorbeeldlogboek te parseren](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Paden van logboekverzamelingen toevoegen
Hallo-logboekbestanden zich in de *C:\MyApp\Logs*.  Elke dag met een naam die Hallo datum in Hallo-patroon bevat wordt gemaakt door een nieuw bestand *appYYYYMMDD.log*.  Een voldoende patroon voor dit logboek zou worden *C:\MyApp\Logs\\\*.log*.

![Verzameling logboekpad](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Geef een naam en beschrijving voor het Hallo-logboek
We gebruiken een naam van *MyApp_CL* en typt u in een **beschrijving**.

![Logboeknaam](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Valideren dat de aangepaste logboeken Hallo worden verzameld
We gebruiken een query voor *Type = MyApp_CL* tooreturn alle records van Hallo verzamelde logboekgegevens.

![Logboek query met geen aangepaste velden](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>De aangepaste logboekvermeldingen Hallo parseren
We gebruiken van aangepaste velden toodefine hello *EventTime*, *Code*, *Status*, en *bericht* velden en we zien Hallo verschil in Hallo records die zijn geretourneerd door Hallo-query.

![Logboek query met aangepaste velden](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Volgende stappen
* Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse Hallo vermeldingen in Hallo aangepaste logboek in tooindividual velden.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.
