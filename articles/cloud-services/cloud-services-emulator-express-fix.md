---
title: Setup-emulator express voor foutopsporing Cloud Services-toepassingen in Visual Studio | Microsoft Docs
description: Wordt uitgelegd hoe u de C++ redistributable zodat Emulator in Visual Studio Express installeren
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="41ac8-103">Emulator Express gebruiken om op te sporen Cloud Services-toepassing in VS-2017</span><span class="sxs-lookup"><span data-stu-id="41ac8-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="41ac8-104">In dit artikel wordt uitgelegd hoe Emulator Express gebruiken om op te sporen Cloud Services-toepassingen in VS-2017.</span><span class="sxs-lookup"><span data-stu-id="41ac8-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="41ac8-105">Achtergrond-context</span><span class="sxs-lookup"><span data-stu-id="41ac8-105">Background context</span></span>
<span data-ttu-id="41ac8-106">Emulator Express wordt standaard gebruikt voor het opsporen van Cloud Services-Web- en werkrollen rollen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41ac8-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="41ac8-107">Deze instelling is opgegeven in de eigenschappenpagina van de Cloud Services-project.</span><span class="sxs-lookup"><span data-stu-id="41ac8-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Eigenschappen van het project openen][0]

![Snelle emulator is standaard geselecteerd][1]

<span data-ttu-id="41ac8-110">De [Visual C++ Redistributable] [ Visual C++ Redistributable] voor Visual Studio is vereist voor de Emulator express.</span><span class="sxs-lookup"><span data-stu-id="41ac8-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="41ac8-111">Het is momenteel niet geïnstalleerd met de Azure-workload.</span><span class="sxs-lookup"><span data-stu-id="41ac8-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="41ac8-112">Bij F5 gebaar opsporen in een Cloud Services-toepassingen, Visual Studio gevraagd voor het installeren van dit onderdeel en doorgaan met het opsporen van fouten.</span><span class="sxs-lookup"><span data-stu-id="41ac8-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Prompt voor C++ Redistributable installeren][2]

<span data-ttu-id="41ac8-114">Klik op Ja als u wilt C++ Redistributable installeren.</span><span class="sxs-lookup"><span data-stu-id="41ac8-114">Click Yes to install C++ Redistributable.</span></span>

![C++ Redistributable installeren][3]

<span data-ttu-id="41ac8-116">Druk op F5 opnieuw te starten foutopsporingssessies.</span><span class="sxs-lookup"><span data-stu-id="41ac8-116">Press F5 again to launch debugging sessions.</span></span>

![Foutopsporing starten][4]

![Foutopsporing geslaagd][5]

> <span data-ttu-id="41ac8-119">Opmerking: Visual C++ Redistributable installeren is een eenmalige inspanning.</span><span class="sxs-lookup"><span data-stu-id="41ac8-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="41ac8-120">Als u een van een oudere versie van Azure SDK upgrade en Emulator Express hebt geïnstalleerd, kunt u dit probleem won't optreedt.</span><span class="sxs-lookup"><span data-stu-id="41ac8-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="41ac8-121">Handmatige tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="41ac8-121">Manual workaround</span></span>
<span data-ttu-id="41ac8-122">U kunt ook installeren de [Visual C++ Redistributable] [ Visual C++ Redistributable] handmatig en hetzelfde effect worden toegepast zoals hoe Visual Studio het op uw systeem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="41ac8-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="41ac8-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="41ac8-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="41ac8-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="41ac8-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="41ac8-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41ac8-125">Next Steps</span></span>
<span data-ttu-id="41ac8-126">Meer informatie over het gebruik van Azure Computer Emulator opsporen in uw Cloud Services-toepassingen in Visual Studio: [Emulator Express gebruiken voor het uitvoeren en fouten opsporen in een cloudservice op een lokale computer][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="41ac8-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
