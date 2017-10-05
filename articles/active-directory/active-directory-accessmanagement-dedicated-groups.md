---
title: Toegewezen groepen in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="7e332-103">Toegewezen groepen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e332-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="7e332-104">In Azure Active Directory (Azure AD), de functie toegewezen groepen maakt en automatisch gevuld lidmaatschap voor groepen van Azure AD zijn vooraf gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="7e332-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="7e332-105">Leden van specifieke groepen kan niet worden toegevoegd of verwijderd met behulp van de klassieke Azure-portal, de Windows PowerShell-cmdlets of via een programma.</span><span class="sxs-lookup"><span data-stu-id="7e332-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="7e332-106">Toegewezen groepen moeten een Azure AD Premium-licentie is toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="7e332-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="7e332-107">De beheerder van de regel voor een groep</span><span class="sxs-lookup"><span data-stu-id="7e332-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="7e332-108">alle gebruikers die zijn geselecteerd door de regel moet lid zijn van de groep</span><span class="sxs-lookup"><span data-stu-id="7e332-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="7e332-109">**Toegewezen groepen inschakelen**</span><span class="sxs-lookup"><span data-stu-id="7e332-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="7e332-110">In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="7e332-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="7e332-111">Selecteer de **groepen** tabblad en open vervolgens de groep die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="7e332-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="7e332-112">Selecteer de **configureren** tabblad en stel vervolgens **toegewezen groepen inschakelen** naar **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7e332-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="7e332-113">Zodra de switch toegewezen groepen inschakelen is ingesteld op **Ja**, verder kunt u de map voor het automatisch maken van de speciale groep alle gebruikers door in te stellen de **inschakelen 'Alle gebruikers' groep** overschakelen naar  **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7e332-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="7e332-114">U kunt vervolgens ook bewerken de naam van deze groep toegewezen door te typen in de **weergavenaam voor 'Alle gebruikers' groep** veld.</span><span class="sxs-lookup"><span data-stu-id="7e332-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="7e332-115">De groep alle gebruikers kan worden gebruikt dezelfde machtigingen toewijzen aan alle gebruikers in uw directory.</span><span class="sxs-lookup"><span data-stu-id="7e332-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="7e332-116">Bijvoorbeeld, kunt u alle gebruikers in uw directory toegang tot een SaaS-toepassing verlenen toegang voor de speciale groep alle gebruikers toewijzen aan deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e332-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="7e332-117">De speciale groep alle gebruikers bevat alle gebruikers in de directory, inclusief gasten en externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7e332-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="7e332-118">Als u een groep moet op die externe gebruikers worden uitgesloten en u kunt dit doen door het maken van een groep met een kenmerk op basis van een dynamische regel zoals de volgende:</span><span class="sxs-lookup"><span data-stu-id="7e332-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="7e332-119">Voor een groep die omvat niet alle gasten, gebruikt u een regel, zoals de volgende:</span><span class="sxs-lookup"><span data-stu-id="7e332-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="7e332-120">Zie [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md) (Engelstalig) voor meer informatie over het maken van *geavanceerde* regels (regels met meerdere vergelijkingen).</span><span class="sxs-lookup"><span data-stu-id="7e332-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="7e332-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e332-121">Next steps</span></span>
<span data-ttu-id="7e332-122">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e332-122">These articles provide additional information on Azure Active Directory.</span></span>

* <span data-ttu-id="7e332-123">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="7e332-123">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* <span data-ttu-id="7e332-124">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="7e332-124">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="7e332-125">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="7e332-125">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="7e332-126">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e332-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
