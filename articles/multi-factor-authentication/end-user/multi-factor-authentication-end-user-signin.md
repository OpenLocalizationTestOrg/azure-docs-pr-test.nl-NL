---
title: Azure MFA aanmelden met verificatie in twee stappen | Microsoft Docs
description: Deze pagina vindt u u richtlijnen voor het bekijken van de verschillende aanmelden methoden beschikbaar met Azure MFA.
keywords: verificatie van gebruikers, -aanmeldingservaring aanpast, aanmelden met een mobiele telefoon, aanmelden met een telefoon (werk)
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="1b500-104">De ervaring aanmelden met Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1b500-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="1b500-105">Het doel van dit artikel is een typische aanmeldingservaring doorlopen.</span><span class="sxs-lookup"><span data-stu-id="1b500-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="1b500-106">Zie voor meer informatie met het aanmelden of problemen [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="1b500-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="1b500-107">Wat is uw ervaring aanmelden?</span><span class="sxs-lookup"><span data-stu-id="1b500-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="1b500-108">Uw aanmeldingservaring is afhankelijk van wat u wilt gebruiken als uw tweede factor: een telefonische oproep of een app authentication teksten.</span><span class="sxs-lookup"><span data-stu-id="1b500-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="1b500-109">Kies de optie die het beste beschrijft wat u doet:</span><span class="sxs-lookup"><span data-stu-id="1b500-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="1b500-110">Hoe meld u aan?</span><span class="sxs-lookup"><span data-stu-id="1b500-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="1b500-111">Met een telefonische oproep naar mijn telefoon mobile- of office</span><span class="sxs-lookup"><span data-stu-id="1b500-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="1b500-112">Met een tekst naar mijn mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="1b500-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="1b500-113">Met meldingen van de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="1b500-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="1b500-114">Met verificatiecodes vanuit de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="1b500-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="1b500-115">Met een alternatieve methode omdat ik mijn voorkeursmethode nu kunt gebruiken</span><span class="sxs-lookup"><span data-stu-id="1b500-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="1b500-116">Aanmelden met een telefonische oproep</span><span class="sxs-lookup"><span data-stu-id="1b500-116">Signing in with a phone call</span></span>
<span data-ttu-id="1b500-117">De volgende informatie beschrijft de ervaring van de verificatie in twee stappen met een aanroep naar uw telefoon mobile- of kantoornetwerk.</span><span class="sxs-lookup"><span data-stu-id="1b500-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="1b500-118">Aanmelden bij een toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b500-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="1b500-119">Microsoft roept u.</span><span class="sxs-lookup"><span data-stu-id="1b500-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="1b500-120">Beantwoord de telefoon en druk op de #-toets.</span><span class="sxs-lookup"><span data-stu-id="1b500-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="1b500-121">Aanmelden met een SMS-bericht</span><span class="sxs-lookup"><span data-stu-id="1b500-121">Signing in with a text message</span></span>
<span data-ttu-id="1b500-122">De volgende informatie beschrijft de ervaring van de verificatie in twee stappen met een SMS-bericht naar uw mobiele telefoon:</span><span class="sxs-lookup"><span data-stu-id="1b500-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="1b500-123">Aanmelden bij een toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b500-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="1b500-124">Microsoft stuurt u een SMS-bericht met een aantal code.</span><span class="sxs-lookup"><span data-stu-id="1b500-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="1b500-125">Voer de code in de daarvoor bestemde vak op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="1b500-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="1b500-126">Aanmelden met de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="1b500-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="1b500-127">De volgende informatie beschrijft de ervaring van het gebruik van de Microsoft Authenticator-app voor verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="1b500-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="1b500-128">Er zijn twee verschillende manieren om de app te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b500-128">There are two different ways to use the app.</span></span> <span data-ttu-id="1b500-129">U pushmeldingen kan ontvangen op uw apparaat kunt, of u de app als u een verificatiecode.</span><span class="sxs-lookup"><span data-stu-id="1b500-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="1b500-130">Aanmelden met een melding van de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="1b500-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="1b500-131">Aanmelden bij een toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b500-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="1b500-132">Microsoft stuurt een melding met de Microsoft Authenticator-app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="1b500-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft verzendt melding](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="1b500-134">Open de melding op uw telefoon en selecteer de **controleren** sleutel.</span><span class="sxs-lookup"><span data-stu-id="1b500-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="1b500-135">Als uw bedrijf een PINCODE vereist is, moet u deze hier opgeven.</span><span class="sxs-lookup"><span data-stu-id="1b500-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="1b500-136">U moet nu worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="1b500-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="1b500-137">Aanmelden met een verificatiecode met de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="1b500-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="1b500-138">Als u de Microsoft Authenticator-app om op te halen verificatiecodes gebruikt, vervolgens ziet wanneer u de app opent u een getal onder de accountnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="1b500-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="1b500-139">Deze waarde verandert elke 30 seconden, zodat u niet hetzelfde nummer twee keer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1b500-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="1b500-140">Wanneer u wordt gevraagd of u voor een verificatiecode, open de app en gebruiken met het opgegeven getal momenteel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b500-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="1b500-141">Aanmelden bij een toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b500-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="1b500-142">Microsoft vraagt u om een verificatiecode.</span><span class="sxs-lookup"><span data-stu-id="1b500-142">Microsoft prompts you for a verification code.</span></span>

  ![Voer de verificatiecode in](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="1b500-144">Open de Microsoft Authenticator-app op uw telefoon en voer de code in het vak waar u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="1b500-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="1b500-145">Aanmelden met een alternatieve methode</span><span class="sxs-lookup"><span data-stu-id="1b500-145">Signing in with an alternate method</span></span>
<span data-ttu-id="1b500-146">Soms hebt u niet de telefoon of het apparaat die u hebt ingesteld als uw contactmethode voorkeursoptie voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="1b500-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="1b500-147">Deze situatie is de reden waarom het is raadzaam dat u back-upmethoden voor uw account ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1b500-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="1b500-148">De volgende sectie leest u hoe zich kunnen aanmelden met een alternatieve methode als uw primaire contactmethode mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1b500-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="1b500-149">Aanmelden bij een toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b500-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="1b500-150">Selecteer **gebruik een andere verificatieoptie**.</span><span class="sxs-lookup"><span data-stu-id="1b500-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="1b500-151">Er zijn andere verificatie-opties op basis van hoeveel ingesteld hebt.</span><span class="sxs-lookup"><span data-stu-id="1b500-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="1b500-152">Selecteer een alternatieve methode en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="1b500-152">Choose an alternate method and sign in.</span></span>

  ![Alternatieve methode gebruiken](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="1b500-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b500-154">Next steps</span></span>

<span data-ttu-id="1b500-155">Als u problemen met aanmelden met verificatie in twee stappen hebt, informatie op te krijgen [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="1b500-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="1b500-156">Meer informatie over hoe [de instellingen van de verificatie in twee stappen beheren](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1b500-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="1b500-157">Ontdek hoe [aan de slag met de app Microsoft Authenticator](microsoft-authenticator-app-how-to.md) zodat u meldingen kunt aan te melden, in plaats van teksten en telefoongesprekken.</span><span class="sxs-lookup"><span data-stu-id="1b500-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 