---
title: aaaHow tooget AppSource gecertificeerd voor Azure Active Directory | Microsoft Docs
description: Informatie over hoe tooget uw toepassing AppSource gecertificeerd voor Azure Active Directory.
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
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="c4c7d-103">Hoe tooget AppSource gecertificeerd voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4c7d-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="c4c7d-104">[Microsoft AppSource](https://appsource.microsoft.com/) een doel voor zakelijke gebruikers toodiscover, probeer en beheren van LOB-SaaS-toepassingen (zelfstandige SaaS en invoegtoepassing tooexisting Microsoft SaaS-producten).</span><span class="sxs-lookup"><span data-stu-id="c4c7d-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="c4c7d-105">een zelfstandige SaaS-toepassing op AppSource toolist, uw toepassing moet accepteren eenmalige aanmelding van werkaccounts van een bedrijf of organisatie die Azure Active Directory heeft.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="c4c7d-106">Hallo-in proces moet hello gebruiken [OpenID Connect](./active-directory-protocols-openid-connect-code.md) of [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocollen.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="c4c7d-107">SAML-integratie wordt niet geaccepteerd voor AppSource-certificering.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="c4c7d-108">Handleidingen en codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="c4c7d-108">Guides and code samples</span></span>
<span data-ttu-id="c4c7d-109">Als u toolearn wilt over hoe toointegrate uw toepassing met Azure Active Directory met Open ID connect, volg onze handleidingen en codevoorbeelden in Hallo [ontwikkelaarshandleiding Azure Active Directory](./active-directory-developers-guide.md#get-started "aan de slag met Azure AD voor ontwikkelaars").</span><span class="sxs-lookup"><span data-stu-id="c4c7d-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="c4c7d-110">Multitenant-toepassingen</span><span class="sxs-lookup"><span data-stu-id="c4c7d-110">Multi-tenant applications</span></span>

<span data-ttu-id="c4c7d-111">Een toepassing die aan de aanmeldingen van gebruikers van een bedrijf of organisatie die Azure Active Directory zijn zonder een afzonderlijk exemplaar, de configuratie of de implementatie accepteert wordt ook wel een *multitenant toepassing*.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="c4c7d-112">AppSource raadt aan dat toepassingen multi-tenancymodus tooenable hello implementeren *éénkliks-* gratis evaluatieversie.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="c4c7d-113">In de volgorde tooenable multi-tenancymodus op uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="c4c7d-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="c4c7d-114">Ingesteld `Multi-Tenanted` eigenschap te`Yes` van gegevens van uw toepassing registreren in Hallo [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (toepassingen die zijn gemaakt in Azure Portal Hallo zijn standaard geconfigureerd als *single-tenant*)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="c4c7d-115">Werk uw code toosend aanvragen toohello '`common`' eindpunt (Hallo-eindpunt van bijgewerkt *https://login.microsoftonline.com/ {yourtenant}* te*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="c4c7d-116">Voor sommige platformen, zoals ASP.NET, moet u ook tooupdate uw code tooaccept meerdere uitgevers van certificaten</span><span class="sxs-lookup"><span data-stu-id="c4c7d-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="c4c7d-117">Zie voor meer informatie over multi-tenancymodus: [hoe toosign aan alle Azure Active Directory (AD) gebruiker met patroon multitenant toepassing hello](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4c7d-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="c4c7d-118">Toepassingen voor één tenant</span><span class="sxs-lookup"><span data-stu-id="c4c7d-118">Single-tenant applications</span></span>
<span data-ttu-id="c4c7d-119">Toepassingen die alleen aanmeldingen van gebruikers van een gedefinieerde Azure Active Directory-exemplaar accepteren worden aangeduid als *toepassing voor één tenant*.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="c4c7d-120">Externe gebruikers (inclusief werk of School accounts van andere organisaties of persoonlijk account) kunnen aanmelden tooa één tenant toepassing na het toevoegen van elke gebruiker als *gastaccount* toohello Azure Active Directory-exemplaar Hallo-toepassing is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="c4c7d-121">U kunt gebruikers toevoegen als Gast accounts tooan Azure Active Directory via Hallo [ *Azure AD B2B-samenwerking* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - en kan worden gedaan [via programmacode](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4c7d-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="c4c7d-122">Wanneer u een gebruiker als Gast-account tooan Azure Active Directory toevoegen, wordt een uitnodiging voor een e-mailbericht toohello voor gebruikers, tooaccept Hallo uitnodiging door te klikken op Hallo-koppeling in Hallo uitnodiging e-mail verzonden.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="c4c7d-123">Uitnodigingen die tooan extra gebruiker worden verzonden in een uitnodiging organisatie die ook lid zijn van de partnerorganisatie Hallo zijn niet vereist tooaccept een uitnodiging toosign in.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="c4c7d-124">Toepassingen voor één tenant kunnen inschakelen Hallo *Contact met mij opnemen* ervaring, maar als u wilt dat tooenable hello éénkliks- / gratis evaluatieversie die AppSource aanbeveelt, schakelt u multi-tenancymodus op uw toepassing in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="c4c7d-125">De evaluatieversie ervaringen AppSource</span><span class="sxs-lookup"><span data-stu-id="c4c7d-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="c4c7d-126">Gratis proefversie (klant geleid proefversie experience)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="c4c7d-127">Hallo *klant geleid proefversie* Hallo-ervaring die AppSource aanbeveelt zoals een enkele klik access tooyour-toepassing biedt is.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="c4c7d-128">Hieronder een illustratie van hoe ziet deze ervaring:</span><span class="sxs-lookup"><span data-stu-id="c4c7d-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-129">Gebruiker uw toepassing worden gevonden in AppSource website</span><span class="sxs-lookup"><span data-stu-id="c4c7d-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="c4c7d-130">Optie 'Gratis proefversie' geselecteerd</span><span class="sxs-lookup"><span data-stu-id="c4c7d-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="c4c7d-131">AppSource leidt de gebruiker tooa URL in uw website</span><span class="sxs-lookup"><span data-stu-id="c4c7d-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="c4c7d-132">Uw website begint Hallo <i>eenmalige aanmelding</i> processen automatisch (laden van de pagina)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-133">Gebruiker is omgeleid tooMicrosoft aanmelden pagina</span><span class="sxs-lookup"><span data-stu-id="c4c7d-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="c4c7d-134">Gebruiker heeft toosign referenties in</span><span class="sxs-lookup"><span data-stu-id="c4c7d-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-135">Gebruiker geeft toestemming voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="c4c7d-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-136">Aanmelden is voltooid en de gebruiker is omgeleid back tooyour website</span><span class="sxs-lookup"><span data-stu-id="c4c7d-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="c4c7d-137">Gebruiker begint Hallo gratis proefversie</span><span class="sxs-lookup"><span data-stu-id="c4c7d-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="c4c7d-138">Contact met Me (proefversie experience partners)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="c4c7d-139">Hallo *evaluatieversie partner* kan worden gebruikt wanneer een handmatige of een langdurige bewerking toohappen tooprovision Hallo gebruiker moet / company: bijvoorbeeld uw toepassing moet tooprovision virtuele machines, database-exemplaren of bewerkingen die veel toocomplete tijd duren.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="c4c7d-140">In dit geval nadat de gebruiker selecteert Hallo *'Proefversie aanvragen'* knop en het formulier invult, AppSource verzendt Hallo van contactgegevens van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="c4c7d-141">Bij ontvangst van deze informatie, u vervolgens inrichten Hallo-omgeving en Hallo instructies toohello gebruiker op hoe tooaccess evaluatieversie Hallo verzenden:</span><span class="sxs-lookup"><span data-stu-id="c4c7d-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-142">Uw toepassing in de website AppSource gevonden met een gebruiker</span><span class="sxs-lookup"><span data-stu-id="c4c7d-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="c4c7d-143">De optie 'Contact Me' geselecteerd</span><span class="sxs-lookup"><span data-stu-id="c4c7d-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-144">Een formulier met contactgegevens invult</span><span class="sxs-lookup"><span data-stu-id="c4c7d-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="c4c7d-145">U ontvangt gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="c4c7d-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="c4c7d-146">Setup-omgeving</span><span class="sxs-lookup"><span data-stu-id="c4c7d-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="c4c7d-147">Neem contact op met gebruiker met de proefversie info</span><span class="sxs-lookup"><span data-stu-id="c4c7d-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="c4c7d-148">U ontvangt van de gebruiker informatie en proefversie exemplaar van setup</span><span class="sxs-lookup"><span data-stu-id="c4c7d-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="c4c7d-149">U verzenden uw toepassing toohello gebruiker Hallo hyperlink tooaccess</span><span class="sxs-lookup"><span data-stu-id="c4c7d-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-150">Gebruiker toegang krijgt tot uw toepassing en de volledige Hallo-op-proces</span><span class="sxs-lookup"><span data-stu-id="c4c7d-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-151">Gebruiker geeft toestemming voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="c4c7d-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="c4c7d-152">Aanmelden is voltooid en de gebruiker is omgeleid back tooyour website</span><span class="sxs-lookup"><span data-stu-id="c4c7d-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="c4c7d-153">Gebruiker begint Hallo gratis proefversie</span><span class="sxs-lookup"><span data-stu-id="c4c7d-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="c4c7d-154">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="c4c7d-154">More information</span></span>
<span data-ttu-id="c4c7d-155">Zie voor meer informatie over de evaluatieversie van Hallo AppSource [in deze video](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="c4c7d-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="c4c7d-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4c7d-156">Next Steps</span></span>

- <span data-ttu-id="c4c7d-157">Zie voor meer informatie over het bouwen van toepassingen die ondersteuning bieden voor Azure Active Directory aanmeldingen [verificatie scenario's voor Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="c4c7d-158">Voor informatie over hoe toolist uw SaaS-toepassing in AppSource, gaat u Zie [AppSource partnergegevens](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="c4c7d-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="c4c7d-159">Krijg ondersteuning</span><span class="sxs-lookup"><span data-stu-id="c4c7d-159">Get Support</span></span>
<span data-ttu-id="c4c7d-160">We gebruiken voor Azure Active Directory-integratie [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) met Hallo tooprovide communityondersteuning.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="c4c7d-161">We raden u eerst uw vragen stellen over stackoverloop en bestaande problemen toosee Bladeren als iemand anders uw vraag voordat al heeft gesteld.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="c4c7d-162">Zorg ervoor dat uw vragen of opmerkingen zijn gelabeld met `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="c4c7d-163">Gebruik Hallo opmerkingen sectie tooprovide feedback te volgen en help ons verfijnen en onze content vorm.</span><span class="sxs-lookup"><span data-stu-id="c4c7d-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->