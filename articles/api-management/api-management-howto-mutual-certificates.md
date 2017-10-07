---
title: aaaSecure back-end-services met behulp van verificatie van clientcertificaten - Azure API Management | Microsoft Docs
description: Meer informatie over hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie in Azure API Management
API Management biedt Hallo mogelijkheid toosecure access toohello back-end-service van een API met behulp van clientcertificaten. Deze handleiding wordt getoond hoe toomanage certificaten in de publicatieportal Hallo API en hoe een API tooconfigure toouse een tooaccess certificaat de back-endservice.

Zie voor meer informatie over het beheren van certificaten met behulp van API Management REST API Hallo [Azure API Management REST API certificaat entiteit][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Vereisten
Deze handleiding wordt getoond hoe tooconfigure uw API Management-service-exemplaar toouse client certificaat verificatie tooaccess Hallo back-end-service voor een API. Voordat de volgende Hallo stappen in dit onderwerp, moet u beschikken over uw back-end-service die is geconfigureerd voor verificatie van clientcertificaten ([tooconfigure certificaat verificatie in Azure WebSites verwijzen toothis artikel] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), en toohello certificaat en Hallo wachtwoord voor toegang tot Hallo-certificaat voor het uploaden van in de publicatieportal van API Management Hallo hebben.

## <a name="step1"></a>Een certificaat uploaden
tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

![API-publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **beveiliging** van Hallo **API Management** menu op Hallo linkerkant en klik op **clientcertificaten**.

![Clientcertificaten][api-management-security-client-certificates]

een nieuw certificaat tooupload klikt u op **certificaat uploaden**.

![Certificaat uploaden][api-management-upload-certificate]

Blader tooyour certificaat en vervolgens Hallo wachtwoord invoeren voor Hallo certificaat.

> Hallo-certificaat moet **.pfx** indeling. Zelfondertekende certificaten zijn toegestaan.
> 
> 

![Certificaat uploaden][api-management-upload-certificate-form]

Klik op **uploaden** tooupload Hallo certificaat.

> Hallo certificaatwachtwoord wordt op dit moment gevalideerd. Als dit onjuist is wordt een foutbericht weergegeven.
> 
> 

![Certificaat geüpload][api-management-certificate-uploaded]

Zodra het Hallo-certificaat is geüpload, wordt deze weergegeven op Hallo **clientcertificaten** tabblad. Als er meerdere certificaten, noteer Hallo onderwerp of laatste vier tekens van Hallo-vingerafdruk die gebruikte tooselect Hallo certificaat bij het configureren van een API-toouse certificaten, zoals beschreven in de volgende Hallo Hallo [configureren een API-toouse een clientcertificaat voor gatewayverificatie] [ Configure an API toouse a client certificate for gateway authentication] sectie.

> tooturn uit de validatie van certificaatketen wanneer u bijvoorbeeld een zelfondertekend certificaat Volg Hallo stappen in deze Veelgestelde vragen [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Een clientcertificaat verwijderen
toodelete een certificaat, klik op **verwijderen** naast Hallo gewenste certificaat.

![Certificaat verwijderen][api-management-certificate-delete]

Klik op **Ja, deze verwijderen** tooconfirm.

![De verwijdering bevestigen][api-management-confirm-delete]

Als het Hallo-certificaat wordt gebruikt door een API, wordt een scherm waarschuwing weergegeven. toodelete hello certificaat, moet u eerst Hallo verwijderen van het certificaat van een API's die zijn geconfigureerd toouse deze.

![De verwijdering bevestigen][api-management-confirm-delete-policy]

## <a name="step2"></a>Een API-toouse een clientcertificaat voor gatewayverificatie configureren
Klik op **API's** van Hallo **API Management** menu op Hallo links, klikt u op de naam Hallo van Hallo gewenst API en op Hallo **beveiliging** tabblad.

![API-beveiliging][api-management-api-security]

Selecteer **clientcertificaten** van Hallo **met referenties** vervolgkeuzelijst.

![Clientcertificaten][api-management-mutual-certificates]

Selecteer Hallo gewenste certificaat van Hallo **clientcertificaat** vervolgkeuzelijst. Als er meerdere certificaten kunt u bekijkt hello onderwerp of Hallo laatste vier tekens van Hallo vingerafdruk zoals aangegeven in Hallo vorige sectie toodetermine Hallo juiste certificaat.

![Selecteer het certificaat][api-management-select-certificate]

Klik op **opslaan** toosave Hallo-configuratie wijzigen toohello API.

> Deze wijziging wordt onmiddellijk van kracht en aanroepen toooperations van die API gebruikt Hallo certificaat tooauthenticate op Hallo back-endserver.
> 
> 

![Sla de wijzigingen van de API][api-management-save-api]

> Wanneer een certificaat voor gatewayverificatie voor Hallo back-end-service van een API is opgegeven, wordt het onderdeel van het Hallo-beleid voor die API en kunnen worden weergegeven in de beleidseditor Hallo.
> 
> 

![Certificaatbeleid][api-management-certificate-policy]

## <a name="next-steps"></a>Volgende stappen
Uw back-endservice zoals HTTP basic of gedeelde geheime-verificatie, Zie voor meer informatie over andere manieren toosecure Hallo video te volgen.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



