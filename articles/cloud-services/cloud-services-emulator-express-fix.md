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
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a>Emulator Express gebruiken om op te sporen Cloud Services-toepassing in VS-2017
In dit artikel wordt uitgelegd hoe Emulator Express gebruiken om op te sporen Cloud Services-toepassingen in VS-2017.

## <a name="background-context"></a>Achtergrond-context
Emulator Express wordt standaard gebruikt voor het opsporen van Cloud Services-Web- en werkrollen rollen in Visual Studio. Deze instelling is opgegeven in de eigenschappenpagina van de Cloud Services-project.

![Eigenschappen van het project openen][0]

![Snelle emulator is standaard geselecteerd][1]

De [Visual C++ Redistributable] [ Visual C++ Redistributable] voor Visual Studio is vereist voor de Emulator express. Het is momenteel niet geïnstalleerd met de Azure-workload. Bij F5 gebaar opsporen in een Cloud Services-toepassingen, Visual Studio gevraagd voor het installeren van dit onderdeel en doorgaan met het opsporen van fouten.

![Prompt voor C++ Redistributable installeren][2]

Klik op Ja als u wilt C++ Redistributable installeren.

![C++ Redistributable installeren][3]

Druk op F5 opnieuw te starten foutopsporingssessies.

![Foutopsporing starten][4]

![Foutopsporing geslaagd][5]

> Opmerking: Visual C++ Redistributable installeren is een eenmalige inspanning. Als u een van een oudere versie van Azure SDK upgrade en Emulator Express hebt geïnstalleerd, kunt u dit probleem won't optreedt.
> 
> 

## <a name="manual-workaround"></a>Handmatige tijdelijke oplossing
U kunt ook installeren de [Visual C++ Redistributable] [ Visual C++ Redistributable] handmatig en hetzelfde effect worden toegepast zoals hoe Visual Studio het op uw systeem geïnstalleerd.

[vcredist_x86.exe][vcredist_x86.exe]

[vcredist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het gebruik van Azure Computer Emulator opsporen in uw Cloud Services-toepassingen in Visual Studio: [Emulator Express gebruiken voor het uitvoeren en fouten opsporen in een cloudservice op een lokale computer][Using Emulator Express to run and debug a cloud service on a local machine]

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
