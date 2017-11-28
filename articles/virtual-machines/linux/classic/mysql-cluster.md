---
title: MySQL clusterize met gelijke taakverdeling sets | Microsoft Docs
description: Instellen van een taakverdeling hoge beschikbaarheid Linux MySQL-cluster met het klassieke implementatiemodel in Azure gemaakt
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="1186c-103">Sets met gelijke taakverdeling kunt clusterize MySQL op Linux</span><span class="sxs-lookup"><span data-stu-id="1186c-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1186c-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="1186c-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="1186c-105">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1186c-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="1186c-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1186c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1186c-107">Een [Resource Manager-sjabloon](https://azure.microsoft.com/documentation/templates/mysql-replication/) is beschikbaar als u moet een MySQL-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="1186c-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="1186c-108">Dit artikel wordt verkend en ziet u de verschillende methoden beschikbaar om maximaal beschikbare op basis van Linux-services op Microsoft Azure kunt verkennen van hoge beschikbaarheid van de MySQL-Server als een primer te implementeren.</span><span class="sxs-lookup"><span data-stu-id="1186c-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="1186c-109">Een video ter illustratie van deze benadering is beschikbaar op [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="1186c-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="1186c-110">Er wordt een overzicht van niets wordt gedeeld, twee knooppunten, één master MySQL oplossing met hoge beschikbaarheid op basis van DRBD Corosync en pacemaker heeft.</span><span class="sxs-lookup"><span data-stu-id="1186c-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="1186c-111">Slechts één knooppunt MySQL op een tijdstip wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1186c-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="1186c-112">Lezen en schrijven van de resource DRBD is ook beperkt tot slechts één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="1186c-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="1186c-113">Er is niet nodig om een VIP-oplossing zoals LVS, omdat u sets met gelijke taakverdeling in Microsoft Azure voor round robin-functionaliteit en eindpunt detectie, verwijderen en correcte herstel van de VIP.</span><span class="sxs-lookup"><span data-stu-id="1186c-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="1186c-114">De VIP is een algemeen routeerbaar IPv4-adres toegewezen door Microsoft Azure wanneer u eerst de cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="1186c-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="1186c-115">Er zijn andere mogelijke architecturen voor MySQL, met inbegrip van de volgende werkdag Cluster, Percona Galera en verschillende middleware oplossingen, waaronder ten minste één beschikbaar als een virtuele machine op [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="1186c-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="1186c-116">Zolang deze oplossingen op unicast-vs. multicast of broadcast repliceren kunnen en Vertrouw niet op de gedeelde opslag of meerdere netwerkinterfaces, zijn de scenario's moet eenvoudig te implementeren in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1186c-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="1186c-117">Deze clustering architecturen kunnen worden uitgebreid naar andere producten, zoals PostgreSQL en OpenLDAP op soortgelijke wijze.</span><span class="sxs-lookup"><span data-stu-id="1186c-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="1186c-118">Bijvoorbeeld: deze procedure taakverdeling met waarbij niets wordt gedeeld met succes is getest met meerdere master OpenLDAP en kunt u deze bekijken op ons blog Channel 9.</span><span class="sxs-lookup"><span data-stu-id="1186c-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="1186c-119">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="1186c-119">Get ready</span></span>
<span data-ttu-id="1186c-120">U moet de volgende resources en de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="1186c-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="1186c-121">Een Microsoft Azure-account met een geldig abonnement ten minste twee virtuele machines maken (XS is gebruikt in dit voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="1186c-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="1186c-122">Een netwerk en een subnet</span><span class="sxs-lookup"><span data-stu-id="1186c-122">A network and a subnet</span></span>
  - <span data-ttu-id="1186c-123">Een affiniteitsgroep</span><span class="sxs-lookup"><span data-stu-id="1186c-123">An affinity group</span></span>
  - <span data-ttu-id="1186c-124">Een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="1186c-124">An availability set</span></span>
  - <span data-ttu-id="1186c-125">De mogelijkheid om te maken van VHD's in dezelfde regio bevinden als de service in de cloud en koppel deze aan de virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="1186c-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="1186c-126">Geteste omgeving</span><span class="sxs-lookup"><span data-stu-id="1186c-126">Tested environment</span></span>
* <span data-ttu-id="1186c-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="1186c-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="1186c-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="1186c-128">DRBD</span></span>
  * <span data-ttu-id="1186c-129">MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="1186c-129">MySQL Server</span></span>
  * <span data-ttu-id="1186c-130">Corosync en pacemaker heeft</span><span class="sxs-lookup"><span data-stu-id="1186c-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="1186c-131">Affiniteitsgroep</span><span class="sxs-lookup"><span data-stu-id="1186c-131">Affinity group</span></span>
<span data-ttu-id="1186c-132">Maken van een affiniteitsgroep voor de oplossing aanmeldt bij de klassieke Azure portal selecteren **instellingen**, en het maken van een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="1186c-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="1186c-133">Toegewezen bronnen maken later wordt toegewezen aan deze groep affiniteit.</span><span class="sxs-lookup"><span data-stu-id="1186c-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="1186c-134">Netwerken</span><span class="sxs-lookup"><span data-stu-id="1186c-134">Networks</span></span>
<span data-ttu-id="1186c-135">Een nieuw netwerk wordt gemaakt en een subnet wordt gemaakt in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="1186c-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="1186c-136">Dit voorbeeld wordt een 10.10.10.0/24-netwerk met slechts één /24 subnet binnen.</span><span class="sxs-lookup"><span data-stu-id="1186c-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="1186c-137">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="1186c-137">Virtual machines</span></span>
<span data-ttu-id="1186c-138">De eerste Ubuntu 13.10 VM wordt gemaakt met behulp van een afbeelding Endorsed Ubuntu en heet `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="1186c-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="1186c-139">Een nieuwe cloudservice wordt gemaakt in het proces, hadb aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1186c-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="1186c-140">Deze naam ziet u de gedeelde, taakverdeling aard die de service hebben wanneer er meer resources worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1186c-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="1186c-141">Het maken van `hadb01` wordt probleemloze ingevuld met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="1186c-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="1186c-142">Een eindpunt voor SSH wordt automatisch gemaakt en het nieuwe netwerk is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1186c-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="1186c-143">U kunt nu de beschikbaarheidsset voor de virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="1186c-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="1186c-144">Nadat de eerste virtuele machine is gemaakt (technisch, wanneer de cloudservice is gemaakt), maakt u de tweede VM `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="1186c-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="1186c-145">Voor de tweede VM Ubuntu 13.10 VM uit de galerie met behulp van de portal, maar met een bestaande cloudservice `hadb.cloudapp.net`, in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="1186c-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="1186c-146">De netwerk- en beschikbaarheid set moet automatisch worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1186c-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="1186c-147">Een SSH-eindpunt wordt gemaakt, te.</span><span class="sxs-lookup"><span data-stu-id="1186c-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="1186c-148">Nadat beide virtuele machines zijn gemaakt, dient u de SSH-poort voor `hadb01` (TCP 22) en `hadb02` (automatisch toegewezen door Azure).</span><span class="sxs-lookup"><span data-stu-id="1186c-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="1186c-149">Gekoppelde opslag</span><span class="sxs-lookup"><span data-stu-id="1186c-149">Attached storage</span></span>
<span data-ttu-id="1186c-150">Een nieuwe schijf koppelen aan beide virtuele machines en 5 GB schijven maken in het proces.</span><span class="sxs-lookup"><span data-stu-id="1186c-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="1186c-151">De schijven worden in de VHD-container in het gebruik van de schijven van de belangrijkste besturingssysteem gehost.</span><span class="sxs-lookup"><span data-stu-id="1186c-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="1186c-152">Nadat de schijven zijn gemaakt en gekoppeld, hoeft niet opnieuw opstarten van Linux omdat de kernel wordt het nieuwe apparaat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1186c-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="1186c-153">Dit apparaat is meestal `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="1186c-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="1186c-154">Controleer `dmesg` voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1186c-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="1186c-155">Op elke virtuele machine, kunt u een partitie maken met behulp van `cfdisk` (primaire, Linux-partitie) en de nieuwe partitietabel schrijven.</span><span class="sxs-lookup"><span data-stu-id="1186c-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="1186c-156">Maak een bestandssysteem geen op deze partitie.</span><span class="sxs-lookup"><span data-stu-id="1186c-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="1186c-157">De cluster instellen</span><span class="sxs-lookup"><span data-stu-id="1186c-157">Set up the cluster</span></span>
<span data-ttu-id="1186c-158">Gebruik APT Corosync pacemaker heeft en DRBD installeren op beide Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="1186c-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="1186c-159">Om dit te doen met `apt-get`, voert u de volgende code:</span><span class="sxs-lookup"><span data-stu-id="1186c-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="1186c-160">Installeer geen MySQL op dit moment.</span><span class="sxs-lookup"><span data-stu-id="1186c-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="1186c-161">Debian en Ubuntu installatiescripts een MySQL-gegevensmap op wordt geïnitialiseerd `/var/lib/mysql`, maar omdat de map wordt vervangen door een bestandssysteem DRBD, moet u MySQL om later te installeren.</span><span class="sxs-lookup"><span data-stu-id="1186c-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="1186c-162">Controleer of (met behulp van `/sbin/ifconfig`) dat beide VM gebruikmaakt van adressen in het subnet 10.10.10.0/24 en dat ze elkaar op naam kunnen pingen.</span><span class="sxs-lookup"><span data-stu-id="1186c-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="1186c-163">U kunt ook `ssh-keygen` en `ssh-copy-id` om ervoor te zorgen dat beide virtuele machines kunnen communiceren via SSH zonder een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1186c-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="1186c-164">DRBD instellen</span><span class="sxs-lookup"><span data-stu-id="1186c-164">Set up DRBD</span></span>
<span data-ttu-id="1186c-165">Maak een DRBD resource die gebruikmaakt van de onderliggende `/dev/sdc1` partitie voor het produceren van een `/dev/drbd1` resource die kan worden geformatteerd met ext3 en gebruikt in de primaire en secundaire knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1186c-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="1186c-166">Open `/etc/drbd.d/r0.res` en kopieer de volgende resourcedefinitie op beide virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="1186c-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="1186c-167">Initialiseren van de resource met behulp van `drbdadm` op beide virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="1186c-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="1186c-168">Op de primaire virtuele machine (`hadb01`), eigendom (primair) van de resource DRBD afdwingen:</span><span class="sxs-lookup"><span data-stu-id="1186c-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="1186c-169">Als u de inhoud van proc/drbd bekijken (`sudo cat /proc/drbd`) op beide virtuele machines, ziet u `Primary/Secondary` op `hadb01` en `Secondary/Primary` op `hadb02`, in overeenstemming met de oplossing op dit moment.</span><span class="sxs-lookup"><span data-stu-id="1186c-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="1186c-170">De schijf 5 GB is gesynchroniseerd via het netwerk 10.10.10.0/24 gratis aan klanten.</span><span class="sxs-lookup"><span data-stu-id="1186c-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="1186c-171">Nadat de schijf wordt gesynchroniseerd, kunt u het bestandssysteem op `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="1186c-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="1186c-172">Voor testdoeleinden, hebben we ext2 gebruikt, maar de volgende code maakt een bestandssysteem ext3:</span><span class="sxs-lookup"><span data-stu-id="1186c-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="1186c-173">De resource DRBD koppelen</span><span class="sxs-lookup"><span data-stu-id="1186c-173">Mount the DRBD resource</span></span>
<span data-ttu-id="1186c-174">U kunt nu de DRBD resources koppelen aan `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="1186c-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="1186c-175">Debian en afleidingen gebruik `/var/lib/mysql` als de gegevensmap van MySQL.</span><span class="sxs-lookup"><span data-stu-id="1186c-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="1186c-176">Omdat u MySQL nog niet hebt geïnstalleerd, de map niet maken en koppelen van de resource DRBD.</span><span class="sxs-lookup"><span data-stu-id="1186c-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="1186c-177">Als u deze optie, voert u de volgende code op `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="1186c-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="1186c-178">MySQL instellen</span><span class="sxs-lookup"><span data-stu-id="1186c-178">Set up MySQL</span></span>
<span data-ttu-id="1186c-179">Nu u klaar bent voor het installeren van MySQL op `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="1186c-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="1186c-180">Voor `hadb02`, hebt u twee opties.</span><span class="sxs-lookup"><span data-stu-id="1186c-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="1186c-181">Mysql-server, die wordt /var/lib/mysql maken, vult u deze met een nieuwe map voor gegevens en verwijder vervolgens de inhoud, kunt u installeren.</span><span class="sxs-lookup"><span data-stu-id="1186c-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="1186c-182">Als u deze optie, voert u de volgende code op `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="1186c-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="1186c-183">De tweede optie is failover `hadb02` en installeer vervolgens er mysql-server.</span><span class="sxs-lookup"><span data-stu-id="1186c-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="1186c-184">Installatiescripts ziet de bestaande installatie en het heeft geen invloed.</span><span class="sxs-lookup"><span data-stu-id="1186c-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="1186c-185">De volgende code uitvoeren op `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="1186c-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="1186c-186">De volgende code uitvoeren op `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="1186c-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="1186c-187">Als u niet wilt failover DRBD nu, is de eerste optie Hoewel weliswaar minder elegante eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="1186c-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="1186c-188">Nadat u dit instellen, kunt u beginnen aan uw MySQL-database werkt.</span><span class="sxs-lookup"><span data-stu-id="1186c-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="1186c-189">De volgende code uitvoeren op `hadb02` (of elk ander een van de servers is actief, volgens DRBD):</span><span class="sxs-lookup"><span data-stu-id="1186c-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="1186c-190">Deze laatste instructie effectief dat verificatie is uitgeschakeld voor de hoofdgebruiker in deze tabel.</span><span class="sxs-lookup"><span data-stu-id="1186c-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="1186c-191">Dit moet worden vervangen door uw productie-hoogwaardige instructies verlenen en is opgenomen alleen ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="1186c-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="1186c-192">Als u wilt maken van query's van buiten de virtuele machines (dit is het doel van deze handleiding), moet u ook netwerken voor MySQL inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1186c-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="1186c-193">Open op beide VM `/etc/mysql/my.cnf` en Ga naar `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="1186c-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="1186c-194">Wijzig het adres van 127.0.0.1 op 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="1186c-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="1186c-195">Na het opslaan van het bestand geven een `sudo service mysql restart` op uw huidige primaire.</span><span class="sxs-lookup"><span data-stu-id="1186c-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="1186c-196">De set MySQL taakverdeling maken</span><span class="sxs-lookup"><span data-stu-id="1186c-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="1186c-197">Ga terug naar de portal, gaat u naar `hadb01`, en kies **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="1186c-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="1186c-198">Voor het maken van een eindpunt (TCP 3306) MySQL kiezen uit de vervolgkeuzelijst en selecteer **set met gelijke taakverdeling maken nieuwe load**.</span><span class="sxs-lookup"><span data-stu-id="1186c-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="1186c-199">Naam van het eindpunt taakverdeling `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="1186c-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="1186c-200">Stel **tijd** op 5 seconden, minimale.</span><span class="sxs-lookup"><span data-stu-id="1186c-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="1186c-201">Nadat u het eindpunt hebt gemaakt, gaat u naar `hadb02`, kies **eindpunten**, en een eindpunt te maken.</span><span class="sxs-lookup"><span data-stu-id="1186c-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="1186c-202">Kies `lb-mysql`, en selecteer vervolgens MySQL in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="1186c-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="1186c-203">U kunt ook de Azure CLI gebruiken voor deze stap.</span><span class="sxs-lookup"><span data-stu-id="1186c-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="1186c-204">U hebt nu alles wat die u nodig hebt voor handmatige bewerking van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1186c-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="1186c-205">Testen van de set met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="1186c-205">Test the load-balanced set</span></span>
<span data-ttu-id="1186c-206">Tests kunnen worden uitgevoerd vanaf een externe computer via een MySQL-client of met behulp van bepaalde toepassingen, zoals phpMyAdmin uitgevoerd als een Azure-website.</span><span class="sxs-lookup"><span data-stu-id="1186c-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="1186c-207">In dit geval gebruikt u het opdrachtregelprogramma van MySQL in een andere Linux:</span><span class="sxs-lookup"><span data-stu-id="1186c-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="1186c-208">Handmatig failover wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="1186c-208">Manually failing over</span></span>
<span data-ttu-id="1186c-209">U kunt failovers simuleren door MySQL afgesloten, overschakelen DRBD van primaire en MySQL opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="1186c-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="1186c-210">Als u wilt uitvoeren van deze taak voert u de volgende code op hadb01:</span><span class="sxs-lookup"><span data-stu-id="1186c-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="1186c-211">Klik op hadb02:</span><span class="sxs-lookup"><span data-stu-id="1186c-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="1186c-212">Nadat u handmatig een failover, kunt u uw externe query herhalen en deze moet perfect werkt.</span><span class="sxs-lookup"><span data-stu-id="1186c-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="1186c-213">Corosync instellen</span><span class="sxs-lookup"><span data-stu-id="1186c-213">Set up Corosync</span></span>
<span data-ttu-id="1186c-214">Corosync is de onderliggende clusterinfrastructuur vereist voor pacemaker heeft om te werken.</span><span class="sxs-lookup"><span data-stu-id="1186c-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="1186c-215">Corosync is een splitsing van de CRM-functionaliteit voor Heartbeat (en andere methoden zoals Ultramonkey), terwijl pacemaker heeft meer lijken op Heartbeat in de functionaliteit blijft.</span><span class="sxs-lookup"><span data-stu-id="1186c-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="1186c-216">De belangrijkste beperking voor Corosync in Azure is dat Corosync multicast via broadcast boven unicast-communicatie verkiest, maar Microsoft Azure-netwerken alleen unicast ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="1186c-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="1186c-217">Gelukkig heeft Corosync een werkende unicast-modus.</span><span class="sxs-lookup"><span data-stu-id="1186c-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="1186c-218">De enige echte beperking is omdat alle knooppunten niet onderling communiceert zijn, u de knooppunten in uw configuratiebestanden moet, met inbegrip van de IP-adressen definiëren.</span><span class="sxs-lookup"><span data-stu-id="1186c-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="1186c-219">We kunnen de Corosync voorbeeld-bestanden gebruiken voor Unicast en wijzig adres, knooppunt lijsten en logboekregistratie-mappen binden (Ubuntu gebruikt `/var/log/corosync` terwijl het voorbeeld gebruik bestanden `/var/log/cluster`), en hulpprogramma's voor quorum inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1186c-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="1186c-220">Gebruik de volgende `transport: udpu` richtlijn en de handmatig gedefinieerde IP-adressen voor beide knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1186c-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="1186c-221">De volgende code uitvoeren op `/etc/corosync/corosync.conf` voor beide knooppunten:</span><span class="sxs-lookup"><span data-stu-id="1186c-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="1186c-222">Kopieer dit configuratiebestand op beide virtuele machines en Corosync in beide knooppunten te starten:</span><span class="sxs-lookup"><span data-stu-id="1186c-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="1186c-223">Het cluster moet worden vastgesteld in de huidige ring kort na het starten van de service en quorum moet worden gevormd.</span><span class="sxs-lookup"><span data-stu-id="1186c-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="1186c-224">We kunnen deze functionaliteit controleren aan de hand van Logboeken of door het uitvoeren van de volgende code:</span><span class="sxs-lookup"><span data-stu-id="1186c-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="1186c-225">Hier ziet u uitvoer die vergelijkbaar is met de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="1186c-225">You will see output similar to the following image:</span></span>

![voorbeelduitvoer van corosync quorumtool - l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="1186c-227">Pacemaker heeft instellen</span><span class="sxs-lookup"><span data-stu-id="1186c-227">Set up Pacemaker</span></span>
<span data-ttu-id="1186c-228">Het cluster pacemaker heeft gebruikt voor het bewaken voor resources, definiëren wanneer de primaire omlaag gaan en deze resources overschakelen naar de secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="1186c-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="1186c-229">Resources kunnen worden gedefinieerd van een reeks beschikbaar scripts of van LSB (init-achtige)-scripts, onder andere opties.</span><span class="sxs-lookup"><span data-stu-id="1186c-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="1186c-230">We willen pacemaker ' eigenaar ' de DRBD-bron, het koppelpunt wordt gehost en de MySQL-service heeft.</span><span class="sxs-lookup"><span data-stu-id="1186c-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="1186c-231">Als pacemaker heeft kunt en deactiveren DRBD activeren koppelen en ontkoppelen, en vervolgens start en stop MySQL in de juiste volgorde wanneer een probleem met de primaire gebeurt, kan setup is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1186c-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="1186c-232">Wanneer u pacemaker heeft voor het eerst installeert, worden uw configuratie eenvoudige genoeg is, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1186c-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="1186c-233">Controleer de configuratie door te voeren `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="1186c-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="1186c-234">Maak een bestand (zoals `/tmp/cluster.conf`) met de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="1186c-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="1186c-235">Het bestand laden in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="1186c-235">Load the file into the configuration.</span></span> <span data-ttu-id="1186c-236">U hoeft alleen te doen in één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1186c-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="1186c-237">Zorg ervoor dat pacemaker heeft tijdens het opstarten in beide knooppunten begint:</span><span class="sxs-lookup"><span data-stu-id="1186c-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="1186c-238">Met behulp van `sudo crm_mon –L`, Controleer of een van de knooppunten van het model voor het cluster is geworden en alle resources wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1186c-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="1186c-239">U kunt koppelen en ps gebruiken om te controleren dat de bronnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1186c-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="1186c-240">De volgende schermafbeelding ziet `crm_mon` met één knooppunt gestopt (afsluiten door te selecteren Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="1186c-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon knooppunt gestopt](./media/mysql-cluster/image002.png)

<span data-ttu-id="1186c-242">Deze schermafbeelding ziet u knooppunten, één master en een lager niveau bevindende:</span><span class="sxs-lookup"><span data-stu-id="1186c-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operationele master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="1186c-244">Testen</span><span class="sxs-lookup"><span data-stu-id="1186c-244">Testing</span></span>
<span data-ttu-id="1186c-245">U bent klaar voor de simulatie van een automatische failover.</span><span class="sxs-lookup"><span data-stu-id="1186c-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="1186c-246">Er zijn twee manieren om dit te doen: zachte en harde.</span><span class="sxs-lookup"><span data-stu-id="1186c-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="1186c-247">De zachte manier maakt gebruik van de clusterfunctie afsluiten: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="1186c-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="1186c-248">Als u deze op de master gebruiken, neemt de slave op.</span><span class="sxs-lookup"><span data-stu-id="1186c-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="1186c-249">Moet u dit opnieuw ingesteld op uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1186c-249">Remember to set this back to off.</span></span> <span data-ttu-id="1186c-250">Als u dit niet doet, ziet crm_mon één knooppunt op stand-by.</span><span class="sxs-lookup"><span data-stu-id="1186c-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="1186c-251">De vaste manier wordt afgesloten met de primaire virtuele machine (hadb01) via de portal of door het wijzigen van de (uitvoeringsniveau) op de virtuele machine (dat wil zeggen, stoppen, afsluiten).</span><span class="sxs-lookup"><span data-stu-id="1186c-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="1186c-252">Hierdoor kunnen Corosync en pacemaker heeft door-signalering die de master de tijdelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1186c-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="1186c-253">U kunt dit testen (dit is nuttig voor onderhoudsvensters), maar u kunt ook het scenario afdwingen door de virtuele machine blokkeren.</span><span class="sxs-lookup"><span data-stu-id="1186c-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="1186c-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="1186c-254">STONITH</span></span>
<span data-ttu-id="1186c-255">Het moet mogelijk een afsluiten van de virtuele machine via de Azure CLI in plaats van een STONITH-script waarmee een fysiek apparaat uitgeven.</span><span class="sxs-lookup"><span data-stu-id="1186c-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="1186c-256">U kunt `/usr/lib/stonith/plugins/external/ssh` als een basis- en STONITH inschakelen in de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1186c-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="1186c-257">Azure CLI globaal moet worden geïnstalleerd en de publicatie-instellingen en het profiel moeten worden geladen voor de gebruiker van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1186c-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="1186c-258">Voorbeeld van code voor de resource is beschikbaar op [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="1186c-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="1186c-259">De cluster-configuratie wijzigen door het volgende toe te voegen `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="1186c-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="1186c-260">Het script uitvoeren niet omhoog/omlaag controles.</span><span class="sxs-lookup"><span data-stu-id="1186c-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="1186c-261">De oorspronkelijke SSH-resource 15 ping cheques had, maar het moment van herstel voor een Azure VM mogelijk meer variabele.</span><span class="sxs-lookup"><span data-stu-id="1186c-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="1186c-262">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1186c-262">Limitations</span></span>
<span data-ttu-id="1186c-263">Er gelden de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="1186c-263">The following limitations apply:</span></span>

* <span data-ttu-id="1186c-264">Het script linbit DRBD resource die wordt beheerd DRBD als een resource in pacemaker heeft gebruikt `drbdadm down` bij het afsluiten van een knooppunt, zelfs als het knooppunt wordt alleen op stand-by.</span><span class="sxs-lookup"><span data-stu-id="1186c-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="1186c-265">Dit is niet ideaal omdat de slave niet de resource DRBD synchroniseert wordt terwijl de master schrijfbewerkingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1186c-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="1186c-266">Als het model niet vriendelijk mislukt, kan de slave de systeemstatus van een oudere bestand overnemen.</span><span class="sxs-lookup"><span data-stu-id="1186c-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="1186c-267">Er zijn twee mogelijke manieren om dit op te lossen:</span><span class="sxs-lookup"><span data-stu-id="1186c-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="1186c-268">Afdwingen van een `drbdadm up r0` op alle clusterknooppunten via een lokale (niet-clusterized) watchdog</span><span class="sxs-lookup"><span data-stu-id="1186c-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="1186c-269">Het bewerken van het linbit DRBD script, om ervoor te zorgen dat `down` niet wordt aangeroepen in`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="1186c-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="1186c-270">De load balancer moet ten minste vijf seconden reageert, zodat toepassingen clusterbewust is en minder gevoelig voor time-out.</span><span class="sxs-lookup"><span data-stu-id="1186c-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="1186c-271">Andere architecturen, zoals in-app-wachtrijen en query middlewares, kunnen ook helpen.</span><span class="sxs-lookup"><span data-stu-id="1186c-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="1186c-272">MySQL-afstemming is nodig om ervoor te zorgen dat beheerbare tempo geschreven en caches worden leeggemaakt naar de schijf zo vaak mogelijk geheugen gegevensverlies te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="1186c-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="1186c-273">Prestaties zijn afhankelijk in VM schrijven onderling verbinding maken in de virtuele switch, omdat dit het mechanisme dat door DRBD is voor replicatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="1186c-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
