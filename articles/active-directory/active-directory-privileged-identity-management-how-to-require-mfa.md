---
title: aaaHow toorequire meervoudige verificatie | Microsoft Docs
description: Meer informatie over hoe toorequire multi-factor authentication (MFA) voor bevoegde identiteiten met hello Azure Active Directory Privileged Identity Management-extensie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Hoe toorequire MFA in Azure AD Privileged Identity Management
Het is raadzaam dat u multi-factor authentication (MFA) voor al uw beheerders vereist. Dit vermindert het risico van een aanval vanwege tooa geknoeid wachtwoord Hallo.

U kunt vereisen dat gebruikers een challenge MFA voltooid wanneer ze zich aanmelden. Hallo blogbericht [MFA voor Office 365 en MFA voor Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) vergelijkt wat is opgenomen in de Office- en Azure-abonnementen, met Hallo-functies die zijn opgenomen in Hallo multi-factor Authentication in Microsoft Azure-aanbieding.

U kunt ook vereisen dat gebruikers een challenge MFA voltooien bij het activeren van een rol in Azure AD PIM. Op deze manier als Hallo gebruiker niet een challenge MFA voltooid wanneer ze zich aangemeld, worden deze vraag toodo geval door PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Het vereisen van MFA in Azure AD Privileged Identity Management
Bij het beheren van identiteiten in PIM als een beheerder met bevoorrechte rol, ziet u waarschuwingen die u kunt het beste MFA voor bevoegde accounts. Klik op Hallo beveiliging waarschuwing in Hallo PIM dashboard en een nieuwe blade geopend met een lijst met beheerdersaccounts Hallo die MFA te vereisen.  U kunt MFA vereisen door meerdere rollen selecteren en vervolgens te klikken op Hallo **los** knop, of u kunt op Hallo weglatingstekens volgende tooindividual rollen en klik op Hallo **los** knop.

> [!IMPORTANT]
> Rechts nu werkt alleen voor Azure MFA met werk of schoolaccounts, geen Microsoft-accounts (meestal een persoonlijk account die toosign is gebruikt in tooMicrosoft services zoals Skype, Xbox, Outlook.com, enz.). Daarom kan iedereen met een Microsoft-account een in aanmerking komende beheerder niet omdat ze MFA tooactivate hun rollen niet gebruiken. Als deze gebruikers toocontinue werkbelastingen met een Microsoft-account te beheren moeten, worden de bevoegdheden ze toopermanent beheerders nu.
> 
> 

U kunt bovendien Hallo MFA-vereiste voor een specifieke rol wijzigen door erop te klikken in Hallo sectie van de functies van Hallo PIM-dashboard. Klik vervolgens op **instellingen** in Hallo rolblade en vervolgens te klikken op **inschakelen** onder multi-factor authentication-server.

## <a name="how-azure-ad-pim-validates-mfa"></a>Hoe Azure AD PIM wordt gevalideerd met MFA
Er zijn twee opties voor het valideren van MFA wanneer een gebruiker een rol activeren.

de eenvoudigste optie Hallo is toorely op Azure MFA voor gebruikers die een bevoorrechte rol wilt activeren. toodo deze, eerste controle die deze gebruikers zijn gelicentieerd, indien nodig en hebt geregistreerd voor Azure MFA. Meer informatie over hoe toodo dit is in [aan de slag met Azure multi-factor Authentication in de cloud Hallo](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Het wordt aanbevolen, maar niet vereist, dat u Azure AD tooenforce MFA voor deze gebruikers configureert wanneer ze zich aanmelden. Dit is omdat Hallo MFA wordt door Azure AD PIM zelf wordt uitgevoerd.

Als gebruikers lokale verificatie kunt u ook hebt id-provider is verantwoordelijk voor MFA. Bijvoorbeeld, als u AD Federation Services toorequire smartcard gebaseerde verificatie voor de toegang tot Azure AD hebt geconfigureerd [cloudresources beveiligen met Azure multi-factor Authentication en AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) bevat instructies voor het configureren van AD FS toosend claims tooAzure AD. Wanneer een gebruiker een rol tooactivate probeert, accepteert Azure AD PIM dat MFA is al gevalideerd voor Hallo gebruiker zodra het Hallo juiste claims ontvangt.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

