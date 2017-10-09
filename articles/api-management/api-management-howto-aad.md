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
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Hoe tooauthorize developer gebruikersaccounts via Azure Active Directory in Azure API Management
## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooenable toegang krijgen tot toohello developer-portal voor gebruikers van Azure Active Directory. Deze handleiding ziet u ook hoe toomanage groepen Azure Active Directory-gebruikers door het toevoegen van externe groepen met gebruikers van een Azure Active Directory Hallo.

> toocomplete hello stappen in deze handleiding u moet eerst een Azure Active Directory in welke toocreate een toepassing hebben.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Hoe tooauthorize developer gebruikersaccounts via Azure Active Directory
tooget gestart, klikt u op **publicatieportal** in hello Azure-portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **beveiliging** van Hallo **API Management** menu op Hallo linkerkant en klik op **externe identiteiten**.

![Externe identiteit][api-management-security-external-identities]

Klik op **Azure Active Directory**. Maak een notitie van Hallo **Omleidings-URL** en tooyour Azure Active Directory in de klassieke Azure-Portal Hallo overgeschakeld.

![Externe identiteit][api-management-security-aad-new]

Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory-toepassing, en kies **mijn organisatie ontwikkelt toepassing toevoegen**.

![Nieuwe Azure Active Directory-toepassing toevoegen][api-management-new-aad-application-menu]

Voer een naam voor toepassing hello, selecteert **Web-toepassing en/of Web-API**, en klik op de volgende knop Hallo.

![Nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-1]

Voor **aanmeldings-URL**, Voer Hallo aanmeldings-URL van uw ontwikkelaarsportal. In dit voorbeeld Hallo **aanmeldings-URL** is `https://aad03.portal.current.int-azure-api.net/signin`. 

Voor Hallo **App-ID-URL**standaarddomein hello of een aangepast domein invoeren voor hello Azure Active Directory en een unieke tekenreeks tooit toevoegen. In dit voorbeeld Hallo standaarddomein van **https://contoso5api.onmicrosoft.com** wordt gebruikt en het achtervoegsel Hallo **/api** opgegeven.

![Eigenschappen van nieuwe Azure Active Directory-toepassing][api-management-new-aad-application-2]

Klik op Hallo selectievakje knop toosave en toohello overschakelen Hallo-toepassing maken **configureren** tabblad tooconfigure Hallo nieuwe toepassing.

![Nieuwe Azure Active Directory-toepassing gemaakt][api-management-new-aad-app-created]

Als meerdere Azure Active Directory's toobe gebruikt voor deze toepassing gaat, klikt u op **Ja** voor **toepassing is multitenant**. Hallo standaardwaarde is **Nee**.

![Toepassing is multitenant][api-management-aad-app-multi-tenant]

Kopiëren Hallo **Omleidings-URL** van Hallo **Azure Active Directory** sectie Hallo **externe identiteiten** tabblad in de publicatieportal hello en plak deze in Hallo **Antwoord-URL** in het tekstvak. 

![Antwoord-URL][api-management-aad-reply-url]

Scroll toohello onderaan Hallo configureren tabblad Selecteer Hallo **Toepassingsmachtigingen** vervolgkeuzelijst en Controleer **mapgegevens lezen**.

![Toepassingsmachtigingen][api-management-aad-app-permissions]

Selecteer Hallo **machtigingen delegeren** vervolgkeuzelijst en Controleer **aanmelding inschakelen en gebruikersprofiel lezen**.

![Gedelegeerde machtigingen][api-management-aad-delegated-permissions]

> Zie voor meer informatie over de toepassing en gedelegeerde machtigingen, [toegang tot Hallo Graph API][Accessing hello Graph API].
> 
> 

Kopiëren Hallo **Client-Id** toohello Klembord.

![Client-Id][api-management-aad-app-client-id]

Overschakelen van de publicatieportal back toohello en plak in Hallo **Client-Id** gekopieerd van de configuratie van een hello Azure Active Directory-toepassing.

![Client-Id][api-management-client-id]

Switch back toohello Azure Active Directory-configuratie en klikt u op Hallo **Selecteer duur** vervolgkeuzelijst in Hallo **sleutels** sectie en geeft u een interval. In dit voorbeeld **1 jaar** wordt gebruikt.

![Sleutel][api-management-aad-key-before-save]

Klik op **opslaan** toosave Hallo configuratie- en Hallo sleutel. Hallo sleutel toohello Klembord kopiëren.

> Noteer deze sleutel. Wanneer u een venster hello Azure Active Directory-configuratie hebt gesloten, kan niet opnieuw Hallo sleutel weergegeven.
> 
> 

![Sleutel][api-management-aad-key-after-save]

Switch back toohello publisher-portal en plakken Hallo sleutel in Hallo **Clientgeheim** in het tekstvak.

![Clientgeheim][api-management-client-secret]

**Tenants toegestaan** geeft aan welke mappen zijn toegang toohello API's van Hallo API Management service-exemplaar. Geef de domeinen Hallo Hallo Azure Active Directory-exemplaren toowhich gewenste toogrant toegang. U kunt meerdere domeinen scheiden met nieuwe regels, spaties of komma's.

![Toegestane tenants][api-management-client-allowed-tenants]


Zodra het Hallo gewenst configuratie is opgegeven, klikt u op **opslaan**.

![Opslaan][api-management-client-allowed-tenants-save]

Wanneer Hallo wijzigingen zijn opgeslagen, Hallo gebruikers in Hallo opgegeven Azure Active Directory toohello Developer-portal kunt aanmelden volgens de stappen Hallo in [toohello Developer-portal met een Azure Active Directory-account aanmelden] [Log in toohello Developer portal using an Azure Active Directory account].

Meerdere domeinen kunnen worden opgegeven in Hallo **Tenants toegestaan** sectie. Voordat een gebruiker zich vanaf een ander domein dan de oorspronkelijke Hallo-domein waar de toepassing hello is geregistreerd aanmelden kan, moet een globale beheerder van een ander domein Hallo machtigen Hallo toepassing tooaccess Active directory-gegevens. toogrant machtiging Hallo globale beheerder moet te gaan`https://<URL of your developer portal>/aadadminconsent` (bijvoorbeeld https://contoso.portal.azure-api.net/aadadminconsent), typt u Hallo-domeinnaam van Active Directory-tenant die ze willen toogive toegang tooand Hallo klikt u op verzenden. In de volgende Hallo bijvoorbeeld, een globale beheerder van `miaoaad.onmicrosoft.com` probeert toogive machtiging toothis bepaalde developer-portal. 

![Machtigingen][api-management-aad-consent]

In het volgende scherm hello niet Hallo globale beheerder vraag tooconfirm Hallo toestemming geven. 

![Machtigingen][api-management-permissions-form]

> Als een niet-globale beheerder probeert toolog in voordat u machtigingen worden verleend door een globale beheerder Hallo aanmeldingspoging mislukt en een fout wordt weergegeven.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Hoe tooadd een externe Azure Active Directory groeperen
Nadat de toegang voor gebruikers in een Azure Active Directory is ingeschakeld, kunt u toevoegen Azure Active Directory-groepen in API Management toomore eenvoudig hello koppeling van ontwikkelaars Hallo in Hallo groep met Hallo gewenst producten te beheren.

> tooconfigure een externe Azure Active Directory-groep hello Azure Active Directory moet eerst worden geconfigureerd op Hallo identiteiten tabblad door Hallo-procedure in de vorige sectie hello te volgen. 
> 
> 

Externe Azure Active Directory-groepen worden toegevoegd vanuit Hallo **zichtbaarheid** tabblad van het Hallo-product waarvoor u wenst dat de toegangsgroep toohello toogrant. Klik op **producten**, en klik vervolgens op Hallo-naam van de gewenste product Hallo.

![Product configureren][api-management-configure-product]

Overschakelen van toohello **zichtbaarheid** tabblad en klik op **groepen toevoegen van Azure Active Directory**.

![Groepen toevoegen][api-management-add-groups]

Selecteer Hallo **Azure Active Directory-Tenant** uit de vervolgkeuzelijst Hallo en vervolgens Hallo-typenaam van de gewenste groep Hallo in Hallo **groepen** toobe toegevoegd in het tekstvak.

![Groep selecteren][api-management-select-group]

De naam van deze groep kan worden gevonden in Hallo **groepen** lijst voor uw Azure Active Directory, zoals wordt weergegeven in Hallo voorbeeld te volgen.

![Lijst van Azure Active Directory-groepen][api-management-aad-groups-list]

Klik op **toevoegen** toovalidate Hallo groepsnaam en Hallo groep toevoegen. In dit voorbeeld Hallo **Contoso 5 ontwikkelaars** externe groep wordt toegevoegd. 

![Groep toegevoegd][api-management-aad-group-added]

Klik op **opslaan** toosave Hallo nieuwe groep selecteren.

Zodra een Azure Active Directory-groep van een product is geconfigureerd, is beschikbaar toobe gecontroleerd op Hallo **zichtbaarheid** tabblad voor andere producten in API Management service-exemplaar Hallo Hallo.

tooreview en Hallo eigenschappen configureren voor externe groepen zodra ze zijn toegevoegd, klikt u op Hallo naam van groep van Hallo Hallo **groepen** tabblad.

![Groepen beheren][api-management-groups]

Hier kunt u Hallo **naam** en Hallo **beschrijving** van Hallo-groep.

![Groep bewerken][api-management-edit-group]

Gebruikers van Hallo geconfigureerde Azure Active Directory kunnen aanmelden toohello Developer-portal en bekijk en zich abonneren tooany groepen waarvan ze inzicht door Hallo-instructies in de volgende sectie Hallo hebben.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Hoe toolog in toohello portal voor ontwikkelaars met een Azure Active Directory-account
toolog in Hallo Developer-portal met een Azure Active Directory-account geconfigureerd in de vorige secties Hallo, open een nieuw browservenster Hallo met **aanmeldings-URL** in configuratie van Active Directory-toepassing hello en klik op **Azure Active Directory**.

![Portal voor ontwikkelaars][api-management-dev-portal-signin]

Geef referenties op Hallo van een van Hallo gebruikers in uw Azure Active Directory en klikt u op **aanmelden**.

![Aanmelden][api-management-aad-signin]

U wordt mogelijk gevraagd met een registratieformulier als eventuele aanvullende informatie vereist is. Hallo-registratieformulier voltooid en klik op **aanmelden**.

![Registratie][api-management-complete-registration]

De gebruiker is nu aangemeld bij Hallo developer-portal voor uw API Management-service-exemplaar.

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

