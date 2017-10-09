---
title: aaaGet de slag met Azure Notification Hubs die gebruikmaken van Baidu | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooAndroid apparaten gebruikmaken van Baidu.
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="aabc3-103">Aan de slag met Azure Notification Hubs die gebruikmaken van Baidu</span><span class="sxs-lookup"><span data-stu-id="aabc3-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="aabc3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="aabc3-104">Overview</span></span>
<span data-ttu-id="aabc3-105">Baidu cloud push is een Chinese cloudservice waarmee u toosend push notifications toomobile apparaten kunt.</span><span class="sxs-lookup"><span data-stu-id="aabc3-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="aabc3-106">Deze service is handig in China, waar leveren van pushmeldingen tooAndroid is complex vanwege Hallo aanwezigheid van verschillende app stores en push services, Daarnaast toohello beschikbaarheid van Android-apparaten die niet doorgaans verbonden tooGCM (Google zijn Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="aabc3-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aabc3-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aabc3-107">Prerequisites</span></span>
<span data-ttu-id="aabc3-108">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="aabc3-108">This tutorial requires:</span></span>

* <span data-ttu-id="aabc3-109">Android SDK (Aannemende dat u Eclipse gebruikt), die u via Hallo downloaden kunt <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a></span><span class="sxs-lookup"><span data-stu-id="aabc3-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="aabc3-110">[Android-SDK voor Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="aabc3-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="aabc3-111">[Android SDK Baidu Push]</span><span class="sxs-lookup"><span data-stu-id="aabc3-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="aabc3-112">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="aabc3-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="aabc3-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="aabc3-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aabc3-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aabc3-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="aabc3-115">Een Baidu-account maken</span><span class="sxs-lookup"><span data-stu-id="aabc3-115">Create a Baidu account</span></span>
<span data-ttu-id="aabc3-116">toouse Baidu, moet u een Baidu-account hebben.</span><span class="sxs-lookup"><span data-stu-id="aabc3-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="aabc3-117">Als u al hebt, meldt u zich in toohello [Baidu portal] en toohello volgende stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="aabc3-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="aabc3-118">Raadpleeg anders Hallo instructies te volgen over het toocreate een Baidu-account.</span><span class="sxs-lookup"><span data-stu-id="aabc3-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="aabc3-119">Ga toohello [Baidu portal] en klik op Hallo**登录**(**aanmelding**) koppelen.</span><span class="sxs-lookup"><span data-stu-id="aabc3-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="aabc3-120">Klik op**立即注册**toostart Hallo account registratieproces.</span><span class="sxs-lookup"><span data-stu-id="aabc3-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="aabc3-121">Voer details voor Hallo vereist: telefoon, e-mailadres, wachtwoord en verificatiecode, en klik op **aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="aabc3-122">U ontvangt een e-mailadres toohello e-mailadres dat u hebt ingevoerd met een koppeling tooactivate uw Baidu-account.</span><span class="sxs-lookup"><span data-stu-id="aabc3-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="aabc3-123">Aanmelden tooyour e-mailaccount, open Hallo e-mailbericht en op Hallo activering koppeling tooactivate uw Baidu-account.</span><span class="sxs-lookup"><span data-stu-id="aabc3-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="aabc3-124">Zodra u een geactiveerde Baidu-account hebt, meld u bij toohello [Baidu portal].</span><span class="sxs-lookup"><span data-stu-id="aabc3-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="aabc3-125">Registreer u als een Baidu-ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="aabc3-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="aabc3-126">Zodra u zich hebt aangemeld toohello [Baidu portal], klikt u op**更多 >>** (**meer**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="aabc3-127">Schuif omlaag in Hallo**站长与开发者服务 (webbeheerder en Ontwikkelaarsservices)** sectie en klik op**百度开放云平台**(**Baidu cloud-platform open**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="aabc3-128">Klik op volgende pagina Hallo**开发者服务**(**Ontwikkelaarsservices**) in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="aabc3-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="aabc3-129">Klik op volgende pagina Hallo**注册开发者**(**ontwikkelaars geregistreerd**) in Hallo-menu op Hallo rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="aabc3-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="aabc3-130">Voer uw naam, een beschrijving en een mobiel telefoonnummer in voor het ontvangen van een sms-bericht voor verificatie en klik vervolgens op **送验证码** (**Verificatiecode verzenden**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="aabc3-131">Internationaal telefoonnummer moet u tooenclose Hallo landcode tussen haakjes.</span><span class="sxs-lookup"><span data-stu-id="aabc3-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="aabc3-132">Voor een nummer in de Verenigde Staten moet u bijvoorbeeld de volgende indeling gebruiken: **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="aabc3-133">U ontvangt vervolgens een SMS-bericht met een verificatiecode, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="aabc3-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="aabc3-134">Voer de verificatiecode Hallo van Hallo-bericht in**验证码**(**bevestigingscode**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="aabc3-135">Voltooi ten slotte Hallo developer registratie door Hallo Baidu overeenkomst te accepteren en te klikken**提交**(**indienen**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="aabc3-136">Hier ziet u Hallo volgende pagina van de registratie is gelukt:</span><span class="sxs-lookup"><span data-stu-id="aabc3-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="aabc3-137">Een Baidu-cloudpushproject maken</span><span class="sxs-lookup"><span data-stu-id="aabc3-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="aabc3-138">Als u een Baidu-cloudpushproject maakt, ontvangt u uw app-id, API-sleutel en een geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="aabc3-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="aabc3-139">Zodra u zich hebt aangemeld toohello [Baidu portal], klikt u op**更多 >>** (**meer**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="aabc3-140">Schuif omlaag in Hallo**站长与开发者服务**(**webbeheerder en Ontwikkelaarsservices**) sectie en klik op**百度开放云平台**(**Baidu cloud-platform open**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="aabc3-141">Klik op volgende pagina Hallo**开发者服务**(**Ontwikkelaarsservices**) in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="aabc3-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="aabc3-142">Klik op volgende pagina Hallo**云推送**(**Cloud Push**) van Hallo**云服务**(**Cloudservices**) sectie.</span><span class="sxs-lookup"><span data-stu-id="aabc3-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="aabc3-143">Nadat u een geregistreerde ontwikkelaar bent, ziet u**管理控制台**(**beheerconsole**) op het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="aabc3-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="aabc3-144">Klik op **开发者服务管理** (**Beheer van ontwikkelaarsservices**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="aabc3-145">Klik op volgende pagina Hallo**创建工程**(**Project maken**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="aabc3-146">Voer een toepassingsnaam in en klik op **创建** (**Maken**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="aabc3-147">Als u een Baidu Cloud Push-project hebt gemaakt, ziet u een pagina met de **App-id**, de **API-sleutel** en een **geheime sleutel**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="aabc3-148">Maak een notitie van Hallo API-sleutel en geheime sleutel, die we later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aabc3-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="aabc3-149">Hallo-project voor pushmeldingen configureren door te klikken op**云推送**(**Cloud Push**) in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="aabc3-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="aabc3-150">Klik op volgende pagina Hallo Hallo**推送设置**(**Push instellingen**) knop.</span><span class="sxs-lookup"><span data-stu-id="aabc3-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="aabc3-151">Toevoegen op de configuratiepagina Hallo Hallo pakketnaam die u in uw Android-project in Hallo gebruiken wilt**应用包名**(**toepassingspakket**) en klik vervolgens op**保存设置**() **Opslaan**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="aabc3-152">U ziet Hallo**保存成功!** (**Opgeslagen!**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="aabc3-153">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="aabc3-153">Configure your notification hub</span></span>
1. <span data-ttu-id="aabc3-154">Meld u aan toohello [klassieke Azure-Portal], en klik vervolgens op **+ nieuw** Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="aabc3-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="aabc3-155">Klik achtereenvolgens op **App Services**, **Service Bus**, **Notification Hub** en **Snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="aabc3-156">Geef een naam voor uw **Notification Hub**, selecteer Hallo **regio** en Hallo **Namespace** waar deze notification hub wordt gemaakt en klik vervolgens op  **Maak een nieuwe Notification Hub**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="aabc3-157">Klik op Hallo naamruimte waarin u uw notification hub hebt gemaakt en klik vervolgens op **Notification Hubs** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="aabc3-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="aabc3-158">Selecteer Hallo notification hub die u gemaakt en klik vervolgens op **configureren** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="aabc3-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="aabc3-159">Schuif omlaag toohello **baidu meldingsinstellingen** sectie en Voer Hallo API-sleutel en geheime sleutel die u hebt verkregen via de Baidu-console Hallo eerder voor uw Baidu-cloudpushproject.</span><span class="sxs-lookup"><span data-stu-id="aabc3-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="aabc3-160">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="aabc3-161">Klik op Hallo **Dashboard** tabblad boven Hallo voor Hallo notification hub en klik vervolgens op **verbindingsreeks weergeven**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="aabc3-162">Maak een notitie van Hallo **DefaultListenSharedAccessSignature** en **DefaultFullSharedAccessSignature** van Hallo **toegang tot verbindingsgegevens** venster.</span><span class="sxs-lookup"><span data-stu-id="aabc3-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="aabc3-163">Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="aabc3-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="aabc3-164">Maak in Eclipse ADT een nieuw Android-project (**Bestand** > **Nieuw** > **Android-toepassingsproject**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="aabc3-165">Voer een **toepassingsnaam** en zorg ervoor dat Hallo **minimale vereiste SDK** -versie is ingesteld, te**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="aabc3-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="aabc3-166">Klik op **volgende** en doorgaan na Hallo wizard totdat Hallo **activiteit maken** venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aabc3-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="aabc3-167">Zorg ervoor dat **Blank Activity** is geselecteerd en selecteer vervolgens **voltooien** toocreate een nieuwe Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aabc3-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="aabc3-168">Zorg ervoor dat Hallo **doel van de Projectbuild** correct is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="aabc3-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="aabc3-169">Hallo notification-hubs-0.4.jar bestand downloaden van Hallo **bestanden** tabblad Hallo [Notification-Hubs-Android-SDK op Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="aabc3-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="aabc3-170">Toevoegen van Hallo bestand toohello **bibliotheken** map van uw Eclipse-project en vernieuw Hallo *bibliotheken* map.</span><span class="sxs-lookup"><span data-stu-id="aabc3-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="aabc3-171">Downloaden en uitpakken Hallo [Android SDK Baidu Push]Open Hallo **bibliotheken** map en kopieer Hallo **pushservice x.y.z** jar-bestand en Hallo **armeabi**  &  **mips** mappen in Hallo **bibliotheken** map van uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aabc3-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="aabc3-172">Open Hallo **AndroidManifest.xml** -bestand van uw Android-project en Hallo machtigingen die door Hallo SDK Baidu vereist zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aabc3-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="aabc3-173">Hallo toevoegen **android: name** eigenschap tooyour **toepassing** -element in **AndroidManifest.xml**en vervang *yourprojectname* (voor voorbeeld **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="aabc3-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="aabc3-174">Zorg ervoor dat deze naam overeenkomt met Hallo een die u hebt geconfigureerd in Hallo Baidu-console.</span><span class="sxs-lookup"><span data-stu-id="aabc3-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="aabc3-175">Hallo na binnen Hallo toepassingselement na Hallo configuratie toevoegen **. MainActivity** activiteit element vervangen *yourprojectname* (bijvoorbeeld **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="aabc3-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="aabc3-176">Voeg een nieuwe klasse aangeroepen **ConfigurationSettings.java** toohello project.</span><span class="sxs-lookup"><span data-stu-id="aabc3-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="aabc3-177">Hallo code tooit volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="aabc3-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="aabc3-178">Stel de waarde Hallo van **API_KEY** met wat u eerder hebt opgehaald uit de Baidu-cloudproject hello, **NotificationHubName** met de naam van uw notification hub van Hallo klassieke Azure-Portal en  **NotificationHubConnectionString** defaultlistensharedaccesssignature op van Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="aabc3-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="aabc3-179">Voeg een nieuwe klasse aangeroepen **DemoApplication.java**, en voeg Hallo code tooit te volgen:</span><span class="sxs-lookup"><span data-stu-id="aabc3-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="aabc3-180">Toevoegen van een andere nieuwe klasse met de naam **MyPushMessageReceiver.java**, en voeg Hallo code tooit te volgen.</span><span class="sxs-lookup"><span data-stu-id="aabc3-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="aabc3-181">Het is Hallo-klasse die ingangen Hallo pushmeldingen die afkomstig zijn van Hallo Baidu push-server.</span><span class="sxs-lookup"><span data-stu-id="aabc3-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="aabc3-182">Open **MainActivity.java**, en Voeg na toohello hello **onCreate** methode:</span><span class="sxs-lookup"><span data-stu-id="aabc3-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="aabc3-183">Open de volgende importinstructies boven Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="aabc3-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="aabc3-184">Meldingen tooyour app verzenden</span><span class="sxs-lookup"><span data-stu-id="aabc3-184">Send notifications tooyour app</span></span>
<span data-ttu-id="aabc3-185">U kunt snel testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [Azure-portal](https://portal.azure.com/) met Hallo **verzenden** knop op Hallo notification hub, zoals weergegeven in het volgende scherm Hallo:</span><span class="sxs-lookup"><span data-stu-id="aabc3-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="aabc3-186">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="aabc3-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="aabc3-187">Als een bibliotheek niet beschikbaar voor uw back-end is, kunt u Hallo REST-API toosend meldingen worden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="aabc3-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="aabc3-188">In deze zelfstudie we Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden.</span><span class="sxs-lookup"><span data-stu-id="aabc3-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="aabc3-189">We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="aabc3-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="aabc3-190">Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:</span><span class="sxs-lookup"><span data-stu-id="aabc3-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="aabc3-191">**REST-Interface**: U kunt meldingen ondersteunen op elk back-end-platform Hallo met [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="aabc3-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="aabc3-192">**Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="aabc3-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="aabc3-193">**Node.js**: [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="aabc3-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="aabc3-194">**Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een back-end voor een Azure App Service Mobile Apps die geïntegreerd met Notification Hubs toosend Zie [Add push notifications tooyour mobiele app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="aabc3-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="aabc3-195">**Java / PHP**: Zie voor een voorbeeld van hoe toosend meldingen met REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="aabc3-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="aabc3-196">(Optioneel) Meldingen verzenden vanuit een .NET-console-app</span><span class="sxs-lookup"><span data-stu-id="aabc3-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="aabc3-197">In dit gedeelte behandelen we hoe u een melding vanuit een .NET-console-app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="aabc3-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="aabc3-198">Maak een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="aabc3-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="aabc3-199">In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="aabc3-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="aabc3-200">Deze instructie een verwijzing toohello Azure Notification Hubs SDK wordt toegevoegd met behulp van Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="aabc3-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="aabc3-201">Open Hallo bestand **Program.cs** en voeg de volgende Hallo toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="aabc3-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="aabc3-202">In uw `Program` klasse Hallo volgende methode toe en vervang *DefaultFullSharedAccessSignatureSASConnectionString* en *NotificationHubName* met Hallo-waarden die u hebt.</span><span class="sxs-lookup"><span data-stu-id="aabc3-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="aabc3-203">Toevoegen van de volgende regels in Hallo uw **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="aabc3-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="aabc3-204">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="aabc3-204">Test your app</span></span>
<span data-ttu-id="aabc3-205">Deze app met een telefoon, alleen verbinding tootest Hallo phone tooyour computer via een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="aabc3-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="aabc3-206">Deze actie wordt uw app naar Hallo gekoppelde telefoon geladen.</span><span class="sxs-lookup"><span data-stu-id="aabc3-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="aabc3-207">tootest deze app met Hallo-emulator op de bovenste werkbalk van Hallo Eclipse, klikt u op **uitvoeren**, en selecteer vervolgens uw app: het Hallo-emulator is geladen wordt gestart en wordt uitgevoerd Hallo app.</span><span class="sxs-lookup"><span data-stu-id="aabc3-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="aabc3-208">Hallo app Hallo 'userId' en 'channelId' opgehaald uit Hallo Baidu Push notification service en voor Hallo notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aabc3-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="aabc3-209">een Testmelding toosend, kunt u het foutopsporingstabblad Hallo Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="aabc3-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="aabc3-210">Als u gebouwd Hallo .NET-consoletoepassing voor Visual Studio, druk op F5-toets Hallo in Visual Studio toorun Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="aabc3-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="aabc3-211">de toepassing Hello stuurt een melding die wordt weergegeven in de bovenste systeemvak Hallo van uw apparaat of emulator.</span><span class="sxs-lookup"><span data-stu-id="aabc3-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Android-SDK voor Mobile Services]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Android SDK Baidu Push]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[klassieke Azure-Portal]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
