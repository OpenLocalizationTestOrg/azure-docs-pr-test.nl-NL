---
title: aaaDeploy Docker-container-cluster in Azure | Microsoft Docs
description: Een oplossing voor Kubernetes, DC/OS of Docker Swarm in Azure Container Service implementeren met behulp van hello Azure-portal of een Resource Manager-sjabloon.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>Implementeert een Docker-container die als host fungeert voor oplossing met behulp van hello Azure-portal



Azure Container Service biedt een snelle implementatie van populaire open-sourceoplossingen voor containerclustering en -orchestration. Dit document begeleidt u bij een Azure Container Service-cluster implementeren met behulp van hello Azure-portal of een snelstartsjabloon met de Azure Resource Manager. 

U kunt ook een Azure Container Service-cluster implementeren met behulp van Hallo [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) of hello Azure Container Service API's.

Zie [Kennismaking met Azure Container Service](../container-service-intro.md) voor achtergrondinformatie.


## <a name="prerequisites"></a>Vereisten

* **Azure-abonnement**: als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). Voor een groter cluster kunt u een Betalen per gebruik-abonnement of andere aanschafopties overwegen.

    > [!NOTE]
    > Het gebruik van uw Azure-abonnement en [resourcequota toe](../../azure-subscription-service-limits.md), zoals kernen quota, Hallo grootte van Hallo cluster die u implementeert kunt beperken. toorequest een verhoging van het quotum, open een [online klant ondersteuningsaanvraag](../../azure-supportability/how-to-create-azure-support-request.md) zonder kosten.
    >

* **Openbare SSH-RSA-sleutel**: bij het implementeren via het Hallo-portal of een van de Azure-snelstartsjablonen hello, moet u tooprovide Hallo openbare sleutel voor verificatie met een Azure Container Service virtuele machines. toocreate Secure Shell (SSH) RSA-sleutels, Zie Hallo [OS X- en Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../../virtual-machines/linux/ssh-from-windows.md) richtlijnen. 

* **Service-principal client-ID en geheim** (alleen Kubernetes): Zie voor meer informatie over en richtlijnen toocreate een Azure Active Directory-service-principal, [over service-principal voor een cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Maken van een cluster met behulp van hello Azure-portal
1. Aanmelden toohello Azure-portal, selecteer **nieuw**, en zoek hello Azure Marketplace voor **Azure Container Service**.

    ![Azure Container Service in Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. Klik op **Azure Container Service** en klik op **Create**.

3. Op Hallo **basisbeginselen** blade Voer Hallo volgende informatie:

    * **Orchestrator**: Selecteer een van de Hallo container orchestrators toodeploy op Hallo-cluster.
        * **DC/OS**: implementeert een DC/OS-cluster.
        * **Swarm**: implementeert een Docker Swarm-cluster.
        * **Kubernetes**: implementeert een Kubernetes-cluster.
    * **Subscription**: selecteer een Azure-abonnement.
    * **Resourcegroep**: Hallo-naam van een nieuwe resourcegroep voor Hallo-implementatie.
    * **Locatie**: Selecteer een Azure-regio voor hello Azure Container Service-implementatie. Raadpleeg voor beschikbaarheid, [Beschikbare producten per regio](https://azure.microsoft.com/regions/services/).
    
    ![Basisinstellingen](./media/container-service-deployment/acs-portal3.png)  <br />
    
    Klik op **OK** wanneer u bent klaar tooproceed.

4. Op Hallo **de hoofdsleutel van de configuratie** blade Voer Hallo-instellingen voor Linux-hoofdknooppunt Hallo of knooppunten in het Hallo-cluster (sommige instellingen zijn specifiek tooeach orchestrator) te volgen:

    * **Basispagina-DNS-naam**: Hallo voorvoegsel gebruikt toocreate een unieke volledig gekwalificeerde domeinnaam (FQDN) voor Hallo master. Hallo master FQDN-naam van het formulier Hallo is *voorvoegsel*beheergegevens*locatie*. cloudapp.azure.com.
    * **Gebruikersnaam**: Hallo gebruikersnaam op voor een account op elk Hallo Linux virtuele machines in Hallo-cluster.
    * **Openbare SSH-RSA-sleutel**: Hallo openbare sleutel toobe gebruikt voor verificatie met een virtuele Linux-machines Hallo toevoegen. Het is belangrijk dat deze sleutel geen regeleinden bevat en het Hallo omvat `ssh-rsa` voorvoegsel. Hallo `username@domain` postfix is optioneel. Hallo sleutel moet er ongeveer als volgende Hallo: **ssh-rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** . 
    * **Service-principal**: als u Hallo Kubernetes orchestrator hebt geselecteerd, voert u een Azure Active Directory **Service-principal client-ID** (ook wel Hallo appId) en **geheim voor Service-principal client** (wachtwoord). Zie voor meer informatie [over service-principal voor een cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).
    * **De hoofdsleutel van de count**: Hallo aantal masters in het Hallo-cluster.
    * **VM diagnostics**: voor sommige orchestrators, kunt u VM diagnostics op Hallo masters inschakelen.

    ![Master configuration](./media/container-service-deployment/acs-portal4.png)  <br />

    Klik op **OK** wanneer u bent klaar tooproceed.

5. Op Hallo **agentconfiguratie** blade Voer Hallo volgende informatie:

    * **Aantal agents**: voor Docker Swarm en Kubernetes, is deze waarde Hallo kunt u het oorspronkelijke aantal agents in de agentschaalset Hallo. Voor DC/OS is het oorspronkelijke aantal agents in een persoonlijke schaalset Hallo. Bovendien wordt een openbare schaalset gemaakt voor DC/OS, die een vooraf bepaald aantal agents bevat. Hallo is aantal agents in deze openbare schaalsets bepaald door het aantal masters in het cluster Hallo Hallo: één openbare agent voor een model en twee openbare agents voor drie of 5 masters.
    * **De grootte van de virtuele machine agent**: Hallo grootte van Hallo agent virtuele machines.
    * **Besturingssysteem**: deze instelling is momenteel alleen beschikbaar als u Hallo Kubernetes orchestrator geselecteerd. Kies een Linux-distributie of een toorun van het besturingssysteem Windows Server op Hallo agents. Op basis van deze instelling wordt bepaald of op het cluster Linux- of Windows-container-apps kunnen worden uitgevoerd. 

        > [!NOTE]
        > Ondersteuning voor Windows-containers bevindt zich voor Kubernetes-clusters nog in de preview-fase. Op DC/OS- en Swarm-clusters worden momenteel alleen Linux-agents ondersteund in Azure-Container Service.

    * **Agentreferenties**: als u de Windows-besturingssysteem Hallo hebt geselecteerd, voert u een beheerder **gebruikersnaam** en **wachtwoord** voor Hallo agent virtuele machines. 

    ![Agent configuration](./media/container-service-deployment/acs-portal5.png)  <br />

    Klik op **OK** wanneer u bent klaar tooproceed.

6. Klik op **OK** nadat de servicevalidatie is voltooid.

    ![Validatie](./media/container-service-deployment/acs-portal6.png)  <br />

7. Hallo rwaarden. implementatieproces toostart hello, klikt u op **maken**.

    Als u toopin Hallo implementatie toohello Azure-portal hebt gekozen, ziet u de implementatiestatus Hallo.

    ![Implementatiestatus](./media/container-service-deployment/acs-portal8.png)  <br />

Hallo implementatie duurt enkele minuten toocomplete. Hello Azure Container Service-cluster is klaar voor gebruik.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>Een cluster maken met het snelstartsjabloon
Azure-snelstartsjablonen zijn beschikbaar toodeploy een cluster in Azure Container Service. Hallo opgegeven Quick Start-sjablonen kunnen worden gewijzigd tooinclude extra of geavanceerde configuratie van Azure. een Azure Container Service-cluster met behulp van een sjabloon voor de Azure quickstart toocreate, moet u een Azure-abonnement. Als u er geen hebt, kunt u zich [registreren voor een gratis proefversie](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). 

Volg deze stappen toodeploy een cluster met een sjabloon en Azure CLI 2.0 Hallo (Zie [installatie en configuratie-instructies](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Als u van een Windows-systeem gebruikmaakt, kunt u dezelfde stappen toodeploy een sjabloon met Azure PowerShell. De stappen worden verderop in dit gedeelte beschreven. U kunt ook een sjabloon via Hallo implementeren [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) of andere methoden.

1. toodeploy een DC/OS, Docker Swarm of Kubernetes-cluster, selecteer een van Hallo beschikbaar Quick Start-sjablonen in GitHub. Hierna volgt een gedeeltelijke lijst. Hello DC/OS- en Swarm-sjablonen zijn hetzelfde, behalve de standaardselectie voor orchestrator Hallo Hallo.

    * [DC/OS-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Meld u bij tooyour Azure-account (`az login`), en zorg ervoor dat hello Azure CLI is verbonden tooyour Azure-abonnement. Hallo standaardabonnement kunt u met behulp van de volgende opdracht Hallo zien:

    ```azurecli
    az account show
    ```
    
    Als u meer dan één abonnement en de noodzaak tooset op een andere standaard-abonnement hebt, voert u `az account set --subscription` en Hallo abonnements-ID of naam opgeven.

3. Een aanbevolen procedure is om een nieuwe resourcegroep voor Hallo-implementatie te gebruiken. een resourcegroep toocreate gebruiken Hallo `az group create` opdracht een naam van een resourcegroep en locatie opgeven: 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. Maak een JSON-bestand met Hallo vereiste sjabloon parameters. Download Hallo parameterbestand met de naam `azuredeploy.parameters.json` die wordt meegestuurd met hello Azure Container Service-sjabloon `azuredeploy.json` in GitHub. Voer de vereiste parameterwaarden voor uw cluster. 

    Bijvoorbeeld: toouse hello [DC/OS-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), parameterwaarden worden doorgegeven voor `dnsNamePrefix` en `sshRSAPublicKey`. Zie de beschrijvingen van Hallo in `azuredeploy.json` en opties voor andere parameters.  
 

5. Een Container Service-cluster maken bestand door te geven Hallo implementatie parameters Hello volgende opdracht, waarbij:

    * **RESOURCE_GROUP** Hallo-naam van resourcegroep Hallo die u hebt gemaakt in de vorige stap Hallo is.
    * **DEPLOYMENT_NAME** (optioneel) Dit is een naam toohello-implementatie.
    * **TEMPLATE_URI** Hallo-locatie van het implementatiebestand Hallo `azuredeploy.json`. Deze URI moet Hallo Raw-bestand niet de toohello van een wijzer GitHub UI. toofind deze URI, selecteer Hallo `azuredeploy.json` bestand in GitHub en op Hallo **Raw** knop.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    U kunt ook parameters opgeven als een tekenreeks JSON-indeling op Hallo-opdrachtregel. U kunt een opdracht vergelijkbare toohello volgt:

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > Hallo implementatie duurt enkele minuten toocomplete.
    > 

### <a name="equivalent-powershell-commands"></a>Vergelijkbare PowerShell-opdrachten
U kunt een Azure Container Service-clustersjabloon ook implementeren met PowerShell. Dit document is gebaseerd op Hallo versie 1.0 [Azure PowerShell-module](https://azure.microsoft.com/blog/azps-1-0/).

1. toodeploy een DC/OS, Docker Swarm of Kubernetes-cluster, selecteer een van Hallo beschikbaar Quick Start-sjablonen in GitHub. Hierna volgt een gedeeltelijke lijst. Opmerking dat hello DC/OS- en Swarm-sjablonen zijn Hallo dezelfde zijn, met uitzondering van de standaardselectie voor orchestrator Hallo Hallo.

    * [DC/OS-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Controleer of uw PowerShell-sessie in tooAzure is ondertekend voordat het maken van een cluster in uw Azure-abonnement. U kunt dit doen met Hallo `Get-AzureRMSubscription` opdracht:

    ```powershell
    Get-AzureRmSubscription
    ```

3. Als u toosign in tooAzure moet, gebruikt u Hallo `Login-AzureRMAccount` opdracht:

    ```powershell
    Login-AzureRmAccount
    ```

4. Een aanbevolen procedure is om een nieuwe resourcegroep voor Hallo-implementatie te gebruiken. een resourcegroep toocreate gebruiken Hallo `New-AzureRmResourceGroup` opdracht in en geef een naam en doel-regio voor de groep voor resource:

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. Nadat u een resourcegroep hebt gemaakt, kunt u uw cluster maken met de volgende opdracht Hallo. Hallo-URI van Hallo gewenste sjabloon wordt opgegeven met de Hallo `-TemplateUri` parameter. Wanneer u deze opdracht uitvoert, vraagt PowerShell u de parameterwaarden voor de implementatie op te geven.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>Sjabloonparameters opgeven
Als u bekend met PowerShell bent, weet u dat u door de beschikbare parameters voor een cmdlet Hallo bladeren kunt met een minteken (-) te typen en vervolgens op Hallo TAB-toets te drukken. Dezelfde functionaliteit werkt ook met parameters die u in de sjabloon definieert. Zodra u de sjabloonnaam Hallo typt, Hallo-cmdlet haalt Hallo sjabloon parseert Hallo parameters en Hallo sjabloon parameters toohello opdracht dynamisch worden toegevoegd. Dit maakt het eenvoudig toospecify Hallo sjabloonparameterwaarden. En als u een waarde van de vereiste parameter bent vergeten, vraagt PowerShell u om Hallo-waarde.

Hier volgt de volledige opdracht Hallo met parameters die zijn opgenomen. Geef uw eigen waarden voor Hallo namen van Hallo resources.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>Volgende stappen
Nu u een werkend cluster hebt, kunt u deze documenten lezen voor meer informatie over verbinding en beheer:

* [Verbinding maken met tooan Azure Container Service-cluster](../container-service-connect.md)
* [Werken met de Azure Container Service en DC/OS](container-service-mesos-marathon-rest.md)
* [Werken met de Azure Container Service en Docker Swarm](container-service-docker-swarm.md)
* [Werken met de Azure Container Service en Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)
