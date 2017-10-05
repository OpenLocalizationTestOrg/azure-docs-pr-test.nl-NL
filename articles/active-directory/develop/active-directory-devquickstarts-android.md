---
title: Azure AD-Android aan de slag | Microsoft Docs
description: Het bouwen van een Android-toepassing die met Azure AD voor aanmelden en Azure AD-aanroepen integreert beveiligd API's met behulp van OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="aa51c-103">Azure AD integreren met een Android-app</span><span class="sxs-lookup"><span data-stu-id="aa51c-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="aa51c-104">Deze Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/Android), die helpt u bij leren werken met Azure AD in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="aa51c-105">De portal voor ontwikkelaars begeleidt u door het proces van registreren van een app en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="aa51c-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="aa51c-106">Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="aa51c-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="aa51c-107">Als u een bureaubladtoepassing ontwikkelt, kunt Azure Active Directory (Azure AD) u eenvoudig en snel u uw gebruikers verifiëren met behulp van de lokale Active Directory-accounts.</span><span class="sxs-lookup"><span data-stu-id="aa51c-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="aa51c-108">Ook kunt uw toepassing veilig gebruiken voor een web-API die zijn beveiligd door Azure AD, zoals de Office 365-API of de Azure-API.</span><span class="sxs-lookup"><span data-stu-id="aa51c-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="aa51c-109">Voor Android clients die toegang moeten krijgen tot beveiligde bronnen, levert Azure AD de Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="aa51c-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="aa51c-110">Het enige doel van ADAL is gemakkelijker voor uw app toegangstokens ophalen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="aa51c-111">Om te demonstreren hoe eenvoudig het is, moet we die een takenlijst Android-toepassing bouwen:</span><span class="sxs-lookup"><span data-stu-id="aa51c-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="aa51c-112">Krijgt toegang tot tokens voor een taak lijst-API aanroept met behulp van de [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa51c-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="aa51c-113">De takenlijst van een gebruiker opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aa51c-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="aa51c-114">Tekenen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="aa51c-114">Signs out users.</span></span>

<span data-ttu-id="aa51c-115">Om te beginnen, moet u een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="aa51c-116">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="aa51c-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="aa51c-117">Stap 1: Downloaden en uitvoeren van de server Node.js REST-API TODO-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="aa51c-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="aa51c-118">Het voorbeeld voor Node.js REST-API TODO wordt geschreven om specifiek te kunnen werken met onze huidige voorbeeld voor het bouwen van een één-tenant taak REST-API voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa51c-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="aa51c-119">Dit is een vereiste voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="aa51c-120">Zie voor informatie over hoe dit onze bestaande voorbeelden in [Microsoft Azure Active Directory-voorbeeld REST API-Service voor Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa51c-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="aa51c-121">Stap 2: Uw web-API registreren bij uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="aa51c-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="aa51c-122">Active Directory ondersteunt twee soorten toepassingen toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="aa51c-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="aa51c-123">Web-API's die services aan gebruikers bieden</span><span class="sxs-lookup"><span data-stu-id="aa51c-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="aa51c-124">Toepassingen (die worden uitgevoerd op het web of op een apparaat) die toegang hebben tot de web-API 's</span><span class="sxs-lookup"><span data-stu-id="aa51c-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="aa51c-125">In deze stap kunt u de web-API die u lokaal worden uitgevoerd voor het testen van dit voorbeeld wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aa51c-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="aa51c-126">Deze web-API is normaal gesproken een REST-service die wordt functionaliteit die u wilt dat een app om toegang te bieden.</span><span class="sxs-lookup"><span data-stu-id="aa51c-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="aa51c-127">Azure AD kunt een willekeurig eindpunt beschermen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="aa51c-128">We ervan uit dat u bent u registreert de waarnaar wordt verwezen eerder TODO REST-API.</span><span class="sxs-lookup"><span data-stu-id="aa51c-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="aa51c-129">Maar dit werkt voor alle web-API die u wilt dat Azure Active Directory om te beschermen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="aa51c-130">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa51c-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aa51c-131">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="aa51c-131">On the top bar, click your account.</span></span> <span data-ttu-id="aa51c-132">In de **Directory** kiest u de Azure AD-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="aa51c-133">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="aa51c-134">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="aa51c-135">Een beschrijvende naam voor de toepassing (bijvoorbeeld **TodoListService**), selecteer **webtoepassing en/of Web-API**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="aa51c-136">Voer de basis-URL voor het voorbeeld voor de URL eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aa51c-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="aa51c-137">Dit is standaard `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="aa51c-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="aa51c-138">Klik op **OK** om de inschrijving te voltooien.</span><span class="sxs-lookup"><span data-stu-id="aa51c-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="aa51c-139">Terwijl u nog steeds in de Azure portal, Ga naar de toepassingspagina, de waarde van de toepassing-ID vinden en kopiëren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="aa51c-140">U hebt dit later nodig bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa51c-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="aa51c-141">Van de **instellingen** -> **eigenschappen** pagina, de app ID URI bijwerken - Voer `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="aa51c-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="aa51c-142">Vervang `<your_tenant_name>` met de naam van uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="aa51c-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="aa51c-143">Stap 3: De voorbeeldtoepassing Android Native Client registreren</span><span class="sxs-lookup"><span data-stu-id="aa51c-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="aa51c-144">In dit voorbeeld moet u uw webtoepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-144">You must register your web application in this sample.</span></span> <span data-ttu-id="aa51c-145">Hierdoor kan de toepassing om te communiceren met de zojuist hebt geregistreerd web-API.</span><span class="sxs-lookup"><span data-stu-id="aa51c-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="aa51c-146">Azure AD weigert zelfs zodat uw toepassing te vragen voor aanmelden, tenzij deze is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aa51c-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="aa51c-147">Die uitmaakt deel van de beveiliging van het model.</span><span class="sxs-lookup"><span data-stu-id="aa51c-147">That's part of the security of the model.</span></span>

<span data-ttu-id="aa51c-148">We ervan uit dat u bent u registreert de voorbeeldtoepassing waarnaar wordt verwezen eerder.</span><span class="sxs-lookup"><span data-stu-id="aa51c-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="aa51c-149">Maar deze procedure werkt voor elke app die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="aa51c-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="aa51c-150">U vraagt zich misschien af waarom u een toepassing en een web-API wilt opslaan in een tenant.</span><span class="sxs-lookup"><span data-stu-id="aa51c-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="aa51c-151">Als u mogelijk hebt geraden, kunt u een app die toegang heeft tot een externe API die is geregistreerd in Azure AD van een andere tenant.</span><span class="sxs-lookup"><span data-stu-id="aa51c-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="aa51c-152">Als u dat doet, wordt uw klanten wordt gevraagd om toestemming voor het gebruik van de API in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa51c-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="aa51c-153">Active Directory Authentication Library voor iOS zorgt voor deze toestemming voor u.</span><span class="sxs-lookup"><span data-stu-id="aa51c-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="aa51c-154">Als we geavanceerdere functies, verkennen, ziet u dat dit een belangrijk onderdeel van het werk dat nodig is is voor toegang tot de suite van Microsoft APIs van Azure en Office, evenals andere serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="aa51c-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="aa51c-155">Op dit moment omdat u zowel uw web-API en uw toepassing onder dezelfde tenant geregistreerd ziet u niet om toestemming vragen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="aa51c-156">Dit is meestal het geval als u bij het ontwikkelen van een toepassing alleen voor uw eigen bedrijf te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="aa51c-157">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa51c-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aa51c-158">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="aa51c-158">On the top bar, click your account.</span></span> <span data-ttu-id="aa51c-159">In de **Directory** kiest u de Azure AD-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="aa51c-160">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="aa51c-161">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="aa51c-162">Een beschrijvende naam voor de toepassing (bijvoorbeeld **TodoListClient Android**), selecteer **systeemeigen clienttoepassing**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="aa51c-163">Voer voor de omleidings-URI `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="aa51c-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="aa51c-164">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-164">Click **Finish**.</span></span>
7. <span data-ttu-id="aa51c-165">De waarde van de toepassing-ID vinden en kopieer het via de toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="aa51c-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="aa51c-166">U hebt dit later nodig bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa51c-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="aa51c-167">Van de **instellingen** pagina **Required Permissions** en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="aa51c-168">Zoek en selecteer TodoListService, toevoegen de **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="aa51c-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="aa51c-169">Als u wilt maken met Maven, kunt u pom.xml op het hoogste niveau:</span><span class="sxs-lookup"><span data-stu-id="aa51c-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="aa51c-170">Deze opslagplaats klonen naar een map van uw keuze:</span><span class="sxs-lookup"><span data-stu-id="aa51c-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="aa51c-171">Volg de stappen in de [vereisten voor het instellen van uw omgeving Maven voor Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="aa51c-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="aa51c-172">Instellen van de SDK-19-emulator.</span><span class="sxs-lookup"><span data-stu-id="aa51c-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="aa51c-173">Ga naar de hoofdmap waar u de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="aa51c-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="aa51c-174">Deze opdracht uitvoeren:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="aa51c-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="aa51c-175">Wijzig de directory in het voorbeeld snel starten:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="aa51c-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="aa51c-176">Deze opdracht uitvoeren:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="aa51c-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="aa51c-177">U ziet dat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="aa51c-177">You should see the app starting.</span></span>
8. <span data-ttu-id="aa51c-178">Voer de referenties van gebruiker testen om te proberen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="aa51c-179">Naast het pakket AAR worden JAR-pakketten verzonden.</span><span class="sxs-lookup"><span data-stu-id="aa51c-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="aa51c-180">Stap 4: Download de Android ADAL en toe te voegen aan uw Eclipse-werkruimte</span><span class="sxs-lookup"><span data-stu-id="aa51c-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="aa51c-181">We hebben aangebracht u hebt meerdere mogelijkheden voor het gebruik van ADAL in uw Android-project eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="aa51c-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="aa51c-182">U kunt de broncode voor het importeren van deze bibliotheek in Eclipse en een koppeling naar uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="aa51c-183">Als u Android Studio, kunt u gebruik van de indeling van het pakket AAR en verwijzen naar de binaire bestanden.</span><span class="sxs-lookup"><span data-stu-id="aa51c-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="aa51c-184">Optie 1: Bron Zip</span><span class="sxs-lookup"><span data-stu-id="aa51c-184">Option 1: Source Zip</span></span>
<span data-ttu-id="aa51c-185">Een kopie van de broncode downloaden, klikt u op **ZIP downloaden** aan de rechterkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="aa51c-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="aa51c-186">U kunt [downloaden vanuit GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="aa51c-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="aa51c-187">Optie 2: Bron via Git</span><span class="sxs-lookup"><span data-stu-id="aa51c-187">Option 2: Source via Git</span></span>
<span data-ttu-id="aa51c-188">Als u de broncode van de SDK via Git, typt u:</span><span class="sxs-lookup"><span data-stu-id="aa51c-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="aa51c-189">Optie 3: Binaire bestanden via Gradle</span><span class="sxs-lookup"><span data-stu-id="aa51c-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="aa51c-190">U kunt de binaire bestanden ophalen uit de centrale opslagplaats met Maven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="aa51c-191">Het pakket AAR kan als volgt worden opgenomen in uw project in Android Studio:</span><span class="sxs-lookup"><span data-stu-id="aa51c-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="aa51c-192">Optie 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="aa51c-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="aa51c-193">Als u de invoegtoepassing M2Eclipse gebruikt, kunt u de afhankelijkheid in uw pom.xml-bestand opgeven:</span><span class="sxs-lookup"><span data-stu-id="aa51c-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="aa51c-194">Optie 5: JAR-pakket in de map libs</span><span class="sxs-lookup"><span data-stu-id="aa51c-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="aa51c-195">U kunt het JAR-bestand ophalen uit de opslagplaats met Maven en neer in de **bibliotheken** map in uw project.</span><span class="sxs-lookup"><span data-stu-id="aa51c-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="aa51c-196">U moet de vereiste resources aan uw project, evenals kopiëren omdat de JAR-pakketten niet opnemen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="aa51c-197">Stap 5: Verwijzingen naar Android ADAL toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="aa51c-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="aa51c-198">Voeg een verwijzing naar uw project en dit opgeven als een Android-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="aa51c-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="aa51c-199">Als u niet zeker hoe u dit doet, krijgt u meer informatie over de [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="aa51c-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="aa51c-200">De project-afhankelijkheid voor foutopsporing in de instellingen van uw project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="aa51c-201">Bijwerken van uw project AndroidManifest.xml dat moet worden opgenomen:</span><span class="sxs-lookup"><span data-stu-id="aa51c-201">Update your project's AndroidManifest.xml file to include:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="aa51c-202">Een exemplaar van AuthenticationContext op uw belangrijkste activiteit maken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="aa51c-203">De details van deze aanroep zijn buiten het bereik van dit onderwerp, maar u kunt een goede start ophalen door te kijken de [Android Native Client voorbeeld](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="aa51c-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="aa51c-204">In het volgende voorbeeld is SharedPreferences de standaardcache en instantie is in de vorm van `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="aa51c-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="aa51c-205">Kopieer dit codeblok voor het afhandelen van het einde van AuthenticationActivity nadat de gebruiker referenties invoert en een autorisatiecode ontvangt:</span><span class="sxs-lookup"><span data-stu-id="aa51c-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="aa51c-206">Als u vragen voor een token, definieert u een retouraanroep:</span><span class="sxs-lookup"><span data-stu-id="aa51c-206">To ask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="aa51c-207">Ten slotte vragen voor een token met behulp van terugbellen:</span><span class="sxs-lookup"><span data-stu-id="aa51c-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="aa51c-208">Hier volgt een uitleg van de parameters:</span><span class="sxs-lookup"><span data-stu-id="aa51c-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="aa51c-209">*resource* is vereist en de bron die u probeert te openen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="aa51c-210">*clientid* is vereist en afkomstig zijn van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa51c-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="aa51c-211">*RedirectUri* is niet vereist voor de aanroep acquireToken worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="aa51c-212">U kunt instellen deze als de pakketnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="aa51c-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="aa51c-213">*PromptBehavior* helpt vragen om referenties voor het overslaan van de cache en de cookie.</span><span class="sxs-lookup"><span data-stu-id="aa51c-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="aa51c-214">*callback* wordt aangeroepen nadat de autorisatiecode worden uitgewisseld voor een token.</span><span class="sxs-lookup"><span data-stu-id="aa51c-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="aa51c-215">Heeft een object van het AuthenticationResult waarvoor toegangstoken, datum verlopen en ID token-informatie.</span><span class="sxs-lookup"><span data-stu-id="aa51c-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="aa51c-216">*acquireTokenSilent* is optioneel.</span><span class="sxs-lookup"><span data-stu-id="aa51c-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="aa51c-217">U kunt deze aanroepen om te verwerken, opslaan in cache en token vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="aa51c-218">Het bevat ook de synchronisatieversie.</span><span class="sxs-lookup"><span data-stu-id="aa51c-218">It also provides the sync version.</span></span> <span data-ttu-id="aa51c-219">De cmdlet accepteert *userId* als parameter.</span><span class="sxs-lookup"><span data-stu-id="aa51c-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="aa51c-220">Met behulp van dit scenario hebt u wat u moet is geïntegreerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa51c-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="aa51c-221">Voor meer voorbeelden van deze werken, gaat u naar de AzureADSamples / opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa51c-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="aa51c-222">Belangrijke informatie</span><span class="sxs-lookup"><span data-stu-id="aa51c-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="aa51c-223">Aanpassing</span><span class="sxs-lookup"><span data-stu-id="aa51c-223">Customization</span></span>
<span data-ttu-id="aa51c-224">Uw toepassingsresources kunnen project bibliotheekresources overschrijven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="aa51c-225">Dit gebeurt wanneer uw app wordt samengesteld.</span><span class="sxs-lookup"><span data-stu-id="aa51c-225">This happens when your app is being built.</span></span> <span data-ttu-id="aa51c-226">Daarom kunt u verificatie activiteit indeling zoals die u wilt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="aa51c-227">Zorg ervoor dat de ID van de besturingselementen dat gebruikmaakt van ADAL (webweergave).</span><span class="sxs-lookup"><span data-stu-id="aa51c-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="aa51c-228">Broker</span><span class="sxs-lookup"><span data-stu-id="aa51c-228">Broker</span></span>
<span data-ttu-id="aa51c-229">De Microsoft Intune-bedrijfsportal-app biedt het broker-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="aa51c-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="aa51c-230">Het account wordt gemaakt in AccountManager.</span><span class="sxs-lookup"><span data-stu-id="aa51c-230">The account is created in AccountManager.</span></span> <span data-ttu-id="aa51c-231">Het accounttype is 'com.microsoft.workaccount'.</span><span class="sxs-lookup"><span data-stu-id="aa51c-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="aa51c-232">AccountManager kan slechts één SSO-account.</span><span class="sxs-lookup"><span data-stu-id="aa51c-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="aa51c-233">Een SSO-cookie voor de gebruiker wordt gemaakt na het voltooien van de uitdaging van het apparaat voor een van de apps.</span><span class="sxs-lookup"><span data-stu-id="aa51c-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="aa51c-234">ADAL maakt gebruik van het broker-account als een gebruikersaccount is gemaakt op deze verificator en u wilt niet overslaan.</span><span class="sxs-lookup"><span data-stu-id="aa51c-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="aa51c-235">U kunt de broker-gebruiker met overslaan:</span><span class="sxs-lookup"><span data-stu-id="aa51c-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="aa51c-236">U moet een speciale RedirectUri voor het gebruik van de broker registreren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="aa51c-237">RedirectUri bevindt zich in de indeling van `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="aa51c-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="aa51c-238">U kunt uw RedirectUri ophalen voor uw app met behulp van het script brokerRedirectPrint.ps1 of de API-aanroep mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="aa51c-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="aa51c-239">De handtekening is gerelateerd aan het ondertekenen van certificaten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="aa51c-240">Het huidige model van de broker is voor één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa51c-240">The current broker model is for one user.</span></span> <span data-ttu-id="aa51c-241">AuthenticationContext biedt de API-methode voor het ophalen van de broker-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa51c-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="aa51c-242">Uw app-manifest moet de volgende machtigingen hebben voor AccountManager accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="aa51c-243">Zie voor meer informatie de [AccountManager informatie over de Android-site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="aa51c-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="aa51c-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="aa51c-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="aa51c-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="aa51c-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="aa51c-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="aa51c-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="aa51c-247">Instantie-URL en AD FS</span><span class="sxs-lookup"><span data-stu-id="aa51c-247">Authority URL and AD FS</span></span>
<span data-ttu-id="aa51c-248">Active Directory Federation Services (AD FS) is niet herkend als productie STS, dus u moet voor het inschakelen van exemplaar van detectie en geef ' false ' in de constructor AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="aa51c-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="aa51c-249">De URL van de instantie moet een STS-exemplaar en een [tenantnaam](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="aa51c-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="aa51c-250">Opvragen van cache-items</span><span class="sxs-lookup"><span data-stu-id="aa51c-250">Querying cache items</span></span>
<span data-ttu-id="aa51c-251">ADAL biedt een standaardcache in SharedPreferences met enkele eenvoudige cache queryfuncties.</span><span class="sxs-lookup"><span data-stu-id="aa51c-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="aa51c-252">U kunt de huidige cache van AuthenticationContext krijgen met behulp van:</span><span class="sxs-lookup"><span data-stu-id="aa51c-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="aa51c-253">Als u wilt aanpassen, kunt u uw implementatie cache opgeven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="aa51c-254">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="aa51c-254">Prompt behavior</span></span>
<span data-ttu-id="aa51c-255">ADAL biedt een optie om aan te vragen gedrag opgeven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="aa51c-256">PromptBehavior.Auto wordt de gebruikersinterface weergegeven als het vernieuwingstoken dat ongeldig is en gebruikersreferenties vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="aa51c-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="aa51c-257">PromptBehavior.Always wordt het gebruik van de cache overslaan en altijd de UI niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="aa51c-258">Achtergrond tokenaanvraag uit de cache en vernieuwen</span><span class="sxs-lookup"><span data-stu-id="aa51c-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="aa51c-259">Een achtergrond tokenaanvraag maakt geen gebruik van de pop-gebruikersinterface en vereist geen een activiteit.</span><span class="sxs-lookup"><span data-stu-id="aa51c-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="aa51c-260">Retourneert een token uit de cache beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="aa51c-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="aa51c-261">Als het token is verlopen, wordt deze methode probeert te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="aa51c-262">Als het vernieuwingstoken dat is verlopen of is mislukt, wordt er AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="aa51c-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="aa51c-263">U kunt een synchronisatie met deze methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="aa51c-264">U kunt naar callback null instellen of acquireTokenSilentSync gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="aa51c-265">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="aa51c-265">Diagnostics</span></span>
<span data-ttu-id="aa51c-266">Dit zijn de primaire bronnen met informatie voor het oplossen van problemen:</span><span class="sxs-lookup"><span data-stu-id="aa51c-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="aa51c-267">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="aa51c-267">Exceptions</span></span>
* <span data-ttu-id="aa51c-268">Logboeken</span><span class="sxs-lookup"><span data-stu-id="aa51c-268">Logs</span></span>
* <span data-ttu-id="aa51c-269">Netwerktracering</span><span class="sxs-lookup"><span data-stu-id="aa51c-269">Network traces</span></span>

<span data-ttu-id="aa51c-270">Houd er rekening mee dat de correlatie-id's centraal staat in de diagnostische gegevens in de bibliotheek zijn.</span><span class="sxs-lookup"><span data-stu-id="aa51c-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="aa51c-271">U kunt instellen dat uw correlatie id's op basis van per aanvraag als u wilt een ADAL correleren met andere bewerkingen zijn in uw code aanvragen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="aa51c-272">Als u een correlatie-ID niet instelt, wordt de ADAL een willekeurige token genereren.</span><span class="sxs-lookup"><span data-stu-id="aa51c-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="aa51c-273">Alle berichten logboekbestanden en netwerk aanroepen wordt vervolgens wordt voorzien van de correlatie-ID.</span><span class="sxs-lookup"><span data-stu-id="aa51c-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="aa51c-274">De automatisch gegenereerde ID wijzigingen bij elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="aa51c-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="aa51c-275">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="aa51c-275">Exceptions</span></span>
<span data-ttu-id="aa51c-276">Uitzonderingen zijn de eerste diagnose.</span><span class="sxs-lookup"><span data-stu-id="aa51c-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="aa51c-277">We proberen te bieden handige foutberichten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="aa51c-278">Als u een die niet handig vinden, Controleer het bestand een probleem en laat ons weten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="aa51c-279">Apparaatgegevens zoals model en SDK getal bevatten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="aa51c-280">Logboeken</span><span class="sxs-lookup"><span data-stu-id="aa51c-280">Logs</span></span>
<span data-ttu-id="aa51c-281">U kunt de bibliotheek voor het genereren van logboekberichten die u gebruiken kunt om u te helpen bij het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="aa51c-282">U kunt logboekregistratie configureren door het maken van de volgende oproep verzenden voor het configureren van een callback die ADAL aan de hand uit elk logboekbericht gebruiken zoals deze wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="aa51c-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="aa51c-283">Berichten kunnen worden geschreven naar een aangepaste logboekbestand, zoals wordt weergegeven in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="aa51c-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="aa51c-284">Er is geen standaardmethode voor het ophalen van Logboeken vanaf een apparaat.</span><span class="sxs-lookup"><span data-stu-id="aa51c-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="aa51c-285">Er zijn bepaalde services waarmee u kunnen met deze.</span><span class="sxs-lookup"><span data-stu-id="aa51c-285">There are some services that can help you with this.</span></span> <span data-ttu-id="aa51c-286">U kunt ook uw eigen, zoals het verzenden van het bestand naar een server voor voorraad.</span><span class="sxs-lookup"><span data-stu-id="aa51c-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="aa51c-287">Dit zijn de registratieniveaus:</span><span class="sxs-lookup"><span data-stu-id="aa51c-287">These are the logging levels:</span></span>
* <span data-ttu-id="aa51c-288">Fout (uitzonderingen)</span><span class="sxs-lookup"><span data-stu-id="aa51c-288">Error (exceptions)</span></span>
* <span data-ttu-id="aa51c-289">Waarschuwen (waarschuwing)</span><span class="sxs-lookup"><span data-stu-id="aa51c-289">Warn (warning)</span></span>
* <span data-ttu-id="aa51c-290">Info (doelen)</span><span class="sxs-lookup"><span data-stu-id="aa51c-290">Info (information purposes)</span></span>
* <span data-ttu-id="aa51c-291">Uitgebreid (meer informatie)</span><span class="sxs-lookup"><span data-stu-id="aa51c-291">Verbose (more details)</span></span>

<span data-ttu-id="aa51c-292">U instellen het logboekniveau als volgt:</span><span class="sxs-lookup"><span data-stu-id="aa51c-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="aa51c-293">Alle berichten in het logboek zijn verzonden naar logcat, naast eventuele aangepaste logboek retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="aa51c-294">U kunt krijgen een logboek naar een bestand uit logcat als volgt:</span><span class="sxs-lookup"><span data-stu-id="aa51c-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="aa51c-295">Zie voor meer informatie over adb opdrachten de [logcat informatie over de Android-site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="aa51c-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="aa51c-296">Netwerktracering</span><span class="sxs-lookup"><span data-stu-id="aa51c-296">Network traces</span></span>
<span data-ttu-id="aa51c-297">U kunt verschillende hulpprogramma's gebruiken om vast te leggen van de HTTP-verkeer dat ADAL genereert.</span><span class="sxs-lookup"><span data-stu-id="aa51c-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="aa51c-298">Dit is vooral handig als u bekend met het OAuth-protocol bent of als u nodig hebt om Microsoft of andere ondersteuningskanalen diagnostische informatie te geven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="aa51c-299">Fiddler is de eenvoudigste hulpmiddel voor het traceren van HTTP.</span><span class="sxs-lookup"><span data-stu-id="aa51c-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="aa51c-300">Gebruik de volgende koppelingen in te stellen tot correct record ADAL-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="aa51c-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="aa51c-301">Voor een hulpprogramma zoals Fiddler of Jeroen nuttig voor tracering, moet u configureren om vast te leggen van niet-versleutelde SSL-verkeer.</span><span class="sxs-lookup"><span data-stu-id="aa51c-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="aa51c-302">Traceringen gegenereerd op deze manier kunnen zeer vertrouwelijke informatie zoals toegangstokens, gebruikersnamen en wachtwoorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="aa51c-303">Als u van productie-accounts gebruikmaakt, deze traceringen niet delen met derden.</span><span class="sxs-lookup"><span data-stu-id="aa51c-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="aa51c-304">Als u nodig hebt om op te geven van een tracering voor iemand om ondersteuning krijgen, reproduceer het probleem met behulp van een tijdelijke rekening met gebruikersnamen en wachtwoorden op dat u geen rekening met het delen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="aa51c-305">Van de website Telerik: [instelling Up Fiddler voor Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="aa51c-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="aa51c-306">Vanuit GitHub: [Fiddler regels configureren voor ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="aa51c-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="aa51c-307">Dialoogvenster modus</span><span class="sxs-lookup"><span data-stu-id="aa51c-307">Dialog mode</span></span>
<span data-ttu-id="aa51c-308">De methode acquireToken zonder activiteit ondersteunt een dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa51c-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="aa51c-309">Versleuteling</span><span class="sxs-lookup"><span data-stu-id="aa51c-309">Encryption</span></span>
<span data-ttu-id="aa51c-310">ADAL versleutelt de tokens en opslaan in SharedPreferences standaard.</span><span class="sxs-lookup"><span data-stu-id="aa51c-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="aa51c-311">U kunt zoeken op de klasse StorageHelper om de details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="aa51c-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="aa51c-312">Android Keystore android geïntroduceerd voor 4.3 (API 18) veilige opslag van persoonlijke sleutels.</span><span class="sxs-lookup"><span data-stu-id="aa51c-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="aa51c-313">ADAL gebruikt voor API 18 en hoger.</span><span class="sxs-lookup"><span data-stu-id="aa51c-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="aa51c-314">Als u gebruikmaken van ADAL voor lagere SDK-versies wilt, moet u een geheime sleutel op AuthenticationSettings.INSTANCE.setSecretKey bieden.</span><span class="sxs-lookup"><span data-stu-id="aa51c-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="aa51c-315">OAuth2 bearer uitdaging</span><span class="sxs-lookup"><span data-stu-id="aa51c-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="aa51c-316">De klasse AuthenticationParameters biedt functionaliteit om authorization_uri ophalen uit de OAuth2 bearer-uitdaging.</span><span class="sxs-lookup"><span data-stu-id="aa51c-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="aa51c-317">Sessiecookies in webweergave</span><span class="sxs-lookup"><span data-stu-id="aa51c-317">Session cookies in WebView</span></span>
<span data-ttu-id="aa51c-318">Android webweergave wist niet sessiecookies nadat de app is gesloten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="aa51c-319">U kunt die verwerkt met behulp van deze voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="aa51c-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="aa51c-320">Zie voor meer informatie over cookies de [CookieSyncManager informatie over de Android-site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="aa51c-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="aa51c-321">Resource-onderdrukkingen</span><span class="sxs-lookup"><span data-stu-id="aa51c-321">Resource overrides</span></span>
<span data-ttu-id="aa51c-322">De ADAL-bibliotheek bevat Engelse tekenreeksen voor de ProgressDialog berichten.</span><span class="sxs-lookup"><span data-stu-id="aa51c-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="aa51c-323">Uw toepassing moet ze als u gelokaliseerde tekenreeksen wilt overschrijven.</span><span class="sxs-lookup"><span data-stu-id="aa51c-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="aa51c-324">Dialoogvenster NTLM</span><span class="sxs-lookup"><span data-stu-id="aa51c-324">NTLM dialog box</span></span>
<span data-ttu-id="aa51c-325">ADAL-versie 1.1.0 ondersteunt een NTLM-dialoogvenster dat wordt verwerkt door de gebeurtenis onReceivedHttpAuthRequest van WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="aa51c-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="aa51c-326">U kunt de tekenreeksen voor het dialoogvenster met de indeling en aanpassen.</span><span class="sxs-lookup"><span data-stu-id="aa51c-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="aa51c-327">Cross-app eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa51c-327">Cross-app SSO</span></span>
<span data-ttu-id="aa51c-328">Meer informatie over [het inschakelen van eenmalige aanmelding voor cross-app voor Android met behulp van ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="aa51c-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
