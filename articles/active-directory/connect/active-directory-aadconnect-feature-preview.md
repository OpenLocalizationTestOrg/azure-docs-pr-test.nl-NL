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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="9bf87-103">Meer informatie over functies in preview</span><span class="sxs-lookup"><span data-stu-id="9bf87-103">More details about features in preview</span></span>
<span data-ttu-id="9bf87-104">Dit onderwerp wordt beschreven hoe u functies die momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="9bf87-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="9bf87-105">Groep terugschrijven</span><span class="sxs-lookup"><span data-stu-id="9bf87-105">Group writeback</span></span>
<span data-ttu-id="9bf87-106">De optie voor write-back van groep in optionele functies kunt u Write-back van **Office 365-groepen** naar een forest met Exchange geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9bf87-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="9bf87-107">Dit is een groep die altijd is gemaakt in de cloud.</span><span class="sxs-lookup"><span data-stu-id="9bf87-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="9bf87-108">Als u Exchange lokale hebt, kunt klikt u vervolgens u schrijven terug deze groepen met on-premises zodat gebruikers met een lokale Exchange-postvak kunnen verzenden en ontvangen van e-mailberichten van deze groepen.</span><span class="sxs-lookup"><span data-stu-id="9bf87-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="9bf87-109">Meer informatie over Office 365-groepen en het gebruik ervan vindt [hier](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="9bf87-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="9bf87-110">Een Office 365-groep wordt weergegeven als een distributiegroep op on-premises AD DS.</span><span class="sxs-lookup"><span data-stu-id="9bf87-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="9bf87-111">Uw lokale Exchange-server moet zich op Exchange 2013 cumulatieve update 8 (uitgebracht in maart 2015) of Exchange 2016 dit nieuwe groepstype kan herkennen.</span><span class="sxs-lookup"><span data-stu-id="9bf87-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="9bf87-112">**Opmerkingen bij de tijdens de preview**</span><span class="sxs-lookup"><span data-stu-id="9bf87-112">**Notes during the preview**</span></span>

* <span data-ttu-id="9bf87-113">Het kenmerk van het adresboek adres momenteel niet is ingevuld in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9bf87-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="9bf87-114">De groep is niet zichtbaar in de algemene Adreslijst zonder dit kenmerk.</span><span class="sxs-lookup"><span data-stu-id="9bf87-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="9bf87-115">De eenvoudigste manier om het vullen van dit kenmerk is met de Exchange-PowerShell-cmdlet `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="9bf87-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="9bf87-116">Alleen-forests met het Exchange-schema zijn geldige doelen voor groepen.</span><span class="sxs-lookup"><span data-stu-id="9bf87-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="9bf87-117">Als er geen Exchange is gedetecteerd, vervolgens is Write-back van groep niet mogelijk om in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="9bf87-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="9bf87-118">Alleen één forest Exchange organisatie implementaties worden momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9bf87-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="9bf87-119">Als u meer dan één Exchange organisatie lokale hebt, moet u een on-premises GALSync oplossing voor deze groepen worden weergegeven in de andere forests.</span><span class="sxs-lookup"><span data-stu-id="9bf87-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="9bf87-120">Het onderdeel van de Write-back van groep verwerkt beveiligingsgroepen of distributiegroepen niet.</span><span class="sxs-lookup"><span data-stu-id="9bf87-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="9bf87-121">Een abonnement op Azure AD Premium is vereist voor write-back van groep.</span><span class="sxs-lookup"><span data-stu-id="9bf87-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="9bf87-122">Write-back van gebruiker</span><span class="sxs-lookup"><span data-stu-id="9bf87-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9bf87-123">De gebruiker terugschrijven preview-functie is verwijderd in de update augustus 2015 naar Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9bf87-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="9bf87-124">Als u deze hebt ingeschakeld, moet u deze functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="9bf87-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9bf87-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bf87-125">Next steps</span></span>
<span data-ttu-id="9bf87-126">Blijven uw [aangepaste installatie van Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9bf87-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="9bf87-127">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9bf87-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
