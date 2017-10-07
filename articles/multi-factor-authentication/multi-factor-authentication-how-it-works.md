---
title: Multi-factor Authentication - aaaAzure hoe het werkt
description: Azure multi-factor Authentication helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="b8818-104">De werking van Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="b8818-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="b8818-105">Hallo beveiliging van verificatie in twee stappen ligt de gelaagde benadering.</span><span class="sxs-lookup"><span data-stu-id="b8818-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="b8818-106">Inbreuk op meerdere verificatiefactoren geeft een belangrijke uitdaging voor kwaadwillende personen.</span><span class="sxs-lookup"><span data-stu-id="b8818-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="b8818-107">Zelfs als een aanvaller erin toolearn Hallo het wachtwoord van gebruiker slaagt, is deze onbruikbaar zonder dat ook het bezit van Hallo vertrouwd apparaat.</span><span class="sxs-lookup"><span data-stu-id="b8818-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="b8818-109">Azure multi-factor Authentication helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b8818-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="b8818-110">Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.</span><span class="sxs-lookup"><span data-stu-id="b8818-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="b8818-111">Methoden voor verificatie in twee stappen</span><span class="sxs-lookup"><span data-stu-id="b8818-111">Methods available for two-step verification</span></span>
<span data-ttu-id="b8818-112">Wanneer een gebruiker zich aanmeldt, wordt een aanvullende verificatie toohello gebruiker verzonden.</span><span class="sxs-lookup"><span data-stu-id="b8818-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="b8818-113">Hallo hieronder vindt u een lijst met methoden die kunnen worden gebruikt voor deze tweede verificatie.</span><span class="sxs-lookup"><span data-stu-id="b8818-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="b8818-114">Verificatiemethode</span><span class="sxs-lookup"><span data-stu-id="b8818-114">Verification Method</span></span> | <span data-ttu-id="b8818-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b8818-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8818-116">Telefoonoproep</span><span class="sxs-lookup"><span data-stu-id="b8818-116">Phone call</span></span> |<span data-ttu-id="b8818-117">Het geregistreerde telefoonnummer van de gebruiker van de tooa is gebeld.</span><span class="sxs-lookup"><span data-stu-id="b8818-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="b8818-118">Hallo-gebruiker een PINCODE invoert, indien nodig vervolgens Hallo #-toets indrukt.</span><span class="sxs-lookup"><span data-stu-id="b8818-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="b8818-119">SMS-bericht</span><span class="sxs-lookup"><span data-stu-id="b8818-119">Text message</span></span> |<span data-ttu-id="b8818-120">Een SMS-bericht verzonden van de gebruiker tooa mobiele telefoon met een code van zes cijfers.</span><span class="sxs-lookup"><span data-stu-id="b8818-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="b8818-121">Hallo gebruiker voert deze code aan de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="b8818-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="b8818-122">Meldingen voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="b8818-122">Mobile app notification</span></span> |<span data-ttu-id="b8818-123">Een verzoek voor identiteitverificatie verzonden Smartphone tooa van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b8818-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="b8818-124">Hallo gebruiker een PINCODE invoert, indien nodig en vervolgens selecteert **controleren** op Hallo mobiele app.</span><span class="sxs-lookup"><span data-stu-id="b8818-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="b8818-125">Verificatiecode van mobiele app</span><span class="sxs-lookup"><span data-stu-id="b8818-125">Mobile app verification code</span></span> |<span data-ttu-id="b8818-126">Hallo mobiele app, die wordt uitgevoerd op de Smartphone van een gebruiker, wordt een bevestigingscode die elke 30 seconden wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b8818-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="b8818-127">Hallo gebruiker zoeken naar de meest recente code Hallo en krijgt de op de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="b8818-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="b8818-128">OATH-tokens van derde partij</span><span class="sxs-lookup"><span data-stu-id="b8818-128">Third-party OATH tokens</span></span> | <span data-ttu-id="b8818-129">Azure multi-factor Authentication-Server kan worden geconfigureerd tooaccept verificatiemethoden van derden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8818-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="b8818-130">Azure multi-factor Authentication biedt selecteerbare verificatiemethoden voor zowel cloud als de server.</span><span class="sxs-lookup"><span data-stu-id="b8818-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="b8818-131">U kunt kiezen welke methoden zijn beschikbaar voor uw gebruikers: telefoonoproep, tekst, app-melding of app-codes.</span><span class="sxs-lookup"><span data-stu-id="b8818-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="b8818-132">Zie voor meer informatie [selecteerbare verificatiemethoden](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="b8818-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8818-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8818-133">Next steps</span></span>

- <span data-ttu-id="b8818-134">Meer informatie over andere Hallo [versies en verbruikmethoden voor Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="b8818-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="b8818-135">Kies of toodeploy Azure MFA [in Hallo cloud of on-premises](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b8818-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="b8818-136">Lees de antwoorden voor [Veelgestelde vragen](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="b8818-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>