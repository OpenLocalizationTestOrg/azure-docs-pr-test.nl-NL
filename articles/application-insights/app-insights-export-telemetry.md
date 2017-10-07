---
title: aaaContinuous exporteren van telemetrie in Application Insights | Microsoft Docs
description: Diagnostische en gebruiksgegevens gegevens toostorage in Microsoft Azure exporteren en dit van daaruit te downloaden.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Exporteren van telemetrie in Application Insights
Wilt u tookeep uw telemetrie langer dan de standaard bewaarperiode Hallo? Of op een speciale wijze worden verwerkt? Continue Export is ideaal voor dit. u in de Application Insights-portal Hallo ziet Hallo-gebeurtenissen kunnen worden geëxporteerde toostorage in Microsoft Azure in JSON-indeling. Daar kunt u downloaden van uw gegevens en wat u code schrijven tooprocess moet het.  

Met behulp van continue Export mogelijk extra kosten in rekening gebracht. Controleer uw [prijzen model](http://azure.microsoft.com/pricing/details/application-insights/).

Voordat u de continue export instelt, zijn er enkele alternatieven kunt u tooconsider:

* Hallo Export knop Hallo boven aan een blade metrische gegevens of zoeken kunt u tabellen en grafieken tooan Excel-spreadsheet overdragen.

* [Analytics](app-insights-analytics.md) biedt een krachtige querytaal voor telemetrie. Het kan ook resultaten exporteren.
* Als u op zoek bent te[Verken uw gegevens in Power BI](app-insights-export-power-bi.md), kunt u dat doen zonder gebruik van continue Export.
* Hallo [REST-API toegang tot de gegevens](https://dev.applicationinsights.io/) kunt u programmatisch toegang krijgen tot uw telemetrie.

Nadat uw gegevens toostorage (waar het kunt blijven voor als u wilt) continue Export zijn gekopieerd, is het nog steeds beschikbaar in Application Insights voor Hallo gebruikelijke [bewaarperiode](app-insights-data-retention-privacy.md).

## <a name="setup"></a>Maken van een continue Export
1. Open continue Export in Hallo Application Insights-resource voor uw app, en kies **toevoegen**:

    ![Schuif naar beneden en klik op de continue Export](./media/app-insights-export-telemetry/01-export.png)

2. Kies Hallo telemetrie gegevenstypen gewenste tooexport.

3. Maak of Selecteer een [Azure storage-account](../storage/common/storage-introduction.md) waar u toostore Hallo gegevens.

    > [!Warning]
    > Hallo-opslaglocatie zal worden standaard toohello dezelfde geografische regio als uw Application Insights-resource. Als u in een andere regio opslaat, u mogelijk ook wijzigingskosten overdracht.

    ![Klik op toevoegen, exporteren bestemming Storage-account en maakt een nieuwe winkel of kies een bestaand archief](./media/app-insights-export-telemetry/02-add.png)

4. Maak of Selecteer een container in Hallo opslag:

    ![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/create-container.png)

Als u uw export hebt gemaakt, wordt er gestart gaan. U alleen ophalen gegevens die na het maken van Hallo export aankomt.

Er is een vertraging van ongeveer een uur voordat gegevens worden weergegeven in het Hallo-opslag.

### <a name="tooedit-continuous-export"></a>continue export tooedit

Als u wilt dat toochange Hallo gebeurtenistypen later, net Hallo export bewerken:

![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>continue export toostop

toostop hello exporteren, klikt u op uitschakelen. Als u opnieuw inschakelen op, kunnen Hallo exporteren wordt opnieuw opgestart met nieuwe gegevens. U won't Hallo gegevens dat is ontvangen in de portal Hallo terwijl export is uitgeschakeld.

toostop hello exporteren, deze permanent verwijderen. In dat geval verwijdert niet de gegevens van opslag.

### <a name="cant-add-or-change-an-export"></a>Kan niet toevoegen of wijzigen van een exporteren?
* de uitvoer tooadd of wijzigen, moet u eigenaar, bijdrager of Application Insights Inzender toegangsrechten. [Meer informatie over functies][roles].

## <a name="analyze"></a>Welke gebeurtenissen krijgt u?
Hallo is geëxporteerde gegevens Hallo onbewerkte telemetrie die we van uw toepassing ontvangen, behalve dat we locatiegegevens waarmee de berekening van Hallo client-IP-adres toevoegen.

Gegevens die zijn genegeerd door [steekproeven](app-insights-sampling.md) is niet opgenomen in Hallo geëxporteerde gegevens.

Andere berekende waarden zijn niet opgenomen. Bijvoorbeeld: gemiddelde CPU-gebruik niet worden geëxporteerd, maar we Exporteer Hallo onbewerkte telemetrie waaruit Hallo gemiddelde wordt berekend.

Hallo gegevens omvatten ook Hallo resultaten van een [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) die u hebt ingesteld.

> [!NOTE]
> **Een steekproef.** Als uw toepassing grote hoeveelheden gegevens verzendt, wordt Hallo steekproeven functie werkt en wordt alleen een fractie van Hallo gegenereerd telemetrie verzenden. [Meer informatie over steekproeven.](app-insights-sampling.md)
>
>

## <a name="get"></a>Hallo gegevens controleren
U kunt inspecteren Hallo opslag rechtstreeks in het Hallo-portal. Klik op **Bladeren**, selecteer uw storage-account en open vervolgens **Containers**.

tooinspect Azure-opslag in Visual Studio openen **weergave**, **Cloud Explorer**. (Als u deze menuopdracht niet hebt, moet u tooinstall hello Azure SDK: Open Hallo **nieuw Project** dialoogvenster Vouw Visual C# / Cloud en kies **ophalen van Microsoft Azure SDK voor .NET**.)

Wanneer u uw bloblarchief opent, ziet u een container met een set van blob-bestanden. Hallo-URI van elk bestand dat is afgeleid van de naam van uw Application Insights-resource, de instrumentatiesleutel, telemetrie-type/datum/tijd. (Hallo resourcenaam is alleen kleine letters bevatten, en de instrumentatiesleutel Hallo streepjes worden weggelaten.)

![Hallo blob-opslag met een geschikt hulpprogramma controleren](./media/app-insights-export-telemetry/04-data.png)

Hallo-datum en tijd UTC zijn en zijn wanneer Hallo telemetrie is gedeponeerd in Hallo store - niet Hallo tijd is gegenereerd. Als u code toodownload Hallo gegevens schrijft, het verplaatsen lineair Hallo-gegevens.

Hier volgt Hallo vorm van Hallo-pad:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

waar

* `blobCreationTimeUtc`tijdstip waarop blob is gemaakt in Hallo interne is staging-opslag
* `blobDeliveryTimeUtc`Hallo keer is dat wanneer blob gekopieerde toohello export-doelopslag is

## <a name="format"></a>Indeling van gegevens
* Elke blob is een tekstbestand dat meerdere bevat ' \n'-separated rijen. Het bevat Hallo telemetrie gedurende een periode van ongeveer een halve minuut is verwerkt.
* Elke rij vertegenwoordigt een gegevenspunt telemetrie zoals een aanvraag of een pagina weergave.
* Elke rij is een niet-opgemaakte JSON-document. Als u toosit wilt en op het staart, opent u het in Visual Studio en kies bewerken, Geavanceerd indelingsbestand:

![Telemetrie van paginaweergaven Hallo met een geschikt hulpprogramma](./media/app-insights-export-telemetry/06-json.png)

Tijdsduren zijn in ticks, waarbij 10 000 bedraagt ticks = 1ms. Bijvoorbeeld: deze waarden weergeven voor een periode van 1ms toosend een aanvraag van Hallo browser, 3 MS tooreceive en 1.8s tooprocess Hallo pagina in de browser Hallo:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Hallo verwerken van gegevens
Op kleine schaal, kunt u sommige code toopull elkaar uw gegevens te schrijven, lezen in een werkblad, enzovoort. Bijvoorbeeld:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

Zie voor een grotere codevoorbeeld [met behulp van een werkrol][exportasa].

## <a name="delete"></a>Uw oude gegevens verwijderen
Houd er rekening mee dat u zelf verantwoordelijk bent voor het beheren van uw opslagcapaciteit en het verwijderen van oude gegevens Hallo indien nodig.

## <a name="if-you-regenerate-your-storage-key"></a>Als u uw opslagsleutel opnieuw genereren...
Als u Hallo sleutel tooyour opslag wijzigt, wordt continue export niet meer. U ziet een melding in uw Azure-account.

Hallo continue Export blade openen en bewerken van het exporteren. Hallo exporteren bestemming bewerken, maar stelt u Hallo dezelfde opslag geselecteerd. Klik op OK tooconfirm.

![Bewerken Hallo continue exporteren, openen en sluiten thee exportbestemming.](./media/app-insights-export-telemetry/07-resetstore.png)

Hallo continue export wordt opnieuw opgestart.

## <a name="export-samples"></a>Exporteren van voorbeelden

* [Met Stream Analytics tooSQL exporteren][exportasa]
* [Stream Analytics voorbeeld 2](app-insights-export-stream-analytics.md)

Overweeg op grotere schaal [HDInsight](https://azure.microsoft.com/services/hdinsight/) -Hadoop-clusters in Hallo cloud. HDInsight biedt een reeks technologieën voor het beheren en analyseren van grote gegevens en u tooprocess gegevens die zijn geëxporteerd uit de Application Insights kan gebruiken.

## <a name="q--a"></a>Vragen en antwoorden
* *Maar alle gewenste is een eenmalige download van een grafiek.*  

    Ja, kunt u dat doen. Klik boven Hallo van Hallo-blade op **gegevens exporteren**.
* *Ik heb een export ingesteld, maar er zijn geen gegevens in de winkel.*

    Heeft Application Insights ontvangen alle telemetrie van uw app omdat u Hallo export instellen? U ontvangt alleen nieuwe gegevens.
* *Tooset up exporteren van een geprobeerd, maar is toegang geweigerd*

    Als Hallo account eigendom is van uw organisatie, hebt u toobe lid is van Hallo eigenaars of inzenders groepen.
* *Kan ik rechte toomy eigen lokale store exporteren?*

    Nee, momenteel. De engine voor het exporteren wordt momenteel alleen ondersteund met Azure storage op dit moment.  
* *Is er limiet toohello hoeveelheid gegevens die u in Mijn archief plaatsen?*

    Nee. We je houden gegevens worden gepusht totdat u Hallo export verwijdert. We stopt als wij Hallo buitenste limieten voor blob-opslag bereikt, maar dat is heel groot. Is tooyou toocontrol hoeveel opslagruimte die u gebruikt.  
* *Hoeveel blobs moet ik Zie in Hallo storage?*

  * Voor elk gegevenstype u wordt geselecteerde tooexport, een nieuwe blob elke minuut gemaakt (als de gegevens beschikbaar is).
  * Bovendien voor toepassingen met intensief verkeer moet extra partitie eenheden zijn toegewezen. Elke eenheid maakt een blob in dit geval elke minuut.
* *Ik Hallo sleutel toomy opslag opnieuw gegenereerd of Hallo-naam van de container Hallo gewijzigd en nu Hallo export niet werkt.*

    Hallo export bewerken blade en open Hallo export bestemming. Laat Hallo dezelfde opslag als voorheen geselecteerd en klik op OK tooconfirm. Exporteren wordt opnieuw opgestart. Als Hallo wijzigen binnen Hallo afgelopen paar dagen was, geen gegevens verloren gaan.
* *Kan ik Hallo export onderbreken?*

    Ja. Klik op uitschakelen.

## <a name="code-samples"></a>Codevoorbeelden

* [Stream Analytics-voorbeeld](app-insights-export-stream-analytics.md)
* [Met Stream Analytics tooSQL exporteren][exportasa]
* [Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
