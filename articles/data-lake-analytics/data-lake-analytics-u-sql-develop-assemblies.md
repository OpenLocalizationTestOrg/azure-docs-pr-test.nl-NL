---
title: aaaDevelop U-SQL-assembly's voor Azure Data Lake Analytics-taken | Microsoft Docs
description: 'Ontdek hoe toodevelop assembly''s toobe gebruikt en hergebruikt in Data Lake Analytics-taken. '
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken
Meer informatie over hoe tooturn code-behind in assembly's toobe gebruikt en opnieuw gebruikt in Data Lake Analytics-taken. 

U-SQL maakt het eenvoudig tooadd uw eigen aangepaste code in .net-talen, zoals C#, of traditiegetrouw F #. U kunt uw eigen toosupport runtime zelfs andere talen implementeren.

Hallo gemakkelijkste manier toouse aangepaste code is toouse Hallo Data Lake Tools voor Visual Studio code-behind mogelijkheden. Zie voor meer informatie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Er zijn enkele nadelen van het gebruik van code-behind:

- Hallo broncode opgehaald voor de verzending van elk script geüpload.
- code-behind kan niet worden gedeeld met andere taken.

tooaddress deze nadelen code-behind in assembly's inschakelen en registreren Hallo-assembly's toohello Data Lake Analytics-catalogus.

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012 met Visual C++ geïnstalleerd
* Microsoft Azure SDK voor .NET versie 2.5 of hoger.  Installeren met behulp van de webplatforminstallatieprogramma voor Windows hello of Visual Studio Installer
* Een Data Lake Analytics-account.  Zie [Aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md).
* Ga via Hallo [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md) zelfstudie.
* Verbinding maken met tooAzure.
* Hallo brongegevens uploaden, Zie [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Assembly's voor de U-SQL ontwikkelen

**toocreate en het verzenden van een U-SQL-taak**

1. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
2. Vouw **geïnstalleerde**, **sjablonen**, **Azure Data Lake**, **U-SQL(ADLA)**, selecteer Hallo **Class Library (voor U-SQL Toepassing)** sjabloon en klik vervolgens op **OK**.
3. Schrijf uw code in Class1.cs.  Hallo Hieronder volgt een voorbeeld van code.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Klik op Hallo **bouwen** menu en klik vervolgens op **Build Solution** toocreate Hallo dll-bestand.

## <a name="register-assemblies"></a>Assembly's registreren

Zie [gebruik Data Lake Analytics(U-SQL) catalogus](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Hallo-assembly's gebruiken

Zie [gebruiken hello Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Zie ook
* [Aan de slag met Data Lake Analytics met PowerShell](data-lake-analytics-get-started-powershell.md)
* [Aan de slag met Data Lake Analytics met hello Azure-portal](data-lake-analytics-get-started-portal.md)
* [Data Lake Tools voor Visual Studio gebruiken voor het ontwikkelen van U-SQL-toepassingen](data-lake-analytics-data-lake-tools-get-started.md)
* [Gebruik Data Lake Analytics(U-SQL) catalogus](data-lake-analytics-use-u-sql-catalog.md)
* [Hello Azure Data Lake Tools voor Visual Studio Code gebruiken](data-lake-analytics-data-lake-tools-for-vscode.md)
