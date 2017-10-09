---
title: aaaAzure zoeken multi taal | Microsoft Docs
description: Azure Search biedt ondersteuning voor 56 talen gebruik taalanalyse van Lucene en het verwerken van natuurlijke taal-technologie van Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Een index voor documenten in meerdere talen in Azure Search maken
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing hello kracht van taalanalyse is net zo eenvoudig als een eigenschap van de instelling voor een doorzoekbaar veld in de indexdefinitie Hallo. Nu kunt u deze stap bij het Hallo-portal doen.

Hieronder vindt u schermopnamen van hello Azure Portal-blades voor Azure Search waarmee gebruikers toodefine een indexschema. Gebruikers kunnen via deze blade alle Hallo velden maken en Hallo analyzer eigenschap instellen voor elk van deze.

> [!IMPORTANT]
> U kunt alleen een taalanalyse instellen tijdens de definitie van veld, zoals in wanneer maken van een nieuwe index van Hallo gemalen, of bij het toevoegen van een nieuw veld tooan bestaande index. Zorg ervoor dat u alle kenmerken, zoals Hallo analyzer, tijdens het maken van Hallo veld volledig opgeven. U niet kunt tooedit zijn Hallo-kenmerken en niet Hallo analyzer type niet wijzigen wanneer u uw wijzigingen hebt opgeslagen.
>
>

## <a name="define-a-new-field-definition"></a>De velddefinitie van een nieuw definiëren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) en open Hallo service blade van uw zoekservice.
2. Klik op **toevoegen index** balk Hallo Hallo service dashboard toostart bovenaan in een nieuwe index of open een bestaande index tooset een analyzer op nieuwe velden die u wilt toevoegen in Hallo opdracht tooan bestaande index.
3. Hallo velden blade wordt weergegeven, zodat u de opties voor het definiëren van Hallo-schema van Hallo index, waaronder Hallo Analyzer tabblad gebruikt voor het kiezen van een taalanalyse.
4. In velden, start u de velddefinitie van een door een naam geven, Hallo gegevenstype te kiezen en instellen van kenmerken toomark Hallo veld als de volledige tekst doorzoekbaar, worden opgehaald in de zoekresultaten, kan worden gebruikt in de navigatiestructuur facet, sorteerbaar, enzovoort.
5. Voordat u doorgaat toohello volgende veld, open Hallo **Analyzer** tabblad.

![][1]
*tooselect een analyzer, klik op Hallo Analyzer tabblad op Hallo velden blade*

## <a name="choose-an-analyzer"></a>Kies een analyzer
1. Schuif toofind Hallo veld definiëren.
2. Als u dit nog niet hebt gemarkeerd Hallo veld als doorzoekbaar, klikt u op Hallo selectievakje nu toomark als **doorzoekbaar**.
3. Klik op Hallo Analyzer gebied toodisplay Hallo lijst met beschikbare analyzers.
4. Kies Hallo analyzer gewenste toouse.

![][2]
*Selecteer een van de analyzers Hallo ondersteund voor elk veld*

Standaard gebruiken alle doorzoekbare velden Hallo [standaard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) welke taal networkdirect is. tooview hello volledige lijst met ondersteunde analyzers, Zie [taalondersteuning in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Nadat Hallo taalanalyse voor een veld is geselecteerd, wordt deze met elke aanvraag indexeren en de zoekcriteria voor dat veld gebruikt. Wanneer een query op basis van meerdere velden met behulp van verschillende analyzers is uitgegeven, zullen Hallo query onafhankelijk worden verwerkt door de juiste analyzers Hallo voor elk veld.

Veel webtoepassingen en mobiele toepassingen fungeren gebruikers hele Hallo wereld met behulp van verschillende talen. Het is mogelijk toodefine een index voor een scenario zoals deze door het maken van een veld voor elke taal die wordt ondersteund.

![][3]
*Definitie van de index met een beschrijvingsveld voor elke taal ondersteund*

Als de taal Hallo van Hallo agent een query uitvoert bekend is, een zoekaanvraag bereik tooa bepaald veld met de Hallo kan worden **searchFields** queryparameter. Hallo worden volgende query uitgegeven alleen tegen Hallo beschrijving in pools:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

U kunt uw index vanuit de portal Hallo query met **Search explorer** toopaste in een query vergelijkbare toohello melding hierboven. Search explorer is beschikbaar in de opdrachtbalk Hallo Hallo service blade. Zie [query uitvoeren op uw Azure Search-index in de portal Hallo](search-explorer.md) voor meer informatie.

Soms hello taal van het Hallo-agent een query uitvoert niet bekend is, in welk geval Hallo query kan worden uitgegeven op basis van alle velden tegelijkertijd. Indien nodig, de voorkeur voor de resultaten in een bepaalde taal kan worden gedefinieerd met behulp van [score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx). In onderstaande Hallo voorbeeld, overeenkomsten gevonden in het vak Beschrijving in het Engels Hallo hogere relatieve toomatches in Pools en Frans score:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Als u een .NET-ontwikkelaar bent, houd er rekening mee dat u met behulp van Hallo taalanalyse kunt configureren [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search). de meest recente release Hallo biedt ondersteuning voor Hallo Microsoft taalanalyse ook.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
