---
title: Apps, machtigingen en toestemming in Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integreert uw on-premises adreslijsten met Azure Active Directory. Hiermee kunt u een algemene identiteit bieden voor Office 365-, Azure- en SaaS-toepassingen die zijn geïntegreerd met Azure AD."
keywords: inleiding tot Azure AD, apps, wat is Azure AD Connect, Active Directory installeren
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 6f6baf5e1538fb280a899065c64ca5688473c04a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="08a84-105">Apps, machtigingen en toestemming in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08a84-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="08a84-106">In Azure Active Directory kunt u toepassingen toevoegen aan uw directory.</span><span class="sxs-lookup"><span data-stu-id="08a84-106">Within Azure Active Directory, you can add applications to your directory.</span></span>  <span data-ttu-id="08a84-107">De toepassingen kunnen variëren afhankelijk van het type toepassing.</span><span class="sxs-lookup"><span data-stu-id="08a84-107">The applications can vary depending on the type of application.</span></span>  <span data-ttu-id="08a84-108">Als u toepassingen in de klassieke portal wilt bekijken, selecteert u een directory en kiest u toepassingen.</span><span class="sxs-lookup"><span data-stu-id="08a84-108">To view applications in the classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="08a84-109">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="08a84-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="08a84-110">App-typen</span><span class="sxs-lookup"><span data-stu-id="08a84-110">Types of apps</span></span>

1. <span data-ttu-id="08a84-111">**Apps met één tenant**</span><span class="sxs-lookup"><span data-stu-id="08a84-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="08a84-112">**Apps met één tenant** - Ook vaak Line-of-Business-apps (LOB) genoemd.</span><span class="sxs-lookup"><span data-stu-id="08a84-112">**Single-tenant apps** - Often referred to as line-of-business (LOB) apps.</span></span> <span data-ttu-id="08a84-113">Dit is het geval wanneer iemand binnen uw organisatie een eigen app ontwikkelt en wilt dat gebruikers in de organisatie zich kunnen aanmelden bij de app.</span><span class="sxs-lookup"><span data-stu-id="08a84-113">This is the case where someone within your organization develops their own app, and would like users in the organization to be able to sign in to the app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="08a84-114">**App Proxy-apps** - Wanneer u een on-premises toepassing gebruikt met Azure AD App Proxy wordt een app met één tenant geregistreerd in uw tenant (naast de App Proxy-service).</span><span class="sxs-lookup"><span data-stu-id="08a84-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition to the App Proxy service).</span></span> <span data-ttu-id="08a84-115">Deze app vertegenwoordigt uw on-premises toepassing voor alle cloudinteracties (bijvoorbeeld verificatie).</span><span class="sxs-lookup"><span data-stu-id="08a84-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="08a84-116">(App Proxy vereist Azure AD Basic of hoger.)</span><span class="sxs-lookup"><span data-stu-id="08a84-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="08a84-117">**Apps met meerdere tenants**</span><span class="sxs-lookup"><span data-stu-id="08a84-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="08a84-118">**Apps met meerdere tenants waar anderen toestemming voor kunnen geven** - Vergelijkbaar met 'apps met één tenant die uw organisatie ontwikkelt'.</span><span class="sxs-lookup"><span data-stu-id="08a84-118">**Multi-tenant apps which others can consent to** - similar to “single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="08a84-119">Het belangrijkste verschil (naast de logica in de app zelf) is dat gebruikers van andere tenants kunnen ook toestemming kunnen geven voor de app en zich erbij kunnen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="08a84-119">The main difference (besides the logic in the app itself) is that users from other tenants can also consent to and sign in to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="08a84-120">**Apps met meerdere tenants die anderen ontwikkelen en waar Contoso toestemming voor kan geven**.</span><span class="sxs-lookup"><span data-stu-id="08a84-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="08a84-121">(Kort gezegd ook 'toegestane apps'.) Dit is het tegenovergestelde van 'apps met meerdere tenants die uw organisatie ontwikkelt'.</span><span class="sxs-lookup"><span data-stu-id="08a84-121">(Or “consented apps”, for short.) This is the flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="08a84-122">Wanneer een andere organisatie een app met meerdere tenants ontwikkelt, kunnen de gebruikers in uw organisatie er toestemming voor geven en zich erbij aanmelden.</span><span class="sxs-lookup"><span data-stu-id="08a84-122">When another organization develops a multi-tenant app, users of your organization can consent to the app and sign in to it.</span></span>
    - <span data-ttu-id="08a84-123">**Apps van Microsoft** - Apps die Microsoft-services vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="08a84-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="08a84-124">U geeft toestemming wanneer u zich registreert voor de service.</span><span class="sxs-lookup"><span data-stu-id="08a84-124">Consent is driven by the fact that you sign up for the service.</span></span> <span data-ttu-id="08a84-125">Er is soms sprake van speciale UX en logica voor apps van Microsoft. Vaak wordt hier gebruik van gemaakt voor het definiëren van beleid voor toegang tot de app.</span><span class="sxs-lookup"><span data-stu-id="08a84-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="08a84-126">**Vooraf geïntegreerde apps** - Apps die beschikbaar zijn in de Azure AD App Gallery en die u aan uw directory kunt toevoegen voor eenmalige-aanmeldingsfunctionaliteit voor (en in sommige gevallen voor inrichting van) populaire SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="08a84-126">**Pre-integrated apps** - Apps available in the Azure AD App Gallery, which you can add to your directory to provide single sign-on (and in some cases, provisioning) to popular SaaS apps.</span></span>
    - <span data-ttu-id="08a84-127">**Azure AD met eenmalige aanmelding** - 'Echte' eenmalige aanmelding voor apps die met Azure AD kunnen worden geïntegreerd via een ondersteund aanmeldingsprotocol zoals SAML 2.0 of OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="08a84-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="08a84-128">De wizard begeleidt u bij het instellen.</span><span class="sxs-lookup"><span data-stu-id="08a84-128">The wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="08a84-129">**Wachtwoord voor eenmalige aanmelding**: Azure AD bewaart de referenties van de gebruiker voor de app op een veilige manier. De referenties worden door de Azure AD App Access-browserextensie in het aanmeldingsformulier geplaatst.</span><span class="sxs-lookup"><span data-stu-id="08a84-129">**Password single sign-on**: Azure AD securely stores the user’s credentials for the app, and the credentials are “injected” into the sign-in form by the Azure AD App Access browser extension.</span></span> <span data-ttu-id="08a84-130">Dit heet ook wel 'password vaulting'.</span><span class="sxs-lookup"><span data-stu-id="08a84-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="08a84-131">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="08a84-131">Permissions</span></span>

<span data-ttu-id="08a84-132">Wanneer een app wordt geregistreerd, definieert de gebruiker die de app registreert (de ontwikkelaar) tot welke machtigingen en resources de app toegang nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="08a84-132">When an app is registered, the user performing the app registration (that is, the developer) defines which permissions the app needs access to, and which resources.</span></span> <span data-ttu-id="08a84-133">(De resources worden gedefinieerd als andere apps.) Iemand die bijvoorbeeld een e-mail-app bouwt, verklaart dat de app toegang nodig heeft tot de postvakken van de aangemelde gebruiker ('Postvakken van de aangemelde gebruiker openen'). Dit is een machtiging die beschikbaar is via de resource Office 365 Exchange Online:</span><span class="sxs-lookup"><span data-stu-id="08a84-133">(The resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires the “Access mailboxes as the signed-in user” permission in the “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="08a84-134">Om het mogelijk te maken dat één app (de client) een bepaalde machtiging kan aanvragen bij een andere app (de resource), moet de ontwikkelaar van de resource-app de bestaande machtigingen definiëren.</span><span class="sxs-lookup"><span data-stu-id="08a84-134">In order for one app (the client) to request a certain permission from another app (the resource), the developer of the resource app defines the permissions that exist.</span></span> <span data-ttu-id="08a84-135">In ons voorbeeld heeft Microsoft, de eigenaar van de resource-app Office 365 Exchange Online, een machtiging met de naam 'Postvakken van de aangemelde gebruiker openen' gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="08a84-135">In our example, Microsoft, the owner of the “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as the signed-in user”.</span></span>

<span data-ttu-id="08a84-136">Bij het definiëren van machtigingen moet de app-ontwikkelaar opgeven of er toestemming voor de machtigingen kan worden gegeven en of een beheerder er toestemming voor moet geven.</span><span class="sxs-lookup"><span data-stu-id="08a84-136">When defining permissions, the app developer must define if the permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="08a84-137">Op die manier kunnen ontwikkelaars gebruikers in staat stellen om zelf toestemming te geven voor apps die machtigingen met een lage gevoeligheid aanvragen. Beheerders moeten in dit geval wel nog toestemming geven voor machtigingen met een hogere gevoeligheid.</span><span class="sxs-lookup"><span data-stu-id="08a84-137">This allows developers to allow users to consent on their own to apps requesting only low-sensitivity permissions, but require admins to consent to more sensitive permissions.</span></span> <span data-ttu-id="08a84-138">De Azure Active Directory-resource-app is bijvoorbeeld zodanig ingesteld dat gebruikers toestemming kunnen geven voor het aanvragen van beperkte, alleen-lezen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="08a84-138">For example, the “Azure Active Directory” resource app, has been defined, so users can consent to apps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="08a84-139">Er is echter toestemming van een beheerder nodig voor volledige lees- en schrijftoegang.</span><span class="sxs-lookup"><span data-stu-id="08a84-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="08a84-140">Omdat systeemeigen clients niet worden geverifieerd, kan een app die is gedefinieerd als systeemeigen client-app alleen overgedragen machtigingen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="08a84-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="08a84-141">Dit betekent dat er altijd een daadwerkelijke gebruiker betrokken moet zijn bij het ophalen van een token.</span><span class="sxs-lookup"><span data-stu-id="08a84-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="08a84-142">Web-apps en web-API's (vertrouwelijke clients) moeten altijd worden geverifieerd door Azure AD bij het ophalen van een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="08a84-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="08a84-143">Dit betekent dat ze ook machtigingen die zich beperken tot apps kunnen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="08a84-143">Meaning they also have the possibility of requesting app-only permissions.</span></span> <span data-ttu-id="08a84-144">Dat is bijvoorbeeld nodig als een back-endservice moet worden geverifieerd door een andere back-endservice.</span><span class="sxs-lookup"><span data-stu-id="08a84-144">For example, if one back-end service needs to authenticate to another back-end service.</span></span> <span data-ttu-id="08a84-145">Toepassingen waarvoor machtigingen die zich beperken tot de app worden aangevraagd, moeten altijd worden goedgekeurd door een beheerder.</span><span class="sxs-lookup"><span data-stu-id="08a84-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="08a84-146">Samenvatting:</span><span class="sxs-lookup"><span data-stu-id="08a84-146">Summarizing:</span></span>



- <span data-ttu-id="08a84-147">In een app (client) is vastgelegd welke machtigingen nodig zijn voor andere apps (resources).</span><span class="sxs-lookup"><span data-stu-id="08a84-147">An app (client) states the permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="08a84-148">In een app (resource) is vastgelegd welke machtigingen beschikbaar zijn voor andere apps (clients).</span><span class="sxs-lookup"><span data-stu-id="08a84-148">An app (resource) states what permissions are exposed to other apps (clients).</span></span>
- <span data-ttu-id="08a84-149">Een machtiging kan zich beperken tot één app of kan overgedragen zijn.</span><span class="sxs-lookup"><span data-stu-id="08a84-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="08a84-150">Een overgedragen machtiging kan worden gemarkeerd als 'gebruikerstoestemming toegestaan' of 'beheerderstoestemming vereist'.</span><span class="sxs-lookup"><span data-stu-id="08a84-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="08a84-151">Een app kan functioneren als een client (door op te geven dat machtigingen voor een resource nodig zijn), als een resource (door op te geven welke machtigingen beschikbaar zijn) of als beide.</span><span class="sxs-lookup"><span data-stu-id="08a84-151">An app can behave as a client (by declaring that it needs permissions to a resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="08a84-152">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="08a84-152">Controls</span></span>

<span data-ttu-id="08a84-153">Hier volgt een lijst van de verschillende besturingselementen voor beheerders die beschikbaar zijn voor deze zaken.</span><span class="sxs-lookup"><span data-stu-id="08a84-153">The following is a list of the different admin controls available for all this behavior.</span></span> <span data-ttu-id="08a84-154">De besturingselementen voor beheerders kunnen worden geopend in de klassieke portal. Ga daarvoor naar Configureren in de map.</span><span class="sxs-lookup"><span data-stu-id="08a84-154">The admin controls can be accessed in the classic portal from configure under the directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="08a84-155">In Azure Portal gaat u onder **Beheren** naar **Gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="08a84-155">In the Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="08a84-156">U bepaalt of gebruikers toestemming kunnen geven voor apps:</span><span class="sxs-lookup"><span data-stu-id="08a84-156">You can control whether users can consent to apps:</span></span>

<span data-ttu-id="08a84-157">Selecteer in de klassieke portal de optie **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png) (Gebruikers mogen toepassingen machtigingen verlenen voor toegang tot hun gegevens.)</span><span class="sxs-lookup"><span data-stu-id="08a84-157">In the classic portal, select **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="08a84-158">In Azure Portal selecteert u de optie **Gebruikers kunnen apps toegang tot de gegevens verlenen**.</span><span class="sxs-lookup"><span data-stu-id="08a84-158">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="08a84-159">U bepaalt of gebruikers hun eigen LOB-apps met één tenant mogen registreren. In de klassieke portal selecteert u **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png) (Gebruikers mogen geïntegreerde toepassingen toevoegen.)</span><span class="sxs-lookup"><span data-stu-id="08a84-159">You can control whether users can register their own single-tenant LOB apps: In the classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="08a84-160">In Azure Portal selecteert u de optie **Gebruikers kunnen apps toegang tot de gegevens verlenen**.</span><span class="sxs-lookup"><span data-stu-id="08a84-160">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="08a84-161">Zelfs als u gebruikers toestaat om LOB-apps met één tenant te registreren, gelden er beperkingen voor wat er mag worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="08a84-161">Even if you do allow users to register single-tenant LOB apps, there are limits to what can be registered.</span></span>  
><span data-ttu-id="08a84-162">Dit geldt bijvoorbeeld voor ontwikkelaars die geen directorybeheerder zijn.</span><span class="sxs-lookup"><span data-stu-id="08a84-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="08a84-163">Gebruikers mogen van een app met één tenant geen app met meerdere tenants maken.</span><span class="sxs-lookup"><span data-stu-id="08a84-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="08a84-164">Bij het registreren van LOB-apps met één tenant mogen gebruikers geen machtigingen voor andere apps aanvragen.</span><span class="sxs-lookup"><span data-stu-id="08a84-164">When registering single-tenant LOB apps, users cannot request app-only permissions to other apps.</span></span>
>- <span data-ttu-id="08a84-165">Bij het registreren van LOB-apps met één tenant mogen gebruikers geen overgedragen machtigingen voor andere apps aanvragen als er toestemming van een beheerder voor nodig is.</span><span class="sxs-lookup"><span data-stu-id="08a84-165">When registering single-tenant LOB apps, users cannot request delegated permissions to other apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="08a84-166">Gebruikers mogen geen wijzigingen aanbrengen aan apps waar ze geen eigenaar van zijn.</span><span class="sxs-lookup"><span data-stu-id="08a84-166">Users cannot make changes to apps that they are not owners of.</span></span>



- <span data-ttu-id="08a84-167">U bepaalt of gebruikers zelf vooraf geïntegreerde apps mogen toevoegen waarvoor eenmalige aanmelding met een wachtwoord wordt gebruikt ('password vaulting') ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="08a84-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="08a84-168">U bepaalt onder welke omstandigheden toepassingen kunnen worden geopend (voorwaardelijke toegang).</span><span class="sxs-lookup"><span data-stu-id="08a84-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="08a84-169">Dit geldt zowel voor de client-app als de resource-app.</span><span class="sxs-lookup"><span data-stu-id="08a84-169">Be aware this applies both to the client app and to the resource app.</span></span> <span data-ttu-id="08a84-170">U stelt dus beleid voor voorwaardelijke toegang in waarmee u verklaart dat de app Office 365 Exchange Online alleen kan worden geopend vanaf apparaten die aan de voorwaarden voldoen.</span><span class="sxs-lookup"><span data-stu-id="08a84-170">So, say you set a conditional access policy that says that the “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="08a84-171">Dit beleid wordt ook gehandhaafd wanneer een gebruiker probeert een client-app te gebruiken die machtigingen voor Exchange Online aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="08a84-171">This policy will also kick in when a user attempts to use a client app which requests permissions to Exchange Online.</span></span>



- <span data-ttu-id="08a84-172">U hebt inzicht in welke apps zijn goedgekeurd en in welke apps worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="08a84-172">You have visibility into which apps have been consented to and which ones are being used.</span></span>

1.  <span data-ttu-id="08a84-173">Wanneer een gebruiker toestemming heeft voor een app, wordt er een ServicePrincipal-object gemaakt in de tenant.</span><span class="sxs-lookup"><span data-stu-id="08a84-173">When a user consents to an app, a ServicePrincipal object is created in the tenant.</span></span> <span data-ttu-id="08a84-174">In het controlerapport staat ook dat het ServicePrincipal-object is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a84-174">ServicePrincipal creation is included in the audit report.</span></span>
2.  <span data-ttu-id="08a84-175">De gebruikersrapporten over aanmeldingsactiviteit staat bij welke apps de gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="08a84-175">User sign-in activity reports tell you which app the user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="08a84-176">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="08a84-176">Example</span></span>

<span data-ttu-id="08a84-177">Als voorbeeld wordt de FabrikamMail for Office 365-app gebruikt. U hebt gemerkt dat gebruikers in uw tenant zich daarbij aanmelden.</span><span class="sxs-lookup"><span data-stu-id="08a84-177">As an example, let’s take the “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="08a84-178">FabrikamMail is een e-mail-app voor gebruik op Android-apparaten, gepubliceerd door Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="08a84-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="08a84-179">Deze app valt in de categorie 'Apps met meerdere tenants die anderen ontwikkelen en waar Contoso toestemming voor kan geven'.</span><span class="sxs-lookup"><span data-stu-id="08a84-179">This falls into the “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="08a84-180">Als gebruikers toestemming mogen geven, krijgen ze bij de eerste keer aanmelden een toestemmingsprompt te zien: ![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="08a84-180">If users are allowed to consent, they get a consent prompt the first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="08a84-181">'Uw postvakken openen' is de goedkeuringstekenreeks die aan de gebruiker wordt weergegeven voor de machtiging 'Postvakken van de aangemelde gebruiker openen' van Office 365 Exchange Online, Exchange in het kort.</span><span class="sxs-lookup"><span data-stu-id="08a84-181">“Access your mailboxes” is the user-facing consent string for the “Access mailboxes as the signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="08a84-182">U kunt de machtigingen bekijken door het ServicePrincipal-object voor Exchange (de resource) te zoeken dat is toegevoegd toen u zich registreerde voor Office 365.</span><span class="sxs-lookup"><span data-stu-id="08a84-182">You can see the permissions by looking up the ServicePrincipal object for Exchange (the resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="08a84-183">U kunt het ServicePrincipal-object zien als een exemplaar van de app in uw tenant dat wordt gebruikt voor het vastleggen van verschillende opties en configuraties.</span><span class="sxs-lookup"><span data-stu-id="08a84-183">You can think of the ServicePrincipal object of an “instance” of the app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="08a84-184">U kunt het bekijken met behulp van de `Get-AzureADServicePrincipal` in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08a84-184">You can see this by using the `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows the app to have the same access to mailboxes as the signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as the signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows the app full access to your mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="08a84-185">Er wordt toestemming gegeven wanneer de gebruiker op Accepteren klikt.</span><span class="sxs-lookup"><span data-stu-id="08a84-185">Consent is initiated when the user clicks “Accept”.</span></span> <span data-ttu-id="08a84-186">Eerst wordt er in de tenant een ServicePrincipal-object gemaakt voor FabrikamMail for Office 365.</span><span class="sxs-lookup"><span data-stu-id="08a84-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in the tenant.</span></span> <span data-ttu-id="08a84-187">De ServicePrincipal ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="08a84-187">The ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="08a84-188">Als u toestemming geeft voor een app, wordt er een Oauth2PermissionGrant-koppeling gemaakt tussen deze zaken:</span><span class="sxs-lookup"><span data-stu-id="08a84-188">Consenting to an app creates an Oauth2PermissionGrant link between the following:</span></span>
  
- <span data-ttu-id="08a84-189">het gebruikersobject</span><span class="sxs-lookup"><span data-stu-id="08a84-189">the user object</span></span>
- <span data-ttu-id="08a84-190">de ServicePrincipalName (SPN) van de client-app</span><span class="sxs-lookup"><span data-stu-id="08a84-190">the client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="08a84-191">de ServicePrincipalName (SPN) van de resource-app</span><span class="sxs-lookup"><span data-stu-id="08a84-191">the resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="08a84-192">machtigingen in de resource-app.</span><span class="sxs-lookup"><span data-stu-id="08a84-192">permissions in the resource app.</span></span>  

<span data-ttu-id="08a84-193">In het geval van FabrikamMail, ziet dit er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="08a84-193">In the case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="08a84-194">(**ClientId** is de service-principal object-id van FabrikamMail (de id die zojuist is gemaakt), **PrincipalId** is de gebruikersobject-id (van de gebruiker die toestemming heeft gegeven), **ResourceId** is de service-principal object-id van Exchange en het bereik is de machtiging in Exchange waar toestemming voor is gegeven).</span><span class="sxs-lookup"><span data-stu-id="08a84-194">(**ClientId** is FabrikamMail’s service principal object ID (the one that just got created), **PrincipalId** is the user object ID (of the user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is the permission in Exchange that was consented to).</span></span>

<span data-ttu-id="08a84-195">Als gebruikers geen toestemming mogen geven, krijgen ze een scherm te zien waarin staat dat machtiging is vereist.</span><span class="sxs-lookup"><span data-stu-id="08a84-195">If users are not allowed to consent, they will see a screen that says that permission is required.</span></span>

