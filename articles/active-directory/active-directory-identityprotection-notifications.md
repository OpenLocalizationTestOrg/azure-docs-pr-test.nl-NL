---
title: 'Active Directory: Identity Protection-meldingen aaaAzure | Microsoft Docs'
description: Meer informatie over hoe de onderzoeksactiviteiten van uw ondersteuning bieden voor meldingen.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="c174c-104">Azure Active Directory: Identity Protection-meldingen</span><span class="sxs-lookup"><span data-stu-id="c174c-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="c174c-105">Azure AD Identity Protection verzendt twee soorten geautomatiseerde meldingen e-mails toohelp die u beheert gebruiker risico en risico's:</span><span class="sxs-lookup"><span data-stu-id="c174c-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="c174c-106">Gebruiker e-mailwaarschuwingen geknoeid</span><span class="sxs-lookup"><span data-stu-id="c174c-106">User compromised alert email</span></span>
* <span data-ttu-id="c174c-107">Wekelijks overzicht via e-mail</span><span class="sxs-lookup"><span data-stu-id="c174c-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="c174c-108">Gebruiker e-mailwaarschuwingen geknoeid</span><span class="sxs-lookup"><span data-stu-id="c174c-108">User compromised alert email</span></span>
<span data-ttu-id="c174c-109">Een gebruiker verdachte e-mailmelding wordt gegenereerd wanneer een account van Azure AD Identity Protection wordt aangemerkt als geknoeid.</span><span class="sxs-lookup"><span data-stu-id="c174c-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="c174c-110">Hallo e-mailbericht bevat een koppeling toohello gebruikers die zijn gemarkeerd voor risico rapport in Hallo Identity Protection-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c174c-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="c174c-111">Het is raadzaam dat u onmiddellijk meldingen van accounts waarmee is geknoeid onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="c174c-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="c174c-112">Wekelijks overzicht via e-mail</span><span class="sxs-lookup"><span data-stu-id="c174c-112">Weekly digest email</span></span>
<span data-ttu-id="c174c-113">Hallo wekelijkse digest e-mailbericht bevat een overzicht van nieuwe risico's.</span><span class="sxs-lookup"><span data-stu-id="c174c-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="c174c-114">Het bevat:</span><span class="sxs-lookup"><span data-stu-id="c174c-114">It includes:</span></span>

* <span data-ttu-id="c174c-115">Gebruikers die risico lopen</span><span class="sxs-lookup"><span data-stu-id="c174c-115">Users at risk</span></span>
* <span data-ttu-id="c174c-116">Verdachte activiteiten</span><span class="sxs-lookup"><span data-stu-id="c174c-116">Suspicious activities</span></span>
* <span data-ttu-id="c174c-117">Gedetecteerde kwetsbaarheden</span><span class="sxs-lookup"><span data-stu-id="c174c-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="c174c-118">Koppelingen toohello gerelateerde rapporten in Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c174c-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="c174c-119">
![Herstel](./media/active-directory-identityprotection-notifications/400.png "herstel")
</span><span class="sxs-lookup"><span data-stu-id="c174c-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="c174c-120">U kunt overschakelen verzenden van wekelijkse Verificatiesamenvatting uit.</span><span class="sxs-lookup"><span data-stu-id="c174c-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="c174c-121">
![Gebruiker risico's](./media/active-directory-identityprotection-notifications/62.png "gebruiker risico's")
</span><span class="sxs-lookup"><span data-stu-id="c174c-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="c174c-122">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="c174c-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="c174c-123">Op Hallo **Azure AD Identity Protection** blade, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="c174c-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="c174c-124">
   ![Gebruikersbeleid risico](./media/active-directory-identityprotection-notifications/401.png "risico gebruikersbeleid")
   </span><span class="sxs-lookup"><span data-stu-id="c174c-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="c174c-125">In Hallo **algemene** sectie, klikt u op **meldingen**.</span><span class="sxs-lookup"><span data-stu-id="c174c-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="c174c-126">
   ![Gebruikersbeleid risico](./media/active-directory-identityprotection-notifications/405.png "risico gebruikersbeleid")
   </span><span class="sxs-lookup"><span data-stu-id="c174c-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="c174c-127">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c174c-127">See also</span></span>
* [<span data-ttu-id="c174c-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c174c-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
