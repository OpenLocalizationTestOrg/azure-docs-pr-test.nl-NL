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
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="b838d-103">Een persoonlijke apparaat koppelt aan uw organisatie</span><span class="sxs-lookup"><span data-stu-id="b838d-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="b838d-104">Een Windows 10-apparaat koppelen aan uw organisatie</span><span class="sxs-lookup"><span data-stu-id="b838d-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="b838d-105">Van de **Start** selecteert u **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b838d-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="b838d-106">Selecteer **Accounts**, en klik vervolgens op **uw account**.</span><span class="sxs-lookup"><span data-stu-id="b838d-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="b838d-107">Klik op **toevoegen werk of School-account**, en typt u in uw organisatie-account.</span><span class="sxs-lookup"><span data-stu-id="b838d-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="b838d-108">Voer uw gebruikersnaam en wachtwoord op de aanmeldingspagina voor uw organisatie, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b838d-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="b838d-109">U wordt gevraagd om een challenge multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="b838d-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="b838d-110">(Deze uitdaging is geconfigureerd door een IT-beheerder.)</span><span class="sxs-lookup"><span data-stu-id="b838d-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="b838d-111">Azure Active Directory (Azure AD) controleert of het apparaat is vereist voor inschrijving voor beheer van mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="b838d-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="b838d-112">Windows het apparaat in de map van de organisatie wordt geregistreerd in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b838d-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="b838d-113">Als u een beheerde gebruiker bent, gaat Windows u naar het bureaublad via het automatisch aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b838d-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="b838d-114">Als u een federatieve gebruiker bent, gaat u naar een Windows-aanmeldingsscherm uw referenties in te voeren.</span><span class="sxs-lookup"><span data-stu-id="b838d-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="b838d-115">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="b838d-115">Additional information</span></span>
* <span data-ttu-id="b838d-116">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)</span><span class="sxs-lookup"><span data-stu-id="b838d-116">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md)</span></span>
* <span data-ttu-id="b838d-117">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)</span><span class="sxs-lookup"><span data-stu-id="b838d-117">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)</span></span>
* [<span data-ttu-id="b838d-118">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="b838d-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* <span data-ttu-id="b838d-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="b838d-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* <span data-ttu-id="b838d-120">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)</span><span class="sxs-lookup"><span data-stu-id="b838d-120">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)</span></span>
* [<span data-ttu-id="b838d-121">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="b838d-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

