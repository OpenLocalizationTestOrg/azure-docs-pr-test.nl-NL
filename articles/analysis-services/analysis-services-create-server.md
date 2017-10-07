---
title: aaaCreate een Analysis Services-server in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Analysis Services-server-instantie in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="7aed3-103">Een Azure Analysis Services-server maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="7aed3-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="7aed3-104">Dit artikel begeleidt u bij het maken van een resource van Analysis Services-server in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7aed3-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7aed3-105">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7aed3-105">Before you begin</span></span>
<span data-ttu-id="7aed3-106">toocomplete deze snelstartgids die u nodig:</span><span class="sxs-lookup"><span data-stu-id="7aed3-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="7aed3-107">**Azure-abonnement**: Ga naar [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="7aed3-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="7aed3-108">**Azure Active Directory**: uw abonnement moet worden gekoppeld aan een Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="7aed3-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="7aed3-109">En moet u toobe tooAzure aangemeld met een account in dat Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7aed3-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="7aed3-110">Microsoft-accounts worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7aed3-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="7aed3-111">toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="7aed3-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="7aed3-112">**Resourcegroep**: een resourcegroep die u al hebt gebruikt of [Maak een nieuwe](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7aed3-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7aed3-113">Het maken van een server kan zorgen voor een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="7aed3-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="7aed3-114">toolearn meer, Zie [Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="7aed3-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="7aed3-115">toocreate een server in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7aed3-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="7aed3-116">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7aed3-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="7aed3-117">Klik op **+ nieuw** > **gegevens en analyse** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="7aed3-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="7aed3-118">In Hallo **Analysis Services** blade Vul Hallo vereiste velden in en druk vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7aed3-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Server maken](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="7aed3-120">**Servernaam**: Typ een unieke naam gebruikt tooreference Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="7aed3-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="7aed3-121">**Abonnement**: Hallo abonnement deze server te stuklijsten selecteren.</span><span class="sxs-lookup"><span data-stu-id="7aed3-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="7aed3-122">**Resourcegroep**: deze containers worden ontworpen toohelp u een verzameling Azure-resources beheren.</span><span class="sxs-lookup"><span data-stu-id="7aed3-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="7aed3-123">toolearn meer, Zie [resourcegroepen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7aed3-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="7aed3-124">**Locatie**: deze Azure datacenter locatie hosts Hallo server.</span><span class="sxs-lookup"><span data-stu-id="7aed3-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="7aed3-125">Kies een locatie dichtstbijzijnde uw grootste gebruikersgroep.</span><span class="sxs-lookup"><span data-stu-id="7aed3-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="7aed3-126">**Prijscategorie**: een prijscategorie selecteren.</span><span class="sxs-lookup"><span data-stu-id="7aed3-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="7aed3-127">Modellen in tabelvorm up too400 GB worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7aed3-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="7aed3-128">toolearn meer, Zie [Azure Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="7aed3-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="7aed3-129">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7aed3-129">Click **Create**.</span></span>

<span data-ttu-id="7aed3-130">Maak gewoonlijk duurt minder dan een minuut; vaak slechts enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="7aed3-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="7aed3-131">Als u hebt geselecteerd **tooPortal toevoegen**, navigeer tooyour portal toosee uw nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="7aed3-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="7aed3-132">Of Ga te**meer services** > **Analysis Services** toosee als de server klaar is.</span><span class="sxs-lookup"><span data-stu-id="7aed3-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="7aed3-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7aed3-134">Next steps</span></span>
<span data-ttu-id="7aed3-135">Nadat u uw server hebt gemaakt, kunt u [implementeert een model](analysis-services-deploy.md) tooit met behulp van SSDT of met SSMS.</span><span class="sxs-lookup"><span data-stu-id="7aed3-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="7aed3-136">Als een model u tooyour-server implementeren verbinding tooon-premises gegevensbronnen, moet u tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md) op een computer in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7aed3-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

