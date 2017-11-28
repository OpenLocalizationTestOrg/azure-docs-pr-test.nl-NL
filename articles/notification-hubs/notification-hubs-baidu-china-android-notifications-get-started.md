---
title: Aan de slag met Notification Hubs die gebruikmaken van Baidu | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar Android-apparaten die gebruikmaken van Baidu.
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
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="f921e-103">Aan de slag met Azure Notification Hubs die gebruikmaken van Baidu</span><span class="sxs-lookup"><span data-stu-id="f921e-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f921e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f921e-104">Overview</span></span>
<span data-ttu-id="f921e-105">Baidu Cloud Push is een Chinese cloudservice waarmee u pushmeldingen naar mobiele apparaten kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="f921e-105">Baidu cloud push is a Chinese cloud service that you can use to send push notifications to mobile devices.</span></span> <span data-ttu-id="f921e-106">Deze service is handig in China, omdat het leveren van pushmeldingen aan Android daar complex is vanwege de aanwezigheid van verschillende app stores en pushservices. Bovendien zijn er Android-apparaten die niet standaard verbonden zijn met GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="f921e-106">This service is useful in China, where delivering push notifications to Android is complex because of the presence of different app stores and push services, in addition to the availability of Android devices that are not typically connected to GCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f921e-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f921e-107">Prerequisites</span></span>
<span data-ttu-id="f921e-108">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="f921e-108">This tutorial requires:</span></span>

* <span data-ttu-id="f921e-109">Android-SDK (aannemende dat u Eclipse gebruikt), die u kunt downloaden van de <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a></span><span class="sxs-lookup"><span data-stu-id="f921e-109">Android SDK (we assume that you use Eclipse), which you can download from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="f921e-110">[Android-SDK voor Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="f921e-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="f921e-111">[Android SDK Baidu Push]</span><span class="sxs-lookup"><span data-stu-id="f921e-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="f921e-112">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f921e-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f921e-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="f921e-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f921e-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f921e-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="f921e-115">Een Baidu-account maken</span><span class="sxs-lookup"><span data-stu-id="f921e-115">Create a Baidu account</span></span>
<span data-ttu-id="f921e-116">Voor het gebruik van Baidu moet u een Baidu-account hebben.</span><span class="sxs-lookup"><span data-stu-id="f921e-116">To use Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="f921e-117">Als u er al een hebt, meldt u zich aan bij de [Baidu Portal] en gaat u verder met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="f921e-117">If you already have one, log in to the [Baidu portal] and skip to the next step.</span></span> <span data-ttu-id="f921e-118">Als u nog geen account hebt, raadpleegt u de instructies hieronder voor het maken van een Baidu-account.</span><span class="sxs-lookup"><span data-stu-id="f921e-118">Otherwise, see the following instructions on how to create a Baidu account.</span></span>  

1. <span data-ttu-id="f921e-119">Ga naar de [Baidu Portal] en klik op de koppeling **登录** (**Aanmelden**).</span><span class="sxs-lookup"><span data-stu-id="f921e-119">Go to the [Baidu portal] and click the **登录** (**Login**) link.</span></span> <span data-ttu-id="f921e-120">Klik op **立即注册** om de registratie van het account te starten.</span><span class="sxs-lookup"><span data-stu-id="f921e-120">Click **立即注册** to start the account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="f921e-121">Voer de vereiste gegevens in: telefoon, e-mailadres, wachtwoord en verificatiecode en klik vervolgens op **Registreren**.</span><span class="sxs-lookup"><span data-stu-id="f921e-121">Enter the required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="f921e-122">U ontvangt een e-mailbericht op het e-mailadres dat u hebt ingevoerd met daarin een koppeling om uw Baidu-account te activeren.</span><span class="sxs-lookup"><span data-stu-id="f921e-122">You will be sent an email to the email address that you entered with a link to activate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="f921e-123">Meld u aan bij uw e-mailaccount, open het e-mailbericht en klik op de activeringskoppeling om uw Baidu-account te activeren.</span><span class="sxs-lookup"><span data-stu-id="f921e-123">Log in to your email account, open the Baidu activation mail, and click the activation link to activate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="f921e-124">Als uw Baidu-account is geactiveerd, meldt u zich aan bij de [Baidu Portal].</span><span class="sxs-lookup"><span data-stu-id="f921e-124">Once you have an activated Baidu account, log in to the [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="f921e-125">Registreer u als een Baidu-ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="f921e-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="f921e-126">Nadat u zich hebt aangemeld bij de [Baidu Portal], klikt u op **更多 >>** (**meer**).</span><span class="sxs-lookup"><span data-stu-id="f921e-126">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="f921e-127">Schuif omlaag in het gedeelte **站长与开发者服务 (Webmaster- en Ontwikkelaarsservices)** en klik op **百度开放云平台** (**Baidu-opencloudplatform**).</span><span class="sxs-lookup"><span data-stu-id="f921e-127">Scroll down in the **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="f921e-128">Klik op de volgende pagina op **开发者服务** (**Ontwikkelaarsservices**) in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="f921e-128">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="f921e-129">Klik op de volgende pagina op **注册开发者** (**Geregistreerde ontwikkelaars**) in het menu in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="f921e-129">On the next page, click **注册开发者** (**Registered Developers**) from the menu on the top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="f921e-130">Voer uw naam, een beschrijving en een mobiel telefoonnummer in voor het ontvangen van een sms-bericht voor verificatie en klik vervolgens op **送验证码** (**Verificatiecode verzenden**).</span><span class="sxs-lookup"><span data-stu-id="f921e-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="f921e-131">Voor een internationaal telefoonnummer moet u de landcode tussen haakjes plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f921e-131">For international phone numbers, you need to enclose the country code in parentheses.</span></span> <span data-ttu-id="f921e-132">Voor een nummer in de Verenigde Staten moet u bijvoorbeeld de volgende indeling gebruiken: **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="f921e-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="f921e-133">U ontvangt vervolgens een sms-bericht met een verificatiecode, zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f921e-133">You should then receive a text message with a verification number, as shown in the following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="f921e-134">Voer de verificatiecode uit het sms-bericht in **验证码** (**Bevestigingscode**) in.</span><span class="sxs-lookup"><span data-stu-id="f921e-134">Enter the verification number from the message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="f921e-135">Voltooi de registratie voor ontwikkelaars door de Baidu-overeenkomst te accepteren en te klikken op **提交** (**Verzenden**).</span><span class="sxs-lookup"><span data-stu-id="f921e-135">Finally, complete the developer registration by accepting the Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="f921e-136">Als de registratie is gelukt, verschijnt de volgende pagina:</span><span class="sxs-lookup"><span data-stu-id="f921e-136">You will see the following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="f921e-137">Een Baidu-cloudpushproject maken</span><span class="sxs-lookup"><span data-stu-id="f921e-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="f921e-138">Als u een Baidu-cloudpushproject maakt, ontvangt u uw app-id, API-sleutel en een geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="f921e-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="f921e-139">Nadat u zich hebt aangemeld bij de [Baidu Portal], klikt u op **更多 >>** (**meer**).</span><span class="sxs-lookup"><span data-stu-id="f921e-139">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="f921e-140">Schuif omlaag in het gedeelte **站长与开发者服务** (**Webmaster- en Ontwikkelaarsservices)** en klik op **百度开放云平台** (**Baidu-opencloudplatform**).</span><span class="sxs-lookup"><span data-stu-id="f921e-140">Scroll down in the **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="f921e-141">Klik op de volgende pagina op **开发者服务** (**Ontwikkelaarsservices**) in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="f921e-141">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="f921e-142">Klik op de volgende pagina op **云推送** (**Cloud Push**) in het gedeelte **云服务** (**Cloud Services**).</span><span class="sxs-lookup"><span data-stu-id="f921e-142">On the next page, click **云推送** (**Cloud Push**) from the **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="f921e-143">Als u zich hebt geregistreerd als ontwikkelaar, ziet u **管理控制台** (**Beheerconsole**) in het bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="f921e-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at the top menu.</span></span> <span data-ttu-id="f921e-144">Klik op **开发者服务管理** (**Beheer van ontwikkelaarsservices**).</span><span class="sxs-lookup"><span data-stu-id="f921e-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="f921e-145">Klik op de volgende pagina **创建工程** (**Project maken**).</span><span class="sxs-lookup"><span data-stu-id="f921e-145">On the next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="f921e-146">Voer een toepassingsnaam in en klik op **创建** (**Maken**).</span><span class="sxs-lookup"><span data-stu-id="f921e-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="f921e-147">Als u een Baidu Cloud Push-project hebt gemaakt, ziet u een pagina met de **App-id**, de **API-sleutel** en een **geheime sleutel**.</span><span class="sxs-lookup"><span data-stu-id="f921e-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="f921e-148">Noteer de API-sleutel en de geheime sleutel. U hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="f921e-148">Make a note of the API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="f921e-149">Configureer het project voor pushmeldingen door te klikken op **云推送** (**Cloud Push**) in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f921e-149">Configure the project for push notifications by clicking **云推送** (**Cloud Push**) on the left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="f921e-150">Klik op de volgende pagina op de knop **推送设置** (**Pushinstellingen**).</span><span class="sxs-lookup"><span data-stu-id="f921e-150">On the next page, click the **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="f921e-151">Voeg op de configuratiepagina de pakketnaam toe die u wilt gebruiken in uw Android-project in het veld **应用包名** (**Toepassingspakket**) en klik vervolgens op **保存设置** (**Opslaan**).</span><span class="sxs-lookup"><span data-stu-id="f921e-151">On the configuration page, add the package name that you will be using in your Android project in the **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="f921e-152">U ziet het bericht **保存成功！** (**Opgeslagen!**).</span><span class="sxs-lookup"><span data-stu-id="f921e-152">You see the **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="f921e-153">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="f921e-153">Configure your notification hub</span></span>
1. <span data-ttu-id="f921e-154">Meld u aan bij de [Klassieke Azure Portal] en klik op **+NIEUW** onder aan het scherm.</span><span class="sxs-lookup"><span data-stu-id="f921e-154">Sign in to the [Azure Classic Portal], and then click **+NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="f921e-155">Klik achtereenvolgens op **App Services**, **Service Bus**, **Notification Hub** en **Snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="f921e-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="f921e-156">Geef een naam op voor uw **Notification Hub**, selecteer de **regio** en de **naamruimte** waar deze Notification Hub wordt gemaakt en klik vervolgens op **Een nieuwe Notification Hub maken**.</span><span class="sxs-lookup"><span data-stu-id="f921e-156">Provide a name for your **Notification Hub**, select the **Region** and the **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="f921e-157">Klik op de naamruimte waarin u de Notification Hub hebt gemaakt en klik vervolgens op **Notification Hubs** bovenin.</span><span class="sxs-lookup"><span data-stu-id="f921e-157">Click the namespace in which you created your notification hub, and then click **Notification Hubs** at the top.</span></span>
   
      ![][18]
5. <span data-ttu-id="f921e-158">Selecteer de Notification Hub die u hebt gemaakt en klik vervolgens op **Configureren** in het bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="f921e-158">Select the notification hub that you created, and then click **Configure** from the top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="f921e-159">Schuif omlaag naar het gedeelte **Baidu-instellingen voor meldingen** en voer voor uw Baidu-cloudpushproject de API-sleutel en de geheime sleutel in die u eerder van de Baidu-console hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f921e-159">Scroll down to the **baidu notification settings** section and enter the API key and secret key that you obtained from the Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="f921e-160">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f921e-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="f921e-161">Klik op het tabblad **Dashboard** in de rechterbovenhoek van de Notification Hub en klik vervolgens op **Verbindingsreeks weergeven**.</span><span class="sxs-lookup"><span data-stu-id="f921e-161">Click the **Dashboard** tab at the top for the notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="f921e-162">Noteer de **DefaultListenSharedAccessSignature** en **DefaultFullSharedAccessSignature** in het venster **Toegang tot de verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="f921e-162">Make a note of the **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from the **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="f921e-163">Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="f921e-163">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="f921e-164">Maak in Eclipse ADT een nieuw Android-project (**Bestand** > **Nieuw** > **Android-toepassingsproject**).</span><span class="sxs-lookup"><span data-stu-id="f921e-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="f921e-165">Voer een **toepassingsnaam** in en zorg ervoor dat de **minimale vereiste SDK**-versie is ingesteld op **API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="f921e-165">Enter an **Application Name** and ensure that the **Minimum Required SDK** version is set to **API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="f921e-166">Klik op **Volgende** en doorloop de wizard totdat het venster **Activiteit maken** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f921e-166">Click **Next** and continue following the wizard until the **Create Activity** window appears.</span></span> <span data-ttu-id="f921e-167">Zorg ervoor dat **Lege activiteit** is geselecteerd en selecteer vervolgens **Voltooien** om een nieuwe Android-toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="f921e-167">Make sure that **Blank Activity** is selected, and finally select **Finish** to create a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="f921e-168">Zorg ervoor dat het **doel van de projectbuild** juist is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f921e-168">Make sure that the **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="f921e-169">Download het bestand notification-hubs-0.4.jar van het tabblad **Bestanden** van de [Notification-Hubs-Android-SDK op Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="f921e-169">Download the notification-hubs-0.4.jar file from the **Files** tab of the [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="f921e-170">Voeg het bestand toe aan de map **bibliotheken** van uw Eclipse-project en vernieuw de map *bibliotheken*.</span><span class="sxs-lookup"><span data-stu-id="f921e-170">Add the file to the **libs** folder of your Eclipse project, and refresh the *libs* folder.</span></span>
6. <span data-ttu-id="f921e-171">Download de [Android SDK Baidu Push] en pak deze uit. Open de map **bibliotheken** en kopieer het **pushservice x.y.z** jar-bestand en de **armeabi** & **mips**-mappen in de map **bibliotheken** van uw Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f921e-171">Download and unzip the [Baidu Push Android SDK], open the **libs** folder, and then copy the **pushservice-x.y.z** jar file and the **armeabi** & **mips** folders in the **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="f921e-172">Open het bestand **AndroidManifest.xml** van uw Android-project en voeg de machtigingen toe die voor de SDK Baidu zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="f921e-172">Open the **AndroidManifest.xml** file of your Android project and add the permissions that are required by the Baidu SDK.</span></span>
   
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
8. <span data-ttu-id="f921e-173">Voeg de eigenschap **android:name** toe aan uw **toepassings**element in **AndroidManifest.xml**, waarbij u *yourprojectname* (bijvoorbeeld **com.example.BaiduTest**) vervangt.</span><span class="sxs-lookup"><span data-stu-id="f921e-173">Add the **android:name** property to your **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="f921e-174">Zorg ervoor dat deze naam overeenkomt met de naam die u in de Baidu-console hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f921e-174">Make sure that this project name matches the one that you configured in the Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="f921e-175">Voeg de volgende configuratie toe aan het toepassingselement na het activiteitelement **.MainActivity**, waarbij u *yourprojectname* (bijvoorbeeld **com.example.BaiduTest**) vervangt:</span><span class="sxs-lookup"><span data-stu-id="f921e-175">Add the following configuration within the application element after the **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
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
10. <span data-ttu-id="f921e-176">Voeg een nieuwe klasse met de naam **ConfigurationSettings.java** toe aan het project.</span><span class="sxs-lookup"><span data-stu-id="f921e-176">Add a new class called **ConfigurationSettings.java** to the project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="f921e-177">Voeg de volgende code toe aan de klasse:</span><span class="sxs-lookup"><span data-stu-id="f921e-177">Add the following code to it:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="f921e-178">Stel de waarde van **API_KEY** in op de waarde die u eerder hebt opgehaald uit het Baidu-cloudproject, geef voor **NotificationHubName** de naam op van de Notification Hub van de klassieke Azure Portal en geef voor **NotificationHubConnectionString** DefaultListenSharedAccessSignature op van de klassieke Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f921e-178">Set the value of **API_KEY** with what you retrieved from the Baidu cloud project earlier, **NotificationHubName** with your notification hub name from the Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from the Azure Classic Portal.</span></span>
12. <span data-ttu-id="f921e-179">Voeg een nieuwe klasse toe met de naam **DemoApplication.java** en voeg de volgende code toe:</span><span class="sxs-lookup"><span data-stu-id="f921e-179">Add a new class called **DemoApplication.java**, and add the following code to it:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="f921e-180">Voeg nog een nieuwe klasse toe met de naam **MyPushMessageReceiver.java** en voeg de volgende code eraan toe.</span><span class="sxs-lookup"><span data-stu-id="f921e-180">Add another new class called **MyPushMessageReceiver.java**, and add the following code to it.</span></span> <span data-ttu-id="f921e-181">Dit is de klasse die verantwoordelijk is voor de pushmeldingen die worden ontvangen van de Baidu-pushserver.</span><span class="sxs-lookup"><span data-stu-id="f921e-181">It is the class that handles the push notifications that are received from the Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
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
14. <span data-ttu-id="f921e-182">Open **MainActivity.java** en voeg het volgende toe aan de methode **onCreate**:</span><span class="sxs-lookup"><span data-stu-id="f921e-182">Open **MainActivity.java**, and add the following to the **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="f921e-183">Open bovenin de volgende importinstructies:</span><span class="sxs-lookup"><span data-stu-id="f921e-183">Open the following import statements at the top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a><span data-ttu-id="f921e-184">Pushmeldingen naar uw app verzenden</span><span class="sxs-lookup"><span data-stu-id="f921e-184">Send notifications to your app</span></span>
<span data-ttu-id="f921e-185">U kunt de ontvangst van meldingen in uw app snel testen door in [Azure Portal](https://portal.azure.com/) meldingen te verzenden met behulp van de knop **Verzenden** in de Notification Hub, zoals in het volgende scherm wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f921e-185">You can quickly test receiving notifications in your app by sending notifications in the [Azure portal](https://portal.azure.com/) using the **Send** button on the notification hub, as shown in the following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="f921e-186">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="f921e-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="f921e-187">U kunt de REST API ook rechtstreeks gebruiken om meldingsberichten te verzenden als er geen bibliotheek beschikbaar is voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="f921e-187">If a library is not available for your back-end, you can use the REST API directly to send notification messages .</span></span>

<span data-ttu-id="f921e-188">In deze zelfstudie houden we het eenvoudig en wordt alleen gedemonstreerd hoe u uw client-app test door meldingen te verzenden met de .NET SDK voor Notification Hubs in een consoletoepassing in plaats van een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="f921e-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="f921e-189">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) doornemen voor informatie over het verzenden van meldingen vanuit een ASP.NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="f921e-189">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="f921e-190">Voor het verzenden van meldingen kunt u echter de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f921e-190">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="f921e-191">**REST-interface**: u kunt meldingen op elk back-endplatform ondersteunen met de [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="f921e-191">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="f921e-192">**Microsoft Azure Notification Hubs .NET SDK**: in NuGet Package Manager voor Visual Studio voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) uit.</span><span class="sxs-lookup"><span data-stu-id="f921e-192">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="f921e-193">**Node.js**: [Notification Hubs gebruiken vanuit Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f921e-193">**Node.js**: [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="f921e-194">**Mobile Apps**: zie [Pushmeldingen toevoegen voor mobiele apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) voor een voorbeeld van hoe u meldingen verzendt vanuit een Azure App Service Mobile Apps-backend die is geïntegreerd met Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="f921e-194">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="f921e-195">**Java/PHP**: zie 'Notification Hubs gebruiken vanuit Java/PHP' voor een voorbeeld van hoe u meldingen verzendt met de REST API's ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="f921e-195">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="f921e-196">(Optioneel) Meldingen verzenden vanuit een .NET-console-app</span><span class="sxs-lookup"><span data-stu-id="f921e-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="f921e-197">In dit gedeelte behandelen we hoe u een melding vanuit een .NET-console-app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="f921e-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="f921e-198">Maak een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="f921e-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="f921e-199">Stel in het venster Package Manager-console het **standaardproject** in op uw nieuwe consoletoepassingsproject en voer vervolgens in het consolevenster de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="f921e-199">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="f921e-200">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs-SDK met het <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="f921e-200">This instruction adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="f921e-201">Open het bestand **Program.cs** en voeg de volgende gebruiksinstructie toe:</span><span class="sxs-lookup"><span data-stu-id="f921e-201">Open the file **Program.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="f921e-202">Voeg in uw klasse `Program` de volgende methode toe en vervang *DefaultFullSharedAccessSignatureSASConnectionString* en *NotificationHubName* door de waarden die u hebt.</span><span class="sxs-lookup"><span data-stu-id="f921e-202">In your `Program` class, add the following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with the values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="f921e-203">Voeg de volgende regels in de **Main**-methode toe:</span><span class="sxs-lookup"><span data-stu-id="f921e-203">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="f921e-204">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="f921e-204">Test your app</span></span>
<span data-ttu-id="f921e-205">Als u uw app met een telefoon wilt testen, sluit u de telefoon met een USB-kabel op uw computer aan.</span><span class="sxs-lookup"><span data-stu-id="f921e-205">To test this app with an actual phone, just connect the phone to your computer by using a USB cable.</span></span> <span data-ttu-id="f921e-206">Met deze actie wordt uw app naar de gekoppelde telefoon geladen.</span><span class="sxs-lookup"><span data-stu-id="f921e-206">This action loads your app onto the attached phone.</span></span>

<span data-ttu-id="f921e-207">Als u deze app wilt testen met de emulator klikt u op de bovenste Eclipse-taakbalk op **Uitvoeren** en selecteert u uw app. De emulator wordt dan gestart en daarna wordt de app geladen en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f921e-207">To test this app with the emulator, on the Eclipse top toolbar, click **Run**, and then select your app: it starts the emulator, loads, and runs the app.</span></span>

<span data-ttu-id="f921e-208">De app haalt de gebruikers-id en de channelId op uit de Baidu Push Notification Service en registreert zich bij de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="f921e-208">The app retrieves the 'userId' and 'channelId' from the Baidu Push notification service and registers with the notification hub.</span></span>

<span data-ttu-id="f921e-209">U kunt vanaf het foutopsporingstabblad van de klassieke Azure-portal een testmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="f921e-209">To send a test notification, you can use the debug tab of the Azure Classic Portal.</span></span> <span data-ttu-id="f921e-210">Als u de .Net-console-toepassing hebt gebouwd voor Visual Studio, drukt u in Visual Studio op F5 om de toepassing te starten.</span><span class="sxs-lookup"><span data-stu-id="f921e-210">If you built the .NET console application for Visual Studio, just press the F5 key in Visual Studio to run the application.</span></span> <span data-ttu-id="f921e-211">De toepassing verstuurt een melding. Deze verschijnt in het bovenste gedeelte voor meldingen op uw apparaat of in de emulator.</span><span class="sxs-lookup"><span data-stu-id="f921e-211">The application sends a notification that appears in the top notification area of your device or emulator.</span></span>

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
<span data-ttu-id="f921e-212">[Android-SDK voor Mobile Services]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="f921e-212">[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span></span>
<span data-ttu-id="f921e-213">[Android SDK Baidu Push]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span><span class="sxs-lookup"><span data-stu-id="f921e-213">[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span></span>
<span data-ttu-id="f921e-214">[Klassieke Azure Portal]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="f921e-214">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="f921e-215">[Baidu Portal]: http://www.baidu.com/</span><span class="sxs-lookup"><span data-stu-id="f921e-215">[Baidu portal]: http://www.baidu.com/</span></span>
