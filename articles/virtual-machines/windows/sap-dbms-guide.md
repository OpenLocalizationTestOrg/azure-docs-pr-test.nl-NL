---
title: "aaaSAP NetWeaver op Azure Virtual machines – DBMS Deployment Guide | Microsoft Docs"
description: "SAP NetWeaver op Azure virtuele Machines (VM's) – DBMS Implementatiehandleiding"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver op Windows Azure virtuele Machines (VM's) – DBMS Implementatiehandleiding
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

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

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
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
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
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

Deze handleiding is onderdeel van het Hallo-documentatie over het implementeren en te implementeren Hallo SAP-software in Microsoft Azure. Lees voordat u deze handleiding leest, Hallo [plannen en implementatiehandleiding][planning-guide]. Dit document bevat informatie over Hallo-implementatie van verschillende relationele Database Management Systems (RDBMS) en verwante producten in combinatie met SAP op Microsoft Azure Virtual Machines (VM's) met hello Azure-infrastructuur als een Service (IaaS)-mogelijkheden.

Hallo papier aanvullingen Hallo SAP-documentatie voor installatie en SAP-opmerkingen Hallo primaire bronnen voor installaties en implementaties van software op SAP vertegenwoordigen opgegeven platforms

## <a name="general-considerations"></a>Algemene overwegingen
In dit hoofdstuk gerelateerd overwegingen van actieve SAP DBMS-systemen in Azure VM's zijn geïntroduceerd. Er zijn enkele verwijzingen toospecific DBMS-systemen in dit hoofdstuk. In plaats daarvan worden Hallo specifieke DBMS-systemen behandeld in dit artikel, na dit hoofdstuk.

### <a name="definitions-upfront"></a>Definities van tevoren
In hele document hello gebruiken we Hallo volgende voorwaarden:

* IaaS: Infrastructuur als een Service.
* PaaS: Platform als een Service.
* SaaS: Software als een Service.
* SAP-onderdeel: een afzonderlijke SAP toepassing zoals ECC, BW, oplossing Manager of EP is geplaatst.  SAP-onderdelen kunnen worden gebaseerd op traditionele ABAP of Java-technologieën of een NetWeaver op basis van toepassing zoals zakelijke objecten.
* SAP-omgeving: een of meer onderdelen voor SAP logisch zijn gegroepeerd tooperform een zakelijke functie zoals ontwikkeling, QAS, Training, DR of productie.
* SAP liggend: Dit verwijst toohello gehele SAP activa in een klant IT Liggend. Hallo SAP liggend bevat alle productie en niet-productieve omgevingen.
* SAP-systeem: Hallo combinatie van laag DBMS en toepassingslaag van bijvoorbeeld een SAP ERP-ontwikkelsysteem, SAP BW testsysteem, productiesysteem SAP CRM, enzovoort. Implementaties is het niet ondersteund toodivide deze twee lagen tussen on-premises en Azure in Azure. Dit betekent dat er ofwel een SAP-systeem lokale geïmplementeerd of deze is geïmplementeerd in Azure. U kunt echter verschillende systemen Hallo van een liggend SAP in Azure of on-premises implementeren. U kunt bijvoorbeeld Hallo SAP CRM ontwikkeling en tests systemen in Azure implementeren maar SAP CRM productie system lokale Hallo.
* Cloud-implementatie: een implementatie waarbij hello Azure-abonnement niet is verbonden via een site-naar-site of ExpressRoute-verbinding toohello lokale netwerkinfrastructuur. Gemeenschappelijk Azure-documentatie dergelijke implementaties worden ook beschreven als 'Cloud-Only'-implementaties. Virtuele Machines die worden geïmplementeerd met deze methode toegankelijk zijn via Internet Hallo en openbare Internet eindpunten toegewezen toohello virtuele machines in Azure. Hallo lokale Active Directory (AD) en DNS is niet uitgebreid tooAzure in dergelijke implementaties. Daarom maken Hallo VM's geen deel uit van Hallo op lokale Active Directory. Opmerking: Cloud-implementaties in dit document worden gedefinieerd als volledige SAP landschappen welke on-premises in openbare cloud uitsluitend in Azure zonder extensie van Active Directory of naamomzetting worden uitgevoerd. Alleen in de cloud-configuraties worden niet ondersteund voor productie SAP-systemen of -configuraties waar nodig toobe gebruikt tussen SAP-systemen die worden gehost op Azure en bronnen die zich lokaal SAP stm of andere lokale bronnen.
* Cross-Premises: Beschrijft een scenario waarin VM's zijn geïmplementeerde tooan Azure-abonnement met site-naar-site, meerdere locaties of ExpressRoute-verbindingen tussen Hallo lokale clientresources en Azure. Gemeenschappelijk Azure-documentatie, dit soort implementaties worden ook beschreven als Cross-Premises scenario's. Hallo reden voor Hallo verbinding is tooextend on-premises domeinen, on-premises Active Directory en lokale DNS in Azure. Hallo lokale liggend is uitgebreide toohello Azure activa van Hallo-abonnement. Met deze uitbreiding, kan Hallo VMs deel uitmaken van Hallo lokaal domein. Domeingebruikers van Hallo lokale domein hebben toegang tot Hallo-servers en services kunnen uitvoeren op de virtuele machines (zoals DBMS services). Communicatie en naamomzetting tussen VM's geïmplementeerd lokale en virtuele machines die zijn geïmplementeerd in Azure is mogelijk. We verwachten dat dit toobe Hallo meest voorkomende scenario voor het implementeren van SAP activa in Azure. Zie [dit] [ vpn-gateway-cross-premises-options] artikel en [dit] [ vpn-gateway-site-to-site-create] voor meer informatie.

> [!NOTE]
> Cross-Premises implementaties van waar Azure Virtual Machines SAP computers lid van een lokaal domein zijn SAP-systemen worden ondersteund voor productie SAP-systemen. Cross-Premises configuraties worden ondersteund voor het implementeren van onderdelen of SAP landschappen in Azure te voltooien. Hallo voltooid SAP liggend zelfs worden uitgevoerd in Azure vereist dat deze VMs deel van het lokale domein en ADVERTENTIES. In eerdere versies van Hallo documentatie besproken we hybride IT-scenario's waarbij Hallo term 'Hybride' verankerd in Hallo feit ligt dat er een cross-premises-connectiviteit tussen on-premises en Azure. In dit geval 'Hybride' ook betekent dat Hallo virtuele machines in Azure deel van Hallo uitmaken een on-premises Active Directory.
>
>

Sommige Microsoft-documentatie worden scenario's voor Cross-Premises iets anders, met name voor DBMS HA configuraties beschreven. In Hallo geval Hallo SAP gerelateerde documenten, Hallo Cross-Premises scenario slechts komt meestal neer toohaving een site-naar-site of privé (ExpressRoute)-connectiviteit en toohello fact dat Hallo SAP Liggend wordt verdeeld tussen on-premises en Azure.

### <a name="resources"></a>Resources
Hallo zijn volgende handleidingen beschikbaar voor Hallo onderwerp SAP-implementaties op Azure:

* [SAP NetWeaver op Azure virtuele Machines (VM's) – Planning en implementatiehandleiding][planning-guide]
* [SAP NetWeaver op Azure virtuele Machines (VM's) – Implementatiehandleiding][deployment-guide]
* [SAP NetWeaver op Azure Virtual Machines (VM's) – DBMS Deployment Guide (in dit document)][dbms-guide]
* [SAP NetWeaver op Azure virtuele Machines (VM's) – Implementatiehandleiding voor hoge beschikbaarheid][ha-guide]

Hallo SAP opmerkingen bij de volgende zijn gerelateerde toohello onderwerp van SAP op Azure:

| Het nummer | Titel |
| --- | --- |
| [1928533] |SAP-toepassingen in Azure: typen ondersteunde producten en de virtuele machine in Azure |
| [2015553] |SAP op Microsoft Azure: ondersteuning voor vereisten |
| [1999351] |Het oplossen van uitgebreide Azure-bewaking voor SAP |
| [2178632] |Sleutel bewaking van metrische gegevens voor SAP op Microsoft Azure |
| [1409604] |Virtualisatie in Windows: uitgebreide bewaking |
| [2191498] |SAP op Linux met Azure: uitgebreide bewaking |
| [2039619] |SAP-toepassingen over het gebruik van Microsoft Azure Hallo Oracle-Database: ondersteunde producten en versies |
| [2233094] |DB6: SAP-toepassingen in Azure met IBM DB2 voor Linux, UNIX- en Windows - aanvullende informatie |
| [2243692] |Linux op Microsoft Azure (IaaS) VM: problemen met SAP-licentie |
| [1984787] |SUSE LINUX Enterprise Server 12: Opmerkingen bij de installatie |
| [2002167] |Red Hat Enterprise Linux 7.x: installatie en Upgrade |

Lees ook Hallo [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) die alle SAP notities voor Linux bevat.

U hebt een praktische kennis over Hallo Microsoft Azure-architectuur en hoe Microsoft Azure Virtual Machines zijn geïmplementeerd en beheerd. U vindt meer informatie hier <https://azure.microsoft.com/documentation/>

> [!NOTE]
> We zijn **niet** Microsoft Azure-Platform als een Service (PaaS)-aanbiedingen van Microsoft Azure-Platform Hallo bespreken. Dit artikel is over het uitvoeren van een databasebeheersysteem (DBMS) in Microsoft Azure Virtual Machines (IaaS) net zoals u Hallo DBMS in uw on-premises omgeving uitvoeren zou. Database-mogelijkheden en functies tussen deze twee aanbiedingen heel verschillend zijn en moeten niet wordt verward met elkaar. Zie ook: <https://azure.microsoft.com/services/sql-database/>
>
>

Aangezien we IaaS bespreekt, zijn in het algemeen Hallo Windows, Linux en DBMS installatie en configuratie in wezen Hallo hetzelfde als elke virtuele machine of bare metal machine zou u on-premises installeert. Er zijn echter enkele architectuur en system management-implementatie beslissingen die verschillen bij gebruik van IaaS. Hallo-doel van dit document is tooexplain Hallo specifieke architecturale en system management verschillen die u moet worden voorbereid voor wanneer u IaaS.

In het algemeen zijn hello algehele gebieden van verschil dat in dit artikel wordt uitgelegd hoe:

* Hallo juiste VM/VHD-indeling van SAP systemen tooensure planning u Hallo juiste gegevens bestand lay-out hebben en voldoende IOP's voor uw workload kunt bereiken.
* Netwerken overwegingen bij het gebruik van IaaS.
* Specifieke database functies toouse in volgorde toooptimize Hallo database lay-out.
* Overwegingen voor back-up en herstel in IaaS.
* Met behulp van verschillende typen installatiekopieën voor implementatie.
* Hoge beschikbaarheid in Azure IaaS.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Structuur van een RDBMS-implementatie
Volg dit hoofdstuk in volgorde, wordt deze nodig toounderstand gepresenteerde [dit] [ deployment-guide-3] hoofdstuk Hallo [Deployment Guide][deployment-guide]. Kennis over andere VM-serie Hallo en hun verschillen en verschillen tussen Azure Standard en Premium-opslag moeten worden begrepen en bekend voordat dit hoofdstuk wordt gelezen.

Tot en met maart 2015 zijn VHD's van Azure een besturingssysteem met beperkte too127 GB groot. Deze beperking is opgeheven maart 2015 (voor meer informatie controle <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> ). Van daaruit op VHD's kunt met Hallo-besturingssysteem hebben Hallo dezelfde grootte hebben als een andere VHD. Niettemin liever we nog steeds een implementatie waarbij hello besturingssysteem, de DBMS en de uiteindelijke SAP-binaire bestanden gescheiden van databasebestanden Hallo zijn-structuur. We verwachten daarom SAP-systemen die zijn uitgevoerd in Azure Virtual Machines hebben Hallo base VM (of VHD) met het Hallo-besturingssysteem is geïnstalleerd, database management system uitvoerbare bestanden en SAP uitvoerbare bestanden. Hallo DBMS gegevens en logboekbestanden worden opgeslagen in Azure Storage (Standard of Premium-opslag) in afzonderlijke VHD-bestanden en als logische schijven toohello oorspronkelijke Azure besturingssysteemkopie VM gekoppeld.

Afhankelijk van het gebruik van Azure Standard of Premium-opslag (bijvoorbeeld via Hallo DS-serie- of GS-serie VM's) er zijn andere quota's in Azure die worden beschreven [hier][virtual-machines-sizes]. Bij het plannen van uw Azure-VHD's, moet u toofind Hallo beste balans van Hallo quota voor Hallo volgende:

* Hallo aantal gegevensbestanden worden opgeslagen.
* Hallo aantal VHD's die Hallo bestanden bevatten.
* Hallo IOPS quota's van een enkele VHD.
* Hallo gegevensdoorvoer per VHD.
* Hallo aantal aanvullende VHD's mogelijk per VM-grootte.
* Hallo algemene opslagdoorvoer een VM kan bieden.

Azure wordt afgedwongen door een quotum IOP's per schijf van de VHD. Deze quota zijn verschillend voor VHD's die worden gehost op Azure Standard-opslag- en Premium-opslag. I/o-latentie worden ook heel verschillend tussen twee opslagtypen Hallo met Premium-opslag factoren leveren betere i/o-latentie. Elk van de andere VM-typen Hallo hebben een beperkt aantal VHD's dat u kunt tooattach zijn. Een andere beperking is dat alleen bepaalde typen VM van Azure Premium-opslag gebruikmaken kunnen. Dit betekent dat Hallo besluit voor een bepaald type van de virtuele machine kan niet alleen worden veroorzaakt door Hallo CPU en geheugen nodig, maar ook door Hallo IOP's, latentie en schijf doorvoer vereisten die gewoonlijk worden geschaald met het aantal virtuele harde schijven Hallo of Hallo type Premium-opslag-schijven. Vooral met Premium-opslag kan Hallo grootte van een VHD ook worden bepaald door Hallo aantal IOPS en doorvoerlimieten die toobe bereikt door elke VHD behoeften.

Hallo feit dat Hallo IOPS snelheid, Hallo VHD's die zijn gekoppeld, aantal en grootte van de VM zijn alle gebundeld, Hallo Hallo leiden tot een Azure-configuratie van een SAP system toobe die afwijken van de on-premises implementatie. limieten voor Hallo IOP's per LUN worden doorgaans geconfigureerd in on-premises implementaties. Terwijl met Azure Storage deze limieten vaste of zoals in Premium-opslag die afhankelijk zijn van het type Hallo-schijf zijn. Dus met on-premises implementaties zien we klant configuraties van database-servers die gebruikmaken van veel verschillende volumes voor speciale uitvoerbare bestanden, zoals SAP en Hallo DBMS of speciale volumes voor tijdelijke databases of tabel spaties. Wanneer deze een on-premises systeem verplaatste tooAzure kan dit ertoe leiden tooa afval van mogelijke IOPS bandbreedte door verspilling van een VHD voor uitvoerbare bestanden of databases die niet alle of geen een groot aantal IOPS uitvoert. In Azure VM's adviseren wij daarom deze Hallo DBMS en SAP uitvoerbare bestanden worden geïnstalleerd op de schijf Hallo OS indien mogelijk.

Hallo moet plaatsing van de databasebestanden Hallo en logboekbestanden en Hallo type Azure-opslag gebruikt, worden gedefinieerd door IOPS, doorvoer vereisten en latentie. In de volgorde toohave voldoende IOPS aan voor het transactielogboek hello, mogelijk geforceerde tooleverage meerdere VHD's voor het transactielogboek Hallo bestand of gebruik een grotere schijf van de Premium-opslag. In dat geval een zou gewoon bouwen van een software RAID-(bijvoorbeeld Windows Storage Pool voor Windows of MDADM en LVM (beheer van logische Volume) voor Linux) Hello VHD's die Hallo transactielogboek zal bevatten.

- - -
> ![Windows][Logo_Windows] Windows
>
> Station D:\ in een Azure VM is een niet-persistente station die wordt ondersteund door een aantal lokale schijven op Hallo Azure compute-knooppunt. Omdat het niet-persistente, betekent dit dat alle wijzigingen toohello inhoud op station D:\ Hallo verloren gaat wanneer Hallo VM opnieuw wordt opgestart. Door 'wijzigingen' dat we opgeslagen bestanden, mappen die zijn gemaakt, toepassingen die zijn geïnstalleerd, enzovoort.
>
> ![Linux][Logo_Linux] Linux
>
> Linux Azure Virtual machines automatisch een station koppelen aan /mnt/resource die een niet-persistente station ondersteund door het lokale schijven op Hallo Azure compute-knooppunt is. Omdat het niet-persistente, betekent dit dat eventuele wijzigingen toocontent in /mnt/resource verloren gaat wanneer Hallo VM opnieuw wordt opgestart. De wijzigingen bedoelen we opgeslagen bestanden, mappen die zijn gemaakt, toepassingen die zijn geïnstalleerd, enzovoort.
>
>

- - -
Afhankelijk van hello Azure VM-serie, Hallo lokale schijven op Hallo compute knooppunt verschillende prestaties weergeven die kan worden ingedeeld als volgt:

* A0-A7: Zeer beperkt prestaties. Niet worden gebruikt voor alles afgezien van wisselbestand van windows
* A8-A11: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde
* D-reeks: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde
* DS-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde
* G-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde
* GS-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde

Instructies hierboven zijn toohello VM typen die zijn gecertificeerd met SAP toepassen. Hallo VM-serie met uitstekende IOPS en doorvoerlimieten in aanmerking voor gebruik door sommige DBMS-functies, zoals tempdb of tijdelijke tabelruimte.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Cache voor virtuele machines en VHD 's
Wanneer we deze schijven/VHD's via Hallo portal of wanneer we de geüploade virtuele harde schijven tooVMs koppelen maakt, kunnen we kiezen of Hallo i/o-verkeer tussen Hallo VM en deze VHD's zich bevinden in Azure-opslag in cache zijn opgeslagen. Azure Standard en Premium-opslag kunt u twee verschillende technologieën gebruiken voor dit type van de cache. In beide gevallen Hallo cache zelf zou worden schijf ondersteund op Hallo dezelfde stations gebruikt door Hallo tijdelijke schijf (D:\ in Windows) of /mnt/resource op Linux Hallo VM.

Hallo mogelijke cache typen zijn voor Azure Standard-opslag:

* Er is geen cache
* Opslaan in cache lezen
* Lezen en schrijven in cache opslaan

In de volgorde tooget consistent en deterministisch prestaties, moet u instellen Hallo cachegebruik op Azure Standard-opslag voor alle virtuele harde schijven met **DBMS gerelateerde gegevensbestanden, logboekbestanden en tabel ruimte too'NONE'**. Hallo caching van Hallo VM kan blijven met Hallo standaard.

Azure Premium-opslag bestaan Hallo cacheopties te volgen:

* Er is geen cache
* Opslaan in cache lezen

Aanbeveling voor Azure Premium-opslag is tooleverage **gegevensbestanden opslaan in cache lezen** van Hallo SAP-database en kies **niet in cache opslaan voor Hallo VHD(s) van logboekbestanden**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>Software-RAID
Zoals hierboven al vermeld moet u toobalance Hallo aantal IOPS die nodig zijn voor de databasebestanden Hallo over Hallo aantal VHD's die u kunt configureren en Hallo maximumaantal IOPS een Azure VM per VHD- of Premium-opslag biedt schijftype. Eenvoudigst toodeal Hello IOPS via VHD's laden een software-RAID toobuild ligt boven de Hallo verschillende VHD's. Plaats vervolgens een aantal gegevensbestanden Hallo SAP DBMS op Hallo die LUN 's oppervlaktevariaties buiten Hallo software-RAID. Afhankelijk van het Hallo-vereisten dat kunt u tooconsider Hallo gebruik van Premium-opslag ook sinds twee Hallo drie verschillende schijven in de Premium-opslag bieden hogere IOPS quotum dan VHD's op basis van de Standard-opslag. Hallo naast belangrijke beter i/o-latentie verstrekt door Azure Premium-opslag.

Dit geldt ook toohello transactielogboek van Hallo verschillende DBMS-systemen. Met veel van deze alleen toe te voegen meer Tlog bestanden helpt niet omdat Hallo DBMS-systemen in een van de Hallo bestanden tegelijk alleen schrijven. Als hogere IOPS tarieven nodig zijn dan één standaard opslag op basis van VHD kunt leveren, kunt u stripe via meerdere Standard-opslag-VHD's of kunt u een grotere schijftype voor Premium-opslag die buiten de tarieven voor hogere IOPS ook factoren lagere latentie voor Hallo schrijven biedt ik / Het besturingssysteem in het transactielogboek Hallo.

Situaties opgetreden in de Azure-implementaties die zou voorkeur met behulp van een software-RAID zijn:

* Logboek/opnieuw transactielogboek vereisen meer IOPS dan Azure worden verstrekt voor een enkele VHD. Zoals hierboven vermeld dit kan worden opgelost door het bouwen van een LUN via meerdere VHD's met behulp van een software-RAID.
* Ongelijke i/o-werkbelasting distributie via verschillende Hallo-gegevensbestanden van Hallo SAP-database. In dergelijke gevallen kan een ervaren één gegevensbestand, kunt u in plaats van te vaak door Hallo quotum. Terwijl andere gegevensbestanden nog niet sluiten toohello IOPS quotum van een enkele VHD krijgen zijn. In dergelijke gevallen Hallo gemakkelijke oplossing is toobuild een LUN via meerdere VHD's met behulp van een software-RAID.
* U niet weet welke Hallo exacte i/o-werkbelasting per gegevensbestand is en alleen ongeveer weten wat Hallo totale IOP's werkbelasting tegen Hallo DBMS is. Eenvoudigste toodo is toobuild één LUN Hello help van een software-RAID. Hallo som van quota van meerdere VHD's achter deze LUN moet vervolgens voldoen Hallo IOPS bekend snelheid.

- - -
> ![Windows][Logo_Windows] Windows
>
> Informatie over het gebruik van Windows Server 2012 of hoger opslagruimten verdient omdat het is efficiënter dan Windows Striping van eerdere versies van Windows. Zorg ervoor dat u mogelijk nodig hebt toocreate Hallo Windows opslaggroepen en opslagruimten met PowerShell-opdrachten bij gebruik van Windows Server 2012 als besturingssysteem. Hallo PowerShell-opdrachten vindt u hier <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Alleen MDADM en LVM (beheer van logische Volume) zijn ondersteunde toobuild een software-RAID op Linux. Voor meer informatie lezen Hallo artikelen te volgen:
>
> * [Configureren van Software-RAID op Linux] [ virtual-machines-linux-configure-raid] (voor MDADM)
> * [LVM configureren op een virtuele Linux-machine in Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Overwegingen voor het gebruik van VM-serie, die meestal kunnen toowork met Azure Premium-opslag zijn:

* Verzoeken voor i/o-latentie die sluit toowhat SAN/NAS-apparaten leveren.
* Verzoek tot factoren betere i/o-latentie dan Azure Standard-opslag kunt leveren.
* Hogere IOP's per VM dan wat kan worden verkregen met meerdere standaard opslag VHD's op basis van een bepaald type van de virtuele machine.

Sinds hello repliceert Azure Storage onderliggende elke opslagknooppunten VHD tooat minimaal drie eenvoudige RAID 0 striping kan worden gebruikt. Er is geen noodzaak tooimplement RAID 5- of RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Microsoft Azure Storage
Microsoft Azure Storage slaat Hallo base VM (met OS) en virtuele harde schijven of BLOBs tooat minimaal 3 afzonderlijke opslagknooppunten. Wanneer u een opslagaccount maakt, is er een keuze uit de beveiliging als volgt te werk:

![Geo-replicatie is ingeschakeld voor Azure Storage-account][dbms-guide-figure-100]

Azure Storage lokale-replicatie (lokaal Redundant) biedt bescherming tegen gegevensverlies vanwege fout tooinfrastructure dat enkele klanten kunnen worden gebruikt voor het toestaan van toodeploy. Zoals hierboven er zijn 4 verschillende opties met een vijfde wordt een variant van een van de Hallo eerst drie. Dichter ze zoeken kunt we onderscheiden:

* **Premium lokaal redundante opslag (LRS)**: Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines met I/O-intensieve werkbelastingen. Er zijn 3 kopieën van gegevens binnen Hallo Hallo dezelfde Azure-datacenter van een Azure-regio. Hallo kopieën worden in verschillende domeinen met fouten en domeinen upgraden (voor Zie concepten [dit] [ planning-guide-3.2] hoofdstuk in Hallo [Planningshandleiding][planning-guide]). In geval van een replica van Hallo gegevens uit de service vervaldatum tooa opslag knooppuntfout of schijffout gaan, wordt een nieuwe replica automatisch gegenereerd.
* **Lokaal redundante opslag (LRS)**: In dit geval zijn er 3 kopieën van gegevens binnen Hallo Hallo dezelfde Azure-datacenter van een Azure-regio. Hallo kopieën worden in verschillende domeinen met fouten en domeinen upgraden (voor Zie concepten [dit] [ planning-guide-3.2] hoofdstuk in Hallo [Planningshandleiding][planning-guide]). In geval van een replica van Hallo gegevens uit de service vervaldatum tooa opslag knooppuntfout of schijffout gaan, wordt een nieuwe replica automatisch gegenereerd.
* **Geografisch redundante opslag (GRS)**: Er is In dit geval een asynchrone replicatie die wordt een extra feed 3 replica's van Hallo-gegevens in een andere Azure-regio die in de meeste gevallen Hallo in dezelfde geografische regio (zoals Noord-Europa en West Hallo Europa). Dit leidt tot 3 extra replica's, zodat er 6 replica's in sum zijn. Een variant van dit is een aanvulling waar Hallo-gegevens in Hallo geografisch gerepliceerde Azure-regio voor lezen (Read-Access Geo-Redundant) kunnen worden gebruikt.
* **Zone-redundante opslag (ZRS)**: In dit geval Hallo 3 replica's van Hallo gegevens blijven in dezelfde Azure-regio Hallo. Zoals uitgelegd in [dit] [ planning-guide-3.1] hoofdstuk Hallo [Planningshandleiding] [ planning-guide] een Azure-regio een aantal datacenters dicht kan zijn. In geval van LRS Hallo zou Hallo replica's worden verdeeld over verschillende datacenters Hallo waaruit een Azure-regio.

Meer informatie vindt u [hier][storage-redundancy].

> [!NOTE]
> Voor implementaties van DBMS, wordt niet Hallo gebruik van geografisch redundante opslag aanbevolen
>
> Azure Storage-Geo-replicatie is asynchroon. Replicatie van afzonderlijke virtuele harde schijven gekoppeld tooa één virtuele machine zijn niet gesynchroniseerd in de stap vergrendelen. Het is daarom niet geschikte tooreplicate DBMS bestanden die worden verdeeld over verschillende virtuele harde schijven of geïmplementeerd op basis van een software-RAID, op basis van meerdere VHD's. DBMS software vereist dat de permanente schijfopslag Hallo nauwkeurig worden gesynchroniseerd binnen andere LUN's en onderliggende schijven/VHD's / aandrijfassen. DBMS software maakt gebruik van verschillende mechanismen toosequence i/o-schrijfactiviteiten en een DBMS rapporteert dat Hallo schijfopslag gericht door Hallo replicatie als deze zelfs door enkele milliseconden verschillen is beschadigd. Als een echt een databaseconfiguratie met een database die over meerdere VHD's geogerepliceerde uitgerekt wil, moet deze replicatie daarom toobe uitgevoerd betekent dat de database en functionaliteit worden benut. Een verstandig niet Azure Storage-Geo-replicatie tooperform deze taak.
>
> Hallo probleem is de eenvoudigste tooexplain met een voorbeeld-systeem. Stel dat u hebt een SAP-systeem dat is geüpload naar Azure met 8 VHD's met gegevensbestanden Hallo DBMS plus een VHD met Hallo transactielogbestand. Elk criterium van deze 9 VHD's hebben gegevens toothem geschreven in een consistente methode toohello DBMS, volgens of Hallo gegevens toohello gegevens of transacties logboekbestanden wordt geschreven.
>
> In volgorde tooproperly geo-replicatie Hallo van gegevens en onderhouden van een kopie van de database consistent, Hallo inhoud van alle negen VHD's zou hebben toobe geogerepliceerde in Hallo exacte volgorde Hallo i/o-bewerkingen zijn uitgevoerd tegen Hallo negen verschillende VHD's. Azure Storage geo-replicatie kunnen echter niet toodeclare afhankelijkheden tussen de virtuele harde schijven. Dit betekent dat Microsoft Azure Storage geo-replicatie niet kent Hallo fact dat Hallo inhoud in deze negen verschillende VHD's zijn andere gerelateerde tooeach en Hallo gegevenswijzigingen zijn consistent alleen bij het repliceren in Hallo Hallo i/o-bewerkingen hebben plaatsgevonden voor alle Hallo 9 VHD's.
>
> Naast de kans op hoog dat Hallo geogerepliceerde afbeeldingen in Hallo scenario bieden geen een consistente database-installatiekopie, is er een prestatiestraf die wordt weergegeven met geografisch redundante opslag die ernstige problemen kunnen ook worden de prestaties beïnvloeden. In de samenvatting van gebruik geen dit soort redundantie van gegevensopslag voor DBMS type werkbelastingen.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>VHD's wilt toewijzen aan virtuele Machine van Azure Service Storage-Accounts
Een Azure Storage-Account is niet alleen een administratieve constructie, maar ook een onderwerp van beperkingen. Terwijl Hallo beperkingen of we over een standaard Azure-Opslagaccount of een Azure Premium Storage-Account hebben verschillen. Hallo exacte mogelijkheden en beperkingen worden vermeld [hier][storage-scalability-targets]

Dus voor Azure Standard-opslag is het belangrijk toonote er geldt een limiet op Hallo IOP's per storage-account ('Totale snelheid van aanvragen voor' die rij [Hallo artikel][storage-scalability-targets]). Bovendien is er een initiële limiet van 100 Opslagaccounts per Azure-abonnement (van juli 2015). Daarom wordt aanbevolen toobalance IOP's van VM's tussen meerdere opslagaccounts bij gebruik van Azure Standard-opslag. Terwijl een enkele virtuele machine in het ideale geval één opslagaccount indien mogelijk gebruikt. Als we over DBMS implementaties waarbij elke VHD die wordt gehost op Azure Standard-opslag de quotalimiet bereiken hebben kan, moet u dus alleen 30 tot 40 VHD's per Azure-Opslagaccount die gebruikmaakt van Azure Standard-opslag implementeren. Op Hallo anderzijds, als u gebruikmaken van Azure Premium-opslag en toostore database grote volumes, wilt u mogelijk fijn in termen van IOPS. Maar er is een Azure Premium Storage-Account manier meer beperkende in gegevensvolume dan een standaard Azure-Opslagaccount. Als gevolg hiervan kunt u slechts een beperkt aantal VHD's binnen een Azure Premium Storage-Account implementeren voordat roept Hallo-limiet voor het volume van gegevens. Op Hallo vergelijken met het einde van een Azure Storage-Account als een 'virtuele SAN' die beperkte mogelijkheden in IOPS en/of capaciteit heeft. Als gevolg hiervan blijft Hallo taak, zoals in on-premises implementaties, toodefine Hallo lay-out van Hallo VHD's van verschillende SAP systemen via Hallo verschillende 'denkbeeldige SAN-apparaten' hello of een Azure Storage-Accounts.

Eén VM indien mogelijk voor Azure Standard-opslag niet is raadzaam andere opslag accounts tooa toopresent-opslag.

Terwijl met Hallo DS- of GS-serie van Azure VM's is het mogelijk toomount VHD's uit de Azure Storage-Accounts en Premium Storage-Accounts. Gebruiksvoorbeelden zoals back-ups geschreven naar de Standard-opslag ondersteund VHD's dat DBMS gegevens en logboekbestanden op de Premium-opslag komen toomind waar deze heterogene opslag kan worden gebruikt.

Op basis van implementaties van klanten en het testen ongeveer 30 too40 VHD's met de gegevensbestanden van de database en logboekbestanden kunnen worden ingericht op een enkele Azure Standard-Opslagaccount met acceptabele prestaties. Zoals eerder vermeld, wordt Hallo beperking van een Azure Premium Storage-Account is waarschijnlijk toobe Hallo gegevenscapaciteit die kan bevatten en niet IOPS.

Zoals met SAN-apparaten on-premises, delen, moet bepaalde bewakingsfuncties in volgorde tooeventually detecteren knelpunten in een Azure Storage-Account. Hello Azure extensie Monitoring voor SAP en hello Azure-Portal zijn hulpprogramma's die kunnen worden gebruikt toodetect bezette Azure Storage-Accounts die van suboptimale i/o-prestaties leveren kunnen.  Als deze situatie wordt gedetecteerd dat het wordt aanbevolen toomove bezet VMs tooanother Azure Storage-Account. Raadpleeg toohello [Deployment Guide] [ deployment-guide] voor meer informatie over hoe tooactivate Hallo SAP bewakingsmogelijkheden hosten.

Een ander artikel samenvatten aanbevolen procedures om Azure Standard-opslag- en Azure Storage-Accounts vindt u hier <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>DBMS virtuele machines van Azure Standard-opslag tooAzure Premium-opslag verplaatsen geïmplementeerd
We er wel een aantal scenario's waar u als klant toomove een geïmplementeerde virtuele machine van Azure Standard-opslag naar Azure Premium-opslag optreden. Dit is niet mogelijk zonder Hallo gegevens fysiek worden verplaatst. Er zijn verschillende manieren tooachieve Hallo doel:

* Alle VHD's, basis-VHD, evenals gegevens VHD's kan u gewoon kopiëren naar een nieuwe Azure Premium Storage-Account. Vaak u hebt gekozen Hallo aantal VHD's in Azure Standard-opslag niet vanwege Hallo feit dat u Hallo gegevensvolume nodig. Maar u zoveel VHD's vanwege Hallo IOP's nodig. Nu dat u tooAzure Premium-opslag kan naartoe manier verplaatsen Hallo minder tooachieve VHD's sommige IOPS-doorvoer. Hallo feit dat in Azure Standard-opslag u voor Hallo betaalt gegevens en niet de grootte van Hallo-nominaal schijf gebruikt gezien, Hallo aantal VHD's niet echt van belang in termen van kosten. Echter, met Azure Premium Storage zou betaalt u voor Hallo nominaal schijfgrootte. De meeste van de klant Hallo Probeer daarom tookeep Hallo aantal Azure VHD's in Premium-opslag op Hallo aantal benodigde tooachieve hello IOPS doorvoer nodig. Dus besluiten de meeste klanten tegen Hallo manier van een eenvoudige 1:1 exemplaar.
* Als u nog niet is gekoppeld, kunt u een één-VHD met een databaseback-up van uw SAP-database koppelen. Na de back-up hello, ontkoppelen van alle VHD's, met inbegrip van Hallo VHD met Hallo back-up en kopiëren Hallo basis-VHD en Hallo VHD met Hallo back-up naar een Azure Premium Storage-account. Vervolgens zou implementeert u Hallo die VM op basis van Hallo base VHD en koppelpunten Hallo VHD met Hallo back-up. Nu maken u extra leeg Premium Storage schijven voor Hallo VM die zijn gebruikt toorestore Hallo database in. Hierbij wordt ervan uitgegaan dat Hallo DBMS kunt u toochange paden toohello gegevens en logboekbestanden bestanden als onderdeel van het herstelproces Hallo.
* Een andere mogelijkheid is een variatie van Hallo voormalige proces, waarin u alleen back-up Hallo VHD kopiëren naar Azure Premium-opslag en koppelt u dit op basis van een virtuele machine die u zojuist hebt geïmplementeerd en geïnstalleerd.
* Hallo vierde mogelijkheid kiest u wanneer u nodig toochange Hallo aantal gegevensbestanden van de database bent. In dat geval voert u een SAP homogene system kopie export/import te gebruiken. Plaats de bestanden exporteren naar een VHD die wordt gekopieerd naar een Azure Premium Storage-Account en koppelt u dit tooa VM toorun Hallo importeren processen te gebruiken. Klanten gebruiken deze mogelijkheid, vooral wanneer hij of zij wil toodecrease Hallo aantal gegevensbestanden.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Implementatie van virtuele machines voor SAP in Azure
Microsoft Azure biedt verschillende manieren toodeploy virtuele machines en gekoppelde schijven. Het is daardoor erg belangrijk toounderstand Hallo verschillen aangezien voorbereidingen van virtuele machines Hallo afhankelijk van Hallo manier van implementatie verschillen. In het algemeen kijken we naar Hallo scenario's beschreven in de volgende hoofdstukken Hallo.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Een virtuele machine uit Azure Marketplace Hallo implementeren
U tootake een door Microsoft, zoals of 3e partij verstrekt de installatiekopie van hello Azure Marketplace toodeploy uw virtuele machine. Nadat u uw virtuele machine in Azure hebt geïmplementeerd, volgt u Hallo dezelfde richtlijnen en hulpprogramma's voor tooinstall Hallo SAP-software in uw virtuele machine zoals u in een on-premises omgeving doen zou. Voor het installeren van Hallo SAP-software in hello Azure VM SAP en Microsoft tooupload raden en sla Hallo SAP-installatiemedia in Azure virtuele harde schijven of toocreate een Azure VM werkt als een 'bestandsserver' waarin alle benodigde SAP Hallo-installatiemedia.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Een virtuele machine met een klant een specifieke algemene installatiekopie implementeren
Vervaldatum toospecific patch vereisten in groet tooyour OS of DBMS-versie, mogelijk Hallo opgegeven afbeeldingen in hello Azure Marketplace niet aansluiten bij uw behoeften. Daarom moet u mogelijk toocreate een VM die gebruikmaakt van uw eigen 'persoonlijke' OS/DBMS VM-installatiekopie die verschillende keren daarna kan worden geïmplementeerd. een 'persoonlijke' installatiekopie voor duplicatie tooprepare, OS op Hallo gegeneraliseerde Hallo lokale VM. Raadpleeg toohello [Deployment Guide] [ deployment-guide] voor meer informatie over het toogeneralize een virtuele machine.

Als u al SAP-inhoud in uw lokale virtuele machine (vooral voor laag 2-systemen) hebt geïnstalleerd, kunt u Hallo SAP-systeeminstellingen aanpassen nadat het Hallo-implementatie van hello Azure VM via Hallo instantie naam van procedure ondersteund door Hallo SAP softwarelevering Manager (SAP-notitie [1619720]). U kunt anders Hallo SAP-software installeren nadat Hallo-implementatie van hello Azure VM.

Vanaf Hallo database inhoud die wordt gebruikt door Hallo SAP-toepassing, kunt u ofwel genereren Hallo inhoud opnieuw worden door een SAP-installatie of u kunt uw inhoud in Azure importeren met behulp van een VHD met een DBMS databaseback-up of door gebruik te maken van de mogelijkheden van Hallo DBMS toodirectly back-up in Microsoft Azure Storage. U kunt in dit geval wordt voorbereid op VHD's met Hallo DBMS gegevens en bestanden lokaal aanmelden en die als schijven vervolgens importeren in Azure. Maar Hallo overdracht van gegevens op DBMS die wordt geladen vanaf de lokale tooAzure zou werken via de VHD-schijven die toobe lokale voorbereid moeten.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Verplaatsen van een virtuele machine van de lokale tooAzure met een niet-gegeneraliseerd schijf
U van plan bent toomove een specifiek systeem SAP van lokale tooAzure (lift en shift). Dit kan worden gedaan door Hallo VHD waarin Hallo OS uploaden, Hallo SAP binaire bestanden en binaire bestanden voor uiteindelijke DBMS plus Hallo VHD's met de gegevens en logboekbestanden bestanden Hallo van Hallo DBMS tooAzure. In tegenover tooscenario #2 hierboven, houden u Hallo hostnaam, SAP-SID en SAP-gebruikersaccounts hello Azure VM zoals ze zijn geconfigureerd in Hallo on-premises omgeving. Hallo installatiekopie generaliseren is daarom niet nodig. In dit geval wordt voornamelijk toegepast voor Cross-Premises-scenario's waar een deel van Hallo SAP liggend on-premises en onderdelen wordt uitgevoerd op Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Hoge beschikbaarheid en herstel na noodgevallen met virtuele machines in Azure
Azure biedt Hallo na functionaliteiten voor hoge beschikbaarheid en herstel na noodgeval (DR) die van toepassing zijn toodifferent onderdelen die we voor SAP en DBMS-implementaties gebruiken zou

### <a name="vms-deployed-on-azure-nodes"></a>Virtuele machines die worden geïmplementeerd op Azure knooppunten
Hello Azure-Platform biedt geen functies, zoals livemigratie voor geïmplementeerde virtuele machines. Dit betekent dat als er onderhoud nodig op een cluster waarop een virtuele machine is geïmplementeerd, Hallo VM moet tooget gestopt en opnieuw opgestart. Onderhoud in Azure wordt uitgevoerd met behulp van zogenaamde domeinen upgraden binnen clusters van servers. Slechts één Upgrade domein tegelijk wordt onderhouden. Tijdens het opnieuw opstarten zal er een onderbreking van de service tijdens het Hallo die VM wordt afgesloten, onderhoud wordt uitgevoerd en VM opnieuw opgestart. De meeste leveranciers van DBMS bieden echter hoge beschikbaarheid en herstel na noodgevallen functionaliteit die snel Hallo DBMS services op een ander knooppunt wordt opnieuw als het primaire knooppunt Hallo niet beschikbaar is. Hello biedt Azure-Platform functionaliteit toodistribute virtuele machines, opslag en andere Azure-services tussen domeinen upgraden tooensure die gepland onderhoud of infrastructuur fouten alleen gevolgen zou hebben voor een kleine subset van de virtuele machines of services.  Met een zorgvuldige planning is het mogelijk tooachieve beschikbaarheid niveaus vergelijkbare tooon-premises infrastructuur.

Beschikbaarheidssets voor Microsoft Azure een logische groepering van virtuele machines of Services die ervoor zorgt dat virtuele machines en andere services zijn gedistribueerde toodifferent veroorzaakt en -domeinen upgraden binnen een cluster zodat er zou niet meer dan één knooppunt wordt uitgeschakeld op enig punt in tijd ( gelezen[dit] [ virtual-machines-manage-availability] artikel voor meer informatie).

Het moet doel geconfigureerd bij het implementeren van virtuele machines, zoals hier toobe:

![Definitie van de Beschikbaarheidsset voor DBMS HA-configuraties][dbms-guide-figure-200]

Als we willen dat de maximaal beschikbare configuraties toocreate DBMS-implementaties (onafhankelijk van de Hallo afzonderlijke DBMS HA-functionaliteit gebruikt), moet Hallo DBMS VMs aan:

* Hallo VMs toohello toevoegen hetzelfde virtuele Azure-netwerk (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Hallo virtuele machines van de HA-configuratie Hallo in Hallo moet hetzelfde subnet. Naamomzetting tussen de verschillende subnetten Hallo is niet mogelijk in de Cloud-implementaties, alleen IP-naamomzetting werkt. Met behulp van site-naar-site- of ExpressRoute-verbindingen voor Cross-Premises implementaties, worden een netwerk met ten minste één subnet al vastgesteld. Naamomzetting worden uitgevoerd volgens toohello on-premises AD-beleid en netwerkinfrastructuur.

[comment]: <> (MSSedusch TODO Test indien nog steeds waar in ARM)

#### <a name="ip-addresses"></a>IP-adressen
Het verdient maximaal toosetup hello, virtuele machines voor HA configuraties op een flexibele manier. Vertrouwen op IP-adressen tooaddress Hallo HA partner (s) binnen Hallo HA configuration is niet betrouwbaar in Azure tenzij statische IP-adressen worden gebruikt. Er zijn twee 'Afsluiten' concepten in Azure:

* Via de Azure Portal of Azure PowerShell-cmdlet Stop-AzureRmVM afgesloten: In dit geval Hallo virtuele Machine wordt afgesloten en ongedaan toegewezen. Uw Azure-account wordt niet meer in rekening gebracht voor deze virtuele machine zodat Hallo alleen de kosten, worden voor Hallo opslag gebruikt. Als privé IP-adres van netwerkinterface Hallo Hallo niet statisch is, Hallo IP-adres is vrijgegeven en is er geen garantie dat netwerkinterface Hallo Hallo oude toegewezen IP-adres na een herstart van Hallo VM opnieuw opgehaald. Hallo uitvoeren via Azure Portal Hallo afgesloten of door het aanroepen van Stop-AzureRmVM automatisch, wordt de toewijzing. Als u niet wilt dat toodeallocat Hallo machine Stop-AzureRmVM - StayProvisioned gebruiken
* Als u op Hallo VM van het niveau van een besturingssysteem wordt afgesloten, opgehaald Hallo VM afsluiten en niet ongedaan toegewezen. Echter in dit geval uw Azure-account wordt nog steeds in rekening gebracht voor Hallo VM, ondanks Hallo feit dat deze afgesloten wordt. In dat geval hello toewijzing van Hallo IP-adres tooa gestopte VM blijven behouden. Hallo afgesloten forceert VM van binnen automatisch geen toewijzing ongedaan.

Zelfs voor Cross-Premises-scenario's standaard een afsluiten en de toewijzing ongedaan betekent dat de toewijzing van Hallo IP-adressen uit Hallo VM, zelfs als het lokale beleid in de DHCP-instellingen zijn verschillend.

* Hallo uitzondering wordt als een een statische IP-adres tooa netwerkinterface als wijst beschreven [hier][virtual-networks-reserved-private-ip].
* In dat geval is Hallo IP-adres blijft ongewijzigd, zolang het Hallo-netwerkinterface is niet verwijderd.

> [!IMPORTANT]
> In de volgorde tookeep Hallo hele implementatie eenvoudig en beheerbare Hallo Hallo duidelijk aanbeveling toosetup virtuele machines in een configuratie DBMS HA of DR in Azure op een manier die er is een werkende naamomzetting tussen de verschillende virtuele machines betrokken Hallo samenwerking.
>
>

## <a name="deployment-of-host-monitoring"></a>Implementatie van de Host bewaking
SAP vereist voor productief gebruik van SAP-toepassingen in Azure Virtual Machines Hallo mogelijkheid tooget host bewakingsgegevens van de fysieke hosts Hallo hello Azure Virtual Machines uitgevoerd. Een specifiek niveau van de HostAgent SAP-patch worden waarmee deze mogelijkheid in SAPOSCOL en SAP HostAgent. de exacte patchniveau Hello wordt beschreven in SAP-notitie [1409604].

Raadpleeg voor meer informatie voor een Hallo met betrekking tot implementatie van onderdelen die host gegevens tooSAPOSCOL leveren en levenscyclusbeheer van deze onderdelen SAPHostAgent en hello, toohello [Implementatiehandleiding][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Specificaties tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>SQL Server IaaS
Beginnen met Microsoft Azure, kunt u gemakkelijk migreren uw bestaande SQL Server-toepassingen dat is gebaseerd op Windows Server-platform tooAzure virtuele Machines. SQL Server in een virtuele Machine kunt u tooreduce Hallo totale eigendomskosten van implementatie, beheer en onderhoud van de breedte van bedrijfstoepassingen door eenvoudig deze toepassingen tooMicrosoft Azure te migreren. Met SQL Server in een virtuele Machine van Azure, beheerders en ontwikkelaars kunnen nog steeds gebruiken Hallo dezelfde ontwikkelings- en hulpprogramma's die beschikbaar zijn op lokale.

> [!IMPORTANT]
> Opmerking: we niet bespreekt Microsoft Azure SQL Database die een Platform als een Service-aanbieding Hallo Microsoft Azure-Platform is. Hallo discussie in dit artikel is over het uitvoeren van SQL Server-product Hallo zoals bekend voor on-premises implementaties in Azure Virtual Machines, inzetten Hallo infrastructuur als de mogelijkheid van een Service van Azure. Database-mogelijkheden en functies tussen deze twee aanbiedingen zijn verschillend en moeten niet wordt verward met elkaar. Zie ook: <https://azure.microsoft.com/services/sql-database/>
>
>

Het is raadzaam tooreview [dit] [ virtual-machines-sql-server-infrastructure-services] documentatie voordat u doorgaat.

In Hallo wordt volgende secties stukjes delen van Hallo documentatie onder Hallo koppeling hierboven geaggregeerd en vermeld. Specificaties rond SAP worden ook vermeld en enkele concepten die worden beschreven in meer detail. Echter, het is raadzaam toowork door Hallo documentatie boven eerste voordat het lezen van de specifieke documentatie bij Hallo SQL Server.

Er is een aantal SQL-Server in IaaS specifieke informatie die u voordat u verdergaat weten moet:

* **Virtuele Machine SLA**: Er is een SLA voor virtuele Machines worden uitgevoerd in Azure die u kunt hier vinden: <https://azure.microsoft.com/support/legal/sla/>  
* **Ondersteuning voor SQL-versie**: voor SAP-klanten we ondersteuning voor de SQL Server 2008 R2 en hoger op Microsoft Azure virtuele Machine. Eerdere versies worden niet ondersteund. Bekijk deze algemene [ondersteuningsverklaring](https://support.microsoft.com/kb/956893) voor meer informatie. Houd er rekening mee dat in het algemeen SQL Server 2008 wordt ondersteund door Microsoft ook. SQL Server 2008 R2 is echter vanwege toosignificant functionaliteit voor SAP dat werd geïntroduceerd in SQL Server 2008 R2, minimale versie van de Hallo voor SAP. Houd er rekening mee dat SQL Server 2012 en 2014 hebt uitgebreid diepgaande integratie met Hallo IaaS-scenario (zoals back-ups van rechtstreeks met Azure Storage). Daarom wordt deze papier tooSQL Server 2012 en 2014 met de meest recente patchniveau beperken voor Azure.
* **Ondersteuning voor SQL-functie**: meest SQL Server-functies in Microsoft Azure Virtual Machines met enkele uitzonderingen worden ondersteund. **SQL Server Failover Clustering met gedeelde schijven wordt niet ondersteund**.  Gedistribueerd technologieën zoals databasespiegeling, AlwaysOn-beschikbaarheidsgroepen, replicatie, logboekverzending en Service Broker worden ondersteund in één Azure-regio. SQL Server AlwaysOn ook wordt ondersteund tussen verschillende Azure-regio's zoals hier wordt beschreven: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Bekijk Hallo [ondersteuningsverklaring](https://support.microsoft.com/kb/956893) voor meer informatie. Een voorbeeld van hoe toodeploy een AlwaysOn-configuratie wordt weergegeven in [dit] [ virtual-machines-workload-template-sql-alwayson] artikel. Bekijk ook Hallo aanbevolen procedures beschreven [hier][virtual-machines-sql-server-infrastructure-services]
* **SQL-prestaties**: We zijn ervan overtuigd dat Microsoft Azure gehoste virtuele Machines zeer goed wordt uitgevoerd in vergelijking tooother openbare cloud virtualization aanbiedingen, maar de afzonderlijke resultaten kan verschillen. Bekijk [dit] [ virtual-machines-sql-server-performance-best-practices] artikel.
* **Met behulp van installatiekopieën uit Azure Marketplace**: Hallo snelste manier toodeploy een nieuw Microsoft Azure VM is toouse een installatiekopie van hello Azure Marketplace. Er zijn afbeeldingen in hello Azure Marketplace waarin SQL Server. Hallo-installatiekopieën waarop SQL Server al is geïnstalleerd worden niet onmiddellijk gebruikt voor SAP NetWeaver toepassingen. Hallo reden is Hallo standaard SQL Server-sortering in deze installatiekopieën en niet Hallo sortering is vereist voor SAP NetWeaver systemen is geïnstalleerd. In order toouse dergelijke afbeeldingen, Controleer Hallo stappen die zijn beschreven in hoofdstuk [afbeeldingen met behulp van een SQL-Server buiten de Microsoft Azure Marketplace Hallo][dbms-guide-5.6].
* Bekijk [prijsinformatie](https://azure.microsoft.com/pricing/) voor meer informatie. Hallo [SQL Server 2012-licentieverlening Guide](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) en [SQL Server 2014 licentieverlening Guide](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) zijn ook een belangrijke bron.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>SQL Server-configuratie-instructies voor SAP gerelateerde SQL Server-installaties in Azure VM 's
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Aanbevelingen voor VM/VHD-structuur voor SAP gerelateerde implementaties van SQL Server
Hallo algemene beschrijving, in overeenstemming met uitvoerbare programma's van SQL Server moet zich bevinden of in Hallo systeemstation van de basis-VHD Hallo van de virtuele machine is geïnstalleerd (station C:\).  Normaal gesproken worden de meeste van SQL Server-systeemdatabases hello gebruikt op een hoog niveau door SAP NetWeaver werkbelasting. Daarom kunnen Hallo systeemdatabases van SQL Server (master, msdb en model) blijven op Hallo ook station C:\. Een uitzondering tempdb die in geval van sommige ERP SAP en alle BW werkbelastingen Hallo hoger gegevensvolume of i/o-bewerkingen volume dat niet in Hallo past vereist kan zijn oorspronkelijke VM. Voor dergelijke systemen moet Hallo stappen te volgen worden uitgevoerd:

* Hallo primaire tempdb gegevens bestand(en) toohello verplaatsen dezelfde logisch station als primaire gegevensbestand(en) Hallo van Hallo SAP-database.
* Eventuele extra tempdb gegevens bestanden tooeach Hallo andere logische stations met een gegevensbestand van database Hallo SAP-gebruiker toevoegen.
* Hallo tempdb logfile toohello logisch station waarin het logboekbestand van database Hallo-gebruiker toevoegen.
* **Uitsluitend bedoeld is voor VM-typen die gebruikmaken van de lokale SSD's** op Hallo compute knooppunt tempdb gegevens en logboekbestanden bestanden op station D:\ Hallo kunnen worden geplaatst. Evenwel kan het zijn aanbevolen toouse meerdere tempdb-gegevensbestanden. Let D:\ stationsvolumes zijn verschillend op basis van Hallo VM-type.

Deze configuraties inschakelen tempdb tooconsume meer ruimte dan Hallo systeemstation kunnen tooprovide is. Een kunt Hallo tempdb grootten op bestaande systemen die on-premises uitgevoerd controleren in volgorde toodetermine Hallo juiste tempdb grootte. Een dergelijke configuratie zou bovendien IOPS getallen op basis van tempdb die kan niet worden voorzien van het systeemstation Hallo inschakelen. Systemen met lokale mag opnieuw gebruikte toomonitor i/o-werkbelasting tegen tempdb zodat u Hallo IOPS cijfers u toosee verwacht op uw tempdb kunt afleiden.

Een VM-configuratie die SQL Server wordt uitgevoerd met een SAP-database en waar tempdb-gegevens en tempdb logboekbestand worden geplaatst op Hallo D:\ station eruit als:

![Verwijzing configuratie van Azure IaaS VM voor SAP][dbms-guide-figure-300]

Let erop dat Hallo station D:\ Hallo VM-type is afhankelijk van verschillende grootte heeft. Afhankelijk van de vereiste voor Hallo-grootte van tempdb mogelijk geforceerd toopair tempdb gegevens en logboekbestanden Hello SAP-databasegegevens en logboekbestanden in gevallen waarbij D:\ station te klein is.

#### <a name="formatting-hello-vhds"></a>Opmaak Hallo VHD 's
Voor SQL Server-Hallo NTFS blokgrootte voor virtuele harde schijven met SQL Server-gegevens en logboekbestanden zich bestanden 64 kB. Er is geen noodzaak tooformat hello D:\ station. Dit station komt vooraf ingestelde.

In de volgorde toomake zorgen dat hello terugzetten of maken van databases wordt niet geïnitialiseerd Hallo gegevensbestanden worden opgeslagen door zeroing Hallo inhoud van het Hallo-bestanden, een moet ervoor zorgen heeft dat Hallo gebruiker context Hallo SQL Server-service wordt uitgevoerd in een bepaalde machtiging. Gebruikers in Windows-beheerdersgroep Hallo hebben meestal deze machtigingen. Als Hallo SQL Server-service wordt uitgevoerd in de context van de gebruiker Hallo van niet - Windows-beheerder, moet u tooassign die gebruiker Hallo gebruikersrecht uitvoeren volumeonderhoudstaken.  Hallo-informatie in dit Microsoft Knowledge Base-artikel: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Gevolgen van het database-compressie
In configuraties waar i/o-bandbreedte kan een beperkende factor, kan elke meting waardoor IOPS toostretch Hallo werkbelasting een in een IaaS-scenario zoals Azure uitvoeren kunt helpen. Daarom als u nog niet doet, wordt toepassen van de pagina met SQL Server-compressie sterk aanbevolen door Microsoft en SAP voordat het uploaden van een bestaande SAP tooAzure-databases.

Hallo aanbeveling tooperform compressie van de Database voordat u uploadt tooAzure wordt gegeven buiten twee redenen:

* Hallo hoeveelheid gegevens toobe geüpload is lager.
* Hallo duur van Hallo compressie uitvoering is korter, ervan uitgaande dat sterkere hardware kunnen worden gebruikt met meer CPU's of hogere i/o-bandbreedte of minder i/o-latentie lokale.
* Kleinere database kunnen leiden tot tooless kosten voor schijftoewijzing

Database-compressie werkt ook in een Azure Virtual Machines als lokale. Voor meer informatie over hoe een bestaande SAP SQL Server-database toocompress Controleer hier: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014: opslaan van bestanden op Azure-Blog databaseopslag
SQL Server 2014 Hallo mogelijkheid toostore databasebestanden rechtstreeks in Azure Blob-Store zonder Hallo 'wrapper' van een VHD omheen geopend. Hierdoor kunnen scenario's waarbij u Hallo grenzen van de IOPS op dat zou worden afgedwongen door een beperkt aantal virtuele harde schijven die gekoppeld toosome kleinere VM-typen zijn kan ondervangen vooral met het gebruik van standaard Azure Storage of kleinere VM-typen. Dit werkt voor gebruikersdatabases maar niet voor systeemdatabases van SQL Server. Dit werkt voor gegevens en logboekbestanden van SQL Server. Als u wilt toodeploy een SAP SQL Server-database op deze manier in plaats van 'wrapping' deze in de VHD's, houd Hallo volgende in gedachten:

* Hallo Storage-Account gebruikt behoeften toobe in Hallo hetzelfde Azure-gebied als Hallo een gebruikte toodeploy Hallo VM SQL Server wordt uitgevoerd in.
* Overwegingen die eerder in groet toodistribute VHD's via andere Azure Storage-Accounts voor deze implementaties ook van toepassing. Betekent Hallo i/o-bewerkingen, tellen mee voor Hallo grenzen van hello Azure Storage-Account.

[comment]: <> (MSSedusch TODO, maar dit gebruikt netwerkbandbreedte en niet-opslag bandbreedte, het?)

Meer informatie over dit type implementatie worden hier vermeld: <https://msdn.microsoft.com/library/dn385720.aspx>

In de volgorde toostore SQL Server-gegevensbestanden rechtstreeks op Azure Premium-opslag, moet u een minimale versie van SQL Server 2014 toohave patch release die hier wordt beschreven: <https://support.microsoft.com/kb/3063054>. Opslaan van SQL Server-gegevensbestanden op Azure Standard-opslag werkt in combinatie met Hallo vrijgegeven versie van SQL Server 2014. Hallo diezelfde patches bevat echter een andere reeks correcties waardoor Hallo rechtstreeks gebruik van Azure Blob-opslag voor SQL Server-gegevensbestanden en back-ups betrouwbaarder. Daarom raadzaam toouse deze patches in het algemeen.

### <a name="sql-server-2014-buffer-pool-extension"></a>De Buffergroepuitbreiding van SQL Server 2014
SQL Server 2014 geïntroduceerd om een nieuwe functie die de Buffergroepuitbreiding wordt genoemd. Deze functionaliteit breidt de buffergroep Hallo van SQL Server die wordt opgeslagen in het geheugen met een tweede niveau cache dat wordt ondersteund door de lokale SSD's van een server of de virtuele machine. Hierdoor tookeep een grotere werkset van gegevens 'in het geheugen'. Vergeleken tooaccessing Azure Standard-opslag Hallo toegang tot Hallo uitbreiding van de buffergroep Hallo die is opgeslagen op de lokale SSD's van een Azure VM is sneller veel factoren.  Gebruik van lokale D:\ schijf Hallo Hallo VM typen waarvoor uitstekende IOPS en doorvoerlimieten kan dus een zeer redelijke manier tooreduce Hallo IOP's laden met Azure Storage en de reactietijd van query's aanzienlijk verbeteren. Dit geldt met name wanneer u geen Premium-opslag. In geval van een Premium-opslag en het Hallo-gebruik van Hallo Premium Azure lezen Cache op Hallo rekenknooppunt, zoals aanbevolen voor gegevensbestanden, worden geen grote verschillen verwacht. Reden is dat beide caches (SQL Server-Buffergroepuitbreiding en Premium-opslag lezen Cache) Hallo lokale schijven van de rekenknooppunten Hallo gebruikt.
Controleer voor meer informatie over deze functionaliteit in deze documentatie: <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>Overwegingen voor back-up/herstel voor SQL Server
Uw back-upmethode moet worden gecontroleerd bij het implementeren van SQL Server in Azure. Zelfs als het Hallo-systeem is niet een productieve systeem, Hallo SAP-database gehost door SQL Server moet een back-up regelmatig. Omdat Azure Storage drie afbeeldingen houdt, is nu een back-up minder belangrijke toocompensating ten opzichte van een crash van de opslag. Hallo prioriteit reden voor het onderhouden van een juiste back-up en herstel plan is meer die u logische/handmatige fouten compenseren kunt door punt in tijd herstelfuncties te bieden. Zodat het Hallo-doel is tooeither gebruik back-ups toorestore Hallo database terug tooa bepaalde punt in tijd of toouse Hallo back-ups in Azure tooseed een ander systeem Hallo bestaande database kopiëren. Bijvoorbeeld, u kan overzetten van een 2-Tier SAP configuratie tooa 3-Laagse setup van system Hallo dezelfde systeem door het herstellen van een back-up.

Er zijn drie verschillende manieren toobackup SQL Server tooAzure opslag:

1. SQL Server 2012 CU4 en hoger kan systeemeigen back-databases tooa URL. Dit wordt beschreven in de blog Hallo [nieuwe functionaliteit in SQL Server 2014 – deel 5: Backup/Restore verbeteringen](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Zie hoofdstuk [SQL Server 2012 SP1 CU4 of hoger][dbms-guide-5.5.1].
2. Eerdere tooSQL voor de versies van SQL Server 2012 CU4 toegang tot een omleiding functionaliteit toobackup tooa VHD en in feite Hallo schrijfstroom verplaatsen naar een locatie voor de Azure-opslag die is geconfigureerd. Zie hoofdstuk [SQL Server 2012 SP1 CU3 en eerdere versies][dbms-guide-5.5.2].
3. de laatste methode Hallo is tooperform een conventionele SQL Server-back-toodisk opdracht naar een VHD-schijfstation.  Dit is identiek toohello lokale implementatie patroon en niet wordt uitgebreid beschreven in dit document.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 of hoger
Deze functie kunt u toodirectly back-tooAzure BLOB-opslag. Zonder deze methode, moet u de back-up tooother Azure VHD's die VHD- en IOPS capaciteit zou gebruiken. Hallo idee is in feite dit:

 ![Met behulp van back-up van SQL Server 2012 tooMicrosoft Azure Storage-BLOB][dbms-guide-figure-400]

Hallo-voordeel wordt in dit geval is dat een toospend VHD's toostore SQL Server-back-ups niet hoeft op. Zo hebt u minder VHD's die zijn toegewezen en Hallo hele bandbreedte van VHD IOPS kan worden gebruikt voor gegevens en logboekbestanden. Houd er rekening mee dat Hallo maximale grootte van een back-up beperkt tooa maximaal 1 TB is, zoals beschreven in Hallo sectie 'Beperkingen' in dit artikel: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Als Hallo back-up, ondanks het gebruik van SQL Server-back-compressie zou groter zijn dan 1 TB groot, Hallo functionaliteit die worden beschreven in hoofdstuk [SQL Server 2012 SP1 CU3 en eerdere versies] [ dbms-guide-5.5.2] moet in dit document toobe gebruikt.

[Verwante documentatie](https://msdn.microsoft.com/library/dn449492.aspx) niet toorestore rechtstreeks uit Azure BLOB-archief Hallo terugzetten van de databases van back-ups tegen Azure Blob-opslag met een beschrijving van het beste als back-ups Hallo > 25 GB. Hallo aanbeveling in dit artikel is gewoon gebaseerd op de prestatie-overwegingen en niet vervallen toofunctional beperkingen. Daarom kunnen verschillende voorwaarden van toepassing op basis van geval tot geval.

Documentatie over hoe dit type back-up is ingesteld en gebruikt kan worden gevonden in [dit](https://msdn.microsoft.com/library/dn466438.aspx) zelfstudie

Een voorbeeld van een reeks stappen Hallo kan worden gelezen [hier](https://msdn.microsoft.com/library/dn435916.aspx).

Automatisering van back-ups, is het van hoogste belang toomake ervoor dat de naam van de BLOBs Hallo voor elke back-up anders. Anders wordt deze overschreven en Hallo restore-keten is verbroken.

In order niet toomix spullen tussen verschillende soorten back-ups Hallo 3 is het raadzaam toocreate verschillende containers onder Hallo storage-account gebruikt voor back-ups. Hallo containers kunnen alleen door virtuele machine zijn of op virtuele machine en back-up-type. Hallo schema kan eruitzien als:

 ![Met behulp van back-up van SQL Server 2012 tooMicrosoft Azure Storage-BLOB – verschillende containers onder afzonderlijke Storage-Account][dbms-guide-figure-500]

In voorbeeld van de Hallo hierboven Hallo back-ups niet wordt uitgevoerd in dezelfde opslag account waar Hallo Hallo zijn virtuele machines geïmplementeerd. Er is een nieuw opslagaccount, speciaal voor Hallo back-ups. Binnen Hallo storage-accounts, zou er verschillende containers die zijn gemaakt met een matrix van het type Hallo van back-up en Hallo VM-naam. Dergelijke segmentering maken het gemakkelijker tooadministrate Hallo back-ups van Hallo andere virtuele machines.

Hallo BLOBs een rechtstreeks Hallo back-ups, schrijft toevoegt toohello aantal Hallo VHD's van een virtuele machine niet. Daarom kan een Hallo maximum van VHD's van Hallo specifieke VM SKU voor Hallo gegevens gekoppeld maximaliseren en transactie logboekbestand en een back-up op basis van een opslagcontainer nog steeds uitvoeren.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 en eerdere versies
Hallo van de eerste stap moet u een back-up rechtstreeks met Azure Storage in volgorde tooachieve uitvoeren zou worden toodownload Hallo msi die is gekoppeld te[dit](https://www.microsoft.com/download/details.aspx?id=40740) KBA artikel.

Hallo x64-installatiebestand en Hallo documentatie downloaden. Hallo-bestand installeert een programma met de naam: Microsoft SQL Server back-up tooMicrosoft Azure-hulpprogramma. Lees zorgvuldig Hallo-documentatie van Hallo product.  Hallo hulpprogramma werkt in feite in Hallo volgende manieren:

* Van SQL Server-side hello, de locatie van een schijf voor SQL Server back-up Hallo is gedefinieerd (Hallo D:\ station niet gebruiken voor deze).
* Hallo-hulpprogramma kunt u toodefine regels die gebruikt toodirect verschillende typen back-ups toodifferent Azure Storage-containers worden kunnen.
* Zodra het Hallo-regels zijn gemaakt, omleidt Hallo hulpprogramma Hallo schrijfstroom van back-tooone Hallo van Hallo VHD's / schijven toohello locatie voor de Azure-opslag die eerder is gedefinieerd.
* Hallo hulpprogramma laat een kleine stub-bestand met een grootte van een paar KB op Hallo VHD/schijf die is gedefinieerd voor Hallo SQL Server back-up. **Dit bestand moet worden links op Hallo-opslaglocatie, omdat het vereiste toorestore opnieuw uit Azure Storage.**
  * Als u kwijt Hallo stub-bestand (bijvoorbeeld via verlies van opslagmedia Hallo die Hallo stub-bestand opgenomen) en u ervoor Hallo-optie gekozen hebt van een back-up tooa Microsoft Azure Storage-account, herstellen u Hallo stub-bestand via Microsoft Azure Storage door downloaden van de opslagcontainer Hallo waarin deze is geplaatst. U moet vervolgens Hallo stubbestand plaatsen in een map op de lokale machine Hallo waarbij Hallo hulpprogramma geconfigureerde toodetect en uploaden toohello dezelfde container Hello dezelfde Versleutelingswachtwoord als versleuteling is gebruikt met de oorspronkelijke regel Hallo.

Dit betekent dat Hallo schema zoals hierboven beschreven voor een meer recente versies van SQL Server kan worden ingevoerd en voor SQL Server-versies die zijn niet toestaan direct adres een Azure-opslaglocatie.

Deze methode mag niet worden gebruikt bij een meer recente versies van SQL Server die back-ups maken van systeemeigen ondersteuning voor Azure Storage. Uitzonderingen zijn waar beperkingen van Hallo systeemeigen back-up naar Azure blokkeren het systeemeigen back-up kan worden uitgevoerd in Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Andere mogelijkheden toobackup SQL Server-databases
Andere mogelijkheden toobackup databases is tooattach extra virtuele harde schijven tooa VM die u voor toostore back-ups. In dat geval moet u toomake zeker weet dat Hallo VHD's worden niet uitgevoerd volledig. Als dit Hallo geval is, moet u toounmount Hallo VHD en dus toospeak deze ' archiveren en vervang deze door een nieuwe lege VHD. Als u falen dat pad beide, kunt u tookeep deze VHD's in afzonderlijke Azure Storage-Accounts van Hallo die in de VHD's met de databasebestanden Hallo Hallo.

Een tweede mogelijkheid is toouse een grote virtuele machine waarvoor veel virtuele harde schijven die zijn gekoppeld. Bijvoorbeeld D14 met 32VHDs. Gebruik opslagruimten toobuild een flexibele omgeving waarin u kan samenstellen shares die worden vervolgens gebruikt als back-doelen voor Hallo verschillende DBMS-servers.

Enkele aanbevolen procedures zijn gedocumenteerd [hier](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) ook.

#### <a name="performance-considerations-for-backupsrestores"></a>Prestatie-overwegingen voor back-ups/herstelacties
Prestaties van back-up/herstel is net zoals in de bare-metal implementaties, afhankelijk van hoeveel volumes parallel kunnen worden gelezen en welke Hallo doorvoer van deze volumes mogelijk. Bovendien speelt Hallo CPU-verbruik door back-compressie gebruikt een belangrijke rol op virtuele machines met slechts komen too8 CPU threads. Daarom kan een aannemen:

* Hallo minder Hallo aantal virtuele harde schijven gebruikt toostore Hallo gegevensbestanden, Hallo Hallo kleinere totale doorvoer in lezen.
* Hallo kleinere Hallo aantal threads in Hallo VM CPU, Hallo ernstige Hallo gevolgen van het back-compressie.
* Hallo minder doelen (BLOBs of VHD's) toowrite Hallo back-up naar, Hallo minder Hallo doorvoer.
* Hallo kleinere hello VM-grootte, Hallo kleinere Hallo doorvoer opslaglimiet schrijven en te lezen van Azure Storage. Onafhankelijk van of Hallo back-ups rechtstreeks op Azure Blob zijn opgeslagen of dat deze zijn opgeslagen in VHD's die opnieuw zijn opgeslagen in Azure Blobs.

Wanneer u een Microsoft Azure Storage-BLOB gebruikt als de back-updoel Hallo in recentere versies, bent u beperkt toodesignating slechts één URL-doel voor elke specifieke back-up.

Maar wanneer u Hallo 'Microsoft SQL Server back-up tooMicrosoft Azure Tool' in oudere versies gebruikt, kunt u meer dan één bestand-doel definiëren. Met meer dan één doel Hallo back-up kan worden geschaald en hello doorvoer van back-up Hallo hoger is. Dit zou vervolgens leiden tot meerdere bestanden ook in hello Azure Storage-account. Bij onze tests met behulp van meerdere bestand bestemmingen een absoluut Hallo doorvoer die een met Hallo back-extensies bereiken kan kunt bereiken in geïmplementeerd van SQL Server 2012 SP1 CU4 op. U worden ook niet geblokkeerd door de limiet van 1TB Hallo zoals in Hallo systeemeigen back-up naar Azure.

Houd er echter rekening, Hallo doorvoer is ook afhankelijk van Hallo-locatie van Azure Storage-Account u voor back-up Hallo gebruiken Hallo. Een idee mogelijk toolocate Hallo storage-account in een andere regio dan Hallo die VM 's worden uitgevoerd in. Bijvoorbeeld u zou Hallo VM-configuratie worden uitgevoerd in West-Europa, maar u kunt plaatsen Hallo Storage-Account dat u tooback up tegen in Noord-Europa. Zeker is van invloed op Hallo back-doorvoer en is niet waarschijnlijk toogenerate als het toobe mogelijk in gevallen waarbij Hallo doelopslag en Hallo van virtuele machines worden uitgevoerd in de Hallo lijkt een doorvoer van 150MB per seconde hetzelfde regionale datacenter.

#### <a name="managing-backup-blobs"></a>Back-Upblobs beheren
Er is een back-ups van vereiste toomanage Hallo op uw eigen. Aangezien Hallo verwachting is dat veel blobs wordt gemaakt door het uitvoeren van regelmatige transactielogboekback-ups, kunt beheer van deze BLOB's gemakkelijk overbelast hello Azure-Portal. Daarom is het recommendable tooleverage een Azure Storage Explorer. Er zijn verschillende goed beschikbaar waarmee toomanage Azure storage-account

* Microsoft Visual Studio met Azure SDK is geïnstalleerd (<https://azure.microsoft.com/downloads/>)
* Microsoft Azure Opslagverkenner (<https://azure.microsoft.com/downloads/>)
* 3e hulpprogramma's van derden

[comment]: <> (Nog niet ondersteund op ARM)
[comment]: <> (### Azure VM-back-up)
[comment]: <> (Virtuele machines binnen Hallo SAP-systeem kunnen worden back-up met Azure virtuele Machine back-up-functionaliteit. Azure virtuele Machine back-up is geïntroduceerd vroeg in Hallo jaar 2015 en ondertussen is een standaardmethode toobackup een volledige virtuele machine in Azure. Azure Backup Hallo back-ups opslaat in Azure en Hiermee kunt een herstel van een virtuele machine opnieuw.)
[comment]: <> (Virtuele machines die uitvoeren databases kunnen een back-up op een consistente manier ook als Hallo DBMS systemen ondersteunt Windows VSS Volume Shadow Copy Service Hallo < https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> SQL-Server komt. Dus een manier tooget tooa-terug te zetten met behulp van de virtuele machine van Azure back-up kan worden back-up van een SAP-database. Let echter dat op basis van de virtuele machine van Azure back-ups punt in tijd van databases herstelt is niet mogelijk. Hallo-aanbeveling is daarom tooperform back-ups van databases met DBMS-functionaliteit in plaats van te vertrouwen op Azure VM Backup.)
[comment]: <> (tooget bekend bent met de back-up van Azure virtuele Machine start hier < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Met behulp van een SQL Server-installatiekopieën buiten Hallo Microsoft Azure Marketplace
Microsoft biedt virtuele machines in hello Azure Marketplace waarin al versies van SQL Server. Voor SAP-klanten die licenties voor SQL Server en Windows vereist, dit wordt mogelijk een kans toobasically behandeld Hallo nodig voor licenties op draaien virtuele machines met SQL Server is al geïnstalleerd. In de volgorde toouse dergelijke afbeeldingen voor SAP, Hallo overwegingen na moet toobe aangebracht:

* Hallo SQL Server-niet-evaluatieversies verkrijgen duurder dan slechts een 'Windows-only' virtuele machine van Azure Marketplace geïmplementeerd. Raadpleeg deze artikelen toocompare prijzen: <https://azure.microsoft.com/pricing/details/virtual-machines/> en <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* U kunt alleen SQL Server-versies die worden ondersteund door SAP, zoals SQL Server 2012 gebruiken.
* Hallo-sortering van Hallo SQL Server-exemplaar dat wordt geïnstalleerd in Hallo virtuele machines die worden aangeboden in hello Azure Marketplace is geen Hallo sortering SAP NetWeaver Hallo SQL Server-exemplaar toorun vereist. Hoewel u met de Hallo aanwijzingen in de volgende sectie Hallo kunt u Hallo sortering.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Hallo SQL Server-sortering van een virtuele Microsoft Windows/SQL Server wijzigen
Omdat SQL Server-installatiekopieën in Azure Marketplace Hallo Hallo niet toouse Hallo sortering die wordt door SAP NetWeaver toepassingen vereist zijn ingesteld, moet deze toobe onmiddellijk na het Hallo-implementatie gewijzigd. Voor SQL Server 2012, kunt dit doen met Hallo volgende stappen uit zoals hello VM is geïmplementeerd en een beheerder kan toolog in Hallo geïmplementeerd VM:

* Open een opdrachtvenster Windows 'als beheerder'.
* Hallo directory tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012 wijzigen.
* Hallo-opdracht uitvoeren: Setup.exe/quiet/Action = REBUILDDATABASE/InstanceName = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`> /SQLCOLLATION SQL_Latin1_General_Cp850_BIN2 =   
  * `<local_admin_account_name`> Hallo-account die is gedefinieerd als Hallo administrator-account bij het implementeren van Hallo VM voor Hallo eerst door Hallo-galerie.

Hallo moet alleen een paar minuten duren. In de volgorde toomake ervoor of Hallo stap uiteindelijk met de juiste resultaat hello, Voer Hallo stappen te volgen:

* Open SQL Server Management Studio.
* Open een queryvenster.
* Hallo opdracht sp_helpsort uitvoeren in Hallo SQL Server-hoofddatabase.

Hallo gewenst resultaat moet eruitzien als:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Als dit niet Hallo resultaat stoppen SAP implementeren en onderzoeken waarom Hallo setup-opdracht niet werkt zoals verwacht. Implementatie van toepassingen naar SQL Server-exemplaar met een andere SQL Server-codetabellen SAP NetWeaver dan een bovengenoemde Hallo is **niet** ondersteund.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>SQL Server hoge beschikbaarheid voor SAP in Azure
Zoals eerder in dit artikel wordt vermeld, is er geen mogelijkheid toocreate gedeelde opslag die nodig zijn voor gebruik van de oudste functionaliteit van SQL Server hoge beschikbaarheid Hallo Hallo. Deze functionaliteit zou twee of meer exemplaren van SQL Server installeren in een Windows Server Failover Cluster (WSFC) met een gedeelde schijf voor Hallo gebruikersdatabases (en uiteindelijk tempdb). Dit is Hallo lang standaard hoge beschikbaarheidsmethode die ook wordt ondersteund door SAP. Omdat Azure biedt geen ondersteuning voor gedeelde opslag, kunnen niet SQL Server-configuraties voor hoge beschikbaarheid met een configuratie met een gedeelde schijf worden gerealiseerd. Veel andere methoden van hoge beschikbaarheid zijn echter nog steeds mogelijk en worden beschreven in Hallo uit te voeren.

[comment]: <> (Artikel nog steeds verwezen tooASM)
[comment]: <> (Voordat u technologieën voor hoge beschikbaarheid van andere specifieke Hallo bruikbare leest voor SQL Server in Azure, is een zeer goede document waarmee meer informatie en verwijzingen [[[[hier] Virtual-machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Meld u back-ups van SQL Server
Een van de methoden Hallo van hoge beschikbaarheid (HA) is logboekverzending van SQL Server. Hallo virtuele machines die deel uitmaken van Hallo HA configuratie hebt naamomzetting werkt, er is geen probleem als Hallo-instellingen in Azure wordt niet verschillen van elke instelling die lokaal wordt uitgevoerd. Het is niet raadzaam toorely op alleen IP-adresomzetting. Schakel deze documentatie in groet toosetting up logboekverzending en Hallo principes rond logboekverzending:

<https://technet.Microsoft.com/library/ms187103.aspx>

In de volgorde tooreally voor een andere hoge beschikbaarheid, moet één toodeploy Hallo virtuele machines die zijn binnen deze een back-upfunctie voor logboekbestanden configuratie toobe binnen Hallo dezelfde Azure-Beschikbaarheidsset.

#### <a name="database-mirroring"></a>Databasespiegeling
Spiegelen database zoals ondersteund door SAP (Zie SAP-notitie [965908]) is afhankelijk van het definiëren van een failoverpartner in Hallo SAP-verbindingsreeks. Hallo Cross-Premises gevallen, gaan we ervan uit dat twee virtuele machines in Hallo worden Hallo hetzelfde domein of Hallo gebruiker context Hallo twee SQL Server-exemplaren worden uitgevoerd onder ook domeingebruikers en zijn voldoende rechten hebt om in Hallo twee SQL Server-exemplaren die zijn betrokken. Hallo-installatie van het spiegelen van de Database in Azure daarom niet van een typische on-premises setup/configuratie verschillen.

Alleen in de Cloud-implementaties, is de eenvoudigste methode Hallo toohave een ander domein instellen in Azure toohave die DBMS VMs (en in het ideale geval toegewezen SAP-virtuele machines) binnen een domein.

Als een domein niet mogelijk is, kan een ook certificaten gebruiken voor Hallo databasespiegeling eindpunten zoals hier wordt beschreven: <https://technet.microsoft.com/library/ms191477.aspx>

Een zelfstudie tooset-up databasespiegeling in Azure vindt u hier: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
Als AlwaysOn wordt ondersteund voor SAP on-premises (Zie SAP-notitie [1772688]), het ondersteunde toobe gebruikt in combinatie met SAP in Azure is. Hallo feit dat u niet kunt toocreate gedeelde schijven in Azure betekent niet dat een configuratie niet een AlwaysOn Windows Server Failover Cluster (WSFC) tussen de verschillende virtuele machines maken kan. Alleen betekent dit dat er geen Hallo mogelijkheid toouse een gedeelde schijf als een quorum in Hallo clusterconfiguratie. Daarom kunt u een configuratie van AlwaysOn WSFC in Azure bouwen en eenvoudig hello quorumtype die gebruikmaakt van gedeelde schijf niet selecteren. Hello Azure-omgeving die virtuele machines zijn geïmplementeerd in moet worden omgezet Hallo van virtuele machines met de naam en Hallo VMs Hallo moet zijn hetzelfde domein. Dit geldt voor Azure alleen en Cross-Premises implementaties. Er zijn enkele speciale overwegingen in de installatie van SQL Server beschikbaarheidsgroep-Listener (kan niet in toobe worden verward met hello Azure Beschikbaarheidsset) Hallo omdat Azure op dit moment niet toegestaan toosimply AD en DNS-object maken als het is mogelijk een on-premises. Daarom zijn sommige andere installatiestappen nodig tooovercome Hallo specifiek gedrag van Azure.

Enkele overwegingen met behulp van een beschikbaarheidsgroep-Listener zijn:

* Met behulp van een beschikbaarheidsgroep-Listener is alleen mogelijk met Windows Server 2012 of Windows Server 2012 R2 als gastbesturingssysteem Hallo VM. Voor Windows Server 2012 moet u controleren of deze patch is toegepast toomake: <https://support.microsoft.com/kb/2854082>
* Voor Windows Server 2008 R2 deze patch niet bestaat en AlwaysOn moet toobe gebruikt in Hallo dezelfde manier als het spiegelen van de Database door te geven van een failoverpartner in Hallo verbindingen tekenreeks (via Hallo SAP default.pfl parameter databases/mss/server: Zie SAP-notitie [965908]).
* Wanneer met behulp van een beschikbaarheidsgroep-Listener, Hallo Database VMs toobe verbonden moeten specifiek tooa Load Balancer. Naamomzetting in de Cloud-implementaties moet ofwel alle virtuele machines van een SAP-systeem (toepassingsservers, DBMS-server en (A) server SCS) zijn hetzelfde virtuele netwerk Hallo of zou moeten uit een SAP toepassing laag Hallo onderhoud van Hallo etc\host bestand in volgorde tooget Hallo VM namen van Hallo SQL Server-VM's opgelost. In de volgorde tooavoid Azure toewijzen van nieuwe IP-adressen in gevallen waarin beide VM afsluiten incidenteel zijn, moet een statische IP-adressen toohello netwerkinterfaces van deze VMs in Hallo AlwaysOn-configuratie (definiëren van een statisch IP-adres is beschreven in toewijzen [dit] [ virtual-networks-reserved-private-ip] artikel)

[comment]: <> (Oude blogs)
[comment]: <> (< https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, < https://blogs.technet.com/b/rmilne/ Archive/2015/07/27/How-to-set-static-IP-on-Azure-VM.aspx >)
* Er zijn speciale stappen vereist wanneer bouwen Hallo WSFC-clusterconfiguratie waarin Hallo cluster een speciale IP-adres moet is toegewezen, omdat Azure met de huidige functionaliteit Hallo clusternaam toewijzen zou hetzelfde IP-adres als cluster met knooppunt Hallo HALLO hallo wordt gemaakt op. Dit betekent dat een handmatige stap moet uitgevoerd tooassign een ander IP-adres toohello cluster.
* Hallo beschikbaarheidsgroep-Listener gaat toobe in Azure gemaakt met de TCP/IP-eindpunten die zijn toegewezen toohello VMs Hallo primaire en secundaire replica van beschikbaarheidsgroep Hallo uitgevoerd.
* Er mogelijk een toosecure moeten deze eindpunten met ACL's.

[comment]: <> (Oude TODO-blog)
[comment]: <> (Hallo gedetailleerde stappen en noodzakelijke items moeten meebrengen van het installeren van een AlwaysOn-configuratie op Azure zijn het best bij stap voor stap Hallo zelfstudie beschikbaar [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Vooraf geconfigureerde AlwaysOn-setup via hello Azure-galerie < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Het maken van een beschikbaarheidsgroep-Listener is beste beschreven in de zelfstudie [this][virtual-machines-windows-classic-ps-sql-int-listener])
[comment]: <> (Beveiligen netwerkeindpunten met ACL's worden uitgelegd beste hier:)
[comment]: <> (* < https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>)

Het is mogelijk toodeploy een SQL Server AlwaysOn-beschikbaarheidsgroep via verschillende Azure-regio's ook. Deze functionaliteit worden benut als hello Azure VNet-naar-Vnet-connectiviteit ([meer details][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Oude TODO-blog)
[comment]: <> (Hallo-installatie van SQL Server AlwaysOn-beschikbaarheidsgroepen in een dergelijk scenario Hier wordt beschreven: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Overzicht van hoge beschikbaarheid van SQL Server in Azure
Opgegeven Hallo fact dat Azure Storage Hallo inhoud beveiligt, is er een minder reden tooinsist op een hot stand-by-installatiekopie. Dit betekent dat uw scenario hoge beschikbaarheid moet tooonly bescherming tegen Hallo volgende gevallen:

* Niet beschikbaar zijn Hallo VM als geheel vervaldatum toomaintenance op Hallo server-cluster in Azure of andere redenen
* Softwareproblemen in Hallo SQL Server-exemplaar
* Beveiligen van handmatige fout waarbij gegevens wordt verwijderd en herstel van de punt in tijd nodig is

Kijken naar overeenkomende technologieën een kunt voeren aan dat de eerste twee gevallen Hallo kunnen worden volstaan met databasespiegeling of AlwaysOn, terwijl de derde geval Hallo alleen kan worden volstaan met upfunctie voor logboekbestanden.

U moet toobalance Hallo complexere setup van AlwaysOn, vergeleken tooDatabase Mirroring met Hallo voordelen van AlwaysOn. Deze voordelen kunnen worden weergegeven zoals:

* Leesbare secundaire replica's.
* Back-ups van secundaire replica's.
* Betere schaalbaarheid.
* Meer dan één secundaire replica's.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Algemene SQL Server voor SAP op Azure samenvatting
Er zijn veel aanbevelingen in deze handleiding en het is raadzaam gelezen meer dan één keer voordat u uw Azure-implementatie plannen. In het algemeen echter zeker toofollow Hallo top tien algemene DBMS op Azure specifieke punten:

[comment]: <> (2.3 hogere doorvoer dan? Dan één VHD?)
1. Gebruik Hallo nieuwste DBMS release, zoals SQL Server 2014 met Hallo meeste voordelen in Azure. Dit is voor SQL Server, SQL Server 2012 SP1 CU4 waaronder Hallo-functie van de back-ups maken zich verhouden tot Azure Storage. We raden echter in combinatie met SAP zou aan ten minste CU1 voor SQL Server 2014 SP1 of SQL Server 2012 SP2 en Hallo nieuwste CU.
2. Uw SAP-systeem Liggend in Azure toobalance Hallo gegevensindeling bestand en Azure beperkingen zorgvuldig te plannen:
   * Hoeft niet te veel VHD's, maar hebben onvoldoende tooensure die u kunt de vereiste IOPS bereiken.
   * Houd er rekening mee IOP's zijn ook beperkt per Azure-Opslagaccount en dat Storage-Accounts beperkt in elk Azure-abonnement zijn ([meer details][azure-subscription-service-limits]).
   * Alleen streep over VHD's als u een hogere doorvoer tooachieve nodig.
3. Nooit software te installeren of bestanden die gebruikmaken van persistentie op Hallo D:\ station als het niet-permanente is en alles op dit station gaan verloren wanneer u een Windows opnieuw opstart te plaatsen.
4. Gebruik geen VHD van de Azure cache voor Azure Standard-opslag.
5. Gebruik geen Azure geogerepliceerde Storage-Accounts.  Lokaal Redundant voor DBMS werkbelastingen gebruiken.
6. Gebruik van de leverancier van uw DBMS HA-/ DR tooreplicate database oplossingsgegevens.
7. Altijd naamomzetting gebruiken, niet vertrouwen op IP-adressen.
8. Hallo hoogste database compressie mogelijk gebruiken. Dit is de compressie van de pagina voor SQL Server.
9. Wees voorzichtig met behulp van SQL Server-installatiekopieën van hello Azure Marketplace. Als u SQL Server een Hallo gebruikt, moet u de sortering van het Hallo-exemplaar voordat u een systeem SAP NetWeaver installeert op deze wijzigen.
10. Installeren en configureren van Hallo SAP Host bewaking voor Azure, zoals beschreven in [Deployment Guide][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Specificaties tooSAP as op Windows-omgeving
Beginnen met Microsoft Azure, kunt u gemakkelijk migreren uw bestaande SAP-as-omgeving toepassingen tooAzure virtuele Machines. SAP-as-omgeving in een virtuele Machine kunt u tooreduce Hallo totale eigendomskosten van implementatie, beheer en onderhoud van de breedte van bedrijfstoepassingen door eenvoudig deze toepassingen tooMicrosoft Azure te migreren. Met as-SAP omgeving in een virtuele Machine van Azure, beheerders en ontwikkelaars kunnen nog steeds gebruiken Hallo dezelfde ontwikkelings- en hulpprogramma's die beschikbaar zijn op lokale.

Er is een SLA voor hello Azure Virtual Machines die u kunt hier vinden: <https://azure.microsoft.com/support/legal/sla>

We zijn ervan overtuigd dat Microsoft Azure gehoste virtuele Machines zeer goed wordt uitgevoerd in vergelijking tooother openbare cloud virtualization aanbiedingen, maar de afzonderlijke resultaten kan verschillen. SAP sizing SAP's aantallen Hallo verschillende SAP gecertificeerd VM-SKU's worden vermeld in een afzonderlijke SAP-notitie [1928533].

Instructies en aanbevelingen in inachtneming toohello informatie over het gebruik van Azure Storage, de implementatie van de SAP VM's of de SAP bewaking van toepassing toodeployments van SAP-as-omgeving in combinatie met SAP-toepassingen zoals vermeld in de gehele Hallo vier hoofdstukken van dit document.

### <a name="sap-ase-version-support"></a>Ondersteuning voor SAP-versie van de as-omgeving
SAP momenteel ondersteunt SAP-as-omgeving versie 16,0 voor gebruik met SAP Business Suite producten. Alle updates voor SAP-as-omgeving server of JDBC en ODBC-stuurprogramma's toobe gebruikt met SAP Business Suite-producten worden geleverd enkel via SAP Service Marketplace op Hallo: <https://support.sap.com/swdc>.

Als voor installaties downloaden on-premises updates voor Hallo SAP-as-omgeving server, of hello JDBC- en ODBC-stuurprogramma's rechtstreeks vanuit de Sybase-websites niet. Zie voor gedetailleerde informatie over patches die worden ondersteund voor gebruik met SAP Business Suite producten on-premises en in Azure Virtual Machines Hallo SAP notities te volgen:

* [1590719]
* [1973241]

Algemene informatie over het uitvoeren van SAP Business Suite van SAP-as-omgeving vindt u in Hallo [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Richtlijnen voor SAP as-omgeving voor SAP gerelateerde SAP as-omgeving installaties in Azure Virtual machines
#### <a name="structure-of-hello-sap-ase-deployment"></a>Structuur van Hallo SAP-implementatie voor as-omgeving
Hallo algemene beschrijving, in overeenstemming met SAP-as-omgeving uitvoerbare bestanden moet zich bevinden of in Hallo systeemstation van de basis-VHD Hallo van de virtuele machine is geïnstalleerd (station c:\). Normaal gesproken worden de meeste Hallo SAP-as-omgeving system en hulpprogramma's voor databases niet echt gebruikt hard door SAP NetWeaver werkbelasting. Daarom Hallo system en hulpprogramma's voor databases (master, model, saptools, sybmgmtdb, sybsystemdb) op Hallo C:\drive ook kunnen blijven staan.

Een uitzondering kan Hallo tijdelijke database bevat alle werktabellen en tijdelijke tabellen die zijn gemaakt door SAP as-omgeving, die in geval van een bepaalde ERP SAP en alle BW werkbelastingen hoger gegevensvolume of i/o-bewerkingen volume dat niet in oorspronkelijke Hallo past vereist zijn Basis-VHD van de virtuele machine (station c:\).

Afhankelijk van Hallo versie van SAPInst/SWPM tooinstall Hallo system gebruikt, Hallo-database bevat mogelijk:

* Een eenmalige SAP-as-omgeving tempdb die wordt gemaakt bij het installeren van SAP-as-omgeving
* Een SAP-as-omgeving tempdb gemaakt door SAP-as-omgeving en een extra saptempdb gemaakt door Hallo SAP-installatieprogramma te installeren
* Een SAP-as-omgeving tempdb gemaakt door het installeren van SAP-as-omgeving en een extra tempdb die handmatig is gemaakt (bijvoorbeeld de volgende SAP-notitie [1752266]) toomeet ERP/BW specifieke tempdb-vereisten

In geval van een specifieke ERP of alle BW werkbelastingen zinvol het, in inachtneming van tooperformance, tookeep Hallo tempdb apparaten van Hallo bovendien gemaakt tempdb (door SWPM of handmatig) op een ander station dan C:\. Als er geen aanvullende tempdb het bestaat wordt aanbevolen toocreate een (SAP-notitie [1752266]).

Voor dergelijke systemen Hallo moeten de volgende stappen worden uitgevoerd voor Hallo bovendien tempdb gemaakt:

* Hallo eerste tempdb apparaat toohello eerste apparaat van Hallo SAP-database verplaatsen
* Toevoegen van tempdb apparaten tooeach Hallo VHD's met daarin een apparaten van Hallo SAP-database

Deze configuratie kunt tempdb tooeither verbruikt meer ruimte dan Hallo systeemstation kunnen tooprovide is. Als een verwijzing kunt een Hallo tempdb apparaat grootten op bestaande systemen die on-premises uitgevoerd controleren. Of een dergelijke configuratie IOPS getallen op basis van tempdb die kan niet worden voorzien van het systeemstation hello wilt inschakelen. Systemen met lokale mag opnieuw gebruikte toomonitor i/o-werkbelasting op tempdb.

Nooit apparaten SAP-as-omgeving op Hallo station D:\ Hallo VM geplaatst. Dit geldt ook toohello tempdb, zelfs als het Hallo-objecten in tempdb Hallo bewaard zijn slechts tijdelijk.

#### <a name="impact-of-database-compression"></a>Gevolgen van het Database-compressie
In configuraties waar i/o-bandbreedte kan een beperkende factor, kan elke meting waardoor IOPS toostretch Hallo werkbelasting een in een IaaS-scenario zoals Azure uitvoeren kunt helpen. Daarom is het raadzaam toomake ervoor dat de SAP-as-omgeving compressie wordt gebruikt voordat u een bestaande database tooAzure voor SAP uploadt.

Hallo aanbeveling tooperform compressie voordat u uploadt tooAzure als deze is niet geïmplementeerd wordt gegeven buiten verschillende redenen:

* Hallo hoeveelheid gegevens geüpload toobe tooAzure is lager
* Hallo duur van Hallo compressie uitvoering is korter, ervan uitgaande dat sterkere hardware kunnen worden gebruikt met meer CPU's of hogere i/o-bandbreedte of minder i/o-latentie lokale
* Kleinere database kunnen leiden tot tooless kosten voor schijftoewijzing

Compressie van gegevens en LOB werken in een virtuele machine in Azure Virtual Machines gehost als er een lokale. Voor meer informatie over hoe toocheck als compressie is al in gebruik in een bestaande as SAP-omgeving database Controleer SAP-notitie [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Met behulp van DBACockpit toomonitor Database-exemplaren
Voor SAP-systemen die SAP-as-omgeving als databaseplatform gebruiken, is de Hallo DBACockpit toegankelijk als ingesloten browservensters in transactie DBACockpit of Webdynpro. Echter Hallo volledige functionaliteit voor bewaking en beheer Hallo-database is beschikbaar in Hallo Webdynpro uitvoering van Hallo DBACockpit alleen.

Als met on-premises systemen die verschillende stappen zijn vereist tooenable alle SAP NetWeaver functionaliteit die wordt gebruikt door Hallo Webdynpro uitvoering van Hallo DBACockpit. Volg SAP-notitie [1245200] tooenable Hallo gebruik van webdynpros en het genereren van Hallo vereist zijn. Wanneer Hallo volgende Hallo-instructies in Hallo hierboven opmerkingen die u ook Hallo Internet Communication Manager (icm) samen met configureert poorten toobe gebruikt voor http en https-verbindingen. Hallo standaardinstelling voor HTTP-ziet er als volgt:

> ICM/server_port_0 = b = HTTP, poort = 8000, PROCTIMEOUT = 600, time-out = 600
>
> ICM/server_port_1 = b = HTTPS, poort = 443$ $, PROCTIMEOUT = 600, time-out = 600
>
>

en Hallo koppelingen gegenereerd in transactie DBACockpit eruit vergelijkbare toothis:

> https://`<fullyqualifiedhostname`>: sap/44300/bc/sap/webdynpro/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: sap/8000/bc/sap/webdynpro/dba_cockpit
>
>

Afhankelijk van of en hoe hello Azure virtuele Machine hosting Hallo SAP-systeem is verbonden via site-naar-site meerdere locaties of ExpressRoute (Cross-Premises implementatie), moet u toomake ervoor dat ICM gebruikmaakt van een volledig gekwalificeerde hostnaam die kan worden omgezet op Hallo computer waarop u tooopen probeert Hallo DBACockpit uit. Zie SAP-notitie [773830] toounderstand hoe ICM bepaalt Hallo volledig gekwalificeerde hostnaam, afhankelijk van de parameters-profiel en set-parameter icm/host_name_full expliciet indien nodig.

Als u Hallo VM in een Cloudconfiguratie scenario zonder cross-premises-connectiviteit tussen on-premises en Azure hebt geïmplementeerd, moet u toodefine een openbaar IP-adres en een domainlabel. Hallo-indeling van het openbare DNS-naam Hallo Hallo VM ziet vervolgens er als volgt:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Meer informatie gerelateerd toohello DNS-naam vindt [hier][virtual-machines-azurerm-versus-azuresm].

Instelling Hallo SAP profiel parameter icm/host_name_full toohello DNS-naam van hello Azure VM Hallo koppeling eruit als in:

> sap/https://mydomainlabel.westeurope.cloudapp.NET:44300/bc/sap/webdynpro/dba_cockpit
>
> sap/http://mydomainlabel.westeurope.cloudapp.NET:8000/bc/sap/webdynpro/dba_cockpit
>
>

In dit geval moet u toomake Zorg ervoor dat:

* Regels voor binnenkomende verbindingen toohello Netwerkbeveiligingsgroep in hello Azure-Portal voor Hallo TCP/IP-poorten gebruikt toocommunicate met ICM toevoegen
* Regels voor binnenkomende verbindingen toohello Windows Firewall-configuratie voor Hallo TCP/IP-poorten die worden gebruikt toocommunicate Hello ICM toevoegen

Voor een geautomatiseerde geïmporteerd met alle correcties beschikbaar, is het raadzaam tooperiodically Hallo correctie verzameling SAP-notitie van toepassing tooyour SAP versie toe te passen:

* [1558958]
* [1619967]
* [1882376]

Meer informatie over DBA Cockpit voor SAP-as-omgeving vindt u in de volgende opmerkingen bij de SAP Hallo:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Overwegingen voor back-up/herstel voor SAP-as-omgeving
Uw back-upmethode moet worden gecontroleerd bij het implementeren van SAP-as-omgeving in Azure. Zelfs als het Hallo-systeem is niet een productieve systeem, Hallo SAP-database gehost door SAP-as-omgeving moet een back-up regelmatig. Omdat Azure Storage drie afbeeldingen houdt, is nu een back-up minder belangrijke toocompensating ten opzichte van een crash van de opslag. Hello primaire reden voor het onderhouden van een juiste back-up en herstel plan is meer die u logische/handmatige fouten compenseren kunt door punt in tijd herstelfuncties te bieden. Zodat het Hallo-doel is tooeither gebruik back-ups toorestore Hallo database terug tooa bepaalde punt in tijd of toouse Hallo back-ups in Azure tooseed een ander systeem Hallo bestaande database kopiëren. Bijvoorbeeld, u kan overzetten van een 2-Tier SAP configuratie tooa 3-Laagse setup van system Hallo dezelfde systeem door het herstellen van een back-up.

Back-up en terugzetten van een database in Azure werkt Hallo dezelfde manier als er een lokale is. Zie SAP-opmerkingen:

* [1588316]
* [1585981]

voor informatie over maken dump configuraties en planning back-ups. Afhankelijk van uw strategie en behoeften kunt u configureren database en logboekbestanden dumpen toodisk naar een bestaande VHD's hello of een extra VHD voor back-up Hallo toevoegen.  tooreduce hello gevaar gegevensverlies in geval van een fout is aanbevolen toouse een VHD waar geen databaseapparaat zich bevindt.

Compressie SAP-as-omgeving biedt naast gegevens- en LOB ook back-compressie. toooccupy minder ruimte met Hallo-database en logboekbestanden dumpbestanden voor deze toouse back-compressie wordt aanbevolen. Zie SAP-notitie [1588316] voor meer informatie. Comprimeren Hallo back-up is ook cruciaal tooreduce Hallo hoeveelheid gegevens toobe overgedragen als u van plan bent toodownload back-ups of VHD's met back-dumps van hello Azure virtuele Machine tooon-premises.

Gebruik geen station D:\ als doel-dump database of logboekbestanden.

#### <a name="performance-considerations-for-backupsrestores"></a>Prestatie-overwegingen voor back-ups/herstelacties
Prestaties van back-up/herstel is net zoals in de bare-metal implementaties, afhankelijk van hoeveel volumes parallel kunnen worden gelezen en welke Hallo doorvoer van deze volumes mogelijk. Bovendien speelt Hallo CPU-verbruik door back-compressie gebruikt een belangrijke rol op virtuele machines met slechts komen too8 CPU threads. Daarom kan een aannemen:

* Hallo minder Hallo aantal virtuele harde schijven gebruikt toostore Hallo databaseapparaten Hallo Hallo kleinere totale doorvoer in lezen
* Hallo kleinere Hallo aantal threads in Hallo VM CPU, Hallo ernstige Hallo gevolgen van het back-compressie
* Hallo minder doelen (Stripe-mappen, VHD's) toowrite Hallo back-up, Hallo minder Hallo doorvoer

tooincrease hello aantal doelen toowrite toothere zijn twee opties die kunnen worden gebruikt/gecombineerd afhankelijk van uw behoeften:

* De back-up doelvolume Hallo striping over meerdere gekoppelde VHD's in een volgorde tooimprove hello IOPS doorvoer op dat volume striped
* Maken van een configuratie dump op niveau SAP-as-omgeving maakt gebruik van meer dan één doel directory toowrite Hallo dump naar

Eerder in deze handleiding is een volume striping over meerdere gekoppelde VHD's beschreven. Voor meer informatie over het gebruik van meerdere directory's in de configuratie van de dump Hallo SAP-as-omgeving raadpleegt u toohello documentatie over de opgeslagen Procedure sp_config_dump die gebruikte toocreate Hallo dump configuratie op Hallo [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Herstel na noodgevallen met virtuele machines in Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Gegevensreplicatie met SAP Sybase replicatie Server
Hallo biedt SAP Sybase Replication Server (SRS) SAP-as-omgeving een warme stand-by-oplossing tootransfer transacties tooa verafgelegen databaselocatie asynchroon.

Hallo-installatie en de werking van SRS werkt ook in een virtuele machine in Azure Services op virtuele Machine wordt gehost als er een lokale functioneel.

As-omgeving HADR via SAP replicatie Server is met een toekomstige release gepland. Het wordt getest met en uitgebracht voor Microsoft Azure-platforms, zodra deze beschikbaar is.

## <a name="specifics-toosap-ase-on-linux"></a>Specificaties tooSAP as-omgeving op Linux
Beginnen met Microsoft Azure, kunt u gemakkelijk migreren uw bestaande SAP-as-omgeving toepassingen tooAzure virtuele Machines. SAP-as-omgeving in een virtuele Machine kunt u tooreduce Hallo totale eigendomskosten van implementatie, beheer en onderhoud van de breedte van bedrijfstoepassingen door eenvoudig deze toepassingen tooMicrosoft Azure te migreren. Met as-SAP omgeving in een virtuele Machine van Azure, beheerders en ontwikkelaars kunnen nog steeds gebruiken Hallo dezelfde ontwikkelings- en hulpprogramma's die beschikbaar zijn op lokale.

Voor het implementeren van Azure VM's van belangrijke tooknow Hallo officiële Sla's die u kunnen hier vinden: <https://azure.microsoft.com/support/legal/sla>

SAP sizinginformatie en een lijst met SAP gecertificeerd VM-SKU's worden vermeld in SAP-notitie [1928533]. Aanvullende SAP sizing documenten voor Azure Virtual machines u hier vindt <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> en hier <http : //blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Instructies en aanbevelingen in inachtneming toohello informatie over het gebruik van Azure Storage, de implementatie van de SAP VM's of de SAP bewaking van toepassing toodeployments van SAP-as-omgeving in combinatie met SAP-toepassingen zoals vermeld in de gehele Hallo vier hoofdstukken van dit document.

Hallo bevatten twee volgende SAP-opmerkingen algemene informatie over as-omgeving op Linux- en as-omgeving in Hallo Cloud:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Ondersteuning voor SAP-versie van de as-omgeving
SAP momenteel ondersteunt SAP-as-omgeving versie 16,0 voor gebruik met SAP Business Suite producten. Alle updates voor SAP-as-omgeving server of JDBC en ODBC-stuurprogramma's toobe gebruikt met SAP Business Suite-producten worden geleverd enkel via SAP Service Marketplace op Hallo: <https://support.sap.com/swdc>.

Als voor installaties downloaden on-premises updates voor Hallo SAP-as-omgeving server, of hello JDBC- en ODBC-stuurprogramma's rechtstreeks vanuit de Sybase-websites niet. Zie voor gedetailleerde informatie over patches die worden ondersteund voor gebruik met SAP Business Suite producten on-premises en in Azure Virtual Machines Hallo SAP notities te volgen:

* [1590719]
* [1973241]

Algemene informatie over het uitvoeren van SAP Business Suite van SAP-as-omgeving vindt u in Hallo [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Richtlijnen voor SAP as-omgeving voor SAP gerelateerde SAP as-omgeving installaties in Azure Virtual machines
#### <a name="structure-of-hello-sap-ase-deployment"></a>Structuur van Hallo SAP-implementatie voor as-omgeving
Hallo algemene beschrijving, in overeenstemming met moet SAP-as-omgeving uitvoerbare bestanden zich bevinden of in Hallo hoofdmap bestandssysteem Hallo VM (/sybase) geïnstalleerd. Normaal gesproken worden de meeste Hallo SAP-as-omgeving system en hulpprogramma's voor databases niet echt gebruikt hard door SAP NetWeaver werkbelasting. Daarom Hallo system en hulpprogramma's voor databases (master, model, saptools, sybmgmtdb, sybsystemdb) op Hallo hoofdmap bestandssysteem ook kunnen blijven staan.

Een uitzondering kan Hallo tijdelijke database bevat alle werktabellen en tijdelijke tabellen die zijn gemaakt door SAP as-omgeving, die in geval van een bepaalde ERP SAP en alle BW werkbelastingen hoger gegevensvolume of i/o-bewerkingen volume dat niet in oorspronkelijke Hallo past vereist zijn De besturingssysteemschijf van de virtuele machine.

Afhankelijk van Hallo versie van SAPInst/SWPM tooinstall Hallo system gebruikt, Hallo-database bevat mogelijk:

* Een eenmalige SAP-as-omgeving tempdb die wordt gemaakt bij het installeren van SAP-as-omgeving
* Een SAP-as-omgeving tempdb gemaakt door SAP-as-omgeving en een extra saptempdb gemaakt door Hallo SAP-installatieprogramma te installeren
* Een SAP-as-omgeving tempdb gemaakt door het installeren van SAP-as-omgeving en een extra tempdb die handmatig is gemaakt (bijvoorbeeld de volgende SAP-notitie [1752266]) toomeet ERP/BW specifieke tempdb-vereisten

In geval van een specifieke ERP of alle BW werkbelastingen is het zinvol, in inachtneming van tooperformance, tookeep Hallo tempdb apparaten van Hallo bovendien gemaakt tempdb (door SWPM of handmatig) op een afzonderlijk bestand-systeem dat kan worden vertegenwoordigd door een gegevensschijf met één Azure of een RAID Linux meerdere Azure gegevensschijven-spanning. Als er geen aanvullende tempdb het bestaat wordt aanbevolen toocreate een (SAP-notitie [1752266]).

Voor dergelijke systemen Hallo moeten de volgende stappen worden uitgevoerd voor Hallo bovendien tempdb gemaakt:

* Hallo eerste tempdb directory toohello eerste bestandssysteem van Hallo SAP-database verplaatsen
* Toevoegen van tempdb mappen tooeach Hallo VHD's met een bestandssysteem van Hallo SAP-database

Deze configuratie kunt tempdb tooeither verbruikt meer ruimte dan Hallo systeemstation kunnen tooprovide is. Als een verwijzing kunt een Hallo tempdb directory grootten op bestaande systemen die on-premises uitgevoerd controleren. Of een dergelijke configuratie IOPS getallen op basis van tempdb die kan niet worden voorzien van het systeemstation hello wilt inschakelen. Systemen met lokale mag opnieuw gebruikte toomonitor i/o-werkbelasting op tempdb.

Plaats alle mappen SAP-as-omgeving nooit naar mnt of /mnt/resource Hallo VM. Dit geldt ook toohello tempdb, zelfs als het Hallo-objecten in tempdb Hallo bewaard zijn slechts tijdelijk omdat mnt of /mnt/resource is een standaard virtuele machine van Azure tijdelijke ruimte die niet persistent is. Meer informatie over hello Azure VM tijdelijke ruimte vindt u in [in dit artikel][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Gevolgen van het Database-compressie
In configuraties waar i/o-bandbreedte kan een beperkende factor, kan elke meting waardoor IOPS toostretch Hallo werkbelasting een in een IaaS-scenario zoals Azure uitvoeren kunt helpen. Daarom is het raadzaam toomake ervoor dat de SAP-as-omgeving compressie wordt gebruikt voordat u een bestaande database tooAzure voor SAP uploadt.

Hallo aanbeveling tooperform compressie voordat u uploadt tooAzure als deze is niet geïmplementeerd wordt gegeven buiten verschillende redenen:

* Hallo hoeveelheid gegevens geüpload toobe tooAzure is lager
* Hallo duur van Hallo compressie uitvoering is korter, ervan uitgaande dat sterkere hardware kunnen worden gebruikt met meer CPU's of hogere i/o-bandbreedte of minder i/o-latentie lokale
* Kleinere database kunnen leiden tot tooless kosten voor schijftoewijzing

Compressie van gegevens en LOB werken in een virtuele machine in Azure Virtual Machines gehost als er een lokale. Voor meer informatie over hoe toocheck als compressie is al in gebruik in een bestaande as SAP-omgeving database Controleer SAP-notitie [1750510]. Zie ook SAP-notitie [2121797] voor aanvullende informatie met betrekking tot de database-compressie.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Met behulp van DBACockpit toomonitor Database-exemplaren
Voor SAP-systemen die SAP-as-omgeving als databaseplatform gebruiken, is de Hallo DBACockpit toegankelijk als ingesloten browservensters in transactie DBACockpit of Webdynpro. Echter Hallo volledige functionaliteit voor bewaking en beheer Hallo-database is beschikbaar in Hallo Webdynpro uitvoering van Hallo DBACockpit alleen.

Als met on-premises systemen die verschillende stappen zijn vereist tooenable alle SAP NetWeaver functionaliteit die wordt gebruikt door Hallo Webdynpro uitvoering van Hallo DBACockpit. Volg SAP-notitie [1245200] tooenable Hallo gebruik van webdynpros en het genereren van Hallo vereist zijn. Wanneer Hallo volgende Hallo-instructies in Hallo hierboven opmerkingen die u ook Hallo Internet Communication Manager (icm) samen met configureert poorten toobe gebruikt voor http en https-verbindingen. Hallo standaardinstelling voor HTTP-ziet er als volgt:

> ICM/server_port_0 = b = HTTP, poort = 8000, PROCTIMEOUT = 600, time-out = 600
>
> ICM/server_port_1 = b = HTTPS, poort = 443$ $, PROCTIMEOUT = 600, time-out = 600
>
>

en Hallo koppelingen gegenereerd in transactie DBACockpit eruit vergelijkbare toothis:

> https://`<fullyqualifiedhostname`>: sap/44300/bc/sap/webdynpro/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: sap/8000/bc/sap/webdynpro/dba_cockpit
>
>

Afhankelijk van of en hoe hello Azure virtuele Machine hosting Hallo SAP-systeem is verbonden via site-naar-site meerdere locaties of ExpressRoute (Cross-Premises implementatie), moet u toomake ervoor dat ICM gebruikmaakt van een volledig gekwalificeerde hostnaam die kan worden omgezet op Hallo computer waarop u tooopen probeert Hallo DBACockpit uit. Zie SAP-notitie [773830] toounderstand hoe ICM bepaalt Hallo volledig gekwalificeerde hostnaam, afhankelijk van de parameters-profiel en set-parameter icm/host_name_full expliciet indien nodig.

Als u Hallo VM in een Cloudconfiguratie scenario zonder cross-premises-connectiviteit tussen on-premises en Azure hebt geïmplementeerd, moet u toodefine een openbaar IP-adres en een domainlabel. Hallo-indeling van het openbare DNS-naam Hallo Hallo VM ziet vervolgens er als volgt:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Meer informatie gerelateerd toohello DNS-naam vindt [hier][virtual-machines-azurerm-versus-azuresm].

Instelling Hallo SAP profiel parameter icm/host_name_full toohello DNS-naam van hello Azure VM Hallo koppeling eruit als in:

> sap/https://mydomainlabel.westeurope.cloudapp.NET:44300/bc/sap/webdynpro/dba_cockpit
>
> sap/http://mydomainlabel.westeurope.cloudapp.NET:8000/bc/sap/webdynpro/dba_cockpit
>
>

In dit geval moet u toomake Zorg ervoor dat:

* Regels voor binnenkomende verbindingen toohello Netwerkbeveiligingsgroep in hello Azure-Portal voor Hallo TCP/IP-poorten gebruikt toocommunicate met ICM toevoegen
* Regels voor binnenkomende verbindingen toohello Windows Firewall-configuratie voor Hallo TCP/IP-poorten die worden gebruikt toocommunicate Hello ICM toevoegen

Voor een geautomatiseerde geïmporteerd met alle correcties beschikbaar, is het raadzaam tooperiodically Hallo correctie verzameling SAP-notitie van toepassing tooyour SAP versie toe te passen:

* [1558958]
* [1619967]
* [1882376]

Meer informatie over DBA Cockpit voor SAP-as-omgeving vindt u in de volgende opmerkingen bij de SAP Hallo:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Overwegingen voor back-up/herstel voor SAP-as-omgeving
Uw back-upmethode moet worden gecontroleerd bij het implementeren van SAP-as-omgeving in Azure. Zelfs als het Hallo-systeem is niet een productieve systeem, Hallo SAP-database gehost door SAP-as-omgeving moet een back-up regelmatig. Omdat Azure Storage drie afbeeldingen houdt, is nu een back-up minder belangrijke toocompensating ten opzichte van een crash van de opslag. Hello primaire reden voor het onderhouden van een juiste back-up en herstel plan is meer die u logische/handmatige fouten compenseren kunt door punt in tijd herstelfuncties te bieden. Zodat het Hallo-doel is tooeither gebruik back-ups toorestore Hallo database terug tooa bepaalde punt in tijd of toouse Hallo back-ups in Azure tooseed een ander systeem Hallo bestaande database kopiëren. Bijvoorbeeld, u kan overzetten van een 2-Tier SAP configuratie tooa 3-Laagse setup van system Hallo dezelfde systeem door het herstellen van een back-up.

Back-up en terugzetten van een database in Azure werkt Hallo dezelfde manier als er een lokale is. Zie SAP-opmerkingen:

* [1588316]
* [1585981]

voor informatie over maken dump configuraties en planning back-ups. Afhankelijk van uw strategie en behoeften kunt u configureren database en logboekbestanden dumpen toodisk naar een bestaande VHD's hello of een extra VHD voor back-up Hallo toevoegen.  tooreduce hello gevaar gegevensverlies in geval van een fout is aanbevolen toouse een VHD waarin er geen database map/bestand zich bevindt.

Compressie SAP-as-omgeving biedt naast gegevens- en LOB ook back-compressie. toooccupy minder ruimte met Hallo-database en logboekbestanden dumpbestanden voor deze toouse back-compressie wordt aanbevolen. Zie SAP-notitie [1588316] voor meer informatie. Comprimeren Hallo back-up is ook cruciaal tooreduce Hallo hoeveelheid gegevens toobe overgedragen als u van plan bent toodownload back-ups of VHD's met back-dumps van hello Azure virtuele Machine tooon-premises.

Gebruik geen hello Azure VM tijdelijke ruimte mnt of /mnt/resource als doel-dump database of logboekbestanden.

#### <a name="performance-considerations-for-backupsrestores"></a>Prestatie-overwegingen voor back-ups/herstelacties
Prestaties van back-up/herstel is net zoals in de bare-metal implementaties, afhankelijk van hoeveel volumes parallel kunnen worden gelezen en welke Hallo doorvoer van deze volumes mogelijk. Bovendien speelt Hallo CPU-verbruik door back-compressie gebruikt een belangrijke rol op virtuele machines met slechts komen too8 CPU threads. Daarom kan een aannemen:

* Hallo minder Hallo aantal virtuele harde schijven gebruikt toostore Hallo databaseapparaten Hallo Hallo kleinere totale doorvoer in lezen
* Hallo kleinere Hallo aantal threads in Hallo VM CPU, Hallo ernstige Hallo gevolgen van het back-compressie
* Hallo minder doelen (Linux-software RAID, VHD's) toowrite Hallo back-up naar, Hallo minder Hallo doorvoer

tooincrease hello aantal doelen toowrite toothere zijn twee opties die kunnen worden gebruikt/gecombineerd afhankelijk van uw behoeften:

* De back-up doelvolume Hallo striping over meerdere gekoppelde VHD's in een volgorde tooimprove hello IOPS doorvoer op dat volume striped
* Maken van een configuratie dump op niveau SAP-as-omgeving maakt gebruik van meer dan één doel directory toowrite Hallo dump naar

Eerder in deze handleiding is een volume striping over meerdere gekoppelde VHD's beschreven. Voor meer informatie over het gebruik van meerdere directory's in de configuratie van de dump Hallo SAP-as-omgeving raadpleegt u toohello documentatie over de opgeslagen Procedure sp_config_dump die gebruikte toocreate Hallo dump configuratie op Hallo [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Herstel na noodgevallen met virtuele machines in Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Gegevensreplicatie met SAP Sybase replicatie Server
Hallo biedt SAP Sybase Replication Server (SRS) SAP-as-omgeving een warme stand-by-oplossing tootransfer transacties tooa verafgelegen databaselocatie asynchroon.

Hallo-installatie en de werking van SRS werkt ook in een virtuele machine in Azure Services op virtuele Machine wordt gehost als er een lokale functioneel.

As-omgeving HADR via SAP replicatie Server wordt op dit moment niet ondersteund. Het kan worden getest met en uitgebracht voor Microsoft Azure-platforms in toekomstige Hallo.

## <a name="specifics-toooracle-database-on-windows"></a>Specificaties tooOracle Database in Windows
Sinds midyear 2013, wordt Oracle-software ondersteund door Oracle toorun op Microsoft Windows Hyper-V en Azure. Lees dit artikel tooget meer informatie over algemene ondersteuning van Windows Hyper-V en Azure door Oracle Hallo: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Na algemene Hallo-ondersteuning wordt ook specifieke scenario Hallo van SAP-toepassingen die gebruik van Oracle-Databases ondersteund. Details zijn met de naam in dit gedeelte van het Hallo-document.

### <a name="oracle-version-support"></a>Ondersteuning voor Oracle-versie
Alle informatie over de Oracle-versies en bijbehorende OS-versies die worden ondersteund voor SAP uitgevoerd op Oracle op Azure Virtual Machines vindt u in de volgende SAP-notitie Hallo [2039619]

Algemene informatie over het uitvoeren van SAP Business Suite op Oracle vindt u op SCN: <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Oracle-configuratie-instructies voor SAP-installaties in virtuele machines in Azure
#### <a name="storage-configuration"></a>Opslagconfiguratie
Slechts één exemplaar Oracle met NTFS-geformatteerde schijven wordt ondersteund. Alle databasebestanden moeten worden opgeslagen op Hallo NTFS-bestandssysteem op basis van schijven van de VHD. Deze virtuele harde schijven zijn gekoppeld toohello virtuele machine van Azure en zijn gebaseerd op de pagina Azure BLOB-opslag (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Elk soort netwerkstations of externe shares zoals Azure Bestandsservices:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-connections-to-Microsoft-Azure-Files.aspx>

zijn **niet** ondersteund voor Oracle-databasebestanden!

Met behulp van Azure VHD's op basis van de Azure-blobopslag pagina Hallo verklaringen in dit document in hoofdstuk [in cache opslaan voor virtuele machines en VHD's] [ dbms-guide-2.1] en [Microsoft Azure Storage] [ dbms-guide-2.3] toodeployments Hello Oracle-Database ook van toepassing.

Zoals uitgelegd eerder in Hallo algemene deel van Hallo document, bestaan quota voor IOPS-doorvoer voor virtuele harde schijven van Azure. Hallo exacte quota's zijn afhankelijk van Hallo VM type gebruikt. Een lijst met VM-typen met hun quota vindt [hier][virtual-machines-sizes]

tooidentify hello ondersteunde typen van de virtuele machine in Azure, raadpleegt u tooSAP Opmerking [1928533]

Zolang Hallo vereisten voldoet aan de huidige IOPS quotum per schijf hello, het is mogelijk toostore alle Hallo DB-bestanden op slechts één Azure VHD gekoppeld.

Als meer IOPS nodig zijn, is het raadzaam toouse venster opslaggroepen (alleen beschikbaar in Windows Server 2012 en hoger) of Windows striping voor Windows 2008 R2 toocreate één groot logisch apparaat via meerdere gekoppelde VHD-schijven. Zie ook hoofdstuk [Software RAID] [ dbms-guide-2.2] van dit document. Deze aanpak vereenvoudigt Hallo beheer overhead toomanage Hallo schijfruimte vrij en voorkomt Hallo inspanning toomanually bestanden verdelen over meerdere gekoppelde VHD's.

#### <a name="backup--restore"></a>Back-up en herstellen
Voor back-up / functionaliteit herstellen, Hallo SAP-Brazilië * hulpprogramma's voor Oracle worden ondersteund Hallo dezelfde manier als op standaard Windows-serverbesturingssystemen en Hyper-V. Oracle Recovery Manager (RMAN) wordt ook ondersteund voor back-ups toodisk en het terugzetten van de schijf.

#### <a name="high-availability"></a>Hoge beschikbaarheid
[comment]: <> (koppeling verwijst tooASM)
Oracle Data Guard wordt ondersteund voor hoge beschikbaarheid en noodherstel. Meer informatie vindt u in [dit] [ virtual-machines-windows-classic-configure-oracle-data-guard] documentatie.

#### <a name="other"></a>Overige
Andere algemene onderwerpen, zoals Beschikbaarheidssets van Azure of SAP bewaking zoals beschreven in Hallo eerste drie hoofdstukken van dit document voor implementaties van virtuele machines met Hallo Oracle-Database ook van toepassing.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Specifieke informatie voor Hallo SAP MaxDB Database in Windows
### <a name="sap-maxdb-version-support"></a>SAP-MaxDB versie-ondersteuning
SAP momenteel ondersteunt SAP MaxDB versie 7,9 voor gebruik met producten op basis van een SAP NetWeaver in Azure. Alle updates voor SAP MaxDB server of JDBC en ODBC-stuurprogramma's toobe gebruikt met producten op basis van een SAP NetWeaver vindt uitsluitend via Hallo SAP Service Marketplace van <https://support.sap.com/swdc>.
Algemene informatie over het uitvoeren van SAP NetWeaver op SAP MaxDB kan worden gevonden op <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Microsoft Windows-versies en de Azure VM-typen ondersteund voor SAP MaxDB DBMS
toofind hello ondersteund Microsoft Windows-versie voor SAP MaxDB DBMS in Azure, Zie:

* [SAP Product beschikbaarheid Matrix (PAM)][sap-pam]
* SAP-notitie [1928533]

Het is raadzaam toouse Hallo nieuwste versie van besturingssysteem Hallo Microsoft Windows, Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Beschikbare SAP MaxDB documentatie
U kunt Hallo bijgewerkt lijst van SAP MaxDB documentatie vinden in Hallo SAP-notitie na [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP MaxDB configuratie-instructies voor SAP-installaties in virtuele machines in Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Opslagconfiguratie
Aanbevolen procedures van de Azure-opslag voor SAP MaxDB Volg Hallo algemene aanbevelingen die worden vermeld in hoofdstuk [structuur van een implementatie RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Net als andere databases heeft SAP MaxDB ook gegevens en logboekbestanden. Hallo juiste term is echter in SAP MaxDB terminologie 'volume' (geen ' file'). Er zijn bijvoorbeeld SAP MaxDB gegevensvolumes en logboekvolumes. Verwar deze voor OS schijfvolumes niet.
>
>

Kort gezegd hebt u:

* Stel hello Azure storage-account waarin Hallo SAP MaxDB gegevens en logboekbestanden volumes (dat wil zeggen-bestanden) te**lokaal redundante opslag (LRS)** zoals opgegeven in hoofdstuk [Microsoft Azure Storage] [ dbms-guide-2.3].
* Afzonderlijke Hallo i/o-pad voor SAP MaxDB gegevensvolumes (dat wil zeggen-bestanden) van Hallo i/o-pad voor logboekbestanden-volumes (dat wil zeggen-bestanden). Dit betekent dat SAP MaxDB gegevensvolumes (dat wil zeggen-bestanden) geïnstalleerd op één logisch station toobe hebt en SAP MaxDB logboekvolumes (dat wil zeggen-bestanden) geïnstalleerd op een andere logische schijf toobe hebt.
* Stel Hallo juiste bestandscache voor elke Azure-blob, afhankelijk van of u deze gebruiken voor SAP MaxDB gegevensbestand of logboekbestand volumes (dat wil zeggen-bestanden) en of het gebruiken van Azure Standard of Premium-opslag voor Azure, zoals beschreven in hoofdstuk [in cache opslaan voor virtuele machines] [ dbms-guide-2.1].
* Zolang Hallo huidige IOPS quotum per schijf Hallo vereisten voldoet, is mogelijk toostore alle Hallo gegevensvolumes op een enkele gekoppelde Azure-VHD en ook alle logboekvolumes voor database opslaan op een andere één gekoppelde Azure-VHD.
* Als meer IOPS en/of ruimte nodig zijn, is het raadzaam toouse Microsoft venster opslaggroepen (alleen beschikbaar in Microsoft Windows Server 2012 en hoger) of Microsoft Windows striping voor Microsoft Windows 2008 R2 toocreate één grote logisch apparaat via meerdere gekoppelde VHD-schijven. Zie ook hoofdstuk [Software RAID] [ dbms-guide-2.2] van dit document. Deze aanpak vereenvoudigt Hallo beheer overhead toomanage Hallo schijfruimte vrij en vermijdt Hallo inspanning van bestanden handmatig over meerdere gekoppelde VHD's verdeeld.
* Voor Hallo hoogste IOPS vereisten, kunt u Azure Premium-opslag gebruiken die beschikbaar zijn op DS-serie en GS-serie virtuele machines is.

![Configuratie van Azure IaaS VM voor SAP MaxDB DBMS verwijzing][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Back-up en herstel
Bij het SAP MaxDB implementeren in Azure, moet u uw back-upmethode doornemen. Zelfs als het Hallo-systeem is niet een productieve systeem, Hallo SAP-database gehost door SAP MaxDB moet een back-up regelmatig. Omdat Azure Storage drie afbeeldingen houdt, is nu een back-up minder belangrijk in termen van bescherming van uw systeem tegen storingen van opslag en belangrijker operationele of administratieve fouten. Hallo primaire reden voor het onderhouden van een goede back-up en herstel plannen is zodat u logische of handmatige fouten compenseren kunt dankzij de punt in tijd herstelfuncties. Zodat het Hallo-doel is tooeither gebruik back-ups toorestore Hallo database tooa bepaalde punt in tijd of toouse Hallo back-ups in Azure tooseed een ander systeem Hallo bestaande database kopiëren. Bijvoorbeeld, u kan overzetten van een laag 2 SAP configuratie tooa 3-laagse setup van system Hallo dezelfde systeem door het herstellen van een back-up.

Back-up en terugzetten van een database in Azure werkt Hallo dezelfde manier als voor on-premises systemen, zodat u standaard SAP MaxDB kunt back-up/herstel hulpprogramma's die worden beschreven in een van de Hallo SAP MaxDB documentatie documenten die worden vermeld in SAP-notitie [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Prestatie-overwegingen voor back-up en herstel
Prestaties van back-up en herstel is net zoals in de bare-metal implementaties, afhankelijk van hoeveel volumes in parallelle instructies en Hallo doorvoer van deze volumes kunnen worden gelezen. Hallo CPU-verbruik gebruikt door de back-compressie kan een belangrijke rol bovendien afspelen op virtuele machines met komen too8 CPU threads. Daarom kan een aannemen:

* Hallo minder Hallo aantal gebruikte VHD's toostore Hallo databaseapparaten, Hallo lagere Hallo algehele doorvoer lezen
* Hallo kleinere Hallo aantal threads in Hallo VM CPU, Hallo ernstige Hallo gevolgen van het back-compressie
* Hallo minder doelen (Stripe-mappen, VHD's) toowrite Hallo back-up, Hallo lagere Hallo doorvoer

tooincrease Hallo aantal toowrite naar doel, zijn er twee opties die u, mogelijk in combinatie, afhankelijk van uw behoeften gebruiken kunt:

* Afzonderlijke volumes dat voor back-up
* De back-up doelvolume Hallo striping over meerdere gekoppelde VHD's in een volgorde tooimprove hello IOPS doorvoer op dat schijfvolume striped
* Apparaten voor afzonderlijke specifieke logische schijf hebben:
  * SAP-MaxDB back-upvolumes (dat wil zeggen-bestanden)
  * SAP-MaxDB gegevensvolumes (dat wil zeggen-bestanden)
  * SAP-MaxDB logboekvolumes (dat wil zeggen-bestanden)

Een volume striping over meerdere gekoppelde VHD's zijn besproken eerder in hoofdstuk [Software RAID] [ dbms-guide-2.2] van dit document.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Andere
Andere algemene onderwerpen, zoals Beschikbaarheidssets van Azure of SAP controle zijn ook van toepassing zoals beschreven in Hallo eerste drie hoofdstukken van dit document voor implementaties van virtuele machines met Hallo MaxDB SAP-database.
Andere SAP MaxDB-specifieke instellingen transparante tooAzure VM's en worden beschreven in verschillende documenten die worden vermeld in SAP-notitie [767598 ] en in deze SAP-opmerkingen:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Specifieke informatie voor SAP liveCache in Windows
### <a name="sap-livecache-version-support"></a>SAP liveCache versie-ondersteuning
Minimale versie van SAP liveCache ondersteund in Azure Virtual Machines **SAP LC/LCAPPS 10.0 SP 25** inclusief **liveCache 7.9.08.31** en **LCA-Build 25**, vrijgegeven voor **EhP 2 voor SAP SCM 7.0** en hoger.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Microsoft Windows-versies en de Azure VM-typen ondersteund voor SAP liveCache DBMS
toofind hello ondersteund Microsoft Windows-versie voor SAP liveCache in Azure, Zie:

* [SAP Product beschikbaarheid Matrix (PAM)][sap-pam]
* SAP-notitie [1928533]

Het is raadzaam toouse Hallo nieuwste versie van besturingssysteem Hallo Microsoft Windows, Microsoft Windows 2012 R2.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP liveCache configuratie-instructies voor SAP-installaties in Azure VM 's
#### <a name="recommended-azure-vm-types"></a>Aanbevolen Azure VM-typen
Heeft een grote invloed op de prestaties van SAP liveCache zoals SAP liveCache is een toepassing met grote berekeningen, Hallo bedrag en de snelheid van het RAM-geheugen en CPU.

Voor hello Azure VM die worden ondersteund door SAP (SAP-notitie [1928533]), alle virtuele CPU-resources toegewezen toohello VM worden ondersteund door toegewijde fysieke CPU-bronnen Hallo hypervisor. Er is geen overmatige inrichting (en dus concurrentie voor CPU-bronnen) plaatsvindt.

Op deze manier voor alle virtuele Azure-machine exemplaar typen ondersteund door SAP, Hallo VM geheugen is 100% toegewezen toohello fysiek geheugen – overmatige inrichting (te veel streven), bijvoorbeeld wordt niet gebruikt.

Van dit perspectief is het raadzaam toouse Hallo nieuwe D-reeks of virtuele machine van Azure Active Directory-serie (in combinatie met Azure Premium-opslag) type, aangezien de snellere processors 60% dan Hallo A-serie. Voor Hallo hoogste RAM-geheugen en CPU-belasting, kunt u G-serie en GS-serie (in combinatie met Azure Premium-opslag) virtuele machines met Hallo nieuwste Intel Xeon® processor E5 v3-familie tweemaal Hallo geheugen en vier keer Hallo Solid-State opslag drive (SSD's) van Hallo D / DS-serie.

#### <a name="storage-configuration"></a>Opslagconfiguratie
Zoals SAP liveCache is gebaseerd op MaxDB SAP-technologie, alle Azure-opslag aanbevolen werkwijzen besproken in hoofdstuk wordt vermeld voor SAP MaxDB Hallo [opslagconfiguratie] [ dbms-guide-8.4.1] zijn ook geldig voor SAP liveCache.

#### <a name="dedicated-azure-vm-for-livecache"></a>Toegewezen virtuele machine van Azure voor liveCache
Zoals SAP liveCache wordt intensief verwerkingskracht gebruikt, voor productief gebruik is het raadzaam toodeploy op een specifieke virtuele Machine van Azure.

![Virtuele machine van Azure voor liveCache voor productief gebruiksvoorbeeld Dedicated][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Back-up en herstel
Back-up en herstel, met inbegrip van prestatie-overwegingen al worden beschreven in de desbetreffende SAP MaxDB hoofdstukken Hallo [back-up en herstel] [ dbms-guide-8.4.2] en [prestatie-overwegingen voor back-up maken en terugzetten][dbms-guide-8.4.3].

#### <a name="other"></a>Overige
Andere algemene onderwerpen al worden beschreven in Hallo relevante SAP MaxDB [dit] [ dbms-guide-8.4.4] hoofdstuk.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Specifieke informatie voor SAP inhoudsserver op Windows hello
Hallo SAP Content Server is de inhoud van een afzonderlijke, op basis van een server onderdeel toostore zoals elektronische documenten in verschillende indelingen. Hallo SAP inhoudsserver wordt geleverd door de ontwikkeling van technologie en toobe gebruikt tussen verschillende toepassingen voor alle SAP-toepassingen is. Het is geïnstalleerd op een afzonderlijk systeem. Inhoud is training materiaal en documentatie uit Knowledge datawarehouse of technische tekeningen die afkomstig zijn van Hallo mySAP PLM Document Management-systeem.

### <a name="sap-content-server-version-support"></a>Ondersteuning voor SAP inhoudsserver versie
SAP momenteel ondersteunt:

* **SAP-inhoudsserver** met versie **6.50 (en hoger)**
* **SAP MaxDB versie 7,9**
* **Microsoft IIS (Internet Information Server) versie 8.0 (en hoger)**

Het is raadzaam toouse Hallo nieuwste versie van de Content Server SAP, dat op Hallo moment van publicatie van dit document **6.50 SP4**, en de nieuwste versie van Hallo **Microsoft IIS 8.5**.

Controleert Hallo laatste ondersteunde versies van inhoud SAP-Server en Microsoft IIS in Hallo [SAP Product beschikbaarheid Matrix (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Microsoft Windows en de Azure VM-typen ondersteund voor SAP-inhoudsserver
toofind uit de ondersteunde Windows-versie voor Content SAP-Server op Azure, Zie:

* [SAP Product beschikbaarheid Matrix (PAM)][sap-pam]
* SAP-notitie [1928533]

Het is raadzaam toouse Hallo nieuwste versie van Microsoft Windows, dat op Hallo moment van publicatie van dit document **Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>SAP inhoudsserver configuratie-instructies voor SAP-installaties in virtuele machines in Azure
#### <a name="storage-configuration"></a>Opslagconfiguratie
Als u de inhoudsserver SAP toostore bestanden in Hallo MaxDB SAP-database configureert, alle Azure-opslag best practices aanbeveling in hoofdstuk wordt vermeld voor SAP MaxDB [opslagconfiguratie] [ dbms-guide-8.4.1] zijn ook is alleen geldig voor Hallo SAP inhoudsserver scenario.

Als u de inhoudsserver SAP toostore bestanden in het bestandssysteem Hallo configureert, is het aanbevolen toouse een specifieke logische schijf. Met opslagruimten kunt u tooalso toename logische schijfgrootte en de doorvoer IOP's, zoals beschreven in in hoofdstuk [Software RAID][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>SAP inhoudsserver locatie
Inhoud SAP-Server is geïmplementeerd in Hallo toobe dezelfde Azure-regio en Azure VNET waarop Hallo SAP-systeem wordt geïmplementeerd. U bent gratis toodecide of u wilt toodeploy inhoud SAP-Server-onderdelen op een specifieke Azure virtuele machine of op Hallo dezelfde virtuele machine waarop Hallo SAP-systeem wordt uitgevoerd.

![Speciale Azure VM voor SAP-inhoudsserver][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>SAP-cachelocatie Server
Hallo SAP-Cache-Server is een extra server gebaseerde onderdeel tooprovide toegang too(cached) documenten lokaal. Hallo SAP-Cache-Server in de cache opgeslagen Hallo documenten van een inhoudsserver van SAP. Dit is toooptimize netwerkverkeer als documenten toobe meer dan één keer worden opgehaald vanaf verschillende locaties hebben. Hallo regel heeft die Hallo SAP-cacheserver toobe fysiek sluiten toohello client die toegang heeft tot Hallo SAP-cacheserver.

Hier hebt u twee opties:

1. **Client is een back-end SAP-systeem** als een back-end SAP-systeem geconfigureerd tooaccess inhoudsserver SAP is, dat SAP-systeem is een client. Als zowel de SAP-systeem en de inhoud SAP-Server zijn geïmplementeerd in Hallo dezelfde Azure-regio – in Hallo dezelfde Azure-datacenter – ze fysiek sluiten zijn tooeach andere. Daarom is er geen noodzaak toohave een speciale Server voor SAP-Cache. SAP-gebruikersinterface (SAP-GUI of web browser)-clients toegang Hallo SAP-systeem rechtstreeks en hello SAP-systeem haalt documenten uit Hallo SAP-inhoudsserver.
2. **Client is een webbrowser die lokale** Hallo SAP inhoudsserver geconfigureerde toobe rechtstreeks toegang verkregen door de webbrowser Hallo kan zijn. In dit geval is een webbrowser op het lokale met een client Hallo SAP-inhoudsserver. On-premises datacentrum en Azure-datacenter worden geplaatst op verschillende fysieke locaties (in het ideale geval sluiten tooeach andere). Uw on-premises datacentrum is verbonden tooAzure via Azure Site-naar-Site VPN- of ExpressRoute. Hoewel beide opties veilige VPN-netwerk verbinding tooAzure bieden, site-naar-site-netwerkverbinding een SLA netwerk bandbreedte en de latentie tussen Hallo on-premises datacentrum en hello Azure-datacenter niet aangeboden. toospeed up toegang toodocuments, kunt u een van de volgende Hallo kunt doen:
   1. SAP-cacheserver on-premises installeert, sluit u toohello lokale webbrowser (optie op [dit] [ dbms-guide-900-sap-cache-server-on-premises] afbeelding)
   2. Configureer Azure ExpressRoute, met een hoge en lage latentie speciaal netwerkverbinding tussen on-premises datacentrum en Azure-datacenter.

![Optie tooinstall SAP-cacheserver lokale][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Back-up en herstellen
Als u Hallo SAP inhoudsserver toostore bestanden in Hallo MaxDB SAP-database configureert, de back-up/herstel procedure- en Prestatieoverwegingen Hallo al worden beschreven in SAP MaxDB hoofdstuk [back-up en herstel] [ dbms-guide-8.4.2] en hoofdstuk [Prestatieoverwegingen voor back-up en herstel][dbms-guide-8.4.3].

Als u Hallo SAP inhoudsserver toostore bestanden in het bestandssysteem Hallo configureert, is een optie tooexecute handmatige back-up/herstel van de hele bestandsstructuur Hallo waarin Hallo documenten bevinden. Vergelijkbare tooSAP MaxDB back-up/herstel, het is aanbevolen toohave een toegewezen schijfvolume voor back-doel.

#### <a name="other"></a>Overige
Andere inhoudsserver SAP-specifieke instellingen transparante tooAzure VM's en in verschillende documenten en -opmerkingen bij de SAP worden beschreven:

* <https://service.SAP.com/contentserver>
* SAP-notitie [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Specificaties tooIBM DB2 voor LUW in Windows
U kunt eenvoudig uw bestaande SAP-toepassing uitgevoerd op IBM DB2 voor Linux, UNIX- en Windows (LUW) tooAzure virtuele machines migreren met Microsoft Azure. Met SAP op IBM DB2 voor LUW, beheerders en ontwikkelaars kunnen nog steeds gebruiken Hallo dezelfde ontwikkelings- en hulpprogramma's die beschikbaar zijn op lokale.
Algemene informatie over het uitvoeren van SAP Business Suite op IBM DB2 voor LUW vindt u SAP Community netwerk (SCN) op Hallo <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Zie voor meer informatie en updates over SAP op DB2 voor LUW op Azure, SAP-notitie [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 voor Linux, UNIX- en ondersteuning voor Windows-versie
SAP op IBM DB2 voor LUW op Services van Microsoft Azure-virtuele Machine wordt ondersteund vanaf DB2 versie 10.5.

Raadpleeg voor informatie over ondersteunde SAP-producten en typen van de virtuele machine van Azure tooSAP Opmerking [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>IBM DB2 voor Linux, UNIX- en Windows-configuratie-instructies voor SAP-installaties in virtuele machines in Azure
#### <a name="storage-configuration"></a>Opslagconfiguratie
Alle databasebestanden moeten worden opgeslagen op Hallo NTFS-bestandssysteem op basis van schijven van de VHD. Deze virtuele harde schijven zijn gekoppelde toohello virtuele machine van Azure en zijn gebaseerd in Azure pagina-BLOB-opslag (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Elk soort netwerkstations of externe shares zijn hello Azure Bestandsservices na **niet** ondersteund voor databasebestanden:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-connections-to-Microsoft-Azure-Files.aspx>

Als u van Azure VHD's op basis van de pagina Azure BLOB-opslag gebruikmaakt, Hallo verklaringen in dit document in hoofdstuk [structuur van een implementatie RDBMS] [ dbms-guide-2] toodeployments Hello IBM DB2 ook van toepassing op LUW De database.

Zoals uitgelegd eerder in Hallo algemene deel van Hallo document, bestaan quota voor IOPS-doorvoer voor virtuele harde schijven van Azure. Hallo exacte quota, is afhankelijk van Hallo VM type gebruikt. Een lijst met VM-typen met hun quota vindt [hier][virtual-machines-sizes]

Zolang Hallo huidige IOPS quotum per schijf voldoende is, dat het is mogelijk toostore die alle databasebestanden op Hallo gekoppelde wordt slechts één Azure-VHD.

Voor prestaties ook verwijzen toochapter 'veiligheid en prestaties overwegingen voor Database gegevensmappen' in de installatiehandleidingen SAP aandachtspunten.

U kunt ook kunt u Windows Storage Pools (alleen beschikbaar in Windows Server 2012 en hoger) of Windows striping voor Windows 2008 R2 als beschreven in hoofdstuk [Software RAID] [ dbms-guide-2.2] van dit document toocreate één groot logisch apparaat via meerdere gekoppelde VHD-schijven.
Hallo-schijven met Hallo DB2 opslagpaden voor uw mappen sapdata en saptmp, moet u een fysieke Schijfsectorgrootte van 512 KB. Wanneer u Windows-opslaggroepen, moet u Hallo opslaggroepen handmatig via de opdrachtregelinterface met Hallo parameter '-LogicalSectorSizeDefault '. Zie voor meer informatie <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Back-up maken/terugzetten
Hallo back-up/herstel functionaliteit voor IBM DB2 voor LUW wordt ondersteund Hallo dezelfde manier als op standaard Windows-serverbesturingssystemen en Hyper-V.

U moet ervoor zorgen dat u beschikken over een geldige database back-upstrategie.

Net zoals in de bare-metal implementaties afhankelijk back-up/herstel prestaties van hoeveel volumes parallel kunnen worden gelezen en welke Hallo doorvoer van deze volumes mogelijk. Bovendien speelt Hallo CPU-verbruik door back-compressie gebruikt een belangrijke rol op virtuele machines met slechts komen too8 CPU threads. Daarom kan een aannemen:

* Hallo minder Hallo aantal virtuele harde schijven gebruikt toostore Hallo databaseapparaten Hallo Hallo kleinere totale doorvoer in lezen
* Hallo kleinere Hallo aantal threads in Hallo VM CPU, Hallo ernstige Hallo gevolgen van het back-compressie
* Hallo minder doelen (Stripe-mappen, VHD's) toowrite Hallo back-up, Hallo lagere Hallo doorvoer

tooincrease hello doelen toowrite naar, twee opties kunnen worden gebruikt/gecombineerd afhankelijk van uw behoeften:

* De back-up doelvolume Hallo striping over meerdere gekoppelde VHD's in een volgorde tooimprove hello IOPS doorvoer op dat volume striped
* Met behulp van meer dan één doel directory toowrite Hallo back-up

#### <a name="high-availability-and-disaster-recovery"></a>Hoge beschikbaarheid en herstel na noodgevallen
Microsoft Cluster Server (MSCS) wordt niet ondersteund.

DB2 herstel na noodgevallen voor hoge beschikbaarheid (HADR) wordt ondersteund. Als Hallo virtuele machines van de HA-configuratie Hallo naamomzetting werkt hebt, wordt niet Hallo-instellingen in Azure verschillen van elke instelling die lokaal wordt uitgevoerd. Het is niet raadzaam toorely op alleen IP-adresomzetting.

Gebruik geen Azure Store Geo-replicatie. Raadpleeg voor meer informatie toochapter [Microsoft Azure Storage] [ dbms-guide-2.3] en hoofdstuk [hoge beschikbaarheid en herstel na noodgevallen met Azure Virtual machines] [ dbms-guide-3].

#### <a name="other"></a>Overige
Andere algemene onderwerpen, zoals Beschikbaarheidssets van Azure of SAP bewaking van toepassing zoals beschreven in Hallo eerste drie hoofdstukken van dit document voor andere implementaties van virtuele machines met IBM DB2 voor LUW.

Raadpleeg ook toochapter [algemene SQL Server voor SAP op Azure samenvatting][dbms-guide-5.8].
