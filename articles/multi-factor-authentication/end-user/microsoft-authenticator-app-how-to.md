---
title: Microsoft Authenticator-app voor mobiele telefoons | Microsoft Docs
description: Informatie over het upgraden naar de nieuwste versie van Azure Authenticator.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="8cd20-103">Aan de slag met de Microsoft Authenticator-app</span><span class="sxs-lookup"><span data-stu-id="8cd20-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="8cd20-104">De Microsoft Authenticator-app biedt een extra beveiligingsniveau in uw werk of school-account (bijvoorbeeld bsimon@contoso.com) of uw Microsoft-account (bijvoorbeeld bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="8cd20-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="8cd20-105">De app werkt op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="8cd20-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="8cd20-106">**Melding**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-106">**Notification**.</span></span> <span data-ttu-id="8cd20-107">De app kan helpen voorkomen dat onbevoegde toegang tot accounts en frauduleuze transacties stoppen door een melding naar uw smartphone of tablet worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="8cd20-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="8cd20-108">Gewoon de melding weergeven en als deze geldig is, selecteert u **controleren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="8cd20-109">Anders kunt u **weigeren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="8cd20-110">**Verificatiecode**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-110">**Verification code**.</span></span> <span data-ttu-id="8cd20-111">De app kan worden gebruikt als een Softwaretoken voor het genereren van een verificatiecode OAuth.</span><span class="sxs-lookup"><span data-stu-id="8cd20-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="8cd20-112">Nadat u uw gebruikersnaam en wachtwoord hebt ingevoerd, voert u de code die wordt geleverd door de app in het aanmeldingsscherm.</span><span class="sxs-lookup"><span data-stu-id="8cd20-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="8cd20-113">De verificatiecode biedt een tweede vorm van verificatie.</span><span class="sxs-lookup"><span data-stu-id="8cd20-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="8cd20-114">De Microsoft Authenticator-app wordt vervangen door de Azure Authenticator-app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="8cd20-115">De Azure Authenticator-app werkt nog altijd, maar als u besluit om naar de nieuwe Microsoft Authenticator-app te verplaatsen, in dit artikel kan u helpen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="8cd20-116">Opt-in voor verificatie in twee stappen</span><span class="sxs-lookup"><span data-stu-id="8cd20-116">Opt in for two-step verification</span></span>

<span data-ttu-id="8cd20-117">De Microsoft Authenticator-app werkt niet op zichzelf.</span><span class="sxs-lookup"><span data-stu-id="8cd20-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="8cd20-118">Elk van uw accounts vraagt u om een tweede verificatiemethode nadat u zich met uw gebruikersnaam en wachtwoord aanmelden configureren.</span><span class="sxs-lookup"><span data-stu-id="8cd20-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="8cd20-119">Om een werk- of schoolaccount krijgt u niet normaal gesproken kiest u deze functie voor uzelf.</span><span class="sxs-lookup"><span data-stu-id="8cd20-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="8cd20-120">In plaats daarvan een beveiligingsbeheerder kiest namens jou en verwittigt vervolgens registreren verificatiemethoden voor uw account.</span><span class="sxs-lookup"><span data-stu-id="8cd20-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="8cd20-121">Meer informatie in dit scenario is van toepassing op u, [wat Azure multi-factor Authentication betekent voor mij](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="8cd20-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="8cd20-122">Voor een persoonlijke account moet u de verificatie in twee stappen voor uzelf instellen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="8cd20-123">Als u een Microsoft-account hebt, deze stappen zijn beschikbaar in [over verificatie in twee stappen](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="8cd20-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="8cd20-124">U kunt ook de Microsoft-Authenticator gebruiken met niet-Microsoft-accounts.</span><span class="sxs-lookup"><span data-stu-id="8cd20-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="8cd20-125">Ze kunnen de functie iets anders dan verificatie in twee stappen aanroepen, maar moet u kunnen vinden onder beveiligings- of instellingen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="8cd20-126">De app installeren</span><span class="sxs-lookup"><span data-stu-id="8cd20-126">Install the app</span></span>
<span data-ttu-id="8cd20-127">De Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="8cd20-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="8cd20-128">Accounts toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-128">Add accounts to the app</span></span>
<span data-ttu-id="8cd20-129">Voor elke account die u wilt toevoegen aan de Microsoft Authenticator-app, gebruikt u een van de volgende procedures:</span><span class="sxs-lookup"><span data-stu-id="8cd20-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="8cd20-130">Een persoonlijk Microsoft-account toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="8cd20-131">Voor een persoonlijk Microsoft-account (één waarmee u zich aanmeldt bij Outlook.com, Xbox, Skype, enzovoort), is hoeft u zich aanmelden bij uw account in de Microsoft Authenticator-app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="8cd20-132">Een account voor werk of school toevoegen aan de app via de scanner QR-code</span><span class="sxs-lookup"><span data-stu-id="8cd20-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="8cd20-133">Ga naar het scherm beveiliging verificatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="8cd20-134">Zie voor informatie over hoe u naar dit scherm, [wijzigen van uw beveiligingsinstellingen](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="8cd20-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="8cd20-135">Schakel het selectievakje in naast **verificator-app** Selecteer **configureren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![De knop configureren op het scherm beveiliging verificatie-instellingen](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="8cd20-137">Hiermee wordt een scherm met een QR-code erop.</span><span class="sxs-lookup"><span data-stu-id="8cd20-137">This brings up a screen with a QR code on it.</span></span>

    ![Scherm waarmee de QR-code](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="8cd20-139">Open de Microsoft Authenticator-app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="8cd20-140">Op de **accounts** Schakel in het scherm  **+** , en geef vervolgens dat u wilt een werk- of schoolaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="8cd20-141">Gebruik van de camera moet scan de QR-code en selecteer vervolgens **gedaan** te sluiten van het scherm QR-code.</span><span class="sxs-lookup"><span data-stu-id="8cd20-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="8cd20-142">Als uw camera niet goed werkt is, kunt u [de QR-code en URL handmatig invoeren](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="8cd20-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="8cd20-143">Als de app wordt de naam van uw account een 6-cijferige code eronder weergegeven, kunt u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="8cd20-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Accounts scherm](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="8cd20-145">Een account handmatig toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="8cd20-146">Ga naar het scherm beveiliging verificatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="8cd20-147">Zie voor informatie over hoe u naar dit scherm, [wijzigen van uw beveiligingsinstellingen](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="8cd20-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="8cd20-148">Selecteer **configureren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-148">Select **Configure**.</span></span>

    ![De knop configureren op het scherm beveiliging verificatie-instellingen](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="8cd20-150">Hiermee wordt een scherm met een QR-code erop.</span><span class="sxs-lookup"><span data-stu-id="8cd20-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="8cd20-151">Noteer de code en URL.</span><span class="sxs-lookup"><span data-stu-id="8cd20-151">Note the code and URL.</span></span>

    ![Scherm waarmee de QR-code en URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="8cd20-153">Open de Microsoft Authenticator-app.</span><span class="sxs-lookup"><span data-stu-id="8cd20-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="8cd20-154">Op de **accounts** Schakel in het scherm  **+** , en geef vervolgens dat u wilt een werk- of schoolaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8cd20-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="8cd20-155">Selecteer in de scanner **code handmatig invoeren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-155">In the scanner, select **enter code manually**.</span></span>

    ![Scherm voor het scannen van QR-code](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="8cd20-157">Voer de code en de URL in de desbetreffende vakken in de app en selecteer **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Scherm voor het invoeren van code en URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="8cd20-159">Als de app wordt de naam van uw account een 6-cijferige code eronder weergegeven, kunt u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="8cd20-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Accounts scherm](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="8cd20-161">Een account toevoegen aan de app Touch ID gebruikt</span><span class="sxs-lookup"><span data-stu-id="8cd20-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="8cd20-162">De Microsoft Authenticator-app voor iOS ondersteunt Touch-ID.</span><span class="sxs-lookup"><span data-stu-id="8cd20-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="8cd20-163">Azure multi-factor Authentication kunnen organisaties een PINCODE vereisen voor apparaten.</span><span class="sxs-lookup"><span data-stu-id="8cd20-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="8cd20-164">Niet met Touch ID moeten iOS-gebruikers een PINCODE op te geven.</span><span class="sxs-lookup"><span data-stu-id="8cd20-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="8cd20-165">In plaats daarvan ze kunnen hun vingerafdruk scannen en selecteer **goedkeuren**.</span><span class="sxs-lookup"><span data-stu-id="8cd20-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="8cd20-166">Instellen van Touch ID met Microsoft Authenticator is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="8cd20-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="8cd20-167">Voltooi een challenge normale verificatie met een PINCODE.</span><span class="sxs-lookup"><span data-stu-id="8cd20-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="8cd20-168">Als uw apparaat Touch ID ondersteunt, stelt Microsoft Authenticator deze automatisch voor dat account.</span><span class="sxs-lookup"><span data-stu-id="8cd20-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Verificatie van Touch ID setup](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="8cd20-170">Vanaf dat punt doorsturen, wanneer u klaar om te controleren of uw aanmelden vereist, u de pushmelding ontvangen selecteren en scannen van uw vingerafdruk in plaats van uw pincode.</span><span class="sxs-lookup"><span data-stu-id="8cd20-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Push-melding](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="8cd20-172">De app gebruiken wanneer u zich aanmeldt</span><span class="sxs-lookup"><span data-stu-id="8cd20-172">Use the app when you sign in</span></span>

<span data-ttu-id="8cd20-173">Wanneer uw account is toegevoegd aan de app, wordt u mogelijk gevraagd te doen een testverificatie om te controleren of dat alles correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8cd20-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="8cd20-174">Daarna kunt bent nu u klaar!</span><span class="sxs-lookup"><span data-stu-id="8cd20-174">After that, you're done!</span></span> <span data-ttu-id="8cd20-175">U hoeft niet te iets anders doen totdat de volgende keer dat u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="8cd20-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="8cd20-176">Als u ervoor verificatie te gebruiken in de app kiest, start u deze op de startpagina te zien.</span><span class="sxs-lookup"><span data-stu-id="8cd20-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="8cd20-177">Ze wijzigen elke 30 seconden zodat u altijd een nieuwe code hebt wanneer u een nodig.</span><span class="sxs-lookup"><span data-stu-id="8cd20-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="8cd20-178">Maar u hoeft verder niets te doen met hen totdat u zich aanmeldt, wordt gevraagd een verificatiecode invoeren.</span><span class="sxs-lookup"><span data-stu-id="8cd20-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  