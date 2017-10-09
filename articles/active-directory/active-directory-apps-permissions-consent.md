---
title: Apps, machtigingen en toestemming in Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide."
keywords: active directory inleiding tooAzure AD, apps, wat is Azure AD Connect installeren
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
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="ce171-105">Apps, machtigingen en toestemming in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce171-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="ce171-106">U kunt toepassingen tooyour directory toevoegen in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ce171-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="ce171-107">Hallo-toepassingen kunnen variëren afhankelijk van de toepassing hello type.</span><span class="sxs-lookup"><span data-stu-id="ce171-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="ce171-108">tooview toepassingen in de klassieke portal hello, selecteer een map en kies de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ce171-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="ce171-109">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ce171-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="ce171-110">App-typen</span><span class="sxs-lookup"><span data-stu-id="ce171-110">Types of apps</span></span>

1. <span data-ttu-id="ce171-111">**Apps met één tenant**</span><span class="sxs-lookup"><span data-stu-id="ce171-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="ce171-112">**Apps voor één tenant** -vaak tooas line-of-business (LOB)-apps.</span><span class="sxs-lookup"><span data-stu-id="ce171-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="ce171-113">Dit is Hallo geval waar iemand binnen uw organisatie ontwikkelt van hun eigen app en wilt dat gebruikers in Hallo organisatie toobe kunnen toosign in toohello-app.</span><span class="sxs-lookup"><span data-stu-id="ce171-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="ce171-114">**Toepassingsproxy van apps** : wanneer u een on-premises toepassing met Azure AD-toepassingsproxy, weer een één-tenant-app in uw tenant (in aanvulling toohello App Proxy-service) is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="ce171-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="ce171-115">Deze app vertegenwoordigt uw on-premises toepassing voor alle cloudinteracties (bijvoorbeeld verificatie).</span><span class="sxs-lookup"><span data-stu-id="ce171-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="ce171-116">(App Proxy vereist Azure AD Basic of hoger.)</span><span class="sxs-lookup"><span data-stu-id="ce171-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="ce171-117">**Apps met meerdere tenants**</span><span class="sxs-lookup"><span data-stu-id="ce171-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="ce171-118">**Multitenant-apps die anderen met instemmen kunnen** - vergelijkbare te 'single-tenant-apps die uw organisatie ontwikkelt'.</span><span class="sxs-lookup"><span data-stu-id="ce171-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="ce171-119">de belangrijkste verschil hello (naast het Hallo-logica in Hallo app zelf) is de gebruikers van andere tenants kunnen ook toestemming geven tooand toohello app aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ce171-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="ce171-120">**Apps met meerdere tenants die anderen ontwikkelen en waar Contoso toestemming voor kan geven**.</span><span class="sxs-lookup"><span data-stu-id="ce171-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="ce171-121">(Kort gezegd ook 'toegestane apps'.) Dit is Hallo spiegelen zijde van 'multitenant apps in die uw organisatie ontwikkelt'.</span><span class="sxs-lookup"><span data-stu-id="ce171-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="ce171-122">Wanneer een andere organisatie een multitenant-app ontwikkelt, kunnen gebruikers van uw organisatie toohello app toestemming en tooit aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ce171-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="ce171-123">**Apps van Microsoft** - Apps die Microsoft-services vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="ce171-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="ce171-124">Toestemming wordt aangedreven door Hallo feit dat u zich aanmeldt voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ce171-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="ce171-125">Er is het soms speciale UX en logica voor bepaalde Microsoft-apps die vaak wordt gebruikt bij het opstellen van beleid rond toegang toohello app.</span><span class="sxs-lookup"><span data-stu-id="ce171-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="ce171-126">**Vooraf geïntegreerde apps** -Apps die beschikbaar zijn in Azure AD App-galerie, die u kunt toevoegen Hallo tooyour directory tooprovide één eenmalige aanmelding (en in sommige gevallen, inrichting) toopopular SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ce171-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="ce171-127">**Azure AD met eenmalige aanmelding** - 'Echte' eenmalige aanmelding voor apps die met Azure AD kunnen worden geïntegreerd via een ondersteund aanmeldingsprotocol zoals SAML 2.0 of OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ce171-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="ce171-128">Hallo wizard leidt u door het instelt.</span><span class="sxs-lookup"><span data-stu-id="ce171-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="ce171-129">**Eenmalige aanmelding wachtwoord**: Azure AD Hallo gebruikersreferenties voor Hallo app veilig opgeslagen en Hallo referenties zijn 'geïnjecteerd' in hello aanmelden formulier door Hallo Browseruitbreiding van de toegang tot Apps van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce171-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="ce171-130">Dit heet ook wel 'password vaulting'.</span><span class="sxs-lookup"><span data-stu-id="ce171-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="ce171-131">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="ce171-131">Permissions</span></span>

<span data-ttu-id="ce171-132">Wanneer een app is geregistreerd, wordt Hallo gebruiker uitvoeren Hallo app-registratie (dat wil zeggen, Hallo developer) definieert welke machtigingen Hallo-app moet toegang tot en welke bronnen.</span><span class="sxs-lookup"><span data-stu-id="ce171-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="ce171-133">(Hallo resources zijn, zelf, gedefinieerd als andere apps). Bijvoorbeeld zou iemand een e-mail reader-app bouwen vermeld dat de app Hallo 'Postvakken toegang als de gebruiker is aangemeld Hallo' toestemming in Hallo 'Office 365 Exchange Online' resource vereist:</span><span class="sxs-lookup"><span data-stu-id="ce171-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="ce171-134">Om een app (Hallo client) toorequest een bepaalde machtiging vanuit een andere app (Hallo resource) definieert Hallo ontwikkelaar van Hallo resource app Hallo machtigingen die aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="ce171-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="ce171-135">In ons voorbeeld Microsoft hello eigenaar van de 'Office 365 Exchange Online' hello resource app, gedefinieerd hebben een machtiging met de naam "Postvakken toegang als de gebruiker is aangemeld Hallo".</span><span class="sxs-lookup"><span data-stu-id="ce171-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="ce171-136">Bij het definiëren van machtigingen moet Hallo app-ontwikkelaar definiëren als Hallo-machtiging kunt wil of als hiervoor toestemming van de beheerder.</span><span class="sxs-lookup"><span data-stu-id="ce171-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="ce171-137">Hierdoor kunnen ontwikkelaars tooallow gebruikers tooconsent op hun eigen tooapps alleen machtigingen voor lage gevoeligheid aangevraagd, maar tooconsent toomore gevoelige beheerdersmachtigingen nodig.</span><span class="sxs-lookup"><span data-stu-id="ce171-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="ce171-138">Bijvoorbeeld, Hallo 'Azure Active Directory' resource app, is gedefinieerd, zodat gebruikers kunnen toestemming van tooapps, vraagt beperkte machtigingen voor alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="ce171-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="ce171-139">Er is echter toestemming van een beheerder nodig voor volledige lees- en schrijftoegang.</span><span class="sxs-lookup"><span data-stu-id="ce171-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="ce171-140">Omdat systeemeigen clients niet worden geverifieerd, kan een app die is gedefinieerd als systeemeigen client-app alleen overgedragen machtigingen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ce171-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="ce171-141">Dit betekent dat er altijd een daadwerkelijke gebruiker betrokken moet zijn bij het ophalen van een token.</span><span class="sxs-lookup"><span data-stu-id="ce171-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="ce171-142">Web-apps en web-API's (vertrouwelijke clients) moeten altijd worden geverifieerd door Azure AD bij het ophalen van een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="ce171-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="ce171-143">Dit betekent dat ze hebben ook Hallo mogelijkheid app alleen-lezen machtigingen om te vragen.</span><span class="sxs-lookup"><span data-stu-id="ce171-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="ce171-144">Als bijvoorbeeld een back-end-service moet tooauthenticate tooanother back-end-service.</span><span class="sxs-lookup"><span data-stu-id="ce171-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="ce171-145">Toepassingen waarvoor machtigingen die zich beperken tot de app worden aangevraagd, moeten altijd worden goedgekeurd door een beheerder.</span><span class="sxs-lookup"><span data-stu-id="ce171-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="ce171-146">Samenvatting:</span><span class="sxs-lookup"><span data-stu-id="ce171-146">Summarizing:</span></span>



- <span data-ttu-id="ce171-147">Hallo-machtigingen die nodig zijn voor andere apps (bronnen) wordt aangegeven door een app (client).</span><span class="sxs-lookup"><span data-stu-id="ce171-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="ce171-148">Een app (resource) wordt aangegeven welke machtigingen zijn blootgestelde tooother apps (clients).</span><span class="sxs-lookup"><span data-stu-id="ce171-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="ce171-149">Een machtiging kan zich beperken tot één app of kan overgedragen zijn.</span><span class="sxs-lookup"><span data-stu-id="ce171-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="ce171-150">Een overgedragen machtiging kan worden gemarkeerd als 'gebruikerstoestemming toegestaan' of 'beheerderstoestemming vereist'.</span><span class="sxs-lookup"><span data-stu-id="ce171-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="ce171-151">Een app kan functioneren als een client (door op te geven dat het moet machtigingen tooa resource), als een bron (door op te geven welke machtigingen worden getoond), of als beide.</span><span class="sxs-lookup"><span data-stu-id="ce171-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="ce171-152">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="ce171-152">Controls</span></span>

<span data-ttu-id="ce171-153">Hallo Hieronder volgt een lijst met besturingselementen voor verschillende admin Hallo beschikbaar voor alle dit gedrag.</span><span class="sxs-lookup"><span data-stu-id="ce171-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="ce171-154">Hallo beheerder besturingselementen kunnen worden geopend in de klassieke portal Hallo van configureren onder Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="ce171-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="ce171-155">In hello Azure portal onder **beheren**, **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ce171-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="ce171-156">U kunt bepalen of gebruikers toestemming van tooapps geven kunnen:</span><span class="sxs-lookup"><span data-stu-id="ce171-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="ce171-157">Selecteer in de klassieke portal Hallo **gebruikers toepassingen machtigingen tooaccess kunnen geven hun gegevens.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="ce171-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="ce171-158">Selecteer in de Azure-portal hello, **gebruikers apps tooaccess kunnen toestaan hun gegevens**.</span><span class="sxs-lookup"><span data-stu-id="ce171-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="ce171-159">Kunt u bepalen of gebruikers hun eigen LOB-apps voor één tenant kunnen registreren: In de klassieke portal Selecteer Hallo **gebruikers geïntegreerde toepassingen kunnen toevoegen.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="ce171-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="ce171-160">Selecteer in de Azure-portal hello, **gebruikers apps tooaccess kunnen toestaan hun gegevens**.</span><span class="sxs-lookup"><span data-stu-id="ce171-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="ce171-161">Zelfs als u gebruikers tooregister één tenant LOB-apps toestaat, zijn er beperkingen met toowhat kunnen worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="ce171-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="ce171-162">Dit geldt bijvoorbeeld voor ontwikkelaars die geen directorybeheerder zijn.</span><span class="sxs-lookup"><span data-stu-id="ce171-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="ce171-163">Gebruikers mogen van een app met één tenant geen app met meerdere tenants maken.</span><span class="sxs-lookup"><span data-stu-id="ce171-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="ce171-164">Bij het registreren van LOB-apps voor één tenant kunnen geen gebruikers app alleen-lezen machtigingen tooother apps vragen.</span><span class="sxs-lookup"><span data-stu-id="ce171-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="ce171-165">Bij het registreren van LOB-apps voor één tenant kunnen geen gebruikers gedelegeerde machtigingen tooother apps vragen als deze machtigingen admin toestemming vereist.</span><span class="sxs-lookup"><span data-stu-id="ce171-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="ce171-166">Gebruikers maken geen wijzigingen tooapps dat ze geen eigenaren van zijn.</span><span class="sxs-lookup"><span data-stu-id="ce171-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="ce171-167">U bepaalt of gebruikers zelf vooraf geïntegreerde apps mogen toevoegen waarvoor eenmalige aanmelding met een wachtwoord wordt gebruikt ('password vaulting') ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="ce171-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="ce171-168">U bepaalt onder welke omstandigheden toepassingen kunnen worden geopend (voorwaardelijke toegang).</span><span class="sxs-lookup"><span data-stu-id="ce171-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="ce171-169">Let erop dat dit geldt voor zowel client-app toohello en toohello resource app.</span><span class="sxs-lookup"><span data-stu-id="ce171-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="ce171-170">Ja, dat u een beleid voor voorwaardelijke toegang met de tekst dat die Hallo 'Office 365 Exchange Online' app alleen toegankelijk vanaf computers die voldoen aan het beleid.</span><span class="sxs-lookup"><span data-stu-id="ce171-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="ce171-171">Dit beleid wordt ook starten wanneer een gebruiker probeert een client-app die Online machtigingen tooExchange vraagt toouse.</span><span class="sxs-lookup"><span data-stu-id="ce171-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="ce171-172">U hebt zichtbaarheid waarop apps zijn instemming tooand welke worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ce171-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="ce171-173">Wanneer een gebruiker hiermee akkoord tooan app gaat, wordt een ServicePrincipal-object gemaakt in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="ce171-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="ce171-174">Maken van het ServicePrincipal is opgenomen in het Hallo-controlerapport.</span><span class="sxs-lookup"><span data-stu-id="ce171-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="ce171-175">Gebruiker aanmelden activiteitsrapporten laat u weten welke app Hallo-gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="ce171-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="ce171-176">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ce171-176">Example</span></span>

<span data-ttu-id="ce171-177">Een voorbeeld: u gaat nu Hallo 'FabrikamMail voor Office 365' app, die u opgevallen dat gebruikers in uw tenant zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="ce171-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="ce171-178">FabrikamMail is een e-mail-app voor gebruik op Android-apparaten, gepubliceerd door Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="ce171-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="ce171-179">Hiermee worden onderverdeeld in Hallo ' multitenant apps andere ontwikkelen, Contoso met instemmen kunt '.</span><span class="sxs-lookup"><span data-stu-id="ce171-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="ce171-180">Als gebruikers tooconsent mogen, krijgen ze een toestemming vragen Hallo eerste keer dat ze zich aanmeldt:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="ce171-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="ce171-181">'Toegang tot uw postvakken' is hello gebruikersgerichte toestemming tekenreeks voor Hallo 'Postvakken toegang als de gebruiker is aangemeld Hallo' machtiging door 'Office 365 Exchange Online' (dat wil zeggen, Exchange) beschikbaar gesteld.</span><span class="sxs-lookup"><span data-stu-id="ce171-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="ce171-182">Hallo-machtigingen kunt u zien door het opzoeken van Hallo ServicePrincipal object voor Exchange (Hallo resource), dat is toegevoegd wanneer u zich registreerde voor Office 365.</span><span class="sxs-lookup"><span data-stu-id="ce171-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="ce171-183">U kunt zien van Hallo ServicePrincipal-object van een 'exemplaar' Hallo-App in uw tenant, die wordt gebruikt voor het vastleggen van verschillende opties en configuraties.</span><span class="sxs-lookup"><span data-stu-id="ce171-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="ce171-184">U kunt dit zien met behulp van Hallo `Get-AzureADServicePrincipal` in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce171-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

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
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
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

<span data-ttu-id="ce171-185">Toestemming wordt gestart wanneer 'Accepteren' Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce171-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="ce171-186">Eerst wordt een ServicePrincipal-object voor 'FabrikamMail voor Office 365' gemaakt in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="ce171-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="ce171-187">Hallo ServicePrincipal ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="ce171-187">hello ServicePrincipal looks something like this:</span></span>

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

<span data-ttu-id="ce171-188">Tooan app ermee akkoord dat een Oauth2PermissionGrant koppeling maakt tussen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ce171-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="ce171-189">Hallo-gebruikersobject</span><span class="sxs-lookup"><span data-stu-id="ce171-189">hello user object</span></span>
- <span data-ttu-id="ce171-190">Hallo van client-apps ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="ce171-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ce171-191">Hallo resource apps ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="ce171-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ce171-192">machtigingen in Hallo resource-app.</span><span class="sxs-lookup"><span data-stu-id="ce171-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="ce171-193">In geval van FabrikamMail Hallo ziet deze er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="ce171-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="ce171-194">(**ClientId** FabrikamMail van service principal-object-id (hello die u zojuist hebt gemaakt) **PrincipalId** Hallo gebruiker de object-ID (Hallo gebruiker die heeft ingestemd), is **ResourceId**is van de Exchange-service principal-object-ID, een bereik is Hallo toestemming in Exchange is wil).</span><span class="sxs-lookup"><span data-stu-id="ce171-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="ce171-195">Als gebruikers zijn niet toegestaan voor tooconsent, zien ze een scherm weergegeven dat dat de machtiging aangeeft is vereist.</span><span class="sxs-lookup"><span data-stu-id="ce171-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

