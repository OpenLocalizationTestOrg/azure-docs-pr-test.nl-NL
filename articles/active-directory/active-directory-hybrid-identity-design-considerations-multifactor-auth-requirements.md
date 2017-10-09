---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - bepalen vereisten voor multi-factor authentication-server
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
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
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="4357d-104">Vereisten multi-factor authentication voor uw oplossing voor hybride identiteit bepalen</span><span class="sxs-lookup"><span data-stu-id="4357d-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="4357d-105">In deze wereld van mobility met gebruikers die toegang tot gegevens en toepassingen in de cloud Hallo en vanaf elk apparaat is voor het beveiligen van deze informatie geworden vooral gekeken naar.</span><span class="sxs-lookup"><span data-stu-id="4357d-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="4357d-106">Elke dag wordt er een nieuwe kop over een inbreuk op de beveiliging is.</span><span class="sxs-lookup"><span data-stu-id="4357d-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="4357d-107">Hoewel er is geen garantie tegen dergelijke schendingen, meervoudige verificatie biedt een extra laag van beveiliging toohelp te voorkomen dat deze inbreuk.</span><span class="sxs-lookup"><span data-stu-id="4357d-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="4357d-108">Start Hallo organisaties vereisten voor multi-factor authentication evalueren.</span><span class="sxs-lookup"><span data-stu-id="4357d-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="4357d-109">Wat is Hallo organisatie poging toosecure.</span><span class="sxs-lookup"><span data-stu-id="4357d-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="4357d-110">Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor het instellen en inschakelen van Hallo organisaties gebruikers voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4357d-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="4357d-111">Als u niet bekend met MFA en wat het doet bent, is het raadzaam dat u lees Hallo artikel [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) voorafgaande toocontinue lezen van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4357d-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="4357d-112">Zorg ervoor dat tooanswer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4357d-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="4357d-113">Is uw bedrijf probeert toosecure Microsoft-apps?</span><span class="sxs-lookup"><span data-stu-id="4357d-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="4357d-114">Hoe deze apps worden gepubliceerd?</span><span class="sxs-lookup"><span data-stu-id="4357d-114">How these apps are published?</span></span>
* <span data-ttu-id="4357d-115">Uw bedrijf biedt externe toegang tooallow werknemers tooaccess lokale apps?</span><span class="sxs-lookup"><span data-stu-id="4357d-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="4357d-116">Zo ja, welk type externe toegang? U moet ook tooevaluate waar Hallo-gebruikers die toegang deze toepassingen tot geplaatst worden.</span><span class="sxs-lookup"><span data-stu-id="4357d-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="4357d-117">Deze evaluatie is een andere belangrijke stap toodefine Hallo juiste multi-factor authentication-strategie.</span><span class="sxs-lookup"><span data-stu-id="4357d-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="4357d-118">Zorg ervoor dat tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4357d-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="4357d-119">Waar bevinden de Hallo gebruikers gaan toobe zich?</span><span class="sxs-lookup"><span data-stu-id="4357d-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="4357d-120">Ze zijn locatie overal?</span><span class="sxs-lookup"><span data-stu-id="4357d-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="4357d-121">Wil uw bedrijf tooestablish beperkingen op basis van de locatie van de gebruiker toohello?</span><span class="sxs-lookup"><span data-stu-id="4357d-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="4357d-122">Als u weet dat deze vereisten voldoet, is het belangrijk tooalso evalueren van de gebruiker van het Hallo-vereisten voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4357d-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="4357d-123">Deze evaluatie is belangrijk omdat het Hallo-vereisten definieert voor het implementeren van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="4357d-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="4357d-124">Zorg ervoor dat tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4357d-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="4357d-125">Hallo gebruikers bekend bent met multi-factor authentication-server?</span><span class="sxs-lookup"><span data-stu-id="4357d-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="4357d-126">Enkele aanvullende authenticatie vereist tooprovide worden?</span><span class="sxs-lookup"><span data-stu-id="4357d-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="4357d-127">Zo ja, alle Hallo tijd, wanneer die afkomstig is van externe netwerken of toegang tot specifieke toepassingen of andere voorwaarden?</span><span class="sxs-lookup"><span data-stu-id="4357d-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="4357d-128">Hallo gebruikers training in nodig toosetup en implementeer multi-factor authentication-server?</span><span class="sxs-lookup"><span data-stu-id="4357d-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="4357d-129">Wat zijn Hallo belangrijke scenario's dat uw bedrijf wil tooenable multi-factor authentication voor hun gebruikers?</span><span class="sxs-lookup"><span data-stu-id="4357d-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="4357d-130">Na het Hallo vorige vragen beantwoorden, kunt u zich kunt toounderstand als er meerdere factoren verificatie al geïmplementeerd op locatie.</span><span class="sxs-lookup"><span data-stu-id="4357d-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="4357d-131">Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor het instellen en inschakelen van Hallo organisaties gebruikers voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4357d-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="4357d-132">Zorg ervoor dat tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4357d-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="4357d-133">Heeft uw bedrijf behoefte aan tooprotect bevoegde accounts met MFA?</span><span class="sxs-lookup"><span data-stu-id="4357d-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="4357d-134">Heeft uw bedrijf behoefte tooenable MFA voor bepaalde toepassing om wettelijke redenen?</span><span class="sxs-lookup"><span data-stu-id="4357d-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="4357d-135">Heeft uw bedrijf tooenable MFA nodig voor alle in aanmerking komende gebruikers van deze toepassing of alleen beheerders</span><span class="sxs-lookup"><span data-stu-id="4357d-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="4357d-136">Hebt u nog moet MFA altijd ingeschakeld of alleen wanneer Hallo gebruikers zijn aangemeld buiten uw bedrijfsnetwerk?</span><span class="sxs-lookup"><span data-stu-id="4357d-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="4357d-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4357d-137">Next steps</span></span>
[<span data-ttu-id="4357d-138">Een strategie voor hybride identiteit acceptatie definiëren</span><span class="sxs-lookup"><span data-stu-id="4357d-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="4357d-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4357d-139">See also</span></span>
[<span data-ttu-id="4357d-140">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="4357d-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

