---
title: Extern delen van Office 365 en Azure Active Directory B2B-samenwerking | Microsoft Docs
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="37aa1-103">Extern delen van Office 365 en Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="37aa1-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="37aa1-104">Extern delen in Office 365 (OneDrive, SharePoint Online, uniforme, groepen, enzovoort) en Azure Active Directory (Azure AD) B2B-samenwerking zijn technisch hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="37aa1-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="37aa1-105">Alle extern delen (met uitzondering van OneDrive/SharePoint Online), inclusief gasten in Office 365-groepen, wordt de Azure AD B2B-samenwerking uitnodiging API's al gebruikt voor het delen.</span><span class="sxs-lookup"><span data-stu-id="37aa1-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="37aa1-106">OneDrive/SharePoint Online heeft een uitnodiging voor een afzonderlijke-manager.</span><span class="sxs-lookup"><span data-stu-id="37aa1-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="37aa1-107">Ondersteuning voor extern delen in OneDrive/SharePoint Online gestart voordat de ondersteuning die Azure AD zijn ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="37aa1-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="37aa1-108">Na verloop van tijd OneDrive/SharePoint Online extern delen, is enkele functies samengevoegd en veel miljoenen gebruikers die gebruikmaken van het product van de ingebouwde patroon delen.</span><span class="sxs-lookup"><span data-stu-id="37aa1-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="37aa1-109">Er zijn echter enkele subtiele verschillen tussen hoe extern delen OneDrive/SharePoint Online werkt en de werking van Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="37aa1-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="37aa1-110">OneDrive/SharePoint Online gebruikers toegevoegd aan de map nadat gebruikers hebben hun uitnodigingen ingewisseld.</span><span class="sxs-lookup"><span data-stu-id="37aa1-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="37aa1-111">Dus voordat inwisseling er geen de gebruiker in Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="37aa1-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="37aa1-112">Als een andere site in de tussentijd nodigt van een gebruiker, wordt een nieuwe uitnodiging gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="37aa1-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="37aa1-113">Wanneer u Azure AD B2B-samenwerking, worden gebruikers echter toegevoegd onmiddellijk op uitnodiging zodat ze overal worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="37aa1-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="37aa1-114">De ervaring van de inwisselcode in OneDrive/SharePoint Online er anders uit de ervaring in Azure AD B2B-samenwerking.</span><span class="sxs-lookup"><span data-stu-id="37aa1-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="37aa1-115">Nadat een gebruiker een uitnodiging wordt ingewisseld, worden de ervaringen lijken.</span><span class="sxs-lookup"><span data-stu-id="37aa1-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="37aa1-116">Azure AD B2B-samenwerking uitgenodigd gebruikers kunnen worden verzameld van OneDrive/SharePoint Online-dialoogvensters voor delen.</span><span class="sxs-lookup"><span data-stu-id="37aa1-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="37aa1-117">OneDrive/SharePoint Online uitgenodigd gebruikers ook weergegeven in Azure AD wanneer ze hun uitnodigingen inwisselen.</span><span class="sxs-lookup"><span data-stu-id="37aa1-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="37aa1-118">Voor het beheren van extern delen in OneDrive/SharePoint Online met Azure AD B2B-samenwerking ingesteld OneDrive/SharePoint Online extern delen instelling **dat alleen delen met externe gebruikers al in de map**.</span><span class="sxs-lookup"><span data-stu-id="37aa1-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="37aa1-119">Gebruikers kunnen gaat u naar extern gedeelde sites en kiest uit externe deelnemers die de beheerder heeft toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="37aa1-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="37aa1-120">De beheerder kan de externe deelnemers via de B2B-samenwerking uitnodiging API's kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37aa1-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![De OneDrive/SharePoint Online extern delen van de instelling](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="37aa1-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37aa1-122">Next steps</span></span>

<span data-ttu-id="37aa1-123">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="37aa1-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="37aa1-124">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="37aa1-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="37aa1-125">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="37aa1-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="37aa1-126">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="37aa1-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="37aa1-127">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="37aa1-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="37aa1-128">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="37aa1-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="37aa1-129">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="37aa1-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="37aa1-130">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="37aa1-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="37aa1-131">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="37aa1-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="37aa1-132">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="37aa1-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="37aa1-133">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="37aa1-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
