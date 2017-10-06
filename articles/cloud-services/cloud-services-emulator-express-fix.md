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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Toodebug Cloud Services-toepassing Emulator Express gebruiken in de VS 2017
Dit artikel wordt uitgelegd hoe toouse Emulator Express toodebug Cloud Services-toepassingen in VS-2017.

## <a name="background-context"></a>Achtergrond-context
Emulator Express wordt standaard gebruikt voor het opsporen van Cloud Services-Web- en werkrollen rollen in Visual Studio. Deze instelling is opgegeven in de pagina eigenschappen Hallo Cloud Services-project.

![Eigenschappen van het project openen][0]

![Snelle emulator is standaard geselecteerd][1]

Hallo [Visual C++ Redistributable] [ Visual C++ Redistributable] voor Visual Studio is vereist voor de Emulator express. Het is momenteel niet geïnstalleerd Hello Azure-workload. Bij F5 gebaar toodebug naar een Cloud Services-toepassingen, Visual Studio zou tooinstall gevraagd dit onderdeel en doorgaan met het opsporen van fouten.

![Prompt voor C++ Redistributable installeren][2]

Klik op Ja tooinstall C++ Redistributable.

![C++ Redistributable installeren][3]

Druk op F5 opnieuw toolaunch foutopsporing sessies.

![Foutopsporing starten][4]

![Foutopsporing geslaagd][5]

> Opmerking: Visual C++ Redistributable installeren is een eenmalige inspanning. Als u een van een oudere versie van Azure SDK upgrade en Emulator Express hebt geïnstalleerd, kunt u dit probleem won't optreedt.
> 
> 

## <a name="manual-workaround"></a>Handmatige tijdelijke oplossing
U kunt ook installeren Hallo [Visual C++ Redistributable] [ Visual C++ Redistributable] handmatig en hetzelfde effect worden toegepast zoals hoe Visual Studio het op uw systeem geïnstalleerd.

[vcredist_x86.exe][vcredist_x86.exe]

[vcredist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het gebruik van Azure Computer Emulator toodebug uw Cloud Services-toepassingen in Visual Studio: [toorun Emulator Express gebruiken en foutopsporing een cloudservice op een lokale computer][Using Emulator Express toorun and debug a cloud service on a local machine]

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
