---
title: aaaCreate uw eerste app in Azure microservices op Linux met C# | Microsoft Docs
description: Een Service Fabric-toepassing maken en implementeren met behulp van C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Uw eerste Azure Service Fabric-toepassing maken
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric biedt SDK's voor het bouwen van services in Linux in zowel .NET Core als Java. In deze zelfstudie kijken we hoe toocreate een toepassing voor Linux en build een service met C# (.NET Core).

## <a name="prerequisites"></a>Vereisten
Zorg voordat u begint ervoor dat u [uw Linux-ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started-linux.md). Als u Mac OS X gebruikt, kunt u [een Linux one-box omgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).

Wilt u ook tooinstall hello [Service Fabric CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Installeren en Hallo genereren voor CSharp instellen
Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric CSharp-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator. Volg de stappen Hallo hieronder tooensure er Hallo Service Fabric yeoman sjabloon generator voor CSharp werkt op uw computer.
1. nodejs en NPM installeren op uw computer

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. [Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM

  ```bash
  sudo npm install -g yo
  ```
3. Hallo Service Fabric Yeo Java-toepassing generator installeren via NPM

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Hallo-toepassing maken
Een Service Fabric-toepassing kan een of meer services, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing hello bevatten. Hallo Service Fabric [Yeoman](http://yeoman.io/) generator voor CSharp die u in de laatste stap hebt geïnstalleerd, maakt het eenvoudig toocreate uw eerste service en later tooadd. Laten we Yeoman toocreate een toepassing met een enkele service gebruiken.

1. Typ in een terminal Hallo opdracht toostart bouwen Hallo steigers te volgen:`yo azuresfcsharp`
2. Geef uw toepassing een naam.
3. Hallo-type van uw eerste service kiezen en noem deze. Voor Hallo doel van deze zelfstudie kiest u een betrouwbare Actor-Service.

   ![Service Fabric Yeoman-generator voor C#][sf-yeoman]

> [!NOTE]
> Zie voor meer informatie over opties voor Hallo [Service Fabric programming model overzicht](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Hallo-toepassing bouwen
Hallo Service Fabric Yeoman sjablonen bevatten een build-script dat u toobuild Hallo-app uit Hallo terminal gebruiken kunt (na de toepassingsmap toohello navigeren).

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a>Hallo-toepassing implementeren

Als de toepassing hello is gebouwd, kunt u het lokale cluster toohello implementeren.

1. Verbinding maken met toohello lokale Service Fabric-cluster.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Voer Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype hello, en maken van een exemplaar van de toepassing hello.

    ```bash
    ./install.sh
    ```

Implementatie Hallo gebouwd toepassing is dezelfde als een andere Service Fabric-toepassing hello. Raadpleeg de documentatie Hallo op [het beheren van een Service Fabric-toepassing Hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) voor gedetailleerde instructies.

Parameters toothese opdrachten vindt u in de manifesten in programmapakket Hallo Hallo gegenereerd.

Zodra het Hallo-toepassing is geïmplementeerd, open een browser en Ga naar [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) op [http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Vouw vervolgens Hallo **toepassingen** knooppunt en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type opmerking.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Hallo testclient Start en een failover uitvoeren
Actorprojecten doen niets uit zichzelf. Vereist een andere service of client toosend ze berichten. Hallo actor-sjabloon bevat een eenvoudige test-script dat u toointeract met Hallo actor-service gebruiken kunt.

1. Met behulp van Hallo controle hulpprogramma toosee Hallo uitvoer van Hallo actor service Hallo-script uitvoeren.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. Zoek knooppunt Hallo primaire replica voor Hallo actor service gehost in Service Fabric Explorer. In onderstaande Hallo schermafbeelding is het knooppunt 3.

    ![Zoeken naar de primaire replica Hallo in Service Fabric Explorer][sfx-primary]
3. Klik op Hallo knooppunt u gevonden in de vorige stap Hallo en selecteer vervolgens **uitschakelen (opnieuw opstarten)** van menu Hallo-acties. Deze actie wordt één knooppunt in het lokale cluster een failover-tooa secundaire replica uitgevoerd op een ander knooppunt geforceerd opnieuw opgestart. Als u deze actie uitvoert, betaalt u aandacht toohello uitvoer van Hallo testclient en opmerking dat Hallo item blijft tooincrement ondanks Hallo failover.

## <a name="adding-more-services-tooan-existing-application"></a>Meer services tooan bestaande toepassing toe te voegen

tooadd een andere service tooan toepassing al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren:
1. Toohello hoofdmap van de bestaande toepassing hello wijzigen.  Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.
2. Voer `yo azuresfcsharp:AddService` uit.

## <a name="migrating-from-projectjson-toocsproj"></a>Migreren van project.json too.csproj
1. Uitgevoerd 'dotnet migreren' in de hoofdmap project worden alle Hallo project.json toocsproj indeling worden gemigreerd.
2. Update Hallo project verwijst naar dienovereenkomstig toocsproj bestanden in de project-bestanden.
3. Hallo bestand namen toocsproj projectbestanden in build.sh bijwerken.

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interactie met Service Fabric-clusters met Hallo Service Fabric CLI](service-fabric-cli.md)
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)
* [Aan de slag met de Service Fabric-CLI](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
