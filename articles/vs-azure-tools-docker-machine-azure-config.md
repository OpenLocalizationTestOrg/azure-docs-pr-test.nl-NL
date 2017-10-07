---
title: aaaCreate Docker-hosts in Azure met Docker-Machine | Microsoft Docs
description: Beschrijving van de Docker-Machine toocreate docker-hosts in Azure.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Docker-hosts in Azure maken met Docker-Machine
Met [Docker](https://www.docker.com/) containers vereist een host VM actieve Hallo docker-daemon.
Dit onderwerp wordt beschreven hoe toouse hello [docker-machine](https://docs.docker.com/machine/) opdracht toocreate nieuwe Linux-VM's geconfigureerd met Hallo Docker-daemon worden uitgevoerd in Azure. 

**Opmerking:** 

* *In dit artikel hangt samen met docker-machine versie 0.9.0-rc2 of hoger*
* *Windows-Containers worden ondersteund via de docker-machine in Hallo nabije toekomst*

## <a name="create-vms-with-docker-machine"></a>Virtuele machines met Docker-Machine maken
Docker host virtuele machines in Azure maken met de Hallo `docker-machine create` opdracht met Hallo `azure` stuurprogramma. 

Hello Azure stuurprogramma is vereist voor uw abonnement-ID. U kunt Hallo [Azure CLI](cli-install-nodejs.md) of Hallo [Azure Portal](https://portal.azure.com) tooretrieve uw Azure-abonnement. 

**Met behulp van hello Azure Portal**

* Selecteer **abonnementen** van Hallo linkernavigatievenster pagina en kopieer Hallo abonnement-id.

**Hello Azure CLI gebruiken**

* Type ```azure account list``` en kopiëren Hallo abonnements-id.

Type `docker-machine create --driver azure` toosee Hallo opties en hun standaardwaarden.
U ziet ook Hallo [Docker Azure stuurprogramma documentatie](https://docs.docker.com/machine/drivers/azure/) voor meer informatie. 

Hallo volgende voorbeeld is afhankelijk van Hallo [standaardwaarden](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), maar eventueel deze waarden ingesteld: 

* Azure dns voor Hallo-naam die is gekoppeld aan de openbare IP-adres Hallo en certificaten die zijn gegenereerd. Dit is Hallo DNS-naam van uw virtuele machine. Hallo VM kan vervolgens veilig stoppen, vrijgeven Hallo dynamische IP en Hallo mogelijkheid tooreconnect nadat Hallo vm wordt opnieuw met een nieuwe IP-adres gestart opgeven. Hallo-voorvoegsel moet uniek zijn voor deze regio UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Open poort 80 op Hallo VM voor uitgaande internetverbinding
* grootte van Hallo VM tooutilize sneller premium-opslag
* Premium-opslag gebruikt voor Hallo vm-schijf

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Kies een host docker met docker-machine
Zodra u een vermelding in de docker-machine voor de host hebt, kunt u Hallo standaardhost kunt instellen wanneer docker opdrachten uit te voeren.

## <a name="using-powershell"></a>PowerShell gebruiken
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Met behulp van Bash
```bash
eval $(docker-machine env MyDockerHost)
```

U kunt nu docker-opdrachten uitvoeren op de opgegeven host Hallo

```
docker ps
docker info
```

## <a name="run-a-container"></a>Een container worden uitgevoerd
U kunt nu een eenvoudige web server tootest uitvoeren met een host die is geconfigureerd, of de host correct is geconfigureerd.
Hier wordt een installatiekopie van het standaard nginx gebruiken, geeft u het moet luisteren op poort 80, en als Hallo host VM opnieuw wordt opgestart, wordt de container Hallo wordt opnieuw gestart ook (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hallo-uitvoer ziet er ongeveer als Hallo volgende:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Test Hallo container
Bekijk actieve containers met `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

En toosee Hallo-container, type uitgevoerd `docker-machine ip <VM name>` toofind Hallo IP-adres tooenter in Hallo browser:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Actieve ngnix container](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Samenvatting
U kunt eenvoudig docker-hosts in Azure voor uw afzonderlijke docker host validaties met docker-machine inrichten.
Voor productie Hallo hosting van containers, Zie [Azure Container Service](http://aka.ms/AzureContainerService)

toodevelop .NET Core-toepassingen met Visual Studio, Zie [Docker-Tools voor Visual Studio](http://aka.ms/DockerToolsForVS)

