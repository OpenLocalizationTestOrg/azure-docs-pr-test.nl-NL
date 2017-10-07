---
title: aaaSet up Hallo zakelijke woordenlijst voor geregeld tags in Azure Data Catalog | Microsoft Docs
description: "Hoe tooarticle markeren Hallo zakelijke woordenlijst in Azure Data Catalog voor het definiëren en met behulp van een algemene zakelijke woordenlijst tootag geregistreerde gegevensassets."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Hallo zakelijke woordenlijst instellen voor een bepaald tagging
## <a name="introduction"></a>Inleiding
Azure Data Catalog kunnen gegevensbron detectie, zodat u eenvoudig kunt detecteren en Hallo gegevensbronnen begrijpen die u tooperform analyse nodig hebt en beslissingen te nemen. Deze mogelijkheden maken de grootste impact Hallo wanneer u deze kunt vinden en Hallo breedste scala aan beschikbare gegevensbronnen begrijpen.

Een functie van Data Catalog die bijdraagt aan beter inzicht in gegevens van de activa is labels. U kunt met behulp van de labels trefwoorden koppelen aan een asset of een kolom, die op zijn beurt het eenvoudiger toodiscover Hallo asset maakt via zoeken of bladeren. Labels kunt u gemakkelijk begrijpen Hallo context en doel van Hallo asset.

Echter kan tagging soms problemen veroorzaken voor zichzelf. Enkele voorbeelden van labels kan leiden tot problemen zijn:

* Hallo gebruik van afkortingen op bepaalde activa- en uitgebreide tekst op andere. Deze inconsistentie belemmert Hallo detectie van activa, hoewel Hallo bedoeling tootag Hallo activa met Hallo is dezelfde tag.
* Mogelijke verschillen in de zin, afhankelijk van de context. Bijvoorbeeld een label aangeroepen *omzet* op een klant gegevensset omzet door de klant kan betekenen, maar hello dezelfde tag van een kwartaal verkoop gegevensset mogelijk zeggen dat elk kwartaal omzet voor Hallo bedrijf.  

toohelp adres deze en andere vergelijkbare uitdagingen, Data Catalog bevat een zakelijke woordenlijst.

Een organisatie kunt met behulp van Hallo Data Catalog zakelijke woordenlijst documenteren belangrijke zakelijke voorwaarden en hun definities toocreate een algemene zakelijke woordenlijst. Deze governance kunt consistentie in het gebruik van gegevens binnen de organisatie Hallo. Nadat u een term in Hallo zakelijke woordenlijst is gedefinieerd, kan worden deze tooa gegevensasset in de catalogus Hallo toegewezen. Deze aanpak *geregeld tagging*, is dezelfde manier als tagging Hallo.

## <a name="glossary-availability-and-privileges"></a>Verklarende woordenlijst beschikbaarheid en bevoegdheden
Hallo zakelijke woordenlijst is alleen beschikbaar in Standard-editie van Azure Data Catalog Hallo. Hallo gratis editie van Data Catalog bevat geen een verklarende woordenlijst en biedt geen mogelijkheden voor geregeld labelen.

U hebt toegang tot zakelijke woordenlijst Hallo via Hallo **verklarende woordenlijst** optie in het navigatiemenu Hallo Data Catalog portal.  

![Toegang tot Hallo zakelijke woordenlijst](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Data Catalog beheerders en leden van Hallo verklarende woordenlijst rol beheerders maken kunt, bewerken en verwijderen van termen in de in Hallo zakelijke woordenlijst. Alle gebruikers van Data Catalog kunnen Hallo term definities en activa met termen in de tag bekijken.

![Toevoegen van een nieuwe term voor de verklarende woordenlijst](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Verklarende woordenlijst voorwaarden maken
Data Catalog beheerders en beheerders van de verklarende woordenlijst termen in de maken door te klikken op Hallo **nieuwe Term** knop. Elke term verklarende woordenlijst bevat Hallo volgende velden:

* De definitie van een zakelijke Hallo term
* Een beschrijving op die worden vastgelegd Hallo bedoeld gebruik of business-regels voor Hallo asset of kolom
* Een lijst met belanghebbenden die Hallo meest over Hallo term kennen
* Hallo bovenliggende term, waarmee wordt gedefinieerd in welke Hallo term is georganiseerd Hallo-hiërarchie

## <a name="glossary-term-hierarchies"></a>Verklarende woordenlijst term hiërarchieën
Met behulp van Hallo Data Catalog zakelijke woordenlijst een organisatie kan de zakelijke woordenlijst beschrijven als een hiërarchie van termen en deze een classificatie van termen die beter de zakelijke taxonomie vertegenwoordigt kunt maken.

Een term moet op een bepaald niveau van de hiërarchie uniek zijn. Dubbele namen zijn niet toegestaan. Er is geen limiet toohello het aantal niveaus in een hiërarchie, maar een hiërarchie is vaak gemakkelijker te begrijpen wanneer er drie niveaus of minder zijn.

Hallo-gebruik van hiërarchieën in Hallo zakelijke woordenlijst is optioneel. Verlaten Hallo bovenliggende term veld leeg laten voor termen in de maakt een platte (niet-hiërarchische) lijst met termen in Hallo verklarende woordenlijst.  

## <a name="tagging-assets-with-glossary-terms"></a>Labels van activa met termen in de
Nadat termen zijn gedefinieerd in de catalogus hello, is het Hallo-ervaring van activa-labels geoptimaliseerde toosearch Hallo verklarende woordenlijst als een gebruiker typt een label. Hallo Data Catalog-portal geeft een lijst met overeenkomende verklarende woordenlijst voorwaarden toochoose uit. Als Hallo gebruiker term in een woordenlijst in de lijst hello selecteert, Hallo term toohello asset toegevoegd als een tag (ook wel een tag verklarende woordenlijst). Hallo gebruiker kunt ook toocreate een nieuwe code door een term die zich niet in Hallo verklarende woordenlijst (ook wel een label voor de gebruiker).

![Gegevensasset gemarkeerd met één gebruikerstag en labels voor twee verklarende woordenlijst](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Gebruiker tags zijn Hallo alleen type label wordt ondersteund in Hallo gratis editie van Data Catalog.
>
>

### <a name="hover-behavior-on-tags"></a>Beweeg de muisaanwijzer gedrag tags
In Hallo Data Catalog-portal zijn twee soorten labels Hallo visueel uniek en aanwezig verschillende aanwijzen gedrag. Wanneer u de muisaanwijzer op het label van een gebruiker, kunt u zien Hallo labeltekst en Hallo gebruiker of gebruikers die Hallo tag hebt toegevoegd. Als u de muisaanwijzer op een label verklarende woordenlijst, ziet u ook Hallo definitie van Hallo verklarende woordenlijst term en een koppeling tooopen Hallo business verklarende woordenlijst tooview Hallo volledige definitie van Hallo term.

### <a name="search-filters-for-tags"></a>Zoekfilters voor tags
Verklarende woordenlijst tags en gebruiker tags zijn beide doorzoekbare en u ze als filters in een zoekopdracht kunt toepassen.

## <a name="summary"></a>Samenvatting
Met behulp van Hallo zakelijke woordenlijst in Azure Data Catalog en Hallo geregeld tagging deze maakt, kunt u identificeren, beheren en gegevensassets detecteren op een consistente manier. Hallo zakelijke woordenlijst kunt leren van Hallo zakelijke woordenlijst door leden van de organisatie verhogen. Hallo verklarende woordenlijst biedt ook ondersteuning voor het vastleggen zinvolle metadata die asset detectie en inzicht vereenvoudigt.

## <a name="next-steps"></a>Volgende stappen
* [REST-API-documentatie voor bedrijfsactiviteiten verklarende woordenlijst](https://msdn.microsoft.com/library/mt708855.aspx)
