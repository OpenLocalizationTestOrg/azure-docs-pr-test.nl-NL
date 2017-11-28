---
title: Instellen van MySQL op een Linux VM in Azure | Microsoft Docs
description: Informatie over het installeren van de MySQL-stack op een virtuele Linux-machine (Ubuntu of RedHat familie OS) in Azure
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 0ee70bda954cf0a193d43b5b47702e7b2c37844d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-mysql-on-azure"></a><span data-ttu-id="6eef5-103">MySQL installeren op Azure</span><span class="sxs-lookup"><span data-stu-id="6eef5-103">How to install MySQL on Azure</span></span>
<span data-ttu-id="6eef5-104">In dit artikel leert u hoe installeren en configureren van MySQL in Azure een virtuele machine waarop Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6eef5-104">In this article, you will learn how to install and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="6eef5-105">MySQL installeren op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6eef5-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="6eef5-106">U moet al een Microsoft Azure virtuele machine waarop Linux wordt uitgevoerd om te kunnen voltooien van deze zelfstudie hebben.</span><span class="sxs-lookup"><span data-stu-id="6eef5-106">You must already have a Microsoft Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="6eef5-107">Zie de [Azure Linux VM-zelfstudie](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) maken en instellen van een Linux-VM met `mysqlnode` als naam van de VM en `azureuser` als gebruiker voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="6eef5-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create and set up a Linux VM with `mysqlnode` as the VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="6eef5-108">In dit geval 3306 poort gebruiken als de MySQL-poort.</span><span class="sxs-lookup"><span data-stu-id="6eef5-108">In this case, use 3306 port as the MySQL port.</span></span>  

<span data-ttu-id="6eef5-109">Verbinding maken met de Linux VM die u hebt gemaakt via de putty.</span><span class="sxs-lookup"><span data-stu-id="6eef5-109">Connect to the Linux VM you created via putty.</span></span> <span data-ttu-id="6eef5-110">Als dit de eerste keer dat u Azure Linux VM gebruikt, ziet u hoe u met putty verbinding maken met een Linux-VM [hier](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6eef5-110">If this is the first time you use Azure Linux VM, see how to use putty connect to a Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6eef5-111">We gebruiken opslagplaats pakket MySQL5.6 installeren als een voorbeeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6eef5-111">We will use repository package to install MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="6eef5-112">MySQL5.6 heeft eigenlijk meer verbetering in prestaties dan MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="6eef5-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="6eef5-113">Meer informatie [hier](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="6eef5-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-to-install-mysql56-on-ubuntu"></a><span data-ttu-id="6eef5-114">MySQL5.6 op Ubuntu installeren</span><span class="sxs-lookup"><span data-stu-id="6eef5-114">How to install MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="6eef5-115">We gebruiken Linux VM hier met Ubuntu van Azure.</span><span class="sxs-lookup"><span data-stu-id="6eef5-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="6eef5-116">Stap 1: Installeer MySQL Server 5.6 overschakelen naar `root` gebruiker:</span><span class="sxs-lookup"><span data-stu-id="6eef5-116">Step 1: Install MySQL Server 5.6   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="6eef5-117">Mysql-server 5.6 installeren:</span><span class="sxs-lookup"><span data-stu-id="6eef5-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="6eef5-118">Tijdens de installatie ziet u een dialoogvenster venster poping tot vragen u hieronder MySQL root-wachtwoord instellen, en u moet de hier wachtwoord instelt.</span><span class="sxs-lookup"><span data-stu-id="6eef5-118">During installation, you will see a dialog window poping up to ask you to set MySQL root password below, and you need set the password here.</span></span>
  
    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="6eef5-120">Voer het wachtwoord ter bevestiging nogmaals op.</span><span class="sxs-lookup"><span data-stu-id="6eef5-120">Input the password again to confirm.</span></span>

    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="6eef5-122">Stap 2: Aanmelding MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="6eef5-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="6eef5-123">Wanneer de installatie van de MySQL-server is voltooid, wordt MySQL-service automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="6eef5-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="6eef5-124">U kunt zich aanmelden MySQL-Server met `root` gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6eef5-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="6eef5-125">Gebruik de onderstaande opdracht voor het wachtwoord voor aanmelding en invoer.</span><span class="sxs-lookup"><span data-stu-id="6eef5-125">Use the below command to login and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="6eef5-126">Stap 3: De MySQL service beheren</span><span class="sxs-lookup"><span data-stu-id="6eef5-126">Step 3: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="6eef5-127">(a) de status van MySQL-service ophalen</span><span class="sxs-lookup"><span data-stu-id="6eef5-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="6eef5-128">(b) MySQL-Service starten</span><span class="sxs-lookup"><span data-stu-id="6eef5-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="6eef5-129">(c) MySQL-service stoppen</span><span class="sxs-lookup"><span data-stu-id="6eef5-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="6eef5-130">(d) de MySQL-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="6eef5-130">(d) Restart the MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-to-install-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="6eef5-131">Het installeren van MySQL op Red Hat OS-familie zoals CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6eef5-131">How to install MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="6eef5-132">We gebruiken Linux VM hier met de CentOS, Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="6eef5-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="6eef5-133">Stap 1: De opslagplaats MySQL Yum Switch toevoegen aan `root` gebruiker:</span><span class="sxs-lookup"><span data-stu-id="6eef5-133">Step 1: Add the MySQL Yum repository   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="6eef5-134">Download en installeer het releasepakket van MySQL:</span><span class="sxs-lookup"><span data-stu-id="6eef5-134">Download and install the MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="6eef5-135">Stap 2: Bewerken hieronder bestand zodat de MySQL-opslagplaats voor het downloaden van het pakket MySQL5.6.</span><span class="sxs-lookup"><span data-stu-id="6eef5-135">Step 2: Edit below file to enable the MySQL repository for downloading the MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="6eef5-136">Update voor elke waarde van dit bestand hieronder:</span><span class="sxs-lookup"><span data-stu-id="6eef5-136">Update each value of this file to below:</span></span>
  
        \# *Enable to use MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="6eef5-137">Stap 3: Installatie MySQL van MySQL-opslagplaats MySQL installeren:</span><span class="sxs-lookup"><span data-stu-id="6eef5-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="6eef5-138">MySQL-RPM-pakket en alle gerelateerde pakketten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6eef5-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="6eef5-139">Stap 4: De MySQL service beheren</span><span class="sxs-lookup"><span data-stu-id="6eef5-139">Step 4: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="6eef5-140">(a) Controleer de servicestatus van de MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="6eef5-140">(a) Check the service status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="6eef5-141">(b) Controleer of de standaard poort van MySQL-server actief is:</span><span class="sxs-lookup"><span data-stu-id="6eef5-141">(b) Check whether the default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="6eef5-142">(c) de MySQL-server niet starten:</span><span class="sxs-lookup"><span data-stu-id="6eef5-142">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="6eef5-143">(d) stoppen van de MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="6eef5-143">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="6eef5-144">(e) MySQL ingesteld om te starten wanneer het systeem boot-up:</span><span class="sxs-lookup"><span data-stu-id="6eef5-144">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-to-install-mysql-on-suse-linux"></a><span data-ttu-id="6eef5-145">MySQL op SUSE Linux installeren</span><span class="sxs-lookup"><span data-stu-id="6eef5-145">How to install MySQL on SUSE Linux</span></span>
<span data-ttu-id="6eef5-146">We gebruiken Linux VM hier met OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="6eef5-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="6eef5-147">Stap 1: Download en installeer MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="6eef5-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="6eef5-148">Overschakelen naar `root` gebruiker via de onderstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="6eef5-148">Switch to `root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="6eef5-149">Download en installeer MySQL pakket:</span><span class="sxs-lookup"><span data-stu-id="6eef5-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="6eef5-150">Stap 2: De MySQL service beheren</span><span class="sxs-lookup"><span data-stu-id="6eef5-150">Step 2: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="6eef5-151">(a) Controleer de status van de MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="6eef5-151">(a) Check the status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="6eef5-152">(b) Controleer of de standaardpoort van de MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="6eef5-152">(b) Check whether the default port of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="6eef5-153">(c) de MySQL-server niet starten:</span><span class="sxs-lookup"><span data-stu-id="6eef5-153">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="6eef5-154">(d) stoppen van de MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="6eef5-154">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="6eef5-155">(e) MySQL ingesteld om te starten wanneer het systeem boot-up:</span><span class="sxs-lookup"><span data-stu-id="6eef5-155">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="6eef5-156">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="6eef5-156">Next Step</span></span>
<span data-ttu-id="6eef5-157">Meer informatie over het gebruik en informatie met betrekking tot MySQL vinden [hier](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="6eef5-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

