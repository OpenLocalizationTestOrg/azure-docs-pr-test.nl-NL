---
title: Een Docker-container te publiceren met behulp van de Azure-Toolkit voor Eclipse | Microsoft Docs
description: Informatie over het publiceren van een web-app naar Microsoft Azure als een Docker-container met behulp van de Azure-Toolkit voor Eclipse.
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor Eclipse

Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen. Met behulp van Docker-containers kunnen ontwikkelaars hun project-bestanden en afhankelijkheden in een enkel pakket voor implementatie naar een server consolideren. De Azure-werkset voor Eclipse vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* onderdelen voor implementatie naar Microsoft Azure. Dit artikel begeleidt u bij de stappen die nodig zijn voor het publiceren van uw toepassingen naar Azure als Docker-containers.

> [!NOTE]
> Meer informatie over Docker is beschikbaar op de [Docker-website].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Uw web-app publiceren naar Azure met behulp van Docker-container

1. Open uw web-app-project in Eclipse.

2. Starten de **publiceren als Docker-Container** wizard een van de volgende handelingen uit:

   * In de **Navigator** weergeven, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**.

      ![Weergave van de Navigator publiceren als de opdracht Docker-Container][PUB01]

   * Klik op de werkbalk van Eclipse op de **publiceren** knop en klik vervolgens op **publiceren als Docker-Container**.

      ![Werkbalk van eclipse publiceren als de opdracht Docker-Container][PUB02]
      
    De **Docker-Container in Azure implementeren** wizard wordt geopend.

    ![De Docker-Container implementeren in de Azure-wizard][PUB03]

3. In de **typt u een installatiekopie met de naam, selecteer het artefact pad en controleren van een Docker-host moet worden gebruikt** venster de volgende handelingen uit:

    a. In de **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host. (De wizard maakt automatisch een naam, maar u kunt deze wijzigen.)

    b. De **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt. Voer een van de volgende bewerkingen uit:

    * Als u een bestaande Docker-host hebt, kunt u uw web-app te implementeren.
    * Klik op om een nieuwe Docker-host **toevoegen**.  
      
    De **Docker-Host maken** dialoogvenster wordt geopend.

    ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. In de **configureren van de nieuwe virtuele machine** venster de volgende opties voor de Docker-host. (De wizard wordt automatisch gegenereerd voor de meeste opties voor u, maar u kunt een van deze wijzigen.)

   a. **Naam**: Voer een unieke naam voor de Docker-host. (Dit is niet hetzelfde zijn als de naam van de Docker-installatiekopie die u eerder hebt opgegeven.)

   b. **Abonnement**: Voer het Azure-abonnement dat u voor de host gebruikt.

   c. **Regio**: Voer de geografische regio waar uw host bevindt.

   d. Op de **Host-OS en de grootte** tabblad:
     * **Host-OS**: Geef het besturingssysteem voor de virtuele machine die de host bevat.
     * **De grootte van**: Geef de grootte van de virtuele machine voor de host.

   e. Op de **resourcegroep** tabblad:
     * **Nieuwe resourcegroep**: een nieuwe resourcegroep maken voor de host.
     * **Bestaande resourcegroep**: Voer een bestaande resourcegroep van uw Azure-account.

   f. Op de **netwerk** tabblad:
     * **Nieuw virtueel netwerk**: Maak een nieuw virtueel netwerk voor de host.
     * **Bestaand virtueel netwerk**: Voer een bestaand virtueel netwerk van uw Azure-account.

   g. Op de **opslag** tabblad:
     * **Nieuw opslagaccount**: Maak een nieuw opslagaccount voor de host.
     * **Bestaande opslagaccount**: Voer een bestaand opslagaccount van uw Azure-account.

5. Klik op **Volgende**.

6. In de **logboek referenties configureren en poortinstellingen** venster, selecteert u een van de volgende opties:

    * **Referenties importeren uit Azure Key Vault**: Hiermee geeft u een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.

      >[!NOTE]
      >Een Azure Key Vault dat gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die het abonnement deelt. Als u wilt toestaan een ander account of -service principal gebruik van de Sleutelkluis, moet u de Azure-portal de account of de service-principal toe te voegen.

    * **Nieuwe aanmelding referenties**: maakt een nieuwe set aanmeldingsreferenties. Als u deze optie selecteert, het volgende doen:
    
      * Op de **VM referenties** tabblad, kiest u een van de volgende opties voor de virtuele machine-aanmeldingsreferenties van de Docker-host:

          * **Gebruikersnaam**: Geef de gebruikersnaam voor de aanmeldingsreferenties van de virtuele machine.
          * **Wachtwoord** en **bevestigen**: Voer het wachtwoord voor uw virtuele machine-aanmeldingsreferenties.
          * **SSH**: Geef de instellingen van Secure Shell (SSH) voor de Docker-host. U kunt kiezen uit de volgende opties:
            * **Geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.
            * **Automatisch genereren**: de vereiste instellingen automatisch maakt om verbinding te maken via SSH.
            * **Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen SSH-instellingen. De map moet bevatten de volgende twee bestanden:
                * *id_rsa*: bevat de RSA-id voor een gebruiker.
                * *id_rsa.pub*: bevat de openbare RSA-sleutel die wordt gebruikt voor verificatie.
        
        ![Docker-Host maken][PUB05]

      * Op de **Docker-Daemon referenties** tabblad, geeft u de volgende opties:

          * **Docker-Daemon poort**: Voer de unieke TCP-poort voor de Docker-host.
          * **TLS beveiliging**: Geef de Transport Layer Security-instellingen voor de Docker-host. U kunt kiezen uit de volgende opties:
            * **Geen**: Hiermee geeft u de virtuele machine staat niet toe dat TLS-verbindingen.
            * **Automatisch genereren**: de vereiste instellingen automatisch maakt voor het verbinding maken via TLS.
            * **Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen TLS-instellingen. Meer specifiek, moet de map de volgende zes bestanden bevatten:
                * *CA.PEM* en *ca key.pem*: het certificaat en openbare sleutel voor de TLS-certificeringsinstantie bevatten.
                * *CERT.PEM* en *key.pem*: de client-certificaat en openbare sleutel die wordt gebruikt voor het TLS-verificatie bevatten.
                * *Server.PEM* en *server key.pem*: het servercertificaat en de openbare sleutel voor de host bevatten.

        ![Docker-Host maken][PUB06]

7. Nadat u alle voorgaande informatie hebt ingevoerd, klikt u op **voltooien**.

8. In de **Docker-Container in Azure implementeren** wizard, klikt u op **volgende**.

   ![De Docker-Container implementeren in de Azure-wizard][PUB07]

9. In de **configureren de Docker-container gemaakt** venster de volgende handelingen uit:

   a. In de **Docker-containernaam** Voer een unieke naam voor uw Docker-container.

   b. Kies een van de volgende Docker-afbeeldingen:
     * **De installatiekopie van een vooraf gedefinieerde Docker**: Hiermee geeft u een bestaande Docker-installatiekopie uit Azure.

       >[!NOTE]
       >De lijst met Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die de Azure-Toolkit is geconfigureerd voor het patch zodat uw artefacten automatisch wordt geïmplementeerd.

     * **Aangepaste Dockerfile**: Hiermee geeft u een eerder opgeslagen Dockerfile vanaf uw lokale computer.

       >[!NOTE]
       >Dit is een geavanceerde functie voor ontwikkelaars die willen hun eigen Dockerfile implementeren. Het is echter maximaal ontwikkelaars die gebruikmaken van deze optie om ervoor te zorgen dat hun Dockerfile correct is gebouwd. De Azure-Toolkit wordt de inhoud van een aangepaste Dockerfile niet gevalideerd, zodat de implementatie mislukken kan als de Dockerfile problemen heeft. Bovendien de Toolkit Azure verwacht de aangepaste Dockerfile bevatten een web-app-artefacten en wordt geprobeerd om een HTTP-verbinding te openen. Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.

   c. **Poortinstellingen**: Voer de unieke TCP-poort-binding voor de Docker-container.

     ![Het configureren van de Docker-container venster worden gemaakt][PUB08]

10. Nadat u alle voorgaande stappen hebt voltooid, klikt u op **voltooien**.

De Toolkit Azure begint uw web-app implementeren naar Azure in een Docker-container. 

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in de Azure-werkset voor Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [Aanmelden instructies voor de Azure-werkset voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in de Azure-werkset voor IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

Zie voor aanvullende bronnen voor Docker de officiële [Docker-website].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

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