---
title: aaaSet van uw ontwikkelomgeving op Mac OS X-toowork met Azure Service Fabric | Microsoft Docs
description: Installeer Hallo runtime, SDK en hulpprogramma's en maak een lokaal ontwikkelcluster. Na het voltooien van deze installatie, kunt u zich gereed toobuild toepassingen op Mac OS X.
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
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="2c5a9-104">Uw ontwikkelomgeving instellen in Mac OS X</span><span class="sxs-lookup"><span data-stu-id="2c5a9-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c5a9-105">Windows</span><span class="sxs-lookup"><span data-stu-id="2c5a9-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="2c5a9-106">Linux</span><span class="sxs-lookup"><span data-stu-id="2c5a9-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="2c5a9-107">OSX</span><span class="sxs-lookup"><span data-stu-id="2c5a9-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="2c5a9-108">U kunt Service Fabric-toepassingen toorun opbouwen op Linux-clusters met Mac OS X. In dit artikel bevat informatie over hoe tooset van uw Mac voor ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c5a9-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c5a9-109">Prerequisites</span></span>
<span data-ttu-id="2c5a9-110">Service Fabric voert geen systeemeigen op OS X. toorun lokale Service Fabric-cluster, bieden we een vooraf geconfigureerde Ubuntu-virtuele machine met behulp van Vagrant en VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="2c5a9-111">Voordat u aan de slag gaat, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2c5a9-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="2c5a9-112">Vagrant (v1.8.4 of hoger)</span><span class="sxs-lookup"><span data-stu-id="2c5a9-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="2c5a9-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="2c5a9-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="2c5a9-114">U moet toouse wederzijds ondersteunde versies van Vagrant en VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="2c5a9-115">Vagrant functioneert mogelijk niet goed in combinatie met een niet-ondersteunde versie van VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="2c5a9-116">Maak Hallo lokale virtuele machine</span><span class="sxs-lookup"><span data-stu-id="2c5a9-116">Create hello local VM</span></span>
<span data-ttu-id="2c5a9-117">toocreate Hallo lokale virtuele machine met een 5-knooppunt Service Fabric-cluster, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c5a9-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="2c5a9-118">Kloon Hallo `Vagrantfile` opslagplaats</span><span class="sxs-lookup"><span data-stu-id="2c5a9-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="2c5a9-119">Deze stappen brengen keuzelijsten Hallo bestand `Vagrantfile` met Hallo VM configuratie samen met de Hallo locatie Hallo VM wordt gedownload van.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="2c5a9-120">Navigeer toohello lokale kloon van de opslagplaats Hallo</span><span class="sxs-lookup"><span data-stu-id="2c5a9-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="2c5a9-121">(Optioneel) Hallo VM standaardinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="2c5a9-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="2c5a9-122">Standaard is hello lokale virtuele machine geconfigureerd als volgt:</span><span class="sxs-lookup"><span data-stu-id="2c5a9-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="2c5a9-123">3 GB toegewezen geheugen</span><span class="sxs-lookup"><span data-stu-id="2c5a9-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="2c5a9-124">Persoonlijke host netwerk geconfigureerd IP-192.168.50.50 passthrough van verkeer van Hallo Mac host inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c5a9-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="2c5a9-125">U kunt een van deze instellingen wijzigen of toevoegen van andere configuratie toohello VM in Hallo `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="2c5a9-126">Zie Hallo [Vagrant documentatie](http://www.vagrantup.com/docs) voor Hallo volledige lijst met configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="2c5a9-127">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="2c5a9-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="2c5a9-128">Deze stap downloadt Hallo vooraf geconfigureerde VM-installatiekopie, het lokaal en stel vervolgens een lokale Service Fabric-cluster in het opstarten.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="2c5a9-129">U moet verwacht dat het tootake enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="2c5a9-130">Als setup voltooid is, ziet u een bericht in Hallo-uitvoer die aangeeft dat Hallo-cluster wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![Starten van clusterinstallatie na inrichting van VM][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="2c5a9-132">Als Hallo VM downloaden lang duurt, kunt u downloaden met behulp van wget of curl of via een browser door te navigeren toohello koppeling opgegeven door **config.vm.box_url** in Hallo bestand `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="2c5a9-133">Na het downloaden van het lokaal, bewerken `Vagrantfile` toopoint toohello lokaal pad waar u de installatiekopie van het Hallo hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="2c5a9-134">Voor bijvoorbeeld als u Hallo installatiekopie too/home/users/test/azureservicefabric.tp8.box, gedownload vervolgens ingesteld **config.vm.box_url** toothat pad.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="2c5a9-135">Testen die Hallo cluster heeft correct zijn ingesteld door te navigeren tooService Fabric Explorer op http://192.168.50.50:19080/Explorer (ervan uitgaande dat u bewaard Hallo standaard particuliere netwerk-IP).</span><span class="sxs-lookup"><span data-stu-id="2c5a9-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric Explorer weergegeven van de host Hallo Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="2c5a9-137">Toepassingen maken op een Mac met Yeoman</span><span class="sxs-lookup"><span data-stu-id="2c5a9-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="2c5a9-138">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="2c5a9-139">Volg de stappen Hallo hieronder tooensure er Hallo Service Fabric yeoman sjabloon generator op uw computer werkt.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="2c5a9-140">U moet toohave Node.js en geïnstalleerd op een mac u NPM.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="2c5a9-141">Als dat niet kunt u Node.js en NPM met gebruik van de volgende Hallo Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="2c5a9-142">toocheck hello versies van Node.js en geïnstalleerd op uw Mac NPM, kunt u Hallo ``-v`` optie.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="2c5a9-143">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="2c5a9-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="2c5a9-144">Hallo Yeoman installeren generator gewenste toouse, stappen te volgen Hallo in aan de slag Hallo [documentatie](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2c5a9-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="2c5a9-145">toocreate Service Fabric-toepassingen met behulp van Yeoman, stappen Hallo-</span><span class="sxs-lookup"><span data-stu-id="2c5a9-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="2c5a9-146">een Service Fabric-Java-toepassing op Mac toobuild, moet u - JDK 1.8 en Gradle op Hallo machine geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="2c5a9-147">Hallo Service Fabric-invoegtoepassing voor Eclipse Neon installeren</span><span class="sxs-lookup"><span data-stu-id="2c5a9-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="2c5a9-148">Service Fabric bevat een invoegtoepassing voor Hallo **Eclipse Neon voor IDE voor Java** die Hallo-proces voor het maken, bouwen en implementeren van Java-services kunt vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="2c5a9-149">U kunt stappen Hallo installatie vermeld in deze algemene [documentatie](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) over het installeren of bijwerken van Service Fabric Eclipse-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="2c5a9-150">Standaard wordt Hallo default IP ondersteund zoals vermeld in Hallo ``Vagrantfile`` in Hallo ``Local.json`` van de toepassing hello gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="2c5a9-151">Werk Hallo bijbehorende IP-adres in als u deze instelling wijzigen en Vagrant met een ander IP-adres implementeert, ``Local.json`` van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c5a9-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c5a9-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c5a9-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="2c5a9-153">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="2c5a9-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="2c5a9-154">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="2c5a9-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="2c5a9-155">Maken van een Service Fabric-cluster in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2c5a9-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="2c5a9-156">Maken van een Service Fabric-cluster met behulp van hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c5a9-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="2c5a9-157">Hallo Service Fabric-toepassingsmodel begrijpen</span><span class="sxs-lookup"><span data-stu-id="2c5a9-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
