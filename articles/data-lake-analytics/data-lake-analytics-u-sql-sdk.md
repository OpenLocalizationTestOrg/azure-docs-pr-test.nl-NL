---
title: aaaScale U-SQL lokaal uitvoeren en testen met Azure Data Lake U-SQL-SDK | Microsoft Docs
description: Ontdek hoe lokale toouse Azure Data Lake U-SQL-SDK tooscale U-SQL-taken uitvoeren en testen met de opdrachtregel en API's op uw lokale werkstation.
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="d7e3a-103">Schaal U-SQL lokaal uitvoeren en testen met Azure Data Lake U-SQL-SDK</span><span class="sxs-lookup"><span data-stu-id="d7e3a-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="d7e3a-104">Bij het ontwikkelen van U-SQL-script, is het algemene toorun en U-SQL-testscript lokaal vóór het indienen toocloud.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="d7e3a-105">Azure Data Lake biedt een Nuget-pakket Azure Data Lake U-SQL-SDK voor dit scenario aangeroepen, via die u kunt gemakkelijk de schaal van U-SQL lokaal uitvoeren en testen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="d7e3a-106">Het is ook mogelijk toointegrate dit U-SQL testen met CI (continue integratie) systeem tooautomate Hallo compileren en testen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="d7e3a-107">Als u het belangrijkst hoe toomanually lokale uitvoeren en fouten opsporen in U-SQL-script met GUI tooling, kunt u Azure Data Lake Tools voor Visual Studio gebruiken voor die.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="d7e3a-108">U kunt meer informatie van [hier](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="d7e3a-109">Installeren Azure Data Lake U-SQL-SDK</span><span class="sxs-lookup"><span data-stu-id="d7e3a-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="d7e3a-110">U krijgt hello Azure Data Lake U-SQL-SDK [hier](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) op Nuget.org. En voordat u deze gebruikt, moet u ervoor dat u als volgt afhankelijkheden hebt toomake.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="d7e3a-111">Afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="d7e3a-111">Dependencies</span></span>

<span data-ttu-id="d7e3a-112">Hallo SDK voor Data Lake U-SQL vereist Hallo afhankelijkheden te volgen:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="d7e3a-113">[Microsoft .NET Framework 4.6 of nieuwere](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="d7e3a-114">Microsoft Visual C++-14 en Windows-SDK 10.0.10240.0 of hoger (die wordt CppSDK in dit artikel genoemd).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="d7e3a-115">Er zijn twee manieren tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="d7e3a-116">Installeer [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="d7e3a-117">U hebt een \Windows Kits\10 map onder de map Program Files van Hallo--bijvoorbeeld C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="d7e3a-118">Ook vindt u Hallo Windows 10 SDK versie onder \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="d7e3a-119">Als u deze mappen niet ziet, installeer Visual Studio en ervoor tooselect Hallo SDK voor Windows 10 worden tijdens de installatie van Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="d7e3a-120">Als u dit geïnstalleerd met Visual Studio hebt, vindt lokale Hallo U-SQL-compiler deze automatisch.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools voor Visual Studio local-klaar Windows 10-SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="d7e3a-122">Installeer [Data Lake Tools voor Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="d7e3a-123">U vindt Hallo voorverpakt Visual C++- en Windows SDK-bestanden op C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="d7e3a-124">Hallo afhankelijkheden niet in dit geval automatisch door lokale U-SQL-compiler Hallo vinden.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="d7e3a-125">Hiervoor moet u toospecify hello CppSDK pad.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="d7e3a-126">Hallo bestanden tooanother locatie kopiëren of gebruikt u deze zo is.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="d7e3a-127">Basisconcepten begrijpen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="d7e3a-128">Gegevenshoofdmap</span><span class="sxs-lookup"><span data-stu-id="d7e3a-128">Data root</span></span>

<span data-ttu-id="d7e3a-129">Hallo-gegevens-hoofdmap is een 'lokale store' voor Hallo lokale compute-account.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="d7e3a-130">Het is equivalente toohello Azure Data Lake Store-account van een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="d7e3a-131">Overschakelen van tooa is verschillende gegevens uit een hoofdmap net als andere store-account tooa overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="d7e3a-132">Als u gegevens tooaccess vaak gedeeld met andere gegevens hoofdmappen wilt, moet u in uw scripts absolute paden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="d7e3a-133">Of het bestand system symbolische koppelingen maken (bijvoorbeeld **mklink** van NTFS) onder het Hallo-gegevenshoofdmap map toopoint toohello gedeelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="d7e3a-134">Hallo data-hoofdmap wordt gebruikt voor:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="d7e3a-135">Lokale metagegevens, zoals databases, tabellen, tabelfuncties (tvf's) en assembly's opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="d7e3a-136">Hallo invoer en uitvoerpaden die zijn gedefinieerd als relatieve paden in de U-SQL opzoeken.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="d7e3a-137">Gebruik relatieve paden maakt het eenvoudiger toodeploy uw tooAzure U-SQL-projecten.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="d7e3a-138">Bestandspad in U-SQL</span><span class="sxs-lookup"><span data-stu-id="d7e3a-138">File path in U-SQL</span></span>

<span data-ttu-id="d7e3a-139">U kunt een relatief pad en een lokaal absoluut pad in U-SQL-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="d7e3a-140">Hallo relatief pad is relatief toohello opgegeven gegevenshoofdmap mappad.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="d7e3a-141">U wordt aangeraden dat u gebruik ' / ' Hallo als pad scheidingsteken toomake uw scripts die compatibel is met het Hallo-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="d7e3a-142">Hier volgen enkele voorbeelden van relatieve paden en hun equivalente absolute paden.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="d7e3a-143">In deze voorbeelden is C:\LocalRunDataRoot hello, gegevens-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="d7e3a-144">Relatief pad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-144">Relative path</span></span>|<span data-ttu-id="d7e3a-145">Het absolute pad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="d7e3a-146">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-146">/abc/def/input.csv</span></span> |<span data-ttu-id="d7e3a-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="d7e3a-148">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-148">abc/def/input.csv</span></span>  |<span data-ttu-id="d7e3a-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="d7e3a-150">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="d7e3a-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d7e3a-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="d7e3a-152">Werkmap</span><span class="sxs-lookup"><span data-stu-id="d7e3a-152">Working directory</span></span>

<span data-ttu-id="d7e3a-153">Wanneer Hallo U-SQL-script lokaal wordt uitgevoerd, wordt een werkmap tijdens de compilatie onder de huidige actieve directory gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="d7e3a-154">Bovendien toohello compilatie levert, hello nodig runtime-bestanden voor lokale uitvoering worden shadow gekopieerde toothis werkmap.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="d7e3a-155">Hallo werken directory hoofdmap 'ScopeWorkDir' wordt genoemd en Hallo bestanden onder Hallo werkmap zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="d7e3a-156">Map/bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-156">Directory/file</span></span>|<span data-ttu-id="d7e3a-157">Map/bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-157">Directory/file</span></span>|<span data-ttu-id="d7e3a-158">Map/bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-158">Directory/file</span></span>|<span data-ttu-id="d7e3a-159">Definitie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-159">Definition</span></span>|<span data-ttu-id="d7e3a-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="d7e3a-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="d7e3a-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="d7e3a-162">Hash-tekenreeks van de runtime-versie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-162">Hash string of runtime version</span></span>|<span data-ttu-id="d7e3a-163">Schaduwkopie van de runtimebestanden die nodig zijn voor lokale uitvoering</span><span class="sxs-lookup"><span data-stu-id="d7e3a-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="d7e3a-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="d7e3a-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="d7e3a-165">De naam van een script + hash-tekenreeks van scriptpad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-165">Script name + hash string of script path</span></span>|<span data-ttu-id="d7e3a-166">Compilatie-uitvoer en uitvoering van stap logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="d7e3a-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="d7e3a-167">\_script\_.abr</span></span>|<span data-ttu-id="d7e3a-168">Compiler-uitvoer</span><span class="sxs-lookup"><span data-stu-id="d7e3a-168">Compiler output</span></span>|<span data-ttu-id="d7e3a-169">Wiskundige bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-169">Algebra file</span></span>|
| | |<span data-ttu-id="d7e3a-170">\_ScopeCodeGen\_. *</span><span class="sxs-lookup"><span data-stu-id="d7e3a-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="d7e3a-171">Compiler-uitvoer</span><span class="sxs-lookup"><span data-stu-id="d7e3a-171">Compiler output</span></span>|<span data-ttu-id="d7e3a-172">Beheerde code gegenereerd</span><span class="sxs-lookup"><span data-stu-id="d7e3a-172">Generated managed code</span></span>|
| | |<span data-ttu-id="d7e3a-173">\_ScopeCodeGenEngine\_. *</span><span class="sxs-lookup"><span data-stu-id="d7e3a-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="d7e3a-174">Compiler-uitvoer</span><span class="sxs-lookup"><span data-stu-id="d7e3a-174">Compiler output</span></span>|<span data-ttu-id="d7e3a-175">Gegenereerde systeemeigen code</span><span class="sxs-lookup"><span data-stu-id="d7e3a-175">Generated native code</span></span>|
| | |<span data-ttu-id="d7e3a-176">assemblies waarnaar wordt verwezen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-176">referenced assemblies</span></span>|<span data-ttu-id="d7e3a-177">Assembly-verwijzing</span><span class="sxs-lookup"><span data-stu-id="d7e3a-177">Assembly reference</span></span>|<span data-ttu-id="d7e3a-178">Bestanden van de assembly waarnaar wordt verwezen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="d7e3a-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="d7e3a-179">deployed_resources</span></span>|<span data-ttu-id="d7e3a-180">Resources implementeren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-180">Resource deployment</span></span>|<span data-ttu-id="d7e3a-181">Bronbestanden van de implementatie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="d7e3a-182">XXXXXXXX.xxx[1..n]\_\*. *</span><span class="sxs-lookup"><span data-stu-id="d7e3a-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="d7e3a-183">Uitvoeringslogboek</span><span class="sxs-lookup"><span data-stu-id="d7e3a-183">Execution log</span></span>|<span data-ttu-id="d7e3a-184">Logboek van de stappen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="d7e3a-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="d7e3a-185">Hallo SDK vanaf de opdrachtregel hello gebruiken</span><span class="sxs-lookup"><span data-stu-id="d7e3a-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="d7e3a-186">Opdrachtregelinterface van Hallo helper-toepassing</span><span class="sxs-lookup"><span data-stu-id="d7e3a-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="d7e3a-187">Onder de SDK-directory\build\runtime is LocalRunHelper.exe Hallo opdrachtregelprogramma toepassing die voorziet in interfaces toomost Hallo gebruikte lokaal uitvoeren functies.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="d7e3a-188">Houd er rekening mee dat zowel opdracht Hallo en Hallo schakelopties hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="d7e3a-189">tooinvoke het:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="d7e3a-190">LocalRunHelper.exe worden uitgevoerd zonder argumenten of met Hallo **help** overschakelen tooshow Hallo help-informatie:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="d7e3a-191">In Hallo help-informatie:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-191">In hello help information:</span></span>

-  <span data-ttu-id="d7e3a-192">**Opdracht** geeft de naam van de opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="d7e3a-193">**Een vereist Argument** een lijst met argumenten die moeten worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="d7e3a-194">**Optioneel Argument** een lijst met argumenten die optioneel, met standaardwaarden zijn.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="d7e3a-195">Optionele Booleaanse argumenten geen parameters hebben en hun uiterlijk betekenen negatieve tootheir standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="d7e3a-196">Retourwaarde en logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-196">Return value and logging</span></span>

<span data-ttu-id="d7e3a-197">retourneert de helper-toepassing Hello **0** voor succes en **-1** van de fout.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="d7e3a-198">Hallo helper verzendt standaard alle berichten toohello huidige console.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="d7e3a-199">De meeste opdrachten Hallo ondersteunen echter Hallo **- MessageOut pad_naar_logboekbestand** optioneel argument die enterpriseenrollment.contoso.com Hallo levert tooa logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="d7e3a-200">Omgeving variabele configureren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-200">Environment variable configuring</span></span>

<span data-ttu-id="d7e3a-201">U-SQL lokaal moet een hoofdmap opgegeven gegevens run as-account met lokale opslag, evenals een opgegeven pad CppSDK voor afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="d7e3a-202">U kunt beide argument set Hallo in opdrachtregel- of stel omgevingsvariabele voor hen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="d7e3a-203">Set Hallo **SCOPE_CPP_SDK** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="d7e3a-204">Als u Microsoft Visual C++ en Hallo Windows SDK door het installeren van Data Lake Tools voor Visual Studio, Controleer of u Hallo volgende map:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="d7e3a-205">Definieer een nieuwe omgevingsvariabele aangeroepen **SCOPE_CPP_SDK** toopoint toothis directory.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="d7e3a-206">Of Hallo map toohello andere locatie kopiëren en geef **SCOPE_CPP_SDK** als die.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="d7e3a-207">In de omgevingsvariabele voor toevoeging toosetting hello, kunt u Hallo **- CppSDK** argument wanneer u Hallo vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="d7e3a-208">Dit argument overschrijft uw standaard CppSDK-omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="d7e3a-209">Set Hallo **LOCALRUN_DATAROOT** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="d7e3a-210">Definieer een nieuwe omgevingsvariabele aangeroepen **LOCALRUN_DATAROOT** die toohello gegevenshoofdmap verwijst.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="d7e3a-211">In de omgevingsvariabele voor toevoeging toosetting hello, kunt u Hallo **- DataRoot** argument met het Hallo-gegevenshoofdmap pad wanneer u een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="d7e3a-212">Dit argument wordt overschreven door de omgevingsvariabele van uw standaard-hoofdmap van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="d7e3a-213">U moet dit argument tooevery vanaf de opdrachtregel uitvoert zodat u kunt Hallo standaard gegevenshoofdmap omgevingsvariabele voor alle bewerkingen overschrijven tooadd.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="d7e3a-214">SDK opdrachtregel usage-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d7e3a-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="d7e3a-215">Compileren en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-215">Compile and run</span></span>

<span data-ttu-id="d7e3a-216">Hallo **uitvoeren** opdracht wordt gebruikt voor toocompile Hallo script en vervolgens de resultaten wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="d7e3a-217">De opdrachtregelargumenten zijn een combinatie van die van **compileren** en **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="d7e3a-218">Hallo volgen optionele argumenten voor **uitvoeren**:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="d7e3a-219">Argument</span><span class="sxs-lookup"><span data-stu-id="d7e3a-219">Argument</span></span>|<span data-ttu-id="d7e3a-220">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="d7e3a-220">Default value</span></span>|<span data-ttu-id="d7e3a-221">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="d7e3a-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="d7e3a-222">-CodeBehind</span></span>|<span data-ttu-id="d7e3a-223">False</span><span class="sxs-lookup"><span data-stu-id="d7e3a-223">False</span></span>|<span data-ttu-id="d7e3a-224">Hallo-script heeft .cs code achter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="d7e3a-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="d7e3a-225">-CppSDK</span></span>| |<span data-ttu-id="d7e3a-226">CppSDK Directory</span><span class="sxs-lookup"><span data-stu-id="d7e3a-226">CppSDK Directory</span></span>|
|<span data-ttu-id="d7e3a-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="d7e3a-227">-DataRoot</span></span>| <span data-ttu-id="d7e3a-228">De omgevingsvariabele DataRoot</span><span class="sxs-lookup"><span data-stu-id="d7e3a-228">DataRoot environment variable</span></span>|<span data-ttu-id="d7e3a-229">DataRoot voor lokale uitvoering te standaard 'LOCALRUN_DATAROOT'-omgevingsvariabele</span><span class="sxs-lookup"><span data-stu-id="d7e3a-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="d7e3a-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="d7e3a-230">-MessageOut</span></span>| |<span data-ttu-id="d7e3a-231">Dump berichten op console tooa bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="d7e3a-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="d7e3a-232">-Parallel</span></span>|<span data-ttu-id="d7e3a-233">1</span><span class="sxs-lookup"><span data-stu-id="d7e3a-233">1</span></span>|<span data-ttu-id="d7e3a-234">Voer Hallo plan met Hallo opgegeven parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="d7e3a-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="d7e3a-235">-Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-235">-References</span></span>| |<span data-ttu-id="d7e3a-236">Lijst met paden tooextra verwijzings-assembly's of de gegevensbestanden van de code achter, gescheiden door ';'</span><span class="sxs-lookup"><span data-stu-id="d7e3a-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="d7e3a-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="d7e3a-237">-UdoRedirect</span></span>|<span data-ttu-id="d7e3a-238">False</span><span class="sxs-lookup"><span data-stu-id="d7e3a-238">False</span></span>|<span data-ttu-id="d7e3a-239">Udo assembly omleiding config genereren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="d7e3a-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="d7e3a-240">-UseDatabase</span></span>|<span data-ttu-id="d7e3a-241">model</span><span class="sxs-lookup"><span data-stu-id="d7e3a-241">master</span></span>|<span data-ttu-id="d7e3a-242">Database-toouse voor code achter tijdelijke assembly-registratie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="d7e3a-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="d7e3a-243">-Verbose</span></span>|<span data-ttu-id="d7e3a-244">False</span><span class="sxs-lookup"><span data-stu-id="d7e3a-244">False</span></span>|<span data-ttu-id="d7e3a-245">Gedetailleerde uitvoer van de runtime weergeven</span><span class="sxs-lookup"><span data-stu-id="d7e3a-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="d7e3a-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-246">-WorkDir</span></span>|<span data-ttu-id="d7e3a-247">Huidige map</span><span class="sxs-lookup"><span data-stu-id="d7e3a-247">Current Directory</span></span>|<span data-ttu-id="d7e3a-248">Map voor de compiler gebruiks- en uitvoer</span><span class="sxs-lookup"><span data-stu-id="d7e3a-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="d7e3a-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="d7e3a-249">-RunScopeCEP</span></span>|<span data-ttu-id="d7e3a-250">0</span><span class="sxs-lookup"><span data-stu-id="d7e3a-250">0</span></span>|<span data-ttu-id="d7e3a-251">ScopeCEP modus toouse</span><span class="sxs-lookup"><span data-stu-id="d7e3a-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="d7e3a-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="d7e3a-253">TEMP</span><span class="sxs-lookup"><span data-stu-id="d7e3a-253">temp</span></span>|<span data-ttu-id="d7e3a-254">Toouse temp-pad voor het streamen van gegevens</span><span class="sxs-lookup"><span data-stu-id="d7e3a-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="d7e3a-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="d7e3a-255">-OptFlags</span></span>| |<span data-ttu-id="d7e3a-256">Door komma's gescheiden lijst met optimalisatie van vlaggen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="d7e3a-257">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="d7e3a-258">Naast combineren **compileren** en **uitvoeren**, u kunt compileren en uitvoerbare bestanden Hallo gecompileerd afzonderlijk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="d7e3a-259">Compileren van een U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="d7e3a-259">Compile a U-SQL script</span></span>

<span data-ttu-id="d7e3a-260">Hallo **compileren** opdracht gebruikte toocompile een U-SQL-script tooexecutables is.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="d7e3a-261">Hallo volgen optionele argumenten voor **compileren**:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="d7e3a-262">Argument</span><span class="sxs-lookup"><span data-stu-id="d7e3a-262">Argument</span></span>|<span data-ttu-id="d7e3a-263">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="d7e3a-264">-CodeBehind [standaardwaarde 'False']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="d7e3a-265">Hallo-script heeft .cs code achter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="d7e3a-266">-CppSDK [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="d7e3a-267">CppSDK Directory</span><span class="sxs-lookup"><span data-stu-id="d7e3a-267">CppSDK Directory</span></span>|
| <span data-ttu-id="d7e3a-268">-DataRoot [standaardwaarde 'Omgevingsvariabele DataRoot']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="d7e3a-269">DataRoot voor lokale uitvoering te standaard 'LOCALRUN_DATAROOT'-omgevingsvariabele</span><span class="sxs-lookup"><span data-stu-id="d7e3a-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="d7e3a-270">-MessageOut [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="d7e3a-271">Dump berichten op console tooa bestand</span><span class="sxs-lookup"><span data-stu-id="d7e3a-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="d7e3a-272">-Verwijst naar [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-272">-References [default value '']</span></span>|<span data-ttu-id="d7e3a-273">Lijst met paden tooextra verwijzings-assembly's of de gegevensbestanden van de code achter, gescheiden door ';'</span><span class="sxs-lookup"><span data-stu-id="d7e3a-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="d7e3a-274">-Recente [standaardwaarde 'False']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="d7e3a-275">Recente compileren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-275">Shallow compile</span></span>|
| <span data-ttu-id="d7e3a-276">-UdoRedirect [standaardwaarde 'False']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="d7e3a-277">Udo assembly omleiding config genereren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="d7e3a-278">-UseDatabase [standaardwaarde 'master']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="d7e3a-279">Database-toouse voor code achter tijdelijke assembly-registratie</span><span class="sxs-lookup"><span data-stu-id="d7e3a-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="d7e3a-280">-WorkDir [standaardwaarde 'Huidige map']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="d7e3a-281">Map voor de compiler gebruiks- en uitvoer</span><span class="sxs-lookup"><span data-stu-id="d7e3a-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="d7e3a-282">-RunScopeCEP [standaardwaarde '0']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="d7e3a-283">ScopeCEP modus toouse</span><span class="sxs-lookup"><span data-stu-id="d7e3a-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="d7e3a-284">-ScopeCEPTempPath [standaardwaarde 'temp']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="d7e3a-285">Toouse temp-pad voor het streamen van gegevens</span><span class="sxs-lookup"><span data-stu-id="d7e3a-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="d7e3a-286">-OptFlags [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="d7e3a-287">Door komma's gescheiden lijst met optimalisatie van vlaggen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="d7e3a-288">Hier volgen enkele voorbeelden van het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-288">Here are some usage examples.</span></span>

<span data-ttu-id="d7e3a-289">Compileren van een U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="d7e3a-290">Compileren van een U-SQL-script en stel Hallo data-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="d7e3a-291">Houd er rekening mee dat dit Hallo set omgevingsvariabele wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="d7e3a-292">Compileren van een U-SQL-script en stel een werkmap, de referentie-assembly en de database:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="d7e3a-293">Gecompileerde resultaten uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-293">Execute compiled results</span></span>

<span data-ttu-id="d7e3a-294">Hallo **uitvoeren** opdracht is gebruikte tooexecute gecompileerd resultaten.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="d7e3a-295">Hallo volgen optionele argumenten voor **uitvoeren**:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="d7e3a-296">Argument</span><span class="sxs-lookup"><span data-stu-id="d7e3a-296">Argument</span></span>|<span data-ttu-id="d7e3a-297">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="d7e3a-298">-DataRoot [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="d7e3a-299">De gegevenshoofdmap voor de uitvoering van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-299">Data root for metadata execution.</span></span> <span data-ttu-id="d7e3a-300">Wordt standaard toohello **LOCALRUN_DATAROOT** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="d7e3a-301">-MessageOut [standaardwaarde '']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="d7e3a-302">Dump berichten op het Hallo-console tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="d7e3a-303">-Parallel standaardwaarde '1'</span><span class="sxs-lookup"><span data-stu-id="d7e3a-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="d7e3a-304">Indicator toorun Hallo gegenereerd lokaal uitvoeren stappen Hello opgegeven parallelle uitvoering niveau.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="d7e3a-305">-Verbose [standaardwaarde 'False']</span><span class="sxs-lookup"><span data-stu-id="d7e3a-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="d7e3a-306">Indicator tooshow gedetailleerde uitvoer van de runtime.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="d7e3a-307">Hier volgt een voorbeeld van gebruik:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="d7e3a-308">Hallo SDK gebruiken met API 's</span><span class="sxs-lookup"><span data-stu-id="d7e3a-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="d7e3a-309">Hallo-API's bevinden zich in Hallo LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="d7e3a-310">U kunt ze toointegrate Hallo functionaliteit van Hallo U-SQL-SDK gebruiken en C# test framework tooscale Hallo uw U-SQL-script lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="d7e3a-311">In dit artikel ik gebruik Hallo standaard C#-eenheid test project tooshow hoe toouse deze interfaces tootest uw U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="d7e3a-312">Stap 1: C#-eenheid test-project en de configuratie maken</span><span class="sxs-lookup"><span data-stu-id="d7e3a-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="d7e3a-313">Maak een C#-eenheid test-project via Bestand > Nieuw > Project > Visual C# > testen > Project eenheid testen.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="d7e3a-314">LocalRunHelper.exe toevoegen als een verwijzing voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="d7e3a-315">Hallo LocalRunHelper.exe bevindt zich op \build\runtime\LocalRunHelper.exe in Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL-SDK verwijzing toevoegen](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="d7e3a-317">U-SQL-SDK **alleen** x64 ondersteuningsomgeving, zorg ervoor dat tooset build platform doel als x64.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="d7e3a-318">Dat kunt u instellen via projecteigenschap > bouwen > Platform doel.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL-SDK configureren x64 Project](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="d7e3a-320">Zorg ervoor dat tooset uw testomgeving als x64.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="d7e3a-321">In Visual Studio kunt u dit instellen via testen > instellingen testen > processorarchitectuur standaard > x64.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL-SDK configureren x64 testomgeving](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="d7e3a-323">Zorg ervoor dat toocopy alle afhankelijkheidsbestanden onder NugetPackage\build\runtime\ tooproject werkmap namelijk doorgaans ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="d7e3a-324">Stap 2: Maak Testscenario U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="d7e3a-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="d7e3a-325">Hieronder vindt u de voorbeeldcode Hallo voor U-SQL-script test.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="d7e3a-326">Voor het testen, moet u tooprepare scripts, invoerbestanden en bestanden van de verwachte uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="d7e3a-327">Programming interfaces in LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="d7e3a-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="d7e3a-328">LocalRunHelper.exe biedt Hallo programming interfaces voor de U-SQL lokaal compileren, uitvoeren, enz. Hallo interfaces als volgt worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="d7e3a-329">**Constructor**</span><span class="sxs-lookup"><span data-stu-id="d7e3a-329">**Constructor**</span></span>

<span data-ttu-id="d7e3a-330">openbare LocalRunHelper ([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="d7e3a-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="d7e3a-331">Parameter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-331">Parameter</span></span>|<span data-ttu-id="d7e3a-332">Type</span><span class="sxs-lookup"><span data-stu-id="d7e3a-332">Type</span></span>|<span data-ttu-id="d7e3a-333">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="d7e3a-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="d7e3a-334">messageOutput</span></span>|<span data-ttu-id="d7e3a-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-335">System.IO.TextWriter</span></span>|<span data-ttu-id="d7e3a-336">voor Uitvoerberichten, stelt u toonull toouse Console</span><span class="sxs-lookup"><span data-stu-id="d7e3a-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="d7e3a-337">**Eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="d7e3a-337">**Properties**</span></span>

|<span data-ttu-id="d7e3a-338">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d7e3a-338">Property</span></span>|<span data-ttu-id="d7e3a-339">Type</span><span class="sxs-lookup"><span data-stu-id="d7e3a-339">Type</span></span>|<span data-ttu-id="d7e3a-340">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="d7e3a-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-341">AlgebraPath</span></span>|<span data-ttu-id="d7e3a-342">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-342">string</span></span>|<span data-ttu-id="d7e3a-343">Hallo pad tooalgebra bestand (wiskundige-bestand is een van de resultaten van Hallo compilatie)</span><span class="sxs-lookup"><span data-stu-id="d7e3a-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="d7e3a-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="d7e3a-344">CodeBehindReferences</span></span>|<span data-ttu-id="d7e3a-345">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-345">string</span></span>|<span data-ttu-id="d7e3a-346">Als Hallo script aanvullende code achter verwijzingen heeft, geeft u Hallo paden van elkaar gescheiden door ';'</span><span class="sxs-lookup"><span data-stu-id="d7e3a-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="d7e3a-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-347">CppSdkDir</span></span>|<span data-ttu-id="d7e3a-348">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-348">string</span></span>|<span data-ttu-id="d7e3a-349">CppSDK directory</span><span class="sxs-lookup"><span data-stu-id="d7e3a-349">CppSDK directory</span></span>|
|<span data-ttu-id="d7e3a-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-350">CurrentDir</span></span>|<span data-ttu-id="d7e3a-351">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-351">string</span></span>|<span data-ttu-id="d7e3a-352">Huidige map</span><span class="sxs-lookup"><span data-stu-id="d7e3a-352">Current directory</span></span>|
|<span data-ttu-id="d7e3a-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="d7e3a-353">DataRoot</span></span>|<span data-ttu-id="d7e3a-354">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-354">string</span></span>|<span data-ttu-id="d7e3a-355">Pad naar de hoofdmap van gegevens</span><span class="sxs-lookup"><span data-stu-id="d7e3a-355">Data root path</span></span>|
|<span data-ttu-id="d7e3a-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-356">DebuggerMailPath</span></span>|<span data-ttu-id="d7e3a-357">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-357">string</span></span>|<span data-ttu-id="d7e3a-358">Hallo pad toodebugger mailslot</span><span class="sxs-lookup"><span data-stu-id="d7e3a-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="d7e3a-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="d7e3a-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="d7e3a-360">BOOL</span><span class="sxs-lookup"><span data-stu-id="d7e3a-360">bool</span></span>|<span data-ttu-id="d7e3a-361">Als we willen toogenerate assembly geladen omleiding config overschrijven</span><span class="sxs-lookup"><span data-stu-id="d7e3a-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="d7e3a-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="d7e3a-362">HasCodeBehind</span></span>|<span data-ttu-id="d7e3a-363">BOOL</span><span class="sxs-lookup"><span data-stu-id="d7e3a-363">bool</span></span>|<span data-ttu-id="d7e3a-364">Als Hallo script heeft code achter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-364">If hello script has code behind</span></span>|
|<span data-ttu-id="d7e3a-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-365">InputDir</span></span>|<span data-ttu-id="d7e3a-366">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-366">string</span></span>|<span data-ttu-id="d7e3a-367">Map voor invoergegevens</span><span class="sxs-lookup"><span data-stu-id="d7e3a-367">Directory for input data</span></span>|
|<span data-ttu-id="d7e3a-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-368">MessagePath</span></span>|<span data-ttu-id="d7e3a-369">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-369">string</span></span>|<span data-ttu-id="d7e3a-370">Bericht dump bestandspad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-370">Message dump file path</span></span>|
|<span data-ttu-id="d7e3a-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-371">OutputDir</span></span>|<span data-ttu-id="d7e3a-372">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-372">string</span></span>|<span data-ttu-id="d7e3a-373">Map voor de uitvoergegevens</span><span class="sxs-lookup"><span data-stu-id="d7e3a-373">Directory for output data</span></span>|
|<span data-ttu-id="d7e3a-374">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="d7e3a-374">Parallelism</span></span>|<span data-ttu-id="d7e3a-375">int</span><span class="sxs-lookup"><span data-stu-id="d7e3a-375">int</span></span>|<span data-ttu-id="d7e3a-376">Parallelle uitvoering toorun Hallo wiskundige</span><span class="sxs-lookup"><span data-stu-id="d7e3a-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="d7e3a-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="d7e3a-377">ParentPid</span></span>|<span data-ttu-id="d7e3a-378">int</span><span class="sxs-lookup"><span data-stu-id="d7e3a-378">int</span></span>|<span data-ttu-id="d7e3a-379">PID van Hallo bovenliggende op welke Hallo service tooexit, set too0 of negatieve tooignore bewaakt</span><span class="sxs-lookup"><span data-stu-id="d7e3a-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="d7e3a-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-380">ResultPath</span></span>|<span data-ttu-id="d7e3a-381">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-381">string</span></span>|<span data-ttu-id="d7e3a-382">Resultaat dump bestandspad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-382">Result dump file path</span></span>|
|<span data-ttu-id="d7e3a-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-383">RuntimeDir</span></span>|<span data-ttu-id="d7e3a-384">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-384">string</span></span>|<span data-ttu-id="d7e3a-385">Runtime-map</span><span class="sxs-lookup"><span data-stu-id="d7e3a-385">Runtime directory</span></span>|
|<span data-ttu-id="d7e3a-386">scriptPath</span><span class="sxs-lookup"><span data-stu-id="d7e3a-386">ScriptPath</span></span>|<span data-ttu-id="d7e3a-387">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-387">string</span></span>|<span data-ttu-id="d7e3a-388">Waar toofind script Hallo</span><span class="sxs-lookup"><span data-stu-id="d7e3a-388">Where toofind hello script</span></span>|
|<span data-ttu-id="d7e3a-389">Recente</span><span class="sxs-lookup"><span data-stu-id="d7e3a-389">Shallow</span></span>|<span data-ttu-id="d7e3a-390">BOOL</span><span class="sxs-lookup"><span data-stu-id="d7e3a-390">bool</span></span>|<span data-ttu-id="d7e3a-391">Recente compileren of niet</span><span class="sxs-lookup"><span data-stu-id="d7e3a-391">Shallow compile or not</span></span>|
|<span data-ttu-id="d7e3a-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-392">TempDir</span></span>|<span data-ttu-id="d7e3a-393">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-393">string</span></span>|<span data-ttu-id="d7e3a-394">Tijdelijke map</span><span class="sxs-lookup"><span data-stu-id="d7e3a-394">Temp directory</span></span>|
|<span data-ttu-id="d7e3a-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="d7e3a-395">UseDataBase</span></span>|<span data-ttu-id="d7e3a-396">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-396">string</span></span>|<span data-ttu-id="d7e3a-397">Hallo database toouse voor code achter tijdelijke assembly-registratie, master standaard opgeven</span><span class="sxs-lookup"><span data-stu-id="d7e3a-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="d7e3a-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="d7e3a-398">WorkDir</span></span>|<span data-ttu-id="d7e3a-399">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d7e3a-399">string</span></span>|<span data-ttu-id="d7e3a-400">Voorkeur werkmap</span><span class="sxs-lookup"><span data-stu-id="d7e3a-400">Preferred working directory</span></span>|


<span data-ttu-id="d7e3a-401">**Methode**</span><span class="sxs-lookup"><span data-stu-id="d7e3a-401">**Method**</span></span>

|<span data-ttu-id="d7e3a-402">Methode</span><span class="sxs-lookup"><span data-stu-id="d7e3a-402">Method</span></span>|<span data-ttu-id="d7e3a-403">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7e3a-403">Description</span></span>|<span data-ttu-id="d7e3a-404">retourneren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-404">Return</span></span>|<span data-ttu-id="d7e3a-405">Parameter</span><span class="sxs-lookup"><span data-stu-id="d7e3a-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="d7e3a-406">openbare bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="d7e3a-406">public bool DoCompile()</span></span>|<span data-ttu-id="d7e3a-407">Hallo U-SQL-script compileren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="d7e3a-408">True indien geslaagd</span><span class="sxs-lookup"><span data-stu-id="d7e3a-408">True on success</span></span>| |
|<span data-ttu-id="d7e3a-409">openbare bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="d7e3a-409">public bool DoExec()</span></span>|<span data-ttu-id="d7e3a-410">Hallo gecompileerd resultaat uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d7e3a-410">Execute hello compiled result</span></span>|<span data-ttu-id="d7e3a-411">True indien geslaagd</span><span class="sxs-lookup"><span data-stu-id="d7e3a-411">True on success</span></span>| |
|<span data-ttu-id="d7e3a-412">openbare bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="d7e3a-412">public bool DoRun()</span></span>|<span data-ttu-id="d7e3a-413">Voer Hallo U-SQL-script (compileren + uitvoeren)</span><span class="sxs-lookup"><span data-stu-id="d7e3a-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="d7e3a-414">True indien geslaagd</span><span class="sxs-lookup"><span data-stu-id="d7e3a-414">True on success</span></span>| |
|<span data-ttu-id="d7e3a-415">openbare bool IsValidRuntimeDir (pad tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="d7e3a-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="d7e3a-416">Controleer of de Hallo opgegeven pad geldig runtime pad</span><span class="sxs-lookup"><span data-stu-id="d7e3a-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="d7e3a-417">Geldt voor geldige</span><span class="sxs-lookup"><span data-stu-id="d7e3a-417">True for valid</span></span>|<span data-ttu-id="d7e3a-418">Hallo-pad van de runtime-map</span><span class="sxs-lookup"><span data-stu-id="d7e3a-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="d7e3a-419">Veelgestelde vragen over veel voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="d7e3a-420">Fout 1:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-420">Error 1:</span></span>
<span data-ttu-id="d7e3a-421">E_CSC_SYSTEM_INTERNAL: Interne fout!</span><span class="sxs-lookup"><span data-stu-id="d7e3a-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="d7e3a-422">Kan bestand of assembly 'ScopeEngineManaged.dll' of een afhankelijkheid hiervan niet laden.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="d7e3a-423">de opgegeven module Hallo kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-423">hello specified module could not be found.</span></span>

<span data-ttu-id="d7e3a-424">Neem contact op met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d7e3a-424">Please check hello following:</span></span>

- <span data-ttu-id="d7e3a-425">Zorg ervoor dat u hebt x64 omgeving.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="d7e3a-426">Hallo build-doelplatform en Hallo testomgeving moet worden x64, raadpleeg dan te**stap 1: eenheid maken C#-project en configuratie testen** hierboven.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="d7e3a-427">Zorg ervoor dat u alle afhankelijkheidsbestanden onder NugetPackage\build\runtime\ tooproject werkmap hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="d7e3a-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7e3a-428">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7e3a-428">Next steps</span></span>

* <span data-ttu-id="d7e3a-429">toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="d7e3a-430">toolog diagnostische informatie, Zie [toegang tot logboeken met diagnostische gegevens voor Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="d7e3a-431">Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="d7e3a-432">taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data Lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="d7e3a-433">toouse hello hoekpunt uitvoering weergave Zie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="d7e3a-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
