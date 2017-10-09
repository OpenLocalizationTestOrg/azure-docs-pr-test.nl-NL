---
title: aaaClusterize MySQL met gelijke taakverdeling sets | Microsoft Docs
description: Instellen van een taakverdeling hoge beschikbaarheid Linux MySQL-cluster met de Hallo klassieke implementatiemodel in Azure gemaakt
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
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="b5128-103">Sets met gelijke taakverdeling tooclusterize MySQL gebruiken op Linux</span><span class="sxs-lookup"><span data-stu-id="b5128-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b5128-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="b5128-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="b5128-105">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5128-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b5128-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5128-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b5128-107">Een [Resource Manager-sjabloon](https://azure.microsoft.com/documentation/templates/mysql-replication/) is beschikbaar als u een MySQL-cluster toodeploy nodig.</span><span class="sxs-lookup"><span data-stu-id="b5128-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="b5128-108">Dit artikel wordt verkend en ziet u Hallo verschillende benaderingen beschikbaar toodeploy maximaal beschikbare op basis van Linux services op Microsoft Azure, hoge beschikbaarheid van de MySQL-Server als een primer verkennen.</span><span class="sxs-lookup"><span data-stu-id="b5128-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="b5128-109">Een video ter illustratie van deze benadering is beschikbaar op [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="b5128-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="b5128-110">Er wordt een overzicht van niets wordt gedeeld, twee knooppunten, één master MySQL oplossing met hoge beschikbaarheid op basis van DRBD Corosync en pacemaker heeft.</span><span class="sxs-lookup"><span data-stu-id="b5128-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="b5128-111">Slechts één knooppunt MySQL op een tijdstip wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="b5128-112">Lezen en schrijven van Hallo DRBD resource is ook beperkte tooonly één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="b5128-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="b5128-113">Er is niet nodig om een VIP-oplossing zoals LVS, omdat u Netwerktaakverdeling sets in Microsoft Azure tooprovide round robin-functionaliteit en eindpunt detectie, verwijderen en gecontroleerde herstelprocedure Hallo VIP.</span><span class="sxs-lookup"><span data-stu-id="b5128-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="b5128-114">Hallo VIP is een algemeen routeerbaar IPv4-adres toegewezen door Microsoft Azure wanneer u eerst de cloudservice Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="b5128-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="b5128-115">Er zijn andere mogelijke architecturen voor MySQL, met inbegrip van de volgende werkdag Cluster, Percona Galera en verschillende middleware oplossingen, waaronder ten minste één beschikbaar als een virtuele machine op [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="b5128-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="b5128-116">Zolang deze oplossingen op unicast-vs. multicast of broadcast repliceren kunnen en Vertrouw niet op de gedeelde opslag of meerdere netwerkinterfaces, moet Hallo scenario's gemakkelijk toodeploy in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b5128-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="b5128-117">Deze clustering architecturen kunnen tooother producten, zoals PostgreSQL en OpenLDAP op soortgelijke wijze worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="b5128-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="b5128-118">Bijvoorbeeld: deze procedure taakverdeling met waarbij niets wordt gedeeld met succes is getest met meerdere master OpenLDAP en kunt u deze bekijken op ons blog Channel 9.</span><span class="sxs-lookup"><span data-stu-id="b5128-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="b5128-119">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="b5128-119">Get ready</span></span>
<span data-ttu-id="b5128-120">U moet de volgende Hallo bronnen en mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="b5128-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="b5128-121">Een Microsoft Azure-account met een geldig abonnement, kunnen toocreate ten minste twee virtuele machines (XS is gebruikt in dit voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="b5128-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="b5128-122">Een netwerk en een subnet</span><span class="sxs-lookup"><span data-stu-id="b5128-122">A network and a subnet</span></span>
  - <span data-ttu-id="b5128-123">Een affiniteitsgroep</span><span class="sxs-lookup"><span data-stu-id="b5128-123">An affinity group</span></span>
  - <span data-ttu-id="b5128-124">Een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="b5128-124">An availability set</span></span>
  - <span data-ttu-id="b5128-125">Hallo mogelijkheid toocreate VHD's in dezelfde regio bevinden als de cloudservice Hallo Hallo en koppel deze toohello virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="b5128-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="b5128-126">Geteste omgeving</span><span class="sxs-lookup"><span data-stu-id="b5128-126">Tested environment</span></span>
* <span data-ttu-id="b5128-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="b5128-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="b5128-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="b5128-128">DRBD</span></span>
  * <span data-ttu-id="b5128-129">MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="b5128-129">MySQL Server</span></span>
  * <span data-ttu-id="b5128-130">Corosync en pacemaker heeft</span><span class="sxs-lookup"><span data-stu-id="b5128-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="b5128-131">Affiniteitsgroep</span><span class="sxs-lookup"><span data-stu-id="b5128-131">Affinity group</span></span>
<span data-ttu-id="b5128-132">Maken van een affiniteitsgroep voor Hallo oplossing met toohello klassieke Azure-portal aanmelden selecteren **instellingen**, en het maken van een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="b5128-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="b5128-133">Toegewezen bronnen maken later worden toothis affiniteitsgroep bevinden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b5128-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="b5128-134">Netwerken</span><span class="sxs-lookup"><span data-stu-id="b5128-134">Networks</span></span>
<span data-ttu-id="b5128-135">Een nieuw netwerk wordt gemaakt en een subnet binnen Hallo-netwerk wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5128-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="b5128-136">Dit voorbeeld wordt een 10.10.10.0/24-netwerk met slechts één /24 subnet binnen.</span><span class="sxs-lookup"><span data-stu-id="b5128-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="b5128-137">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b5128-137">Virtual machines</span></span>
<span data-ttu-id="b5128-138">Hallo eerste Ubuntu 13.10 VM wordt gemaakt met behulp van een afbeelding Endorsed Ubuntu en heet `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="b5128-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="b5128-139">Een nieuwe cloudservice wordt gemaakt bij Hallo hadb aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b5128-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="b5128-140">Deze naam illustreert Hallo gedeeld, taakverdeling aard Hallo service hebben wanneer er meer resources worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b5128-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="b5128-141">het maken van Hallo `hadb01` wordt probleemloze ingevuld met behulp van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="b5128-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="b5128-142">Een eindpunt voor SSH wordt automatisch gemaakt en nieuwe Hallo-netwerk is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="b5128-143">U kunt nu een beschikbaarheidsset voor Hallo virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="b5128-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="b5128-144">Nadat de Hallo eerste VM wordt gemaakt (technisch gezien is bij het Hallo-cloudservice is gemaakt), maakt u Hallo tweede VM `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="b5128-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="b5128-145">Tweede VM voor hello, Ubuntu 13.10 VM van Hallo galerie met behulp van de portal hello gebruiken, maar een bestaande cloudservice `hadb.cloudapp.net`, in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="b5128-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="b5128-146">Hallo-netwerk en beschikbaarheid set moet automatisch worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="b5128-147">Een SSH-eindpunt wordt gemaakt, te.</span><span class="sxs-lookup"><span data-stu-id="b5128-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="b5128-148">Nadat beide virtuele machines zijn gemaakt, noteer Hallo SSH-poort voor `hadb01` (TCP 22) en `hadb02` (automatisch toegewezen door Azure).</span><span class="sxs-lookup"><span data-stu-id="b5128-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="b5128-149">Gekoppelde opslag</span><span class="sxs-lookup"><span data-stu-id="b5128-149">Attached storage</span></span>
<span data-ttu-id="b5128-150">Koppelen van een nieuwe schijf tooboth VM's en 5 GB schijven in Hallo proces maken.</span><span class="sxs-lookup"><span data-stu-id="b5128-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="b5128-151">Hallo-schijven worden in VHD-container in het gebruik van de belangrijkste besturingssysteem schijven Hallo gehost.</span><span class="sxs-lookup"><span data-stu-id="b5128-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="b5128-152">Nadat de schijven zijn gemaakt en gekoppeld, is er geen noodzaak toorestart Linux omdat Hallo kernel Hallo nieuw apparaat ziet.</span><span class="sxs-lookup"><span data-stu-id="b5128-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="b5128-153">Dit apparaat is meestal `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="b5128-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="b5128-154">Controleer `dmesg` voor Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b5128-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="b5128-155">Op elke virtuele machine, kunt u een partitie maken met behulp van `cfdisk` (primaire, Linux-partitie) en nieuwe partitietabel Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="b5128-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="b5128-156">Maak een bestandssysteem geen op deze partitie.</span><span class="sxs-lookup"><span data-stu-id="b5128-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="b5128-157">Hallo-cluster instellen</span><span class="sxs-lookup"><span data-stu-id="b5128-157">Set up hello cluster</span></span>
<span data-ttu-id="b5128-158">Gebruik APT tooinstall Corosync pacemaker heeft en DRBD op beide Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="b5128-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="b5128-159">toodo geval met `apt-get`, voert hello volgende code:</span><span class="sxs-lookup"><span data-stu-id="b5128-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="b5128-160">Installeer geen MySQL op dit moment.</span><span class="sxs-lookup"><span data-stu-id="b5128-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="b5128-161">Debian en Ubuntu installatiescripts een MySQL-gegevensmap op wordt geïnitialiseerd `/var/lib/mysql`, maar omdat Hallo directory wordt vervangen door een bestandssysteem DRBD, moet u later tooinstall MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5128-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="b5128-162">Controleer of (met behulp van `/sbin/ifconfig`) dat beide VM gebruikmaakt van adressen in Hallo 10.10.10.0/24 subnet en dat ze elkaar op naam kunnen pingen.</span><span class="sxs-lookup"><span data-stu-id="b5128-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="b5128-163">U kunt ook `ssh-keygen` en `ssh-copy-id` toomake ervoor dat beide virtuele machines kunnen communiceren via SSH zonder een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b5128-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="b5128-164">DRBD instellen</span><span class="sxs-lookup"><span data-stu-id="b5128-164">Set up DRBD</span></span>
<span data-ttu-id="b5128-165">Maak een DRBD resource die gebruikmaakt van onderliggende hello `/dev/sdc1` tooproduce partitie een `/dev/drbd1` resource die kan worden geformatteerd met ext3 en gebruikt in de primaire en secundaire knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b5128-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="b5128-166">Open `/etc/drbd.d/r0.res` en kopiëren Hallo resourcedefinitie op beide VM:</span><span class="sxs-lookup"><span data-stu-id="b5128-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="b5128-167">Hallo resource initialiseren met `drbdadm` op beide virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="b5128-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="b5128-168">Op Hallo van primaire virtuele machine (`hadb01`), eigendom (primair) van Hallo DRBD resource afdwingen:</span><span class="sxs-lookup"><span data-stu-id="b5128-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="b5128-169">Als u hello-inhoud van proc/drbd bekijkt (`sudo cat /proc/drbd`) op beide virtuele machines, ziet u `Primary/Secondary` op `hadb01` en `Secondary/Primary` op `hadb02`, in overeenstemming met het Hallo-oplossing op dit moment.</span><span class="sxs-lookup"><span data-stu-id="b5128-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="b5128-170">Hallo 5 GB schijfruimte is via Hallo 10.10.10.0/24 netwerk op geen kosten toocustomers gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="b5128-171">Nadat het Hallo-schijf wordt gesynchroniseerd, kunt u Hallo bestandssysteem maken op `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="b5128-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="b5128-172">Voor testdoeleinden, hebben we ext2 gebruikt, maar Hallo volgende code maakt een bestandssysteem ext3:</span><span class="sxs-lookup"><span data-stu-id="b5128-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="b5128-173">Hallo DRBD resource koppelen</span><span class="sxs-lookup"><span data-stu-id="b5128-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="b5128-174">U bent nu klaar toomount hello DRBD bronnen op `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="b5128-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="b5128-175">Debian en afleidingen gebruik `/var/lib/mysql` als de gegevensmap van MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5128-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="b5128-176">Omdat u MySQL nog niet hebt geïnstalleerd, Hallo-map maken en koppelen Hallo DRBD resource.</span><span class="sxs-lookup"><span data-stu-id="b5128-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="b5128-177">tooperform deze optie worden uitgevoerd na de code op Hallo `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="b5128-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="b5128-178">MySQL instellen</span><span class="sxs-lookup"><span data-stu-id="b5128-178">Set up MySQL</span></span>
<span data-ttu-id="b5128-179">U kunt nu klaar tooinstall MySQL op `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="b5128-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="b5128-180">Voor `hadb02`, hebt u twee opties.</span><span class="sxs-lookup"><span data-stu-id="b5128-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="b5128-181">U kunt de mysql-server, die wordt /var/lib/mysql maken, vult u deze met een nieuwe map voor gegevens, en verwijder vervolgens Hallo inhoud installeren.</span><span class="sxs-lookup"><span data-stu-id="b5128-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="b5128-182">tooperform deze optie worden uitgevoerd na de code op Hallo `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="b5128-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="b5128-183">de tweede optie Hallo is toofailover te`hadb02` en installeer vervolgens er mysql-server.</span><span class="sxs-lookup"><span data-stu-id="b5128-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="b5128-184">Installatiescripts ziet Hallo bestaande installatie en het heeft geen invloed.</span><span class="sxs-lookup"><span data-stu-id="b5128-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="b5128-185">Voer hello na de code op `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="b5128-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="b5128-186">Voer hello na de code op `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="b5128-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="b5128-187">Als u niet van plan toofailover DRBD nu bent, is de eerste optie Hallo Hoewel weliswaar minder elegante eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="b5128-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="b5128-188">Nadat u dit instellen, kunt u beginnen aan uw MySQL-database werkt.</span><span class="sxs-lookup"><span data-stu-id="b5128-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="b5128-189">Voer hello na de code op `hadb02` (of elk ander een van de servers Hallo actief is, op basis van tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="b5128-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="b5128-190">Deze laatste instructie effectief dat verificatie is uitgeschakeld voor de hoofdgebruiker Hallo in deze tabel.</span><span class="sxs-lookup"><span data-stu-id="b5128-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="b5128-191">Dit moet worden vervangen door uw productie-hoogwaardige instructies verlenen en is opgenomen alleen ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="b5128-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="b5128-192">Als u wilt toomake query's van VM's voor externe hello (dit is Hallo doel van deze handleiding), moet u ook tooenable netwerken voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5128-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="b5128-193">Open op beide VM `/etc/mysql/my.cnf` en ga te`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="b5128-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="b5128-194">Hallo-adres wijzigen van 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5128-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="b5128-195">Na het Hallo-bestand opslaan, geven een `sudo service mysql restart` op uw huidige primaire.</span><span class="sxs-lookup"><span data-stu-id="b5128-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="b5128-196">Hallo MySQL taakverdeling set maken</span><span class="sxs-lookup"><span data-stu-id="b5128-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="b5128-197">Ga terug toohello portal, gaat u te`hadb01`, en kies **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="b5128-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="b5128-198">toocreate een eindpunt, MySQL (TCP 3306) kiezen uit de vervolgkeuzelijst Hallo en selecteer **set met gelijke taakverdeling maken nieuwe load**.</span><span class="sxs-lookup"><span data-stu-id="b5128-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="b5128-199">Naam Hallo taakverdeling eindpunt `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="b5128-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="b5128-200">Stel **tijd** minimale too5 seconden.</span><span class="sxs-lookup"><span data-stu-id="b5128-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="b5128-201">Nadat u Hallo-eindpunt maken, gaat u te`hadb02`, kies **eindpunten**, en een eindpunt te maken.</span><span class="sxs-lookup"><span data-stu-id="b5128-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="b5128-202">Kies `lb-mysql`, en selecteer vervolgens MySQL in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5128-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="b5128-203">U kunt ook hello Azure CLI gebruiken voor deze stap.</span><span class="sxs-lookup"><span data-stu-id="b5128-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="b5128-204">U hebt nu alles wat die u nodig hebt voor handmatige bewerking van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b5128-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="b5128-205">Hallo taakverdeling set testen</span><span class="sxs-lookup"><span data-stu-id="b5128-205">Test hello load-balanced set</span></span>
<span data-ttu-id="b5128-206">Tests kunnen worden uitgevoerd vanaf een externe computer via een MySQL-client of met behulp van bepaalde toepassingen, zoals phpMyAdmin uitgevoerd als een Azure-website.</span><span class="sxs-lookup"><span data-stu-id="b5128-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="b5128-207">In dit geval gebruikt u het opdrachtregelprogramma van MySQL in een andere Linux:</span><span class="sxs-lookup"><span data-stu-id="b5128-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="b5128-208">Handmatig failover wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="b5128-208">Manually failing over</span></span>
<span data-ttu-id="b5128-209">U kunt failovers simuleren door MySQL afgesloten, overschakelen DRBD van primaire en MySQL opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="b5128-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="b5128-210">tooperform deze taak uitvoeren na de code op hadb01 Hallo:</span><span class="sxs-lookup"><span data-stu-id="b5128-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="b5128-211">Klik op hadb02:</span><span class="sxs-lookup"><span data-stu-id="b5128-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="b5128-212">Nadat u handmatig een failover, kunt u uw externe query herhalen en deze moet perfect werkt.</span><span class="sxs-lookup"><span data-stu-id="b5128-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="b5128-213">Corosync instellen</span><span class="sxs-lookup"><span data-stu-id="b5128-213">Set up Corosync</span></span>
<span data-ttu-id="b5128-214">Corosync is Hallo onderliggende clusterinfrastructuur is vereist voor toowork pacemaker heeft.</span><span class="sxs-lookup"><span data-stu-id="b5128-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="b5128-215">Corosync is een splitsing van Hallo-CRM-functionaliteit voor Heartbeat (en andere methoden zoals Ultramonkey), terwijl pacemaker heeft meer lijken tooHeartbeat in de functionaliteit blijft.</span><span class="sxs-lookup"><span data-stu-id="b5128-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="b5128-216">Hallo belangrijkste beperking voor Corosync in Azure is dat Corosync multicast via broadcast boven unicast-communicatie verkiest, maar Microsoft Azure-netwerken alleen unicast ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="b5128-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="b5128-217">Gelukkig heeft Corosync een werkende unicast-modus.</span><span class="sxs-lookup"><span data-stu-id="b5128-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="b5128-218">Hallo alleen echte beperking is omdat alle knooppunten niet onderling communiceren zijn, u toodefine Hallo knooppunten in uw configuratiebestanden moet, met inbegrip van de IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="b5128-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="b5128-219">We Hallo Corosync voorbeeldbestanden kunnen gebruiken voor Unicast en wijzig adres, knooppunt lijsten en logboekregistratie-mappen binden (Ubuntu gebruikt `/var/log/corosync` terwijl Hallo voorbeeld gebruik bestanden `/var/log/cluster`), en hulpprogramma's voor quorum inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5128-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="b5128-220">Gebruik de volgende Hallo `transport: udpu` richtlijn en Hallo handmatig IP-adressen voor beide knooppunten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="b5128-221">Voer hello na de code op `/etc/corosync/corosync.conf` voor beide knooppunten:</span><span class="sxs-lookup"><span data-stu-id="b5128-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="b5128-222">Kopieer dit configuratiebestand op beide virtuele machines en Corosync in beide knooppunten te starten:</span><span class="sxs-lookup"><span data-stu-id="b5128-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="b5128-223">Hallo-cluster moet worden gemaakt in de huidige ring Hallo kort na het Hallo-service wordt gestart, en quorum moet worden gevormd.</span><span class="sxs-lookup"><span data-stu-id="b5128-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="b5128-224">We kunnen deze functionaliteit controleren aan de hand van Logboeken of door te voeren Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5128-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="b5128-225">Hier ziet u uitvoer vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5128-225">You will see output similar toohello following image:</span></span>

![voorbeelduitvoer van corosync quorumtool - l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="b5128-227">Pacemaker heeft instellen</span><span class="sxs-lookup"><span data-stu-id="b5128-227">Set up Pacemaker</span></span>
<span data-ttu-id="b5128-228">Pacemaker heeft gebruikt Hallo cluster toomonitor voor resources, definiëren wanneer de primaire omlaag gaan en deze resources toosecondaries overschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5128-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="b5128-229">Resources kunnen worden gedefinieerd van een reeks beschikbaar scripts of van LSB (init-achtige)-scripts, onder andere opties.</span><span class="sxs-lookup"><span data-stu-id="b5128-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="b5128-230">We willen pacemaker heeft te 'eigen' hello DRBD resource Hallo koppelpunt en Hallo MySQL-service.</span><span class="sxs-lookup"><span data-stu-id="b5128-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="b5128-231">Als pacemaker heeft en uitschakelen DRBD inschakelen kunt, koppelen en ontkoppelen, en vervolgens starten en stoppen MySQL in Hallo juiste volgorde wanneer er een probleem gebeurt Hello primaire, setup is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b5128-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="b5128-232">Wanneer u pacemaker heeft voor het eerst installeert, worden uw configuratie eenvoudige genoeg is, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5128-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="b5128-233">Controleer de configuratie van Hallo door het uitvoeren van `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="b5128-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="b5128-234">Maak een bestand (zoals `/tmp/cluster.conf`) Hello resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5128-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

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

3. <span data-ttu-id="b5128-235">Hallo-bestand in Hallo configuratie laden.</span><span class="sxs-lookup"><span data-stu-id="b5128-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="b5128-236">U hoeft alleen toodo dit in één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b5128-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="b5128-237">Zorg ervoor dat pacemaker heeft tijdens het opstarten in beide knooppunten begint:</span><span class="sxs-lookup"><span data-stu-id="b5128-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="b5128-238">Met behulp van `sudo crm_mon –L`, controleert u of een van uw knooppunten Hallo master voor Hallo-cluster is geworden en alle Hallo resources wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b5128-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="b5128-239">U kunt koppelen en ps toocheck Hallo resources met gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5128-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="b5128-240">Hallo volgende schermafbeelding ziet `crm_mon` met één knooppunt gestopt (afsluiten door te selecteren Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="b5128-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon knooppunt gestopt](./media/mysql-cluster/image002.png)

<span data-ttu-id="b5128-242">Deze schermafbeelding ziet u knooppunten, één master en een lager niveau bevindende:</span><span class="sxs-lookup"><span data-stu-id="b5128-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operationele master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="b5128-244">Testen</span><span class="sxs-lookup"><span data-stu-id="b5128-244">Testing</span></span>
<span data-ttu-id="b5128-245">U bent klaar voor de simulatie van een automatische failover.</span><span class="sxs-lookup"><span data-stu-id="b5128-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="b5128-246">Er zijn van twee manieren toodo dit: zachte en harde.</span><span class="sxs-lookup"><span data-stu-id="b5128-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="b5128-247">Hallo zachte manier gebruikt van het cluster Hallo afsluiten functie: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="b5128-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="b5128-248">Als u deze op Hallo master gebruiken, neemt Hallo slave op.</span><span class="sxs-lookup"><span data-stu-id="b5128-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="b5128-249">Houd er rekening mee tooset deze back-toooff.</span><span class="sxs-lookup"><span data-stu-id="b5128-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="b5128-250">Als u dit niet doet, ziet crm_mon één knooppunt op stand-by.</span><span class="sxs-lookup"><span data-stu-id="b5128-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="b5128-251">Hallo vaste manier wordt afgesloten omlaag Hallo Hallo primaire virtuele machine (hadb01) via de portal Hallo of door te wijzigen (uitvoeringsniveau) op Hallo VM (dat wil zeggen, stoppen, afsluiten).</span><span class="sxs-lookup"><span data-stu-id="b5128-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="b5128-252">Hierdoor kunnen Corosync en pacemaker heeft door-signalering gaat omlaag dat Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="b5128-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="b5128-253">U kunt dit testen (dit is nuttig voor onderhoudsvensters), maar u kunt ook Hallo scenario afdwingen door bevriezing Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="b5128-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="b5128-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="b5128-254">STONITH</span></span>
<span data-ttu-id="b5128-255">Het moet mogelijk tooissue VM afsluiten via hello Azure CLI in plaats van een script STONITH die een fysiek apparaat bepaalt.</span><span class="sxs-lookup"><span data-stu-id="b5128-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="b5128-256">U kunt `/usr/lib/stonith/plugins/external/ssh` als een basis- en inschakelen STONITH in Hallo clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b5128-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="b5128-257">Azure CLI globaal moet worden geïnstalleerd en Hallo publish settings-profiel moet worden geladen voor de gebruiker Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b5128-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="b5128-258">Voorbeeldcode voor Hallo resource is beschikbaar op [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="b5128-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="b5128-259">Hallo clusterconfiguratie wijzigen door toe te voegen hello te volgen`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="b5128-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="b5128-260">Hallo-script uitvoeren niet omhoog/omlaag controles.</span><span class="sxs-lookup"><span data-stu-id="b5128-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="b5128-261">Hallo oorspronkelijke SSH resource 15 ping cheques had, maar hersteltijd voor een Azure-virtuele machine mogelijk meer variabele.</span><span class="sxs-lookup"><span data-stu-id="b5128-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="b5128-262">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="b5128-262">Limitations</span></span>
<span data-ttu-id="b5128-263">Hallo volgen beperkingen toepassen:</span><span class="sxs-lookup"><span data-stu-id="b5128-263">hello following limitations apply:</span></span>

* <span data-ttu-id="b5128-264">Hallo linbit DRBD resource script waarmee DRBD worden beheerd als een resource in pacemaker heeft gebruikt `drbdadm down` bij het afsluiten van een knooppunt, zelfs als er Hallo knooppunt net op stand-by.</span><span class="sxs-lookup"><span data-stu-id="b5128-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="b5128-265">Dit is niet ideaal omdat Hallo slave zal niet worden synchroniseren Hallo DRBD resource terwijl Hallo master schrijfbewerkingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b5128-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="b5128-266">Als Hallo master niet vriendelijk mislukt, kan Hallo slave de systeemstatus van een oudere bestand overnemen.</span><span class="sxs-lookup"><span data-stu-id="b5128-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="b5128-267">Er zijn twee mogelijke manieren om dit op te lossen:</span><span class="sxs-lookup"><span data-stu-id="b5128-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="b5128-268">Afdwingen van een `drbdadm up r0` op alle clusterknooppunten via een lokale (niet-clusterized) watchdog</span><span class="sxs-lookup"><span data-stu-id="b5128-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="b5128-269">Hallo linbit DRBD script bewerken en ervoor te zorgen dat `down` niet wordt aangeroepen in`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="b5128-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="b5128-270">Hallo load balancer moet ten minste vijf seconden toorespond, zodat toepassingen clusterbewust is en minder gevoelig voor time-out.</span><span class="sxs-lookup"><span data-stu-id="b5128-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="b5128-271">Andere architecturen, zoals in-app-wachtrijen en query middlewares, kunnen ook helpen.</span><span class="sxs-lookup"><span data-stu-id="b5128-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="b5128-272">MySQL afstemmen nodig tooensure die beheerbare tempo geschreven en caches leeggemaakte toodisk zo vaak als mogelijke toominimize geheugen gegevensverlies.</span><span class="sxs-lookup"><span data-stu-id="b5128-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="b5128-273">Prestaties zijn afhankelijk in VM schrijven onderling verbinding maken in de virtuele switch hello, omdat dit Hallo mechanisme dat wordt gebruikt door DRBD tooreplicate Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="b5128-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
