---
title: een Azure Service Fabric betrouwbare actoren Java-toepassing op Linux aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van een toepassing Java Service Fabric betrouwbare actoren in vijf minuten.
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Uw eerste betrouwbare Service Fabric Java-actortoepassing maken in Linux
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Met deze Quick Start kunt u in een paar minuten uw eerste Azure Service Fabric Java-toepassing maken in een Linux-ontwikkelomgeving.  Wanneer u klaar bent, hebt u een eenvoudige Java één service-toepassing uitgevoerd op Hallo lokaal ontwikkelcluster.  

## <a name="prerequisites"></a>Vereisten
Voordat u begint, Hallo Service Fabric SDK installeren, Service Fabric CLI Hallo en instellen van een cluster ontwikkeling in uw [Linux ontwikkelomgeving](service-fabric-get-started-linux.md). Als u Mac OS X gebruikt, kunt u [een Linux-ontwikkelomgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).

Wilt u ook tooinstall hello [Service Fabric CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Installeren en instellen Hallo genereren voor Java
Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric Java-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator. Volg de stappen Hallo hieronder tooensure die u Hallo Service Fabric-generator voor yeoman sjabloon voor Java hebt op uw computer werkt.
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
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Hallo-toepassing maken
Een Service Fabric-toepassing bevat een of meer services, elk met een specifieke rol in de functionaliteit van de toepassing hello leveren. Hallo-generator u geïnstalleerd in de laatste sectie hello, maakt het eenvoudig toocreate uw eerste service en later tooadd.  U kunt ook Service Fabric-Java-toepassingen maken, ontwikkelen en implementeren met behulp van een invoegtoepassing voor Eclipse. Zie [Uw eerste Java-toepassing maken en implementeren met behulp van Eclipse](service-fabric-get-started-eclipse.md). Gebruik Yeoman toocreate een toepassing met een enkele service die worden opgeslagen en opgehaald van een waarde van het prestatiemeteritem voor deze snel starten.

1. Typ in een terminal ``yo azuresfjava``.
2. Geef uw toepassing een naam.
3. Hallo-type van uw eerste service kiezen en noem deze. In deze zelfstudie kiest u voor een Reliable Actor Service. Zie voor meer informatie over Hallo andere soorten services, [Service Fabric programming model overzicht](service-fabric-choose-framework.md).
   ![Service Fabric Yeoman-generator voor Java][sf-yeoman]

## <a name="build-hello-application"></a>Hallo-toepassing bouwen
Hallo Service Fabric Yeoman sjablonen bevatten een build script voor [Gradle](https://gradle.org/), waardoor u toobuild Hallo toepassing hello terminal kunt gebruiken.
Java-afhankelijkheden in Service Fabric worden opgehaald uit Maven. toobuild en werk op Hallo Service Fabric-Java-toepassingen, moet u tooensure dat u JDK hebt en Gradle geïnstalleerd. Als nog niet is geïnstalleerd, kunt u Hallo uitvoeren na de tooinstall JDK(openjdk-8-jdk) en Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild en pakket Hallo-toepassing hello volgende uitvoeren:

  ```bash
  cd myapp
  gradle
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

Zodra het Hallo-toepassing is geïmplementeerd, open een browser en Ga naar [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) op [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).
Vouw vervolgens Hallo **toepassingen** knooppunt en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type opmerking.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Hallo testclient Start en een failover uitvoeren
Actoren iets op hun eigen niet doet, ze een andere service of client toosend vereisen ze berichten. Hallo actor-sjabloon bevat een eenvoudige test-script dat u toointeract met Hallo actor-service gebruiken kunt.

1. Met behulp van Hallo controle hulpprogramma toosee Hallo uitvoer van Hallo actor service Hallo-script uitvoeren.  Hallo testscript roept Hallo `setCountAsync()` methodeaanroepen op Hallo actor tooincrement een teller Hallo `getCountAsync()` methode op Hallo actor tooget Hallo nieuwe itemwaarde en geeft die waarde toohello-console.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. Zoek in Service Fabric Explorer Hallo knooppunt hosting Hallo primaire replica voor Hallo actor-service. In onderstaande Hallo schermafbeelding is het knooppunt 3. Hallo primaire service replica ingangen lees- en schrijfbewerkingen.  Wijzigingen in de status van service vervolgens uit toohello secundaire replica's uitgevoerd op knooppunten 0 en 1 in de onderstaande schermafdruk Hallo worden gerepliceerd.

    ![Zoeken naar de primaire replica Hallo in Service Fabric Explorer][sfx-primary]

3. In **knooppunten**, klikt u op Hallo knooppunt u gevonden in de vorige stap Hallo en selecteer vervolgens **uitschakelen (opnieuw opstarten)** van menu Hallo-acties. Deze actie Hallo knooppunt uitgevoerd Hallo service primaire replica opnieuw is opgestart en zorgt ervoor dat een failover-tooone van Hallo secundaire replica's uitgevoerd op een ander knooppunt.  Die secundaire replica is gepromoveerde tooprimary, een andere secundaire replica is gemaakt op een ander knooppunt en de primaire replica Hallo begint tootake lees-en schrijfbewerkingen. Omdat hello knooppunt opnieuw wordt opgestart, wordt controle Hallo uitvoer van Hallo client testen en houd er rekening mee dat teller Hallo blijft tooincrement ondanks Hallo failover.

## <a name="remove-hello-application"></a>Hallo-toepassing verwijderen
Hallo uninstall-script is opgegeven in Hallo toodelete Hallo toepassing sjabloonexemplaar gebruiken, hef de registratie van het toepassingspakket Hallo en Hallo toepassingspakket verwijderen uit de installatiekopieopslag Hallo-cluster.

```bash
./uninstall.sh
```

In Service Fabric explorer ziet u dat Hallo-toepassing en toepassingstype niet meer in Hallo weergegeven **toepassingen** knooppunt.

## <a name="service-fabric-java-libraries-on-maven"></a>Service Fabric-Java-bibliotheken op Maven
Service Fabric Java-bibliotheken worden gehost in Maven. U kunt op Hallo Hallo afhankelijkheden toevoegen ``pom.xml`` of ``build.gradle`` van uw projecten toouse Service Fabric-Java-bibliotheken van **mavenCentral**.

### <a name="actors"></a>Actoren

Ondersteuning voor betrouwbare actoren in Service Fabric voor uw toepassing.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Services

Betrouwbare ondersteuning voor stateless services in Service Fabric voor uw toepassing.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Andere
#### <a name="transport"></a>Transport

Ondersteuning van transportlaag voor Service Fabric Java-toepassing. U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen, toevoegen, tenzij u programmeren op Hallo transportlaag.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Fabric-ondersteuning

Niveau ondersteuning voor Service Fabric, die wordt gesproken toonative Service Fabric-runtime. U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen toevoegen. Dit wordt automatisch opgehaald uit de Maven, wanneer u opneemt Hallo andere bovenstaande afhankelijkheden.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Oude Service Fabric-Java-toepassingen toobe gebruikt met Maven migreren
We hebben onlangs Service Fabric-Java-bibliotheken verplaatst vanuit Service Fabric Java SDK tooMaven opslagplaats. Tijdens het Hallo nieuwe toepassingen die u met Yeoman of Eclipse genereren genereert de meest recente bijgewerkte projecten (die worden kunnen toowork met Maven), kunt u uw bestaande Service Fabric staatloze of actor Java-toepassingen, wat Hallo Service gebruikten bijwerken Fabric Java SDK eerder toouse Hallo Service Fabric Java afhankelijkheden van Maven. Stappen Hallo vermeld [hier](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure de oudere toepassing met Maven werkt.

## <a name="next-steps"></a>Volgende stappen

* [Uw eerste Service Fabric Java-toepassing maken op Linux met Eclipse](service-fabric-get-started-eclipse.md)
* [Meer informatie over Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interactie met Service Fabric-clusters met Hallo Service Fabric CLI](service-fabric-cli.md)
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)
* [Aan de slag met de Service Fabric-CLI](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
