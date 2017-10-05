---
title: Azure AD Privileged Identity Management configureren | Microsoft Docs
description: Dit onderwerp wordt beschreven wat Azure AD Privileged Identity Management is en hoe u PIM gebruikt om de beveiliging van uw cloud te verbeteren.
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
ms.openlocfilehash: eb7059368cb80be7dd625f9dc6ad2aab1bad709a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Wat is Azure AD Privileged Identity Management?
Met Azure Active Directory (AD) Privileged Identity Management kunt u toegang binnen de organisatie beheren, controleren en bewaken. Dit is inclusief toegang tot resources in Azure AD en andere Microsoft-onlineservices zoals Office 365 en Microsoft Intune.  

> [!NOTE]
> Privileged Identity Management is beschikbaar voor uw hele organisatie wanneer u uw beheerders met de Premium P2-editie van Azure Active Directory van licentie. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.

Beperk het aantal gebruikers die toegang tot beveiligde gegevens of bronnen heeft, omdat die vermindert de kans op een kwaadwillende gebruiker die toegang krijgen dat organisaties willen. Gebruikers moeten echter nog steeds bij het uitvoeren van bevoorrechte bewerkingen in Azure, Office 365 of SaaS-apps. Organisaties gebruikers bevoorrechte toegang te geven in Azure AD zonder te controleren wat gebruikers doen met hun beheerdersbevoegdheden. Azure AD Privileged Identity Management helpt bij het oplossen van dit risico.  

Azure AD Privileged Identity Management kunt u:  

* Zien welke gebruikers zijn Azure AD-beheerders
* On-demand 'just in time' beheerderstoegang toewijzen voor Microsoft Online Services, zoals Office 365 en Intune inschakelen
* Rapporten over beheerder toegang tot geschiedenis en wijzigingen in beheerderstoewijzingen ophalen
* Ontvang waarschuwingen over de toegang tot een bevoorrechte rol
* Goedkeuring vereist voor het activeren van (Preview)

Azure AD Privileged Identity Management kunt beheren de ingebouwde Azure AD organisatie-functies, inclusief (maar niet beperkt tot):  

* Globale beheerder
* Financieel medewerker
* Servicebeheerder  
* De beheerder van de gebruiker
* Wachtwoordbeheerder

## <a name="just-in-time-administrator-access"></a>Alleen bij beheerderstoegang tijd
In het verleden hebben toewijzen u een gebruiker aan een rol admin via de klassieke Azure-portal of de Windows PowerShell. Als gevolg hiervan die gebruiker wordt een **permanente beheerder**, altijd actief is in de toegewezen rol. Azure AD Privileged Identity Management introduceert het concept van een **in aanmerking komende admin**. In aanmerking komende beheerders moeten gebruikers die bevoorrechte toegang af en toe, maar niet elke dag moeten. De rol is niet actief totdat de gebruiker toegang, moet vervolgens zij een activering te voltooien en een actieve beheerder voor een vooraf bepaalde hoeveelheid tijd zijn geworden.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Privileged Identity Management voor uw directory inschakelen
U kunt starten met Azure AD Privileged Identity Management in de [Azure-portal](https://portal.azure.com/).

> [!NOTE]
> U moet een globale beheerder met een organisatieaccount (bijvoorbeeld @yourdomain.com), niet in een Microsoft-account (bijvoorbeeld @outlook.com), zodat de Azure AD Privileged Identity Management voor een map.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/) als globale beheerder van uw directory.
2. Als uw organisatie meerdere directory's heeft, selecteert u uw gebruikersnaam rechtsboven in de Azure Portal. Selecteer de map waar u Azure AD Privileged Identity Management gebruikt.
3. Selecteer **Meer services** en gebruik het tekstvak Filteren om te zoeken naar **Azure AD Privileged Identity Management**.
4. Schakel **Vastmaken aan dashboard** in en klik op de knop **Maken**. De Privileged Identity Management-toepassing wordt geopend.

Als u de eerste persoon bent die Azure AD Privileged Identity Management in uw directory gebruikt, wordt u via de [wizard Beveiliging](active-directory-privileged-identity-management-security-wizard.md) stapsgewijs begeleid bij de eerste toewijzing. Hierna als u automatisch de eerste **beveiligingsbeheerder** en **beheerder met bevoorrechte rol** van de map.

Alleen een beheerder met bevoorrechte rol kan toegang beheren voor andere beheerders. U kunt [bieden andere gebruikers de mogelijkheid om te beheren en PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management admin-dashboard
Azure AD Privileged Identity Manager biedt een beheerder dashboard waarmee u belangrijke informatie zoals:

* Waarschuwingen die wijzen op de mogelijkheden voor verbeterde beveiliging
* Het aantal gebruikers die zijn toegewezen aan elke bevoorrechte rol  
* Het aantal in aanmerking komende en permanente beheerders
* Een grafiek van activeringen voor bevoorrechte rollen in uw directory

![PIM-dashboard - schermafbeelding][2]

## <a name="privileged-role-management"></a>Bevoorrechte rollen beheren
Met Azure AD Privileged Identity Management, kunt u de beheerders beheren door toe te voegen of te verwijderen of de in aanmerking komende beheerders aan elke rol.

![PIM toevoegen of verwijderen administrators - schermafbeelding][3]

## <a name="configure-the-role-activation-settings"></a>Configureer de instellingen van de activering
Met behulp van de [rolinstellingen](active-directory-privileged-identity-management-how-to-change-default-settings.md) kunt u de rol van in aanmerking komende activering-eigenschappen, waaronder:

* De duur van de rol activeringsperiode
* De melding van rolactivering
* De informatie die een gebruiker moet worden geleverd tijdens de activering van de rol
* Nummer van het ticket of incident service
* [Vereisten voor goedkeuring workflow - Preview](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM-instellingen - activering van de administrator - schermafbeelding][4]

Houd er rekening mee dat in de installatiekopie van de knoppen voor **multi-Factor Authentication** zijn uitgeschakeld. Voor bepaalde, maximaal beschermde rollen, MFA is vereist voor betere beveiliging.

## <a name="role-activation"></a>Rolactivering
Naar [een rol activeren](active-directory-privileged-identity-management-how-to-activate-role.md), een in aanmerking komende beheerder vraagt een tijdsgebonden 'activation' voor de rol. De activering kan worden aangevraagd met behulp van de **mijn rol activeren** optie in Azure AD Privileged Identity Management.

Een beheerder die een rol activeren wil moet het initialiseren van Azure AD Privileged Identity Management in Azure portal.

Rolactivering kan worden aangepast. In de PIM-instellingen, kunt u bepalen de lengte van de activering en wat de beheerder moet worden geleverd voor het activeren van de rol informatie.

![PIM-beheerder aanvraag rolactivering - schermafbeelding][5]

## <a name="review-role-activity"></a>Rol controleactiviteit
Er zijn twee manieren om bij te houden hoe uw werknemers en beheerders bevoorrechte rollen gebruiken. Het gebruik van de eerste optie [Directory rollen controlegeschiedenis](active-directory-privileged-identity-management-how-to-use-audit-log.md). De controlegeschiedenis registreert het bijhouden van wijzigingen in de toewijzingen van bevoorrechte rollen en rol activering geschiedenis.

![PIM-activering geschiedenis - schermafbeelding][6]

De tweede optie is het instellen van reguliere [toegang tot beoordelingen](active-directory-privileged-identity-management-how-to-start-security-review.md). Deze beoordelingen toegang kunnen worden uitgevoerd door en toegewezen revisor (zoals een teammanager) of de werknemers zelf kunnen bekijken. Dit is de beste manier om te controleren die nog steeds toegang is vereist en die niet langer wordt.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM op het abonnement is verlopen
Vóór de algemene beschikbaarheid is bereikt Azure AD PIM Preview-versie is en er zijn geen controles licentie voor een tenant voor de preview van Azure AD PIM.  Nu dat Azure AD PIM algemene beschikbaarheid bereikt heeft, moeten proefaccount of betaald licenties worden toegewezen aan de groep administrators van de tenant wilt blijven gebruiken PIM.  Als uw organisatie geen Azure AD Premium-P2 aanschaffen heeft of de proefversie verloopt, wordt voornamelijk alle Azure AD PIM functies niet langer beschikbaar in uw tenant.  U kunt meer informatie in de [vereisten voor Azure AD PIM-abonnement](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
