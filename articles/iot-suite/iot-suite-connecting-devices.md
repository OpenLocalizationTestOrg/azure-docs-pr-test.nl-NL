---
title: aaaConnect een apparaat met C op Windows | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in C met Windows.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Verbinding maken met uw apparaat toohello voor externe controle vooraf geconfigureerde oplossing (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Een voorbeeld C oplossing maken in Windows
Hallo stappen ziet u hoe toocreate een clienttoepassing die met de Hallo externe controle communiceert vooraf geconfigureerde oplossing. Deze toepassing is geschreven in C en gebouwd en op Windows worden uitgevoerd.

Maak een starter-project in Visual Studio 2015 of Visual Studio 2017 en Hallo Iothub apparaat-client NuGet-pakketten toevoegen:

1. Maak in Visual Studio een C-consoletoepassing met behulp van Visual C++ Hallo **Win32-consoletoepassing** sjabloon. Naam Hallo project **RMDevice**.
2. Op Hallo **toepassingsinstellingen** pagina in Hallo **Wizard Win32-toepassing**, zorg ervoor dat **consoletoepassing** is geselecteerd en schakel het selectievakje **Precompiled koptekst** en **Security Development Lifecycle (SDL) controleert**.
3. In **Solution Explorer**, Hallo bestanden stdafx.h, targetver.h en stdafx.cpp worden verwijderd.
4. In **Solution Explorer**, wijzig de naam van Hallo bestand RMDevice.cpp tooRMDevice.c.
5. In **Solution Explorer**, met de rechtermuisknop op Hallo **RMDevice** project en klik vervolgens op **beheren NuGet-pakketten**. Klik op **Bladeren**, zoek vervolgens naar en installeren van Hallo NuGet-pakketten te volgen:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. In **Solution Explorer**, met de rechtermuisknop op Hallo **RMDevice** project en klik vervolgens op **eigenschappen** tooopen Hallo project **eigenschappenvensters**in het dialoogvenster. Zie voor meer informatie [instelling Visual C++-Projecteigenschappen][lnk-c-project-properties]. 
7. Klik op Hallo **Linker** map, klikt u vervolgens op Hallo **invoer** eigenschappenpagina.
8. Voeg **crypt32.lib** toohello **extra afhankelijkheden** eigenschap. Klik op **OK** en vervolgens **OK** opnieuw toosave Hallo project eigenschapswaarden.

Toevoegen van Hallo Parson JSON bibliotheek toohello **RMDevice** project en voeg Hallo vereist `#include` instructies:

1. Kloon Hallo Parson GitHub-opslagplaats met behulp van de volgende opdracht Hallo in een geschikte map op uw computer:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Hallo parson.h en parson.c bestanden kopiëren van de lokale kopie Hallo van Hallo Parson opslagplaats tooyour **RMDevice** projectmap.

1. In Visual Studio met de rechtermuisknop op Hallo **RMDevice** project, klikt u op **toevoegen**, en klik vervolgens op **bestaand Item**.

1. In Hallo **Add Existing Item** dialoogvenster, selecteer Hallo parson.h en parson.c bestanden in Hallo **RMDevice** projectmap. Klik vervolgens op **toevoegen** tooadd deze twee bestanden tooyour-project.

1. In Visual Studio Hallo RMDevice.c bestand te openen. Hallo bestaande `#include` instructies met Hallo code te volgen:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Nu kunt u controleren of uw project de juiste afhankelijkheden Hallo is ingesteld heeft door het opstellen.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Bouwen en uitvoeren van Hallo-voorbeeld

Toevoegen van code tooinvoke Hallo **externe\_bewaking\_uitvoeren** werken en vervolgens toepassing bouwen en uitvoeren Hallo apparaat.

1. Vervang Hallo **belangrijkste** functie met de volgende code tooinvoke hello **externe\_bewaking\_uitvoeren** functie:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Klik op **bouwen** en vervolgens **Build Solution** toobuild Hallo device-toepassing.

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **RMDevice** project, klikt u op **Debug**, en klik vervolgens op **nieuw exemplaar gestart** toorun Hallo voorbeeld. Hallo-console geeft weer berichten hello toepassing verzendt voorbeeld telemetrie toohello vooraf geconfigureerde oplossing, ontvangt de gewenste eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageert.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
