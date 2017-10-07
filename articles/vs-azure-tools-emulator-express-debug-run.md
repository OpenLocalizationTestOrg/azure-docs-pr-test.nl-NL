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
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Met Emulator Express cloud toorun en foutopsporing een Azure service op een lokale computer
U kunt testen en fouten opsporen in een cloudservice zonder Visual Studio als administrator uitvoeren met behulp van de Express-Emulator. U kunt uw project instellingen toouse beide Emulator Express instellen of Hallo volledige emulator, afhankelijk van Hallo vereisten van uw cloudservice. Zie voor meer informatie over de volledige emulator Hallo [een Azure-toepassing uitvoert in Hallo Compute-Emulator](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Met een Emulator snelle in Visual Studio
Wanneer u een Azure-project in de Azure SDK 2.3 of hoger maakt, wordt Emulator Express automatisch gebruikt. Gebruik voor bestaande projecten die zijn gemaakt met een eerdere versie van hello Azure SDK Hallo stappen tooselect Emulator Express te volgen:

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.

1. Selecteer in de Hallo projecten eigenschappenpagina's Hallo **Web** tabblad.

    ![Eigenschappen voor een Azure-cloud service-project](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Onder **lokale Ontwikkelaarsserver**, selecteer **optie Gebruik IIS Express**.

1. Onder **Emulator**, selecteer **gebruik Emulator Express**.
   
1. toolaunch hello Emulator Express, uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Emulator Express beperkingen
Hallo problemen volgen enkele bekende beperkingen van de Emulator Express: 

- Emulator Express is niet compatibel met IIS-webserver.
- Uw cloudservice meerdere rollen kan bevatten, maar elke rol beperkt tooone exemplaar is.
- U kunt poortnummers minder dan 1000 niet openen. Als u een verificatieprovider die normaal gesproken gebruikmaakt van een poort minder dan 1000 gebruikt, moet u mogelijk toochange deze waarde tooa-poortnummer dat is meer dan 1000.
- De beperkingen die van toepassing zijn toohello Azure Compute-Emulator tooEmulator Express ook van toepassing. Er geen bijvoorbeeld meer dan 50 rolinstanties per implementatie. Zie voor meer informatie over hello Azure Compute-Emulator [een Azure-toepassing uitvoert in Hallo Compute-Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Volgende stappen
[Foutopsporing van Azure-cloudservices](https://msdn.microsoft.com/library/azure/ee405479.aspx)
