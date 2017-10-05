---
title: Azure Active Directory hybride identiteit ontwerpoverwegingen - vereisten voor toegangsbeheer bepalen | Microsoft Docs
description: Bevat informatie over de stijlen van identiteit en het bepalen van de toegangsvereisten voor de bronnen voor gebruikers in een hybride omgeving.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="8d99c-103">Vereisten voor toegangsbeheer voor uw oplossing voor hybride identiteit bepalen</span><span class="sxs-lookup"><span data-stu-id="8d99c-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="8d99c-104">Wanneer een organisatie hun hybride identiteitsoplossing ontwerpt kunnen ze deze mogelijkheid ook gebruiken om te controleren van de toegangsvereisten voor de resources die ze willen beschikbaar maken voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8d99c-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="8d99c-105">De data access cross alle vier stijlen van identiteit, die zijn:</span><span class="sxs-lookup"><span data-stu-id="8d99c-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="8d99c-106">Beheer</span><span class="sxs-lookup"><span data-stu-id="8d99c-106">Administration</span></span>
* <span data-ttu-id="8d99c-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="8d99c-107">Authentication</span></span>
* <span data-ttu-id="8d99c-108">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="8d99c-108">Authorization</span></span>
* <span data-ttu-id="8d99c-109">Controleren</span><span class="sxs-lookup"><span data-stu-id="8d99c-109">Auditing</span></span>

<span data-ttu-id="8d99c-110">De volgende secties wordt uitgelegd, verificatie en autorisatie in meer details, beheer en controle deel uitmaken van de levenscyclus van hybride identiteit.</span><span class="sxs-lookup"><span data-stu-id="8d99c-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="8d99c-111">Lees [beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) voor meer informatie over deze mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8d99c-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="8d99c-112">Lees [de vier stijlen van identiteit - identiteitsbeheer in de leeftijd van hybride IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) voor meer informatie over elk van deze stijlen.</span><span class="sxs-lookup"><span data-stu-id="8d99c-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="8d99c-113">Verificatie en autorisatie</span><span class="sxs-lookup"><span data-stu-id="8d99c-113">Authentication and authorization</span></span>
<span data-ttu-id="8d99c-114">Er zijn verschillende scenario's voor verificatie en autorisatie, heeft deze scenario's de specifieke vereisten waaraan moeten worden voldaan door de oplossing voor hybride identiteiten die het bedrijf gaat hanteren.</span><span class="sxs-lookup"><span data-stu-id="8d99c-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="8d99c-115">Scenario's met betrekking tot communicatie voor bedrijven (B2B) kunnen een extra uitdaging voor IT-beheerders toevoegen, omdat ze ervoor zorgen moet dat de methode voor verificatie en autorisatie gebruikt door de organisatie met hun zakelijke partners communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="8d99c-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="8d99c-116">Zorg ervoor dat de volgende vragen worden beantwoord tijdens het ontwerpen van wordt voor verificatie en autorisatie-vereisten:</span><span class="sxs-lookup"><span data-stu-id="8d99c-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="8d99c-117">Wordt van uw organisatie verifiëren en autoriseren van alleen gebruikers die zich bevindt op hun identiteitsbeheersysteem?</span><span class="sxs-lookup"><span data-stu-id="8d99c-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="8d99c-118">Zijn er plannen voor B2B-scenario's?</span><span class="sxs-lookup"><span data-stu-id="8d99c-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="8d99c-119">Zo ja, u al weet welke protocollen (SAML, OAuth, Kerberos, Tokens of certificaten) wordt gebruikt voor het verbinden van beide bedrijven?</span><span class="sxs-lookup"><span data-stu-id="8d99c-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="8d99c-120">De oplossing voor hybride identiteiten die u wilt vaststellen ondersteuning die protocollen ondersteunt?</span><span class="sxs-lookup"><span data-stu-id="8d99c-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="8d99c-121">Een ander belangrijk punt in overweging moet nemen is waar de verificatie-opslagplaats die wordt gebruikt door gebruikers en partners zich bevindt en het beheermodel moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8d99c-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="8d99c-122">Houd rekening met de volgende twee belangrijkste opties:</span><span class="sxs-lookup"><span data-stu-id="8d99c-122">Consider the following two core options:</span></span>

* <span data-ttu-id="8d99c-123">Gecentraliseerd: in dit model van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8d99c-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="8d99c-124">Hybride: in dit model van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie en een gerepliceerde in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8d99c-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="8d99c-125">Welk model van uw organisatie invoert varieert volgens de vereisten van hun bedrijf, die u wilt de volgende vragen om aan te duiden waar de identiteitsbeheersysteem blijven staan en de beheerdersmodus te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d99c-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="8d99c-126">Beschikt uw organisatie momenteel over identity management lokale?</span><span class="sxs-lookup"><span data-stu-id="8d99c-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="8d99c-127">Zo ja, wilt ze houden?</span><span class="sxs-lookup"><span data-stu-id="8d99c-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="8d99c-128">Zijn er eventuele voorschriften of naleving vereisten die uw organisatie moet volgen die bepaald waarin de identiteitsbeheersysteem zich moet bevinden?</span><span class="sxs-lookup"><span data-stu-id="8d99c-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="8d99c-129">Uw organisatie gebruikt eenmalige aanmelding voor apps die zich on-premises of in de cloud?</span><span class="sxs-lookup"><span data-stu-id="8d99c-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="8d99c-130">Zo ja, de acceptatie van een model van hybride identiteit beïnvloedt dit proces?</span><span class="sxs-lookup"><span data-stu-id="8d99c-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="8d99c-131">Access Control</span><span class="sxs-lookup"><span data-stu-id="8d99c-131">Access Control</span></span>
<span data-ttu-id="8d99c-132">Hoewel verificatie en autorisatie core-elementen voor toegang tot zakelijke gegevens via de validatie van de gebruiker zijn, is het ook belangrijk om te bepalen het niveau van toegang dat deze gebruikers zijn en het niveau van toegangbeheerders hebben via de bronnen die ze beheert.</span><span class="sxs-lookup"><span data-stu-id="8d99c-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="8d99c-133">Uw oplossing voor hybride identiteit moet kunnen bieden gedetailleerde toegang tot bronnen, overdracht en role base access control.</span><span class="sxs-lookup"><span data-stu-id="8d99c-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="8d99c-134">Zorg ervoor dat de volgende vraag worden beantwoord met betrekking tot toegangsbeheer:</span><span class="sxs-lookup"><span data-stu-id="8d99c-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="8d99c-135">Heeft uw bedrijf meer dan één gebruiker met verhoogde bevoegdheden voor het beheren van identiteiten?</span><span class="sxs-lookup"><span data-stu-id="8d99c-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="8d99c-136">Zo ja, heeft elke gebruiker behoefte aan hetzelfde toegangsniveau?</span><span class="sxs-lookup"><span data-stu-id="8d99c-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="8d99c-137">Moet uw bedrijf toegang tot gebruikers voor het beheren van specifieke bronnen delegeren?</span><span class="sxs-lookup"><span data-stu-id="8d99c-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="8d99c-138">Zo ja, hoe vaak dit gebeurt?</span><span class="sxs-lookup"><span data-stu-id="8d99c-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="8d99c-139">Moet uw bedrijf access control-mogelijkheden tussen on-premises en cloud integreren bronnen?</span><span class="sxs-lookup"><span data-stu-id="8d99c-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="8d99c-140">Moet uw bedrijf te beperken van toegang tot bronnen op basis van een aantal voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="8d99c-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="8d99c-141">Moet uw bedrijf alle toepassingen die toegang tot bepaalde bronnen aangepast besturingselement nodig?</span><span class="sxs-lookup"><span data-stu-id="8d99c-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="8d99c-142">Zo ja, waarbij deze apps zich bevinden (lokaal of in de cloud)?</span><span class="sxs-lookup"><span data-stu-id="8d99c-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="8d99c-143">Zo ja, waar zijn die zijn gericht bronnen (lokaal of in de cloud)?</span><span class="sxs-lookup"><span data-stu-id="8d99c-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="8d99c-144">Zorg ervoor dat elk antwoord noteert de logica achter het antwoord begrijpt.</span><span class="sxs-lookup"><span data-stu-id="8d99c-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="8d99c-145">[Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties en de voor-en nadelen van elke optie.</span><span class="sxs-lookup"><span data-stu-id="8d99c-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="8d99c-146">Door deze vragen te beantwoorden wordt u selecteren welke optie het beste aansluit op uw bedrijfsbehoeften.</span><span class="sxs-lookup"><span data-stu-id="8d99c-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8d99c-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d99c-147">Next steps</span></span>
[<span data-ttu-id="8d99c-148">Vereisten voor respons op incidenten bepalen</span><span class="sxs-lookup"><span data-stu-id="8d99c-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="8d99c-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8d99c-149">See Also</span></span>
[<span data-ttu-id="8d99c-150">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="8d99c-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

