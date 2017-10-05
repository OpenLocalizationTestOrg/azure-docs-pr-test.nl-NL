---
title: Azure multi-factor Authentication - hoe het werkt
description: Multi-Factor Authentication van Azure helpt bij het bewaken van de toegang tot uw gegevens en toepassingen en komt tegemoet aan de wensen van gebruikers met een eenvoudige aanmeldprocedure. Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="e6271-104">De werking van Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e6271-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="e6271-105">De beveiliging van verificatie in twee stappen ligt de gelaagde benadering.</span><span class="sxs-lookup"><span data-stu-id="e6271-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="e6271-106">Inbreuk op meerdere verificatiefactoren geeft een belangrijke uitdaging voor kwaadwillende personen.</span><span class="sxs-lookup"><span data-stu-id="e6271-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="e6271-107">Zelfs als een aanvaller erin slaagt voor meer informatie over het wachtwoord van gebruikers, is deze onbruikbaar zonder dat ook bezit is van het vertrouwde apparaat.</span><span class="sxs-lookup"><span data-stu-id="e6271-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="e6271-109">Multi-Factor Authentication van Azure helpt bij het bewaken van de toegang tot uw gegevens en toepassingen en komt tegemoet aan de wensen van gebruikers met een eenvoudige aanmeldprocedure.</span><span class="sxs-lookup"><span data-stu-id="e6271-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="e6271-110">Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.</span><span class="sxs-lookup"><span data-stu-id="e6271-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="e6271-111">Methoden voor verificatie in twee stappen</span><span class="sxs-lookup"><span data-stu-id="e6271-111">Methods available for two-step verification</span></span>
<span data-ttu-id="e6271-112">Wanneer een gebruiker zich aanmeldt, wordt een aanvullende verificatie verzonden naar de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e6271-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="e6271-113">Hieronder vindt u een lijst met methoden die kunnen worden gebruikt voor deze tweede verificatie.</span><span class="sxs-lookup"><span data-stu-id="e6271-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="e6271-114">Verificatiemethode</span><span class="sxs-lookup"><span data-stu-id="e6271-114">Verification Method</span></span> | <span data-ttu-id="e6271-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e6271-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6271-116">Telefoonoproep</span><span class="sxs-lookup"><span data-stu-id="e6271-116">Phone call</span></span> |<span data-ttu-id="e6271-117">Een aanroep van wordt het geregistreerde telefoonnummer van een gebruiker geplaatst.</span><span class="sxs-lookup"><span data-stu-id="e6271-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="e6271-118">De gebruiker voert een PINCODE, indien nodig worden vervolgens de #-toets indrukt.</span><span class="sxs-lookup"><span data-stu-id="e6271-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="e6271-119">SMS-bericht</span><span class="sxs-lookup"><span data-stu-id="e6271-119">Text message</span></span> |<span data-ttu-id="e6271-120">Een SMS-bericht verzonden naar een gebruiker mobiele telefoon met een code van zes cijfers.</span><span class="sxs-lookup"><span data-stu-id="e6271-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="e6271-121">De gebruiker voert deze code op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="e6271-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="e6271-122">Meldingen voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="e6271-122">Mobile app notification</span></span> |<span data-ttu-id="e6271-123">Een verzoek voor identiteitverificatie verzonden naar een gebruiker Smartphone.</span><span class="sxs-lookup"><span data-stu-id="e6271-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="e6271-124">De gebruiker een PINCODE invoert, indien nodig en vervolgens selecteert **controleren** op de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="e6271-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="e6271-125">Verificatiecode van mobiele app</span><span class="sxs-lookup"><span data-stu-id="e6271-125">Mobile app verification code</span></span> |<span data-ttu-id="e6271-126">De mobiele app, die wordt uitgevoerd op de Smartphone van een gebruiker, wordt een bevestigingscode die elke 30 seconden wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e6271-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="e6271-127">De gebruiker de meest recente code zoekt en krijgt de op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="e6271-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="e6271-128">OATH-tokens van derde partij</span><span class="sxs-lookup"><span data-stu-id="e6271-128">Third-party OATH tokens</span></span> | <span data-ttu-id="e6271-129">Azure multi-factor Authentication-Server kan worden geconfigureerd voor het accepteren van derden verificatiemethoden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e6271-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="e6271-130">Azure multi-factor Authentication biedt selecteerbare verificatiemethoden voor zowel cloud als de server.</span><span class="sxs-lookup"><span data-stu-id="e6271-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="e6271-131">U kunt kiezen welke methoden zijn beschikbaar voor uw gebruikers: telefoonoproep, tekst, app-melding of app-codes.</span><span class="sxs-lookup"><span data-stu-id="e6271-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="e6271-132">Zie voor meer informatie [selecteerbare verificatiemethoden](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="e6271-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6271-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6271-133">Next steps</span></span>

- <span data-ttu-id="e6271-134">Meer informatie over de verschillende [versies en verbruikmethoden voor Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="e6271-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="e6271-135">Kies of u voor het implementeren van Azure MFA [in de cloud of on-premises](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e6271-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="e6271-136">Lees de antwoorden voor [Veelgestelde vragen](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e6271-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>