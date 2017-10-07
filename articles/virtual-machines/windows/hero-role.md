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
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="8b003-103">Experimenteer met een rol installeren op uw Windows-VM</span><span class="sxs-lookup"><span data-stu-id="8b003-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="8b003-104">Zodra u uw eerste virtuele machine (VM) up en wordt uitgevoerd hebt, kunt u gaan tooinstalling software en services.</span><span class="sxs-lookup"><span data-stu-id="8b003-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="8b003-105">Voor deze zelfstudie gaan we toouse Serverbeheer op Hallo VM van Windows Server tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="8b003-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="8b003-106">Vervolgens wordt er een Netwerkbeveiligingsgroep (NSG) met behulp van hello Azure portal tooopen poort 80 tooIIS verkeer maakt.</span><span class="sxs-lookup"><span data-stu-id="8b003-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="8b003-107">Als u al uw eerste virtuele machine dat nog niet hebt gemaakt, moet gaat u terug te[uw eerste virtuele Windows-machine maken in Azure-portal Hallo](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u doorgaat met deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8b003-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="8b003-108">Zorg ervoor dat Hallo die VM wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="8b003-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="8b003-109">Open Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b003-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8b003-110">Klik op het menu hub Hallo **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="8b003-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8b003-111">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b003-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="8b003-112">Als de status van de Hallo **gestopt (Deallocated)**, klikt u op Hallo **Start** knop op Hallo **Essentials** blade Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8b003-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="8b003-113">Als de status van de Hallo **met**, kunt u op de volgende stap toohello.</span><span class="sxs-lookup"><span data-stu-id="8b003-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="8b003-114">Verbinding maken met toohello virtuele machine en aanmelden</span><span class="sxs-lookup"><span data-stu-id="8b003-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="8b003-115">Klik op het menu hub Hallo **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="8b003-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8b003-116">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b003-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="8b003-117">Klik op de blade voor de virtuele machine van Hallo Hallo **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8b003-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="8b003-118">Hiermee maakt en een Remote Desktop Protocol-bestand (.rdp-bestand) dat lijkt op een machine snelkoppeling tooconnect tooyour downloadt.</span><span class="sxs-lookup"><span data-stu-id="8b003-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="8b003-119">Wilt u mogelijk toosave Hallo bestand tooyour bureaublad voor eenvoudige toegang.</span><span class="sxs-lookup"><span data-stu-id="8b003-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="8b003-120">**Open** dit bestand tooconnect tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="8b003-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Schermopname van hello Azure portal weergeeft hoe tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="8b003-122">U gewaarschuwd dat .rdp Hallo van een onbekende uitgever is.</span><span class="sxs-lookup"><span data-stu-id="8b003-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="8b003-123">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="8b003-123">This is normal.</span></span> <span data-ttu-id="8b003-124">Klik in het venster extern bureaublad Hallo op **Connect** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8b003-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Schermafbeelding met waarschuwing over een onbekende uitgever](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="8b003-126">In het venster Windows-beveiliging Hallo Hallo type Hallo gebruikersnaam en wachtwoord voor lokaal account Hallo die u hebt gemaakt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="8b003-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="8b003-127">Hallo gebruikersnaam wordt ingevoerd als *vmname*&#92; *gebruikersnaam*, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b003-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Schermopname van het Hallo VM-naam, gebruikersnaam en wachtwoord invoeren](./media/hero-role/credentials.png)
5. <span data-ttu-id="8b003-129">U gewaarschuwd dat Hallo-certificaat kan niet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="8b003-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="8b003-130">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="8b003-130">This is normal.</span></span> <span data-ttu-id="8b003-131">Klik op **Ja** tooverify Hallo identiteit van Hallo virtuele machine en aanmelden te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8b003-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Schermafbeelding met een bericht over het verifiëren van de identiteit Hallo Hallo VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="8b003-133">Als u in tootrouble uitvoert wanneer u tooconnect probeert, Zie [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b003-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="8b003-134">IIS installeren op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8b003-134">Install IIS on your VM</span></span>
<span data-ttu-id="8b003-135">Nu dat u bent aangemeld in toohello VM, wordt er een serverfunctie installeren zodat u meer kunt experimenteren.</span><span class="sxs-lookup"><span data-stu-id="8b003-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="8b003-136">Open **Serverbeheer** als dit nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="8b003-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="8b003-137">Klik op Hallo **Start** menu en klik vervolgens op **Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="8b003-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="8b003-138">In **Serverbeheer**, selecteer **lokale Server** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b003-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="8b003-139">Selecteer in het menu Hallo **beheren** > **functies en onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8b003-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="8b003-140">In het Hallo toevoegen Wizard functies en onderdelen, op Hallo **installatietype** pagina **op basis van functie of onderdeel gebaseerde installatie**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8b003-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Schermopname die laat zien Hallo Wizard Functies toevoegen en onderdelen tabblad installatietype](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="8b003-142">Selecteer Hallo VM uit Hallo servergroep en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8b003-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="8b003-143">Op Hallo **serverfuncties** pagina **webserver (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="8b003-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Schermopname die laat zien Hallo Wizard Functies toevoegen en onderdelen tabblad serverfuncties](./media/hero-role/add-iis.png)
7. <span data-ttu-id="8b003-145">Hallo pop over het toevoegen van functies die nodig zijn voor IIS, zorg ervoor dat **beheerprogramma's opnemen** is geselecteerd en klik vervolgens op **onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8b003-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="8b003-146">Wanneer Hallo pop-upvenster wordt gesloten, klikt u op **volgende** in Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="8b003-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Schermopname van de pop-tooconfirm Hallo IIS-functie toevoegen](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="8b003-148">Klik op de pagina onderdelen Hallo **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8b003-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="8b003-149">Op Hallo **webserverfunctie (IIS)** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8b003-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="8b003-150">Op Hallo **functieservices** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8b003-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="8b003-151">Op Hallo **bevestiging** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="8b003-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="8b003-152">Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten** op Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="8b003-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="8b003-153">Poort 80 openen</span><span class="sxs-lookup"><span data-stu-id="8b003-153">Open port 80</span></span>
<span data-ttu-id="8b003-154">Om uw VM tooaccept al het verkeer via poort 80, moet u tooadd een inkomende regel toohello netwerkbeveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8b003-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="8b003-155">Open Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b003-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8b003-156">In **virtuele machines** Selecteer Hallo VM die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8b003-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="8b003-157">Selecteer in de instellingen voor virtuele machines Hallo **netwerkinterfaces** en vervolgens selecteert Hallo bestaande netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="8b003-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Schermopname van de instelling van de virtuele machine Hallo voor Hallo netwerkinterfaces](./media/hero-role/network-interface.png)
4. <span data-ttu-id="8b003-159">In **Essentials** voor netwerkinterface hello, klikt u op Hallo **netwerkbeveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="8b003-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Schermopname van Hallo Essentials sectie voor de netwerkinterface Hallo](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="8b003-161">In Hallo **Essentials** blade voor Hallo NSG, moet u een bestaande standaard regel voor binnenkomende hebben **standaard-toestaan rdp** waarmee u toolog in toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8b003-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="8b003-162">Voegt u een andere regel voor binnenkomende verbindingen tooallow IIS-verkeer.</span><span class="sxs-lookup"><span data-stu-id="8b003-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="8b003-163">Klik op **Binnenkomende beveiligingsregel**.</span><span class="sxs-lookup"><span data-stu-id="8b003-163">Click **Inbound security rule**.</span></span>
   
    ![Schermopname van Hallo Essentials sectie voor Hallo NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="8b003-165">Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8b003-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Schermopname van Hallo knop tooadd een beveiligingsregel](./media/hero-role/add-rule.png)
7. <span data-ttu-id="8b003-167">Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8b003-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="8b003-168">Type **80** in Hallo poortbereik en zorg ervoor dat **toestaan** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8b003-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="8b003-169">Klik als u klaar bent op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b003-169">When you are done, click **OK**.</span></span>
   
    ![Schermopname van Hallo knop tooadd een beveiligingsregel](./media/hero-role/port-80.png)

<span data-ttu-id="8b003-171">Zie voor meer informatie over het nsg's, regels voor binnenkomende en uitgaande [toestaan externe toegang tooyour virtuele machine met behulp van hello Azure-portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8b003-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="8b003-172">Verbinding maken met toohello standaard IIS-website</span><span class="sxs-lookup"><span data-stu-id="8b003-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="8b003-173">Klik in hello Azure-portal, op **virtuele machines** en selecteer vervolgens uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b003-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="8b003-174">In Hallo **Essentials** blade-, Kopieer uw **openbaar IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="8b003-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Schermopname die laat zien waar toofind Hallo openbare IP-adres van uw virtuele machine](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="8b003-176">Open een browser en in de adresbalk hello, typt u in uw openbare IP-adres als volgt: http://<publicIPaddress> en klik op **Enter** toogo toothat adres.</span><span class="sxs-lookup"><span data-stu-id="8b003-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="8b003-177">Uw browser moet Hallo IIS standaardwebpagina openen.</span><span class="sxs-lookup"><span data-stu-id="8b003-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="8b003-178">Deze ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="8b003-178">It looks something like this:</span></span>
   
    ![Schermopname die laat zien welke Hallo-standaardpagina IIS ziet eruit als in een browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="8b003-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b003-180">Next steps</span></span>
* <span data-ttu-id="8b003-181">U kunt ook experimenteren met [koppelen van een gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b003-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="8b003-182">Gegevensschijven bieden meer opslagruimte voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b003-182">Data disks provide more storage for your virtual machine.</span></span>

