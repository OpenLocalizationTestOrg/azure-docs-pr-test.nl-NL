---
title: Een Docker-container te publiceren met behulp van de Azure-Toolkit voor IntelliJ | Microsoft Docs
description: Informatie over het publiceren van een web-app naar Microsoft Azure als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ.
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
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ

Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen. Met behulp van Docker-containers kunnen ontwikkelaars hun project-bestanden en afhankelijkheden in een enkel pakket voor implementatie naar een server consolideren. De Azure-werkset voor IntelliJ vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* onderdelen voor implementatie naar Microsoft Azure. Dit artikel begeleidt u bij de stappen die nodig zijn voor het publiceren van uw toepassingen naar Azure als Docker-containers.

> [!NOTE]
>
> Meer informatie over Docker is beschikbaar op de [Docker-website].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Uw web-app publiceren naar Azure met behulp van Docker-container

> [!NOTE]
> * Voor het publiceren van uw web-app, moet u een artefact implementatie gereed te maken. Zie voor meer informatie, de [aanvullende informatie over het maken van artefacten](#artifacts) sectie.
>
> * Nadat u de implementatiewizard ten minste eenmaal hebt voltooid, worden de meeste van uw instellingen als standaardwaarden gebruikt wanneer u de wizard opnieuw uitvoeren.
>

1. Open IntelliJ uw web-app-project.

2. Starten de **publiceren als Docker-Container** wizard een van de volgende handelingen uit:

   * In de **Project** venster hulpprogramma, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**:

      ![Het publiceren als de opdracht Docker-Container][PUB01]

   * Klik op de werkbalk IntelliJ de **groep publiceren** knop en klik vervolgens op **publiceren als Docker-Container**:

      ![Het publiceren als de opdracht Docker-Container][PUB02]  
    De **Docker-Container in Azure implementeren** wizard wordt geopend.

   ![De Docker-Container implementeren in de Azure-wizard][PUB03]

3. In de **typt u een installatiekopie met de naam, selecteer het artefact pad en controleren van een Docker-host moet worden gebruikt** venster de volgende handelingen uit: 

   a. In de **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host. (De wizard maakt automatisch een naam, maar u kunt deze wijzigen.) 

   b. De **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt. Voer een van de volgende bewerkingen uit: 
      * Als u een bestaande Docker-host hebt, kunt u uw web-app te implementeren.
      * Klik op het groen plusteken om een Docker-host (**+**).  
       De **Docker-Host maken** dialoogvenster wordt geopend. 

      ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. In de **configureren van de nieuwe virtuele machine** venster de volgende informatie over de Docker-host. (De wizard automatisch de meeste informatie voor u gegenereerd, maar u deze kunt wijzigen.) 

   a. In de **naam** Voer een unieke naam voor de Docker-host. (Dit is niet hetzelfde zijn als de naam van de Docker-installatiekopie die u eerder hebt opgegeven.) 
    
   b. In de **abonnement** Voer het Azure-abonnement dat u voor de host gebruikt. 
      
   c. In de **regio** Voer de geografische regio waar uw host bevindt.
      
   d. Op de **OS en de grootte** tabblad, het volgende doen:      
      * **Host-OS**: Geef het besturingssysteem voor de virtuele machine die de host bevat. 
      * **De grootte van**: Geef de grootte van de virtuele machine voor de host.   
       
   e. Op de **resourcegroep** tabblad, selecteert u een van de volgende:      
      * **Nieuwe resourcegroep**: een resourcegroep maken voor de host.
      * **Bestaande resourcegroep**: Geef een bestaande resourcegroep van uw Azure-account. 
       
   f. Op de **netwerk** tabblad, selecteert u een van de volgende:      
      * **Nieuw virtueel netwerk**: een virtueel netwerk maken voor de host.
      * **Bestaand virtueel netwerk**: Geef een bestaand virtueel netwerk van uw Azure-account. 
       
   g. Op de **opslag** tabblad, selecteert u een van de volgende:      
      * **Nieuw opslagaccount**: een opslagaccount maken voor de host.
      * **Bestaande opslagaccount**: Geef een bestaand opslagaccount van uw Azure-account.
       
5. Klik op **Volgende**.  
     De **logboek referenties configureren en poortinstellingen** venster wordt geopend.

      ![Het logboek configureren in de referenties en poort instellingenvenster][PUB05]

6. Selecteer een van de volgende opties:

      * **Referenties importeren uit Azure Key Vault**: Geef een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.

          > [!NOTE]
          > Een Azure sleutelkluis die gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die het abonnement deelt. Als u wilt toestaan een ander account of -service principal gebruik van de sleutelkluis, moet u de Azure-portal de account of de service-principal toe te voegen.

      * **Nieuwe aanmelding referenties**: Maak een nieuwe set aanmeldingsreferenties. Als u deze optie selecteert, het volgende doen:

        a. Op de **VM referenties** tabblad, bieden de volgende informatie voor de virtuele machine-aanmeldingsreferenties van de Docker-host: * **gebruikersnaam**: Geef de gebruikersnaam voor uw virtuele machines aanmeldingsreferenties.
             * **Wachtwoord** en **bevestigen**: Voer het wachtwoord voor uw virtuele machines aanmeldingsreferenties.
             * **SSH**: Geef de instellingen van Secure Shell (SSH) voor de Docker-host. U kunt een van de volgende opties selecteren: * **geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.
                * **Automatisch genereren**: de vereiste instellingen automatisch maakt om verbinding te maken via SSH.
                * **Importeren uit directory**: Hiermee kunt u een map met een set van de eerder opgeslagen SSH-instellingen opgeven. De map moet bevatten de volgende twee bestanden:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Op de **Docker-Daemon toegang** tabblad, geef de volgende informatie:

          ![Docker-Host maken][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Nadat u de vereiste gegevens hebt ingevoerd, klikt u op **voltooien**.  
    De **Docker-Container in Azure implementeren** wizard opnieuw wordt weergegeven.

   ![Docker-Container in de Wizard Azure implementeren][PUB07]

8. Klik op **Volgende**.  
    De **configureren de Docker-container gemaakt** venster wordt geopend.

   ![Het configureren van de Docker-container venster worden gemaakt][PUB08]

9. In de **configureren de Docker-container gemaakt** venster de volgende informatie: 

   a. In de **Docker-containernaam** Voer een unieke naam voor uw Docker-container.

   b. Kies een van de volgende Docker-afbeeldingen: 

      * **De installatiekopie van een vooraf gedefinieerde Docker**: Geef een bestaande Docker-installatiekopie uit Azure. 

        > [!NOTE]
        > De lijst met Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die de Azure-Toolkit is geconfigureerd voor het patch zodat uw artefacten automatisch wordt geïmplementeerd. 

      * **Aangepaste Dockerfile**: Geef een eerder opgeslagen Dockerfile vanaf uw lokale computer.

        > [!NOTE]
        > Dit is een geavanceerde functie voor ontwikkelaars die willen hun eigen Dockerfile implementeren. Het is echter maximaal ontwikkelaars die gebruikmaken van deze optie om ervoor te zorgen dat hun Dockerfile correct is gebouwd. Omdat de Azure-Toolkit wordt de inhoud van een aangepaste Dockerfile niet gevalideerd, wordt de implementatie kan mislukken als de Dockerfile problemen heeft. Bovendien, omdat de Azure-Toolkit de aangepaste Dockerfile verwacht bevatten een web-app-artefacten, probeert te openen van een HTTP-verbinding. Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.

   c. In de **poortinstellingen** Geef de unieke TCP-poort-binding voor de Docker-container. 

10. Nadat u de voorgaande stappen hebt voltooid, klikt u op **voltooien**. 

De Toolkit Azure begint uw web-app implementeren naar Azure in een Docker-container. Tenzij u hebt geconfigureerd IntelliJ worden geïmplementeerd op de achtergrond een **implementeren naar Azure** voortgangsbalk weergegeven. 

![De voortgangsbalk implementatie][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Als u meer informatie over het maken van artefacten

Voor het maken van een implementatie-gereed-artefacten, het volgende doen:

1. Open IntelliJ uw web-app-project.

2. Klik op **bestand**, en klik vervolgens op **projectstructuur**.

   ![De structuur van de Project-opdracht][ART01]

3. Klik op Help als u een artefact groen plusteken (**+**), en klik vervolgens op **webtoepassing: archief**.

   ![De opdracht 'Toepassing: webarchief'][ART02]

4. In de **naam** Voer een naam voor uw artefacten (omvatten geen de *.war* extensie), en klik vervolgens op **OK**.

   ![Het naamvak artefact][ART03]

Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op de website JetBrains.

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

Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].

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

[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/
[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

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
