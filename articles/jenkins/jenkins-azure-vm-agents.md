---
title: voor continue integratie met Jenkins aaaUse Azure VM-agents.
description: Azure VM-agents als Jenkins-slaves.
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Azure VM-agents gebruiken voor continue integratie met Jenkins

Deze snelstartgids ziet u hoe toouse Hallo Jenkins Azure VM Agents invoegtoepassing toocreate een agent op aanvraag Linux (Ubuntu) in Azure.

## <a name="prerequisites"></a>Vereisten

toocomplete deze snelstartgids:

* Als u nog geen een model Jenkins, kunt u beginnen met Hallo [oplossingssjabloon](install-jenkins-solution-template.md) 
* Raadpleeg te[een Azure-Service-principal maken met Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) als u nog geen een Azure-service-principal.

## <a name="install-azure-vm-agents-plugin"></a>Azure VM Agents-invoegtoepassing installeren

Als u vanaf Hallo [oplossingssjabloon](install-jenkins-solution-template.md), hello Azure VM-Agent-invoegtoepassing is geïnstalleerd in de Hallo Jenkins master.

Anders installeert Hallo **Azure VM Agents** invoegtoepassing uit binnen Hallo Jenkins dashboard.

## <a name="configure-hello-plugin"></a>Hallo-invoegtoepassing configureren

* Klik in het Hallo Jenkins dashboard op **Jenkins beheren -> systeem configureren ->**. Schuif toohello onder aan de pagina Hallo en Hallo sectie met Hallo dropdown zoeken **toevoegen van nieuwe cloud**. Hallo-menu en selecteer **Microsoft Azure VM-Agents**
* Selecteer een bestaand account in hello Azure-referenties vervolgkeuzelijst.  tooadd een nieuwe **Microsoft Azure Service-Principal** Hallo waarden volgende invoeren: abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt.

![Azure-referenties](./media/jenkins-azure-vm-agents/service-principal.png)

* Klik op **controleren configuratie** toomake of die Hallo profielconfiguratie juist is.
* Hallo-configuratie op te slaan en verder toohello volgende stap.

## <a name="template-configuration"></a>Sjabloonconfiguratie

### <a name="general-configuration"></a>Algemene configuratie
Configureer vervolgens een sjabloon voor gebruik toodefine een Azure VM-agent. 

* Klik op **toevoegen** tooadd een sjabloon. 
* Geef een naam op voor de nieuwe sjabloon. 
* Voer voor Hallo-label "ubuntu." Dit label wordt gebruikt tijdens het Hallo taak configureren.
* Selecteer de gewenste regio Hallo in Hallo keuzelijst met invoervak.
* Selecteer Hallo gewenste VM-grootte.
* Geef hello Azure Storage-accountnaam of laat dit leeg toouse Hallo standaardnaam 'jenkinsarmst'.
* Geef de bewaartijd Hallo in minuten. Deze instelling bepaalt Hallo aantal minuten die jenkins wachten kunt voordat u een niet-actieve agent automatisch worden verwijderd. Geef 0 als u niet dat niet-actieve agents toobe automatisch verwijderd wilt.

![Algemene configuratie](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Configuratie van installatiekopie

Selecteer toocreate (Ubuntu) Linux-agent **verwijzing afbeelding** en gebruik Hallo configuratie als een voorbeeld te volgen. Raadpleeg te[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) voor Hallo meest recente Azure installatiekopieën ondersteund.

* Image Publisher: Canonical
* Image Offer: UbuntuServer
* Image Sku: 14.04.5-LTS
* Image Version: latest
* OS Type: Linux
* Launch Method: SSH
* Voer referenties van een beheerder in
* Voer het volgende in voor het script voor de initialisatie van virtuele machines:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuratie van installatiekopie](./media/jenkins-azure-vm-agents/image-config.png)

* Klik op **sjabloon controleren** tooverify Hallo configuratie.
* Klik op **Opslaan**.

## <a name="create-a-job-in-jenkins"></a>Een taak maken in Jenkins

* Klik in het Hallo Jenkins dashboard op **Nieuw Item**. 
* Voer een naam in, selecteer **Freestyle project** en klik op **OK**.
* In Hallo **algemene** tabblad, selecteer 'Beperken waar project kan worden uitgevoerd' en het type 'ubuntu' in de Label-expressie. U ziet nu 'ubuntu' hello vervolgkeuzelijst.
* Klik op **Opslaan**.

![Een taak instellen](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Het nieuwe project bouwen

* Ga terug toohello Jenkins dashboard.
* Klik met de rechtermuisknop Hallo nieuwe taak die u hebt gemaakt, klikt u op **nu samenstellen**. De bewerking wordt gestart. 
* Zodra de Hallo build is voltooid, gaat u te**Console uitvoer**. U ziet Hallo build op afstand is uitgevoerd op Azure.

![Console-uitvoer](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Naslaginformatie

* Video van Azure Friday: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Continue integratie met Jenkins met behulp van Azure VM-agents)
* Ondersteuningsinformatie en configuratie-opties: de Engelstalige wiki van Jenkins [Azure VM Agents plugin](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

