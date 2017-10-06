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
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Hoe tooauthorize developer gebruikersaccounts met behulp van Azure Active Directory B2C in Azure API Management
## <a name="overview"></a>Overzicht
Azure Active Directory B2C is een oplossing voor identiteitsbeheer voor consumentgerichte webtoepassingen en mobiele toepassingen cloud. U kunt deze gebruiken toomanage toegang tooyour developer-portal. Deze handleiding ziet u de configuratie die vereist is in uw API Management-service toointegrate met Azure Active Directory B2C Hallo. Zie voor meer informatie over het inschakelen van toegang toohello developer-portal met behulp van de klassieke Azure Active Directory [hoe tooauthorize developer gebruikersaccounts via Azure Active Directory].

> [!NOTE]
> toocomplete hello stappen in deze handleiding, moet u eerst hebben een Azure Active Directory B2C-tenant toocreate een toepassing. U moet ook toohave aanmelding en aanmelding beleidsregels gereed. Zie voor meer informatie [overzicht van Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Ontwikkelaarsaccounts autoriseren met behulp van Azure Active Directory B2C

1. tooget gestart, klikt u op **publicatieportal** in hello Azure-portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

   ![Publicatieportal][api-management-management-console]

   > [!NOTE]
   > Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management-zelfstudie][Get started with Azure API Management].

2. Op Hallo **API Management** menu, klikt u op **beveiliging**. Op Hallo **identiteiten** Kies **Azure Active Directory B2C**.

  ![Externe identiteiten 1][api-management-howto-aad-b2c-security-tab]

3. Maak een notitie van Hallo **Omleidings-URL** en switch via Active Directory B2C tooAzure in hello Azure-portal.

  ![Externe identiteiten 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Klik op Hallo **toepassingen** knop.

  ![Een nieuwe toepassing 1 registreren][api-management-howto-aad-b2c-portal-menu]

5. Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory B2C-toepassing.

  ![Een nieuwe toepassing 2 registreren][api-management-howto-aad-b2c-add-button]

6. In Hallo **nieuwe toepassing** blade een naam voor de toepassing hello invoeren. Kies **Ja** onder **Web App of Web-API**, en kies **Ja** onder **toestaan impliciete stroom**. Vervolgens kopiëren Hallo **Omleidings-URL** van Hallo **Azure Active Directory B2C** sectie Hallo **identiteiten** tabblad in de publicatieportal hello en plak deze in Hallo **Antwoord-URL** in het tekstvak.

  ![Registreren van een nieuwe toepassing 3][api-management-howto-aad-b2c-app-details]

7. Klik op Hallo **maken** knop. Wanneer de toepassing hello wordt gemaakt, wordt deze in Hallo **toepassingen** blade. Klik op Hallo toepassing naam toosee de details ervan.

  ![Een nieuwe toepassing 4 registreren][api-management-howto-aad-b2c-app-created]

8. Van Hallo **eigenschappen** blade, kopie Hallo **toepassings-ID** toohello Klembord.

  ![Toepassings-ID 1][api-management-howto-aad-b2c-app-id]

9. Overschakelen van de publicatieportal back toohello en plakt u Hallo-ID in Hallo **Client-Id** in het tekstvak.

  ![Toepassings-ID 2][api-management-howto-aad-b2c-client-id]

10. Back-toohello Azure-portal overschakelen, klikt u op Hallo **sleutels** knop en klik vervolgens op **sleutel genereren**. Klik op **opslaan** toosave Hallo Hallo van configuratie- en **App-sleutel**. Hallo sleutel toohello Klembord kopiëren.

  ![App-sleutel 1][api-management-howto-aad-b2c-app-key]

11. Switch back toohello publisher-portal en plakken Hallo sleutel in Hallo **Clientgeheim** in het tekstvak.

  ![App-sleutel 2][api-management-howto-aad-b2c-client-secret]

12. Geef de domeinnaam Hallo van hello Azure Active Directory B2C-tenant in **Tenant toegestaan**.

  ![Toegestane tenant][api-management-howto-aad-b2c-allowed-tenant]

13. Geef Hallo **aanmelding beleid** en **aanmelding beleid**. Desgewenst kunt u ook Hallo opgeven **profiel bewerken beleid** en **opnieuw instellen wachtwoordbeleid**.

  ![Beleidsregels][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Zie voor meer informatie over beleidsregels [Azure Active Directory B2C: uitbreidbaar beleidsframework].

14. Nadat u de gewenste configuratie Hallo hebt opgegeven, klikt u op **opslaan**.

  Nadat het Hallo wijzigingen zijn opgeslagen, wordt de ontwikkelaars kunnen toocreate worden nieuwe accounts en de toohello developer-portal aanmelden via Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Aanmelden voor een ontwikkelaarsaccount met behulp van Azure Active Directory B2C

1. toosign voor een developer-account met behulp van Azure Active Directory B2C, open een nieuw browservenster en gaat u toohello developer-portal. Klik op Hallo **aanmelden** knop.

   ![1-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal]

2. Kies toosign up met **Azure Active Directory B2C**.

   ![2-portal voor ontwikkelaars][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. U kunt beleid voor omgeleide toohello aanmelding die u hebt geconfigureerd in de vorige sectie Hallo. Kies toosign up met behulp van uw e-mailadres of een van uw bestaande sociale accounts.

   > [!NOTE]
   > Als u Azure Active Directory B2C is Hallo enige optie die ingeschakeld op Hallo **identiteiten** tabblad in de publicatieportal hello, moet u omgeleide toohello aanmelding beleid rechtstreeks.

   ![ontwikkelaarsportal][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Wanneer het Hallo-aanmelding is voltooid, bent u klaar omgeleide back toohello developer-portal. U bent nu aangemeld toohello developer-portal voor uw API Management-service-exemplaar.

    ![Inschrijving voltooid][api-management-registration-complete]

## <a name="next-steps"></a>Volgende stappen

*  [overzicht van Azure Active Directory B2C]
*  [Azure Active Directory B2C: uitbreidbaar beleidsframework]
*  [Een Microsoft-account gebruiken als een id-provider in Azure Active Directory B2C]
*  [Een Google-account gebruiken als een id-provider in Azure Active Directory B2C]
*  [Een LinkedIn-account gebruiken als een id-provider in Azure Active Directory B2C]
*  [Een Facebook-account gebruiken als een id-provider in Azure Active Directory B2C]




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
