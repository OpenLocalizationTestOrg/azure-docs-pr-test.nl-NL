---
title: aaaQuickly een bestaande app tooan Azure Service Fabric-cluster implementeren
description: Een Azure Service Fabric-cluster toohost een bestaande Node.js-toepassing met Visual Studio gebruiken.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Een Node.js-toepassing hosten in Azure Service Fabric

Deze snelstartgids kunt u een bestaande toepassing (Node.js in dit voorbeeld) tooa Service Fabric-cluster implementeren uitgevoerd op Azure.

## <a name="prerequisites"></a>Vereisten

Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md). Dit omvat Hallo Service Fabric SDK en Visual Studio 2017 of 2015 installeren.

U moet ook een bestaande Node.js-toepassing toohave voor implementatie. Deze snelstartgids maakt gebruik van een eenvoudige Node.js-website die [hier][download-sample] kan worden gedownload. Dit bestand tooyour uitpakken `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` map nadat u in de volgende stap Hallo Hallo-project maakt.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account][create-account] aan.

## <a name="create-hello-service"></a>Hallo-service maken

Start Visual Studio als **beheerder**.

Maak een project met `CTRL`+`SHIFT`+`N`

In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.

Naam van de toepassing hello **MyGuestApp** en druk op **OK**.

>[!IMPORTANT]
>Node.js kunnen eenvoudig 260 tekens voor paden met windows hello worden verbroken. Een korte pad gebruiken voor het Hallo-project zelf zoals **c:\code\svc1**.
   
![Dialoogvenster voor nieuw project in Visual Studio][new-project]

U kunt elk type Service Fabric-service van het volgende dialoogvenster Hallo maken. Kies voor deze snelstartgids **Door gast uitvoerbaar bestand**.

Service voor Hallo **MyGuestService** en Hallo opties instellen op de juiste toohello Hallo de volgende waarden:

| Instelling                   | Waarde |
| ------------------------- | ------ |
| Map met codepakket       | _&lt;Hallo-map met uw Node.js-app&gt;_ |
| Gedrag codepakket     | Kopieer de map inhoud tooproject |
| Programma                   | node.exe |
| Argumenten                 | server.js |
| Werkmap            | CodePackage |

Druk op **OK**.

![Dialoogvenster voor nieuwe service in Visual Studio][new-service]

Visual Studio maakt het toepassingsproject Hallo en Hallo actor-serviceproject en geeft deze weer in Solution Explorer.

Hallo-toepassingsproject (**MyGuestApp**) bevat geen code rechtstreeks. Het verwijst naar een reeks serviceprojecten. Daarnaast bevat het project drie andere typen inhoud:

* **Profielen publiceren**  
Hulpprogrammavoorkeuren voor verschillende omgevingen.

* **Scripts**  
PowerShell-script voor het implementeren/bijwerken van uw toepassing.

* **Toepassingsdefinitie**  
Hallo-toepassingsmanifest onder omvat *ApplicationPackageRoot*. Bijbehorende parameter voor toepassingsbestanden onder zijn *ApplicationParameters*, die toepassing hello definiëren en kunt u tooconfigure specifiek voor een bepaalde omgeving.
    
Zie voor een overzicht van Hallo inhoud van het serviceproject Hallo [aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Netwerkservice instellen

Hallo-voorbeeld we implementeert Node.js-app gebruikt poort **80** en moeten tootell Service Fabric die we nodig hebben die poort weergegeven.

Open Hallo **ServiceManifest.xml** bestand in Hallo-project. Aan de onderkant van de Hallo van Hallo manifest, er is een `<Resources> \ <Endpoints>` met een vermelding is al gedefinieerd. Wijzigen van deze vermelding tooadd `Port`, `Protocol`, en `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>TooAzure implementeren

Als u op **F5** en Hallo-project uitvoeren, is het lokale cluster geïmplementeerde toohello. We gaan echter tooAzure in plaats daarvan implementeren.

Met de rechtermuisknop op het Hallo-project en kies **publiceren...**  waarmee u een dialoogvenster toopublish tooAzure opent.

![Dialoogvenster tooazure voor een service fabric-service publiceren][publish]

Selecteer Hallo **PublishProfiles\Cloud.xml** profiel als doel.

Als u niet eerder hebt, kiest u een Azure-account toodeploy naar. Als u er nog geen hebt, [meldt u zich er voor een aan][create-account].

Onder **verbindingseindpunt**, selecteer Hallo toodeploy voor Service Fabric-cluster aan. Als u geen abonnement hebt, selecteert u  **&lt;nieuw Cluster maken... &gt;**  die web browser venster toohello Azure-portal wordt geopend. Zie voor meer informatie [maken van een cluster in Hallo portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Wanneer u Hallo Service Fabric-cluster maakt, moet u ervoor dat tooset hello **aangepaste eindpunten** instellen te**80**.

![Service Fabric-knooppuntconfiguratie met aangepast eindpunt][custom-endpoint]

Maken van een nieuwe Service Fabric-cluster duurt enige tijd toocomplete. Nadat deze is gemaakt, gaat u terug toohello dialoogvenster publiceren en selecteer  **&lt;vernieuwen&gt;**. het nieuwe cluster Hello wordt vermeld in de vervolgkeuzelijst Hallo; Selecteer deze.

Druk op **publiceren** en wachten op Hallo implementatie toofinish.

Dit kan enkele minuten duren. Nadat deze is voltooid, wordt het duurt enkele minuten voor Hallo toepassing toobe volledig beschikbaar.

## <a name="test-hello-website"></a>Test Hallo website

Test uw service na publicatie in een webbrowser. 

Eerst openen hello Azure-portal en zoek de Service Fabric-service.

Ga naar de blade overzicht Hallo van Hallo-serviceadres. Hallo-domeinnaam voor gebruik van Hallo _verbindingseindpunt Client_ eigenschap. Bijvoorbeeld `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Service fabric-overzichtsblade op Hallo Azure-portal][overview]

Navigeer toothis adres waar u Hallo ziet `HELLO WORLD` antwoord.

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

Vergeet niet alle Hallo-resources die u hebt gemaakt voor deze snelstartgids, als u in rekening voor die resources gebracht toodelete.

## <a name="next-steps"></a>Volgende stappen
Lees meer over [door gast uitvoerbare bestanden](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F