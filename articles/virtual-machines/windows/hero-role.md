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
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="08aab-103">Experimenteer met een rol installeren op uw Windows-VM</span><span class="sxs-lookup"><span data-stu-id="08aab-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="08aab-104">Zodra u uw eerste virtuele machine (VM) zetten hebt, kunt u op verplaatsen naar het installeren van software en services.</span><span class="sxs-lookup"><span data-stu-id="08aab-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="08aab-105">Voor deze zelfstudie gaan we gebruik van Serverbeheer op de virtuele machine van Windows Server IIS te installeren.</span><span class="sxs-lookup"><span data-stu-id="08aab-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="08aab-106">We Maak vervolgens een Netwerkbeveiligingsgroep (NSG) met de Azure portal poort 80 voor verkeer van IIS te openen.</span><span class="sxs-lookup"><span data-stu-id="08aab-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="08aab-107">Als u al uw eerste virtuele machine dat nog niet hebt gemaakt, moet gaat u terug naar [uw eerste virtuele Windows-machine maken in de Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat u doorgaat met deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="08aab-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="08aab-108">Zorg ervoor dat de VM wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="08aab-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="08aab-109">Open de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08aab-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="08aab-110">Klik in het menu Hub op **Virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="08aab-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="08aab-111">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="08aab-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="08aab-112">Als de status **gestopt (Deallocated)**, klikt u op de **Start** knop op de **Essentials** blade van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="08aab-113">Als de status **met**, kunt u op met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="08aab-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="08aab-114">Verbinding maken met de virtuele machine en aanmelden</span><span class="sxs-lookup"><span data-stu-id="08aab-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="08aab-115">Klik in het menu Hub op **Virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="08aab-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="08aab-116">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="08aab-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="08aab-117">Klik op de blade voor de virtuele machine op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="08aab-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="08aab-118">Er wordt nu een Remote Desktop Protocol-bestand (RDP-bestand) gemaakt en gedownload. Een RDP-bestand is een soort snelkoppeling om verbinding te maken met uw computer.</span><span class="sxs-lookup"><span data-stu-id="08aab-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="08aab-119">Uit oogpunt van gemak is het mogelijk een goed idee om het bestand op uw bureaublad op te slaan.</span><span class="sxs-lookup"><span data-stu-id="08aab-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="08aab-120">**Open** dit bestand om verbinding te maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-120">**Open** this file to connect to your VM.</span></span>
   
    ![Schermafbeelding van de Azure Portal waarin wordt getoond hoe u verbinding maakt met uw VM](./media/hero-role/connect.png)
3. <span data-ttu-id="08aab-122">U ontvangt een waarschuwing dat het RDP-bestand van een onbekende uitgever is.</span><span class="sxs-lookup"><span data-stu-id="08aab-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="08aab-123">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="08aab-123">This is normal.</span></span> <span data-ttu-id="08aab-124">Klik in het venster Extern bureaublad op **Verbinden** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="08aab-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Schermafbeelding met waarschuwing over een onbekende uitgever](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="08aab-126">Typ in het venster Windows-beveiliging de gebruikersnaam en het wachtwoord voor het lokale account dat u hebt gemaakt tijdens het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="08aab-127">U voert de gebruikersnaam in als *naam_van_virtuele_machine*&#92;*gebruikersnaam*. Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="08aab-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Schermafbeelding van de VM-naam, gebruikersnaam en wachtwoord invoeren](./media/hero-role/credentials.png)
5. <span data-ttu-id="08aab-129">U ontvangt een waarschuwing dat het certificaat niet kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="08aab-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="08aab-130">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="08aab-130">This is normal.</span></span> <span data-ttu-id="08aab-131">Klik op **Ja** om de identiteit van de virtuele machine te controleren en het aanmelden te voltooien.</span><span class="sxs-lookup"><span data-stu-id="08aab-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Schermafbeelding met een bericht over het verifiëren van de identiteit van de VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="08aab-133">Als u problemen ondervindt wanneer u verbinding probeert te maken, raadpleegt u [Problemen oplossen met Extern bureaublad-verbindingen met een virtuele Windows-machine in Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08aab-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="08aab-134">IIS installeren op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="08aab-134">Install IIS on your VM</span></span>
<span data-ttu-id="08aab-135">Nu u bent aangemeld bij de virtuele machine gaan we een serverfunctie installeren zodat u meer kunt experimenteren.</span><span class="sxs-lookup"><span data-stu-id="08aab-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="08aab-136">Open **Serverbeheer** als dit nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="08aab-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="08aab-137">Klik op de **Start** menu en klik vervolgens op **Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="08aab-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="08aab-138">Selecteer in **Serverbeheer** de optie **Lokale server** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="08aab-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="08aab-139">Selecteer in het menu **Beheren** > **Functies en onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08aab-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="08aab-140">In de Wizard functies en functies toevoegen op de **installatietype** pagina **op basis van functie of onderdeel gebaseerde installatie**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Schermopname van het tabblad Wizard Functies toevoegen en onderdelen voor Type installatie](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="08aab-142">Selecteer de virtuele machine in de serverpool en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="08aab-143">Selecteer op de pagina **Serverfuncties** de optie **Webserver (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="08aab-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Schermopname van het tabblad Wizard Functies toevoegen en onderdelen voor serverfuncties](./media/hero-role/add-iis.png)
7. <span data-ttu-id="08aab-145">Controleer of in het pop-upvenster over het toevoegen van functies die nodig zijn voor IIS dat **Beheerprogramma's opnemen (indien van toepassing)** is geselecteerd en klik vervolgens op **Onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08aab-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="08aab-146">Als het pop-upvenster wordt gesloten, klikt u in de wizard op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Schermopname van het pop-om te bevestigen dat u de IIS-functie](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="08aab-148">Klik op de pagina met onderdelen op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="08aab-149">Klik op de pagina **Webserverfunctie (IIS)** op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="08aab-150">Klik op de pagina **Functieservices** op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08aab-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="08aab-151">Klik op de pagina **Bevestiging** op **Installeren**.</span><span class="sxs-lookup"><span data-stu-id="08aab-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="08aab-152">Klik nadat de installatie is voltooid op **Sluiten** in de wizard.</span><span class="sxs-lookup"><span data-stu-id="08aab-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="08aab-153">Poort 80 openen</span><span class="sxs-lookup"><span data-stu-id="08aab-153">Open port 80</span></span>
<span data-ttu-id="08aab-154">Als u wilt dat uw virtuele machine binnenkomend verkeer accepteert via poort 80, moet u een regel voor binnenkomend verkeer toevoegen aan de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="08aab-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="08aab-155">Open de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08aab-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="08aab-156">In **virtuele machines** selecteert u de virtuele machine die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08aab-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="08aab-157">Selecteer in de instellingen voor virtuele machines **netwerkinterfaces** en selecteer vervolgens de bestaande netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="08aab-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Schermopname van de instelling van de virtuele machine voor de netwerkinterfaces](./media/hero-role/network-interface.png)
4. <span data-ttu-id="08aab-159">In **Essentials** voor de netwerkinterface, klikt u op de **netwerkbeveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="08aab-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Schermopname van de sectie Essentials voor de netwerkinterface](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="08aab-161">Op de blade **Essentials** voor de netwerkbeveiligingsgroep moet u één bestaande regel voor binnenkomend verkeer hebben voor **default-allow-rdp** waarmee u zich kunt aanmelden bij de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="08aab-162">U moet een andere regel voor binnenkomend verkeer toevoegen voor IIS-verkeer.</span><span class="sxs-lookup"><span data-stu-id="08aab-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="08aab-163">Klik op **Binnenkomende beveiligingsregel**.</span><span class="sxs-lookup"><span data-stu-id="08aab-163">Click **Inbound security rule**.</span></span>
   
    ![Schermopname van de sectie Essentials voor het NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="08aab-165">Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08aab-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Schermafbeelding met de knop een beveiligingsregel toevoegen](./media/hero-role/add-rule.png)
7. <span data-ttu-id="08aab-167">Klik in **Binnenkomende beveiligingsregels** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08aab-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="08aab-168">Type **80** in het poortbereik en zorg ervoor dat **Toestaan** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="08aab-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="08aab-169">Klik als u klaar bent op **OK**.</span><span class="sxs-lookup"><span data-stu-id="08aab-169">When you are done, click **OK**.</span></span>
   
    ![Schermafbeelding met de knop een beveiligingsregel toevoegen](./media/hero-role/port-80.png)

<span data-ttu-id="08aab-171">Zie [Externe toegang tot de virtuele machine toestaan met behulp van de Azure Portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over netwerkbeveiligingsgroepen en regels voor binnenkomend en uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="08aab-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="08aab-172">Verbinding maken met de standaardwebsite van IIS</span><span class="sxs-lookup"><span data-stu-id="08aab-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="08aab-173">Klik in de Azure Portal op **Virtuele machines** en selecteer de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="08aab-174">Kopieer op de blade **Essentials** uw **Openbare IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="08aab-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Schermopname die laat zien waar vind ik het openbare IP-adres van uw virtuele machine](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="08aab-176">Open een browser en typ uw openbare IP-adres als volgt in de adresbalk: http://<publicIPaddress> en klik op **Enter** om naar dat adres te gaan.</span><span class="sxs-lookup"><span data-stu-id="08aab-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="08aab-177">Uw browser moet de standaard IIS-webpagina geopend.</span><span class="sxs-lookup"><span data-stu-id="08aab-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="08aab-178">Deze ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="08aab-178">It looks something like this:</span></span>
   
    ![Schermopname die laat zien hoe de standaard IIS-pagina eruit in een browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="08aab-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08aab-180">Next steps</span></span>
* <span data-ttu-id="08aab-181">U kunt ook experimenteren met het [koppelen van een gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="08aab-182">Gegevensschijven bieden meer opslagruimte voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08aab-182">Data disks provide more storage for your virtual machine.</span></span>

