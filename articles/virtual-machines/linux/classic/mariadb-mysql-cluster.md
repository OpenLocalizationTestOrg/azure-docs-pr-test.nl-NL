---
title: aaaRun een MariaDB (MySQL)-cluster in Azure | Microsoft Docs
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
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="e0d30-103">MariaDB (MySQL)-cluster: zelfstudie voor Azure</span><span class="sxs-lookup"><span data-stu-id="e0d30-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e0d30-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="e0d30-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="e0d30-105">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e0d30-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="e0d30-106">Microsoft raadt aan dat de meeste nieuwe implementaties hello Azure Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="e0d30-107">MariaDB Enterprise-cluster is nu beschikbaar in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0d30-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="e0d30-108">nieuwe aanbieding Hallo implementeren automatisch een MariaDB Galera-cluster op Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0d30-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="e0d30-109">Moet u de nieuwe aanbieding Hallo van [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="e0d30-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="e0d30-110">Dit artikel ziet u hoe een meerdere Master toocreate [Galera](http://galeracluster.com/products/) cluster [MariaDBs](https://mariadb.org/en/about/) (een robuuste, schaalbare en betrouwbare onverwachte ter vervanging van MySQL) toowork in een maximaal beschikbare omgeving op Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e0d30-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="e0d30-111">Overzicht van de architectuur</span><span class="sxs-lookup"><span data-stu-id="e0d30-111">Architecture overview</span></span>
<span data-ttu-id="e0d30-112">Dit artikel wordt beschreven hoe toocomplete Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e0d30-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="e0d30-113">Maak een cluster met drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="e0d30-114">Afzonderlijke Hallo gegevensschijven van Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="e0d30-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="e0d30-115">Hallo gegevensschijven in de instelling RAID-0/striped tooincrease IOP's maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="e0d30-116">Gebruik Azure Load Balancer toobalance Hallo load voor Hallo drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="e0d30-117">herhaalde toominimize werken, een VM-installatiekopie waarin MariaDB + Galera maken en deze gebruiken toocreate Hallo andere cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e0d30-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Systeemarchitectuur](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="e0d30-119">In dit onderwerp maakt gebruik van Hallo [Azure CLI](../../../cli-install-nodejs.md) hulpprogramma's, dus zorg ervoor dat toodownload ze en verbindt u ze tooyour Azure-abonnement volgens toohello instructies.</span><span class="sxs-lookup"><span data-stu-id="e0d30-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="e0d30-120">Als u een verwijzing toohello opdrachten die beschikbaar zijn in hello Azure CLI moet, Zie Hallo [Azure CLI-opdrachten](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e0d30-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="e0d30-121">U moet ook te[maken van een SSH-sleutel voor verificatie] en noteer Hallo .pem bestandslocatie.</span><span class="sxs-lookup"><span data-stu-id="e0d30-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="e0d30-122">Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="e0d30-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="e0d30-123">Infrastructuur</span><span class="sxs-lookup"><span data-stu-id="e0d30-123">Infrastructure</span></span>
1. <span data-ttu-id="e0d30-124">Maken van een affiniteitsgroep toohold Hallo resources samen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="e0d30-125">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="e0d30-126">Alle onze schijven voor een toohost storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="e0d30-127">U mag niet meer dan 40 intensief gebruikte schijven te plaatsen op Hallo dezelfde opslag account tooavoid roept Hallo 20.000 IOPS opslaglimiet-account.</span><span class="sxs-lookup"><span data-stu-id="e0d30-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="e0d30-128">In dit geval je ruim onder deze limiet, zodat u alles wat u wilt opslaan op Hallo dezelfde voor de eenvoud account.</span><span class="sxs-lookup"><span data-stu-id="e0d30-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="e0d30-129">Hallo-naam van de installatiekopie van de virtuele machine Hallo CentOS 7 vinden.</span><span class="sxs-lookup"><span data-stu-id="e0d30-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="e0d30-130">Hallo-uitvoer is ongeveer `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="e0d30-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="e0d30-131">Deze naam in de volgende stap Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="e0d30-132">Hallo VM-sjabloon maken en vervang /path/to/key.pem door Hallo pad op waar u Hallo gegenereerd .pem SSH-sleutel hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="e0d30-133">Koppel vier 500 GB aan gegevens schijven toohello VM voor gebruik in Hallo RAID-configuratie.</span><span class="sxs-lookup"><span data-stu-id="e0d30-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="e0d30-134">SSH toosign gebruiken in toohello sjabloon voor virtuele machine die u hebt gemaakt op mariadbhatemplate.cloudapp.net:22 en verbinding maken met behulp van uw persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="e0d30-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="e0d30-135">Software</span><span class="sxs-lookup"><span data-stu-id="e0d30-135">Software</span></span>
1. <span data-ttu-id="e0d30-136">Hallo-hoofdmap ophalen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="e0d30-137">Ondersteuning voor RAID installeren:</span><span class="sxs-lookup"><span data-stu-id="e0d30-137">Install RAID support:</span></span>

    <span data-ttu-id="e0d30-138">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-138">a.</span></span> <span data-ttu-id="e0d30-139">Mdadm installeren.</span><span class="sxs-lookup"><span data-stu-id="e0d30-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="e0d30-140">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-140">b.</span></span> <span data-ttu-id="e0d30-141">Hallo RAID 0/stripe-configuratie maken met een bestandssysteem EXT4.</span><span class="sxs-lookup"><span data-stu-id="e0d30-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="e0d30-142">c.</span><span class="sxs-lookup"><span data-stu-id="e0d30-142">c.</span></span> <span data-ttu-id="e0d30-143">Hallo punt Koppelmap maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="e0d30-144">d.</span><span class="sxs-lookup"><span data-stu-id="e0d30-144">d.</span></span> <span data-ttu-id="e0d30-145">Hallo UUID van Hallo nieuw gemaakte RAID apparaat worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="e0d30-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="e0d30-146">e.</span><span class="sxs-lookup"><span data-stu-id="e0d30-146">e.</span></span> <span data-ttu-id="e0d30-147">/Etc/fstab bewerken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="e0d30-148">f.</span><span class="sxs-lookup"><span data-stu-id="e0d30-148">f.</span></span> <span data-ttu-id="e0d30-149">Voeg Hallo apparaat tooenable automatisch koppelen op opnieuw opstarten, Hallo UUID vervangen door een Hallo-waarde opgehaald uit de vorige Hallo **blkid** opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0d30-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="e0d30-150">g.</span><span class="sxs-lookup"><span data-stu-id="e0d30-150">g.</span></span> <span data-ttu-id="e0d30-151">Koppel Hallo nieuwe partitie.</span><span class="sxs-lookup"><span data-stu-id="e0d30-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="e0d30-152">MariaDB installeren.</span><span class="sxs-lookup"><span data-stu-id="e0d30-152">Install MariaDB.</span></span>

    <span data-ttu-id="e0d30-153">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-153">a.</span></span> <span data-ttu-id="e0d30-154">Hallo MariaDB.repo bestand maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="e0d30-155">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-155">b.</span></span> <span data-ttu-id="e0d30-156">Vul Hallo-repo-bestand met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="e0d30-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="e0d30-157">c.</span><span class="sxs-lookup"><span data-stu-id="e0d30-157">c.</span></span> <span data-ttu-id="e0d30-158">tooavoid conflicten, verwijder de bestaande postfix en mariadb-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="e0d30-159">d.</span><span class="sxs-lookup"><span data-stu-id="e0d30-159">d.</span></span> <span data-ttu-id="e0d30-160">Installeer MariaDB met Galera.</span><span class="sxs-lookup"><span data-stu-id="e0d30-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="e0d30-161">Hallo MySQL directory toohello RAID blok gegevensapparaat verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="e0d30-162">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-162">a.</span></span> <span data-ttu-id="e0d30-163">Hallo huidige MySQL map kopiëren naar de nieuwe locatie en Hallo oude map verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="e0d30-164">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-164">b.</span></span> <span data-ttu-id="e0d30-165">Stel machtigingen voor de nieuwe map Hallo dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="e0d30-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="e0d30-166">c.</span><span class="sxs-lookup"><span data-stu-id="e0d30-166">c.</span></span> <span data-ttu-id="e0d30-167">Maak een symlink die Hallo oude toohello nieuwe maplocatie op Hallo RAID-partitie verwijst.</span><span class="sxs-lookup"><span data-stu-id="e0d30-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="e0d30-168">Omdat [SELinux verstoort Hallo clusterbewerkingen](http://galeracluster.com/documentation-webpages/configuration.html#selinux), toodisable nodig is voor de huidige sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0d30-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="e0d30-169">Bewerken `/etc/selinux/config` toodisable voor latere opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="e0d30-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="e0d30-170">Valideren van MySQL wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0d30-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="e0d30-171">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-171">a.</span></span> <span data-ttu-id="e0d30-172">MySQL wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e0d30-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="e0d30-173">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-173">b.</span></span> <span data-ttu-id="e0d30-174">Hallo MySQL installatie Secure Hallo root-wachtwoord instellen, verwijder anonieme gebruikers toodisable externe hoofdmap aanmelding en Hallo testdatabase verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="e0d30-175">c.</span><span class="sxs-lookup"><span data-stu-id="e0d30-175">c.</span></span> <span data-ttu-id="e0d30-176">Maak een gebruiker op Hallo database voor bewerkingen voor een cluster, en desgewenst voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="e0d30-177">d.</span><span class="sxs-lookup"><span data-stu-id="e0d30-177">d.</span></span> <span data-ttu-id="e0d30-178">MySQL stoppen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="e0d30-179">Maak een configuratie-tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="e0d30-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="e0d30-180">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-180">a.</span></span> <span data-ttu-id="e0d30-181">Hallo MySQL configuratie toocreate een tijdelijke aanduiding voor Hallo clusterinstellingen bewerken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="e0d30-182">Hallo niet vervangen  **`<Variables>`**  of verwijder de opmerking nu.</span><span class="sxs-lookup"><span data-stu-id="e0d30-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="e0d30-183">Dat gebeurt nadat u een virtuele machine met deze sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="e0d30-184">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-184">b.</span></span> <span data-ttu-id="e0d30-185">Hallo bewerken  **[galera]**  sectie en maak deze.</span><span class="sxs-lookup"><span data-stu-id="e0d30-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="e0d30-186">c.</span><span class="sxs-lookup"><span data-stu-id="e0d30-186">c.</span></span> <span data-ttu-id="e0d30-187">Hallo bewerken **[mariadb]** sectie.</span><span class="sxs-lookup"><span data-stu-id="e0d30-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="e0d30-188">Vereiste poorten op Hallo firewall openen met behulp van FirewallD op CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="e0d30-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="e0d30-189">MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e0d30-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="e0d30-190">GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e0d30-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="e0d30-191">GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e0d30-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="e0d30-192">RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="e0d30-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="e0d30-193">Opnieuw laden Hallo firewall:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="e0d30-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="e0d30-194">Hallo-systeem voor prestaties optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="e0d30-194">Optimize hello system for performance.</span></span> <span data-ttu-id="e0d30-195">Zie voor meer informatie [prestaties afstemmen strategie](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="e0d30-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="e0d30-196">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-196">a.</span></span> <span data-ttu-id="e0d30-197">Hallo MySQL-configuratiebestand opnieuw bewerken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="e0d30-198">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-198">b.</span></span> <span data-ttu-id="e0d30-199">Hallo bewerken **[mariadb]** sectie en toevoeg-Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="e0d30-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="e0d30-200">We raden aan dat innodb\_buffer\_pool_size 70 procent van het geheugen van de VM is.</span><span class="sxs-lookup"><span data-stu-id="e0d30-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="e0d30-201">In dit voorbeeld is deze ingesteld op 2,45 GB voor de Hallo middelgrote virtuele machine van Azure met 3.5 GB aan RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="e0d30-202">MySQL stoppen, MySQL-service worden uitgevoerd op opstarten tooavoid Hallo cluster verstoren bij het toevoegen van een knooppunt uitschakelen en inrichting ervan ongedaan Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="e0d30-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="e0d30-203">Hallo VM via de portal Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="e0d30-204">(Momenteel [#1268 in hello Azure CLI-hulpprogramma's uitgeven](https://github.com/Azure/azure-xplat-cli/issues/1268) beschrijft Hallo feit afbeeldingen die zijn vastgelegd door hello Azure CLI-hulpprogramma's worden niet vastgelegd gegevensschijven Hallo gekoppeld.)</span><span class="sxs-lookup"><span data-stu-id="e0d30-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="e0d30-205">a.</span><span class="sxs-lookup"><span data-stu-id="e0d30-205">a.</span></span> <span data-ttu-id="e0d30-206">Sluit de machine Hallo via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="e0d30-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="e0d30-207">b.</span><span class="sxs-lookup"><span data-stu-id="e0d30-207">b.</span></span> <span data-ttu-id="e0d30-208">Klik op **vastleggen** en geeft u de procesnaam Hallo als **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="e0d30-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="e0d30-209">Geef een beschrijving op en controleer 'Ik hebben waagent uitvoeren'.</span><span class="sxs-lookup"><span data-stu-id="e0d30-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Hallo-machine vastleggen](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="e0d30-211">Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e0d30-211">Create hello cluster</span></span>
<span data-ttu-id="e0d30-212">Maak drie virtuele machines met Hallo sjabloon die u hebt gemaakt, en vervolgens configureren en Hallo cluster starten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="e0d30-213">Maak Hallo eerste CentOS 7 VM van Hallo mariadb galera image installatiekopie hebt gemaakt, bieden Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="e0d30-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="e0d30-214">Virtuele-netwerknaam: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="e0d30-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="e0d30-215">Subnet: mariadb</span><span class="sxs-lookup"><span data-stu-id="e0d30-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="e0d30-216">Grootte van de computer: gemiddeld</span><span class="sxs-lookup"><span data-stu-id="e0d30-216">Machine size: medium</span></span>
 - <span data-ttu-id="e0d30-217">Cloudservicenaam: mariadbha (of welke naam u wilt dat toegankelijk is via mariadbha.cloudapp.net toobe)</span><span class="sxs-lookup"><span data-stu-id="e0d30-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="e0d30-218">Computernaam: mariadb1</span><span class="sxs-lookup"><span data-stu-id="e0d30-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="e0d30-219">Gebruikersnaam: azureuser</span><span class="sxs-lookup"><span data-stu-id="e0d30-219">Username: azureuser</span></span>
 - <span data-ttu-id="e0d30-220">SSH-toegang: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e0d30-220">SSH access: enabled</span></span>
 - <span data-ttu-id="e0d30-221">Hallo SSH-certificaat .pem-bestand doorgeeft en /path/to/key.pem vervangen door een Hallo pad op waar u Hallo opgeslagen gegenereerd .pem SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e0d30-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e0d30-222">Hallo volgende opdrachten verdeeld zijn over meerdere regels voor de duidelijkheid, maar u moet elk als één regel invoeren.</span><span class="sxs-lookup"><span data-stu-id="e0d30-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="e0d30-223">Twee meer virtuele machines door deze te verbinden toohello mariadbha cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="e0d30-224">Hallo dezelfde cloudservice Hallo VM-naam wijzigen en Hallo SSH-poort tooa unieke poort niet conflicteert met andere virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="e0d30-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

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
  <span data-ttu-id="e0d30-225">Voor MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="e0d30-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="e0d30-226">U moet tooget Hallo interne IP-adres van elk van de Hallo drie virtuele machines voor de volgende stap Hallo:</span><span class="sxs-lookup"><span data-stu-id="e0d30-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![IP-adres ophalen](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="e0d30-228">Gebruik van SSH toosign in toohello drie virtuele machines en Hallo-configuratiebestand op elk van deze bewerken.</span><span class="sxs-lookup"><span data-stu-id="e0d30-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="e0d30-229">Verwijder de opmerking  **`wsrep_cluster_name`**  en  **`wsrep_cluster_address`**  door het verwijderen van Hallo  **#**  aan begin van regel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0d30-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="e0d30-230">Verder vervangen  **`<ServerIP>`**  in  **`wsrep_node_address`**  en  **`<NodeName>`**  in  **`wsrep_node_name`**  Hello De VM-IP-adres een naam, respectievelijk, en verwijder deze regels ook de opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="e0d30-231">Hallo cluster starten op MariaDB1 en laat deze uitgevoerd bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="e0d30-232">Start MySQL op MariaDB2 en MariaDB3 en laat het uitgevoerd bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="e0d30-233">Load balance Hallo cluster</span><span class="sxs-lookup"><span data-stu-id="e0d30-233">Load balance hello cluster</span></span>
<span data-ttu-id="e0d30-234">Wanneer u Hallo geclusterde virtuele machines hebt gemaakt, kunt u ze in een beschikbaarheidsset clusteravset tooensure dat ze op verschillende domeinen met fouten en update domeinen zijn geplaatst en dat Azure nooit onderhoud op alle computers in één keer biedt aangeroepen toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e0d30-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="e0d30-235">Deze configuratie voldoet Hallo toobe ondersteund door hello Azure service level agreement (SLA).</span><span class="sxs-lookup"><span data-stu-id="e0d30-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="e0d30-236">Nu gebruikmaken van Azure Load Balancer toobalance aanvragen tussen Hallo drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0d30-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="e0d30-237">Hallo opdrachten op uw computer te volgen met behulp van Azure CLI Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0d30-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="e0d30-238">Hallo parameters opdrachtstructuur is:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="e0d30-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="e0d30-239">Hallo CLI stelt Hallo load balancer-test interval too15 seconden, dat mogelijk iets te lang.</span><span class="sxs-lookup"><span data-stu-id="e0d30-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="e0d30-240">Dit wijzigen in de portal Hallo onder **eindpunten** voor alle virtuele machines Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0d30-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Eindpunt bewerken](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="e0d30-242">Selecteer **Reconfigure Hallo Load-Balanced ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="e0d30-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Configureer opnieuw Hallo load-Set met gelijke taakverdeling](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="e0d30-244">Wijziging **Probe Interval** too5 seconden en sla de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="e0d30-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Interval voor wijzigen van test](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="e0d30-246">Hallo cluster valideren</span><span class="sxs-lookup"><span data-stu-id="e0d30-246">Validate hello cluster</span></span>
<span data-ttu-id="e0d30-247">Hallo harde werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0d30-247">hello hard work is done.</span></span> <span data-ttu-id="e0d30-248">Hallo-cluster moet nu toegankelijk zijn op `mariadbha.cloudapp.net:3306`, die Hallo load balancer treffers en route-aanvragen tussen drie virtuele machines Hallo soepel en efficiënt.</span><span class="sxs-lookup"><span data-stu-id="e0d30-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="e0d30-249">Uw favoriete MySQL client tooconnect gebruiken of verbinding maakt vanaf een Hallo VMs tooverify dat dit cluster werkt.</span><span class="sxs-lookup"><span data-stu-id="e0d30-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="e0d30-250">Vervolgens maakt u een database en deze vullen met gegevens.</span><span class="sxs-lookup"><span data-stu-id="e0d30-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="e0d30-251">Hallo-database die u hebt gemaakt, retourneert Hallo volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="e0d30-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="e0d30-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0d30-252">Next steps</span></span>
<span data-ttu-id="e0d30-253">In dit artikel wordt gemaakt van een drie-knooppunt MariaDB + Galera maximaal beschikbare cluster in Azure virtuele machines actief CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="e0d30-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="e0d30-254">Hallo VM's zijn taakverdeling met Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e0d30-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="e0d30-255">U kunt toolook op [een andere manier toocluster MySQL op Linux](mysql-cluster.md) en manieren te[optimaliseren en test de prestaties van MySQL op Azure Linux VM's](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="e0d30-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[maken van een SSH-sleutel voor verificatie]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
