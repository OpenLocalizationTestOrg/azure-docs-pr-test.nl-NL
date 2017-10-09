---
title: Quick Start aaaAzure-Cloud-Shell (Preview) | Microsoft Docs
description: Quick Start voor hello Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Quick Start voor het gebruik van hello Azure Cloud Shell

Dit document beschrijft hoe toouse Azure Cloud Shell in Hallo Hallo [Azure-portal](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Cloud-Shell starten
1. Start **Cloud Shell** van de bovenste navigatiebalk Hallo Hallo Azure-portal <br>
![](media/shell-icon.png)
2. Selecteer een abonnement toocreate een opslagaccount en een Azure-bestandsshare
3. Selecteer 'Opslag maken'

> [!TIP]
> U bent automatisch geverifieerd voor Azure CLI 2.0 in elke sesssion.

### <a name="set-your-subscription"></a>Stel uw abonnement
1. Lijst met abonnementen u toegang tot hebt: <br>
`az account list`
2. Stel uw voorkeur abonnement: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Uw abonnement worden opgeslagen voor toekomstige sessies met behulp van `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Een resourcegroep maken
Maak een nieuwe resourcegroep in WestUS met de naam 'MyRG': <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Een Linux-VM maken
Maak een VM Ubuntu in uw nieuwe resourcegroep. Hello Azure CLI 2.0 maakt SSH-sleutels en setup Hallo VM mee. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Hallo tooauthenticate van openbare en persoonlijke sleutels die worden gebruikt in uw virtuele machine worden geplaatst `/User/.ssh/id_rsa` en `/User/.ssh/id_rsa.pub` door Azure CLI 2.0 standaard. De SSH-map wordt bewaard in de gekoppelde Azure-bestandsshare van 5 GB installatiekopie.

Uw gebruikersnaam op deze virtuele machine worden uw gebruikersnaam die wordt gebruikt in de Cloud-Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH in uw virtuele Linux-machine
1. Zoeken naar de naam van uw VM in Hallo zoekbalk met Azure portal
2. Klik op "Connect" en voer:`ssh username@ipaddress`

![](media/sshcmd-copy.png)

Bij het tot stand brengen van SSH-verbinding hello, ziet u Hallo Ubuntu Welkom prompt.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Opschonen 
De resourcegroep en alle resources binnen deze verwijderen: <br>
Voer `az group delete -n MyRG` uit.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over persistent maken van de opslag op Cloud-Shell](persisting-shell-storage.md) <br>
[Meer informatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Meer informatie over Azure File storage](../storage/files/storage-files-introduction.md) <br>