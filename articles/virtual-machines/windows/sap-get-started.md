---
title: aaaGetting gestart met SAP op Windows-machines in Azure | Microsoft Docs
description: Meer informatie over SAP oplossingen die worden uitgevoerd op virtuele machines (VM's) in Microsoft Azure
services: virtual-machines-windows
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e714c47-add3-44c5-a6c8-9d26472ddcc4
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 678770955ecc78bf1d39c193c833ae4e11912fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-azure-windows-virtual-machines-vms"></a><span data-ttu-id="da1e7-103">SAP gebruiken op Windows Azure virtuele Machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="da1e7-103">Using SAP on Azure Windows Virtual Machines (VMs)</span></span>
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription

[dbms-guide]:../virtual-machines-windows-sap-dbms-guide.md 
[dbms-guide-2.1]:../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md  
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:virtual-machines-windows-../linux/classic/sap-get-started.md
[getting-started-dbms]:virtual-machines-windows-../linux/classic/sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:virtual-machines-windows-../linux/classic/sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:virtual-machines-windows-../linux/classic/sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md
[getting-started-windows-classic-dbms]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

<span data-ttu-id="da1e7-104">Als u Microsoft Azure als uw SAP gereed cloud partner, kunt u zich kunt tooreliably uw bedrijfskritieke SAP taken op een scaaleable, compatibel zijn, en de enterprise bewezen platform worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="da1e7-104">By choosing Microsoft Azure as your SAP ready cloud partner, you will be able tooreliably run your mission critical SAP workloads on a scaaleable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="da1e7-105">Hallo Schaalbaarheidprestaties, flexability, ophalen en kosten besparen van Azure.</span><span class="sxs-lookup"><span data-stu-id="da1e7-105">Get hello scaleability, flexability, and cost savings of Azure.</span></span> <span data-ttu-id="da1e7-106">Hallo uitgevouwen samenwerking tussen Microsoft en SAP, u kunt tegenkomen SAP-toepassingen ontwikkelen en testen en productie scenario's in azure - en volledig worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="da1e7-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in azure - and be fully supported.</span></span> <span data-ttu-id="da1e7-107">Uit SAP NetWeaver tooSAP S4/HANA, Linux tooWindows, SAP HANA tooSQL, hebt u behandeld.</span><span class="sxs-lookup"><span data-stu-id="da1e7-107">From SAP NetWeaver tooSAP S4/HANA, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="da1e7-108">Met de services van Microsoft Azure-virtuele machine en SAP HANA op Azure-grote exemplaren biedt Microsoft een uitgebreide Infrastructure As A Service (IaaS)-platform.</span><span class="sxs-lookup"><span data-stu-id="da1e7-108">With Microsoft Azure virtual machine services, and SAP HANA on Azure large instances, Microsoft offers a comprehensive Infrastructure As A Service (IaaS) platform.</span></span> <span data-ttu-id="da1e7-109">Omdat een breed SAP-oplossingen worden ondersteund in Azure, dit 'ophalen gestart document fungeert als een tabel met inhoud voor de huidige set SAP-documenten.</span><span class="sxs-lookup"><span data-stu-id="da1e7-109">Because a wide range of SAP solutions are supported on Azure, this "getting started document will serve as a Table of Contents for our current set of SAP documents.</span></span> <span data-ttu-id="da1e7-110">Als meer titels ophalen tooour documentbibliotheek - toegevoegd ziet u deze hier toevoegen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-110">As more titles get added tooour document library - you will see them added here.</span></span> 

## <a name="sap-hana-certifications-on-microsoft-azure"></a><span data-ttu-id="da1e7-111">SAP HANA certificeringen op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="da1e7-111">SAP HANA Certifications on Microsoft Azure</span></span>
| <span data-ttu-id="da1e7-112">SAP-product</span><span class="sxs-lookup"><span data-stu-id="da1e7-112">SAP Product</span></span> | <span data-ttu-id="da1e7-113">Ondersteund besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="da1e7-113">Supported OS</span></span> | <span data-ttu-id="da1e7-114">Aanbiedingen voor Azure</span><span class="sxs-lookup"><span data-stu-id="da1e7-114">Azure Offerings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da1e7-115">SAP HANA-ontwikkelaarsversie (inclusief Hallo HANA clientsoftware bestaan uit SQLODBC, ODBO-alleen Windows, ODBC, JDBC-stuurprogramma's, HANA studio en HANA-database)</span><span class="sxs-lookup"><span data-stu-id="da1e7-115">SAP HANA Developer Edition (including hello HANA client software comprised of SQLODBC, ODBO-Windows only, ODBC, JDBC drivers, HANA studio, and HANA database)</span></span> |<span data-ttu-id="da1e7-116">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-116">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-117">A7, A8</span><span class="sxs-lookup"><span data-stu-id="da1e7-117">A7, A8</span></span> |
| <span data-ttu-id="da1e7-118">Een MHANA</span><span class="sxs-lookup"><span data-stu-id="da1e7-118">MHANA One</span></span> |<span data-ttu-id="da1e7-119">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-119">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-120">DS14_v2 (bij algemene beschikbaarheid)</span><span class="sxs-lookup"><span data-stu-id="da1e7-120">DS14_v2 (upon general availability)</span></span> |
| <span data-ttu-id="da1e7-121">SAP S/4HANA</span><span class="sxs-lookup"><span data-stu-id="da1e7-121">SAP S/4HANA</span></span> |<span data-ttu-id="da1e7-122">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-122">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-123">Gecontroleerde beschikbaarheid voor GS5, SAP HANA in Azure (grote exemplaren)</span><span class="sxs-lookup"><span data-stu-id="da1e7-123">Controlled Availability for GS5, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="da1e7-124">Suite op HANA, OLTP</span><span class="sxs-lookup"><span data-stu-id="da1e7-124">Suite on HANA, OLTP</span></span> |<span data-ttu-id="da1e7-125">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-125">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-126">SAP HANA op Azure (grote exemplaren)</span><span class="sxs-lookup"><span data-stu-id="da1e7-126">SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="da1e7-127">HANA Enterprise voor BW, OLAP</span><span class="sxs-lookup"><span data-stu-id="da1e7-127">HANA Enterprise for BW, OLAP</span></span> |<span data-ttu-id="da1e7-128">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-128">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-129">GS5 voor implementaties met één knooppunt, SAP HANA in Azure (grote exemplaren)</span><span class="sxs-lookup"><span data-stu-id="da1e7-129">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="da1e7-130">SAP BW/4HANA</span><span class="sxs-lookup"><span data-stu-id="da1e7-130">SAP BW/4HANA</span></span> |<span data-ttu-id="da1e7-131">Red Hat Enterprise Linux SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="da1e7-131">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="da1e7-132">GS5 voor implementaties met één knooppunt, SAP HANA in Azure (grote exemplaren)</span><span class="sxs-lookup"><span data-stu-id="da1e7-132">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |

## <a name="sap-netweaver-certifications"></a><span data-ttu-id="da1e7-133">SAP NetWeaver certificeringen</span><span class="sxs-lookup"><span data-stu-id="da1e7-133">SAP NetWeaver Certifications</span></span>
<span data-ttu-id="da1e7-134">Microsoft Azure is gecertificeerd voor Hallo SAP-producten, met volledige ondersteuning van Microsoft en SAP te volgen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-134">Microsoft Azure is certified for hello following SAP products, with full support from Microsoft and SAP.</span></span>

| <span data-ttu-id="da1e7-135">SAP-product</span><span class="sxs-lookup"><span data-stu-id="da1e7-135">SAP Product</span></span> | <span data-ttu-id="da1e7-136">Gastbesturingssysteem</span><span class="sxs-lookup"><span data-stu-id="da1e7-136">Guest OS</span></span> | <span data-ttu-id="da1e7-137">RDBMS</span><span class="sxs-lookup"><span data-stu-id="da1e7-137">RDBMS</span></span> | <span data-ttu-id="da1e7-138">Typen virtuele machines</span><span class="sxs-lookup"><span data-stu-id="da1e7-138">Virtual Machine Types</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da1e7-139">SAP Business Suite-software</span><span class="sxs-lookup"><span data-stu-id="da1e7-139">SAP Business Suite Software</span></span> |<span data-ttu-id="da1e7-140">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="da1e7-140">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="da1e7-141">SQL Server, Oracle (alleen Windows), DB2, SAP-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="da1e7-141">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="da1e7-142">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="da1e7-142">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="da1e7-143">SAP Business All-in-One</span><span class="sxs-lookup"><span data-stu-id="da1e7-143">SAP Business All-in-One</span></span> |<span data-ttu-id="da1e7-144">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="da1e7-144">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="da1e7-145">SQL Server, Oracle (alleen Windows), DB2, SAP-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="da1e7-145">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="da1e7-146">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="da1e7-146">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="da1e7-147">SAP Business Objects BI</span><span class="sxs-lookup"><span data-stu-id="da1e7-147">SAP BusinessObjects BI</span></span> |<span data-ttu-id="da1e7-148">Windows</span><span class="sxs-lookup"><span data-stu-id="da1e7-148">Windows</span></span> |<span data-ttu-id="da1e7-149">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="da1e7-149">N/A</span></span> |<span data-ttu-id="da1e7-150">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="da1e7-150">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="da1e7-151">SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="da1e7-151">SAP NetWeaver</span></span> |<span data-ttu-id="da1e7-152">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="da1e7-152">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="da1e7-153">SQL Server, Oracle (alleen Windows), DB2, SAP-as-omgeving</span><span class="sxs-lookup"><span data-stu-id="da1e7-153">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="da1e7-154">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="da1e7-154">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |

## <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="da1e7-155">Aan de slag met SAP HANA op Azure</span><span class="sxs-lookup"><span data-stu-id="da1e7-155">Getting Started with SAP HANA on Azure</span></span>
<span data-ttu-id="da1e7-156">titel: aaaQuickstart-handleiding voor handmatige installatie van het SAP HANA op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="da1e7-156">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="da1e7-157">Overzicht: Deze snelstartgids kunt tooset een single instance SAP HANA prototype/demo systeem op Azure VM's door een handmatige installatie van SAP NetWeaver 7.5 en SAP HANA SP12.</span><span class="sxs-lookup"><span data-stu-id="da1e7-157">Summary: This quickstart guide will help tooset up a single-instance SAP HANA prototype/demo system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="da1e7-158">Hallo handleiding wordt ervan uitgegaan dat Hallo lezer vertrouwd met de basisbeginselen van Azure IaaS is zoals hoe toodeploy virtuele machines of virtuele netwerken, hetzij via hello Azure-portal of Powershell/CLI inclusief Hallo optie toouse json-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-158">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="da1e7-159">Bovendien wordt verwacht dat de lezer Hallo vertrouwd met SAP HANA, SAP NetWeaver en hoe tooinstall het on is-premises.</span><span class="sxs-lookup"><span data-stu-id="da1e7-159">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="da1e7-160">Bijgewerkte: September 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-160">Updated: September 2016</span></span>

[<span data-ttu-id="da1e7-161">Deze handleiding vindt u hier</span><span class="sxs-lookup"><span data-stu-id="da1e7-161">This guide can be found here</span></span>](../virtual-machines-linux-sap-hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="da1e7-162">Snelstartgids voor NetWeaver op SUSE Linux op Azure</span><span class="sxs-lookup"><span data-stu-id="da1e7-162">Quickstart Guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="da1e7-163">titel: aaaTesting SAP NetWeaver op Microsoft Azure SUSE Linux VM's</span><span class="sxs-lookup"><span data-stu-id="da1e7-163">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="da1e7-164">Overzicht: In dit artikel beschrijft verschillende dingen tooconsider wanneer u SAP NetWeaver op virtuele Microsoft Azure SUSE Linux-machines (VM's) uitvoert.</span><span class="sxs-lookup"><span data-stu-id="da1e7-164">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="da1e7-165">SAP NetWeaver wordt vanaf mei 19 2016 officieel ondersteund in SUSE Linux virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="da1e7-165">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="da1e7-166">Alle gegevens met betrekking tot Linux-versies en versies van de kernel SAP vindt u in SAP-notitie 1928533 ' SAP-toepassingen in Azure: ondersteunde producten en Azure VM typen '.</span><span class="sxs-lookup"><span data-stu-id="da1e7-166">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="da1e7-167">Bijgewerkte: September 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-167">Updated: September 2016</span></span>

[<span data-ttu-id="da1e7-168">Deze handleiding vindt u hier</span><span class="sxs-lookup"><span data-stu-id="da1e7-168">This guide can be found here</span></span>](../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deploying-sap-ides-ehp7-sp3-for-sap-erp-60-on-microsoft-azure"></a><span data-ttu-id="da1e7-169">SAP IDE EHP7 SP3 implementeren voor SAP ERP 6.0 op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="da1e7-169">Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure</span></span>
<span data-ttu-id="da1e7-170">titel: aaaQuickstart-handleiding voor handmatige installatie van het SAP HANA op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="da1e7-170">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="da1e7-171">Overzicht: Dit artikel wordt beschreven hoe toodeploy SAP IDE met SQL Server en Windows-besturingssysteem op Microsoft Azure via SAP Cloud toestel bibliotheek 3.0 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="da1e7-171">Summary: This article describes how toodeploy SAP IDES running with SQL Server and Windows OS on Microsoft Azure via SAP Cloud Appliance Library 3.0.</span></span> 

<span data-ttu-id="da1e7-172">Bijgewerkte: September 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-172">Updated: September 2016</span></span>

[<span data-ttu-id="da1e7-173">Deze handleiding vindt u hier</span><span class="sxs-lookup"><span data-stu-id="da1e7-173">This guide can be found here</span></span>](sap-cal-ides-erp6-ehp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <span data-ttu-id="da1e7-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning en implementatie</span><span class="sxs-lookup"><span data-stu-id="da1e7-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and Implementation</span></span>
<span data-ttu-id="da1e7-175">titel: aaaSAP NetWeaver op Azure Virtual Machines (VM's) – plannen en implementatiehandleiding</span><span class="sxs-lookup"><span data-stu-id="da1e7-175">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide</span></span>

<span data-ttu-id="da1e7-176">Overzicht: Dit Hallo papier toostart met is als u denkt u over SAP NetWeaver in Azure virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="da1e7-176">Summary: This is hello paper toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="da1e7-177">Deze handleiding voor planning en implementatie helpt u evalueren of een bestaande of geplande SAP NetWeaver-systeem kan tooan geïmplementeerde virtuele Machines van Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="da1e7-177">This planning and implementation guide will help you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="da1e7-178">Dit omvat meerdere SAP NetWeaver implementatiescenario's en SAP-configuraties die specifieke tooAzure bevat.</span><span class="sxs-lookup"><span data-stu-id="da1e7-178">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="da1e7-179">Hallo papier bevat en alle Hallo benodigde configuratie-informatie u moet op Hallo SAP/Azure side toorun een hybride SAP liggend beschrijft.</span><span class="sxs-lookup"><span data-stu-id="da1e7-179">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="da1e7-180">Maatregelen kunt u hoge beschikbaarheid van systemen op basis van een SAP NetWeaver tooensure uitvoeren op IaaS vallen ook.</span><span class="sxs-lookup"><span data-stu-id="da1e7-180">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="da1e7-181">Bijgewerkte: Augustus 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-181">Updated: August 2016</span></span>

<span data-ttu-id="da1e7-182">[Deze handleiding vindt u hier][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="da1e7-182">[This guide can be found here][planning-guide]</span></span>

## <span data-ttu-id="da1e7-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Implementatie</span><span class="sxs-lookup"><span data-stu-id="da1e7-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment</span></span>
<span data-ttu-id="da1e7-184">titel: aaaSAP NetWeaver op Azure Virtual Machines (VM's) – Implementatiehandleiding</span><span class="sxs-lookup"><span data-stu-id="da1e7-184">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – Deployment Guide</span></span>

<span data-ttu-id="da1e7-185">Overzicht: Dit document bevat procedurele richtlijnen voor het implementeren van SAP NetWeaver software toovirtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="da1e7-185">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="da1e7-186">Dit artikel is gericht op drie specifieke implementatiescenario's met de nadruk op Hallo Azure Monitoring extensies voor SAP, inclusief het oplossen van aanbevelingen voor hello Azure Monitoring uitbreidingen voor SAP inschakelen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-186">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="da1e7-187">Dit artikel wordt ervan uitgegaan dat u hebt gelezen Hallo planning en implementatie helpen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-187">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="da1e7-188">Bijgewerkte: December 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-188">Updated: December 2016</span></span>

<span data-ttu-id="da1e7-189">[Deze handleiding vindt u hier][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="da1e7-189">[This guide can be found here][deployment-guide]</span></span>

## <span data-ttu-id="da1e7-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS Implementatiehandleiding</span><span class="sxs-lookup"><span data-stu-id="da1e7-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS Deployment Guide</span></span>
<span data-ttu-id="da1e7-191">titel: aaaSAP NetWeaver op Azure Virtual Machines (VM's) – DBMS Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="da1e7-191">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – DBMS Deployment Guide</span></span>

<span data-ttu-id="da1e7-192">Overzicht: In dit artikel bevat informatie over overwegingen voor planning en implementatie voor Hallo DBMS-systemen die moeten worden uitgevoerd in combinatie met SAP.</span><span class="sxs-lookup"><span data-stu-id="da1e7-192">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="da1e7-193">In het eerste deel hello, algemene overwegingen die worden vermeld en gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="da1e7-193">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="da1e7-194">Hallo volgende delen Hallo papier zich verhouden toodeployments van verschillende DBMS in Azure die worden ondersteund door SAP.</span><span class="sxs-lookup"><span data-stu-id="da1e7-194">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="da1e7-195">De verschillende DBMS-systemen die worden beschreven, zijn SQL Server, SAP ASE en Oracle.</span><span class="sxs-lookup"><span data-stu-id="da1e7-195">Different DBMS presented are SQL Server, SAP ASE and Oracle.</span></span> <span data-ttu-id="da1e7-196">In die specifieke delen worden overwegingen die u hebt tooaccount voor wanneer u SAP-systemen worden uitgevoerd op Azure in combinatie met deze DBMS besproken.</span><span class="sxs-lookup"><span data-stu-id="da1e7-196">In those specific parts considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="da1e7-197">Onderwerpen zoals back-up en hoge beschikbaarheid-methoden die worden ondersteund door verschillende DBMS in Azure worden weergegeven voor gebruik met SAP-toepassingen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="da1e7-197">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="da1e7-198">Bijgewerkte: Augustus 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-198">Updated: August 2016</span></span>

<span data-ttu-id="da1e7-199">[Deze handleiding vindt u hier][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="da1e7-199">[This guide can be found here][dbms-guide]</span></span>

## <span data-ttu-id="da1e7-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>Implementatiehandleiding voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="da1e7-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>High Availability Deployment Guide</span></span>
<span data-ttu-id="da1e7-201">titel: aaaSAP NetWeaver op Azure Virtual Machines (VM's) – Implementatiehandleiding voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="da1e7-201">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – High Availability Deployment Guide</span></span>

<span data-ttu-id="da1e7-202">Overzicht: Dit document beschrijft hoe SAP storingspunt fout onderdelen, zoals SAP ASC's / SCS Hallo en DBMS in Azure kan worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="da1e7-202">Summary: This document describes how SAP single point of failure components like hello SAP ASCS/SCS and DBMS can be protected in Azure.</span></span> <span data-ttu-id="da1e7-203">Onderdelen van Hallo SAP ASC's / SCS, DBMS en toepassing servers zijn essentieel voor het Hallo-functionaliteit van SAP NetWeaver systemen, zoals SAP NetWeaver ABAP, SAP NetWeaver Java, SAP NetWeaver ABAP + Java-systemen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-203">Components of hello SAP ASCS/SCS, DBMS and application servers are essential for hello functionality of SAP NetWeaver systems, e.g. SAP NetWeaver ABAP, SAP NetWeaver Java, SAP NetWeaver ABAP+Java systems.</span></span> <span data-ttu-id="da1e7-204">Hoge beschikbaarheid functionaliteit behoeften toobe plaatsen in plaats daarom toomake ervoor dat deze onderdelen een storing van een server of een virtuele machine tolereren kunnen terwijl u doen met Windows clusterconfiguraties voor bare metal- en Hyper-V-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="da1e7-204">Therefore, high-availability functionality needs toobe put in place toomake sure that those components can sustain a failure of a server or a VM as done with Windows Cluster configurations for bare-metal and Hyper-V environments.</span></span>

<span data-ttu-id="da1e7-205">Bijgewerkte: December 2016</span><span class="sxs-lookup"><span data-stu-id="da1e7-205">Updated: December 2016</span></span>

<span data-ttu-id="da1e7-206">[Deze handleiding vindt u hier][ha-guide]</span><span class="sxs-lookup"><span data-stu-id="da1e7-206">[This guide can be found here][ha-guide]</span></span>

