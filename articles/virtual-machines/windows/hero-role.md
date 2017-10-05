---
title: IIS installeren op uw eerste virtuele Windows-machine | Microsoft Docs
description: Uw eerste virtuele Windows-machine experimenteren door IIS en openen van poort 80 met behulp van de Azure-portal te installeren.
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
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Experimenteer met een rol installeren op uw Windows-VM
Zodra u uw eerste virtuele machine (VM) zetten hebt, kunt u op verplaatsen naar het installeren van software en services. Voor deze zelfstudie gaan we gebruik van Serverbeheer op de virtuele machine van Windows Server IIS te installeren. We Maak vervolgens een Netwerkbeveiligingsgroep (NSG) met de Azure portal poort 80 voor verkeer van IIS te openen. 

Als u al uw eerste virtuele machine dat nog niet hebt gemaakt, moet gaat u terug naar [uw eerste virtuele Windows-machine maken in de Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u doorgaat met deze zelfstudie.

## <a name="make-sure-the-vm-is-running"></a>Zorg ervoor dat de VM wordt uitgevoerd
1. Open de [Azure Portal](https://portal.azure.com).
2. Klik in het menu Hub op **Virtuele machines**. Selecteer de virtuele machine in de lijst.
3. Als de status **gestopt (Deallocated)**, klikt u op de **Start** knop op de **Essentials** blade van de virtuele machine. Als de status **met**, kunt u op met de volgende stap.

## <a name="connect-to-the-virtual-machine-and-sign-in"></a>Verbinding maken met de virtuele machine en aanmelden
1. Klik in het menu Hub op **Virtuele machines**. Selecteer de virtuele machine in de lijst.
2. Klik op de blade voor de virtuele machine op **Verbinden**. Er wordt nu een Remote Desktop Protocol-bestand (RDP-bestand) gemaakt en gedownload. Een RDP-bestand is een soort snelkoppeling om verbinding te maken met uw computer. Uit oogpunt van gemak is het mogelijk een goed idee om het bestand op uw bureaublad op te slaan. **Open** dit bestand om verbinding te maken met de virtuele machine.
   
    ![Schermafbeelding van de Azure Portal waarin wordt getoond hoe u verbinding maakt met uw VM](./media/hero-role/connect.png)
3. U ontvangt een waarschuwing dat het RDP-bestand van een onbekende uitgever is. Dit is normaal. Klik in het venster Extern bureaublad op **Verbinden** om door te gaan.
   
    ![Schermafbeelding met waarschuwing over een onbekende uitgever](./media/hero-role/rdp-warn.png)
4. Typ in het venster Windows-beveiliging de gebruikersnaam en het wachtwoord voor het lokale account dat u hebt gemaakt tijdens het maken van de virtuele machine. U voert de gebruikersnaam in als *naam_van_virtuele_machine*&#92;*gebruikersnaam*. Klik vervolgens op **OK**.
   
    ![Schermafbeelding van de VM-naam, gebruikersnaam en wachtwoord invoeren](./media/hero-role/credentials.png)
5. U ontvangt een waarschuwing dat het certificaat niet kan worden geverifieerd. Dit is normaal. Klik op **Ja** om de identiteit van de virtuele machine te controleren en het aanmelden te voltooien.
   
   ![Schermafbeelding met een bericht over het verifiëren van de identiteit van de VM](./media/hero-role/cert-warning.png)

Als u problemen ondervindt wanneer u verbinding probeert te maken, raadpleegt u [Problemen oplossen met Extern bureaublad-verbindingen met een virtuele Windows-machine in Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>IIS installeren op de virtuele machine
Nu u bent aangemeld bij de virtuele machine gaan we een serverfunctie installeren zodat u meer kunt experimenteren.

1. Open **Serverbeheer** als dit nog niet is geopend. Klik op de **Start** menu en klik vervolgens op **Serverbeheer**.
2. Selecteer in **Serverbeheer** de optie **Lokale server** in het linkerdeelvenster. 
3. Selecteer in het menu **Beheren** > **Functies en onderdelen toevoegen**.
4. In de Wizard functies en functies toevoegen op de **installatietype** pagina **op basis van functie of onderdeel gebaseerde installatie**, en klik vervolgens op **volgende**.
   
    ![Schermopname van het tabblad Wizard Functies toevoegen en onderdelen voor Type installatie](./media/hero-role/role-wizard.png)
5. Selecteer de virtuele machine in de serverpool en klik op **Volgende**.
6. Selecteer op de pagina **Serverfuncties** de optie **Webserver (IIS)**.
   
    ![Schermopname van het tabblad Wizard Functies toevoegen en onderdelen voor serverfuncties](./media/hero-role/add-iis.png)
7. Controleer of in het pop-upvenster over het toevoegen van functies die nodig zijn voor IIS dat **Beheerprogramma's opnemen (indien van toepassing)** is geselecteerd en klik vervolgens op **Onderdelen toevoegen**. Als het pop-upvenster wordt gesloten, klikt u in de wizard op **Volgende**.
   
    ![Schermopname van het pop-om te bevestigen dat u de IIS-functie](./media/hero-role/confirm-add-feature.png)
8. Klik op de pagina met onderdelen op **Volgende**.
9. Klik op de pagina **Webserverfunctie (IIS)** op **Volgende**. 
10. Klik op de pagina **Functieservices** op **Volgende**. 
11. Klik op de pagina **Bevestiging** op **Installeren**. 
12. Klik nadat de installatie is voltooid op **Sluiten** in de wizard.

## <a name="open-port-80"></a>Poort 80 openen
Als u wilt dat uw virtuele machine binnenkomend verkeer accepteert via poort 80, moet u een regel voor binnenkomend verkeer toevoegen aan de netwerkbeveiligingsgroep. 

1. Open de [Azure Portal](https://portal.azure.com).
2. In **virtuele machines** selecteert u de virtuele machine die u hebt gemaakt.
3. Selecteer in de instellingen voor virtuele machines **netwerkinterfaces** en selecteer vervolgens de bestaande netwerkinterface.
   
    ![Schermopname van de instelling van de virtuele machine voor de netwerkinterfaces](./media/hero-role/network-interface.png)
4. In **Essentials** voor de netwerkinterface, klikt u op de **netwerkbeveiligingsgroep**.
   
    ![Schermopname van de sectie Essentials voor de netwerkinterface](./media/hero-role/select-nsg.png)
5. Op de blade **Essentials** voor de netwerkbeveiligingsgroep moet u één bestaande regel voor binnenkomend verkeer hebben voor **default-allow-rdp** waarmee u zich kunt aanmelden bij de virtuele machine. U moet een andere regel voor binnenkomend verkeer toevoegen voor IIS-verkeer. Klik op **Binnenkomende beveiligingsregel**.
   
    ![Schermopname van de sectie Essentials voor het NSG](./media/hero-role/inbound.png)
6. Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.
   
    ![Schermafbeelding met de knop een beveiligingsregel toevoegen](./media/hero-role/add-rule.png)
7. Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**. Type **80** in het poortbereik en zorg ervoor dat **Toestaan** is geselecteerd. Klik als u klaar bent op **OK**.
   
    ![Schermafbeelding met de knop een beveiligingsregel toevoegen](./media/hero-role/port-80.png)

Zie [Externe toegang tot de virtuele machine toestaan met behulp van de Azure Portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over netwerkbeveiligingsgroepen en regels voor binnenkomend en uitgaand verkeer.

## <a name="connect-to-the-default-iis-website"></a>Verbinding maken met de standaardwebsite van IIS
1. Klik in de Azure Portal op **Virtuele machines** en selecteer de virtuele machine.
2. Kopieer op de blade **Essentials** uw **Openbare IP-adres**.
   
    ![Schermopname die laat zien waar vind ik het openbare IP-adres van uw virtuele machine](./media/hero-role/ipaddress.png)
3. Open een browser en typ uw openbare IP-adres als volgt in de adresbalk: http://<publicIPaddress> en klik op **Enter** om naar dat adres te gaan.
4. Uw browser moet de standaard IIS-webpagina geopend. Deze ziet er ongeveer als volgt:
   
    ![Schermopname die laat zien hoe de standaard IIS-pagina eruit in een browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Volgende stappen
* U kunt ook experimenteren met het [koppelen van een gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) aan de virtuele machine. Gegevensschijven bieden meer opslagruimte voor uw virtuele machine.

