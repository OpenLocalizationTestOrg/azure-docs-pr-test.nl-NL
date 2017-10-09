---
title: aaaLinux en Open-Source Computing in Azure | Microsoft Docs
description: "Een lijst met Linux en Open-Source Computing artikelen op Azure, met inbegrip van basisgebruik Linux enkele belangrijke concepten over uitgevoerd of bij het uploaden van afbeeldingen op Azure en andere inhoud over specifieke technologieën en optimalisatie van Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Linux en open-source computing in Azure
Alle documentatie Hallo u toocreate nodig hebt en beheren op basis van Linux virtuele machines in het klassieke implementatiemodel Hallo vinden.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="get-started"></a>Aan de slag
* [Inleiding voor Linux op Azure](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Veelgestelde vragen over Azure virtuele Machines die zijn gemaakt met het klassieke implementatiemodel Hallo](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Over de installatiekopieën voor virtuele machines](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Uploaden van uw eigen installatiekopie Distro](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (en ook instructies met een [Azure-Endorsed distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))
* [Meld u aan tooa Linux VM gebruik Hallo klassieke Azure-portal](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Instellen
* [Installeren Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Zelfstudies
* [Hallo licht Stack installeren op een virtuele Linux-machine in Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ruby op Rails webtoepassing op een virtuele machine in Azure](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [How to: installatie Apache Qpid Proton-C voor AMQP en Servicebus](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Databases
* [Optimaliseren van MySQL in Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MySQL-Clusters](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Cassandra uitgevoerd met Linux op Azure en benaderen met Node.js](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Een cluster met meerdere masters van MariaDbs maken](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Aan de slag met Linux-rekenknooppunten in een cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Voer NAMD met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Met behulp van Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Met behulp van Docker VM-extensie Hallo van hello Azure-portal](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hoe toouse docker-machine in Azure](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [How to: MySQL-Clusters](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [How to: Node.js en Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [How to: installeren en uitvoeren van MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [How to: virtuele CoreOS gebruiken in Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Planning
* [Implementatierichtlijnen voor Azure-infrastructuurservices](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux-gebruikersnamen selecteren](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hoe tooconfigure een beschikbaarheidsset voor virtuele machines in het klassieke implementatiemodel Hallo](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hoe tooSchedule gepland onderhoud op Azure Virtual machines](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hallo-beschikbaarheid van virtuele machines beheren](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Gepland onderhoud voor Linux virtuele machines in Azure](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Implementatie
* [Een aangepaste virtuele machine met Linux maken](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hallo basisprincipes: het vastleggen van een Linux-VM tooMake een sjabloon](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>Beheer
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hoe tooReset een wachtwoord of SSH-eigenschappen voor Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Met behulp van basis](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Azure-bronnen
* [Hello Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM-extensies en functies](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Injecteren van aangepaste gegevens in een VM-toouse met Cloud-init](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Storage
* [Een gegevensschijf tooa Linux VM koppelen](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Voor het ontkoppelen van een gegevensschijf van een virtuele Linux-machine](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Netwerken
* [Hoe tooset eindpunten op een klassieke virtuele machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Problemen oplossen
* [Secure Shell (SSH) verbindingen tooa op basis van Linux virtuele machine van Azure oplossen](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Klassieke implementatieproblemen met het maken van een nieuwe virtuele Linux-machine in Azure oplossen](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>Naslaginformatie
* [Azure CLI-opdrachten in de modus Azure Service Management (asm)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure Service Management REST-API](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Algemene koppelingen
Hallo koppelingen volgen zijn voor blogs van Microsoft, Technet-pagina's en externe sites plaats Azure.com documentatie als hierboven. Als zowel Azure als Hallo open source computing world fast-verplaatst doelen, is bijna bepaalde die Hallo na koppelingen zijn verouderd, *ondanks* Hallo feit dat we onze best toocontinually doet nieuwere onderwerpen toevoegen en verwijderen verouderde die zijn. Als er een hebt gemist, neem laat het ons weten in Hallo opmerkingen of verzenden van een pull-aanvraag tooour [GitHub-repo-](https://github.com/Azure/azure-content/).

* [ASP.NET 5 uitgevoerd op Linux met behulp van Docker-Containers](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [Hoe een CentOS VM-installatiekopie uit OpenLogic tooDeploy](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE Update-infrastructuur](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server voor SAP-Cloudbibliotheek toestel](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Maximaal beschikbare Linux bouwen op Azure in 12 stappen](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Linux inrichten op Azure met Azure CLI, node.js, jhawk automatiseren](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [GlusterFS op Azure](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [FreeBSD worden uitgevoerd in Azure](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [Eenvoudig implementeren FreeBSD](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [Een aangepaste installatiekopie van de FreeBSD implementeren](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky AV voor Linux-bestandsserver](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [8 open-source NoSql-Databases voor Azure](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech): Ervaringen met CouchDb op Azure](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [CouchDB-as-a-Service met node.js, CORS en knorvis uitgevoerd](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Redis in Windows in hello Azure Redis Cache Service](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [ASP.NET-sessiestatus-Provider voor de Preview-versie Redis aangekondigd](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog: RavenHQ nu beschikbaar in hello Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Big Data
* [Hadoop op Azure Linux VM's installeren](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>Relationele database
* [Architectuur van MySQL hoge beschikbaarheid in Microsoft Azure](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Installatie van Postgres met corosync, pg_bouncer ILB gebruiken](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Linux high performance computing (HPC)
* [Quick Start-sjabloon: een cluster SLURM ronddraaien](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (en [blogbericht](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Quick Start-sjabloon: een HPC-cluster maken met Linux-rekenknooppunten](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>Devops-, beheers- en optimalisatie
Als Hallo wereld van devops-, beheers- en optimalisatie heel omvangrijk is en zeer snel te wijzigen, kunt u overwegen Hallo lijst onder een beginpunt.

* [Video: Azure virtuele Machines: met behulp van Chef, Puppet en Docker voor het beheren van virtuele Linux-machines](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [Handleiding tooautomated Kubernetes Clusterimplementatie met virtuele CoreOS en weefpatroon voltooien](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Jenkins Slave invoegtoepassing voor Azure](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [GitHub-repo: Jenkins Storage Plug-in voor Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Externe partij: Hudson Slave Plug-in voor Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Externe partij: Hudson Storage Plug-in voor Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Video: Wat is er Chef en hoe werkt dit?](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Video: Hoe tooUse Azure Automation met Linux VM's](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog: Hoe toodo Powershell DSC voor Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: Docker Client DSC](https://github.com/anweiss/DockerClientDSC)
* [Verpakker-invoegtoepassing voor Azure](https://github.com/msopentech/packer-azure)

