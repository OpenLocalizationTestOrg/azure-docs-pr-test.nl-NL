---
title: Autoriseren ontwikkelaarsaccounts met Azure Active Directory - Azure API Management | Microsoft Docs
description: Informatie over het autoriseren van gebruikers met Azure Active Directory in API Management.
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
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="013e9-103">Hoe ontwikkelaarsaccounts in Azure API Management met behulp van Azure Active Directory autoriseren</span><span class="sxs-lookup"><span data-stu-id="013e9-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="013e9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="013e9-104">Overview</span></span>
<span data-ttu-id="013e9-105">Deze handleiding wordt beschreven hoe u toegang inschakelen voor de portal voor ontwikkelaars voor gebruikers van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="013e9-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="013e9-106">Deze handleiding ook wordt beschreven hoe u groepen met Azure Active Directory-gebruikers beheren door externe groepen de gebruikers van een Azure Active Directory bevatten toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="013e9-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="013e9-107">U moet een Azure Active Directory in te maken van een toepassing hebben voor het voltooien van de stappen in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="013e9-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="013e9-108">Hoe ontwikkelaarsaccounts met Azure Active Directory autoriseren</span><span class="sxs-lookup"><span data-stu-id="013e9-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="013e9-109">Om te beginnen, klikt u op **publicatieportal** in de Azure portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="013e9-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="013e9-110">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="013e9-110">This takes you to the API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="013e9-112">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="013e9-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="013e9-113">Klik op **beveiliging** van de **API Management** menu aan de linkerkant en klik op **externe identiteiten**.</span><span class="sxs-lookup"><span data-stu-id="013e9-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![Externe identiteit][api-management-security-external-identities]

<span data-ttu-id="013e9-115">Klik op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="013e9-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="013e9-116">Noteer de **Omleidings-URL** en schakel naar uw Azure Active Directory in de klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="013e9-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![Externe identiteit][api-management-security-aad-new]

<span data-ttu-id="013e9-118">Klik op de **toevoegen** klikken om een nieuwe Azure Active Directory-toepassing maken en kies **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="013e9-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nieuwe Azure Active Directory-toepassing toevoegen][api-management-new-aad-application-menu]

<span data-ttu-id="013e9-120">Voer een naam voor de toepassing, selecteer **Web-toepassing en/of Web-API**, en klik op de knop Volgende.</span><span class="sxs-lookup"><span data-stu-id="013e9-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-1]

<span data-ttu-id="013e9-122">Voor **aanmeldings-URL**, voer de aanmeldings-URL van uw ontwikkelaarsportal.</span><span class="sxs-lookup"><span data-stu-id="013e9-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="013e9-123">In dit voorbeeld wordt de **aanmeldings-URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="013e9-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="013e9-124">Voor de **App-ID-URL**, voer het standaarddomein of een aangepast domein voor de Azure Active Directory en een unieke tekenreeks toegevoegd aan.</span><span class="sxs-lookup"><span data-stu-id="013e9-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="013e9-125">In dit voorbeeld wordt het standaarddomein van **https://contoso5api.onmicrosoft.com** wordt gebruikt met het achtervoegsel van **/api** opgegeven.</span><span class="sxs-lookup"><span data-stu-id="013e9-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Eigenschappen van nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-2]

<span data-ttu-id="013e9-127">Klik op de knop met het vinkje om op te slaan en de toepassing maken overschakelen naar de **configureren** tabblad configureren van de nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="013e9-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Nieuwe Azure Active Directory-toepassing gemaakt][api-management-new-aad-app-created]

<span data-ttu-id="013e9-129">Als meerdere Azure Active Directory's worden gebruikt voor deze toepassing gaat, klikt u op **Ja** voor **toepassing is multitenant**.</span><span class="sxs-lookup"><span data-stu-id="013e9-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="013e9-130">De standaardwaarde is **Nee**.</span><span class="sxs-lookup"><span data-stu-id="013e9-130">The default is **No**.</span></span>

![Toepassing is multitenant][api-management-aad-app-multi-tenant]

<span data-ttu-id="013e9-132">Kopieer de **Omleidings-URL** van de **Azure Active Directory** sectie van de **externe identiteiten** tabblad in de publicatieportal en plak deze in de **antwoord-URL** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="013e9-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![Antwoord-URL][api-management-aad-reply-url]

<span data-ttu-id="013e9-134">Ga naar de onderkant van het tabblad configureren, selecteer de **Toepassingsmachtigingen** vervolgkeuzelijst en Controleer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="013e9-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Toepassingsmachtigingen][api-management-aad-app-permissions]

<span data-ttu-id="013e9-136">Selecteer de **machtigingen delegeren** vervolgkeuzelijst en Controleer **aanmelding inschakelen en gebruikersprofiel lezen**.</span><span class="sxs-lookup"><span data-stu-id="013e9-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Gedelegeerde machtigingen][api-management-aad-delegated-permissions]

> <span data-ttu-id="013e9-138">Zie voor meer informatie over de toepassing en gedelegeerde machtigingen, [toegang tot de Graph API][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="013e9-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="013e9-139">Kopieer de **Client-Id** naar het Klembord.</span><span class="sxs-lookup"><span data-stu-id="013e9-139">Copy the **Client Id** to the clipboard.</span></span>

![Client-Id][api-management-aad-app-client-id]

<span data-ttu-id="013e9-141">Ga terug naar de publicatieportal en plak in het **Client-Id** gekopieerd van de configuratie van de Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="013e9-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Client-Id][api-management-client-id]

<span data-ttu-id="013e9-143">Ga terug naar de Azure Active Directory-configuratie en klikt u op de **Selecteer duur** omlaag in de **sleutels** sectie en geeft u een interval.</span><span class="sxs-lookup"><span data-stu-id="013e9-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="013e9-144">In dit voorbeeld **1 jaar** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="013e9-144">In this example, **1 year** is used.</span></span>

![Sleutel][api-management-aad-key-before-save]

<span data-ttu-id="013e9-146">Klik op **opslaan** de configuratie op te slaan en de sleutel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="013e9-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="013e9-147">De sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="013e9-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="013e9-148">Noteer deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="013e9-148">Make a note of this key.</span></span> <span data-ttu-id="013e9-149">Wanneer u het venster Azure Active Directory-configuratie hebt gesloten, wordt de sleutel kan niet opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="013e9-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Sleutel][api-management-aad-key-after-save]

<span data-ttu-id="013e9-151">Ga terug naar de publicatieportal en plak de sleutel in de **Clientgeheim** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="013e9-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Clientgeheim][api-management-client-secret]

<span data-ttu-id="013e9-153">**Tenants toegestaan** geeft aan welke mappen zijn voor toegang tot de API's van het exemplaar van API Management-service.</span><span class="sxs-lookup"><span data-stu-id="013e9-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="013e9-154">Geef de domeinen van de Azure Active Directory-exemplaren waartoe u toegang wilt verlenen.</span><span class="sxs-lookup"><span data-stu-id="013e9-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="013e9-155">U kunt meerdere domeinen scheiden met nieuwe regels, spaties of komma's.</span><span class="sxs-lookup"><span data-stu-id="013e9-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Toegestane tenants][api-management-client-allowed-tenants]


<span data-ttu-id="013e9-157">Nadat de gewenste configuratie wordt opgegeven, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="013e9-157">Once the desired configuration is specified, click **Save**.</span></span>

![Opslaan][api-management-client-allowed-tenants-save]

<span data-ttu-id="013e9-159">Wanneer de wijzigingen zijn opgeslagen, de gebruikers in de opgegeven Azure Active Directory kunnen aanmelden bij de portal voor ontwikkelaars door de stappen in [aanmelden bij de portal voor ontwikkelaars met een Azure Active Directory-account][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="013e9-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="013e9-160">Meerdere domeinen kunnen worden opgegeven in de **Tenants toegestaan** sectie.</span><span class="sxs-lookup"><span data-stu-id="013e9-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="013e9-161">Voordat een gebruiker zich vanaf een ander domein dan het oorspronkelijke domein waar de toepassing is geregistreerd aanmelden kan, moet een globale beheerder van het andere domein machtiging voor de toepassing directorygegevens toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="013e9-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="013e9-162">Als u wilt machtigen, de globale beheerder moet gaat u naar `https://<URL of your developer portal>/aadadminconsent` (bijvoorbeeld https://contoso.portal.azure-api.net/aadadminconsent), typt u de domeinnaam van de Active Directory-tenant die ze willen krijgen en klik op verzenden.</span><span class="sxs-lookup"><span data-stu-id="013e9-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="013e9-163">In het volgende voorbeeld wordt een globale beheerder van `miaoaad.onmicrosoft.com` wilt machtigen voor deze specifieke developer-portal.</span><span class="sxs-lookup"><span data-stu-id="013e9-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Machtigingen][api-management-aad-consent]

<span data-ttu-id="013e9-165">In het volgende scherm wordt de globale beheerder wordt gevraagd om te bevestigen dat de toestemming geven.</span><span class="sxs-lookup"><span data-stu-id="013e9-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Machtigingen][api-management-permissions-form]

> <span data-ttu-id="013e9-167">Als een niet-globale beheerder probeert aan te melden voordat een globale beheerder machtigingen worden verleend, wordt de aanmeldingspoging mislukt en wordt een fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="013e9-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="013e9-168">Het toevoegen van een externe Azure Active Directory-groep</span><span class="sxs-lookup"><span data-stu-id="013e9-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="013e9-169">Nadat de toegang voor gebruikers in een Azure Active Directory is ingeschakeld, kunt u Azure Active Directory-groepen toevoegen in API Management koppeling van de ontwikkelaars in de groep met de gewenste producten eenvoudiger te beheren.</span><span class="sxs-lookup"><span data-stu-id="013e9-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="013e9-170">Voor het configureren van een externe Azure Active Directory-groep moet de Azure Active Directory eerst worden geconfigureerd op het tabblad identiteiten via de volgende procedure in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="013e9-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="013e9-171">Externe Azure Active Directory-groepen worden toegevoegd vanuit de **zichtbaarheid** tabblad van het product waarvoor u toegang wilt verlenen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="013e9-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="013e9-172">Klik op **producten**, en klik vervolgens op de naam van de gewenste product.</span><span class="sxs-lookup"><span data-stu-id="013e9-172">Click **Products**, and then click the name of the desired product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="013e9-174">Overschakelen naar de **zichtbaarheid** tabblad en klik op **groepen toevoegen van Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="013e9-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Groepen toevoegen][api-management-add-groups]

<span data-ttu-id="013e9-176">Selecteer de **Azure Active Directory-Tenant** in de vervolgkeuzelijst lijst en typ vervolgens de naam van de gewenste groep in de **groepen** moet worden toegevoegd in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="013e9-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Groep selecteren][api-management-select-group]

<span data-ttu-id="013e9-178">De naam van deze groep kan worden gevonden in de **groepen** lijst voor uw Azure Active Directory, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="013e9-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Lijst van Azure Active Directory-groepen][api-management-aad-groups-list]

<span data-ttu-id="013e9-180">Klik op **toevoegen** valideren van de groepsnaam en voeg de groep.</span><span class="sxs-lookup"><span data-stu-id="013e9-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="013e9-181">In dit voorbeeld wordt de **Contoso 5 ontwikkelaars** externe groep wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="013e9-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Groep toegevoegd][api-management-aad-group-added]

<span data-ttu-id="013e9-183">Klik op **opslaan** om op te slaan van de selectie van de nieuwe groep.</span><span class="sxs-lookup"><span data-stu-id="013e9-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="013e9-184">Zodra een Azure Active Directory-groep van een product is geconfigureerd, is het beschikbaar moet worden gecontroleerd op de **zichtbaarheid** tabblad voor de andere producten in de service-exemplaar van API Management.</span><span class="sxs-lookup"><span data-stu-id="013e9-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="013e9-185">Om te bekijken en configureren van de eigenschappen voor externe groepen nadat ze zijn toegevoegd, klikt u op de naam van de groep uit de **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="013e9-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Groepen beheren][api-management-groups]

<span data-ttu-id="013e9-187">Hier kunt u de **naam** en de **beschrijving** van de groep.</span><span class="sxs-lookup"><span data-stu-id="013e9-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Groep bewerken][api-management-edit-group]

<span data-ttu-id="013e9-189">Gebruikers van de geconfigureerde Azure Active Directory kunnen aanmelden bij de portal voor ontwikkelaars en de weergave en zich abonneren op alle groepen waarvan ze inzicht hebben door de instructies in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="013e9-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="013e9-190">Hoe u zich aanmelden bij de portal voor ontwikkelaars met een Azure Active Directory-account</span><span class="sxs-lookup"><span data-stu-id="013e9-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="013e9-191">Als u wilt zich aanmelden bij de portal voor ontwikkelaars met een Azure Active Directory-account geconfigureerd in de vorige secties, open een nieuw browser venster met de **aanmeldings-URL** in de configuratie van Active Directory-toepassing en klik op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="013e9-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portal voor ontwikkelaars][api-management-dev-portal-signin]

<span data-ttu-id="013e9-193">Voer de referenties van een van de gebruikers in uw Azure Active Directory en klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="013e9-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Aanmelden][api-management-aad-signin]

<span data-ttu-id="013e9-195">U wordt mogelijk gevraagd met een registratieformulier als eventuele aanvullende informatie vereist is.</span><span class="sxs-lookup"><span data-stu-id="013e9-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="013e9-196">Vul het registratieformulier en klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="013e9-196">Complete the registration form and click **Sign up**.</span></span>

![Registratie][api-management-complete-registration]

<span data-ttu-id="013e9-198">De gebruiker is nu aangemeld bij de portal voor ontwikkelaars voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="013e9-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

