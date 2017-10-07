---
title: aaaFile share voor Azure DC/OS-cluster | Microsoft Docs
description: Maken en koppelen van een bestandsshare tooa DC/OS-cluster in Azure Container Service
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Mesos, Azure, bestandsshare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Maken en koppelen van een bestandsshare tooa DC/OS-cluster
Deze zelfstudie wordt beschreven hoe toocreate een bestand delen in Azure en dit koppelen op elke agent en de hoofdserver van DC/OS-cluster Hallo. Instellen van een bestandsshare maakt het eenvoudiger tooshare bestanden in uw cluster, zoals configuratie, toegang en Logboeken. Hallo taken te volgen zijn in deze zelfstudie voltooid:

> [!div class="checklist"]
> * Een Azure-opslagaccount maken
> * Een bestandsshare maken
> * Hallo-share in Hallo DC/OS-cluster koppelen

U moet een ACS DC/OS cluster toocomplete Hallo in deze zelfstudie stappen. Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Een bestandsshare maken in Microsoft Azure

Voordat u een Azure-bestandsshare met een ACS-DC/OS-cluster, moet de Hallo storage-account en bestandsshare worden gemaakt. Voer Hallo script toocreate Hallo opslag en bestandsshare te volgen. Hallo parameters bijwerken met thoes uit uw omgeving.

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>Hallo-share in het cluster koppelen

Hallo-bestandsshare vervolgens behoeften toobe gekoppeld aan elke virtuele machine in uw cluster. Deze taak is voltooid met behulp van Hallo cifs hulpprogramma/protocol. Hallo koppelbewerking kan handmatig worden uitgevoerd op elk knooppunt van de cluster Hallo of door een script uitgevoerd op elk knooppunt in het Hallo-cluster.

In dit voorbeeld twee scripts worden uitgevoerd, één toomount hello Azure file share- en een tweede toorun dit script op elk knooppunt van Hallo DC/OS-cluster.

Eerst hello Azure storage-accountnaam en toegangssleutel nodig. Voer Hallo opdrachten tooget na deze informatie. Let op elk, deze waarden worden gebruikt in een later stadium.

Opslagaccountnaam:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Toegangssleutel voor opslagaccount:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Haal vervolgens Hallo FQDN-naam van Hallo DC/OS-master en op te slaan in een variabele.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Kopieer het hoofdknooppunt van uw persoonlijke sleutel toohello. Deze sleutel is vereist toocreate een ssh-verbinding met alle knooppunten in cluster Hallo. Hallo-gebruikersnaam bijwerken als een niet-standaard-waarde is gebruikt bij het maken van Hallo-cluster. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Een SSH-verbinding maken met Hallo master (of het eerste model Hallo) van uw DC/OS gebaseerde cluster. Hallo-gebruikersnaam bijwerken als een niet-standaard-waarde is gebruikt bij het maken van Hallo-cluster.

```azurecli-interactive
ssh azureuser@$FQDN
```

Maak een bestand met de naam **cifsMount.sh**, en kopiëren Hallo inhoud in de App. 

Dit script is gebruikte toomount hello Azure-bestandsshare. Update Hallo `STORAGE_ACCT_NAME` en `ACCESS_KEY` met Hallo informatie die eerder zijn verzameld.

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
Maak een tweede bestand met de naam **getNodesRunScript.sh** en kopiëren Hallo inhoud in Hallo-bestand. 

Dit script detecteert alle clusterknooppunten en voert vervolgens Hallo **cifsMount.sh** script toomount Hallo-bestandsshare op elk.

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Hallo script toomount hello Azure-bestandsshare worden uitgevoerd op alle knooppunten van het Hallo-cluster.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Hallo bestandsshare is nu toegankelijk op `/mnt/share/dcosshare` op elk knooppunt van het Hallo-cluster.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie een Azure is de bestandsshare en-klare beschikbaar tooa DC/OS-cluster met behulp van Hallo stappen:

> [!div class="checklist"]
> * Een Azure-opslagaccount maken
> * Een bestandsshare maken
> * Hallo-share in Hallo DC/OS-cluster koppelen

Ga toohello volgende zelfstudie toolearn over de integratie van een Azure Container register met DC/OS in Azure.  

> [!div class="nextstepaction"]
> [Load balancing gebruiken voor toepassingen](container-service-dcos-acr.md)