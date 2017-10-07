---
title: aaaRun Java-toepassingsserver op een klassieke Azure-virtuele machine | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo en toont hoe toocreate een Windows-virtuele machine en configureer deze toorun Apache Tomcat-toepassingsserver.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Hoe toorun Java-toepassingsserver op een virtuele machine gemaakt met het klassieke implementatiemodel Hallo
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor toodeploy een webapp met Java 8 en Tomcat van een Resource Manager-sjabloon [hier](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

U kunt een virtuele machine tooprovide server mogelijkheden kunt gebruiken met Azure. Als u bijvoorbeeld mag een virtuele machine uitgevoerd op Azure geconfigureerde toohost Java-toepassingsserver, zoals Apache Tomcat.

Na het voltooien van deze handleiding hebt u een goed begrip van hoe u een virtuele machine toocreate uitgevoerd op Azure en configureer deze toorun Java-toepassingsserver. U leert en Hallo volgende taken uitvoeren:

* Hoe toocreate een virtuele machine die heeft een Java Development Kit (JDK) al is geïnstalleerd.
* Hoe tooremotely log in tooyour virtuele machine.
* Hoe tooinstall Java-toepassingsserver--Apache Tomcat--op de virtuele machine.
* Hoe toocreate een eindpunt voor uw virtuele machine.
* Hoe een poort in Hallo tooopen firewall voor de toepassingsserver.

Hallo voltooid Installatieresultaten in Tomcat uitgevoerd op een virtuele machine.

![Virtuele machine met Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate een virtuele machine
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).  
2. Klik op **nieuw**, klikt u op **Compute**, klikt u vervolgens op **alle** in Hallo **aanbevolen apps**.
3. Klik op **JDK**, klikt u op **JDK 8** in Hallo **JDK** deelvenster.  
   Installatiekopieën van virtuele machine die ondersteuning bieden voor **JDK 6** en **JDK 7** beschikbaar zijn als u oudere toepassingen die niet gereed toorun in JDK 8.
4. Selecteer in het deelvenster Hallo JDK 8 **klassieke**, klikt u vervolgens op **maken**.
5. In Hallo **basisbeginselen** blade:
   1. Geef een naam voor de Hallo virtuele machine.
   2. Voer een naam voor Hallo beheerder in Hallo **gebruikersnaam** veld. Houd er rekening mee deze naam en bijbehorende wachtwoord dat volgt op in het volgende veld Hallo Hallo. U moet deze als u zich extern toohello virtuele machine aanmelden.
   3. Voer een wachtwoord in Hallo **nieuw wachtwoord** veld en voer deze opnieuw in Hallo **wachtwoord bevestigen** veld. Dit wachtwoord is voor Hallo Administrator-account.
   4. Selecteer Hallo juiste **abonnement**.
   5. Voor Hallo **resourcegroep**, klikt u op **nieuw** en Voer Hallo-naam van een nieuwe resourcegroep. Of klik op **gebruik bestaande** en selecteer een van de beschikbare resourcegroepen Hallo.
   6. Selecteer een locatie waarin Hallo virtuele machine zich, zoals bevindt **Zuid-centraal VS**.
6. Klik op **Volgende**.
7. In Hallo **de grootte van de virtuele machine-installatiekopie** blade Selecteer **A1 standaard** of een andere juiste installatiekopie.
8. Klik op **Selecteren**.

9. In Hallo **instellingen** blade, klikt u op **OK**. U kunt de standaardwaarden Hallo verstrekt door Azure gebruiken.  
10. In Hallo **samenvatting** blade, klikt u op **OK**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely aanmelden tooyour virtuele machine
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **virtuele machines (klassiek)**. Klik indien nodig op **meer services** in linkerbenedenhoek onder servicecategorieën Hallo Hallo. Hallo **virtuele machines (klassiek)** vermelding wordt vermeld in Hallo **Compute** groep.
3. Klik op de naam Hallo van Hallo virtuele machine die u wilt toosign in.
4. Nadat Hallo virtuele machine is gestart, kunt een menu bovenaan Hallo Hallo deelvenster verbindingen.
5. Klik op **Verbinden**.
6. Reageren op toohello prompts als benodigde tooconnect toohello virtuele machine. Normaal gesproken opslaan of Hallo RDP-bestand met de Hallo verbindingsgegevens openen. U kunt toocopy Hallo url: poort als Hallo laatste deel van de eerste regel Hallo van Hallo RDP-bestand hebben en plak deze in een toepassing voor externe aanmelding.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall Java-toepassingsserver op de virtuele machine
U kunt een virtuele machine voor Java application server tooyour kopiëren of kunt u een Java-toepassingsserver via een installatieprogramma installeren.

Deze zelfstudie wordt Tomcat als Hallo Java application server tooinstall.

1. Wanneer u bent aangemeld in tooyour virtuele machine, opent u een browsersessie te[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Dubbelklik op de koppeling Hallo voor **32-bits/64-bits Windows-Service Installer**. Met deze techniek kunnen installeert Tomcat als een Windows-service.
3. Wanneer u wordt gevraagd, kiest u toorun Hallo installatieprogramma.
4. Binnen Hallo **Apache Tomcat Setup** , volg Hallo gevraagd tooinstall Tomcat. Voor Hallo doel van deze zelfstudie is het fijn Hallo standaardinstellingen accepteren. Wanneer u Hallo bereikt **voltooien Hallo Apache Tomcat-installatiewizard** in het dialoogvenster kunt u eventueel controleren **uitvoeren Apache Tomcat** toohave nu Tomcat start. Klik op **voltooien** toocomplete Hallo Tomcat-installatieproces.

## <a name="toostart-tomcat"></a>toostart Tomcat

U kunt Tomcat handmatig starten via een opdrachtprompt op de virtuele machine en de actieve Hallo opdracht **net&nbsp;start&nbsp;Tomcat8**.

Wanneer Tomcat wordt uitgevoerd, kunt u Tomcat openen door te voeren Hallo URL <http://localhost: 8080> in de browser Hallo virtuele machine.

toosee Tomcat vanaf externe computers wordt uitgevoerd, u toocreate een eindpunt nodig hebt en een poort openen.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate een eindpunt voor uw virtuele machine
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **virtuele machines (klassiek)**.
3. Klik op de naam Hallo van Hallo virtuele machine waarop uw Java-toepassingsserver wordt uitgevoerd.
4. Klik op **Eindpunten**.
5. Klik op **Add**.
6. In Hallo **eindpunt toevoegen** in het dialoogvenster:
   1. Geef een naam voor het eindpunt Hallo; bijvoorbeeld: **HttpIn**.
   2. Selecteer **TCP** voor het Hallo-protocol.
   3. Geef **80** voor Hallo openbare poort.
   4. Geef **8080** voor Hallo particuliere poort.
   5. Selecteer **uitgeschakelde** voor Hallo zwevend IP-adres.
   6. Laat Hallo toegangsbeheerlijst is.
   7. Klik op Hallo **OK** tooclose Hallo dialoogvenster knop en Hallo-eindpunt worden gemaakt.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen een poort in de firewall Hallo voor uw virtuele machine
1. Meld u aan tooyour virtuele machine.
2. Klik op **Windows Start**.
3. Klik op **Configuratiescherm**.
4. Klik op **systeem en beveiliging**, klikt u op **Windows Firewall**, en klik vervolgens op **geavanceerde instellingen**.
5. Klik op **regels voor binnenkomende verbindingen**, en klik vervolgens op **nieuwe regel**.  
   ![Nieuwe regel binnenkomende verbindingen][NewIBRule]
6. Voor Hallo **regeltype**, selecteer **poort**, en klik vervolgens op **volgende**.  
   ![Nieuwe regel voor binnenkomende verbindingen poort][NewRulePort]
7. Op Hallo **protocollen en poorten** Schakel in het scherm **TCP**, geef **8080** als Hallo **specifieke lokale poort**, en klik vervolgens op **Volgende**.  
  ![Nieuwe regel binnenkomende verbindingen][NewRuleProtocol]
8. Op Hallo **actie** Schakel in het scherm **Hallo verbinding toestaan**, en klik vervolgens op **volgende**.
   ![Nieuwe regel voor binnenkomende verbindingen actie][NewRuleAction]
9. Op Hallo **profiel** scherm **domein**, **persoonlijke**, en **openbare** zijn geselecteerd en klik vervolgens op **volgende** .
   ![Nieuwe regel voor binnenkomende verbindingen profiel][NewRuleProfile]
10. Op Hallo **naam** scherm, Geef een naam voor de regel hello, zoals **HttpIn** (Hallo regelnaam is niet vereist toomatch Hallo eindpuntnaam, echter), en klik vervolgens op **voltooien**.  
    ![De naam van een nieuwe regel voor binnenkomende verbindingen][NewRuleName]

Op dit moment uw website Tomcat worden weergegeven op een externe browser. Typ in het venster van de webbrowser van het Hallo-adres met Hallo URL  **http://*uw\_DNS\_naam*. cloudapp.net**, waarbij ***uw\_DNS\_naam*** Hallo DNS-naam die u hebt opgegeven toen u Hallo virtuele machine hebt gemaakt.

## <a name="application-lifecycle-considerations"></a>Toepassing lifecycle overwegingen
* Kan u uw eigen toepassing webarchief (WAR) maken en toe te voegen toohello **webapps** map. Bijvoorbeeld, een elementaire Java Service pagina (JSP) dynamic webproject maken en exporteren als een WAR-bestand. Kopieer vervolgens Hallo WAR toohello Apache Tomcat **webapps** map Hallo voor virtuele machines vervolgens uit te voeren in een browser.
* Wanneer Hallo Tomcat-service is geïnstalleerd, is deze standaard ingesteld toostart handmatig. U kunt schakelen deze toostart automatisch via Hallo-module Services. Hallo-module Services starten door te klikken op **Start Windows**, **Systeembeheer**, en vervolgens **Services**. Dubbelklik op Hallo **Apache Tomcat** service en stel **opstarttype** te**automatische**.

    ![Een service toostart instellen automatisch][service_automatic_startup]

    Hallo is voordeel van Tomcat automatisch wordt gestart met dat het wordt gestart wanneer Hallo virtuele machine opnieuw wordt opgestart (bijvoorbeeld nadat software-updates waarvoor opnieuw opstarten zijn geïnstalleerd).

## <a name="next-steps"></a>Volgende stappen
U kunt meer informatie over andere services (zoals Azure Storage, servicebus en SQL-Database) die u kunt tooinclude met uw Java-toepassingen. Hallo beschikbare informatie bekijken op Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
