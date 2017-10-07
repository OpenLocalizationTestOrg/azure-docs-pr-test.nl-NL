---
title: de SSH-verbinding aaaTroubleshoot problemen tooan Azure VM | Microsoft Docs
description: Hoe tootroubleshoot problemen zoals 'SSH-verbinding is mislukt' of 'SSH-verbinding geweigerd' voor een Azure VM waarop Linux wordt uitgevoerd.
keywords: SSH verbinding geweigerd, ssh fout, azure ssh, SSH-verbinding is mislukt
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Problemen met SSH-verbindingen tooan Azure Linux VM die is mislukt, fouten, of wordt geweigerd
Er zijn diverse redenen dat u op problemen Secure Shell (SSH), SSH verbindingsfouten stuit, of SSH wordt geweigerd wanneer u tooconnect tooa virtuele Linux-machine (VM probeert). In dit artikel helpt u bij het zoeken en de juiste Hallo problemen. U kunt het gebruiken van hello Azure-portal, Azure CLI of VM-extensie voor toegang voor Linux tootroubleshoot en oplossen van problemen met de verbinding.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](http://azure.microsoft.com/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](http://azure.microsoft.com/support/options/) en selecteer **ondersteuning krijgen**. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Snelle stappen voor probleemoplossing
Probeer opnieuw verbinding te maken toohello VM na elke stap voor probleemoplossing.

1. Hallo SSH-configuratie opnieuw instellen.
2. Hallo-referenties voor Hallo gebruiker instellen.
3. Controleer of Hallo [Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) regels SSH-verkeer toestaan.
   * Zorg ervoor dat een regel Netwerkbeveiligingsgroep toopermit SSH verkeer (standaard TCP-poort 22 bestaat).
   * U kunt geen poortomleiding gebruiken / toewijzen zonder gebruik van een Azure load balancer.
4. Controleer de Hallo [VM resourcestatus](../../resource-health/resource-health-overview.md). 
   * Zorg ervoor dat Hallo VM rapporten als in orde.
   * Als er diagnostische gegevens over opstarten is ingeschakeld, controleert u of Hallo VM is niet opstartfouten rapporteert in Hallo Logboeken.
5. Opnieuw opstarten Hallo VM.
6. Hallo VM implementeren.

Blijven lezen voor meer gedetailleerde stappen voor probleemoplossing en uitleg.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Beschikbare methoden tootroubleshoot SSH-verbindingsproblemen
U kunt opnieuw instellen van referenties of met een van de volgende methoden Hallo SSH-configuratie:

* [Azure-portal](#use-the-azure-portal) - handig als u tooquickly moet Hallo SSH-configuratie of SSH-sleutel opnieuw instellen en u geen Hallo van Azure-hulpprogramma's geïnstalleerd.
* [Azure CLI 2.0](#use-the-azure-cli-20) : als u al op de opdrachtregel Hallo snel Hallo SSH-configuratie opnieuw instellen of referenties bent. U kunt ook Hallo [Azure CLI 1.0](#use-the-azure-cli-10)
* [Azure VMAccessForLinux-extensie](#use-the-vmaccess-extension) - maken en gebruiken van json-definitie bestanden tooreset Hallo SSH-configuratie of gebruikersreferenties.

Probeer na elke stap tooyour VM opnieuw verbinding te maken. Als u nog steeds geen verbinding maken, probeert u de volgende stap Hallo.

## <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal
Hello Azure-portal biedt een snelle manier tooreset Hallo SSH-configuratie of gebruikersreferenties zonder alle hulpprogramma's installeert op uw lokale computer.

Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag toohello **ondersteuning + probleemoplossing** sectie en selecteer **wachtwoord opnieuw instellen** zoals Hallo volgt in:

![SSH-configuratie of de referenties in hello Azure-portal opnieuw instellen](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Hallo SSH-configuratie opnieuw instellen
Selecteer als eerste stap `Reset configuration only` van Hallo **modus** Vervolgkeuzelijst als in Hallo voorgaande schermafbeelding, klik vervolgens op Hallo **opnieuw instellen** knop. Zodra deze actie is voltooid, probeer het tooaccess uw virtuele machine opnieuw.

### <a name="reset-ssh-credentials-for-a-user"></a>SSH-referenties voor een gebruiker opnieuw instellen
tooreset hello referenties van een bestaande gebruiker selecteren `Reset SSH public key` of `Reset password` van Hallo **modus** vervolgkeuzelijst zoals in Hallo voorgaande schermafbeelding. Geef Hallo gebruikersnaam en een SSH-sleutel of het nieuwe wachtwoord en klik op Hallo **opnieuw** knop.

U kunt ook een gebruiker met sudo-bevoegdheden op Hallo VM in dit menu maken. Voer een nieuwe gebruikersnaam en het bijbehorende wachtwoord of de SSH-sleutel en klik vervolgens op Hallo **opnieuw** knop.

## <a name="use-hello-azure-cli-20"></a>Hello Azure CLI 2.0 gebruiken
Als u nog niet gedaan hebt, installeert u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).

Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, zorg ervoor dat Hallo [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd. VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.

### <a name="reset-ssh-configuration"></a>SSH-configuratie opnieuw instellen
U kunt in eerste instantie probeer het opnieuw instellen Hallo SSH toodefault configuratiewaarden en Hallo SSH-server opnieuw op te starten op Hallo VM. Houd er rekening mee dat dit niet Hallo gebruikersnaam, wachtwoord of SSH-sleutels wijzigt.
Hallo volgende voorbeeld wordt [az vm gebruiker opnieuw instellen-ssh](/cli/azure/vm/user#reset-ssh) tooreset Hallo SSH-configuratie op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>SSH-referenties voor een gebruiker opnieuw instellen
Hallo volgende voorbeeld wordt [az vm gebruikersupdate](/cli/azure/vm/user#update) tooreset Hallo-referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op Hallo VM met de naam `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Als u verificatie van SSH-sleutel gebruikt, kunt u Hallo SSH-sleutel voor een bepaalde gebruiker herstellen. Hallo volgende voorbeeld wordt **az vm set-linux-gebruikers toegang tot** tooupdate Hallo SSH-sleutel wordt opgeslagen in `~/.ssh/id_rsa.pub` voor Hallo-gebruiker met de naam `myUsername`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Hallo VMAccess-extensie gebruiken
Hallo VM-extensie voor toegang voor Linux wordt gelezen in een json-bestand dat wordt gedefinieerd toocarry acties uit. Deze acties omvatten opnieuw instellen van SSHD, opnieuw instellen van een SSH-sleutel of een gebruiker toe te voegen. U hello Azure CLI toocall hello VMAccess-extensie, maar hergebruik Hallo json-bestanden over meerdere VM's desgewenst. Deze aanpak kunt u toocreate een opslagplaats voor json-bestanden die vervolgens kan worden aangeroepen voor bepaalde scenario's.

### <a name="reset-sshd"></a>SSHD opnieuw instellen
Maak een bestand met de naam `settings.json` Hello volgende inhoud:

```json
{  
    "reset_ssh":"True"
}
```

Hello Azure CLI, u vervolgens aanroepen Hallo `VMAccessForLinux` extensie tooreset uw SSHD verbinding door te geven van uw json-bestand. Hallo volgende voorbeeld wordt [az vm-extensie set](/cli/azure/vm/extension#set) tooreset SSHD op Hallo VM met de naam `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>SSH-referenties voor een gebruiker opnieuw instellen
Als SSHD correct wordt weergegeven toofunction, kunt u Hallo-referenties voor een afzender gebruiker herstellen. tooreset hello wachtwoord voor een gebruiker, maak een bestand met de naam `settings.json`. Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`. Voer de volgende regels in Hallo uw `settings.json` -bestand, met behulp van uw eigen waarden:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Of tooreset Hallo SSH-sleutel voor een gebruiker, maakt u eerst een bestand met de naam `settings.json`. Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`. Voer de volgende regels in Hallo uw `settings.json` -bestand, met behulp van uw eigen waarden:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Nadat uw json-bestand is gemaakt, gebruikt u hello Azure CLI toocall hello `VMAccessForLinux` extensie tooreset uw SSH-gebruikersreferenties door te geven van uw json-bestand. Hallo volgende voorbeeld worden de referenties op Hallo VM met de naam `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Gebruik hello Azure CLI 1.0
Als u dat nog niet gedaan hebt, [hello Azure CLI 1.0 installeren en verbinding maken met Azure-abonnement tooyour](../../cli-install-nodejs.md). Zorg ervoor dat u van Resource Manager-modus als volgt gebruikmaakt:

```azurecli
azure config mode arm
```

Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, zorg ervoor dat Hallo [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd. VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.

### <a name="reset-ssh-configuration"></a>SSH-configuratie opnieuw instellen
Hallo SSHD configuratie zelf is mogelijk onjuist geconfigureerd of Hallo-service is een fout opgetreden. U kunt herstellen SSHD toomake of SSH-configuratie voor Hallo zelf geldig is. Opnieuw instellen van SSHD moet Hallo eerste probleemoplossing die u rekening houden.

Hallo volgende voorbeeld wordt SSHD op een virtuele machine met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`. Uw eigen namen voor virtuele machine en de resource als volgt gebruiken:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>SSH-referenties voor een gebruiker opnieuw instellen
Als SSHD correct wordt weergegeven toofunction, kunt u Hallo wachtwoord voor een afzender gebruiker herstellen. Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Als u verificatie van SSH-sleutel gebruikt, kunt u Hallo SSH-sleutel voor een bepaalde gebruiker herstellen. Voorbeeld van updates na Hallo Hallo SSH-sleutel die zijn opgeslagen in `~/.ssh/id_rsa.pub` voor Hallo-gebruiker met de naam `myUsername`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Een VM opnieuw opstarten
Als u opnieuw instellen van de SSH-configuratie en gebruikersreferenties hello, of is een fout opgetreden in dat geval, kunt u proberen opnieuw te starten Hallo VM tooaddress onderliggende compute-problemen.

### <a name="azure-portal"></a>Azure Portal
een virtuele machine met toorestart Hallo Azure portal, selecteer uw virtuele machine en klik op Hallo **opnieuw** knop zoals in het volgende voorbeeld Hallo:

![Opnieuw opstarten van een virtuele machine in hello Azure-portal](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Hallo voorbeeld opnieuw wordt opgestart na Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Hallo volgende voorbeeld wordt [az vm opnieuw](/cli/azure/vm#restart) toorestart Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Een virtuele machine opnieuw implementeren
U kunt een virtuele machine tooanother-knooppunt in Azure, die mogelijk onderliggende netwerkproblemen opgelost opnieuw implementeren. Zie voor meer informatie over het opnieuw distribueren van een virtuele machine [opnieuw implementeren van virtuele machine toonew Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan Hallo virtuele machine zijn wordt bijgewerkt.
> 
> 

### <a name="azure-portal"></a>Azure Portal
een virtuele machine met tooredeploy Hallo Azure portal, selecteer uw virtuele machine en schuif omlaag toohello **ondersteuning + probleemoplossing** sectie. Klik op Hallo **implementeren** knop zoals Hallo volgt in:

![Implementeren van een virtuele machine in hello Azure-portal](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
voorbeeld redeploys na Hallo Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Hallo na gebruik bijvoorbeeld [az vm opnieuw distribueren](/cli/azure/vm#redeploy) tooredeploy Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`. Uw eigen waarden als volgt gebruiken:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Virtuele machines die zijn gemaakt met behulp van Hallo klassieke implementatiemodel
Probeer deze stappen tooresolve Hallo meest voorkomende SSH verbindingsfouten voor virtuele machines die zijn gemaakt met het klassieke implementatiemodel Hallo. Probeer opnieuw verbinding te maken toohello VM na elke stap.

* Opnieuw instellen van externe toegang van Hallo [Azure-portal](https://portal.azure.com). Op Hallo van Azure-portal, selecteer uw virtuele machine en klikt u op Hallo **extern opnieuw instellen...**  knop.
* Opnieuw opstarten Hallo VM. Op Hallo [Azure-portal](https://portal.azure.com), selecteert u de virtuele machine en klik op Hallo **opnieuw** knop.
    
* Implementeer Hallo VM tooa nieuwe Azure knooppunt opnieuw. Voor informatie over het tooredeploy een VM, Zie [opnieuw implementeren van virtuele machine toonew Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan Hallo virtuele machine zijn wordt bijgewerkt.
* Volg de instructies in Hallo [hoe tooreset een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) naar:
  
  * Hallo-wachtwoord opnieuw instellen of SSH-sleutel.
  * Maak een *sudo* gebruikersaccount.
  * Hallo SSH-configuratie opnieuw instellen.
* Controleer de resourcestatus Hallo van de virtuele machine voor problemen met het platform.<br>
     Selecteer uw virtuele machine en schuif naar beneden **instellingen** > **Controleer Health**.

## <a name="additional-resources"></a>Aanvullende bronnen
* Als u nog steeds niet tooSSH tooyour VM nadat de volgende stappen hello, Zie [meer gedetailleerde stappen voor probleemoplossing](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview extra stappen tooresolve uw probleem.
* Zie voor meer informatie over het oplossen van toegang tot toepassingen [problemen met toegang tooan toepassing die wordt uitgevoerd op een virtuele machine van Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zie voor meer informatie over het oplossen van virtuele machines die zijn gemaakt met het klassieke implementatiemodel Hallo [hoe tooreset een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

