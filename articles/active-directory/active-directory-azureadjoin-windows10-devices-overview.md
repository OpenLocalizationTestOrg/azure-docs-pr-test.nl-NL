---
title: 'Windows 10 voor ondernemingen: manieren apparaten gebruiken voor werk | Microsoft Docs'
description: Overzicht van de implementatie van Windows 10-apparaten voor ondernemingen, en het integreren met Azure Active Directory voor de Windows-cloud. Anders dan de verschillende manieren een apparaat kunnen worden ingericht en gebruikt in een onderneming via de Azure portal.
keywords: cloud van Windows, Windows op Azure Active Directory, Windows 10-apparaten op Azure, Azure Windows-apparaten
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="74e2f-105">Windows 10 for the enterprise: Ways to use devices for work (Engelstalig)</span><span class="sxs-lookup"><span data-stu-id="74e2f-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="74e2f-106">Windows 10 biedt u de mogelijkheid voor het benutten van Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74e2f-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="74e2f-107">U kunt Windows 10-apparaten verbinden met Azure AD, zodat gebruikers bij Windows aanmelden zich met behulp van Azure AD-accounts of door de Azure-id's toe te voegen toegang te krijgen tot zakelijke apps en resources.</span><span class="sxs-lookup"><span data-stu-id="74e2f-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory met Windows-Cloud](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="74e2f-109">Windows 10-apparaten integreren met Azure Active Directory--een inhoudsoverzicht</span><span class="sxs-lookup"><span data-stu-id="74e2f-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="74e2f-110">De volgende onderwerpen bieden inzicht in verschillende mogelijkheden van Windows 10-apparaten in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="74e2f-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="74e2f-111">Onderwerpen</span><span class="sxs-lookup"><span data-stu-id="74e2f-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="74e2f-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="74e2f-112">Getting started</span></span> |[<span data-ttu-id="74e2f-113">Met behulp van Windows 10-apparaten in uw werkplek</span><span class="sxs-lookup"><span data-stu-id="74e2f-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> <span data-ttu-id="74e2f-114">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)</span><span class="sxs-lookup"><span data-stu-id="74e2f-114">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md)</span></span> <br> <br> [<span data-ttu-id="74e2f-115">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="74e2f-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="74e2f-116">Implementatie</span><span class="sxs-lookup"><span data-stu-id="74e2f-116">Deployment</span></span> |[<span data-ttu-id="74e2f-117">Gebruiksscenario's en overwegingen voor de implementatie voor deelname aan Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e2f-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="74e2f-118">Domein-apparaten verbinding laten maken met Azure AD voor Windows 10 optreedt</span><span class="sxs-lookup"><span data-stu-id="74e2f-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="74e2f-119">Microsoft Passport for work. in de organisatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="74e2f-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="74e2f-120">Inschakelen van Enterprise State Roaming voor Windows 10</span><span class="sxs-lookup"><span data-stu-id="74e2f-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="74e2f-121">Gebruikerstaken</span><span class="sxs-lookup"><span data-stu-id="74e2f-121">User tasks</span></span> |[<span data-ttu-id="74e2f-122">Instellen van een nieuw Windows 10-apparaat met Azure AD tijdens de installatie</span><span class="sxs-lookup"><span data-stu-id="74e2f-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="74e2f-123">Instellen van een Windows 10-apparaat met Azure AD in het menu instellingen</span><span class="sxs-lookup"><span data-stu-id="74e2f-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="74e2f-124">U een persoonlijk Windows 10-apparaat toevoegt aan uw organisatie</span><span class="sxs-lookup"><span data-stu-id="74e2f-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

