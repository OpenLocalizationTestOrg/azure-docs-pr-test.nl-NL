---
title: Scenario's voor geavanceerde analyses bepalen voor Azure Machine Learning | Microsoft Docs
description: Selecteer de juiste scenario's voor geavanceerde voorspellende analyses met het Team gegevens wetenschap proces doen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="c1d7e-103">Scenario's voor geavanceerde analyses in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1d7e-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="c1d7e-104">In dit artikel bevat een overzicht van de verschillende gegevensbronnen voorbeeld en doel-scenario's die kunnen worden verwerkt door de [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="c1d7e-105">De TDSP biedt een systematische aanpak voor teams die samenwerken aan intelligente toepassingen bouwen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="c1d7e-106">De scenario's die hier wordt gepresenteerd illustreren beschikbare opties in de werkstroom gegevensverwerking die afhankelijk van de gegevenskenmerken, bronlocaties en doel-opslagplaatsen in Azure zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="c1d7e-107">De **beslissingsstructuur** voor het selecteren van de voorbeeldscenario's die geschikt is voor uw gegevens en het doel is opgenomen in de laatste sectie.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="c1d7e-108">Elk van de volgende secties geeft een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="c1d7e-109">Voor elk scenario, een mogelijke gegevenswetenschap of geavanceerde analyses stroom en de ondersteunende Azure-resources die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d7e-110">**Voor alle van de volgende scenario's moet u:**
> </span><span class="sxs-lookup"><span data-stu-id="c1d7e-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="c1d7e-111">[Een opslagaccount maken](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="c1d7e-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="c1d7e-112">Een Azure Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="c1d7e-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="c1d7e-113"><a name="smalllocal"></a>Scenario \#1: kleine tot middelgrote in tabelvorm gegevensset in een lokale bestanden</span><span class="sxs-lookup"><span data-stu-id="c1d7e-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Kleine tot middelgrote lokale bestanden][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="c1d7e-115">Extra Azure-resources: geen</span><span class="sxs-lookup"><span data-stu-id="c1d7e-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="c1d7e-116">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="c1d7e-117">Upload een dataset.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-117">Upload a dataset.</span></span>
3. <span data-ttu-id="c1d7e-118">Maak een Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset (s).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="c1d7e-119"><a name="smalllocalprocess"></a>Scenario \#2: kleine tot middelgrote gegevensset van lokale bestanden die moeten worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="c1d7e-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Kleine tot middelgrote lokale bestanden met de verwerking][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c1d7e-121">Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-122">Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="c1d7e-123">Gegevens uploaden naar een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c1d7e-124">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure storage-container opschonen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="c1d7e-125">Transformeer gegevens gereinigd, in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="c1d7e-126">Getransformeerde gegevens opslaan in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="c1d7e-127">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="c1d7e-128">Leest de gegevens uit Azure blobs met de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="c1d7e-129">Maak een Azure Machine Learning-experiment stroom vanaf opgenomen gegevensset (s).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c1d7e-130"><a name="largelocal"></a>Scenario \#3: grote gegevensset van lokale bestanden, die gericht is op Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="c1d7e-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Grote lokale bestanden][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c1d7e-132">Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-133">Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="c1d7e-134">Gegevens uploaden naar een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c1d7e-135">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure blobs opschonen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="c1d7e-136">Transformeer gegevens gereinigd, in tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="c1d7e-137">Gegevens verkennen en functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="c1d7e-138">Een voorbeeld van kleine tot middelgrote gegevens extraheren.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="c1d7e-139">Sla de steekproefgegevens in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="c1d7e-140">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="c1d7e-141">Leest de gegevens uit Azure blobs met de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="c1d7e-142">Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c1d7e-143"><a name="smalllocaltodb"></a>Scenario \#4: klein middelgrote DataSet van lokale bestanden, die gericht is op SQL Server in een virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="c1d7e-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Kleine tot middelgrote lokale bestanden aan de SQL-database in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c1d7e-145">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-146">Maak een virtuele Machine van Azure SQL-Server + IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="c1d7e-147">Gegevens uploaden naar een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c1d7e-148">Vooraf verwerken en de gegevens in Azure storage-container met IPython Notebook opschonen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="c1d7e-149">Transformeer gegevens gereinigd, in tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="c1d7e-150">Gegevens opslaan naar VM-local-bestanden (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen naar VM-schijven).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="c1d7e-151">Laden van gegevens naar SQL Server-database op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="c1d7e-152">Optie \#1: met SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="c1d7e-153">Aanmelden bij SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="c1d7e-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="c1d7e-154">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="c1d7e-155">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-155">Create database and target tables.</span></span>
   * <span data-ttu-id="c1d7e-156">Gebruik een van de bulksgewijs importeren methoden voor het laden van de gegevens van VM-lokale bestanden.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="c1d7e-157">Optie \#2: met behulp van IPython Notebook – niet aanbevolen voor middelgrote en grote gegevenssets</span><span class="sxs-lookup"><span data-stu-id="c1d7e-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="c1d7e-158">ODBC-verbindingsreeks gebruiken voor toegang tot SQL Server op virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="c1d7e-159">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-159">Create database and target tables.</span></span>
   * <span data-ttu-id="c1d7e-160">Gebruik een van de bulksgewijs importeren methoden voor het laden van de gegevens van VM-lokale bestanden.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="c1d7e-161">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-161">Explore data, create features as needed.</span></span> <span data-ttu-id="c1d7e-162">Houd er rekening mee dat de functies niet hoeft te worden gematerialiseerd in de databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c1d7e-163">Opmerking alleen de benodigde query om deze te maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="c1d7e-164">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="c1d7e-165">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="c1d7e-166">Lezen van de gegevens rechtstreeks vanuit de SQL Server met de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c1d7e-167">Plak de benodigde query velden extraheert en maakt functies en voorbeelden van gegevens, indien nodig rechtstreeks in de [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="c1d7e-168">Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c1d7e-169"><a name="largelocaltodb"></a>Scenario \#5: grote gegevensset in een lokale bestanden doel-SQL-Server in Azure VM</span><span class="sxs-lookup"><span data-stu-id="c1d7e-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Grote lokale bestanden aan de SQL-database in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c1d7e-171">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-172">Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="c1d7e-173">Gegevens uploaden naar een Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c1d7e-174">(Optioneel) Vooraf verwerken en gegevens opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="c1d7e-175">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-175">a.</span></span>  <span data-ttu-id="c1d7e-176">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen</span><span class="sxs-lookup"><span data-stu-id="c1d7e-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="c1d7e-177">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-177">b.</span></span>  <span data-ttu-id="c1d7e-178">Transformeer gegevens gereinigd, in tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="c1d7e-179">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-179">c.</span></span>  <span data-ttu-id="c1d7e-180">Gegevens opslaan naar VM-local-bestanden (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen naar VM-schijven).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="c1d7e-181">Laden van gegevens naar SQL Server-database op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="c1d7e-182">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-182">a.</span></span>  <span data-ttu-id="c1d7e-183">Aanmelden bij SQL Server-machine.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="c1d7e-184">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-184">b.</span></span>  <span data-ttu-id="c1d7e-185">Als gegevens niet al opgeslagen, downloaden van gegevensbestanden van Azure</span><span class="sxs-lookup"><span data-stu-id="c1d7e-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="c1d7e-186">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-186">c.</span></span>  <span data-ttu-id="c1d7e-187">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="c1d7e-188">d.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-188">d.</span></span>  <span data-ttu-id="c1d7e-189">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="c1d7e-190">e.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-190">e.</span></span>  <span data-ttu-id="c1d7e-191">Gebruik een van de bulksgewijs importeren methoden om de gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="c1d7e-192">f.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-192">f.</span></span>  <span data-ttu-id="c1d7e-193">Als tabelsamenvoegingen nodig zijn, worden de indexen joins sneller maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1d7e-194">Voor sneller laden van grote hoeveelheden gegevens grootten verdient het aanbeveling dat u gepartitioneerde tabellen maken en grote hoeveelheden gegevens parallel importeren.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="c1d7e-195">Zie voor meer informatie [parallelle gegevens importeren in SQL-tabellen gepartitioneerd](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="c1d7e-196">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-196">Explore data, create features as needed.</span></span> <span data-ttu-id="c1d7e-197">Houd er rekening mee dat de functies niet hoeft te worden gematerialiseerd in de databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c1d7e-198">Opmerking alleen de benodigde query om deze te maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="c1d7e-199">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="c1d7e-200">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="c1d7e-201">Lezen van de gegevens rechtstreeks vanuit de SQL Server met de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c1d7e-202">Plak de benodigde query velden extraheert en maakt functies en voorbeelden van gegevens, indien nodig rechtstreeks in de [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="c1d7e-203">Eenvoudige Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset</span><span class="sxs-lookup"><span data-stu-id="c1d7e-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="c1d7e-204"><a name="largedbtodb"></a>Scenario \#6: grote gegevensset in een SQL Server-database on-premises, die gericht is op SQL Server in een virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="c1d7e-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Grote SQL DB on-premises aan de SQL-database in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c1d7e-206">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-207">Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="c1d7e-208">Gebruik een van de gegevens exporteren methoden voor het exporteren van de gegevens uit SQL Server naar dumpbestanden.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1d7e-209">Als u besluit alle gegevens te verplaatsen uit de on-premises database, een alternatieve (sneller) methode de volledige database verplaatsen naar de SQL Server-exemplaar in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="c1d7e-210">De stappen voor het exporteren van gegevens, database maken en belasting/importeren van gegevens naar de doeldatabase en volgt u de alternatieve methode overslaan.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="c1d7e-211">Dumpbestanden uploaden naar Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="c1d7e-212">Laden van de gegevens naar een SQL Server-database op een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="c1d7e-213">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-213">a.</span></span>  <span data-ttu-id="c1d7e-214">Meld u aan met de SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="c1d7e-215">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-215">b.</span></span>  <span data-ttu-id="c1d7e-216">Het downloaden van gegevensbestanden van een Azure storage-container naar de map local-VM.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="c1d7e-217">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-217">c.</span></span>  <span data-ttu-id="c1d7e-218">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="c1d7e-219">d.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-219">d.</span></span>  <span data-ttu-id="c1d7e-220">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="c1d7e-221">e.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-221">e.</span></span>  <span data-ttu-id="c1d7e-222">Gebruik een van de bulksgewijs importeren methoden om de gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="c1d7e-223">f.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-223">f.</span></span>  <span data-ttu-id="c1d7e-224">Als tabelsamenvoegingen nodig zijn, worden de indexen joins sneller maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1d7e-225">Importeer gegevens parallel voor sneller laden van grote hoeveelheden gegevens grootte en gepartitioneerde tabellen maken en voor bulkinschrijving.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="c1d7e-226">Zie voor meer informatie [parallelle gegevens importeren in SQL-tabellen gepartitioneerd](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="c1d7e-227">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-227">Explore data, create features as needed.</span></span> <span data-ttu-id="c1d7e-228">Houd er rekening mee dat de functies niet hoeft te worden gematerialiseerd in de databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c1d7e-229">Opmerking alleen de benodigde query om deze te maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="c1d7e-230">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="c1d7e-231">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="c1d7e-232">Lezen van de gegevens rechtstreeks vanuit de SQL Server met de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c1d7e-233">Plak de benodigde query velden extraheert en maakt functies en voorbeelden van gegevens, indien nodig rechtstreeks in de [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="c1d7e-234">Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="c1d7e-235">Alternatieve methode volledige database kopiëren vanuit een lokale SQL Server naar Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c1d7e-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Lokale database loskoppelen en koppelen aan SQL-database in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c1d7e-237">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="c1d7e-238">Als u wilt repliceren van de volledige SQL Server-database in uw SQL Server VM, moet u kopiëren een database van één locatie of de server naar een andere, ervan uitgaande dat de database kan worden gehouden die tijdelijk offline.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="c1d7e-239">Dit doet u in de SQL Server Management Studio Object Explorer of met behulp van de equivalente Transact-SQL-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="c1d7e-240">Ontkoppel de database op de bronlocatie.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-240">Detach the database at the source location.</span></span> <span data-ttu-id="c1d7e-241">Zie voor meer informatie [loskoppelen van een database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="c1d7e-242">Kopieer in Windows Verkenner of Windows-opdrachtprompt venster de losgekoppelde databasebestand of de bestanden en het logboekbestand of de bestanden naar de doellocatie op de SQL Server-virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="c1d7e-243">De gekopieerde bestanden toevoegen aan het doelexemplaar van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="c1d7e-244">Zie voor meer informatie [om een Database koppelen](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="c1d7e-245">[Verplaatsen van een Database met loskoppelen en koppelt (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="c1d7e-246"><a name="largedbtohive"></a>Scenario \#7: Big data in lokale bestanden doel Hive-database in Azure HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="c1d7e-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![BIG data in lokale doel Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c1d7e-248">Extra Azure-resources: Azure HDInsight Hadoop-Cluster en Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="c1d7e-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c1d7e-249">Maak een Azure virtuele Machine waarop IPython Notebook server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="c1d7e-250">Maak een Azure HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="c1d7e-251">(Optioneel) Vooraf verwerken en gegevens opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="c1d7e-252">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-252">a.</span></span>  <span data-ttu-id="c1d7e-253">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen</span><span class="sxs-lookup"><span data-stu-id="c1d7e-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="c1d7e-254">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-254">b.</span></span>  <span data-ttu-id="c1d7e-255">Transformeer gegevens gereinigd, in tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="c1d7e-256">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-256">c.</span></span>  <span data-ttu-id="c1d7e-257">Gegevens opslaan naar VM-local-bestanden (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen naar VM-schijven).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="c1d7e-258">Gegevens uploaden naar de standaardcontainer van het Hadoop-cluster dat is geselecteerd in stap 2.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="c1d7e-259">Laden van gegevens met Hive-database in Azure HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="c1d7e-260">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-260">a.</span></span>  <span data-ttu-id="c1d7e-261">Aanmelden met het hoofdknooppunt van het Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="c1d7e-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="c1d7e-262">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-262">b.</span></span>  <span data-ttu-id="c1d7e-263">Open de Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c1d7e-264">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-264">c.</span></span>  <span data-ttu-id="c1d7e-265">Voer in de hoofdmap van Hive met opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c1d7e-266">d.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-266">d.</span></span>  <span data-ttu-id="c1d7e-267">Voer de Hive-query's voor het maken van de database en tabellen en laden van gegevens uit blob storage naar Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1d7e-268">Als de gegevens groot is, kunnen gebruikers de Hive-tabel met partities maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="c1d7e-269">Vervolgens kunnen gebruikers gebruiken een `for` lus in de Hadoop opdrachtregel hoofdknooppunt van het laden van gegevens in de Hive-tabel is gepartitioneerd door partitie.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="c1d7e-270">Gegevens verkennen en functies maken indien nodig in de Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="c1d7e-271">Houd er rekening mee dat de functies niet hoeft te worden gematerialiseerd in de databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c1d7e-272">Opmerking alleen de benodigde query om deze te maken.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="c1d7e-273">a.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-273">a.</span></span>  <span data-ttu-id="c1d7e-274">Aanmelden met het hoofdknooppunt van het Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="c1d7e-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="c1d7e-275">b.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-275">b.</span></span>  <span data-ttu-id="c1d7e-276">Open de Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c1d7e-277">c.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-277">c.</span></span>  <span data-ttu-id="c1d7e-278">Voer in de hoofdmap van Hive met opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c1d7e-279">d.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-279">d.</span></span>  <span data-ttu-id="c1d7e-280">Hive-query's in de Hadoop-opdrachtregel op het hoofdknooppunt van het Hadoop-cluster Verken de gegevens en functies maken indien nodig uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="c1d7e-281">Als nodig is en/of gewenst, de gegevens in Azure Machine Learning Studio past controleren.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="c1d7e-282">Aanmelden bij de [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="c1d7e-283">Lezen van de gegevens rechtstreeks vanuit de `Hive Queries` met behulp van de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c1d7e-284">Plak de benodigde query velden extraheert en maakt functies en voorbeelden van gegevens, indien nodig rechtstreeks in de [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="c1d7e-285">Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="c1d7e-286"><a name="decisiontree"></a>Beslissingsstructuur voor de selectie van scenario</span><span class="sxs-lookup"><span data-stu-id="c1d7e-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="c1d7e-287">Het volgende diagram ziet u de scenario's die hierboven worden beschreven en het proces van Advanced Analytics en technologie die u hebt gekozen om naar de gespecificeerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="c1d7e-288">Denk eraan dat gegevensverwerking, exploratie functie-engineering en steekproeven kunnen duren plaats in een of meer methode/omgeving--op de bronlocatie, tussenliggende, en/of doel omgevingen: en iteratief naar behoefte kunt doorgaan.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="c1d7e-289">Het diagram alleen fungeert als een illustratie van enkele mogelijke stromen en biedt geen een uitputtende opsomming.</span><span class="sxs-lookup"><span data-stu-id="c1d7e-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Voorbeeldscenario DS proces scenario 's][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="c1d7e-291">Geavanceerde analyses in actie voorbeelden</span><span class="sxs-lookup"><span data-stu-id="c1d7e-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="c1d7e-292">Zie voor end-to-end Azure Machine Learning-scenario's die gebruikmaken van het proces van Advanced Analytics en technologie openbare gegevenssets:</span><span class="sxs-lookup"><span data-stu-id="c1d7e-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="c1d7e-293">[Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="c1d7e-294">[Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c1d7e-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
