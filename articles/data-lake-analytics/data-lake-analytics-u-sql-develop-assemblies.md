---
title: U-SQL-assembly's voor Azure Data Lake Analytics-taken te ontwikkelen | Microsoft Docs
description: 'Informatie over het ontwikkelen van assembly''s worden gebruikt en hergebruikt in Data Lake Analytics-taken. '
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
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="457bd-103">Ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="457bd-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="457bd-104">Informatie over het code-behind omzetten in assembly's die moeten worden gebruikt en hergebruikt in Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="457bd-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="457bd-105">U-SQL kunt eenvoudig uw eigen aangepaste code toevoegen in .net-talen, zoals C#, of traditiegetrouw F #.</span><span class="sxs-lookup"><span data-stu-id="457bd-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="457bd-106">U kunt zelfs uw eigen runtime ter ondersteuning van andere talen implementeren.</span><span class="sxs-lookup"><span data-stu-id="457bd-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="457bd-107">De eenvoudigste manier om het gebruik van aangepaste code is met het Data Lake Tools voor Visual Studio code-behind mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="457bd-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="457bd-108">Zie voor meer informatie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="457bd-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="457bd-109">Er zijn enkele nadelen van het gebruik van code-behind:</span><span class="sxs-lookup"><span data-stu-id="457bd-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="457bd-110">De broncode wordt voor de verzending van elk script geüpload.</span><span class="sxs-lookup"><span data-stu-id="457bd-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="457bd-111">code-behind kan niet worden gedeeld met andere taken.</span><span class="sxs-lookup"><span data-stu-id="457bd-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="457bd-112">Om deze nadelen op te lossen, kunt u code-behind omzetten in assembly's en registreer de assembly's naar de Data Lake Analytics-catalogus.</span><span class="sxs-lookup"><span data-stu-id="457bd-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="457bd-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="457bd-113">Prerequisites</span></span>
* <span data-ttu-id="457bd-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012 met Visual C++ geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="457bd-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="457bd-115">Microsoft Azure SDK voor .NET versie 2.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="457bd-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="457bd-116">Installeren met behulp van de webplatforminstallatieprogramma of Visual Studio Installer</span><span class="sxs-lookup"><span data-stu-id="457bd-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="457bd-117">Een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="457bd-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="457bd-118">Zie [Aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="457bd-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="457bd-119">Ga via de [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="457bd-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="457bd-120">Verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="457bd-120">Connect to Azure.</span></span>
* <span data-ttu-id="457bd-121">Uploaden van de brongegevens, Zie [aan de slag met Azure Data Lake Analytics U-SQL-Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="457bd-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="457bd-122">Assembly's voor de U-SQL ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="457bd-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="457bd-123">**Maken en verzenden van een U-SQL-taak**</span><span class="sxs-lookup"><span data-stu-id="457bd-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="457bd-124">Klik in het menu **File** op **New** en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="457bd-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="457bd-125">Vouw **geïnstalleerde**, **sjablonen**, **Azure Data Lake**, **U-SQL(ADLA)**, selecteer de **Class Library (voor U-SQL-toepassing)** sjabloon en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="457bd-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="457bd-126">Schrijf uw code in Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="457bd-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="457bd-127">Hier volgt een voorbeeld van code.</span><span class="sxs-lookup"><span data-stu-id="457bd-127">The following is a code sample.</span></span>

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
4. <span data-ttu-id="457bd-128">Klik op de **bouwen** menu en klik vervolgens op **Build Solution** voor het maken van het DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="457bd-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="457bd-129">Assembly's registreren</span><span class="sxs-lookup"><span data-stu-id="457bd-129">Register assemblies</span></span>

<span data-ttu-id="457bd-130">Zie [gebruik Data Lake Analytics(U-SQL) catalogus](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="457bd-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="457bd-131">De assembly's gebruiken</span><span class="sxs-lookup"><span data-stu-id="457bd-131">Use the assemblies</span></span>

<span data-ttu-id="457bd-132">Zie [gebruik Azure Data Lake Tools voor Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="457bd-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="457bd-133">Zie ook</span><span class="sxs-lookup"><span data-stu-id="457bd-133">See also</span></span>
* [<span data-ttu-id="457bd-134">Aan de slag met Data Lake Analytics met PowerShell</span><span class="sxs-lookup"><span data-stu-id="457bd-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="457bd-135">Aan de slag met Data Lake Analytics met Azure portal</span><span class="sxs-lookup"><span data-stu-id="457bd-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="457bd-136">Data Lake Tools voor Visual Studio gebruiken voor het ontwikkelen van U-SQL-toepassingen</span><span class="sxs-lookup"><span data-stu-id="457bd-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="457bd-137">Gebruik Data Lake Analytics(U-SQL) catalogus</span><span class="sxs-lookup"><span data-stu-id="457bd-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="457bd-138">De Azure Data Lake-tools gebruiken voor Visual Studio-code</span><span class="sxs-lookup"><span data-stu-id="457bd-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)