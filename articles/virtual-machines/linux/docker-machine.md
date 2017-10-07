---
title: aaaUse Docker-Machine toocreate Linux wordt gehost in Azure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Docker-Machine toocreate Docker-hosts in Azure.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Hoe toouse Docker-Machine toocreate gehost in Azure
Dit artikel details hoe toouse [Docker-Machine](https://docs.docker.com/machine/) toocreate hosts in Azure. Hallo `docker-machine` opdracht maakt u een Linux-virtuele machine (VM) in Azure vervolgens Docker geïnstalleerd. U kunt uw Docker-hosts in het gebruik van Azure beheren Hallo dezelfde lokale hulpprogramma's en werkstromen.

## <a name="create-vms-with-docker-machine"></a>Virtuele machines met Docker-Machine maken
Eerst moet u uw Azure-abonnement-ID met [az account weergeven](/cli/azure/account#show) als volgt:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Maken van virtuele machines Docker-host in Azure met `docker-machine create` door te geven *azure* als Hallo-stuurprogramma. Zie voor meer informatie, Hallo [Docker Azure stuurprogramma-documentatie](https://docs.docker.com/machine/drivers/azure/)

Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*, maakt u een gebruikersaccount met de naam *azureuser*, en poort geopend *80* hosten op Hallo VM. Volg alle prompts toolog in tooyour Azure-account en Docker-Machine machtigingen toocreate verlenen en beheren van resources.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>De Docker-shell configureren
tooconnect tooyour Docker-host in Azure, de juiste verbindingsinstellingen Hallo definiëren. Zoals eerder aan Hallo einde van Hallo uitvoer, als volgt Hallo verbindingsgegevens voor de Docker-host weergeven: 

```bash
docker-machine env myvmdocker
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

Hallo-verbindingsinstellingen voor de toodefine kunt u beide uitvoeren Hallo voorgestelde configuratieopdracht (`eval $(docker-machine env myvmdocker)`), of u kunt de omgevingsvariabelen Hallo handmatig instellen. 

## <a name="run-a-container"></a>Een container worden uitgevoerd
toosee een container in actie, kunt een eenvoudige NGINX-webserver uitgevoerd. Maken van een container met `docker run` en weer te geven van poort 80 voor internetverkeer als volgt:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Weergave actieve containers met `docker ps`. Hallo volgende voorbeelduitvoer wordt weergegeven Hallo NGINX-container met met poort 80 weergegeven:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Test Hallo container
Hallo openbaar IP-adres van Docker-host als volgt verkrijgen:


```bash
docker-machine ip myvmdocker
```

toosee hello container in actie, open een webbrowser en Voer Hallo openbare IP-adres hebt genoteerd in Hallo-uitvoer van de voorgaande opdracht Hallo:

![Actieve ngnix container](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Volgende stappen
U kunt ook hosts maken met de Hallo [Docker VM-extensie](dockerextension.md). Zie voor voorbeelden op met behulp van Docker Compose [aan de slag met Docker en opstellen in Azure](docker-compose-quickstart.md).
