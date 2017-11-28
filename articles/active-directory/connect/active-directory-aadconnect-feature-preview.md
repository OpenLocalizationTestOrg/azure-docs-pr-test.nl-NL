---
title: 'Azure AD Connect: Functies in preview | Microsoft Docs'
description: Dit onderwerp wordt beschreven in meer detail-onderdelen in het voorbeeld in Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="c1382-103">Meer informatie over functies in preview</span><span class="sxs-lookup"><span data-stu-id="c1382-103">More details about features in preview</span></span>
<span data-ttu-id="c1382-104">Dit onderwerp wordt beschreven hoe toouse functies die momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="c1382-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="c1382-105">Groep terugschrijven</span><span class="sxs-lookup"><span data-stu-id="c1382-105">Group writeback</span></span>
<span data-ttu-id="c1382-106">Hallo-optie voor write-back van groep in optionele functies kunt u toowriteback **Office 365-groepen** tooa forest met Exchange geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c1382-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="c1382-107">Dit is een groep die altijd in de cloud Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1382-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="c1382-108">Als u Exchange lokale hebt, kunt klikt u vervolgens u schrijven terug deze groepen tooon-premises zodat gebruikers met een lokale Exchange-postvak kunnen verzenden en ontvangen van e-mailberichten van deze groepen.</span><span class="sxs-lookup"><span data-stu-id="c1382-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="c1382-109">Meer informatie over Office 365-groepen en hoe toouse ze kunnen worden gevonden [hier](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="c1382-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="c1382-110">Een Office 365-groep wordt weergegeven als een distributiegroep op on-premises AD DS.</span><span class="sxs-lookup"><span data-stu-id="c1382-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="c1382-111">Uw lokale Exchange-server moet zich op Exchange 2013 cumulatieve update 8 (uitgebracht in maart 2015) of Exchange 2016 toorecognize dit nieuwe groepstype.</span><span class="sxs-lookup"><span data-stu-id="c1382-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="c1382-112">**Opmerkingen bij de tijdens Hallo preview**</span><span class="sxs-lookup"><span data-stu-id="c1382-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="c1382-113">Hallo-book mailadreskenmerk momenteel niet is ingevuld in Hallo preview.</span><span class="sxs-lookup"><span data-stu-id="c1382-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="c1382-114">Hallo groep is niet zichtbaar in Hallo GAL zonder dit kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1382-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="c1382-115">Hallo gemakkelijkste manier toopopulate dit kenmerk is toouse Hallo Exchange PowerShell-cmdlet `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="c1382-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="c1382-116">Alleen-forests met Hallo Exchange schema zijn geldige doelen voor groepen.</span><span class="sxs-lookup"><span data-stu-id="c1382-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="c1382-117">Er zijn geen Exchange is gedetecteerd, vervolgens is Write-back van groep niet als mogelijke tooenable.</span><span class="sxs-lookup"><span data-stu-id="c1382-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="c1382-118">Alleen één forest Exchange organisatie implementaties worden momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c1382-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="c1382-119">Als u meer dan één Exchange organisatie lokale hebt, moet u een on-premises GALSync oplossing voor deze tooappear groepen in uw andere forests.</span><span class="sxs-lookup"><span data-stu-id="c1382-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="c1382-120">beveiligingsgroepen of distributiegroepen verwerkt Hallo groep Write-back-functie niet.</span><span class="sxs-lookup"><span data-stu-id="c1382-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="c1382-121">Een abonnement tooAzure AD Premium is vereist voor write-back van groep.</span><span class="sxs-lookup"><span data-stu-id="c1382-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="c1382-122">Write-back van gebruiker</span><span class="sxs-lookup"><span data-stu-id="c1382-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c1382-123">Hallo gebruiker terugschrijven preview-functie in was verwijderd Hallo augustus 2015 update tooAzure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c1382-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="c1382-124">Als u deze hebt ingeschakeld, moet u deze functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c1382-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c1382-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1382-125">Next steps</span></span>
<span data-ttu-id="c1382-126">Blijven uw [aangepaste installatie van Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c1382-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="c1382-127">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c1382-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
