---
title: Het ophalen van AppSource gecertificeerd voor Azure Active Directory | Microsoft Docs
description: Meer informatie over het ophalen van uw toepassing AppSource gecertificeerd voor Azure Active Directory.
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="4adb4-103">Het ophalen van AppSource gecertificeerd voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4adb4-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="4adb4-104">[Microsoft AppSource](https://appsource.microsoft.com/) een doel voor zakelijke gebruikers om te detecteren, probeer en beheren van LOB-SaaS-toepassingen (zelfstandige SaaS en add-on voor bestaande Microsoft SaaS-producten).</span><span class="sxs-lookup"><span data-stu-id="4adb4-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="4adb4-105">Als een zelfstandige SaaS-toepassing op AppSource wilt weergeven, moet uw toepassing accepteren eenmalige aanmelding van werkaccounts van een bedrijf of organisatie die Azure Active Directory heeft.</span><span class="sxs-lookup"><span data-stu-id="4adb4-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="4adb4-106">Het proces voor aanmelden moet gebruiken de [OpenID Connect](./active-directory-protocols-openid-connect-code.md) of [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocollen.</span><span class="sxs-lookup"><span data-stu-id="4adb4-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="4adb4-107">SAML-integratie wordt niet geaccepteerd voor AppSource-certificering.</span><span class="sxs-lookup"><span data-stu-id="4adb4-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="4adb4-108">Handleidingen en codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="4adb4-108">Guides and code samples</span></span>
<span data-ttu-id="4adb4-109">Als u wilt weten over het integreren van uw toepassing met Azure Active Directory met Open ID verbinding, onze richtlijnen te volgen en codevoorbeelden in de [ontwikkelaarshandleiding Azure Active Directory](./active-directory-developers-guide.md#get-started "aan de slag met Azure AD voor ontwikkelaars").</span><span class="sxs-lookup"><span data-stu-id="4adb4-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="4adb4-110">Multitenant-toepassingen</span><span class="sxs-lookup"><span data-stu-id="4adb4-110">Multi-tenant applications</span></span>

<span data-ttu-id="4adb4-111">Een toepassing die aan de aanmeldingen van gebruikers van een bedrijf of organisatie die Azure Active Directory zijn zonder een afzonderlijk exemplaar, de configuratie of de implementatie accepteert wordt ook wel een *multitenant toepassing*.</span><span class="sxs-lookup"><span data-stu-id="4adb4-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="4adb4-112">AppSource raadt aan dat de multi-tenancymodus om in te schakelen voor het implementeren van toepassingen de *éénkliks-* gratis evaluatieversie.</span><span class="sxs-lookup"><span data-stu-id="4adb4-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="4adb4-113">Om in te schakelen multi-tenancymodus op uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="4adb4-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="4adb4-114">Ingesteld `Multi-Tenanted` eigenschap `Yes` van gegevens van uw toepassing registreren in de [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (toepassingen die zijn gemaakt in de Azure Portal zijn standaard geconfigureerd als *single-tenant*)</span><span class="sxs-lookup"><span data-stu-id="4adb4-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="4adb4-115">Werk uw code voor het verzenden van aanvragen voor de '`common`' eindpunt (bijwerken van het eindpunt van *https://login.microsoftonline.com/ {yourtenant}* naar *https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="4adb4-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="4adb4-116">Voor sommige platformen, zoals ASP.NET, moet u ook werk uw code voor het accepteren van meerdere uitgevers van certificaten</span><span class="sxs-lookup"><span data-stu-id="4adb4-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="4adb4-117">Zie voor meer informatie over multi-tenancymodus: [aanmelden met een Azure Active Directory (AD) gebruiker met behulp van het patroon toepassing met meerdere tenants](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4adb4-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="4adb4-118">Toepassingen voor één tenant</span><span class="sxs-lookup"><span data-stu-id="4adb4-118">Single-tenant applications</span></span>
<span data-ttu-id="4adb4-119">Toepassingen die alleen aanmeldingen van gebruikers van een gedefinieerde Azure Active Directory-exemplaar accepteren worden aangeduid als *toepassing voor één tenant*.</span><span class="sxs-lookup"><span data-stu-id="4adb4-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="4adb4-120">Externe gebruikers (inclusief werk of School accounts van andere organisaties of persoonlijk account) kunnen aanmelden bij een toepassing voor één tenant na het toevoegen van elke gebruiker als *gastaccount* met Azure Active Directory-instantie die de toepassing is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4adb4-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="4adb4-121">U kunt gebruikers als gastaccounts toevoegen aan een Azure Active Directory via de [ *Azure AD B2B-samenwerking* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - en kan worden gedaan [via programmacode](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4adb4-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="4adb4-122">Wanneer u een gebruiker als Gast-account aan een Azure Active Directory toevoegt, wordt een uitnodiging voor een e-mailbericht verzonden naar de gebruiker die de uitnodiging te accepteren door te klikken op de koppeling in de uitnodiging via e-mail.</span><span class="sxs-lookup"><span data-stu-id="4adb4-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="4adb4-123">Uitnodigingen die worden verzonden naar een extra gebruiker in een uitnodiging organisatie die deel uitmaakt van de partnerorganisatie zijn niet vereist voor het accepteren van een uitnodiging aan te melden.</span><span class="sxs-lookup"><span data-stu-id="4adb4-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="4adb4-124">Toepassingen voor één tenant kunnen inschakelen de *Contact met mij opnemen* ervaring, maar als u de éénkliks- / gratis proefabonnement ervaring die AppSource aanbeveelt inschakelen wilt, schakelt u multi-tenancymodus op uw toepassing in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="4adb4-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="4adb4-125">De evaluatieversie ervaringen AppSource</span><span class="sxs-lookup"><span data-stu-id="4adb4-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="4adb4-126">Gratis proefversie (klant geleid proefversie experience)</span><span class="sxs-lookup"><span data-stu-id="4adb4-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="4adb4-127">De *klant geleid proefversie* de ervaring die AppSource aanbeveelt zoals een één-op-toegang tot uw toepassing biedt is.</span><span class="sxs-lookup"><span data-stu-id="4adb4-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="4adb4-128">Hieronder een illustratie van hoe ziet deze ervaring:</span><span class="sxs-lookup"><span data-stu-id="4adb4-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="4adb4-129">Gebruiker uw toepassing worden gevonden in AppSource website</span><span class="sxs-lookup"><span data-stu-id="4adb4-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="4adb4-130">Optie 'Gratis proefversie' geselecteerd</span><span class="sxs-lookup"><span data-stu-id="4adb4-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="4adb4-131">AppSource wordt de gebruiker omgeleid naar een URL in uw website</span><span class="sxs-lookup"><span data-stu-id="4adb4-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="4adb4-132">De website wordt opgestart de <i>eenmalige aanmelding</i> processen automatisch (laden van de pagina)</span><span class="sxs-lookup"><span data-stu-id="4adb4-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="4adb4-133">Gebruiker wordt omgeleid naar de Microsoft-aanmeldingspagina</span><span class="sxs-lookup"><span data-stu-id="4adb4-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="4adb4-134">Gebruiker heeft referenties aan te melden</span><span class="sxs-lookup"><span data-stu-id="4adb4-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="4adb4-135">Gebruiker geeft toestemming voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="4adb4-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="4adb4-136">Aanmelden is voltooid en de gebruiker wordt omgeleid naar uw website</span><span class="sxs-lookup"><span data-stu-id="4adb4-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="4adb4-137">Gebruiker begint de gratis proefversie</span><span class="sxs-lookup"><span data-stu-id="4adb4-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="4adb4-138">Contact met Me (proefversie experience partners)</span><span class="sxs-lookup"><span data-stu-id="4adb4-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="4adb4-139">De *evaluatieversie partner* kan worden gebruikt wanneer een handmatige of een langdurige bewerking moet worden uitgevoerd voor het inrichten van de gebruiker / company: bijvoorbeeld uw toepassing nodig voor het inrichten van virtuele machines, database-exemplaren of bewerkingen die veel tijd in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="4adb4-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="4adb4-140">In dit geval nadat de gebruiker selecteert de *'Proefversie aanvragen'* knop en de opvulling van een formulier, AppSource verzendt u de contactgegevens van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4adb4-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="4adb4-141">Bij ontvangst van deze informatie vervolgens inrichten van de omgeving en de instructies verzenden naar de gebruiker over toegang krijgen tot de evaluatieversie:</span><span class="sxs-lookup"><span data-stu-id="4adb4-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="4adb4-142">Uw toepassing in de website AppSource gevonden met een gebruiker</span><span class="sxs-lookup"><span data-stu-id="4adb4-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="4adb4-143">De optie 'Contact Me' geselecteerd</span><span class="sxs-lookup"><span data-stu-id="4adb4-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="4adb4-144">Een formulier met contactgegevens invult</span><span class="sxs-lookup"><span data-stu-id="4adb4-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="4adb4-145">U ontvangt gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="4adb4-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="4adb4-146">Setup-omgeving</span><span class="sxs-lookup"><span data-stu-id="4adb4-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="4adb4-147">Neem contact op met gebruiker met de proefversie info</span><span class="sxs-lookup"><span data-stu-id="4adb4-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="4adb4-148">U ontvangt van de gebruiker informatie en proefversie exemplaar van setup</span><span class="sxs-lookup"><span data-stu-id="4adb4-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="4adb4-149">Verzenden van de hyperlink voor toegang tot uw toepassing aan de gebruiker</span><span class="sxs-lookup"><span data-stu-id="4adb4-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="4adb4-150">Gebruiker heeft toegang tot uw toepassing en het proces voor eenmalige aanmelding te voltooien</span><span class="sxs-lookup"><span data-stu-id="4adb4-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="4adb4-151">Gebruiker geeft toestemming voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="4adb4-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="4adb4-152">Aanmelden is voltooid en de gebruiker wordt omgeleid naar uw website</span><span class="sxs-lookup"><span data-stu-id="4adb4-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="4adb4-153">Gebruiker begint de gratis proefversie</span><span class="sxs-lookup"><span data-stu-id="4adb4-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="4adb4-154">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="4adb4-154">More information</span></span>
<span data-ttu-id="4adb4-155">Zie voor meer informatie over de evaluatieversie AppSource [in deze video](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="4adb4-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="4adb4-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4adb4-156">Next Steps</span></span>

- <span data-ttu-id="4adb4-157">Zie voor meer informatie over het bouwen van toepassingen die ondersteuning bieden voor Azure Active Directory aanmeldingen [verificatie scenario's voor Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="4adb4-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="4adb4-158">Ga voor informatie over hoe u uw SaaS-toepassing in AppSource, Zie [AppSource partnergegevens](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="4adb4-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="4adb4-159">Krijg ondersteuning</span><span class="sxs-lookup"><span data-stu-id="4adb4-159">Get Support</span></span>
<span data-ttu-id="4adb4-160">We gebruiken voor Azure Active Directory-integratie [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) met de community om ondersteuning te bieden.</span><span class="sxs-lookup"><span data-stu-id="4adb4-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="4adb4-161">We raden u eerst uw vragen stellen over stackoverloop en blader bestaande problemen om te zien of iemand anders uw vraag voordat heeft gesteld.</span><span class="sxs-lookup"><span data-stu-id="4adb4-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="4adb4-162">Zorg ervoor dat uw vragen of opmerkingen zijn gelabeld met `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="4adb4-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="4adb4-163">Gebruik de volgende sectie met opmerkingen uw feedback en help ons verfijnen en onze content vorm.</span><span class="sxs-lookup"><span data-stu-id="4adb4-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->