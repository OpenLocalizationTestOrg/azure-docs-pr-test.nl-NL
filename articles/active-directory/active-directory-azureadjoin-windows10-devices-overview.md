---
title: 'Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work. | Microsoft Docs'
description: Overzicht van de implementatie van Windows 10-apparaten voor ondernemingen, en hoe toointegrate met Azure Active Directory voor Hallo Windows cloud. In tegenstelling tot Hallo verschillende manieren een apparaat kan worden ingericht en gebruikt in een onderneming via hello Azure-portal.
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
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="12daf-105">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="12daf-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="12daf-106">Windows 10 biedt u Hallo mogelijkheid tooleverage Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12daf-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="12daf-107">U kunt Windows 10-apparaten tooAzure AD verbinden, zodat gebruikers zich tooWindows aanmelden kunnen met behulp van Azure AD-accounts of hun Azure-id's toogain toegang toobusiness apps en resources toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="12daf-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Azure Active Directory met Windows-Cloud](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="12daf-109">Windows 10-apparaten integreren met Azure Active Directory--een inhoudsoverzicht</span><span class="sxs-lookup"><span data-stu-id="12daf-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="12daf-110">Hallo volgende onderwerpen bieden inzicht in verschillende mogelijkheden van Windows 10-apparaten in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="12daf-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="12daf-111">Onderwerpen</span><span class="sxs-lookup"><span data-stu-id="12daf-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="12daf-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="12daf-112">Getting started</span></span> |[<span data-ttu-id="12daf-113">Met behulp van Windows 10-apparaten in uw werkplek</span><span class="sxs-lookup"><span data-stu-id="12daf-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="12daf-114">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="12daf-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="12daf-115">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="12daf-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="12daf-116">Implementatie</span><span class="sxs-lookup"><span data-stu-id="12daf-116">Deployment</span></span> |[<span data-ttu-id="12daf-117">Gebruiksscenario's en overwegingen voor de implementatie voor deelname aan Azure AD</span><span class="sxs-lookup"><span data-stu-id="12daf-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="12daf-118">Er is met domeinapparaten tooAzure AD, verbinding te maken voor Windows 10</span><span class="sxs-lookup"><span data-stu-id="12daf-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="12daf-119">Inschakelen Microsoft Passport for work in Hallo organisatie</span><span class="sxs-lookup"><span data-stu-id="12daf-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="12daf-120">Inschakelen van Enterprise State Roaming voor Windows 10</span><span class="sxs-lookup"><span data-stu-id="12daf-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="12daf-121">Gebruikerstaken</span><span class="sxs-lookup"><span data-stu-id="12daf-121">User tasks</span></span> |[<span data-ttu-id="12daf-122">Instellen van een nieuw Windows 10-apparaat met Azure AD tijdens de installatie</span><span class="sxs-lookup"><span data-stu-id="12daf-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="12daf-123">Instellen van een Windows 10-apparaat met Azure AD in Hallo-instellingen</span><span class="sxs-lookup"><span data-stu-id="12daf-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="12daf-124">Lid worden van een persoonlijke tooyour organisatie voor Windows 10-apparaat</span><span class="sxs-lookup"><span data-stu-id="12daf-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

