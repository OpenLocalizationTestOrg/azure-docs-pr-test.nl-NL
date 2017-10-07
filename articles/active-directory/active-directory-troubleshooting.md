---
title: 'Problemen oplossen: ''Active Directory'' item is ontbreekt of is niet beschikbaar | Microsoft Docs'
description: Welke toodo wanneer Active Directory-menu-item wordt niet in hello Azure Management Portal weergegeven.
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
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="d2535-103">Problemen oplossen: 'Active Directory' item is ontbreekt of is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="d2535-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="d2535-104">Veel van Hallo instructies voor het gebruik van Azure Active Directory-functies en services beginnen met ' Ga toohello Azure Management Portal en klik op **Active Directory**. "</span><span class="sxs-lookup"><span data-stu-id="d2535-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="d2535-105">Wat doet u als Hallo Active Directory-extensie of menu-item niet weergegeven of als deze is gemarkeerd, maar **niet beschikbaar**?</span><span class="sxs-lookup"><span data-stu-id="d2535-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="d2535-106">Dit onderwerp is ontworpen toohelp.</span><span class="sxs-lookup"><span data-stu-id="d2535-106">This topic is designed toohelp.</span></span> <span data-ttu-id="d2535-107">Beschrijft Hallo omstandigheden waaronder **Active Directory** niet wordt weergegeven of is niet beschikbaar en wordt uitgelegd hoe tooproceed.</span><span class="sxs-lookup"><span data-stu-id="d2535-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="d2535-108">Active Directory ontbreekt</span><span class="sxs-lookup"><span data-stu-id="d2535-108">Active Directory is missing</span></span>
<span data-ttu-id="d2535-109">Normaal gesproken een **Active Directory** item wordt weergegeven in het linkerdeelvenster navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2535-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="d2535-110">Hallo-instructies in Azure Active Directory-procedures wordt ervan uitgegaan dat dit item in de weergave.</span><span class="sxs-lookup"><span data-stu-id="d2535-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Schermopname: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="d2535-112">Hallo Active Directory-item wordt weergegeven in het linkerdeelvenster navigatiemenu Hallo wanneer elk Hallo volgende voorwaarden is waar.</span><span class="sxs-lookup"><span data-stu-id="d2535-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="d2535-113">Anders weergegeven Hallo item niet.</span><span class="sxs-lookup"><span data-stu-id="d2535-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="d2535-114">Hallo huidige gebruiker is aangemeld met een Microsoft-account (voorheen bekend als een Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="d2535-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="d2535-115">OF</span><span class="sxs-lookup"><span data-stu-id="d2535-115">OR</span></span>
* <span data-ttu-id="d2535-116">Hello Azure-tenant heeft een map en Hallo huidige account is een directory-beheerder.</span><span class="sxs-lookup"><span data-stu-id="d2535-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="d2535-117">OF</span><span class="sxs-lookup"><span data-stu-id="d2535-117">OR</span></span>
* <span data-ttu-id="d2535-118">Hello Azure-tenant heeft ten minste één Azure AD Access Control (ACS)-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="d2535-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="d2535-119">Zie voor meer informatie [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2535-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="d2535-120">OF</span><span class="sxs-lookup"><span data-stu-id="d2535-120">OR</span></span>
* <span data-ttu-id="d2535-121">Hello Azure-tenant heeft ten minste één Azure multi-factor Authentication-provider.</span><span class="sxs-lookup"><span data-stu-id="d2535-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="d2535-122">Zie voor meer informatie [Azure multi-factor Authentication-Providers beheren](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="d2535-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="d2535-123">toocreate Access Control-naamruimte of een multi-Factor Authentication-provider, klikt u op **+ nieuw** > **App Services** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2535-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="d2535-124">tooget beheerdersrechten tooa directory, hebben een beheerder een beheerder rol tooyour account toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d2535-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="d2535-125">Zie voor meer informatie [beheerdersrollen toewijzen](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d2535-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="d2535-126">Active Directory is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="d2535-126">Active Directory is not available</span></span>
<span data-ttu-id="d2535-127">Wanneer u klikt op **+ nieuw** > **App Services**, een **Active Directory** item wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d2535-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="d2535-128">Hallo Active Directory-item wordt weergegeven in het bijzonder voor wanneer Hallo Active Directory-functies, zoals Directory, Access Control of multi-factor Authentication-Provider, de huidige gebruiker toohello beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="d2535-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="d2535-129">Echter tijdens het laden van pagina hello, Hallo item grijs wordt weergegeven en is gemarkeerd als **niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="d2535-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="d2535-130">Dit is een tijdelijke status.</span><span class="sxs-lookup"><span data-stu-id="d2535-130">This is a temporary state.</span></span> <span data-ttu-id="d2535-131">Als u een paar seconden wachten, beschikbaar Hallo item.</span><span class="sxs-lookup"><span data-stu-id="d2535-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="d2535-132">Als Hallo vertraging wordt verlengd, vernieuwen Hallo webpagina vaak probleem wordt opgelost Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2535-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Schermopname: Active Directory is niet beschikbaar](./media/active-directory-troubleshooting/not-available.png)

