---
title: Azure AD Privileged Identity Management aaaConfigure | Microsoft Docs
description: In dit onderwerp wordt uitgelegd wat Azure AD Privileged Identity Management is en hoe toouse PIM tooimprove de beveiliging van uw cloud.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Wat is Azure AD Privileged Identity Management?
Met Azure Active Directory (AD) Privileged Identity Management kunt u toegang binnen de organisatie beheren, controleren en bewaken. Dit omvat toegang tooresources in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune.  

> [!NOTE]
> Privileged Identity Management is de hele organisatie beschikbaar tooyour wanneer licentie van uw beheerders met Hallo Premium P2-editie van Azure Active Directory. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.

Organisaties wilt toominimize Hallo aantal mensen toegang toosecure informatie of bronnen, omdat die minder kans op Hallo van een kwaadwillende gebruiker die toegang krijgen. Gebruikers moeten echter nog steeds toocarry bevoorrechte bewerkingen in Azure, Office 365 of SaaS-apps. Organisaties gebruikers bevoorrechte toegang te geven in Azure AD zonder te controleren wat gebruikers doen met hun beheerdersbevoegdheden. Azure AD Privileged Identity Management helpt tooresolve dit risico.  

Azure AD Privileged Identity Management kunt u:  

* Zien welke gebruikers zijn Azure AD-beheerders
* On-demand 'just in time' beheerderstoegang tooMicrosoft Online Services, zoals Office 365 en Intune inschakelen
* Rapporten over beheerder toegang tot geschiedenis en wijzigingen in beheerderstoewijzingen ophalen
* Ontvang waarschuwingen over toegang tooa bevoorrechte rol
* Vereist goedkeuring tooactivate (Preview)

Azure AD Privileged Identity Management kunt Hallo ingebouwde Azure AD organisatie rollen, inclusief (maar niet beperkt tot) beheren:  

* Globale beheerder
* Financieel medewerker
* Servicebeheerder  
* De beheerder van de gebruiker
* Wachtwoordbeheerder

## <a name="just-in-time-administrator-access"></a>Alleen bij beheerderstoegang tijd
In het verleden, kunt u een gebruikersrol voor het beheer van tooan via Hallo klassieke Azure-portal of Windows PowerShell toewijzen. Als gevolg hiervan die gebruiker wordt een **permanente beheerder**, altijd actief in Hallo toegewezen rol. Azure AD Privileged Identity Management introduceert Hallo concept van een **in aanmerking komende admin**. In aanmerking komende beheerders moeten gebruikers die bevoorrechte toegang af en toe, maar niet elke dag moeten. Hallo-rol is niet actief totdat Hallo gebruiker toegang, moet vervolgens zij een activering te voltooien en een actieve beheerder voor een vooraf bepaalde hoeveelheid tijd zijn geworden.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Privileged Identity Management voor uw directory inschakelen
U kunt starten met behulp van Azure AD Privileged Identity Management in Hallo [Azure-portal](https://portal.azure.com/).

> [!NOTE]
> U moet een globale beheerder met een organisatieaccount (bijvoorbeeld @yourdomain.com), niet in een Microsoft-account (bijvoorbeeld @outlook.com), tooenable Azure AD Privileged Identity Management voor een map.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) als globale beheerder van uw directory.
2. Als uw organisatie meer dan één map heeft, selecteert u uw gebruikersnaam in Hallo rechterbovenhoek Hallo Azure-portal. Selecteer Hallo map waar u Azure AD Privileged Identity Management gebruikt.
3. Selecteer **meer services** en gebruik Hallo Filter textbox toosearch voor **Azure AD Privileged Identity Management**.
4. Controleer **pincode toodashboard** en klik vervolgens op **maken**. Hallo Privileged Identity Management-toepassing wordt geopend.

Als u bent eerste persoon toouse Azure AD Privileged Identity Management in uw directory hello, Hallo [beveiligingswizard](active-directory-privileged-identity-management-security-wizard.md) wordt u begeleid bij Hallo eerste toewijzing ervaring. Na die u automatisch meer Hallo eerst **beveiligingsbeheerder** en **beheerder met bevoorrechte rol** van Hallo-directory.

Alleen een beheerder met bevoorrechte rol kan toegang beheren voor andere beheerders. U kunt [geeft andere gebruikers Hallo mogelijkheid toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management admin-dashboard
Azure AD Privileged Identity Manager biedt een beheerder dashboard waarmee u belangrijke informatie zoals:

* Waarschuwingen die wijzen op verkoopkansen tooimprove beveiliging
* het aantal gebruikers die zijn toegewezen tooeach bevoorrechte rol Hallo  
* Hallo-nummer van in aanmerking komende en permanente beheerders
* Een grafiek van activeringen voor bevoorrechte rollen in uw directory

![PIM-dashboard - schermafbeelding][2]

## <a name="privileged-role-management"></a>Bevoorrechte rollen beheren
U kunt Hallo beheerders toe te voegen of te verwijderen of de in aanmerking komende beheerders tooeach functie beheren met Azure AD Privileged Identity Management.

![PIM toevoegen of verwijderen administrators - schermafbeelding][3]

## <a name="configure-hello-role-activation-settings"></a>Hallo rol activeringsinstellingen configureren
Met behulp van Hallo [rolinstellingen](active-directory-privileged-identity-management-how-to-change-default-settings.md) kunt u Hallo in aanmerking komende rol activeringseigenschappen, waaronder:

* Hallo duur van de periode voor Hallo rol activeren
* melding van rolactivering Hallo
* Hallo gegevens die een gebruiker moet tooprovide tijdens activeringsproces Hallo-rol
* Nummer van het ticket of incident service
* [Vereisten voor goedkeuring workflow - Preview](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM-instellingen - activering van de administrator - schermafbeelding][4]

Houd er rekening mee dat in de afbeelding Hallo Hallo knoppen voor **multi-Factor Authentication** zijn uitgeschakeld. Voor bepaalde, maximaal beschermde rollen, MFA is vereist voor betere beveiliging.

## <a name="role-activation"></a>Rolactivering
te[een rol activeren](active-directory-privileged-identity-management-how-to-activate-role.md), een in aanmerking komende beheerder vraagt een tijdsgebonden 'activation' voor Hallo-rol. Hallo activering kan worden aangevraagd met behulp van Hallo **mijn rol activeren** optie in Azure AD Privileged Identity Management.

Een beheerder die een rol tooactivate wil moet tooinitialize Azure AD Privileged Identity Management in hello Azure-portal.

Rolactivering kan worden aangepast. In Hallo PIM-instellingen, kunt u bepalen Hallo lengte van Hallo activering en welke informatie Hallo beheerder moet tooprovide tooactivate Hallo rol.

![PIM-beheerder aanvraag rolactivering - schermafbeelding][5]

## <a name="review-role-activity"></a>Rol controleactiviteit
Er zijn twee manieren tootrack hoe uw werknemers en beheerders gebruikt uitgebreide functies. het gebruik van de eerste optie Hallo [Directory rollen controlegeschiedenis](active-directory-privileged-identity-management-how-to-use-audit-log.md). Hallo controlegeschiedenis registreert wijzigingen bijhouden in de toewijzingen van bevoorrechte rollen en rol activering geschiedenis.

![PIM-activering geschiedenis - schermafbeelding][6]

Hallo tweede optie is tooset up reguliere [toegang tot beoordelingen](active-directory-privileged-identity-management-how-to-start-security-review.md). Deze beoordelingen toegang kunnen worden uitgevoerd door en toegewezen revisor (zoals een teammanager) of Hallo werknemers zelf kunnen bekijken. Dit is Hallo aanbevolen manier toomonitor die nog steeds toegang vereist en die niet meer heeft.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM op het abonnement is verlopen
Een tenant toopreview Azure AD PIM controleert voorafgaande tooreaching algemene beschikbaarheid Azure AD PIM werd preview en er zijn geen licentie.  Nu dat Azure AD PIM algemene beschikbaarheid bereikt heeft, moeten proefaccount of betaald licenties toohello beheerders van Hallo tenant toocontinue met PIM worden toegewezen.  Als uw organisatie geen Azure AD Premium-P2 aanschaffen heeft of de proefversie verloopt, wordt voornamelijk al hello Azure AD PIM functies niet langer beschikbaar in uw tenant.  U vindt meer in Hallo [vereisten voor Azure AD PIM-abonnement](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
