---
title: de organisatie van een persoonlijk apparaat tooyour aaaJoin | Microsoft Docs
description: Wordt uitgelegd hoe gebruikers hun persoonlijke Windows 10-apparaten tootheir bedrijfsnetwerk kunnen registreren en voorziet in implementatiestappen voor een BYOD-scenario.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a>Deelnemen aan de organisatie van een persoonlijk apparaat tooyour
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a>toojoin een Windows 10-apparaat tooyour organisatie
1. Van Hallo **Start** selecteert u **instellingen**.
2. Selecteer **Accounts**, en klik vervolgens op **uw account**.
3. Klik op **toevoegen werk of School-account**, en typt u in uw organisatie-account.
4. Voer uw gebruikersnaam en wachtwoord op Hallo aanmeldingspagina voor uw organisatie, en klik vervolgens op **OK**.
5. U wordt gevraagd om een challenge multi-factor authentication-server. (Deze uitdaging is geconfigureerd door een IT-beheerder.)
6. Azure Active Directory (Azure AD) controleert of Hallo apparaat registratie voor beheer van mobiele apparaten vereist.
7. Windows hello apparaat geregistreerd bij Hallo organisatiemap in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.
8. Als u een beheerde gebruiker bent, gaat u in Windows desktop toohello via Hallo automatisch aanmelden in.
9. Als u een federatieve gebruiker bent, zult u zijn genomen tooa Windows aanmelden scherm tooenter uw referenties.

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

