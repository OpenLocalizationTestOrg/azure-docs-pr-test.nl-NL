---
title: aaaSet van uw ontwikkelomgeving op Linux | Microsoft Docs
description: Hallo-runtime en -SDK installeren en maak een lokaal ontwikkelcluster op Linux. Na het voltooien van deze installatie, kunt u zich gereed toobuild toepassingen.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="c1254-104">Uw ontwikkelomgeving voorbereiden in Linux</span><span class="sxs-lookup"><span data-stu-id="c1254-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1254-105">Windows</span><span class="sxs-lookup"><span data-stu-id="c1254-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="c1254-106">Linux</span><span class="sxs-lookup"><span data-stu-id="c1254-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="c1254-107">OSX</span><span class="sxs-lookup"><span data-stu-id="c1254-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="c1254-108">toodeploy en voer [Azure Service Fabric-toepassingen](service-fabric-application-model.md) op uw ontwikkelcomputer Linux Hallo runtime en algemene SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="c1254-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="c1254-109">U kunt ook optionele SDK's voor Java en .NET Core installeren.</span><span class="sxs-lookup"><span data-stu-id="c1254-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1254-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c1254-110">Prerequisites</span></span>

<span data-ttu-id="c1254-111">Hallo volgende versies van besturingssystemen worden ondersteund voor ontwikkeling:</span><span class="sxs-lookup"><span data-stu-id="c1254-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="c1254-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="c1254-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="c1254-113">Uw APT-bronnen bijwerken</span><span class="sxs-lookup"><span data-stu-id="c1254-113">Update your APT sources</span></span>
<span data-ttu-id="c1254-114">tooinstall hello SDK en Hallo gekoppeld runtime-pakket via Hallo apt get-opdrachtregelprogramma, moet u eerst uw bronnen geavanceerde verpakking hulpprogramma (APT) bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c1254-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="c1254-115">Open een terminal.</span><span class="sxs-lookup"><span data-stu-id="c1254-115">Open a terminal.</span></span>
2. <span data-ttu-id="c1254-116">Hallo Service Fabric-repo-tooyour bronnen lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c1254-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="c1254-117">Hallo toevoegen `dotnet` opslagplaats tooyour lijst met bronnen.</span><span class="sxs-lookup"><span data-stu-id="c1254-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="c1254-118">Hallo toevoegen Privacy Guard (gnupg installeert of GPG) een nieuwe Gnu tooyour APT sleutelhanger sleutel.</span><span class="sxs-lookup"><span data-stu-id="c1254-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="c1254-119">Hallo officiële Docker GPG key tooyour APT sleutelhanger toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c1254-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="c1254-120">Hallo Docker-opslagplaats instellen.</span><span class="sxs-lookup"><span data-stu-id="c1254-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="c1254-121">Vernieuwen van het pakket op basis van het Hallo zojuist toegevoegd opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c1254-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="c1254-122">Installeren en instellen Hallo SDK voor de installatie van de lokale cluster</span><span class="sxs-lookup"><span data-stu-id="c1254-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="c1254-123">Nadat u uw gegevensbronnen hebt bijgewerkt, kunt u Hallo SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="c1254-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="c1254-124">Hallo Service Fabric SDK-pakket installeert, Hallo installatie bevestigen en ik ga hiermee akkoord toohello gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="c1254-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="c1254-125">Hallo automatiseren volgende opdrachten overnemende Hallo-licentie voor Service Fabric-pakketten:</span><span class="sxs-lookup"><span data-stu-id="c1254-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="c1254-126">Een lokaal cluster instellen</span><span class="sxs-lookup"><span data-stu-id="c1254-126">Set up a local cluster</span></span>
  <span data-ttu-id="c1254-127">Als het Hallo-installatie is voltooid, moet u kunnen toostart een lokaal cluster.</span><span class="sxs-lookup"><span data-stu-id="c1254-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="c1254-128">Hallo cluster setup-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c1254-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="c1254-129">Open een webbrowser en ga te[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="c1254-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="c1254-130">Als het Hallo-cluster is gestart, ziet u Hallo Service Fabric Explorer dashboard.</span><span class="sxs-lookup"><span data-stu-id="c1254-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer in Linux][sfx-linux]

  <span data-ttu-id="c1254-132">Op dit punt kunt u vooraf samengestelde Service Fabric-toepassingspakketten of nieuwe implementeren op basis van gastcontainers of uitvoerbare gastbestanden.</span><span class="sxs-lookup"><span data-stu-id="c1254-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="c1254-133">nieuwe services met behulp van Hallo Java of .NET Core SDK's, toobuild stappen Hallo optionele instellingen die beschikbaar zijn in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="c1254-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="c1254-134">Zelfstandige clusters worden niet ondersteund in Linux.</span><span class="sxs-lookup"><span data-stu-id="c1254-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="c1254-135">Hallo preview ondersteunt slechts één selectievakje en meerdere machines Azure Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="c1254-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="c1254-136">Hallo Service Fabric CLI instellen</span><span class="sxs-lookup"><span data-stu-id="c1254-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="c1254-137">Hallo [Service Fabric CLI](service-fabric-cli.md) bevat opdrachten voor interactie met Service Fabric-entiteiten, inclusief clusters en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c1254-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="c1254-138">Deze is gebaseerd op python, dus wees zeker toohave python en via pip geïnstalleerd voordat u verdergaat met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c1254-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="c1254-139">Installeren en instellen Hallo genereren voor containers en Gast-uitvoerbare bestanden</span><span class="sxs-lookup"><span data-stu-id="c1254-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="c1254-140">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="c1254-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="c1254-141">Volg de stappen Hallo hieronder tooensure die u Hallo Service Fabric yeoman sjabloon generator voor het werken op uw computer hebt.</span><span class="sxs-lookup"><span data-stu-id="c1254-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="c1254-142">nodejs en NPM installeren op uw computer</span><span class="sxs-lookup"><span data-stu-id="c1254-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="c1254-143">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="c1254-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="c1254-144">Hallo Service Fabric Yeo container generator en Gast execuatble generator installeren via NPM</span><span class="sxs-lookup"><span data-stu-id="c1254-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="c1254-145">Nadat u Hallo hierboven genereren hebt geïnstalleerd, moet u de apps kunnen toocreate met gastservices uitvoerbaar bestand of de container door te voeren `yo azuresfguest` of `yo azuresfcontainer` respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="c1254-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="c1254-146">Hallo nodig Java artefacten (optioneel, indien gewenst toouse Hallo Java modellen programming) installeren</span><span class="sxs-lookup"><span data-stu-id="c1254-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="c1254-147">toobuild Service Fabric-services met behulp van Java, zorg ervoor dat er JDK 1.8 geïnstalleerd samen met Gradle die wordt gebruikt voor het uitvoeren van build-taken.</span><span class="sxs-lookup"><span data-stu-id="c1254-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="c1254-148">Hallo volgende codefragment installeert Open JDK 1.8 samen met Gradle.</span><span class="sxs-lookup"><span data-stu-id="c1254-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="c1254-149">Hallo Service Fabric-Java-bibliotheken worden opgehaald uit Maven.</span><span class="sxs-lookup"><span data-stu-id="c1254-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="c1254-150">Hallo Eclipse Neon invoegtoepassing installeren (optioneel)</span><span class="sxs-lookup"><span data-stu-id="c1254-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="c1254-151">U kunt Hallo Eclipse-invoegtoepassing installeren voor Service Fabric uit binnen Hallo **Eclipse IDE voor Java-ontwikkelaars**.</span><span class="sxs-lookup"><span data-stu-id="c1254-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="c1254-152">U kunt Eclipse toocreate Service Fabric Gast uitvoerbare toepassingen en containertoepassingen in toevoeging tooService Fabric Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c1254-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="c1254-153">In Eclipse of de meest recente Eclipse Neon en meest recente versie van de Buildship Hallo (1.0.17 of nieuwer) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c1254-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="c1254-154">U kunt Hallo versies van geïnstalleerde onderdelen controleren door het selecteren van **Help** > **installatiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="c1254-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="c1254-155">U kunt Buildship bijwerken met behulp van instructies op Hallo [Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="c1254-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="c1254-156">tooinstall Hallo Service Fabric-invoegtoepassing, selecteer **Help** > **nieuwe Software installeren**.</span><span class="sxs-lookup"><span data-stu-id="c1254-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="c1254-157">In Hallo **werken met** in het vak **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="c1254-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="c1254-158">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c1254-158">Click **Add**.</span></span>

    ![Hallo beschikbare Software pagina][sf-eclipse-plugin]

5. <span data-ttu-id="c1254-160">Selecteer Hallo **ServiceFabric** invoegtoepassing, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c1254-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="c1254-161">Hallo installatiestappen voltooien en accepteer de gebruiksrechtovereenkomst Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1254-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="c1254-162">Als u al Hallo Service Fabric Eclipse-invoegtoepassing is geïnstalleerd, zorg ervoor dat hebt u Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="c1254-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="c1254-163">U kunt controleren door het selecteren van **Help** > **installatiegegevens** en vervolgens te zoeken naar Service Fabric in Hallo lijst met geïnstalleerde modules. Selecteer **Update** als er een nieuwere versie beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="c1254-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="c1254-164">Zie [Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen](service-fabric-get-started-eclipse.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1254-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="c1254-165">Hallo .NET Core SDK (optioneel, indien toouse Hallo .NET Core programmeermodellen gewenst) installeren</span><span class="sxs-lookup"><span data-stu-id="c1254-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="c1254-166">Hallo .NET Core SDK biedt Hallo-bibliotheken en sjablonen die vereist toobuild Service Fabric-services met .NET Core zijn.</span><span class="sxs-lookup"><span data-stu-id="c1254-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="c1254-167">Hallo .NET Core SDK-pakket aan de hand van de actieve Hallo - installeren</span><span class="sxs-lookup"><span data-stu-id="c1254-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="c1254-168">Update Hallo SDK en runtime</span><span class="sxs-lookup"><span data-stu-id="c1254-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="c1254-169">tooupdate toohello meest recente versie van Hallo SDK en runtime, Hallo volgende opdrachten uitvoeren (deselecteren Hallo-SDK's die u niet wilt):</span><span class="sxs-lookup"><span data-stu-id="c1254-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="c1254-170">tooupdate hello Java SDK binaire bestanden van Maven, moet u tooupdate Hallo versie details van de bijbehorende binaire Hallo in Hallo ``build.gradle`` toopoint toohello meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="c1254-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="c1254-171">tooknow exact hier moet u tooupdate Hallo versie, raadpleegt u tooany ``build.gradle`` bestand in de voorbeelden van Service Fabric aan de slag [hier](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c1254-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="c1254-172">Hello-pakketten bijwerken kan ertoe leiden dat uw lokale ontwikkeling cluster toostop uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1254-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="c1254-173">Start opnieuw op uw lokale cluster na een upgrade door Hallo instructies te volgen op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="c1254-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1254-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1254-174">Next steps</span></span>

* [<span data-ttu-id="c1254-175">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="c1254-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="c1254-176">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="c1254-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="c1254-177">Uw eerste CSharp-toepassing in Linux maken</span><span class="sxs-lookup"><span data-stu-id="c1254-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="c1254-178">Uw ontwikkelomgeving voorbereiden in OSX</span><span class="sxs-lookup"><span data-stu-id="c1254-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="c1254-179">Hallo Service Fabric CLI toomanage uw toepassingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="c1254-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="c1254-180">Verschillen tussen Service Fabric in Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="c1254-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="c1254-181">Aan de slag met Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="c1254-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
