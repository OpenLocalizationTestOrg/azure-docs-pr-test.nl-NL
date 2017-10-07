---
title: aaaSecuring bevoorrechte toegang in Azure AD | Microsoft Docs
description: Dit onderwerp wordt beschreven Hallo benadert voor bevoegde toegang beveiligen in Azure, Azure Active Directory en Microsoft Online Services.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Bevoegde toegang beveiligen in Azure AD
Beveiligen van bevoegde toegang is een belangrijke eerste stap toohelp bedrijfsmiddelen in een moderne organisatie beveiligen. Bevoegde accounts zijn accounts dat beheren en het beheer van IT-systemen. Cyberbeveiliging aanvallers doel voor deze accounts toogain toegang tooan van gegevens en organisatie-systemen. toosecure bevoegde toegang, moet u Hallo accounts isoleren en systemen van Hallo risico worden blootgesteld tooa kwaadwillende gebruiker.

Meer gebruikers zijn tooget bevoegde toegang via cloud-services wordt gestart. Dit kunnen bijvoorbeeld globale beheerders van Office365, Azure-abonnementbeheerders en gebruikers die beheerderstoegang op de SaaS-apps of virtuele machines hebben.

Microsoft raadt u Volg deze roadmap op [bevoegde toegang beveiligen](https://technet.microsoft.com/library/mt631194.aspx).

Deze principes toepassen voor klanten met Azure Active Directory, Office 365 of andere Microsoft-services en toepassingen, of gebruikersaccounts worden beheerd en geverifieerd door Active Directory of in Azure Active Directory. Hallo volgende secties bevatten meer informatie over Azure AD-functies toosupport bevoegde toegang beveiligen.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
tooincrease hello beveiliging van de verificatie door de beheerder, moet u de verificatie in twee stappen voordat u verleent rechten vereisen. Verificatie in twee stappen is een methode om te controleren wie u bent die Hallo gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist. Het biedt een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties.

Azure multi-factor Authentication (MFA) is een oplossing van Microsoft in twee stappen verificatie, welke u beveiligt toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Sterke verificatie via een bereik van eenvoudige verificatie-opties zoals levert:

- telefoongesprekken
- SMS-berichten
- mobiele app-meldingen
- mobiele app verificatiecodes
- OATH-tokens van derde partij

Zie voor een overzicht van de werking van Azure multi-factor Authentication Hallo video te volgen:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Zie voor meer informatie [MFA voor Office 365 en MFA voor Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Tijdsgebonden bevoegdheden
Sommige organisaties kunnen het gebeuren dat ze te veel gebruikers in maximaal bevoorrechte rollen hebben. Een gebruiker mogelijk toegevoegd toohello rol voor een bepaalde activiteit, zoals toosign voor een service, maar deze rechten niet vaak later gebruiken.

toolower hello blootstellingstijd bevoegdheden en het verhogen van de zichtbaarheid van hun gebruik, limiet gebruikers tooonly nemen over hun bevoegdheden 'just in time' (Just in time), wanneer ze een taak tooperform nodig. Voor Azure Active Directory en Microsoft Online Services, kunt u [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).

![PIM-dashboard][2]

## <a name="attack-detection"></a>Aanvalsdetectie
[Azure Active Directory: Identity Protection](../active-directory-identityprotection.md) biedt een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie. Op basis van de risico's, Identity Protection berekent het risiconiveau van een gebruiker voor elke gebruiker, zodat u tooconfigure risico beleid op basis van tooautomatically beveiligen Hallo identiteiten van uw organisatie. Dit beleid, samen met andere besturingselementen voorwaardelijke toegang is verstrekt door Azure Active Directory en EMS, kunnen automatisch Hallo gebruiker blokkeren of suggesties met wachtwoord opnieuw instellen en afdwingen van multi-factor authentication-server.

![Azure AD-identiteitsbeveiliging][3]

## <a name="conditional-access"></a>Voorwaardelijke toegang
Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van een gebruiker, alvorens deze toegang tooan toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan.

![Instellen van regels voor voorwaardelijke toegang met MFA][4]

## <a name="related-articles"></a>Verwante artikelen:
* Schakel [Azure multi-factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Schakel [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Schakel [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Schakel [voorwaardelijk toegangsbeheer](../active-directory-conditional-access.md)

Zie voor meer informatie over het bouwen van een volledige beveiliging roadmap Hallo 'verantwoordelijkheden van de klant en roadmap' sectie Hallo [Microsoft Cloud Security voor Enterprise-architecten](http://aka.ms/securecustomer) document. Voor meer informatie over Microsoft-services tooassist met een van deze onderwerpen bezighouden, neem contact op met uw Microsoft-vertegenwoordiger of gaat u naar onze [Cybersecurity oplossingen pagina](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
