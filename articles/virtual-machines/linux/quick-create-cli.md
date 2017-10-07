---
title: Quick Start - aaaAzure maken VM CLI | Microsoft Docs
description: Snel meer toocreate virtuele machines met hello Azure CLI.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Een virtuele Linux-machine maken met hello Azure CLI

Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. Deze handleiding details hello Azure CLI toodeploy met een virtuele machine met Ubuntu server. Zodra Hallo-server is geïmplementeerd, een SSH-verbinding wordt gemaakt en een NGINX-webserver is geïnstalleerd.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Virtuele machine maken

Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht. 

Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* en SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel. toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. Let op Hallo `publicIpAddress`. Dit adres is gebruikte tooaccess Hallo VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Poort 80 openen voor webverkeer 

Standaard worden alleen SSH-verbindingen toegestaan naar virtuele Linux-machines die zijn geïmplementeerd in Azure. Als deze virtuele machine wordt toobe een webserver, moet u tooopen poort 80 van Hallo Internet. Gebruik Hallo [az vm open poort](/cli/azure/vm#open-port) opdracht tooopen Hallo gewenst poort.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>SSH in uw virtuele machine

Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine. Zorg ervoor dat tooreplace  *<publicIpAddress>*  Hello Corrigeer openbare IP-adres van uw virtuele machine.  In ons voorbeeld hierboven was *40.68.254.142* ons IP-adres.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>NGINX installeren

Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Hallo-NGINX welkomstpagina weergeven

U kunt een webbrowser van uw keuze tooview hello NGINX standaardwelkomstpagina gebruiken van NGINX geïnstalleerd en de poort 80 is nu open op de virtuele machine van de Internet - Hallo. Ervoor toouse Hallo worden *publicIpAddress* u hiervoor toovisit Hallo standaardpagina beschreven. 

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd. toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.


> [!div class="nextstepaction"]
> [Zelfstudies over virtuele Linux-machines](./tutorial-manage-vm.md)
