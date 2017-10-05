---
title: Bestanden uploaden naar een Azure Media Services-account met behulp van Aspera | Microsoft Docs
description: Deze zelfstudie wordt u door de stappen voor het uploaden van bestanden in een opslagaccount die is gekoppeld aan een Media Services-account met de ** Aspera Server op aanvraag **-service op Azure.
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
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="07f77-103">Bestanden uploaden naar een Media Services-account met behulp van de service Aspera Server On Demand in Azure</span><span class="sxs-lookup"><span data-stu-id="07f77-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="07f77-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="07f77-104">Overview</span></span>

<span data-ttu-id="07f77-105">**Aspera** is software die een snelle bestandsoverdracht mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="07f77-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="07f77-106">**Aspera Server On Demand** voor Azure maakt snel uploaden en downloaden van grote bestanden rechtstreeks in Azure Blob-objectopslag mogelijk.</span><span class="sxs-lookup"><span data-stu-id="07f77-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="07f77-107">Zie de [Aspera Cloud](http://cloud.asperasoft.com/)-site voor informatie over **Aspera On Demand**.</span><span class="sxs-lookup"><span data-stu-id="07f77-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="07f77-108">**Aspera Server On Demand** voor Azure is verkrijgbaar in [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="07f77-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="07f77-109">Om de aankoop van **Aspera Server On Demand** voor Azure te voltooien, meldt u zich aan bij Azure Marketplace met uw Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="07f77-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="07f77-110">In deze zelfstudie leert u stapsgewijs hoe u bestanden uploadt naar een opslagaccount dat is gekoppeld aan een Media Services-account met behulp van de service **Aspera Server On Demand** in Azure.</span><span class="sxs-lookup"><span data-stu-id="07f77-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="07f77-111">[Hier](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest) vindt u een voorbeeld waarin wordt uitgelegd hoe u Azure Functions gebruikt met Aspera en Media Services.</span><span class="sxs-lookup"><span data-stu-id="07f77-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="07f77-112">Er is een maximale bestandsgrootte voor de verwerking met Azure Media Services-mediaprocessors (mp's).</span><span class="sxs-lookup"><span data-stu-id="07f77-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="07f77-113">Raadpleeg [dit onderwerp](media-services-quotas-and-limitations.md) voor meer informatie over de maximale bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="07f77-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="07f77-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="07f77-114">Prerequisites</span></span> 

<span data-ttu-id="07f77-115">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="07f77-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="07f77-116">Een Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="07f77-116">A Windows Live ID</span></span>
* <span data-ttu-id="07f77-117">Een [Azure-account](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="07f77-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="07f77-118">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="07f77-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="07f77-119">Een [Azure Media Services-account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="07f77-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="07f77-120">Aspera On Demand kopen voor Azure</span><span class="sxs-lookup"><span data-stu-id="07f77-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="07f77-121">Nadat u zich hebt aangemeld bij Azure Marketplace, volgt u deze eenvoudige stappen om de aankoop van Aspera On Demand voor Azure te voltooien.</span><span class="sxs-lookup"><span data-stu-id="07f77-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="07f77-122">Zoek naar Aspera en selecteer 'Server On Demand'.</span><span class="sxs-lookup"><span data-stu-id="07f77-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="07f77-124">Bekijk de abonnementen en klik op 'Aanmelden'</span><span class="sxs-lookup"><span data-stu-id="07f77-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="07f77-126">Voer de gegevens voor het Server On Demand-abonnement in.</span><span class="sxs-lookup"><span data-stu-id="07f77-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="07f77-128">Klik op de **prijscategorie** en selecteer het gewenste maandelijkse volume in het deelvenster.</span><span class="sxs-lookup"><span data-stu-id="07f77-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="07f77-129">In het deelvenster **Plan details** (Abonnementsgegevens) selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="07f77-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="07f77-130">Klik in het deelvenster **Uw prijscategorie kiezen** op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="07f77-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="07f77-132">Klik op **Juridische voorwaarden** om de juridische voorwaarden in het deelvenster te bekijken en te accepteren.</span><span class="sxs-lookup"><span data-stu-id="07f77-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="07f77-133">Nadat u de juridische voorwaarden hebt gelezen, klikt u op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="07f77-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="07f77-135">Voltooi de aankoop door op **Maken** te klikken.</span><span class="sxs-lookup"><span data-stu-id="07f77-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="07f77-137">Op het Azure-dashboard wordt weergegeven dat de service wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="07f77-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="07f77-138">Wanneer het inrichten is voltooid, kunt u het nieuwe abonnement vinden door op de naam van de service te zoeken in uw resources.</span><span class="sxs-lookup"><span data-stu-id="07f77-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="07f77-139">Zodra u de service hebt gevonden, dubbelklikt u erop om de beheerportal van de service te openen.</span><span class="sxs-lookup"><span data-stu-id="07f77-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="07f77-141">Start de Aspera-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="07f77-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="07f77-142">Zodra u de nieuwe Aspera-service hebt gevonden, klikt u op de service om de beheerportal te openen.</span><span class="sxs-lookup"><span data-stu-id="07f77-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="07f77-143">Er wordt een nieuw deelvenster geopend.</span><span class="sxs-lookup"><span data-stu-id="07f77-143">A new panel will be launched.</span></span> <span data-ttu-id="07f77-144">Klik binnen het nieuwe deelvenster op de **resourcenaam** van uw nieuwe service.</span><span class="sxs-lookup"><span data-stu-id="07f77-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="07f77-145">De resourcenaam in de volgende schermafbeelding is 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="07f77-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="07f77-146">Zodra u op de resourcenaam klikt, wordt er een nieuw deelvenster geopend.</span><span class="sxs-lookup"><span data-stu-id="07f77-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="07f77-147">In het nieuwe deelvenster ziet u een koppeling 'Beheren'.</span><span class="sxs-lookup"><span data-stu-id="07f77-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="07f77-148">Klik op de koppeling 'Beheren' om de beheerportal van Aspera te openen.</span><span class="sxs-lookup"><span data-stu-id="07f77-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="07f77-150">Door op de koppeling 'Beheren' te klikken, wordt u naar de registratiepagina geleid. Deze is nodig om toegang te krijgen tot de service.</span><span class="sxs-lookup"><span data-stu-id="07f77-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="07f77-152">U hoort nu toegang te hebben tot de beheerportal van de Aspera-service. Hier kunt u toegangstoetsen maken, Aspera-clients en -licenties downloaden, het gebruik bekijken en meer informatie over de API's krijgen.</span><span class="sxs-lookup"><span data-stu-id="07f77-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="07f77-153">In de volgende schermafbeelding ziet u hoe toegang maken in zijn werk gaat.</span><span class="sxs-lookup"><span data-stu-id="07f77-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="07f77-155">In de volgende schermafbeelding ziet u de interfaces voor gebruiksrapporten in de portal.</span><span class="sxs-lookup"><span data-stu-id="07f77-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="07f77-157">Bestanden uploaden met Aspera</span><span class="sxs-lookup"><span data-stu-id="07f77-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="07f77-158">Download en installeer de clientsoftware van Aspera:</span><span class="sxs-lookup"><span data-stu-id="07f77-158">Download and install the Aspera client software:</span></span>
    
    * [<span data-ttu-id="07f77-159">Invoegtoepassing browser</span><span class="sxs-lookup"><span data-stu-id="07f77-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="07f77-160">Rich client</span><span class="sxs-lookup"><span data-stu-id="07f77-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="07f77-161">Voer uw eerste overdracht uit.</span><span class="sxs-lookup"><span data-stu-id="07f77-161">Make your first transfer.</span></span> <span data-ttu-id="07f77-162">Voer het volgende uit om de Aspera-client te gebruiken om overdrachten uit te voeren met de Aspera-overdrachtsservice:</span><span class="sxs-lookup"><span data-stu-id="07f77-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="07f77-163">Maak een toegangstoets via de Aspera-portal.</span><span class="sxs-lookup"><span data-stu-id="07f77-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="07f77-164">Download, installeer en licentieer de Aspera-client (de software vindt u in de Aspera-portal).</span><span class="sxs-lookup"><span data-stu-id="07f77-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="07f77-165">Lees de gids van de Aspera-client voor informatie over de configuratie.</span><span class="sxs-lookup"><span data-stu-id="07f77-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="07f77-166">Haal bepaalde gegevens van uw opslagaccount op die zijn gekoppeld aan uw Azure-media-account met behulp van [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="07f77-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="07f77-167">Specifiek gaat het om de naam en sleutel, en de naam van de opslag-blob-container waarin u uw inhoud wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="07f77-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="07f77-168">Opslaggegevens ophalen uit de portal: zoek uw opslagaccount, klik op de toegangstoetsen en kopieer de naam en sleutel van uw account.</span><span class="sxs-lookup"><span data-stu-id="07f77-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="07f77-169">De containernaam ophalen: zoek uw opslagaccount, selecteer **Blobs**, selecteer de naam van de container waarnaar u de inhoud wilt uploaden.</span><span class="sxs-lookup"><span data-stu-id="07f77-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="07f77-170">Hieronder ziet u een schermafbeelding van **Verbindingsbeheer** van de Aspera-client waarin u het type Azure-opslag en referenties dient op te geven, evenals de blob-container.</span><span class="sxs-lookup"><span data-stu-id="07f77-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="07f77-172">Resources</span><span class="sxs-lookup"><span data-stu-id="07f77-172">Resources</span></span>

<span data-ttu-id="07f77-173">De volgende resources zijn vermeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="07f77-173">The following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="07f77-174">Connect Browser Plugin</span><span class="sxs-lookup"><span data-stu-id="07f77-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="07f77-175">Connect-handleiding</span><span class="sxs-lookup"><span data-stu-id="07f77-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="07f77-176">Aspera-client</span><span class="sxs-lookup"><span data-stu-id="07f77-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="07f77-177">Clienthandleiding</span><span class="sxs-lookup"><span data-stu-id="07f77-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="07f77-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07f77-178">Next steps</span></span>

<span data-ttu-id="07f77-179">U kunt nu [blobs vanuit een opslagaccount kopiëren naar een AMS-account](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="07f77-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="07f77-180">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="07f77-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="07f77-181">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="07f77-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

