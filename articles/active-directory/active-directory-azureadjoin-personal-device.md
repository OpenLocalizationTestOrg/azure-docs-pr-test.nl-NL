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
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="855df-103">Deelnemen aan de organisatie van een persoonlijk apparaat tooyour</span><span class="sxs-lookup"><span data-stu-id="855df-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="855df-104">toojoin een Windows 10-apparaat tooyour organisatie</span><span class="sxs-lookup"><span data-stu-id="855df-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="855df-105">Van Hallo **Start** selecteert u **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="855df-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="855df-106">Selecteer **Accounts**, en klik vervolgens op **uw account**.</span><span class="sxs-lookup"><span data-stu-id="855df-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="855df-107">Klik op **toevoegen werk of School-account**, en typt u in uw organisatie-account.</span><span class="sxs-lookup"><span data-stu-id="855df-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="855df-108">Voer uw gebruikersnaam en wachtwoord op Hallo aanmeldingspagina voor uw organisatie, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="855df-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="855df-109">U wordt gevraagd om een challenge multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="855df-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="855df-110">(Deze uitdaging is geconfigureerd door een IT-beheerder.)</span><span class="sxs-lookup"><span data-stu-id="855df-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="855df-111">Azure Active Directory (Azure AD) controleert of Hallo apparaat registratie voor beheer van mobiele apparaten vereist.</span><span class="sxs-lookup"><span data-stu-id="855df-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="855df-112">Windows hello apparaat geregistreerd bij Hallo organisatiemap in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="855df-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="855df-113">Als u een beheerde gebruiker bent, gaat u in Windows desktop toohello via Hallo automatisch aanmelden in.</span><span class="sxs-lookup"><span data-stu-id="855df-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="855df-114">Als u een federatieve gebruiker bent, zult u zijn genomen tooa Windows aanmelden scherm tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="855df-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="855df-115">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="855df-115">Additional information</span></span>
* [<span data-ttu-id="855df-116">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="855df-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="855df-117">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="855df-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="855df-118">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="855df-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* <span data-ttu-id="855df-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="855df-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="855df-120">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="855df-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="855df-121">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="855df-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

