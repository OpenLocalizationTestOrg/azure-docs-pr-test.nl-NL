---
title: aaaAzure terminologie Data Catalog | Microsoft Docs
description: In dit artikel biedt een inleiding tooconcepts en termen die worden gebruikt in de documentatie van Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminologie voor Azure Data Catalog
## <a name="catalog"></a>Catalogus
Hello Azure Data Catalog is een cloud-gebaseerde metagegevens-opslagplaats in welke gegevens activa gegevensbronnen en gegevens kunnen worden geregistreerd. Hallo catalog fungeert als een centrale opslaglocatie voor de structurele metagegevens die zijn geëxtraheerd uit gegevensbronnen en beschrijvende metagegevens die zijn toegevoegd door gebruikers.

## <a name="data-source"></a>Gegevensbron
Een gegevensbron is een systeem of de container die gegevensassets beheert. Voorbeelden zijn SQL Server-databases, Oracle-databases, SQL Server Analysis Services-databases (in tabelvorm of multidimensionale) en SQL Server Reporting Services-servers.

## <a name="data-asset"></a>Gegevensasset
Gegevensassets zijn opgenomen in de gegevensbronnen die kunnen worden geregistreerd met de catalogus Hallo-objecten. Voorbeelden zijn SQL Server-tabellen en weergaven, Oracle-tabellen en weergaven, SQL Server Analysis Services metingen, dimensies en KPI's en rapporten van SQL Server Reporting Services.

## <a name="data-asset-location"></a>Locatie van de asset
Hallo catalogus wordt opgeslagen Hallo-locatie van een gegevensbron of een gegevensasset, wat kan gebruikte tooconnect toohello gegevensbron via een clienttoepassing. Hallo-indeling en de details van Hallo locatie variëren, afhankelijk van Hallo gegevensbrontype. Een tabel met SQL Server kan bijvoorbeeld worden geïdentificeerd door de vierdelige naam – servernaam, databasenaam, de naam van schema, objectnaam – terwijl een SQL Server Reporting Services-rapport kan worden geïdentificeerd door de URL.

## <a name="structural-metadata"></a>Structurele metagegevens
Structurele metagegevens is opgehaald uit een gegevensbron die Hallo-structuur van een gegevensasset beschrijft Hallo-metagegevens. Dit omvat Hallo activa locatie, de objectnaam en type en aanvullende typespecifieke kenmerken. Hallo structurele metagegevens voor tabellen en weergaven bevat bijvoorbeeld Hallo namen en gegevenstypen voor kolommen van het Hallo-object.

## <a name="descriptive-metadata"></a>Beschrijvende metagegevens
Beschrijvende metagegevens zijn metagegevens die Hallo doel of de bedoeling van een gegevensasset beschrijft. Doorgaans beschrijvende metagegevens wordt toegevoegd door gebruikers van de catalogus met hello Azure Data Catalog-portal, maar deze kan ook worden geëxtraheerd uit de gegevensbron Hallo tijdens de registratie. Bijvoorbeeld, hulpprogramma voor registratie van hello Azure Data Catalog wordt opgehaald door de beschrijvingen van Hallo eigenschap Description in SQL Server Analysis Services en SQL Server Reporting Services en van Hallo [ms_description uitgebreide eigenschap](https://technet.microsoft.com/library/ms190243.aspx)in SQL Server-databases, als deze eigenschappen zijn ingevuld met waarden.

## <a name="request-access"></a>Toegang aanvragen
Een gegevensasset beschrijvende metagegevens kan bevatten informatie over hoe toorequest toegang krijgen tot toohello gegevens asset of de gegevensbron. Deze informatie krijgt Hallo asset gegevenslocatie en kan bevatten een of meer van de Hallo volgende opties:

* Hallo e-mailadres van Hallo gebruiker of het team dat verantwoordelijk is voor het verlenen van toegang toohello-gegevensbron.
* Hallo-URL van Hallo gedocumenteerd proces dat gebruikers toogain access toohello gegevensbron moeten volgen.
* Hallo-URL van een identiteit en toegang management tool (zoals Microsoft Identity Manager) die gebruikt toogain access toohello-gegevensbron worden kan.
* Een item met vrije tekst waarin wordt beschreven hoe gebruikers toegang toohello-gegevensbron kunnen krijgen.

## <a name="preview"></a>Preview
Een voorbeeld van in Azure Data Catalog is een momentopname van too20 records die kunnen worden opgehaald uit de gegevensbron Hallo tijdens de registratie en opgeslagen in de catalogus Hallo met Hallo gegevens asset metagegevens. Hallo preview kan helpen bij gebruikers die een gegevensasset detecteren beter begrip van de functie en het doel. Met andere woorden, ziet voorbeeldgegevens mag meer waard dan zien alleen Hallo kolomnamen en gegevenstypen.
Voorbeelden worden alleen ondersteund voor tabellen en weergaven en moeten worden expliciet is geselecteerd door de gebruiker Hallo tijdens de registratie.

## <a name="data-profile"></a>Data-profiel
Een profiel van de gegevens in Azure Data Catalog is een momentopname van de tabel op gebruikersniveau en op kolomniveau metagegevens over een geregistreerde gegevensasset die kan worden opgehaald uit de gegevensbron Hallo tijdens de registratie en opgeslagen in de catalogus Hallo met Hallo gegevens asset metagegevens. Hallo gegevens profiel kunt gebruikers die een gegevensasset detecteren beter begrip van de functie en het doel. Vergelijkbare toopreviews, gegevens profielen moet expliciet worden geselecteerd door de gebruiker Hallo tijdens de registratie.

> [!NOTE]
> Uitpakken van een profiel van de gegevens kan een kostbare bewerking voor grote tabellen en weergaven, en kan aanzienlijk verhogen Hallo tooregister tijd die nodig is een gegevensbron.
>
>

## <a name="user-perspective"></a>Gebruikersperspectief
In Azure Data Catalog, kan elke gebruiker beschrijvende metagegevens leveren voor een geregistreerde gegevensasset. Elke gebruiker heeft een afzonderlijke perspectief op Hallo gegevens en het gebruik ervan. Hallo beheerder die verantwoordelijk is voor een server voorschrijven bijvoorbeeld Hallo details van de serviceovereenkomst (SLA) of de back-upvensters; een wereldburgers gegevens kan bepalen dat koppelingen toodocumentation voor bedrijven Hallo verwerkt Hallo gegevens ondersteunt; en een analist kan Geef een beschrijving in Hallo voorwaarden die de meest relevante tooother analisten zijn en wat het nuttigst toothose gebruikers die moeten toodiscover en Hallo gegevens begrijpen kan zijn.

Elk van deze perspectieven zijn inherent waardevol en met Azure Data Catalog elke gebruiker Hallo-informatie die relevant toothem is terwijl alle gebruikers kunnen gebruiken die informatie toounderstand Hallo gegevens en het doel kan bevatten.

## <a name="expert"></a>deskundige
Een expert is een gebruiker die is geïdentificeerd als een gefundeerde 'deskundige' perspectief voor een gegevensasset hebben. Elke gebruiker kan zichzelf of een andere gebruiker toevoegen als een expert voor een asset. Wordt vermeld als een expert extra bevoegdheden in Azure Data Catalog; niet overbrengen gebruikers tooeasily die perspectieven die waarschijnlijk toobe nuttig zijn bij het controleren van een asset beschrijvende metagegevens vinden.

## <a name="owner"></a>Eigenaar
Een eigenaar is een gebruiker met aanvullende bevoegdheden voor het beheren van een gegevensasset in Azure Data Catalog. Gebruikers kunnen eigenaar worden van geregistreerde gegevensassets en eigenaren van andere gebruikers kunnen toevoegen als mede-eigenaren. Zie voor meer informatie [hoe toomanage gegevensassets](data-catalog-how-to-manage.md)  

> [!NOTE]
> Eigendom en het beheer zijn alleen beschikbaar in Standard-editie van Azure Data Catalog Hallo.
>
>

## <a name="registration"></a>Registratie
Registratie is Hallo handeling gegevens asset metagegevens extraheren uit een gegevensbron en kopiëren toohello Azure Data Catalog-service. Gegevensassets die zijn geregistreerd, kunnen vervolgens aangetekend en gedetecteerd.

## <a name="see-also"></a>Zie ook
* [Wat is Azure Data Catalog?](data-catalog-what-is-data-catalog.md) -Dit artikel bevat een overzicht van hello Azure Data Catalog-service, Hallo meerwaarde en Hallo scenario's ondersteund.
* [Aan de slag met Azure Data Catalog](data-catalog-get-started.md) -in dit artikel biedt een end-to-end zelfstudie waarin wordt getoond hoe toouse Azure Data Catalog voor detectie van gegevensbronnen.  
