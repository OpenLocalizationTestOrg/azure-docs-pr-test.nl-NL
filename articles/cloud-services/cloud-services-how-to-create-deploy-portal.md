---
title: aaaHow toocreate en implementeren van een service in de cloud | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van een cloudservice met hello Azure-portal.
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
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="78584-103">Hoe toocreate en implementeren van een service in de cloud</span><span class="sxs-lookup"><span data-stu-id="78584-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78584-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78584-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="78584-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78584-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="78584-106">Hello Azure portal biedt twee manieren u toocreate en implementeren van een cloudservice: *snelle invoer* en *aangepast maken*.</span><span class="sxs-lookup"><span data-stu-id="78584-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="78584-107">Dit artikel wordt uitgelegd hoe toouse Hallo toocreate snelle invoer voor methode een nieuwe cloudservice en gebruik vervolgens **uploaden** tooupload en implementeren van een cloud service-pakket in Azure.</span><span class="sxs-lookup"><span data-stu-id="78584-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="78584-108">Wanneer u deze methode gebruikt, kunt u hello Azure-portal beschikbaar handige koppelingen voor het voltooien van alle vereisten die u gaat.</span><span class="sxs-lookup"><span data-stu-id="78584-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="78584-109">Als u klaar toodeploy uw cloud service bent wanneer u dit hebt gemaakt, kunt u zowel op Hallo doen met behulp van aangepast maken tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="78584-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="78584-110">Als u van plan bent toopublish uw cloudservice vanuit Visual Studio Team Services (VSTS), snel kunt maken en vervolgens VSTS publiceren vanuit de Azure Quickstart of Hallo dashboard Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="78584-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="78584-111">Zie voor meer informatie [continue levering tooAzure door met behulp van Visual Studio Team Services][TFSTutorialForCloudService], of Zie help voor Hallo **Quick Start** pagina.</span><span class="sxs-lookup"><span data-stu-id="78584-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="78584-112">Concepten</span><span class="sxs-lookup"><span data-stu-id="78584-112">Concepts</span></span>
<span data-ttu-id="78584-113">Drie onderdelen zijn vereist toodeploy een toepassing als een cloudservice in Azure:</span><span class="sxs-lookup"><span data-stu-id="78584-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="78584-114">**Servicedefinitie**</span><span class="sxs-lookup"><span data-stu-id="78584-114">**Service Definition**</span></span>  
  <span data-ttu-id="78584-115">Hallo cloud servicedefinitiebestand (.csdef) definieert Hallo-servicemodel, waaronder het aantal rollen Hallo.</span><span class="sxs-lookup"><span data-stu-id="78584-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="78584-116">**Configuratie van de service**</span><span class="sxs-lookup"><span data-stu-id="78584-116">**Service Configuration**</span></span>  
  <span data-ttu-id="78584-117">Hallo cloud service-configuratiebestand (.cscfg) biedt configuratie-instellingen voor het Hallo-cloudservice en de afzonderlijke rollen, met inbegrip van het aantal rolinstanties Hallo.</span><span class="sxs-lookup"><span data-stu-id="78584-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="78584-118">**Servicepakket**</span><span class="sxs-lookup"><span data-stu-id="78584-118">**Service Package**</span></span>  
  <span data-ttu-id="78584-119">Hallo-service-pakket (.cspkg) bevat Hallo toepassingscode en configuraties en het servicedefinitiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="78584-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="78584-120">U kunt meer informatie over deze en hoe een pakket toocreate [hier](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="78584-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="78584-121">Voorbereiden van uw app</span><span class="sxs-lookup"><span data-stu-id="78584-121">Prepare your app</span></span>
<span data-ttu-id="78584-122">Voordat u een cloudservice implementeren kunt, moet u Hallo cloud service-pakket (.cspkg) van uw toepassingscode en een cloud service-configuratiebestand (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="78584-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="78584-123">Hello Azure SDK biedt hulpprogramma's voor het voorbereiden van deze bestanden vereiste implementatie.</span><span class="sxs-lookup"><span data-stu-id="78584-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="78584-124">U kunt vanuit Hallo Hallo SDK installeren [Azure downloadt](https://azure.microsoft.com/downloads/) pagina in Hallo taal waarin u toodevelop liever uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="78584-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="78584-125">Drie functies van de cloud zijn speciale configuraties vereist voordat u een servicepakket exporteren:</span><span class="sxs-lookup"><span data-stu-id="78584-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="78584-126">Als u wilt dat een cloudservice die gebruikmaakt van Secure Sockets Layer (SSL) om gegevens te coderen, toodeploy [uw toepassing configureren](cloud-services-configure-ssl-certificate-portal.md#modify) voor SSL.</span><span class="sxs-lookup"><span data-stu-id="78584-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="78584-127">Als u wilt dat tooconfigure extern bureaublad-verbindingen toorole exemplaren [Hallo rollen configureren](cloud-services-role-enable-remote-desktop-new-portal.md) voor extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="78584-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="78584-128">Als u tooconfigure uitgebreide bewaking voor uw cloudservice wilt, schakelt u Azure Diagnostics voor Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="78584-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="78584-129">*Minimale bewaking* (Hallo standaard niveau bewaking) maakt gebruik van prestatiemeteritems die afkomstig zijn van Hallo hostbesturingssystemen voor rolexemplaren (virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="78584-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="78584-130">*Uitgebreide bewaking* aanvullende gegevens op basis van prestatiegegevens binnen Hallo rol exemplaren tooenable dichter analyse van problemen die tijdens de verwerking van de toepassing optreden moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="78584-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="78584-131">toofind hoe tooenable Azure Diagnostics, Zie [inschakelen van diagnostische gegevens in Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="78584-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="78584-132">een cloudservice met implementaties van webrollen of werkrollen toocreate, moet u [Hallo servicepakket maken](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="78584-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="78584-133">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="78584-133">Before you begin</span></span>
* <span data-ttu-id="78584-134">Als u hello Azure SDK nog niet hebt geïnstalleerd, klikt u op **Azure SDK installeren** tooopen hello [pagina Azure Downloads](https://azure.microsoft.com/downloads/), en download vervolgens het Hallo-SDK voor Hallo taal waarin u liever toodevelop uw code.</span><span class="sxs-lookup"><span data-stu-id="78584-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="78584-135">(U hebt een kans toodo dit later.)</span><span class="sxs-lookup"><span data-stu-id="78584-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="78584-136">Als alle rolinstanties een certificaat vereist, maakt u Hallo certificaten.</span><span class="sxs-lookup"><span data-stu-id="78584-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="78584-137">Cloudservices moeten een pfx-bestand met een persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="78584-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="78584-138">Bij het maken en implementeren Hallo-cloudservice, kunt u Hallo certificaten tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="78584-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="78584-139">Maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="78584-139">Create and deploy</span></span>
1. <span data-ttu-id="78584-140">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="78584-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="78584-141">Klik op **Nieuw > berekenen**, en schuif omlaag tooand Klik **Cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="78584-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="78584-143">In de nieuwe Hallo **Cloudservice** blade, voer een waarde voor Hallo **DNS-naam**.</span><span class="sxs-lookup"><span data-stu-id="78584-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="78584-144">Maak een nieuwe **resourcegroep** of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="78584-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="78584-145">Selecteer een **locatie**.</span><span class="sxs-lookup"><span data-stu-id="78584-145">Select a **Location**.</span></span>
6. <span data-ttu-id="78584-146">Klik op **pakket**.</span><span class="sxs-lookup"><span data-stu-id="78584-146">Click **Package**.</span></span> <span data-ttu-id="78584-147">Hiermee opent u Hallo **uploaden van een pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="78584-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="78584-148">Vul de velden Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="78584-148">Fill in hello required fields.</span></span> <span data-ttu-id="78584-149">Als een van de rollen één exemplaar bevatten, zorg er dan **toch implementeren als een of meer rollen met één exemplaar** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="78584-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="78584-150">Zorg ervoor dat **implementatie Start** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="78584-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="78584-151">Klik op **OK** die hello wordt gesloten **uploaden van een pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="78584-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="78584-152">Als u certificaten tooadd niet hebt, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="78584-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="78584-154">Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="78584-154">Upload a certificate</span></span>
<span data-ttu-id="78584-155">Als uw implementatiepakket [toouse certificaten geconfigureerd](cloud-services-configure-ssl-certificate-portal.md#modify), kunt u nu Hallo-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="78584-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="78584-156">Selecteer **certificaten**, en op Hallo **certificaten toevoegen** blade Hallo SSL-certificaat pfx-bestand selecteren en geef vervolgens Hallo **wachtwoord** voor Hallo-certificaat</span><span class="sxs-lookup"><span data-stu-id="78584-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="78584-157">Klik op **Attach certificaat**, en klik vervolgens op **OK** op Hallo **certificaten toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="78584-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="78584-158">Klik op **maken** op Hallo **Cloudservice** blade.</span><span class="sxs-lookup"><span data-stu-id="78584-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="78584-159">Wanneer de implementatie van Hallo Hallo heeft bereikt **gereed** status, kunt u de volgende stappen toohello doorgaan.</span><span class="sxs-lookup"><span data-stu-id="78584-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="78584-161">Controleer of de implementatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="78584-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="78584-162">Klik op Hallo cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="78584-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="78584-163">Hallo status moet worden weergegeven dat Hallo-service is **met**.</span><span class="sxs-lookup"><span data-stu-id="78584-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="78584-164">Onder **Essentials**, klikt u op Hallo **Site-URL** tooopen uw cloud-service in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="78584-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="78584-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78584-166">Next steps</span></span>
* <span data-ttu-id="78584-167">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78584-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="78584-168">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78584-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="78584-169">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78584-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="78584-170">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78584-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
