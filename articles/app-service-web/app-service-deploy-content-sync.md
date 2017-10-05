---
title: Synchronisatie-inhoud uit een cloud-map in Azure App Service
description: Informatie over het implementeren van uw app in Azure App Service via inhoud synchronisatie uit een cloud-map.
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
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="6d7e7-103">Synchronisatie-inhoud uit een cloud-map in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6d7e7-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="6d7e7-104">Deze zelfstudie leert u hoe u implementeert in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) door het synchroniseren van uw inhoud van de opslagservices populaire cloudtoepassingen zoals Dropbox en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="6d7e7-105"><a name="overview"></a>Overzicht van de implementatie van inhoud synchroniseren</span><span class="sxs-lookup"><span data-stu-id="6d7e7-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="6d7e7-106">De implementatie van inhoud op aanvraag-synchronisatie wordt mogelijk gemaakt door de [implementatie-engine Kudu](https://github.com/projectkudu/kudu/wiki) geïntegreerd met App Service.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="6d7e7-107">In de [Azure Portal](https://portal.azure.com), kunt u een map in de cloudopslag, werken met uw app-code en de inhoud in de map en synchroniseren in App Service met de op een knop te klikken.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="6d7e7-108">Inhoud synchronisatie maakt gebruik van de Kudu-proces voor het bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="6d7e7-109"><a name="contentsync"></a>Het inschakelen van inhoud sync-implementatie</span><span class="sxs-lookup"><span data-stu-id="6d7e7-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="6d7e7-110">Inschakelen van inhoud synchroniseren vanuit de [Azure Portal](https://portal.azure.com), als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="6d7e7-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="6d7e7-111">Klik in de blade van uw app in de Azure Portal op **instellingen** > **Implementatiebron**.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="6d7e7-112">Klik op **bron kiezen**, selecteer daarna **OneDrive** of **Dropbox** als bron voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Inhoud synchroniseren](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d7e7-114">Vanwege onderliggende verschillen in de API's, **OneDrive voor bedrijven** wordt niet ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="6d7e7-115">Het voltooien van de werkstroom autorisatie om in te schakelen van App Service toegang krijgen tot een specifiek pad van de vooraf gedefinieerde aangewezen voor OneDrive of Dropbox waarin alle inhoud van de App Service wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="6d7e7-116">Na autorisatie App Service krijgt platform u de optie voor het maken van een map met inhoud onder het pad naar de aangewezen inhoud of een bestaande map met inhoud onder deze aangewezen Inhoudspad kiezen.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="6d7e7-117">De opgegeven paden naar inhoud toe onder uw cloud-opslag-accounts die worden gebruikt voor synchronisatie van App Service, zijn de volgende:</span><span class="sxs-lookup"><span data-stu-id="6d7e7-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="6d7e7-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="6d7e7-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="6d7e7-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="6d7e7-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="6d7e7-120">Na de initiële synchronisatie van de inhoud kan de inhoud synchronisatie worden gestart op verzoek vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="6d7e7-121">Geschiedenis van implementatie is beschikbaar met de **implementaties** blade.</span><span class="sxs-lookup"><span data-stu-id="6d7e7-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Implementatiegeschiedenis](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="6d7e7-123">Meer informatie voor de implementatie van Dropbox vindt onder [implementeren van Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d7e7-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

