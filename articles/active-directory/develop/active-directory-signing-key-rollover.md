---
title: aaaSigning overschakeling van de sleutel in Azure AD | Microsoft Docs
description: Dit artikel wordt beschreven Hallo ondertekening sleutelrollover aanbevolen procedures voor Azure Active Directory
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="62747-103">Ondertekening sleutelrollover in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62747-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="62747-104">In dit onderwerp wordt beschreven wat u moet tooknow over Hallo openbare sleutels die worden gebruikt in Azure Active Directory (Azure AD) toosign beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="62747-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="62747-105">Het is belangrijk toonote die deze rollover voor sleutels op periodieke basis en, in geval van nood, kan worden vernieuwd onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="62747-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="62747-106">Alle toepassingen die gebruikmaken van Azure AD moeten kunnen tooprogrammatically ingang Hallo sleutelrollover proces of een overschakeling van de periodieke handmatige proces tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="62747-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="62747-107">Doorgaan toounderstand lezen hoe Hallo sleutels werkt, hoe tooassess gevolgen van het Hallo rollover tooyour toepassing hello en hoe tooupdate uw toepassing of een sleutelrollover van periodieke overschakeling van de handmatige proces toohandle maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="62747-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="62747-108">Overzicht van ondertekeningssleutels in Azure AD</span><span class="sxs-lookup"><span data-stu-id="62747-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="62747-109">Azure AD maakt gebruik van cryptografie van openbare sleutels is gebouwd op branche standaarden tooestablish vertrouwensrelatie tussen zichzelf en Hallo toepassingen die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62747-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="62747-110">In de praktijk dit werkt in de volgende manieren Hallo: Azure AD maakt gebruik van een ondertekeningssleutel die uit een openbare en persoonlijke sleutelpaar bestaat.</span><span class="sxs-lookup"><span data-stu-id="62747-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="62747-111">Wanneer een gebruiker zich aanmeldt tooan-toepassing die gebruikmaakt van Azure AD voor verificatie, wordt een beveiligingstoken dat informatie over Hallo gebruiker bevat gemaakt in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62747-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="62747-112">Dit token is ondertekend door Azure AD met behulp van de persoonlijke sleutel voordat deze terug toohello toepassing wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="62747-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="62747-113">tooverify die Hallo token geldig is en daadwerkelijk oorsprong van Azure AD, Hallo toepassing hello-token handtekening met de Hallo openbare sleutel die worden weergegeven door Azure AD dat is opgenomen in het Hallo-tenant moet valideren [discovery-document OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) of WS-SAML-Fed [document met federatieve metagegevens](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="62747-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="62747-114">Om veiligheidsredenen kan ondertekening sleutel rollen op periodieke basis en, in geval van nood, Hallo van Azure AD worden vernieuwd onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="62747-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="62747-115">Alle toepassingen die kan worden geïntegreerd met Azure AD moet worden voorbereid toohandle een sleutelrollover-gebeurtenis niet van belang hoe vaak het optreden.</span><span class="sxs-lookup"><span data-stu-id="62747-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="62747-116">Als dit niet het geval, en uw toepassing een verlopen sleutels tooverify Hallo handtekening op een token toouse probeert, mislukt Hallo aanmeldingsverzoek.</span><span class="sxs-lookup"><span data-stu-id="62747-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="62747-117">Er is altijd meer dan een geldige sleutel beschikbaar in het discovery-document met OpenID Connect Hallo en Hallo document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="62747-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="62747-118">Uw toepassing moet worden voorbereid toouse Hallo sleutels opgegeven in Hallo document, omdat één sleutel, wordt mogelijk teruggedraaid binnenkort een andere kan worden de vervanging ervan, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="62747-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="62747-119">Hoe tooassess als uw toepassing worden beïnvloed en welke toodo erover</span><span class="sxs-lookup"><span data-stu-id="62747-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="62747-120">Hoe uw toepassing sleutelrollover verwerkt, is afhankelijk van variabelen zoals Hallo-type van de toepassing of welke identiteit protocol en de bibliotheek is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62747-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="62747-121">de volgende secties voor Hallo te beoordelen of Hallo meest voorkomende typen toepassingen worden beïnvloed door Hallo sleutelrollover en advies geven over de wijze waarop tooupdate toepassing toosupport automatische rollover Hallo Hallo sleutel handmatig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="62747-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="62747-122">Systeemeigen clienttoepassingen toegang krijgen tot bronnen</span><span class="sxs-lookup"><span data-stu-id="62747-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="62747-123">Webtoepassingen / API's toegang tot bronnen</span><span class="sxs-lookup"><span data-stu-id="62747-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="62747-124">Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services</span><span class="sxs-lookup"><span data-stu-id="62747-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="62747-125">Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="62747-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="62747-126">Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="62747-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="62747-127">Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module</span><span class="sxs-lookup"><span data-stu-id="62747-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="62747-128">Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="62747-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="62747-129">Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt</span><span class="sxs-lookup"><span data-stu-id="62747-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="62747-130">Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="62747-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="62747-131">Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt</span><span class="sxs-lookup"><span data-stu-id="62747-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="62747-132">Webtoepassingen bescherming van bronnen en met Visual Studio 2010, 2008 o met behulp van Windows Identity Foundation gemaakt</span><span class="sxs-lookup"><span data-stu-id="62747-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="62747-133">Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteund protocollen</span><span class="sxs-lookup"><span data-stu-id="62747-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="62747-134">Dit advies is **niet** van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="62747-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="62747-135">Toepassingen die zijn toegevoegd vanuit Azure AD-Toepassingsgalerie (met inbegrip van aangepaste) hebben afzonderlijke richtlijnen met betrekking toosigning sleutels.</span><span class="sxs-lookup"><span data-stu-id="62747-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="62747-136">Meer informatie.</span><span class="sxs-lookup"><span data-stu-id="62747-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="62747-137">Een on-premises toepassingen die zijn gepubliceerd via toepassingsproxy tooworry over het ondertekenen van sleutels niet hebt.</span><span class="sxs-lookup"><span data-stu-id="62747-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="62747-138"><a name="nativeclient"></a>Systeemeigen clienttoepassingen toegang krijgen tot bronnen</span><span class="sxs-lookup"><span data-stu-id="62747-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="62747-139">Toepassingen die alleen toegang bronnen (eenledige tot zijn</span><span class="sxs-lookup"><span data-stu-id="62747-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="62747-140">Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en het resource-eigenaar toohello doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="62747-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="62747-141">Gezien het feit dat ze niet alle bronnen beveiligen, ze doen Hallo token niet controleren en hoeven dus geen tooensure die goed zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="62747-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="62747-142">Native client-toepassingen, of desktop of mobile, vallen in deze categorie en worden dus niet van invloed op Hallo rollover.</span><span class="sxs-lookup"><span data-stu-id="62747-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="62747-143"><a name="webclient"></a>Webtoepassingen / API's toegang tot bronnen</span><span class="sxs-lookup"><span data-stu-id="62747-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="62747-144">Toepassingen die alleen toegang bronnen (eenledige tot zijn</span><span class="sxs-lookup"><span data-stu-id="62747-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="62747-145">Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en het resource-eigenaar toohello doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="62747-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="62747-146">Gezien het feit dat ze niet alle bronnen beveiligen, ze doen Hallo token niet controleren en hoeven dus geen tooensure die goed zijn ondertekend.</span><span class="sxs-lookup"><span data-stu-id="62747-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="62747-147">Webtoepassingen en -API's die van de app alleen-lezen stroom hello gebruikmaken (clientreferenties / clientcertificaat), vallen in deze categorie en worden dus niet van invloed op Hallo rollover.</span><span class="sxs-lookup"><span data-stu-id="62747-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="62747-148"><a name="appservices"></a>Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services</span><span class="sxs-lookup"><span data-stu-id="62747-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="62747-149">Azure App Services verificatie / autorisatie (EasyAuth)-functionaliteit is al Hallo benodigde logica toohandle sleutelrollover automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="62747-150"><a name="owin"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="62747-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="62747-151">Als uw toepassing van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication-middleware Hallo gebruikmaakt al er Hallo benodigde logica toohandle sleutelrollover automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="62747-152">U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs Hallo</span><span class="sxs-lookup"><span data-stu-id="62747-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="62747-153"><a name="owincore"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="62747-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="62747-154">Als uw toepassing van .NET Core OWIN OpenID Connect Hallo of JwtBearerAuthentication middleware gebruikmaakt, al er Hallo benodigde logica toohandle sleutelrollover automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="62747-155">U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs Hallo</span><span class="sxs-lookup"><span data-stu-id="62747-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="62747-156"><a name="passport"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module</span><span class="sxs-lookup"><span data-stu-id="62747-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="62747-157">Als uw toepassing hello Node.js passport-ad-module gebruikt, deze is al Hallo benodigde logica toohandle sleutelrollover automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="62747-158">U kunt bevestigen dat uw toepassing passport-ad door te zoeken naar het volgende codefragment in uw toepassing app.js Hallo</span><span class="sxs-lookup"><span data-stu-id="62747-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="62747-159"><a name="vs2015"></a>Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="62747-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="62747-160">Als uw toepassing is gemaakt met een sjabloon in Visual Studio 2015 of Visual Studio 2017 en u hebt geselecteerd **werk-en Schoolaccounts** van Hallo **verificatie wijzigen** menu al Hallo benodigde logica toohandle sleutelrollover heeft automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="62747-161">Deze logica, ingesloten in Hallo OWIN OpenID Connect middleware opgehaald en in de cache opgeslagen Hallo sleutels van de discovery-document met OpenID Connect Hallo en ze worden regelmatig vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="62747-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="62747-162">Als u de oplossing tooyour verificatie handmatig hebt toegevoegd, is uw toepassing wellicht niet Hallo rollover van de benodigde logica.</span><span class="sxs-lookup"><span data-stu-id="62747-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="62747-163">U moet toowrite het uzelf of Hallo Volg de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteunde protocollen.](#other).</span><span class="sxs-lookup"><span data-stu-id="62747-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="62747-164"><a name="vs2013"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt</span><span class="sxs-lookup"><span data-stu-id="62747-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="62747-165">Als uw toepassing is gemaakt met behulp van een sjabloon in Visual Studio 2013 en u hebt geselecteerd **Organisatieaccounts** van Hallo **verificatie wijzigen** menu heeft al Hallo nodig logica toohandle key rollover automatisch.</span><span class="sxs-lookup"><span data-stu-id="62747-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="62747-166">Deze logica slaat de unieke id van uw organisatie en Hallo ondertekening sleutelgegevens in twee databasetabellen die zijn gekoppeld aan het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="62747-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="62747-167">U vindt Hallo-verbindingsreeks voor Hallo-database in het Web.config-bestand van het project Hallo.</span><span class="sxs-lookup"><span data-stu-id="62747-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="62747-168">Als u de oplossing tooyour verificatie handmatig hebt toegevoegd, is uw toepassing wellicht niet Hallo rollover van de benodigde logica.</span><span class="sxs-lookup"><span data-stu-id="62747-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="62747-169">U moet toowrite het uzelf of Hallo Volg de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteunde protocollen.](#other).</span><span class="sxs-lookup"><span data-stu-id="62747-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="62747-170">Hallo stappen volgen helpt u of Hallo logica juist werkt in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="62747-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="62747-171">Open Hallo oplossing in Visual Studio 2013, en klik vervolgens op Hallo **Server Explorer** tabblad op Hallo rechtervenster.</span><span class="sxs-lookup"><span data-stu-id="62747-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="62747-172">Vouw **gegevensverbindingen**, **DefaultConnection**, en vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="62747-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="62747-173">Zoek Hallo **IssuingAuthorityKeys** tabel, met de rechtermuisknop en klik vervolgens op **tabelgegevens weergeven**.</span><span class="sxs-lookup"><span data-stu-id="62747-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="62747-174">In Hallo **IssuingAuthorityKeys** tabel, gaan er ten minste een rij die overeenkomt met de vingerafdrukwaarde toohello voor Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="62747-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="62747-175">Alle rijen in Hallo tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="62747-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="62747-176">Klik met de rechtermuisknop Hallo **Tenants** tabel en klik vervolgens op **tabelgegevens weergeven**.</span><span class="sxs-lookup"><span data-stu-id="62747-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="62747-177">In Hallo **Tenants** tabel, gaan er ten minste een rij die overeenkomt met tooa unieke directory-tenant-id.</span><span class="sxs-lookup"><span data-stu-id="62747-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="62747-178">Alle rijen in Hallo tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="62747-178">Delete any rows in hello table.</span></span> <span data-ttu-id="62747-179">Als u niet Hallo rijen in beide Hallo verwijdert **Tenants** tabel en **IssuingAuthorityKeys** tabel, ontvangt u een fout opgetreden tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="62747-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="62747-180">Toepassing bouwen en uitvoeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="62747-180">Build and run hello application.</span></span> <span data-ttu-id="62747-181">Nadat u zich hebt aangemeld in tooyour-account, kunt u de toepassing hello stoppen.</span><span class="sxs-lookup"><span data-stu-id="62747-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="62747-182">Retourneren van toohello **Server Explorer** en bekijkt hello waarden in Hallo **IssuingAuthorityKeys** en **Tenants** tabel.</span><span class="sxs-lookup"><span data-stu-id="62747-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="62747-183">U zult zien dat ze hebben is automatisch opnieuw gevuld met de juiste informatie Hallo van Hallo document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="62747-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="62747-184"><a name="vs2013"></a>Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="62747-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="62747-185">Als u een web API-toepassing in Visual Studio 2013 met Hallo Web API-sjabloon hebt gemaakt en vervolgens geselecteerd **Organisatieaccounts** van Hallo **verificatie wijzigen** menu u al hebt Hallo benodigde logica in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="62747-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="62747-186">Als u verificatie handmatig hebt geconfigureerd, volgt u onderstaande toolearn Hallo instructies hoe tooconfigure uw Web-API-tooautomatically bijwerken van de belangrijke informatie.</span><span class="sxs-lookup"><span data-stu-id="62747-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="62747-187">Hallo volgende codefragment wordt gedemonstreerd hoe tooget Hallo nieuwste sleutels van het document met federatieve metagegevens hello, en gebruik vervolgens Hallo [JWT-Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="62747-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="62747-188">Hallo-codefragment wordt ervan uitgegaan dat u uw eigen mechanisme voor het persistent maken Hallo sleutel toovalidate toekomstige caching tokens van Azure AD gebruikt ongeacht of deze in een database, configuratiebestand of elders.</span><span class="sxs-lookup"><span data-stu-id="62747-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="62747-189"><a name="vs2012"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt</span><span class="sxs-lookup"><span data-stu-id="62747-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="62747-190">Als uw toepassing is gemaakt in Visual Studio 2012, u waarschijnlijk gebruikt Hallo identiteit en toegang tot hulpprogramma tooconfigure uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="62747-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="62747-191">Ook is het waarschijnlijk dat u van Hallo gebruikmaakt [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="62747-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="62747-192">Hallo VINR is verantwoordelijk voor het onderhouden van informatie over vertrouwde id-providers (Azure AD) en Hallo sleutels toovalidate tokens die zijn uitgegeven door ze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62747-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="62747-193">Hallo VINR maakt het ook eenvoudig tooautomatically update Hallo belangrijke informatie opgeslagen in een Web.config-bestand downloaden Hallo nieuwste document met federatieve metagegevens die zijn gekoppeld aan uw directory, als Hallo-configuratie verouderd Hello laatste is controleren document en bijwerken Hallo toouse Hallo nieuwe Toepassingssleutel indien nodig.</span><span class="sxs-lookup"><span data-stu-id="62747-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="62747-194">Als u uw toepassing met behulp van een Hallo-codevoorbeelden of walkthrough documentatie van Microsoft hebt gemaakt, wordt Hallo sleutelrollover logica is al opgenomen in uw project.</span><span class="sxs-lookup"><span data-stu-id="62747-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="62747-195">U ziet dat Hallo onderstaande code in uw project al bestaat.</span><span class="sxs-lookup"><span data-stu-id="62747-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="62747-196">Als uw toepassing geen al deze logica heeft, stappen Hallo hieronder tooadd en tooverify die correct werkt.</span><span class="sxs-lookup"><span data-stu-id="62747-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="62747-197">In **Solution Explorer**, Voeg een verwijzing toohello **System.IdentityModel** assembly voor de juiste Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="62747-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="62747-198">Open Hallo **Global.asax.cs** -bestand en voeg de volgende Hallo met behulp van instructies:</span><span class="sxs-lookup"><span data-stu-id="62747-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="62747-199">Hallo na methode toohello toevoegen **Global.asax.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="62747-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="62747-200">Hallo aanroepen **RefreshValidationSettings()** methode in Hallo **Application_Start()** methode in **Global.asax.cs** zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="62747-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="62747-201">Zodra u deze stappen hebt uitgevoerd, wordt Web.config van uw toepassing worden bijgewerkt met de meest recente gegevens Hallo van Hallo document met federatieve metagegevens, met inbegrip van de meest recente sleutels Hallo.</span><span class="sxs-lookup"><span data-stu-id="62747-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="62747-202">Deze update wordt uitgevoerd telkens wanneer de groep van toepassingen wordt gerecycled in IIS. IIS is standaard ingesteld toorecycle toepassingen om 29 uur.</span><span class="sxs-lookup"><span data-stu-id="62747-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="62747-203">Hallo stappen hieronder tooverify hello sleutelrollover logica werkt.</span><span class="sxs-lookup"><span data-stu-id="62747-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="62747-204">Nadat u hebt gecontroleerd dat uw toepassing van Hallo code hierboven, open Hallo gebruikmaakt **Web.config** bestands- en navigeer toohello  **<issuerNameRegistry>**  blok, zoekt specifiek Hallo paar regels te volgen:</span><span class="sxs-lookup"><span data-stu-id="62747-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="62747-205">In Hallo  **<add thumbprint=””>**  instelling Hallo vingerafdrukwaarde wijzigen door willekeurig teken vervangen door een andere naam.</span><span class="sxs-lookup"><span data-stu-id="62747-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="62747-206">Hallo opslaan **Web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="62747-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="62747-207">Hallo-toepassing bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="62747-207">Build hello application, and then run it.</span></span> <span data-ttu-id="62747-208">Als u Hallo aanmelden proces voltooien kunt, wordt uw toepassing hello sleutel is bijgewerkt door Hallo vereist informatie te downloaden via document met federatieve metagegevens van uw directory.</span><span class="sxs-lookup"><span data-stu-id="62747-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="62747-209">Als u problemen met aanmelden ondervindt, zorg er dan Hallo wijzigingen in uw toepassing correct zijn door te lezen Hallo [toe te voegen aanmelding tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) onderwerp of bij het downloaden en Hallo volgende codevoorbeeld te bekijken: [ Multitenant Cloudtoepassing voor Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="62747-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="62747-210"><a name="vs2010"></a>Webtoepassingen bescherming van bronnen en zijn gemaakt met Visual Studio 2008 of 2010 en Windows Identity Foundation (WIF) v1.0 voor .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="62747-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="62747-211">Als u een toepassing op WIF v1.0 gebouwd, is er geen tooautomatically opgegeven mechanisme vernieuwing toouse van de configuratie van uw toepassing een nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="62747-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="62747-212">*Eenvoudigst* hello FedUtil tooling opgenomen in Hallo WIF SDK, die de meest recente metagegevensdocument Hallo ophalen en bijwerken van uw configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="62747-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="62747-213">Uw toepassing too.NET 4.5, waaronder de nieuwste versie van WIF zich in de naamruimte System Hallo Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="62747-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="62747-214">Vervolgens kunt u Hallo [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatische updates van de configuratie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="62747-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="62747-215">Voer een handmatige rollover volgens de instructies Hallo aan Hallo einde van dit document richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="62747-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="62747-216">Instructies toouse Hallo FedUtil tooupdate uw configuratie:</span><span class="sxs-lookup"><span data-stu-id="62747-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="62747-217">Controleer of u Hallo WIF v1.0 SDK is geïnstalleerd op uw ontwikkelcomputer voor Visual Studio 2008 of 2010.</span><span class="sxs-lookup"><span data-stu-id="62747-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="62747-218">U kunt [downloaden vanaf hier](https://www.microsoft.com/en-us/download/details.aspx?id=4451) als u nog niet hebt geïnstalleerd het.</span><span class="sxs-lookup"><span data-stu-id="62747-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="62747-219">Open in Visual Studio Hallo-oplossing, klik met de rechtermuisknop op Hallo van toepassing project en selecteer **federatiemetagegevens bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="62747-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="62747-220">Als deze optie niet beschikbaar is, is FedUtil en/of Hallo WIF v1.0 SDK niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="62747-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="62747-221">Selecteer in het Hallo-prompt **Update** toobegin bijwerken van uw federatiemetagegevens.</span><span class="sxs-lookup"><span data-stu-id="62747-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="62747-222">Als u toegang toohello server-omgeving waar de toepassing hello wordt gehost hebt, kunt u eventueel gebruiken van FedUtil [metagegevens van de automatische update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="62747-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="62747-223">Klik op **voltooien** toocomplete Hallo updateproces.</span><span class="sxs-lookup"><span data-stu-id="62747-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="62747-224"><a name="other"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van Hallo ondersteund protocollen</span><span class="sxs-lookup"><span data-stu-id="62747-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="62747-225">Als u van een aantal andere bibliotheek gebruikmaakt of geïmplementeerd handmatig van de protocollen Hallo ondersteund, moet u tooreview Hallo-bibliotheek of uw implementatie tooensure die sleutel Hallo is opgehaald van de discovery-document met OpenID Connect Hallo of Hallo document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="62747-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="62747-226">Eenzijdige toocheck voor dit is een zoekopdracht in uw code of code Hallo-bibliotheek voor alle aanroepen tooeither hello OpenID discovery-document of een document met federatieve metagegevens Hallo toodo.</span><span class="sxs-lookup"><span data-stu-id="62747-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="62747-227">Als deze sleutel is ergens wordt opgeslagen of vastgelegd in uw toepassing, u handmatig kunt ophalen Hallo sleutel en het dienovereenkomstig door uitvoeren van een handmatige rollover volgens de instructies aan einde van dit document richtlijnen Hallo Hallo-update.</span><span class="sxs-lookup"><span data-stu-id="62747-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="62747-228">**Het wordt ten zeerste aangemoedigd verbeteren van uw toepassing toosupport automatische rollover** met behulp van een Hallo nadert overzicht in dit artikel tooavoid toekomstige onderbrekingen en overhead als Azure AD de rollover uitgebracht verhoogt of heeft een de overschakeling van de out-of-band noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="62747-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="62747-229">Hoe tootest uw toepassing toodetermine als deze worden beïnvloed</span><span class="sxs-lookup"><span data-stu-id="62747-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="62747-230">U kunt nagaan of uw toepassing automatische sleutelrollover ondersteunt door het Hallo-scripts downloaden en instructies te volgen Hallo in [deze GitHub-opslagplaats.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="62747-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="62747-231">Hoe tooperform een handmatige rollover als u een toepassing biedt geen ondersteuning voor automatische rollover</span><span class="sxs-lookup"><span data-stu-id="62747-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="62747-232">Als uw toepassing wel **niet** automatische rollover ondersteunen, moet u tooestablish een proces dat periodiek monitors Azure AD het ondertekenen van sleutels en voert een handmatige rollover dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="62747-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="62747-233">[Deze GitHub-opslagplaats](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) bevat scripts en instructies voor het toodo dit.</span><span class="sxs-lookup"><span data-stu-id="62747-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

