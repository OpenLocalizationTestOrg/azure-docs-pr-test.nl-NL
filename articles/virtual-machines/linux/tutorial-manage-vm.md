---
title: aaaCreate- en Linux VM's beheren met Azure CLI Hallo | Microsoft Docs
description: Zelfstudie - maken en beheren van virtuele Linux-machines met hello Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Maken en beheren van virtuele Linux-machines met hello Azure CLI

Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving. Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie items zoals het selecteren van een VM-grootte, een VM-installatiekopie te selecteren en implementeren van een virtuele machine. Procedures voor:

> [!div class="checklist"]
> * Maken en koppelen tooa VM
> * Selecteer en gebruik van VM-installatiekopieën
> * Weergeven en gebruiken van specifieke VM-grootten
> * De grootte van een virtuele machine wijzigen
> * Bekijken en te begrijpen status virtuele machine


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht. 

Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Een resourcegroep moet worden gemaakt voordat een virtuele machine. In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroupVM* wordt gemaakt in Hallo *eastus* regio. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

Hallo-resourcegroep is opgegeven bij het maken of wijzigen van een virtuele machine die in deze zelfstudie kan worden gezien.

## <a name="create-virtual-machine"></a>Virtuele machine maken

Een virtuele machine maken met de Hallo [az vm maken](https://docs.microsoft.com/cli/azure/vm#create) opdracht. 

Wanneer u een virtuele machine maakt, er zijn diverse opties beschikbaar zoals besturingssysteemkopie schijf sizing en administratieve referenties. In dit voorbeeld wordt een virtuele machine gemaakt met de naam *myVM* Ubuntu Server uitgevoerd. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Eenmaal Hallo die VM is gemaakt, levert hello Azure CLI informatie over Hallo VM. Let op Hallo `publicIpAddress`, dit adres mag gebruikte tooaccess Hallo virtuele machine... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Verbinding maken met tooVM

U kunt nu verbinding toohello VM via SSH. Hallo voorbeeld IP-adres vervangen door Hallo `publicIpAddress` in Hallo vorige stap hebt genoteerd.

```bash
ssh 52.174.34.95
```

Zodra u klaar bent met de Hallo VM, sluit u Hallo SSH-sessie. 

```bash
exit
```

## <a name="understand-vm-images"></a>VM-installatiekopieën begrijpen

Hello Azure marketplace bevat veel afbeeldingen die gebruikt toocreate virtuele machines worden kunnen. In de vorige stappen hello, is een virtuele machine gemaakt met behulp van een installatiekopie van een virtuele Ubuntu. Hello die Azure CLI gebruikte toosearch Hallo marketplace voor een installatiekopie CentOS, die vervolgens wordt gebruikt in deze stap toodeploy een tweede virtuele machine.  

een lijst met Hallo toosee meest gebruikte afbeeldingen, gebruikt u Hallo [az vm afbeeldingenlijst](/cli/azure/vm/image#list) opdracht.

```azurecli-interactive 
az vm image list --output table
```

Hallo-opdrachtuitvoer retourneert de meest populaire VM-installatiekopieën Hallo op Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Een volledige lijst ziet door toe te voegen Hallo `--all` argument. lijst met Hallo afbeeldingen kan ook worden gefilterd door `--publisher` of `–-offer`. In dit voorbeeld wordt Hallo lijst gefilterd voor alle afbeeldingen met een aanbieding die overeenkomt met *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Gedeeltelijke uitvoer:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

een virtuele machine met de installatiekopie van een specifieke toodeploy Noteer van Hallo-waarde in Hallo *Urn* kolom. Bij het opgeven van de installatiekopie van het Hallo kan versienummer Hallo-installatiekopie worden vervangen door 'nieuwste', die Hallo meest recente versie van Hallo-distributiepunt selecteert. In dit voorbeeld Hallo `--image` argument gebruikte toospecify Hallo meest recente versie van de installatiekopie van een CentOS 6.5 is.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>VM-grootten begrijpen

De grootte van een virtuele machine bepaalt Hallo hoeveelheid rekenresources zoals CPU en GPU geheugen die beschikbaar toohello virtuele machine zijn aangebracht. Toobe de juiste grootte voor de werklast Hallo verwacht, moeten virtuele machines. Als de werkbelasting toeneemt, kan een bestaande virtuele machine kan worden gewijzigd.

### <a name="vm-sizes"></a>VM-grootten

Hallo tabel categoriseert grootten in gebruiksvoorbeelden.  

| Type                     | Grootten           |    Beschrijving       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Algemeen doel](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7| Taakverdeling CPU-naar-geheugen. Ideaal voor dev / test- en kleine toomedium toepassingen en gegevens oplossingen.  |
| [Geoptimaliseerde rekenkracht](sizes-compute.md)   | FS, F             | Hoog CPU-naar-geheugen. Goede voor gemiddeld verkeer toepassingen, netwerkapparatuur en batchprocessen.        |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Hoge geheugen-naar-core. Ideaal voor relationele databases, gemiddeld toolarge caches en in het geheugen analytics.                 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md)      | Ls                | Snelle doorvoer van schijfgegevens en IO. Ideaal voor big data-, SQL- en NoSQL-databases.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Gespecialiseerde VMs gericht voor zware grafische weergave en het bewerken van video's.       |
| [Hoge prestaties](sizes-hpc.md) | H, A8 11          | De krachtigste CPU VMs met optionele hoge gegevensdoorvoer netwerkinterfaces (RDMA). 


### <a name="find-available-vm-sizes"></a>Zoeken naar beschikbare VM-grootten

een lijst met VM toosee groottes beschikbaar in een bepaalde regio, gebruikt u Hallo [az vm-lijst-groottes](/cli/azure/vm#list-sizes) opdracht. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Gedeeltelijke uitvoer:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Virtuele machine maken met een specifieke grootte

In Hallo vorige VM maken bijvoorbeeld is een grootte niet opgegeven, waardoor het een standaardgrootte. Een VM-grootte kan worden geselecteerd maken met behulp van tijd [az vm maken](/cli/azure/vm#create) en Hallo `--size` argument. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>De grootte van een virtuele machine wijzigen

Nadat een virtuele machine is geïmplementeerd, kan het formaat is gewijzigd tooincrease of resourcetoewijzing verlagen.

Voordat het formaat van een virtuele machine, controleren als hello gewenste grootte beschikbaar op Hallo huidige Azure-cluster is. Hallo [az vm-vm-formaat-opties voor](/cli/azure/vm#list-vm-resize-options) opdracht retourneert de lijst met grootten Hallo. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Desgewenst Hallo grootte is beschikbaar kan hello VM worden gewijzigd vanuit een status ingeschakeld op maar deze opnieuw wordt opgestart tijdens het Hallo-bewerking. Gebruik Hallo [az vm vergroten of verkleinen]( /cli/azure/vm#resize) opdracht tooperform Hallo formaat.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Desgewenst Hallo grootte is niet op Hallo huidig cluster Hallo VM behoeften toobe ongedaan voordat Hallo vergroten of verkleinen van de bewerking kan zich voordoen. Gebruik Hallo [az vm ongedaan]( /cli/azure/vm#deallocate) opdracht toostop en Hallo VM ongedaan gemaakt. Let op wanneer hello VM weer is ingeschakeld, worden alle gegevens op de tijdelijke schijf Hallo mogelijk verwijderd. Hallo openbaar IP-adres verandert ook tenzij een statisch IP-adres wordt gebruikt. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Zodra de toewijzing opgeheven, kan Hallo formaat optreden. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Nadat het Hallo vergroten of verkleinen, kunnen Hallo VM kan worden gestart.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>VM-energiestatus

Een Azure VM kan een van de vele energiestatussen hebben. Deze status vertegenwoordigt de huidige status Hallo Hallo VM Hallo verwerkt Hallo hypervisor. 

### <a name="power-states"></a>Energiestatus

| Energieniveau | Beschrijving
|----|----|
| Starting | Hiermee wordt aangegeven op Hallo virtuele machine wordt gestart. |
| Running | Hiermee wordt aangegeven dat de Hallo virtuele machine wordt uitgevoerd. |
| Stopping | Hiermee wordt aangegeven dat de virtuele machine hello wordt gestopt. | 
| Stopped | Geeft aan dat de virtuele machine Hallo is gestopt. Virtuele machines in de status gestopt Hallo nog steeds kosten compute.  |
| Toewijzing | Hiermee wordt aangegeven dat de virtuele machine hello wordt opgeheven. |
| De toewijzing ongedaan gemaakt | Hiermee wordt aangegeven dat de virtuele machine Hallo wordt verwijderd uit het Hallo-hypervisor, maar nog steeds beschikbaar in Hallo besturingselement vlak. Virtuele machines in Hallo Deallocated status kan niet worden compute-kosten in rekening. |
| - | Geeft aan dat de energiestatus Hallo van Hallo virtuele machine onbekend. |

### <a name="find-power-state"></a>Energieniveau vinden

tooretrieve hello status van een bepaalde virtuele machine, gebruik Hallo [az vm-instantieweergave ophalen](/cli/azure/vm#get-instance-view) opdracht. Niet zeker toospecify een geldige naam voor een virtuele machine en de resourcegroep. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Uitvoer:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Beheertaken

Tijdens het Hallo-levenscyclus van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd. U kunt bovendien toocreate scripts tooautomate herhalende of complexe taken. Met behulp van Azure CLI Hallo kunnen veel algemene beheertaken worden uitgevoerd vanaf de opdrachtregel hello, hetzij in scripts. 

### <a name="get-ip-address"></a>IP-adres

Deze opdracht retourneert Hallo persoonlijke en openbare IP-adressen van een virtuele machine.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Virtuele machine stoppen

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Virtuele machine starten

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Verwijderen van resourcegroep

Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over basic VM maken en beheren zoals het:

> [!div class="checklist"]
> * Maken en koppelen tooa VM
> * Selecteer en gebruik van VM-installatiekopieën
> * Weergeven en gebruiken van specifieke VM-grootten
> * De grootte van een virtuele machine wijzigen
> * Bekijken en te begrijpen status virtuele machine

Ga toohello volgende zelfstudie toolearn over VM-schijven.  

> [!div class="nextstepaction"]
> [Maken en beheren van VM-schijven](./tutorial-manage-disks.md)
