---
title: aaaPublish een Docker-container met behulp van Azure Toolkit voor Eclipse Hallo | Microsoft Docs
description: Meer informatie over hoe toopublish een web-app tooMicrosoft Azure als een Docker-container met behulp van Azure Toolkit voor Eclipse Hallo.
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor Eclipse

Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen. Met behulp van Docker-containers kunnen ontwikkelaars alle projectbestanden en afhankelijkheden in een enkel pakket voor tooa implementatieserver consolideren. Hello Azure Toolkit voor Eclipse vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* functies voor implementatie tooMicrosoft Azure. Dit artikel begeleidt u bij Hallo stappen vereist toopublish uw toepassingen tooAzure als Docker-containers.

> [!NOTE]
> Meer informatie over Docker is beschikbaar op Hallo [Docker-website].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Uw web-app tooAzure publiceren met behulp van Docker-container

1. Open uw web-app-project in Eclipse.

2. Hallo toostart **publiceren als Docker-Container** wizard Hallo volgende doen:

   * In Hallo **Navigator** weergeven, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**.

      ![Weergave van de Navigator publiceren als de opdracht Docker-Container][PUB01]

   * Klik op Hallo Eclipse werkbalk op Hallo **publiceren** knop en klik vervolgens op **publiceren als Docker-Container**.

      ![Werkbalk van eclipse publiceren als de opdracht Docker-Container][PUB02]
      
    Hallo **Docker-Container in Azure implementeren** wizard wordt geopend.

    ![Hallo Docker-Container in de wizard Azure implementeren][PUB03]

3. In Hallo **typt u een installatiekopie met de naam, selecteer Hallo-artefact pad en controleren van een Docker host toobe gebruikt** venster Hallo te volgen:

    a. In Hallo **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host. (Hallo wizard maakt automatisch een naam, maar u kunt deze wijzigen.)

    b. Hallo **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt. Hallo volgende doen:

    * Als u een bestaande Docker-host hebt, kunt u uw web-app tooit kunt implementeren.
    * toocreate een nieuwe Docker-host, klikt u op **toevoegen**.  
      
    Hallo **Docker-Host maken** dialoogvenster wordt geopend.

    ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. In Hallo **Hallo nieuwe virtuele machine configureren** venster Hallo volgend opties voor de Docker-host opgeeft. (Hallo wizard genereert automatisch Hallo opties waarmee u de meeste, maar u deze kunt wijzigen.)

   a. **Naam**: Voer een unieke naam voor Hallo Docker-host. (Dit is hetzelfde als de naam van de Docker-installatiekopie die u eerder hebt opgegeven Hallo niet Hallo.)

   b. **Abonnement**: Voer hello Azure-abonnement dat u voor de host gebruikt.

   c. **Regio**: Voer Hallo geografische regio waar uw host bevindt.

   d. Op Hallo **Host-OS en de grootte** tabblad:
     * **Host-OS**: Voer Hallo-besturingssysteem voor Hallo virtuele machine met de host.
     * **De grootte van**: Geef de grootte voor de virtuele machine Hallo voor de host.

   e. Op Hallo **resourcegroep** tabblad:
     * **Nieuwe resourcegroep**: een nieuwe resourcegroep maken voor de host.
     * **Bestaande resourcegroep**: Voer een bestaande resourcegroep van uw Azure-account.

   f. Op Hallo **netwerk** tabblad:
     * **Nieuw virtueel netwerk**: Maak een nieuw virtueel netwerk voor de host.
     * **Bestaand virtueel netwerk**: Voer een bestaand virtueel netwerk van uw Azure-account.

   g. Op Hallo **opslag** tabblad:
     * **Nieuw opslagaccount**: Maak een nieuw opslagaccount voor de host.
     * **Bestaande opslagaccount**: Voer een bestaand opslagaccount van uw Azure-account.

5. Klik op **Volgende**.

6. In Hallo **logboek referenties configureren en poortinstellingen** venster, selecteert u een van de Hallo volgende opties:

    * **Referenties importeren uit Azure Key Vault**: Hiermee geeft u een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.

      >[!NOTE]
      >Een Azure Key Vault dat gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die Hallo-abonnement deelt. tooallow een ander account of de service principal toouse Hallo Sleutelkluis, moet u hello Azure portal tooadd Hallo account of service-principal gebruiken.

    * **Nieuwe aanmelding referenties**: maakt een nieuwe set aanmeldingsreferenties. Als u deze optie selecteert, Hallo te volgen:
    
      * Op Hallo **VM referenties** tabblad, kiest u een van de volgende Hallo opties voor Hallo virtuele machines-aanmeldingsreferenties van de Docker-host:

          * **Gebruikersnaam**: Hallo gebruikersnaam invoeren voor de aanmeldingsreferenties van de virtuele machine.
          * **Wachtwoord** en **bevestigen**: Hallo wachtwoord invoeren voor de aanmeldingsreferenties van de virtuele machine.
          * **SSH**: Voer Hallo Secure Shell (SSH)-instellingen voor de Docker-host. U kunt kiezen uit Hallo volgende opties:
            * **Geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.
            * **Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via SSH.
            * **Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen SSH-instellingen. Hallo directory moet de volgende twee bestanden Hallo bevatten:
                * *id_rsa*: Hallo RSA-id voor een gebruiker bevat.
                * *id_rsa.pub*: bevat Hallo openbare RSA-sleutel die wordt gebruikt voor verificatie.
        
        ![Docker-Host maken][PUB05]

      * Op Hallo **Docker-Daemon referenties** tabblad, Hallo volgende opties opgeven:

          * **Docker-Daemon poort**: Voer Hallo unieke TCP-poort voor de Docker-host.
          * **TLS beveiliging**: Voer Hallo Transport Layer Security-instellingen voor de Docker-host. U kunt kiezen uit Hallo volgende opties:
            * **Geen**: Hiermee geeft u de virtuele machine staat niet toe dat TLS-verbindingen.
            * **Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via TLS.
            * **Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen TLS-instellingen. Hallo directory moet meer specifiek, Hallo volgende zes bestanden bevatten:
                * *CA.PEM* en *ca key.pem*: Hallo-certificaat en openbare sleutel voor Hallo TLS certificeringsinstantie bevatten.
                * *CERT.PEM* en *key.pem*: Hallo-clientcertificaat en openbare sleutel die wordt gebruikt voor het TLS-verificatie bevatten.
                * *Server.PEM* en *server key.pem*: Hallo servercertificaat en openbare sleutel voor Hallo host bevatten.

        ![Docker-Host maken][PUB06]

7. Nadat u alle voorgaande informatie Hallo hebt ingevoerd, klikt u op **voltooien**.

8. In Hallo **Docker-Container in Azure implementeren** wizard, klikt u op **volgende**.

   ![Hallo Docker-Container in de wizard Azure implementeren][PUB07]

9. In Hallo **hello Docker-container toobe gemaakt configureren** venster Hallo te volgen:

   a. In Hallo **Docker-containernaam** Voer een unieke naam voor uw Docker-container.

   b. Kies een van de Hallo Docker-installatiekopieën te volgen:
     * **De installatiekopie van een vooraf gedefinieerde Docker**: Hiermee geeft u een bestaande Docker-installatiekopie uit Azure.

       >[!NOTE]
       >Hallo-lijst van Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die Azure Toolkit is Hallo toopatch zo geconfigureerd dat uw artefacten automatisch wordt geïmplementeerd.

     * **Aangepaste Dockerfile**: Hiermee geeft u een eerder opgeslagen Dockerfile vanaf uw lokale computer.

       >[!NOTE]
       >Dit is een geavanceerde functie voor ontwikkelaars die toodeploy hun eigen Dockerfile willen. Het is echter van toodevelopers die gebruikmaken van deze optie tooensure die hun Dockerfile correct is ingebouwd. Hello Azure Toolkit valideren Hallo inhoud in een aangepaste Dockerfile zodat het Hallo-implementatie kan mislukken als Hallo Dockerfile problemen heeft. Bovendien hello Azure Toolkit verwacht Hallo aangepaste Dockerfile toocontain een artefact van web-app en wordt geprobeerd tooopen een HTTP-verbinding. Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.

   c. **Poortinstellingen**: Voer Hallo unieke TCP-poortbinding voor de Docker-container.

     ![Hallo configureren Hallo Docker-container gemaakt toobe venster][PUB08]

10. Nadat u alle Hallo vorige stappen hebt voltooid, klikt u op **voltooien**.

Hello Azure Toolkit begint de tooAzure van uw web-app in een Docker-container te implementeren. 

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

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

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

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png