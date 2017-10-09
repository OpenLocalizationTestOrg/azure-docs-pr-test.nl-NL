---
title: aaaManage gegevensassets in Azure Data Catalog | Microsoft Docs
description: Hallo artikel ziet u hoe toocontrol zichtbaarheid en eigendom van gegevensassets geregistreerd in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Gegevensassets in Azure Data Catalog beheren
## <a name="introduction"></a>Inleiding
Azure Data Catalog is ontworpen voor detectie van de gegevensbron, zodat u eenvoudig kunt detecteren en begrijpen van gegevensbronnen Hallo u tooperform analyse nodig hebt en beslissingen te nemen. Deze mogelijkheden voor detectie maken de grootste impact Hallo wanneer u en andere gebruikers kunnen vinden en begrijpen Hallo breedste scala aan beschikbare gegevensbronnen waren. Met de volgende elementen rekening is Hallo standaardgedrag van Data Catalog voor alle geregistreerde gegevensbronnen toobe zichtbaar tooand kunnen worden gedetecteerd door alle gebruikers van de catalogus.

Data Catalog geeft u geen toegang tot toohello gegevens zelf. Gegevenstoegang wordt bepaald door de eigenaar van de gegevensbron Hallo Hallo. U kunt met Data Catalog gegevensbronnen detecteren en Hallo metagegevens die gerelateerde toohello bronnen die zijn geregistreerd in Hallo-catalogus weergeven.

Er zijn mogelijk situaties echter waar gegevensbronnen alleen zichtbaar toospecific gebruikers of toomembers van specifieke groepen worden mogen. In dergelijke gevallen kunnen gebruikers eigenaar worden van geregistreerde gegevensassets binnen Hallo-catalogus en vervolgens bepalen Hallo zichtbaarheid van Hallo activa die ze eigenaar.

> [!NOTE]
> Hallo-functionaliteit die wordt beschreven in dit artikel is alleen beschikbaar in Standard-editie van Azure Data Catalog Hallo. Hallo biedt editie Free geen mogelijkheden voor eigendom en gegevens asset-zichtbaarheid beperken.
>
>

## <a name="manage-ownership-of-data-assets"></a>Eigendom van gegevensassets beheren
Standaard zijn de gegevensassets die zijn geregistreerd in Data Catalog zonder eigenaar. Elke gebruiker met machtigingen tooaccess Hallo catalog kan detecteren en aantekeningen toevoegen aan deze activa. Gebruikers kunnen eigenaar worden van gegevensassets zonder eigenaar en vervolgens beperken Hallo zichtbaarheid van Hallo activa die ze eigenaar.

Wanneer u het eigendom van een activum gegevens in Data Catalog is alleen gebruikers die zijn geautoriseerd door eigenaren van Hallo Hallo asset detecteren en weergeven van de metagegevens en alleen Hallo eigenaars Hallo asset kunnen verwijderen uit de catalogus Hallo.

> [!NOTE]
> Data Catalog eigendom is van invloed op Hallo alleen metagegevens die zijn opgeslagen in de catalogus Hallo. Eigenaar verleent alle machtigingen op Hallo onderliggende gegevensbron.
>
>

### <a name="take-ownership"></a>Eigenaar worden
Gebruikers kunnen eigenaar worden van gegevensassets door het selecteren van Hallo **eigenaar** optie in Hallo Data Catalog-portal. Er is geen speciale machtigingen zijn vereist tootake eigendom van een actief gegevens zonder eigenaar. Elke gebruiker kan de eigenaar van een activum zonder eigenaar gegevens.

### <a name="add-owners-and-co-owners"></a>Eigenaar en mede-eigenaren toevoegen
Gewoon als een gegevensasset is al het eigendom, andere gebruikers kunnen geen eigenaar. Ze moeten worden toegevoegd als mede-eigenaren door de eigenaar van een bestaande. Eigenaar kunt extra gebruikers of beveiligingsgroepen toevoegen als mede-eigenaren.

> [!NOTE]
> Er is een best practice toohave voor een gegevensasset die eigendom zijn van ten minste twee personen als eigenaars.
>
>

### <a name="remove-owners"></a>Eigenaars verwijderen
Net zoals een activumeigenaar mede-eigenaren toevoegen kunt, kunt een activumeigenaar mede-eigenaar verwijderen.

De eigenaar van een asset die zichzelf als eigenaar van een verwijderd kunt Hallo asset niet langer beheren. Als de activumeigenaar Hallo zichzelf als eigenaar van een verwijderd en er geen andere mede-eigenaars, terug Hallo asset tooan staat geen eigenaar ingesteld.

## <a name="control-visibility"></a>Zichtbaarheid besturingselement
Gegevensasset eigenaars kunnen beheren Hallo zichtbaarheid van gegevensassets Hallo die ze eigenaar zijn. toorestrict zichtbaarheid als Hallo standaard, wanneer alle Data Catalog gebruikers kunnen detecteren en weergave Hallo gegevensasset, activumeigenaar Hallo kunt schakelen Hallo zichtbaarheidsinstelling van **iedereen** te**eigenaars en deze gebruikers** in de eigenschappen van Hallo voor Hallo asset. Eigenaars kunnen vervolgens specifieke gebruikers en beveiligingsgroepen toevoegen.

> [!NOTE]
> Indien mogelijk moeten machtigingen voor het eigendom en de zichtbaarheid van asset toosecurity groepen en niet tooindividual gebruikers worden toegewezen.
>
>

## <a name="catalog-administrators"></a>Beheerders van de catalogus
Data Catalog beheerders zijn impliciet mede-eigenaren van alle activa in Hallo-catalogus. Asset eigenaars zichtbaarheid aan beheerders niet verwijderen en beheerders kunnen beheren, eigendom en de zichtbaarheid van alle gegevens activa in Hallo-catalogus.

## <a name="summary"></a>Samenvatting
Hallo Data Catalog crowdsourcing-model toometadata asset detectie en kunnen alle catalogus gebruikers toocontribute en detecteren. Hallo Standard-editie van Data Catalog is ontworpen voor het eigenaarschap en beheer toolimit Hallo zichtbaarheid en het gebruik van specifieke gegevensassets.
