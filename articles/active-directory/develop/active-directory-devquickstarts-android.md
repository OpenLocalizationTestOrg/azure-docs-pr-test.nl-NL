---
title: aaaAzure AD Android aan de slag | Microsoft Docs
description: Hoe beveiligd toobuild een Android-toepassing die met Azure AD voor aanmelden en Azure AD-aanroepen integreert API's met behulp van OAuth.
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
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="4c278-103">Azure AD integreren met een Android-app</span><span class="sxs-lookup"><span data-stu-id="4c278-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="4c278-104">Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/Android), die helpt u bij leren werken met Azure AD in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="4c278-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="4c278-105">Hallo-portal voor ontwikkelaars begeleidt u door Hallo van een app registreren en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="4c278-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="4c278-106">Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="4c278-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="4c278-107">Als u een bureaubladtoepassing ontwikkelt, kunt Azure Active Directory (Azure AD) u eenvoudig en snel voor tooauthenticate u uw gebruikers via hun lokale Active Directory-accounts.</span><span class="sxs-lookup"><span data-stu-id="4c278-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="4c278-108">Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="4c278-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="4c278-109">Azure AD levert voor Android-clients die tooaccess beveiligde bronnen nodig Hallo Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="4c278-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="4c278-110">Hallo enig doel van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="4c278-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="4c278-111">hoe eenvoudig het is, gaan we gaat verder met een takenlijst Android-toepassing die toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="4c278-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="4c278-112">Krijgt toegang tot tokens voor een taak lijst-API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c278-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="4c278-113">De takenlijst van een gebruiker opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4c278-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="4c278-114">Tekenen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4c278-114">Signs out users.</span></span>

<span data-ttu-id="4c278-115">tooget gestart, moet u een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="4c278-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="4c278-116">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="4c278-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="4c278-117">Stap 1: Download en Hallo Node.js REST-API TODO voorbeeldserver wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4c278-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="4c278-118">Hallo Node.js REST-API TODO voorbeeld geschreven specifiek toowork tegen onze huidige voorbeeld voor het bouwen van een één-tenant taak REST-API voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c278-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="4c278-119">Dit is een vereiste voor Hallo snel starten.</span><span class="sxs-lookup"><span data-stu-id="4c278-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="4c278-120">Voor informatie over hoe tooset dit, Zie onze bestaande voorbeelden in [Microsoft Azure Active Directory-voorbeeld REST API-Service voor Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4c278-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="4c278-121">Stap 2: Uw web-API registreren bij uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="4c278-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="4c278-122">Active Directory ondersteunt twee soorten toepassingen toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="4c278-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="4c278-123">Web-API's die worden geboden door services toousers</span><span class="sxs-lookup"><span data-stu-id="4c278-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="4c278-124">Toepassingen (die worden uitgevoerd op Hallo web of op een apparaat) die toegang hebben tot de web-API 's</span><span class="sxs-lookup"><span data-stu-id="4c278-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="4c278-125">U bent Hallo web-API die u lokaal worden uitgevoerd voor het testen van dit voorbeeld wordt geregistreerd in deze stap.</span><span class="sxs-lookup"><span data-stu-id="4c278-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="4c278-126">Deze web-API is normaal gesproken een REST-service die aanbieding functionaliteit die u wilt een app-tooaccess is.</span><span class="sxs-lookup"><span data-stu-id="4c278-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="4c278-127">Azure AD kunt een willekeurig eindpunt beschermen.</span><span class="sxs-lookup"><span data-stu-id="4c278-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="4c278-128">We ervan uit dat u bent u registreert Hallo TODO waarnaar wordt verwezen eerder REST-API.</span><span class="sxs-lookup"><span data-stu-id="4c278-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="4c278-129">Maar dit werkt voor alle web-API die u wilt dat Azure Active Directory toohelp beveiligen.</span><span class="sxs-lookup"><span data-stu-id="4c278-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="4c278-130">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c278-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c278-131">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="4c278-131">On hello top bar, click your account.</span></span> <span data-ttu-id="4c278-132">In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c278-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="4c278-133">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c278-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4c278-134">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4c278-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4c278-135">Een beschrijvende naam voor de toepassing hello (bijvoorbeeld **TodoListService**), selecteer **webtoepassing en/of Web-API**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4c278-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="4c278-136">Voer voor Hallo aanmeldings-URL, Hallo basis-URL voor Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4c278-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="4c278-137">Dit is standaard `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="4c278-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="4c278-138">Klik op **OK** toocomplete Hallo registratie.</span><span class="sxs-lookup"><span data-stu-id="4c278-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="4c278-139">Terwijl u nog steeds in hello Azure-portal, Ga tooyour toepassingspagina, Hallo toepassing id-waarde vinden en kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4c278-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="4c278-140">U hebt dit later nodig bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c278-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="4c278-141">Van Hallo **instellingen** -> **eigenschappen** pagina, Hallo app ID URI bijwerken - Voer `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="4c278-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="4c278-142">Vervang `<your_tenant_name>` met Hallo-naam van uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="4c278-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="4c278-143">Stap 3: De voorbeeldtoepassing Android Native Client Hallo registreren</span><span class="sxs-lookup"><span data-stu-id="4c278-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="4c278-144">In dit voorbeeld moet u uw webtoepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="4c278-144">You must register your web application in this sample.</span></span> <span data-ttu-id="4c278-145">Hiermee kunt uw toepassing toocommunicate met Hallo zojuist hebt geregistreerd web-API.</span><span class="sxs-lookup"><span data-stu-id="4c278-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="4c278-146">Azure AD weigert tooeven toestaan uw toepassing tooask voor aanmelden, tenzij deze is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4c278-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="4c278-147">Die uitmaakt deel van Hallo beveiliging van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="4c278-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="4c278-148">We ervan uit dat u bent u registreert Hallo voorbeeldtoepassing eerder verwezen.</span><span class="sxs-lookup"><span data-stu-id="4c278-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="4c278-149">Maar deze procedure werkt voor elke app die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="4c278-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="4c278-150">U vraagt zich misschien af waarom u een toepassing en een web-API wilt opslaan in een tenant.</span><span class="sxs-lookup"><span data-stu-id="4c278-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="4c278-151">Als u mogelijk hebt geraden, kunt u een app die toegang heeft tot een externe API die is geregistreerd in Azure AD van een andere tenant.</span><span class="sxs-lookup"><span data-stu-id="4c278-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="4c278-152">Als u dat doet, uw klanten zich tooconsent toohello gebruik van Hallo API in de toepassing hello gevraagd.</span><span class="sxs-lookup"><span data-stu-id="4c278-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="4c278-153">Active Directory Authentication Library voor iOS zorgt voor deze toestemming voor u.</span><span class="sxs-lookup"><span data-stu-id="4c278-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="4c278-154">Als we geavanceerdere functies, verkennen, ziet u dat dit een belangrijk onderdeel van Hallo werk nodig tooaccess Hallo suite van Microsoft APIs van Azure en Office, evenals andere serviceprovider is.</span><span class="sxs-lookup"><span data-stu-id="4c278-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="4c278-155">Op dit moment omdat u zowel uw web-API en uw toepassing onder Hallo geregistreerd dezelfde tenant, ziet u niet de prompts om toestemming.</span><span class="sxs-lookup"><span data-stu-id="4c278-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="4c278-156">Dit is meestal Hallo geval als u een toepassing alleen voor uw eigen bedrijf toouse ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="4c278-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="4c278-157">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c278-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c278-158">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="4c278-158">On hello top bar, click your account.</span></span> <span data-ttu-id="4c278-159">In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c278-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="4c278-160">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c278-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4c278-161">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4c278-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4c278-162">Een beschrijvende naam voor de toepassing hello (bijvoorbeeld **TodoListClient Android**), selecteer **systeemeigen clienttoepassing**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4c278-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="4c278-163">Omleidings-URI voor hello, voert u `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="4c278-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="4c278-164">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="4c278-164">Click **Finish**.</span></span>
7. <span data-ttu-id="4c278-165">Hallo toepassing pagina Hallo toepassing id-waarde vinden en kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4c278-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="4c278-166">U hebt dit later nodig bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c278-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="4c278-167">Van Hallo **instellingen** pagina **Required Permissions** en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4c278-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="4c278-168">Zoek en selecteer TodoListService, Hallo toevoegen **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="4c278-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="4c278-169">toobuild met Maven, kunt u pom.xml op het hoogste niveau hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4c278-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="4c278-170">Deze opslagplaats klonen naar een map van uw keuze:</span><span class="sxs-lookup"><span data-stu-id="4c278-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="4c278-171">Volg de stappen Hallo in Hallo [tooset vereisten van uw omgeving Maven voor Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="4c278-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="4c278-172">Hallo-emulator met de SDK-19 instellen.</span><span class="sxs-lookup"><span data-stu-id="4c278-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="4c278-173">Ga toohello hoofdmap waar u Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4c278-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="4c278-174">Deze opdracht uitvoeren:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="4c278-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="4c278-175">Hallo directory toohello Quick Start voorbeeld wijzigen:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="4c278-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="4c278-176">Deze opdracht uitvoeren:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="4c278-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="4c278-177">U ziet Hallo app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4c278-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="4c278-178">Voer test gebruiker referenties tootry.</span><span class="sxs-lookup"><span data-stu-id="4c278-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="4c278-179">Naast Hallo AAR pakket worden JAR-pakketten verzonden.</span><span class="sxs-lookup"><span data-stu-id="4c278-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="4c278-180">Stap 4: Android ADAL Hallo downloaden en deze tooyour Eclipse werkruimte toevoegen</span><span class="sxs-lookup"><span data-stu-id="4c278-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="4c278-181">We hebt gemaakt dat u toohave meerdere opties toouse ADAL in uw Android-project:</span><span class="sxs-lookup"><span data-stu-id="4c278-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="4c278-182">U kunt Hallo source code tooimport deze bibliotheek in Eclipse en koppeling tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c278-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="4c278-183">Als u Android Studio, kunt u Hallo AAR pakket indeling en verwijzing Hallo binaire bestanden.</span><span class="sxs-lookup"><span data-stu-id="4c278-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="4c278-184">Optie 1: Bron Zip</span><span class="sxs-lookup"><span data-stu-id="4c278-184">Option 1: Source Zip</span></span>
<span data-ttu-id="4c278-185">toodownload een kopie van de broncode hello, klikt u op **ZIP downloaden** aan de rechterkant Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="4c278-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="4c278-186">U kunt [downloaden vanuit GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="4c278-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="4c278-187">Optie 2: Bron via Git</span><span class="sxs-lookup"><span data-stu-id="4c278-187">Option 2: Source via Git</span></span>
<span data-ttu-id="4c278-188">tooget hello broncode Hallo SDK via Git, typt u:</span><span class="sxs-lookup"><span data-stu-id="4c278-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="4c278-189">Optie 3: Binaire bestanden via Gradle</span><span class="sxs-lookup"><span data-stu-id="4c278-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="4c278-190">U kunt Hallo binaire bestanden ophalen uit Hallo Maven centrale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4c278-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="4c278-191">Hallo AAR pakket kan als volgt worden opgenomen in uw project in Android Studio:</span><span class="sxs-lookup"><span data-stu-id="4c278-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="4c278-192">Optie 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="4c278-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="4c278-193">Als u Hallo M2Eclipse invoegtoepassing gebruikt, kunt u Hallo afhankelijkheid opgeven in het bestand pom.xml:</span><span class="sxs-lookup"><span data-stu-id="4c278-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="4c278-194">Optie 5: JAR-pakket in de map libs Hallo</span><span class="sxs-lookup"><span data-stu-id="4c278-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="4c278-195">U kunt ophalen Hallo JAR-bestand uit Hallo Maven opslagplaats en zet het neer in Hallo **bibliotheken** map in uw project.</span><span class="sxs-lookup"><span data-stu-id="4c278-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="4c278-196">U moet toocopy Hallo vereiste resources tooyour project, omdat Hallo JAR pakketten niet opnemen.</span><span class="sxs-lookup"><span data-stu-id="4c278-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="4c278-197">Stap 5: Verwijzingen tooAndroid ADAL tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="4c278-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="4c278-198">Voeg een verwijzing tooyour-project en dit opgeven als een Android-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="4c278-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="4c278-199">Als u niet zeker hoe toodo, krijgt u meer informatie over het Hallo [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="4c278-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="4c278-200">Hallo project afhankelijkheid voor foutopsporing in de instellingen van uw project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c278-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="4c278-201">Bijwerken van uw project AndroidManifest.xml bestand tooinclude:</span><span class="sxs-lookup"><span data-stu-id="4c278-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

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

4. <span data-ttu-id="4c278-202">Een exemplaar van AuthenticationContext op uw belangrijkste activiteit maken.</span><span class="sxs-lookup"><span data-stu-id="4c278-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="4c278-203">Hallo-details van deze aanroep zijn buiten bereik Hallo van dit onderwerp, maar u kunt een goede start door te kijken Hallo [Android Native Client voorbeeld](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="4c278-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="4c278-204">In Hallo voorbeeld te volgen, SharedPreferences Hallo standaardcache is en instantie in de vorm van Hallo `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="4c278-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="4c278-205">Kopieer deze code blok toohandle Hallo einde van AuthenticationActivity nadat Hallo gebruiker referenties invoert en een autorisatiecode ontvangt:</span><span class="sxs-lookup"><span data-stu-id="4c278-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="4c278-206">tooask voor een token een retouraanroep definiëren:</span><span class="sxs-lookup"><span data-stu-id="4c278-206">tooask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="4c278-207">Ten slotte vragen voor een token met behulp van terugbellen:</span><span class="sxs-lookup"><span data-stu-id="4c278-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="4c278-208">Hier volgt een uitleg van Hallo parameters:</span><span class="sxs-lookup"><span data-stu-id="4c278-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="4c278-209">*resource* is vereist en u probeert tooaccess Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="4c278-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="4c278-210">*clientid* is vereist en afkomstig zijn van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c278-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="4c278-211">*RedirectUri* is niet vereist toobe hello acquireToken aanroep voorzien.</span><span class="sxs-lookup"><span data-stu-id="4c278-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="4c278-212">U kunt instellen deze als de pakketnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="4c278-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="4c278-213">*PromptBehavior* helpt tooask voor referenties tooskip Hallo cache en cookie.</span><span class="sxs-lookup"><span data-stu-id="4c278-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="4c278-214">*callback* wordt aangeroepen nadat de autorisatiecode Hallo worden uitgewisseld voor een token.</span><span class="sxs-lookup"><span data-stu-id="4c278-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="4c278-215">Heeft een object van het AuthenticationResult waarvoor toegangstoken, datum verlopen en ID token-informatie.</span><span class="sxs-lookup"><span data-stu-id="4c278-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="4c278-216">*acquireTokenSilent* is optioneel.</span><span class="sxs-lookup"><span data-stu-id="4c278-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="4c278-217">U kunt deze aanroepen toohandle opslaan in cache en token vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="4c278-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="4c278-218">Het bevat ook Hallo synchronisatieversie.</span><span class="sxs-lookup"><span data-stu-id="4c278-218">It also provides hello sync version.</span></span> <span data-ttu-id="4c278-219">De cmdlet accepteert *userId* als parameter.</span><span class="sxs-lookup"><span data-stu-id="4c278-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="4c278-220">Met behulp van dit scenario hebt u wat u moet toosuccessfully integreren met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c278-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="4c278-221">Voor meer voorbeelden van deze werken, gaat u naar Hallo AzureADSamples / opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c278-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="4c278-222">Belangrijke informatie</span><span class="sxs-lookup"><span data-stu-id="4c278-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="4c278-223">Aanpassing</span><span class="sxs-lookup"><span data-stu-id="4c278-223">Customization</span></span>
<span data-ttu-id="4c278-224">Uw toepassingsresources kunnen project bibliotheekresources overschrijven.</span><span class="sxs-lookup"><span data-stu-id="4c278-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="4c278-225">Dit gebeurt wanneer uw app wordt samengesteld.</span><span class="sxs-lookup"><span data-stu-id="4c278-225">This happens when your app is being built.</span></span> <span data-ttu-id="4c278-226">Daarom kunt u verificatie activiteit indeling Hallo zoals die u wilt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4c278-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="4c278-227">Ervoor tookeep Hallo-id van Hallo besturingselementen die ADAL (webweergave) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4c278-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="4c278-228">Broker</span><span class="sxs-lookup"><span data-stu-id="4c278-228">Broker</span></span>
<span data-ttu-id="4c278-229">Hallo Microsoft Intune-bedrijfsportal-app biedt Hallo broker onderdeel.</span><span class="sxs-lookup"><span data-stu-id="4c278-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="4c278-230">Hallo-account wordt gemaakt in AccountManager.</span><span class="sxs-lookup"><span data-stu-id="4c278-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="4c278-231">Hallo-accounttype is 'com.microsoft.workaccount'.</span><span class="sxs-lookup"><span data-stu-id="4c278-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="4c278-232">AccountManager kan slechts één SSO-account.</span><span class="sxs-lookup"><span data-stu-id="4c278-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="4c278-233">Maakt een SSO-cookie voor Hallo gebruiker na het voltooien van Hallo apparaat uitdaging voor een Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="4c278-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="4c278-234">ADAL hello broker account wordt gebruikt als een gebruikersaccount op deze verificator wordt gemaakt en u ervoor geen tooskip kiest deze.</span><span class="sxs-lookup"><span data-stu-id="4c278-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="4c278-235">U kunt doorgaan Hallo broker gebruiker met:</span><span class="sxs-lookup"><span data-stu-id="4c278-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="4c278-236">Een speciale RedirectUri tooregister moet u voor het gebruik van de broker.</span><span class="sxs-lookup"><span data-stu-id="4c278-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="4c278-237">RedirectUri is Hallo notatie `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="4c278-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="4c278-238">U kunt uw RedirectUri ophalen voor uw app met behulp van Hallo script brokerRedirectPrint.ps1 of Hallo API-aanroep mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="4c278-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="4c278-239">Hallo-handtekening is gerelateerde tooyour ondertekenen van certificaten.</span><span class="sxs-lookup"><span data-stu-id="4c278-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="4c278-240">Hallo huidige broker model is voor één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4c278-240">hello current broker model is for one user.</span></span> <span data-ttu-id="4c278-241">AuthenticationContext biedt Hallo API methode tooget Hallo broker gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4c278-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="4c278-242">Uw app-manifest hebt Hallo machtigingen toouse AccountManager accounts te volgen.</span><span class="sxs-lookup"><span data-stu-id="4c278-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="4c278-243">Zie voor meer informatie, Hallo [AccountManager informatie over Android-site Hallo](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="4c278-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="4c278-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="4c278-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="4c278-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="4c278-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="4c278-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="4c278-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="4c278-247">Instantie-URL en AD FS</span><span class="sxs-lookup"><span data-stu-id="4c278-247">Authority URL and AD FS</span></span>
<span data-ttu-id="4c278-248">Active Directory Federation Services (AD FS) is niet herkend als productie STS, zodat u tooturn van exemplaar van detectie moet en geef ' false ' op Hallo AuthenticationContext constructor.</span><span class="sxs-lookup"><span data-stu-id="4c278-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="4c278-249">Hallo-instantie URL moet een STS-exemplaar en een [tenantnaam](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4c278-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="4c278-250">Opvragen van cache-items</span><span class="sxs-lookup"><span data-stu-id="4c278-250">Querying cache items</span></span>
<span data-ttu-id="4c278-251">ADAL biedt een standaardcache in SharedPreferences met enkele eenvoudige cache queryfuncties.</span><span class="sxs-lookup"><span data-stu-id="4c278-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="4c278-252">U kunt de huidige cache Hallo krijgen van AuthenticationContext met behulp van:</span><span class="sxs-lookup"><span data-stu-id="4c278-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="4c278-253">U kunt ook uw cache-implementatie opgeven als u wilt dat toocustomize deze.</span><span class="sxs-lookup"><span data-stu-id="4c278-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="4c278-254">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="4c278-254">Prompt behavior</span></span>
<span data-ttu-id="4c278-255">ADAL biedt een optie toospecify vragen gedrag.</span><span class="sxs-lookup"><span data-stu-id="4c278-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="4c278-256">PromptBehavior.Auto wordt Hallo gebruikersinterface weergegeven als het vernieuwingstoken Hallo ongeldig is en gebruikersreferenties vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="4c278-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="4c278-257">PromptBehavior.Always wordt Hallo cache gebruik overslaan en altijd weergeven Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="4c278-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="4c278-258">Achtergrond tokenaanvraag uit de cache en vernieuwen</span><span class="sxs-lookup"><span data-stu-id="4c278-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="4c278-259">Een achtergrond tokenaanvraag gebruikt geen Hallo pop-UI en vereist geen een activiteit.</span><span class="sxs-lookup"><span data-stu-id="4c278-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="4c278-260">Het resultaat een token uit cache Hallo indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4c278-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="4c278-261">Als het Hallo-token is verlopen, deze methode toorefresh probeert deze.</span><span class="sxs-lookup"><span data-stu-id="4c278-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="4c278-262">Als het Hallo-vernieuwingstoken is verlopen of is mislukt, wordt AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="4c278-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="4c278-263">U kunt een synchronisatie met deze methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4c278-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="4c278-264">U kunt instellen null toocallback of acquireTokenSilentSync gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4c278-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="4c278-265">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="4c278-265">Diagnostics</span></span>
<span data-ttu-id="4c278-266">Hallo primaire bronnen met informatie voor het oplossen van problemen zijn:</span><span class="sxs-lookup"><span data-stu-id="4c278-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="4c278-267">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="4c278-267">Exceptions</span></span>
* <span data-ttu-id="4c278-268">Logboeken</span><span class="sxs-lookup"><span data-stu-id="4c278-268">Logs</span></span>
* <span data-ttu-id="4c278-269">Netwerktracering</span><span class="sxs-lookup"><span data-stu-id="4c278-269">Network traces</span></span>

<span data-ttu-id="4c278-270">Houd er rekening mee dat correlatie-id's centrale toohello diagnostics in Hallo-bibliotheek zijn.</span><span class="sxs-lookup"><span data-stu-id="4c278-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="4c278-271">U kunt de correlatie-id's op basis van per aanvraag instellen als u wilt dat toocorrelate een ADAL aanvragen met andere bewerkingen zijn in uw code.</span><span class="sxs-lookup"><span data-stu-id="4c278-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="4c278-272">Als u een correlatie-ID niet instelt, wordt de ADAL een willekeurige token genereren.</span><span class="sxs-lookup"><span data-stu-id="4c278-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="4c278-273">Alle berichten logboekbestanden en netwerk aanroepen wordt vervolgens wordt voorzien van Hallo correlatie-ID.</span><span class="sxs-lookup"><span data-stu-id="4c278-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="4c278-274">Hallo zelfgegenereerd ID wijzigingen bij elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4c278-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="4c278-275">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="4c278-275">Exceptions</span></span>
<span data-ttu-id="4c278-276">Uitzonderingen worden eerst diagnostische Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c278-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="4c278-277">We proberen tooprovide handig foutberichten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c278-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="4c278-278">Als u een die niet handig vinden, Controleer het bestand een probleem en laat ons weten.</span><span class="sxs-lookup"><span data-stu-id="4c278-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="4c278-279">Apparaatgegevens zoals model en SDK getal bevatten.</span><span class="sxs-lookup"><span data-stu-id="4c278-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="4c278-280">Logboeken</span><span class="sxs-lookup"><span data-stu-id="4c278-280">Logs</span></span>
<span data-ttu-id="4c278-281">U kunt Hallo bibliotheek toogenerate configureren waarmee u toohelp kunt logboekberichten vaststellen van problemen.</span><span class="sxs-lookup"><span data-stu-id="4c278-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="4c278-282">U kunt logboekregistratie configureren doordat Hallo volgende aanroepen tooconfigure een retouraanroep dat ADAL toohand uit elk logboekbericht gebruiken zoals deze wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4c278-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="4c278-283">Berichten kunnen worden geschreven worden tooa aangepaste logboekbestand, zoals wordt weergegeven in de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c278-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="4c278-284">Er is geen standaardmethode voor het ophalen van Logboeken vanaf een apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c278-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="4c278-285">Er zijn bepaalde services waarmee u kunnen met deze.</span><span class="sxs-lookup"><span data-stu-id="4c278-285">There are some services that can help you with this.</span></span> <span data-ttu-id="4c278-286">U kunt ook uw eigen zoals verzenden Hallo tooa bestandsserver tot.</span><span class="sxs-lookup"><span data-stu-id="4c278-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="4c278-287">Dit zijn de registratieniveaus Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c278-287">These are hello logging levels:</span></span>
* <span data-ttu-id="4c278-288">Fout (uitzonderingen)</span><span class="sxs-lookup"><span data-stu-id="4c278-288">Error (exceptions)</span></span>
* <span data-ttu-id="4c278-289">Waarschuwen (waarschuwing)</span><span class="sxs-lookup"><span data-stu-id="4c278-289">Warn (warning)</span></span>
* <span data-ttu-id="4c278-290">Info (doelen)</span><span class="sxs-lookup"><span data-stu-id="4c278-290">Info (information purposes)</span></span>
* <span data-ttu-id="4c278-291">Uitgebreid (meer informatie)</span><span class="sxs-lookup"><span data-stu-id="4c278-291">Verbose (more details)</span></span>

<span data-ttu-id="4c278-292">U instellen Hallo logboekniveau als volgt:</span><span class="sxs-lookup"><span data-stu-id="4c278-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="4c278-293">Alle berichten in het logboek worden toevoeging tooany aangepaste logboek retouraanroepen toologcat, verzonden.</span><span class="sxs-lookup"><span data-stu-id="4c278-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="4c278-294">U kunt als volgt een logboekbestand tooa van logcat krijgen:</span><span class="sxs-lookup"><span data-stu-id="4c278-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="4c278-295">Zie voor meer informatie over adb opdrachten Hallo [logcat informatie over Android-site Hallo](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="4c278-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="4c278-296">Netwerktracering</span><span class="sxs-lookup"><span data-stu-id="4c278-296">Network traces</span></span>
<span data-ttu-id="4c278-297">U kunt verschillende hulpprogramma's voor toocapture Hallo HTTP-verkeer dat ADAL genereert.</span><span class="sxs-lookup"><span data-stu-id="4c278-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="4c278-298">Dit is vooral handig als u bekend met de Hallo OAuth-protocol bent of als u tooprovide diagnostische gegevens tooMicrosoft of andere ondersteuningskanalen nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="4c278-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="4c278-299">Fiddler is Hallo-hulpmiddel voor het traceren van eenvoudigste HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c278-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="4c278-300">Gebruik Hallo volgende koppelingen tooset het toocorrectly record ADAL-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="4c278-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="4c278-301">Voor een tracering hulpprogramma zoals Fiddler of Jeroen toobe nuttig, moet u deze configureren toorecord ongecodeerd SSL-verkeer.</span><span class="sxs-lookup"><span data-stu-id="4c278-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="4c278-302">Traceringen gegenereerd op deze manier kunnen zeer vertrouwelijke informatie zoals toegangstokens, gebruikersnamen en wachtwoorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="4c278-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="4c278-303">Als u van productie-accounts gebruikmaakt, deze traceringen niet delen met derden.</span><span class="sxs-lookup"><span data-stu-id="4c278-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="4c278-304">Als u een toosomeone tracering in de volgorde tooget ondersteuning toosupply moet, reproduceren Hallo probleem met behulp van een tijdelijke rekening met gebruikersnamen en wachtwoorden dat wel delen.</span><span class="sxs-lookup"><span data-stu-id="4c278-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="4c278-305">Van Hallo Telerik website: [instelling Up Fiddler voor Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="4c278-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="4c278-306">Vanuit GitHub: [Fiddler regels configureren voor ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="4c278-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="4c278-307">Dialoogvenster modus</span><span class="sxs-lookup"><span data-stu-id="4c278-307">Dialog mode</span></span>
<span data-ttu-id="4c278-308">Hallo acquireToken methode zonder activiteit ondersteunt een dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c278-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="4c278-309">Versleuteling</span><span class="sxs-lookup"><span data-stu-id="4c278-309">Encryption</span></span>
<span data-ttu-id="4c278-310">ADAL versleutelt Hallo tokens en opslaan in SharedPreferences standaard.</span><span class="sxs-lookup"><span data-stu-id="4c278-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="4c278-311">U kunt zoeken op Hallo StorageHelper klasse toosee Hallo details.</span><span class="sxs-lookup"><span data-stu-id="4c278-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="4c278-312">Android Keystore android geïntroduceerd voor 4.3 (API 18) veilige opslag van persoonlijke sleutels.</span><span class="sxs-lookup"><span data-stu-id="4c278-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="4c278-313">ADAL gebruikt voor API 18 en hoger.</span><span class="sxs-lookup"><span data-stu-id="4c278-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="4c278-314">Als u wilt dat toouse ADAL voor lagere SDK-versies, moet u een geheime sleutel op AuthenticationSettings.INSTANCE.setSecretKey tooprovide.</span><span class="sxs-lookup"><span data-stu-id="4c278-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="4c278-315">OAuth2 bearer uitdaging</span><span class="sxs-lookup"><span data-stu-id="4c278-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="4c278-316">Hallo AuthenticationParameters klasse biedt functionaliteit tooget authorization_uri van Hallo OAuth2 bearer uitdaging.</span><span class="sxs-lookup"><span data-stu-id="4c278-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="4c278-317">Sessiecookies in webweergave</span><span class="sxs-lookup"><span data-stu-id="4c278-317">Session cookies in WebView</span></span>
<span data-ttu-id="4c278-318">Android webweergave wist niet sessiecookies nadat Hallo app is gesloten.</span><span class="sxs-lookup"><span data-stu-id="4c278-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="4c278-319">U kunt die verwerkt met behulp van deze voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="4c278-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="4c278-320">Zie voor meer informatie over cookies Hallo [CookieSyncManager informatie over Android-site Hallo](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="4c278-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="4c278-321">Resource-onderdrukkingen</span><span class="sxs-lookup"><span data-stu-id="4c278-321">Resource overrides</span></span>
<span data-ttu-id="4c278-322">Hallo ADAL-bibliotheek bevat Engelse tekenreeksen voor de ProgressDialog berichten.</span><span class="sxs-lookup"><span data-stu-id="4c278-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="4c278-323">Uw toepassing moet ze als u gelokaliseerde tekenreeksen wilt overschrijven.</span><span class="sxs-lookup"><span data-stu-id="4c278-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="4c278-324">Dialoogvenster NTLM</span><span class="sxs-lookup"><span data-stu-id="4c278-324">NTLM dialog box</span></span>
<span data-ttu-id="4c278-325">ADAL-versie 1.1.0 ondersteunt een NTLM-dialoogvenster dat wordt verwerkt via Hallo onReceivedHttpAuthRequest gebeurtenis uit WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="4c278-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="4c278-326">U kunt Hallo indeling en tekenreeksen voor dialoogvenster Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4c278-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="4c278-327">Cross-app eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c278-327">Cross-app SSO</span></span>
<span data-ttu-id="4c278-328">Meer informatie over [hoe tooenable SSO cross-app voor Android met behulp van ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="4c278-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
