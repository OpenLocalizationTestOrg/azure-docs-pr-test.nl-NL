---
title: Ondertekening sleutelrollover in Azure AD | Microsoft Docs
description: Dit artikel wordt de ondertekening sleutelrollover best practices voor Azure Active Directory
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
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="d0bf5-103">Ondertekening sleutelrollover in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0bf5-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="d0bf5-104">In dit onderwerp wordt beschreven wat u moet weten over de openbare sleutels die worden gebruikt in Azure Active Directory (Azure AD) voor het ondertekenen van beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="d0bf5-105">Het is belangrijk te weten dat deze rollover voor sleutels op periodieke basis en, in een noodsituatie onmiddellijk kan worden overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="d0bf5-106">Alle toepassingen die gebruikmaken van Azure AD moeten kunnen programmatisch verwerken van het proces sleutelrollover of een overschakeling van de periodieke handmatige proces tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="d0bf5-107">Blijven lezen om te begrijpen hoe de sleutels werken, het beoordelen van de impact van de overschakeling van uw toepassing en het bijwerken van uw toepassing of tot stand brengen van een overschakeling van de periodieke handmatige proces voor het afhandelen van sleutelrollover indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="d0bf5-108">Overzicht van ondertekeningssleutels in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0bf5-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="d0bf5-109">Azure AD maakt gebruik van cryptografie met openbare sleutels gebaseerd op industriestandaarden vertrouwensrelatie tussen zichzelf en de toepassingen die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="d0bf5-110">In de praktijk dit werkt in de volgende manier: Azure AD maakt gebruik van een ondertekeningssleutel die uit een openbare en persoonlijke sleutelpaar bestaat.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="d0bf5-111">Wanneer een gebruiker zich bij een toepassing die gebruikmaakt van Azure AD voor verificatie aanmeldt, maakt Azure AD een beveiligingstoken dat informatie over de gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="d0bf5-112">Dit token is ondertekend door Azure AD met behulp van de persoonlijke sleutel voordat deze terug naar de toepassing wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="d0bf5-113">Om te verifiëren dat het token geldig en daadwerkelijk oorsprong van Azure AD is, moet de toepassing de handtekening van het token met de openbare sleutel die worden weergegeven door Azure AD dat is opgenomen in de tenant valideren [OpenID Connect discovery-document](http://openid.net/specs/openid-connect-discovery-1_0.html) of de WS-SAML-Fed [document met federatieve metagegevens](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="d0bf5-114">Om veiligheidsredenen kan sleutel rollen op periodieke basis en, in het geval van een noodgeval voor ondertekening van Azure AD worden vernieuwd onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="d0bf5-115">Alle toepassingen die kan worden geïntegreerd met Azure AD moet worden voorbereid voor het afhandelen van een gebeurtenis sleutelrollover ongeacht hoe vaak deze optreden.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="d0bf5-116">Als dit niet het geval, en uw toepassing probeert een verlopen sleutel gebruiken om te verifiëren van de handtekening van een token, mislukt de aanvraag aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="d0bf5-117">Er is altijd meer dan een geldige sleutel beschikbaar is in het discovery-document met OpenID Connect en het document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="d0bf5-118">Uw toepassing moet een van de sleutels die zijn opgegeven in het document, omdat één sleutel kan snel worden teruggedraaid, een ander kan worden de vervanging ervan, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="d0bf5-119">Hoe vast te stellen als uw toepassing worden beïnvloed en wat u moet doen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="d0bf5-120">Hoe uw toepassing sleutelrollover verwerkt, is afhankelijk van variabelen zoals het type van de toepassing of welke identiteit protocol en de bibliotheek is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="d0bf5-121">De volgende secties te beoordelen of de meest voorkomende typen toepassingen worden beïnvloed door de sleutelrollover en advies over het bijwerken van de toepassing geven voor de ondersteuning van automatische rollover of handmatig bijwerken van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="d0bf5-122">Systeemeigen clienttoepassingen toegang krijgen tot bronnen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="d0bf5-123">Webtoepassingen / API's toegang tot bronnen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="d0bf5-124">Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services</span><span class="sxs-lookup"><span data-stu-id="d0bf5-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="d0bf5-125">Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="d0bf5-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="d0bf5-126">Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="d0bf5-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="d0bf5-127">Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module</span><span class="sxs-lookup"><span data-stu-id="d0bf5-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="d0bf5-128">Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d0bf5-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="d0bf5-129">Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt</span><span class="sxs-lookup"><span data-stu-id="d0bf5-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="d0bf5-130">Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d0bf5-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="d0bf5-131">Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt</span><span class="sxs-lookup"><span data-stu-id="d0bf5-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="d0bf5-132">Webtoepassingen bescherming van bronnen en met Visual Studio 2010, 2008 o met behulp van Windows Identity Foundation gemaakt</span><span class="sxs-lookup"><span data-stu-id="d0bf5-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="d0bf5-133">Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van de ondersteunde protocollen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="d0bf5-134">Dit advies is **niet** van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="d0bf5-135">Toepassingen die zijn toegevoegd vanuit Azure AD-Toepassingsgalerie (met inbegrip van aangepaste) hebben afzonderlijke richtlijnen met betrekking tot het ondertekenen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="d0bf5-136">Meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="d0bf5-137">Een on-premises toepassingen die zijn gepubliceerd via toepassingsproxy hoeft over het ondertekenen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="d0bf5-138"><a name="nativeclient"></a>Systeemeigen clienttoepassingen toegang krijgen tot bronnen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="d0bf5-139">Toepassingen die alleen toegang bronnen (eenledige tot zijn</span><span class="sxs-lookup"><span data-stu-id="d0bf5-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="d0bf5-140">Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en deze doorgeven aan de resource-eigenaar.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="d0bf5-141">Gezien het feit dat ze niet alle resources beveiligt, worden ze doen het token niet controleren en hoeft dus niet om te controleren of dat deze correct is ondertekend.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="d0bf5-142">Native client-toepassingen, of desktop of mobile, vallen in deze categorie en worden dus niet beïnvloed door de overschakeling van de.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="d0bf5-143"><a name="webclient"></a>Webtoepassingen / API's toegang tot bronnen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="d0bf5-144">Toepassingen die alleen toegang bronnen (eenledige tot zijn</span><span class="sxs-lookup"><span data-stu-id="d0bf5-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="d0bf5-145">Microsoft Graph, KeyVault, API Outlook en andere Microsoft-APIs) in het algemeen alleen een token verkrijgen en deze doorgeven aan de resource-eigenaar.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="d0bf5-146">Gezien het feit dat ze niet alle resources beveiligt, worden ze doen het token niet controleren en hoeft dus niet om te controleren of dat deze correct is ondertekend.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="d0bf5-147">Webtoepassingen en -API's die van de app alleen-lezen stroom gebruikmaken (clientreferenties / clientcertificaat), vallen in deze categorie en worden dus niet beïnvloed door de overschakeling van de.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="d0bf5-148"><a name="appservices"></a>Webtoepassingen / API's voor het beveiligen van resources en gebouwd met behulp van Azure App Services</span><span class="sxs-lookup"><span data-stu-id="d0bf5-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="d0bf5-149">Azure App Services verificatie / autorisatie (EasyAuth)-functionaliteit is al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="d0bf5-150"><a name="owin"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="d0bf5-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="d0bf5-151">Als uw toepassing van de .NET OWIN OpenID Connect, WS-Fed of WindowsAzureActiveDirectoryBearerAuthentication middleware gebruikmaakt, is deze al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d0bf5-152">U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="d0bf5-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="d0bf5-153"><a name="owincore"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van .NET Core OpenID Connect of JwtBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="d0bf5-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="d0bf5-154">Als uw toepassing van de .NET Core OWIN OpenID Connect of JwtBearerAuthentication middleware gebruikmaakt, is deze al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d0bf5-155">U kunt bevestigen dat uw toepassing van een van deze gebruikmaakt door te zoeken naar een van de volgende codefragmenten in uw toepassing Startup.cs of Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="d0bf5-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="d0bf5-156"><a name="passport"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van Node.js passport-azure-ad-module</span><span class="sxs-lookup"><span data-stu-id="d0bf5-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="d0bf5-157">Als uw toepassing van de passport-ad-module voor Node.js gebruikmaakt, is deze al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="d0bf5-158">U kunt bevestigen dat uw toepassing passport-ad door te zoeken naar het volgende fragment in uw toepassing app.js</span><span class="sxs-lookup"><span data-stu-id="d0bf5-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="d0bf5-159"><a name="vs2015"></a>Webtoepassingen / API's voor het beveiligen van resources en gemaakt met Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d0bf5-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="d0bf5-160">Als uw toepassing is gemaakt met een sjabloon in Visual Studio 2015 of Visual Studio 2017 en u hebt geselecteerd **werk-en Schoolaccounts** van de **verificatie wijzigen** menu er al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="d0bf5-161">Deze logica, ingesloten in de middleware OWIN OpenID Connect opgehaald en de sleutels van het OpenID Connect discovery-document opslaat in de cache en ze worden regelmatig vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="d0bf5-162">Als u verificatie handmatig toegevoegd aan uw oplossing, hebben de toepassing mogelijk niet de benodigde sleutelrollover logica.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="d0bf5-163">U moet zelf schrijven of de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van de ondersteunde protocollen.](#other).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="d0bf5-164"><a name="vs2013"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2013 gemaakt</span><span class="sxs-lookup"><span data-stu-id="d0bf5-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="d0bf5-165">Als uw toepassing is gemaakt met behulp van een sjabloon in Visual Studio 2013 en u hebt geselecteerd **Organisatieaccounts** van de **verificatie wijzigen** menu heeft al de benodigde logica sleutelrollover automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="d0bf5-166">Deze logica slaat de unieke id van uw organisatie en de gegevens van de ondertekening sleutel in twee databasetabellen die zijn gekoppeld aan het project.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="d0bf5-167">U vindt de verbindingsreeks voor de database in het Web.config-bestand van het project.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="d0bf5-168">Als u verificatie handmatig toegevoegd aan uw oplossing, hebben de toepassing mogelijk niet de benodigde sleutelrollover logica.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="d0bf5-169">U moet zelf schrijven of de stappen in [webtoepassingen / API's met behulp van een andere bibliotheken of handmatig implementeren van de ondersteunde protocollen.](#other).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="d0bf5-170">De volgende stappen kunt u controleren of de logica goed in uw toepassing werkt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="d0bf5-171">Open de oplossing in Visual Studio 2013, en klik vervolgens op de **Server Explorer** tabblad op het rechtervenster.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="d0bf5-172">Vouw **gegevensverbindingen**, **DefaultConnection**, en vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="d0bf5-173">Zoek de **IssuingAuthorityKeys** tabel, met de rechtermuisknop en klik vervolgens op **tabelgegevens weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="d0bf5-174">In de **IssuingAuthorityKeys** tabel, gaan er ten minste een rij die overeenkomt met de vingerafdrukwaarde voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="d0bf5-175">Alle rijen in de tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="d0bf5-176">Met de rechtermuisknop op de **Tenants** tabel en klik vervolgens op **tabelgegevens weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="d0bf5-177">In de **Tenants** tabel, gaan er ten minste een rij die overeenkomt met een unieke map tenant-id.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="d0bf5-178">Alle rijen in de tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-178">Delete any rows in the table.</span></span> <span data-ttu-id="d0bf5-179">Als u de rijen in beide niet verwijdert de **Tenants** tabel en **IssuingAuthorityKeys** tabel, ontvangt u een fout opgetreden tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="d0bf5-180">Ontwikkel en voer de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-180">Build and run the application.</span></span> <span data-ttu-id="d0bf5-181">Nadat u zich hebt aangemeld bij uw account, kunt u de toepassing stoppen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="d0bf5-182">Ga terug naar de **Server Explorer** en bekijk de waarden in de **IssuingAuthorityKeys** en **Tenants** tabel.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="d0bf5-183">U zult zien dat ze hebben is automatisch opnieuw gevuld met de bijbehorende gegevens uit het document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="d0bf5-184"><a name="vs2013"></a>Web-API's voor het beveiligen van resources en gemaakt met Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d0bf5-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="d0bf5-185">Als u een web API-toepassing in Visual Studio 2013 met de Web-API-sjabloon hebt gemaakt en vervolgens geselecteerd **Organisatieaccounts** van de **verificatie wijzigen** menu u al is de benodigde de logica in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="d0bf5-186">Als u verificatie handmatig hebt geconfigureerd, volgt u de onderstaande instructies voor informatie over het configureren van uw Web-API voor het automatisch bijwerken van de belangrijke informatie.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="d0bf5-187">Het volgende codefragment laat zien hoe u de meest recente sleutels ophalen uit het document met federatieve metagegevens en gebruik vervolgens de [JWT-Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) valideren van het token.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="d0bf5-188">Het codefragment gaat ervan uit dat u uw eigen cachemechanisme voor persistent maken van de sleutel om toekomstige tokens van Azure AD te valideren ongeacht of deze in een database, configuratiebestand of elders.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
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

### <span data-ttu-id="d0bf5-189"><a name="vs2012"></a>Webtoepassingen bescherming van bronnen en met Visual Studio 2012 gemaakt</span><span class="sxs-lookup"><span data-stu-id="d0bf5-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="d0bf5-190">Als uw toepassing is gemaakt in Visual Studio 2012, u waarschijnlijk gebruikt de identiteit en toegang tot hulpprogramma voor het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="d0bf5-191">Het is ook mogelijk dat u gebruikmaakt van de [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="d0bf5-192">De VINR is verantwoordelijk voor het onderhouden van informatie over vertrouwde id-providers (Azure AD) en de sleutels die worden gebruikt om tokens die zijn uitgegeven door ze te valideren.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="d0bf5-193">De VINR ook kunt u gemakkelijk automatisch bijwerken van de belangrijkste informatie opgeslagen in een Web.config-bestand downloaden van de meest recente document met federatieve metagegevens die zijn gekoppeld aan uw directory, controleren of de configuratie bijgewerkt met de meest recente document is en bijwerken van de toepassing naar de nieuwe sleutel gebruiken als nodig.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="d0bf5-194">Als u uw toepassing met behulp van de codevoorbeelden of walkthrough documentatie van Microsoft hebt gemaakt, wordt de logica voor de overschakeling van de gegevensversleutelingssleutel is al opgenomen in uw project.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="d0bf5-195">U ziet dat de onderstaande code in uw project al bestaat.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="d0bf5-196">Als uw toepassing geen al deze logica heeft, de volgende stappen toe te voegen en te controleren of deze correct werkt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="d0bf5-197">In **Solution Explorer**, Voeg een verwijzing naar de **System.IdentityModel** assembly voor het juiste project.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="d0bf5-198">Open de **Global.asax.cs** -bestand en voeg het volgende toe met behulp van instructies:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="d0bf5-199">Voeg de volgende methode voor de **Global.asax.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="d0bf5-200">Aanroepen de **RefreshValidationSettings()** methode in de **Application_Start()** methode in **Global.asax.cs** zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="d0bf5-201">Zodra u deze stappen hebt uitgevoerd, wordt Web.config voor uw toepassing met de meest recente gegevens uit het document met federatieve metagegevens, met inbegrip van de meest recente sleutels worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="d0bf5-202">Deze update wordt uitgevoerd telkens wanneer de groep van toepassingen wordt gerecycled in IIS. IIS is standaard ingesteld op het recyclen van toepassingen om 29 uur.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="d0bf5-203">Volg de onderstaande stappen om te controleren of de logica sleutelrollover werkt.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="d0bf5-204">Nadat u hebt gecontroleerd dat uw toepassing van de bovenstaande code gebruikmaakt, opent u de **Web.config** bestands- en navigeer naar de  **<issuerNameRegistry>**  blok, speciaal op zoek naar de volgende paar regels:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="d0bf5-205">In de  **<add thumbprint=””>**  instelt, de vingerafdrukwaarde wijzigen door te willekeurig teken vervangen door een andere naam.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="d0bf5-206">Sla de **Web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="d0bf5-207">De toepassing bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-207">Build the application, and then run it.</span></span> <span data-ttu-id="d0bf5-208">Als u het proces aanmelden voltooien kunt, wordt uw toepassing de sleutel is bijgewerkt door de vereiste gegevens van uw directory document met federatieve metagegevens wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="d0bf5-209">Als u problemen met aanmelden ondervindt, controleert u de wijzigingen in uw toepassing correct zijn door te lezen de [toevoegen van aanmelding bij uw Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) onderwerp of downloaden en bekijken in het volgende voorbeeld: [ Multitenant Cloudtoepassing voor Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="d0bf5-210"><a name="vs2010"></a>Webtoepassingen bescherming van bronnen en zijn gemaakt met Visual Studio 2008 of 2010 en Windows Identity Foundation (WIF) v1.0 voor .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="d0bf5-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="d0bf5-211">Als u een toepassing op WIF v1.0 gebouwd, is er geen opgegeven mechanisme voor automatisch vernieuwen van de configuratie van uw toepassing om een nieuwe sleutel te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="d0bf5-212">*Eenvoudigst* gebruiken de FedUtil tooling opgenomen in de SDK WIF, die het meest recente metagegevensdocument ophalen en bijwerken van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="d0bf5-213">Uw toepassing bijwerken voor .NET 4.5, waaronder de nieuwste versie van WIF zich in de naamruimte System.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="d0bf5-214">U kunt de [valideren van certificaatverlener naam register (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) automatische updates van de configuratie van de toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="d0bf5-215">Voer een handmatige rollover volgens de instructies aan het einde van dit document richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="d0bf5-216">Instructies voor het gebruik van de FedUtil uw configuratie bij te werken:</span><span class="sxs-lookup"><span data-stu-id="d0bf5-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="d0bf5-217">Controleer of u de WIF v1.0 SDK is geïnstalleerd op uw ontwikkelcomputer voor Visual Studio 2008 of 2010.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="d0bf5-218">U kunt [downloaden vanaf hier](https://www.microsoft.com/en-us/download/details.aspx?id=4451) als u nog niet hebt geïnstalleerd het.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="d0bf5-219">Open de oplossing in Visual Studio, en met de rechtermuisknop op het betreffende project en selecteer **federatiemetagegevens bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="d0bf5-220">Als deze optie is niet beschikbaar, is FedUtil en/of de WIF v1.0 SDK niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="d0bf5-221">Selecteer in de prompt **Update** om te beginnen met het bijwerken van uw federatiemetagegevens.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="d0bf5-222">Als u toegang tot de server-omgeving waar de toepassing wordt gehost hebt, kunt u eventueel de FedUtil gebruiken [metagegevens van de automatische update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0bf5-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="d0bf5-223">Klik op **voltooien** om het bijwerkproces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="d0bf5-224"><a name="other"></a>Webtoepassingen / API's voor het beveiligen van resources met behulp van een andere bibliotheken of handmatig implementeren van de ondersteunde protocollen</span><span class="sxs-lookup"><span data-stu-id="d0bf5-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="d0bf5-225">Als u van een aantal andere bibliotheek gebruikmaakt of geïmplementeerd handmatig van de ondersteunde protocollen, hebt u nodig om te controleren van de bibliotheek of uw implementatie om ervoor te zorgen dat de sleutel van het OpenID Connect discovery-document of de federatiemetagegevens worden opgehaald document.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="d0bf5-226">Een manier om dit te controleren of is een zoekopdracht in uw code of code van de bibliotheek voor alle aanroepen van het OpenID discovery-document of het document met federatieve metagegevens doen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="d0bf5-227">Als deze sleutel is ergens wordt opgeslagen of vastgelegd in uw toepassing, u handmatig kunt de sleutel en het dienovereenkomstig door uitvoeren van een handmatige rollover volgens de instructies aan het einde van dit document richtlijnen update ophalen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="d0bf5-228">**Het wordt ten zeerste aangemoedigd verbeteren van uw toepassing ter ondersteuning van automatische rollover** met behulp van een van de omtrek benaderingen in dit artikel om te voorkomen dat toekomstige onderbrekingen en overhead als Azure AD de rollover uitgebracht verhoogt of een noodsituatie heeft overschakeling van de out-of-band.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="d0bf5-229">Het testen van uw toepassing om te bepalen of deze wordt beïnvloed</span><span class="sxs-lookup"><span data-stu-id="d0bf5-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="d0bf5-230">U kunt nagaan of uw toepassing automatische sleutelrollover ondersteunt door te downloaden van de scripts en volg de instructies in [deze GitHub-opslagplaats.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="d0bf5-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="d0bf5-231">Het uitvoeren van een handmatige rollover als u een toepassing biedt geen ondersteuning voor automatische rollover</span><span class="sxs-lookup"><span data-stu-id="d0bf5-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="d0bf5-232">Als uw toepassing wel **niet** automatische rollover ondersteunen, moet u een proces dat periodiek monitors Azure AD het ondertekenen van sleutels en voert een handmatige rollover dienovereenkomstig vast te stellen.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="d0bf5-233">[Deze GitHub-opslagplaats](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) bevat scripts en instructies over hoe u dit doet.</span><span class="sxs-lookup"><span data-stu-id="d0bf5-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

