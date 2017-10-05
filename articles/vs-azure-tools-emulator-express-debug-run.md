---
title: Emulator Express gebruiken voor het uitvoeren en fouten opsporen in een Azure-cloud-service op een lokale machine | Microsoft Docs
description: Emulator Express gebruiken voor het uitvoeren en fouten opsporen in een cloudservice op een lokale computer
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="65710-103">Emulator Express gebruiken voor het uitvoeren en fouten opsporen in een Azure-cloud-service op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="65710-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="65710-104">U kunt testen en fouten opsporen in een cloudservice zonder Visual Studio als administrator uitvoeren met behulp van de Express-Emulator.</span><span class="sxs-lookup"><span data-stu-id="65710-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="65710-105">U kunt instellen dat uw projectinstellingen Emulator Express of de volledige emulator, afhankelijk van de vereisten van uw cloudservice te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65710-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="65710-106">Zie voor meer informatie over de volledige emulator, [een Azure-toepassing uitvoert in de Emulator Compute](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="65710-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="65710-107">Met een Emulator snelle in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65710-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="65710-108">Wanneer u een Azure-project in de Azure SDK 2.3 of hoger maakt, wordt Emulator Express automatisch gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65710-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="65710-109">Gebruik de volgende stappen om te selecteren Emulator Express voor bestaande projecten die zijn gemaakt met een eerdere versie van de Azure SDK:</span><span class="sxs-lookup"><span data-stu-id="65710-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="65710-110">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65710-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="65710-111">In **Solution Explorer**, met de rechtermuisknop op het project en selecteer in het contextmenu **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="65710-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="65710-112">Selecteer in de projecten eigenschappenpagina's, de **Web** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65710-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Eigenschappen voor een Azure-cloud service-project](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="65710-114">Onder **lokale Ontwikkelaarsserver**, selecteer **optie Gebruik IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="65710-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="65710-115">Onder **Emulator**, selecteer **gebruik Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="65710-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="65710-116">Start de Emulator Express, de volgende opdracht uit te voeren achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="65710-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="65710-117">Emulator Express beperkingen</span><span class="sxs-lookup"><span data-stu-id="65710-117">Emulator Express limitations</span></span>
<span data-ttu-id="65710-118">De volgende problemen zijn bekende beperkingen van de Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="65710-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="65710-119">Emulator Express is niet compatibel met IIS-webserver.</span><span class="sxs-lookup"><span data-stu-id="65710-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="65710-120">Uw cloudservice meerdere rollen kan bevatten, maar elke rol is beperkt tot één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65710-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="65710-121">U kunt poortnummers minder dan 1000 niet openen.</span><span class="sxs-lookup"><span data-stu-id="65710-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="65710-122">Als u een verificatieprovider die normaal gesproken gebruikmaakt van een poort minder dan 1000 gebruikt, moet u mogelijk deze waarde wijzigen in een poortnummer dat is meer dan 1000.</span><span class="sxs-lookup"><span data-stu-id="65710-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="65710-123">De beperkingen die van toepassing op de Azure Compute-Emulator zijn ook van toepassing op de Express-Emulator.</span><span class="sxs-lookup"><span data-stu-id="65710-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="65710-124">Er geen bijvoorbeeld meer dan 50 rolinstanties per implementatie.</span><span class="sxs-lookup"><span data-stu-id="65710-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="65710-125">Zie voor meer informatie over de Azure Compute-Emulator [een Azure-toepassing uitvoert in de Emulator Compute](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="65710-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65710-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65710-126">Next steps</span></span>
[<span data-ttu-id="65710-127">Foutopsporing van Azure-cloudservices</span><span class="sxs-lookup"><span data-stu-id="65710-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
