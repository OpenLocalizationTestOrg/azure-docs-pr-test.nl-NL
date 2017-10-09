---
title: aaaCI/CD van Jenkins tooAzure virtuele machines in een Team Services | Microsoft Docs
description: Stel doorlopende integratie (CI) en continue implementatie (CD) van een Node.js-app met behulp van Jenkins tooAzure virtuele machines van Release Management in Visual Studio Team Services (VSTS) of Microsoft Team Foundation Server (TFS)
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Uw app tooLinux virtuele machines implementeren met behulp van Jenkins en Team Services

Continue integratie (CI) en continue implementatie (CD) is een pijplijn waarmee u kunt bouwen, vrijgeven en implementeer uw code. Teamservices biedt een complete, volledig functionele aantal CI/CD automation-hulpprogramma's voor implementatie tooAzure. Jenkins is een populaire 3rd derden CI/CD servergebaseerde hulpprogramma dat ook CI/CD automation biedt. U kunt beide samen toocustomize hoe u uw cloud-app of service leveren.

In deze zelfstudie gebruikt u Jenkins toobuild een **Node.js-web-app**, en Visual Studio Team Services toodeploy het tooa [implementatiegroep](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) met virtuele Linux-machines.

U gaat het volgende doen:

> [!div class="checklist"]
> * Uw app in Jenkins maken
> * Jenkins configureren voor integratie met Team Services
> * Een implementatiegroep voor hello Azure virtuele machines maken
> * De definitie van een versie die Hallo VMs configureert en implementeert Hallo-app maken

## <a name="before-you-begin"></a>Voordat u begint

* U hebt toegang tot tooa Jenkins account nodig. Als u een server Jenkins nog geen hebt gemaakt, raadpleegt u [Jenkins documentatie](https://jenkins.io/doc/). 

* Meld u aan tooyour Team Services-account (`https://{youraccount}.visualstudio.com`). 
  U krijgt een [gratis account Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Zie voor meer informatie [tooTeam Services verbinding](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Maak een persoonlijk toegangstoken (PAT) in uw Team Services-account als u er nog geen hebt. Jenkins vereist deze informatie tooaccess uw Team Services-account.
  Lees [hoe maak ik een persoonlijk toegangstoken voor Team Services en TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn hoe toogenerate een.

## <a name="get-hello-sample-app"></a>Hallo voorbeeld-app downloaden

U moet een app toodeploy opgeslagen in een Git-opslagplaats.
Voor deze zelfstudie wordt aangeraden u [deze voorbeeldapp beschikbaar is via GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Maak een fork van deze app en noteer Hallo locatie (URL) voor gebruik in latere stappen van deze zelfstudie.

1. Controleer Hallo fork **openbare** toosimplify tooGitHub later verbinding te maken.

> [!NOTE]
> Zie voor meer informatie [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/) en [een opslagplaats voor persoonlijke openbaar te maken](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> Hallo-app is gemaakt met [Yeoman](http://yeoman.io/learning/index.html); hierbij **Express**, **bower**, en **grunt**; en heeft een aantal **npm**pakketten als afhankelijkheden.
> Hallo voorbeeld-app bevat een set [Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) dat zijn gebruikte toodynamically Hallo virtuele machines maken voor implementatie op Azure. Deze sjablonen worden gebruikt door de taken in Hallo [Team Services release definitie](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> Hallo belangrijkste sjabloon maakt u een netwerkbeveiligingsgroep en een virtuele machine een virtueel netwerk. Het een openbare IP-adres toewijst en binnenkomende poort 80 wordt geopend. Ook een code die wordt gebruikt door Hallo implementatie te selecteren Hallo machines tooreceive Hallo implementatie worden toegevoegd.
>
> Hallo-voorbeeld bevat ook een script dat Nginx ingesteld en het Hallo-app wordt geïmplementeerd. Deze wordt uitgevoerd op elke Hallo virtuele machines. In het bijzonder installeert Hallo script knooppunt, Nginx en PM2; Hiermee configureert u Nginx en PM2; vervolgens wordt de Hallo knooppunt app gestart.

## <a name="configure-jenkins-plugins"></a>Jenkins plugins configureren

Eerst moet u twee Jenkins invoegtoepassingen voor **NodeJS** en **integratie met Team Services**.

1. Open uw Jenkins-account en kies **Jenkins beheren**.

1. In Hallo **beheren Jenkins** pagina **invoegtoepassingen beheren**.

1. Filter Hallo lijst toolocate hello **NodeJS** invoegtoepassing en zonder opnieuw te installeren.

   ![Hallo NodeJS invoegtoepassing tooJenkins toevoegen](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filter Hallo lijst toofind hello **Team Foundation Server** invoegtoepassing en te installeren. (Deze invoegtoepassing werkt voor zowel Team Services en Team Foundation Server.) Jenkins opnieuw te starten is niet nodig.

## <a name="configure-jenkins-build-for-nodejs"></a>Jenkins build configureren voor Node.js

Maak een nieuwe build-project in Jenkins, en als volgt configureren:

1. In Hallo **algemene** tabblad, voer een naam voor uw project bouwen.

1. In Hallo **Source Code Management** tabblad **Git** en Hallo details van Hallo opslagplaats en Hallo vertakking met uw app-code invoeren.

   ![Een opslagplaats tooyour build toevoegen](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Als uw opslagplaats niet openbaar is, kiest u **toevoegen** en referenties tooconnect tooit bieden.

1. In Hallo **bouwen Triggers** tabblad **Poll SCM** en Voer Hallo planning `H/03 * * * *` toopoll Hallo Git-opslagplaats voor elke drie minuten wijzigingen. 

1. In Hallo **bouwen omgeving** tabblad **bieden knooppunt &amp; npm bin / map pad** en voer `NodeJS` voor Hallo knooppunt JS installatie waarde. Laat **npmrc bestand** ingesteld op "systeemstandaard gebruiken".

1. In Hallo **bouwen** tabblad, gebruikt u de opdracht Hallo `npm install` tooensure alle afhankelijkheden zijn bijgewerkt.

## <a name="configure-jenkins-for-team-services-integration"></a>Jenkins configureren voor integratie met Team Services

1. In Hallo **na build acties** tabblad voor **bestanden tooarchive**, voer `**/*` tooinclude alle bestanden.

1. Voor **release in TFS/Team Services activeren**, Hallo volledige URL van uw account opgeven (zoals `https://your-account-name.visualstudio.com`), Hallo projectnaam, een naam voor de definitie van release hello (later gemaakt), en Hallo referenties tooconnect tooyour account.
   U moet uw gebruikersnaam en het Hallo PAT die u eerder hebt gemaakt. 

   ![Jenkins na build acties configureren](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Hallo build project opslaan.

## <a name="create-a-jenkins-service-endpoint"></a>Een Jenkins service-eindpunt maken

Een service-eindpunt kunt Team Services tooconnect tooJenkins.

1. Open Hallo **Services** pagina in een Team Services, open Hallo **nieuwe Service-eindpunt** lijst en kies **Jenkins**.

   ![Een eindpunt Jenkins toevoegen](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Voer een naam die u toorefer toothis verbinding wilt gebruiken.

1. Voer Hallo-URL van uw server Jenkins en maatstreepjes Hallo **accepteren van niet-vertrouwde certificaten voor SSL** optie.

1. Hallo-gebruikersnaam en wachtwoord invoeren voor uw account Jenkins.

1. Kies **verbinding controleren** toocheck die Hallo informatie juist is.

1. Kies **OK** toocreate Hallo service-eindpunt.

## <a name="create-a-deployment-group"></a>Een implementatiegroep maken

U moet een [implementatiegroep](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Hallo virtuele machines te bevatten.

1. Open Hallo **Releases** tabblad Hallo **bouwen &amp; Release** hub en open Hallo **implementatiegroepen** tabblad en kies **+ nieuw**.

1. Voer een naam voor de groep van Hallo-implementatie, en een optionele beschrijving.
   Kies vervolgens **maken**.

Hello Azure Resource Group Deployment taak maakt en registreert Hallo VM's wanneer deze wordt uitgevoerd met behulp van hello Azure Resource Manager-sjabloon.
U geen toocreate nodig hebt en Hallo virtuele machines uzelf te registreren.

## <a name="create-a-release-definition"></a>Een release-definitie maken

De definitie van een release geeft Hallo proces Team Services toodeploy Hallo app wordt uitgevoerd.
toocreate hello release definitie in Team Services:

1. Open Hallo **Releases** tabblad Hallo **bouwen &amp; Release** hub, open Hallo  **+**  omlaag in de lijst Hallo van release definities en kies Hallo **maken release definitie**. 

1. Selecteer Hallo **leeg** sjabloon en kies **volgende**.

1. In Hallo **artefacten** sectie, klikt u op **koppelen van een artefact** en kies **Jenkins**. Selecteer uw verbinding Jenkins service-eindpunt. Vervolgens selecteert u Hallo Jenkins bron taak en kies **maken**. 

1. In de nieuwe Hallo definitie release, kies **+ taken toevoegen** en voeg een **Azure Resource Group Deployment** taak toohello standaardomgeving.

1. Kies Hallo vervolgkeuzelijst pijl volgende toohello **+ taken toevoegen** koppelen en het toevoegen van een implementatie fase toohello groepsdefinitie.

   ![Toevoegen van een groep implementatiefase](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Open in Hallo taak catalogus Hallo **hulpprogramma** sectie en het toevoegen van een exemplaar van Hallo **Shell-Script** taak.

1. Hallo parameters sjabloon die wordt gebruikt in hello Azure Resource Group Deployment taak stelt Hallo beheerder serverwachtwoord tooconnect toohello virtuele machines.
   U wachtwoord opgeven met de variabele Hallo **$(adminpassword)**:
   
   - Open Hallo **variabelen** tabblad en, in Hallo **variabelen** sectie, voert u de naam van de Hallo `adminpassword`.

   - Hallo beheerderswachtwoord invoeren.

   - Hallo 'hangslot' pictogram volgende toohello waarde textbox tooprotect Hallo wachtwoord kiezen. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Hello Azure Resource Group Deployment taak configureren

Hallo **Azure Resource Group Deployment** taak gebruikte toocreate hello implementatiegroep is. Als volgt configureren:

* **Azure-abonnement:** Selecteer een verbinding in de lijst onder Hallo **beschikbare Azure serviceverbindingen**. 
  Als geen verbindingen worden weergegeven, kiest u **beheren**, selecteer **nieuwe Service-eindpunt** vervolgens **Azure Resource Manager**, en volg de aanwijzingen Hallo.
  Definitie van tooyour release, vernieuwen Hallo retourneren **AzureRM abonnement** lijst, en selecteer Hallo-verbinding die u hebt gemaakt.

* **Resourcegroep**: Voer een naam in van Hallo-resourcegroep die u eerder hebt gemaakt.

* **Locatie**: Selecteer een regio voor Hallo-implementatie.

  ![Een nieuwe resourcegroep maken](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Sjabloonlocatie**:`URL of hello file`

* **Sjabloonkoppeling**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Koppeling van sjabloon parameters**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Sjabloonparameters overschrijven**: een lijst met Hallo onderdrukkingswaarden, bijvoorbeeld: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Voeg in uw eigen specifieke waarden Hallo {tijdelijke aanduidingen}. 

* **Vereiste onderdelen inschakelt**:`Configure with Deployment Group agent`

* **TFS/VSTS eindpunt**: kies **toevoegen** en selecteer in het dialoogvenster 'Nieuw Team Foundation Server-Team Services-verbinding toevoegen' hello **tokenverificatie op basis van**. Voer een naam van de verbinding Hallo en Hallo-URL van uw teamproject. Vervolgens genereren en voer een [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate Hallo verbinding tooyour-teamproject.

  ![Maken van een persoonlijk toegangstoken](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Teamproject**: Selecteer het huidige project.

* **Implementatiegroep**: Voer dezelfde implementatie groepsnaam Hallo als u voor Hallo gebruikt **resourcegroep** parameter.

Hallo standaardinstellingen voor hello Azure Resource Group Deployment taak toocreate zijn of een resource en toodo dus stapsgewijs bijwerken. Hallo taak maakt Hallo VMs Hallo eerste keer wordt uitgevoerd en ze vervolgens net bijwerken.

## <a name="configure-hello-shell-script-task"></a>Hallo shellscript taak configureren

Hallo **Shell-Script** taak gebruikte tooprovide Hallo configuratie voor een script toorun op elke server tooinstall Node.js en start Hallo app is. Als volgt configureren:

* **Pad naar een script**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Geef werkende Directory**:`Checked`

* **Werkmap**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Wijzig de naam en Hallo release definitie op te slaan

1. Bewerken Hallo naam van Hallo release definitie toohello u hebt opgegeven in de **na build acties** tabblad van Hallo build in Jenkins. Jenkins vereist deze naam toobe kunnen tootrigger een nieuwe release wanneer Hallo bron artefacten zijn bijgewerkt.

1. Hallo-naam van Hallo omgeving desgewenst wijzigen door te klikken op Hallo-naam. 

1. Kies **opslaan**, en kies **OK**.

## <a name="start-a-manual-deployment"></a>Start een handmatige implementatie

1. Kies **+ Release** en selecteer **maken Release**.

1. Hallo-build u voltooid Hallo gemarkeerde vervolgkeuzelijst selecteert en kiest **maken**.

1. Kies Hallo release koppeling in het pop-upbericht Hallo. Bijvoorbeeld: ' Release **Release 1** is gemaakt. "

1. Open Hallo **logboeken** tabblad toowatch Hallo release console-uitvoer.

1. Open in uw browser Hallo-URL van een van de servers Hallo u tooyour implementatiegroep toegevoegd. Voer bijvoorbeeld`http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>Start een CI/CD-implementatie

1. Release definitie in hello, schakelt u Hallo **ingeschakeld** checkbox in Hallo **beheeropties** sectie van het Hallo-instellingen voor hello Azure Resource Group Deployment taak.
   Voor toekomstige implementaties toohello bestaande implementatiegroep, hoeft u niet toore-deze taak niet uitvoeren.

1. Ga toohello bron Git-opslagplaats en Hallo inhoud Hallo wijzigen **h1** in de kop van Hallo bestand [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Uw wijzigingen worden doorgevoerd.

1. Na een paar minuten ziet u een nieuwe release gemaakt in Hallo **Releases** pagina van het Team Services of TFS. Open Hallo release toosee Hallo implementatie plaatsvinden. Gefeliciteerd.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt geautomatiseerde u Hallo-implementatie van een app tooAzure met Jenkins build en Team Services voor release. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Uw app in Jenkins maken
> * Jenkins configureren voor integratie met Team Services
> * Een implementatiegroep voor hello Azure virtuele machines maken
> * De definitie van een versie die Hallo VMs configureert en implementeert Hallo-app maken

De volgende zelfstudie toolearn toohello voor vooraf meer informatie over hoe stack is toodeploy een licht (Linux, Apache, MySQL en PHP).

> [!div class="nextstepaction"]
> [LAMP-stack implementeren](tutorial-lamp-stack.md)