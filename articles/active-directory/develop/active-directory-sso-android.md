---
title: aaaHow tooenable SSO cross-app voor Android met behulp van ADAL | Microsoft Docs
description: 'Hoe Hallo toouse Hallo functies van ADAL SDK tooenable eenmalige aanmelding via uw toepassingen. '
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="7e72a-103">Hoe tooenable SSO cross-app voor Android met behulp van ADAL</span><span class="sxs-lookup"><span data-stu-id="7e72a-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="7e72a-104">Eenmalige aanmelding (SSO) bieden zodat gebruikers alleen tooenter eenmaal hun referenties nodig en deze referenties automatisch werk verschillende toepassingen hebben wordt nu door klanten verwacht.</span><span class="sxs-lookup"><span data-stu-id="7e72a-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="7e72a-105">Hallo problemen in hun gebruikersnaam en wachtwoord invoeren op een klein scherm, vaak keren gecombineerd met een extra factor (2FA), zoals een telefoongesprek of ge-code, resulteert in een snelle ergernis als een gebruiker heeft toodo dit meer dan één keer voor het product.</span><span class="sxs-lookup"><span data-stu-id="7e72a-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="7e72a-106">Bovendien, als u een identiteitsplatform die van andere toepassingen zoals Microsoft-Accounts of een werkaccount van Office365 gebruikmaken mogelijk toepast, verwachten klanten dat deze referenties toobe toouse beschikbaar op alle toepassingen met hun Hallo leverancier niet van belang.</span><span class="sxs-lookup"><span data-stu-id="7e72a-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="7e72a-107">Hallo Microsoft Identity-platform, samen met onze SDK's van Microsoft Identity komt dit harde werk voor u en geeft u de mogelijkheid toodelight Hallo uw klanten met eenmalige aanmelding bij uw eigen suite van toepassingen, of als met onze broker-functie en de verificator toepassingen in het hele apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e72a-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="7e72a-108">In dit scenario wordt uitgelegd hoe tooconfigure onze SDK in uw toepassing tooprovide deze voordeel tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="7e72a-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="7e72a-109">In dit scenario is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="7e72a-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="7e72a-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e72a-110">Azure Active Directory</span></span>
* <span data-ttu-id="7e72a-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7e72a-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="7e72a-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="7e72a-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="7e72a-113">Voorwaardelijke toegang voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e72a-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="7e72a-114">Hallo document voorgaande wordt ervan uitgegaan dat u weet hoe te[inrichten van toepassingen in de oude portal Hallo voor Azure Active Directory](active-directory-how-to-integrate.md) en uw toepassing Hello geïntegreerd [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .</span><span class="sxs-lookup"><span data-stu-id="7e72a-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="7e72a-115">SSO-concepten in Hallo Identiteitsplatform van Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e72a-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="7e72a-116">Microsoft Identity Beleggingsmakelaars</span><span class="sxs-lookup"><span data-stu-id="7e72a-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="7e72a-117">Microsoft biedt voor elk mobiel platform-toepassingen die voor Hallo bridging van referenties voor toepassingen van verschillende leveranciers en kunt voor speciale verbeterde functies waarvoor een enkele veilige plaats waar toovalidate referenties.</span><span class="sxs-lookup"><span data-stu-id="7e72a-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="7e72a-118">We noemen deze **beleggingsmakelaars**.</span><span class="sxs-lookup"><span data-stu-id="7e72a-118">We call these **brokers**.</span></span> <span data-ttu-id="7e72a-119">Op iOS en Android zijn deze opgenomen in downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die enkele of alle Hallo apparaat voor hun werknemers beheert.</span><span class="sxs-lookup"><span data-stu-id="7e72a-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="7e72a-120">Deze beleggingsmakelaars ondersteuning voor het beheer van beveiliging voor sommige toepassingen of de hele Hallo-apparaat op basis van wat de IT-beheerders willen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="7e72a-121">In Windows, wordt deze functionaliteit verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="7e72a-122">We gebruiken deze beleggingsmakelaars en hoe uw klanten mogelijk ze in hun aanmelding stroom voor Hallo Microsoft Identity platform Lees verder voor meer informatie over het.</span><span class="sxs-lookup"><span data-stu-id="7e72a-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="7e72a-123">Patronen voor logboekregistratie in op mobiele apparaten</span><span class="sxs-lookup"><span data-stu-id="7e72a-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="7e72a-124">Toegang toocredentials op apparaten als volgt twee basispatronen voor Hallo Microsoft Identity-platform:</span><span class="sxs-lookup"><span data-stu-id="7e72a-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="7e72a-125">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="7e72a-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="7e72a-126">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="7e72a-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="7e72a-127">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="7e72a-127">Non-broker assisted logins</span></span>
<span data-ttu-id="7e72a-128">Niet-broker assisted aanmeldingen zijn aanmelding ervaringen die inline met de toepassing hello gebeuren en Hallo lokale opslag op Hallo-apparaat voor die toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7e72a-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="7e72a-129">Deze opslag kan worden gedeeld tussen toepassingen maar Hallo referenties zijn nauw gebonden toohello app of suite van apps met behulp van deze referentie.</span><span class="sxs-lookup"><span data-stu-id="7e72a-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="7e72a-130">U hebt waarschijnlijk is dit in veel mobiele toepassingen wanneer u een gebruikersnaam en wachtwoord in Hallo toepassing zelf invoert.</span><span class="sxs-lookup"><span data-stu-id="7e72a-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="7e72a-131">Deze aanmeldingen hebben Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7e72a-132">Er bestaat een gebruikerservaring volledig in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="7e72a-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="7e72a-133">Referenties kunnen worden gedeeld door toepassingen die zijn ondertekend door Hallo hetzelfde certificaat, een ervaring voor eenmalige aanmelding tooyour reeks toepassingen bieden.</span><span class="sxs-lookup"><span data-stu-id="7e72a-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="7e72a-134">Besturingselement rond Hallo ervaring met het aanmelden wordt verstrekt toohello toepassing vóór en na het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7e72a-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="7e72a-135">Deze aanmeldingen hebben Hallo volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7e72a-136">Kan niet-gebruikerservaring eenmalige aanmelding via alle apps die gebruikmaken van een Microsoft-Identity alleen via de Microsoft-Identities die uw toepassing is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7e72a-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="7e72a-137">Uw toepassing kan niet worden gebruikt met meer geavanceerde zakelijke functies zoals voorwaardelijke toegang of gebruik Hallo InTune reeks producten.</span><span class="sxs-lookup"><span data-stu-id="7e72a-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7e72a-138">Uw toepassing ondersteunt geen verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7e72a-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="7e72a-139">Hier volgt een weergave over de werking van Hallo Microsoft Identity SDK's met Hallo gedeelde opslag van uw toepassingen tooenable eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="7e72a-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="7e72a-140">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="7e72a-140">Broker assisted logins</span></span>
<span data-ttu-id="7e72a-141">Aanmeldingen Broker-ondersteunde zijn aanmelding ervaringen die optreden in Hallo broker toepassing en Hallo opslag en beveiliging van Hallo broker tooshare referenties gebruiken voor alle toepassingen die van toepassing hello Microsoft Identity platform op Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="7e72a-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="7e72a-142">Dit betekent dat uw toepassingen afhankelijk zijn van Hallo broker toosign gebruikers in.</span><span class="sxs-lookup"><span data-stu-id="7e72a-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="7e72a-143">Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die Hallo-apparaat voor de gebruiker beheert.</span><span class="sxs-lookup"><span data-stu-id="7e72a-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="7e72a-144">Een voorbeeld van dit type toepassing is Hallo Microsoft Authenticator-toepassing op iOS.</span><span class="sxs-lookup"><span data-stu-id="7e72a-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="7e72a-145">In Windows worden deze functionaliteit wordt verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="7e72a-146">Hallo-ervaring varieert per platform en kan verstoren toousers soms zijn als het niet correct worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="7e72a-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="7e72a-147">U kunt waarschijnlijk meest bekend zijn met dit patroon als u Hallo Facebook-toepassing is geïnstalleerd en Facebook-verbinding van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="7e72a-148">Hallo Hallo platform maakt gebruik van Microsoft Identity hetzelfde patroon.</span><span class="sxs-lookup"><span data-stu-id="7e72a-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="7e72a-149">Voor iOS leidt dit tooa 'overgang' animatie waarbij uw toepassing wordt verzonden toohello achtergrond tijdens Hallo Microsoft Authenticator toepassingen wordt geleverd toohello voorgrond voor Hallo gebruiker tooselect welk account wil toosign met.</span><span class="sxs-lookup"><span data-stu-id="7e72a-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="7e72a-150">Voor Android en Windows hello account kiezer boven op uw toepassing minder verstoren toohello gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7e72a-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="7e72a-151">Hoe Hallo broker opgehaald aangeroepen</span><span class="sxs-lookup"><span data-stu-id="7e72a-151">How hello broker gets invoked</span></span>
<span data-ttu-id="7e72a-152">Als een compatibel broker is geïnstalleerd op het Hallo-apparaat, zoals Hallo Microsoft Authenticator-toepassing hello Microsoft Identity-SDK's automatisch wordt werk van het Hallo-broker voor u wordt aangeroepen wanneer een gebruiker dat zij toolog aangeeft aan met een account van wensen Hallo Hallo Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="7e72a-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="7e72a-153">Dit account kan worden een persoonlijk Microsoft-Account, werk of schoolaccount of een account dat u opgeeft en host in Azure met behulp van onze producten B2C en B2B.</span><span class="sxs-lookup"><span data-stu-id="7e72a-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="7e72a-154">Hoe we zorgen dat de toepassing hello is geldig</span><span class="sxs-lookup"><span data-stu-id="7e72a-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="7e72a-155">Hallo nodig tooensure Hallo identiteit van een toepassing aanroep Hallo broker is cruciaal toohello beveiliging we in broker assisted-aanmeldingen bieden.</span><span class="sxs-lookup"><span data-stu-id="7e72a-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="7e72a-156">Geen iOS of Android zorgt ervoor dat unieke id's die alleen geldig voor een bepaalde toepassing zijn zodat schadelijke toepassingen mogelijk '' een legitieme toepassings-id vervalsen en Hallo-tokens die zijn bedoeld voor legitieme toepassing hello ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="7e72a-157">tooensure die we altijd met de juiste toepassing hello tijdens runtime communiceren, vragen we Hallo developer tooprovide een aangepaste redirectURI bij het registreren van de toepassing met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e72a-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="7e72a-158">**Hoe ontwikkelaars deze omleidings-URI moeten stellen wordt hieronder in detail besproken.**</span><span class="sxs-lookup"><span data-stu-id="7e72a-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="7e72a-159">Deze aangepaste redirectURI Hallo certificaatvingerafdruk van de toepassing hello bevat en wordt ervoor gezorgd dat toobe unieke toohello toepassing door Hallo Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="7e72a-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="7e72a-160">Wanneer een toepassing aanroept Hallo broker, Hallo broker vraagt Hallo besturingssysteem Android tooprovide met Hallo vingerafdruk van het certificaat dat opgeroepen Hallo broker.</span><span class="sxs-lookup"><span data-stu-id="7e72a-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="7e72a-161">Dit certificaat vingerafdruk tooMicrosoft vindt Hallo broker in Hallo aanroep tooour identiteitssysteem.</span><span class="sxs-lookup"><span data-stu-id="7e72a-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="7e72a-162">Als vingerafdruk van de toepassing hello komt niet overeen met de certificaatvingerafdruk Hallo Hallo-certificaat hebt opgegeven tijdens de registratie toous door Hallo ontwikkelaar, wordt de toegang weigert toohello tokens voor Hallo resource Hallo toepassing vraagt.</span><span class="sxs-lookup"><span data-stu-id="7e72a-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="7e72a-163">Deze controle zorgt ervoor dat alleen Hallo toepassing die zijn geregistreerd door de ontwikkelaar Hallo tokens ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7e72a-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="7e72a-164">**Hallo developer heeft Hallo keuze van als Hallo Microsoft Identity SDK Hallo broker aanroepen of Hallo geen broker assisted stroom wordt gebruikt.**</span><span class="sxs-lookup"><span data-stu-id="7e72a-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="7e72a-165">Echter als Hallo developer ervoor geen toouse Hallo broker-ondersteunde stroom kiest gaat Hallo voordeel verloren van het gebruik van eenmalige aanmelding referenties die gebruiker Hallo mogelijk al toegevoegd op Hallo-apparaat en wordt voorkomen dat de toepassing wordt gebruikt met business functies van Microsoft biedt zijn klanten zoals voorwaardelijke toegang, beheermogelijkheden voor Intune en verificatie op basis van certificaten.</span><span class="sxs-lookup"><span data-stu-id="7e72a-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="7e72a-166">Deze aanmeldingen hebben Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7e72a-167">Gebruiker merkt dat eenmalige aanmelding via hun toepassingen ongeacht Hallo leverancier.</span><span class="sxs-lookup"><span data-stu-id="7e72a-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="7e72a-168">Uw toepassing kunt meer geavanceerde zakelijke functies zoals voorwaardelijke toegang gebruiken of Hallo InTune productreeks gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e72a-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7e72a-169">Uw toepassing kan ondersteuning voor verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7e72a-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="7e72a-170">Veel veiligere aanmelden als Hallo identiteit van de toepassing hello en Hallo gebruiker zijn geverifieerd door Hallo broker toepassing met algoritmen voor extra beveiliging en versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7e72a-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="7e72a-171">Deze aanmeldingen hebben Hallo volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7e72a-172">In iOS-gebruiker Hallo overgegaan buiten de ervaring van uw toepassing, terwijl referenties worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="7e72a-173">Verlies van Hallo mogelijkheid toomanage Hallo aanmelding optreden voor uw klanten in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="7e72a-174">Hier volgt een weergave van hoe Hallo Microsoft Identity-SDK's werken met Hallo toepassingen tooenable SSO broker:</span><span class="sxs-lookup"><span data-stu-id="7e72a-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="7e72a-175">. Met deze achtergrondinformatie moet u kunnen toobetter begrijpen en eenmalige aanmelding implementeren in uw toepassing met behulp van Microsoft Identity-platform Hallo en SDK's.</span><span class="sxs-lookup"><span data-stu-id="7e72a-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="7e72a-176">Inschakelen van verschillende Apps eenmalige aanmelding met ADAL</span><span class="sxs-lookup"><span data-stu-id="7e72a-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="7e72a-177">Hier gebruiken we Hallo ADAL Android SDK naar:</span><span class="sxs-lookup"><span data-stu-id="7e72a-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="7e72a-178">Geen broker assisted eenmalige aanmelding voor uw suite van apps inschakelen</span><span class="sxs-lookup"><span data-stu-id="7e72a-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="7e72a-179">Ondersteuning voor broker-ondersteunde eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="7e72a-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="7e72a-180">Eenmalige aanmelding inschakelen voor niet-broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e72a-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="7e72a-181">Voor niet-broker assisted eenmalige aanmelding via toepassingen beheren Hallo Microsoft Identity-SDK's veel van de complexiteit Hallo van eenmalige aanmelding voor u.</span><span class="sxs-lookup"><span data-stu-id="7e72a-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="7e72a-182">Dit omvat Hallo rechts gebruiker zoeken in de cache Hallo en onderhouden van een lijst met aangemelde gebruikers voor u tooquery.</span><span class="sxs-lookup"><span data-stu-id="7e72a-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="7e72a-183">tooenable SSO alle toepassingen die u bezit, moet u toodo hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="7e72a-184">Zorg ervoor dat alle uw toepassingen gebruiker Hallo dezelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="7e72a-185">Controleer dat al uw toepassingen hebben Hallo die dezelfde SharedUserID ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7e72a-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="7e72a-186">Zorg ervoor dat alle van uw toepassingen delen Hallo hetzelfde certificaat voor ondertekening van Google Play Hallo opslaan, zodat u opslag kunt delen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="7e72a-187">Stap 1: Met behulp van hetzelfde Client-ID Hallo / toepassing-ID voor alle toepassingen in uw pakket apps Hallo</span><span class="sxs-lookup"><span data-stu-id="7e72a-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="7e72a-188">Hallo Microsoft Identity platform tooknow wordt dat het tooshare tokens toegestaan voor uw toepassingen, elke toepassing moet tooshare Hallo dezelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="7e72a-189">Dit is Hallo unieke id die is opgegeven tooyou bij de registratie van uw eerste toepassing in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="7e72a-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="7e72a-190">U vraagt zich misschien af hoe u verschillende apps wordt geïdentificeerd toohello Microsoft Identity-service als hierbij Hallo dezelfde toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="7e72a-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="7e72a-191">Hallo-antwoord is Hello **omleidings-URI's**.</span><span class="sxs-lookup"><span data-stu-id="7e72a-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="7e72a-192">Elke toepassing kan meerdere omleidings-URI's geregistreerd in Hallo onboarding portal hebben.</span><span class="sxs-lookup"><span data-stu-id="7e72a-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="7e72a-193">Elke app in de suite hebben een verschillende omleidings-URI.</span><span class="sxs-lookup"><span data-stu-id="7e72a-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="7e72a-194">Een voorbeeld van hoe dit eruitziet lager is dan:</span><span class="sxs-lookup"><span data-stu-id="7e72a-194">An example of how this looks is below:</span></span>

<span data-ttu-id="7e72a-195">App1 omleidings-URI:`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="7e72a-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="7e72a-196">App2 omleidings-URI:`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="7e72a-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="7e72a-197">App3 omleidings-URI:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="7e72a-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="7e72a-198">....</span><span class="sxs-lookup"><span data-stu-id="7e72a-198">....</span></span>

<span data-ttu-id="7e72a-199">Deze zijn genest onder dezelfde client-ID Hallo / toepassings-ID en opgezocht op basis van Hallo omleidings-URI die u in uw configuratie SDK toous retourneren.</span><span class="sxs-lookup"><span data-stu-id="7e72a-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="7e72a-200">*Let op Hallo van de indeling van deze omleidings-URI's worden hieronder beschreven. U mag een omleidings-URI gebruiken, tenzij u wenst dat toosupport Hallo broker, in welk geval ze moeten er ongeveer zo uitzien Hallo bovenstaande*</span><span class="sxs-lookup"><span data-stu-id="7e72a-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="7e72a-201">Stap 2: Gedeelde opslag configureren in Android</span><span class="sxs-lookup"><span data-stu-id="7e72a-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="7e72a-202">Instelling Hallo `SharedUserID` valt buiten het bereik van dit document hello, maar kan worden geleerd door te lezen Hallo Google Android-documentatie op Hallo [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="7e72a-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="7e72a-203">Wat is het belangrijk is dat u besluit dat u wilt uw sharedUserID wordt aangeroepen en wordt deze gebruikt op al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="7e72a-204">Zodra u Hallo hebt `SharedUserID` in al uw toepassingen bent u klaar toouse eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7e72a-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="7e72a-205">Wanneer u delen van opslag in uw toepassingen kunt elke toepassing gebruikers verwijderen of slechter alle Hallo tokens verwijderen inlezen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="7e72a-206">Dit is vooral rampzalig zijn als u toepassingen die afhankelijk van Hallo tokens toodo achtergrondwerk zijn hebt.</span><span class="sxs-lookup"><span data-stu-id="7e72a-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="7e72a-207">Delen van opslag, betekent dat u voorzichtig in alle verwijderingsbewerkingen via Hallo Microsoft Identity-SDK's moet zijn.</span><span class="sxs-lookup"><span data-stu-id="7e72a-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="7e72a-208">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7e72a-208">That's it!</span></span> <span data-ttu-id="7e72a-209">Hallo Microsoft Identity SDK wordt nu referenties delen in al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="7e72a-210">Hallo-gebruikerslijst wordt ook gedeeld met exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e72a-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="7e72a-211">Eenmalige aanmelding inschakelen voor broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e72a-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="7e72a-212">mogelijkheid voor een toepassing toouse broker die is geïnstalleerd op Hallo apparaat is Hallo **standaard uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="7e72a-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="7e72a-213">In volgorde toouse uw toepassing met Hallo broker moet u enkele aanvullende configuratiestappen doen en sommige code tooyour toepassing toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="7e72a-214">Hallo stappen toofollow zijn:</span><span class="sxs-lookup"><span data-stu-id="7e72a-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="7e72a-215">Schakel de broker-modus in uw toepassingscode aanroep toohello MS-SDK</span><span class="sxs-lookup"><span data-stu-id="7e72a-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="7e72a-216">Tot stand brengen van een nieuwe omleidings-URI en geef die tooboth Hallo-app en uw app-registratie</span><span class="sxs-lookup"><span data-stu-id="7e72a-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="7e72a-217">Instellen van de juiste machtigingen Hallo in Hallo Android-manifestbestand</span><span class="sxs-lookup"><span data-stu-id="7e72a-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="7e72a-218">Stap 1: Broker-modus inschakelen in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="7e72a-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="7e72a-219">Hallo mogelijkheid voor uw toepassing toouse Hallo broker is ingeschakeld wanneer u Hallo 'instellingen' of de eerste installatie van de verificatie-instantie maakt.</span><span class="sxs-lookup"><span data-stu-id="7e72a-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="7e72a-220">U doen dit door het instellen van uw type ApplicationSettings in uw code:</span><span class="sxs-lookup"><span data-stu-id="7e72a-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="7e72a-221">Stap 2: Een nieuwe omleidings-URI met URL-schema maken</span><span class="sxs-lookup"><span data-stu-id="7e72a-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="7e72a-222">In de volgorde tooensure dat we altijd retourneren Hallo referentie tokens toohello juiste toepassingsnaam, moeten we toomake ervoor dat we terugbellen tooyour toepassing op een manier die Hallo Android-besturingssysteem kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="7e72a-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="7e72a-223">Hallo-hash van het certificaat Hallo Hallo Android-besturingssysteem gebruikt in Hallo Google Play store.</span><span class="sxs-lookup"><span data-stu-id="7e72a-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="7e72a-224">Dit kan niet door een rogue-toepassing worden vervalst.</span><span class="sxs-lookup"><span data-stu-id="7e72a-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="7e72a-225">Daarom we maken gebruik van dit samen met de Hallo-URI van onze broker toepassing tooensure dat Hallo tokens toohello juiste toepassingsnaam worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7e72a-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="7e72a-226">Moet u tooestablish deze unieke omleidings-URI in uw toepassing en een set als een omleidings-URI in onze portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="7e72a-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="7e72a-227">Hallo juiste vorm van de omleidings-URI moet zijn:</span><span class="sxs-lookup"><span data-stu-id="7e72a-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="7e72a-228">Voorbeeld: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="7e72a-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="7e72a-229">Deze omleidings-URI moet toobe opgegeven in de registratie van uw app met behulp van Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7e72a-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7e72a-230">Zie voor meer informatie over Azure AD-app-registratie [integreren met Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="7e72a-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="7e72a-231">Stap 3: De juiste machtigingen Hallo in uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="7e72a-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="7e72a-232">Hallo Accounts Manager-functie van Hallo Android OS toomanage referenties onze toepassing broker in Android gebruikt op toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7e72a-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="7e72a-233">In de volgorde toouse Hallo broker in Android moet uw app-manifest machtigingen toouse AccountManager accounts hebben.</span><span class="sxs-lookup"><span data-stu-id="7e72a-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="7e72a-234">Dit wordt uitgebreid beschreven in Hallo [Google documentatie voor Account Manager hier](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="7e72a-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="7e72a-235">In het bijzonder zijn deze machtigingen:</span><span class="sxs-lookup"><span data-stu-id="7e72a-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="7e72a-236">U kunt eenmalige aanmelding hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7e72a-236">You've configured SSO!</span></span>
<span data-ttu-id="7e72a-237">Nu Hallo Microsoft Identity SDK automatisch zowel referenties delen in uw toepassingen en Hallo broker aanroepen, indien aanwezig zijn op hun apparaat.</span><span class="sxs-lookup"><span data-stu-id="7e72a-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

