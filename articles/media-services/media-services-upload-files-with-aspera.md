---
title: aaaUpload bestanden naar een Azure Media Services-account met behulp van Aspera | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het uploaden van bestanden in een opslagaccount dat is gekoppeld aan een Media Services-account met behulp van Hallo ** Aspera Server op aanvraag **-service op Azure.
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="08e02-103">Bestanden uploaden naar een Media Services-account met Hallo Aspera Server On Demand-service op Azure</span><span class="sxs-lookup"><span data-stu-id="08e02-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="08e02-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="08e02-104">Overview</span></span>

<span data-ttu-id="08e02-105">**Aspera** is software die een snelle bestandsoverdracht mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="08e02-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="08e02-106">**Aspera Server On Demand** voor Azure maakt snel uploaden en downloaden van grote bestanden rechtstreeks in Azure Blob-objectopslag mogelijk.</span><span class="sxs-lookup"><span data-stu-id="08e02-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="08e02-107">Voor informatie over **Aspera On Demand**, Zie Hallo [Aspera Cloud](http://cloud.asperasoft.com/) site.</span><span class="sxs-lookup"><span data-stu-id="08e02-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="08e02-108">**Aspera Server On Demand** voor Azure gekocht bij Hallo is [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="08e02-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="08e02-109">In volgorde toocomplete een aankoop van **Aspera Server On Demand** voor Azure, meld u in Azure Marketplace met uw Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="08e02-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="08e02-110">Deze zelfstudie wordt u begeleid Hallo stappen voor het uploaden van bestanden in een opslagaccount dat is gekoppeld aan een Media Services-account met behulp van Hallo **Aspera Server On Demand** service op Azure.</span><span class="sxs-lookup"><span data-stu-id="08e02-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="08e02-111">U vindt een voorbeeld ziet u hoe toouse Azure werkt met Aspera en Media Services [hier](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="08e02-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="08e02-112">Er is een limiet toohello maximale bestandsgrootte ondersteund voor de verwerking met Azure Media Services-mediaprocessoren (Management Packs).</span><span class="sxs-lookup"><span data-stu-id="08e02-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="08e02-113">Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="08e02-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="08e02-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="08e02-114">Prerequisites</span></span> 

<span data-ttu-id="08e02-115">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="08e02-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="08e02-116">Een Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="08e02-116">A Windows Live ID</span></span>
* <span data-ttu-id="08e02-117">Een [Azure-account](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="08e02-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="08e02-118">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="08e02-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="08e02-119">Een [Azure Media Services-account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="08e02-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="08e02-120">Aspera On Demand kopen voor Azure</span><span class="sxs-lookup"><span data-stu-id="08e02-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="08e02-121">Zodra u hebt geregistreerd in Azure Marketplace, volgt u deze basisstappen toocomplete uw aanschaf van Aspera On Demand voor Azure.</span><span class="sxs-lookup"><span data-stu-id="08e02-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="08e02-122">Zoek naar Aspera en selecteer 'Server On Demand'.</span><span class="sxs-lookup"><span data-stu-id="08e02-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="08e02-124">Hallo-abonnementen en klik op Sign Up</span><span class="sxs-lookup"><span data-stu-id="08e02-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="08e02-126">Vul in het Hallo-specifieke informatie voor uw Server op verzoek-abonnement.</span><span class="sxs-lookup"><span data-stu-id="08e02-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="08e02-128">Klik op Hallo **prijscategorie** in en selecteer de gewenste maandelijkse volume Hallo sub Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="08e02-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="08e02-129">In Hallo **plannen details** Configuratiescherm, selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="08e02-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="08e02-130">Klik op Hallo **Kies uw prijscategorie** -scherm, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="08e02-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="08e02-132">Klik op **juridische voorwaarden** tooview en accepteer de juridische bepalingen Hallo Hallo sub Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="08e02-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="08e02-133">Nadat u de juridische voorwaarden Hallo hebt bekeken, klikt u op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="08e02-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="08e02-135">Hallo aankoop voltooien door te klikken op **maken**.</span><span class="sxs-lookup"><span data-stu-id="08e02-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="08e02-137">Hello Azure-dashboard wordt aangekondigd dat het Hallo-service is ingericht.</span><span class="sxs-lookup"><span data-stu-id="08e02-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="08e02-138">Zodra deze is voltooid met het leveren, kunt u Hallo nieuw abonnement vinden door te zoeken in uw resources voor Hallo-naam van het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="08e02-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="08e02-139">Als u Hallo-service, dubbele klik erop toolaunch Hallo service management-portal gevonden hebt.</span><span class="sxs-lookup"><span data-stu-id="08e02-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="08e02-141">Start Hallo Aspera-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="08e02-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="08e02-142">Als u uw nieuwe Aspera-service hebt gevonden, krijgt u toegang toohello-beheerportal door te klikken op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="08e02-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="08e02-143">Er wordt een nieuw deelvenster geopend.</span><span class="sxs-lookup"><span data-stu-id="08e02-143">A new panel will be launched.</span></span> <span data-ttu-id="08e02-144">Uit binnen die nieuw deelvenster, moet u tooclick op Hallo **resourcenaam** van uw nieuwe service.</span><span class="sxs-lookup"><span data-stu-id="08e02-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="08e02-145">In Hallo schermafbeelding te volgen, is het Hallo-resourcenaam 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="08e02-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="08e02-146">Zodra u op Hallo Resourcenaam klikt, wordt een ander deelvenster wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="08e02-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="08e02-147">In het nieuwe deelvenster ziet u een koppeling 'Beheren'.</span><span class="sxs-lookup"><span data-stu-id="08e02-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="08e02-148">Klik op Hallo 'Beheren' koppeling toolaunch hello Aspera-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="08e02-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="08e02-150">Door te klikken op Hallo beheren koppeling, krijgt u de registratiepagina toohello, die vereist is tooaccess Hallo service.</span><span class="sxs-lookup"><span data-stu-id="08e02-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="08e02-152">U hebt nu toegang toohello Aspera service management-portal, kunt u toegangstoetsen maken, downloaden clients Aspera en licenties, adresgebruik weergeven en meer informatie over Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="08e02-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="08e02-153">Hallo toont volgende schermafbeelding Hallo toegang maken.</span><span class="sxs-lookup"><span data-stu-id="08e02-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="08e02-155">Hallo toont volgende schermafbeelding Hallo gebruiksrapportage-interfaces in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="08e02-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="08e02-157">Bestanden uploaden met Aspera</span><span class="sxs-lookup"><span data-stu-id="08e02-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="08e02-158">Download en installeer Hallo Aspera clientsoftware:</span><span class="sxs-lookup"><span data-stu-id="08e02-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="08e02-159">Invoegtoepassing browser</span><span class="sxs-lookup"><span data-stu-id="08e02-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="08e02-160">Rich client</span><span class="sxs-lookup"><span data-stu-id="08e02-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="08e02-161">Voer uw eerste overdracht uit.</span><span class="sxs-lookup"><span data-stu-id="08e02-161">Make your first transfer.</span></span> <span data-ttu-id="08e02-162">In de volgorde toouse hello Aspera client tootransfer Hello Aspera transfer-service moet u toocomplete Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="08e02-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="08e02-163">Maak een toegangssleutel met Hallo Aspera portal.</span><span class="sxs-lookup"><span data-stu-id="08e02-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="08e02-164">Downloaden, installeren en licentie Hallo Aspera client (software kunt u vinden in Hallo Aspera portal).</span><span class="sxs-lookup"><span data-stu-id="08e02-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="08e02-165">Lees Hallo Aspera client-handleiding voor configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="08e02-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="08e02-166">Sommige gegevens van uw opslagaccount die is gekoppeld aan uw Azure-Media-Account met Hallo ophalen [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08e02-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="08e02-167">In het bijzonder naam en sleutel en naam Hallo opslag blob-container in toowhich gewenste tooplace uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="08e02-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="08e02-168">tooget hello opslag info van Hallo-portal: vinden uw storage-account, klikt u op Hallo toegangstoetsen en kopiëren Hallo naam en het Hallo-sleutel van uw account.</span><span class="sxs-lookup"><span data-stu-id="08e02-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="08e02-169">tooget hello containernaam: vinden van uw opslagaccount, selecteer **Blobs**, selecteer Hallo-naam van Hallo-container die u wilt dat tooupload Hallo inhoud in.</span><span class="sxs-lookup"><span data-stu-id="08e02-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="08e02-170">Hieronder vindt u Hallo schermopname van Hallo Aspera client **Verbindingsbeheer** waarin u de 'Azure' opslagtype Hallo en referenties, evenals Hallo blob-container moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="08e02-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="08e02-172">Resources</span><span class="sxs-lookup"><span data-stu-id="08e02-172">Resources</span></span>

<span data-ttu-id="08e02-173">Hallo volgende resources zijn vermeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="08e02-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="08e02-174">Connect Browser Plugin</span><span class="sxs-lookup"><span data-stu-id="08e02-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="08e02-175">Connect-handleiding</span><span class="sxs-lookup"><span data-stu-id="08e02-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="08e02-176">Aspera-client</span><span class="sxs-lookup"><span data-stu-id="08e02-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="08e02-177">Clienthandleiding</span><span class="sxs-lookup"><span data-stu-id="08e02-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="08e02-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08e02-178">Next steps</span></span>

<span data-ttu-id="08e02-179">U kunt nu [blobs vanuit een opslagaccount kopiëren naar een AMS-account](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="08e02-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="08e02-180">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="08e02-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="08e02-181">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="08e02-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

