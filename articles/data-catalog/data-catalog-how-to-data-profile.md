---
title: aaaHow tooData profiel gegevensbronnen
description: Hoe-tooarticle hoe tooinclude tabel - en op kolomniveau gegevens bij het registreren van gegevensbronnen in Azure Data Catalog profielen en hoe gegevens toouse toounderstand gegevensbronnen profielen is gemarkeerd.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Gegevensbronnen met gegevensprofielen
## <a name="introduction"></a>Inleiding
**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert. Met andere woorden, **Azure Data Catalog** wordt alle informatie over mensen helpen detecteren, begrijpen en gebruiken van gegevensbronnen en helpt organisaties tooget meer waarde van hun bestaande gegevens. Wanneer een gegevensbron is geregistreerd met **Azure Data Catalog**, de metagegevens wordt gekopieerd en geïndexeerd door Hallo-service, maar Hallo verhaal er eindigt niet.

Hallo **gegevens profilering** functie van **Azure Data Catalog** Hallo gegevens van ondersteunde gegevensbronnen in de catalogus worden gecontroleerd en verzamelt statistische gegevens en informatie over die gegevens. Het is gemakkelijk tooinclude een profiel van de activa van uw gegevens. Wanneer u een gegevensasset registreert, kies **gegevens profiel opnemen** in hulpprogramma voor registratie van gegevensbronnen Hallo.

## <a name="what-is-data-profiling"></a>Wat is profileren van gegevens
Profileren van gegevens onderzoekt Hallo-gegevens in het Hallo-gegevensbron wordt geregistreerd en verzamelt statistische gegevens en informatie over die gegevens. Tijdens de detectie van gegevensbron kunt deze statistische gegevens u bepalen Hallo geschiktheid van Hallo gegevens toosolve het zakelijke probleem.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Hallo ondersteunen volgende gegevensbronnen gegevens samenstellen van profiel:

* SQL Server (inclusief Azure SQL DB en Azure SQL Data Warehouse)-tabellen en weergaven
* Oracle-tabellen en weergaven
* Teradata-tabellen en weergaven
* Hive-tabellen

Inclusief gegevens profielen wanneer gebruikers voor het registreren van gegevensassets helpt beantwoorden vragen over gegevensbronnen, waaronder:

* Deze kunnen worden gebruikt toosolve mijn zakelijke probleem?
* Voldoet Hallo gegevens tooparticular standaarden of patronen?
* Wat zijn enkele Hallo afwijkingen van de gegevensbron Hallo?
* Wat zijn mogelijk uitdagingen bij het integreren van deze gegevens in mijn toepassing?

> [!NOTE]
> U kunt ook de documentatie bij tooan asset toodescribe hoe gegevens kan worden geïntegreerd in een toepassing toevoegen. Zie [hoe gegevensbronnen toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Hoe tooinclude data profiel bij het registreren van een gegevensbron
Het is gemakkelijk tooinclude een profiel van de gegevensbron. Wanneer u een gegevensbron registreren in Hallo **objecten toobe geregistreerd** Configuratiescherm van de registratie van gegevensbron Hallo hulpprogramma, kiest u **gegevens profiel opnemen**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

toolearn informatie over hoe tooregister gegevensbronnen, Zie [hoe gegevensbronnen tooregister](data-catalog-how-to-register.md) en [aan de slag met Azure Data Catalog](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filteren op gegevensassets die gegevens profielen bevatten
gegevensassets toodiscover die een profiel van de gegevens bevatten, die u kunt opnemen `has:tableDataProfiles` of `has:columnsDataProfiles` als een van de zoektermen.

> [!NOTE]
> Selecteren **gegevens profiel opnemen** in Hallo gegevens bevat hulpprogramma voor registratie tabel en profielgegevens op kolomniveau. Hallo kunnen API van Data Catalog echter gegevens activa toobe geregistreerd met slechts één set met profielgegevens opgenomen.
>
>

## <a name="viewing-data-profile-information"></a>Data-profielgegevens weergeven
Als u een geschikte gegevensbron aan een profiel hebt gevonden, kunt u gegevens uit het profiel Hallo gegevens kunt weergeven. tooview hello gegevens profiel, selecteert u een gegevensasset en kiest u **gegevens profiel** Hallo Data Catalog-portal-venster.

![](media/data-catalog-data-profile/data-catalog-view.png)

Een profiel van de gegevens in **Azure Data Catalog** toont tabel en de kolom profiel informatie zoals:

### <a name="object-data-profile"></a>Object gegevens profiel
* Aantal rijen
* De tabelgrootte van de
* Wanneer Hallo-object voor het laatst is bijgewerkt

### <a name="column-data-profile"></a>Kolom gegevens profiel
* Gegevenstype van kolom
* Aantal afzonderlijke waarden
* Aantal rijen met NULL-waarden
* Minimum, maximum, gemiddelde en standaarddeviatie voor kolomwaarden

## <a name="summary"></a>Samenvatting
Profileren van gegevens voorziet in statistieken en informatie over gegevens activa toohelp u Hallo geschiktheid van Hallo gegevens toosolve zakelijke problemen vaststellen geregistreerd. Samen met aantekeningen maken en gegevensbronnen documenteren, kunnen profielen van de gegevens gebruikers geven een beter begrip van uw gegevens.

## <a name="see-also"></a>Zie ook
* [Hoe tooregister gegevensbronnen](data-catalog-how-to-register.md)
* [Aan de slag met Azure Data Catalog](data-catalog-get-started.md)
