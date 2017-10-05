---
title: Uitvoeren van een MariaDB (MySQL)-cluster in Azure | Microsoft Docs
description: Maken van een MariaDB + Galera MySQL-cluster op virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: 53e9bf18b26338212411ea7c4f260eb308486738
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="923af-103">MariaDB (MySQL)-cluster: zelfstudie voor Azure</span><span class="sxs-lookup"><span data-stu-id="923af-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="923af-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="923af-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="923af-105">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="923af-105">This article covers the classic deployment model.</span></span> <span data-ttu-id="923af-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Azure Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="923af-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="923af-107">MariaDB Enterprise-cluster is nu beschikbaar in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="923af-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span></span> <span data-ttu-id="923af-108">De nieuwe aanbieding implementeren automatisch een MariaDB Galera-cluster op Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="923af-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="923af-109">Moet u de nieuwe aanbieding van [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="923af-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="923af-110">Dit artikel ziet u het maken van een model met meerdere [Galera](http://galeracluster.com/products/) cluster [MariaDBs](https://mariadb.org/en/about/) (een robuuste, schaalbare en betrouwbare onverwachte ter vervanging van MySQL) werkt in een maximaal beschikbare omgeving op Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="923af-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="923af-111">Overzicht van de architectuur</span><span class="sxs-lookup"><span data-stu-id="923af-111">Architecture overview</span></span>
<span data-ttu-id="923af-112">Dit artikel wordt beschreven hoe u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="923af-112">This article describes how to complete the following steps:</span></span>

- <span data-ttu-id="923af-113">Maak een cluster met drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="923af-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="923af-114">De gegevensschijven scheiden van de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="923af-114">Separate the data disks from the OS disk.</span></span>
- <span data-ttu-id="923af-115">De gegevensschijven in RAID-0/striped instelling te verhogen IOP's maken.</span><span class="sxs-lookup"><span data-stu-id="923af-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span></span>
- <span data-ttu-id="923af-116">Azure Load Balancer gebruiken voor taakverdeling voor de drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="923af-116">Use Azure Load Balancer to balance the load for the three nodes.</span></span>
- <span data-ttu-id="923af-117">Om te beperken herhalende werk, een VM-installatiekopie waarin MariaDB + Galera maken en deze gebruiken om het andere cluster virtuele machines te maken.</span><span class="sxs-lookup"><span data-stu-id="923af-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span></span>

![Systeemarchitectuur](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="923af-119">In dit onderwerp worden de [Azure CLI](../../../cli-install-nodejs.md) hulpprogramma's, dus zorg ervoor dat u deze downloaden en verbind ze met uw Azure-abonnement volgens de instructies.</span><span class="sxs-lookup"><span data-stu-id="923af-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span></span> <span data-ttu-id="923af-120">Als u een verwijzing naar de opdrachten die beschikbaar zijn in de Azure CLI moet, Zie de [Azure CLI-opdrachten](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="923af-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="923af-121">U moet ook [maken van een SSH-sleutel voor verificatie] en noteer de locatie van het .pem-bestand.</span><span class="sxs-lookup"><span data-stu-id="923af-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span></span>
>
>

## <a name="create-the-template"></a><span data-ttu-id="923af-122">De sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="923af-122">Create the template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="923af-123">Infrastructuur</span><span class="sxs-lookup"><span data-stu-id="923af-123">Infrastructure</span></span>
1. <span data-ttu-id="923af-124">Maak een affiniteitsgroep voor het opslaan van de resources samen.</span><span class="sxs-lookup"><span data-stu-id="923af-124">Create an affinity group to hold the resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="923af-125">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="923af-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="923af-126">Een opslagaccount voor het hosten van alle onze schijven maken.</span><span class="sxs-lookup"><span data-stu-id="923af-126">Create a storage account to host all our disks.</span></span> <span data-ttu-id="923af-127">U mag niet meer dan 40 intensief gebruikte schijven op hetzelfde opslagaccount om te voorkomen dat de 20.000 IOPS account opslaglimiet roept plaatsen.</span><span class="sxs-lookup"><span data-stu-id="923af-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="923af-128">In dit geval je ruim onder deze limiet, zodat u alles wat u wilt opslaan op dezelfde account voor de eenvoud.</span><span class="sxs-lookup"><span data-stu-id="923af-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="923af-129">De naam van de installatiekopie van de virtuele machine CentOS 7 vinden.</span><span class="sxs-lookup"><span data-stu-id="923af-129">Find the name of the CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="923af-130">De uitvoer is ongeveer `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="923af-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="923af-131">Gebruikt u de naam in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="923af-131">Use that name in the following step.</span></span>
5. <span data-ttu-id="923af-132">De VM-sjabloon maken en /path/to/key.pem vervangen door het pad waar u de gegenereerde .pem SSH-sleutel hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="923af-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="923af-133">Vier 500 GB gegevensschijven koppelen aan de virtuele machine voor gebruik in de RAID-configuratie.</span><span class="sxs-lookup"><span data-stu-id="923af-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="923af-134">SSH aan te melden bij de virtuele machine die u hebt gemaakt op mariadbhatemplate.cloudapp.net:22-sjabloon gebruiken en verbinding maken met behulp van uw persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="923af-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="923af-135">Software</span><span class="sxs-lookup"><span data-stu-id="923af-135">Software</span></span>
1. <span data-ttu-id="923af-136">Haal de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="923af-136">Get the root.</span></span>

        sudo su

2. <span data-ttu-id="923af-137">Ondersteuning voor RAID installeren:</span><span class="sxs-lookup"><span data-stu-id="923af-137">Install RAID support:</span></span>

    <span data-ttu-id="923af-138">a.</span><span class="sxs-lookup"><span data-stu-id="923af-138">a.</span></span> <span data-ttu-id="923af-139">Mdadm installeren.</span><span class="sxs-lookup"><span data-stu-id="923af-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="923af-140">b.</span><span class="sxs-lookup"><span data-stu-id="923af-140">b.</span></span> <span data-ttu-id="923af-141">Maak de RAID 0/stripe-configuratie met een bestandssysteem EXT4.</span><span class="sxs-lookup"><span data-stu-id="923af-141">Create the RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="923af-142">c.</span><span class="sxs-lookup"><span data-stu-id="923af-142">c.</span></span> <span data-ttu-id="923af-143">Het punt Koppelmap maken.</span><span class="sxs-lookup"><span data-stu-id="923af-143">Create the mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="923af-144">d.</span><span class="sxs-lookup"><span data-stu-id="923af-144">d.</span></span> <span data-ttu-id="923af-145">De UUID van het zojuist gemaakte RAID-apparaat worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="923af-145">Retrieve the UUID of the newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="923af-146">e.</span><span class="sxs-lookup"><span data-stu-id="923af-146">e.</span></span> <span data-ttu-id="923af-147">/Etc/fstab bewerken.</span><span class="sxs-lookup"><span data-stu-id="923af-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="923af-148">f.</span><span class="sxs-lookup"><span data-stu-id="923af-148">f.</span></span> <span data-ttu-id="923af-149">Toevoegen van het apparaat zodat automatisch koppelen op opnieuw opstarten, de UUID vervangen door de waarde die is verkregen van de vorige **blkid** opdracht.</span><span class="sxs-lookup"><span data-stu-id="923af-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="923af-150">g.</span><span class="sxs-lookup"><span data-stu-id="923af-150">g.</span></span> <span data-ttu-id="923af-151">Koppel de nieuwe partitie.</span><span class="sxs-lookup"><span data-stu-id="923af-151">Mount the new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="923af-152">MariaDB installeren.</span><span class="sxs-lookup"><span data-stu-id="923af-152">Install MariaDB.</span></span>

    <span data-ttu-id="923af-153">a.</span><span class="sxs-lookup"><span data-stu-id="923af-153">a.</span></span> <span data-ttu-id="923af-154">Het bestand MariaDB.repo maken.</span><span class="sxs-lookup"><span data-stu-id="923af-154">Create the MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="923af-155">b.</span><span class="sxs-lookup"><span data-stu-id="923af-155">b.</span></span> <span data-ttu-id="923af-156">Vul het repo-bestand met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="923af-156">Fill the repo file with the following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="923af-157">c.</span><span class="sxs-lookup"><span data-stu-id="923af-157">c.</span></span> <span data-ttu-id="923af-158">Om conflicten te voorkomen, verwijder bestaande postfix en mariadb-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="923af-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="923af-159">d.</span><span class="sxs-lookup"><span data-stu-id="923af-159">d.</span></span> <span data-ttu-id="923af-160">Installeer MariaDB met Galera.</span><span class="sxs-lookup"><span data-stu-id="923af-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="923af-161">De gegevensmap MySQL verplaatsen naar het apparaat RAID-blok.</span><span class="sxs-lookup"><span data-stu-id="923af-161">Move the MySQL data directory to the RAID block device.</span></span>

    <span data-ttu-id="923af-162">a.</span><span class="sxs-lookup"><span data-stu-id="923af-162">a.</span></span> <span data-ttu-id="923af-163">De huidige MySQL-map kopiëren naar de nieuwe locatie en de oude map verwijderen.</span><span class="sxs-lookup"><span data-stu-id="923af-163">Copy the current MySQL directory into its new location and remove the old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="923af-164">b.</span><span class="sxs-lookup"><span data-stu-id="923af-164">b.</span></span> <span data-ttu-id="923af-165">Stel machtigingen voor de nieuwe map dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="923af-165">Set permissions for the new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="923af-166">c.</span><span class="sxs-lookup"><span data-stu-id="923af-166">c.</span></span> <span data-ttu-id="923af-167">Maak een symlink die de oude map naar de nieuwe locatie op de RAID-partitie verwijst.</span><span class="sxs-lookup"><span data-stu-id="923af-167">Create a symlink that points the old directory to the new location on the RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="923af-168">Omdat [SELinux verstoort clusterbewerkingen](http://galeracluster.com/documentation-webpages/configuration.html#selinux), is het nodig dat u deze uitschakelt voor de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="923af-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span></span> <span data-ttu-id="923af-169">Bewerken `/etc/selinux/config` dat u deze uitschakelt voor latere opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="923af-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` to set `SELINUX=permissive`
6. <span data-ttu-id="923af-170">Valideren van MySQL wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="923af-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="923af-171">a.</span><span class="sxs-lookup"><span data-stu-id="923af-171">a.</span></span> <span data-ttu-id="923af-172">MySQL wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="923af-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="923af-173">b.</span><span class="sxs-lookup"><span data-stu-id="923af-173">b.</span></span> <span data-ttu-id="923af-174">Beveiligen van de MySQL-installatie, het root-wachtwoord instellen, anonieme gebruikers om uit te schakelen externe hoofdmap aanmelding verwijderen en de testdatabase verwijderen.</span><span class="sxs-lookup"><span data-stu-id="923af-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="923af-175">c.</span><span class="sxs-lookup"><span data-stu-id="923af-175">c.</span></span> <span data-ttu-id="923af-176">Maak een gebruiker op de database voor bewerkingen voor een cluster, en desgewenst voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="923af-176">Create a user on the database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* TO 'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="923af-177">d.</span><span class="sxs-lookup"><span data-stu-id="923af-177">d.</span></span> <span data-ttu-id="923af-178">MySQL stoppen.</span><span class="sxs-lookup"><span data-stu-id="923af-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="923af-179">Maak een configuratie-tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="923af-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="923af-180">a.</span><span class="sxs-lookup"><span data-stu-id="923af-180">a.</span></span> <span data-ttu-id="923af-181">De MySQL-configuratie voor het maken van een tijdelijke aanduiding voor de clusterinstellingen bewerken.</span><span class="sxs-lookup"><span data-stu-id="923af-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span></span> <span data-ttu-id="923af-182">Geen vervanging voor de  **`<Variables>`**  of verwijder de opmerking nu.</span><span class="sxs-lookup"><span data-stu-id="923af-182">Do not replace the **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="923af-183">Dat gebeurt nadat u een virtuele machine met deze sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="923af-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="923af-184">b.</span><span class="sxs-lookup"><span data-stu-id="923af-184">b.</span></span> <span data-ttu-id="923af-185">Bewerk de  **[galera]**  sectie en maak deze.</span><span class="sxs-lookup"><span data-stu-id="923af-185">Edit the **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="923af-186">c.</span><span class="sxs-lookup"><span data-stu-id="923af-186">c.</span></span> <span data-ttu-id="923af-187">Bewerk de **[mariadb]** sectie.</span><span class="sxs-lookup"><span data-stu-id="923af-187">Edit the **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set to 0.0.0.0, the server listens to remote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for the SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set the node name of this server
8. <span data-ttu-id="923af-188">Vereiste poorten op de firewall openen met behulp van FirewallD op CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="923af-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="923af-189">MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="923af-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="923af-190">GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="923af-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="923af-191">GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="923af-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="923af-192">RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="923af-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="923af-193">Laden van de firewall:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="923af-193">Reload the firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="923af-194">Het systeem voor prestaties optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="923af-194">Optimize the system for performance.</span></span> <span data-ttu-id="923af-195">Zie voor meer informatie [prestaties afstemmen strategie](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="923af-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="923af-196">a.</span><span class="sxs-lookup"><span data-stu-id="923af-196">a.</span></span> <span data-ttu-id="923af-197">Het configuratiebestand MySQL opnieuw bewerken.</span><span class="sxs-lookup"><span data-stu-id="923af-197">Edit the MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="923af-198">b.</span><span class="sxs-lookup"><span data-stu-id="923af-198">b.</span></span> <span data-ttu-id="923af-199">Bewerk de **[mariadb]** sectie en het toevoegen van de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="923af-199">Edit the **[mariadb]** section and append the following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="923af-200">We raden aan dat innodb\_buffer\_pool_size 70 procent van het geheugen van de VM is.</span><span class="sxs-lookup"><span data-stu-id="923af-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="923af-201">In dit voorbeeld is deze ingesteld op 2,45 GB voor de virtuele machine van Azure met 3.5 GB aan RAM-geheugen van het medium.</span><span class="sxs-lookup"><span data-stu-id="923af-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # The buffer pool contains buffered data and the index. This is usually set to 70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give the server more time to recycle idled connections
           innodb_file_per_table = 1 # Speed up the table space transmission and optimize the debris management performance
           innodb_log_buffer_size = 128M # The log buffer allows transactions to run without having to flush the log to disk before the transactions commit
           innodb_flush_log_at_trx_commit = 2 # The setting of 2 enables the most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="923af-202">Stop MySQL, MySQL-service worden uitgevoerd op starten om te voorkomen dat het cluster verstoren bij het toevoegen van een knooppunt uitschakelen en inrichting ervan ongedaan maakt de machine.</span><span class="sxs-lookup"><span data-stu-id="923af-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="923af-203">Vastleggen van de virtuele machine via de portal.</span><span class="sxs-lookup"><span data-stu-id="923af-203">Capture the VM through the portal.</span></span> <span data-ttu-id="923af-204">(Momenteel [#1268 in de Azure CLI-hulpprogramma's uitgeven](https://github.com/Azure/azure-xplat-cli/issues/1268) beschrijving van het feit afbeeldingen die zijn vastgelegd door de Azure CLI-hulpprogramma's worden niet vastgelegd voor de schijven bijgesloten gegevens.)</span><span class="sxs-lookup"><span data-stu-id="923af-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span></span>

    <span data-ttu-id="923af-205">a.</span><span class="sxs-lookup"><span data-stu-id="923af-205">a.</span></span> <span data-ttu-id="923af-206">Sluit de machine via de portal.</span><span class="sxs-lookup"><span data-stu-id="923af-206">Shut down the machine through the portal.</span></span>

    <span data-ttu-id="923af-207">b.</span><span class="sxs-lookup"><span data-stu-id="923af-207">b.</span></span> <span data-ttu-id="923af-208">Klik op **vastleggen** en geef de naam van de installatiekopie als **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="923af-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="923af-209">Geef een beschrijving op en controleer 'Ik hebben waagent uitvoeren'.</span><span class="sxs-lookup"><span data-stu-id="923af-209">Provide a description and check "I have run waagent."</span></span>
      
      ![De virtuele machine vastleggen](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-the-cluster"></a><span data-ttu-id="923af-211">Het cluster maken</span><span class="sxs-lookup"><span data-stu-id="923af-211">Create the cluster</span></span>
<span data-ttu-id="923af-212">Maak drie virtuele machines met de sjabloon die u hebt gemaakt, en vervolgens configureren en starten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="923af-212">Create three VMs with the template you created, and then configure and start the cluster.</span></span>

1. <span data-ttu-id="923af-213">De eerste CentOS 7 VM maken van de installatiekopie van het mariadb-galera-installatiekopie die u hebt gemaakt, met de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="923af-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span></span>

 - <span data-ttu-id="923af-214">Virtuele-netwerknaam: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="923af-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="923af-215">Subnet: mariadb</span><span class="sxs-lookup"><span data-stu-id="923af-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="923af-216">Grootte van de computer: gemiddeld</span><span class="sxs-lookup"><span data-stu-id="923af-216">Machine size: medium</span></span>
 - <span data-ttu-id="923af-217">Cloudservicenaam: mariadbha (of de naam die u wilt worden benaderd via mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="923af-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="923af-218">Computernaam: mariadb1</span><span class="sxs-lookup"><span data-stu-id="923af-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="923af-219">Gebruikersnaam: azureuser</span><span class="sxs-lookup"><span data-stu-id="923af-219">Username: azureuser</span></span>
 - <span data-ttu-id="923af-220">SSH-toegang: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="923af-220">SSH access: enabled</span></span>
 - <span data-ttu-id="923af-221">Het .pem-bestand van de SSH-certificaat doorgeeft en /path/to/key.pem vervangen door het pad waar u de gegenereerde .pem SSH-sleutel hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="923af-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="923af-222">De volgende opdrachten worden gesplitst over meerdere regels voor de duidelijkheid, maar u moet elk als één regel invoeren.</span><span class="sxs-lookup"><span data-stu-id="923af-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="923af-223">Twee meer virtuele machines door deze te verbinden met de cloudservice mariadbha maken.</span><span class="sxs-lookup"><span data-stu-id="923af-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span></span> <span data-ttu-id="923af-224">Wijzig de naam van de virtuele machine en de SSH-poort in een unieke poort niet conflicteert met andere virtuele machines in dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="923af-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="923af-225">Voor MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="923af-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="923af-226">U moet de interne IP-adres van elk van de drie virtuele machines ophalen voor de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="923af-226">You will need to get the internal IP address of each of the three VMs for the next step:</span></span>

    ![IP-adres ophalen](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="923af-228">SSH gebruiken om te melden bij de drie virtuele machines en bewerken van het configuratiebestand op elk van deze.</span><span class="sxs-lookup"><span data-stu-id="923af-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="923af-229">Verwijder de opmerking  **`wsrep_cluster_name`**  en  **`wsrep_cluster_address`**  door het verwijderen van de  **#**  aan het begin van de regel.</span><span class="sxs-lookup"><span data-stu-id="923af-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span></span>
    <span data-ttu-id="923af-230">Verder vervangen  **`<ServerIP>`**  in  **`wsrep_node_address`**  en  **`<NodeName>`**  in  **`wsrep_node_name`**  met de VM-IP-adres een naam, respectievelijk, en verwijder deze regels ook de opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="923af-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="923af-231">Start het cluster op MariaDB1 en laat het uitgevoerd bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="923af-231">Start the cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="923af-232">Start MySQL op MariaDB2 en MariaDB3 en laat het uitgevoerd bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="923af-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-the-cluster"></a><span data-ttu-id="923af-233">Taakverdeling het cluster</span><span class="sxs-lookup"><span data-stu-id="923af-233">Load balance the cluster</span></span>
<span data-ttu-id="923af-234">Wanneer u de geclusterde virtuele machines hebt gemaakt, kunt u ze in een beschikbaarheidsset aangeroepen clusteravset om ervoor te zorgen dat ze op verschillende domeinen met fouten en update domeinen zijn geplaatst en nooit onderhoud op alle computers in één keer die Azure biedt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="923af-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="923af-235">Deze configuratie voldoet aan de vereisten worden ondersteund door Azure service level agreement (SLA).</span><span class="sxs-lookup"><span data-stu-id="923af-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span></span>

<span data-ttu-id="923af-236">Nu Azure Load Balancer gebruiken voor een evenwicht tussen aanvragen tussen de drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="923af-236">Now use Azure Load Balancer to balance requests between the three nodes.</span></span>

<span data-ttu-id="923af-237">De volgende opdrachten uitvoeren op uw computer met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="923af-237">Run the following commands on your machine by using the Azure CLI.</span></span>

<span data-ttu-id="923af-238">De parameters-structuur van de opdracht is:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="923af-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="923af-239">De CLI Hiermee stelt u het interval van load balancer-test op 15 seconden en dit is mogelijk iets te lang.</span><span class="sxs-lookup"><span data-stu-id="923af-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="923af-240">Dit wijzigen in de portal onder **eindpunten** voor een van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="923af-240">Change it in the portal under **Endpoints** for any of the VMs.</span></span>

![Eindpunt bewerken](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="923af-242">Selecteer **opnieuw configureren van de Set met gelijke taakverdeling**.</span><span class="sxs-lookup"><span data-stu-id="923af-242">Select **Reconfigure the Load-Balanced Set**.</span></span>

![De Set met gelijke taakverdeling configureren](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="923af-244">Wijziging **Probe Interval** op 5 seconden en sla de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="923af-244">Change **Probe Interval** to 5 seconds and save your changes.</span></span>

![Interval voor wijzigen van test](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-the-cluster"></a><span data-ttu-id="923af-246">Het cluster valideren</span><span class="sxs-lookup"><span data-stu-id="923af-246">Validate the cluster</span></span>
<span data-ttu-id="923af-247">De vaste werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="923af-247">The hard work is done.</span></span> <span data-ttu-id="923af-248">Het cluster toegankelijk moet zijn nu op `mariadbha.cloudapp.net:3306`, die de load balancer en route-aanvragen tussen de drie virtuele machines treffers soepel en efficiënt.</span><span class="sxs-lookup"><span data-stu-id="923af-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="923af-249">Uw favoriete MySQL-client gebruiken om verbinding maken of verbinding maakt vanaf een van de virtuele machines om te controleren of dit cluster werkt.</span><span class="sxs-lookup"><span data-stu-id="923af-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="923af-250">Vervolgens maakt u een database en deze vullen met gegevens.</span><span class="sxs-lookup"><span data-stu-id="923af-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="923af-251">De database die u hebt gemaakt, retourneert de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="923af-251">The database you created returns the following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="923af-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="923af-252">Next steps</span></span>
<span data-ttu-id="923af-253">In dit artikel wordt gemaakt van een drie-knooppunt MariaDB + Galera maximaal beschikbare cluster in Azure virtuele machines actief CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="923af-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="923af-254">De virtuele machines zijn taakverdeling met Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="923af-254">The VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="923af-255">U kunt kijken [MySQL-cluster op Linux op een andere manier](mysql-cluster.md) en manieren om te [optimaliseren en test de prestaties van MySQL op Azure Linux VM's](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="923af-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating the template]:#creating-the-template
[Creating the cluster]:#creating-the-cluster
[Load balancing the cluster]:#load-balancing-the-cluster
[Validating the cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
<span data-ttu-id="923af-256">[Galera]:http://galeracluster.com/products/</span><span class="sxs-lookup"><span data-stu-id="923af-256">[Galera]:http://galeracluster.com/products/</span></span>
[MariaDBs]:https://mariadb.org/en/about/
<span data-ttu-id="923af-257">[maken van een SSH-sleutel voor verificatie]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span><span class="sxs-lookup"><span data-stu-id="923af-257">[create an SSH key for authentication]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span></span>
[issue #1268 in the Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
