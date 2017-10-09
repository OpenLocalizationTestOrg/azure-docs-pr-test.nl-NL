---
title: aaaDevelop U-SQL-gebruiker gedefinieerde operators (UDO's) | Microsoft Docs
description: 'Ontdek hoe toodevelop gebruiker gedefinieerde operators toobe gebruikt en hergebruikt in Data Lake Analytics-taken. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="056d3-103">Ontwikkelen van U-SQL-gebruiker gedefinieerde operators (UDO's)</span><span class="sxs-lookup"><span data-stu-id="056d3-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="056d3-104">Meer informatie over hoe toodevelop gebruiker gedefinieerde operators tooprocess gegevens in een U-SQL-taak.</span><span class="sxs-lookup"><span data-stu-id="056d3-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="056d3-105">Zie voor instructies over het ontwikkelen van algemene assembly's voor de U-SQL [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="056d3-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="056d3-106">Definieer en het gebruik van een gebruiker gedefinieerde operator in U-SQL</span><span class="sxs-lookup"><span data-stu-id="056d3-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="056d3-107">**toocreate en het verzenden van een U-SQL-taak**</span><span class="sxs-lookup"><span data-stu-id="056d3-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="056d3-108">Selecteer in Visual Studio Hallo **bestand > Nieuw > Project > U-SQL Project**.</span><span class="sxs-lookup"><span data-stu-id="056d3-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="056d3-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="056d3-109">Click **OK**.</span></span> <span data-ttu-id="056d3-110">Visual Studio maakt een oplossing met een bestand Script.usql.</span><span class="sxs-lookup"><span data-stu-id="056d3-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="056d3-111">Van **Solution Explorer**, vouw Script.usql en dubbelklikt u vervolgens op **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="056d3-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="056d3-112">Plak Hallo code in Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="056d3-112">Paste hello following code into hello file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="056d3-113">Open **Script.usql**, en U-SQL-script te plakken Hallo volgen:</span><span class="sxs-lookup"><span data-stu-id="056d3-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="056d3-114">Hallo Data Lake Analytics-account, Database en Schema opgeven.</span><span class="sxs-lookup"><span data-stu-id="056d3-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="056d3-115">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="056d3-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="056d3-116">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="056d3-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="056d3-117">Als u dit nog niet hebt tooyour Azure-abonnement verbonden, wordt u na vragen aan gebruiker tooenter worden de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="056d3-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="056d3-118">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="056d3-118">Click **Submit**.</span></span> <span data-ttu-id="056d3-119">Resultaat van het verzenden en een koppeling naar de taak zijn beschikbaar in het resultatenvenster Hallo wanneer Hallo verzenden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="056d3-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="056d3-120">Klik op Hallo **vernieuwen** knop toosee meest recente taak status en vernieuw Hallo welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="056d3-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="056d3-121">**toosee Hallo-uitvoer**</span><span class="sxs-lookup"><span data-stu-id="056d3-121">**toosee hello output**</span></span>

1. <span data-ttu-id="056d3-122">Van **Server Explorer**, vouw **Azure**, vouw **Data Lake Analytics**, vouw uw Data Lake Analytics-account, vouw **Opslagaccounts**, met de rechtermuisknop op Hallo Default Storage en klik vervolgens op **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="056d3-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="056d3-123">Vouw voorbeelden uit, vouw uitvoer en dubbelklikt u vervolgens op **Stuurprogramma's.csv**.</span><span class="sxs-lookup"><span data-stu-id="056d3-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="056d3-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="056d3-124">See also</span></span>
* [<span data-ttu-id="056d3-125">Aan de slag met Data Lake Analytics met PowerShell</span><span class="sxs-lookup"><span data-stu-id="056d3-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="056d3-126">Aan de slag met Data Lake Analytics met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="056d3-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="056d3-127">Data Lake Tools voor Visual Studio gebruiken voor het ontwikkelen van U-SQL-toepassingen</span><span class="sxs-lookup"><span data-stu-id="056d3-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
