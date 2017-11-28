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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="096b5-103">Hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="096b5-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="096b5-104">API Management biedt Hallo mogelijkheid toosecure access toohello back-end-service van een API met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="096b5-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="096b5-105">Deze handleiding wordt getoond hoe toomanage certificaten in de publicatieportal Hallo API en hoe een API tooconfigure toouse een tooaccess certificaat de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="096b5-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="096b5-106">Zie voor meer informatie over het beheren van certificaten met behulp van API Management REST API Hallo [Azure API Management REST API certificaat entiteit][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="096b5-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="096b5-107"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="096b5-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="096b5-108">Deze handleiding wordt getoond hoe tooconfigure uw API Management-service-exemplaar toouse client certificaat verificatie tooaccess Hallo back-end-service voor een API.</span><span class="sxs-lookup"><span data-stu-id="096b5-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="096b5-109">Voordat de volgende Hallo stappen in dit onderwerp, moet u beschikken over uw back-end-service die is geconfigureerd voor verificatie van clientcertificaten ([tooconfigure certificaat verificatie in Azure WebSites verwijzen toothis artikel] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), en toohello certificaat en Hallo wachtwoord voor toegang tot Hallo-certificaat voor het uploaden van in de publicatieportal van API Management Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="096b5-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="096b5-110"><a name="step1"></a>Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="096b5-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="096b5-111">tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="096b5-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="096b5-112">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="096b5-112">This takes you toohello API Management publisher portal.</span></span>

![API-publicatieportal][api-management-management-console]

> <span data-ttu-id="096b5-114">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="096b5-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="096b5-115">Klik op **beveiliging** van Hallo **API Management** menu op Hallo linkerkant en klik op **clientcertificaten**.</span><span class="sxs-lookup"><span data-stu-id="096b5-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Clientcertificaten][api-management-security-client-certificates]

<span data-ttu-id="096b5-117">een nieuw certificaat tooupload klikt u op **certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="096b5-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Certificaat uploaden][api-management-upload-certificate]

<span data-ttu-id="096b5-119">Blader tooyour certificaat en vervolgens Hallo wachtwoord invoeren voor Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="096b5-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="096b5-120">Hallo-certificaat moet **.pfx** indeling.</span><span class="sxs-lookup"><span data-stu-id="096b5-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="096b5-121">Zelfondertekende certificaten zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="096b5-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Certificaat uploaden][api-management-upload-certificate-form]

<span data-ttu-id="096b5-123">Klik op **uploaden** tooupload Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="096b5-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="096b5-124">Hallo certificaatwachtwoord wordt op dit moment gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="096b5-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="096b5-125">Als dit onjuist is wordt een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="096b5-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificaat geüpload][api-management-certificate-uploaded]

<span data-ttu-id="096b5-127">Zodra het Hallo-certificaat is geüpload, wordt deze weergegeven op Hallo **clientcertificaten** tabblad. Als er meerdere certificaten, noteer Hallo onderwerp of laatste vier tekens van Hallo-vingerafdruk die gebruikte tooselect Hallo certificaat bij het configureren van een API-toouse certificaten, zoals beschreven in de volgende Hallo Hallo [configureren een API-toouse een clientcertificaat voor gatewayverificatie] [ Configure an API toouse a client certificate for gateway authentication] sectie.</span><span class="sxs-lookup"><span data-stu-id="096b5-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="096b5-128">tooturn uit de validatie van certificaatketen wanneer u bijvoorbeeld een zelfondertekend certificaat Volg Hallo stappen in deze Veelgestelde vragen [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="096b5-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="096b5-129"><a name="step1a"></a>Een clientcertificaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="096b5-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="096b5-130">toodelete een certificaat, klik op **verwijderen** naast Hallo gewenste certificaat.</span><span class="sxs-lookup"><span data-stu-id="096b5-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Certificaat verwijderen][api-management-certificate-delete]

<span data-ttu-id="096b5-132">Klik op **Ja, deze verwijderen** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="096b5-132">Click **Yes, delete it** tooconfirm.</span></span>

![De verwijdering bevestigen][api-management-confirm-delete]

<span data-ttu-id="096b5-134">Als het Hallo-certificaat wordt gebruikt door een API, wordt een scherm waarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="096b5-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="096b5-135">toodelete hello certificaat, moet u eerst Hallo verwijderen van het certificaat van een API's die zijn geconfigureerd toouse deze.</span><span class="sxs-lookup"><span data-stu-id="096b5-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![De verwijdering bevestigen][api-management-confirm-delete-policy]

## <span data-ttu-id="096b5-137"><a name="step2"></a>Een API-toouse een clientcertificaat voor gatewayverificatie configureren</span><span class="sxs-lookup"><span data-stu-id="096b5-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="096b5-138">Klik op **API's** van Hallo **API Management** menu op Hallo links, klikt u op de naam Hallo van Hallo gewenst API en op Hallo **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="096b5-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![API-beveiliging][api-management-api-security]

<span data-ttu-id="096b5-140">Selecteer **clientcertificaten** van Hallo **met referenties** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="096b5-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Clientcertificaten][api-management-mutual-certificates]

<span data-ttu-id="096b5-142">Selecteer Hallo gewenste certificaat van Hallo **clientcertificaat** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="096b5-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="096b5-143">Als er meerdere certificaten kunt u bekijkt hello onderwerp of Hallo laatste vier tekens van Hallo vingerafdruk zoals aangegeven in Hallo vorige sectie toodetermine Hallo juiste certificaat.</span><span class="sxs-lookup"><span data-stu-id="096b5-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Selecteer het certificaat][api-management-select-certificate]

<span data-ttu-id="096b5-145">Klik op **opslaan** toosave Hallo-configuratie wijzigen toohello API.</span><span class="sxs-lookup"><span data-stu-id="096b5-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="096b5-146">Deze wijziging wordt onmiddellijk van kracht en aanroepen toooperations van die API gebruikt Hallo certificaat tooauthenticate op Hallo back-endserver.</span><span class="sxs-lookup"><span data-stu-id="096b5-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Sla de wijzigingen van de API][api-management-save-api]

> <span data-ttu-id="096b5-148">Wanneer een certificaat voor gatewayverificatie voor Hallo back-end-service van een API is opgegeven, wordt het onderdeel van het Hallo-beleid voor die API en kunnen worden weergegeven in de beleidseditor Hallo.</span><span class="sxs-lookup"><span data-stu-id="096b5-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Certificaatbeleid][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="096b5-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="096b5-150">Next steps</span></span>
<span data-ttu-id="096b5-151">Uw back-endservice zoals HTTP basic of gedeelde geheime-verificatie, Zie voor meer informatie over andere manieren toosecure Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="096b5-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

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



