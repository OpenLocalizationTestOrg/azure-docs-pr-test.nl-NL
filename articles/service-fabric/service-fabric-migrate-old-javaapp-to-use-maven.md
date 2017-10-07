---
title: aaaMigrate van Java SDK tooMaven - oude Azure Service Fabric-Java-toepassingen toouse Maven bijwerken | Microsoft Docs
description: Hallo oudere Java-toepassingen die toouse Hallo Service Fabric Java SDK gebruikt toofetch Service Fabric Java afhankelijkheden van Maven bijwerken. Na het voltooien van deze installatie, zou uw oudere Java-toepassingen kunnen toobuild zijn.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Uw vorige Java Service Fabric-toepassing toofetch Java-bibliotheken van Maven bijwerken
Binaire bestanden voor Service Fabric Java onlangs verplaatst Hallo Service Fabric Java SDK tooMaven hosten. Nu kunt u **mavencentral** toofetch Hallo nieuwste Service Fabric-Java-afhankelijkheden. Sjabloon of Eclipse toobe compatibel is met de Hallo gebaseerd Maven build, gebruikt deze snel starten helpt bij het bijwerken van uw bestaande Java-toepassingen die u eerder toobe gemaakt met Service Fabric Java SDK, met behulp van beide Yeoman.

## <a name="prerequisites"></a>Vereisten
1. U moet eerst toouninstall Hallo bestaande Java SDK.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Installatie Hallo nieuwste Service Fabric CLI volgende Hallo stappen vermeld [hier](service-fabric-cli.md).

3. toobuild en werk op Hallo Service Fabric-Java-toepassingen, moet u tooensure dat u JDK 1.8 hebt en Gradle geïnstalleerd. Als u nog niet is geïnstalleerd, kunt u uitvoeren na tooinstall Hallo JDK 1.8 (openjdk-8-jdk) en Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Hallo installeren/verwijderen scripts voor het bijwerken van uw toepassing toouse Hallo nieuwe Service Fabric CLI Hallo stappen uit te voeren die worden vermeld [hier](service-fabric-application-lifecycle-sfctl.md). U kunt aan de slag tooour verwijzen [voorbeelden](https://github.com/Azure-Samples/service-fabric-java-getting-started) ter referentie.

>[!TIP]
> Na het verwijderen van Service Fabric Java SDK Hallo werkt Yeoman niet. Ga als volgt Hallo vereisten vermeld [hier](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java sjabloon generator van en werken.

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


## <a name="migrating-service-fabric-stateless-service"></a>Stateless service in Service Fabric migreren

toobe kunnen toobuild uw bestaande Service Fabric staatloze Java service met behulp van Service Fabric-afhankelijkheden van Maven opgehaald, moet u tooupdate hello ``build.gradle`` bestand in de Hallo Service. Eerder als volgt - toobe zoals gebruikt
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
In het algemeen tooget een idee te geven over het Hallo script bouwen eruitziet voor een Service Fabric staatloze Java-service, raadpleegt u tooany voorbeeld van onze voorbeelden aan de slag. Hier volgt Hallo [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) voor Hallo EchoServer voorbeeld.

## <a name="migrating-service-fabric-actor-service"></a>Actor-service van Service Fabric migreren

toobe kunnen toobuild uw bestaande Service Fabric Actor Java-toepassing met behulp van Service Fabric-afhankelijkheden van Maven opgehaald, moet u tooupdate hello ``build.gradle`` bestand in de interface-pakket hello en in het servicepakket Hallo. Als u een pakket TestClient hebt, moet u dat ook tooupdate. In dat geval voor uw actor ``Myactor``, Hallo volgende Hallo locaties waar u tooupdate - nodig zou zijn
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Build script voor Hallo interface project bijwerken

Eerder als volgt - toobe zoals gebruikt
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a>Build script voor Hallo actor project bijwerken

Eerder als volgt - toobe zoals gebruikt
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a>Build script voor Hallo client testproject bijwerken

Wijzigingen die hier zijn vergelijkbaar toohello wijzigingen beschreven in de vorige sectie, dat wil zeggen, Hallo actor-project. Eerder Hallo Gradle toobe script gebruikt, zoals als volgt-
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a>Volgende stappen

* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse](service-fabric-get-started-eclipse.md)
* [Interactie met Service Fabric-clusters met Hallo Service Fabric CLI](service-fabric-cli.md)
