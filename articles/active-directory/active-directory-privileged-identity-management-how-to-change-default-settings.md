---
title: aaaHow toomanage rolinstellingen activering | Microsoft Docs
description: Meer informatie over hoe toochange standaardinstellingen voor bevoegde identiteiten Hallo Hello Azure Active Directory Privileged Identity Management-extensie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Hoe toomanage rolinstellingen activering in Azure AD Privileged Identity Management
Een beheerder met bevoorrechte rol kunt aanpassen Azure AD Privileged Identity Management (PIM) in hun organisatie, inclusief wijzigen Hallo ervaring voor een gebruiker die een in aanmerking komende roltoewijzing is geactiveerd.

## <a name="manage-hello-role-activation-settings"></a>Hallo rol activeringsinstellingen beheren
1. Ga toohello [Azure-portal](https://portal.azure.com) en selecteer Hallo **Azure AD Privileged Identity Management** app vanuit Hallo-dashboard.
2. Selecteer **bevoorrechte rollen beheren** > **instellingen** > **bevoorrechte rollen**.
3. Kies Hallo rol waarvan u de instellingen u wilt dat toomanage.

Er zijn een aantal instellingen die u kunt configureren op Hallo instellingenpagina voor elke rol. Deze instellingen zijn alleen van invloed op gebruikers die in aanmerking komende beheerders, niet-permanente beheerders zijn.

**Activeringen**: Hallo tijd, in uren, die een rol actief blijft voordat het verloopt. Dit kan zijn tussen 1 en 72 uur.

**Meldingen**: U kunt kiezen of Hallo verzendt het afdruksysteem van e-mailberichten tooadmins bevestigen dat ze een rol hebben geactiveerd. Dit kan handig zijn voor het detecteren van niet-geautoriseerde of illegale activeringen zijn.

**Ticket incident/aanvraag**: U kunt kiezen of toorequire in aanmerking komende admins tooinclude een ticket number wanneer ze hun rol activeert. Dit kan nuttig zijn wanneer u de rol toegang audits uitvoert.

**Multi-Factor Authentication**: U kunt kiezen of toorequire gebruikers tooverify hun identiteit met MFA voordat ze hun rollen kunnen activeren. Ze alleen hebben tooverify deze eenmaal per sessie niet elke keer dat ze een rol activeren. Er zijn twee tips tookeep in rekening wanneer u MFA inschakelen:

* Gebruikers met Microsoft-account voor hun e-mailadressen (meestal @outlook.com, maar niet altijd) kan niet registreren voor Azure MFA. Als u tooassign rollen toousers met Microsoft-accounts wilt, moet u doen permanente beheerders of MFA uitschakelen voor die rol.
* U kunt MFA niet uitschakelen voor maximaal bevoorrechte rollen voor Azure AD en Office365. Dit is een functie veiligheid omdat deze rollen moeten zorgvuldig worden beveiligd:  
  
  * Toepassingsbeheerder
  * Toepassingsbeheerder Proxy server
  * Financieel medewerker  
  * Naleving beheerder  
  * CRM-servicebeheerder
  * Klant LockBox toegang goedkeurder
  * Schrijver van de Directory  
  * Exchange-beheerder  
  * Globale beheerder
  * Intune-servicebeheerder
  * Postvak beheerder  
  * Partner tier1-ondersteuning  
  * Partner tier2-ondersteuning  
  * Beheerder met bevoorrechte rol   
  * Beveiligingsbeheerder  
  * SharePoint-beheerder  
  * Skype voor Bedrijven-beheerder  
  * De beheerder van gebruiker  

Zie voor meer informatie over het gebruik van MFA met PIM [hoe tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

