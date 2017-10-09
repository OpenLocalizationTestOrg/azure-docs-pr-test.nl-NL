---
title: aaaSet van MySQL op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo MySQL stack is op een virtuele Linux-machine (Ubuntu of RedHat familie OS) in Azure
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
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="58bd8-103">Hoe tooinstall MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="58bd8-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="58bd8-104">In dit artikel leert u hoe tooinstall en MySQL configureren op een virtuele machine van Azure waarop Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58bd8-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="58bd8-105">MySQL installeren op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="58bd8-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="58bd8-106">U moet al een Microsoft Azure virtuele machine waarop Linux wordt uitgevoerd in de volgorde toocomplete in deze zelfstudie hebben.</span><span class="sxs-lookup"><span data-stu-id="58bd8-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="58bd8-107">Zie de [Azure Linux VM-zelfstudie](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate en instellen van een Linux-VM met `mysqlnode` als Hallo VM-naam en `azureuser` als gebruiker voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="58bd8-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="58bd8-108">In dit geval 3306 poort gebruiken als Hallo MySQL-poort.</span><span class="sxs-lookup"><span data-stu-id="58bd8-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="58bd8-109">Verbinding maken met toohello Linux VM u via de putty hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58bd8-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="58bd8-110">Als dit Hallo eerste keer dat u Azure Linux VM gebruikt, Zie hoe toouse putty verbinding tooa Linux VM [hier](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58bd8-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="58bd8-111">We gebruiken opslagplaats pakket tooinstall MySQL5.6 als voorbeeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="58bd8-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="58bd8-112">MySQL5.6 heeft eigenlijk meer verbetering in prestaties dan MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="58bd8-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="58bd8-113">Meer informatie [hier](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="58bd8-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="58bd8-114">Hoe tooinstall MySQL5.6 op Ubuntu</span><span class="sxs-lookup"><span data-stu-id="58bd8-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="58bd8-115">We gebruiken Linux VM hier met Ubuntu van Azure.</span><span class="sxs-lookup"><span data-stu-id="58bd8-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="58bd8-116">Stap 1: Installeer MySQL Server 5.6 te schakelen`root` gebruiker:</span><span class="sxs-lookup"><span data-stu-id="58bd8-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="58bd8-117">Mysql-server 5.6 installeren:</span><span class="sxs-lookup"><span data-stu-id="58bd8-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="58bd8-118">Tijdens de installatie, ziet u een dialoogvenster venster poping up tooask u tooset MySQL hoofdwachtwoord hieronder, en u moet Hallo hier wachtwoord instelt.</span><span class="sxs-lookup"><span data-stu-id="58bd8-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="58bd8-120">Invoer Hallo wachtwoord opnieuw tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="58bd8-120">Input hello password again tooconfirm.</span></span>

    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="58bd8-122">Stap 2: Aanmelding MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="58bd8-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="58bd8-123">Wanneer de installatie van de MySQL-server is voltooid, wordt MySQL-service automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="58bd8-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="58bd8-124">U kunt zich aanmelden MySQL-Server met `root` gebruiker.</span><span class="sxs-lookup"><span data-stu-id="58bd8-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="58bd8-125">Hallo onderstaande opdracht toologin en invoer wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="58bd8-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="58bd8-126">Stap 3: Beheren Hallo MySQL-service wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="58bd8-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="58bd8-127">(a) de status van MySQL-service ophalen</span><span class="sxs-lookup"><span data-stu-id="58bd8-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="58bd8-128">(b) MySQL-Service starten</span><span class="sxs-lookup"><span data-stu-id="58bd8-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="58bd8-129">(c) MySQL-service stoppen</span><span class="sxs-lookup"><span data-stu-id="58bd8-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="58bd8-130">(d) Hallo MySQL-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="58bd8-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="58bd8-131">Hoe tooinstall MySQL op Red Hat OS-familie, zoals CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="58bd8-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="58bd8-132">We gebruiken Linux VM hier met de CentOS, Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="58bd8-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="58bd8-133">Stap 1: Toevoegen Hallo MySQL Yum opslagplaats Switch te`root` gebruiker:</span><span class="sxs-lookup"><span data-stu-id="58bd8-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="58bd8-134">Download en installeer Hallo MySQL releasepakket:</span><span class="sxs-lookup"><span data-stu-id="58bd8-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="58bd8-135">Stap 2: Hieronder bestand tooenable Hallo MySQL opslagplaats voor het downloaden van het Hallo MySQL5.6 pakket bewerken</span><span class="sxs-lookup"><span data-stu-id="58bd8-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="58bd8-136">Elke waarde van dit bestand toobelow bijwerken:</span><span class="sxs-lookup"><span data-stu-id="58bd8-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="58bd8-137">Stap 3: Installatie MySQL van MySQL-opslagplaats MySQL installeren:</span><span class="sxs-lookup"><span data-stu-id="58bd8-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="58bd8-138">MySQL-RPM-pakket en alle gerelateerde pakketten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="58bd8-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="58bd8-139">Stap 4: Beheren Hallo MySQL-service wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="58bd8-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="58bd8-140">(a) Controleer de servicestatus Hallo van Hallo MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="58bd8-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="58bd8-141">(b) Controleer of de poort van MySQL standaardserver Hallo actief is:</span><span class="sxs-lookup"><span data-stu-id="58bd8-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="58bd8-142">(c) Hallo MySQL-server niet starten:</span><span class="sxs-lookup"><span data-stu-id="58bd8-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="58bd8-143">(d) stoppen Hallo MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="58bd8-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="58bd8-144">(e) MySQL toostart instellen als Hallo system boot-up:</span><span class="sxs-lookup"><span data-stu-id="58bd8-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="58bd8-145">Hoe tooinstall MySQL in SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="58bd8-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="58bd8-146">We gebruiken Linux VM hier met OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="58bd8-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="58bd8-147">Stap 1: Download en installeer MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="58bd8-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="58bd8-148">Switch te`root` gebruiker via de onderstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="58bd8-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="58bd8-149">Download en installeer MySQL pakket:</span><span class="sxs-lookup"><span data-stu-id="58bd8-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="58bd8-150">Stap 2: Beheren Hallo MySQL-service wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="58bd8-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="58bd8-151">(a) Hallo status controleren van Hallo MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="58bd8-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="58bd8-152">(b) Controleer of Hallo standaardpoort Hallo MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="58bd8-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="58bd8-153">(c) Hallo MySQL-server niet starten:</span><span class="sxs-lookup"><span data-stu-id="58bd8-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="58bd8-154">(d) stoppen Hallo MySQL-server:</span><span class="sxs-lookup"><span data-stu-id="58bd8-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="58bd8-155">(e) MySQL toostart instellen als Hallo system boot-up:</span><span class="sxs-lookup"><span data-stu-id="58bd8-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="58bd8-156">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="58bd8-156">Next Step</span></span>
<span data-ttu-id="58bd8-157">Meer informatie over het gebruik en informatie met betrekking tot MySQL vinden [hier](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="58bd8-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

