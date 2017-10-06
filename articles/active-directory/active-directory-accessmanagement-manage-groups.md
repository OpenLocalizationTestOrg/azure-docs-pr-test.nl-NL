---
title: aaaManaging groepen in Azure Active Directory | Microsoft Docs
description: Hoe toocreate en beheren van groepen toomanage Azure gebruikers met Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Groepen beheren in Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Een van de functies Hallo van Gebruikersbeheer van Azure Active Directory (Azure AD) is Hallo mogelijkheid toocreate groepen gebruikers. U een groep tooperform beheertaken, zoals het toewijzen van licenties of machtigingen tooa aantal gebruikers tegelijk gebruiken. Bovendien kunt u groepen tooassign toegangsmachtigingen voor

* Resources zoals objecten in de directory Hallo
* Bronnen extern toohello directory zoals SaaS-toepassingen, Azure-services, SharePoint-sites of lokale bronnen

Bovendien kan een resource-eigenaar ook toegang tooa resource tooan Azure AD-groep eigendom van iemand anders toewijzen. Deze toewijzing hebben Hallo leden van die groep toegang toohello resource. Hallo-eigenaar van Hallo groep beheert vervolgens lidmaatschap van groep Hallo. Effectief Hallo resource eigenaar gemachtigden toohello eigenaar van Hallo Hallo machtiging tooassign gebruikers tootheir groepsbron.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe toomanage in hello Azure AD-beheercentrum groepen, [een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Hoe maak ik een groep?
Afhankelijk van Hallo services toowhich die uw organisatie is geabonneerd, kunt u een groep met behulp van een van de volgende Hallo:

* Hallo klassieke Azure-portal
* Hallo Office 365-accountportal
* Hallo Windows Intune-accountportal

We beschrijven taken zoals uitgevoerd in de klassieke Azure-portal Hallo. Zie voor meer informatie over het gebruik van niet-Azure-portals toomanage uw Azure AD-directory [beheer van uw Azure AD-directory](active-directory-administer.md).

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.
2. Selecteer Hallo **groepen** tabblad.
3. Selecteer **Groep toevoegen**.
4. In Hallo **groep toevoegen** venster Geef Hallo naam en beschrijving van een groep Hallo.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Hoe kan ik afzonderlijke gebruikers in een beveiligingsgroep toevoegen of verwijderen?
**een afzonderlijke gebruiker tooa groep tooadd**

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.
2. Selecteer Hallo **groepen** tabblad.
3. Hallo groep toowhich u tooadd leden wilt openen. Open Hallo **leden** tabblad Hallo groep geselecteerd als deze nog niet weergeven.
4. Selecteer **Leden toevoegen**.
5. Op Hallo **leden toevoegen** pagina, selecteer Hallo-naam van het Hallo-gebruiker of groep dat u tooadd wilt gebruiken als een lid van deze groep. Controleer of deze naam is toegevoegd toohello **geselecteerde** deelvenster.

**tooremove een afzonderlijke gebruiker uit een groep**

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.
2. Selecteer Hallo **groepen** tabblad.
3. Hallo-groep waaruit u tooremove leden wilt openen.
4. Selecteer Hallo **leden** tabblad, selecteer Hallo-naam van Hallo lid dat u tooremove uit deze groep wilt en klik vervolgens op **verwijderen**.
5. Hallo een opdrachtprompt wilt bevestigen dat u tooremove dit lid uit Hallo-groep.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Hoe kan ik Hallo lidmaatschap van een groep dynamisch beheren?
In Azure AD, kunt u heel eenvoudig een eenvoudige regel toodetermine welke gebruikers toobe lid van Hallo groep zijn instellen. Een eenvoudige regel is een regel die slechts één vergelijking maakt. Bijvoorbeeld, als een groep is toegewezen tooa SaaS-toepassing, kunt u instellen van een regel tooadd gebruikers die de functienaam 'Vertegenwoordiger'. Deze regel verleent toegang vervolgens toothis SaaS-toepassing tooall gebruikers met die functienaam in uw directory.

Wanneer Hallo system evalueert. kenmerken van een wijziging van de gebruiker, worden alle regels voor dynamische groepen in een directory toosee als Hallo kenmerkwijziging van Hallo gebruiker zou een groep toegevoegd of verwijderd. Als een gebruiker voldoet aan een regel voor een groep, worden ze toegevoegd als een lid toothat-groep. Als ze voldoen aan het niet langer Hallo-regel van een groep die ze lid van zijn, worden ze verwijderd als een leden van die groep.

> [!NOTE]
> U kunt een regel instellen voor dynamisch lidmaatschap voor beveiligingsgroepen of Office 365-groepen. Genest groepslidmaatschap worden momenteel niet ondersteund voor toewijzing op basis van een groep tooapplications.
>
> Dynamisch lidmaatschap voor groepen moet een Azure AD Premium-licentie toobe toegewezen aan
>
> * Hallo beheerder van Hallo-regel voor een groep
> * Alle leden van de groep Hallo
>
>

**tooenable dynamisch lidmaatschap voor een groep**

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.
2. Selecteer Hallo **groepen** tabblad en gewenste tooedit open Hallo-groep.
3. Selecteer Hallo **configureren** tabblad en stel vervolgens **dynamische lidmaatschappen inschakelen** te**Ja**.
4. Een eenvoudige regel voor Hallo groep toocontrol instellen hoe dynamisch lidmaatschap werkt voor deze groep. Zorg ervoor dat Hallo **gebruikers toevoegen waarbij** optie is geselecteerd en selecteer vervolgens een gebruikerseigenschap in Hallo lijst (bijvoorbeeld afdeling, functietitel, enz.)
5. Selecteer vervolgens een voorwaarde (niet gelijk aan, gelijk aan, begint niet met, begint met, bevat niet, bevat, geen overeenkomst, overeenkomst).
6. Geef een vergelijkingswaarde voor gebruikerseigenschap Hallo geselecteerd.

toolearn over het toocreate *geavanceerde* regels (regels met meerdere vergelijkingen) voor dynamisch groepslidmaatschap, Zie [met behulp van kenmerken toocreate geavanceerde regels](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Aanvullende informatie
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
