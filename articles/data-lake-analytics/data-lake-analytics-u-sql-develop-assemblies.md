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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="c99a4-103">Ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="c99a4-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="c99a4-104">Meer informatie over hoe tooturn code-behind in assembly's toobe gebruikt en opnieuw gebruikt in Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="c99a4-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="c99a4-105">U-SQL maakt het eenvoudig tooadd uw eigen aangepaste code in .net-talen, zoals C#, of traditiegetrouw F #.</span><span class="sxs-lookup"><span data-stu-id="c99a4-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="c99a4-106">U kunt uw eigen toosupport runtime zelfs andere talen implementeren.</span><span class="sxs-lookup"><span data-stu-id="c99a4-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="c99a4-107">Hallo gemakkelijkste manier toouse aangepaste code is toouse Hallo Data Lake Tools voor Visual Studio code-behind mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="c99a4-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="c99a4-108">Zie voor meer informatie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c99a4-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="c99a4-109">Er zijn enkele nadelen van het gebruik van code-behind:</span><span class="sxs-lookup"><span data-stu-id="c99a4-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="c99a4-110">Hallo broncode opgehaald voor de verzending van elk script geüpload.</span><span class="sxs-lookup"><span data-stu-id="c99a4-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="c99a4-111">code-behind kan niet worden gedeeld met andere taken.</span><span class="sxs-lookup"><span data-stu-id="c99a4-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="c99a4-112">tooaddress deze nadelen code-behind in assembly's inschakelen en registreren Hallo-assembly's toohello Data Lake Analytics-catalogus.</span><span class="sxs-lookup"><span data-stu-id="c99a4-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c99a4-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c99a4-113">Prerequisites</span></span>
* <span data-ttu-id="c99a4-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012 met Visual C++ geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="c99a4-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="c99a4-115">Microsoft Azure SDK voor .NET versie 2.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c99a4-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="c99a4-116">Installeren met behulp van de webplatforminstallatieprogramma voor Windows hello of Visual Studio Installer</span><span class="sxs-lookup"><span data-stu-id="c99a4-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="c99a4-117">Een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="c99a4-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="c99a4-118">Zie [Aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c99a4-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="c99a4-119">Ga via Hallo [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c99a4-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="c99a4-120">Verbinding maken met tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c99a4-120">Connect tooAzure.</span></span>
* <span data-ttu-id="c99a4-121">Hallo brongegevens uploaden, Zie [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c99a4-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="c99a4-122">Assembly's voor de U-SQL ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="c99a4-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="c99a4-123">**toocreate en het verzenden van een U-SQL-taak**</span><span class="sxs-lookup"><span data-stu-id="c99a4-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="c99a4-124">Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="c99a4-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="c99a4-125">Vouw **geïnstalleerde**, **sjablonen**, **Azure Data Lake**, **U-SQL(ADLA)**, selecteer Hallo **Class Library (voor U-SQL Toepassing)** sjabloon en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c99a4-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="c99a4-126">Schrijf uw code in Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="c99a4-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="c99a4-127">Hallo Hieronder volgt een voorbeeld van code.</span><span class="sxs-lookup"><span data-stu-id="c99a4-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="c99a4-128">Klik op Hallo **bouwen** menu en klik vervolgens op **Build Solution** toocreate Hallo dll-bestand.</span><span class="sxs-lookup"><span data-stu-id="c99a4-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="c99a4-129">Assembly's registreren</span><span class="sxs-lookup"><span data-stu-id="c99a4-129">Register assemblies</span></span>

<span data-ttu-id="c99a4-130">Zie [gebruik Data Lake Analytics(U-SQL) catalogus](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="c99a4-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="c99a4-131">Hallo-assembly's gebruiken</span><span class="sxs-lookup"><span data-stu-id="c99a4-131">Use hello assemblies</span></span>

<span data-ttu-id="c99a4-132">Zie [gebruiken hello Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="c99a4-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c99a4-133">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c99a4-133">See also</span></span>
* [<span data-ttu-id="c99a4-134">Aan de slag met Data Lake Analytics met PowerShell</span><span class="sxs-lookup"><span data-stu-id="c99a4-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="c99a4-135">Aan de slag met Data Lake Analytics met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c99a4-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c99a4-136">Data Lake Tools voor Visual Studio gebruiken voor het ontwikkelen van U-SQL-toepassingen</span><span class="sxs-lookup"><span data-stu-id="c99a4-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c99a4-137">Gebruik Data Lake Analytics(U-SQL) catalogus</span><span class="sxs-lookup"><span data-stu-id="c99a4-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="c99a4-138">Hello Azure Data Lake Tools voor Visual Studio Code gebruiken</span><span class="sxs-lookup"><span data-stu-id="c99a4-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
