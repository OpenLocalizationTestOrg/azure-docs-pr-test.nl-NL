---
title: aaaHow toosecure toegang tooAzure Data Catalog | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe toosecure catalogus met gegevens en de gegevensassets.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Hoe toosecure toegang krijgen tot de catalogus en gegevens activa toodata
> [!IMPORTANT]
> Deze functie is alleen beschikbaar in standard Hallo-editie van Azure Data Catalog.

Azure Data Catalog, kunt u toospecify die toegang hebben tot Hallo gegevenscatalogus en welke bewerkingen (registreren, aantekeningen toevoegen aan, eigenaar) ze van metagegevens in de catalogus Hallo kunnen uitvoeren. 

## <a name="catalog-users-and-permissions"></a>: Catalogusgebruikers en machtigingen
toogive een gebruiker of een groep Hallo tooa gegevenscatalogus toegang en machtigingen instellen:

1. Op Hallo [startpagina van uw data catalog](http://www.azuredatacatalog.com), klikt u op **instellingen** op Hallo-werkbalk.

    ![catalogus voor gegevens - instellingen](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Vouw in de pagina instellingen Hallo Hallo **Catalogusgebruikers** sectie.
    ![Gebruikers - catalogus toevoegen](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Klik op **Add**.
4. Voer Hallo volledig gekwalificeerd **gebruikersnaam** of de naam van Hallo **beveiligingsgroep** in Azure Active Directory (AAD) die zijn gekoppeld aan de catalogus Hallo Hallo. Gebruik komma (', ') als scheidingsteken als u wilt toevoegen van meer dan één gebruiker of groep.
    ![Gebruikers van de catalogus - gebruikers of groepen](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Druk op **ENTER** of **tabblad** buiten het Hallo-tekstvak. 
6.  Controleer of alle machtigingen (**aantekening**, **registreren**, en **eigenaar**) toothese gebruikers of groepen standaard toegewezen. Dat wil zeggen, Hallo gebruiker of groep kunt [registreren gegevensassets]( data-catalog-how-to-register.md), [aantekeningen toevoegen aan gegevensassets]( data-catalog-how-to-annotate.md), en [eigenaar worden van gegevensassets]( data-catalog-how-to-manage.md). 
    ![Gebruikers van de catalogus - standaardmachtigingen](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive een gebruiker of groep alleen Hallo lezen toegang tot toohello catalogus wissen Hallo **aantekeningen toevoegen aan** optie voor die gebruiker of groep. Wanneer u doet dit, Hallo gebruiker of groep kan niet gegevensassets in Hallo catalogus aantekeningen maar kunnen weergeven. 
8.  toodeny een gebruiker of groep van het registreren van gegevensassets, schakelt u Hallo **registreren** optie voor die gebruiker of groep.
9.  een gebruiker van de eigenaar van een gegevensasset, wissen Hallo toodeny **eigenaar** optie voor die gebruiker of groep. 
10. toodelete een gebruiker of groep van catalogusgebruikers, klikt u op **x** voor Hallo gebruikersgroep Hallo Hallo lijst onderaan in. 
    ![Gebruikers van catalogus - gebruiker verwijderen](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > U wordt aangeraden dat u rechtstreeks toevoegen van beveiliging groepen toocatalog gebruikers in plaats van met toevoegen van gebruikers en machtigingen toe te wijzen. Vervolgens voegt u gebruikers toohello beveiligingsgroepen die overeenkomen met hun rollen en de vereiste toegang toohello-catalogus.

## <a name="special-considerations"></a>Speciale overwegingen

- Hallo machtigingen toegewezen groepen toosecurity additief zijn. Een gebruiker is, en wel in twee groepen. Één groep heeft aantekeningen toevoegen aan machtigingen en andere groep heeft geen hebben aantekeningen machtigingen. Gebruiker heeft vervolgens aantekeningen toevoegen aan machtigingen. 
- Hallo machtigingen toegewezen expliciet tooa gebruiker opheffen Hallo machtigingen worden toegewezen toogroups toowhich Hallo gebruiker behoort. In het vorige voorbeeld hello, bijvoorbeeld u Hallo gebruiker toocatalog gebruikers expliciet zijn toegevoegd en geen toewijzen aantekeningen toevoegen aan machtigingen. Hallo-gebruiker kan geen aantekeningen toevoegen aan gegevensassets Hoewel Hallo gebruiker is lid van een groep die beschikt over aantekeningen toevoegen aan machtigingen.

## <a name="next-steps"></a>Volgende stappen
- [Aan de slag met Azure Data Catalog](data-catalog-get-started.md)

