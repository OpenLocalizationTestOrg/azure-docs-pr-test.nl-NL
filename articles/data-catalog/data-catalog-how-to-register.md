---
title: de gegevensbronnen aaaRegister in Azure Data Catalog | Microsoft Docs
description: In dit artikel ziet u hoe tooregister gegevensbronnen in Azure Data Catalog, met inbegrip van Hallo metagegevensvelden tijdens de registratie hebt uitgepakt.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Gegevensbronnen registreren in Azure Data Catalog
## <a name="introduction"></a>Inleiding
Azure Data Catalog is een volledig beheerde cloudservice die als een systeem van registratie en detectie van zakelijke gegevensbronnen fungeert. Met andere woorden, Data Catalog helpt mensen detecteren, begrijpen en gebruiken van gegevensbronnen en het helpt organisaties Haal meer uit hun bestaande gegevens. eerste stap toomaking een gegevensbron Hallo kan worden gedetecteerd via Data Catalog is tooregister die gegevensbron.

## <a name="register-data-sources"></a>Gegevensbronnen registreren
Registratie is Hallo proces van het extraheren van metagegevens van de gegevensbron Hallo en die gegevens toohello Data Catalog-service te kopiëren. Hallo gegevens blijven waar deze zich momenteel bevindt, en blijft onder Hallo-besturingselement van het Hallo-beheerders en het beleid van het huidige systeem Hallo.

een gegevensbron tooregister Hallo te volgen:
1. Start Hallo Data Catalog hulpprogramma voor registratie in hello Azure Data Catalog-portal. 
2. Aanmelden met uw werk- of schoolaccount Hello dezelfde Azure Active Directory-referenties in portal toohello toosign te gebruiken.
3. Selecteer de gewenste tooregister Hallo-gegevensbron.

Zie voor meer informatie stapsgewijze Hallo [aan de slag met Azure Data Catalog](data-catalog-get-started.md) zelfstudie.

Nadat u de gegevensbron Hallo hebt geregistreerd, wordt Hallo catalogus houdt de locatie en de metagegevens van de indexen. Gebruikers kunnen zoeken, bladert, Hallo gegevensbron detecteren en gebruik vervolgens de locatie tooconnect tooit met behulp van de toepassing hello of hulpprogramma van hun keuze.

## <a name="supported-data-sources"></a>Ondersteunde gegevensbronnen
Zie voor een lijst met ondersteunde gegevensbronnen, [Data Catalog DSR](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Structurele metagegevens
Wanneer u een gegevensbron registreert, haalt Hallo-hulpprogramma voor registratie informatie over de structuur Hallo Hallo-objecten die u selecteert. Deze informatie is bedoeld tooas structurele metagegevens.

Voor alle objecten omvat deze structurele metagegevens van het object Hallo locatie, zodat gebruikers die gegevens Hallo detecteren dat informatie tooconnect toohello object in Hallo clienthulpprogramma's van hun keuze gebruiken kunnen. Andere structurele metagegevens bevat objectnaam en -type en typ kenmerk-/ kolomnaam en gegevens.

## <a name="descriptive-metadata"></a>Beschrijvende metagegevens
Bovendien toohello structurele metagegevens die zijn geëxtraheerd uit de gegevensbron Hallo core, hulpprogramma voor registratie van gegevensbronnen Hallo extraheert beschrijvende metagegevens. Voor SQL Server Analysis Services en SQL Server Reporting Services, wordt deze metagegevens worden overgenomen uit Hallo beschrijving eigenschappen van deze services. Voor SQL Server, die zijn opgegeven met behulp van ms Hallo\_beschrijving uitgebreide eigenschap wordt opgehaald. Hallo-gegevensbron registratie hulpprogramma uitgepakt Hallo kolom opmerkingen van Hallo voor Oracle-Database, alle\_tabblad\_opmerkingen weergeven.

In de toevoeging toohello beschrijvende metagegevens die wordt opgehaald uit de gegevensbron hello, kunnen gebruikers met behulp van hulpprogramma voor registratie van gegevensbronnen Hallo beschrijvende metagegevens invoeren. Gebruikers kunnen tags toevoegen en ze kunnen identificeren experts voor Hallo-objecten wordt geregistreerd. Alle deze beschrijvende metagegevens is toohello Data Catalog-service samen met de structurele metagegevens Hallo gekopieerd.

## <a name="include-previews"></a>Voorbeelden zijn
Standaard wordt alleen metagegevens opgehaald uit de gegevensbronnen en gekopieerde toohello Data Catalog-service, maar wat die een gegevensbron is vaak het eenvoudiger wanneer vindt u een voorbeeld van Hallo gegevens bevat.

Met behulp van hulpprogramma voor registratie van Data Catalog gegevensbronnen hello, kunt u een voorbeeld van de momentopname van Hallo gegevens opnemen in elke tabel en de weergave die is geregistreerd. Als u tooinclude previews tijdens de registratie kiest, bevat hulpprogramma voor registratie Hallo too20 records uit elke tabel en de weergave. Deze momentopname wordt vervolgens gekopieerd toohello catalogus samen met de Hallo structurele en beschrijvende metagegevens.

> [!NOTE]
> Wide tabellen met een groot aantal kolommen hebben mogelijk minder dan 20 records die zijn opgenomen in de preview.
>
>

## <a name="include-data-profiles"></a>Profielen van de gegevens bevatten
Net zoals inclusief voorbeelden waardevolle context voor gebruikers die voor gegevensbronnen in Data Catalog bieden kunnen zoeken, kunt met inbegrip van een profiel van de gegevens u gemakkelijker toounderstand gedetecteerd-gegevensbronnen.

U kunt een profiel van de gegevens voor elke tabel en de weergave die is geregistreerd opnemen met behulp van hulpprogramma voor registratie Hallo Data Catalog-gegevensbron. Als u een profiel gegevens tooinclude tijdens de registratie kiest, Hallo-hulpprogramma voor registratie samengevoegde statistieken over Hallo gegevens bevat in elke tabel en de weergave, met inbegrip van:

* Hallo aantal rijen en de grootte van Hallo-gegevens in het Hallo-object.
* Hallo datum voor de meest recente update Hallo van Hallo gegevens en het Hallo-object schema.
* Hallo aantal null records en verschillende waarden voor kolommen.
* Hallo waarden minimum, maximum, gemiddelde en standaarddeviatie voor kolommen.

Deze statistische gegevens worden vervolgens gekopieerd toohello catalogus samen met de Hallo structurele en beschrijvende metagegevens.

> [!NOTE]
> Tekst- en datum kolommen opnemen gemiddelde of standaarddeviatie statistieken niet in hun profiel gegevens.
>
>

## <a name="update-registrations"></a>Registraties bijwerken
Registreren van een gegevensbron maakt het gevonden in de catalogus met gegevens wanneer u Hallo metagegevens en optionele preview tijdens de registratie hebt uitgepakt. Als de gegevensbron Hallo moet toobe bijgewerkt in de catalogus hello (bijvoorbeeld als Hallo-schema van een object is gewijzigd, tabellen oorspronkelijk uitgesloten opgenomen worden moeten of gewenste tooupdate Hallo gegevens die zijn opgenomen in Hallo voorbeelden), hulpprogramma voor registratie van gegevensbronnen Hallo u kunt opnieuw uitvoeren.

Opnieuw registreren van een reeds geregistreerde gegevensbron voert een "upsert" samenvoegbewerking: bestaande objecten worden bijgewerkt en nieuwe objecten zijn gemaakt. Alle metagegevens die door gebruikers via Hallo Data Catalog-portal worden bewaard.

## <a name="summary"></a>Samenvatting
Omdat het structurele en beschrijvende metagegevens uit een gegevensservice bron toohello catalogus wordt gekopieerd, Hallo-gegevensbron registreert in Data Catalog Hallo gegevens eenvoudiger toodiscover maakt en begrijpen. Nadat u de gegevensbron Hallo hebt geregistreerd, kunt u aantekeningen toevoegen aan, beheren en te ontdekken met behulp van Hallo Data Catalog-portal.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het registreren van gegevensbronnen Hallo [aan de slag met Azure Data Catalog](data-catalog-get-started.md) zelfstudie.
