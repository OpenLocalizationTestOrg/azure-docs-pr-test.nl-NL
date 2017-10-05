---
title: Het configureren van een toepassing toepassingsproxy | Microsoft Docs
description: Informatie over het maken van een configureren een toepassingsproxy-toepassing in een paar eenvoudige stappen
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="38fb6-103">Het configureren van een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="38fb6-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="38fb6-104">In dit artikel helpt u bij het begrijpen van het configureren van een toepassing toepassingsproxy in Azure AD om uw on-premises toepassingen naar de cloud weer te geven.</span><span class="sxs-lookup"><span data-stu-id="38fb6-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="38fb6-105">Aanbevolen documenten</span><span class="sxs-lookup"><span data-stu-id="38fb6-105">Recommended documents</span></span> 

<span data-ttu-id="38fb6-106">Voor meer informatie over de eerste configuraties en het maken van een toepassing toepassingsproxy via de beheerportal, volgt u de [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="38fb6-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="38fb6-107">Zie voor meer informatie over het configureren van Connectors [toepassingsproxy inschakelen in de Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="38fb6-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="38fb6-108">Zie voor meer informatie over het uploaden van certificaten en gebruiken van aangepaste domeinen [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="38fb6-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="38fb6-109">De URL's voor de toepassingsinstelling maken</span><span class="sxs-lookup"><span data-stu-id="38fb6-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="38fb6-110">Als u volgt de stappen in de [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentatie en zijn voor het ophalen van een fout bij het maken van de toepassing, Zie de foutdetails voor informatie en suggesties voor het oplossen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="38fb6-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="38fb6-111">De meeste foutberichten bevatten een voorgestelde oplossing.</span><span class="sxs-lookup"><span data-stu-id="38fb6-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="38fb6-112">Controleer of algemene fouten te voorkomen:</span><span class="sxs-lookup"><span data-stu-id="38fb6-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="38fb6-113">U bent een beheerder met een machtiging voor het maken van een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="38fb6-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="38fb6-114">De interne URL is uniek.</span><span class="sxs-lookup"><span data-stu-id="38fb6-114">The internal URL is unique</span></span>

-   <span data-ttu-id="38fb6-115">De externe URL is uniek.</span><span class="sxs-lookup"><span data-stu-id="38fb6-115">The external URL is unique</span></span>

-   <span data-ttu-id="38fb6-116">De URL's met http of https beginnen en eindigen met een "/"</span><span class="sxs-lookup"><span data-stu-id="38fb6-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="38fb6-117">De URL moet een domeinnaam, geen IP-adres</span><span class="sxs-lookup"><span data-stu-id="38fb6-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="38fb6-118">Het foutbericht moet worden weergegeven in de rechterbovenhoek bij het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="38fb6-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="38fb6-119">U kunt ook het meldingspictogram voor de foutberichten selecteren.</span><span class="sxs-lookup"><span data-stu-id="38fb6-119">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="38fb6-121">Connectors/connector groepen configureren</span><span class="sxs-lookup"><span data-stu-id="38fb6-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="38fb6-122">Als u problemen bij het configureren van uw toepassing vanwege een waarschuwing over connectors en connector groepen ondervindt, raadpleegt u de instructies op de toepassingsproxy inschakelen voor meer informatie over het downloaden van connectors.</span><span class="sxs-lookup"><span data-stu-id="38fb6-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="38fb6-123">Als u weten over connectors wilt, raadpleegt u de [connectors documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="38fb6-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="38fb6-124">Als uw connectors niet actief zijn, betekent dit dat ze niet bereiken van de service zijn.</span><span class="sxs-lookup"><span data-stu-id="38fb6-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="38fb6-125">Dit is vaak omdat niet de vereiste poorten geopend zijn.</span><span class="sxs-lookup"><span data-stu-id="38fb6-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="38fb6-126">Een lijst met vereiste poorten, Zie de sectie vereisten van de documentatie van de toepassingsproxy inschakelen.</span><span class="sxs-lookup"><span data-stu-id="38fb6-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="38fb6-127">Certificaten voor aangepaste domeinen uploaden</span><span class="sxs-lookup"><span data-stu-id="38fb6-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="38fb6-128">Aangepaste domeinen kunnen u het domein van de externe URL's opgeven.</span><span class="sxs-lookup"><span data-stu-id="38fb6-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="38fb6-129">Voor het gebruik van aangepaste domeinen, moet u het certificaat voor dat domein uploaden.</span><span class="sxs-lookup"><span data-stu-id="38fb6-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="38fb6-130">Zie voor meer informatie over het gebruik van aangepaste domeinen en certificaten [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="38fb6-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="38fb6-131">Als er problemen zijn uw certificaat uploaden, zoekt u de foutberichten in de portal voor meer informatie over het probleem met het certificaat.</span><span class="sxs-lookup"><span data-stu-id="38fb6-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="38fb6-132">Algemene problemen met de certificaten zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="38fb6-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="38fb6-133">Verlopen certificaat</span><span class="sxs-lookup"><span data-stu-id="38fb6-133">Expired certificate</span></span>

-   <span data-ttu-id="38fb6-134">Certificaat is zelfondertekend</span><span class="sxs-lookup"><span data-stu-id="38fb6-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="38fb6-135">Certificaat ontbreekt voor de persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="38fb6-135">Certificate is missing the private key</span></span>

<span data-ttu-id="38fb6-136">Het foutbericht wordt weergegeven in de rechterbovenhoek als u probeert om het certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="38fb6-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="38fb6-137">U kunt ook het meldingspictogram voor de foutberichten selecteren.</span><span class="sxs-lookup"><span data-stu-id="38fb6-137">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="38fb6-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38fb6-139">Next steps</span></span>
[<span data-ttu-id="38fb6-140">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="38fb6-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
