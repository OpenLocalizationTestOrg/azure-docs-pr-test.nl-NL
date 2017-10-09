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
# <a name="prepare-your-development-environment-on-linux"></a>Uw ontwikkelomgeving voorbereiden in Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy en voer [Azure Service Fabric-toepassingen](service-fabric-application-model.md) op uw ontwikkelcomputer Linux Hallo runtime en algemene SDK installeren. U kunt ook optionele SDK's voor Java en .NET Core installeren.

## <a name="prerequisites"></a>Vereisten

Hallo volgende versies van besturingssystemen worden ondersteund voor ontwikkeling:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Uw APT-bronnen bijwerken
tooinstall hello SDK en Hallo gekoppeld runtime-pakket via Hallo apt get-opdrachtregelprogramma, moet u eerst uw bronnen geavanceerde verpakking hulpprogramma (APT) bijwerken.

1. Open een terminal.
2. Hallo Service Fabric-repo-tooyour bronnen lijst toevoegen.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Hallo toevoegen `dotnet` opslagplaats tooyour lijst met bronnen.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Hallo toevoegen Privacy Guard (gnupg installeert of GPG) een nieuwe Gnu tooyour APT sleutelhanger sleutel.

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Hallo officiële Docker GPG key tooyour APT sleutelhanger toevoegen.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Hallo Docker-opslagplaats instellen.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Vernieuwen van het pakket op basis van het Hallo zojuist toegevoegd opslagplaatsen.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Installeren en instellen Hallo SDK voor de installatie van de lokale cluster

Nadat u uw gegevensbronnen hebt bijgewerkt, kunt u Hallo SDK installeren. Hallo Service Fabric SDK-pakket installeert, Hallo installatie bevestigen en ik ga hiermee akkoord toohello gebruiksrechtovereenkomst.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Hallo automatiseren volgende opdrachten overnemende Hallo-licentie voor Service Fabric-pakketten:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Een lokaal cluster instellen
  Als het Hallo-installatie is voltooid, moet u kunnen toostart een lokaal cluster.

  1. Hallo cluster setup-script uitvoeren.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Open een webbrowser en ga te[Service Fabric Explorer](http://localhost:19080/Explorer). Als het Hallo-cluster is gestart, ziet u Hallo Service Fabric Explorer dashboard.

      ![Service Fabric Explorer in Linux][sfx-linux]

  Op dit punt kunt u vooraf samengestelde Service Fabric-toepassingspakketten of nieuwe implementeren op basis van gastcontainers of uitvoerbare gastbestanden. nieuwe services met behulp van Hallo Java of .NET Core SDK's, toobuild stappen Hallo optionele instellingen die beschikbaar zijn in de volgende secties.


  > [!NOTE]
  > Zelfstandige clusters worden niet ondersteund in Linux. Hallo preview ondersteunt slechts één selectievakje en meerdere machines Azure Linux-clusters.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Hallo Service Fabric CLI instellen

Hallo [Service Fabric CLI](service-fabric-cli.md) bevat opdrachten voor interactie met Service Fabric-entiteiten, inclusief clusters en toepassingen. Deze is gebaseerd op python, dus wees zeker toohave python en via pip geïnstalleerd voordat u verdergaat met de volgende opdracht Hallo:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Installeren en instellen Hallo genereren voor containers en Gast-uitvoerbare bestanden
Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator. Volg de stappen Hallo hieronder tooensure die u Hallo Service Fabric yeoman sjabloon generator voor het werken op uw computer hebt.

1. nodejs en NPM installeren op uw computer

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. [Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM

  ```bash
  sudo npm install -g yo
  ```
3. Hallo Service Fabric Yeo container generator en Gast execuatble generator installeren via NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Nadat u Hallo hierboven genereren hebt geïnstalleerd, moet u de apps kunnen toocreate met gastservices uitvoerbaar bestand of de container door te voeren `yo azuresfguest` of `yo azuresfcontainer` respectievelijk.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Hallo nodig Java artefacten (optioneel, indien gewenst toouse Hallo Java modellen programming) installeren

toobuild Service Fabric-services met behulp van Java, zorg ervoor dat er JDK 1.8 geïnstalleerd samen met Gradle die wordt gebruikt voor het uitvoeren van build-taken. Hallo volgende codefragment installeert Open JDK 1.8 samen met Gradle. Hallo Service Fabric-Java-bibliotheken worden opgehaald uit Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Hallo Eclipse Neon invoegtoepassing installeren (optioneel)

U kunt Hallo Eclipse-invoegtoepassing installeren voor Service Fabric uit binnen Hallo **Eclipse IDE voor Java-ontwikkelaars**. U kunt Eclipse toocreate Service Fabric Gast uitvoerbare toepassingen en containertoepassingen in toevoeging tooService Fabric Java-toepassingen.

1. In Eclipse of de meest recente Eclipse Neon en meest recente versie van de Buildship Hallo (1.0.17 of nieuwer) geïnstalleerd. U kunt Hallo versies van geïnstalleerde onderdelen controleren door het selecteren van **Help** > **installatiegegevens**. U kunt Buildship bijwerken met behulp van instructies op Hallo [Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle][buildship-update].

2. tooinstall Hallo Service Fabric-invoegtoepassing, selecteer **Help** > **nieuwe Software installeren**.

3. In Hallo **werken met** in het vak **http://dl.microsoft.com/eclipse**.

4. Klik op **Add**.

    ![Hallo beschikbare Software pagina][sf-eclipse-plugin]

5. Selecteer Hallo **ServiceFabric** invoegtoepassing, en klik vervolgens op **volgende**.

6. Hallo installatiestappen voltooien en accepteer de gebruiksrechtovereenkomst Hallo.

Als u al Hallo Service Fabric Eclipse-invoegtoepassing is geïnstalleerd, zorg ervoor dat hebt u Hallo meest recente versie. U kunt controleren door het selecteren van **Help** > **installatiegegevens** en vervolgens te zoeken naar Service Fabric in Hallo lijst met geïnstalleerde modules. Selecteer **Update** als er een nieuwere versie beschikbaar is.

Zie [Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen](service-fabric-get-started-eclipse.md) voor meer informatie.


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Hallo .NET Core SDK (optioneel, indien toouse Hallo .NET Core programmeermodellen gewenst) installeren
Hallo .NET Core SDK biedt Hallo-bibliotheken en sjablonen die vereist toobuild Service Fabric-services met .NET Core zijn. Hallo .NET Core SDK-pakket aan de hand van de actieve Hallo - installeren

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Update Hallo SDK en runtime

tooupdate toohello meest recente versie van Hallo SDK en runtime, Hallo volgende opdrachten uitvoeren (deselecteren Hallo-SDK's die u niet wilt):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate hello Java SDK binaire bestanden van Maven, moet u tooupdate Hallo versie details van de bijbehorende binaire Hallo in Hallo ``build.gradle`` toopoint toohello meest recente versie. tooknow exact hier moet u tooupdate Hallo versie, raadpleegt u tooany ``build.gradle`` bestand in de voorbeelden van Service Fabric aan de slag [hier](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Hello-pakketten bijwerken kan ertoe leiden dat uw lokale ontwikkeling cluster toostop uitgevoerd. Start opnieuw op uw lokale cluster na een upgrade door Hallo instructies te volgen op deze pagina.

## <a name="next-steps"></a>Volgende stappen

* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse](service-fabric-get-started-eclipse.md)
* [Uw eerste CSharp-toepassing in Linux maken](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Uw ontwikkelomgeving voorbereiden in OSX](service-fabric-get-started-mac.md)
* [Hallo Service Fabric CLI toomanage uw toepassingen gebruiken](service-fabric-application-lifecycle-sfctl.md)
* [Verschillen tussen Service Fabric in Windows en Linux](service-fabric-linux-windows-differences.md)
* [Aan de slag met Service Fabric-CLI](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
