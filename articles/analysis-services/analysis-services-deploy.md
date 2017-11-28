---
title: aaaDeploy tooAzure Analysis Services met behulp van SSDT | Microsoft Docs
description: Meer informatie over hoe een model in tabelvorm tooan toodeploy Azure Analysis Services-server met behulp van SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="22e66-103">Een model implementeren vanuit SSDT</span><span class="sxs-lookup"><span data-stu-id="22e66-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="22e66-104">Wanneer u een server in uw Azure-abonnement hebt gemaakt, bent u klaar toodeploy een model in tabelvorm database tooit.</span><span class="sxs-lookup"><span data-stu-id="22e66-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="22e66-105">U kunt SQL Server Data Tools (SSDT) toobuild gebruiken en implementeren van een model in tabelvorm project waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="22e66-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="22e66-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="22e66-106">Prerequisites</span></span>
<span data-ttu-id="22e66-107">tooget gestart, moet u de:</span><span class="sxs-lookup"><span data-stu-id="22e66-107">tooget started, you need:</span></span>

* <span data-ttu-id="22e66-108">**Analysis Services-server** in Azure.</span><span class="sxs-lookup"><span data-stu-id="22e66-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="22e66-109">toolearn meer, Zie [maken van een Azure Analysis Services-server](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="22e66-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="22e66-110">**Model in tabelvorm project** in SSDT of een bestaande tabellaire model op Hallo 1200 of hoger compatibiliteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="22e66-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="22e66-111">Nog nooit zo'n project gemaakt?</span><span class="sxs-lookup"><span data-stu-id="22e66-111">Never created one?</span></span> <span data-ttu-id="22e66-112">Probeer Hallo [Adventure Works Internet verkoop in tabelvorm modellering zelfstudie](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="22e66-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="22e66-113">**Lokale gateway** -als een of meer gegevensbronnen zich on-premises in het netwerk van uw organisatie, moet u tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="22e66-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="22e66-114">Hallo-gateway is nodig voor uw server in de cloud Hallo tooyour on-premises gegevensbronnen tooprocess en vernieuwen van gegevens in Hallo model verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="22e66-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="22e66-115">Zorg voordat u implementeert, dat kunt u gegevens hello in tabellen verwerken.</span><span class="sxs-lookup"><span data-stu-id="22e66-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="22e66-116">Klik in SSDT op **Model** > **Process** > **Process All**.</span><span class="sxs-lookup"><span data-stu-id="22e66-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="22e66-117">Als de verwerking mislukt, kunt u niet implementeren.</span><span class="sxs-lookup"><span data-stu-id="22e66-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="22e66-118">een model in tabelvorm van SSDT toodeploy</span><span class="sxs-lookup"><span data-stu-id="22e66-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="22e66-119">Voordat u implementeert, moet u de naam van de server Hallo tooget.</span><span class="sxs-lookup"><span data-stu-id="22e66-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="22e66-120">In **Azure-portal** > server > **overzicht** > **servernaam**, kopie Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="22e66-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="22e66-122">In SSDT > **Solution Explorer**, klik met de rechtermuisknop Hallo project > **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="22e66-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="22e66-123">Klik dan in **implementatie** > **Server** Hallo servernaam plakken.</span><span class="sxs-lookup"><span data-stu-id="22e66-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Servernaam plakken in de eigenschap Deployment Server](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="22e66-125">Klik in **Solution Explorer** met de rechtermuisknop op **Properties** en klik vervolgens op **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="22e66-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="22e66-126">Hebt u mogelijk na vragen aan gebruiker toosign in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="22e66-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Tooserver implementeren](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="22e66-128">Status van de implementatie wordt weergegeven in beide uitvoervenster Hallo en implementeren.</span><span class="sxs-lookup"><span data-stu-id="22e66-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Implementatiestatus](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="22e66-130">Dit is alles wat er is tooit!</span><span class="sxs-lookup"><span data-stu-id="22e66-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="22e66-131">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="22e66-131">Troubleshooting</span></span>
<span data-ttu-id="22e66-132">Als de implementatie mislukt bij het implementeren van metagegevens, is het waarschijnlijk omdat SSDT kan geen verbinding tooyour-server maken.</span><span class="sxs-lookup"><span data-stu-id="22e66-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="22e66-133">Zorg ervoor dat u kunt verbinding maken met behulp van SSMS tooyour-server.</span><span class="sxs-lookup"><span data-stu-id="22e66-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="22e66-134">Controleer vervolgens of Hallo implementatieserver-eigenschap voor Hallo project juist is.</span><span class="sxs-lookup"><span data-stu-id="22e66-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="22e66-135">Als de implementatie voor een tabel mislukt, is het waarschijnlijk omdat de server kan geen verbinding tooa-gegevensbron maken.</span><span class="sxs-lookup"><span data-stu-id="22e66-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="22e66-136">Als uw gegevensbron lokale in het netwerk van uw organisatie, moet u ervoor dat tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="22e66-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="22e66-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22e66-137">Next steps</span></span>
<span data-ttu-id="22e66-138">Nu u uw model in tabelvorm geïmplementeerde tooyour server hebt, bent u klaar tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="22e66-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="22e66-139">U kunt [tooit verbinding met SSMS](analysis-services-manage.md) toomanage deze.</span><span class="sxs-lookup"><span data-stu-id="22e66-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="22e66-140">En kunt u [verbinding maken met een clienthulpprogramma tooit](analysis-services-connect.md) , zoals Power BI, Power BI Desktop of Excel en start het maken van rapporten.</span><span class="sxs-lookup"><span data-stu-id="22e66-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

