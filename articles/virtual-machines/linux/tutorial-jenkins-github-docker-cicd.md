---
title: een pijplijn ontwikkeling in Azure met Jenkins aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Jenkins virtuele machine in Azure dat worden vanuit GitHub op elke code doorvoeren en een nieuwe Docker-container toorun builds uw app
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Hoe een ontwikkeling infrastructuur op een Linux-VM in Azure met Jenkins, GitHub en Docker toocreate
tooautomate Hallo build en fase testen van de ontwikkeling van toepassingen, kunt u een continue integratie en implementatie (CI/CD) pijplijn. In deze zelfstudie maakt u een pijplijn CI/CD maken op een virtuele machine in Azure met inbegrip van hoe:

> [!div class="checklist"]
> * Maak een VM Jenkins
> * Installeren en configureren van Jenkins
> * Webhook-integratie tussen GitHub en Jenkins maken
> * Maken en activeren Jenkins build taken van GitHub doorvoeringen
> * Een Docker-installatiekopie voor uw app maken
> * Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Jenkins exemplaar maken
In een vorige zelfstudie over [hoe een virtuele Linux-machine op de eerste keer opstarten toocustomize](tutorial-automate-vm-deployment.md), u leert hoe tooautomate VM aanpassing met cloud-init. Deze zelfstudie maakt gebruik van een cloud-init bestand tooinstall Jenkins en Docker op een virtuele machine. 

Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie. Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken. Voer `sensible-editor cloud-init-jenkins.txt` toocreate Hallo bestand en een overzicht van beschikbare editors. Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupJenkins* in Hallo *eastus* locatie:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create). Gebruik Hallo `--custom-data` parameter toopass in uw cloud-init-configuratiebestand. Volledig pad hello te bieden*cloud-init-jenkins.txt* als Hallo bestand buiten de huidige werkmap is opgeslagen.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Het duurt enkele minuten duren voordat Hallo VM toobe gemaakt en geconfigureerd.

virtuele machine, gebruik van web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port) tooopen poort *8080* voor Jenkins verkeer en poort *1337* voor Hallo Node.js-app die is gebruikt toorun een voorbeeld-app:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Jenkins configureren
tooaccess uw Jenkins exemplaar, Hallo openbare IP-adres van uw virtuele machine verkrijgen:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Uit veiligheidsoverwegingen moet u tooenter Hallo initiële beheerderswachtwoord die is opgeslagen in een tekstbestand op uw VM toostart hello die jenkins installeren. Hallo openbare IP-adres verkregen in Hallo vorige stap tooSSH tooyour VM gebruiken:

```bash
ssh azureuser@<publicIps>
```

Weergave Hallo `initialAdminPassword` voor uw Jenkins installeren en dit te kopiëren:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Als het Hallo-bestand is nog niet beschikbaar, wacht u enkele minuten voor cloud-init toocomplete hello Jenkins en Docker-installatie.

Nu open een webbrowser en ga te`http://<publicIps>:8080`. Voer Hallo initiële Jenkins setup als volgt:

- Voer Hallo *initialAdminPassword* verkregen van Hallo VM in de vorige stap Hallo.
- Klik op **plugins tooinstall selecteren**
- Zoeken naar *GitHub* selecteren in het tekstvak Hallo Hallo bovenaan, Hallo *GitHub-invoegtoepassing*, klikt u vervolgens op **installeren**
- een gebruikersaccount Jenkins toocreate Hallo-formulier naar wens invullen. Vanuit beveiligingsoogpunt, moet u deze eerste Jenkins-gebruiker in plaats van u doorgaat als Hallo standaard admin-account maken.
- Wanneer u klaar bent, klikt u op **Jenkins gebruiken**


## <a name="create-github-webhook"></a>GitHub webhook maken
tooconfigure hello integratie met GitHub, open Hallo [Node.js Hallo wereld-voorbeeld-app](https://github.com/Azure-Samples/nodejs-docs-hello-world) uit hello Azure-voorbeelden opslagplaats. toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.

Maak een webhook binnen Hallo fork die u hebt gemaakt:

- Klik op **instellingen**, selecteer daarna **integraties & services** aan de linkerkant Hallo.
- Klik op **service toevoegen**, voer dan *Jenkins* in het filtervak.
- Selecteer *Jenkins (GitHub-invoegtoepassing)*
- Voor Hallo **Jenkins hook URL**, voer `http://<publicIps>:8080/github-webhook/`. Zorg ervoor dat u hallo afsluitende /
- Klik op **service toevoegen**

![GitHub-repo-webhook tooyour forked toevoegen](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Jenkins taak maken
toohave Jenkins reageren tooan gebeurtenis in GitHub zoals het vastleggen van de code wordt een taak Jenkins maken. 

Klik op in uw website Jenkins **nieuwe taken maken** vanaf de startpagina Hallo:

- Voer *HelloWorld* als de taaknaam van de. Kies **Freestyle project**, selecteer daarna **OK**.
- Onder Hallo **algemene** sectie **GitHub** project en voer uw Gevorkte repo-URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Onder Hallo **Source code management** sectie **Git**, Voer uw Gevorkte opslagplaats *.git* -URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Onder Hallo **bouwen Triggers** sectie **GitHub haakje trigger voor GITscm polling**.
- Onder Hallo **bouwen** sectie **toevoegen build stap**. Selecteer **shell uitvoeren**, voer dan `echo "Testing"` toocommand-venster.
- Klik op **opslaan** aan Hallo onderkant van het venster taken Hallo.


## <a name="test-github-integration"></a>Integratie van GitHub testen
tootest hello GitHub-integratie met Jenkins, een wijziging in uw fork doorvoeren. 

Terug in de GitHub-webgebruikersinterface, selecteer uw Gevorkte opslagplaats en klik vervolgens op Hallo **index.js** bestand. Klik op Hallo pen pictogram tooedit dit bestand zodat de regel 6 leest:

```nodejs
response.end("Hello World!");
```

toocommit uw wijzigingen, klikt u op Hallo **wijzigingen doorvoeren** knop Hallo onder aan.

Een nieuwe build begint in Jenkins, onder Hallo **bouwen geschiedenis** sectie van de linkerbenedenhoek van de pagina van de taak Hallo. Klik op de koppeling van Hallo build en selecteer **Console uitvoer** op Hallo links grootte. U kunt bekijken Hallo stappen Jenkins wordt als uw code wordt opgehaald uit GitHub en Hallo build actie uitvoer Hallo-bericht `Testing` toohello-console. Telkens wanneer een doorvoer wordt gedaan in GitHub webhook hello tooJenkins gezocht en activeren van een nieuwe build op deze manier.


## <a name="define-docker-build-image"></a>Afbeelding van Docker-build definiëren
toosee hello Node.js-app uitgevoerd op basis van uw GitHub-doorvoeracties kunt bouwen van een Docker-afbeelding toorun Hallo app. Hallo-installatiekopie wordt gemaakt van een Dockerfile die definieert hoe tooconfigure Hallo-container die Hallo app uitvoert. 

Wijzigen van Hallo SSH-verbinding tooyour VM toohello Jenkins werkruimte map na Hallo-taak die u in de vorige stap hebt gemaakt. In ons voorbeeld die heette *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Maken van een bestand met de in deze map werkruimte met `sudo sensible-editor Dockerfile` en inhoud te plakken Hallo volgen. Zorg ervoor dat Hallo die hele Dockerfile is correct, met name Hallo eerste regel gekopieerd:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Deze Dockerfile gebruikt Hallo Node.js basisinstallatiekopie gebruik Alpine Linux, zichtbaar gemaakt poort 1337 die app Hallo wereld Hallo wordt uitgevoerd op, en vervolgens kopieert Hallo app-bestanden en geïnitialiseerd met behulp van.


## <a name="create-jenkins-build-rules"></a>Jenkins build regels maken
In de vorige stap, moet u een basic Jenkins build regel die een bericht toohello console uitvoeren gemaakt. Hiermee kunt Hallo build stap toouse onze Dockerfile maken en uitvoeren van Hallo-app.

Selecteer terug in uw exemplaar Jenkins Hallo-taak die u in de vorige stap hebt gemaakt. Klik op **configureren** op Hallo linkerkant en schuif omlaag toohello **bouwen** sectie:

- Verwijder de bestaande `echo "Test"` stap bouwen. Klik op Hallo rode kruislings op Hallo rechterbovenhoek van Hallo bestaande build stap box.
- Klik op **toevoegen build stap**, selecteer daarna **shell uitvoeren**
- In Hallo **opdracht** vak, Voer Hallo Docker-opdrachten te volgen en selecteer **opslaan**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

Hallo Docker build stappen maakt een installatiekopie en de tag met Hallo Jenkins build-nummer zodat u kunt een geschiedenis van installatiekopieën onderhouden. Eventuele bestaande containers Hallo app uitgevoerd worden gestopt en verwijderd. Een nieuwe container wordt gestart met behulp van de installatiekopie Hallo en voert u uw Node.js-app op basis van de meest recente doorvoeracties Hallo in GitHub.


## <a name="test-your-pipeline"></a>Test uw pijplijn
toosee hello hele pijplijn in actie bewerken Hallo *index.js* bestand in uw GitHub-repo-Gevorkte opnieuw en klik op **wijziging doorvoeren**. Een nieuwe taak wordt gestart met Jenkins op basis van de webhook Hallo voor GitHub. Het duurt enkele seconden toocreate hello Docker installatiekopie en uw app te starten in een nieuwe container.

Indien nodig, opnieuw Hallo openbare IP-adres van uw virtuele machine verkrijgen:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Open een webbrowser en voer `http://<publicIps>:1337`. Uw Node.js-app wordt weergegeven en reflecteert de meest recente doorvoeracties Hallo in uw GitHub-fork als volgt:

![Actieve Node.js-app](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Maak nu een andere bewerken toohello *index.js* bestand in GitHub en doorvoeren Hallo wijzigen. Wacht een paar seconden voor Hallo taak toocomplete in Jenkins en vernieuw vervolgens uw web browser toosee Hallo bijgewerkt versie van uw app uitgevoerd in een nieuwe container als volgt:

![Node.js-app uitgevoerd na een ander GitHub doorvoeren](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie GitHub toorun een taak van de build Jenkins geconfigureerd op elke doorvoer code en vervolgens uw app implementeert een Docker-container tootest. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Maak een VM Jenkins
> * Installeren en configureren van Jenkins
> * Webhook-integratie tussen GitHub en Jenkins maken
> * Maken en activeren Jenkins build taken van GitHub doorvoeringen
> * Een Docker-installatiekopie voor uw app maken
> * Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates

Gaan de volgende zelfstudie toolearn toohello meer informatie over hoe toointegrate Jenkins met Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Apps implementeren met Jenkins en teamservices](tutorial-build-deploy-jenkins.md)