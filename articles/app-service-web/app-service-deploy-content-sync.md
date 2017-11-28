---
title: aaaSync inhoud van een map tooAzure voor cloud-App Service
description: Meer informatie over hoe toodeploy uw app tooAzure App Service via inhoud synchroniseren vanuit een map van de cloud.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="c55a8-103">Synchronisatie-inhoud van een map tooAzure voor cloud-App Service</span><span class="sxs-lookup"><span data-stu-id="c55a8-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="c55a8-104">Deze zelfstudie leert u hoe toodeploy te[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) door het synchroniseren van uw inhoud van de opslagservices populaire cloudtoepassingen zoals Dropbox en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="c55a8-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="c55a8-105"><a name="overview"></a>Overzicht van de implementatie van inhoud synchroniseren</span><span class="sxs-lookup"><span data-stu-id="c55a8-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="c55a8-106">Hallo inhoud op aanvraag-sync-implementatie wordt aangedreven door Hallo [implementatie-engine Kudu](https://github.com/projectkudu/kudu/wiki) geïntegreerd met App Service.</span><span class="sxs-lookup"><span data-stu-id="c55a8-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="c55a8-107">In Hallo [Azure Portal](https://portal.azure.com), kunt u een map in de cloudopslag, werken met uw app-code en de inhoud in de map en sync tooApp Service Hello op een knop.</span><span class="sxs-lookup"><span data-stu-id="c55a8-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="c55a8-108">Inhoud synchronisatie maakt gebruik van Hallo Kudu proces voor het bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c55a8-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="c55a8-109"><a name="contentsync"></a>Hoe tooenable inhoud implementatie synchroniseren</span><span class="sxs-lookup"><span data-stu-id="c55a8-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="c55a8-110">tooenable inhoud synchroniseren vanuit Hallo [Azure Portal](https://portal.azure.com), als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="c55a8-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="c55a8-111">Klik in de blade van uw app in Azure Portal Hallo op **instellingen** > **Implementatiebron**.</span><span class="sxs-lookup"><span data-stu-id="c55a8-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="c55a8-112">Klik op **bron kiezen**, selecteer daarna **OneDrive** of **Dropbox** als Hallo bron voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c55a8-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Inhoud synchroniseren](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="c55a8-114">Vanwege onderliggende verschillen in Hallo-API's, **OneDrive voor bedrijven** wordt niet ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="c55a8-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="c55a8-115">Volledige Hallo autorisatie werkstroom tooenable tooaccess App Service een specifieke vooraf gedefinieerde opgegeven pad voor OneDrive of Dropbox waarin alle inhoud van de App Service wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c55a8-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="c55a8-116">Hallo optie toocreate een map met inhoud onder Hallo aangewezen na autorisatie Hallo App Service-platform u krijgt, het pad naar inhoud of een bestaande map met inhoud onder deze aangewezen Inhoudspad toochoose.</span><span class="sxs-lookup"><span data-stu-id="c55a8-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="c55a8-117">paden naar inhoud in uw cloud-opslag-accounts die worden gebruikt voor synchronisatie van App Service Hallo aangewezen zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c55a8-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="c55a8-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="c55a8-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="c55a8-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="c55a8-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="c55a8-120">Na Hallo kan de initiële synchronisatie van de inhoud Hallo inhoud synchronisatie worden gestart op verzoek via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c55a8-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="c55a8-121">Geschiedenis van implementatie is beschikbaar met Hallo **implementaties** blade.</span><span class="sxs-lookup"><span data-stu-id="c55a8-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Implementatiegeschiedenis](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="c55a8-123">Meer informatie voor de implementatie van Dropbox vindt onder [implementeren van Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="c55a8-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

