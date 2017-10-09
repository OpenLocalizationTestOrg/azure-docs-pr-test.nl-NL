---
title: aaaOffice 365 extern delen en Azure Active Directory B2B-samenwerking | Microsoft Docs
description: claims toewijzing verwijzing voor Azure Active Directory B2B-samenwerking
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1d54b-103">Extern delen van Office 365 en Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1d54b-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1d54b-104">Extern delen in Office 365 (OneDrive, SharePoint Online, uniforme, groepen, enz.) en Azure Active Directory (Azure AD) B2B collaboration zijn technisch Hallo dezelfde ding.</span><span class="sxs-lookup"><span data-stu-id="1d54b-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="1d54b-105">Alle extern delen (met uitzondering van OneDrive/SharePoint Online), inclusief gasten in Office 365-groepen, al hello Azure AD B2B-samenwerking uitnodiging API's gebruikt voor het delen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="1d54b-106">OneDrive/SharePoint Online heeft een uitnodiging voor een afzonderlijke-manager.</span><span class="sxs-lookup"><span data-stu-id="1d54b-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="1d54b-107">Ondersteuning voor extern delen in OneDrive/SharePoint Online gestart voordat de ondersteuning die Azure AD zijn ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="1d54b-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="1d54b-108">Na verloop van tijd OneDrive/SharePoint Online extern delen, is enkele functies samengevoegd en veel miljoenen gebruikers die werken met Hallo product van de ingebouwde patroon delen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="1d54b-109">Er zijn echter enkele subtiele verschillen tussen hoe extern delen OneDrive/SharePoint Online werkt en de werking van Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="1d54b-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="1d54b-110">OneDrive/SharePoint Online voegt gebruikers toohello directory nadat gebruikers hebben hun uitnodigingen ingewisseld.</span><span class="sxs-lookup"><span data-stu-id="1d54b-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="1d54b-111">Dus voordat inwisseling er geen Hallo-gebruiker in Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="1d54b-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="1d54b-112">Als een andere site tussentijd een gebruiker in hello nodigt, wordt een uitnodiging voor een nieuwe gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1d54b-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="1d54b-113">Wanneer u Azure AD B2B-samenwerking, worden gebruikers echter toegevoegd onmiddellijk op uitnodiging zodat ze overal worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d54b-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="1d54b-114">Hallo inwisseling ervaring in OneDrive/SharePoint Online er anders uit Hallo ervaring in Azure AD B2B-samenwerking.</span><span class="sxs-lookup"><span data-stu-id="1d54b-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="1d54b-115">Nadat een gebruiker een uitnodiging wordt ingewisseld, lijken Hallo ervaringen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="1d54b-116">Azure AD B2B-samenwerking uitgenodigd gebruikers kunnen worden verzameld van OneDrive/SharePoint Online-dialoogvensters voor delen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="1d54b-117">OneDrive/SharePoint Online uitgenodigd gebruikers ook weergegeven in Azure AD wanneer ze hun uitnodigingen inwisselen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="1d54b-118">externe toomanage delen in OneDrive/SharePoint Online met Azure AD B2B-samenwerking ingesteld Hallo OneDrive/SharePoint Online extern delen te stellen**dat alleen delen met externe gebruikers al in de map Hallo**.</span><span class="sxs-lookup"><span data-stu-id="1d54b-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="1d54b-119">Gebruikers kunnen gaan tooexternally gedeelde sites en kiezen uit externe deelnemers die Hallo beheerder is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1d54b-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="1d54b-120">Hallo beheerder kan Hallo externe deelnemers via Hallo B2B-samenwerking uitnodiging API's kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1d54b-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Hallo extern delen instelling OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="1d54b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d54b-122">Next steps</span></span>

<span data-ttu-id="1d54b-123">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="1d54b-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1d54b-124">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="1d54b-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1d54b-125">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1d54b-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1d54b-126">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d54b-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1d54b-127">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="1d54b-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1d54b-128">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1d54b-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1d54b-129">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="1d54b-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1d54b-130">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="1d54b-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1d54b-131">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="1d54b-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1d54b-132">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="1d54b-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1d54b-133">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1d54b-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
