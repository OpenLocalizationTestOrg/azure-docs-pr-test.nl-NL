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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code

## <a name="prerequisites"></a>Vereisten
Controleer of er Hallo vereisten is voldaan voordat u deze procedures te volgen:
- Azure Data Lake-hulpprogramma voor Visual Studio Code. Zie voor instructies [gebruik Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# voor Visual Studio Code (als u wilt dat de lokale foutopsporing tooperform een U-SQL).

   ![Installeer C# in Data Lake Tools voor Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Hallo U-SQL lokaal uitvoeren en functies voor foutopsporing momenteel alleen ondersteuning voor Windows-gebruikers. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Hallo U-SQL lokaal uitvoeren omgeving instellen

1. Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: downloaden LocalRun afhankelijkheid** toodownload hello-pakketten.  

   ![Hallo ADL LocalRun afhankelijkheid pakketten downloaden](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Zoek Hallo afhankelijkheid pakketten uit Hallo pad wordt weergegeven in Hallo **uitvoer** deelvenster en installeer vervolgens BuildTools en Win10SDK 10240. Hier volgt een voorbeeldpad:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Hallo afhankelijkheid pakketten zoeken](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, volg de instructies van de wizard Hallo.   

  ![BuildTools installeren](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, volg de instructies van de wizard Hallo.  

  ![Installeer Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Hallo-omgevingsvariabele instellen. Set Hallo **SCOPE_CPP_SDK** omgevingsvariabele:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Opnieuw opstarten Hallo OS toomake ervoor dat omgevingsvariabele Hallo-instellingen van kracht.  

   ![Zorg ervoor dat Hallo SCOPE_CPP_SDK omgevingsvariabele is geïnstalleerd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Hallo lokale uitvoering service starten en het verzenden van lokale tooa-account van de Hallo U-SQL-taak 
Voor Hallo eerst gebruiker, zijn de vraag toodownload Hallo ADL: downloaden LocalRun afhankelijkheid pakketten als ze nog niet zijn geïnstalleerd.
1. Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: lokale Run Service Start**.
2. Selecteer **accepteren** tooaccept Hallo licentievoorwaarden voor Microsoft-Software voor Hallo eerst. 

   ![Accepteer de licentievoorwaarden voor Microsoft-Software Hallo](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Hallo cmd-console wordt geopend. Voor de eerste keer dat gebruikers, moet u tooenter **3**, en ga vervolgens naar de lokale mappad Hallo voor uw gegevens invoer en uitvoer. U kunt Hallo standaardwaarden gebruiken voor andere opties. 

   ![Data Lake Tools voor Visual Studio Code lokaal uitvoeren cmd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Ctrl + Shift + P tooopen Hallo opdracht palet selecteert, voer **ADL: Submit Job**, en selecteer vervolgens **lokale** toosubmit Hallo taak tooyour lokale account.

   ![Data Lake Tools voor Visual Studio Code selecteren lokale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Nadat u de taak Hallo hebt ingediend, kunt u Hallo verzending details weergeven. verzending van tooview Hallo details Selecteer **jobUrl** in Hallo **uitvoer** venster. U kunt ook Hallo taakstatus verzending van hello cmd-console weergeven. Voer **7** in Hallo cmd-console als u wilt dat tooknow meer taakgegevens.

   ![Data Lake Tools voor Visual Studio Code lokaal uitvoeren uitvoer](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools voor Visual Studio Code lokaal uitvoeren cmd-status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Start een lokale foutopsporing voor Hallo U-SQL-taak  
Voor Hallo eerst gebruiker, zijn de vraag toodownload Hallo ADL: downloaden LocalRun afhankelijkheid pakketten als ze nog niet zijn geïnstalleerd.
  
1. Ctrl + Shift + P tooopen Hallo opdracht palet selecteren en voer vervolgens **ADL: lokale Run Service Start**. Hallo cmd-console wordt geopend. Zorg ervoor dat Hallo **DataRoot** is ingesteld.
3. Stel een onderbrekingspunt in uw C# code-behind.
4. Terug in Hallo scripteditor Selecteer Ctrl + Shift + P tooopen Hallo opdrachtconsole en voer **fouten opsporen in lokale** toostart uw lokale debug-service.

![Data Lake Tools voor Visual Studio Code lokale foutopsporing resultaat](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Volgende stappen
- Zie voor het gebruik van Azure Data Lake Tools voor Visual Studio Code, [gebruik Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Zie voor het ophalen van gestarte informatie over Data Lake Analytics [zelfstudie: aan de slag met Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Zie voor meer informatie over Data Lake Tools voor Visual Studio [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Zie voor informatie over het ontwikkelen van assembly's Hallo [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).
