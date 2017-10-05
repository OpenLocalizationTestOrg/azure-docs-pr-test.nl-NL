---
title: 'Problemen oplossen: ''Active Directory'' item is ontbreekt of is niet beschikbaar | Microsoft Docs'
description: Wat te doen wanneer de menuopdracht Active Directory niet wordt weergegeven in de Azure-beheerportal.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="3eafa-103">Problemen oplossen: 'Active Directory' item is ontbreekt of is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="3eafa-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="3eafa-104">Veel van de instructies voor het gebruik van Azure Active Directory-functies en services beginnen met ' Ga naar de Azure-beheerportal en klik **Active Directory**. "</span><span class="sxs-lookup"><span data-stu-id="3eafa-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="3eafa-105">Wat doet u als het Active Directory-extensie of menu-item niet wordt weergegeven of als deze is gemarkeerd, maar **niet beschikbaar**?</span><span class="sxs-lookup"><span data-stu-id="3eafa-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="3eafa-106">Dit onderwerp is bedoeld om u te helpen.</span><span class="sxs-lookup"><span data-stu-id="3eafa-106">This topic is designed to help.</span></span> <span data-ttu-id="3eafa-107">Beschrijft de omstandigheden waaronder **Active Directory** niet wordt weergegeven of is niet beschikbaar en wordt uitgelegd hoe u om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="3eafa-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="3eafa-108">Active Directory ontbreekt</span><span class="sxs-lookup"><span data-stu-id="3eafa-108">Active Directory is missing</span></span>
<span data-ttu-id="3eafa-109">Normaal gesproken een **Active Directory** item wordt weergegeven in het navigatiemenu links.</span><span class="sxs-lookup"><span data-stu-id="3eafa-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="3eafa-110">De instructies in Azure Active Directory-procedures wordt ervan uitgegaan dat dit item in de weergave.</span><span class="sxs-lookup"><span data-stu-id="3eafa-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Schermopname: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="3eafa-112">Het Active Directory-item wordt weergegeven in het navigatiemenu links wanneer elk van de volgende voorwaarden is waar.</span><span class="sxs-lookup"><span data-stu-id="3eafa-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="3eafa-113">Anders wordt weergegeven het item niet.</span><span class="sxs-lookup"><span data-stu-id="3eafa-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="3eafa-114">De huidige gebruiker aangemeld met een Microsoft-account (voorheen bekend als een Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="3eafa-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="3eafa-115">OF</span><span class="sxs-lookup"><span data-stu-id="3eafa-115">OR</span></span>
* <span data-ttu-id="3eafa-116">De Azure-tenant heeft een map en het huidige account is een directory-beheerder.</span><span class="sxs-lookup"><span data-stu-id="3eafa-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="3eafa-117">OF</span><span class="sxs-lookup"><span data-stu-id="3eafa-117">OR</span></span>
* <span data-ttu-id="3eafa-118">De Azure-tenant heeft ten minste één Azure AD Access Control (ACS)-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="3eafa-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="3eafa-119">Zie voor meer informatie [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="3eafa-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="3eafa-120">OF</span><span class="sxs-lookup"><span data-stu-id="3eafa-120">OR</span></span>
* <span data-ttu-id="3eafa-121">De Azure-tenant heeft ten minste één Azure multi-factor Authentication-provider.</span><span class="sxs-lookup"><span data-stu-id="3eafa-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="3eafa-122">Zie voor meer informatie [Azure multi-factor Authentication-Providers beheren](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="3eafa-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="3eafa-123">Klik op om een Access Control-naamruimte of een multi-Factor Authentication-provider **+ nieuw** > **App Services** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3eafa-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="3eafa-124">Als u beheerdersrechten voor een map, hebt u een beheerder een beheerdersrol toewijzen aan uw account.</span><span class="sxs-lookup"><span data-stu-id="3eafa-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="3eafa-125">Zie voor meer informatie [beheerdersrollen toewijzen](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3eafa-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="3eafa-126">Active Directory is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="3eafa-126">Active Directory is not available</span></span>
<span data-ttu-id="3eafa-127">Wanneer u klikt op **+ nieuw** > **App Services**, een **Active Directory** item wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3eafa-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="3eafa-128">De Active Directory-item wordt weergegeven in het bijzonder voor wanneer een van de Active Directory-functies, zoals de map, Access Control of multi-factor Authentication-Provider, beschikbaar voor de huidige gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="3eafa-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="3eafa-129">Echter tijdens het laden van de pagina is het item wordt grijs weergegeven en is gemarkeerd als **niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="3eafa-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="3eafa-130">Dit is een tijdelijke status.</span><span class="sxs-lookup"><span data-stu-id="3eafa-130">This is a temporary state.</span></span> <span data-ttu-id="3eafa-131">Als u een paar seconden wacht, wordt het item beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="3eafa-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="3eafa-132">Als de vertraging wordt verlengd, vernieuwen van de webpagina vaak het probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="3eafa-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Schermopname: Active Directory is niet beschikbaar](./media/active-directory-troubleshooting/not-available.png)

