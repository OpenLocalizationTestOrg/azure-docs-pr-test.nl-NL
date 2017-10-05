---
title: Inrichting van apps met bereikfilters | Microsoft Docs
description: Informatie over het bereik filters gebruiken om te voorkomen dat de objecten in apps die ondersteuning bieden voor geautomatiseerde gebruikersinrichting van daadwerkelijk wordt ingericht als een object niet voldoet aan uw zakelijke vereisten.
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="0b0cf-103">Inrichten van toepassing op basis van kenmerken met bereikfilters</span><span class="sxs-lookup"><span data-stu-id="0b0cf-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="0b0cf-104">Het doel van deze sectie is wordt uitgelegd hoe u bereik filters gebruiken om te bepalen op kenmerken gebaseerde regels die bepalen welke gebruikers zijn ingericht voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="0b0cf-105">Componenten en Scope-groepen</span><span class="sxs-lookup"><span data-stu-id="0b0cf-105">Clauses and Scope Groups</span></span>
![Bereikfilter][1] 

<span data-ttu-id="0b0cf-107">Bereik filters zijn gedefinieerd door een of meer **bereik groepen**, elk van die een of meer houdt **componenten**.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="0b0cf-108">Overzicht van de componenten voor een bepaald bereik-groep, kunt u het uitbreiden door te klikken op de pijl naar links van de groepsnaam.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="0b0cf-109">Een **component** bepaalt welke gebruikers kunnen het bereik filter doorgeven door elke gebruiker kenmerken te evalueren.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="0b0cf-110">U wellicht bijvoorbeeld één component die vereist dat een gebruikerskenmerk 'status' gelijk zijn aan New York, zodat alleen Den Haag gebruikers zijn ingericht in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![De naam van bereik][2] 

<span data-ttu-id="0b0cf-112">Elke **bereikgroep** begint met een verplichte **component**, zoals wordt weergegeven in de bovenstaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="0b0cf-113">Deze component gewoon wordt aangegeven dat de gebruiker moet eerst worden toegewezen aan de toepassing voordat dit wordt geëvalueerd door uw bereik filters.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="0b0cf-114">Deze component kan niet worden verwijderd of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="0b0cf-115">U kunt nieuwe componenten of nieuwe scope groepen toevoegen door de juiste knop te drukken.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="0b0cf-116">U kunt elke scope-groep een naam geven door het bewerken van de **groep scopenaam** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="0b0cf-117">Hoe Scoping Filters worden geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="0b0cf-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="0b0cf-118">Tijdens het inrichten test u elke toegewezen gebruiker tegen bereik filters om te bepalen als die gebruiker toegang tot de toepassing verdient.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="0b0cf-119">U kunt zien van elk component als een test die moet worden doorgegeven in volgorde van de gebruiker om te voorkomen dat ophalen uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="0b0cf-120">Als er meerdere scope-groepen gedefinieerd, moet elke gebruiker ten minste één van ze toegang krijgen tot de toepassing doorgeven.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="0b0cf-121">In elke bereikgroep echter de gebruiker moet doorgeven elke component doorgeven die bepaalde scope-groep.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="0b0cf-122">Met andere woorden, u kunt zien van bereikgroepen als of gekoppeld en u kunt zien van de componenten binnen deze als en gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="0b0cf-123">Neem bijvoorbeeld het volgende bereik filter:</span><span class="sxs-lookup"><span data-stu-id="0b0cf-123">For example, consider the scoping filter below:</span></span>

![De naam van bereik][3]  

<span data-ttu-id="0b0cf-125">Gebruikers moeten voldoen aan de volgende criteria, moeten worden ingericht volgens dit bereik filter:</span><span class="sxs-lookup"><span data-stu-id="0b0cf-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="0b0cf-126">Ze moeten worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="0b0cf-127">Moet worden gebruikt in de afdeling Engineering</span><span class="sxs-lookup"><span data-stu-id="0b0cf-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="0b0cf-128">Werk moeten echter in San Francisco of Canada.</span><span class="sxs-lookup"><span data-stu-id="0b0cf-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="0b0cf-129">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="0b0cf-129">Related Articles</span></span>
* <span data-ttu-id="0b0cf-130">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0b0cf-130">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="0b0cf-131">Automatisch gebruikers inrichten en opheffen van inrichting tot SaaS-toepassingen</span><span class="sxs-lookup"><span data-stu-id="0b0cf-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="0b0cf-132">Kenmerktoewijzingen voor gebruikers inrichten aanpassen</span><span class="sxs-lookup"><span data-stu-id="0b0cf-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="0b0cf-133">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="0b0cf-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="0b0cf-134">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="0b0cf-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* <span data-ttu-id="0b0cf-135">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md) (SCIM gebruiken om in te stellen dat gebruikers en groepen van Azure Active Directory automatisch worden ingericht voor toepassingen)</span><span class="sxs-lookup"><span data-stu-id="0b0cf-135">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md)</span></span>
* [<span data-ttu-id="0b0cf-136">Lijst met zelfstudies over het integreren van SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="0b0cf-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
