---
title: aaaSetup emulator toodebug Cloud Services-toepassingen in Visual Studio express | Microsoft Docs
description: Legt uit hoe tooinstall Hallo C++ redistributable tooenable Emulator in Visual Studio Express
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="35e05-103">Toodebug Cloud Services-toepassing Emulator Express gebruiken in de VS 2017</span><span class="sxs-lookup"><span data-stu-id="35e05-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="35e05-104">Dit artikel wordt uitgelegd hoe toouse Emulator Express toodebug Cloud Services-toepassingen in VS-2017.</span><span class="sxs-lookup"><span data-stu-id="35e05-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="35e05-105">Achtergrond-context</span><span class="sxs-lookup"><span data-stu-id="35e05-105">Background context</span></span>
<span data-ttu-id="35e05-106">Emulator Express wordt standaard gebruikt voor het opsporen van Cloud Services-Web- en werkrollen rollen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35e05-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="35e05-107">Deze instelling is opgegeven in de pagina eigenschappen Hallo Cloud Services-project.</span><span class="sxs-lookup"><span data-stu-id="35e05-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Eigenschappen van het project openen][0]

![Snelle emulator is standaard geselecteerd][1]

<span data-ttu-id="35e05-110">Hallo [Visual C++ Redistributable] [ Visual C++ Redistributable] voor Visual Studio is vereist voor de Emulator express.</span><span class="sxs-lookup"><span data-stu-id="35e05-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="35e05-111">Het is momenteel niet geïnstalleerd Hello Azure-workload.</span><span class="sxs-lookup"><span data-stu-id="35e05-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="35e05-112">Bij F5 gebaar toodebug naar een Cloud Services-toepassingen, Visual Studio zou tooinstall gevraagd dit onderdeel en doorgaan met het opsporen van fouten.</span><span class="sxs-lookup"><span data-stu-id="35e05-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Prompt voor C++ Redistributable installeren][2]

<span data-ttu-id="35e05-114">Klik op Ja tooinstall C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="35e05-114">Click Yes tooinstall C++ Redistributable.</span></span>

![C++ Redistributable installeren][3]

<span data-ttu-id="35e05-116">Druk op F5 opnieuw toolaunch foutopsporing sessies.</span><span class="sxs-lookup"><span data-stu-id="35e05-116">Press F5 again toolaunch debugging sessions.</span></span>

![Foutopsporing starten][4]

![Foutopsporing geslaagd][5]

> <span data-ttu-id="35e05-119">Opmerking: Visual C++ Redistributable installeren is een eenmalige inspanning.</span><span class="sxs-lookup"><span data-stu-id="35e05-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="35e05-120">Als u een van een oudere versie van Azure SDK upgrade en Emulator Express hebt geïnstalleerd, kunt u dit probleem won't optreedt.</span><span class="sxs-lookup"><span data-stu-id="35e05-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="35e05-121">Handmatige tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="35e05-121">Manual workaround</span></span>
<span data-ttu-id="35e05-122">U kunt ook installeren Hallo [Visual C++ Redistributable] [ Visual C++ Redistributable] handmatig en hetzelfde effect worden toegepast zoals hoe Visual Studio het op uw systeem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="35e05-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="35e05-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="35e05-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="35e05-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="35e05-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="35e05-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35e05-125">Next Steps</span></span>
<span data-ttu-id="35e05-126">Meer informatie over het gebruik van Azure Computer Emulator toodebug uw Cloud Services-toepassingen in Visual Studio: [toorun Emulator Express gebruiken en foutopsporing een cloudservice op een lokale computer][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="35e05-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
