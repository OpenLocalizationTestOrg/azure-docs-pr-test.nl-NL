---
title: aaaContinuous bouwen en de integratie voor uw Azure Service Fabric Linux Java-toepassing met behulp van Jenkins | Microsoft Docs
description: Doorlopend bouwen en integreren voor uw Linux Java-toepassing met behulp van Jenkins
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Jenkins toobuild te gebruiken en uw Linux-Java-toepassing implementeren
Jenkins is een populair hulpprogramma voor doorlopende integratie en implementatie van uw apps. Hier ziet u hoe toobuild en uw Azure Service Fabric-toepassing implementeren met behulp van Jenkins.

## <a name="general-prerequisites"></a>Algemene vereisten
- Zorg ervoor dat Git lokaal is geïnstalleerd. U kunt installeren Hallo juiste Git-versie van [Hallo Git pagina met downloads](https://git-scm.com/downloads), op basis van uw besturingssysteem. Als u nieuwe tooGit, meer informatie over deze van Hallo [Git documentatie](https://git-scm.com/docs).
- Hallo Service Fabric Jenkins invoegtoepassing hebt bij de hand hebt. U kunt deze ook downloaden via [Service Fabric-downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Jenkins instellen in een Service Fabric-cluster

U kunt Jenkins instellen binnen of buiten een Service Fabric-cluster. Hallo volgende secties tonen hoe tooset het in een cluster tijdens het gebruik van een Azure-opslag administratief toosave Hallo status van de instantie van de container Hallo.

### <a name="prerequisites"></a>Vereisten
1. Zorg ervoor dat u beschikt over een Service Fabric-cluster voor Linux. Een Service Fabric-cluster gemaakt op basis van hello Azure-portal al heeft Docker geïnstalleerd. Als u Hallo cluster lokaal uitvoert, controleert u of Docker is geïnstalleerd met behulp van de opdracht Hallo ``docker info``. Als dit niet is geïnstalleerd, deze dienovereenkomstig met behulp van installeren Hallo volgende opdrachten:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Hebben Hallo Service Fabric-containertoepassing geïmplementeerd op het Hallo-cluster, met behulp van Hallo stappen te volgen:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. U moet Hallo verbinding maken met de details van de optie Hallo Azure storage-bestandsshare, waar u toopersist Hallo status van Hallo Jenkins container exemplaar. Als u Microsoft Azure-portal Hallo voor Hallo dezelfde zijn, geef Hallo stappen - spreek een Azure storage-account maken ``sfjenkinsstorage1``. Maak een **bestandsshare** onder dat opslagaccount spreken ``sfjenkins``. Klik op **Connect** voor Hallo-bestandsshare en de opmerking Hallo waarden wordt weergegeven onder **verbinding te maken van Linux**, spreek dit eruit zou als volgt -
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Hallo tijdelijke aanduiding voor waarden in Hallo bijwerken ```setupentrypoint.sh``` script met de bijbehorende details van de azure-opslag.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Vervang ``[REMOTE_FILE_SHARE_LOCATION]`` met Hallo waarde ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` verbinding van de uitvoer Hallo Hallo in punt 3.
Vervang ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` met Hallo waarde ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` vanaf punt 3 hierboven.

5. Verbinding maken met toohello cluster en installeer Hallo containertoepassing.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Dit wordt een container Jenkins op Hallo-cluster geïnstalleerd en kan worden bewaakt met behulp van Hallo Service Fabric Explorer.

### <a name="steps"></a>Stappen
1. Vanuit de browser, ga te``http://PublicIPorFQDN:8081``. Het biedt pad van Hallo initiële admin wachtwoord vereist toosign in Hallo. U kunt toouse Jenkins blijven als een gebruiker met beheerdersrechten. Of u kunt maken en Hallo-gebruiker niet wijzigen nadat u zich met initiële Hallo-beheerdersaccount aanmeldt.

   > [!NOTE]
   > Zorg ervoor dat Hallo 8081 poort is opgegeven als eindpuntpoort Hallo-toepassing tijdens het Hallo-cluster maken.
   >

2. Hallo container exemplaar-ID ophalen met behulp van ``docker ps -a``.
3. Secure Shell (SSH) aanmelden toohello container en plak Hallo pad die hebt u geleerd op Hallo Jenkins portal. Bijvoorbeeld, als in de portal Hallo geeft het Hallo pad `PATH_TO_INITIAL_ADMIN_PASSWORD`, voert u de volgende Hallo:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Instellen van GitHub toowork met Jenkins, met behulp van Hallo stappen vermeld in [genereren van een nieuwe SSH-sleutel en deze toe te voegen toohello SSH-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Gebruik Hallo instructies van GitHub toogenerate Hallo SSH-sleutel en tooadd Hallo SSH sleutel toohello GitHub-account dat als host voor uw opslagplaats fungeert.
    * Voer Hallo-opdrachten in Hallo voorgaande link in Hallo Jenkins Docker-shell (en niet op uw host) genoemd.
    * toosign in toohello Jenkins shell vanaf de host, gebruik Hallo volgende opdracht:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Jenkins instellen buiten een Service Fabric-cluster

U kunt Jenkins instellen binnen of buiten een Service Fabric-cluster. Hallo van de volgende secties tonen hoe tooset het buiten een cluster.

### <a name="prerequisites"></a>Vereisten
U moet toohave Docker geïnstalleerd. Hallo opdrachten na kan gebruikte tooinstall Docker van Hallo terminal zijn:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Nu bij het uitvoeren van ``docker info`` in terminal hello, ziet u in de uitvoer van de Hallo die Hallo Docker-service wordt uitgevoerd.

### <a name="steps"></a>Stappen
  1. Pull-hallo Service Fabric Jenkins container installatiekopie:``docker pull raunakpandya/jenkins:v1``
  2. Hallo container installatiekopie uitvoert:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Hallo-ID van Hallo container installatiekopie exemplaar verkrijgen. U kunt alle Hallo Docker-containers met Hallo opdracht weergeven``docker ps –a``
  4. Meld u aan toohello Jenkins portal met behulp van Hallo stappen te volgen:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Als de container-id 2d24a73b5964 is, gebruikt u 2d24.
    * Dit wachtwoord is vereist voor toohello Jenkins dashboard vanuit de portal die is aangemeld``http://<HOST-IP>:8080``
    * Nadat u zich aanmeldt voor Hallo eerst, u kunt uw eigen gebruikersaccount maken en die worden gebruikt voor toekomstige doeleinden of toouse Hallo administrator-account kan worden voortgezet. Nadat u een gebruiker maken, moet u toocontinue met die.
  5. Instellen van GitHub toowork met Jenkins, met behulp van Hallo stappen vermeld in [genereren van een nieuwe SSH-sleutel en deze toe te voegen toohello SSH-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Hallo instructies van GitHub toogenerate Hallo SSH-sleutel en tooadd Hallo SSH sleutel toohello GitHub-account dat als host voor de opslagplaats hello fungeert gebruiken.
        * Voer Hallo-opdrachten in Hallo voorgaande link in Hallo Jenkins Docker-shell (en niet op uw host) genoemd.
      * toosign in toohello Jenkins shell vanaf de host, gebruik Hallo volgende opdrachten:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Zorg ervoor dat Hallo cluster of de machine waar Hallo Jenkins container installatiekopie wordt gehost een openbare IP-adres heeft. Hierdoor Hallo Jenkins exemplaar tooreceive meldingen vanuit GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Hallo Service Fabric Jenkins invoegtoepassing vanuit Hallo-portal installeren

1. Te gaan``http://PublicIPorFQDN:8081``
2. Hallo Jenkins dashboard, selecteer **beheren Jenkins** > **invoegtoepassingen beheren** > **Geavanceerd**.
Hier kunt u een invoegtoepassing uploaden. Selecteer **bestand kiezen**, en selecteer vervolgens Hallo **serviceFabric.hpi** bestand, dat u hebt gedownload onder vereisten. Wanneer u selecteert **uploaden**, Jenkins automatisch Hallo invoegtoepassing geïnstalleerd. Sta opnieuw starten toe als hierom wordt gevraagd.

## <a name="create-and-configure-a-jenkins-job"></a>Een Jenkins-taak maken en configureren

1. Maak een **nieuw item** vanaf het dashboard.
2. Voer een itemnaam in (bijvoorbeeld **MyJob**). Selecteer **free-style project** en klik op **OK**.
3. Hallo taak pagina gaan en op **configureren**.

   a. In het algemene gedeelte hello, onder **GitHub project**, geef de URL van de GitHub-project. Deze URL-hosts Hallo Service Fabric Java-toepassing die u wilt dat toointegrate Hello Jenkins continue integratie, continue implementatie (CI/CD) stromen (bijvoorbeeld ``https://github.com/sayantancs/SFJenkins``).

   b. Onder Hallo **Source Code Management** sectie **Git**. Hallo-opslagplaats URL opgeven die als host fungeert voor Hallo Service Fabric-Java-toepassing die u wilt dat toointegrate Hello Jenkins CI/CD-stroom (bijvoorbeeld ``https://github.com/sayantancs/SFJenkins.git``). Bovendien kunt u hier welke toobuild vertakking (bijvoorbeeld **/model**).
4. Configureer uw *GitHub* (die fungeert als host Hallo opslagplaats) zodat deze kunnen tootalk tooJenkins. Gebruik Hallo stappen te volgen:

   a. Tooyour GitHub-opslagplaats pagina gaan. Ga te**instellingen** > **integraties en Services**.

   b. Selecteer **Service toevoegen**, type **Jenkins**, en selecteer Hallo **Jenkins GitHub-invoegtoepassing**.

   c. Geef de Jenkins-webhook-URL op (standaard is dit ``http://<PublicIPorFQDN>:8081/github-webhook/``). Klik op **add/update service**.

   d. Een testgebeurtenis verzonden tooyour Jenkins exemplaar. U ziet een groen vinkje door Hallo webhook in GitHub en uw project bouwt.

   e. Onder Hallo **bouwen Triggers** sectie, selecteert u die optie die u wilt maken. Bijvoorbeeld wilt u tootrigger een build zien wanneer de opslagplaats van sommige push toohello gebeurt. Selecteer daarom de optie **GitHub hook trigger for GITScm polling**. (Voorheen deze optie is aangeroepen **bouwen wanneer een wijziging wordt doorgeschoven, tooGitHub**.)

   f. Onder Hallo **bouwen sectie**, in de vervolgkeuzelijst Hallo **toevoegen build stap**, Hallo optie **aanroepen Gradle Script**. Geef in het Hallo-object dat wordt geleverd, Hallo pad te**hoofdmap build script** voor uw toepassing. Deze build.gradle van Hallo-pad opgegeven opneemt en dienovereenkomstig werkt. Als u een project met de naam maakt ``MyActor`` (met Hallo Eclipse invoegtoepassing of Yeoman generator), Hallo hoofdmap build script moet bevatten ``${WORKSPACE}/MyActor``. Zie de volgende schermafdruk voor een voorbeeld van hoe dit eruitziet Hallo:

    ![Service Fabric-bouwactie voor Jenkins][build-step]

   g. Van Hallo **na Build acties** vervolgkeuzelijst, selecteer **Service Fabric-Project implementeert**. U moet hier tooprovide cluster details waar hello Jenkins gecompileerd Service Fabric-toepassing wordt geïmplementeerd. U kunt ook een extra Toepassingdetails gebruikt toodeploy Hallo toepassing opgeven. Zie de volgende schermafdruk voor een voorbeeld van hoe dit eruitziet Hallo:

    ![Service Fabric-bouwactie voor Jenkins][post-build-step]

   > [!NOTE]
   > Hier Hallo-cluster kan niet hetzelfde zijn als Hallo één hosting Hallo Jenkins containertoepassing, als u van Service Fabric toodeploy hello Jenkins container installatiekopie gebruikmaakt.
   >

## <a name="next-steps"></a>Volgende stappen
GitHub en Jenkins zijn nu geconfigureerd. Overweeg aantal voorbeelden wijzigen uw ``MyActor`` project in Hallo opslagplaats bijvoorbeeld https://github.com/sayantancs/SFJenkins. Uw wijzigingen tooa externe push ``master`` vertakking (of een tak die u hebt geconfigureerd toowork met). Dit activeert Hallo Jenkins taak, ``MyJob``, die u hebt geconfigureerd. Het Hallo wijzigingen haalt vanuit GitHub, ze maakt en implementeert Hallo toepassing toohello clustereindpunt die u hebt opgegeven in de acties na het samenstellen.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
