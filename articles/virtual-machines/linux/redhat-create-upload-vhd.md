---
title: Maken en uploaden van een Red Hat Enterprise Linux VHD voor gebruik in Azure | Microsoft Docs
description: Informatie over het maken en uploaden van een Azure virtuele harde schijf (VHD) waarop een Red Hat Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="523d0-103">Een op Red Hat gebaseerde virtuele machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="523d0-104">In dit artikel leert u hoe u een virtuele machine van Red Hat Enterprise Linux (RHEL) voorbereidt voor gebruik in Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="523d0-105">De versies van RHEL die worden beschreven in dit artikel zijn 6.7 + en 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="523d0-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="523d0-106">De hypervisors voor voorbereiding die worden besproken in dit artikel zijn Hyper-V, op basis van de kernel virtuele machine (KVM) en VMware.</span><span class="sxs-lookup"><span data-stu-id="523d0-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="523d0-107">Zie voor meer informatie over de vereisten voor in aanmerking komt voor deelname aan het programma voor toegang tot de Cloud van Red Hat [Red Hat van toegang tot de Cloud website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) en [RHEL uitgevoerd op Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="523d0-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="523d0-108">Voorbereiden van een Red Hat-virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="523d0-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="523d0-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="523d0-109">Prerequisites</span></span>
<span data-ttu-id="523d0-110">Deze sectie wordt ervan uitgegaan dat u hebt al een ISO-bestand van de website van Red Hat verkregen en de installatiekopie van het RHEL geïnstalleerd op een virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="523d0-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="523d0-111">Zie voor meer informatie over het gebruik van Hyper-V-beheer voor het installeren van een besturingssysteeminstallatiekopie [de Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="523d0-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="523d0-112">**Opmerkingen bij de installatie van de RHEL**</span><span class="sxs-lookup"><span data-stu-id="523d0-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="523d0-113">Azure biedt geen ondersteuning voor VHDX-indeling.</span><span class="sxs-lookup"><span data-stu-id="523d0-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="523d0-114">Azure ondersteunt alleen vaste VHD.</span><span class="sxs-lookup"><span data-stu-id="523d0-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="523d0-115">U kunt Hyper-V-beheer de schijf converteren naar VHD-indeling of kunt u de cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="523d0-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="523d0-116">Als u VirtualBox gebruikt, selecteert u **een vaste grootte** in plaats van de standaard dynamisch toegewezen optie wanneer u de schijf maken.</span><span class="sxs-lookup"><span data-stu-id="523d0-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="523d0-117">Azure ondersteunt alleen virtuele machines van generatie 1.</span><span class="sxs-lookup"><span data-stu-id="523d0-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="523d0-118">U kunt virtuele machines van generatie 1 converteren uit VHDX voor de VHD-indeling en dynamisch uitbreidbare naar een schijf met vaste grootte.</span><span class="sxs-lookup"><span data-stu-id="523d0-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="523d0-119">U kunt een virtuele machine generatie niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="523d0-120">Zie voor meer informatie [moet ik een virtuele machine van generatie 1 of 2 maken in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="523d0-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="523d0-121">De maximale grootte die toegestaan voor de VHD is 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="523d0-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="523d0-122">Wanneer u de Linux-besturingssysteem installeert, wordt u aangeraden dat u standaard partities in plaats van logische Volume Manager (LVM) Dit is vaak de standaardwaarde voor vele installaties.</span><span class="sxs-lookup"><span data-stu-id="523d0-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="523d0-123">Hierdoor wordt voorkomen LVM naam conflicteert met de gekloonde virtuele machines, met name als u ooit een schijf koppelen aan een andere identieke virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="523d0-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="523d0-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="523d0-125">Kernel-ondersteuning voor het koppelen van bestandssystemen Universal UDF (Disk Format) is vereist.</span><span class="sxs-lookup"><span data-stu-id="523d0-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="523d0-126">Op de eerste keer opstarten op Azure geeft de UDF-indeling media die is gekoppeld aan de Gast de configuratie van de inrichting aan de virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="523d0-127">De Azure Linux Agent moet kunnen de UDF-bestandssysteem voor het lezen van de configuratie en inrichten van de virtuele machine te koppelen.</span><span class="sxs-lookup"><span data-stu-id="523d0-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="523d0-128">Versies van de kernel Linux die ouder dan 2.6.37 zijn ondersteunen geen niet-uniforme geheugentoegang (NUMA) op Hyper-V met grotere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="523d0-129">Dit probleem voornamelijk effecten oudere distributies die gebruikmaken van de upstream-kernel Red Hat 2.6.32 en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="523d0-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="523d0-130">Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of RHEL-kernels die ouder dan 2.6.32-504 zijn moeten ingesteld de `numa=off` parameter op de opdrachtregel van de kernel in grub.conf opstart.</span><span class="sxs-lookup"><span data-stu-id="523d0-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="523d0-131">Zie voor meer informatie, Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="523d0-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="523d0-132">Configureer een partitie van de wisseling niet op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="523d0-133">De Linux-Agent kan worden geconfigureerd voor het maken van een wisselbestand op de tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="523d0-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="523d0-134">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="523d0-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="523d0-135">Alle VHD's moeten hebben-groottes met veelvouden van 1 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="523d0-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="523d0-136">Voorbereiden van een RHEL 6 virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="523d0-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="523d0-137">Selecteer de virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="523d0-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="523d0-138">Klik op **Connect** om een consolevenster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="523d0-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="523d0-139">In de RHEL 6, NetworkManager kan leiden tot problemen met de Azure Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="523d0-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="523d0-140">Dit pakket verwijderen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="523d0-141">Creëer of bewerk de `/etc/sysconfig/network` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="523d0-142">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="523d0-143">Verplaats de udev-regels om te voorkomen dat statische regels voor de Ethernet-interface te genereren (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="523d0-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="523d0-144">Deze regels veroorzaken problemen wanneer u een virtuele machine in Microsoft Azure- of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="523d0-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="523d0-145">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="523d0-146">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="523d0-147">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-148">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="523d0-149">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-150">Open hiertoe deze wijziging, `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat de kernel standaard de volgende parameters bevat:</span><span class="sxs-lookup"><span data-stu-id="523d0-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="523d0-151">Dit ook zorgt ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="523d0-152">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="523d0-153">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="523d0-154">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-155">Houd er rekening mee dat deze parameter de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer reduceert.</span><span class="sxs-lookup"><span data-stu-id="523d0-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="523d0-156">Deze configuratie mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="523d0-157">RHEL 6.5 en eerdere moet ook worden ingesteld de `numa=off` kernel-parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="523d0-158">Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="523d0-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="523d0-159">Zorg ervoor dat de secure shell (SSH)-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten, doorgaans de standaardinstelling is.</span><span class="sxs-lookup"><span data-stu-id="523d0-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="523d0-160">Wijzig /etc/ssh/sshd_config zodanig dat de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="523d0-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="523d0-161">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="523d0-162">Installatie van het pakket WALinuxAgent verwijdert de NetworkManager en NetworkManager gnome pakketten als ze zijn niet verwijderd in stap 3.</span><span class="sxs-lookup"><span data-stu-id="523d0-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="523d0-163">Maak geen wisselruimte op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="523d0-164">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-165">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en dat deze kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-166">Nadat u de Azure Linux Agent in de vorige stap hebt geïnstalleerd, op de juiste wijze de volgende parameters in /etc/waagent.conf wijzigen:</span><span class="sxs-lookup"><span data-stu-id="523d0-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="523d0-167">Hef de registratie van het abonnement (indien nodig) met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="523d0-168">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="523d0-169">Klik op **actie** > **afgesloten** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="523d0-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="523d0-170">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="523d0-171">Voorbereiden van een RHEL 7 virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="523d0-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="523d0-172">Selecteer de virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="523d0-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="523d0-173">Klik op **Connect** om een consolevenster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="523d0-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="523d0-174">Creëer of bewerk de `/etc/sysconfig/network` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="523d0-175">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="523d0-176">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="523d0-177">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="523d0-178">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-179">Open hiertoe deze wijziging, `/etc/default/grub` in een teksteditor en bewerk de `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="523d0-180">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="523d0-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="523d0-181">Dit ook zorgt ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="523d0-182">Deze configuratie schakelt ook uit de nieuwe RHEL 7 naamconventies voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="523d0-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="523d0-183">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="523d0-184">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="523d0-185">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-186">Houd er rekening mee dat deze parameter wordt gereduceerd de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="523d0-187">Nadat u klaar bent bewerken `/etc/default/grub`, voer de volgende opdracht voor het opnieuw samenstellen van de configuratie van de grub:</span><span class="sxs-lookup"><span data-stu-id="523d0-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="523d0-188">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten, doorgaans de standaardinstelling is.</span><span class="sxs-lookup"><span data-stu-id="523d0-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="523d0-189">Wijzig `/etc/ssh/sshd_config` om op te nemen van de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="523d0-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="523d0-190">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-191">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="523d0-192">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="523d0-193">Maak geen wisselruimte op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="523d0-194">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-195">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-196">Nadat u de Azure Linux Agent hebt geïnstalleerd in de vorige stap, wijzigt u de volgende parameters in `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="523d0-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="523d0-197">Als u wilt de registratie van het abonnement, voert u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="523d0-198">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="523d0-199">Klik op **actie** > **afgesloten** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="523d0-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="523d0-200">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="523d0-201">Een Red Hat-virtuele machine uit KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="523d0-202">Een virtuele machine van RHEL 6 uit KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="523d0-203">De installatiekopie KVM RHEL 6 downloaden van de website van Red Hat.</span><span class="sxs-lookup"><span data-stu-id="523d0-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="523d0-204">Een root-wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="523d0-204">Set a root password.</span></span>

    <span data-ttu-id="523d0-205">Een versleutelde wachtwoord genereren en kopieer de uitvoer van de opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="523d0-206">Stel het wachtwoord voor een hoofdaccount met guestfish:</span><span class="sxs-lookup"><span data-stu-id="523d0-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="523d0-207">Het tweede veld wijzigen voor de hoofdgebruiker van '. '</span><span class="sxs-lookup"><span data-stu-id="523d0-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="523d0-208">in het versleutelde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="523d0-208">to the encrypted password.</span></span>

3. <span data-ttu-id="523d0-209">Een virtuele machine van de installatiekopie van het qcow2 in KVM maken.</span><span class="sxs-lookup"><span data-stu-id="523d0-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="523d0-210">Het schijftype ingesteld op **qcow2**, en stel het virtuele netwerk interface model op **virtio**.</span><span class="sxs-lookup"><span data-stu-id="523d0-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="523d0-211">Vervolgens de virtuele machine starten en meld u aan als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="523d0-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="523d0-212">Creëer of bewerk de `/etc/sysconfig/network` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="523d0-213">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="523d0-214">Verplaats de udev-regels om te voorkomen dat statische regels voor de Ethernet-interface te genereren (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="523d0-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="523d0-215">Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="523d0-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="523d0-216">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="523d0-217">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="523d0-218">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-219">Open hiertoe deze configuratie, `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat de kernel standaard de volgende parameters bevat:</span><span class="sxs-lookup"><span data-stu-id="523d0-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="523d0-220">Dit ook zorgt ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="523d0-221">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="523d0-222">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="523d0-223">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-224">Houd er rekening mee dat deze parameter wordt gereduceerd de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="523d0-225">RHEL 6.5 en eerdere moet ook worden ingesteld de `numa=off` kernel-parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="523d0-226">Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="523d0-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="523d0-227">Hyper-V-modules toevoegen aan initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="523d0-228">Bewerken `/etc/dracut.conf`, en voeg de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="523d0-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="523d0-229">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="523d0-230">Cloud-init verwijderen:</span><span class="sxs-lookup"><span data-stu-id="523d0-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="523d0-231">Controleer of de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten:</span><span class="sxs-lookup"><span data-stu-id="523d0-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="523d0-232">Wijzig /etc/ssh/sshd_config zodanig dat de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="523d0-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="523d0-233">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-234">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="523d0-235">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="523d0-236">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-237">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-238">Nadat u de Azure Linux Agent hebt geïnstalleerd in de vorige stap, wijzigt u de volgende parameters in **/etc/waagent.conf** op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="523d0-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="523d0-239">Hef de registratie van het abonnement (indien nodig) met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="523d0-240">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="523d0-241">De virtuele machine in KVM afgesloten.</span><span class="sxs-lookup"><span data-stu-id="523d0-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="523d0-242">De installatiekopie van het qcow2 converteren naar het VHD-indeling.</span><span class="sxs-lookup"><span data-stu-id="523d0-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="523d0-243">De installatiekopie eerst niet converteren naar onbewerkte indeling:</span><span class="sxs-lookup"><span data-stu-id="523d0-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="523d0-244">Zorg ervoor dat de grootte van de onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="523d0-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="523d0-245">Anders wordt de grootte uitgelijnd met 1 MB afronden:</span><span class="sxs-lookup"><span data-stu-id="523d0-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="523d0-246">De onbewerkte schijf converteren naar een vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="523d0-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="523d0-247">Een virtuele machine voor RHEL 7 van KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="523d0-248">Download de installatiekopie van het KVM RHEL 7 van de website van Red Hat.</span><span class="sxs-lookup"><span data-stu-id="523d0-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="523d0-249">Deze procedure maakt gebruik van RHEL 7 als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="523d0-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="523d0-250">Een root-wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="523d0-250">Set a root password.</span></span>

    <span data-ttu-id="523d0-251">Een versleutelde wachtwoord genereren en kopieer de uitvoer van de opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="523d0-252">Stel het wachtwoord voor een hoofdaccount met guestfish:</span><span class="sxs-lookup"><span data-stu-id="523d0-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="523d0-253">Het tweede veld wijzigen voor de hoofdgebruiker van '. '</span><span class="sxs-lookup"><span data-stu-id="523d0-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="523d0-254">in het versleutelde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="523d0-254">to the encrypted password.</span></span>

3. <span data-ttu-id="523d0-255">Een virtuele machine van de installatiekopie van het qcow2 in KVM maken.</span><span class="sxs-lookup"><span data-stu-id="523d0-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="523d0-256">Het schijftype ingesteld op **qcow2**, en stel het virtuele netwerk interface model op **virtio**.</span><span class="sxs-lookup"><span data-stu-id="523d0-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="523d0-257">Vervolgens de virtuele machine starten en meld u aan als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="523d0-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="523d0-258">Creëer of bewerk de `/etc/sysconfig/network` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="523d0-259">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="523d0-260">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="523d0-261">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="523d0-262">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-263">Open hiertoe deze configuratie, `/etc/default/grub` in een teksteditor en bewerk de `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="523d0-264">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="523d0-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="523d0-265">Met deze opdracht zorgt er ook voor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="523d0-266">De opdracht schakelt ook uit de nieuwe RHEL 7 naamconventies voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="523d0-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="523d0-267">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="523d0-268">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="523d0-269">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-270">Houd er rekening mee dat deze parameter wordt gereduceerd de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="523d0-271">Nadat u klaar bent bewerken `/etc/default/grub`, voer de volgende opdracht voor het opnieuw samenstellen van de configuratie van de grub:</span><span class="sxs-lookup"><span data-stu-id="523d0-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="523d0-272">Hyper-V-modules toevoegen aan initramfs.</span><span class="sxs-lookup"><span data-stu-id="523d0-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="523d0-273">Bewerken `/etc/dracut.conf` en inhoud toevoegen:</span><span class="sxs-lookup"><span data-stu-id="523d0-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="523d0-274">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="523d0-275">Cloud-init verwijderen:</span><span class="sxs-lookup"><span data-stu-id="523d0-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="523d0-276">Controleer of de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten:</span><span class="sxs-lookup"><span data-stu-id="523d0-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="523d0-277">Wijzig /etc/ssh/sshd_config zodanig dat de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="523d0-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="523d0-278">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-279">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="523d0-280">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="523d0-281">Schakel de waagent-service:</span><span class="sxs-lookup"><span data-stu-id="523d0-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="523d0-282">Maak geen wisselruimte op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="523d0-283">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-284">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-285">Nadat u de Azure Linux Agent hebt geïnstalleerd in de vorige stap, wijzigt u de volgende parameters in `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="523d0-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="523d0-286">Hef de registratie van het abonnement (indien nodig) met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="523d0-287">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="523d0-288">De virtuele machine in KVM afgesloten.</span><span class="sxs-lookup"><span data-stu-id="523d0-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="523d0-289">De installatiekopie van het qcow2 converteren naar het VHD-indeling.</span><span class="sxs-lookup"><span data-stu-id="523d0-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="523d0-290">De installatiekopie eerst niet converteren naar onbewerkte indeling:</span><span class="sxs-lookup"><span data-stu-id="523d0-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="523d0-291">Zorg ervoor dat de grootte van de onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="523d0-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="523d0-292">Anders wordt de grootte uitgelijnd met 1 MB afronden:</span><span class="sxs-lookup"><span data-stu-id="523d0-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="523d0-293">De onbewerkte schijf converteren naar een vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="523d0-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="523d0-294">Een Red Hat-virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="523d0-295">Vereisten</span><span class="sxs-lookup"><span data-stu-id="523d0-295">Prerequisites</span></span>
<span data-ttu-id="523d0-296">Deze sectie wordt ervan uitgegaan dat u al een RHEL virtuele machine in VMware hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="523d0-297">Zie voor meer informatie over het installeren van een besturingssysteem in VMware [VMware Guest Operating System installatiehandleiding](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="523d0-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="523d0-298">Wanneer u de Linux-besturingssysteem installeert, wordt u aangeraden dat u standaard partities in plaats van LVM, dit is vaak de standaardwaarde voor vele installaties.</span><span class="sxs-lookup"><span data-stu-id="523d0-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="523d0-299">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machine, met name als de schijf van een besturingssysteem ooit worden gekoppeld aan een andere virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="523d0-300">LVM of RAID kan worden gebruikt op gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="523d0-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="523d0-301">Configureer een partitie van de wisseling niet op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="523d0-302">U kunt de Linux-agent voor het maken van een wisselbestand op de tijdelijke schijf configureren.</span><span class="sxs-lookup"><span data-stu-id="523d0-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="523d0-303">U vindt meer informatie over deze in de stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="523d0-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="523d0-304">Wanneer u de virtuele harde schijf maakt, selecteert u **Store virtuele schijf als een enkel bestand**.</span><span class="sxs-lookup"><span data-stu-id="523d0-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="523d0-305">Een RHEL 6 virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="523d0-306">In de RHEL 6, NetworkManager kan leiden tot problemen met de Azure Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="523d0-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="523d0-307">Dit pakket verwijderen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="523d0-308">Maak een bestand met de naam **netwerk** in de map/etc/sysconfig/met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="523d0-309">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="523d0-310">Verplaats de udev-regels om te voorkomen dat statische regels voor de Ethernet-interface te genereren (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="523d0-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="523d0-311">Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="523d0-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="523d0-312">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="523d0-313">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="523d0-314">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-315">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="523d0-316">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-317">Open hiervoor `/etc/default/grub` in een teksteditor en bewerk de `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="523d0-318">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="523d0-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="523d0-319">Dit ook zorgt ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="523d0-320">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="523d0-321">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="523d0-322">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-323">Houd er rekening mee dat deze parameter wordt gereduceerd de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="523d0-324">Hyper-V-modules toevoegen aan initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="523d0-325">Bewerken `/etc/dracut.conf`, en voeg de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="523d0-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="523d0-326">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="523d0-327">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten, doorgaans de standaardinstelling is.</span><span class="sxs-lookup"><span data-stu-id="523d0-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="523d0-328">Wijzig `/etc/ssh/sshd_config` om op te nemen van de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="523d0-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="523d0-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="523d0-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="523d0-330">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="523d0-331">Maak geen wisselruimte op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="523d0-332">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-333">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-334">Nadat u de Azure Linux Agent hebt geïnstalleerd in de vorige stap, wijzigt u de volgende parameters in `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="523d0-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="523d0-335">Hef de registratie van het abonnement (indien nodig) met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="523d0-336">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="523d0-337">Sluit de virtuele machine en het bestand VMDK converteren naar een .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="523d0-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="523d0-338">De installatiekopie eerst niet converteren naar onbewerkte indeling:</span><span class="sxs-lookup"><span data-stu-id="523d0-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="523d0-339">Zorg ervoor dat de grootte van de onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="523d0-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="523d0-340">Anders wordt de grootte uitgelijnd met 1 MB afronden:</span><span class="sxs-lookup"><span data-stu-id="523d0-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="523d0-341">De onbewerkte schijf converteren naar een vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="523d0-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="523d0-342">Een RHEL 7 virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="523d0-343">Creëer of bewerk de `/etc/sysconfig/network` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="523d0-344">Creëer of bewerk de `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="523d0-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="523d0-345">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="523d0-346">Registreer uw abonnement Red Hat zodat de installatie van pakketten uit de opslagplaats voor RHEL met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="523d0-347">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="523d0-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="523d0-348">Open hiertoe deze wijziging, `/etc/default/grub` in een teksteditor en bewerk de `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="523d0-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="523d0-349">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="523d0-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="523d0-350">Deze configuratie zorgt er ook voor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="523d0-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="523d0-351">Deze ook schakelt u de nieuwe RHEL 7 naamconventies voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="523d0-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="523d0-352">Bovendien is het raadzaam dat u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="523d0-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="523d0-353">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="523d0-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="523d0-354">U kunt laten de `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="523d0-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="523d0-355">Houd er rekening mee dat deze parameter wordt gereduceerd de hoeveelheid beschikbaar geheugen in de virtuele machine door 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="523d0-356">Nadat u klaar bent bewerken `/etc/default/grub`, voer de volgende opdracht voor het opnieuw samenstellen van de configuratie van de grub:</span><span class="sxs-lookup"><span data-stu-id="523d0-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="523d0-357">Hyper-V-modules toevoegen aan initramfs.</span><span class="sxs-lookup"><span data-stu-id="523d0-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="523d0-358">Bewerken `/etc/dracut.conf`, inhoud toevoegen:</span><span class="sxs-lookup"><span data-stu-id="523d0-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="523d0-359">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="523d0-360">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="523d0-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="523d0-361">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="523d0-361">This setting is usually the default.</span></span> <span data-ttu-id="523d0-362">Wijzig `/etc/ssh/sshd_config` om op te nemen van de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="523d0-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="523d0-363">Het pakket WALinuxAgent `WALinuxAgent-<version>`, is naar de opslagplaats voor Red Hat extra's is gepusht.</span><span class="sxs-lookup"><span data-stu-id="523d0-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="523d0-364">De opslagplaats voor extra's inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="523d0-365">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="523d0-366">Maak geen wisselruimte op de schijf van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="523d0-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="523d0-367">De Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van de schijf van de lokale resource die is gekoppeld aan de virtuele machine nadat de virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="523d0-368">Houd er rekening mee dat de schijf van de lokale resource een tijdelijke schijf is en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="523d0-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="523d0-369">Nadat u de Azure Linux Agent hebt geïnstalleerd in de vorige stap, wijzigt u de volgende parameters in `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="523d0-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="523d0-370">Als u wilt de registratie van het abonnement, voert u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="523d0-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="523d0-371">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="523d0-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="523d0-372">Sluit de virtuele machine en het VMDK-bestand naar de VHD-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="523d0-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="523d0-373">De installatiekopie eerst niet converteren naar onbewerkte indeling:</span><span class="sxs-lookup"><span data-stu-id="523d0-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="523d0-374">Zorg ervoor dat de grootte van de onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="523d0-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="523d0-375">Anders wordt de grootte uitgelijnd met 1 MB afronden:</span><span class="sxs-lookup"><span data-stu-id="523d0-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="523d0-376">De onbewerkte schijf converteren naar een vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="523d0-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="523d0-377">Een Red Hat-virtuele machine van een ISO met behulp van een bestand kickstart automatisch voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="523d0-378">Een RHEL 7 virtuele machine uit een bestand kickstart voorbereiden</span><span class="sxs-lookup"><span data-stu-id="523d0-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="523d0-379">Maak een kickstart-bestand met de volgende inhoud en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="523d0-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="523d0-380">Zie voor meer informatie over installatie kickstart de [Kickstart installatiehandleiding](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="523d0-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear the MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down the machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="523d0-381">Plaats het kickstart bestand waartoe het installatie-systeem toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="523d0-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="523d0-382">Maak een nieuwe virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="523d0-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="523d0-383">Op de **virtuele hardeschijf aansluiten** pagina **later een virtuele harde schijf koppelen**, en voltooi de Wizard Nieuwe virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="523d0-384">Open de instellingen van de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="523d0-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="523d0-385">a.</span><span class="sxs-lookup"><span data-stu-id="523d0-385">a.</span></span>  <span data-ttu-id="523d0-386">Een nieuwe virtuele harde schijf koppelen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="523d0-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="523d0-387">Zorg ervoor dat u selecteert **VHD-indeling** en **vaste grootte**.</span><span class="sxs-lookup"><span data-stu-id="523d0-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="523d0-388">b.</span><span class="sxs-lookup"><span data-stu-id="523d0-388">b.</span></span>  <span data-ttu-id="523d0-389">De installatie van de ISO koppelen aan het DVD-station.</span><span class="sxs-lookup"><span data-stu-id="523d0-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="523d0-390">c.</span><span class="sxs-lookup"><span data-stu-id="523d0-390">c.</span></span>  <span data-ttu-id="523d0-391">Stel het BIOS om op te starten vanaf de CD.</span><span class="sxs-lookup"><span data-stu-id="523d0-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="523d0-392">Hiermee wordt de virtuele machine gestart.</span><span class="sxs-lookup"><span data-stu-id="523d0-392">Start the virtual machine.</span></span> <span data-ttu-id="523d0-393">Wanneer de installatiehandleiding wordt weergegeven, drukt u op **tabblad** de opstartopties te configureren.</span><span class="sxs-lookup"><span data-stu-id="523d0-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="523d0-394">Voer `inst.ks=<the location of the kickstart file>` aan het einde van de opstartopties en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="523d0-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="523d0-395">Wacht totdat de installatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="523d0-395">Wait for the installation to finish.</span></span> <span data-ttu-id="523d0-396">Wanneer deze voltooid, wordt de virtuele machine automatisch afgesloten.</span><span class="sxs-lookup"><span data-stu-id="523d0-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="523d0-397">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="523d0-398">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="523d0-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="523d0-399">Het Hyper-V-stuurprogramma kan niet worden opgenomen in de eerste RAM-schijf wanneer u een niet-Hyper-V-hypervisor</span><span class="sxs-lookup"><span data-stu-id="523d0-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="523d0-400">In sommige gevallen Linux installatieprogramma's mogelijk niet opnemen de stuurprogramma's voor Hyper-V in de eerste RAM-schijf (initrd of initramfs) tenzij Linux vaststelt dat deze wordt uitgevoerd in een Hyper-V-omgeving.</span><span class="sxs-lookup"><span data-stu-id="523d0-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="523d0-401">Wanneer u een andere virtualisatie-systeem (dat wil zeggen, Virtualbox, Xen, enz.) voor het voorbereiden van uw Linux-installatiekopie, moet u mogelijk opnieuw samenstellen initrd om ervoor te zorgen dat ten minste de hv_vmbus en hv_storvsc kernel-modules zijn beschikbaar op de eerste RAM-schijf.</span><span class="sxs-lookup"><span data-stu-id="523d0-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="523d0-402">Dit is een bekend probleem ten minste op systemen die zijn gebaseerd op de upstream Red Hat distributie.</span><span class="sxs-lookup"><span data-stu-id="523d0-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="523d0-403">U lost dit probleem, Hyper-V-modules toevoegen aan initramfs en opnieuw maken:</span><span class="sxs-lookup"><span data-stu-id="523d0-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="523d0-404">Bewerken `/etc/dracut.conf`, en voeg de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="523d0-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="523d0-405">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="523d0-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="523d0-406">Zie voor meer informatie, de informatie over [opnieuw opbouwen van initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="523d0-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="523d0-407">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="523d0-407">Next steps</span></span>
<span data-ttu-id="523d0-408">U bent nu klaar voor gebruik van de Red Hat Enterprise Linux virtuele harde schijf maken van nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="523d0-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="523d0-409">Als dit de eerste keer dat u de VHD-bestand naar Azure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf met het Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="523d0-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="523d0-410">Zie voor meer informatie over de hypervisors die zijn gecertificeerd voor het uitvoeren van Red Hat Enterprise Linux [de website van Red Hat](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="523d0-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
