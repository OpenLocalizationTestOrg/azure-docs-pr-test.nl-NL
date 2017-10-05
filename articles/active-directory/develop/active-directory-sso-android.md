---
title: Het inschakelen van eenmalige aanmelding voor cross-app voor Android met behulp van ADAL | Microsoft Docs
description: 'Het gebruik van de functies van de ADAL-SDK voor eenmalige aanmelding inschakelen tussen uw toepassingen. '
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
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="7b215-103">Het inschakelen van eenmalige aanmelding voor cross-app voor Android met behulp van ADAL</span><span class="sxs-lookup"><span data-stu-id="7b215-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="7b215-104">Mits eenmalige aanmelding (SSO) zodat gebruikers alleen moeten eenmaal hun referenties invoeren en deze referenties automatisch laten samenwerken binnen wordt nu toepassingen door klanten verwacht.</span><span class="sxs-lookup"><span data-stu-id="7b215-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="7b215-105">De problemen in hun gebruikersnaam en wachtwoord invoeren op een klein scherm, vaak keren gecombineerd met een extra factor (2FA), zoals een telefoongesprek of ge-code, resulteert in een snelle ergernis als een gebruiker heeft om dit te doen meer dan één keer voor het product.</span><span class="sxs-lookup"><span data-stu-id="7b215-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="7b215-106">Bovendien, als u een identiteitsplatform die van andere toepassingen zoals Microsoft-Accounts of een werkaccount van Office365 gebruikmaken mogelijk toepast, verwachten klanten dat de referenties die moeten zijn beschikbaar voor gebruik in hun toepassingen ongeacht de leverancier.</span><span class="sxs-lookup"><span data-stu-id="7b215-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="7b215-107">De Microsoft Identity-platform, samen met onze SDK's van Microsoft Identity doet dit harde werk voor u en biedt u de mogelijkheid om u te overleggen van uw klanten met eenmalige aanmelding zich binnen uw eigen reeks toepassingen of, net als bij onze broker-capaciteit en de verificator-toepassingen, via het hele apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b215-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="7b215-108">In dit scenario wordt uitgelegd hoe u onze SDK in uw toepassing voordeel bieden aan uw klanten configureren.</span><span class="sxs-lookup"><span data-stu-id="7b215-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="7b215-109">In dit scenario is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="7b215-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="7b215-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b215-110">Azure Active Directory</span></span>
* <span data-ttu-id="7b215-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7b215-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="7b215-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="7b215-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="7b215-113">Voorwaardelijke toegang voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b215-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="7b215-114">De voorgaande document wordt ervan uitgegaan dat u weet hoe [inrichten van toepassingen in de oude portal voor Azure Active Directory](active-directory-how-to-integrate.md) en uw toepassing met geïntegreerde de [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="7b215-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="7b215-115">SSO-concepten in het Identiteitsplatform van Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b215-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="7b215-116">Microsoft Identity Beleggingsmakelaars</span><span class="sxs-lookup"><span data-stu-id="7b215-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="7b215-117">Microsoft biedt toepassingen voor elk mobiel platform voor het overbruggen van referenties voor toepassingen van verschillende leveranciers en kan voor speciale verbeterde functies waarvoor een enkele veilige plaats waar om referenties te valideren.</span><span class="sxs-lookup"><span data-stu-id="7b215-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="7b215-118">We noemen deze **beleggingsmakelaars**.</span><span class="sxs-lookup"><span data-stu-id="7b215-118">We call these **brokers**.</span></span> <span data-ttu-id="7b215-119">Op iOS en Android zijn deze opgenomen in downloadbare toepassingen dat klanten afzonderlijk installeren of door een bedrijf die enkele of alle van het apparaat voor hun werknemers beheert op het apparaat kunnen worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7b215-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="7b215-120">Deze beleggingsmakelaars ondersteuning voor het beheer van beveiliging voor sommige toepassingen of het hele apparaat op basis van wat de IT-beheerders willen.</span><span class="sxs-lookup"><span data-stu-id="7b215-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="7b215-121">In Windows, wordt deze functionaliteit verstrekt door een ingebouwd in het besturingssysteem en technisch als de Webauthenticatiebroker bekend kiezen.</span><span class="sxs-lookup"><span data-stu-id="7b215-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="7b215-122">Voor meer informatie over hoe we gebruiken deze beleggingsmakelaars en hoe uw klanten mogelijk ze in hun aanmelding stroom voor het lezen van Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="7b215-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="7b215-123">Patronen voor logboekregistratie in op mobiele apparaten</span><span class="sxs-lookup"><span data-stu-id="7b215-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="7b215-124">Toegang tot de referenties op apparaten als volgt twee basispatronen die voor de Microsoft Identity-platform:</span><span class="sxs-lookup"><span data-stu-id="7b215-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="7b215-125">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="7b215-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="7b215-126">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="7b215-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="7b215-127">Niet-broker assisted-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="7b215-127">Non-broker assisted logins</span></span>
<span data-ttu-id="7b215-128">Niet-broker assisted aanmeldingen zijn aanmelding ervaringen die gebeuren inline met de toepassing en het gebruik van de lokale opslag op het apparaat voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="7b215-129">Deze opslag kan worden gedeeld tussen toepassingen, maar de referenties zijn nauw gekoppeld aan de app of suite van apps met behulp van deze referentie.</span><span class="sxs-lookup"><span data-stu-id="7b215-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="7b215-130">U hebt waarschijnlijk is dit in veel mobiele toepassingen wanneer u een gebruikersnaam en wachtwoord in de toepassing zelf invoert.</span><span class="sxs-lookup"><span data-stu-id="7b215-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="7b215-131">Deze aanmeldingen hebben de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="7b215-132">Er bestaat een gebruikerservaring volledig in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="7b215-133">Referenties kunnen worden gedeeld door toepassingen die zijn ondertekend met hetzelfde certificaat, een ervaring voor één aanmelding om uw pakket toepassingen te bieden.</span><span class="sxs-lookup"><span data-stu-id="7b215-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="7b215-134">Besturingselement rond de ervaring van logboekregistratie in is opgegeven voor de toepassing vóór en na het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7b215-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="7b215-135">Deze aanmeldingen hebben de volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="7b215-136">Kan niet-gebruikerservaring eenmalige aanmelding via alle apps die gebruikmaken van een Microsoft-Identity alleen via de Microsoft-Identities die uw toepassing is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7b215-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="7b215-137">Uw toepassing kan niet worden gebruikt met meer geavanceerde zakelijke functies zoals voorwaardelijke toegang, of gebruik het InTune-pakket.</span><span class="sxs-lookup"><span data-stu-id="7b215-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="7b215-138">Uw toepassing ondersteunt geen verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7b215-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="7b215-139">Hier volgt een weergave over de werking van de Microsoft Identity-SDK's met de gedeelde opslag van uw toepassingen en eenmalige aanmelding inschakelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="7b215-140">Assisted aanmeldingen Broker</span><span class="sxs-lookup"><span data-stu-id="7b215-140">Broker assisted logins</span></span>
<span data-ttu-id="7b215-141">Aanmeldingen Broker-ondersteunde zijn aanmelding ervaringen die optreden in de broker-toepassing en de opslag en de beveiliging van de broker gebruiken voor het delen van referenties voor alle toepassingen die de Microsoft Identity-platform van toepassing op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b215-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="7b215-142">Dit betekent dat uw toepassingen afhankelijk zijn van de broker gebruikers aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7b215-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="7b215-143">Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of op het apparaat kunnen worden geactiveerd door een bedrijf die het apparaat voor de gebruiker beheert.</span><span class="sxs-lookup"><span data-stu-id="7b215-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="7b215-144">Een voorbeeld van dit type toepassing is de Microsoft Authenticator-toepassing op iOS.</span><span class="sxs-lookup"><span data-stu-id="7b215-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="7b215-145">In Windows worden deze functionaliteit wordt verstrekt door een ingebouwd in het besturingssysteem en technisch als de Webauthenticatiebroker bekend kiezen.</span><span class="sxs-lookup"><span data-stu-id="7b215-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="7b215-146">De ervaring varieert per platform en kan soms worden verstoren aan gebruikers als dat niet correct worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="7b215-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="7b215-147">U kunt waarschijnlijk meest bekend zijn met dit patroon als u de Facebook-toepassing geïnstalleerd en Facebook-verbinding van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="7b215-148">De Microsoft Identity-platform gebruikt hetzelfde patroon.</span><span class="sxs-lookup"><span data-stu-id="7b215-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="7b215-149">Voor iOS die dit tot een 'overgang leidt' komt animatie waarbij uw toepassing wordt verzonden naar de achtergrond tijdens de Microsoft Authenticator toepassingen naar de achtergrond voor de gebruiker te selecteren welke account die ze graag willen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7b215-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="7b215-150">Voor Android en Windows wordt de account-kiezer boven op uw toepassing minder verstoren aan de gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b215-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="7b215-151">Hoe de broker opgehaald aangeroepen</span><span class="sxs-lookup"><span data-stu-id="7b215-151">How the broker gets invoked</span></span>
<span data-ttu-id="7b215-152">Als een compatibel broker is geïnstalleerd op het apparaat, zoals de toepassing Microsoft Authenticator doet de Microsoft Identity-SDK's automatisch het werk van de broker voor u wordt aangeroepen wanneer een gebruiker aangeeft voor het aanmelden met een account van de Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="7b215-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="7b215-153">Dit account kan worden een persoonlijk Microsoft-Account, werk of schoolaccount of een account dat u opgeeft en host in Azure met behulp van onze producten B2C en B2B.</span><span class="sxs-lookup"><span data-stu-id="7b215-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="7b215-154">Hoe we zorgen dat de toepassing is geldig</span><span class="sxs-lookup"><span data-stu-id="7b215-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="7b215-155">De noodzaak om te controleren of de identiteit van een aanroep van de toepassing die de broker is van cruciaal belang voor de beveiliging we in de broker bieden ondersteunde aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="7b215-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="7b215-156">Geen iOS of Android zorgt ervoor dat unieke id's die alleen geldig voor een bepaalde toepassing zijn zodat schadelijke toepassingen mogelijk '' een legitieme toepassings-id vervalsen en de tokens die zijn bedoeld voor de toepassing legitieme ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7b215-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="7b215-157">Om ervoor te zorgen dat we altijd communiceren met de juiste toepassing tijdens runtime, vraagt u de ontwikkelaar een aangepaste redirectURI bieden bij het registreren van de toepassing met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7b215-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="7b215-158">**Hoe ontwikkelaars deze omleidings-URI moeten stellen wordt hieronder in detail besproken.**</span><span class="sxs-lookup"><span data-stu-id="7b215-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="7b215-159">Deze aangepaste redirectURI de vingerafdruk van het certificaat van de toepassing bevat en uniek zijn voor de toepassing door de Google Play Store is gewaarborgd.</span><span class="sxs-lookup"><span data-stu-id="7b215-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="7b215-160">Wanneer een toepassing de broker aanroept, vraagt de broker het besturingssysteem Android om te voorzien de vingerafdruk van het certificaat dat de broker genoemd.</span><span class="sxs-lookup"><span data-stu-id="7b215-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="7b215-161">De broker biedt de vingerafdruk van dit certificaat naar Microsoft in de aanroep naar ons identiteitssysteem.</span><span class="sxs-lookup"><span data-stu-id="7b215-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="7b215-162">Als de vingerafdruk van het certificaat van de toepassing komt niet overeen met de vingerafdruk van het certificaat aan ons door de ontwikkelaar tijdens de registratie wordt geleverd, wordt er toegang tot de tokens voor de resource van de toepassing aanvragen geweigerd.</span><span class="sxs-lookup"><span data-stu-id="7b215-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="7b215-163">Deze controle zorgt ervoor dat alleen de toepassing die zijn geregistreerd door de ontwikkelaar tokens ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7b215-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="7b215-164">**De ontwikkelaar heeft de keuze van als de SDK van Microsoft Identity de broker roept of gebruikt de niet-broker assisted-stroom.**</span><span class="sxs-lookup"><span data-stu-id="7b215-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="7b215-165">Als de ontwikkelaar ervoor kiest geen gebruik van de broker-ondersteunde stroom te ze echter het voordeel verliezen van het gebruik van eenmalige aanmeldingsreferenties dat de gebruiker mogelijk al toegevoegd op het apparaat en wordt voorkomen dat de toepassing wordt gebruikt met zakelijke functies die Microsoft zijn klanten zoals voorwaardelijke toegang, beheermogelijkheden voor Intune en verificatie op basis van certificaten biedt.</span><span class="sxs-lookup"><span data-stu-id="7b215-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="7b215-166">Deze aanmeldingen hebben de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="7b215-167">Gebruiker merkt dat eenmalige aanmelding via hun toepassingen ongeacht de leverancier.</span><span class="sxs-lookup"><span data-stu-id="7b215-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="7b215-168">Uw toepassing kunt meer geavanceerde zakelijke functies zoals voorwaardelijke toegang gebruiken of de InTune-productreeks gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b215-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="7b215-169">Uw toepassing kan ondersteuning voor verificatie op basis van certificaten voor zakelijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7b215-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="7b215-170">Veel veiligere aanmeldingservaring als de identiteit van de toepassing en de gebruiker worden geverifieerd door de toepassing broker met algoritmen voor extra beveiliging en versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7b215-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="7b215-171">Deze aanmeldingen hebben de volgende nadelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="7b215-172">De gebruiker is overgegaan buiten de ervaring van uw toepassing in iOS terwijl referenties worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="7b215-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="7b215-173">Verlies van de mogelijkheid voor het beheren van de aanmeldingservaring voor uw klanten in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="7b215-174">Hier volgt een weergave over de werking van de Microsoft Identity-SDK's met de toepassingen broker eenmalige aanmelding inschakelen:</span><span class="sxs-lookup"><span data-stu-id="7b215-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="7b215-175">Uitgerust met deze achtergrondinformatie u kunnen moet om beter te begrijpen en eenmalige aanmelding implementeren in uw toepassing met de Microsoft Identity-platform en SDK's.</span><span class="sxs-lookup"><span data-stu-id="7b215-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="7b215-176">Inschakelen van verschillende Apps eenmalige aanmelding met ADAL</span><span class="sxs-lookup"><span data-stu-id="7b215-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="7b215-177">We gebruiken hier de ADAL-Android SDK:</span><span class="sxs-lookup"><span data-stu-id="7b215-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="7b215-178">Geen broker assisted eenmalige aanmelding voor uw suite van apps inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b215-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="7b215-179">Ondersteuning voor broker-ondersteunde eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b215-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="7b215-180">Eenmalige aanmelding inschakelen voor niet-broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b215-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="7b215-181">Geen broker assisted SSO op toepassingen met beheren de Microsoft Identity-SDK's voor veel van de complexiteit van eenmalige aanmelding voor u.</span><span class="sxs-lookup"><span data-stu-id="7b215-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="7b215-182">Dit omvat de juiste gebruiker zoeken in de cache en onderhouden van een lijst met aangemelde gebruikers om te zoeken.</span><span class="sxs-lookup"><span data-stu-id="7b215-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="7b215-183">Eenmalige aanmelding inschakelen voor toepassingen die u bezit, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7b215-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="7b215-184">Zorg ervoor dat alle gebruikers van uw toepassingen dezelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="7b215-185">Zorg ervoor dat al uw toepassingen hebben dezelfde set SharedUserID.</span><span class="sxs-lookup"><span data-stu-id="7b215-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="7b215-186">Zorg ervoor dat alle toepassingen dezelfde handtekeningcertificaat van de uit de Google Play store delen, zodat u opslag kunt delen.</span><span class="sxs-lookup"><span data-stu-id="7b215-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="7b215-187">Stap 1: Met behulp van dezelfde Client-ID / toepassing-ID voor alle toepassingen in uw suite van apps</span><span class="sxs-lookup"><span data-stu-id="7b215-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="7b215-188">In de volgorde voor het platform voor Microsoft Identity weten dat het delen van tokens via uw toepassingen is toegestaan, moet elk van uw toepassingen delen van hetzelfde Client-ID of id van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="7b215-189">Dit is de unieke id die aan u is opgegeven bij de registratie van uw eerste toepassing in de portal.</span><span class="sxs-lookup"><span data-stu-id="7b215-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="7b215-190">U vraagt zich misschien af hoe u verschillende apps met de Microsoft Identity-service wordt geïdentificeerd als deze gebruikmaakt van de dezelfde toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="7b215-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="7b215-191">Het antwoord is met de **omleidings-URI's**.</span><span class="sxs-lookup"><span data-stu-id="7b215-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="7b215-192">Elke toepassing kan meerdere omleidings-URI's geregistreerd in de portal voor onboarding hebben.</span><span class="sxs-lookup"><span data-stu-id="7b215-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="7b215-193">Elke app in de suite hebben een verschillende omleidings-URI.</span><span class="sxs-lookup"><span data-stu-id="7b215-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="7b215-194">Een voorbeeld van hoe dit eruitziet lager is dan:</span><span class="sxs-lookup"><span data-stu-id="7b215-194">An example of how this looks is below:</span></span>

<span data-ttu-id="7b215-195">App1 omleidings-URI:`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="7b215-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="7b215-196">App2 omleidings-URI:`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="7b215-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="7b215-197">App3 omleidings-URI:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="7b215-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="7b215-198">....</span><span class="sxs-lookup"><span data-stu-id="7b215-198">....</span></span>

<span data-ttu-id="7b215-199">Deze zijn genest onder dezelfde client-ID / toepassings-ID en opgezocht op basis van de omleidings-URI die u in de configuratie van de SDK aan ons retourneren.</span><span class="sxs-lookup"><span data-stu-id="7b215-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="7b215-200">*Houd er rekening mee dat de indeling van deze omleidings-URI's hieronder worden beschreven. U kunt een omleidings-URI tenzij u wilt ondersteunen de broker in dat geval moeten ze ziet er ongeveer als de bovenstaande*</span><span class="sxs-lookup"><span data-stu-id="7b215-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="7b215-201">Stap 2: Gedeelde opslag configureren in Android</span><span class="sxs-lookup"><span data-stu-id="7b215-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="7b215-202">Instellen van de `SharedUserID` valt buiten het bereik van dit document, maar kan worden geleerd door de Google Android-documentatie lezen op de [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="7b215-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="7b215-203">Wat is het belangrijk is dat u besluit dat u wilt uw sharedUserID wordt aangeroepen en wordt deze gebruikt op al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7b215-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="7b215-204">Zodra u hebt de `SharedUserID` in al uw toepassingen bent u klaar voor gebruik van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b215-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="7b215-205">Wanneer u delen van opslag in uw toepassingen kunt elke toepassing gebruikers verwijderen of slechter verwijderen van alle tokens inlezen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="7b215-206">Dit is vooral rampzalig zijn als er toepassingen die afhankelijk zijn van de tokens werk op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="7b215-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="7b215-207">Het delen van opslag, betekent dat u voorzichtig in bewerkingen voor alle verwijderen via de Microsoft Identity-SDK's moet zijn.</span><span class="sxs-lookup"><span data-stu-id="7b215-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="7b215-208">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7b215-208">That's it!</span></span> <span data-ttu-id="7b215-209">De Microsoft Identity-SDK wordt nu referenties delen in al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7b215-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="7b215-210">De lijst met gebruikers wordt ook gedeeld met exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="7b215-211">Eenmalige aanmelding inschakelen voor broker ondersteund eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b215-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="7b215-212">De mogelijkheid om een toepassing te gebruiken broker die is geïnstalleerd op het apparaat is **standaard uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="7b215-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="7b215-213">Als u wilt gebruiken van uw toepassing met de broker moet u enkele aanvullende configuratiestappen en code toevoegen aan uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="7b215-214">De stappen te volgen zijn:</span><span class="sxs-lookup"><span data-stu-id="7b215-214">The steps to follow are:</span></span>

1. <span data-ttu-id="7b215-215">Schakel de broker-modus in uw toepassingscode aanroep van de SDK MS</span><span class="sxs-lookup"><span data-stu-id="7b215-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="7b215-216">Stel een nieuwe omleidings-URI en bieden die zowel de app en uw app-registratie</span><span class="sxs-lookup"><span data-stu-id="7b215-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="7b215-217">Instellen van de juiste machtigingen in de Android-manifestbestand</span><span class="sxs-lookup"><span data-stu-id="7b215-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="7b215-218">Stap 1: Broker-modus inschakelen in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="7b215-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="7b215-219">De mogelijkheid voor uw toepassing gebruik van de broker is ingeschakeld wanneer u de 'instellingen' of de eerste installatie van de verificatie-instantie maakt.</span><span class="sxs-lookup"><span data-stu-id="7b215-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="7b215-220">U doen dit door het instellen van uw type ApplicationSettings in uw code:</span><span class="sxs-lookup"><span data-stu-id="7b215-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="7b215-221">Stap 2: Een nieuwe omleidings-URI met URL-schema maken</span><span class="sxs-lookup"><span data-stu-id="7b215-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="7b215-222">Om ervoor te zorgen dat we de referentie-tokens altijd naar de juiste toepassing terugkeren, moeten we controleren of dat we noemen terug naar de toepassing op een manier die het besturingssysteem Android kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="7b215-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="7b215-223">Het besturingssysteem Android maakt gebruik van de hash van het certificaat in de Google Play store.</span><span class="sxs-lookup"><span data-stu-id="7b215-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="7b215-224">Dit kan niet door een rogue-toepassing worden vervalst.</span><span class="sxs-lookup"><span data-stu-id="7b215-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="7b215-225">Daarom we maken gebruik van dit samen met de URI van onze toepassing broker om ervoor te zorgen dat de tokens worden geretourneerd naar de juiste toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b215-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="7b215-226">Moet u voor het maken van deze unieke omleidings-URI voor beide in uw toepassing instellen als een omleidings-URI in onze portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="7b215-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="7b215-227">De omleidings-URI moet de juiste indeling zijn:</span><span class="sxs-lookup"><span data-stu-id="7b215-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="7b215-228">Voorbeeld: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="7b215-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="7b215-229">Deze omleidings-URI moet worden opgegeven in uw app registreren met de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b215-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7b215-230">Zie voor meer informatie over Azure AD-app-registratie [integreren met Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="7b215-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="7b215-231">Stap 3: De juiste machtigingen in uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="7b215-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="7b215-232">Onze toepassing broker in Android gebruikt de Accounts Manager-functie van het besturingssysteem Android voor het beheren van referenties in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7b215-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="7b215-233">Om te gebruiken van de broker in Android moet uw app-manifest machtigingen hebben voor AccountManager accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b215-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="7b215-234">Dit wordt uitgebreid beschreven in de [Google documentatie voor Account Manager hier](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="7b215-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="7b215-235">In het bijzonder zijn deze machtigingen:</span><span class="sxs-lookup"><span data-stu-id="7b215-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="7b215-236">U kunt eenmalige aanmelding hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7b215-236">You've configured SSO!</span></span>
<span data-ttu-id="7b215-237">Nu wordt de Microsoft Identity-SDK automatisch zowel referenties delen in uw toepassingen en aanroepen van de broker, indien aanwezig zijn op hun apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b215-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

