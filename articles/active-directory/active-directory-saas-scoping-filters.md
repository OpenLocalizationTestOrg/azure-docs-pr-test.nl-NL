---
title: apps met bereikfilters aaaProvisioning | Microsoft Docs
description: Meer informatie over hoe toouse scoping filtert tooprevent objecten in apps die ondersteuning bieden voor geautomatiseerde gebruikersinrichting van daadwerkelijk wordt ingericht als een object niet voldoet aan uw zakelijke vereisten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="3a7ca-103">Inrichten van toepassing op basis van kenmerken met bereikfilters</span><span class="sxs-lookup"><span data-stu-id="3a7ca-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="3a7ca-104">Hallo-doel van deze sectie is tooexplain hoe toouse scoping filtert toodefine op kenmerken gebaseerde regels die bepalen welke gebruikers zijn ingericht toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="3a7ca-105">Componenten en Scope-groepen</span><span class="sxs-lookup"><span data-stu-id="3a7ca-105">Clauses and Scope Groups</span></span>
![Bereikfilter][1] 

<span data-ttu-id="3a7ca-107">Bereik filters zijn gedefinieerd door een of meer **bereik groepen**, elk van die een of meer houdt **componenten**.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="3a7ca-108">toosee hello componenten voor een bepaald bereik-groep, weer door te klikken op Hallo pijl toohello links van de groepsnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="3a7ca-109">Een **component** bepaalt welke gebruikers de mogelijkheid toopass via Hallo bereikfilter door elke gebruiker kenmerken te evalueren.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="3a7ca-110">Bijvoorbeeld, wellicht u een component die dat vereist een gebruiker 'status'-kenmerk gelijk New York, zodat alleen Den Haag gebruikers zijn ingericht in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![De naam van bereik][2] 

<span data-ttu-id="3a7ca-112">Elke **bereikgroep** begint met een verplichte **component**, zoals weergegeven in de bovenstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="3a7ca-113">Deze component gewoon aangegeven dat die Hallo-gebruiker moet eerst worden toegewezen toohello toepassing voordat dit wordt geëvalueerd door uw bereik filters.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="3a7ca-114">Deze component kan niet worden verwijderd of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="3a7ca-115">U kunt nieuwe componenten of nieuwe scope groepen toevoegen door de juiste knop hello te drukken.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="3a7ca-116">U kunt elke scope-groep een naam geven door het bewerken van de **groep scopenaam** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="3a7ca-117">Hoe Scoping Filters worden geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="3a7ca-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="3a7ca-118">Tijdens het inrichten testen we elke toegewezen gebruiker op basis van uw bereik filters toodetermine als die gebruiker toegang toohello toepassing verdient.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="3a7ca-119">U kunt zien van elk component als een test die moet worden doorgegeven om Hallo gebruiker tooavoid ophalen uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="3a7ca-120">Als er meerdere scope-groepen gedefinieerd, moet elke gebruiker doorgeven ten minste één van deze tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="3a7ca-121">In elke bereikgroep echter Hallo gebruiker moet doorgeven elke toopass component die bepaalde scope-groep.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="3a7ca-122">Met andere woorden, u kunt zien van bereikgroepen als of gekoppeld en u kunt zien Hallo componenten binnen deze als en gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="3a7ca-123">Denk bijvoorbeeld Hallo bereikfilter hieronder:</span><span class="sxs-lookup"><span data-stu-id="3a7ca-123">For example, consider hello scoping filter below:</span></span>

![De naam van bereik][3]  

<span data-ttu-id="3a7ca-125">Volgens toothis bereikfilter, gebruikers moeten voldoen aan de volgende Hallo criteria, toobe ingericht:</span><span class="sxs-lookup"><span data-stu-id="3a7ca-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="3a7ca-126">Ze moeten toohello toepassing worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="3a7ca-127">Moet worden gebruikt in Hallo Engineering-afdeling</span><span class="sxs-lookup"><span data-stu-id="3a7ca-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="3a7ca-128">Werk moeten echter in San Francisco of Canada.</span><span class="sxs-lookup"><span data-stu-id="3a7ca-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="3a7ca-129">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="3a7ca-129">Related Articles</span></span>
* <span data-ttu-id="3a7ca-130">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="3a7ca-130">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="3a7ca-131">Gebruikers inrichten en Deprovisioning tooSaaS toepassingen automatiseren</span><span class="sxs-lookup"><span data-stu-id="3a7ca-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="3a7ca-132">Kenmerktoewijzingen voor gebruikers inrichten aanpassen</span><span class="sxs-lookup"><span data-stu-id="3a7ca-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="3a7ca-133">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="3a7ca-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="3a7ca-134">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="3a7ca-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="3a7ca-135">Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications</span><span class="sxs-lookup"><span data-stu-id="3a7ca-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="3a7ca-136">Lijst met zelfstudies over het tooIntegrate SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="3a7ca-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
