---
title: een Docker-container met behulp van aaaPublish hello Azure Toolkit voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toopublish een web-app tooMicrosoft Azure als een Docker-container met behulp van Azure Toolkit Hallo voor IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ

Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen. Met behulp van Docker-containers kunnen ontwikkelaars alle projectbestanden en afhankelijkheden in een enkel pakket voor tooa implementatieserver consolideren. Hello Azure Toolkit voor IntelliJ vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* functies voor implementatie tooMicrosoft Azure. Dit artikel begeleidt u bij Hallo stappen vereist toopublish uw toepassingen tooAzure als Docker-containers.

> [!NOTE]
>
> Meer informatie over Docker is beschikbaar op Hallo [Docker-website].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Uw web-app tooAzure publiceren met behulp van Docker-container

> [!NOTE]
> * toopublish uw web-app, moet u een implementatie-ready artefacten maken. meer, Zie Hallo toolearn [aanvullende informatie over het maken van artefacten](#artifacts) sectie.
>
> * Nadat u de wizard implementatie Hallo ten minste eenmaal hebt voltooid, worden de meeste van uw instellingen als standaardwaarden gebruikt wanneer u Hallo wizard opnieuw uitvoeren.
>

1. Open IntelliJ uw web-app-project.

2. Hallo toostart **publiceren als Docker-Container** wizard Hallo volgende doen:

   * In Hallo **Project** venster hulpprogramma, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**:

      ![Hallo publiceren als de opdracht Docker-Container][PUB01]

   * Klik op Hallo IntelliJ werkbalk op Hallo **groep publiceren** knop en klik vervolgens op **publiceren als Docker-Container**:

      ![Hallo publiceren als de opdracht Docker-Container][PUB02]  
    Hallo **Docker-Container in Azure implementeren** wizard wordt geopend.

   ![Hallo Docker-Container in de wizard Azure implementeren][PUB03]

3. In Hallo **typt u een installatiekopie met de naam, selecteer Hallo-artefact pad en controleren van een Docker host toobe gebruikt** venster Hallo te volgen: 

   a. In Hallo **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host. (Hallo wizard maakt automatisch een naam, maar u kunt deze wijzigen.) 

   b. Hallo **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt. Hallo volgende doen: 
      * Als u een bestaande Docker-host hebt, kunt u uw web-app tooit kunt implementeren.
      * toocreate een Docker-host, klikt u op Hallo groen plusteken (**+**).  
       Hallo **Docker-Host maken** dialoogvenster wordt geopend. 

      ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. In Hallo **Hallo nieuwe virtuele machine configureren** venster bieden Hallo informatie over de Docker-host te volgen. (Hallo wizard genereert automatisch Hallo-informatie voor u de meeste, maar u deze kunt wijzigen.) 

   a. In Hallo **naam** Voer een unieke naam voor Hallo Docker-host. (Dit is hetzelfde als de naam van de Docker-installatiekopie die u eerder hebt opgegeven Hallo niet Hallo.) 
    
   b. In Hallo **abonnement** Voer hello Azure-abonnement dat u voor de host gebruikt. 
      
   c. In Hallo **regio** Voer Hallo geografische regio waar uw host bevindt.
      
   d. Op Hallo **OS en de grootte** tabblad, Hallo te volgen:      
      * **Host-OS**: Voer Hallo-besturingssysteem voor Hallo virtuele machine met de host. 
      * **De grootte van**: Geef de grootte voor de virtuele machine Hallo voor de host.   
       
   e. Op Hallo **resourcegroep** tabblad, selecteert u een van de volgende Hallo:      
      * **Nieuwe resourcegroep**: een resourcegroep maken voor de host.
      * **Bestaande resourcegroep**: Geef een bestaande resourcegroep van uw Azure-account. 
       
   f. Op Hallo **netwerk** tabblad, selecteert u een van de volgende Hallo:      
      * **Nieuw virtueel netwerk**: een virtueel netwerk maken voor de host.
      * **Bestaand virtueel netwerk**: Geef een bestaand virtueel netwerk van uw Azure-account. 
       
   g. Op Hallo **opslag** tabblad, selecteert u een van de volgende Hallo:      
      * **Nieuw opslagaccount**: een opslagaccount maken voor de host.
      * **Bestaande opslagaccount**: Geef een bestaand opslagaccount van uw Azure-account.
       
5. Klik op **Volgende**.  
     Hallo **logboek referenties configureren en poortinstellingen** venster wordt geopend.

      ![Hallo configureren aanmelden referenties en poort instellingenvenster][PUB05]

6. Selecteer een Hallo volgende opties:

      * **Referenties importeren uit Azure Key Vault**: Geef een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.

          > [!NOTE]
          > Een Azure sleutelkluis die gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die Hallo-abonnement deelt. tooallow een ander account of de service principal toouse Hallo key vault, moet u hello Azure portal tooadd Hallo account of service-principal gebruiken.

      * **Nieuwe aanmelding referenties**: Maak een nieuwe set aanmeldingsreferenties. Als u deze optie selecteert, Hallo te volgen:

        a. Op Hallo **VM referenties** tabblad, bieden Hallo-gegevens voor Hallo aanmeldingsgegevens voor virtuele machines van de Docker-host te volgen: * **gebruikersnaam**: Hallo gebruikersnaam invoeren voor de aanmelding voor uw virtuele machines de referenties.
             * **Wachtwoord** en **bevestigen**: Hallo wachtwoord invoeren voor uw virtuele machines aanmeldingsreferenties.
             * **SSH**: Voer Hallo Secure Shell (SSH)-instellingen voor de Docker-host. U kunt een Hallo volgende opties selecteren: * **geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.
                * **Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via SSH.
                * **Importeren uit directory**: Hiermee kunt u toospecify een map met een set van de eerder opgeslagen SSH-instellingen. Hallo directory moet de volgende twee bestanden Hallo bevatten:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. Op Hallo **Docker-Daemon toegang** tabblad, bieden Hallo volgende informatie:

          ![Docker-Host maken][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Nadat u Hallo vereiste gegevens hebt ingevoerd, klikt u op **voltooien**.  
    Hallo **Docker-Container in Azure implementeren** wizard opnieuw wordt weergegeven.

   ![Docker-Container in de Wizard Azure implementeren][PUB07]

8. Klik op **Volgende**.  
    Hallo **hello Docker-container toobe gemaakt configureren** venster wordt geopend.

   ![Hallo configureren Hallo Docker-container gemaakt toobe venster][PUB08]

9. In Hallo **hello Docker-container toobe gemaakt configureren** venster bieden Hallo volgende informatie: 

   a. In Hallo **Docker-containernaam** Voer een unieke naam voor uw Docker-container.

   b. Kies een van de Hallo Docker-installatiekopieën te volgen: 

      * **De installatiekopie van een vooraf gedefinieerde Docker**: Geef een bestaande Docker-installatiekopie uit Azure. 

        > [!NOTE]
        > Hallo-lijst van Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die Azure Toolkit is Hallo toopatch zo geconfigureerd dat uw artefacten automatisch wordt geïmplementeerd. 

      * **Aangepaste Dockerfile**: Geef een eerder opgeslagen Dockerfile vanaf uw lokale computer.

        > [!NOTE]
        > Dit is een geavanceerde functie voor ontwikkelaars die toodeploy hun eigen Dockerfile willen. Het is echter van toodevelopers die gebruikmaken van deze optie tooensure die hun Dockerfile correct is ingebouwd. Omdat Azure Toolkit Hallo Hallo inhoud in een aangepaste Dockerfile niet valideren, worden de Hallo-implementatie kan mislukken als Hallo Dockerfile problemen heeft. Bovendien omdat hello Azure Toolkit Hallo aangepaste Dockerfile toocontain een artefact van web-app verwacht, probeert het tooopen een HTTP-verbinding. Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.

   c. In Hallo **poortinstellingen** Voer Hallo unieke TCP-poortbinding voor de Docker-container. 

10. Nadat u Hallo vorige stappen hebt voltooid, klikt u op **voltooien**. 

Hello Azure Toolkit begint de tooAzure van uw web-app in een Docker-container te implementeren. Tenzij u hebt geconfigureerd IntelliJ toobe geïmplementeerd op de achtergrond hello, een **tooAzure implementeren** voortgangsbalk weergegeven. 

![Hallo implementatie voortgangsbalk][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Als u meer informatie over het maken van artefacten

een artefact implementatie gereed toocreate Hallo te volgen:

1. Open IntelliJ uw web-app-project.

2. Klik op **bestand**, en klik vervolgens op **projectstructuur**.

   ![Hallo structuur Project-opdracht][ART01]

3. tooadd een artefact, klikt u op Hallo groen plusteken (**+**), en klik vervolgens op **webtoepassing: archief**.

   ![Hallo 'Toepassing: webarchief'-opdracht][ART02]

4. In Hallo **naam** Voer een naam voor uw artefacten (omvatten geen Hallo *.war* extensie), en klik vervolgens op **OK**.

   ![Hallo artefact naamvak][ART03]

Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op Hallo JetBrains website.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * [Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * [Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

Zie voor aanvullende bronnen voor Docker Hallo officiële [Docker-website].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Docker-website]: https://www.docker.com/
[artefacten configureren]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
