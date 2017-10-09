---
title: aaaHow toodiscover gegevensbronnen in Azure Data Catalog | Microsoft Docs
description: In dit artikel illustreert hoe toodiscover geregistreerde gegevensassets met Azure Data Catalog, met inbegrip van zoeken en filteren en markeren mogelijkheden van hello Azure Data Catalog-portal met behulp van Hallo bereikt.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Hoe toodiscover gegevensbronnen in Azure Data Catalog
## <a name="introduction"></a>Inleiding
Azure Data Catalog is een volledig beheerde cloudservice die als een systeem van registratie en detectie van zakelijke gegevensbronnen fungeert. Met andere woorden, Data Catalog helpt mensen detecteren, begrijpen en gebruiken van gegevensbronnen en het helpt organisaties Haal meer uit hun bestaande gegevens. Nadat een gegevensbron is geregistreerd met Data Catalog, worden de metagegevens wordt geïndexeerd door Hallo-service, zodat u eenvoudig toodiscover Hallo gegevens die u nodig kunt zoeken.

## <a name="searching-and-filtering"></a>Zoeken en filteren
Detectie in Data Catalog gebruikt twee primaire mechanismen: zoeken en filteren.

Het zoeken is ontworpen toobe intuïtieve en krachtige. Standaard worden zoektermen vergeleken met een eigenschap in het Hallo catalog, met inbegrip van de gebruiker opgegeven aantekeningen.

Voor het filteren is ontworpen toocomplement zoeken. U kunt specifieke kenmerken zoals deskundigen, gegevensbrontype, objecttype en labels selecteren. U kunt alleen overeenkomende gegevensassets weergeven en zoeken resultaten toomatching activa beperken.

Met behulp van een combinatie van zoeken en filteren kunt u snel Hallo gegevensbronnen die zijn geregistreerd met Data Catalog toodiscover Hallo gegevensbronnen u moet navigeren.

## <a name="search-syntax"></a>Zoeksyntaxis
Hoewel zoeken met vrije tekst hello standaard eenvoudige en intuïtieve is, kunt u ook zoeksyntaxis van Data Catalog gebruiken voor meer controle over de zoekresultaten Hallo. Data Catalog zoeken ondersteunt Hallo technieken te volgen:

| Techniek | Gebruiken | Voorbeeld |
| --- | --- | --- |
| Basic zoeken |Basic zoeken die gebruikmaakt van een of meer zoektermen. De resultaten zijn elementen die overeenkomen met een eigenschap met een of meer Hallo voorwaarden opgegeven. |`sales data` |
| Bereik van eigenschap definiëren |Retour alleen gegevensbronnen waarbij de zoekterm Hallo komt met de Hallo overeen opgegeven eigenschap. |`name:finance` |
| Booleaanse operators |Verbreed of Verfijn een zoekopdracht met Booleaanse bewerkingen. |`finance NOT corporate` |
| Groeperen met haakjes |Gebruik haakjes toogroup delen van Hallo query tooachieve logische isolatie, met name in combinatie met Booleaanse operators. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Vergelijkingsoperators |Gebruik andere vergelijkingen dan gelijkheid voor eigenschappen die de gegevenstypen Numeriek en datum hebben. |`modifiedTime > "11/05/2014"` |

Zie voor meer informatie over Data Catalog search Hallo [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) artikel.

## <a name="hit-highlighting"></a>Markeren
Wanneer u zoekresultaten wilt weergeven, alle eigenschappen die overeenkomen met opgegeven Hallo weergegeven zoektermen (zoals Hallo gegevens assetnaam, beschrijving en labels) zijn gemarkeerde toomake deze eenvoudiger tooidentify waarom een bepaalde gegevensasset is geretourneerd door een bepaalde zoekactie.

> [!NOTE]
> tooturn uitschakelen hit markeren, gebruik Hallo **Markeer** in Hallo Data Catalog-portal-switch.
>
>

Wanneer u de zoekresultaten weergeeft, niet altijd worden duidelijk waarom een gegevensasset opgenomen, is zelfs met treffers markering is ingeschakeld. Omdat alle eigenschappen standaard worden doorzocht, een gegevensasset mogelijk geretourneerde vanwege een overeenkomst voor een eigenschap op kolomniveau. En omdat meerdere gebruikers kunnen aantekeningen toevoegen aan geregistreerde gegevensassets met hun eigen labels en beschrijvingen, niet alle metagegevens in de lijst met zoekresultaten Hallo kan worden weergegeven.

In de weergave van het Hallo standaard tile elke tegel weergegeven in zoekresultaten Hallo bevat een **weergave zoekterm overeenkomt met** pictogram, zodat u snel Hallo aantal overeenkomsten en de locatie en toojump toothem bekijken kunt als u wilt.

 ![Markeren en zoeken komt overeen met in hello Azure Data Catalog-portal](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Samenvatting
Omdat u een gegevensbron met Data Catalog kopieert structurele en beschrijvende metagegevens uit Hallo gegevens gegevensbron toohello catalogusservice, hello gegevensbron wordt gemakkelijker toodiscover en begrijpen. Nadat u een gegevensbron hebt geregistreerd, kunt u ontdekken met behulp van het filteren en zoeken van in Hallo Data Catalog-portal.

## <a name="next-steps"></a>Volgende stappen
* Voor stapsgewijze informatie over het toodiscover gegevensbronnen, Zie [aan de slag met Azure Data Catalog](data-catalog-get-started.md).
