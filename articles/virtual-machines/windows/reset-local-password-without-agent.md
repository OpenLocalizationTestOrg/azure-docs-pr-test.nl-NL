---
title: een lokale Windows-wachtwoord zonder Azure-agent aaaReset | Microsoft Docs
description: "Hoe tooreset wachtwoord van een lokale Windows-gebruikersaccount Hallo wanneer hello Azure guest-agent is niet geïnstalleerd of op een virtuele machine werkt"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Hoe tooreset lokale Windows-wachtwoord voor de virtuele machine in Azure
U kunt opnieuw instellen Hallo lokale Windows-wachtwoord van een virtuele machine in Azure met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) opgegeven hello Azure guest-agent is geïnstalleerd. Deze methode is Hallo primaire manier tooreset een wachtwoord voor een virtuele machine in Azure. Als u problemen met hello Azure gastagent niet reageert of tooinstall mislukken ondervindt na het uploaden van een aangepaste installatiekopie, kunt u handmatig een Windows-wachtwoord opnieuw instellen. Dit artikel wordt uitgelegd hoe tooreset het wachtwoord van een lokale account door het koppelen van bron OS virtuele schijf tooanother VM Hallo. 

> [!WARNING]
> Gebruik deze methode alleen als een laatste toevlucht. Probeer tooreset altijd een wachtwoord met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) eerste.
> 
> 

## <a name="overview-of-hello-process"></a>Overzicht van Hallo-proces
Hallo core stappen voor het uitvoeren van een lokale wachtwoord opnieuw instellen voor een Windows-VM in Azure als er geen gastagent toegang toohello Azure is als volgt:

* Verwijder Hallo bron-VM. Hallo virtuele schijven worden bewaard.
* Hallo bron van de virtuele machine OS schijf tooanother VM op Hallo koppelen dezelfde locatie binnen uw Azure-abonnement. Deze VM is waarnaar wordt verwezen tooas Hallo VM probleemoplossing.
* Maak met Hallo probleemoplossing VM sommige configuratiebestanden op besturingssysteemschijf Hallo bron van de virtuele machine.
* De besturingssysteemschijf Hallo van de virtuele machine uit Hallo probleemoplossing VM loskoppelen.
* Gebruik een sjabloon toocreate voor Resource Manager een virtuele machine met behulp van de oorspronkelijke virtuele schijf Hallo.
* Wanneer hello nieuwe virtuele machine opnieuw is opgestart, Hallo configuratiebestanden maakt u update Hallo wachtwoord van gebruiker Hallo vereist.

## <a name="detailed-steps"></a>Gedetailleerde stappen
Probeer tooreset altijd een wachtwoord met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u probeert Hallo stappen te volgen. Zorg ervoor dat er een back-up van uw virtuele machine voordat u begint. 

1. Verwijder Hallo van invloed op een virtuele machine in Azure-portal. Verwijderen Hallo VM verwijdert u alleen Hallo metagegevens, Hallo verwijzing van Hallo VM in Azure. Hallo virtuele schijven worden bewaard wanneer Hallo VM wordt verwijderd:
   
   * Selecteer Hallo VM in hello Azure-portal, klikt u op *verwijderen*:
     
     ![Bestaande virtuele machine verwijderen](./media/reset-local-password-without-agent/delete_vm.png)
2. Hallo bron van de virtuele machine OS schijf toohello probleemoplossing VM koppelen. Hallo VM probleemoplossing moet Hallo dezelfde regio bevinden als de besturingssysteemschijf Hallo bron van de virtuele machine (zoals `West US`):
   
   * Selecteer Hallo VM probleemoplossing in hello Azure-portal. Klik op *schijven* | *Attach bestaande*:
     
     ![Bestaande schijf koppelen](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Selecteer *VHD-bestand* en selecteer vervolgens Hallo storage-account met de bron-VM:
     
     ![Opslagaccount selecteren](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Selecteer de bron-container Hallo. Hallo-sourceoplossingen is doorgaans *VHD's*:
     
     ![Storage-container selecteren](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Selecteer Hallo OS vhd tooattach. Klik op *Selecteer* toocomplete Hallo proces:
     
     ![Selecteer de virtuele bronschijf](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Verbinding maken met het oplossen van problemen met extern bureaublad VM toohello en zorg ervoor dat besturingssysteemschijf Hallo bron van de virtuele machine wordt weergegeven:
   
   * Selecteer Hallo VM probleemoplossing in hello Azure-portal en klik op *Connect*.
   * Open Hallo RDP-bestand dat wordt gedownload. Hallo-gebruikersnaam en wachtwoord Hallo probleemoplossing VM invoeren.
   * Zoek naar Hallo gegevensschijf bijgevoegde in Windows Verkenner. Als hello bron van de virtuele machine VHD hello alleen gegevens schijf is gekoppeld aan toohello probleemoplossing van de virtuele machine, moet het Hallo F: station:
     
     ![De schijf bijgesloten gegevens weergeven](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Maak `gpt.ini` in `\Windows\System32\GroupPolicy` op Hallo bron van de virtuele machine station (als gpt.ini bestaat, wijzig toogpt.ini.bak):
   
   > [!WARNING]
   > Zorg ervoor dat u niet per ongeluk maken de volgende bestanden in C:\Windows hello, OS-station voor probleemoplossing VM Hallo Hallo. Maken de volgende bestanden in Hallo OS-station voor de bron-VM die is gekoppeld als een gegevensschijf Hallo.
   > 
   > 
   
   * Toevoegen van de volgende regels in Hallo Hallo `gpt.ini` dat u hebt gemaakt:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Gpt.ini maken](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Maak `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`. Zorg ervoor dat verborgen mappen worden weergegeven. Maak indien nodig Hallo `Machine` of `Scripts` mappen.
   
   * Toevoegen van de volgende regels Hallo Hallo `scripts.ini` dat u hebt gemaakt:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Scripts.ini maken](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Maak `FixAzureVM.cmd` in `\Windows\System32` Hello inhoud te volgen en vervangt `<username>` en `<newpassword>` met uw eigen waarden:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd maken](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    U moet voldoen aan de vereisten voor wachtwoordcomplexiteit Hallo geconfigureerd voor uw virtuele machine bij het definiëren van nieuwe Hallo-wachtwoord.
7. Ontkoppel Hallo schijf van Hallo probleemoplossing VM in Azure-portal:
   
   * Hallo VM probleemoplossing in hello Azure-portal, klik op *schijven*.
   * Selecteer Hallo gegevensschijf gekoppeld in stap 2, klikt u op *Detach*:
     
     ![Loskoppelen van schijf](./media/reset-local-password-without-agent/detach_disk.png)
8. Voordat u een virtuele machine maken, verkrijgen Hallo URI tooyour bronschijf-besturingssysteem:
   
   * Selecteer Hallo storage-account in hello Azure-portal, klikt u op *Blobs*.
   * Selecteer Hallo-container. Hallo-sourceoplossingen is doorgaans *VHD's*:
     
     ![Storage-blob voor account selecteren](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Selecteer de bron-VHD voor VM-OS en klikt u op Hallo *kopie* knop volgende toohello *URL* naam:
     
     ![Kopiëren van schijf URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Een virtuele machine maken van de besturingssysteemschijf Hallo bron van de virtuele machine:
   
   * Gebruik [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate een virtuele machine vanaf een speciale VHD. Klik op Hallo `Deploy tooAzure` knop tooopen hello Azure-portal met Hallo sjablonen details ingevuld voor u.
   * Als u tooretain alle vorige Hallo-instellingen voor Hallo VM wilt, selecteer *template bewerken* tooprovide uw bestaande VNet, subnet, netwerkadapter of openbare IP-adres.
   * In Hallo `OSDISKVHDURI` parametervak plakken Hallo-URI van de bron-VHD in de voorgaande stap Hallo verkrijgen:
     
     ![Maak een VM van sjabloon](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Na Hallo nieuwe virtuele machine wordt uitgevoerd, verbinding maken met virtuele machine via Extern bureaublad met Hallo nieuwe wachtwoord die u hebt opgegeven in Hallo toohello `FixAzureVM.cmd` script.
11. Nieuwe virtuele machine verwijderen Hallo volgende bestanden van de externe sessie toohello tooclean Hallo-omgeving:
    
    * Van %windir%\System32
      * FixAzureVM.cmd verwijderen
    * Van %windir%\System32\GroupPolicy\Machine\
      * scripts.ini verwijderen
    * Van %windir%\System32\GroupPolicy
      * gpt.ini verwijderen (indien gpt.ini bestond en hernoemd u toogpt.ini.bak, wijzig de naam van Hallo .bak-bestand back toogpt.ini)

## <a name="next-steps"></a>Volgende stappen
Als u nog steeds geen verbinding maken met extern bureaublad, raadpleegt u Hallo [RDP-probleemoplossingsgids](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hallo [RDP probleemoplossingsgids gedetailleerde](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) gekeken naar het oplossen van methoden in plaats van specifieke stappen uitvoeren. U kunt ook [opent u een Azure ondersteuningsaanvraag](https://azure.microsoft.com/support/options/) voor praktische hulp.

