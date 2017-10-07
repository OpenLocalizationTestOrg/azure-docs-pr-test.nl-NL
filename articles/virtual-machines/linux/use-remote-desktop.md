---
title: aaaUse extern bureaublad tooa Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureren van extern bureaublad (xrdp) tooconnect tooa Linux VM in Azure met grafische hulpprogramma's
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Installeren en configureren van extern bureaublad tooconnect tooa Linux VM in Azure
Linux virtuele machines (VM's) in Azure worden meestal beheerd vanuit de opdrachtregel Hallo via een secure shell (SSH)-verbinding. Wanneer nieuwe tooLinux of voor snelle scenario's voor probleemoplossing Hallo van extern bureaublad kan bijvoorbeeld worden gebruikt eenvoudiger. Dit artikel details hoe tooinstall en configureren van een bureaublad-omgeving ([xfce](https://www.xfce.org)) en extern bureaublad ([xrdp](http://www.xrdp.org)) voor uw Linux-VM met Hallo Resource Manager-implementatiemodel.


## <a name="prerequisites"></a>Vereisten
In dit artikel is vereist voor een bestaande Linux VM in Azure. Als u toocreate een virtuele machine moet, een van de volgende methoden hello gebruiken:

- Hallo [Azure CLI 2.0](quick-create-cli.md)
- Hallo [Azure-portal](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Een bureaubladomgeving installeren op uw Linux-VM
De meeste Linux virtuele machines in Azure beschikt niet over een bureaubladomgeving standaard geïnstalleerd. Linux VM's worden meestal beheerd met behulp van SSH-verbindingen in plaats van een bureaublad-omgeving. Er zijn verschillende bureaubladomgevingen in Linux die u kunt kiezen. Afhankelijk van uw keuze van bureaubladomgeving van mogelijk één too2 GB aan schijfruimte, gebruiken en 5 too10 minuten tooinstall nemen en alle vereist hello-pakketten te configureren.

Hallo volgende voorbeeld wordt geïnstalleerd Hallo lightweight [xfce4](https://www.xfce.org/) bureaubladomgeving op een Ubuntu VM. Opdrachten voor andere distributies enigszins verschillen (Gebruik `yum` tooinstall op Red Hat Enterprise Linux en configureer de juiste `selinux` regels of gebruik `zypper` tooinstall op SUSE, bijvoorbeeld).

Eerst SSH tooyour VM. Hallo volgende voorbeeld maakt verbinding met de naam VM toohello *myvm.westus.cloudapp.azure.com* Hallo gebruikersnaam van *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Als u van Windows gebruikmaakt en meer informatie over het gebruik van SSH nodig hebt, raadpleegt u [hoe toouse SSH-sleutels met Windows](ssh-from-windows.md).

Vervolgens installeert met behulp van xfce `apt` als volgt:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Installeren en configureren van een extern bureaublad-server
Nu dat u een bureaubladomgeving geïnstalleerd hebt, configureert u een extern bureaublad-services toolisten voor binnenkomende verbindingen. [xrdp](http://xrdp.org) is een open-source Remote Desktop Protocol (RDP)-server die beschikbaar is op de meeste Linux-distributies en werkt goed samen met xfce. Installeer xrdp op uw Ubuntu VM als volgt:

```bash
sudo apt-get install xrdp
```

Vertel xrdp welke toouse bureaubladomgeving bij het starten van uw sessie. Xrdp toouse xfce als de bureaubladomgeving als volgt configureren:

```bash
echo xfce4-session >~/.xsession
```

Hallo xrdp service voor Hallo wijzigingen tootake effect als volgt opnieuw starten:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Wachtwoord voor een lokale gebruikersaccount instellen
Als u een wachtwoord voor uw gebruikersaccount gemaakt toen u uw virtuele machine hebt gemaakt, kunt u deze stap overslaan. Als u alleen verificatie van SSH-sleutel en niet het wachtwoord van een lokale account instellen hoeft, een wachtwoord opgeven voordat u xrdp toolog in tooyour VM gebruiken. xrdp accepteren niet SSH-sleutels voor verificatie. Hallo volgende voorbeeld wordt een wachtwoord voor gebruikersaccount Hallo *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Opgeven van een wachtwoord wordt uw SSHD configuratie toopermit wachtwoord aanmeldingen niet bijgewerkt als die op dit moment niet bestaat. U kunt vanuit het beveiligingsoogpunt van tooconnect tooyour VM desgewenst met een SSH-tunnel met verificatie op basis van sleutels en sluit tooxrdp. Zo ja, overslaan Hallo volgende stap over het maken van een security group regel tooallow extern bureaublad netwerkverkeer.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Een Netwerkbeveiligingsgroep regel maken voor extern bureaublad-verkeer
tooallow extern bureaublad-verkeer tooreach uw Linux VM, een groep voor de netwerkbeveiligingsregel moet toobe gemaakt waarmee TCP op poort 3389 tooreach uw virtuele machine. Zie voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) U kunt ook [gebruik hello Azure portal toocreate een groep voor de netwerkbeveiligingsregel](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hallo volgende voorbeelden maakt een groep van de netwerkbeveiligingsregel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) met de naam *myNetworkSecurityGroupRule* te*toestaan* verkeer op *tcp* poort *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Verbinding maken met uw Linux-VM met een extern bureaublad-client
Open uw lokale extern-bureaubladclient en verbinding maken met toohello IP-adres of de DNS-naam van uw Linux-VM. Hallo gebruikersnaam en wachtwoord invoeren voor Hallo-gebruikersaccount op de virtuele machine als volgt:

![Verbinding maken met behulp van extern bureaublad-client tooxrdp](./media/use-remote-desktop/remote-desktop-client.png)

Als de verificatie is gelukt, Hallo xfce bureaubladomgeving laadt en Zoek vergelijkbare toohello voorbeeld te volgen:

![xfce bureaubladomgeving via xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Problemen oplossen
Als u verbinding maken met behulp van een extern bureaublad-client voor Linux-VM tooyour, `netstat` op uw Linux-VM tooverify die uw virtuele machine naar RDP-verbindingen als volgt luistert:

```bash
sudo netstat -plnt | grep rdp
```

Hallo volgende voorbeeld ziet u Hallo VM luisteren op TCP-poort 3389 zoals verwacht:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Hallo xrdp service niet wordt geluisterd, op een VM Ubuntu start Hallo-service als als volgt:

```bash
sudo service xrdp restart
```

Bekijk wordt geregistreerd in */var/log*Thug op uw VM Ubuntu nakijken op aanwijzingen als toowhy Hallo-service reageert niet. U kunt ook bewaken Hallo syslog tijdens een poging verbinding met extern bureaublad tooview fouten:

```bash
tail -f /var/log/syslog
```

Andere zoals Red Hat Enterprise Linux en SUSE Linux-distributies mogelijk op verschillende manieren toorestart services en alternatieve log-bestand locaties tooreview.

Als u geen antwoord niet in uw extern-bureaubladclient krijgt en alle gebeurtenissen in het systeemlogboek Hallo niet ziet, wordt de reden hiervoor is dat het externe bureaublad verkeer Hallo VM kan niet bereiken. Bekijk uw netwerk beveiliging groep regels tooensure dat u een regel toopermit TCP op poort 3389 hebt. Zie voor meer informatie [problemen met toepassing](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het maken en gebruiken van SSH-sleutels met Linux VM's [maken SSH-sleutels voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).

Zie voor meer informatie over het gebruik van SSH op Windows [hoe toouse SSH-sleutels met Windows](ssh-from-windows.md).

