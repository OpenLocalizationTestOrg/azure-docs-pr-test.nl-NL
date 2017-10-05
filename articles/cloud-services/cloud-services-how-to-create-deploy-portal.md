---
title: Het maken en implementeren van een service in de cloud | Microsoft Docs
description: Informatie over het maken en implementeren van een cloudservice met de Azure portal.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="e5a4a-103">Het maken en implementeren van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="e5a4a-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5a4a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e5a4a-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="e5a4a-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e5a4a-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="e5a4a-106">De Azure portal biedt twee manieren maken en implementeren van een cloudservice: *snelle invoer* en *aangepast maken*.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="e5a4a-107">In dit artikel wordt uitgelegd hoe u een nieuwe cloudservice maken en vervolgens gebruiken met de methode Snelle invoer **uploaden** om te uploaden en implementeren van een cloud service-pakket in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="e5a4a-108">Wanneer u deze methode gebruikt, kunt u de Azure-portal beschikbaar handige koppelingen voor het voltooien van alle vereisten die u gaat.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="e5a4a-109">Als u klaar bent om uw cloudservice implementeren wanneer u dit hebt gemaakt, kunt u beide op hetzelfde moment met behulp van aangepast maken kunt doen.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="e5a4a-110">Als u van plan bent voor het publiceren van uw cloudservice vanuit Visual Studio Team Services (VSTS), snel kunt maken en vervolgens publiceren VSTS instellen van de Azure Quickstart of het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="e5a4a-111">Zie voor meer informatie [continue levering naar Azure met behulp van Visual Studio Team Services][TFSTutorialForCloudService], of Zie help voor de **Quick Start** pagina.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="e5a4a-112">Concepten</span><span class="sxs-lookup"><span data-stu-id="e5a4a-112">Concepts</span></span>
<span data-ttu-id="e5a4a-113">Drie onderdelen zijn vereist voor het implementeren van een toepassing als een cloudservice in Azure:</span><span class="sxs-lookup"><span data-stu-id="e5a4a-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="e5a4a-114">**Servicedefinitie**</span><span class="sxs-lookup"><span data-stu-id="e5a4a-114">**Service Definition**</span></span>  
  <span data-ttu-id="e5a4a-115">Het cloud-servicedefinitiebestand (.csdef) definieert het servicemodel, inclusief het aantal rollen.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="e5a4a-116">**Configuratie van de service**</span><span class="sxs-lookup"><span data-stu-id="e5a4a-116">**Service Configuration**</span></span>  
  <span data-ttu-id="e5a4a-117">Het configuratiebestand (.cscfg) van een cloud-service bevat configuratie-instellingen voor de cloud service en afzonderlijke rollen, met inbegrip van het aantal rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="e5a4a-118">**Servicepakket**</span><span class="sxs-lookup"><span data-stu-id="e5a4a-118">**Service Package**</span></span>  
  <span data-ttu-id="e5a4a-119">Het servicepakket (.cspkg) bevat de toepassingscode en configuraties en het servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="e5a4a-120">U kunt meer informatie over deze en het maken van een pakket [hier](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="e5a4a-121">Voorbereiden van uw app</span><span class="sxs-lookup"><span data-stu-id="e5a4a-121">Prepare your app</span></span>
<span data-ttu-id="e5a4a-122">Voordat u een cloudservice implementeren kunt, moet u het pakket in de cloud-service (.cspkg) maken van uw toepassingscode en een cloud service-configuratiebestand (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="e5a4a-123">De Azure SDK biedt hulpprogramma's voor het voorbereiden van deze bestanden vereiste implementatie.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="e5a4a-124">U kunt installeren de SDK van de [Azure downloadt](https://azure.microsoft.com/downloads/) pagina in de taal waarin u wilt ontwikkelen van uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="e5a4a-125">Drie functies van de cloud zijn speciale configuraties vereist voordat u een servicepakket exporteren:</span><span class="sxs-lookup"><span data-stu-id="e5a4a-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="e5a4a-126">Als u wilt implementeren van een cloudservice die gebruikmaakt van Secure Sockets Layer (SSL) om gegevens te coderen, [uw toepassing configureren](cloud-services-configure-ssl-certificate-portal.md#modify) voor SSL.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="e5a4a-127">Als u wilt configureren van extern bureaublad-verbindingen met rolinstanties, [configureren van de rollen](cloud-services-role-enable-remote-desktop-new-portal.md) voor extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="e5a4a-128">Als u wilt voor het configureren van uitgebreide bewaking voor uw cloudservice, moet u Azure diagnostische gegevens inschakelen voor de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="e5a4a-129">*Minimale bewaking* (de standaardinstelling niveau bewaking) maakt gebruik van prestatiemeteritems die afkomstig zijn van de host-besturingssystemen voor rolexemplaren (virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="e5a4a-130">*Uitgebreide bewaking* aanvullende gegevens op basis van prestatiegegevens binnen de rolexemplaren om in te schakelen dichter analyse van problemen die tijdens de verwerking van de toepassing optreden moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="e5a4a-131">Zie voor meer informatie over het inschakelen van Azure Diagnostics, [inschakelen van diagnostische gegevens in Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="e5a4a-132">Maakt een cloudservice met implementaties van webrollen of werkrollen, moet u [maken het servicepakket](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e5a4a-133">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="e5a4a-133">Before you begin</span></span>
* <span data-ttu-id="e5a4a-134">Als u de Azure SDK nog niet hebt geïnstalleerd, klikt u op **Azure SDK installeren** openen de [pagina Azure Downloads](https://azure.microsoft.com/downloads/), en downloadt u de SDK voor de taal waarin u liever uw code te ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="e5a4a-135">(U hebt een kans om dit later doen.)</span><span class="sxs-lookup"><span data-stu-id="e5a4a-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="e5a4a-136">Als alle rolinstanties een certificaat vereist, maakt u de certificaten.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="e5a4a-137">Cloudservices moeten een pfx-bestand met een persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="e5a4a-138">Bij het maken en implementeren van de cloudservice, kunt u de certificaten uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="e5a4a-139">Maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="e5a4a-139">Create and deploy</span></span>
1. <span data-ttu-id="e5a4a-140">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e5a4a-141">Klik op **Nieuw > berekenen**, en schuif vervolgens omlaag naar en klikt u op **Cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="e5a4a-143">In het nieuwe **Cloudservice** blade, voer een waarde voor de **DNS-naam**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="e5a4a-144">Maak een nieuwe **resourcegroep** of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="e5a4a-145">Selecteer een **locatie**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-145">Select a **Location**.</span></span>
6. <span data-ttu-id="e5a4a-146">Klik op **pakket**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-146">Click **Package**.</span></span> <span data-ttu-id="e5a4a-147">Hiermee opent u de **uploaden van een pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="e5a4a-148">Vul de vereiste velden in.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-148">Fill in the required fields.</span></span> <span data-ttu-id="e5a4a-149">Als een van de rollen één exemplaar bevatten, zorg er dan **toch implementeren als een of meer rollen met één exemplaar** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="e5a4a-150">Zorg ervoor dat **implementatie Start** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="e5a4a-151">Klik op **OK** die wordt gesloten de **uploaden van een pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="e5a4a-152">Als u geen certificaten toevoegen, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="e5a4a-154">Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="e5a4a-154">Upload a certificate</span></span>
<span data-ttu-id="e5a4a-155">Als uw implementatiepakket [geconfigureerd voor het gebruik van certificaten](cloud-services-configure-ssl-certificate-portal.md#modify), kunt u het certificaat nu uploaden.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="e5a4a-156">Selecteer **certificaten**, en klik op de **certificaten toevoegen** blade, selecteert u het .pfx-bestand van de SSL-certificaat en geef vervolgens de **wachtwoord** voor het certificaat</span><span class="sxs-lookup"><span data-stu-id="e5a4a-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="e5a4a-157">Klik op **Attach certificaat**, en klik vervolgens op **OK** op de **certificaten toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="e5a4a-158">Klik op **maken** op de **Cloudservice** blade.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="e5a4a-159">Wanneer de implementatie heeft bereikt de **gereed** status, kunt u doorgaan met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="e5a4a-161">Controleer of de implementatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="e5a4a-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="e5a4a-162">Klik op het cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="e5a4a-163">De status moet worden weergegeven dat de service is **met**.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="e5a4a-164">Onder **Essentials**, klikt u op de **Site-URL** uw cloudservice openen in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e5a4a-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="e5a4a-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e5a4a-166">Next steps</span></span>
* <span data-ttu-id="e5a4a-167">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="e5a4a-168">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="e5a4a-169">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="e5a4a-170">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4a-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
