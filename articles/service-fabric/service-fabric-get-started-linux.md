---
title: Uw ontwikkelomgeving instellen in Linux | Microsoft Docs
description: Installeer de runtime en SDK en maak een lokaal ontwikkelcluster in Linux. Zodra u dit hebt gedaan, kunt u toepassingen bouwen.
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
ms.openlocfilehash: 58c6bbbb16d7008e6b573cf8dbc8cf62da9789f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="ac4df-104">Uw ontwikkelomgeving voorbereiden in Linux</span><span class="sxs-lookup"><span data-stu-id="ac4df-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac4df-105">Windows</span><span class="sxs-lookup"><span data-stu-id="ac4df-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="ac4df-106">Linux</span><span class="sxs-lookup"><span data-stu-id="ac4df-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="ac4df-107">OSX</span><span class="sxs-lookup"><span data-stu-id="ac4df-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="ac4df-108">Als u [Azure Service Fabric-toepassingen](service-fabric-application-model.md) op uw Linux-ontwikkelmachine wilt implementeren en uitvoeren, moet u de runtime en algemene SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="ac4df-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="ac4df-109">U kunt ook optionele SDK's voor Java en .NET Core installeren.</span><span class="sxs-lookup"><span data-stu-id="ac4df-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac4df-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac4df-110">Prerequisites</span></span>

<span data-ttu-id="ac4df-111">De volgende versies van besturingssystemen worden ondersteund voor de ontwikkeling:</span><span class="sxs-lookup"><span data-stu-id="ac4df-111">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="ac4df-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="ac4df-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="ac4df-113">Uw APT-bronnen bijwerken</span><span class="sxs-lookup"><span data-stu-id="ac4df-113">Update your APT sources</span></span>
<span data-ttu-id="ac4df-114">Voor het installeren van de SDK en het bijbehorende runtimepakket via het apt-get-opdrachtregelprogramma, moet u eerst uw APT-bronnen (Advanced Packaging Tool) bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ac4df-114">To install the SDK and the associated runtime package via the apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="ac4df-115">Open een terminal.</span><span class="sxs-lookup"><span data-stu-id="ac4df-115">Open a terminal.</span></span>
2. <span data-ttu-id="ac4df-116">Voeg de Service Fabric-opslagplaats toe aan uw lijst met bronnen.</span><span class="sxs-lookup"><span data-stu-id="ac4df-116">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="ac4df-117">Voeg de `dotnet`-opslagplaats toe aan uw lijst met bronnen.</span><span class="sxs-lookup"><span data-stu-id="ac4df-117">Add the `dotnet` repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="ac4df-118">Voeg de nieuwe Gnu Privacy Guard-code (GnuPG of GPG) toe aan uw APT-sleutelring.</span><span class="sxs-lookup"><span data-stu-id="ac4df-118">Add the new Gnu Privacy Guard (GnuPG, or GPG) key to your APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="ac4df-119">Voeg de officiële GPG-sleutel van Docker toe aan uw APT-sleutelring.</span><span class="sxs-lookup"><span data-stu-id="ac4df-119">Add the official Docker GPG key to your APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="ac4df-120">Stel de Docker-opslagplaats in.</span><span class="sxs-lookup"><span data-stu-id="ac4df-120">Set up the Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="ac4df-121">Vernieuw uw pakketlijsten op basis van de net toegevoegde opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="ac4df-121">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-the-sdk-for-local-cluster-setup"></a><span data-ttu-id="ac4df-122">De SDK installeren en instellen voor gebruik van een lokaal cluster</span><span class="sxs-lookup"><span data-stu-id="ac4df-122">Install and set up the SDK for local cluster setup</span></span>

<span data-ttu-id="ac4df-123">Wanneer u uw bronnen hebt bijgewerkt, kunt u de SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="ac4df-123">After you have updated your sources, you can install the SDK.</span></span> <span data-ttu-id="ac4df-124">Installeer het Service Fabric SDK-pakket, bevestig de installatie en ga akkoord met de gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="ac4df-124">Install the Service Fabric SDK package, confirm the installation, and agree to the license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="ac4df-125">Met de volgende opdrachten kunt u het accepteren van de licentie voor Service Fabric-pakketten automatiseren:</span><span class="sxs-lookup"><span data-stu-id="ac4df-125">The following commands automate accepting the license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="ac4df-126">Een lokaal cluster instellen</span><span class="sxs-lookup"><span data-stu-id="ac4df-126">Set up a local cluster</span></span>
  <span data-ttu-id="ac4df-127">Als de installatie is voltooid, moet u een lokaal cluster kunnen starten.</span><span class="sxs-lookup"><span data-stu-id="ac4df-127">If the installation is successful, you should be able to start a local cluster.</span></span>

  1. <span data-ttu-id="ac4df-128">Voer het installatiescript van het cluster uit.</span><span class="sxs-lookup"><span data-stu-id="ac4df-128">Run the cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="ac4df-129">Open een webbrowser en ga naar [Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="ac4df-129">Open a web browser and go to [Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="ac4df-130">Als het cluster is gestart, ziet u het Service Fabric Explorer-dashboard.</span><span class="sxs-lookup"><span data-stu-id="ac4df-130">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer in Linux][sfx-linux]

  <span data-ttu-id="ac4df-132">Op dit punt kunt u vooraf samengestelde Service Fabric-toepassingspakketten of nieuwe implementeren op basis van gastcontainers of uitvoerbare gastbestanden.</span><span class="sxs-lookup"><span data-stu-id="ac4df-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="ac4df-133">Als u nieuwe services wilt maken met behulp van de Java of .NET Core SDK's, voert u de optionele installatiestappen uit die in de volgende secties worden uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="ac4df-133">To build new services by using the Java or .NET Core SDKs, follow the optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="ac4df-134">Zelfstandige clusters worden niet ondersteund in Linux.</span><span class="sxs-lookup"><span data-stu-id="ac4df-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="ac4df-135">De preview ondersteunt slechts één selectievakje en meerdere Azure Linux-machineclusters.</span><span class="sxs-lookup"><span data-stu-id="ac4df-135">The preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-the-service-fabric-cli"></a><span data-ttu-id="ac4df-136">De Service Fabric-CLI instellen</span><span class="sxs-lookup"><span data-stu-id="ac4df-136">Set up the Service Fabric CLI</span></span>

<span data-ttu-id="ac4df-137">De [Service Fabric-CLI](service-fabric-cli.md) bevat opdrachten voor interactie met Service Fabric-entiteiten, inclusief clusters en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ac4df-137">The [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="ac4df-138">De CLI is gebaseerd op python, dus is het belangrijk dat python en pip zijn geïnstalleerd voordat u verdergaat met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ac4df-138">It is based on python, so be sure to have python and pip installed before you proceed with the following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-the-generators-for-containers-and-guest-executables"></a><span data-ttu-id="ac4df-139">De generatoren voor containers en uitvoerbare gastbestanden installeren en instellen</span><span class="sxs-lookup"><span data-stu-id="ac4df-139">Install and set up the generators for containers and guest-executables</span></span>
<span data-ttu-id="ac4df-140">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="ac4df-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="ac4df-141">Volg de stappen hieronder om te controleren of de Yeoman-sjabloongenerator van Service Fabric werkt op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ac4df-141">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="ac4df-142">nodejs en NPM installeren op uw computer</span><span class="sxs-lookup"><span data-stu-id="ac4df-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="ac4df-143">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="ac4df-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="ac4df-144">Yeo-containergenerator voor Service Fabric en de generator voor uitvoerbare gastbestanden installeren vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="ac4df-144">Install the Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="ac4df-145">Nadat u de bovenstaande generatoren hebt geïnstalleerd, moet u apps kunnen maken met uitvoerbare gastbestanden of containerservices door respectievelijk `yo azuresfguest` of `yo azuresfcontainer` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ac4df-145">After you have installed the above generators, you should be able to create apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-the-necessary-java-artifacts-optional-if-you-want-to-use-the-java-programming-models"></a><span data-ttu-id="ac4df-146">De benodigde Java-artefacten installeren (alleen als u de Java-programmeermodellen wilt gebruiken)</span><span class="sxs-lookup"><span data-stu-id="ac4df-146">Install the necessary Java artifacts (optional, if you want to use the Java programming models)</span></span>

<span data-ttu-id="ac4df-147">Als u Service Fabric-services wilt bouwen met behulp van Java, moet JDK 1.8 zijn samen zijn geïnstalleerd met Gradle, dat wordt gebruikt voor het uitvoeren van build-taken.</span><span class="sxs-lookup"><span data-stu-id="ac4df-147">To build Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="ac4df-148">Met het volgende fragment wordt Open JDK 1.8 samen geïnstalleerd met Gradle.</span><span class="sxs-lookup"><span data-stu-id="ac4df-148">The following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="ac4df-149">De Service Fabric-Java-bibliotheken worden opgehaald uit Maven.</span><span class="sxs-lookup"><span data-stu-id="ac4df-149">The Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-the-eclipse-neon-plug-in-optional"></a><span data-ttu-id="ac4df-150">De Eclipse Neon-invoegtoepassing installeren (optioneel)</span><span class="sxs-lookup"><span data-stu-id="ac4df-150">Install the Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="ac4df-151">U kunt de Eclipse-invoegtoepassing voor Service Fabric installeren vanuit de **Eclipse IDE voor Java-ontwikkelaars**.</span><span class="sxs-lookup"><span data-stu-id="ac4df-151">You can install the Eclipse plug-in for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="ac4df-152">Met Eclipse kunt u behalve Service Fabric Java-toepassingen ook uitvoerbare Fabric Service-gasttoepassingen en containertoepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="ac4df-152">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

1. <span data-ttu-id="ac4df-153">Zorg er in Eclipse voor dat u de meest recente Eclipse Neon en de meest recente Buildship-versie (1.0.17 of hoger) hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ac4df-153">In Eclipse, ensure that you have latest Eclipse Neon and the latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="ac4df-154">U kunt de versies van geïnstalleerde onderdelen controleren door **Help** > **Installation Details** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ac4df-154">You can check the versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="ac4df-155">U kunt Buildship bijwerken met behulp van de instructies in [Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="ac4df-155">You can update Buildship by using the instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="ac4df-156">Als u de Service Fabric-invoegtoepassing wilt installeren, selecteert u **Help** > **Install New Software**.</span><span class="sxs-lookup"><span data-stu-id="ac4df-156">To install the Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="ac4df-157">Geef in het vak **Work with** **http://dl.microsoft.com/eclipse** op.</span><span class="sxs-lookup"><span data-stu-id="ac4df-157">In the **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="ac4df-158">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ac4df-158">Click **Add**.</span></span>

    ![De pagina met beschikbare software][sf-eclipse-plugin]

5. <span data-ttu-id="ac4df-160">Selecteer de **Fabric Service**-invoegtoepassing en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="ac4df-160">Select the **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="ac4df-161">Voer de installatiestappen uit en accepteer de gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="ac4df-161">Complete the installation steps, and then accept the end-user license agreement.</span></span>

<span data-ttu-id="ac4df-162">Als u de Eclipse-invoegtoepassing voor Service Fabric al hebt geïnstalleerd, controleert u of u de meest recente versie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ac4df-162">If you already have the Service Fabric Eclipse plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="ac4df-163">U kunt dit controleren door **Help** > **Installation Details** te selecteren en in de lijst met geïnstalleerde invoegtoepassingen naar Service Fabric te zoeken. Selecteer **Update** als er een nieuwere versie beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="ac4df-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in the list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="ac4df-164">Zie [Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen](service-fabric-get-started-eclipse.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac4df-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-want-to-use-the-net-core-programming-models"></a><span data-ttu-id="ac4df-165">De .NET Core-SDK installeren (alleen als u de .NET Core-programmeermodellen wilt gebruiken)</span><span class="sxs-lookup"><span data-stu-id="ac4df-165">Install the .NET Core SDK (optional, if you want to use the .NET Core programming models)</span></span>
<span data-ttu-id="ac4df-166">De .NET Core-SDK bevat de bibliotheken en sjablonen die vereist zijn voor het maken van Service Fabric-services met .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ac4df-166">The .NET Core SDK provides the libraries and templates that are required to build Service Fabric services with .NET Core.</span></span> <span data-ttu-id="ac4df-167">Installeer het .NET Core SDK-pakket door het volgende uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="ac4df-167">Install the .NET Core SDK package by running the following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-the-sdk-and-runtime"></a><span data-ttu-id="ac4df-168">De SDK en runtime bijwerken</span><span class="sxs-lookup"><span data-stu-id="ac4df-168">Update the SDK and runtime</span></span>

<span data-ttu-id="ac4df-169">Als u wilt bijwerken naar de nieuwste versie van de SDK en runtime, voert u de volgende opdrachten uit (hef de selectie op van ongewenste SDK's):</span><span class="sxs-lookup"><span data-stu-id="ac4df-169">To update to the latest version of the SDK and runtime, run the following commands (deselect the SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="ac4df-170">Als u de binaire bestanden uit de Java SDK wilt bijwerken vanaf Maven, moet u de versiegegevens van het bijbehorende binaire bestand in het bestand ``build.gradle`` aanpassen, zodat deze verwijzen naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="ac4df-170">To update the Java SDK binaries from Maven, you need to update the version details of the corresponding binary in the ``build.gradle`` file to point to the latest version.</span></span> <span data-ttu-id="ac4df-171">Als u precies wilt weten waar u de versie moet bijwerken, kunt u kijken naar een bestand ``build.gradle`` in de [voorbeelden](https://github.com/Azure-Samples/service-fabric-java-getting-started) om snel aan de slag te gaan met Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ac4df-171">To know exactly where you need to update the version, you can refer to any ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="ac4df-172">Als de pakketten worden bijgewerkt, kan dit ertoe leiden dat uw lokale ontwikkelcluster wordt stopgezet.</span><span class="sxs-lookup"><span data-stu-id="ac4df-172">Updating the packages might cause your local development cluster to stop running.</span></span> <span data-ttu-id="ac4df-173">Start uw lokale cluster opnieuw op na een upgrade door de instructies op deze pagina te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac4df-173">Restart your local cluster after an upgrade by following the instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac4df-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac4df-174">Next steps</span></span>

* [<span data-ttu-id="ac4df-175">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="ac4df-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="ac4df-176">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="ac4df-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ac4df-177">Uw eerste CSharp-toepassing in Linux maken</span><span class="sxs-lookup"><span data-stu-id="ac4df-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="ac4df-178">Uw ontwikkelomgeving voorbereiden in OSX</span><span class="sxs-lookup"><span data-stu-id="ac4df-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="ac4df-179">De Service Fabric-CLI gebruiken voor het beheren van uw toepassingen</span><span class="sxs-lookup"><span data-stu-id="ac4df-179">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="ac4df-180">Verschillen tussen Service Fabric in Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="ac4df-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="ac4df-181">Aan de slag met Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="ac4df-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
