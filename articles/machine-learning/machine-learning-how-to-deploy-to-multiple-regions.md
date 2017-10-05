---
title: Een webservice implementeren op meerdere gebieden | Microsoft Docs
description: "Stappen voor het implementeren van (kopiëren) een nieuwe Web-Service naar andere regio's."
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
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="a2149-103">Een webservice implementeren in meerdere regio’s</span><span class="sxs-lookup"><span data-stu-id="a2149-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="a2149-104">De nieuwe Azure-Web-Services kunt u eenvoudig een webservice implementeren in meerdere regio's zonder meerdere abonnementen of werkruimten.</span><span class="sxs-lookup"><span data-stu-id="a2149-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="a2149-105">Prijzen is regio specifiek, dat daarom moet u een abonnement voor elke regio waarin u de webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="a2149-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="a2149-106">Een planning maken in een andere regio</span><span class="sxs-lookup"><span data-stu-id="a2149-106">To create a plan in another region</span></span>
1. <span data-ttu-id="a2149-107">Meld u aan bij [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="a2149-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="a2149-108">Klik op de **plannen** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="a2149-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="a2149-109">Klik op de plannen via de weergavepagina **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a2149-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="a2149-110">Van de **abonnement** vervolgkeuzelijst, selecteer het abonnement waarin het nieuwe plan wilt maken.</span><span class="sxs-lookup"><span data-stu-id="a2149-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="a2149-111">Van de **regio** vervolgkeuzelijst, selecteer een regio voor het nieuwe plan.</span><span class="sxs-lookup"><span data-stu-id="a2149-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="a2149-112">De opties plannen voor de geselecteerde regio wordt weergegeven in de **opties plannen** sectie van de pagina.</span><span class="sxs-lookup"><span data-stu-id="a2149-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="a2149-113">Van de **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor het plan.</span><span class="sxs-lookup"><span data-stu-id="a2149-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="a2149-114">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2149-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="a2149-115">In **naam** typt u de naam van het plan.</span><span class="sxs-lookup"><span data-stu-id="a2149-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="a2149-116">Onder **Plan opties**, klikt u op het niveau van facturering voor het nieuwe plan.</span><span class="sxs-lookup"><span data-stu-id="a2149-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="a2149-117">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2149-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="a2149-118">De webservice implementeren op een andere regio</span><span class="sxs-lookup"><span data-stu-id="a2149-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="a2149-119">Klik op de **webservices** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="a2149-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="a2149-120">Selecteer de webservice die u op een nieuw gebied implementeert.</span><span class="sxs-lookup"><span data-stu-id="a2149-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="a2149-121">Klik op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="a2149-121">Click **Copy**.</span></span>
4. <span data-ttu-id="a2149-122">In **Webservicenaam**, typt u een nieuwe naam voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="a2149-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="a2149-123">In **Web servicebeschrijving**, typt u een beschrijving voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="a2149-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="a2149-124">Van de **abonnement** vervolgkeuzelijst, selecteer het abonnement waarin de nieuwe webservice wilt maken.</span><span class="sxs-lookup"><span data-stu-id="a2149-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="a2149-125">Van de **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="a2149-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="a2149-126">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2149-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="a2149-127">Van de **regio** vervolgkeuzelijst, selecteer de regio waarin u de webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="a2149-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="a2149-128">Van de **opslagaccount** dropdown, selecteert u een opslag-account waarin u voor het opslaan van de webservice.</span><span class="sxs-lookup"><span data-stu-id="a2149-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="a2149-129">Van de **prijs Plan** dropdown, selecteert u een plan in de regio die u hebt geselecteerd in stap 8.</span><span class="sxs-lookup"><span data-stu-id="a2149-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="a2149-130">Klik op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="a2149-130">Click **Copy**.</span></span>

