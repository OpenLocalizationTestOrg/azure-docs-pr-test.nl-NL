---
title: ontwikkelaarsaccounts aaaAuthorize met Azure Active Directory - Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooauthorize gebruikers met Azure Active Directory in API Management.
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="f7df3-103">Hoe tooauthorize developer gebruikersaccounts via Azure Active Directory in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f7df3-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f7df3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f7df3-104">Overview</span></span>
<span data-ttu-id="f7df3-105">Deze handleiding wordt getoond hoe tooenable toegang krijgen tot toohello developer-portal voor gebruikers van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f7df3-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="f7df3-106">Deze handleiding ziet u ook hoe toomanage groepen Azure Active Directory-gebruikers door het toevoegen van externe groepen met gebruikers van een Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7df3-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="f7df3-107">toocomplete hello stappen in deze handleiding u moet eerst een Azure Active Directory in welke toocreate een toepassing hebben.</span><span class="sxs-lookup"><span data-stu-id="f7df3-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="f7df3-108">Hoe tooauthorize developer gebruikersaccounts via Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7df3-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="f7df3-109">tooget gestart, klikt u op **publicatieportal** in hello Azure-portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="f7df3-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="f7df3-110">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="f7df3-110">This takes you toohello API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="f7df3-112">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f7df3-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="f7df3-113">Klik op **beveiliging** van Hallo **API Management** menu op Hallo linkerkant en klik op **externe identiteiten**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Externe identiteit][api-management-security-external-identities]

<span data-ttu-id="f7df3-115">Klik op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="f7df3-116">Maak een notitie van Hallo **Omleidings-URL** en tooyour Azure Active Directory in de klassieke Azure-Portal Hallo overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f7df3-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Externe identiteit][api-management-security-aad-new]

<span data-ttu-id="f7df3-118">Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory-toepassing, en kies **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nieuwe Azure Active Directory-toepassing toevoegen][api-management-new-aad-application-menu]

<span data-ttu-id="f7df3-120">Voer een naam voor toepassing hello, selecteert **Web-toepassing en/of Web-API**, en klik op de volgende knop Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7df3-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-1]

<span data-ttu-id="f7df3-122">Voor **aanmeldings-URL**, Voer Hallo aanmeldings-URL van uw ontwikkelaarsportal.</span><span class="sxs-lookup"><span data-stu-id="f7df3-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="f7df3-123">In dit voorbeeld Hallo **aanmeldings-URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="f7df3-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="f7df3-124">Voor Hallo **App-ID-URL**standaarddomein hello of een aangepast domein invoeren voor hello Azure Active Directory en een unieke tekenreeks tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f7df3-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="f7df3-125">In dit voorbeeld Hallo standaarddomein van **https://contoso5api.onmicrosoft.com** wordt gebruikt en het achtervoegsel Hallo **/api** opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f7df3-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Eigenschappen van nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-2]

<span data-ttu-id="f7df3-127">Klik op Hallo selectievakje knop toosave en toohello overschakelen Hallo-toepassing maken **configureren** tabblad tooconfigure Hallo nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7df3-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Nieuwe Azure Active Directory-toepassing gemaakt][api-management-new-aad-app-created]

<span data-ttu-id="f7df3-129">Als meerdere Azure Active Directory's toobe gebruikt voor deze toepassing gaat, klikt u op **Ja** voor **toepassing is multitenant**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="f7df3-130">Hallo standaardwaarde is **Nee**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-130">hello default is **No**.</span></span>

![Toepassing is multitenant][api-management-aad-app-multi-tenant]

<span data-ttu-id="f7df3-132">Kopiëren Hallo **Omleidings-URL** van Hallo **Azure Active Directory** sectie Hallo **externe identiteiten** tabblad in de publicatieportal hello en plak deze in Hallo **Antwoord-URL** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f7df3-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![Antwoord-URL][api-management-aad-reply-url]

<span data-ttu-id="f7df3-134">Scroll toohello onderaan Hallo configureren tabblad Selecteer Hallo **Toepassingsmachtigingen** vervolgkeuzelijst en Controleer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Toepassingsmachtigingen][api-management-aad-app-permissions]

<span data-ttu-id="f7df3-136">Selecteer Hallo **machtigingen delegeren** vervolgkeuzelijst en Controleer **aanmelding inschakelen en gebruikersprofiel lezen**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Gedelegeerde machtigingen][api-management-aad-delegated-permissions]

> <span data-ttu-id="f7df3-138">Zie voor meer informatie over de toepassing en gedelegeerde machtigingen, [toegang tot Hallo Graph API][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="f7df3-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="f7df3-139">Kopiëren Hallo **Client-Id** toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="f7df3-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Client-Id][api-management-aad-app-client-id]

<span data-ttu-id="f7df3-141">Overschakelen van de publicatieportal back toohello en plak in Hallo **Client-Id** gekopieerd van de configuratie van een hello Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7df3-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Client-Id][api-management-client-id]

<span data-ttu-id="f7df3-143">Switch back toohello Azure Active Directory-configuratie en klikt u op Hallo **Selecteer duur** vervolgkeuzelijst in Hallo **sleutels** sectie en geeft u een interval.</span><span class="sxs-lookup"><span data-stu-id="f7df3-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="f7df3-144">In dit voorbeeld **1 jaar** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f7df3-144">In this example, **1 year** is used.</span></span>

![Sleutel][api-management-aad-key-before-save]

<span data-ttu-id="f7df3-146">Klik op **opslaan** toosave Hallo configuratie- en Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="f7df3-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="f7df3-147">Hallo sleutel toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f7df3-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="f7df3-148">Noteer deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="f7df3-148">Make a note of this key.</span></span> <span data-ttu-id="f7df3-149">Wanneer u een venster hello Azure Active Directory-configuratie hebt gesloten, kan niet opnieuw Hallo sleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f7df3-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Sleutel][api-management-aad-key-after-save]

<span data-ttu-id="f7df3-151">Switch back toohello publisher-portal en plakken Hallo sleutel in Hallo **Clientgeheim** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f7df3-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Clientgeheim][api-management-client-secret]

<span data-ttu-id="f7df3-153">**Tenants toegestaan** geeft aan welke mappen zijn toegang toohello API's van Hallo API Management service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f7df3-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="f7df3-154">Geef de domeinen Hallo Hallo Azure Active Directory-exemplaren toowhich gewenste toogrant toegang.</span><span class="sxs-lookup"><span data-stu-id="f7df3-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="f7df3-155">U kunt meerdere domeinen scheiden met nieuwe regels, spaties of komma's.</span><span class="sxs-lookup"><span data-stu-id="f7df3-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Toegestane tenants][api-management-client-allowed-tenants]


<span data-ttu-id="f7df3-157">Zodra het Hallo gewenst configuratie is opgegeven, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Opslaan][api-management-client-allowed-tenants-save]

<span data-ttu-id="f7df3-159">Wanneer Hallo wijzigingen zijn opgeslagen, Hallo gebruikers in Hallo opgegeven Azure Active Directory toohello Developer-portal kunt aanmelden volgens de stappen Hallo in [toohello Developer-portal met een Azure Active Directory-account aanmelden] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="f7df3-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="f7df3-160">Meerdere domeinen kunnen worden opgegeven in Hallo **Tenants toegestaan** sectie.</span><span class="sxs-lookup"><span data-stu-id="f7df3-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="f7df3-161">Voordat een gebruiker zich vanaf een ander domein dan de oorspronkelijke Hallo-domein waar de toepassing hello is geregistreerd aanmelden kan, moet een globale beheerder van een ander domein Hallo machtigen Hallo toepassing tooaccess Active directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="f7df3-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="f7df3-162">toogrant machtiging Hallo globale beheerder moet te gaan`https://<URL of your developer portal>/aadadminconsent` (bijvoorbeeld https://contoso.portal.azure-api.net/aadadminconsent), typt u Hallo-domeinnaam van Active Directory-tenant die ze willen toogive toegang tooand Hallo klikt u op verzenden.</span><span class="sxs-lookup"><span data-stu-id="f7df3-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="f7df3-163">In de volgende Hallo bijvoorbeeld, een globale beheerder van `miaoaad.onmicrosoft.com` probeert toogive machtiging toothis bepaalde developer-portal.</span><span class="sxs-lookup"><span data-stu-id="f7df3-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Machtigingen][api-management-aad-consent]

<span data-ttu-id="f7df3-165">In het volgende scherm hello niet Hallo globale beheerder vraag tooconfirm Hallo toestemming geven.</span><span class="sxs-lookup"><span data-stu-id="f7df3-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Machtigingen][api-management-permissions-form]

> <span data-ttu-id="f7df3-167">Als een niet-globale beheerder probeert toolog in voordat u machtigingen worden verleend door een globale beheerder Hallo aanmeldingspoging mislukt en een fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f7df3-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="f7df3-168">Hoe tooadd een externe Azure Active Directory groeperen</span><span class="sxs-lookup"><span data-stu-id="f7df3-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="f7df3-169">Nadat de toegang voor gebruikers in een Azure Active Directory is ingeschakeld, kunt u toevoegen Azure Active Directory-groepen in API Management toomore eenvoudig hello koppeling van ontwikkelaars Hallo in Hallo groep met Hallo gewenst producten te beheren.</span><span class="sxs-lookup"><span data-stu-id="f7df3-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="f7df3-170">tooconfigure een externe Azure Active Directory-groep hello Azure Active Directory moet eerst worden geconfigureerd op Hallo identiteiten tabblad door Hallo-procedure in de vorige sectie hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7df3-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="f7df3-171">Externe Azure Active Directory-groepen worden toegevoegd vanuit Hallo **zichtbaarheid** tabblad van het Hallo-product waarvoor u wenst dat de toegangsgroep toohello toogrant.</span><span class="sxs-lookup"><span data-stu-id="f7df3-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="f7df3-172">Klik op **producten**, en klik vervolgens op Hallo-naam van de gewenste product Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7df3-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="f7df3-174">Overschakelen van toohello **zichtbaarheid** tabblad en klik op **groepen toevoegen van Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Groepen toevoegen][api-management-add-groups]

<span data-ttu-id="f7df3-176">Selecteer Hallo **Azure Active Directory-Tenant** uit de vervolgkeuzelijst Hallo en vervolgens Hallo-typenaam van de gewenste groep Hallo in Hallo **groepen** toobe toegevoegd in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f7df3-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Groep selecteren][api-management-select-group]

<span data-ttu-id="f7df3-178">De naam van deze groep kan worden gevonden in Hallo **groepen** lijst voor uw Azure Active Directory, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7df3-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Lijst van Azure Active Directory-groepen][api-management-aad-groups-list]

<span data-ttu-id="f7df3-180">Klik op **toevoegen** toovalidate Hallo groepsnaam en Hallo groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f7df3-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="f7df3-181">In dit voorbeeld Hallo **Contoso 5 ontwikkelaars** externe groep wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f7df3-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Groep toegevoegd][api-management-aad-group-added]

<span data-ttu-id="f7df3-183">Klik op **opslaan** toosave Hallo nieuwe groep selecteren.</span><span class="sxs-lookup"><span data-stu-id="f7df3-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="f7df3-184">Zodra een Azure Active Directory-groep van een product is geconfigureerd, is beschikbaar toobe gecontroleerd op Hallo **zichtbaarheid** tabblad voor andere producten in API Management service-exemplaar Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7df3-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="f7df3-185">tooreview en Hallo eigenschappen configureren voor externe groepen zodra ze zijn toegevoegd, klikt u op Hallo naam van groep van Hallo Hallo **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7df3-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Groepen beheren][api-management-groups]

<span data-ttu-id="f7df3-187">Hier kunt u Hallo **naam** en Hallo **beschrijving** van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="f7df3-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Groep bewerken][api-management-edit-group]

<span data-ttu-id="f7df3-189">Gebruikers van Hallo geconfigureerde Azure Active Directory kunnen aanmelden toohello Developer-portal en bekijk en zich abonneren tooany groepen waarvan ze inzicht door Hallo-instructies in de volgende sectie Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="f7df3-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="f7df3-190">Hoe toolog in toohello portal voor ontwikkelaars met een Azure Active Directory-account</span><span class="sxs-lookup"><span data-stu-id="f7df3-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="f7df3-191">toolog in Hallo Developer-portal met een Azure Active Directory-account geconfigureerd in de vorige secties Hallo, open een nieuw browservenster Hallo met **aanmeldings-URL** in configuratie van Active Directory-toepassing hello en klik op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portal voor ontwikkelaars][api-management-dev-portal-signin]

<span data-ttu-id="f7df3-193">Geef referenties op Hallo van een van Hallo gebruikers in uw Azure Active Directory en klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Aanmelden][api-management-aad-signin]

<span data-ttu-id="f7df3-195">U wordt mogelijk gevraagd met een registratieformulier als eventuele aanvullende informatie vereist is.</span><span class="sxs-lookup"><span data-stu-id="f7df3-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="f7df3-196">Hallo-registratieformulier voltooid en klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="f7df3-196">Complete hello registration form and click **Sign up**.</span></span>

![Registratie][api-management-complete-registration]

<span data-ttu-id="f7df3-198">De gebruiker is nu aangemeld bij Hallo developer-portal voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f7df3-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Inschrijving voltooid][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

