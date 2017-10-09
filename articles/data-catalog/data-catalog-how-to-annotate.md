---
title: aaaHow tooannotate gegevensbronnen | Microsoft Docs
description: Hoe tooarticle markeren hoe tooannotate gegevensassets in Azure Data Catalog, met inbegrip van beschrijvende namen, tags, beschrijvingen en experts.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Hoe tooannotate gegevensbronnen
## <a name="introduction"></a>Inleiding
**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert. Data Catalog is met andere woorden, over medewerkers detecteren, begrijpen en gebruiken van gegevensbronnen helpen en helpt organisaties tooget meerwaarde van hun bestaande gegevens. Als een gegevensbron is geregistreerd met Data Catalog, de metagegevens wordt gekopieerd en geïndexeerd door Hallo-service, maar Hallo verhaal er eindigt niet. Data Catalog kan tooprovide gebruikers hun eigen beschrijvende metagegevens – zoals beschrijvingen en labels – toosupplement Hallo metagegevens die zijn geëxtraheerd uit de gegevensbron Hallo en meer te begrijpen toomore mensen toomake Hallo-gegevensbron.

## <a name="annotation-and-crowdsourcing"></a>Aantekening en crowdsourcing
Iedereen heeft advies. En dit is een goede prestaties.
Data Catalog herkent dat verschillende gebruikers verschillende perspectieven hebben voor zakelijke gegevensbronnen, en dat elk van deze perspectieven waardevol kan zijn. Houd rekening met Hallo scenario te volgen:

* Hallo-systeembeheerder kent Hallo-serviceovereenkomst voor Hallo servers of services die host Hallo-gegevensbron.
* Hallo databasebeheerder kent Hallo back-up plannen voor elke database en toegestane ETL-verwerking windows hello.
* de eigenaar systeem Hallo kent Hallo-proces voor gebruikers toorequest access toohello-gegevensbron.
* Hallo gegevens wereldburgers weet hoe Hallo activa en kenmerken in de gegevensbron Hallo toohello enterprise-gegevensmodel toegewezen.
* Hallo analist weet hoe Hallo in de context van bedrijfsprocessen Hallo die hij ondersteunt hello worden gebruikt.

Elk van deze perspectieven waardevolle is en een crowdsourcing benadering toometadata waarmee elke één toobe vastgelegd en gebruikt een volledig overzicht van geregistreerde gegevensbronnen tooprovide maakt gebruik van Data Catalog. Hallo Data Catalog-portal gebruikt, kan elke gebruiker toevoegen en bewerken van zijn of haar eigen aantekeningen terwijl kunnen tooview aantekeningen die door andere gebruikers.

## <a name="different-types-of-annotations"></a>Verschillende soorten aantekeningen
Data Catalog ondersteunt Hallo soorten aantekeningen te volgen:

| Aantekening | Opmerkingen |
| --- | --- |
| Beschrijvende naam |Beschrijvende namen kunnen worden opgegeven tijdens het Hallo-gegevensniveau asset toomake hello gegevensassets gemakkelijker te begrijpen. Beschrijvende namen zijn handig als onderliggende objectnaam Hallo toousers cryptisch, afgekorte of anderszins niet zinvol is. |
| Beschrijving |Beschrijvingen kunnen worden opgegeven tijdens het Hallo-gegevensasset en het kenmerk / kolomniveaus. Beschrijvingen zijn korte tekstaantekeningen met een beschrijving van de gebruiker Hallo perspectief op Hallo gegevensasset of het gebruik ervan. |
| Labels (gebruiker tags) |Labels kunnen worden opgegeven tijdens het Hallo-gegevensasset en het kenmerk / kolomniveaus. Gebruiker tags zijn aangepaste labels die gebruikt toocategorize gegevensassets of kenmerken worden kunnen. |
| Labels (verklarende woordenlijst tags) |Labels kunnen worden opgegeven tijdens het Hallo-gegevensasset en het kenmerk / kolomniveaus. Verklarende woordenlijst tags zijn centraal gedefinieerd termen die worden kunnen gebruikt toocategorize gegevensassets of kenmerken met een gemeenschappelijke taxonomie voor bedrijven. Zie voor meer informatie [hoe tooset van zakelijke woordenlijst Hallo voor Governed Tagging](data-catalog-how-to-business-glossary.md) |
| Experts |Deskundigen kunnen worden opgegeven tijdens het Hallo-gegevensniveau asset. Experts gebruikers of groepen met deskundige perspectieven op Hallo gegevens identificeren en kunnen fungeren als contactpunten voor gebruikers die Hallo detecteren geregistreerde gegevensbronnen vragen hebt die niet wordt beantwoord door bestaande aantekeningen Hallo. |
| Toegang aanvragen |Aanvraag voor toegang tot informatie kan worden opgegeven op Hallo gegevens asset niveau. Deze informatie is voor gebruikers die een gegevensbron dat ze nog geen machtigingen tooaccess detecteren. Gebruikers kunnen e-mailadres van Hallo gebruiker of groep die toegang verleent, URL van het proces Hallo Hallo of die gebruikers nodig toogain toegang hulpprogramma of Hallo proces zelf kunt invoeren als tekst hello invoeren. |
| Documentatie |Documentatie kan worden opgegeven op Hallo gegevens asset niveau. Documentatie voor asset is RTF-informatie die koppelingen en afbeeldingen kunnen bevatten, en die informatie niet overgebracht via beschrijvingen en labels kunt bieden. |

## <a name="annotating-multiple-assets"></a>Meerdere assets aantekeningen maken
Als u meerdere gegevensassets in Hallo Data Catalog-portal, kunnen gebruikers aantekeningen toevoegen aan alle geselecteerde elementen in één bewerking. Aantekeningen wordt geselecteerd tooall activa, zodat u eenvoudig tooselect toepassen en geef een consistente beschrijving en sets van tags en experts voor verwante gegevensassets.

> [!NOTE]
> Tags en experts kunnen ook worden opgegeven wanneer registreren gegevensassets met behulp van Hallo Data Catalog gegevens bron hulpprogramma voor registratie.
>
>

Wanneer meerdere tabellen en weergaven, alleen kolommen dat alle gegevens activa gemeen hebben geselecteerd selecteren wordt weergegeven in Hallo Data Catalog-portal. Hiermee kunnen gebruikers tooprovide labels en beschrijvingen voor alle kolommen met dezelfde naam Hallo voor alle geselecteerde activa.

## <a name="annotations-and-discovery"></a>Aantekeningen en detectie
Net zoals Hallo metagegevens die zijn geëxtraheerd uit de gegevensbron Hallo tijdens de registratie toohello Data Catalog search-index is toegevoegd, gebruiker opgegeven metagegevens worden ook geïndexeerd. Dit betekent dat niet alleen doen aantekeningen maken het gemakkelijker voor gebruikers toounderstand Hallo-gegevens die ze detecteren, aantekeningen ook maken het gemakkelijker voor gebruikers toodiscover Hallo aangetekend gegevensassets door te zoeken met behulp van Hallo-termen die zin toothem maken.

## <a name="summary"></a>Samenvatting
Registreren van een gegevensbron met Data Catalog, maakt die gegevens kunnen worden gedetecteerd door structurele en beschrijvende metagegevens uit de gegevensbron Hallo kopiëren naar Hallo Catalog-service. Na de registratie van een gegevensbron gebruikers aantekeningen toomake eenvoudiger toodiscover bieden en begrijpen binnen Hallo Data Catalog-portal.

## <a name="see-also"></a>Zie ook
* [Aan de slag met Azure Data Catalog](data-catalog-get-started.md) zelfstudie voor stapsgewijze informatie over het tooannotate-gegevensbronnen.
