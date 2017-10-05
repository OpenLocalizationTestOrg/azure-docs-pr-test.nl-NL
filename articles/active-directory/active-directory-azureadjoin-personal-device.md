---
title: Een persoonlijke apparaat koppelt aan uw organisatie | Microsoft Docs
description: Wordt uitgelegd hoe gebruikers hun eigen Windows 10-apparaten met het bedrijfsnetwerk kunnen registreren en voorziet in implementatiestappen voor een BYOD-scenario.
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
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a>Een persoonlijke apparaat koppelt aan uw organisatie
## <a name="to-join-a-windows-10-device-to-your-organization"></a>Een Windows 10-apparaat koppelen aan uw organisatie
1. Van de **Start** selecteert u **instellingen**.
2. Selecteer **Accounts**, en klik vervolgens op **uw account**.
3. Klik op **toevoegen werk of School-account**, en typt u in uw organisatie-account.
4. Voer uw gebruikersnaam en wachtwoord op de aanmeldingspagina voor uw organisatie, en klik vervolgens op **OK**.
5. U wordt gevraagd om een challenge multi-factor authentication-server. (Deze uitdaging is geconfigureerd door een IT-beheerder.)
6. Azure Active Directory (Azure AD) controleert of het apparaat is vereist voor inschrijving voor beheer van mobiele apparaten.
7. Windows het apparaat in de map van de organisatie wordt geregistreerd in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.
8. Als u een beheerde gebruiker bent, gaat Windows u naar het bureaublad via het automatisch aanmelden.
9. Als u een federatieve gebruiker bent, gaat u naar een Windows-aanmeldingsscherm uw referenties in te voeren.

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

