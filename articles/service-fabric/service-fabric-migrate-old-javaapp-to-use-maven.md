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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="d08b6-104">Uw vorige Java Service Fabric-toepassing toofetch Java-bibliotheken van Maven bijwerken</span><span class="sxs-lookup"><span data-stu-id="d08b6-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="d08b6-105">Binaire bestanden voor Service Fabric Java onlangs verplaatst Hallo Service Fabric Java SDK tooMaven hosten.</span><span class="sxs-lookup"><span data-stu-id="d08b6-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="d08b6-106">Nu kunt u **mavencentral** toofetch Hallo nieuwste Service Fabric-Java-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d08b6-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="d08b6-107">Sjabloon of Eclipse toobe compatibel is met de Hallo gebaseerd Maven build, gebruikt deze snel starten helpt bij het bijwerken van uw bestaande Java-toepassingen die u eerder toobe gemaakt met Service Fabric Java SDK, met behulp van beide Yeoman.</span><span class="sxs-lookup"><span data-stu-id="d08b6-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08b6-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d08b6-108">Prerequisites</span></span>
1. <span data-ttu-id="d08b6-109">U moet eerst toouninstall Hallo bestaande Java SDK.</span><span class="sxs-lookup"><span data-stu-id="d08b6-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="d08b6-110">Installatie Hallo nieuwste Service Fabric CLI volgende Hallo stappen vermeld [hier](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d08b6-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="d08b6-111">toobuild en werk op Hallo Service Fabric-Java-toepassingen, moet u tooensure dat u JDK 1.8 hebt en Gradle geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d08b6-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="d08b6-112">Als u nog niet is geïnstalleerd, kunt u uitvoeren na tooinstall Hallo JDK 1.8 (openjdk-8-jdk) en Gradle -</span><span class="sxs-lookup"><span data-stu-id="d08b6-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="d08b6-113">Hallo installeren/verwijderen scripts voor het bijwerken van uw toepassing toouse Hallo nieuwe Service Fabric CLI Hallo stappen uit te voeren die worden vermeld [hier](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="d08b6-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="d08b6-114">U kunt aan de slag tooour verwijzen [voorbeelden](https://github.com/Azure-Samples/service-fabric-java-getting-started) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="d08b6-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="d08b6-115">Na het verwijderen van Service Fabric Java SDK Hallo werkt Yeoman niet.</span><span class="sxs-lookup"><span data-stu-id="d08b6-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="d08b6-116">Ga als volgt Hallo vereisten vermeld [hier](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java sjabloon generator van en werken.</span><span class="sxs-lookup"><span data-stu-id="d08b6-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="d08b6-117">Service Fabric-Java-bibliotheken op Maven</span><span class="sxs-lookup"><span data-stu-id="d08b6-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="d08b6-118">Service Fabric Java-bibliotheken worden gehost in Maven.</span><span class="sxs-lookup"><span data-stu-id="d08b6-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="d08b6-119">U kunt op Hallo Hallo afhankelijkheden toevoegen ``pom.xml`` of ``build.gradle`` van uw projecten toouse Service Fabric-Java-bibliotheken van **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="d08b6-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="d08b6-120">Actoren</span><span class="sxs-lookup"><span data-stu-id="d08b6-120">Actors</span></span>

<span data-ttu-id="d08b6-121">Ondersteuning voor betrouwbare actoren in Service Fabric voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d08b6-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="d08b6-122">Services</span><span class="sxs-lookup"><span data-stu-id="d08b6-122">Services</span></span>

<span data-ttu-id="d08b6-123">Betrouwbare ondersteuning voor stateless services in Service Fabric voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d08b6-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="d08b6-124">Andere</span><span class="sxs-lookup"><span data-stu-id="d08b6-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="d08b6-125">Transport</span><span class="sxs-lookup"><span data-stu-id="d08b6-125">Transport</span></span>

<span data-ttu-id="d08b6-126">Ondersteuning van transportlaag voor Service Fabric Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d08b6-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="d08b6-127">U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen, toevoegen, tenzij u programmeren op Hallo transportlaag.</span><span class="sxs-lookup"><span data-stu-id="d08b6-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="d08b6-128">Fabric-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="d08b6-128">Fabric support</span></span>

<span data-ttu-id="d08b6-129">Niveau ondersteuning voor Service Fabric, die wordt gesproken toonative Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="d08b6-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="d08b6-130">U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d08b6-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="d08b6-131">Dit wordt automatisch opgehaald uit de Maven, wanneer u opneemt Hallo andere bovenstaande afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d08b6-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="d08b6-132">Stateless service in Service Fabric migreren</span><span class="sxs-lookup"><span data-stu-id="d08b6-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="d08b6-133">toobe kunnen toobuild uw bestaande Service Fabric staatloze Java service met behulp van Service Fabric-afhankelijkheden van Maven opgehaald, moet u tooupdate hello ``build.gradle`` bestand in de Hallo Service.</span><span class="sxs-lookup"><span data-stu-id="d08b6-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="d08b6-134">Eerder als volgt - toobe zoals gebruikt</span><span class="sxs-lookup"><span data-stu-id="d08b6-134">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="d08b6-135">Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben</span><span class="sxs-lookup"><span data-stu-id="d08b6-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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
<span data-ttu-id="d08b6-136">In het algemeen tooget een idee te geven over het Hallo script bouwen eruitziet voor een Service Fabric staatloze Java-service, raadpleegt u tooany voorbeeld van onze voorbeelden aan de slag.</span><span class="sxs-lookup"><span data-stu-id="d08b6-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="d08b6-137">Hier volgt Hallo [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) voor Hallo EchoServer voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d08b6-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="d08b6-138">Actor-service van Service Fabric migreren</span><span class="sxs-lookup"><span data-stu-id="d08b6-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="d08b6-139">toobe kunnen toobuild uw bestaande Service Fabric Actor Java-toepassing met behulp van Service Fabric-afhankelijkheden van Maven opgehaald, moet u tooupdate hello ``build.gradle`` bestand in de interface-pakket hello en in het servicepakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="d08b6-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="d08b6-140">Als u een pakket TestClient hebt, moet u dat ook tooupdate.</span><span class="sxs-lookup"><span data-stu-id="d08b6-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="d08b6-141">In dat geval voor uw actor ``Myactor``, Hallo volgende Hallo locaties waar u tooupdate - nodig zou zijn</span><span class="sxs-lookup"><span data-stu-id="d08b6-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="d08b6-142">Build script voor Hallo interface project bijwerken</span><span class="sxs-lookup"><span data-stu-id="d08b6-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="d08b6-143">Eerder als volgt - toobe zoals gebruikt</span><span class="sxs-lookup"><span data-stu-id="d08b6-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="d08b6-144">Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben</span><span class="sxs-lookup"><span data-stu-id="d08b6-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="d08b6-145">Build script voor Hallo actor project bijwerken</span><span class="sxs-lookup"><span data-stu-id="d08b6-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="d08b6-146">Eerder als volgt - toobe zoals gebruikt</span><span class="sxs-lookup"><span data-stu-id="d08b6-146">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="d08b6-147">Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben</span><span class="sxs-lookup"><span data-stu-id="d08b6-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="d08b6-148">Build script voor Hallo client testproject bijwerken</span><span class="sxs-lookup"><span data-stu-id="d08b6-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="d08b6-149">Wijzigingen die hier zijn vergelijkbaar toohello wijzigingen beschreven in de vorige sectie, dat wil zeggen, Hallo actor-project.</span><span class="sxs-lookup"><span data-stu-id="d08b6-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="d08b6-150">Eerder Hallo Gradle toobe script gebruikt, zoals als volgt-</span><span class="sxs-lookup"><span data-stu-id="d08b6-150">Previously hello Gradle script used toobe like as follows -</span></span>
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
<span data-ttu-id="d08b6-151">Nu toofetch Hallo afhankelijkheden van Maven, Hallo **bijgewerkt** ``build.gradle`` Hallo corresponderende delen zou als volgt - hebben</span><span class="sxs-lookup"><span data-stu-id="d08b6-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d08b6-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d08b6-152">Next steps</span></span>

* [<span data-ttu-id="d08b6-153">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="d08b6-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="d08b6-154">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="d08b6-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="d08b6-155">Interactie met Service Fabric-clusters met Hallo Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="d08b6-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
