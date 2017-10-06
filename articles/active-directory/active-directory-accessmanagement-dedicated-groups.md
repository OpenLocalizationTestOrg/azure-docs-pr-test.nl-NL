---
title: aaaDedicated groepen in Azure Active Directory | Microsoft Docs
description: Overzicht van hoe toegewezen groepen werken in Azure Active Directory en hoe ze worden gemaakt.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="06d90-103">Toegewezen groepen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06d90-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="06d90-104">In Azure Active Directory (Azure AD), Hallo toegewezen groepsfunctie automatisch maakt en vult lidmaatschap voor groepen van Azure AD zijn vooraf gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="06d90-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="06d90-105">Leden van specifieke groepen kunnen niet worden toegevoegd of verwijderd met behulp van hello Azure classic portal Windows PowerShell-cmdlets of via een programma.</span><span class="sxs-lookup"><span data-stu-id="06d90-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="06d90-106">Toegewezen groepen moeten een Azure AD Premium-licentie is toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="06d90-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="06d90-107">Hallo beheerder van Hallo-regel voor een groep</span><span class="sxs-lookup"><span data-stu-id="06d90-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="06d90-108">alle gebruikers die zijn geselecteerd door Hallo toobe lid van groep Hallo regel</span><span class="sxs-lookup"><span data-stu-id="06d90-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="06d90-109">**tooenable toegewezen groepen**</span><span class="sxs-lookup"><span data-stu-id="06d90-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="06d90-110">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="06d90-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="06d90-111">Selecteer Hallo **groepen** tabblad en open vervolgens Hallo groep die u tooedit.</span><span class="sxs-lookup"><span data-stu-id="06d90-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="06d90-112">Selecteer Hallo **configureren** tabblad en stel vervolgens **toegewezen groepen inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="06d90-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="06d90-113">Zodra Hallo toegewezen groepen inschakelen switch te is ingesteld**Ja**, kunt u verder inschakelen Hallo directory tooautomatically Hallo alle gebruikers toegewezen groep maken door de instelling Hallo **inschakelen 'Alle gebruikers' groep** switch te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="06d90-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="06d90-114">Ook kunt u vervolgens bewerken Hallo-naam van deze groep toegewezen door deze te typen in Hallo **weergavenaam voor 'Alle gebruikers' groep** veld.</span><span class="sxs-lookup"><span data-stu-id="06d90-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="06d90-115">de groep alle gebruikers Hallo kan worden gebruikt tooassign Hallo dezelfde machtigingen tooall Hallo gebruikers in uw directory.</span><span class="sxs-lookup"><span data-stu-id="06d90-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="06d90-116">U kunt bijvoorbeeld alle gebruikers in uw directory toegang tooa SaaS-toepassing door het toewijzen van toegang voor alle gebruikers gespecialiseerde groep toothis toepassing hello verlenen.</span><span class="sxs-lookup"><span data-stu-id="06d90-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="06d90-117">Hallo toegewezen alle gebruikers groep bevat alle gebruikers in de directory hello, inclusief gasten en externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="06d90-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="06d90-118">Als u een groep moet op die externe gebruikers worden uitgesloten en u kunt dit doen door het maken van een groep met een kenmerk op basis van een dynamische regel zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="06d90-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="06d90-119">Voor een groep die omvat niet alle gasten, moet u een regel zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="06d90-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="06d90-120">toolearn over het toocreate *geavanceerde* regels (regels met meerdere vergelijkingen) voor dynamisch groepslidmaatschap, Zie [met behulp van kenmerken toocreate geavanceerde regels](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="06d90-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="06d90-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06d90-121">Next steps</span></span>
<span data-ttu-id="06d90-122">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06d90-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="06d90-123">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="06d90-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* <span data-ttu-id="06d90-124">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="06d90-124">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="06d90-125">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="06d90-125">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="06d90-126">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06d90-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
