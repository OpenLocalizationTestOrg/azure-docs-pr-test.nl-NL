---
title: geavanceerde scenario's met gegevensanalyses voor Azure Machine Learning aaaIdentify | Microsoft Docs
description: Selecteer Hallo juiste scenario's voor geavanceerde predictive analytics Hello Team gegevens wetenschap proces doen.
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
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="06c74-103">Scenario's voor geavanceerde analyses in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="06c74-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="06c74-104">In dit artikel bevat een overzicht van Hallo verschillende gegevensbronnen voorbeeld en doel-scenario's die kunnen worden verwerkt door Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06c74-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="06c74-105">Hallo TDSP biedt een systematische aanpak voor teams toocollaborate op intelligente toepassingen bouwen.</span><span class="sxs-lookup"><span data-stu-id="06c74-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="06c74-106">Hallo-scenario's die hier wordt gepresenteerd illustreren beschikbare opties in Hallo gegevensverwerking werkstroom die afhankelijk van Hallo gegevenskenmerken, bronlocaties en doel-opslagplaatsen in Azure zijn.</span><span class="sxs-lookup"><span data-stu-id="06c74-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="06c74-107">Hallo **beslissingsstructuur** voor Hallo voorbeeldscenario's die geschikt is voor uw gegevens en doel selecteren in de laatste sectie hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="06c74-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="06c74-108">Elk van de volgende secties Hallo geeft een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="06c74-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="06c74-109">Voor elk scenario, een mogelijke gegevenswetenschap of geavanceerde analyses stroom en de ondersteunende Azure-resources die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="06c74-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="06c74-110">**Voor alle Hallo volgen scenario's, moet u:**
> </span><span class="sxs-lookup"><span data-stu-id="06c74-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="06c74-111">[Een opslagaccount maken](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="06c74-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="06c74-112">Een Azure Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="06c74-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="06c74-113"><a name="smalllocal"></a>Scenario \#1: kleine toomedium in tabelvorm gegevensset in een lokale bestanden</span><span class="sxs-lookup"><span data-stu-id="06c74-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Kleine toomedium lokale bestanden][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="06c74-115">Extra Azure-resources: geen</span><span class="sxs-lookup"><span data-stu-id="06c74-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="06c74-116">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="06c74-117">Upload een dataset.</span><span class="sxs-lookup"><span data-stu-id="06c74-117">Upload a dataset.</span></span>
3. <span data-ttu-id="06c74-118">Maak een Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset (s).</span><span class="sxs-lookup"><span data-stu-id="06c74-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="06c74-119"><a name="smalllocalprocess"></a>Scenario \#2: kleine toomedium gegevensset van lokale bestanden die moeten worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="06c74-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Kleine toomedium lokale bestanden met de verwerking][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="06c74-121">Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-122">Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="06c74-123">Het uploaden van gegevens tooan Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="06c74-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="06c74-124">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure storage-container opschonen.</span><span class="sxs-lookup"><span data-stu-id="06c74-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="06c74-125">Transformeer gegevens toocleaned, tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="06c74-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="06c74-126">Getransformeerde gegevens opslaan in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="06c74-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="06c74-127">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="06c74-128">Hallo-gegevens lezen uit Azure blobs Hallo met [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="06c74-129">Maak een Azure Machine Learning-experiment stroom vanaf opgenomen gegevensset (s).</span><span class="sxs-lookup"><span data-stu-id="06c74-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="06c74-130"><a name="largelocal"></a>Scenario \#3: grote gegevensset van lokale bestanden, die gericht is op Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="06c74-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Grote lokale bestanden][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="06c74-132">Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-133">Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="06c74-134">Het uploaden van gegevens tooan Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="06c74-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="06c74-135">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure blobs opschonen.</span><span class="sxs-lookup"><span data-stu-id="06c74-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="06c74-136">Transformeer gegevens toocleaned, tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="06c74-137">Gegevens verkennen en functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="06c74-138">Een voorbeeld van kleine tot middelgrote gegevens extraheren.</span><span class="sxs-lookup"><span data-stu-id="06c74-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="06c74-139">Hallo door actieve gegevens opslaan in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="06c74-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="06c74-140">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="06c74-141">Hallo-gegevens lezen uit Azure blobs Hallo met [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="06c74-142">Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.</span><span class="sxs-lookup"><span data-stu-id="06c74-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="06c74-143"><a name="smalllocaltodb"></a>Scenario \#4: klein toomedium gegevensset van lokale bestanden, die gericht is op SQL Server in een virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="06c74-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Kleine toomedium lokale bestanden tooSQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="06c74-145">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-146">Maak een virtuele Machine van Azure SQL-Server + IPython Notebook uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="06c74-147">Het uploaden van gegevens tooan Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="06c74-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="06c74-148">Vooraf verwerken en de gegevens in Azure storage-container met IPython Notebook opschonen.</span><span class="sxs-lookup"><span data-stu-id="06c74-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="06c74-149">Transformeer gegevens toocleaned, tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="06c74-150">Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).</span><span class="sxs-lookup"><span data-stu-id="06c74-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="06c74-151">Laden van gegevens tooSQL Server-database op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="06c74-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="06c74-152">Optie \#1: met SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="06c74-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="06c74-153">Aanmelding tooSQL Server VM</span><span class="sxs-lookup"><span data-stu-id="06c74-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="06c74-154">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="06c74-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="06c74-155">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-155">Create database and target tables.</span></span>
   * <span data-ttu-id="06c74-156">Gebruik een van de Hallo bulksgewijs wordt methoden tooload Hallo gegevens importeren uit VM-lokale bestanden.</span><span class="sxs-lookup"><span data-stu-id="06c74-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="06c74-157">Optie \#2: met behulp van IPython Notebook – niet aanbevolen voor middelgrote en grote gegevenssets</span><span class="sxs-lookup"><span data-stu-id="06c74-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="06c74-158">Gebruik ODBC connection string tooaccess SQL Server op virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="06c74-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="06c74-159">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-159">Create database and target tables.</span></span>
   * <span data-ttu-id="06c74-160">Gebruik een van de Hallo bulksgewijs wordt methoden tooload Hallo gegevens importeren uit VM-lokale bestanden.</span><span class="sxs-lookup"><span data-stu-id="06c74-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="06c74-161">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-161">Explore data, create features as needed.</span></span> <span data-ttu-id="06c74-162">Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="06c74-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="06c74-163">Alleen Houd er rekening mee Hallo nodig query toocreate ze.</span><span class="sxs-lookup"><span data-stu-id="06c74-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="06c74-164">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="06c74-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="06c74-165">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="06c74-166">Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="06c74-167">Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="06c74-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="06c74-168">Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.</span><span class="sxs-lookup"><span data-stu-id="06c74-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="06c74-169"><a name="largelocaltodb"></a>Scenario \#5: grote gegevensset in een lokale bestanden doel-SQL-Server in Azure VM</span><span class="sxs-lookup"><span data-stu-id="06c74-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Grote lokale bestanden tooSQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="06c74-171">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-172">Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="06c74-173">Het uploaden van gegevens tooan Azure storage-container.</span><span class="sxs-lookup"><span data-stu-id="06c74-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="06c74-174">(Optioneel) Vooraf verwerken en gegevens opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="06c74-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="06c74-175">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-175">a.</span></span>  <span data-ttu-id="06c74-176">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen</span><span class="sxs-lookup"><span data-stu-id="06c74-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="06c74-177">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-177">b.</span></span>  <span data-ttu-id="06c74-178">Transformeer gegevens toocleaned, tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="06c74-179">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-179">c.</span></span>  <span data-ttu-id="06c74-180">Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).</span><span class="sxs-lookup"><span data-stu-id="06c74-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="06c74-181">Laden van gegevens tooSQL Server-database op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="06c74-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="06c74-182">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-182">a.</span></span>  <span data-ttu-id="06c74-183">Aanmelding tooSQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="06c74-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="06c74-184">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-184">b.</span></span>  <span data-ttu-id="06c74-185">Als gegevens niet al opgeslagen, downloaden van gegevensbestanden van Azure</span><span class="sxs-lookup"><span data-stu-id="06c74-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="06c74-186">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-186">c.</span></span>  <span data-ttu-id="06c74-187">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="06c74-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="06c74-188">d.</span><span class="sxs-lookup"><span data-stu-id="06c74-188">d.</span></span>  <span data-ttu-id="06c74-189">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="06c74-190">e.</span><span class="sxs-lookup"><span data-stu-id="06c74-190">e.</span></span>  <span data-ttu-id="06c74-191">Gebruik een van de Hallo bulksgewijs methoden tooload Hallo gegevens importeren.</span><span class="sxs-lookup"><span data-stu-id="06c74-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="06c74-192">f.</span><span class="sxs-lookup"><span data-stu-id="06c74-192">f.</span></span>  <span data-ttu-id="06c74-193">Als tabelsamenvoegingen vereist zijn, maakt u indexen tooexpedite joins.</span><span class="sxs-lookup"><span data-stu-id="06c74-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06c74-194">Voor sneller laden van grote hoeveelheden gegevens grootten verdient het aanbeveling gepartitioneerde tabellen te maken en importeren Hallo gegevens parallel bulksgewijs.</span><span class="sxs-lookup"><span data-stu-id="06c74-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="06c74-195">Zie voor meer informatie [parallelle gegevensimport tooSQL gepartitioneerde tabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="06c74-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="06c74-196">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-196">Explore data, create features as needed.</span></span> <span data-ttu-id="06c74-197">Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="06c74-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="06c74-198">Alleen Houd er rekening mee Hallo nodig query toocreate ze.</span><span class="sxs-lookup"><span data-stu-id="06c74-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="06c74-199">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="06c74-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="06c74-200">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="06c74-201">Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="06c74-202">Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="06c74-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="06c74-203">Eenvoudige Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset</span><span class="sxs-lookup"><span data-stu-id="06c74-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="06c74-204"><a name="largedbtodb"></a>Scenario \#6: grote gegevensset in een SQL Server-database on-premises, die gericht is op SQL Server in een virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="06c74-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Grote SQL DB on-premises tooSQL DB in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="06c74-206">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-207">Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="06c74-208">Gebruik een van de gegevens Hallo wordt methoden tooexport Hallo gegevens exporteren uit SQL Server toodump-bestanden.</span><span class="sxs-lookup"><span data-stu-id="06c74-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06c74-209">Als u toomove alle gegevens van Hallo on-premises database, een alternatieve (sneller) methode toomove Hallo volledige database toothe SQL Server-exemplaar in Azure besluit.</span><span class="sxs-lookup"><span data-stu-id="06c74-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="06c74-210">Hallo stappen tooexport gegevens overslaan, database en de belasting/importeren gegevens toohello doeldatabase maken en volg Hallo alternatieve methode.</span><span class="sxs-lookup"><span data-stu-id="06c74-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="06c74-211">Upload dump bestanden tooAzure storage-container.</span><span class="sxs-lookup"><span data-stu-id="06c74-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="06c74-212">Laden Hallo gegevens tooa SQL Server-database op een virtuele Machine van Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="06c74-213">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-213">a.</span></span>  <span data-ttu-id="06c74-214">Aanmelding toohello SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="06c74-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="06c74-215">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-215">b.</span></span>  <span data-ttu-id="06c74-216">Downloaden van gegevensbestanden uit een Azure storage-container toohello lokale VM-map.</span><span class="sxs-lookup"><span data-stu-id="06c74-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="06c74-217">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-217">c.</span></span>  <span data-ttu-id="06c74-218">Voer SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="06c74-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="06c74-219">d.</span><span class="sxs-lookup"><span data-stu-id="06c74-219">d.</span></span>  <span data-ttu-id="06c74-220">Database- en doel-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="06c74-221">e.</span><span class="sxs-lookup"><span data-stu-id="06c74-221">e.</span></span>  <span data-ttu-id="06c74-222">Gebruik een van de Hallo bulksgewijs methoden tooload Hallo gegevens importeren.</span><span class="sxs-lookup"><span data-stu-id="06c74-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="06c74-223">f.</span><span class="sxs-lookup"><span data-stu-id="06c74-223">f.</span></span>  <span data-ttu-id="06c74-224">Als tabelsamenvoegingen vereist zijn, maakt u indexen tooexpedite joins.</span><span class="sxs-lookup"><span data-stu-id="06c74-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06c74-225">Maken voor sneller laden van grote hoeveelheden gegevens grootten gepartitioneerde tabellen en toobulk importeren Hallo gegevens parallel.</span><span class="sxs-lookup"><span data-stu-id="06c74-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="06c74-226">Zie voor meer informatie [parallelle gegevensimport tooSQL gepartitioneerde tabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="06c74-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="06c74-227">Gegevens verkennen, functies maken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-227">Explore data, create features as needed.</span></span> <span data-ttu-id="06c74-228">Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="06c74-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="06c74-229">Alleen Houd er rekening mee Hallo nodig query toocreate ze.</span><span class="sxs-lookup"><span data-stu-id="06c74-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="06c74-230">Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.</span><span class="sxs-lookup"><span data-stu-id="06c74-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="06c74-231">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="06c74-232">Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="06c74-233">Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="06c74-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="06c74-234">Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="06c74-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="06c74-235">Alternatieve methode toocopy volledige database van een lokale SQL Server tooAzure SQL-Database</span><span class="sxs-lookup"><span data-stu-id="06c74-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Loskoppelen van de lokale database en koppelt u tooSQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="06c74-237">Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="06c74-238">tooreplicate hello volledige SQL Server-database in uw SQL Server VM u moet een database kopiëren vanaf één locatie of de server tooanother, ervan uitgaande dat die database Hallo tijdelijk offline kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="06c74-239">Dit doet u in Hallo SQL Server Management Studio Object Explorer of Hallo gelijkwaardige Transact-SQL-opdrachten te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06c74-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="06c74-240">Hallo-database op de bronlocatie Hallo loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="06c74-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="06c74-241">Zie voor meer informatie [loskoppelen van een database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="06c74-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="06c74-242">In Windows Verkenner of Windows-opdrachtprompt venster losgekoppeld kopie Hallo databasebestand of bestanden en logboekbestand of bestanden toohello doellocatie op Hallo van SQL Server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="06c74-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="06c74-243">Hallo gekopieerd bestanden toohello doel SQL Server-exemplaar koppelen.</span><span class="sxs-lookup"><span data-stu-id="06c74-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="06c74-244">Zie voor meer informatie [om een Database koppelen](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="06c74-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="06c74-245">[Verplaatsen van een Database met loskoppelen en koppelt (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="06c74-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="06c74-246"><a name="largedbtohive"></a>Scenario \#7: Big data in lokale bestanden doel Hive-database in Azure HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="06c74-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![BIG data in lokale doel Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="06c74-248">Extra Azure-resources: Azure HDInsight Hadoop-Cluster en Azure virtuele Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="06c74-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="06c74-249">Maak een Azure virtuele Machine waarop IPython Notebook server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="06c74-250">Maak een Azure HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="06c74-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="06c74-251">(Optioneel) Vooraf verwerken en gegevens opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="06c74-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="06c74-252">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-252">a.</span></span>  <span data-ttu-id="06c74-253">Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen</span><span class="sxs-lookup"><span data-stu-id="06c74-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="06c74-254">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-254">b.</span></span>  <span data-ttu-id="06c74-255">Transformeer gegevens toocleaned, tabelvorm, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06c74-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="06c74-256">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-256">c.</span></span>  <span data-ttu-id="06c74-257">Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).</span><span class="sxs-lookup"><span data-stu-id="06c74-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="06c74-258">Het uploaden van gegevens toohello standaardcontainer van Hallo Hadoop-cluster in Hallo stap 2 hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="06c74-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="06c74-259">Laden van gegevens tooHive database in Azure HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="06c74-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="06c74-260">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-260">a.</span></span>  <span data-ttu-id="06c74-261">Meld u bij het hoofdknooppunt van het Hadoop-cluster Hallo toohello</span><span class="sxs-lookup"><span data-stu-id="06c74-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="06c74-262">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-262">b.</span></span>  <span data-ttu-id="06c74-263">Open Hallo Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="06c74-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="06c74-264">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-264">c.</span></span>  <span data-ttu-id="06c74-265">Voer Hallo Hive-hoofdmap door opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="06c74-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="06c74-266">d.</span><span class="sxs-lookup"><span data-stu-id="06c74-266">d.</span></span>  <span data-ttu-id="06c74-267">Voer Hallo Hive-query's toocreate database en tabellen en laden van gegevens uit blob storage-tooHive tabellen.</span><span class="sxs-lookup"><span data-stu-id="06c74-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06c74-268">Als Hallo gegevens groot is, kunnen gebruikers Hallo Hive-tabel met partities maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="06c74-269">Vervolgens kunnen gebruikers gebruiken een `for` lus in Hallo Hadoop vanaf de opdrachtregel op Hallo hoofdknooppunt tooload gegevens in Hallo Hive-tabel is gepartitioneerd door partitie.</span><span class="sxs-lookup"><span data-stu-id="06c74-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="06c74-270">Gegevens verkennen en functies maken indien nodig in de Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="06c74-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="06c74-271">Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="06c74-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="06c74-272">Alleen Houd er rekening mee Hallo nodig query toocreate ze.</span><span class="sxs-lookup"><span data-stu-id="06c74-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="06c74-273">a.</span><span class="sxs-lookup"><span data-stu-id="06c74-273">a.</span></span>  <span data-ttu-id="06c74-274">Meld u bij het hoofdknooppunt van het Hadoop-cluster Hallo toohello</span><span class="sxs-lookup"><span data-stu-id="06c74-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="06c74-275">b.</span><span class="sxs-lookup"><span data-stu-id="06c74-275">b.</span></span>  <span data-ttu-id="06c74-276">Open Hallo Hadoop-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="06c74-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="06c74-277">c.</span><span class="sxs-lookup"><span data-stu-id="06c74-277">c.</span></span>  <span data-ttu-id="06c74-278">Voer Hallo Hive-hoofdmap door opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="06c74-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="06c74-279">d.</span><span class="sxs-lookup"><span data-stu-id="06c74-279">d.</span></span>  <span data-ttu-id="06c74-280">Hallo Hive-query's in de Hadoop-opdrachtregel uitvoeren op Hallo hoofdknooppunt Hallo Hadoop-cluster tooexplore Hallo gegevens en onderdelen naar behoefte maken.</span><span class="sxs-lookup"><span data-stu-id="06c74-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="06c74-281">Indien nodig en/of gewenst, steekproef Hallo gegevens toofit in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="06c74-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="06c74-282">Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="06c74-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="06c74-283">Hallo-gegevens lezen rechtstreeks vanuit Hallo `Hive Queries` met Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="06c74-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="06c74-284">Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="06c74-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="06c74-285">Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="06c74-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="06c74-286"><a name="decisiontree"></a>Beslissingsstructuur voor de selectie van scenario</span><span class="sxs-lookup"><span data-stu-id="06c74-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="06c74-287">Hallo volgende diagram ziet u Hallo scenario's die hierboven worden beschreven en Hallo Advanced Analytics-proces en de technologie hebt gekozen waarmee u tooeach Hallo gespecificeerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="06c74-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="06c74-288">Denk eraan dat gegevensverwerking, exploratie functie-engineering en steekproeven kunnen duren plaats in een of meer methode/omgeving--op Hallo bron, tussenliggende, en/of doel omgevingen: en iteratief naar behoefte kunt doorgaan.</span><span class="sxs-lookup"><span data-stu-id="06c74-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="06c74-289">Hallo diagram alleen fungeert als een illustratie van enkele mogelijke stromen en biedt geen een uitputtende opsomming.</span><span class="sxs-lookup"><span data-stu-id="06c74-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Voorbeeldscenario DS proces scenario 's][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="06c74-291">Geavanceerde analyses in actie voorbeelden</span><span class="sxs-lookup"><span data-stu-id="06c74-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="06c74-292">Voor end-to-end Azure Machine Learning-scenario's die gebruikmaken van met Hallo Advanced Analytics-proces en de technologie met behulp van openbare gegevenssets, Zie:</span><span class="sxs-lookup"><span data-stu-id="06c74-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="06c74-293">[Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="06c74-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="06c74-294">[Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="06c74-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
