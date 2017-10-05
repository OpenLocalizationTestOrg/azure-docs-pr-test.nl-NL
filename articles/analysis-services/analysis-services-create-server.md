---
title: Een Analysis Services-server maken in Azure | Microsoft Docs
description: Informatie over het maken van een exemplaar van Analysis Services-server in Azure.
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
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="32d2c-103">Een Azure Analysis Services-server maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="32d2c-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="32d2c-104">Dit artikel begeleidt u bij het maken van een resource van Analysis Services-server in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="32d2c-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32d2c-105">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="32d2c-105">Before you begin</span></span>
<span data-ttu-id="32d2c-106">U hebt het volgende nodig om deze snelstartgids te voltooien:</span><span class="sxs-lookup"><span data-stu-id="32d2c-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="32d2c-107">**Azure-abonnement**: ga naar [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) om een account te maken.</span><span class="sxs-lookup"><span data-stu-id="32d2c-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="32d2c-108">**Azure Active Directory**: uw abonnement moet worden gekoppeld aan een Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="32d2c-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="32d2c-109">En u moet zijn aangemeld bij Azure met een account in dat Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32d2c-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="32d2c-110">Microsoft-accounts worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="32d2c-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="32d2c-111">Raadpleeg voor meer informatie [Verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="32d2c-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="32d2c-112">**Resourcegroep**: een resourcegroep die u al hebt gebruikt of [Maak een nieuwe](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32d2c-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="32d2c-113">Het maken van een server kan zorgen voor een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="32d2c-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="32d2c-114">Zie [Prijzen van Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="32d2c-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="32d2c-115">Een server maken in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="32d2c-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="32d2c-116">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32d2c-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="32d2c-117">Klik op **+ nieuw** > **gegevens en analyse** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="32d2c-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="32d2c-118">In de **Analysis Services** blade Vul de vereiste velden in en druk vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="32d2c-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Server maken](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="32d2c-120">**Servernaam**: Typ een unieke naam die wordt gebruikt om te verwijzen naar de server.</span><span class="sxs-lookup"><span data-stu-id="32d2c-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="32d2c-121">**Abonnement**: Selecteer het abonnement dat deze server stuklijsten aan.</span><span class="sxs-lookup"><span data-stu-id="32d2c-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="32d2c-122">**Resourcegroep**: deze containers zijn ontworpen om u te helpen bij het beheren van een verzameling Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="32d2c-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="32d2c-123">Zie voor meer informatie, [resourcegroepen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32d2c-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="32d2c-124">**Locatie**: locatie van deze Azure-datacenter als host fungeert voor de server.</span><span class="sxs-lookup"><span data-stu-id="32d2c-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="32d2c-125">Kies een locatie dichtstbijzijnde uw grootste gebruikersgroep.</span><span class="sxs-lookup"><span data-stu-id="32d2c-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="32d2c-126">**Prijscategorie**: een prijscategorie selecteren.</span><span class="sxs-lookup"><span data-stu-id="32d2c-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="32d2c-127">Tabellaire modellen tot 400 GB worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="32d2c-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="32d2c-128">Zie voor meer informatie, [Azure Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="32d2c-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="32d2c-129">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="32d2c-129">Click **Create**.</span></span>

<span data-ttu-id="32d2c-130">Maak gewoonlijk duurt minder dan een minuut; vaak slechts enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="32d2c-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="32d2c-131">Als u hebt geselecteerd **toevoegen aan de Portal**, navigeer naar uw portal om te zien van de nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="32d2c-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="32d2c-132">Of Ga naar **meer services** > **Analysis Services** om te zien als de server klaar is.</span><span class="sxs-lookup"><span data-stu-id="32d2c-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="32d2c-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32d2c-134">Next steps</span></span>
<span data-ttu-id="32d2c-135">Nadat u uw server hebt gemaakt, kunt u [implementeert een model](analysis-services-deploy.md) toe met behulp van SSDT of met SSMS.</span><span class="sxs-lookup"><span data-stu-id="32d2c-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="32d2c-136">Als een model dat u op uw server implementeert verbinding met on-premises gegevensbronnen, moet u voor het installeren van een [On-premises gegevensgateway](analysis-services-gateway.md) op een computer in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="32d2c-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

