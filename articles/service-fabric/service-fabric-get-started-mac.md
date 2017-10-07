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
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Uw ontwikkelomgeving instellen in Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

U kunt Service Fabric-toepassingen toorun opbouwen op Linux-clusters met Mac OS X. In dit artikel bevat informatie over hoe tooset van uw Mac voor ontwikkeling.

## <a name="prerequisites"></a>Vereisten
Service Fabric voert geen systeemeigen op OS X. toorun lokale Service Fabric-cluster, bieden we een vooraf geconfigureerde Ubuntu-virtuele machine met behulp van Vagrant en VirtualBox. Voordat u aan de slag gaat, hebt u het volgende nodig:

* [Vagrant (v1.8.4 of hoger)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> U moet toouse wederzijds ondersteunde versies van Vagrant en VirtualBox. Vagrant functioneert mogelijk niet goed in combinatie met een niet-ondersteunde versie van VirtualBox.
>

## <a name="create-hello-local-vm"></a>Maak Hallo lokale virtuele machine
toocreate Hallo lokale virtuele machine met een 5-knooppunt Service Fabric-cluster, voert u Hallo stappen te volgen:

1. Kloon Hallo `Vagrantfile` opslagplaats

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Deze stappen brengen keuzelijsten Hallo bestand `Vagrantfile` met Hallo VM configuratie samen met de Hallo locatie Hallo VM wordt gedownload van.

2. Navigeer toohello lokale kloon van de opslagplaats Hallo

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Optioneel) Hallo VM standaardinstellingen wijzigen

    Standaard is hello lokale virtuele machine geconfigureerd als volgt:

   * 3 GB toegewezen geheugen
   * Persoonlijke host netwerk geconfigureerd IP-192.168.50.50 passthrough van verkeer van Hallo Mac host inschakelen

     U kunt een van deze instellingen wijzigen of toevoegen van andere configuratie toohello VM in Hallo `Vagrantfile`. Zie Hallo [Vagrant documentatie](http://www.vagrantup.com/docs) voor Hallo volledige lijst met configuratieopties.
4. Hallo VM maken

    ```bash
    vagrant up
    ```

   Deze stap downloadt Hallo vooraf geconfigureerde VM-installatiekopie, het lokaal en stel vervolgens een lokale Service Fabric-cluster in het opstarten. U moet verwacht dat het tootake enkele minuten duren. Als setup voltooid is, ziet u een bericht in Hallo-uitvoer die aangeeft dat Hallo-cluster wordt gestart.

    ![Starten van clusterinstallatie na inrichting van VM][cluster-setup-script]

    >[!TIP]
    > Als Hallo VM downloaden lang duurt, kunt u downloaden met behulp van wget of curl of via een browser door te navigeren toohello koppeling opgegeven door **config.vm.box_url** in Hallo bestand `Vagrantfile`. Na het downloaden van het lokaal, bewerken `Vagrantfile` toopoint toohello lokaal pad waar u de installatiekopie van het Hallo hebt gedownload. Voor bijvoorbeeld als u Hallo installatiekopie too/home/users/test/azureservicefabric.tp8.box, gedownload vervolgens ingesteld **config.vm.box_url** toothat pad.
    >

5. Testen die Hallo cluster heeft correct zijn ingesteld door te navigeren tooService Fabric Explorer op http://192.168.50.50:19080/Explorer (ervan uitgaande dat u bewaard Hallo standaard particuliere netwerk-IP).

    ![Service Fabric Explorer weergegeven van de host Hallo Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Toepassingen maken op een Mac met Yeoman
Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator. Volg de stappen Hallo hieronder tooensure er Hallo Service Fabric yeoman sjabloon generator op uw computer werkt.

1. U moet toohave Node.js en geïnstalleerd op een mac u NPM. Als dat niet kunt u Node.js en NPM met gebruik van de volgende Hallo Homebrew installeren. toocheck hello versies van Node.js en geïnstalleerd op uw Mac NPM, kunt u Hallo ``-v`` optie.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. [Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM

  ```bash
  npm install -g yo
  ```
3. Hallo Yeoman installeren generator gewenste toouse, stappen te volgen Hallo in aan de slag Hallo [documentatie](service-fabric-get-started-linux.md). toocreate Service Fabric-toepassingen met behulp van Yeoman, stappen Hallo-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. een Service Fabric-Java-toepassing op Mac toobuild, moet u - JDK 1.8 en Gradle op Hallo machine geïnstalleerd.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Hallo Service Fabric-invoegtoepassing voor Eclipse Neon installeren

Service Fabric bevat een invoegtoepassing voor Hallo **Eclipse Neon voor IDE voor Java** die Hallo-proces voor het maken, bouwen en implementeren van Java-services kunt vereenvoudigen. U kunt stappen Hallo installatie vermeld in deze algemene [documentatie](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) over het installeren of bijwerken van Service Fabric Eclipse-invoegtoepassing.

>[!TIP]
> Standaard wordt Hallo default IP ondersteund zoals vermeld in Hallo ``Vagrantfile`` in Hallo ``Local.json`` van de toepassing hello gegenereerd. Werk Hallo bijbehorende IP-adres in als u deze instelling wijzigen en Vagrant met een ander IP-adres implementeert, ``Local.json`` van uw toepassing.

## <a name="next-steps"></a>Volgende stappen
<!-- Links -->
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse](service-fabric-get-started-eclipse.md)
* [Maken van een Service Fabric-cluster in hello Azure-portal](service-fabric-cluster-creation-via-portal.md)
* [Maken van een Service Fabric-cluster met behulp van hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Hallo Service Fabric-toepassingsmodel begrijpen](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
