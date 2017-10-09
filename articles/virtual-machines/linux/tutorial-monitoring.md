---
title: aaaMonitor Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toomonitor diagnostische gegevens en maatstaven voor prestaties opstarten op een virtuele Linux-machine in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
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
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Hoe toomonitor virtuele Linux-machine in Azure

tooensure die uw virtuele machines (VM's) in Azure correct worden uitgevoerd, kunt u diagnostische gegevens over opstarten en maatstaven voor prestaties bekijken. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Diagnostische gegevens over opstarten op Hallo VM inschakelen
> * Diagnostische gegevens over opstarten bekijken
> * Metrische gegevens weergeven host
> * Extensie voor diagnostische gegevens op Hallo VM inschakelen
> * Metrische gegevens weergeven VM
> * Waarschuwingen op basis van diagnostische gegevens maken
> * Geavanceerde controle instellen


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>VM maken

toosee diagnostische gegevens en metrische gegevens in te grijpen, moet u een virtuele machine. Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupMonitor* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Maak nu een virtuele machine met [az vm maken](https://docs.microsoft.com/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Diagnostische gegevens over opstarten inschakelen

Virtuele Linux-machines opstart, boot-uitvoer worden vastgelegd en opgeslagen in Azure storage Hallo opstarten diagnostische extensie. Deze gegevens kunnen worden gebruikt tootroubleshoot VM opstartproblemen. Diagnostische gegevens over opstarten zijn niet automatisch ingeschakeld wanneer u een Linux-VM met behulp van Azure CLI Hallo maakt.

Voordat u diagnostische gegevens over opstarten inschakelt, moet een opslagaccount toobe gemaakt voor het opslaan van de logboeken van de opstartinstallatiekopie. Storage-accounts moeten een globaal unieke naam hebben, tussen 3 en 24 tekens bevatten en mogen alleen cijfers en kleine letters bevatten. Een opslagaccount maken met de Hallo [az storage-account maken](/cli/azure/storage/account#create) opdracht. In dit voorbeeld wordt een willekeurige tekenreeks gebruikte toocreate een unieke opslagaccountnaam. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Bij het inschakelen van diagnostische gegevens over opstarten is Hallo URI toohello blob storage-container vereist. Hallo Hallo volgende opdracht query's storage account tooreturn deze URI. Hallo URI-waarde wordt opgeslagen in een variabelenamen *bloburi*, die wordt gebruikt in de volgende stap Hallo.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Nu inschakelen diagnostische gegevens over opstarten met [az vm-diagnostische gegevens over opstarten inschakelen](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Hallo `--storage` waarde Hallo blob URI verzameld in de vorige stap Hallo is.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Diagnostische gegevens over opstarten bekijken

Wanneer diagnostische gegevens over opstarten zijn ingeschakeld, telkens wanneer u stoppen en starten Hallo VM, informatie over het opstartproces Hallo geschreven tooa logboekbestand. Voor dit voorbeeld moet u eerst Hallo VM Hello ongedaan [az vm ongedaan](/cli/azure/vm#deallocate) opdracht als volgt:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Hallo VM nu beginnen met Hallo [az vm start]( /cli/azure/vm#stop) opdracht als volgt:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

U krijgt Hallo opstarten diagnostische gegevens voor *myVM* Hello [az vm diagnostische gegevens over opstarten get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) opdracht als volgt:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Metrische gegevens weergeven host

Een Linux-VM heeft toegewezen host in Azure die deze met samenwerkt. Metrische gegevens worden automatisch verzameld voor Hallo host en kan worden bekeken in hello Azure-portal als volgt:

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroupMonitor**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
1. toosee het Hallo host VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo VM blade en selecteer vervolgens een Hallo *[Host]* metrische gegevens onder **beschikbare metrische gegevens**.

    ![Metrische gegevens weergeven host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Installeren van de extensie voor diagnostische gegevens

> [!IMPORTANT]
> Dit document beschrijft versie 2.3 Hallo Linux diagnostische extensie, die is afgeschaft. Versie 2.3 worden tot en met 30 juni 2018 ondersteund.
>
> Versie 3.0 Hallo diagnostische Linux-extensie kan in plaats daarvan worden ingeschakeld. Zie voor meer informatie [Hallo documentatie](./diagnostic-extension.md).

Hallo basic host metrische gegevens beschikbaar zijn, maar meer gedetailleerd toosee en VM-specifieke metrische gegevens en u tooneed tooinstall hello Azure extensie voor diagnostische gegevens op Hallo VM. Hello Azure diagnostics-extensie kan aanvullende controle en diagnostische gegevens toobe opgehaald uit Hallo VM. U kunt deze maatstaven voor prestaties weergeven en waarschuwingen op basis van hoe Hallo VM wordt uitgevoerd. Hallo diagnostische uitbreiding wordt geïnstalleerd via hello Azure-portal als volgt:

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
1. Klik op **diagnose instellingen**. Hallo lijst ziet u dat *opstarten diagnostics* al uit de vorige sectie Hallo zijn ingeschakeld. Klik op het selectievakje Hallo voor *basismetrieken*.
1. In Hallo *opslagaccount* sectie, selecteer Hallo tooand Bladeren *mydiagdata [1234]* account gemaakt in de vorige sectie Hallo.
1. Klik op Hallo **opslaan** knop.

    ![Diagnostische metrische gegevens weergeven](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Metrische gegevens weergeven VM

U kunt Hallo VM metrische gegevens weergeven in Hallo dezelfde manier dat Hallo host VM metrische gegevens:

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
1. toosee het Hallo VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de diagnostische gegevens metrische gegevens Hallo onder **beschikbare metrische gegevens**.

    ![Metrische gegevens weergeven VM](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Waarschuwingen maken

U kunt waarschuwingen op basis van specifieke prestatiewaarden kunt maken. Waarschuwingen kunnen bijvoorbeeld gebruikte toonotify u wanneer het gemiddelde CPU-gebruik overschrijdt een bepaalde drempelwaarde of beschikbare vrije schijfruimte onder een bepaalde hoeveelheid zakt. Waarschuwingen worden weergegeven in hello Azure-portal of kunnen worden verzonden via e-mail. U kunt ook Azure Automation-runbooks of Azure Logic Apps activeren in het antwoord tooalerts wordt gegenereerd.

Hallo wordt volgende voorbeeld een waarschuwing voor het gemiddelde CPU-gebruik.

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
2. Klik op **waarschuwing regels** op Hallo VM blade en klik vervolgens op **metrische waarschuwing toevoegen** aan de bovenkant Hallo van Hallo waarschuwingen-blade.
4. Geef een **naam** voor de waarschuwing, zoals *myAlertRule*
5. een waarschuwing wanneer CPU-percentage 1.0 gedurende vijf minuten overschrijdt tootrigger standaardinstellingen laten staan alle Hallo andere geselecteerd.
6. Eventueel selectievakje Hallo in voor *e-eigenaren, bijdragers en lezers* toosend e-mailmeldingen. Hallo standaardactie is toopresent een melding in Hallo-portal.
7. Klik op Hallo **OK** knop.


## <a name="advanced-monitoring"></a>Geavanceerde controle 

U kunt doen meer geavanceerde bewaking van uw virtuele machine met behulp van [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Als u dit nog niet hebt gedaan, kunt u zich aanmelden voor een [gratis proefversie](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) van Operations Management Suite.

Wanneer u toegang toohello OMS-portal hebt, kunt u Hallo werkruimte sleutel en de werkruimte-id vinden op de blade instellingen Hallo. Vervang < werkruimtesleutel > en < werkruimte-id > Hallo waarden voor uit uw OMS werkruimte en u vervolgens kunt gebruiken **az vm-extensie set** tooadd Hallo OMS-extensie toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Op Hallo logboek Search-blade van Hallo OMS-portal, ziet u *myVM* zoals wat wordt weergegeven in de volgende afbeelding Hallo:

![OMS-blade](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt geconfigureerd en virtuele machines in Azure Security Center gecontroleerd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Diagnostische gegevens over opstarten op Hallo VM inschakelen
> * Diagnostische gegevens over opstarten bekijken
> * Metrische gegevens weergeven host
> * Extensie voor diagnostische gegevens op Hallo VM inschakelen
> * Metrische gegevens weergeven VM
> * Waarschuwingen op basis van diagnostische gegevens maken
> * Geavanceerde controle instellen

Ga toohello volgende zelfstudie toolearn over Azure security center.

> [!div class="nextstepaction"]
> [VM-beveiliging beheren](./tutorial-azure-security.md)