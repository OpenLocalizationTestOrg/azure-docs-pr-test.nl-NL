---
title: aaaCreate en upload een Red Hat Enterprise Linux VHD voor gebruik in Azure | Microsoft Docs
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) waarop een Red Hat Linux-besturingssysteem.
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
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="8d15a-103">Een op Red Hat gebaseerde virtuele machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="8d15a-104">In dit artikel leert u hoe tooprepare een Red Hat Enterprise Linux (RHEL) virtuele machine voor gebruik in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="8d15a-105">Hallo-versies van RHEL die worden besproken in dit artikel zijn 6.7 + en 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="8d15a-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="8d15a-106">Hallo hypervisors voor voorbereiding die worden besproken in dit artikel zijn Hyper-V, op basis van de kernel virtuele machine (KVM) en VMware.</span><span class="sxs-lookup"><span data-stu-id="8d15a-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="8d15a-107">Zie voor meer informatie over de vereisten voor in aanmerking komt voor deelname aan het programma voor toegang tot de Cloud van Red Hat [Red Hat van toegang tot de Cloud website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) en [RHEL uitgevoerd op Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="8d15a-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="8d15a-108">Voorbereiden van een Red Hat-virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="8d15a-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8d15a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d15a-109">Prerequisites</span></span>
<span data-ttu-id="8d15a-110">Deze sectie wordt ervan uitgegaan dat u al een ISO-bestand van Hallo Red Hat website en de geïnstalleerde Hallo RHEL installatiekopie tooa virtuele harde schijf (VHD) hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="8d15a-111">Voor meer informatie over het toouse Hyper-V-beheer tooinstall een besturingssysteemkopie Zie [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d15a-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="8d15a-112">**Opmerkingen bij de installatie van de RHEL**</span><span class="sxs-lookup"><span data-stu-id="8d15a-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="8d15a-113">Azure biedt geen ondersteuning voor Hallo VHDX-indeling.</span><span class="sxs-lookup"><span data-stu-id="8d15a-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="8d15a-114">Azure ondersteunt alleen vaste VHD.</span><span class="sxs-lookup"><span data-stu-id="8d15a-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="8d15a-115">U kunt Hyper-V-beheer tooconvert Hallo-schijfindeling tooVHD gebruiken of kunt u Hallo convert-vhd-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d15a-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="8d15a-116">Als u VirtualBox gebruikt, selecteert u **een vaste grootte** tegenstelling tot toohello standaard dynamisch toegewezen optie wanneer u Hallo schijf maakt.</span><span class="sxs-lookup"><span data-stu-id="8d15a-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="8d15a-117">Azure ondersteunt alleen virtuele machines van generatie 1.</span><span class="sxs-lookup"><span data-stu-id="8d15a-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="8d15a-118">U kunt virtuele machines van generatie 1 converteren uit VHDX toohello VHD-bestand-indeling en dynamisch uitbreidbare tooa vaste grootte schijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="8d15a-119">U kunt een virtuele machine generatie niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="8d15a-120">Zie voor meer informatie [moet ik een virtuele machine van generatie 1 of 2 maken in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="8d15a-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="8d15a-121">Hallo maximale grootte die toegestaan voor Hallo VHD is 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="8d15a-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="8d15a-122">Wanneer u Hallo Linux-besturingssysteem installeert, wordt u aangeraden dat u gebruikt standaard partities in plaats van logische Volume Manager (LVM) vaak Hallo standaardinstelling voor vele installaties.</span><span class="sxs-lookup"><span data-stu-id="8d15a-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="8d15a-123">Hierdoor wordt voorkomen LVM naam conflicteert met de gekloonde virtuele machines, met name als u ooit tooattach een besturingssysteem schijf tooanother identieke virtuele machine nodig hebt voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="8d15a-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="8d15a-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="8d15a-125">Kernel-ondersteuning voor het koppelen van bestandssystemen Universal UDF (Disk Format) is vereist.</span><span class="sxs-lookup"><span data-stu-id="8d15a-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="8d15a-126">Op de eerste keer opstarten op Azure, Hallo UDF-indeling media die is doorgegeven gekoppelde toohello Gast Hallo inrichting configuratie toohello virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="8d15a-127">Hello Azure Linux Agent moet worden kunnen toomount Hallo UDF-bestand system tooread de configuratie en Hallo virtuele machine inrichten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="8d15a-128">Versies van Linux-kernel Hallo die ouder dan 2.6.37 zijn ondersteunen geen niet-uniforme geheugentoegang (NUMA) op Hyper-V met grotere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="8d15a-129">Dit probleem voornamelijk effecten oudere distributies die gebruikmaken van Hallo stroomopwaarts Red Hat 2.6.32 kernel en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="8d15a-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="8d15a-130">Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of RHEL-kernels die ouder dan 2.6.32-504 zijn moeten Hallo ingesteld `numa=off` parameter op Hallo kernel-opdrachtregel in grub.conf opstart.</span><span class="sxs-lookup"><span data-stu-id="8d15a-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="8d15a-131">Zie voor meer informatie, Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="8d15a-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="8d15a-132">Configureer een partitie van de wisseling niet op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="8d15a-133">Hallo Linux-Agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="8d15a-134">Meer informatie hierover vindt u in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="8d15a-135">Alle VHD's moeten hebben-groottes met veelvouden van 1 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="8d15a-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="8d15a-136">Voorbereiden van een RHEL 6 virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="8d15a-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="8d15a-137">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="8d15a-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="8d15a-138">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="8d15a-139">In de RHEL 6, kan NetworkManager hello Azure Linux agent verstoren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="8d15a-140">Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="8d15a-141">Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="8d15a-142">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="8d15a-143">Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="8d15a-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="8d15a-144">Deze regels veroorzaken problemen wanneer u een virtuele machine in Microsoft Azure- of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="8d15a-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="8d15a-145">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="8d15a-146">De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="8d15a-147">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-148">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="8d15a-149">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-150">toodo deze wijziging, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8d15a-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="8d15a-151">Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="8d15a-152">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="8d15a-153">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="8d15a-154">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-155">Houd er rekening mee dat deze parameter Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo door 128 MB of meer vermindert.</span><span class="sxs-lookup"><span data-stu-id="8d15a-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="8d15a-156">Deze configuratie mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="8d15a-157">RHEL 6.5 en eerdere moet ook worden ingesteld Hallo `numa=off` kernel-parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="8d15a-158">Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="8d15a-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="8d15a-159">Zorg ervoor dat die Hallo secure shell (SSH)-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap.</span><span class="sxs-lookup"><span data-stu-id="8d15a-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="8d15a-160">Wijzig /etc/ssh/sshd_config tooinclude Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="8d15a-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="8d15a-161">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="8d15a-162">Installeren Hallo WALinuxAgent pakket verwijderd Hallo NetworkManager en NetworkManager gnome pakketten als ze zijn niet verwijderd in stap 3.</span><span class="sxs-lookup"><span data-stu-id="8d15a-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="8d15a-163">Maak geen wisselruimte op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="8d15a-164">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-165">Houd er rekening mee dat Hallo lokale schijf van de resource is een tijdelijke schijf en dat deze kan worden leeggemaakt wanneer Hallo virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d15a-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-166">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzig Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="8d15a-167">Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="8d15a-168">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="8d15a-169">Klik op **actie** > **afgesloten** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="8d15a-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="8d15a-170">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="8d15a-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="8d15a-171">Voorbereiden van een RHEL 7 virtuele machine vanuit Hyper-V-beheer</span><span class="sxs-lookup"><span data-stu-id="8d15a-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="8d15a-172">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="8d15a-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="8d15a-173">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="8d15a-174">Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="8d15a-175">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="8d15a-176">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="8d15a-177">De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="8d15a-178">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-179">toodo deze wijziging, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="8d15a-180">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8d15a-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="8d15a-181">Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="8d15a-182">Deze configuratie wordt ook uitgeschakeld Hallo nieuwe RHEL 7 naamgevingsregels voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="8d15a-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="8d15a-183">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="8d15a-184">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="8d15a-185">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-186">Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="8d15a-187">Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:</span><span class="sxs-lookup"><span data-stu-id="8d15a-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="8d15a-188">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap.</span><span class="sxs-lookup"><span data-stu-id="8d15a-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="8d15a-189">Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="8d15a-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="8d15a-190">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-191">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="8d15a-192">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="8d15a-193">Maak geen wisselruimte op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="8d15a-194">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-195">Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="8d15a-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-196">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="8d15a-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="8d15a-197">Als u toounregister Hallo abonnement wilt, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d15a-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="8d15a-198">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="8d15a-199">Klik op **actie** > **afgesloten** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="8d15a-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="8d15a-200">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="8d15a-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="8d15a-201">Een Red Hat-virtuele machine uit KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="8d15a-202">Een virtuele machine van RHEL 6 uit KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="8d15a-203">Hallo KVM-installatiekopie RHEL 6 downloaden van Hallo Red Hat website.</span><span class="sxs-lookup"><span data-stu-id="8d15a-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="8d15a-204">Een root-wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-204">Set a root password.</span></span>

    <span data-ttu-id="8d15a-205">Een versleutelde wachtwoord genereren voor en kopieer de uitvoer Hallo Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d15a-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="8d15a-206">Stel het wachtwoord voor een hoofdaccount met guestfish:</span><span class="sxs-lookup"><span data-stu-id="8d15a-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="8d15a-207">Wijziging Hallo tweede veld van de hoofdgebruiker Hallo uit '. '</span><span class="sxs-lookup"><span data-stu-id="8d15a-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="8d15a-208">toohello versleutelde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8d15a-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="8d15a-209">Een virtuele machine in KVM uit Hallo qcow2 installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="8d15a-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="8d15a-210">Hallo schijftype te ingesteld**qcow2**, en stel Hallo virtueel netwerk interface-Apparaatmodel te**virtio**.</span><span class="sxs-lookup"><span data-stu-id="8d15a-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="8d15a-211">Vervolgens Hallo virtuele machine starten en meld u aan als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="8d15a-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="8d15a-212">Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="8d15a-213">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="8d15a-214">Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="8d15a-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="8d15a-215">Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="8d15a-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="8d15a-216">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="8d15a-217">De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="8d15a-218">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-219">toodo deze configuratie, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8d15a-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="8d15a-220">Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="8d15a-221">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="8d15a-222">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="8d15a-223">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-224">Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="8d15a-225">RHEL 6.5 en eerdere moet ook worden ingesteld Hallo `numa=off` kernel-parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="8d15a-226">Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="8d15a-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="8d15a-227">Hyper-V-modules tooinitramfs toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="8d15a-228">Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="8d15a-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="8d15a-229">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="8d15a-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="8d15a-230">Cloud-init verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="8d15a-231">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten:</span><span class="sxs-lookup"><span data-stu-id="8d15a-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="8d15a-232">Wijzig /etc/ssh/sshd_config tooinclude Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="8d15a-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="8d15a-233">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-234">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="8d15a-235">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="8d15a-236">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-237">Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="8d15a-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-238">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende **/etc/waagent.conf** op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="8d15a-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="8d15a-239">Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="8d15a-240">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="8d15a-241">Hallo virtuele machine in KVM afgesloten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="8d15a-242">Hallo qcow2 installatiekopie toohello VHD-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="8d15a-243">Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:</span><span class="sxs-lookup"><span data-stu-id="8d15a-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="8d15a-244">Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8d15a-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="8d15a-245">Anders afronden Hallo grootte tooalign met minimaal 1 MB:</span><span class="sxs-lookup"><span data-stu-id="8d15a-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="8d15a-246">Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="8d15a-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="8d15a-247">Een virtuele machine voor RHEL 7 van KVM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="8d15a-248">Hallo KVM-installatiekopie RHEL 7 downloaden van Hallo Red Hat website.</span><span class="sxs-lookup"><span data-stu-id="8d15a-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="8d15a-249">Deze procedure maakt gebruik van RHEL 7 als voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="8d15a-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="8d15a-250">Een root-wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-250">Set a root password.</span></span>

    <span data-ttu-id="8d15a-251">Een versleutelde wachtwoord genereren voor en kopieer de uitvoer Hallo Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d15a-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="8d15a-252">Stel het wachtwoord voor een hoofdaccount met guestfish:</span><span class="sxs-lookup"><span data-stu-id="8d15a-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="8d15a-253">Wijziging Hallo tweede veld van de hoofdgebruiker van '. '</span><span class="sxs-lookup"><span data-stu-id="8d15a-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="8d15a-254">toohello versleutelde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8d15a-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="8d15a-255">Een virtuele machine in KVM uit Hallo qcow2 installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="8d15a-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="8d15a-256">Hallo schijftype te ingesteld**qcow2**, en stel Hallo virtueel netwerk interface-Apparaatmodel te**virtio**.</span><span class="sxs-lookup"><span data-stu-id="8d15a-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="8d15a-257">Vervolgens Hallo virtuele machine starten en meld u aan als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="8d15a-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="8d15a-258">Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="8d15a-259">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="8d15a-260">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="8d15a-261">Registreer uw Red Hat abonnement tooenable installatie van pakketten uit Hallo RHEL opslagplaats door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="8d15a-262">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-263">toodo deze configuratie, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="8d15a-264">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8d15a-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="8d15a-265">Met deze opdracht zorgt er ook voor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="8d15a-266">Hallo-opdracht worden ook uitgeschakeld Hallo nieuwe RHEL 7 naamconventies NIC's.</span><span class="sxs-lookup"><span data-stu-id="8d15a-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="8d15a-267">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="8d15a-268">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="8d15a-269">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-270">Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="8d15a-271">Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:</span><span class="sxs-lookup"><span data-stu-id="8d15a-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="8d15a-272">Hyper-V-modules toevoegen aan initramfs.</span><span class="sxs-lookup"><span data-stu-id="8d15a-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="8d15a-273">Bewerken `/etc/dracut.conf` en inhoud toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="8d15a-274">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="8d15a-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="8d15a-275">Cloud-init verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="8d15a-276">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten:</span><span class="sxs-lookup"><span data-stu-id="8d15a-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="8d15a-277">Wijzig /etc/ssh/sshd_config tooinclude Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="8d15a-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="8d15a-278">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-279">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="8d15a-280">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="8d15a-281">Hallo waagent-service inschakelen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="8d15a-282">Maak geen wisselruimte op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="8d15a-283">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-284">Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="8d15a-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-285">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="8d15a-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="8d15a-286">Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="8d15a-287">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="8d15a-288">Hallo virtuele machine in KVM afgesloten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="8d15a-289">Hallo qcow2 installatiekopie toohello VHD-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="8d15a-290">Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:</span><span class="sxs-lookup"><span data-stu-id="8d15a-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="8d15a-291">Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8d15a-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="8d15a-292">Anders afronden Hallo grootte tooalign met minimaal 1 MB:</span><span class="sxs-lookup"><span data-stu-id="8d15a-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="8d15a-293">Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="8d15a-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="8d15a-294">Een Red Hat-virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8d15a-295">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d15a-295">Prerequisites</span></span>
<span data-ttu-id="8d15a-296">Deze sectie wordt ervan uitgegaan dat u al een RHEL virtuele machine in VMware hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="8d15a-297">Voor meer informatie over hoe tooinstall een besturingssysteem in VMware, Zie [VMware Guest Operating System installatiehandleiding](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="8d15a-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="8d15a-298">Wanneer u Hallo Linux-besturingssysteem installeert, wordt u aangeraden dat u gebruikt standaard partities in plaats van LVM, vaak Hallo standaardinstelling voor vele installaties.</span><span class="sxs-lookup"><span data-stu-id="8d15a-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="8d15a-299">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machine, met name als de schijf van een besturingssysteem ooit toobe gekoppeld tooanother virtuele machine voor het oplossen van problemen moet.</span><span class="sxs-lookup"><span data-stu-id="8d15a-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="8d15a-300">LVM of RAID kan worden gebruikt op gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="8d15a-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="8d15a-301">Configureer een partitie van de wisseling niet op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="8d15a-302">U kunt Hallo Linux agent toocreate een wisselbestand op Hallo tijdelijke schijf configureren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="8d15a-303">U vindt meer informatie over deze in Hallo stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="8d15a-304">Wanneer u Hallo virtuele hardeschijf maakt, selecteert u **Store virtuele schijf als een enkel bestand**.</span><span class="sxs-lookup"><span data-stu-id="8d15a-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="8d15a-305">Een RHEL 6 virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="8d15a-306">In de RHEL 6, kan NetworkManager hello Azure Linux agent verstoren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="8d15a-307">Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="8d15a-308">Maak een bestand met de naam **netwerk** Hallo in Hallo/etc/sysconfig/directory waarin tekst te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="8d15a-309">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="8d15a-310">Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen).</span><span class="sxs-lookup"><span data-stu-id="8d15a-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="8d15a-311">Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen</span><span class="sxs-lookup"><span data-stu-id="8d15a-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="8d15a-312">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="8d15a-313">De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="8d15a-314">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-315">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="8d15a-316">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-317">toodo deze, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="8d15a-318">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8d15a-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="8d15a-319">Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="8d15a-320">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="8d15a-321">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="8d15a-322">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-323">Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="8d15a-324">Hyper-V-modules tooinitramfs toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="8d15a-325">Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="8d15a-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="8d15a-326">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="8d15a-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="8d15a-327">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap.</span><span class="sxs-lookup"><span data-stu-id="8d15a-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="8d15a-328">Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="8d15a-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="8d15a-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="8d15a-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="8d15a-330">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="8d15a-331">Maak geen wisselruimte op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="8d15a-332">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-333">Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="8d15a-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-334">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="8d15a-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="8d15a-335">Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="8d15a-336">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="8d15a-337">Hallo virtuele machine afsluiten en converteer deze Hallo VMDK-bestand tooa .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="8d15a-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="8d15a-338">Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:</span><span class="sxs-lookup"><span data-stu-id="8d15a-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="8d15a-339">Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8d15a-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="8d15a-340">Anders afronden Hallo grootte tooalign met minimaal 1 MB:</span><span class="sxs-lookup"><span data-stu-id="8d15a-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="8d15a-341">Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="8d15a-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="8d15a-342">Een RHEL 7 virtuele machine van VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="8d15a-343">Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="8d15a-344">Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="8d15a-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="8d15a-345">Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8d15a-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="8d15a-346">De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="8d15a-347">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8d15a-348">toodo deze wijziging, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d15a-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="8d15a-349">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8d15a-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="8d15a-350">Deze configuratie zorgt er ook voor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="8d15a-351">Het ook uitgeschakeld Hallo nieuwe RHEL 7 naamgevingsregels voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="8d15a-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="8d15a-352">Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="8d15a-353">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="8d15a-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="8d15a-354">U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d15a-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="8d15a-355">Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="8d15a-356">Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:</span><span class="sxs-lookup"><span data-stu-id="8d15a-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="8d15a-357">Hyper-V-modules tooinitramfs toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="8d15a-358">Bewerken `/etc/dracut.conf`, inhoud toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8d15a-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="8d15a-359">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="8d15a-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="8d15a-360">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="8d15a-361">Dit is meestal Hallo standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="8d15a-361">This setting is usually hello default.</span></span> <span data-ttu-id="8d15a-362">Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="8d15a-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="8d15a-363">Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht.</span><span class="sxs-lookup"><span data-stu-id="8d15a-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="8d15a-364">Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="8d15a-365">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="8d15a-366">Maak geen wisselruimte op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="8d15a-367">Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="8d15a-368">Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="8d15a-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="8d15a-369">Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="8d15a-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="8d15a-370">Als u toounregister Hallo abonnement wilt, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d15a-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="8d15a-371">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="8d15a-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="8d15a-372">Hallo virtuele machine afsluiten en Hallo VMDK-bestand toohello VHD-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="8d15a-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="8d15a-373">Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:</span><span class="sxs-lookup"><span data-stu-id="8d15a-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="8d15a-374">Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8d15a-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="8d15a-375">Anders afronden Hallo grootte tooalign met minimaal 1 MB:</span><span class="sxs-lookup"><span data-stu-id="8d15a-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="8d15a-376">Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:</span><span class="sxs-lookup"><span data-stu-id="8d15a-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="8d15a-377">Een Red Hat-virtuele machine van een ISO met behulp van een bestand kickstart automatisch voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="8d15a-378">Een RHEL 7 virtuele machine uit een bestand kickstart voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8d15a-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="8d15a-379">Maak een kickstart-bestand dat Hallo na inhoud bevat en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="8d15a-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="8d15a-380">Zie voor meer informatie over installatie kickstart hello [Kickstart installatiehandleiding](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="8d15a-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
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

        # Clear hello MBR
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

        # Power down hello machine after install
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

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
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

2. <span data-ttu-id="8d15a-381">Plaats Hallo kickstart bestand waartoe Hallo installatie systeem toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="8d15a-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="8d15a-382">Maak een nieuwe virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="8d15a-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="8d15a-383">Op Hallo **virtuele hardeschijf aansluiten** pagina **later een virtuele harde schijf koppelen**, en volledige Hallo Wizard Nieuwe virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="8d15a-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="8d15a-384">Open de instellingen van de virtuele machine Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d15a-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="8d15a-385">a.</span><span class="sxs-lookup"><span data-stu-id="8d15a-385">a.</span></span>  <span data-ttu-id="8d15a-386">Een nieuwe virtuele machine van de virtuele harde schijf toohello koppelen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="8d15a-387">Zorg ervoor dat tooselect **VHD-indeling** en **vaste grootte**.</span><span class="sxs-lookup"><span data-stu-id="8d15a-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="8d15a-388">b.</span><span class="sxs-lookup"><span data-stu-id="8d15a-388">b.</span></span>  <span data-ttu-id="8d15a-389">Hallo installatie ISO toohello DVD-station koppelen.</span><span class="sxs-lookup"><span data-stu-id="8d15a-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="8d15a-390">c.</span><span class="sxs-lookup"><span data-stu-id="8d15a-390">c.</span></span>  <span data-ttu-id="8d15a-391">Hallo BIOS tooboot instellen vanaf de CD.</span><span class="sxs-lookup"><span data-stu-id="8d15a-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="8d15a-392">Hallo virtuele machine te starten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-392">Start hello virtual machine.</span></span> <span data-ttu-id="8d15a-393">Wanneer de installatiehandleiding hello wordt weergegeven, drukt u op **tabblad** tooconfigure Hallo opstartopties.</span><span class="sxs-lookup"><span data-stu-id="8d15a-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="8d15a-394">Voer `inst.ks=<hello location of hello kickstart file>` aan einde van Hallo opstartopties en druk op Hallo **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8d15a-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="8d15a-395">Wachten op Hallo installatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="8d15a-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="8d15a-396">Wanneer deze voltooid, wordt Hallo virtuele machine automatisch afgesloten.</span><span class="sxs-lookup"><span data-stu-id="8d15a-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="8d15a-397">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="8d15a-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="8d15a-398">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="8d15a-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="8d15a-399">Hallo Hyper-V-stuurprogramma kan niet worden opgenomen in Hallo initiële RAM-schijf wanneer u een niet-Hyper-V-hypervisor</span><span class="sxs-lookup"><span data-stu-id="8d15a-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="8d15a-400">In sommige gevallen Linux installatieprogramma's mogelijk niet opnemen Hallo stuurprogramma's voor Hyper-V in Hallo initiële RAM-schijf (initrd of initramfs) tenzij Linux vaststelt dat deze wordt uitgevoerd in een Hyper-V-omgeving.</span><span class="sxs-lookup"><span data-stu-id="8d15a-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="8d15a-401">Wanneer u een andere virtualisatie systeem (dat wil zeggen, Virtualbox, Xen, enz.) tooprepare uw Linux-installatiekopie, moet u mogelijk toorebuild initrd tooensure die ten minste Hallo hv_vmbus en hv_storvsc kernel-modules zijn beschikbaar op Hallo initiële RAM-schijf.</span><span class="sxs-lookup"><span data-stu-id="8d15a-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="8d15a-402">Dit is een bekend probleem ten minste op systemen die zijn gebaseerd op Hallo upstream Red Hat distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="8d15a-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="8d15a-403">tooresolve dit probleem, Hyper-V-modules tooinitramfs toevoegen en opnieuw maken:</span><span class="sxs-lookup"><span data-stu-id="8d15a-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="8d15a-404">Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="8d15a-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="8d15a-405">Opnieuw samenstellen initramfs:</span><span class="sxs-lookup"><span data-stu-id="8d15a-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="8d15a-406">Zie voor meer informatie, Hallo informatie over [opnieuw opbouwen van initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="8d15a-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d15a-407">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d15a-407">Next steps</span></span>
<span data-ttu-id="8d15a-408">U bent nu klaar toouse uw Red Hat Enterprise Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d15a-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="8d15a-409">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8d15a-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="8d15a-410">Zie voor meer informatie over Hallo hypervisors die zijn gecertificeerd toorun Red Hat Enterprise Linux, [Hallo Red Hat website](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="8d15a-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
