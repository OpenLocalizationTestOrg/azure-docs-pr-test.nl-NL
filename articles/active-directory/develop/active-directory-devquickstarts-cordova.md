---
title: Azure AD-Cordova aan de slag | Microsoft Docs
description: "Het bouwen van een Cordova-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-beveiligde API aanroept met behulp van OAuth."
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="02a7a-103">Azure AD integreren met een Apache Cordova-app</span><span class="sxs-lookup"><span data-stu-id="02a7a-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="02a7a-104">U kunt Apache Cordova HTML5/JavaScript-toepassingen die kunnen worden uitgevoerd op mobiele apparaten als volwaardig systeemeigen toepassingen ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="02a7a-105">Met Azure Active Directory (Azure AD), kunt u verificatiefuncties bedrijfsniveau toevoegen aan uw Cordova-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="02a7a-106">Een invoegtoepassing Cordova verpakt Azure AD systeemeigen SDK's op iOS, Android, Windows Store en Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="02a7a-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="02a7a-107">Met dat invoegtoepassing, u door uw toepassing verbeteren kunt ter ondersteuning van aanmelden met Windows Server Active Directory-accounts voor uw gebruikers toegang krijgen tot Office 365 en Azure-API's en zelfs bescherming van uw eigen aangepaste web-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="02a7a-108">In deze zelfstudie gebruiken we de Apache Cordova-invoegtoepassing voor Active Directory Authentication Library (ADAL) voor het verbeteren van een eenvoudige app door de volgende functies toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="02a7a-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="02a7a-109">Verifiëren van een gebruiker met een paar regels code, en een token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="02a7a-110">Gebruik dat token aan te roepen de Graph API om te vragen die map en de resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="02a7a-111">Gebruik de ADAL tokencache verificatie wordt u gevraagd om de gebruiker minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="02a7a-112">Als u deze verbeteringen maken, moet u:</span><span class="sxs-lookup"><span data-stu-id="02a7a-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="02a7a-113">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02a7a-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="02a7a-114">Voeg code toe aan uw app om aanvragen van tokens.</span><span class="sxs-lookup"><span data-stu-id="02a7a-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="02a7a-115">Voeg de code voor het gebruik van het token voor query's in de Graph API en resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="02a7a-116">De implementatie Cordova-project maken met de platforms die u wilt richten, de Cordova ADAL invoegtoepassing toevoegen en testen van de oplossing in emulators.</span><span class="sxs-lookup"><span data-stu-id="02a7a-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02a7a-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="02a7a-117">Prerequisites</span></span>
<span data-ttu-id="02a7a-118">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="02a7a-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="02a7a-119">Een Azure AD-tenant waarin u een account met app-ontwikkeling rechten hebben.</span><span class="sxs-lookup"><span data-stu-id="02a7a-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="02a7a-120">Een ontwikkelingsomgeving die geconfigureerd voor gebruik van Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="02a7a-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="02a7a-121">Als u beide al hebt ingesteld, doorgaan met stap 1.</span><span class="sxs-lookup"><span data-stu-id="02a7a-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="02a7a-122">Als u geen Azure AD-tenant, gebruikt u de [instructies voor het ophalen van een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="02a7a-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="02a7a-123">Als u geen Apache Cordova instellen op uw computer, installeert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="02a7a-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="02a7a-124">Git</span><span class="sxs-lookup"><span data-stu-id="02a7a-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="02a7a-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="02a7a-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="02a7a-126">[Cordova CLI](https://cordova.apache.org/) (kan gemakkelijk worden geïnstalleerd via NPM Pakketbeheer: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="02a7a-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="02a7a-127">De voorgaande installaties moeten werken zowel op de PC als op de Mac.</span><span class="sxs-lookup"><span data-stu-id="02a7a-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="02a7a-128">Elk doelplatform heeft verschillende vereisten:</span><span class="sxs-lookup"><span data-stu-id="02a7a-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="02a7a-129">Het bouwen en uitvoeren van een app voor Windows-Tablet/PC of Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="02a7a-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="02a7a-130">Installeer [Visual Studio 2013 voor Windows met Update 2 of hoger](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express of een andere versie) of [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="02a7a-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="02a7a-131">Het bouwen en uitvoeren van een app voor iOS:</span><span class="sxs-lookup"><span data-stu-id="02a7a-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="02a7a-132">Installeer Xcode 6.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="02a7a-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="02a7a-133">Downloaden van de [Apple Developer site](http://developer.apple.com/downloads) of de [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="02a7a-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="02a7a-134">Installeer [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="02a7a-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="02a7a-135">U kunt het starten van iOS-apps in iOS-Simulator vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="02a7a-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="02a7a-136">(U kunt het eenvoudig installeren via de terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="02a7a-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="02a7a-137">Het bouwen en uitvoeren van een app voor Android:</span><span class="sxs-lookup"><span data-stu-id="02a7a-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="02a7a-138">Installeer [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.</span><span class="sxs-lookup"><span data-stu-id="02a7a-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="02a7a-139">Zorg ervoor dat `JAVA_HOME` (omgevingsvariabele) correct is ingesteld in overeenstemming met het installatiepad JDK (bijvoorbeeld C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="02a7a-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="02a7a-140">Installeer [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) en voeg de `<android-sdk-location>\tools` locatie (bijvoorbeeld C:\tools\Android\android-sdk\tools) voor uw `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="02a7a-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="02a7a-141">Android SDK Manager openen (bijvoorbeeld via de terminal: `android`) en te installeren:</span><span class="sxs-lookup"><span data-stu-id="02a7a-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="02a7a-142">*Android 5.0.1 (API 21)* platform SDK</span><span class="sxs-lookup"><span data-stu-id="02a7a-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="02a7a-143">*Android SDK-Build Tools* versie 19.1.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="02a7a-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="02a7a-144">*Android-ondersteuning opslagplaats* (extra's)</span><span class="sxs-lookup"><span data-stu-id="02a7a-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="02a7a-145">De Android SDK biedt een standaardexemplaar van de emulator niet.</span><span class="sxs-lookup"><span data-stu-id="02a7a-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="02a7a-146">Maken van een door het uitvoeren van `android avd` vanaf de terminal en selecteren **maken**, als u wilt uitvoeren van de Android-app op een emulator.</span><span class="sxs-lookup"><span data-stu-id="02a7a-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="02a7a-147">U wordt aangeraden een API-niveau van 19 of hoger.</span><span class="sxs-lookup"><span data-stu-id="02a7a-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="02a7a-148">Zie voor meer informatie over de Android-emulator en het maken van opties [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) op de Android-site.</span><span class="sxs-lookup"><span data-stu-id="02a7a-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="02a7a-149">Stap 1: Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="02a7a-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="02a7a-150">Deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="02a7a-150">This step is optional.</span></span> <span data-ttu-id="02a7a-151">Deze zelfstudie bevat vooraf is ingericht waarden die u gebruiken kunt om te zien van het voorbeeld in actie zonder eventuele inrichten in uw eigen tenant.</span><span class="sxs-lookup"><span data-stu-id="02a7a-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="02a7a-152">We raden echter aan dat u deze stap uitvoeren en vertrouwd met het proces, raken omdat deze vereist is wanneer u uw eigen toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="02a7a-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="02a7a-153">Azure AD geeft tokens alleen bekende toepassingen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="02a7a-154">Voordat u van uw app kunt u Azure AD, moet u een vermelding maken voor het in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="02a7a-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="02a7a-155">Een nieuwe toepassing registreren in uw tenant:</span><span class="sxs-lookup"><span data-stu-id="02a7a-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="02a7a-156">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02a7a-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="02a7a-157">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="02a7a-157">On the top bar, click your account.</span></span> <span data-ttu-id="02a7a-158">In de **Directory** kiest u de Azure AD-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="02a7a-159">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="02a7a-160">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="02a7a-161">Volg de aanwijzingen en maak een **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="02a7a-162">(Hoewel de Cordova-apps zijn op basis van HTML, we creëren een native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="02a7a-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="02a7a-163">De **systeemeigen clienttoepassing** optie moet zijn geselecteerd of de toepassing werkt niet.)</span><span class="sxs-lookup"><span data-stu-id="02a7a-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="02a7a-164">**Naam** beschrijving van uw toepassing voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02a7a-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="02a7a-165">**Omleidings-URI** is de URI die wordt gebruikt voor tokens terug naar uw app.</span><span class="sxs-lookup"><span data-stu-id="02a7a-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="02a7a-166">Voer **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="02a7a-167">Nadat u de registratie, wijst Azure AD een unieke toepassings-ID toe aan uw app.</span><span class="sxs-lookup"><span data-stu-id="02a7a-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="02a7a-168">U moet deze waarde in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="02a7a-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="02a7a-169">U vindt deze op het toepassingstabblad van de nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="02a7a-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="02a7a-170">Om uit te voeren `DirSearchClient Sample`, de zojuist gemaakte app machtiging query uitvoeren op de Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="02a7a-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="02a7a-171">Van de **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="02a7a-172">Selecteer voor de toepassing Azure Active Directory **Microsoft Graph** als de API en voeg de **toegang tot de map als de gebruiker is aangemeld** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="02a7a-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="02a7a-173">Hierdoor wordt uw toepassing query uitvoeren op de Graph-API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02a7a-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="02a7a-174">Stap 2: De voorbeeld-app-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="02a7a-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="02a7a-175">Typ de volgende opdracht uit uw shell of vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="02a7a-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="02a7a-176">Stap 3: De Cordova-app maken</span><span class="sxs-lookup"><span data-stu-id="02a7a-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="02a7a-177">Er zijn meerdere manieren om Cordova-toepassingen te maken.</span><span class="sxs-lookup"><span data-stu-id="02a7a-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="02a7a-178">In deze zelfstudie gebruikt u de Cordova-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="02a7a-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="02a7a-179">Typ de volgende opdracht uit uw shell of vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="02a7a-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="02a7a-180">Deze opdracht maakt u de mapstructuur en steigers voor de Cordova-project.</span><span class="sxs-lookup"><span data-stu-id="02a7a-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="02a7a-181">Verplaatsen naar de nieuwe DirSearchClient map:</span><span class="sxs-lookup"><span data-stu-id="02a7a-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="02a7a-182">Kopieer de inhoud van het starter-project in de submap www met behulp van de manager van een bestand of de volgende opdracht in uw shell:</span><span class="sxs-lookup"><span data-stu-id="02a7a-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="02a7a-183">Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="02a7a-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="02a7a-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="02a7a-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="02a7a-185">De invoegtoepassing goedgekeurde toevoegen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="02a7a-186">Dit is nodig om de Graph API aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="02a7a-187">Voeg de platforms die u wilt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="02a7a-188">Als u een voorbeeld van een werken, moet u ten minste één van de volgende opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="02a7a-189">Houd er rekening mee dat u niet kan worden geëmuleerd iOS op Windows of emuleren van Windows op een Mac.</span><span class="sxs-lookup"><span data-stu-id="02a7a-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="02a7a-190">De ADAL voor Cordova-invoegtoepassing toevoegen aan uw project:</span><span class="sxs-lookup"><span data-stu-id="02a7a-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="02a7a-191">Stap 4: Code toevoegen om te verifiëren van gebruikers en tokens verkrijgen bij Azure AD</span><span class="sxs-lookup"><span data-stu-id="02a7a-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="02a7a-192">De toepassing die u in deze zelfstudie ontwikkelt bieden een eenvoudige directory zoekfunctie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="02a7a-193">De gebruiker kan vervolgens typt u de alias van een gebruiker in de map en visualiseren van enkele eenvoudige kenmerken.</span><span class="sxs-lookup"><span data-stu-id="02a7a-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="02a7a-194">Het starter-project bevat de definitie van de algemene gebruikersinterface van de app (in www/index.html) en de steiger die van de basis-Apps gebeurtenis kabels cycli, gebruikersinterface bindingen, en resultaten weergeven logica (in www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="02a7a-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="02a7a-195">De enige taak resteren voor u is het toevoegen van de logica die identiteit taken implementeert.</span><span class="sxs-lookup"><span data-stu-id="02a7a-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="02a7a-196">Het eerste wat dat u moet doen in uw code is introduceren van het protocol-waarden die Azure AD worden gebruikt voor het identificeren van uw app en de resources die u zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="02a7a-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="02a7a-197">Deze waarden worden gebruikt om de aanvragen voor beveiligingstokens later samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="02a7a-198">Voeg het volgende codefragment aan de bovenkant van het bestand index.js:</span><span class="sxs-lookup"><span data-stu-id="02a7a-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="02a7a-199">De `redirectUri` en `clientId` waarden moeten overeenkomen met de waarden die uw app in Azure AD te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="02a7a-200">U kunt vinden die uit de **configureren** tabblad in de Azure portal, zoals beschreven in stap 1 eerder in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="02a7a-201">Als u hebt gekozen voor het registreren van een nieuwe app niet in uw eigen tenant, kunt u gewoon de vooraf geconfigureerde waarden ongewijzigd plakken.</span><span class="sxs-lookup"><span data-stu-id="02a7a-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="02a7a-202">Vervolgens ziet u het voorbeeld wordt uitgevoerd, hoewel altijd moet u uw eigen vermelding maken voor uw apps die zijn bedoeld voor productie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="02a7a-203">Voeg vervolgens de tokenaanvraag-code.</span><span class="sxs-lookup"><span data-stu-id="02a7a-203">Next, add the token request code.</span></span> <span data-ttu-id="02a7a-204">Voeg het volgende fragment tussen de `search` en `renderData` definities:</span><span class="sxs-lookup"><span data-stu-id="02a7a-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="02a7a-205">Door deze te splitsen in de twee belangrijkste delen behandeld die functie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="02a7a-206">Dit voorbeeld is ontworpen voor gebruik met een tenant, in plaats van wordt gekoppeld aan een bepaald.</span><span class="sxs-lookup"><span data-stu-id="02a7a-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="02a7a-207">Het eindpunt '/ algemene', die kan de gebruiker een account in verificatie keer invoeren en stuurt de aanvraag naar de tenant waar hoort wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02a7a-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="02a7a-208">Deze eerste deel van de methode inspecteert de ADAL-cache om te zien is al een token opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="02a7a-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="02a7a-209">Zo ja, de methode maakt gebruik van de tenants waar het token vandaan komt voor het initialiseren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="02a7a-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="02a7a-210">Dit is nodig om te voorkomen dat extra prompts omdat het gebruik van '/ algemene' altijd resulteert in de gebruiker een nieuwe account in te voeren wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="02a7a-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="02a7a-211">Het tweede gedeelte van de methode voert de juiste tokenaanvraag.</span><span class="sxs-lookup"><span data-stu-id="02a7a-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="02a7a-212">De `acquireTokenSilentAsync` methode vraagt ADAL te retourneren van een token voor de opgegeven resource zonder dat u eventuele UX weergegeven</span><span class="sxs-lookup"><span data-stu-id="02a7a-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="02a7a-213">Dat kan gebeuren als de cache al een geschikte toegangstoken opgeslagen heeft, of als een vernieuwingstoken kan worden gebruikt om een nieuw toegangstoken ophalen zonder dat een prompt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="02a7a-214">Als dat lukt, we terugvallen op `acquireTokenAsync`--die de gebruiker authenticatie verricht zichtbaar wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="02a7a-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="02a7a-215">Nu dat we het token hebben, kunnen we ten slotte de Graph API aanroepen en de query die we willen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="02a7a-216">Voeg het volgende fragment hieronder de `authenticate` definitie:</span><span class="sxs-lookup"><span data-stu-id="02a7a-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="02a7a-217">Een eenvoudige UX startpunt bestanden opgegeven voor het invoeren van de alias van een gebruiker in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="02a7a-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="02a7a-218">Deze methode wordt die waarde voor maakt u een query, combineren met het toegangstoken verzenden naar Microsoft Graph en parseren van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="02a7a-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="02a7a-219">De `renderData` methode, al aanwezig in het bestand startpunt zorgt voor de resultaten te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="02a7a-220">Stap 5: De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="02a7a-220">Step 5: Run the app</span></span>
<span data-ttu-id="02a7a-221">Uw app is ten slotte gereed om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="02a7a-221">Your app is finally ready to run.</span></span> <span data-ttu-id="02a7a-222">Het besturingssysteem is eenvoudig: wanneer de app wordt gestart, voer de alias van de gebruiker die u wilt zoeken en klik vervolgens op de knop.</span><span class="sxs-lookup"><span data-stu-id="02a7a-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="02a7a-223">U wordt gevraagd om de verificatie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-223">You're prompted for authentication.</span></span> <span data-ttu-id="02a7a-224">Bij de verificatie is geslaagd en zoekactie, worden de kenmerken van de gezochte gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="02a7a-225">Latere uitvoeringen zal de zoekopdracht uitvoeren zonder dat een prompt dankzij de aanwezigheid van het eerder aangeschafte token in cache worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02a7a-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="02a7a-226">De concrete stappen voor het uitvoeren van de app, varieert per platform.</span><span class="sxs-lookup"><span data-stu-id="02a7a-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="02a7a-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="02a7a-227">Windows 10</span></span>
   <span data-ttu-id="02a7a-228">Tablet PC:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="02a7a-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="02a7a-229">Mobile (vereist een Windows 10 Mobile-apparaat dat is verbonden met een PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="02a7a-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="02a7a-230">Tijdens de eerste keer uitvoert, wordt u mogelijk gevraagd aan te melden voor een ontwikkelaarslicentie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="02a7a-231">Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="02a7a-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="02a7a-232">Windows 8.1 Tablet PC</span><span class="sxs-lookup"><span data-stu-id="02a7a-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="02a7a-233">Tijdens de eerste keer uitvoert, wordt u mogelijk gevraagd aan te melden voor een ontwikkelaarslicentie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="02a7a-234">Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="02a7a-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="02a7a-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="02a7a-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="02a7a-236">Uitvoeren op een verbonden apparaat:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="02a7a-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="02a7a-237">Uitvoeren op de standaardemulator:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="02a7a-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="02a7a-238">Gebruik `cordova run windows --list -- --phone` voor een overzicht van alle beschikbare doelen en `cordova run windows --target=<target_name> -- --phone` voor het uitvoeren van de toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="02a7a-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="02a7a-239">Android</span><span class="sxs-lookup"><span data-stu-id="02a7a-239">Android</span></span>
   <span data-ttu-id="02a7a-240">Uitvoeren op een verbonden apparaat:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="02a7a-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="02a7a-241">Uitvoeren op de standaardemulator:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="02a7a-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="02a7a-242">Zorg ervoor dat u hebt een exemplaar van de emulator gemaakt met behulp van AVD Manager, zoals eerder beschreven in de sectie 'Vereisten'.</span><span class="sxs-lookup"><span data-stu-id="02a7a-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="02a7a-243">Gebruik `cordova run android --list` voor een overzicht van alle beschikbare doelen en `cordova run android --target=<target_name>` voor het uitvoeren van de toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="02a7a-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="02a7a-244">iOS</span><span class="sxs-lookup"><span data-stu-id="02a7a-244">iOS</span></span>
   <span data-ttu-id="02a7a-245">Uitvoeren op een verbonden apparaat:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="02a7a-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="02a7a-246">Uitvoeren op de standaardemulator:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="02a7a-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="02a7a-247">Zorg ervoor dat u hebt de `ios-sim` pakket geïnstalleerd voor uitvoering van de emulator.</span><span class="sxs-lookup"><span data-stu-id="02a7a-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="02a7a-248">Zie de sectie 'Vereisten' voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02a7a-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="02a7a-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02a7a-249">Next steps</span></span>
<span data-ttu-id="02a7a-250">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="02a7a-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="02a7a-251">U kunt nu verder met geavanceerdere (en interessante)-scenario's.</span><span class="sxs-lookup"><span data-stu-id="02a7a-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="02a7a-252">U wilt proberen: [beveiligen van een Node.js-Web-API met Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="02a7a-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
