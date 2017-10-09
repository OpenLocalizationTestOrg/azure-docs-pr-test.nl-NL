---
title: aaaDebug U-SQL-taken | Microsoft Docs
description: Meer informatie over hoe hoekpunt met Visual Studio in toodebug een U-SQL is mislukt.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="93e48-103">Foutopsporing van de gebruiker gedefinieerde C#-code voor mislukte U-SQL-taken</span><span class="sxs-lookup"><span data-stu-id="93e48-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="93e48-104">U-SQL biedt een model van uitbreidbaarheid met C#, dus u kunt de functionaliteit van uw code tooadd zoals een aangepaste zelfstandig uitpakken of reducer schrijven.</span><span class="sxs-lookup"><span data-stu-id="93e48-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="93e48-105">toolearn meer, Zie [U-SQL programmeerbaarheid handleiding](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="93e48-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="93e48-106">In de praktijk code mogelijk moet foutopsporing en big-datasystemen leveren alleen beperkt runtime foutopsporingsinformatie zoals logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="93e48-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="93e48-107">Azure Data Lake Tools voor Visual Studio biedt een functie **hoekpunt foutopsporing kan niet**, waarmee u een mislukte taak van Hallo cloud tooyour lokale computer voor het opsporen van klonen.</span><span class="sxs-lookup"><span data-stu-id="93e48-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="93e48-108">Hallo lokale kloon vastgelegd Hallo gehele cloudomgeving, inclusief eventuele invoergegevens en gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="93e48-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="93e48-109">Hallo toont volgende video mislukt hoekpunt fouten opsporen in Azure Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93e48-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="93e48-110">Visual Studio Hallo na twee updates is vereist als ze nog niet zijn geïnstalleerd: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) en de [universeel C Runtime voor Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="93e48-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="93e48-111">Het downloaden is mislukt hoekpunt toolocal machine</span><span class="sxs-lookup"><span data-stu-id="93e48-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="93e48-112">Als u een taak die is mislukt in Azure Data Lake Tools voor Visual Studio opent, ziet u een gele waarschuwing balk met gedetailleerde foutberichten in het tabblad Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="93e48-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="93e48-113">Klik op **downloaden** toodownload alle Hallo vereiste resources en invoer stromen.</span><span class="sxs-lookup"><span data-stu-id="93e48-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="93e48-114">Als het Hallo-download niet voltooien, klikt u op **probeer**.</span><span class="sxs-lookup"><span data-stu-id="93e48-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="93e48-115">Klik op **Open** nadat Hallo downloaden is voltooid toogenerate een lokale foutopsporingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="93e48-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="93e48-116">Een nieuw exemplaar van de Visual Studio met een oplossing voor foutopsporing is automatisch gemaakt en geopend.</span><span class="sxs-lookup"><span data-stu-id="93e48-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL foutopsporing visual studio downloaden hoekpunt](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="93e48-118">Taken kunnen de bronbestanden van de code-behind of geregistreerde assembly's bevatten, en deze twee typen hebben verschillende scenario's voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="93e48-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="93e48-119">Fouten opsporen in een taak die is mislukt met code-behind</span><span class="sxs-lookup"><span data-stu-id="93e48-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="93e48-120">Fouten opsporen in een mislukte taak met assembly 's</span><span class="sxs-lookup"><span data-stu-id="93e48-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="93e48-121">Taak is mislukt met de code-behind voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="93e48-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="93e48-122">Als een U-SQL-taak is mislukt en Hallo taak bevat een gebruikerscode (meestal onder de naam `Script.usql.cs` in een project U-SQL), dat de broncode wordt geïmporteerd in Hallo foutopsporing oplossing.</span><span class="sxs-lookup"><span data-stu-id="93e48-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="93e48-123">Daar kunt u Hallo Visual Studio foutopsporing hulpprogramma's (controle, variabelen, enz.) tootroubleshoot Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="93e48-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="93e48-124">Voordat u foutopsporing, moet u ervoor toocheck **Common Language Runtime uitzonderingen** in Hallo uitzondering instellingen venster (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="93e48-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL foutopsporing visual studio-instelling](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="93e48-126">Druk op **F5** toorun Hallo code-behind code.</span><span class="sxs-lookup"><span data-stu-id="93e48-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="93e48-127">Deze wordt uitgevoerd totdat deze is gestopt vanwege een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="93e48-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="93e48-128">Open Hallo `ADLTool_Codebehind.usql.cs` bestands- en Stel onderbrekingspunten, drukt u vervolgens op **F5** toodebug Hallo code stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="93e48-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL-uitzondering voor foutopsporing](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="93e48-130">Taak is mislukt met de assembly's voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="93e48-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="93e48-131">Als u geregistreerde assembly's in uw U-SQL-script gebruikt, kan geen Hallo system Hallo broncode automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="93e48-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="93e48-132">In dit geval hello assembly source code bestanden toohello oplossing handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="93e48-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="93e48-133">Hallo-oplossing configureren</span><span class="sxs-lookup"><span data-stu-id="93e48-133">Configure hello solution</span></span>

1. <span data-ttu-id="93e48-134">Met de rechtermuisknop op **oplossing 'VertexDebug' > toevoegen > bestaand Project...**  toofind Hallo broncode van de assembly's en Hallo project toohello foutopsporing oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="93e48-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL-foutopsporing project toevoegen](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="93e48-136">Met de rechtermuisknop op **LocalVertexHost > eigenschappen** in de oplossing en kopieer Hallo Hallo **werkmap** pad.</span><span class="sxs-lookup"><span data-stu-id="93e48-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="93e48-137">Met de rechtermuisknop op **CodeProject voor assembly-bron > eigenschappen**, selecteer Hallo **bouwen** tabblad aan de linkerkant en plak Hallo gekopieerd pad als **uitvoer > uitvoerpad**.</span><span class="sxs-lookup"><span data-stu-id="93e48-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL-foutopsporing instellen pdb pad](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="93e48-139">Druk op **Ctrl + Alt + E**, Controleer **Common Language Runtime uitzonderingen** in het venster Instellingen voor uitzondering.</span><span class="sxs-lookup"><span data-stu-id="93e48-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="93e48-140">Foutopsporing starten</span><span class="sxs-lookup"><span data-stu-id="93e48-140">Start debug</span></span>

1. <span data-ttu-id="93e48-141">Met de rechtermuisknop op **CodeProject voor assembly-bron > opnieuw samenstellen** toooutput .pdb bestanden toohello `LocalVertexHost` werkmap.</span><span class="sxs-lookup"><span data-stu-id="93e48-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="93e48-142">Druk op **F5** en het Hallo-project wordt uitgevoerd totdat deze is gestopt vanwege een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="93e48-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="93e48-143">Mogelijk ziet u Hallo volgende waarschuwingsbericht weergegeven, kunt u veilig negeren.</span><span class="sxs-lookup"><span data-stu-id="93e48-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="93e48-144">Tooa minuut tooget toohello foutopsporing scherm kan duren.</span><span class="sxs-lookup"><span data-stu-id="93e48-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL foutopsporing visual studio-waarschuwing](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="93e48-146">Open de broncode en Stel onderbrekingspunten, drukt u vervolgens op **F5** toodebug Hallo code stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="93e48-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="93e48-147">U kunt ook Hallo Visual Studio foutopsporing hulpprogramma's (controle, variabelen, enz.) tootroubleshoot Hallo probleem gebruiken.</span><span class="sxs-lookup"><span data-stu-id="93e48-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="93e48-148">Opnieuw samenstellen Hallo assembly bron CodeProject telkens nadat u Hallo code toogenerate bijgewerkt .pdb bestanden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="93e48-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="93e48-149">Als Hallo-project met succes voltooid wordt toont Hallo uitvoervenster na foutopsporing, Hallo volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="93e48-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL-foutopsporing is mislukt](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="93e48-151">Hallo taak verzenden</span><span class="sxs-lookup"><span data-stu-id="93e48-151">Resubmit hello job</span></span>

<span data-ttu-id="93e48-152">Als u klaar bent met het opsporen van fouten opnieuw indienen Hallo mislukte taak.</span><span class="sxs-lookup"><span data-stu-id="93e48-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="93e48-153">Voor taken met oplossingen voor code-behind uw C#-code naar Hallo code-behind bronbestand kopiëren (meestal `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="93e48-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="93e48-154">Registreren voor taken met assembly's, Hallo bijgewerkt .dll-assembly's in uw database ADLA:</span><span class="sxs-lookup"><span data-stu-id="93e48-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="93e48-155">Vouw Hallo van Server Explorer of Cloud Explorer **ADLA account > Databases** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="93e48-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="93e48-156">Met de rechtermuisknop op **assembly's** en registreren van uw nieuwe .dll-assembly's met de Hallo ADLA database: ![Azure Data Lake Analytics U-SQL-foutopsporing assembly registreren](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="93e48-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="93e48-157">De taak opnieuw.</span><span class="sxs-lookup"><span data-stu-id="93e48-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93e48-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93e48-158">Next steps</span></span>

- [<span data-ttu-id="93e48-159">Handleiding voor het programmeren van U-SQL</span><span class="sxs-lookup"><span data-stu-id="93e48-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="93e48-160">Ontwikkelen van U-SQL-gebruiker gedefinieerde operators voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="93e48-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="93e48-161">Zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93e48-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
