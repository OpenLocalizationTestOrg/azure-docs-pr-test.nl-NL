---
title: ontwikkelaarsaccounts aaaAuthorize met behulp van Azure Active Directory B2C - Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooauthorize gebruikers met behulp van Azure Active Directory B2C in API Management.
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="cb715-103">Hoe tooauthorize developer gebruikersaccounts met behulp van Azure Active Directory B2C in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="cb715-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="cb715-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cb715-104">Overview</span></span>
<span data-ttu-id="cb715-105">Azure Active Directory B2C is een oplossing voor identiteitsbeheer voor consumentgerichte webtoepassingen en mobiele toepassingen cloud.</span><span class="sxs-lookup"><span data-stu-id="cb715-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="cb715-106">U kunt deze gebruiken toomanage toegang tooyour developer-portal.</span><span class="sxs-lookup"><span data-stu-id="cb715-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="cb715-107">Deze handleiding ziet u de configuratie die vereist is in uw API Management-service toointegrate met Azure Active Directory B2C Hallo.</span><span class="sxs-lookup"><span data-stu-id="cb715-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="cb715-108">Zie voor meer informatie over het inschakelen van toegang toohello developer-portal met behulp van de klassieke Azure Active Directory [hoe tooauthorize developer gebruikersaccounts via Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="cb715-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="cb715-109">toocomplete hello stappen in deze handleiding, moet u eerst hebben een Azure Active Directory B2C-tenant toocreate een toepassing.</span><span class="sxs-lookup"><span data-stu-id="cb715-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="cb715-110">U moet ook toohave aanmelding en aanmelding beleidsregels gereed.</span><span class="sxs-lookup"><span data-stu-id="cb715-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="cb715-111">Zie voor meer informatie [overzicht van Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="cb715-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="cb715-112">Ontwikkelaarsaccounts autoriseren met behulp van Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="cb715-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="cb715-113">tooget gestart, klikt u op **publicatieportal** in hello Azure-portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="cb715-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="cb715-114">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="cb715-114">This takes you toohello API Management publisher portal.</span></span>

   ![Publicatieportal][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="cb715-116">Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management-zelfstudie][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="cb715-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="cb715-117">Op Hallo **API Management** menu, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="cb715-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="cb715-118">Op Hallo **identiteiten** Kies **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="cb715-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Externe identiteiten 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="cb715-120">Maak een notitie van Hallo **Omleidings-URL** en switch via Active Directory B2C tooAzure in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cb715-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Externe identiteiten 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="cb715-122">Klik op Hallo **toepassingen** knop.</span><span class="sxs-lookup"><span data-stu-id="cb715-122">Click hello **Applications** button.</span></span>

  ![Een nieuwe toepassing 1 registreren][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="cb715-124">Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory B2C-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cb715-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Een nieuwe toepassing 2 registreren][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="cb715-126">In Hallo **nieuwe toepassing** blade een naam voor de toepassing hello invoeren.</span><span class="sxs-lookup"><span data-stu-id="cb715-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="cb715-127">Kies **Ja** onder **Web App of Web-API**, en kies **Ja** onder **toestaan impliciete stroom**.</span><span class="sxs-lookup"><span data-stu-id="cb715-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="cb715-128">Vervolgens kopiëren Hallo **Omleidings-URL** van Hallo **Azure Active Directory B2C** sectie Hallo **identiteiten** tabblad in de publicatieportal hello en plak deze in Hallo **Antwoord-URL** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="cb715-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Registreren van een nieuwe toepassing 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="cb715-130">Klik op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="cb715-130">Click hello **Create** button.</span></span> <span data-ttu-id="cb715-131">Wanneer de toepassing hello wordt gemaakt, wordt deze in Hallo **toepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="cb715-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="cb715-132">Klik op Hallo toepassing naam toosee de details ervan.</span><span class="sxs-lookup"><span data-stu-id="cb715-132">Click hello application name toosee its details.</span></span>

  ![Een nieuwe toepassing 4 registreren][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="cb715-134">Van Hallo **eigenschappen** blade, kopie Hallo **toepassings-ID** toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="cb715-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![Toepassings-ID 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="cb715-136">Overschakelen van de publicatieportal back toohello en plakt u Hallo-ID in Hallo **Client-Id** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="cb715-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![Toepassings-ID 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="cb715-138">Back-toohello Azure-portal overschakelen, klikt u op Hallo **sleutels** knop en klik vervolgens op **sleutel genereren**.</span><span class="sxs-lookup"><span data-stu-id="cb715-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="cb715-139">Klik op **opslaan** toosave Hallo Hallo van configuratie- en **App-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="cb715-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="cb715-140">Hallo sleutel toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="cb715-140">Copy hello key toohello clipboard.</span></span>

  ![App-sleutel 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="cb715-142">Switch back toohello publisher-portal en plakken Hallo sleutel in Hallo **Clientgeheim** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="cb715-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![App-sleutel 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="cb715-144">Geef de domeinnaam Hallo van hello Azure Active Directory B2C-tenant in **Tenant toegestaan**.</span><span class="sxs-lookup"><span data-stu-id="cb715-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Toegestane tenant][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="cb715-146">Geef Hallo **aanmelding beleid** en **aanmelding beleid**.</span><span class="sxs-lookup"><span data-stu-id="cb715-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="cb715-147">Desgewenst kunt u ook Hallo opgeven **profiel bewerken beleid** en **opnieuw instellen wachtwoordbeleid**.</span><span class="sxs-lookup"><span data-stu-id="cb715-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Beleidsregels][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="cb715-149">Zie voor meer informatie over beleidsregels [Azure Active Directory B2C: uitbreidbaar beleidsframework].</span><span class="sxs-lookup"><span data-stu-id="cb715-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="cb715-150">Nadat u de gewenste configuratie Hallo hebt opgegeven, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cb715-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="cb715-151">Nadat het Hallo wijzigingen zijn opgeslagen, wordt de ontwikkelaars kunnen toocreate worden nieuwe accounts en de toohello developer-portal aanmelden via Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="cb715-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="cb715-152">Aanmelden voor een ontwikkelaarsaccount met behulp van Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="cb715-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="cb715-153">toosign voor een developer-account met behulp van Azure Active Directory B2C, open een nieuw browservenster en gaat u toohello developer-portal.</span><span class="sxs-lookup"><span data-stu-id="cb715-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="cb715-154">Klik op Hallo **aanmelden** knop.</span><span class="sxs-lookup"><span data-stu-id="cb715-154">Click hello **Sign up** button.</span></span>

   ![1-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="cb715-156">Kies toosign up met **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="cb715-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![2-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="cb715-158">U kunt beleid voor omgeleide toohello aanmelding die u hebt geconfigureerd in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="cb715-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="cb715-159">Kies toosign up met behulp van uw e-mailadres of een van uw bestaande sociale accounts.</span><span class="sxs-lookup"><span data-stu-id="cb715-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb715-160">Als u Azure Active Directory B2C is Hallo enige optie die ingeschakeld op Hallo **identiteiten** tabblad in de publicatieportal hello, moet u omgeleide toohello aanmelding beleid rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="cb715-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![ontwikkelaarsportal][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="cb715-162">Wanneer het Hallo-aanmelding is voltooid, bent u klaar omgeleide back toohello developer-portal.</span><span class="sxs-lookup"><span data-stu-id="cb715-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="cb715-163">U bent nu aangemeld toohello developer-portal voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="cb715-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Inschrijving voltooid][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="cb715-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb715-165">Next steps</span></span>

*  <span data-ttu-id="cb715-166">[overzicht van Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cb715-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="cb715-167">[Azure Active Directory B2C: uitbreidbaar beleidsframework]</span><span class="sxs-lookup"><span data-stu-id="cb715-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="cb715-168">[Een Microsoft-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cb715-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cb715-169">[Een Google-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cb715-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cb715-170">[Een LinkedIn-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cb715-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cb715-171">[Een Facebook-account gebruiken als een id-provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cb715-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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
[overzicht van Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[hoe tooauthorize developer gebruikersaccounts via Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: uitbreidbaar beleidsframework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Een Microsoft-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Een Google-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Een Facebook-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Een LinkedIn-account gebruiken als een id-provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
