---
title: 'Azure Data Lake Tools: U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code | Microsoft Docs'
description: Meer informatie over hoe toouse Azure Data Lake Tools voor Visual Studio Code toolocal uitgevoerd en lokale fouten.
Keywords: VScode, Azure Data Lake Tools, lokaal uitvoeren, lokale foutopsporing, lokale Debug preview opslagbestand uploaden toostorage pad
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="6cce0-104">U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6cce0-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cce0-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6cce0-105">Prerequisites</span></span>
<span data-ttu-id="6cce0-106">Controleer of er Hallo vereisten is voldaan voordat u deze procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="6cce0-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="6cce0-107">Azure Data Lake-hulpprogramma voor Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6cce0-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="6cce0-108">Zie voor instructies [gebruik Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="6cce0-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="6cce0-109">C# voor Visual Studio Code (als u wilt dat de lokale foutopsporing tooperform een U-SQL).</span><span class="sxs-lookup"><span data-stu-id="6cce0-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Installeer C# in Data Lake Tools voor Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="6cce0-111">Hallo U-SQL lokaal uitvoeren en functies voor foutopsporing momenteel alleen ondersteuning voor Windows-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6cce0-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="6cce0-112">Hallo U-SQL lokaal uitvoeren omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="6cce0-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="6cce0-113">Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: downloaden LocalRun afhankelijkheid** toodownload hello-pakketten.</span><span class="sxs-lookup"><span data-stu-id="6cce0-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Hallo ADL LocalRun afhankelijkheid pakketten downloaden](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="6cce0-115">Zoek Hallo afhankelijkheid pakketten uit Hallo pad wordt weergegeven in Hallo **uitvoer** deelvenster en installeer vervolgens BuildTools en Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="6cce0-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="6cce0-116">Hier volgt een voorbeeldpad:</span><span class="sxs-lookup"><span data-stu-id="6cce0-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="6cce0-117">![Hallo afhankelijkheid pakketten zoeken](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="6cce0-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="6cce0-118">a.</span><span class="sxs-lookup"><span data-stu-id="6cce0-118">a.</span></span> <span data-ttu-id="6cce0-119">tooinstall BuildTools, volg de instructies van de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cce0-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![BuildTools installeren](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="6cce0-121">b.</span><span class="sxs-lookup"><span data-stu-id="6cce0-121">b.</span></span> <span data-ttu-id="6cce0-122">tooinstall Win10SDK 10240, volg de instructies van de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cce0-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Installeer Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="6cce0-124">Hallo-omgevingsvariabele instellen.</span><span class="sxs-lookup"><span data-stu-id="6cce0-124">Set up hello environment variable.</span></span> <span data-ttu-id="6cce0-125">Set Hallo **SCOPE_CPP_SDK** omgevingsvariabele:</span><span class="sxs-lookup"><span data-stu-id="6cce0-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="6cce0-126">Opnieuw opstarten Hallo OS toomake ervoor dat omgevingsvariabele Hallo-instellingen van kracht.</span><span class="sxs-lookup"><span data-stu-id="6cce0-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Zorg ervoor dat Hallo SCOPE_CPP_SDK omgevingsvariabele is geïnstalleerd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="6cce0-128">Hallo lokale uitvoering service starten en het verzenden van lokale tooa-account van de Hallo U-SQL-taak</span><span class="sxs-lookup"><span data-stu-id="6cce0-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="6cce0-129">Voor Hallo eerst gebruiker, zijn de vraag toodownload Hallo ADL: downloaden LocalRun afhankelijkheid pakketten als ze nog niet zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6cce0-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="6cce0-130">Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: lokale Run Service Start**.</span><span class="sxs-lookup"><span data-stu-id="6cce0-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="6cce0-131">Selecteer **accepteren** tooaccept Hallo licentievoorwaarden voor Microsoft-Software voor Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="6cce0-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Accepteer de licentievoorwaarden voor Microsoft-Software Hallo](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="6cce0-133">Hallo cmd-console wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6cce0-133">hello cmd console opens.</span></span> <span data-ttu-id="6cce0-134">Voor de eerste keer dat gebruikers, moet u tooenter **3**, en ga vervolgens naar de lokale mappad Hallo voor uw gegevens invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6cce0-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="6cce0-135">U kunt Hallo standaardwaarden gebruiken voor andere opties.</span><span class="sxs-lookup"><span data-stu-id="6cce0-135">For other options, you can use hello default values.</span></span> 

   ![Data Lake Tools voor Visual Studio Code lokaal uitvoeren cmd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="6cce0-137">Ctrl + Shift + P tooopen Hallo opdracht palet selecteert, voer **ADL: Submit Job**, en selecteer vervolgens **lokale** toosubmit Hallo taak tooyour lokale account.</span><span class="sxs-lookup"><span data-stu-id="6cce0-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Data Lake Tools voor Visual Studio Code selecteren lokale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="6cce0-139">Nadat u de taak Hallo hebt ingediend, kunt u Hallo verzending details weergeven.</span><span class="sxs-lookup"><span data-stu-id="6cce0-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="6cce0-140">verzending van tooview Hallo details Selecteer **jobUrl** in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="6cce0-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="6cce0-141">U kunt ook Hallo taakstatus verzending van hello cmd-console weergeven.</span><span class="sxs-lookup"><span data-stu-id="6cce0-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="6cce0-142">Voer **7** in Hallo cmd-console als u wilt dat tooknow meer taakgegevens.</span><span class="sxs-lookup"><span data-stu-id="6cce0-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="6cce0-143">![Data Lake Tools voor Visual Studio Code lokaal uitvoeren uitvoer](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools voor Visual Studio Code lokaal uitvoeren cmd-status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="6cce0-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="6cce0-144">Start een lokale foutopsporing voor Hallo U-SQL-taak</span><span class="sxs-lookup"><span data-stu-id="6cce0-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="6cce0-145">Voor Hallo eerst gebruiker, zijn de vraag toodownload Hallo ADL: downloaden LocalRun afhankelijkheid pakketten als ze nog niet zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6cce0-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="6cce0-146">Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: lokale Run Service Start**.</span><span class="sxs-lookup"><span data-stu-id="6cce0-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="6cce0-147">Hallo cmd-console wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6cce0-147">hello cmd console opens.</span></span> <span data-ttu-id="6cce0-148">Zorg ervoor dat Hallo **DataRoot** is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6cce0-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="6cce0-149">Stel een onderbrekingspunt in uw C# code-behind.</span><span class="sxs-lookup"><span data-stu-id="6cce0-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="6cce0-150">Terug in Hallo scripteditor Selecteer Ctrl + Shift + P tooopen Hallo opdrachtconsole en voer **fouten opsporen in lokale** toostart uw lokale debug-service.</span><span class="sxs-lookup"><span data-stu-id="6cce0-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Data Lake Tools voor Visual Studio Code lokale foutopsporing resultaat](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="6cce0-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cce0-152">Next steps</span></span>
- <span data-ttu-id="6cce0-153">Zie voor het gebruik van Azure Data Lake Tools voor Visual Studio Code, [gebruik Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="6cce0-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="6cce0-154">Zie voor het ophalen van gestarte informatie over Data Lake Analytics [zelfstudie: aan de slag met Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6cce0-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="6cce0-155">Zie voor meer informatie over Data Lake Tools voor Visual Studio [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6cce0-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="6cce0-156">Zie voor informatie over het ontwikkelen van assembly's Hallo [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="6cce0-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
