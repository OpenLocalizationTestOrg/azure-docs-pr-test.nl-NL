---
title: aaaAdd Azure Storage met behulp van verbonden Services in Visual Studio | Microsoft Docs
description: Azure Storage tooyour app toevoegen met behulp van Hallo Visual Studio verbonden dialoogvenster Services toevoegen
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="d1142-103">Azure-opslag toe te voegen met behulp van Visual Studio verbonden Services</span><span class="sxs-lookup"><span data-stu-id="d1142-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="d1142-104">Met Visual Studio, kunt u een van de volgende tooAzure opslag met behulp van Hallo Hallo **verbonden Services toevoegen** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="d1142-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="d1142-105">C#-cloudservice</span><span class="sxs-lookup"><span data-stu-id="d1142-105">C# cloud service</span></span>
- <span data-ttu-id="d1142-106">.NET-back-end voor mobiele service</span><span class="sxs-lookup"><span data-stu-id="d1142-106">.NET backend mobile service</span></span>
- <span data-ttu-id="d1142-107">ASP.NET-website of service</span><span class="sxs-lookup"><span data-stu-id="d1142-107">ASP.NET website or service</span></span>
- <span data-ttu-id="d1142-108">ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="d1142-108">ASP.NET Core service</span></span>
- <span data-ttu-id="d1142-109">Azure webtaak-service</span><span class="sxs-lookup"><span data-stu-id="d1142-109">Azure WebJob service</span></span> 

<span data-ttu-id="d1142-110">Hallo verbonden service functionaliteit voegt alle verwijzingen Hallo nodig en verbinding tooyour CodeProject en de configuratiebestanden op de juiste wijze wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d1142-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="d1142-111">Na voltooiing wordt Hallo **verbonden Services toevoegen** dialoogvenster documentatie met gedetailleerde informatie over Hallo stappen vereist toostart werken met blob-opslag, wachtrijen en tabellen automatisch weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d1142-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="d1142-112">Verbinding maken met tooAzure Storage Hallo verbonden Services met dialoogvenster</span><span class="sxs-lookup"><span data-stu-id="d1142-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="d1142-113">Open het project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1142-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="d1142-114">In **Solution Explorer**, klik met de rechtermuisknop Hallo **verbonden Services** knooppunt en klik in het contextmenu Hallo en selecteer **verbonden Service toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d1142-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Toevoegen van Azure service verbonden](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="d1142-116">In Hallo **verbonden Services** pagina **Cloud-opslag met Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="d1142-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure-opslag toevoegen](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="d1142-118">In Hallo **Azure Storage** dialoogvenster, selecteer een bestaand opslagaccount en selecteert u **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d1142-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="d1142-119">Als u een opslagaccount toocreate nodig hebt, gaat u toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="d1142-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="d1142-120">Ga anders verder toostep 6.</span><span class="sxs-lookup"><span data-stu-id="d1142-120">Otherwise, skip toostep 6.</span></span>
    
    ![Bestaande opslag account tooproject toevoegen](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="d1142-122">een opslagaccount toocreate:</span><span class="sxs-lookup"><span data-stu-id="d1142-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="d1142-123">Selecteer **een nieuw Opslagaccount maken** Hallo Hallo dialoogvenster onderaan in.</span><span class="sxs-lookup"><span data-stu-id="d1142-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="d1142-124">Hallo invullen **Storage-Account maken** dialoogvenster en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="d1142-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nieuwe Azure storage-account](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="d1142-126">Wanneer Hallo **Azure Storage** dialoogvenster wordt weergegeven, Hallo nieuw opslagaccount wordt weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1142-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="d1142-127">Selecteer Nieuw opslagaccount Hallo in Hallo lijst, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d1142-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="d1142-128">opslag gekoppelde service wordt weergegeven onder Hallo Hallo **Serviceverwijzingen** knooppunt van uw project.</span><span class="sxs-lookup"><span data-stu-id="d1142-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="d1142-129">Hoe uw project is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="d1142-129">How your project is modified</span></span>
<span data-ttu-id="d1142-130">Wanneer u klaar bent met Hallo dialoogvenster, wordt in Visual Studio verwijzingen worden toegevoegd en bepaalde configuratiebestanden wijzigt.</span><span class="sxs-lookup"><span data-stu-id="d1142-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="d1142-131">Hallo specifieke wijzigingen, is afhankelijk van het projecttype Hallo:</span><span class="sxs-lookup"><span data-stu-id="d1142-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="d1142-132">ASP.NET-project - [wat is er gebeurd – ASP.NET-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="d1142-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="d1142-133">ASP.NET Core project - [wat is er gebeurd – ASP.NET 5-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="d1142-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="d1142-134">Cloudserviceproject (webrollen en werkrollen) - [wat is er gebeurd – Cloud Service-projecten](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="d1142-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="d1142-135">Webtaak project - [wat is er gebeurd - webtaak projecten](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="d1142-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1142-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1142-136">Next steps</span></span>
- [<span data-ttu-id="d1142-137">MSDN-Forum: Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="d1142-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="d1142-138">Blog van Microsoft Azure Storage-Team</span><span class="sxs-lookup"><span data-stu-id="d1142-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="d1142-139">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d1142-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
