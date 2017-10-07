---
title: aaaCreate een Jenkins-server op Azure
description: Jenkins installeren op een virtuele machine van Azure Linux van Hallo Jenkins oplossingssjabloon en een voorbeeld van een Java-toepassing bouwen.
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Een server Jenkins maken op een Azure Linux VM van hello Azure-portal

Deze snelstartgids toont hoe tooinstall [Jenkins](https://jenkins.io) op een virtuele Ubuntu Linux-machine met Hallo-hulpprogramma's en invoegtoepassingen geconfigureerd toowork met Azure. Wanneer u klaar bent, beschikt u over een Jenkins-server die wordt uitgevoerd in Azure voor het bouwen van een Java-voorbeeld-app uit [GitHub](https://github.com).

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement
* Toegang tooSSH op de opdrachtregel van de computer (zoals Hallo Bash shell of [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Hallo Jenkins VM van Hallo oplossingssjabloon maken

Open Hallo [marketplace-installatiekopie voor Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in uw webbrowser en selecteer **IT ophalen nu** vanaf de linkerkant van de pagina Hallo Hallo. Bekijk Hallo pricing details en selecteer **doorgaan**, selecteer daarna **maken** tooconfigure hello Jenkins server in hello Azure-portal. 
   
![Dialoogvenster Azure-portal](./media/install-jenkins-solution-template/ap-create.png)

In Hallo **basisinstellingen configureren** tabblad, vul Hallo velden te volgen:

![Basisinstellingen configureren](./media/install-jenkins-solution-template/ap-basic.png)

* Geef **Jenkins** op bij **Naam**.
* Voer een gebruikersnaam in bij **Gebruikersnaam**. Hallo-gebruikersnaam moet voldoen aan [specifieke vereisten](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Selecteer **wachtwoord** als Hallo **verificatietype** en voer een wachtwoord. Hallo-wachtwoord moet een hoofdletter, cijfer en één speciaal teken.
* Gebruik **myJenkinsResourceGroup** voor Hallo **resourcegroep**.
* Kies Hallo **VS-Oost** [Azure-regio](https://azure.microsoft.com/regions/) van Hallo **locatie** vervolgkeuzelijst.

Selecteer **OK** tooproceed toohello **extra opties configureren** tabblad. Voer een unieke naam tooidentify hello Jenkins domeinserver en selecteer **OK**.

![selecteer aanvullende opties](./media/install-jenkins-solution-template/ap-addtional.png)  

 Als de validatie is geslaagd, selecteert u **OK** opnieuw uit Hallo **samenvatting** tabblad. Tot slot selecteert **aankoop** toocreate Hallo Jenkins VM. Wanneer de server klaar is, kunt u een melding krijgen in hello Azure-portal:   

![Melding dat de Jenkins-server klaar is](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Verbinding maken met tooJenkins

Navigeer tooyour virtuele machine (bijvoorbeeld http://jenkins2517454.eastus.cloudapp.azure.com/) in uw webbrowser. Hallo Jenkins console is niet toegankelijk via niet-beveiligde HTTP, zodat de instructies vindt u op Hallo pagina tooaccess hello Jenkins console veilig vanaf uw computer met behulp van een SSH-tunnel.

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Hallo-tunnel met Hallo instellen `ssh` opdracht op de pagina Hallo vanaf de opdrachtregel Hallo vervangen `username` met Hallo-naam van Hallo virtuele machine admin gebruiker eerder gekozen bij het instellen van Hallo virtuele machine uit Hallo oplossingssjabloon.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Nadat u de tunnel Hallo hebt gestart, gaat u toohttp://localhost:8080 / op uw lokale machine. 

Hallo eerste wachtwoord door het uitvoeren van de volgende opdracht in de opdrachtregel Hallo terwijl u bent verbonden via SSH toohello Jenkins VM Hallo ophalen.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Hallo Jenkins dashboard voor Hallo eerst met behulp van deze eerste wachtwoord ontgrendelen.

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-unlock.png)

Selecteer **voorgestelde invoegtoepassingen installeren** op Hallo voor volgende pagina en maak vervolgens een Jenkins admin gebruikt tooaccess hello Jenkins gebruikersdashboard.

![Jenkins is klaar.](./media/install-jenkins-solution-template/jenkins-welcome.png)

Hallo Jenkins server is nu gereed toobuild code.

## <a name="create-your-first-job"></a>Uw eerste taak maken

Selecteer **nieuwe taken maken** Hallo Jenkins console noem deze **mySampleApp** en selecteer **Freestyle project**, selecteer daarna **OK**.

![Een nieuwe taak maken](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Selecteer Hallo **Source Code Management** tabblad, schakelt u **Git**, en voer de volgende URL in Hallo **URL opslagplaats** veld:`https://github.com/spring-guides/gs-spring-boot.git`

![Hallo Git-opslagplaats definiëren](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Selecteer Hallo **bouwen** tabblad en selecteer vervolgens **toevoegen build stap**, **Gradle aanroepen script**. Selecteer **Use Gradle Wrapper** en voer vervolgens `complete` in bij **Wrapper location** en `build` bij **Tasks**.

![Hallo Gradle wrapper toobuild gebruiken](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Selecteer **Advanced..** en voer vervolgens `complete` in Hallo **hoofdmap Build script** veld. Selecteer **Opslaan**.

![Geavanceerde instellingen opgeven in Hallo Gradle wrapper build stap](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Hallo code bouwen

Selecteer **nu bouwen** toocompile Hallo code en pakket Hallo voorbeeld-app. Als uw build is voltooid, selecteert u Hallo **werkruimte** koppeling voor Hallo-project.

![Blader toohello werkruimte tooget Hallo JAR-bestand van Hallo-versie](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Navigeer te`complete/build/libs` en zorg ervoor dat Hallo `gs-spring-boot-0.1.0.jar` is er tooverify build is geslaagd. Uw Jenkins server nu is klaar toobuild projecten in Azure.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Virtuele Azure-machines toevoegen als Jenkins-agents](jenkins-azure-vm-agents.md)
