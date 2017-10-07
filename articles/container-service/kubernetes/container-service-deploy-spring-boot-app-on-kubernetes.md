---
title: een App Spring opstarten op Kubernetes in Azure Container Service aaaDeploy | Microsoft Docs
description: Deze zelfstudie leert u echter Hallo stappen toodeploy een versie die voorjaar Boot-toepassing in een cluster Kubernetes op Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren

Hallo  **[Spring Framework]**  is een populaire open-source framework waarmee ontwikkelaars van Java web, mobiel en API-toepassingen maken. In deze zelfstudie wordt een voorbeeld-app gemaakt met behulp van [Spring Boot], een conventie voor gestuurde benadering voor het gebruik van Spring tooget snel aan de slag.

**[Kubernetes]**  en  **[Docker]**  zijn open source-oplossingen die ontwikkelaars helpen bij automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in de containers.

Deze zelfstudie helpt u al deze twee populaire open-source technologieën toodevelop combineren en implementeren van een versie die voorjaar opstarten toepassing tooMicrosoft Azure. Meer specifiek, gebruikt u  *[Spring Boot]*  voor toepassingsontwikkeling,  *[Kubernetes]*  voor implementatie van de container en Hallo [Azure Container Service (ACS)] toohost uw toepassing.

### <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].
* Hallo [Azure-opdrachtregelinterface (CLI)].
* Een up-to-date [Java Developer Kit (JDK)].
* Apache van [Maven] bouwen tool (versie 3).
* Een [Git] client.
* Een [Docker] client.

> [!NOTE]
>
> Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Hallo Spring opstarten op Docker aan de slag web-app maken

Hallo stappen te volgen helpt u bij het bouwen van een webtoepassing Spring opstarten en lokaal te testen.

1. Open een opdrachtprompt en maken van een lokale map toohold uw toepassing en de wijziging toothat directory; bijvoorbeeld:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- of--
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo-directory.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Wijzig de directory toohello voltooid project.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Maven toobuild en Voer Hallo voorbeeld-app gebruiken.
   ```
   mvn package spring-boot:run
   ```

1. Test Hallo web-app door te bladeren toohttp://localhost:8080 of door de volgende Hallo `curl` opdracht:
   ```
   curl http://localhost:8080
   ```

1. U ziet Hallo volgende bericht wordt weergegeven: **Hallo Docker wereld**

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Maken van een Azure Container Registry hello Azure CLI gebruiken

1. Open een opdrachtprompt.

1. Meld u bij tooyour Azure-account:
   ```azurecli
   az login
   ```

1. Maak een resourcegroep voor hello Azure-resources in deze zelfstudie gebruikt.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Maak een register persoonlijke Azure-container in Hallo resourcegroep. Hallo-zelfstudie duwt Hallo voorbeeld-app als een Docker installatiekopie toothis register in latere stappen. Vervang `wingtiptoysregistry` met een unieke naam voor het register.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Uw app toohello container register push

1. Navigeer toohello configuratiemap voor uw installatie Maven (standaard ~/.m2/ of C:\Users\username\.m2) en open Hallo *settings.xml* bestand met een teksteditor.

1. Hallo-wachtwoord voor uw register container ophalen met hello Azure CLI.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Toevoegen van uw Azure-Container register-id en wachtwoord tooa nieuwe `<server>` verzameling in hello *settings.xml* bestand.
Hallo `id` en `username` Hallo-naam van het register Hallo zijn. Gebruik Hallo `password` waarde uit de vorige opdracht hello (zonder aanhalingstekens).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld '*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker / volledige*'), en open Hallo *pom.xml* bestand met een teksteditor.

1. Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container-register.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Update Hallo `<plugins>` verzameling in hello *pom.xml* bestand die Hallo `<plugin>` Hallo aanmelding adres en het register servernaam voor uw Azure-Container register bevat.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en Voer Hallo opdracht toobuild hello Docker-container en push Hallo installatiekopie toohello register te volgen:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Er wordt een foutbericht weergegeven dat vergelijkbaar tooone van de volgende Hallo is wanneer Maven pushes Hallo installatiekopie tooAzure:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Als u deze fout krijgt, meld u bij tooAzure vanaf Hallo Docker-opdrachtregel.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Vervolgens push uw container:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Maak een Kubernetes Cluster op ACS hello Azure CLI gebruiken

1. Maak een Kubernetes-cluster in Azure Container Service. Hallo volgende opdracht maakt u een *kubernetes* cluster in Hallo *wingtiptoys kubernetes* resource groep met *wingtiptoys containerservice* als Hallo-cluster naam, en *wingtiptoys kubernetes* als Hallo DNS-voorvoegsel:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Met deze opdracht kan een tijdje duren toocomplete.

1. Installeer `kubectl` met behulp van Azure CLI Hallo. Linux-gebruikers wellicht tooprefix deze opdracht met `sudo` omdat deze Hallo Kubernetes CLI te implementeert`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Downloaden van informatie over de configuratie van de Hallo cluster zodat u uw cluster vanuit de Hallo Kubernetes webinterface beheren kunt en `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Hallo installatiekopie tooyour Kubernetes cluster implementeren

Deze zelfstudie implementeert Hallo app met behulp `kubectl`, klikt u vervolgens kunt u tooexplore Hallo implementatie via Hallo Kubernetes webinterface.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Met de Hallo Kubernetes web-interface implementeren

1. Open een opdrachtprompt.

1. Hallo configuratie website voor uw cluster Kubernetes openen in de standaardbrowser:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Wanneer Hallo Kubernetes configuratie website in uw browser wordt geopend, klikt u op Hallo koppeling te**een beperkte app implementeren**:

   ![Kubernetes configuratie Website][KB01]

1. Wanneer Hallo **een beperkte app implementeren** pagina wordt weergegeven, geeft u Hallo volgende opties:

   a. Selecteer **appdetails hieronder opgeven**.

   b. Voer de naam van uw Spring Boot-toepassing voor Hallo **appnaam**; bijvoorbeeld: '*gs-spring-boot-docker*'.

   c. Voer uw aanmelding server en de container installatiekopie van eerder voor Hallo **Container installatiekopie**; bijvoorbeeld: '*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*'.

   d. Kies **externe** voor Hallo **Service**.

   e. Geef uw interne en externe poorten in Hallo **poort** en **poort doel** tekstvakken.

   ![Kubernetes configuratie Website][KB02]


1. Klik op **implementeren** toodeploy Hallo container.

   ![Container implementeren][KB05]

1. Wanneer uw toepassing is geïmplementeerd, ziet u uw toepassing Spring Boot is vermeld in **Services**.

   ![Kubernetes Services][KB06]

1. Als u klikt op de koppeling Hallo voor **externe eindpunten**, ziet u uw toepassing Spring opstarten op Azure.

   ![Kubernetes Services][KB07]

   ![Voorbeeld-App in Azure bladeren][SB02]


### <a name="deploy-with-kubectl"></a>Met kubectl implementeren

1. Open een opdrachtprompt.

1. De container in Hallo Kubernetes cluster worden uitgevoerd met behulp van Hallo `kubectl run` opdracht. Geef een servicenaam voor uw app in Kubernetes en de naam van de volledige installatiekopie Hallo. Bijvoorbeeld:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   In deze opdracht:

   * Hallo-containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na Hallo `run` opdracht

   * Hallo `--image` parameter geeft u op Hallo gecombineerde login-server en de naam van de installatiekopie als`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Uw cluster Kubernetes blootstellen extern via Hallo `kubectl expose` opdracht. Geef de servicenaam van uw, Hallo openbare TCP-poort die wordt gebruikt tooaccess Hallo app en interne doelpoort Hallo die uw app luistert op. Bijvoorbeeld:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   In deze opdracht:

   * Hallo-containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na Hallo `expose deployment` opdracht

   * Hallo `--type` parameter geeft u op dat cluster Hallo maakt gebruik van load balancer

   * Hallo `--port` parameter geeft Hallo openbare TCP-poort 80. U toegang tot de app Hallo op deze poort.

   * Hallo `--target-port` parameter geeft Hallo interne TCP-poort van 8080. Hallo load balancer verzendt aanvragen tooyour app op deze poort.

1. Zodra het Hallo-app wordt geïmplementeerd wordt toohello cluster, Hallo externe IP-adres zoeken en openen in uw webbrowser:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Voorbeeld-App in Azure bladeren][SB02]


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van opstarten Spring op Azure Hallo artikelen te volgen:

* [Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren](container-service-deploy-spring-boot-app-on-linux.md)

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

Zie voor meer informatie over Hallo Spring opstarten op Docker-voorbeeldproject [Spring opstarten op het Docker aan de slag].

Hallo volgende koppelingen bieden aanvullende informatie over het maken van opstarten Spring toepassingen:

* Zie voor meer informatie over het maken van een eenvoudige Spring Boot-toepassing hello Spring Initializr op https://start.spring.io/.

Hallo vindt volgende koppelingen u meer informatie over het gebruik van Kubernetes met Azure:

* [Aan de slag met een cluster Kubernetes in Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Met behulp van Hallo Kubernetes-webgebruikersinterface met Azure Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Meer informatie over het gebruik van de opdrachtregelinterface Kubernetes is beschikbaar in Hallo **kubectl** gebruikershandleiding op <https://kubernetes.io/docs/user-guide/kubectl/>.

Hallo Kubernetes website heeft verschillende artikelen waarin met afbeeldingen in persoonlijke registers worden besproken:

* [Configureren van Service-Accounts voor het gehele product]
* [Naamruimten]
* [Binnenhalen van een installatiekopie van een persoonlijke register]

Zie voor meer voorbeelden van hoe toouse aangepaste Docker met Azure afbeeldingen [met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux].

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configureren van Service-Accounts voor het gehele product]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Naamruimten]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Binnenhalen van een installatiekopie van een persoonlijke register]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
