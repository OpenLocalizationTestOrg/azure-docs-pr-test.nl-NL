---
title: Uw ontwikkelomgeving in Mac OS X instellen voor gebruik met Azure Service Fabric | Microsoft Docs
description: Installeer de runtime, SDK en hulpprogramma's en maak een lokaal ontwikkelcluster. Zodra u dit hebt gedaan, kunt u toepassingen bouwen in Mac OS X.
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="a64ef-104">Uw ontwikkelomgeving instellen in Mac OS X</span><span class="sxs-lookup"><span data-stu-id="a64ef-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a64ef-105">Windows</span><span class="sxs-lookup"><span data-stu-id="a64ef-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="a64ef-106">Linux</span><span class="sxs-lookup"><span data-stu-id="a64ef-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="a64ef-107">OSX</span><span class="sxs-lookup"><span data-stu-id="a64ef-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="a64ef-108">U kunt Service Fabric-toepassingen bouwen voor uitvoering op Linux-clusters met behulp van Mac OS X. In dit artikel wordt uitgelegd hoe u uw Mac kunt instellen voor ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="a64ef-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a64ef-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a64ef-109">Prerequisites</span></span>
<span data-ttu-id="a64ef-110">Service Fabric wordt niet systeemeigen op OS X uitgevoerd. Als u een lokaal Service Fabric-cluster wilt uitvoeren, bieden we een vooraf geconfigureerde virtuele Ubuntu-machine met Vagrant en VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="a64ef-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="a64ef-111">Voordat u aan de slag gaat, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="a64ef-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="a64ef-112">Vagrant (v1.8.4 of hoger)</span><span class="sxs-lookup"><span data-stu-id="a64ef-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="a64ef-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="a64ef-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="a64ef-114">U moet wederzijds ondersteunde versies van Vagrant en VirtualBox gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a64ef-114">You need to use mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="a64ef-115">Vagrant functioneert mogelijk niet goed in combinatie met een niet-ondersteunde versie van VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="a64ef-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-the-local-vm"></a><span data-ttu-id="a64ef-116">De lokale virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a64ef-116">Create the local VM</span></span>
<span data-ttu-id="a64ef-117">Ga als volgt te werk om de lokale VM te maken met een Service Fabric-cluster met 5-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="a64ef-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="a64ef-118">De `Vagrantfile`-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="a64ef-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="a64ef-119">Met deze stappen verkrijgt u het bestand `Vagrantfile` dat de VM-configuratie bevat plus de locatie van waar de virtuele machine is gedownload.</span><span class="sxs-lookup"><span data-stu-id="a64ef-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>

2. <span data-ttu-id="a64ef-120">Navigeer naar de lokale kloon van de opslagplaats</span><span class="sxs-lookup"><span data-stu-id="a64ef-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="a64ef-121">Wijzig de standaardinstellingen van de virtuele machine (optioneel)</span><span class="sxs-lookup"><span data-stu-id="a64ef-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="a64ef-122">Standaard wordt de lokale virtuele machine als volgt geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="a64ef-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="a64ef-123">3 GB toegewezen geheugen</span><span class="sxs-lookup"><span data-stu-id="a64ef-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="a64ef-124">Persoonlijk hostnetwerk geconfigureerd op IP 192.168.50.50 dat passthrough van verkeer van de Mac-host inschakelt</span><span class="sxs-lookup"><span data-stu-id="a64ef-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="a64ef-125">U kunt deze instellingen wijzigen of een andere configuratie toevoegen aan de virtuele machine in de `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="a64ef-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="a64ef-126">Zie de [Vagrant-documentatie](http://www.vagrantup.com/docs) voor de volledige lijst met configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="a64ef-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="a64ef-127">De virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a64ef-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="a64ef-128">In deze stap wordt de vooraf geconfigureerde VM-installatiekopie gedownload, lokaal opgestart en wordt er vervolgens een lokaal Service Fabric-cluster in ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a64ef-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="a64ef-129">Dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a64ef-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="a64ef-130">Als de installatie is voltooid, ziet u een bericht in de uitvoer dat aangeeft dat de cluster wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a64ef-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![Starten van clusterinstallatie na inrichting van VM][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="a64ef-132">Als het downloaden van de virtuele machine lang duurt, kunt u deze downloaden met behulp van wget of curl, of via een browser door te navigeren naar de koppeling die met **config.vm.box_url** is opgegeven in het bestand `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="a64ef-132">If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`.</span></span> <span data-ttu-id="a64ef-133">Nadat u deze lokaal hebt gedownload, bewerkt u `Vagrantfile`, zodat dit wijst naar het lokale pad waar u de installatiekopie hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="a64ef-133">After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image.</span></span> <span data-ttu-id="a64ef-134">Als u de installatiekopie bijvoorbeeld hebt gedownload naar /home/users/test/azureservicefabric.tp8.box, stelt u **config.vm.box_url** in op dat pad.</span><span class="sxs-lookup"><span data-stu-id="a64ef-134">For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.</span></span>
    >

5. <span data-ttu-id="a64ef-135">Test of het cluster correct is ingesteld door naar Service Fabric Explorer te gaan op http://192.168.50.50:19080/Explorer (ervan uitgaande dat u het standaard IP-adres van het privénetwerk hebt gehouden).</span><span class="sxs-lookup"><span data-stu-id="a64ef-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![Service Fabric Explorer bekeken vanuit de host-Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="a64ef-137">Toepassingen maken op een Mac met Yeoman</span><span class="sxs-lookup"><span data-stu-id="a64ef-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="a64ef-138">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="a64ef-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="a64ef-139">Volg de stappen hieronder om te controleren of de Yeoman-sjabloongenerator van Service Fabric werkt op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a64ef-139">Please follow the steps below to ensure you have the Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="a64ef-140">Node.js en NPM moeten zijn geïnstalleerd op uw Mac.</span><span class="sxs-lookup"><span data-stu-id="a64ef-140">You need to have Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="a64ef-141">Als dat niet het geval is, kunt u Node.js en NPM als volgt installeren met behulp van Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a64ef-141">If not you can install Node.js and NPM using Homebrew using the following.</span></span> <span data-ttu-id="a64ef-142">Gebruik de optie ``-v`` om te controleren welke versies van Node.js en NPM zijn geïnstalleerd op uw Mac.</span><span class="sxs-lookup"><span data-stu-id="a64ef-142">To check the versions of Node.js and NPM installed on your Mac, you can use the ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="a64ef-143">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="a64ef-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="a64ef-144">Installeer de Yeoman generator die u wilt gebruiken. Volg hiervoor de stappen in deze [documentatie](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a64ef-144">Install the Yeoman generator you want to use, following the steps in the getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="a64ef-145">Volg deze stappen om Service Fabric-toepassingen te maken met behulp van Yeoman:</span><span class="sxs-lookup"><span data-stu-id="a64ef-145">To create Service Fabric Applications using Yeoman, follow the steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="a64ef-146">Als u een Service Fabric Java-toepassing wilt maken op een Mac, moeten JDK 1.8 en Gradle op de computer zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a64ef-146">To build a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on the machine.</span></span>


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="a64ef-147">De Service Fabric-invoegtoepassing installeren voor Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="a64ef-147">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="a64ef-148">Service Fabric biedt een invoegtoepassing voor de **Eclipse Neon voor Java IDE** die het maken, bouwen en implementeren van Java-services kan vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="a64ef-148">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="a64ef-149">U kunt de installatiestappen volgen uit deze algemene [documentatie](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) over het installeren en bijwerken van de Service Fabric Eclipse-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a64ef-149">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="a64ef-150">De standaardinstelling is dat het standaard-IP-adres wordt ondersteund dat is opgegeven voor ``Vagrantfile`` in de ``Local.json`` van de gegenereerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="a64ef-150">By default we support the default IP as mentioned in the ``Vagrantfile`` in the ``Local.json`` of the generated application.</span></span> <span data-ttu-id="a64ef-151">Als u dat adres wijzigt en Vagrant implementeert met een ander IP-adres, moet u het bijbehorende IP-adres in de ``Local.json`` van uw toepassing ook bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a64ef-151">In case you change that and deploy Vagrant with a different IP, please update the corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a64ef-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a64ef-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="a64ef-153">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="a64ef-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="a64ef-154">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="a64ef-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="a64ef-155">Een Service Fabric-cluster maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a64ef-155">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="a64ef-156">Een Service Fabric-cluster maken met behulp van de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a64ef-156">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="a64ef-157">Inzicht krijgen in het Service Fabric-toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="a64ef-157">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
