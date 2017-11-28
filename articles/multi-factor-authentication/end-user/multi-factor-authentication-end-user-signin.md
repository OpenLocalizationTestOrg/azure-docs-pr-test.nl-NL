---
title: aaaAzure MFA aanmelden met verificatie in twee stappen | Microsoft Docs
description: Deze pagina vindt u u richtlijnen op waar toogo toosee Hallo verschillende aanmeldingsmethoden beschikbaar met Azure MFA.
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
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="38b04-104">Hallo-aanmeldingservaring aanpast met Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="38b04-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="38b04-105">Hallo-doel van dit artikel is toowalk via een typische-aanmeldingservaring aanpast.</span><span class="sxs-lookup"><span data-stu-id="38b04-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="38b04-106">Zie voor hulp bij het aanmelden of tootroubleshoot problemen, [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="38b04-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="38b04-107">Wat is uw ervaring aanmelden?</span><span class="sxs-lookup"><span data-stu-id="38b04-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="38b04-108">Uw aanmeldingservaring is afhankelijk van wat u toouse als uw tweede factor kiest: een telefonische oproep of een app authentication teksten.</span><span class="sxs-lookup"><span data-stu-id="38b04-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="38b04-109">Kies Hallo-optie die het beste beschrijft wat u doet:</span><span class="sxs-lookup"><span data-stu-id="38b04-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="38b04-110">Hoe meld u aan?</span><span class="sxs-lookup"><span data-stu-id="38b04-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="38b04-111">Met een telefonische oproep toomy mobile- of -telefoon</span><span class="sxs-lookup"><span data-stu-id="38b04-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="38b04-112">Met een tekst toomy mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="38b04-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="38b04-113">Met meldingen van Hallo Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="38b04-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="38b04-114">Met verificatiecodes van Hallo Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="38b04-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="38b04-115">Met een alternatieve methode omdat ik mijn voorkeursmethode nu kunt gebruiken</span><span class="sxs-lookup"><span data-stu-id="38b04-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="38b04-116">Aanmelden met een telefonische oproep</span><span class="sxs-lookup"><span data-stu-id="38b04-116">Signing in with a phone call</span></span>
<span data-ttu-id="38b04-117">Hallo volgende informatie beschrijft Hallo in twee stappen verificatie-ervaring met een aanroep tooyour mobiele telefoon of telefoon (werk).</span><span class="sxs-lookup"><span data-stu-id="38b04-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="38b04-118">Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38b04-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="38b04-119">Microsoft roept u.</span><span class="sxs-lookup"><span data-stu-id="38b04-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="38b04-120">Hallo telefoon te beantwoorden en druk op Hallo #-toets.</span><span class="sxs-lookup"><span data-stu-id="38b04-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="38b04-121">Aanmelden met een SMS-bericht</span><span class="sxs-lookup"><span data-stu-id="38b04-121">Signing in with a text message</span></span>
<span data-ttu-id="38b04-122">Hallo volgende informatie beschrijft Hallo in twee stappen verificatie-ervaring met een SMS-bericht tooyour mobiele telefoon:</span><span class="sxs-lookup"><span data-stu-id="38b04-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="38b04-123">Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38b04-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="38b04-124">Microsoft stuurt u een SMS-bericht met een aantal code.</span><span class="sxs-lookup"><span data-stu-id="38b04-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="38b04-125">Hallo-code invoeren in Hallo daarvoor bestemde vak op de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="38b04-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="38b04-126">Aanmelden met Hallo Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="38b04-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="38b04-127">Hallo beschrijft volgende informatie de ervaring Hallo Hallo Microsoft Authenticator-app gebruiken voor verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="38b04-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="38b04-128">Er zijn twee verschillende manieren toouse Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="38b04-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="38b04-129">U kunt pushmeldingen kan ontvangen op uw apparaat kunt, of u Hallo app tooget een verificatiecode.</span><span class="sxs-lookup"><span data-stu-id="38b04-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="38b04-130">toosign met een melding van Hallo Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="38b04-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="38b04-131">Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38b04-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="38b04-132">Microsoft stuurt een melding toohello Microsoft Authenticator-app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="38b04-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft verzendt melding](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="38b04-134">Open Hallo melding op uw telefoon en selecteer Hallo **controleren** sleutel.</span><span class="sxs-lookup"><span data-stu-id="38b04-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="38b04-135">Als uw bedrijf een PINCODE vereist is, moet u deze hier opgeven.</span><span class="sxs-lookup"><span data-stu-id="38b04-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="38b04-136">U moet nu worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="38b04-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="38b04-137">toosign aan met een verificatiecode met Hallo Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="38b04-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="38b04-138">Als u tooget verificatiecodes voor Hallo Microsoft Authenticator-app gebruikt, vervolgens ziet bij het openen van de app Hallo u een getal onder de accountnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="38b04-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="38b04-139">Deze waarde verandert elke 30 seconden, zodat u niet dezelfde tweemaal number Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38b04-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="38b04-140">Wanneer u wordt gevraagd een voor een verificatiecode Hallo app openen en gebruiken met het opgegeven getal momenteel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="38b04-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="38b04-141">Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38b04-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="38b04-142">Microsoft vraagt u om een verificatiecode.</span><span class="sxs-lookup"><span data-stu-id="38b04-142">Microsoft prompts you for a verification code.</span></span>

  ![Voer de verificatiecode in](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="38b04-144">Open Hallo Microsoft Authenticator-app op uw telefoon en Hallo-code invoeren in Hallo vak waar u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="38b04-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="38b04-145">Aanmelden met een alternatieve methode</span><span class="sxs-lookup"><span data-stu-id="38b04-145">Signing in with an alternate method</span></span>
<span data-ttu-id="38b04-146">Soms hebt u geen telefoon hello of een apparaat die u hebt ingesteld als uw contactmethode voorkeursoptie voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="38b04-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="38b04-147">Deze situatie is de reden waarom het is raadzaam dat u back-upmethoden voor uw account ingesteld.</span><span class="sxs-lookup"><span data-stu-id="38b04-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="38b04-148">Hallo volgende sectie leest u hoe toosign aan met een alternatieve methode als uw primaire contactmethode mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="38b04-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="38b04-149">Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38b04-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="38b04-150">Selecteer **gebruik een andere verificatieoptie**.</span><span class="sxs-lookup"><span data-stu-id="38b04-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="38b04-151">Er zijn andere verificatie-opties op basis van hoeveel ingesteld hebt.</span><span class="sxs-lookup"><span data-stu-id="38b04-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="38b04-152">Selecteer een alternatieve methode en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="38b04-152">Choose an alternate method and sign in.</span></span>

  ![Alternatieve methode gebruiken](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="38b04-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38b04-154">Next steps</span></span>

<span data-ttu-id="38b04-155">Als u problemen met aanmelden met verificatie in twee stappen hebt, informatie op te krijgen [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="38b04-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="38b04-156">Meer informatie over hoe te[de instellingen van de verificatie in twee stappen beheren](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="38b04-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="38b04-157">Ontdek hoe u kunt te[aan de slag met Microsoft Authenticator-app Hallo](microsoft-authenticator-app-how-to.md) zodat u meldingen toosign in, in plaats van teksten en telefoongesprekken kunt.</span><span class="sxs-lookup"><span data-stu-id="38b04-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
