---
title: aaaHow toouse App-wachtwoorden in Azure MFA? | Microsoft Docs
description: Deze pagina helpt gebruikers begrijpen wat app-wachtwoorden zijn en wat ze worden gebruikt voor met inachtneming van tooAzure MFA.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="1c01b-104">Wat zijn App-wachtwoorden in Azure multi-factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="1c01b-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="1c01b-105">Bepaalde niet-browsertoepassingen, zoals Hallo Apple systeemeigen e-mailclient die gebruikmaakt van Exchange Active Sync, ondersteunen momenteel geen multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="1c01b-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="1c01b-106">Multi-factor authentication is ingeschakeld per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c01b-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="1c01b-107">Dit betekent dat een gebruiker multi-factor authentication-server niet gebruiken als:</span><span class="sxs-lookup"><span data-stu-id="1c01b-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="1c01b-108">Hallo-gebruiker is ingeschakeld voor multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="1c01b-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="1c01b-109">Hallo gebruiker probeert toouse een niet-browsertoepassing.</span><span class="sxs-lookup"><span data-stu-id="1c01b-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="1c01b-110">Een app-wachtwoord kunt Hallo gebruiker toouse Hallo app.</span><span class="sxs-lookup"><span data-stu-id="1c01b-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="1c01b-111">Zodra u een app-wachtwoord hebt, kunt u deze gebruiken in plaats van het oorspronkelijke wachtwoord met deze niet-browsertoepassingen.</span><span class="sxs-lookup"><span data-stu-id="1c01b-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="1c01b-112">Wanneer u zich voor verificatie in twee stappen registreert, u bent zorgt ervoor dat Microsoft niet toolet iedereen Meld u aan met uw wachtwoord als ze ook Hallo tweede verificatie niet kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1c01b-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="1c01b-113">Hallo Apple systeemeigen e-mailclient op uw telefoon kan niet aanmelden als u omdat deze kan niet om verificatie in twee stappen vragen.</span><span class="sxs-lookup"><span data-stu-id="1c01b-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="1c01b-114">Hallo oplossing toothis probleem is een veiligere app-wachtwoord die u niet gebruikt toocreate dagelijkse.</span><span class="sxs-lookup"><span data-stu-id="1c01b-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="1c01b-115">App-wachtwoorden zijn alleen voor apps die verificatie in twee stappen niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="1c01b-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="1c01b-116">Hallo app-wachtwoord gebruiken zodat apps kunnen multi-factor authentication overslaan en doorgaan toowork.</span><span class="sxs-lookup"><span data-stu-id="1c01b-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="1c01b-117">Office 2013-clients (inclusief Outlook) bieden ondersteuning voor nieuwe verificatieprotocollen en kan worden gebruikt met verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="1c01b-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="1c01b-118">App-wachtwoorden zijn niet vereist voor gebruik met Office 2013-clients.</span><span class="sxs-lookup"><span data-stu-id="1c01b-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="1c01b-119">Zie voor meer informatie [Office 2013 modern authentication openbare preview aangekondigd](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="1c01b-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="1c01b-120">Hoe toouse app-wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="1c01b-120">How toouse app passwords</span></span>
<span data-ttu-id="1c01b-121">Hier volgen enkele dingen tooknow over app-wachtwoorden:</span><span class="sxs-lookup"><span data-stu-id="1c01b-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="1c01b-122">U kunt uw eigen app-wachtwoorden niet maken.</span><span class="sxs-lookup"><span data-stu-id="1c01b-122">You don't create your own app passwords.</span></span> <span data-ttu-id="1c01b-123">Ze worden automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1c01b-123">They are automatically generated.</span></span>
* <span data-ttu-id="1c01b-124">Er is momenteel een limiet van 40 wachtwoorden per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c01b-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="1c01b-125">Als u een app-wachtwoord toocreate probeert Hallo limiet is bereikt, hebt u toodelete een van uw bestaande app-wachtwoorden voordat u een nieuwe maakt.</span><span class="sxs-lookup"><span data-stu-id="1c01b-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="1c01b-126">Gebruik één appwachtwoord per apparaat, niet per toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c01b-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="1c01b-127">U kunt bijvoorbeeld één app-wachtwoord voor uw laptop maken en dit app-wachtwoord gebruiken voor alle toepassingen op die laptop.</span><span class="sxs-lookup"><span data-stu-id="1c01b-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="1c01b-128">Maak vervolgens een tweede app-wachtwoord toouse voor al uw apps op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="1c01b-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="1c01b-129">Krijgt u een app-wachtwoord Hallo eerste keer dat u zich registreert voor verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="1c01b-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="1c01b-130">Als u aanvullende bepalingen nodig hebt, kunt u ze kunt maken.</span><span class="sxs-lookup"><span data-stu-id="1c01b-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="1c01b-131">Maken en het verwijderen van app-wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="1c01b-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="1c01b-132">Tijdens de eerste aanmelden krijgt u een app-wachtwoord die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c01b-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="1c01b-133">U kunt ook maken en verwijderen van app-wachtwoorden later op.</span><span class="sxs-lookup"><span data-stu-id="1c01b-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="1c01b-134">Hoe u app-wachtwoorden verwijderen, is afhankelijk van hoe u multi-factor authentication-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c01b-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="1c01b-135">Antwoord Hallo volgen vragen toodetermine waar u toomanage app-wachtwoorden moet gaan:</span><span class="sxs-lookup"><span data-stu-id="1c01b-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="1c01b-136">Gebruik je verificatie in twee stappen voor uw persoonlijke Microsoft-account?</span><span class="sxs-lookup"><span data-stu-id="1c01b-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="1c01b-137">Zo ja, raadpleegt u toohello [App-wachtwoorden en verificatie in twee stappen](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artikel voor hulp.</span><span class="sxs-lookup"><span data-stu-id="1c01b-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="1c01b-138">Zo Nee, blijven tooquestion twee.</span><span class="sxs-lookup"><span data-stu-id="1c01b-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="1c01b-139">OK, zodat u verificatie in twee stappen voor uw werk of school-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c01b-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="1c01b-140">Gebruik je deze toosign in tooOffice 365 apps?</span><span class="sxs-lookup"><span data-stu-id="1c01b-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="1c01b-141">Zo ja, raadpleegt u te[maken van een app-wachtwoord voor Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="1c01b-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="1c01b-142">Zo Nee, blijven tooquestion drie.</span><span class="sxs-lookup"><span data-stu-id="1c01b-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="1c01b-143">Gebruik je verificatie in twee stappen met Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="1c01b-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="1c01b-144">Zo ja, gaan toohello [beheren van appwachtwoorden in hello Azure-portal](#manage-app-passwords-in-the-Azure-portal) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1c01b-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="1c01b-145">Zo Nee, blijven tooquestion vier.</span><span class="sxs-lookup"><span data-stu-id="1c01b-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="1c01b-146">Weet u niet waar u verificatie in twee stappen gebruiken?</span><span class="sxs-lookup"><span data-stu-id="1c01b-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="1c01b-147">Doorgaan toohello [beheren van app-wachtwoorden met Hallo MyApps portal](#manage-app-passwords-with-the-myapps-portal) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1c01b-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="1c01b-148">App-wachtwoorden in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1c01b-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="1c01b-149">Als u verificatie in twee stappen met Azure gebruikt, u toocreate app-wachtwoorden via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c01b-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="1c01b-150">app-wachtwoorden toocreate in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="1c01b-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="1c01b-151">Meld u aan toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c01b-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="1c01b-152">Hallo boven aan met de rechtermuisknop op uw gebruikersnaam en aanvullende beveiligingsverificatie.</span><span class="sxs-lookup"><span data-stu-id="1c01b-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="1c01b-153">Selecteer op Hallo proofup pagina Hallo boven aan de app-wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="1c01b-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="1c01b-154">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-154">Click **Create**.</span></span>
5. <span data-ttu-id="1c01b-155">Voer een naam op voor Hallo app-wachtwoord en klik op **volgende**</span><span class="sxs-lookup"><span data-stu-id="1c01b-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="1c01b-156">Hallo app wachtwoord toohello Klembord kopiëren en plakken in uw app.</span><span class="sxs-lookup"><span data-stu-id="1c01b-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="1c01b-158">app-wachtwoorden toodelete in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="1c01b-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="1c01b-159">Meld u aan toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c01b-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="1c01b-160">Hallo boven aan met de rechtermuisknop op uw gebruikersnaam en aanvullende beveiligingsverificatie.</span><span class="sxs-lookup"><span data-stu-id="1c01b-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="1c01b-161">Selecteer boven hello, volgende tooadditional beveiligingsverificatie, **app-wachtwoorden.**</span><span class="sxs-lookup"><span data-stu-id="1c01b-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="1c01b-162">Volgende toohello app-wachtwoord gewenste toodelete, selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="1c01b-163">Hallo bevestigen door te klikken op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="1c01b-164">Zodra de app-wachtwoord Hallo zijn verwijderd, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="1c01b-165">App-wachtwoorden met Hallo MyApps portal beheren.</span><span class="sxs-lookup"><span data-stu-id="1c01b-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="1c01b-166">Als u niet zeker weet hoe u meervoudige verificatie gebruiken, kunt klikt u altijd maken en verwijderen van app-wachtwoorden via Hallo myapps portal.</span><span class="sxs-lookup"><span data-stu-id="1c01b-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="1c01b-167">een app-wachtwoord met toocreate Hallo Myapps portal</span><span class="sxs-lookup"><span data-stu-id="1c01b-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="1c01b-168">Aanmelden te[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="1c01b-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="1c01b-169">De naam van uw Hallo rechts bovenaan op en kies **profiel**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="1c01b-170">Selecteer **aanvullende beveiligingsverificatie**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="1c01b-171">![Selecteer aanvullende beveiligingsverificatie - schermafbeelding](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="1c01b-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="1c01b-172">Selecteer **app-wachtwoorden**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-172">Select **app passwords**.</span></span>
   <span data-ttu-id="1c01b-173">![Selecteer de app-wachtwoorden - schermafbeelding](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="1c01b-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="1c01b-174">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-174">Click **Create**.</span></span>
6. <span data-ttu-id="1c01b-175">Voer een naam op voor Hallo app-wachtwoord en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="1c01b-176">Hallo app wachtwoord toohello Klembord kopiëren en plakken in uw app.</span><span class="sxs-lookup"><span data-stu-id="1c01b-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="1c01b-177">![Een app-wachtwoord maken](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="1c01b-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="1c01b-178">een app-wachtwoord met toodelete Hallo Myapps portal</span><span class="sxs-lookup"><span data-stu-id="1c01b-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="1c01b-179">Aanmelden te[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="1c01b-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="1c01b-180">Selecteer boven Hallo profiel.</span><span class="sxs-lookup"><span data-stu-id="1c01b-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="1c01b-181">Selecteer **aanvullende beveiligingsverificatie**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-181">Select **Additional Security Verification**.</span></span>

   ![Selecteer aanvullende beveiligingsverificatie - schermafbeelding](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="1c01b-183">Selecteer **app-wachtwoorden**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-183">Select **app passwords**.</span></span>

   ![Selecteer de app-wachtwoorden - schermafbeelding](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="1c01b-185">Volgende toohello app-wachtwoord gewenste toodelete, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Verwijderen van een app-wachtwoord](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="1c01b-187">U wilt bevestigen dat toodelete dit wachtwoord door te klikken op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="1c01b-188">Zodra de app-wachtwoord Hallo zijn verwijderd, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="1c01b-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c01b-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c01b-189">Next steps</span></span>

- [<span data-ttu-id="1c01b-190">De instellingen van de verificatie in twee stappen beheren</span><span class="sxs-lookup"><span data-stu-id="1c01b-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="1c01b-191">Hallo uitproberen [Microsoft Authenticator-app](microsoft-authenticator-app-how-to.md) tooverify uw aanmeldingen met app-meldingen in plaats van de ontvangen tekst of aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1c01b-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
