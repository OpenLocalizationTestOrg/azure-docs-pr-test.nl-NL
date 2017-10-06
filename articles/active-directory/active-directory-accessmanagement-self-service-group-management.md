---
title: aaaSetting van Azure Active Directory voor toepassingsbeheer voor toegang tot selfservice | Microsoft Docs
description: Groepsbeheer met Self-service kunnen gebruikers toocreate en beheren van beveiligingsgroepen of Office 365-groepen in Azure Active Directory en aanbiedingen gebruikers Hallo mogelijkheid toorequest beveiligingsgroep of Office 365-groepslidmaatschappen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Azure Active Directory instellen voor groepsbeheer met self-service
Groepsbeheer met Self-service kunnen gebruikers toocreate en beheren van beveiligingsgroepen of Office 365-groepen in Azure Active Directory (Azure AD). Gebruikers kunnen ook aanvragen beveiligingsgroep of Office 365-groepslidmaatschappen en vervolgens hello eigenaar van de groep Hallo kunt goedkeuren of weigeren lidmaatschap. Op deze manier kan dagelijks beheer van het groepslidmaatschap worden gedelegeerd toopeople die Hallo zakelijke context voor dat lidmaatschap begrijpen. Functies van het zelfservicegroepsbeheer zijn enkel bechikbaar voor beveiligingsgroepen en Office 365-groepen, maar niet voor beveiligingsgroepen met mail of distributielijsten.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

Groepsbeheer met self-service bestaat momenteel uit twee kernscenario's: gedelegeerd groepsbeheer en groepsbeheer met self-service.

* **Gedelegeerd groepsbeheer** een voorbeeld is een beheerder die is het beheren van toegang tooa SaaS-toepassing die Hallo bedrijf wordt gebruikt. Het beheren van deze toegangsrechten is omslachtig en daarom vraagt de beheerder Hallo zakelijke eigenaar toocreate een nieuwe groep. Hallo beheerder wijst toegang voor Hallo toohello nieuwe toepassingsgroep en voegt u toohello groep Iedereen al toegang tot toohello toepassing. eigenaar van het bedrijf Hallo vervolgens meer gebruikers kunt toevoegen en die gebruikers kunnen automatisch ingerichte toohello toepassing. eigenaar van het bedrijf Hallo hoeft niet toowait Hallo beheerder toomanage toegang voor gebruikers. Als Hallo beheerder verleent Hallo dezelfde machtiging tooa manager in een andere bedrijfsgroep, en vervolgens toegang voor hun eigen gebruikers ook door deze persoon beheren kan. Hallo zakelijke eigenaar noch Hallo manager kan bekijken of beheren van de gebruikers. Hallo beheerder kan zien alle gebruikers die toegang toohello toepassing en de toegangsrechten blokkeren indien nodig hebben.
* **Self-service voor groepsbeheer** Een voorbeeld van dit scenario zijn twee gebruikers die allebei SharePoint Online-sites hebben die ze onafhankelijk hebben ingesteld. Ze willen toogive elke dat van andere teams toegang krijgen tot tootheir sites. tooaccomplish, ze kunnen één groep maken in Azure AD en in SharePoint Online elk van die groep tooprovide toegang tootheir site hebt geselecteerd. Wanneer iemand toegang wil, ze daarom vragen van Hallo Toegangspaneel en na goedkeuring krijgen ze toegang tot SharePoint Online-sites tooboth automatisch. Een van deze later besluit dat alle personen toegang hebben tot Hallo site ook toegang tooa bepaalde SaaS-toepassing moet krijgen. Hallo beheerder Hallo SaaS-toepassing kan toegangsrechten voor Hallo toohello SharePoint Online-site-toepassing toevoegen. Daarna geeft alle aanvragen die goedgekeurd toegang toohello twee SharePoint Online-sites en ook toothis SaaS-toepassing.

## <a name="making-a-group-available-for-end-user-self-service"></a>Een groep beschikbaar maken voor self-service door eindgebruikers
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), opent u uw Azure AD-directory.
2. Op Hallo **configureren** tabblad, stelt u **gedelegeerd groepsbeheer** tooEnabled.
3. Stel **gebruikers kunnen beveiligingsgroepen maken** of **gebruikers kunnen Office-groepen maken** tooEnabled.

Wanneer **gebruikers kunnen beveiligingsgroepen maken** is ingeschakeld, alle gebruikers in uw directory nieuwe beveiligingsgroepen toocreate zijn toegestaan en leden toothese groepen toevoegen. Deze nieuwe groepen worden ook weergegeven in Hallo Toegangspaneel voor alle andere gebruikers. Als de beleidsinstelling Hallo op Hallo groep is toegestaan, andere gebruikers kunnen aanvragen toojoin deze groepen maken. Als **Gebruikers kunnen beveiligingsgroepen maken** is uitgeschakeld, kunnen gebruikers geen groepen maken en kunnen ze bestaande groepen waarvan ze een eigenaar zijn niet wijzigen. Ze kunnen echter nog steeds Hallo lidmaatschappen van die groepen beheren en goedkeuren van aanvragen van andere gebruikers toojoin hun groepen.

U kunt ook **gebruikers die self-service voor beveiligingsgroepen gebruiken kunnen** tooachieve een meer gedetailleerd toegangsbeheer via Self-service groepsbeheer voor uw gebruikers. Wanneer **kunnen gebruikers groepen maken** is ingeschakeld, alle gebruikers in uw directory nieuwe groepen toocreate zijn toegestaan en leden toothese groepen toevoegen. Daarnaast de optie **gebruikers die self-service voor beveiligingsgroepen gebruiken kunnen** tooSome, bent u beperken groep management tooonly een beperkte groep gebruikers. Wanneer deze switch is tooSome ingesteld, moet u gebruikers toohello groep SSGMSecurityGroupsUsers toevoegen voordat ze kunnen ook nieuwe groepen maken en toevoegen van leden toothem. Door in te stellen **gebruikers die self-service voor beveiligingsgroepen gebruiken kunnen** tooAll, u alle gebruikers in uw directory nieuwe beveiligingsgroepen toocreate inschakelen.

U kunt ook Hallo **groep die self-service voor beveiligingsgroepen gebruiken kan** vak toospecify een aangepaste naam voor een groep waarvan de leden self-service kunnen gebruiken.

## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
