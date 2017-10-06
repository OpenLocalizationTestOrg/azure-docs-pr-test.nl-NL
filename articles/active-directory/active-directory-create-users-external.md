---
title: gebruikers uit andere directory's of partnerbedrijven in Azure Active Directory aaaAdd | Microsoft Docs
description: Legt uit hoe gebruikers tooadd gebruikersgegevens in Azure Active Directory, inclusief externe en gastgebruikers of wijzigen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Add users from other directories or partner companies in Azure Active Directory (Engelstalig)

Dit artikel wordt uitgelegd hoe tooadd gebruikers uit andere directory's in Azure Active Directory of gebruikers van partnerbedrijven toevoegen. Zie voor meer informatie over het toevoegen van nieuwe gebruikers in uw organisatie en toevoegen van gebruikers die Microsoft-account [toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe tooadd B2B-samenwerking gastgebruikers in Azure AD Hallo beheerder centreren, [wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)

Toegevoegde gebruikers hebben geen beheerdersrechten standaard, maar u kunt functies toothem toewijzen op elk gewenst moment.

## <a name="add-a-user"></a>Een gebruiker toevoegen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **Active Directory** en open vervolgens uw directory.
3. Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens in de opdrachtbalk Hallo **gebruiker toevoegen**.
4. Op Hallo **Vertel ons meer over deze gebruiker** pagina onder **Type gebruiker**, selecteer:

   * **Gebruiker in een andere Azure AD-directory** – voegt een gebruiker account tooyour directory dat afkomstig is van een andere Azure AD-directory. U kunt alleen een gebruiker selecteren in een andere directory als u ook lid van die directory bent.
   * **Gebruikers in partnerbedrijven** -tooinvite en autoriseren van de partner bedrijf gebruikers tooyour directory (Zie [Azure Active Directory B2B-samenwerking](active-directory-b2b-what-is-azure-ad-b2b.md)). U moet te[een CSV-bestand met e-mailadressen uploaden](active-directory-b2b-references-csv-file-format.md).
5. Op gebruiker Hallo **profiel** pagina, Geef een naam en achternaam, een gebruiksvriendelijke naam en een gebruikersrol uit Hallo **rollen** lijst. Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen. Opgeven of te**multi-factor Authentication inschakelen** voor Hallo-gebruiker.
6. Op Hallo **tijdelijk wachtwoord** pagina **maken**.

> [!IMPORTANT]
> Als uw organisatie meer dan één domein gebruikt, moet u weten over Hallo problemen te volgen wanneer u een gebruikersaccount toevoegen:
>
> * tooadd gebruikersaccounts met dezelfde UPN (User Principal Name) in meerdere domeinen, Hallo **eerste** toevoegen, bijvoorbeeld geoffgrisso@contoso.onmicrosoft.com, **gevolgd door** geoffgrisso@contoso.com.
> * Voeg geoffgrisso@contoso.com **niet** vóór geoffgrisso@contoso.onmicrosoft.com toe.
>

Als u gegevens voor een gebruiker waarvan de identiteit is gesynchroniseerd met uw on-premises Active Directory-service wijzigt, kunt u Hallo gebruikersgegevens in de klassieke Azure-portal Hallo niet wijzigen. toochange Hallo gebruikersgegevens, uw lokale Active Directory-beheerhulpprogramma's gebruiken.

## <a name="add-external-users"></a>Externe gebruikers toevoegen
Ook kunt u gebruikers van een andere Azure AD directory toowhich die u deel uitmaakt, of van partnerbedrijven toevoegen door het uploaden van een CSV-bestand. een externe gebruiker tooadd voor **Type gebruiker**, geef **gebruiker in een ander Microsoft Azure AD-directory** of **gebruikers in partnerbedrijven**.

Gebruikers van beide typen zijn afkomstig van een andere directory en worden toegevoegd als **externe gebruikers**. Externe gebruikers kunnen samenwerken met andere gebruikers in een map zonder eventuele vereiste tooadd nieuwe accounts en -referenties. Externe gebruikers verifiëren met hun oorspronkelijke directory wanneer ze zich aanmelden en die verificatie werkt ook voor andere mappen-toowhich die ze zijn toegevoegd.

## <a name="external-user-management-and-limitations"></a>Beheer van externe gebruikers en beperkingen
Wanneer u een gebruiker van een andere directory tooyour map toevoegt, wordt die gebruiker een externe gebruiker in uw directory. Hallo-weergavenaam en een gebruikersnaam worden gekopieerd vanuit hun oorspronkelijke directory en gebruikt voor Hallo externe gebruiker in uw directory. Eigenschappen van het externe gebruikersaccount Hallo zijn daarna geheel onafhankelijk. Als u de eigenschap wijzigingen toohello gebruiker in de oorspronkelijke directory, gelden die wijzigingen niet toohello externe gebruikersaccount in uw directory.

Hallo enige connectie tussen de twee accounts Hallo is dat die gebruiker Hallo altijd wordt geverifieerd met de oorspronkelijke directory of met hun Microsoft-account. Daarom wordt u niet ziet een optie tooreset Hallo wachtwoord of meervoudige verificatie inschakelen voor een externe gebruiker. Hallo verificatiebeleid van de basismap Hallo of Microsoft-account is momenteel Hallo slechts één die wordt geëvalueerd wanneer Hallo gebruiker zich aanmeldt.

> [!NOTE]
> U kunt nog steeds uitschakelen Hallo externe gebruiker in Hallo directory, dat toegang tooyour directory wordt geblokkeerd.
>
>

Als een gebruiker wordt verwijderd uit de oorspronkelijke directory of ze hun Microsoft-account annuleren, wordt de externe gebruiker Hallo nog bestaat in uw directory. Echter, Hallo-gebruiker in uw directory geen toegang tot bronnen omdat ze niet met een oorspronkelijke directory of een Microsoft-account verifiëren.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Services die momenteel toegang door externe gebruikers van Azure AD ondersteunen
* **Klassieke Azure-portal**: kan een externe gebruiker die beheerder is van meerdere mappen toomanage elk van deze mappen.
* **SharePoint Online**: als extern delen is ingeschakeld, kunt u een externe gebruiker tooaccess SharePoint Online geautoriseerd-bronnen.
* **Dynamics CRM**: als de gebruiker Hallo is gelicentieerd via PowerShell, kunt u een externe gebruiker tooaccess geautoriseerde resources in Dynamics CRM.
* **Dynamics AX**: als de gebruiker Hallo is gelicentieerd via PowerShell, kunt u een externe gebruiker tooaccess geautoriseerde resources in Dynamics AX. beperkingen voor Hallo [externe gebruikers van Azure AD](#known-limitations-of-azure-ad-external-users) tooexternal gebruikers in Dynamics AX ook van toepassing.

## <a name="next-steps"></a>Volgende stappen
* [Toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-create-users.md)
* [Azure AD beheren](active-directory-administer.md)
* [Wachtwoorden beheren in Azure AD](active-directory-manage-passwords.md)
* [Groepen beheren in Azure Active Directory](active-directory-manage-groups.md)
