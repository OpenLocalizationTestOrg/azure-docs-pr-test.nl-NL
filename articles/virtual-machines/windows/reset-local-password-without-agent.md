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
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="5e568-103">Hoe tooreset lokale Windows-wachtwoord voor de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="5e568-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="5e568-104">U kunt opnieuw instellen Hallo lokale Windows-wachtwoord van een virtuele machine in Azure met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) opgegeven hello Azure guest-agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5e568-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="5e568-105">Deze methode is Hallo primaire manier tooreset een wachtwoord voor een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e568-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="5e568-106">Als u problemen met hello Azure gastagent niet reageert of tooinstall mislukken ondervindt na het uploaden van een aangepaste installatiekopie, kunt u handmatig een Windows-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="5e568-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="5e568-107">Dit artikel wordt uitgelegd hoe tooreset het wachtwoord van een lokale account door het koppelen van bron OS virtuele schijf tooanother VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e568-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="5e568-108">Gebruik deze methode alleen als een laatste toevlucht.</span><span class="sxs-lookup"><span data-stu-id="5e568-108">Only use this process as a last resort.</span></span> <span data-ttu-id="5e568-109">Probeer tooreset altijd een wachtwoord met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) eerste.</span><span class="sxs-lookup"><span data-stu-id="5e568-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="5e568-110">Overzicht van Hallo-proces</span><span class="sxs-lookup"><span data-stu-id="5e568-110">Overview of hello process</span></span>
<span data-ttu-id="5e568-111">Hallo core stappen voor het uitvoeren van een lokale wachtwoord opnieuw instellen voor een Windows-VM in Azure als er geen gastagent toegang toohello Azure is als volgt:</span><span class="sxs-lookup"><span data-stu-id="5e568-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="5e568-112">Verwijder Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="5e568-112">Delete hello source VM.</span></span> <span data-ttu-id="5e568-113">Hallo virtuele schijven worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="5e568-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="5e568-114">Hallo bron van de virtuele machine OS schijf tooanother VM op Hallo koppelen dezelfde locatie binnen uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5e568-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="5e568-115">Deze VM is waarnaar wordt verwezen tooas Hallo VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="5e568-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="5e568-116">Maak met Hallo probleemoplossing VM sommige configuratiebestanden op besturingssysteemschijf Hallo bron van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5e568-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="5e568-117">De besturingssysteemschijf Hallo van de virtuele machine uit Hallo probleemoplossing VM loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="5e568-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="5e568-118">Gebruik een sjabloon toocreate voor Resource Manager een virtuele machine met behulp van de oorspronkelijke virtuele schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e568-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="5e568-119">Wanneer hello nieuwe virtuele machine opnieuw is opgestart, Hallo configuratiebestanden maakt u update Hallo wachtwoord van gebruiker Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="5e568-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="5e568-120">Gedetailleerde stappen</span><span class="sxs-lookup"><span data-stu-id="5e568-120">Detailed steps</span></span>
<span data-ttu-id="5e568-121">Probeer tooreset altijd een wachtwoord met behulp van Hallo [Azure-portal of Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u probeert Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="5e568-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="5e568-122">Zorg ervoor dat er een back-up van uw virtuele machine voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="5e568-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="5e568-123">Verwijder Hallo van invloed op een virtuele machine in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5e568-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="5e568-124">Verwijderen Hallo VM verwijdert u alleen Hallo metagegevens, Hallo verwijzing van Hallo VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e568-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="5e568-125">Hallo virtuele schijven worden bewaard wanneer Hallo VM wordt verwijderd:</span><span class="sxs-lookup"><span data-stu-id="5e568-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="5e568-126">Selecteer Hallo VM in hello Azure-portal, klikt u op *verwijderen*:</span><span class="sxs-lookup"><span data-stu-id="5e568-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Bestaande virtuele machine verwijderen](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="5e568-128">Hallo bron van de virtuele machine OS schijf toohello probleemoplossing VM koppelen.</span><span class="sxs-lookup"><span data-stu-id="5e568-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="5e568-129">Hallo VM probleemoplossing moet Hallo dezelfde regio bevinden als de besturingssysteemschijf Hallo bron van de virtuele machine (zoals `West US`):</span><span class="sxs-lookup"><span data-stu-id="5e568-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="5e568-130">Selecteer Hallo VM probleemoplossing in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5e568-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="5e568-131">Klik op *schijven* | *Attach bestaande*:</span><span class="sxs-lookup"><span data-stu-id="5e568-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Bestaande schijf koppelen](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="5e568-133">Selecteer *VHD-bestand* en selecteer vervolgens Hallo storage-account met de bron-VM:</span><span class="sxs-lookup"><span data-stu-id="5e568-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Opslagaccount selecteren](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="5e568-135">Selecteer de bron-container Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e568-135">Select hello source container.</span></span> <span data-ttu-id="5e568-136">Hallo-sourceoplossingen is doorgaans *VHD's*:</span><span class="sxs-lookup"><span data-stu-id="5e568-136">hello source container is typically *vhds*:</span></span>
     
     ![Storage-container selecteren](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="5e568-138">Selecteer Hallo OS vhd tooattach.</span><span class="sxs-lookup"><span data-stu-id="5e568-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="5e568-139">Klik op *Selecteer* toocomplete Hallo proces:</span><span class="sxs-lookup"><span data-stu-id="5e568-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Selecteer de virtuele bronschijf](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="5e568-141">Verbinding maken met het oplossen van problemen met extern bureaublad VM toohello en zorg ervoor dat besturingssysteemschijf Hallo bron van de virtuele machine wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5e568-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="5e568-142">Selecteer Hallo VM probleemoplossing in hello Azure-portal en klik op *Connect*.</span><span class="sxs-lookup"><span data-stu-id="5e568-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="5e568-143">Open Hallo RDP-bestand dat wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="5e568-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="5e568-144">Hallo-gebruikersnaam en wachtwoord Hallo probleemoplossing VM invoeren.</span><span class="sxs-lookup"><span data-stu-id="5e568-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="5e568-145">Zoek naar Hallo gegevensschijf bijgevoegde in Windows Verkenner.</span><span class="sxs-lookup"><span data-stu-id="5e568-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="5e568-146">Als hello bron van de virtuele machine VHD hello alleen gegevens schijf is gekoppeld aan toohello probleemoplossing van de virtuele machine, moet het Hallo F: station:</span><span class="sxs-lookup"><span data-stu-id="5e568-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![De schijf bijgesloten gegevens weergeven](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="5e568-148">Maak `gpt.ini` in `\Windows\System32\GroupPolicy` op Hallo bron van de virtuele machine station (als gpt.ini bestaat, wijzig toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="5e568-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="5e568-149">Zorg ervoor dat u niet per ongeluk maken de volgende bestanden in C:\Windows hello, OS-station voor probleemoplossing VM Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e568-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="5e568-150">Maken de volgende bestanden in Hallo OS-station voor de bron-VM die is gekoppeld als een gegevensschijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e568-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="5e568-151">Toevoegen van de volgende regels in Hallo Hallo `gpt.ini` dat u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5e568-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Gpt.ini maken](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="5e568-153">Maak `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="5e568-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="5e568-154">Zorg ervoor dat verborgen mappen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e568-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="5e568-155">Maak indien nodig Hallo `Machine` of `Scripts` mappen.</span><span class="sxs-lookup"><span data-stu-id="5e568-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="5e568-156">Toevoegen van de volgende regels Hallo Hallo `scripts.ini` dat u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5e568-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Scripts.ini maken](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="5e568-158">Maak `FixAzureVM.cmd` in `\Windows\System32` Hello inhoud te volgen en vervangt `<username>` en `<newpassword>` met uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="5e568-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd maken](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="5e568-160">U moet voldoen aan de vereisten voor wachtwoordcomplexiteit Hallo geconfigureerd voor uw virtuele machine bij het definiëren van nieuwe Hallo-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5e568-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="5e568-161">Ontkoppel Hallo schijf van Hallo probleemoplossing VM in Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="5e568-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="5e568-162">Hallo VM probleemoplossing in hello Azure-portal, klik op *schijven*.</span><span class="sxs-lookup"><span data-stu-id="5e568-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="5e568-163">Selecteer Hallo gegevensschijf gekoppeld in stap 2, klikt u op *Detach*:</span><span class="sxs-lookup"><span data-stu-id="5e568-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Loskoppelen van schijf](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="5e568-165">Voordat u een virtuele machine maken, verkrijgen Hallo URI tooyour bronschijf-besturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="5e568-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="5e568-166">Selecteer Hallo storage-account in hello Azure-portal, klikt u op *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="5e568-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="5e568-167">Selecteer Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="5e568-167">Select hello container.</span></span> <span data-ttu-id="5e568-168">Hallo-sourceoplossingen is doorgaans *VHD's*:</span><span class="sxs-lookup"><span data-stu-id="5e568-168">hello source container is typically *vhds*:</span></span>
     
     ![Storage-blob voor account selecteren](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="5e568-170">Selecteer de bron-VHD voor VM-OS en klikt u op Hallo *kopie* knop volgende toohello *URL* naam:</span><span class="sxs-lookup"><span data-stu-id="5e568-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Kopiëren van schijf URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="5e568-172">Een virtuele machine maken van de besturingssysteemschijf Hallo bron van de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="5e568-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="5e568-173">Gebruik [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate een virtuele machine vanaf een speciale VHD.</span><span class="sxs-lookup"><span data-stu-id="5e568-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="5e568-174">Klik op Hallo `Deploy tooAzure` knop tooopen hello Azure-portal met Hallo sjablonen details ingevuld voor u.</span><span class="sxs-lookup"><span data-stu-id="5e568-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="5e568-175">Als u tooretain alle vorige Hallo-instellingen voor Hallo VM wilt, selecteer *template bewerken* tooprovide uw bestaande VNet, subnet, netwerkadapter of openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5e568-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="5e568-176">In Hallo `OSDISKVHDURI` parametervak plakken Hallo-URI van de bron-VHD in de voorgaande stap Hallo verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="5e568-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Maak een VM van sjabloon](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="5e568-178">Na Hallo nieuwe virtuele machine wordt uitgevoerd, verbinding maken met virtuele machine via Extern bureaublad met Hallo nieuwe wachtwoord die u hebt opgegeven in Hallo toohello `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="5e568-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="5e568-179">Nieuwe virtuele machine verwijderen Hallo volgende bestanden van de externe sessie toohello tooclean Hallo-omgeving:</span><span class="sxs-lookup"><span data-stu-id="5e568-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="5e568-180">Van %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="5e568-180">From %windir%\System32</span></span>
      * <span data-ttu-id="5e568-181">FixAzureVM.cmd verwijderen</span><span class="sxs-lookup"><span data-stu-id="5e568-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="5e568-182">Van %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="5e568-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="5e568-183">scripts.ini verwijderen</span><span class="sxs-lookup"><span data-stu-id="5e568-183">remove scripts.ini</span></span>
    * <span data-ttu-id="5e568-184">Van %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="5e568-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="5e568-185">gpt.ini verwijderen (indien gpt.ini bestond en hernoemd u toogpt.ini.bak, wijzig de naam van Hallo .bak-bestand back toogpt.ini)</span><span class="sxs-lookup"><span data-stu-id="5e568-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e568-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e568-186">Next steps</span></span>
<span data-ttu-id="5e568-187">Als u nog steeds geen verbinding maken met extern bureaublad, raadpleegt u Hallo [RDP-probleemoplossingsgids](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e568-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5e568-188">Hallo [RDP probleemoplossingsgids gedetailleerde](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) gekeken naar het oplossen van methoden in plaats van specifieke stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5e568-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="5e568-189">U kunt ook [opent u een Azure ondersteuningsaanvraag](https://azure.microsoft.com/support/options/) voor praktische hulp.</span><span class="sxs-lookup"><span data-stu-id="5e568-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

