---
title: aaaUsing Emulator Express toorun en foutopsporing een Azure cloud service op een lokale computer | Microsoft Docs
description: Met behulp van toorun Emulator Express en foutopsporing een cloudservice op een lokale computer
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
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="1bc98-103">Met Emulator Express cloud toorun en foutopsporing een Azure service op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="1bc98-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="1bc98-104">U kunt testen en fouten opsporen in een cloudservice zonder Visual Studio als administrator uitvoeren met behulp van de Express-Emulator.</span><span class="sxs-lookup"><span data-stu-id="1bc98-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="1bc98-105">U kunt uw project instellingen toouse beide Emulator Express instellen of Hallo volledige emulator, afhankelijk van Hallo vereisten van uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1bc98-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="1bc98-106">Zie voor meer informatie over de volledige emulator Hallo [een Azure-toepassing uitvoert in Hallo Compute-Emulator](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1bc98-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="1bc98-107">Met een Emulator snelle in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1bc98-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="1bc98-108">Wanneer u een Azure-project in de Azure SDK 2.3 of hoger maakt, wordt Emulator Express automatisch gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1bc98-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="1bc98-109">Gebruik voor bestaande projecten die zijn gemaakt met een eerdere versie van hello Azure SDK Hallo stappen tooselect Emulator Express te volgen:</span><span class="sxs-lookup"><span data-stu-id="1bc98-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="1bc98-110">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bc98-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1bc98-111">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="1bc98-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="1bc98-112">Selecteer in de Hallo projecten eigenschappenpagina's Hallo **Web** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1bc98-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Eigenschappen voor een Azure-cloud service-project](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="1bc98-114">Onder **lokale Ontwikkelaarsserver**, selecteer **optie Gebruik IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="1bc98-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="1bc98-115">Onder **Emulator**, selecteer **gebruik Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="1bc98-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="1bc98-116">toolaunch hello Emulator Express, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="1bc98-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="1bc98-117">Emulator Express beperkingen</span><span class="sxs-lookup"><span data-stu-id="1bc98-117">Emulator Express limitations</span></span>
<span data-ttu-id="1bc98-118">Hallo problemen volgen enkele bekende beperkingen van de Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="1bc98-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="1bc98-119">Emulator Express is niet compatibel met IIS-webserver.</span><span class="sxs-lookup"><span data-stu-id="1bc98-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="1bc98-120">Uw cloudservice meerdere rollen kan bevatten, maar elke rol beperkt tooone exemplaar is.</span><span class="sxs-lookup"><span data-stu-id="1bc98-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="1bc98-121">U kunt poortnummers minder dan 1000 niet openen.</span><span class="sxs-lookup"><span data-stu-id="1bc98-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="1bc98-122">Als u een verificatieprovider die normaal gesproken gebruikmaakt van een poort minder dan 1000 gebruikt, moet u mogelijk toochange deze waarde tooa-poortnummer dat is meer dan 1000.</span><span class="sxs-lookup"><span data-stu-id="1bc98-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="1bc98-123">De beperkingen die van toepassing zijn toohello Azure Compute-Emulator tooEmulator Express ook van toepassing.</span><span class="sxs-lookup"><span data-stu-id="1bc98-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="1bc98-124">Er geen bijvoorbeeld meer dan 50 rolinstanties per implementatie.</span><span class="sxs-lookup"><span data-stu-id="1bc98-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="1bc98-125">Zie voor meer informatie over hello Azure Compute-Emulator [een Azure-toepassing uitvoert in Hallo Compute-Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="1bc98-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc98-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1bc98-126">Next steps</span></span>
[<span data-ttu-id="1bc98-127">Foutopsporing van Azure-cloudservices</span><span class="sxs-lookup"><span data-stu-id="1bc98-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
