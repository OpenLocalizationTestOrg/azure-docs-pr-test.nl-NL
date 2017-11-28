---
title: een model in tabelvorm via hello Azure Analysis Services-webserver designer aaaCreate | Microsoft Docs
description: Meer informatie over hoe een model in tabelvorm Azure Analysis Services met behulp van toocreate Hallo webdesigner in Azure-portal.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="cf7d8-103">Een model maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="cf7d8-103">Create a model in Azure portal</span></span>

<span data-ttu-id="cf7d8-104">Hello Azure Analysis Services web designer (preview)-functie in Azure-portal biedt een snelle en gemakkelijke manier toocreate en -modellen in tabelvorm en query model direct in uw browser bewerken.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="cf7d8-105">Houd er rekening mee, Hallo webdesigner is **preview**.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="cf7d8-106">Functionaliteit is beperkt, terwijl de nieuwe functionaliteit alle Hallo tijd, in preview wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="cf7d8-107">Voor meer geavanceerde model ontwikkelen en testen is het beste toouse Visual Studio (SSDT) en SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="cf7d8-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf7d8-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf7d8-108">Prerequisites</span></span>

- <span data-ttu-id="cf7d8-109">Een Azure Analysis Services-server op Hallo Standard of ontwikkelaar laag.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="cf7d8-110">Nieuwe modellen die zijn gemaakt met behulp van Hallo webdesigner zijn DirectQuery, wordt alleen ondersteund door deze lagen.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="cf7d8-111">Een Azure SQL Database, Azure SQL Data Warehouse of Power BI Desktop (pbix)-bestand als een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="cf7d8-112">Nieuwe modellen gemaakt op basis van Power BI Desktop-ondersteuning voor Azure SQL Database, Azure SQL Data Warehouse, Oracle en Teradata-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="cf7d8-113">Een SQL Server-account en wachtwoord voor het verbinden van tooAzure SQL-Database of Azure SQL Data Warehouse-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="cf7d8-114">toocreate een nieuw model in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="cf7d8-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="cf7d8-115">In de server **overzicht** blade > **webdesigner**, klikt u op **Open**.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Een model maken in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="cf7d8-117">In **webdesigner** > **modellen**, klikt u op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Een model maken in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="cf7d8-119">In **nieuw model**, typ de modelnaam van een en selecteer vervolgens een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Dialoogvenster voor nieuwe model in Azure-portal](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="cf7d8-121">In **Connect**, Hallo verbindingseigenschappen invoeren.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="cf7d8-122">Gebruikersnaam en het wachtwoord moet een SQL Server-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-122">Username and password must be a SQL Server account.</span></span>

     ![Verbinding maken met het dialoogvenster in Azure-portal](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="cf7d8-124">In **tabellen en weergaven**Hallo tabellen tooinclude selecteren in het model en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="cf7d8-125">Relaties worden automatisch gemaakt tussen de tabellen met een sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selecteer tabellen en weergaven](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="cf7d8-127">Het nieuwe model wordt weergegeven in uw browser.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-127">Your new model appears in your browser.</span></span> <span data-ttu-id="cf7d8-128">U kunt hier:</span><span class="sxs-lookup"><span data-stu-id="cf7d8-128">From here, you can:</span></span>   

- <span data-ttu-id="cf7d8-129">Modelgegevens query door te slepen velden toohello ontwerpfunctie voor query's en filters toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="cf7d8-130">Nieuwe maatregelen in tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-130">Create new measures in tables.</span></span>
- <span data-ttu-id="cf7d8-131">De metagegevens van model bewerken met behulp van Hallo json-editor.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="cf7d8-132">Hallo model openen in Visual Studio (SSDT), Power BI Desktop of Excel.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selecteer tabellen en weergaven](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="cf7d8-134">Wanneer u modelmetagegevens bewerken of maken van nieuwe maatregelen in uw browser, kunt u deze wijzigingen tooyour model wilt opslaan in Azure.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="cf7d8-135">Als u op het model in SSDT, Power BI Desktop of Excel werkt, kan het model niet meer synchroon.</span><span class="sxs-lookup"><span data-stu-id="cf7d8-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf7d8-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf7d8-136">Next steps</span></span> 
[<span data-ttu-id="cf7d8-137">Databaserollen en gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="cf7d8-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="cf7d8-138">Verbinden met Excel</span><span class="sxs-lookup"><span data-stu-id="cf7d8-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


