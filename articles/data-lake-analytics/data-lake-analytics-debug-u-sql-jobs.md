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
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Foutopsporing van de gebruiker gedefinieerde C#-code voor mislukte U-SQL-taken

U-SQL biedt een model van uitbreidbaarheid met C#, dus u kunt de functionaliteit van uw code tooadd zoals een aangepaste zelfstandig uitpakken of reducer schrijven. toolearn meer, Zie [U-SQL programmeerbaarheid handleiding](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). In de praktijk code mogelijk moet foutopsporing en big-datasystemen leveren alleen beperkt runtime foutopsporingsinformatie zoals logboekbestanden.

Azure Data Lake Tools voor Visual Studio biedt een functie **hoekpunt foutopsporing kan niet**, waarmee u een mislukte taak van Hallo cloud tooyour lokale computer voor het opsporen van klonen. Hallo lokale kloon vastgelegd Hallo gehele cloudomgeving, inclusief eventuele invoergegevens en gebruikerscode.

Hallo toont volgende video mislukt hoekpunt fouten opsporen in Azure Data Lake Tools voor Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio Hallo na twee updates is vereist als ze nog niet zijn geïnstalleerd: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) en de [universeel C Runtime voor Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Het downloaden is mislukt hoekpunt toolocal machine

Als u een taak die is mislukt in Azure Data Lake Tools voor Visual Studio opent, ziet u een gele waarschuwing balk met gedetailleerde foutberichten in het tabblad Hallo-fout.

1. Klik op **downloaden** toodownload alle Hallo vereiste resources en invoer stromen. Als het Hallo-download niet voltooien, klikt u op **probeer**.

2. Klik op **Open** nadat Hallo downloaden is voltooid toogenerate een lokale foutopsporingsomgeving. Een nieuw exemplaar van de Visual Studio met een oplossing voor foutopsporing is automatisch gemaakt en geopend.

![Azure Data Lake Analytics U-SQL foutopsporing visual studio downloaden hoekpunt](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Taken kunnen de bronbestanden van de code-behind of geregistreerde assembly's bevatten, en deze twee typen hebben verschillende scenario's voor foutopsporing.

- [Fouten opsporen in een taak die is mislukt met code-behind](#debug-job-failed-with-code-behind)
- [Fouten opsporen in een mislukte taak met assembly 's](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Taak is mislukt met de code-behind voor foutopsporing

Als een U-SQL-taak is mislukt en Hallo taak bevat een gebruikerscode (meestal onder de naam `Script.usql.cs` in een project U-SQL), dat de broncode wordt geïmporteerd in Hallo foutopsporing oplossing.  Daar kunt u Hallo Visual Studio foutopsporing hulpprogramma's (controle, variabelen, enz.) tootroubleshoot Hallo probleem.

> [!NOTE]
> Voordat u foutopsporing, moet u ervoor toocheck **Common Language Runtime uitzonderingen** in Hallo uitzondering instellingen venster (**Ctrl + Alt + E**).

![Azure Data Lake Analytics U-SQL foutopsporing visual studio-instelling](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Druk op **F5** toorun Hallo code-behind code. Deze wordt uitgevoerd totdat deze is gestopt vanwege een uitzondering.

2. Open Hallo `ADLTool_Codebehind.usql.cs` bestands- en Stel onderbrekingspunten, drukt u vervolgens op **F5** toodebug Hallo code stap voor stap.

    ![Azure Data Lake Analytics U-SQL-uitzondering voor foutopsporing](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Taak is mislukt met de assembly's voor foutopsporing

Als u geregistreerde assembly's in uw U-SQL-script gebruikt, kan geen Hallo system Hallo broncode automatisch ophalen. In dit geval hello assembly source code bestanden toohello oplossing handmatig toevoegen.

### <a name="configure-hello-solution"></a>Hallo-oplossing configureren

1. Met de rechtermuisknop op **oplossing 'VertexDebug' > toevoegen > bestaand Project...**  toofind Hallo broncode van de assembly's en Hallo project toohello foutopsporing oplossing toevoegen.

    ![Azure Data Lake Analytics U-SQL-foutopsporing project toevoegen](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Met de rechtermuisknop op **LocalVertexHost > eigenschappen** in de oplossing en kopieer Hallo Hallo **werkmap** pad.

3. Met de rechtermuisknop op **CodeProject voor assembly-bron > eigenschappen**, selecteer Hallo **bouwen** tabblad aan de linkerkant en plak Hallo gekopieerd pad als **uitvoer > uitvoerpad**.

    ![Azure Data Lake Analytics U-SQL-foutopsporing instellen pdb pad](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Druk op **Ctrl + Alt + E**, Controleer **Common Language Runtime uitzonderingen** in het venster Instellingen voor uitzondering.

### <a name="start-debug"></a>Foutopsporing starten

1. Met de rechtermuisknop op **CodeProject voor assembly-bron > opnieuw samenstellen** toooutput .pdb bestanden toohello `LocalVertexHost` werkmap.

2. Druk op **F5** en het Hallo-project wordt uitgevoerd totdat deze is gestopt vanwege een uitzondering. Mogelijk ziet u Hallo volgende waarschuwingsbericht weergegeven, kunt u veilig negeren. Tooa minuut tooget toohello foutopsporing scherm kan duren.

    ![Azure Data Lake Analytics U-SQL foutopsporing visual studio-waarschuwing](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Open de broncode en Stel onderbrekingspunten, drukt u vervolgens op **F5** toodebug Hallo code stap voor stap.

U kunt ook Hallo Visual Studio foutopsporing hulpprogramma's (controle, variabelen, enz.) tootroubleshoot Hallo probleem gebruiken.

> [!NOTE]
> Opnieuw samenstellen Hallo assembly bron CodeProject telkens nadat u Hallo code toogenerate bijgewerkt .pdb bestanden wijzigen.

Als Hallo-project met succes voltooid wordt toont Hallo uitvoervenster na foutopsporing, Hallo volgende bericht:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL-foutopsporing is mislukt](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Hallo taak verzenden

Als u klaar bent met het opsporen van fouten opnieuw indienen Hallo mislukte taak.

1. Voor taken met oplossingen voor code-behind uw C#-code naar Hallo code-behind bronbestand kopiëren (meestal `Script.usql.cs`).
2. Registreren voor taken met assembly's, Hallo bijgewerkt .dll-assembly's in uw database ADLA:
    1. Vouw Hallo van Server Explorer of Cloud Explorer **ADLA account > Databases** knooppunt.
    2. Met de rechtermuisknop op **assembly's** en registreren van uw nieuwe .dll-assembly's met de Hallo ADLA database: ![Azure Data Lake Analytics U-SQL-foutopsporing assembly registreren](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. De taak opnieuw.

## <a name="next-steps"></a>Volgende stappen

- [Handleiding voor het programmeren van U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Ontwikkelen van U-SQL-gebruiker gedefinieerde operators voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
