---
title: aaaHow tooconfigure een toepassing toepassingsproxy | Microsoft Docs
description: Meer informatie over hoe toocreate een configureren van een toepassing toepassingsproxy in een paar eenvoudige stappen
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="cb3cb-103">Hoe een toepassing toepassingsproxy tooconfigure</span><span class="sxs-lookup"><span data-stu-id="cb3cb-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="cb3cb-104">In dit artikel kunt u toounderstand hoe een toepassing toepassingsproxy in Azure AD-tooexpose tooconfigure uw lokale toepassingen toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="cb3cb-105">Aanbevolen documenten</span><span class="sxs-lookup"><span data-stu-id="cb3cb-105">Recommended documents</span></span> 

<span data-ttu-id="cb3cb-106">toolearn over Hallo initiële configuraties en het maken van een toepassing toepassingsproxy via Hallo-beheerportal, volg Hallo [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="cb3cb-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="cb3cb-107">Zie voor meer informatie over het configureren van Connectors [toepassingsproxy inschakelen in Azure-portal Hallo](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="cb3cb-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="cb3cb-108">Zie voor meer informatie over het uploaden van certificaten en gebruiken van aangepaste domeinen [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="cb3cb-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="cb3cb-109">Hallo toepassingsinstelling/Hallo-URL's maken</span><span class="sxs-lookup"><span data-stu-id="cb3cb-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="cb3cb-110">Als u volgt Hallo stappen voor het Hallo [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentatie en weet Hallo foutdetails voor informatie en suggesties voor het ophalen van een fout bij het maken van de toepassing hello, Zie toofix Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="cb3cb-111">De meeste foutberichten bevatten een voorgestelde oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="cb3cb-112">veelvoorkomende fouten tooavoid, controleert u of:</span><span class="sxs-lookup"><span data-stu-id="cb3cb-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="cb3cb-113">U bent een beheerder met de machtiging toocreate een toepassingsproxy-toepassing</span><span class="sxs-lookup"><span data-stu-id="cb3cb-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="cb3cb-114">Interne URL Hallo is uniek.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="cb3cb-115">de externe URL Hallo is uniek.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-115">hello external URL is unique</span></span>

-   <span data-ttu-id="cb3cb-116">Hallo URL's starten met http of https en eindigen met een "/"</span><span class="sxs-lookup"><span data-stu-id="cb3cb-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="cb3cb-117">Hallo-URL moet een domeinnaam, geen IP-adres</span><span class="sxs-lookup"><span data-stu-id="cb3cb-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="cb3cb-118">Fout bij het Hallo-bericht moet worden weergegeven in de rechterbovenhoek Hallo wanneer u de toepassing hello maakt.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="cb3cb-119">U kunt ook Hallo melding pictogram toosee Hallo foutberichten selecteren.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="cb3cb-121">Connectors/connector groepen configureren</span><span class="sxs-lookup"><span data-stu-id="cb3cb-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="cb3cb-122">Als u problemen bij het configureren van uw toepassing vanwege een waarschuwing over Hallo connectors en connector groepen ondervindt, raadpleegt u instructies over het inschakelen van toepassingsproxy voor meer informatie over het toodownload connectors.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="cb3cb-123">Als u meer informatie over connectors toolearn wilt, raadpleegt u Hallo [connectors documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="cb3cb-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="cb3cb-124">Als uw connectors niet actief zijn, betekent dit dat ze niet kan tooreach Hallo service zijn.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="cb3cb-125">Dit is vaak omdat niet alle vereiste Hallo poorten geopend zijn.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="cb3cb-126">een lijst met vereiste poorten toosee Zie Hallo vereisten sectie Hallo documentatie toepassingsproxy inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="cb3cb-127">Certificaten voor aangepaste domeinen uploaden</span><span class="sxs-lookup"><span data-stu-id="cb3cb-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="cb3cb-128">Aangepaste domeinen toestaan toospecify Hallo domein van de externe URL's.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="cb3cb-129">toouse aangepaste domeinen, moet u tooupload Hallo certificaat voor dat domein.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="cb3cb-130">Zie voor meer informatie over het gebruik van aangepaste domeinen en certificaten [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="cb3cb-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="cb3cb-131">Als er problemen zijn uw certificaat uploaden, zoekt u Hallo foutberichten in de portal Hallo voor meer informatie over Hallo probleem is met Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="cb3cb-132">Algemene problemen met de certificaten zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="cb3cb-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="cb3cb-133">Verlopen certificaat</span><span class="sxs-lookup"><span data-stu-id="cb3cb-133">Expired certificate</span></span>

-   <span data-ttu-id="cb3cb-134">Certificaat is zelfondertekend</span><span class="sxs-lookup"><span data-stu-id="cb3cb-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="cb3cb-135">Certificaat ontbreekt Hallo persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="cb3cb-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="cb3cb-136">Hallo-berichtweergave van fouten in Hallo rechterbovenhoek als u tooupload Hallo certificaat probeert.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="cb3cb-137">U kunt ook Hallo melding pictogram toosee Hallo foutberichten selecteren.</span><span class="sxs-lookup"><span data-stu-id="cb3cb-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="cb3cb-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb3cb-139">Next steps</span></span>
[<span data-ttu-id="cb3cb-140">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="cb3cb-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
