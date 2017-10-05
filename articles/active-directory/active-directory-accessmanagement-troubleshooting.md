---
title: Het oplossen van problemen dynamisch lidmaatschap voor groepen | Microsoft Docs
description: Tips voor probleemoplossing voor dynamisch lidmaatschap voor groepen in Azure AD.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="bb4fe-103">Oplossen van problemen met dynamische lidmaatschappen voor groepen</span><span class="sxs-lookup"><span data-stu-id="bb4fe-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="bb4fe-104">**Ik een regel voor een groep hebt geconfigureerd, maar geen lidmaatschappen worden bijgewerkt in de groep**</span><span class="sxs-lookup"><span data-stu-id="bb4fe-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="bb4fe-105">Controleer de **inschakelen gedelegeerd groepsbeheer** is ingesteld op **Ja** in de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="bb4fe-106">U ziet deze instelling alleen als u bent aangemeld als een gebruiker aan wie een Azure Active Directory Premium-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="bb4fe-107">Controleer de waarden voor kenmerken van de gebruiker op de regel: Er zijn van gebruikers die voldoen aan de regel?</span><span class="sxs-lookup"><span data-stu-id="bb4fe-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="bb4fe-108">**Ik een regel hebt geconfigureerd, maar nu de bestaande leden van de regel zijn verwijderd**</span><span class="sxs-lookup"><span data-stu-id="bb4fe-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="bb4fe-109">Dit is verwacht gedrag.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-109">This is expected behavior.</span></span> <span data-ttu-id="bb4fe-110">Bestaande leden van de groep worden verwijderd wanneer een regel is ingeschakeld of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="bb4fe-111">De gebruikers van de evaluatieversie van de regel wordt geretourneerd worden als leden toegevoegd aan de groep.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="bb4fe-112">**Ik zie niet met het lidmaatschap wordt gewijzigd direct als ik toevoegen of wijzigen van een regel, waarom niet?**</span><span class="sxs-lookup"><span data-stu-id="bb4fe-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="bb4fe-113">Evaluatie toegewezen lidmaatschap wordt periodiek uitgevoerd in een asynchrone achtergrondproces.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="bb4fe-114">Hoe lang duurt het proces wordt bepaald door het aantal gebruikers in uw directory en de grootte van de groep gemaakt als gevolg van de regel.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="bb4fe-115">Mappen met een klein aantal gebruikers ziet normaal gesproken de wijzigingen voor een groepslidmaatschap in minder dan een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="bb4fe-116">Mappen met een groot aantal gebruikers kunnen duren voordat de 30 minuten of langer te vullen.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="bb4fe-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb4fe-117">Next steps</span></span>
<span data-ttu-id="bb4fe-118">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bb4fe-118">These articles provide additional information on Azure Active Directory.</span></span>

* <span data-ttu-id="bb4fe-119">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="bb4fe-119">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* <span data-ttu-id="bb4fe-120">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="bb4fe-120">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="bb4fe-121">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="bb4fe-121">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="bb4fe-122">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb4fe-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
