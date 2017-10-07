---
title: aaaHow toodeploy een webservice toomultiple regio's | Microsoft Docs
description: "Stappen toodeploy (kopiëren) een nieuwe webservice tooother regio's."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="58afc-103">Hoe een webservice toodeploy toomultiple regio's</span><span class="sxs-lookup"><span data-stu-id="58afc-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="58afc-104">Hallo nieuwe Azure Web Services kunt u tooeasily een web service toomultiple regio's implementeren zonder meerdere abonnementen of werkruimten.</span><span class="sxs-lookup"><span data-stu-id="58afc-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="58afc-105">Prijzen is regio specifiek, dat daarom moet u een abonnement voor elke regio waarin u Hallo webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="58afc-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="58afc-106">toocreate een plan in een andere regio</span><span class="sxs-lookup"><span data-stu-id="58afc-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="58afc-107">Meld u aan bij [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="58afc-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="58afc-108">Klik op Hallo **plannen** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="58afc-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="58afc-109">Op Hallo plannen via de pagina weergeven, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="58afc-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="58afc-110">Van Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo-abonnement in welke Hallo nieuw plan moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58afc-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="58afc-111">Van Hallo **regio** vervolgkeuzelijst, selecteer een regio voor nieuwe Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="58afc-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="58afc-112">Hallo opties plannen voor de geselecteerde regio hello wordt weergegeven in Hallo **opties plannen** sectie van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="58afc-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="58afc-113">Van Hallo **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="58afc-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="58afc-114">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58afc-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="58afc-115">In **naam** Hallo typenaam van Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="58afc-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="58afc-116">Onder **Plan opties**, klikt u op de facturering niveau Hallo voor nieuwe Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="58afc-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="58afc-117">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="58afc-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="58afc-118">Hallo web service tooanother regio implementeren</span><span class="sxs-lookup"><span data-stu-id="58afc-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="58afc-119">Klik op Hallo **webservices** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="58afc-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="58afc-120">Selecteer Hallo webservice u tooa nieuwe regio implementeert.</span><span class="sxs-lookup"><span data-stu-id="58afc-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="58afc-121">Klik op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="58afc-121">Click **Copy**.</span></span>
4. <span data-ttu-id="58afc-122">In **Webservicenaam**, typt u een nieuwe naam voor het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58afc-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="58afc-123">In **Web servicebeschrijving**, typ een beschrijving voor het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58afc-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="58afc-124">Van Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo-abonnement in welke Hallo nieuwe webservice moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58afc-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="58afc-125">Van Hallo **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58afc-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="58afc-126">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58afc-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="58afc-127">Van Hallo **regio** vervolgkeuzelijst, selecteer Hallo regio in welke toodeploy Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58afc-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="58afc-128">Van Hallo **opslagaccount** vervolgkeuzelijst, selecteer een opslagaccount in welke toostore Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58afc-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="58afc-129">Van Hallo **prijs Plan** dropdown, selecteert u een plan in Hallo regio die u hebt geselecteerd in stap 8.</span><span class="sxs-lookup"><span data-stu-id="58afc-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="58afc-130">Klik op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="58afc-130">Click **Copy**.</span></span>

