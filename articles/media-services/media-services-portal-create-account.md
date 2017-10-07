---
title: een Azure Media Services-account met hello Azure-portal aaaCreate | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het maken van een Azure Media Services-account met hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="d3b77-103">Een Azure Media Services-account maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d3b77-103">Create an Azure Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3b77-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d3b77-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="d3b77-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b77-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="d3b77-106">REST</span><span class="sxs-lookup"><span data-stu-id="d3b77-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="d3b77-107">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d3b77-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3b77-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="d3b77-109">Hello Azure-portal biedt een manier tooquickly account maken voor een Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="d3b77-109">hello Azure portal provides a way tooquickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="d3b77-110">U kunt uw account tooaccess Media Services die u toostore inschakelen, versleutelen, coderen, beheren en streamen van mediainhoud in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b77-110">You can use your account tooaccess Media Services that enable you toostore, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="d3b77-111">Tijdens Hallo maken van een Media Services-account, u ook een gekoppeld opslagaccount maken (of gebruik een bestaande) in Hallo dezelfde geografische regio als Hallo Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-111">At hello time you create a Media Services account, you also create an associated storage account (or use an existing one) in hello same geographic region as hello Media Services account.</span></span>

<span data-ttu-id="d3b77-112">Dit artikel worden enkele algemene concepten uitgelegd en ziet u hoe u een Media Services toocreate administratief Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d3b77-112">This article explains some common concepts and shows how toocreate a Media Services account with hello Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="d3b77-113">Concepten</span><span class="sxs-lookup"><span data-stu-id="d3b77-113">Concepts</span></span>
<span data-ttu-id="d3b77-114">Voor toegang tot Media Services zijn twee gekoppelde accounts vereist: </span><span class="sxs-lookup"><span data-stu-id="d3b77-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="d3b77-115">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-115">A Media Services account.</span></span> <span data-ttu-id="d3b77-116">Uw account biedt u toegang tot tooa set van cloud-gebaseerde Media Services die beschikbaar zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b77-116">Your account gives you access tooa set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="d3b77-117">Er wordt geen echte media-inhoud opgeslagen in een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="d3b77-118">In plaats daarvan worden metagegevens over Hallo media-inhoud en taken voor de verwerking media opgeslagen in uw account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-118">Instead it stores metadata about hello media content and media processing jobs in your account.</span></span> <span data-ttu-id="d3b77-119">Tijdens het Hallo die u Hallo-account maakt, moet u een beschikbare Media Services-regio selecteren.</span><span class="sxs-lookup"><span data-stu-id="d3b77-119">At hello time you create hello account, you select an available Media Services region.</span></span> <span data-ttu-id="d3b77-120">Hallo regio die u selecteert, is een datacenter waarin Hallo media en metagegevensrecords voor uw account wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d3b77-120">hello region you select is a data center that stores hello metadata records for your account.</span></span>
  
* <span data-ttu-id="d3b77-121">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-121">An Azure storage account.</span></span> <span data-ttu-id="d3b77-122">Storage-accounts moeten zich bevinden in Hallo dezelfde geografische regio als Hallo Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-122">Storage accounts must be located in hello same geographic region as hello Media Services account.</span></span> <span data-ttu-id="d3b77-123">Wanneer u een Media Services-account maakt, kunt u kiezen een bestaand opslagaccount in Hallo dezelfde regio, of u een nieuw opslagaccount in Hallo kunt maken dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="d3b77-123">When you create a Media Services account, you can either choose an existing storage account in hello same region, or you can create a new storage account in hello same region.</span></span> <span data-ttu-id="d3b77-124">Als u een Media Services-account verwijdert, worden de Hallo blobs in uw gerelateerde opslagaccount niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d3b77-124">If you delete a Media Services account, hello blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="d3b77-125">Zie [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md#availability) (Scenario's en beschikbaarheid van Media Services-functies via datacenters) voor meer informatie over de beschikbaarheid van Azure Media Services-functies in verschillende regio's.</span><span class="sxs-lookup"><span data-stu-id="d3b77-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="d3b77-126">Een AMS-account maken</span><span class="sxs-lookup"><span data-stu-id="d3b77-126">Create an AMS account</span></span>
<span data-ttu-id="d3b77-127">Hallo stappen in deze sectie tonen hoe toocreate een AMS-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-127">hello steps in this section show how toocreate an AMS account.</span></span>

1. <span data-ttu-id="d3b77-128">Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d3b77-128">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d3b77-129">Klik op **+Nieuw** > **Web en mobiel** > **Media Services**.</span><span class="sxs-lookup"><span data-stu-id="d3b77-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![Media Services-account maken](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="d3b77-131">Voer bij **MEDIA SERVICES-ACCOUNT MAKEN** de vereiste waarden in.</span><span class="sxs-lookup"><span data-stu-id="d3b77-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![Media Services-account maken](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="d3b77-133">In **accountnaam**, voer de naam Hallo van Hallo nieuwe AMS-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-133">In **Account Name**, enter hello name of hello new AMS account.</span></span> <span data-ttu-id="d3b77-134">De naam van een Media Services-account is alle kleine letters of cijfers zonder spaties en 3 too24 tekens lang is.</span><span class="sxs-lookup"><span data-stu-id="d3b77-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 too24 characters in length.</span></span>
   2. <span data-ttu-id="d3b77-135">Selecteer in abonnement tussen Hallo verschillende Azure-abonnementen waartoe u toegang hebt.</span><span class="sxs-lookup"><span data-stu-id="d3b77-135">In Subscription, select among hello different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="d3b77-136">In **resourcegroep**, selecteer Hallo nieuwe of bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d3b77-136">In **Resource Group**, select hello new or existing resource.</span></span>  <span data-ttu-id="d3b77-137">Een resourcegroep is een verzameling resources met dezelfde levenscyclus, dezelfde machtigingen en hetzelfde beleid.</span><span class="sxs-lookup"><span data-stu-id="d3b77-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="d3b77-138">Klik [hier](../azure-resource-manager/resource-group-overview.md#resource-groups) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3b77-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="d3b77-139">In **locatie**, selecteer Hallo geografische regio die wordt gebruikt toostore Hallo media en metagegevensrecords voor uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-139">In **Location**,  select hello geographic region that will be used toostore hello media and metadata records for your Media Services account.</span></span> <span data-ttu-id="d3b77-140">Dit gebied wordt gebruikt tooprocess en media streamen.</span><span class="sxs-lookup"><span data-stu-id="d3b77-140">This  region will be used tooprocess and stream your media.</span></span> <span data-ttu-id="d3b77-141">Alleen Hallo beschikbare Media Services-regio's worden weergegeven in Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d3b77-141">Only hello available Media Services regions appear in hello drop-down list box.</span></span> 
   5. <span data-ttu-id="d3b77-142">In **Opslagaccount**, selecteert u een storage account tooprovide blob storage van Hallo media-inhoud vanaf uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-142">In **Storage Account**, select a storage account tooprovide blob storage of hello media content from your Media Services account.</span></span> <span data-ttu-id="d3b77-143">U kunt een bestaand opslagaccount selecteren in Hallo dezelfde geografische regio als uw Media Services-account, of u kunt een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="d3b77-143">You can select an existing storage account in hello same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="d3b77-144">Een nieuw opslagaccount gemaakt in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="d3b77-144">A new storage account is created in hello same region.</span></span> <span data-ttu-id="d3b77-145">Hallo-regels voor het opslagaccount namen zijn Hallo dezelfde als voor Media Services-accounts.</span><span class="sxs-lookup"><span data-stu-id="d3b77-145">hello rules for storage account names are hello same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="d3b77-146">Klik [hier](../storage/common/storage-introduction.md) voor meer informatie over opslag.</span><span class="sxs-lookup"><span data-stu-id="d3b77-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="d3b77-147">Selecteer **pincode toodashboard** toosee Hallo voortgang van de implementatie van Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-147">Select **Pin toodashboard** toosee hello progress of hello account deployment.</span></span>
4. <span data-ttu-id="d3b77-148">Klik op **maken** onderin Hallo Hallo vorm.</span><span class="sxs-lookup"><span data-stu-id="d3b77-148">Click **Create** at hello bottom of hello form.</span></span>
   
    <span data-ttu-id="d3b77-149">Zodra het Hallo-account is gemaakt, geladen overzichtspagina.</span><span class="sxs-lookup"><span data-stu-id="d3b77-149">Once hello account is successfully created, overview page loads.</span></span> <span data-ttu-id="d3b77-150">In Hallo streaming-eindpunt tabel Hallo account heeft een standaard streaming-eindpunt in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="d3b77-150">In hello streaming endpoint table hello account will have a default streaming endpoint in hello **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="d3b77-151">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="d3b77-151">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d3b77-152">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="d3b77-152">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
   
## <a name="toomanage-your-ams-account"></a><span data-ttu-id="d3b77-153">toomanage uw AMS-account</span><span class="sxs-lookup"><span data-stu-id="d3b77-153">toomanage your AMS account</span></span>

<span data-ttu-id="d3b77-154">toomanage uw AMS-account (bijvoorbeeld verbinding maken via een programma met toohello AMS API, video's uploaden, assets coderen, configureren van beveiliging van inhoud, voortgang taak) Selecteer **instellingen** op Hallo linkerkant van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d3b77-154">toomanage your AMS account (for example, connect toohello AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="d3b77-155">Van Hallo **instellingen**, navigeer tooone Hallo beschikbaar bladen (bijvoorbeeld: **API-toegang**, **activa**, **taken**, **Content protection**).</span><span class="sxs-lookup"><span data-stu-id="d3b77-155">From hello **Settings**, navigate tooone of hello available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d3b77-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3b77-156">Next steps</span></span>

<span data-ttu-id="d3b77-157">U kunt nu bestanden uploaden naar uw AMS-account.</span><span class="sxs-lookup"><span data-stu-id="d3b77-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="d3b77-158">Zie [Bestanden uploaden](media-services-portal-upload-files.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3b77-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="d3b77-159">Als u van plan tooaccess AMS API programmatisch bent, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d3b77-159">If you plan tooaccess AMS API programmatically, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d3b77-160">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="d3b77-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3b77-161">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d3b77-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

