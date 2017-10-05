---
title: Azure Active Directory hybride identiteit ontwerpoverwegingen - bepalen vereisten voor multi-factor authentication-server
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory de specifieke voorwaarden die u kiest bij het verifiëren van de gebruiker en alvorens deze toegang tot de toepassing. Als deze voorwaarden is voldaan, wordt de gebruiker geverifieerd en toegang te krijgen tot de toepassing."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="eae19-104">Vereisten multi-factor authentication voor uw oplossing voor hybride identiteit bepalen</span><span class="sxs-lookup"><span data-stu-id="eae19-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="eae19-105">In deze wereld van mobility met gebruikers die toegang tot gegevens en toepassingen in de cloud en vanaf elk apparaat is voor het beveiligen van deze informatie geworden vooral gekeken naar.</span><span class="sxs-lookup"><span data-stu-id="eae19-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="eae19-106">Elke dag wordt er een nieuwe kop over een inbreuk op de beveiliging is.</span><span class="sxs-lookup"><span data-stu-id="eae19-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="eae19-107">Hoewel er is geen garantie tegen dergelijke schendingen, biedt multi-factor authentication-server, een extra beveiligingslaag om te voorkomen dat deze inbreuk.</span><span class="sxs-lookup"><span data-stu-id="eae19-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="eae19-108">Start de organisaties vereisten voor multi-factor authentication evalueren.</span><span class="sxs-lookup"><span data-stu-id="eae19-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="eae19-109">Dat wil zeggen, wat is de organisatie probeert te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="eae19-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="eae19-110">Deze evaluatie is belangrijk om te definiëren van de technische vereisten voor het instellen en inschakelen van de organisaties gebruikers voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="eae19-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="eae19-111">Als u niet bekend met MFA en wat het doet bent, is het raadzaam dat u lees het artikel [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) voorafgaande om door te gaan met het lezen van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="eae19-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="eae19-112">Zorg ervoor dat het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="eae19-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="eae19-113">Is uw bedrijf bij het beveiligen van Microsoft-apps?</span><span class="sxs-lookup"><span data-stu-id="eae19-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="eae19-114">Hoe deze apps worden gepubliceerd?</span><span class="sxs-lookup"><span data-stu-id="eae19-114">How these apps are published?</span></span>
* <span data-ttu-id="eae19-115">Biedt uw bedrijf externe toegang zodat werknemers toegang tot lokale apps?</span><span class="sxs-lookup"><span data-stu-id="eae19-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="eae19-116">Zo ja, welk type externe toegang? U moet ook evalueren waar de gebruikers die toegang deze toepassingen tot worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="eae19-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="eae19-117">Deze evaluatie is een andere belangrijke stap voor het definiëren van de strategie voor de juiste multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="eae19-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="eae19-118">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="eae19-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="eae19-119">Waar de gebruikers gaat worden gevonden?</span><span class="sxs-lookup"><span data-stu-id="eae19-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="eae19-120">Ze zijn locatie overal?</span><span class="sxs-lookup"><span data-stu-id="eae19-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="eae19-121">Uw bedrijf tot stand wilt brengen beperkingen op basis van de locatie van de gebruiker?</span><span class="sxs-lookup"><span data-stu-id="eae19-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="eae19-122">Zodra u deze vereisten begrijpt, is het belangrijk om te bepalen ook de vereisten van de gebruiker voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="eae19-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="eae19-123">Deze evaluatie is belangrijk, omdat de vereisten voor het implementeren van multi-factor authentication-server zal worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eae19-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="eae19-124">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="eae19-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="eae19-125">De gebruikers bekend bent met multi-factor authentication-server?</span><span class="sxs-lookup"><span data-stu-id="eae19-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="eae19-126">Enkele toepassingen is vereist voor aanvullende verificatie?</span><span class="sxs-lookup"><span data-stu-id="eae19-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="eae19-127">Zo ja, de tijd, wanneer die afkomstig is van externe netwerken of toegang tot specifieke toepassingen of andere voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="eae19-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="eae19-128">De gebruikers training voor het instellen en implementeren van multi-factor authentication-server nodig?</span><span class="sxs-lookup"><span data-stu-id="eae19-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="eae19-129">Wat zijn de belangrijkste scenario's die uw bedrijf wil multi-factor authentication voor gebruikers inschakelen?</span><span class="sxs-lookup"><span data-stu-id="eae19-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="eae19-130">Na de vorige vragen te beantwoorden, zich u te bepalen of er meerdere factoren verificatie al geïmplementeerd op locatie zijn.</span><span class="sxs-lookup"><span data-stu-id="eae19-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="eae19-131">Deze evaluatie is belangrijk om te definiëren van de technische vereisten voor het instellen en inschakelen van de organisaties gebruikers voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="eae19-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="eae19-132">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="eae19-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="eae19-133">Moet uw bedrijf beveiligen van bevoegde accounts met MFA?</span><span class="sxs-lookup"><span data-stu-id="eae19-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="eae19-134">Heeft uw bedrijf behoefte inschakelen van MFA voor bepaalde toepassing om wettelijke redenen?</span><span class="sxs-lookup"><span data-stu-id="eae19-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="eae19-135">Moet uw bedrijf MFA inschakelen voor alle in aanmerking komende gebruikers van deze toepassing of alleen beheerders?</span><span class="sxs-lookup"><span data-stu-id="eae19-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="eae19-136">Hebt u nog moet MFA altijd ingeschakeld of alleen wanneer de gebruikers zijn aangemeld buiten uw bedrijfsnetwerk?</span><span class="sxs-lookup"><span data-stu-id="eae19-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="eae19-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eae19-137">Next steps</span></span>
[<span data-ttu-id="eae19-138">Een strategie voor hybride identiteit acceptatie definiëren</span><span class="sxs-lookup"><span data-stu-id="eae19-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="eae19-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="eae19-139">See also</span></span>
[<span data-ttu-id="eae19-140">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="eae19-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

