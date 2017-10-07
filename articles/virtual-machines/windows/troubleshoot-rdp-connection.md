---
title: aaaCannot verbinding maken met RDP tooa Windows virtuele machine in Azure | Microsoft Docs
description: Problemen oplossen wanneer u een tooyour Windows virtuele machine in Azure met extern bureaublad geen verbinding maken
keywords: Extern bureaublad-fout, verbinding met extern bureaublad-fout, kan geen verbinding maken tooVM, probleemoplossing extern bureaublad
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Extern bureaublad-verbindingen tooan virtuele machine van Azure oplossen
Hallo Remote Desktop Protocol (RDP) verbinding tooyour op basis van Windows Azure virtuele machine (VM) kan mislukken voor verschillende oorzaken hebben, zodat u niet kan tooaccess uw virtuele machine. Hallo probleem kan worden Hello extern bureaublad-service op Hallo VM, Hallo netwerkverbinding of Hallo extern bureaublad-client op de hostcomputer. In dit artikel begeleidt u bij sommige Hallo veelgebruikte methoden tooresolve RDP-verbindingsproblemen. 

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Snelle stappen voor probleemoplossing
Opnieuw verbinding te maken toohello VM na elke stap voor probleemoplossing:

1. Extern bureaublad-configuratie opnieuw instellen.
2. Controleer de Netwerkbeveiligingsgroep regels / Cloud Services-eindpunten.
3. Bekijk de logboeken van de VM-console.
4. Opnieuw instellen van hello NIC voor Hallo VM.
5. Controleer Hallo resourcestatus van virtuele machine.
6. Uw VM-wachtwoord opnieuw instellen.
7. Opnieuw opstarten van de VM.
8. Implementeer uw virtuele machine opnieuw.

Blijven lezen als u meer gedetailleerde stappen en uitleg nodig. Controleer of deze lokale netwerkapparatuur zoals routers en firewalls worden niet geblokkeerd door uitgaande TCP-poort 3389, zoals aangegeven [RDP probleemoplossende scenario's beschreven](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Als hello **Connect** knop voor uw virtuele machine af lichter wordt weergegeven in de portal Hallo en u niet verbonden tooAzure via bent een [Express Route](../../expressroute/expressroute-introduction.md) of [Site-naar-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) verbinding, moet u toocreate en toewijzen van de VM een openbaar IP-adres oplossen voordat u extern bureaublad kunnen gebruiken. Er is meer informatie over [openbare IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) beschikbaar.


## <a name="ways-tootroubleshoot-rdp-issues"></a>Manieren tootroubleshoot RDP-problemen
U kunt virtuele machines die zijn gemaakt met behulp van Resource Manager-implementatiemodel Hallo via een van de volgende methoden Hallo oplossen:

* [Azure-portal](#using-the-azure-portal) - handig als u tooquickly moet Hallo RDP-configuratie of gebruikersreferenties opnieuw instellen en u geen Hallo van Azure-hulpprogramma's geïnstalleerd.
* [Azure PowerShell](#using-azure-powershell) : als u vertrouwd met een PowerShell-prompt snel opnieuw instellen van Hallo RDP-configuratie of gebruikersreferenties bent, met hello Azure PowerShell-cmdlets.

U vindt ook stappen over het oplossen van virtuele machines die zijn gemaakt met behulp van Hallo [klassieke implementatiemodel](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Problemen oplossen met hello Azure-portal
Probeer na elke stap tooyour VM opnieuw verbinding te maken. Als u nog steeds geen verbinding maken, probeert u de volgende stap Hallo.

1. **Opnieuw instellen van uw RDP-verbinding**. Deze stap herstelt Hallo RDP-configuratie als externe verbindingen zijn uitgeschakeld of als Windows Firewall-regels zijn RDP, bijvoorbeeld worden geblokkeerd.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **wachtwoord opnieuw instellen** knop. Set Hallo **modus** te**alleen opnieuw instellen van configuratie** en klik vervolgens op Hallo **Update** knop:
   
    ![Hallo RDP-configuratie in hello Azure-portal opnieuw instellen](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Controleer of de Netwerkbeveiligingsgroep regels**. Gebruik [IP-stroom controleren](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm als een regel in een Netwerkbeveiligingsgroep tooor van een virtuele machine verkeer blokkeert. U kunt ook effectieve beveiligingsgroep tooensure inkomende 'Toestaan' NSG regels regel bestaat en is geplaatst voor RDP-poort (standaard 3389) bekijken. Zie voor meer informatie [effectieve beveiligingsregels voor verbindingen met behulp van tootroubleshoot VM verkeer stroom](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Bekijk VM boot diagnostics**. Deze stap bekijkt hello VM console logboeken toodetermine als Hallo VM is een probleem melden. Niet alle virtuele machines hebben diagnostische gegevens over opstarten is ingeschakeld, zodat het mogelijk is deze stap optioneel.
   
    Specifieke stappen voor probleemoplossing buiten het bereik van dit artikel hello, maar kunnen duiden op een breder probleem dat invloed op RDP-verbinding. Zie voor meer informatie over het weergeven van Logboeken Hallo-console en de schermopname VM [diagnostische gegevens over opstarten voor virtuele machines](boot-diagnostics.md).

4. **Opnieuw instellen van Hallo NIC voor VM Hallo**. Zie voor meer informatie [hoe tooreset NIC voor de virtuele machine van Windows Azure](reset-network-interface.md).
5. **Controleer Hallo VM resourcestatus**. Deze stap controleert u of er zijn geen bekende problemen met hello Azure-platform die mogelijk van invloed op connectiviteit toohello VM.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **resourcestatus** knop. Een gezonde VM rapporten als **beschikbaar**:
   
    ![Controleer de status van de VM-resource in hello Azure-portal](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Opnieuw instellen van gebruikersreferenties**. Deze stap wordt opnieuw ingesteld wachtwoord Hallo op een lokale administrator-account wanneer u niet zeker weet of Hallo-referenties vergeten bent.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **wachtwoord opnieuw instellen** knop. Zorg ervoor dat Hallo **modus** te is ingesteld,**wachtwoord opnieuw instellen** en voer uw gebruikersnaam en een nieuw wachtwoord. Tot slot op Hallo **Update** knop:
   
    ![Hallo gebruikersreferenties in hello Azure-portal opnieuw instellen](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Opnieuw opstarten van uw virtuele machine**. Deze stap eventuele onderliggende problemen kunt corrigeren Hallo VM zelf heeft.
   
    Selecteer uw virtuele machine in hello Azure-portal en klik op Hallo **overzicht** tabblad. Klik op Hallo **opnieuw** knop:
   
    ![Opnieuw opstarten Hallo VM in hello Azure-portal](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Implementeer uw virtuele machine opnieuw**. Deze stap redeploys uw tooanother VM-host binnen Azure toocorrect eventuele onderliggende problemen van platform of netwerken.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **implementeren** knop en klik vervolgens op **implementeren**:
   
    ![Hallo VM in hello Azure-portal opnieuw implementeren](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Nadat deze is voltooid, is de kortstondige schijfgegevens verloren en dynamische IP-adressen die zijn gekoppeld aan Hallo VM worden bijgewerkt.

Als u nog steeds er RDP problemen zijn, kunt u [opent u een ondersteuningsaanvraag](https://azure.microsoft.com/support/options/) of lezen [meer gedetailleerde probleemoplossing concepten en stappen RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Problemen oplossen met Azure PowerShell
Als u dat nog niet gedaan hebt, [installeren en configureren van meest recente Azure PowerShell Hallo](/powershell/azure/overview).

Hallo volgende voorbeelden variabelen gebruiken zoals `myResourceGroup`, `myVM`, en `myVMAccessExtension`. Deze variabele bestandsnamen en locaties vervangen door uw eigen waarden.

> [!NOTE]
> U Hallo gebruikersreferenties en Hallo RDP-configuratie herstellen met behulp van Hallo [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell-cmdlet. In Hallo volgen voorbeelden, `myVMAccessExtension` is een naam die u als onderdeel van het Hallo-proces opgeeft. Als u eerder met Hallo VMAccessAgent hebt gewerkt, kunt u Hallo-naam van de bestaande extensie Hallo krijgen met behulp van `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck Hallo eigenschappen van Hallo VM. naam van tooview hello, kijk onder de sectie Hallo 'Extensions' hello uitvoer.

Probeer na elke stap tooyour VM opnieuw verbinding te maken. Als u nog steeds geen verbinding maken, probeert u de volgende stap Hallo.

1. **Opnieuw instellen van uw RDP-verbinding**. Deze stap herstelt Hallo RDP-configuratie als externe verbindingen zijn uitgeschakeld of als Windows Firewall-regels zijn RDP, bijvoorbeeld worden geblokkeerd.
   
    voorbeeld Hallo Hallo RDP-verbinding op een virtuele machine met de naam stelt `myVM` in Hallo `WestUS` locatie en in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Controleer of de Netwerkbeveiligingsgroep regels**. Deze stap controleert u of u een regel hebt in uw Netwerkbeveiligingsgroep toopermit RDP-verkeer. Hallo-standaardpoort voor RDP is TCP-poort 3389. Een regel toopermit RDP-verkeer kan niet automatisch gemaakt wanneer u uw virtuele machine maakt.
   
    Wijs eerst alle Hallo-configuratiegegevens voor de Netwerkbeveiligingsgroep toohello `$rules` variabele. Hallo volgende voorbeeld haalt informatie over Hallo Netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup` in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Bekijk nu Hallo-regels die zijn geconfigureerd voor deze Netwerkbeveiligingsgroep. Controleer of een regel bestaat tooallow TCP-poort 3389 voor binnenkomende verbindingen als volgt:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Hallo volgende voorbeeld ziet u een geldige beveiligingsregel waarmee RDP-verkeer is toegestaan. U kunt zien `Protocol`, `DestinationPortRange`, `Access`, en `Direction` correct zijn geconfigureerd:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Als u een regel waarmee RDP-verkeer niet hebt [maakt u een regel Netwerkbeveiligingsgroep](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). TCP-poort 3389 toestaan.
3. **Opnieuw instellen van gebruikersreferenties**. Hallo-wachtwoord op Hallo lokale administrator-account dat u opgeeft wanneer u niet zeker weet of bent vergeten, Hallo referenties opnieuw instellen in deze stap.
   
    Geef eerst Hallo gebruikersnaam en een nieuw wachtwoord door toe te wijzen referenties toohello `$cred` variabele als volgt:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Hallo-referenties op de virtuele machine nu bijwerken. Hallo volgende voorbeeld wordt bijgewerkt Hallo-referenties op een virtuele machine met de naam `myVM` in Hallo `WestUS` locatie en in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Opnieuw opstarten van uw virtuele machine**. Deze stap eventuele onderliggende problemen kunt corrigeren Hallo VM zelf heeft.
   
    Hallo voorbeeld opnieuw wordt opgestart na Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Implementeer uw virtuele machine opnieuw**. Deze stap redeploys uw tooanother VM-host binnen Azure toocorrect eventuele onderliggende problemen van platform of netwerken.
   
    voorbeeld redeploys na Hallo Hallo VM met de naam `myVM` in Hallo `WestUS` locatie en in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Als u nog steeds er RDP problemen zijn, kunt u [opent u een ondersteuningsaanvraag](https://azure.microsoft.com/support/options/) of lezen [meer gedetailleerde probleemoplossing concepten en stappen RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Virtuele machines die zijn gemaakt met behulp van de klassieke implementatiemodel Hallo oplossen
Probeer opnieuw verbinding te maken toohello VM na elke stap voor probleemoplossing.

1. **Opnieuw instellen van uw RDP-verbinding**. Deze stap herstelt Hallo RDP-configuratie als externe verbindingen zijn uitgeschakeld of als Windows Firewall-regels zijn RDP, bijvoorbeeld worden geblokkeerd.
   
    Selecteer uw virtuele machine in hello Azure-portal. Klik op Hallo **... Meer** knop en klik vervolgens op **externe toegang opnieuw instellen**:
   
    ![Hallo RDP-configuratie in hello Azure-portal opnieuw instellen](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Controleer of de Cloud Services-eindpunten**. Deze stap controleert u of u eindpunten hebt in uw Cloudservices toopermit RDP-verkeer. Hallo-standaardpoort voor RDP is TCP-poort 3389. Een regel toopermit RDP-verkeer kan niet automatisch gemaakt wanneer u uw virtuele machine maakt.
   
   Selecteer uw virtuele machine in hello Azure-portal. Klik op Hallo **eindpunten** knop tooview Hallo eindpunten die momenteel zijn geconfigureerd voor uw virtuele machine. Controleer of de eindpunten die RDP-verkeer op TCP-poort 3389 toestaan bestaan.
   
   Hallo volgende voorbeeld ziet u geldige eindpunten die RDP-verkeer toestaan:
   
   ![Controleer of de Cloud Services-eindpunten in hello Azure-portal](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Als u een eindpunt dat RDP-verkeer laat niet hebt [een Cloud Services-eindpunt maken](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). TCP-poort 3389 tooprivate toestaan.
3. **Bekijk VM boot diagnostics**. Deze stap bekijkt hello VM console logboeken toodetermine als Hallo VM is een probleem melden. Niet alle virtuele machines hebben diagnostische gegevens over opstarten is ingeschakeld, zodat het mogelijk is deze stap optioneel.
   
    Specifieke stappen voor probleemoplossing buiten het bereik van dit artikel hello, maar kunnen duiden op een breder probleem dat invloed op RDP-verbinding. Zie voor meer informatie over het weergeven van Logboeken Hallo-console en de schermopname VM [diagnostische gegevens over opstarten voor virtuele machines](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Controleer Hallo VM resourcestatus**. Deze stap controleert u of er zijn geen bekende problemen met hello Azure-platform die mogelijk van invloed op connectiviteit toohello VM.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **resourcestatus** knop. Een gezonde VM rapporten als **beschikbaar**:
   
    ![Controleer de status van de VM-resource in hello Azure-portal](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Opnieuw instellen van gebruikersreferenties**. Hallo-wachtwoord op Hallo lokale administrator-account dat u opgeeft wanneer u niet zeker weet of bent vergeten Hallo referenties opnieuw instellen in deze stap.
   
    Selecteer uw virtuele machine in hello Azure-portal. Schuif omlaag Hallo instellingen deelvenster toohello **ondersteuning + probleemoplossing** sectie aan de onderkant van het Hallo-lijst. Klik op Hallo **wachtwoord opnieuw instellen** knop. Voer uw gebruikersnaam en een nieuw wachtwoord. Tot slot op Hallo **opslaan** knop:
   
    ![Hallo gebruikersreferenties in hello Azure-portal opnieuw instellen](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Opnieuw opstarten van uw virtuele machine**. Deze stap eventuele onderliggende problemen kunt corrigeren Hallo VM zelf heeft.
   
    Selecteer uw virtuele machine in hello Azure-portal en klik op Hallo **overzicht** tabblad. Klik op Hallo **opnieuw** knop:
   
    ![Opnieuw opstarten Hallo VM in hello Azure-portal](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Als u nog steeds er RDP problemen zijn, kunt u [opent u een ondersteuningsaanvraag](https://azure.microsoft.com/support/options/) of lezen [meer gedetailleerde probleemoplossing concepten en stappen RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Specifieke RDP-fouten oplossen
U kunt een specifiek foutbericht kan optreden als u van tooconnect tooyour VM via RDP. Hallo Hieronder volgen de meestvoorkomende foutberichten Hallo:

* [Hallo externe sessie is beëindigd omdat er geen extern bureaublad-licentieservers beschikbaar tooprovide een licentie](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Extern bureaublad Hallo kan niet zoeken computer 'name'](troubleshoot-specific-rdp-errors.md#rdpname).
* [Er is een verificatiefout opgetreden. Hallo Local Security Authority is niet bereikbaar](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Fout bij de Windows-beveiliging: uw referenties werken niet](troubleshoot-specific-rdp-errors.md#wincred).
* [Deze computer kan geen verbinding van de externe computer toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Aanvullende bronnen
Als geen van deze fouten is opgetreden en u nog steeds geen verbinding toohello VM via Extern bureaublad maken, leest u Hallo gedetailleerde [problemen oplossen met extern bureaublad](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Zie voor probleemoplossing bij het openen van toepassingen die worden uitgevoerd op een virtuele machine, [problemen met toegang tooan toepassing die wordt uitgevoerd op een Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Als u problemen met het gebruik van Secure Shell (SSH) tooconnect tooa Linux VM in Azure hebt, raadpleegt u [oplossen SSH-verbindingen tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

