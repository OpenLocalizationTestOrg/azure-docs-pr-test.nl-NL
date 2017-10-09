---
title: aaaAzure AD Cordova aan de slag | Microsoft Docs
description: "Hoe toobuild een Cordova-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-beveiligde API aanroept met behulp van OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="edecc-103">Azure AD integreren met een Apache Cordova-app</span><span class="sxs-lookup"><span data-stu-id="edecc-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="edecc-104">U kunt Apache Cordova toodevelop HTML5/JavaScript-toepassingen die kunnen worden uitgevoerd op mobiele apparaten als volwaardig systeemeigen toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="edecc-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="edecc-105">U kunt met Azure Active Directory (Azure AD), bedrijfsniveau verificatie mogelijkheden tooyour Cordova toepassingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="edecc-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="edecc-106">Een invoegtoepassing Cordova verpakt Azure AD systeemeigen SDK's op iOS, Android, Windows Store en Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="edecc-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="edecc-107">Met behulp van dat invoegtoepassing, u door uw toepassing toosupport aanmelden met Windows Server Active Directory-accounts voor uw gebruikers verbeteren kunt krijgen toegang tooOffice 365 en Azure-API's, en zelfs beschermen aanroepen tooyour eigen aangepaste web-API.</span><span class="sxs-lookup"><span data-stu-id="edecc-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="edecc-108">In deze zelfstudie gebruiken we Hallo Apache Cordova-invoegtoepassing voor Active Directory Authentication Library (ADAL) tooimprove een eenvoudige app door toe te voegen Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="edecc-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="edecc-109">Verifiëren van een gebruiker met een paar regels code, en een token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="edecc-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="edecc-110">Gebruik die tooquery token tooinvoke Hallo Graph API die map en Hallo resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edecc-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="edecc-111">Gebruik Hallo ADAL tokencache toominimize verificatie wordt gevraagd om Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edecc-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="edecc-112">toomake deze verbeteringen, moet u:</span><span class="sxs-lookup"><span data-stu-id="edecc-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="edecc-113">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edecc-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="edecc-114">Code tooyour app toorequest-tokens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="edecc-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="edecc-115">Voeg code toouse Hallo token query Hallo Graph API's en resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edecc-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="edecc-116">Hallo Cordova-project voor implementatie te maken met alle Hallo platforms wilt tootarget, Hallo invoegtoepassing Cordova ADAL toevoegen en Hallo oplossing in emulators testen.</span><span class="sxs-lookup"><span data-stu-id="edecc-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edecc-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edecc-117">Prerequisites</span></span>
<span data-ttu-id="edecc-118">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="edecc-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="edecc-119">Een Azure AD-tenant waarin u een account met app-ontwikkeling rechten hebben.</span><span class="sxs-lookup"><span data-stu-id="edecc-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="edecc-120">Een ontwikkelingsomgeving die toouse Apache Cordova is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="edecc-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="edecc-121">Als u beide al hebt ingesteld, gaan rechtstreeks toostep 1.</span><span class="sxs-lookup"><span data-stu-id="edecc-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="edecc-122">Als u geen Azure AD-tenant, gebruikt u Hallo [instructies voor het tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="edecc-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="edecc-123">Als u geen Apache Cordova instellen op uw computer, installeert u Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="edecc-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="edecc-124">Git</span><span class="sxs-lookup"><span data-stu-id="edecc-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="edecc-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="edecc-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="edecc-126">[Cordova CLI](https://cordova.apache.org/) (kan gemakkelijk worden geïnstalleerd via NPM Pakketbeheer: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="edecc-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="edecc-127">Hallo voorgaande installaties moet werken voor Hallo PC en Hallo Mac.</span><span class="sxs-lookup"><span data-stu-id="edecc-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="edecc-128">Elk doelplatform heeft verschillende vereisten:</span><span class="sxs-lookup"><span data-stu-id="edecc-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="edecc-129">toobuild en voer een app voor Windows-Tablet/PC of Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="edecc-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="edecc-130">Installeer [Visual Studio 2013 voor Windows met Update 2 of hoger](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express of een andere versie) of [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="edecc-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="edecc-131">toobuild en voer een app voor iOS:</span><span class="sxs-lookup"><span data-stu-id="edecc-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="edecc-132">Installeer Xcode 6.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="edecc-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="edecc-133">Het downloaden van Hallo [Apple Developer site](http://developer.apple.com/downloads) of Hallo [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="edecc-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="edecc-134">Installeer [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="edecc-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="edecc-135">U kunt deze toostart iOS-apps in iOS-Simulator vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="edecc-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="edecc-136">(U kunt het eenvoudig installeren via Hallo terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="edecc-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="edecc-137">toobuild en voer een app voor Android:</span><span class="sxs-lookup"><span data-stu-id="edecc-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="edecc-138">Installeer [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.</span><span class="sxs-lookup"><span data-stu-id="edecc-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="edecc-139">Zorg ervoor dat `JAVA_HOME` (omgevingsvariabele) correct is ingesteld op basis van toohello JDK installatiepad (bijvoorbeeld C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="edecc-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="edecc-140">Installeer [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) en voeg Hallo `<android-sdk-location>\tools` locatie (bijvoorbeeld C:\tools\Android\android-sdk\tools) tooyour `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="edecc-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="edecc-141">Android SDK Manager openen (bijvoorbeeld via Hallo terminal: `android`) en te installeren:</span><span class="sxs-lookup"><span data-stu-id="edecc-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="edecc-142">*Android 5.0.1 (API 21)* platform SDK</span><span class="sxs-lookup"><span data-stu-id="edecc-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="edecc-143">*Android SDK-Build Tools* versie 19.1.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="edecc-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="edecc-144">*Android-ondersteuning opslagplaats* (extra's)</span><span class="sxs-lookup"><span data-stu-id="edecc-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="edecc-145">Hallo Android SDK biedt een standaardexemplaar van de emulator niet.</span><span class="sxs-lookup"><span data-stu-id="edecc-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="edecc-146">Maken van een door het uitvoeren van `android avd` van Hallo terminal en vervolgens te klikken op **maken**, als u wilt dat toorun hello Android-app op een emulator.</span><span class="sxs-lookup"><span data-stu-id="edecc-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="edecc-147">U wordt aangeraden een API-niveau van 19 of hoger.</span><span class="sxs-lookup"><span data-stu-id="edecc-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="edecc-148">Zie voor meer informatie over de Android-emulator en het maken van opties Hallo [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) op Hallo Android-site.</span><span class="sxs-lookup"><span data-stu-id="edecc-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="edecc-149">Stap 1: Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="edecc-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="edecc-150">Deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="edecc-150">This step is optional.</span></span> <span data-ttu-id="edecc-151">Deze zelfstudie bevat vooraf is ingericht waarden waarmee u toosee kunt Hallo voorbeeld in actie zonder eventuele inrichten in uw eigen tenant.</span><span class="sxs-lookup"><span data-stu-id="edecc-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="edecc-152">We raden echter aan dat u deze stap uitvoeren en vertrouwd met Hallo proces, raken omdat deze vereist is wanneer u uw eigen toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="edecc-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="edecc-153">Azure AD geeft tokens tooonly bekend toepassingen.</span><span class="sxs-lookup"><span data-stu-id="edecc-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="edecc-154">Voordat u Azure AD van uw app gebruiken kunt, moet u toocreate een vermelding voor het in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="edecc-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="edecc-155">een nieuwe toepassing in uw tenant tooregister:</span><span class="sxs-lookup"><span data-stu-id="edecc-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="edecc-156">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edecc-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="edecc-157">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="edecc-157">On hello top bar, click your account.</span></span> <span data-ttu-id="edecc-158">In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="edecc-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="edecc-159">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="edecc-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="edecc-160">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="edecc-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="edecc-161">Volg de aanwijzingen Hallo en maak een **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="edecc-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="edecc-162">(Hoewel de Cordova-apps zijn op basis van HTML, we creëren een native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="edecc-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="edecc-163">Hallo **systeemeigen clienttoepassing** optie moet zijn geselecteerd, of de toepassing hello werken niet.)</span><span class="sxs-lookup"><span data-stu-id="edecc-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="edecc-164">**Naam** beschrijft de toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="edecc-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="edecc-165">**Omleidings-URI** is Hallo URI die tooreturn tokens tooyour app wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="edecc-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="edecc-166">Voer **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="edecc-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="edecc-167">Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe.</span><span class="sxs-lookup"><span data-stu-id="edecc-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="edecc-168">U moet deze waarde in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="edecc-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="edecc-169">U vindt deze op het toepassingstabblad Hallo Hallo app een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="edecc-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="edecc-170">toorun `DirSearchClient Sample`, Hallo nieuwe app machtiging tooquery hello Azure AD Graph API verlenen:</span><span class="sxs-lookup"><span data-stu-id="edecc-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="edecc-171">Van Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="edecc-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="edecc-172">Voor Azure Active Directory-toepassing hello, selecteert u **Microsoft Graph** als Hallo API en voeg Hallo **toegang Hallo directory als de gebruiker is aangemeld Hallo** machtiging onder **gedelegeerde Machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="edecc-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="edecc-173">Hierdoor kan uw toepassing tooquery Hallo Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="edecc-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="edecc-174">Stap 2: Hallo voorbeeld-app opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="edecc-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="edecc-175">Van uw shell of vanaf de opdrachtregel typt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="edecc-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="edecc-176">Stap 3: Hallo Cordova-app maken</span><span class="sxs-lookup"><span data-stu-id="edecc-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="edecc-177">Er zijn meerdere manieren toocreate Cordova-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="edecc-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="edecc-178">In deze zelfstudie gebruiken we Hallo Cordova-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="edecc-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="edecc-179">Van uw shell of vanaf de opdrachtregel typt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="edecc-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="edecc-180">Deze opdracht maakt Hallo mapstructuur en steigers voor Hallo Cordova-project.</span><span class="sxs-lookup"><span data-stu-id="edecc-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="edecc-181">Toohello nieuwe DirSearchClient map verplaatsen:</span><span class="sxs-lookup"><span data-stu-id="edecc-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="edecc-182">Hallo-inhoud van Hallo starter project kopiëren in Hallo www submap met behulp van een bestand manager of de volgende opdracht in uw shell Hallo:</span><span class="sxs-lookup"><span data-stu-id="edecc-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="edecc-183">Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="edecc-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="edecc-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="edecc-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="edecc-185">Hallo geaccepteerde invoegtoepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="edecc-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="edecc-186">Dit is nodig voor het aanroepen van Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="edecc-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="edecc-187">Alle Hallo-platforms die u toosupport wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="edecc-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="edecc-188">een voorbeeld van een werkende toohave, moet u tooexecute ten minste één van de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="edecc-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="edecc-189">Houd er rekening mee dat u niet kunnen tooemulate iOS in Windows worden en emuleren van Windows op een Mac.</span><span class="sxs-lookup"><span data-stu-id="edecc-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="edecc-190">Hallo ADAL voor Cordova-invoegtoepassing tooyour project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="edecc-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="edecc-191">Stap 4: Code tooauthenticate gebruikers toevoegen en tokens verkrijgen bij Azure AD</span><span class="sxs-lookup"><span data-stu-id="edecc-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="edecc-192">Hallo-toepassing die u in deze zelfstudie ontwikkelt bieden een eenvoudige directory zoekfunctie.</span><span class="sxs-lookup"><span data-stu-id="edecc-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="edecc-193">Hallo-gebruiker kan vervolgens Hallo alias van een gebruiker typt in Hallo directory en visualiseren enkele eenvoudige kenmerken.</span><span class="sxs-lookup"><span data-stu-id="edecc-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="edecc-194">Hallo starter project bevat Hallo definitie van de algemene gebruikersinterface Hallo van Hallo-app (in www/index.html) en Hallo steigers die van de basis-Apps gebeurtenis kabels cycli, gebruikersinterface bindingen, en resultaten weergeven logica (in www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="edecc-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="edecc-195">Hallo is alleen gegeven voor u uit de taak tooadd Hallo logica die identiteit taken implementeert.</span><span class="sxs-lookup"><span data-stu-id="edecc-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="edecc-196">Hallo eerste wat u moet toodo in uw code is introduceren Hallo protocol waarden die Azure AD wordt gebruikt voor het identificeren van uw app en Hallo resources die u zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="edecc-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="edecc-197">Deze waarden worden aanvragen voor beveiligingstokens gebruikte tooconstruct hello later op.</span><span class="sxs-lookup"><span data-stu-id="edecc-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="edecc-198">Voeg Hallo codefragment bovenaan Hallo Hallo index.js bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="edecc-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="edecc-199">Hallo `redirectUri` en `clientId` waarden moeten overeenkomen met de Hallo-waarden met een beschrijving van uw app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edecc-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="edecc-200">U kunt vinden die uit Hallo **configureren** tabblad hello Azure-portal, zoals beschreven in stap 1 eerder in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="edecc-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="edecc-201">Als u hebt gekozen voor het registreren van een nieuwe app niet in uw eigen tenant, kunt u eenvoudig hello vooraf geconfigureerde waarden omdat plakken.</span><span class="sxs-lookup"><span data-stu-id="edecc-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="edecc-202">U kunt zien Hallo voorbeeld wordt uitgevoerd, hoewel altijd moet u uw eigen vermelding maken voor uw apps die zijn bedoeld voor productie.</span><span class="sxs-lookup"><span data-stu-id="edecc-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="edecc-203">Vervolgens voegt u Hallo tokenaanvraag code.</span><span class="sxs-lookup"><span data-stu-id="edecc-203">Next, add hello token request code.</span></span> <span data-ttu-id="edecc-204">Invoegen na codefragment tussen Hallo Hallo `search` en `renderData` definities:</span><span class="sxs-lookup"><span data-stu-id="edecc-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="edecc-205">Door deze te splitsen in de twee belangrijkste delen behandeld die functie.</span><span class="sxs-lookup"><span data-stu-id="edecc-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="edecc-206">Dit voorbeeld is ontworpen toowork met een tenant zoals tegengestelde toobeing tooa name een gebonden.</span><span class="sxs-lookup"><span data-stu-id="edecc-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="edecc-207">Hierbij Hallo '/ algemene' eindpunt waarmee Hallo gebruiker tooenter een account kunt verificatie tegelijk, en stuurt Hallo aanvraag toohello tenant waartoe deze behoort.</span><span class="sxs-lookup"><span data-stu-id="edecc-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="edecc-208">Deze eerste deel van de methode Hallo inspecteert Hallo ADAL cache toosee als een token is al opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="edecc-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="edecc-209">Zo ja, Hallo-methode maakt gebruik van Hallo tenants waar Hallo token vandaan komt voor het initialiseren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="edecc-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="edecc-210">Dit is noodzakelijk tooavoid omdat Hallo het gebruik van '/ algemene' altijd resulteert in het Hallo gebruiker tooenter gevraagd een nieuw account extra prompts.</span><span class="sxs-lookup"><span data-stu-id="edecc-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="edecc-211">Hallo secondegedeelte van Hallo methode voert de juiste tokenaanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="edecc-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="edecc-212">Hallo `acquireTokenSilentAsync` methode vraagt ADAL tooreturn een token voor Hallo opgegeven resource zonder dat u eventuele UX weergegeven</span><span class="sxs-lookup"><span data-stu-id="edecc-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="edecc-213">Dat kan gebeuren als het Hallo-cache heeft al een geschikte toegangstoken opgeslagen, of als een vernieuwingstoken kan worden gebruikt u een nieuw toegangstoken tooget zonder een prompt weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edecc-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="edecc-214">Als dat lukt, we terugvallen op `acquireTokenAsync`--die Hallo gebruiker tooauthenticate zichtbaar wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="edecc-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="edecc-215">Nu dat we Hallo-token hebben, kunnen we ten slotte Hallo Graph API aanroepen en Hallo zoekquery die we willen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="edecc-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="edecc-216">Invoegen na de onderstaande Hallo codefragment Hallo `authenticate` definitie:</span><span class="sxs-lookup"><span data-stu-id="edecc-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="edecc-217">een eenvoudige UX Hallo startpunt bestanden opgegeven voor het invoeren van de alias van een gebruiker in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="edecc-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="edecc-218">Deze methode maakt gebruik van die waarde tooconstruct een query, combineren met het toegangstoken Hallo tooMicrosoft grafiek om dit te verzenden en parseren Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="edecc-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="edecc-219">Hallo `renderData` methode, al aanwezig in Hallo startpunt bestand, zorgt voor het Hallo-resultaten te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="edecc-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="edecc-220">Stap 5: Hallo app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="edecc-220">Step 5: Run hello app</span></span>
<span data-ttu-id="edecc-221">Uw app wordt tot slot gereed toorun.</span><span class="sxs-lookup"><span data-stu-id="edecc-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="edecc-222">Het besturingssysteem is eenvoudig: wanneer Hallo-app wordt gestart, Voer Hallo alias van Hallo gebruiker toolook omhoog gewenste en klik vervolgens op Hallo knop.</span><span class="sxs-lookup"><span data-stu-id="edecc-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="edecc-223">U wordt gevraagd om de verificatie.</span><span class="sxs-lookup"><span data-stu-id="edecc-223">You're prompted for authentication.</span></span> <span data-ttu-id="edecc-224">Bij de verificatie is geslaagd en zoekactie worden Hallo kenmerken van Hallo doorzocht gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="edecc-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="edecc-225">Latere uitvoeringen Hallo zoekopdracht wordt uitgevoerd zonder een prompt weer te geven, dankzij toohello aanwezigheid van Hallo eerder hebt verkregen token in de cache.</span><span class="sxs-lookup"><span data-stu-id="edecc-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="edecc-226">Hallo concrete stappen voor het uitvoeren van de app hello, varieert per platform.</span><span class="sxs-lookup"><span data-stu-id="edecc-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="edecc-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="edecc-227">Windows 10</span></span>
   <span data-ttu-id="edecc-228">Tablet PC:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="edecc-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="edecc-229">Mobile (vereist een Windows 10 Mobile-apparaat aansluit tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="edecc-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="edecc-230">Tijdens het Hallo voor het eerst uitvoert, u mogelijk gevraagd toosign in voor een ontwikkelaarslicentie.</span><span class="sxs-lookup"><span data-stu-id="edecc-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="edecc-231">Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="edecc-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="edecc-232">Windows 8.1 Tablet PC</span><span class="sxs-lookup"><span data-stu-id="edecc-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="edecc-233">Tijdens het Hallo voor het eerst uitvoert, u mogelijk gevraagd toosign in voor een ontwikkelaarslicentie.</span><span class="sxs-lookup"><span data-stu-id="edecc-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="edecc-234">Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="edecc-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="edecc-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="edecc-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="edecc-236">toorun op een verbonden apparaat:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="edecc-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="edecc-237">toorun op Hallo standaardemulator:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="edecc-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="edecc-238">Gebruik `cordova run windows --list -- --phone` toosee alle beschikbare doelen en `cordova run windows --target=<target_name> -- --phone` toorun Hallo toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="edecc-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="edecc-239">Android</span><span class="sxs-lookup"><span data-stu-id="edecc-239">Android</span></span>
   <span data-ttu-id="edecc-240">toorun op een verbonden apparaat:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="edecc-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="edecc-241">toorun op Hallo standaardemulator:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="edecc-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="edecc-242">Zorg ervoor dat u hebt een exemplaar van de emulator gemaakt met behulp van AVD Manager, zoals eerder in de sectie 'Vereisten' hello beschreven.</span><span class="sxs-lookup"><span data-stu-id="edecc-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="edecc-243">Gebruik `cordova run android --list` toosee alle beschikbare doelen en `cordova run android --target=<target_name>` toorun Hallo toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="edecc-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="edecc-244">iOS</span><span class="sxs-lookup"><span data-stu-id="edecc-244">iOS</span></span>
   <span data-ttu-id="edecc-245">toorun op een verbonden apparaat:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="edecc-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="edecc-246">toorun op Hallo standaardemulator:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="edecc-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="edecc-247">Controleer of er Hallo `ios-sim` toorun pakket is geïnstalleerd op het Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="edecc-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="edecc-248">Zie voor meer informatie, Hallo 'vereisten' sectie.</span><span class="sxs-lookup"><span data-stu-id="edecc-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="edecc-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edecc-249">Next steps</span></span>
<span data-ttu-id="edecc-250">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="edecc-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="edecc-251">U kunt nu verplaatsen op geavanceerde toomore (en meer interessante)-scenario's.</span><span class="sxs-lookup"><span data-stu-id="edecc-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="edecc-252">U kunt tootry: [beveiligen van een Node.js-Web-API met Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="edecc-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
