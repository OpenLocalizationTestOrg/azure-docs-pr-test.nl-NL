---
title: aaaTest en foutopsporing U-SQL-taken via lokale uitvoeren en Azure Data Lake U-SQL-SDK Hallo | Microsoft Docs
description: Meer informatie over hoe toouse Azure Data Lake Tools voor Visual Studio en hello Azure Data Lake U-SQL-SDK tootest en foutopsporing U-SQL taken op uw lokale werkstation.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="b0c5f-103">Testen en foutopsporing van U-SQL-taken met behulp van lokaal uitvoeren en hello Azure Data Lake U-SQL-SDK</span><span class="sxs-lookup"><span data-stu-id="b0c5f-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="b0c5f-104">U kunt Azure Data Lake Tools voor Visual Studio en hello Azure Data Lake U-SQL-SDK toorun U-SQL-taken op uw werkstation gebruiken, net zoals u in hello Azure Data Lake-service kunt.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="b0c5f-105">Deze twee lokaal uitgevoerde functies besparen tijd op het gebied van het testen en de foutopsporing van uw U-SQL-taken.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="b0c5f-106">Hallo data-hoofdmap en het Hallo-bestandspad begrijpen</span><span class="sxs-lookup"><span data-stu-id="b0c5f-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="b0c5f-107">Zowel lokale uitvoering en Hallo U-SQL-SDK moet een gegevens-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="b0c5f-108">Hallo-gegevens-hoofdmap is een 'lokale store' voor Hallo lokale compute-account.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="b0c5f-109">Het is equivalente toohello Azure Data Lake Store-account van een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="b0c5f-110">Overschakelen van tooa is verschillende gegevens uit een hoofdmap net als andere store-account tooa overschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="b0c5f-111">Als u gegevens tooaccess vaak gedeeld met andere gegevens hoofdmappen wilt, moet u in uw scripts absolute paden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="b0c5f-112">Of het bestand system symbolische koppelingen maken (bijvoorbeeld **mklink** van NTFS) onder het Hallo-gegevenshoofdmap map toopoint toohello gedeelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="b0c5f-113">Hallo data-hoofdmap wordt gebruikt voor:</span><span class="sxs-lookup"><span data-stu-id="b0c5f-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="b0c5f-114">Metagegevens, zoals databases, tabellen, tabelfuncties (tvf's) en assembly's opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="b0c5f-115">Hallo invoer en uitvoerpaden die zijn gedefinieerd als relatieve paden in de U-SQL opzoeken.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="b0c5f-116">Gebruik relatieve paden maakt het eenvoudiger toodeploy uw tooAzure U-SQL-projecten.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="b0c5f-117">U kunt een relatief pad en een lokaal absoluut pad in U-SQL-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="b0c5f-118">Hallo relatief pad is relatief toohello opgegeven gegevenshoofdmap mappad.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="b0c5f-119">U wordt aangeraden dat u gebruik ' / ' Hallo als pad scheidingsteken toomake uw scripts die compatibel is met het Hallo-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="b0c5f-120">Hier volgen enkele voorbeelden van relatieve paden en hun equivalente absolute paden.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="b0c5f-121">In deze voorbeelden is C:\LocalRunDataRoot hello, gegevens-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="b0c5f-122">Relatief pad</span><span class="sxs-lookup"><span data-stu-id="b0c5f-122">Relative path</span></span>|<span data-ttu-id="b0c5f-123">Het absolute pad</span><span class="sxs-lookup"><span data-stu-id="b0c5f-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="b0c5f-124">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-124">/abc/def/input.csv</span></span> |<span data-ttu-id="b0c5f-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="b0c5f-126">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-126">abc/def/input.csv</span></span>  |<span data-ttu-id="b0c5f-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="b0c5f-128">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="b0c5f-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b0c5f-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="b0c5f-130">Gebruik lokale uitvoeren vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0c5f-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="b0c5f-131">Data Lake Tools voor Visual Studio biedt een U-SQL lokaal uitvoeren ervaring in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="b0c5f-132">Met behulp van deze functie kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b0c5f-132">By using this feature, you can:</span></span>

- <span data-ttu-id="b0c5f-133">Een U-SQL-script lokaal uitvoeren samen met C#-assembly's.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="b0c5f-134">Fouten opsporen in een C#-assembly lokaal.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="b0c5f-135">Maken, weergeven en verwijderen van U-SQL-catalogussen (lokale databases, assembly's, schema's en tabellen) in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="b0c5f-136">U kunt ook de lokale catalogus Hallo ook vinden in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren lokale catalogus](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="b0c5f-138">Hallo Data Lake Tools installatieprogramma maakt een C:\LocalRunRoot map toobe gebruikt als Hallo standaard gegevens-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="b0c5f-139">Hallo standaard lokaal uitvoeren parallelle uitvoering is 1.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="b0c5f-140">tooconfigure lokaal worden uitgevoerd in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0c5f-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="b0c5f-141">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="b0c5f-142">Open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="b0c5f-143">Vouw **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="b0c5f-144">Klik op Hallo **Data Lake** menu en klik vervolgens op **opties en instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="b0c5f-145">Vouw in de structuur van Hallo links **Azure Data Lake**, en vouw vervolgens **algemene**.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren configureren instellingen](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="b0c5f-147">Een Visual Studio U-SQL-project is vereist voor het uitvoeren van lokale uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="b0c5f-148">Dit onderdeel wijkt af van het uitvoeren van U-SQL-scripts uit Azure.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="b0c5f-149">lokaal toorun een U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="b0c5f-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="b0c5f-150">Open uw U-SQL-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="b0c5f-151">Met de rechtermuisknop op een U-SQL-script in Solution Explorer en klik vervolgens op **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="b0c5f-152">Selecteer **(lokaal)** zoals hello Analytics-toorun uw script lokaal account.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="b0c5f-153">U kunt ook klikken op Hallo **(lokaal)** account op Hallo boven in de script-venster en klik vervolgens op **indienen** (of gebruik Hallo Ctrl + F5 sneltoets).</span><span class="sxs-lookup"><span data-stu-id="b0c5f-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren indienen taken](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="b0c5f-155">Lokaal fouten opsporen in scripts en C#-assembly's</span><span class="sxs-lookup"><span data-stu-id="b0c5f-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="b0c5f-156">U kunt fouten opsporen C#-assembly's zonder verzenden en registreren tooAzure Data Lake Analytics-Service.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="b0c5f-157">U kunt onderbrekingspunten instellen in beide Hallo onderliggende-codebestand en in een waarnaar wordt verwezen C#-project.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="b0c5f-158">toodebug lokale code in onderliggende-codebestand</span><span class="sxs-lookup"><span data-stu-id="b0c5f-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="b0c5f-159">Onderbrekingspunten instellen in Hallo onderliggende-codebestand.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="b0c5f-160">Druk op F5 toodebug Hallo script lokaal.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="b0c5f-161">Hello te volgen procedure werkt alleen in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="b0c5f-162">In oudere Visual Studio u wellicht toomanually Hallo pdb-bestanden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="b0c5f-163">toodebug lokale code in een waarnaar wordt verwezen C#-project</span><span class="sxs-lookup"><span data-stu-id="b0c5f-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="b0c5f-164">Maak een C#-assemblyproject en bouw het toogenerate Hallo uitvoer-dll.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="b0c5f-165">Registreer Hallo dll-bestand met een U-SQL-instructie:</span><span class="sxs-lookup"><span data-stu-id="b0c5f-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="b0c5f-166">Onderbrekingspunten instellen in Hallo C#-code.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="b0c5f-167">Druk op F5 toodebug Hallo script dat verwijst naar lokaal Hallo C#-DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="b0c5f-168">Gebruik lokale uitvoeren vanaf Hallo Data Lake U-SQL-SDK</span><span class="sxs-lookup"><span data-stu-id="b0c5f-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="b0c5f-169">Bovendien toorunning U-SQL-scripts lokaal met behulp van Visual Studio, kunt u hello Azure Data Lake U-SQL-SDK toorun U-SQL-scripts lokaal met de opdrachtregel en programming interfaces.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="b0c5f-170">Via deze, kunt u uw lokale test U-SQL te schalen.</span><span class="sxs-lookup"><span data-stu-id="b0c5f-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="b0c5f-171">Meer informatie over [SDK van Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b0c5f-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0c5f-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0c5f-172">Next steps</span></span>

* <span data-ttu-id="b0c5f-173">Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="b0c5f-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="b0c5f-174">taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data Lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b0c5f-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="b0c5f-175">toouse hello hoekpunt uitvoering weergave Zie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="b0c5f-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
