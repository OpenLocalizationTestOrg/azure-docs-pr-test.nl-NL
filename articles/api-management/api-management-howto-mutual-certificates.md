---
title: Beveiligen van back-end-services met behulp van client certificaatverificatie - Azure API Management | Microsoft Docs
description: Informatie over het beveiligen van back-end-services met behulp van verificatie van clientcertificaten in Azure API Management.
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="640c4-103">Het beveiligen van back-end-services met behulp van client certificaatverificatie in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="640c4-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="640c4-104">API Management biedt de mogelijkheid voor het beveiligen van toegang tot de back-end-service van een API met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="640c4-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="640c4-105">Deze handleiding wordt beschreven hoe u voor het beheren van certificaten in de publicatieportal van API en het configureren van een API voor het gebruik van een certificaat voor toegang tot de back-end-service.</span><span class="sxs-lookup"><span data-stu-id="640c4-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="640c4-106">Zie voor meer informatie over het beheren van certificaten met behulp van API Management REST API [Azure API Management REST API certificaat entiteit][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="640c4-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="640c4-107"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="640c4-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="640c4-108">Deze handleiding laat zien hoe uw API Management-service-exemplaar voor het gebruik van verificatie van clientcertificaten voor toegang tot de back-end-service voor een API te configureren.</span><span class="sxs-lookup"><span data-stu-id="640c4-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="640c4-109">Voordat u de stappen in dit onderwerp, hebt u uw back-end-service die is geconfigureerd voor verificatie van clientcertificaten ([certificaatverificatie in Azure WebSites configureren Raadpleeg dit artikel] [ to configure certificate authentication in Azure WebSites refer to this article]), en hebben toegang tot het certificaat en het wachtwoord voor het certificaat voor het uploaden van in de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="640c4-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="640c4-110"><a name="step1"></a>Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="640c4-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="640c4-111">Als u aan de slag wilt gaan, klikt u op **Publicatieportal** in Azure Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="640c4-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="640c4-112">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="640c4-112">This takes you to the API Management publisher portal.</span></span>

![API-publicatieportal][api-management-management-console]

> <span data-ttu-id="640c4-114">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="640c4-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="640c4-115">Klik op **beveiliging** van de **API Management** menu aan de linkerkant en klik op **clientcertificaten**.</span><span class="sxs-lookup"><span data-stu-id="640c4-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Clientcertificaten][api-management-security-client-certificates]

<span data-ttu-id="640c4-117">Als u wilt een nieuw certificaat uploaden, klikt u op **certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="640c4-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Certificaat uploaden][api-management-upload-certificate]

<span data-ttu-id="640c4-119">Blader naar uw certificaat en voer vervolgens het wachtwoord voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="640c4-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="640c4-120">Het certificaat moet **.pfx** indeling.</span><span class="sxs-lookup"><span data-stu-id="640c4-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="640c4-121">Zelfondertekende certificaten zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="640c4-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Certificaat uploaden][api-management-upload-certificate-form]

<span data-ttu-id="640c4-123">Klik op **uploaden** om het certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="640c4-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="640c4-124">Wachtwoord voor het certificaat wordt op dit moment gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="640c4-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="640c4-125">Als dit onjuist is wordt een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="640c4-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificaat geüpload][api-management-certificate-uploaded]

<span data-ttu-id="640c4-127">Zodra het certificaat is geüpload, wordt deze weergegeven op de **clientcertificaten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="640c4-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="640c4-128">Als er meerdere certificaten, moet u een notitie van het onderwerp of de laatste vier tekens van de vingerafdruk die worden gebruikt voor het certificaat te selecteren bij het configureren van een API voor het gebruik van certificaten, zoals beschreven in de volgende [configureren van een API gebruiken een clientcertificaat voor gatewayverificatie] [ Configure an API to use a client certificate for gateway authentication] sectie.</span><span class="sxs-lookup"><span data-stu-id="640c4-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="640c4-129">Als u wilt uitschakelen validatie van certificaatketen wanneer u bijvoorbeeld een zelfondertekend certificaat, volg de stappen in deze Veelgestelde vragen [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="640c4-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="640c4-130"><a name="step1a"></a>Een clientcertificaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="640c4-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="640c4-131">Als u wilt een certificaat wilt verwijderen, klikt u op **verwijderen** naast het gewenste certificaat.</span><span class="sxs-lookup"><span data-stu-id="640c4-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Certificaat verwijderen][api-management-certificate-delete]

<span data-ttu-id="640c4-133">Klik op **Ja, deze verwijderen** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="640c4-133">Click **Yes, delete it** to confirm.</span></span>

![De verwijdering bevestigen][api-management-confirm-delete]

<span data-ttu-id="640c4-135">Als het certificaat gebruikt door een API wordt en vervolgens een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="640c4-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="640c4-136">Als u wilt verwijderen van het certificaat moet u eerst het certificaat verwijderen uit alle API's die zijn geconfigureerd voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="640c4-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![De verwijdering bevestigen][api-management-confirm-delete-policy]

## <span data-ttu-id="640c4-138"><a name="step2"></a>Een API voor het gebruik van een certificaat voor gatewayverificatie configureren</span><span class="sxs-lookup"><span data-stu-id="640c4-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="640c4-139">Klik op **API's** van de **API Management** menu aan de linkerkant op de naam van de gewenste API en klik op de **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="640c4-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![API-beveiliging][api-management-api-security]

<span data-ttu-id="640c4-141">Selecteer **clientcertificaten** van de **met referenties** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="640c4-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Clientcertificaten][api-management-mutual-certificates]

<span data-ttu-id="640c4-143">Selecteer het gewenste certificaat van de **clientcertificaat** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="640c4-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="640c4-144">Als er meerdere certificaten kunt u het onderwerp of de laatste vier tekens van de vingerafdruk zoals aangegeven in de vorige sectie om te bepalen van het juiste certificaat kijken.</span><span class="sxs-lookup"><span data-stu-id="640c4-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Selecteer het certificaat][api-management-select-certificate]

<span data-ttu-id="640c4-146">Klik op **opslaan** wijzigen van de configuratie opslaan in de API.</span><span class="sxs-lookup"><span data-stu-id="640c4-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="640c4-147">Deze wijziging wordt onmiddellijk van kracht en aanroepen naar de bewerkingen van deze API gebruikt het certificaat te verifiëren op de back-endserver.</span><span class="sxs-lookup"><span data-stu-id="640c4-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Sla de wijzigingen van de API][api-management-save-api]

> <span data-ttu-id="640c4-149">Wanneer een certificaat voor gatewayverificatie voor de back-end-service van een API is opgegeven, wordt een onderdeel van het beleid voor die API en kunnen worden weergegeven in de beleidseditor.</span><span class="sxs-lookup"><span data-stu-id="640c4-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Certificaatbeleid][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="640c4-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="640c4-151">Next steps</span></span>
<span data-ttu-id="640c4-152">Zie voor meer informatie over andere manieren voor het beveiligen van uw back-endservice zoals HTTP basic of gedeelde geheime-verificatie, de volgende video.</span><span class="sxs-lookup"><span data-stu-id="640c4-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



