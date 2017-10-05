---
title: Ontwikkelaarsaccounts autoriseren met behulp van Azure Active Directory B2C - Azure API Management | Microsoft Docs
description: Informatie over het autoriseren van gebruikers met behulp van Azure Active Directory B2C in API Management.
services: api-management
documentationcenter: API Management
author: miaojiang
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="dc7e0-103">Hoe ontwikkelaarsaccounts autoriseren met behulp van Azure Active Directory B2C in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="dc7e0-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="dc7e0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="dc7e0-104">Overview</span></span>
<span data-ttu-id="dc7e0-105">Azure Active Directory B2C is een oplossing voor identiteitsbeheer voor consumentgerichte webtoepassingen en mobiele toepassingen cloud.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="dc7e0-106">U kunt deze gebruiken voor toegang tot uw ontwikkelaarsportal beheren.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="dc7e0-107">Deze handleiding beschrijft u de configuratie die vereist is in uw API Management-service om te integreren met Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="dc7e0-108">Zie voor meer informatie over het inschakelen van toegang tot de portal voor ontwikkelaars via de klassieke Azure Active Directory [hoe ontwikkelaarsaccounts met Azure Active Directory autoriseren].</span><span class="sxs-lookup"><span data-stu-id="dc7e0-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="dc7e0-109">U moet een Azure Active Directory B2C-tenant maken van een toepassing in hebben voor het voltooien van de stappen in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="dc7e0-110">U moet ook, aanmelding en aanmelding beleid gereed.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="dc7e0-111">Zie voor meer informatie [overzicht van Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="dc7e0-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="dc7e0-112">Ontwikkelaarsaccounts autoriseren met behulp van Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="dc7e0-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="dc7e0-113">Om te beginnen, klikt u op **publicatieportal** in de Azure portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="dc7e0-114">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-114">This takes you to the API Management publisher portal.</span></span>

   ![Publicatieportal][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="dc7e0-116">Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in de [aan de slag met Azure API Management-zelfstudie] [Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="dc7e0-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="dc7e0-117">Op de **API Management** menu, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="dc7e0-118">Op de **identiteiten** Kies **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Externe identiteiten 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="dc7e0-120">Noteer de **Omleidings-URL** en schakel naar Azure Active Directory B2C in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Externe identiteiten 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="dc7e0-122">Klik op de **toepassingen** knop.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-122">Click the **Applications** button.</span></span>

  ![Een nieuwe toepassing 1 registreren][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="dc7e0-124">Klik op de **toevoegen** knop een nieuwe Azure Active Directory B2C-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Een nieuwe toepassing 2 registreren][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="dc7e0-126">In de **nieuwe toepassing** blade een naam voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="dc7e0-127">Kies **Ja** onder **Web App of Web-API**, en kies **Ja** onder **toestaan impliciete stroom**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="dc7e0-128">Kopieer de **Omleidings-URL** van de **Azure Active Directory B2C** sectie van de **identiteiten** tabblad in de publicatieportal en plak deze in de **antwoord URL** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Registreren van een nieuwe toepassing 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="dc7e0-130">Klik op de knop **Maken**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-130">Click the **Create** button.</span></span> <span data-ttu-id="dc7e0-131">Wanneer de toepassing is gemaakt, wordt deze weergegeven de **toepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="dc7e0-132">Klik op de naam van de toepassing om de details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-132">Click the application name to see its details.</span></span>

  ![Een nieuwe toepassing 4 registreren][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="dc7e0-134">Van de **eigenschappen** blade-, Kopieer de **toepassings-ID** naar het Klembord.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![Toepassings-ID 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="dc7e0-136">Ga terug naar de publicatieportal en plakt u de ID in de **Client-Id** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Toepassings-ID 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="dc7e0-138">Ga terug naar de Azure-portal, klikt u op de **sleutels** knop en klik vervolgens op **sleutel genereren**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="dc7e0-139">Klik op **opslaan** de configuratie op te slaan en wordt weergegeven de **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="dc7e0-140">De sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-140">Copy the key to the clipboard.</span></span>

  ![App-sleutel 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="dc7e0-142">Ga terug naar de publicatieportal en plak de sleutel in de **Clientgeheim** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![App-sleutel 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="dc7e0-144">Geef de domeinnaam van de Azure Active Directory B2C-tenant in **Tenant toegestaan**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Toegestane tenant][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="dc7e0-146">Geef de **aanmelding beleid** en **aanmelding beleid**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="dc7e0-147">Desgewenst kunt u ook opgeven de **profiel bewerken beleid** en **opnieuw instellen wachtwoordbeleid**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Beleidsregels][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="dc7e0-149">Zie voor meer informatie over beleidsregels [Azure Active Directory B2C: uitbreidbaar beleidsframework].</span><span class="sxs-lookup"><span data-stu-id="dc7e0-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="dc7e0-150">Nadat u de gewenste configuratie hebt opgegeven, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="dc7e0-151">Nadat de wijzigingen zijn opgeslagen, zich ontwikkelaars voor het maken van nieuwe accounts en aanmelden bij de portal voor ontwikkelaars met behulp van Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="dc7e0-152">Aanmelden voor een ontwikkelaarsaccount met behulp van Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="dc7e0-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="dc7e0-153">Aanmelden voor een ontwikkelaarsaccount met behulp van Azure Active Directory B2C, open een nieuw browservenster en gaat u naar de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="dc7e0-154">Klik op de **aanmelden** knop.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-154">Click the **Sign up** button.</span></span>

   ![1-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="dc7e0-156">Wilt u zich aanmeldt met **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![2-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="dc7e0-158">U wordt omgeleid naar het registratie-beleid die u hebt geconfigureerd in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="dc7e0-159">Kies aan te melden met behulp van uw e-mailadres of een van uw bestaande sociale accounts.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc7e0-160">Als u Azure Active Directory B2C is de enige optie die ingeschakeld op de **identiteiten** tabblad in de publicatieportal u zult omgeleid naar het registratie-beleid rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![ontwikkelaarsportal][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="dc7e0-162">Wanneer de aanmelding voltooid is, bent u omgeleid naar de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="dc7e0-163">U bent nu aangemeld bij de portal voor ontwikkelaars voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="dc7e0-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Inschrijving voltooid][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="dc7e0-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc7e0-165">Next steps</span></span>

*  <span data-ttu-id="dc7e0-166">[overzicht van Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="dc7e0-167">[Azure Active Directory B2C: uitbreidbaar beleidsframework]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="dc7e0-168">[Een Microsoft-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="dc7e0-169">[Een Google-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="dc7e0-170">[Een LinkedIn-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="dc7e0-171">[Een Facebook-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="dc7e0-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
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
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
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
<span data-ttu-id="dc7e0-172">[overzicht van Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="dc7e0-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="dc7e0-173">[hoe ontwikkelaarsaccounts met Azure Active Directory autoriseren]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="dc7e0-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="dc7e0-174">[Azure Active Directory B2C: uitbreidbaar beleidsframework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="dc7e0-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="dc7e0-175">[Een Microsoft-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="dc7e0-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="dc7e0-176">[Een Google-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="dc7e0-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="dc7e0-177">[Een Facebook-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="dc7e0-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="dc7e0-178">[Een LinkedIn-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="dc7e0-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
