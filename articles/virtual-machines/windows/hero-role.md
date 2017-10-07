---
title: aaaInstall IIS op uw eerste virtuele Windows-machine | Microsoft Docs
description: Experimenteer met uw eerste virtuele Windows-computer door IIS installeren en openen met behulp van poort 80 hello Azure-portal.
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Experimenteer met een rol installeren op uw Windows-VM
Zodra u uw eerste virtuele machine (VM) up en wordt uitgevoerd hebt, kunt u gaan tooinstalling software en services. Voor deze zelfstudie gaan we toouse Serverbeheer op Hallo VM van Windows Server tooinstall IIS. Vervolgens wordt er een Netwerkbeveiligingsgroep (NSG) met behulp van hello Azure portal tooopen poort 80 tooIIS verkeer maakt. 

Als u al uw eerste virtuele machine dat nog niet hebt gemaakt, moet gaat u terug te[uw eerste virtuele Windows-machine maken in Azure-portal Hallo](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u doorgaat met deze zelfstudie.

## <a name="make-sure-hello-vm-is-running"></a>Zorg ervoor dat Hallo die VM wordt uitgevoerd
1. Open Hallo [Azure-portal](https://portal.azure.com).
2. Klik op het menu hub Hallo **virtuele Machines**. Selecteer Hallo virtuele machine uit de lijst Hallo.
3. Als de status van de Hallo **gestopt (Deallocated)**, klikt u op Hallo **Start** knop op Hallo **Essentials** blade Hallo VM. Als de status van de Hallo **met**, kunt u op de volgende stap toohello.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Verbinding maken met toohello virtuele machine en aanmelden
1. Klik op het menu hub Hallo **virtuele Machines**. Selecteer Hallo virtuele machine uit de lijst Hallo.
2. Klik op de blade voor de virtuele machine van Hallo Hallo **Connect**. Hiermee maakt en een Remote Desktop Protocol-bestand (.rdp-bestand) dat lijkt op een machine snelkoppeling tooconnect tooyour downloadt. Wilt u mogelijk toosave Hallo bestand tooyour bureaublad voor eenvoudige toegang. **Open** dit bestand tooconnect tooyour VM.
   
    ![Schermopname van hello Azure portal weergeeft hoe tooconnect tooyour VM](./media/hero-role/connect.png)
3. U gewaarschuwd dat .rdp Hallo van een onbekende uitgever is. Dit is normaal. Klik in het venster extern bureaublad Hallo op **Connect** toocontinue.
   
    ![Schermafbeelding met waarschuwing over een onbekende uitgever](./media/hero-role/rdp-warn.png)
4. In het venster Windows-beveiliging Hallo Hallo type Hallo gebruikersnaam en wachtwoord voor lokaal account Hallo die u hebt gemaakt tijdens het maken van VM. Hallo gebruikersnaam wordt ingevoerd als *vmname*&#92; *gebruikersnaam*, klikt u vervolgens op **OK**.
   
    ![Schermopname van het Hallo VM-naam, gebruikersnaam en wachtwoord invoeren](./media/hero-role/credentials.png)
5. U gewaarschuwd dat Hallo-certificaat kan niet worden geverifieerd. Dit is normaal. Klik op **Ja** tooverify Hallo identiteit van Hallo virtuele machine en aanmelden te voltooien.
   
   ![Schermafbeelding met een bericht over het verifiëren van de identiteit Hallo Hallo VM](./media/hero-role/cert-warning.png)

Als u in tootrouble uitvoert wanneer u tooconnect probeert, Zie [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>IIS installeren op de virtuele machine
Nu dat u bent aangemeld in toohello VM, wordt er een serverfunctie installeren zodat u meer kunt experimenteren.

1. Open **Serverbeheer** als dit nog niet is geopend. Klik op Hallo **Start** menu en klik vervolgens op **Serverbeheer**.
2. In **Serverbeheer**, selecteer **lokale Server** in het linkerdeelvenster Hallo. 
3. Selecteer in het menu Hallo **beheren** > **functies en onderdelen toevoegen**.
4. In het Hallo toevoegen Wizard functies en onderdelen, op Hallo **installatietype** pagina **op basis van functie of onderdeel gebaseerde installatie**, en klik vervolgens op **volgende**.
   
    ![Schermopname die laat zien Hallo Wizard Functies toevoegen en onderdelen tabblad installatietype](./media/hero-role/role-wizard.png)
5. Selecteer Hallo VM uit Hallo servergroep en klik op **volgende**.
6. Op Hallo **serverfuncties** pagina **webserver (IIS)**.
   
    ![Schermopname die laat zien Hallo Wizard Functies toevoegen en onderdelen tabblad serverfuncties](./media/hero-role/add-iis.png)
7. Hallo pop over het toevoegen van functies die nodig zijn voor IIS, zorg ervoor dat **beheerprogramma's opnemen** is geselecteerd en klik vervolgens op **onderdelen toevoegen**. Wanneer Hallo pop-upvenster wordt gesloten, klikt u op **volgende** in Hallo-wizard.
   
    ![Schermopname van de pop-tooconfirm Hallo IIS-functie toevoegen](./media/hero-role/confirm-add-feature.png)
8. Klik op de pagina onderdelen Hallo **volgende**.
9. Op Hallo **webserverfunctie (IIS)** pagina, klikt u op **volgende**. 
10. Op Hallo **functieservices** pagina, klikt u op **volgende**. 
11. Op Hallo **bevestiging** pagina, klikt u op **installeren**. 
12. Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten** op Hallo-wizard.

## <a name="open-port-80"></a>Poort 80 openen
Om uw VM tooaccept al het verkeer via poort 80, moet u tooadd een inkomende regel toohello netwerkbeveiligingsgroep toevoegen. 

1. Open Hallo [Azure-portal](https://portal.azure.com).
2. In **virtuele machines** Selecteer Hallo VM die u hebt gemaakt.
3. Selecteer in de instellingen voor virtuele machines Hallo **netwerkinterfaces** en vervolgens selecteert Hallo bestaande netwerkinterface.
   
    ![Schermopname van de instelling van de virtuele machine Hallo voor Hallo netwerkinterfaces](./media/hero-role/network-interface.png)
4. In **Essentials** voor netwerkinterface hello, klikt u op Hallo **netwerkbeveiligingsgroep**.
   
    ![Schermopname van Hallo Essentials sectie voor de netwerkinterface Hallo](./media/hero-role/select-nsg.png)
5. In Hallo **Essentials** blade voor Hallo NSG, moet u een bestaande standaard regel voor binnenkomende hebben **standaard-toestaan rdp** waarmee u toolog in toohello VM. Voegt u een andere regel voor binnenkomende verbindingen tooallow IIS-verkeer. Klik op **Binnenkomende beveiligingsregel**.
   
    ![Schermopname van Hallo Essentials sectie voor Hallo NSG](./media/hero-role/inbound.png)
6. Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.
   
    ![Schermopname van Hallo knop tooadd een beveiligingsregel](./media/hero-role/add-rule.png)
7. Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**. Type **80** in Hallo poortbereik en zorg ervoor dat **toestaan** is geselecteerd. Klik als u klaar bent op **OK**.
   
    ![Schermopname van Hallo knop tooadd een beveiligingsregel](./media/hero-role/port-80.png)

Zie voor meer informatie over het nsg's, regels voor binnenkomende en uitgaande [toestaan externe toegang tooyour virtuele machine met behulp van hello Azure-portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Verbinding maken met toohello standaard IIS-website
1. Klik in hello Azure-portal, op **virtuele machines** en selecteer vervolgens uw virtuele machine.
2. In Hallo **Essentials** blade-, Kopieer uw **openbaar IP-adres**.
   
    ![Schermopname die laat zien waar toofind Hallo openbare IP-adres van uw virtuele machine](./media/hero-role/ipaddress.png)
3. Open een browser en in de adresbalk hello, typt u in uw openbare IP-adres als volgt: http://<publicIPaddress> en klik op **Enter** toogo toothat adres.
4. Uw browser moet Hallo IIS standaardwebpagina openen. Deze ziet er ongeveer als volgt:
   
    ![Schermopname die laat zien welke Hallo-standaardpagina IIS ziet eruit als in een browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Volgende stappen
* U kunt ook experimenteren met [koppelen van een gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtuele machine. Gegevensschijven bieden meer opslagruimte voor uw virtuele machine.

