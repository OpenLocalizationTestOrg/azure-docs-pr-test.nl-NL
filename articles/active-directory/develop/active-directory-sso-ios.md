---
title: aaaHow tooenable SSO cross-app voor iOS met ADAL | Microsoft Docs
description: 'Hoe Hallo toouse Hallo functies van ADAL SDK tooenable eenmalige aanmelding via uw toepassingen. '
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="22623-103">Hoe tooenable SSO cross-app voor iOS met ADAL</span><span class="sxs-lookup"><span data-stu-id="22623-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="22623-104">Eenmalige aanmelding (SSO) bieden zodat gebruikers alleen tooenter eenmaal hun referenties nodig en deze referenties automatisch werk verschillende toepassingen hebben wordt nu door klanten verwacht.</span><span class="sxs-lookup"><span data-stu-id="22623-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="22623-105">Hallo problemen in hun gebruikersnaam en wachtwoord invoeren op een klein scherm, vaak keren gecombineerd met een extra factor (2FA), zoals een telefoongesprek of ge-code, resulteert in een snelle ergernis als een gebruiker heeft toodo dit meer dan één keer voor het product.</span><span class="sxs-lookup"><span data-stu-id="22623-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="22623-106">Bovendien, als u een identiteitsplatform die van andere toepassingen zoals Microsoft-Accounts of een werkaccount van Office365 gebruikmaken mogelijk toepast, verwachten klanten dat deze referenties toobe toouse beschikbaar op alle toepassingen met hun Hallo leverancier niet van belang.</span><span class="sxs-lookup"><span data-stu-id="22623-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="22623-107">Hallo Microsoft Identity-platform, samen met onze SDK's van Microsoft Identity komt dit harde werk voor u en geeft u de mogelijkheid toodelight Hallo uw klanten met eenmalige aanmelding bij uw eigen suite van toepassingen, of als met onze broker-functie en de verificator toepassingen in het hele apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="22623-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="22623-108">In dit scenario wordt uitgelegd hoe tooconfigure onze SDK in uw toepassing tooprovide deze voordeel tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="22623-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="22623-109">In dit scenario is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="22623-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="22623-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22623-110">Azure Active Directory</span></span>
* <span data-ttu-id="22623-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="22623-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="22623-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22623-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="22623-113">Voorwaardelijke toegang voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22623-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="22623-114">Hallo document voorgaande wordt ervan uitgegaan dat u weet hoe te[inrichten van toepassingen in de oude portal Hallo voor Azure Active Directory](active-directory-how-to-integrate.md) en uw toepassing Hello geïntegreerd [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="22623-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="22623-115">SSO-concepten in Hallo Identiteitsplatform van Microsoft</span><span class="sxs-lookup"><span data-stu-id="22623-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="22623-116">Microsoft Identity Beleggingsmakelaars</span><span class="sxs-lookup"><span data-stu-id="22623-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="22623-117">Microsoft biedt voor elk mobiel platform-toepassingen die voor Hallo bridging van referenties voor toepassingen van verschillende leveranciers en kunt voor speciale verbeterde functies waarvoor een enkele veilige plaats waar toovalidate referenties.</span><span class="sxs-lookup"><span data-stu-id="22623-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="22623-118">We noemen deze **beleggingsmakelaars**.</span><span class="sxs-lookup"><span data-stu-id="22623-118">We call these **brokers**.</span></span> <span data-ttu-id="22623-119">Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die enkele of alle Hallo apparaat voor hun werknemers beheert.</span><span class="sxs-lookup"><span data-stu-id="22623-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="22623-120">Deze beleggingsmakelaars ondersteuning voor het beheer van beveiliging voor sommige toepassingen of de hele Hallo-apparaat op basis van wat de IT-beheerders willen.</span><span class="sxs-lookup"><span data-stu-id="22623-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="22623-121">In Windows, wordt deze functionaliteit verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.</span><span class="sxs-lookup"><span data-stu-id="22623-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="22623-122">We gebruiken deze beleggingsmakelaars en hoe uw klanten mogelijk ze in hun aanmelding stroom voor Hallo Microsoft Identity platform Lees verder voor meer informatie over het.</span><span class="sxs-lookup"><span data-stu-id="22623-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="22623-123">Patronen voor logboekregistratie in op mobiele apparaten</span><span class="sxs-lookup"><span data-stu-id="22623-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="22623-124">Toegang toocredentials op apparaten als volgt twee basispatronen voor Hallo Microsoft Identity-platform:</span><span class="sxs-lookup"><span data-stu-id="22623-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="22623-125">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="22623-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="22623-126">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="22623-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="22623-127">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="22623-127">Non-broker assisted logins</span></span>
<span data-ttu-id="22623-128">Niet-broker assisted aanmeldingen zijn aanmelding ervaringen die inline met de toepassing hello gebeuren en Hallo lokale opslag op Hallo-apparaat voor die toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22623-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="22623-129">Deze opslag kan worden gedeeld tussen toepassingen maar Hallo referenties zijn nauw gebonden toohello app of suite van apps met behulp van deze referentie.</span><span class="sxs-lookup"><span data-stu-id="22623-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="22623-130">U hebt waarschijnlijk is dit in veel mobiele toepassingen wanneer u een gebruikersnaam en wachtwoord in Hallo toepassing zelf invoert.</span><span class="sxs-lookup"><span data-stu-id="22623-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="22623-131">Deze aanmeldingen hebben Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="22623-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="22623-132">Er bestaat een gebruikerservaring volledig in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="22623-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="22623-133">Referenties kunnen worden gedeeld door toepassingen die zijn ondertekend door Hallo hetzelfde certificaat, een ervaring voor eenmalige aanmelding tooyour reeks toepassingen bieden.</span><span class="sxs-lookup"><span data-stu-id="22623-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="22623-134">Besturingselement rond Hallo ervaring met het aanmelden wordt verstrekt toohello toepassing vóór en na het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="22623-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="22623-135">Deze aanmeldingen hebben Hallo volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="22623-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="22623-136">Kan niet-gebruikerservaring eenmalige aanmelding via alle apps die gebruikmaken van een Microsoft-Identity alleen via de Microsoft-Identities die uw toepassing is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="22623-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="22623-137">Uw toepassing kan niet worden gebruikt met meer geavanceerde zakelijke functies zoals voorwaardelijke toegang of gebruik Hallo InTune reeks producten.</span><span class="sxs-lookup"><span data-stu-id="22623-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="22623-138">Uw toepassing ondersteunt geen verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="22623-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="22623-139">Hier volgt een weergave over de werking van Hallo Microsoft Identity SDK's met Hallo gedeelde opslag van uw toepassingen tooenable eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="22623-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="22623-140">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="22623-140">Broker assisted logins</span></span>
<span data-ttu-id="22623-141">Aanmeldingen Broker-ondersteunde zijn aanmelding ervaringen die optreden in Hallo broker toepassing en Hallo opslag en beveiliging van Hallo broker tooshare referenties gebruiken voor alle toepassingen die van toepassing hello Microsoft Identity platform op Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="22623-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="22623-142">Dit betekent dat uw toepassingen afhankelijk zijn van Hallo broker toosign gebruikers in.</span><span class="sxs-lookup"><span data-stu-id="22623-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="22623-143">Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die Hallo-apparaat voor de gebruiker beheert.</span><span class="sxs-lookup"><span data-stu-id="22623-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="22623-144">Een voorbeeld van dit type toepassing is Hallo Microsoft Authenticator-toepassing op iOS.</span><span class="sxs-lookup"><span data-stu-id="22623-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="22623-145">In Windows worden deze functionaliteit wordt verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.</span><span class="sxs-lookup"><span data-stu-id="22623-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="22623-146">Hallo-ervaring varieert per platform en kan verstoren toousers soms zijn als het niet correct worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="22623-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="22623-147">U kunt waarschijnlijk meest bekend zijn met dit patroon als u Hallo Facebook-toepassing is geïnstalleerd en Facebook-verbinding van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="22623-148">Hallo Hallo platform maakt gebruik van Microsoft Identity hetzelfde patroon.</span><span class="sxs-lookup"><span data-stu-id="22623-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="22623-149">Voor iOS leidt dit tooa 'overgang' animatie waarbij uw toepassing wordt verzonden toohello achtergrond tijdens Hallo Microsoft Authenticator toepassingen wordt geleverd toohello voorgrond voor Hallo gebruiker tooselect welk account wil toosign met.</span><span class="sxs-lookup"><span data-stu-id="22623-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="22623-150">Voor Android en Windows hello account kiezer boven op uw toepassing minder verstoren toohello gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="22623-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="22623-151">Hoe Hallo broker opgehaald aangeroepen</span><span class="sxs-lookup"><span data-stu-id="22623-151">How hello broker gets invoked</span></span>
<span data-ttu-id="22623-152">Als een compatibel broker is geïnstalleerd op het Hallo-apparaat, zoals Hallo Microsoft Authenticator-toepassing hello Microsoft Identity-SDK's automatisch wordt werk van het Hallo-broker voor u wordt aangeroepen wanneer een gebruiker dat zij toolog aangeeft aan met een account van wensen Hallo Hallo Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="22623-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="22623-153">Dit account kan worden een persoonlijk Microsoft-Account, werk of schoolaccount of een account dat u opgeeft en host in Azure met behulp van onze producten B2C en B2B.</span><span class="sxs-lookup"><span data-stu-id="22623-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="22623-154">Hoe we zorgen dat de toepassing hello is geldig</span><span class="sxs-lookup"><span data-stu-id="22623-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="22623-155">Hallo nodig tooensure Hallo identiteit van een toepassing aanroep Hallo broker is cruciaal toohello beveiliging we in broker assisted-aanmeldingen bieden.</span><span class="sxs-lookup"><span data-stu-id="22623-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="22623-156">Geen iOS of Android zorgt ervoor dat unieke id's die alleen geldig voor een bepaalde toepassing zijn zodat schadelijke toepassingen mogelijk '' een legitieme toepassings-id vervalsen en Hallo-tokens die zijn bedoeld voor legitieme toepassing hello ontvangen.</span><span class="sxs-lookup"><span data-stu-id="22623-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="22623-157">tooensure die we altijd met de juiste toepassing hello tijdens runtime communiceren, vragen we Hallo developer tooprovide een aangepaste redirectURI bij het registreren van de toepassing met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22623-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="22623-158">**Hoe ontwikkelaars deze omleidings-URI moeten stellen wordt hieronder in detail besproken.**</span><span class="sxs-lookup"><span data-stu-id="22623-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="22623-159">Deze aangepaste redirectURI Hallo bundel-ID van de toepassing hello bevat en wordt ervoor gezorgd dat toobe unieke toohello toepassing door Hallo Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="22623-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="22623-160">Wanneer u een toepassing aanroepen Hallo-broker Hallo broker wordt gevraagd Hallo iOS system tooprovide besturingssysteem met bundel-ID die aangeroepen Hallo broker Hallo.</span><span class="sxs-lookup"><span data-stu-id="22623-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="22623-161">Hallo broker vindt deze tooMicrosoft bundel-ID in Hallo aanroep tooour identiteitssysteem.</span><span class="sxs-lookup"><span data-stu-id="22623-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="22623-162">Als Hallo bundel-ID van de toepassing hello komt niet overeen met het Hallo-bundel-ID door de ontwikkelaar Hallo toous tijdens de registratie opgegeven, wordt de toegang weigert toohello tokens voor Hallo resource Hallo toepassing vraagt.</span><span class="sxs-lookup"><span data-stu-id="22623-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="22623-163">Deze controle zorgt ervoor dat alleen Hallo toepassing die zijn geregistreerd door de ontwikkelaar Hallo tokens ontvangt.</span><span class="sxs-lookup"><span data-stu-id="22623-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="22623-164">**Hallo developer heeft Hallo keuze van als Hallo Microsoft Identity SDK Hallo broker aanroepen of Hallo geen broker assisted stroom wordt gebruikt.**</span><span class="sxs-lookup"><span data-stu-id="22623-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="22623-165">Echter als Hallo developer ervoor geen toouse Hallo broker-ondersteunde stroom kiest gaat Hallo voordeel verloren van het gebruik van eenmalige aanmelding referenties die gebruiker Hallo mogelijk al toegevoegd op Hallo-apparaat en wordt voorkomen dat de toepassing wordt gebruikt met business functies van Microsoft biedt zijn klanten zoals voorwaardelijke toegang, beheermogelijkheden voor Intune en verificatie op basis van certificaten.</span><span class="sxs-lookup"><span data-stu-id="22623-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="22623-166">Deze aanmeldingen hebben Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="22623-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="22623-167">Gebruiker merkt dat eenmalige aanmelding via hun toepassingen ongeacht Hallo leverancier.</span><span class="sxs-lookup"><span data-stu-id="22623-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="22623-168">Uw toepassing kunt meer geavanceerde zakelijke functies zoals voorwaardelijke toegang gebruiken of Hallo InTune productreeks gebruikt.</span><span class="sxs-lookup"><span data-stu-id="22623-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="22623-169">Uw toepassing kan ondersteuning voor verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="22623-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="22623-170">Veel veiligere aanmelden als Hallo identiteit van de toepassing hello en Hallo gebruiker zijn geverifieerd door Hallo broker toepassing met algoritmen voor extra beveiliging en versleuteling.</span><span class="sxs-lookup"><span data-stu-id="22623-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="22623-171">Deze aanmeldingen hebben Hallo volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="22623-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="22623-172">In iOS-gebruiker Hallo overgegaan buiten de ervaring van uw toepassing, terwijl referenties worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="22623-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="22623-173">Verlies van Hallo mogelijkheid toomanage Hallo aanmelding optreden voor uw klanten in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="22623-174">Hier volgt een weergave van hoe Hallo Microsoft Identity-SDK's werken met Hallo toepassingen tooenable SSO broker:</span><span class="sxs-lookup"><span data-stu-id="22623-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="22623-175">. Met deze achtergrondinformatie moet u kunnen toobetter begrijpen en eenmalige aanmelding implementeren in uw toepassing met behulp van Microsoft Identity-platform Hallo en SDK's.</span><span class="sxs-lookup"><span data-stu-id="22623-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="22623-176">Inschakelen van verschillende Apps eenmalige aanmelding met ADAL</span><span class="sxs-lookup"><span data-stu-id="22623-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="22623-177">Hier gebruiken we Hallo ADAL iOS SDK naar:</span><span class="sxs-lookup"><span data-stu-id="22623-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="22623-178">Geen broker assisted eenmalige aanmelding voor uw suite van apps inschakelen</span><span class="sxs-lookup"><span data-stu-id="22623-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="22623-179">Ondersteuning voor broker-ondersteunde eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="22623-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="22623-180">Eenmalige aanmelding inschakelen voor niet-broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22623-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="22623-181">Voor niet-broker assisted eenmalige aanmelding via toepassingen beheren Hallo Microsoft Identity-SDK's veel van de complexiteit Hallo van eenmalige aanmelding voor u.</span><span class="sxs-lookup"><span data-stu-id="22623-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="22623-182">Dit omvat Hallo rechts gebruiker zoeken in de cache Hallo en onderhouden van een lijst met aangemelde gebruikers voor u tooquery.</span><span class="sxs-lookup"><span data-stu-id="22623-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="22623-183">tooenable SSO alle toepassingen die u bezit, moet u toodo hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="22623-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="22623-184">Zorg ervoor dat alle uw toepassingen gebruiker Hallo dezelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="22623-185">Zorg ervoor dat alle uw toepassingen delen Hallo dezelfde ondertekening van het certificaat van Apple zodat u sleutelhangers kan delen</span><span class="sxs-lookup"><span data-stu-id="22623-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="22623-186">Aanvragen Hallo dezelfde sleutelhanger recht voor elk van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="22623-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="22623-187">Vertel Hallo Microsoft Identity SDK's over Hallo gedeelde sleutelhanger wilt u ons toouse.</span><span class="sxs-lookup"><span data-stu-id="22623-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="22623-188">Met behulp van hetzelfde Client-ID Hallo / toepassing-ID voor alle toepassingen in uw pakket apps Hallo</span><span class="sxs-lookup"><span data-stu-id="22623-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="22623-189">Hallo Microsoft Identity platform tooknow wordt dat het tooshare tokens toegestaan voor uw toepassingen, elke toepassing moet tooshare Hallo dezelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="22623-190">Dit is Hallo unieke id die is opgegeven tooyou bij de registratie van uw eerste toepassing in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="22623-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="22623-191">U vraagt zich misschien af hoe u verschillende apps wordt geïdentificeerd toohello Microsoft Identity-service als hierbij Hallo dezelfde toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="22623-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="22623-192">Hallo-antwoord is Hello **omleidings-URI's**.</span><span class="sxs-lookup"><span data-stu-id="22623-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="22623-193">Elke toepassing kan meerdere omleidings-URI's geregistreerd in Hallo onboarding portal hebben.</span><span class="sxs-lookup"><span data-stu-id="22623-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="22623-194">Elke app in de suite hebben een verschillende omleidings-URI.</span><span class="sxs-lookup"><span data-stu-id="22623-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="22623-195">Een voorbeeld van hoe dit eruitziet lager is dan:</span><span class="sxs-lookup"><span data-stu-id="22623-195">An example of how this looks is below:</span></span>

<span data-ttu-id="22623-196">App1 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="22623-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="22623-197">App2 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="22623-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="22623-198">App3 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="22623-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="22623-199">....</span><span class="sxs-lookup"><span data-stu-id="22623-199">....</span></span>

<span data-ttu-id="22623-200">Deze zijn genest onder dezelfde client-ID Hallo / toepassings-ID en opgezocht op basis van Hallo omleidings-URI die u in uw configuratie SDK toous retourneren.</span><span class="sxs-lookup"><span data-stu-id="22623-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="22623-201">*Let op Hallo van de indeling van deze omleidings-URI's worden hieronder beschreven. U mag een omleidings-URI gebruiken, tenzij u wenst dat toosupport Hallo broker, in welk geval ze moeten er ongeveer zo uitzien Hallo bovenstaande*</span><span class="sxs-lookup"><span data-stu-id="22623-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="22623-202">Sleutelhanger delen tussen toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="22623-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="22623-203">Inschakelen van het delen van sleutelketens valt buiten het bereik van dit document Hallo en in het document wordt gedekt door Apple [mogelijkheden toevoegen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="22623-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="22623-204">Wat is het belangrijk is dat u bepalen wat u uw sleutelhanger toobe aangeroepen en die mogelijkheid voor alle uw toepassingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="22623-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="22623-205">Wanneer u hebt rechten instellen correct u ziet een bestand in uw projectmap recht `entitlements.plist` die iets dat op Hallo volgende lijkt bevat:</span><span class="sxs-lookup"><span data-stu-id="22623-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="22623-206">Zodra u Hallo sleutelhanger recht ingeschakeld in elk van uw toepassingen hebt en u klaar toouse SSO bent, vertellen Hallo Microsoft Identity SDK de sleutelketen met behulp van de volgende instelling in Hallo uw `ADAuthenticationSettings` Hello instelling te volgen:</span><span class="sxs-lookup"><span data-stu-id="22623-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="22623-207">Wanneer u een sleutelhanger in uw toepassingen delen kan elke toepassing of verwijderen gebruikers slechter alle Hallo tokens inlezen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="22623-208">Dit is vooral rampzalig zijn als u toepassingen die afhankelijk van Hallo tokens toodo achtergrondwerk zijn hebt.</span><span class="sxs-lookup"><span data-stu-id="22623-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="22623-209">Een sleutelhanger delen verwijderen betekent dat u voorzichtig in alle moet bewerkingen via Hallo Microsoft Identity SDK's.</span><span class="sxs-lookup"><span data-stu-id="22623-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="22623-210">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="22623-210">That's it!</span></span> <span data-ttu-id="22623-211">Hallo Microsoft Identity SDK wordt nu referenties delen in al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="22623-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="22623-212">Hallo-gebruikerslijst wordt ook gedeeld met exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="22623-213">Eenmalige aanmelding inschakelen voor broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22623-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="22623-214">mogelijkheid voor een toepassing toouse broker die is geïnstalleerd op Hallo apparaat is Hallo **standaard uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="22623-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="22623-215">In volgorde toouse uw toepassing met Hallo broker moet u enkele aanvullende configuratiestappen doen en sommige code tooyour toepassing toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="22623-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="22623-216">Hallo stappen toofollow zijn:</span><span class="sxs-lookup"><span data-stu-id="22623-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="22623-217">Schakel de broker-modus in uw toepassingscode aanroep toohello MS-SDK.</span><span class="sxs-lookup"><span data-stu-id="22623-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="22623-218">Tot stand brengen van een nieuwe omleidings-URI en geef die tooboth Hallo-app en de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="22623-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="22623-219">Een URL-schema wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="22623-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="22623-220">Ondersteuning voor iOS9: een machtiging tooyour info.plist-bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="22623-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="22623-221">Stap 1: Broker-modus inschakelen in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="22623-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="22623-222">Hallo mogelijkheid voor uw toepassing toouse Hallo broker is ingeschakeld wanneer u Hallo 'context' of de eerste installatie van de verificatie-object maakt.</span><span class="sxs-lookup"><span data-stu-id="22623-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="22623-223">U doen dit door het instellen van het type van uw referenties in uw code:</span><span class="sxs-lookup"><span data-stu-id="22623-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="22623-224">Hallo `AD_CREDENTIALS_AUTO` instelling zorgt dat de Hallo Microsoft Identity SDK tootry toocall uit toohello broker, `AD_CREDENTIALS_EMBEDDED` wordt voorkomen dat Hallo Microsoft Identity SDK toohello broker aanroepen.</span><span class="sxs-lookup"><span data-stu-id="22623-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="22623-225">Stap 2: Registreren van een URL-schema</span><span class="sxs-lookup"><span data-stu-id="22623-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="22623-226">Hallo Microsoft Identity-platform gebruikt de URL's tooinvoke Hallo broker en ga daarna terug besturingselement back tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="22623-227">toofinish die u moet u een URL-schema retouren geregistreerd voor de toepassing die Hallo Microsoft Identity platform weten over.</span><span class="sxs-lookup"><span data-stu-id="22623-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="22623-228">Dit kan worden bovendien tooany andere app-schema's kan u eerder hebt geregistreerd met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="22623-229">Is het raadzaam om Hallo URL-schema redelijk unieke toominimize Hallo kans op een andere app Hallo met dezelfde URL-schema.</span><span class="sxs-lookup"><span data-stu-id="22623-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="22623-230">Apple worden niet afgedwongen door Hallo Uniekheid van URL-schema's die zijn geregistreerd in Hallo appstore.</span><span class="sxs-lookup"><span data-stu-id="22623-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="22623-231">Hieronder volgt een voorbeeld van hoe deze wordt weergegeven in de projectconfiguratie van uw.</span><span class="sxs-lookup"><span data-stu-id="22623-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="22623-232">U kunt dit ook doen in XCode ook:</span><span class="sxs-lookup"><span data-stu-id="22623-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="22623-233">Stap 3: Een nieuwe omleidings-URI met URL-schema vaststellen</span><span class="sxs-lookup"><span data-stu-id="22623-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="22623-234">In de volgorde tooensure dat we altijd retourneren Hallo referentie tokens toohello juiste toepassingsnaam, moeten we toomake ervoor dat we terugbellen tooyour toepassing op een manier die Hallo iOS-besturingssysteem kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="22623-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="22623-235">Hallo iOS-besturingssysteem rapporten toohello Microsoft broker toepassingen Hallo bundel-ID van het aanroepen van het Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="22623-236">Dit kan niet door een rogue-toepassing worden vervalst.</span><span class="sxs-lookup"><span data-stu-id="22623-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="22623-237">Daarom we maken gebruik van dit samen met de Hallo-URI van onze broker toepassing tooensure dat Hallo tokens toohello juiste toepassingsnaam worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="22623-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="22623-238">Moet u tooestablish deze unieke omleidings-URI in uw toepassing en een set als een omleidings-URI in onze portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="22623-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="22623-239">Hallo juiste vorm van de omleidings-URI moet zijn:</span><span class="sxs-lookup"><span data-stu-id="22623-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="22623-240">Voorbeeld: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="22623-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="22623-241">Deze omleidings-URI moet toobe opgegeven in de registratie van uw app met behulp van Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="22623-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="22623-242">Zie voor meer informatie over Azure AD-app-registratie [integreren met Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="22623-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="22623-243">Stap 3a: Voeg een omleidings-URI in uw app en Developer portal toosupport verificatie op basis</span><span class="sxs-lookup"><span data-stu-id="22623-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="22623-244">toosupport certificaat gebaseerde verificatie een tweede 'msauth' moet toobe geregistreerd in uw toepassing en het Hallo [Azure-portal](https://portal.azure.com/) toohandle certificaatverificatie desgewenst tooadd die ondersteuning bieden in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="22623-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="22623-245">Voorbeeld: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="22623-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="22623-246">Stap 4: iOS9: een configuratie parameter tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="22623-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="22623-247">– CanOpenURL maakt gebruik van ADAL: toocheck als Hallo broker op Hallo-apparaat is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="22623-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="22623-248">In iOS vergrendeld 9 Apple wat schema's een toepassing kunnen opvragen.</span><span class="sxs-lookup"><span data-stu-id="22623-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="22623-249">U moet tooadd 'msauth' toohello LSApplicationQueriesSchemes gedeelte van uw `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="22623-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="22623-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="22623-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="22623-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="22623-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="22623-252">U kunt eenmalige aanmelding hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="22623-252">You've configured SSO!</span></span>
<span data-ttu-id="22623-253">Nu Hallo Microsoft Identity SDK automatisch zowel referenties delen in uw toepassingen en Hallo broker aanroepen, indien aanwezig zijn op hun apparaat.</span><span class="sxs-lookup"><span data-stu-id="22623-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

