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
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Testen en foutopsporing van U-SQL-taken met behulp van lokaal uitvoeren en hello Azure Data Lake U-SQL-SDK

U kunt Azure Data Lake Tools voor Visual Studio en hello Azure Data Lake U-SQL-SDK toorun U-SQL-taken op uw werkstation gebruiken, net zoals u in hello Azure Data Lake-service kunt. Deze twee lokaal uitgevoerde functies besparen tijd op het gebied van het testen en de foutopsporing van uw U-SQL-taken.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Hallo data-hoofdmap en het Hallo-bestandspad begrijpen

Zowel lokale uitvoering en Hallo U-SQL-SDK moet een gegevens-hoofdmap. Hallo-gegevens-hoofdmap is een 'lokale store' voor Hallo lokale compute-account. Het is equivalente toohello Azure Data Lake Store-account van een Data Lake Analytics-account. Overschakelen van tooa is verschillende gegevens uit een hoofdmap net als andere store-account tooa overschakelen. Als u gegevens tooaccess vaak gedeeld met andere gegevens hoofdmappen wilt, moet u in uw scripts absolute paden gebruiken. Of het bestand system symbolische koppelingen maken (bijvoorbeeld **mklink** van NTFS) onder het Hallo-gegevenshoofdmap map toopoint toohello gedeelde gegevens.

Hallo data-hoofdmap wordt gebruikt voor:

- Metagegevens, zoals databases, tabellen, tabelfuncties (tvf's) en assembly's opgeslagen.
- Hallo invoer en uitvoerpaden die zijn gedefinieerd als relatieve paden in de U-SQL opzoeken. Gebruik relatieve paden maakt het eenvoudiger toodeploy uw tooAzure U-SQL-projecten.

U kunt een relatief pad en een lokaal absoluut pad in U-SQL-scripts gebruiken. Hallo relatief pad is relatief toohello opgegeven gegevenshoofdmap mappad. U wordt aangeraden dat u gebruik ' / ' Hallo als pad scheidingsteken toomake uw scripts die compatibel is met het Hallo-serverzijde. Hier volgen enkele voorbeelden van relatieve paden en hun equivalente absolute paden. In deze voorbeelden is C:\LocalRunDataRoot hello, gegevens-hoofdmap.

|Relatief pad|Het absolute pad|
|-------------|-------------|
|/ABC/DEF/Input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/Input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/Input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Gebruik lokale uitvoeren vanuit Visual Studio

Data Lake Tools voor Visual Studio biedt een U-SQL lokaal uitvoeren ervaring in Visual Studio. Met behulp van deze functie kunt u het volgende doen:

- Een U-SQL-script lokaal uitvoeren samen met C#-assembly's.
- Fouten opsporen in een C#-assembly lokaal.
- Maken, weergeven en verwijderen van U-SQL-catalogussen (lokale databases, assembly's, schema's en tabellen) in Server Explorer. U kunt ook de lokale catalogus Hallo ook vinden in Server Explorer.

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren lokale catalogus](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Hallo Data Lake Tools installatieprogramma maakt een C:\LocalRunRoot map toobe gebruikt als Hallo standaard gegevens-hoofdmap. Hallo standaard lokaal uitvoeren parallelle uitvoering is 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure lokaal worden uitgevoerd in Visual Studio

1. Open Visual Studio.
2. Open **Server Explorer**.
3. Vouw **Azure** > **Data Lake Analytics**.
4. Klik op Hallo **Data Lake** menu en klik vervolgens op **opties en instellingen**.
5. Vouw in de structuur van Hallo links **Azure Data Lake**, en vouw vervolgens **algemene**.

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren configureren instellingen](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Een Visual Studio U-SQL-project is vereist voor het uitvoeren van lokale uitvoeren. Dit onderdeel wijkt af van het uitvoeren van U-SQL-scripts uit Azure.

### <a name="toorun-a-u-sql-script-locally"></a>lokaal toorun een U-SQL-script
1. Open uw U-SQL-project in Visual Studio.   
2. Met de rechtermuisknop op een U-SQL-script in Solution Explorer en klik vervolgens op **Submit Script**.
3. Selecteer **(lokaal)** zoals hello Analytics-toorun uw script lokaal account.
U kunt ook klikken op Hallo **(lokaal)** account op Hallo boven in de script-venster en klik vervolgens op **indienen** (of gebruik Hallo Ctrl + F5 sneltoets).

    ![Data Lake Tools voor Visual Studio lokaal uitvoeren indienen taken](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Lokaal fouten opsporen in scripts en C#-assembly's

U kunt fouten opsporen C#-assembly's zonder verzenden en registreren tooAzure Data Lake Analytics-Service. U kunt onderbrekingspunten instellen in beide Hallo onderliggende-codebestand en in een waarnaar wordt verwezen C#-project.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug lokale code in onderliggende-codebestand

1. Onderbrekingspunten instellen in Hallo onderliggende-codebestand.
2. Druk op F5 toodebug Hallo script lokaal.

> [!NOTE]
   > Hello te volgen procedure werkt alleen in Visual Studio 2015. In oudere Visual Studio u wellicht toomanually Hallo pdb-bestanden toevoegen.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug lokale code in een waarnaar wordt verwezen C#-project

1. Maak een C#-assemblyproject en bouw het toogenerate Hallo uitvoer-dll.
2. Registreer Hallo dll-bestand met een U-SQL-instructie:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Onderbrekingspunten instellen in Hallo C#-code.
4. Druk op F5 toodebug Hallo script dat verwijst naar lokaal Hallo C#-DLL-bestand.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Gebruik lokale uitvoeren vanaf Hallo Data Lake U-SQL-SDK

Bovendien toorunning U-SQL-scripts lokaal met behulp van Visual Studio, kunt u hello Azure Data Lake U-SQL-SDK toorun U-SQL-scripts lokaal met de opdrachtregel en programming interfaces. Via deze, kunt u uw lokale test U-SQL te schalen.

Meer informatie over [SDK van Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Volgende stappen

* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data Lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md).
* toouse hello hoekpunt uitvoering weergave Zie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
