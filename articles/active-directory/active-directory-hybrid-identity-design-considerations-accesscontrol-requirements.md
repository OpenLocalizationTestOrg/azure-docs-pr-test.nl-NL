---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - vereisten voor toegangsbeheer bepalen | Microsoft Docs
description: Dekt Hallo stijlen van identiteit en identificerende toegangsvereisten voor de bronnen voor gebruikers in een hybride omgeving.
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
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="290e6-103">Vereisten voor toegangsbeheer voor uw oplossing voor hybride identiteit bepalen</span><span class="sxs-lookup"><span data-stu-id="290e6-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="290e6-104">Bij het ontwerpen van een organisatie hun hybride identiteitsoplossing ze kunnen ook gebruiken met deze mogelijkheid tooreview vereisten voor Hallo resources dat zij toomake plannen toegang krijgen tot deze beschikbaar voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="290e6-104">When an organization is designing their hybrid identity solution they can also use this opportunity tooreview access requirements for hello resources that they are planning toomake it available for users.</span></span> <span data-ttu-id="290e6-105">Hallo gegevenstoegang cross alle vier stijlen van identiteit, die zijn:</span><span class="sxs-lookup"><span data-stu-id="290e6-105">hello data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="290e6-106">Beheer</span><span class="sxs-lookup"><span data-stu-id="290e6-106">Administration</span></span>
* <span data-ttu-id="290e6-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="290e6-107">Authentication</span></span>
* <span data-ttu-id="290e6-108">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="290e6-108">Authorization</span></span>
* <span data-ttu-id="290e6-109">Controleren</span><span class="sxs-lookup"><span data-stu-id="290e6-109">Auditing</span></span>

<span data-ttu-id="290e6-110">Hallo-secties die volgt wordt ingegaan op verificatie en autorisatie in meer details, beheer en controle deel uitmaken van Hallo hybride identity lifecycle.</span><span class="sxs-lookup"><span data-stu-id="290e6-110">hello sections that follows will cover authentication and authorization in more details, administration and auditing are part of hello hybrid identity lifecycle.</span></span> <span data-ttu-id="290e6-111">Lees [beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) voor meer informatie over deze mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="290e6-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="290e6-112">Lees [Hallo vier stijlen van identiteit - identiteitsbeheer in Hallo leeftijd van hybride IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) voor meer informatie over elk van deze stijlen.</span><span class="sxs-lookup"><span data-stu-id="290e6-112">Read [hello Four Pillars of Identity - Identity Management in hello Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="290e6-113">Verificatie en autorisatie</span><span class="sxs-lookup"><span data-stu-id="290e6-113">Authentication and authorization</span></span>
<span data-ttu-id="290e6-114">Er zijn verschillende scenario's voor verificatie en autorisatie, heeft deze scenario's de specifieke vereisten waaraan moeten worden voldaan door Hallo hybride identiteitsoplossing dat Hallo bedrijf gaat tooadopt is.</span><span class="sxs-lookup"><span data-stu-id="290e6-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by hello hybrid identity solution that hello company is going tooadopt.</span></span> <span data-ttu-id="290e6-115">Scenario's met betrekking tot zakelijke tooBusiness (B2B) kunt communicatie toevoegen een extra uitdaging voor IT-beheerders omdat moeten tooensure die Hallo-verificatie en autorisatie methode die wordt gebruikt door de organisatie Hallo met hun zakelijke partners communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="290e6-115">Scenarios involving Business tooBusiness (B2B) communication can add an extra challenge for IT Admins since they will need tooensure that hello authentication and authorization method used by hello organization can communicate with their business partners.</span></span> <span data-ttu-id="290e6-116">Tijdens het Hallo-proces voor verificatie en autorisatie vereisten ontwerpen, zorg ervoor dat Hallo volgende vragen worden beantwoord:</span><span class="sxs-lookup"><span data-stu-id="290e6-116">During hello designing process for authentication and authorization requirements, ensure that hello following questions are answered:</span></span>

* <span data-ttu-id="290e6-117">Wordt van uw organisatie verifiëren en autoriseren van alleen gebruikers die zich bevindt op hun identiteitsbeheersysteem?</span><span class="sxs-lookup"><span data-stu-id="290e6-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="290e6-118">Zijn er plannen voor B2B-scenario's?</span><span class="sxs-lookup"><span data-stu-id="290e6-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="290e6-119">Zo ja, u al weet welke protocollen (SAML, OAuth, Kerberos, Tokens of certificaten) wordt gebruikt tooconnect beide bedrijven worden?</span><span class="sxs-lookup"><span data-stu-id="290e6-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used tooconnect both businesses?</span></span>
* <span data-ttu-id="290e6-120">Hallo hybride identiteitsoplossing dat u tooadopt gaat biedt ondersteuning voor deze protocollen?</span><span class="sxs-lookup"><span data-stu-id="290e6-120">Does hello hybrid identity solution that you are going tooadopt support those protocols?</span></span>

<span data-ttu-id="290e6-121">Een ander belangrijk punt tooconsider is waar Hallo verificatie opslagplaats die wordt gebruikt door gebruikers en partners worden geplaatst en Hallo beheermodel toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="290e6-121">Another important point tooconsider is where hello authentication repository that will be used by users and partners will be located and hello administrative model toobe used.</span></span> <span data-ttu-id="290e6-122">Houd rekening met Hallo na twee core opties:</span><span class="sxs-lookup"><span data-stu-id="290e6-122">Consider hello following two core options:</span></span>

* <span data-ttu-id="290e6-123">Gecentraliseerd: in dit model Hallo van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie of in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="290e6-123">Centralized: in this model hello user’s credentials, policies and administration can be centralized on-premises or in hello cloud.</span></span>
* <span data-ttu-id="290e6-124">Hybride: in dit model Hallo van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie en een gerepliceerde in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="290e6-124">Hybrid: in this model hello user’s credentials, policies and administration will be centralized on-premises and a replicated in hello cloud.</span></span>

<span data-ttu-id="290e6-125">Welk model van uw organisatie invoert varieert volgens tootheir zakelijke vereisten, wilt u tooanswer Hallo vragen tooidentify waarbij Hallo identiteitsbeheersysteem wordt zich bevinden en Hallo beheerdersmodus toouse te volgen:</span><span class="sxs-lookup"><span data-stu-id="290e6-125">Which model your organization will adopt will vary according tootheir business requirements, you want tooanswer hello following questions tooidentify where hello identity management system will reside and hello administrative mode toouse:</span></span>

* <span data-ttu-id="290e6-126">Beschikt uw organisatie momenteel over identity management lokale?</span><span class="sxs-lookup"><span data-stu-id="290e6-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="290e6-127">Zo ja, wel ze van plan bent tookeep deze?</span><span class="sxs-lookup"><span data-stu-id="290e6-127">If yes, do they plan tookeep it?</span></span>
  * <span data-ttu-id="290e6-128">Zijn er eventuele voorschriften of naleving vereisten die uw organisatie moet volgen die bepaald waarin Hallo identiteitsbeheersysteem zich moet bevinden?</span><span class="sxs-lookup"><span data-stu-id="290e6-128">Are there any regulation or compliance requirements that your organization must follow that dictates where hello identity management system should reside?</span></span>
* <span data-ttu-id="290e6-129">Uw organisatie gebruikt eenmalige aanmelding voor apps die zich on-premises of in Hallo cloud?</span><span class="sxs-lookup"><span data-stu-id="290e6-129">Does your organization use single sign-on for apps located on-premises or in hello cloud?</span></span>
  * <span data-ttu-id="290e6-130">Zo ja, Hallo acceptatie van een hybride identiteit modellen beïnvloedt dit proces?</span><span class="sxs-lookup"><span data-stu-id="290e6-130">If yes, does hello adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="290e6-131">Access Control</span><span class="sxs-lookup"><span data-stu-id="290e6-131">Access Control</span></span>
<span data-ttu-id="290e6-132">Hoewel verificatie en autorisatie core elementen tooenable toocorporate gegevens opvragen via de validatie van de gebruiker zijn, is het ook belangrijk toocontrol Hallo toegangsniveau dat deze gebruikers zijn en het Hallo-niveau van toegangbeheerders hebben via Hallo bronnen die ze beheert.</span><span class="sxs-lookup"><span data-stu-id="290e6-132">While authentication and authorization are core elements tooenable access toocorporate data through user’s validation, it is also important toocontrol hello level of access that these users will have and hello level of access administrators will have over hello resources that they are managing.</span></span> <span data-ttu-id="290e6-133">Uw oplossing voor hybride identiteit moet kunnen tooprovide gedetailleerde toegang tooresources overdracht en role base access control.</span><span class="sxs-lookup"><span data-stu-id="290e6-133">Your hybrid identity solution must be able tooprovide granular access tooresources, delegation and role base access control.</span></span> <span data-ttu-id="290e6-134">Zorg ervoor dat Hallo volgende vraag worden beantwoord met betrekking tot toegangsbeheer:</span><span class="sxs-lookup"><span data-stu-id="290e6-134">Ensure that hello following question are answered regarding access control:</span></span>

* <span data-ttu-id="290e6-135">Uw bedrijf heeft meer dan één gebruiker met verhoogde bevoegdheden toomanage uw identiteitssysteem?</span><span class="sxs-lookup"><span data-stu-id="290e6-135">Does your company have more than one user with elevated privilege toomanage your identity system?</span></span>
  * <span data-ttu-id="290e6-136">Als u Ja, heeft elke gebruiker behoefte aan Hallo hetzelfde toegangsniveau?</span><span class="sxs-lookup"><span data-stu-id="290e6-136">If yes, does each user need hello same access level?</span></span>
* <span data-ttu-id="290e6-137">Zou uw bedrijf behoefte toodelegate toegang toousers toomanage specifieke bronnen?</span><span class="sxs-lookup"><span data-stu-id="290e6-137">Would your company need toodelegate access toousers toomanage specific resources?</span></span>
  * <span data-ttu-id="290e6-138">Zo ja, hoe vaak dit gebeurt?</span><span class="sxs-lookup"><span data-stu-id="290e6-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="290e6-139">Uw bedrijf moet toointegrate toegangsmogelijkheden besturingselement tussen on-premises en cloud bronnen?</span><span class="sxs-lookup"><span data-stu-id="290e6-139">Would your company need toointegrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="290e6-140">Moet uw bedrijf toolimit toegang tooresources volgens toosome voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="290e6-140">Would your company need toolimit access tooresources according toosome conditions?</span></span>
* <span data-ttu-id="290e6-141">Moet uw bedrijf alle toepassingen die u aangepaste besturingselement toegang tot toosome bronnen moet?</span><span class="sxs-lookup"><span data-stu-id="290e6-141">Would your company have any application that needs custom control access toosome resources?</span></span>
  * <span data-ttu-id="290e6-142">Zo ja, waarbij deze apps zich bevinden (lokaal of in de cloud Hallo)?</span><span class="sxs-lookup"><span data-stu-id="290e6-142">If yes, where are those apps located (on-premises or in hello cloud)?</span></span>
  * <span data-ttu-id="290e6-143">Zo ja, waar zijn die zijn gericht bronnen (lokaal of in de cloud Hallo)?</span><span class="sxs-lookup"><span data-stu-id="290e6-143">If yes, where are those target resources located (on-premises or in hello cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="290e6-144">Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt.</span><span class="sxs-lookup"><span data-stu-id="290e6-144">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="290e6-145">[Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.</span><span class="sxs-lookup"><span data-stu-id="290e6-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="290e6-146">Door deze vragen te beantwoorden wordt u selecteren welke optie het beste aansluit op uw bedrijfsbehoeften.</span><span class="sxs-lookup"><span data-stu-id="290e6-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="290e6-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="290e6-147">Next steps</span></span>
[<span data-ttu-id="290e6-148">Vereisten voor respons op incidenten bepalen</span><span class="sxs-lookup"><span data-stu-id="290e6-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="290e6-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="290e6-149">See Also</span></span>
[<span data-ttu-id="290e6-150">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="290e6-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

