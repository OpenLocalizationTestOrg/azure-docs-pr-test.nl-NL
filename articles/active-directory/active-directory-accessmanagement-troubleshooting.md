---
title: aaaTroubleshooting dynamisch lidmaatschap voor groepen | Microsoft Docs
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="2dd01-103">Oplossen van problemen met dynamische lidmaatschappen voor groepen</span><span class="sxs-lookup"><span data-stu-id="2dd01-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="2dd01-104">**Ik een regel voor een groep hebt geconfigureerd, maar geen lidmaatschappen worden bijgewerkt in de groep Hallo**</span><span class="sxs-lookup"><span data-stu-id="2dd01-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="2dd01-105">Controleer of deze Hallo **inschakelen gedelegeerd groepsbeheer** ingesteld te**Ja** in Hallo **configureren** tabblad. U ziet deze instelling alleen als u bent aangemeld als een gebruiker toowhom een Azure Active Directory Premium-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="2dd01-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="2dd01-106">Controleer Hallo waarden voor kenmerken van de gebruiker op Hallo regel: Er zijn van gebruikers die voldoen aan de regel Hallo?</span><span class="sxs-lookup"><span data-stu-id="2dd01-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="2dd01-107">**Ik een regel hebt geconfigureerd, maar nu Hallo bestaande leden van de regel Hallo zijn verwijderd**</span><span class="sxs-lookup"><span data-stu-id="2dd01-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="2dd01-108">Dit is verwacht gedrag.</span><span class="sxs-lookup"><span data-stu-id="2dd01-108">This is expected behavior.</span></span> <span data-ttu-id="2dd01-109">Bestaande leden van Hallo groep worden verwijderd wanneer een regel is ingeschakeld of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2dd01-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="2dd01-110">Hallo-gebruikers heeft geretourneerd van de evaluatieversie van Hallo regel worden toegevoegd als leden toohello groep.</span><span class="sxs-lookup"><span data-stu-id="2dd01-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="2dd01-111">**Ik zie niet met het lidmaatschap wordt gewijzigd direct als ik toevoegen of wijzigen van een regel, waarom niet?**</span><span class="sxs-lookup"><span data-stu-id="2dd01-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="2dd01-112">Evaluatie toegewezen lidmaatschap wordt periodiek uitgevoerd in een asynchrone achtergrondproces.</span><span class="sxs-lookup"><span data-stu-id="2dd01-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="2dd01-113">Hoe lang Hallo proces duurt is afhankelijk van Hallo aantal gebruikers in uw directory en Hallo grootte van Hallo-groep gemaakt naar aanleiding van Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="2dd01-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="2dd01-114">Mappen met een klein aantal gebruikers ziet doorgaans wijzigingen voor een groepslidmaatschap Hallo in minder dan een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="2dd01-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="2dd01-115">Mappen met een groot aantal gebruikers duurt 30 minuten of langer toopopulate.</span><span class="sxs-lookup"><span data-stu-id="2dd01-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="2dd01-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2dd01-116">Next steps</span></span>
<span data-ttu-id="2dd01-117">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2dd01-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="2dd01-118">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="2dd01-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* <span data-ttu-id="2dd01-119">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="2dd01-119">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="2dd01-120">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="2dd01-120">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="2dd01-121">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dd01-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
