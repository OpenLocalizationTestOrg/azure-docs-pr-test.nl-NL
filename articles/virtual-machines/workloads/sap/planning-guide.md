---
title: Virtuele Machines aaaAzure planning en implementatie voor SAP NetWeaver | Microsoft Docs
description: Azure virtuele Machines, planning en implementatie voor SAP NetWeaver
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>Azure virtuele Machines, planning en implementatie voor SAP NetWeaver
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure kunnen bedrijven tooacquire berekenings- en bronnen in de minimale tijd zonder langdurige inkoop cycli. Virtuele Machines in Azure bedrijven toestaan toodeploy klassieke toepassingen, zoals SAP NetWeaver toepassingen in Azure gebaseerde en de betrouwbaarheid en beschikbaarheid zonder verdere beschikbaar lokale uitbreiden. Virtuele Machine van Azure-Services biedt ook ondersteuning voor cross-premises connectiviteit, welke kunnen bedrijven tooactively Azure Virtual Machines integreren in hun lokale domein, hun Privéclouds en hun liggend SAP-systeem.
Dit technisch document worden beschreven Hallo basisprincipes van Microsoft Azure virtuele Machine en biedt een overzicht van de overwegingen voor planning en implementatie voor SAP NetWeaver installaties in Azure en als zodanig Hallo document tooread moet zijn voordat u begint werkelijke implementaties van SAP NetWeaver op Azure.
Hallo papier aanvullingen hello SAP-documentatie voor installatie- en SAP-opmerkingen Hallo primaire bronnen voor installaties en implementaties van software op SAP vertegenwoordigen gegeven platforms.

## <a name="summary"></a>Samenvatting
Cloudcomputing is een veelgebruikte term die meer belang binnen Hallo IT-sector van kleine bedrijven up toolarge en meertalige ondernemingen winnen wordt.

Microsoft Azure is Hallo Services Cloudplatform van Microsoft, die een breed scala aan nieuwe mogelijkheden biedt. Klanten zijn nu kunnen toorapidly leveren en intrekken toepassingen als een service in de cloud hello, zodat ze niet beperkt tootechnical of budget beperkingen zijn. In plaats van de tijd en geld investeren in hardware-infrastructuur, bedrijven kunnen zich concentreren op Hallo toepassing bedrijfsprocessen en de voordelen voor klanten en gebruikers.

Met Microsoft Azure-services voor virtuele machines biedt Microsoft een uitgebreid IaaS-platform (Infrastructure as a Service). SAP NetWeaver-toepassingen worden ondersteund op virtuele Azure-machines (IaaS). Dit technisch document wordt beschreven hoe tooplan en implementeer SAP NetWeaver toepassingen binnen Microsoft Azure als Hallo platform keuze gebaseerde.

Hallo papier zelf is gericht op twee belangrijke aspecten:

* het eerste deel Hallo beschrijft twee ondersteunde implementaties voor SAP NetWeaver op basis van toepassingen in Azure. Hierin worden ook algemene verwerking van Azure met SAP-implementaties in gedachten.
* Hallo tweede onderdeel details Hallo twee verschillende scenario's beschreven in het eerste deel Hallo implementeren.

Voor aanvullende bronnen Zie hoofdstuk [Resources] [ planning-guide-1.2] in dit document.

### <a name="definitions-upfront"></a>Definities van tevoren
We gebruiken Hallo volgende voorwaarden in Hallo-document:

* IaaS: Infrastructuur als een Service
* PaaS: Platform as a Service
* SaaS: Software als een Service
* ARM: Azure Resource Manager
* SAP-onderdeel: een afzonderlijke SAP toepassing zoals ECC, BW, oplossing Manager of EP is geplaatst.  SAP-onderdelen kunnen worden gebaseerd op traditionele ABAP of Java-technologieën of een NetWeaver op basis van toepassing zoals zakelijke objecten.
* SAP-omgeving: een of meer onderdelen voor SAP logisch zijn gegroepeerd tooperform een zakelijke functie zoals ontwikkeling, QAS, Training, DR of productie.
* SAP liggend: Dit verwijst toohello gehele SAP activa in een klant IT Liggend. Hallo SAP liggend bevat alle productie en niet-productieve omgevingen.
* SAP-systeem: Hallo combinatie van laag DBMS en toepassingslaag van bijvoorbeeld een SAP ERP-ontwikkelsysteem, SAP BW testsysteem, productiesysteem SAP CRM, enzovoort... In implementaties van Azure, is het niet ondersteunde toodivide deze twee lagen tussen on-premises en Azure. Dit betekent dat er ofwel een SAP-systeem lokale geïmplementeerd of deze is geïmplementeerd in Azure. U kunt echter verschillende systemen Hallo van een liggend SAP in Azure of on-premises implementeren. U kunt bijvoorbeeld Hallo SAP CRM ontwikkeling en tests systemen in Azure implementeren maar SAP CRM productie system lokale Hallo.
* Cloud-implementatie: een implementatie waarbij hello Azure-abonnement niet is verbonden via een site-naar-site of ExpressRoute-verbinding toohello lokale netwerkinfrastructuur. Gemeenschappelijk Azure-documentatie dergelijke implementaties worden ook beschreven als 'Cloud-Only'-implementaties. Virtuele Machines die worden geïmplementeerd met deze methode toegankelijk zijn via internet Hallo en een openbare IP-adres en/of een openbare DNS-naam toegewezen toohello virtuele machines in Azure. Voor Microsoft Windows hello lokale Active Directory (AD) en DNS is niet uitgebreid tooAzure in dergelijke implementaties. Daarom maken Hallo VM's geen deel uit van Hallo op lokale Active Directory. Hetzelfde geldt voor Linux-implementaties gebruikt, bijvoorbeeld OpenLDAP + Kerberos.

> [!NOTE]
> Cloud-implementatie in dit document wordt gedefinieerd als volledige SAP landschappen uitsluitend in Azure zonder extensie van Active Directory worden uitgevoerd / OpenLDAP of naamomzetting van de van on-premises in openbare cloud. Alleen in de cloud-configuraties worden niet ondersteund voor productie SAP-systemen of -configuraties waar nodig toobe gebruikt tussen SAP-systemen die worden gehost op Azure en bronnen die zich lokaal SAP stm of andere lokale bronnen.
>
>

* Cross-premises: Beschrijft een scenario waarin VM's zijn geïmplementeerde tooan Azure-abonnement met site-naar-site meerdere locaties of ExpressRoute-verbinding tussen Hallo lokale clientresources en Azure. Gemeenschappelijk Azure-documentatie, dit soort implementaties worden ook beschreven als cross-premises scenario's. Hallo reden voor Hallo verbinding is tooextend on-premises domeinen, on-premises Active Directory/OpenLDAP, en lokale DNS in Azure. Hallo lokale liggend is uitgebreide toohello Azure activa van Hallo-abonnement. Met deze uitbreiding, kan Hallo VMs deel uitmaken van Hallo lokaal domein. Domeingebruikers van Hallo lokale domein hebben toegang tot Hallo-servers en services kunnen uitvoeren op de virtuele machines (zoals DBMS services). Communicatie en naamomzetting tussen de geïmplementeerde virtuele machines on-premises en geïmplementeerde virtuele machines in Azure is mogelijk. Dit is Hallo scenario die we verwachten dat de meeste SAP activa toobe geïmplementeerd in. Zie voor meer informatie [dit] [ vpn-gateway-cross-premises-options] artikel en [dit][vpn-gateway-site-to-site-create].

> [!NOTE]
> Cross-premises implementaties van waar Azure Virtual Machines SAP computers lid van een lokaal domein zijn SAP-systemen worden ondersteund voor productie SAP-systemen. Cross-premises configuraties worden ondersteund voor het implementeren van onderdelen of SAP landschappen in Azure te voltooien. Hallo voltooid SAP liggend zelfs worden uitgevoerd in Azure vereist die virtuele machines die deel van het lokale domein en ADVERTENTIES/OpenLDAP hebben. In eerdere versies van Hallo documentatie besproken we hybride IT-scenario's waarbij Hallo term 'Hybride' verankerd in Hallo feit ligt dat er een cross-premises-connectiviteit tussen on-premises en Azure. Bovendien Hallo feit die Hallo virtuele machines in Azure maken deel uit van Hallo op lokale Active Directory / OpenLDAP.
>
>

Sommige Microsoft-documentatie worden scenario's voor cross-premises iets anders, met name voor DBMS HA configuraties beschreven. In geval van Hallo SAP-gerelateerde documenten Hallo Hallo cross-premises scenario slechts komt meestal neer toohaving een site-naar-site of privé (ExpressRoute)-connectiviteit en Hallo fact dat Hallo SAP Liggend wordt verdeeld tussen on-premises en Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Resources
Hallo zijn volgende aanvullende handleidingen beschikbaar voor Hallo onderwerp SAP-implementaties op Azure:

* [Azure virtuele Machines, planning en implementatie voor SAP NetWeaver (in dit document)][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP NetWeaver][deployment-guide]
* [Azure virtuele Machines DBMS-implementatie voor SAP NetWeaver][dbms-guide]

> [!IMPORTANT]
> Waar mogelijk een koppeling toohello verwijst SAP installatiehandleiding wordt gebruikt (verwijzing InstGuide-01, Zie <http://service.sap.com/instguides>). Als het gaat toohello vereisten en -installatieproces, Hallo SAP NetWeaver installatiehandleidingen moet altijd Lees zorgvuldig, aangezien dit document alleen specifieke taken voor SAP NetWeaver systemen in een Microsoft Azure virtuele Machine geïnstalleerd bevat.
>
>

Hallo SAP opmerkingen bij de volgende zijn gerelateerde toohello onderwerp van SAP op Azure:

| Het nummer | Titel |
| --- | --- |
| [1928533] |SAP-toepassingen in Azure: ondersteunde producten en schaling |
| [2015553] |SAP op Microsoft Azure: ondersteuning voor vereisten |
| [1999351] |Het oplossen van uitgebreide Azure-bewaking voor SAP |
| [2178632] |Sleutel bewaking van metrische gegevens voor SAP op Microsoft Azure |
| [1409604] |Virtualisatie in Windows: uitgebreide bewaking |
| [2191498] |SAP op Linux met Azure: uitgebreide bewaking |
| [2243692] |Linux op Microsoft Azure (IaaS) VM: problemen met SAP-licentie |
| [1984787] |SUSE LINUX Enterprise Server 12: Opmerkingen bij de installatie |
| [2002167] |Red Hat Enterprise Linux 7.x: installatie en Upgrade |
| [2069760] |Oracle Linux 7.x SAP-installatie en Upgrade |
| [1597355] |Wisselruimte aanbeveling voor Linux |

Lees ook Hallo [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) die alle SAP notities voor Linux bevat.

Algemene standaardbeperkingen en de maximale beperkingen van de Azure-abonnementen kunnen worden gevonden [in dit artikel][azure-subscription-service-limits-subscription].

## <a name="possible-scenarios"></a>Mogelijke scenario 's
SAP is vaak gezien als een van de meest cruciale toepassingen Hallo ondernemingen. Hallo-architectuur en de bewerkingen van deze toepassingen is voornamelijk zeer complex en het is belangrijk ervoor te zorgen dat u voldoet aan de vereisten voor de beschikbaarheid en prestaties.

Bedrijven hebben dus toothink zorgvuldig over welke toepassingen kunnen worden uitgevoerd in een openbare cloud-omgeving, onafhankelijk van de cloudprovider Hallo gekozen.

Mogelijke systeemtypes voor het implementeren van SAP NetWeaver gebaseerde toepassingen binnen de openbare cloud omgevingen worden hieronder weergegeven:

1. Middelgrote productiesystemen
2. Ontwikkeling van systemen
3. Testen van systemen
4. Prototypesystemen
5. Learning / demonstratie systemen

In de volgorde toosuccessfully implementeert SAP-systemen in Azure IaaS of IaaS in het algemeen, is het belangrijk toounderstand Hallo belangrijke verschillen tussen de offerings Hallo van traditionele uitbesteders of hosters en IaaS-aanbod. Terwijl Hallo traditionele hoster of outsourcer aanpast infrastructuur (type netwerk, opslag en server) toohello werkbelasting een klant wil toohost, wordt deze in plaats daarvan van Hallo klant verantwoordelijkheid toochoose Hallo rechts werkbelasting voor IaaS-implementaties.

Klanten moeten als eerste stap tooverify Hallo volgende items:

* Hallo SAP ondersteunde typen van de virtuele machine van Azure
* Hallo SAP ondersteunde producten/versies in Azure
* Hallo ondersteund OS en DBMS versies voor Hallo die specifieke SAP releases in Azure
* SAP's doorvoer geleverd door verschillende Azure-SKU 's

Hallo antwoorden toothese vragen kunnen worden gelezen in SAP-notitie [1928533].

Als een tweede stap nodig Azure resource en bandbreedte beperkingen toobe vergeleken tooactual resourceverbruik van on-premises systemen. Daarom Hallo klanten nodig toobe nagegaan Hallo verschillende mogelijkheden van Azure die worden ondersteund met SAP in Hallo gebied van:

* CPU en geheugenbronnen kost van verschillende typen van de virtuele machine en
* IOPS bandbreedte van verschillende typen van de virtuele machine en
* Mogelijkheden van verschillende typen van de VM-netwerk.

De meeste van deze gegevens vindt u [hier (Linux)] [ virtual-machines-sizes-linux] en [hier (Windows)][virtual-machines-sizes-windows].

Houd er rekening mee dat de grenzen die worden vermeld in de bovenstaande koppeling voor Hallo Hallo bovengrenzen zijn. Dit betekent niet dat Hallo limieten voor het Hallo-bronnen, bijvoorbeeld IOP's kan worden opgegeven onder alle omstandigheden. Hallo-uitzonderingen zijn echter Hallo CPU en geheugenbronnen kost van een gekozen VM-type. Voor Hallo VM die worden ondersteund door SAP, zijn Hallo CPU en geheugenbronnen kost gereserveerd en als zodanig beschikbaar zijn op elk punt in tijd voor consumptie in Hallo VM.

Microsoft Azure-platform Hallo zoals andere platforms IaaS is een multitenant-platform. Dit betekent dat de opslag-, netwerk- en andere resources worden gedeeld tussen de tenants. Intelligent bandbreedtebeperking en quota logica is gebruikte tooprevent een tenant Hallo prestaties van een andere tenant (ruis neighbor) op een manier ingrijpende beïnvloeden. Hoewel de logica in Azure probeert tookeep afwijkingen in bandbreedte heeft ondergaan vaak kleine, maximaal gedeelde platforms toointroduce groter afwijkingen in de beschikbaarheid van de resource/bandbreedte dan veel klanten gebruikte tooin hun on-premises-implementaties. Als gevolg hiervan kunt u verschillende niveaus van bandbreedte met betrekking tot het netwerk of de opslag-i/o (Hallo volume evenals latentie) van de minuut toominute ervaren. Hallo-kans dat een SAP-systeem op Azure groter afwijkingen dan in een on-premises systeem optreden kan moet toobe in aanmerking genomen.

Een laatste stap is tooevaluate beschikbaarheidsvereisten. Dit kan gebeuren, die Hallo onderliggende Azure-infrastructuur nodig tooget bijgewerkt en vereist Hallo hosts met virtuele machines toobe opnieuw opgestart. In deze gevallen zou VM's worden uitgevoerd op deze hosts worden uitgeschakeld en opnieuw opgestart ook. Hallo timing van dergelijke onderhoud wordt uitgevoerd tijdens de kantooruren core-voor een bepaalde regio maar Hallo potentiële venster van een paar uur waarover een wordt opnieuw opgestart relatief groot is. Er zijn verschillende technologieën binnen hello Azure-platform die kan worden geconfigureerd toomitigate sommige of alle Hallo impact van dergelijke updates. Toekomstige verbeteringen van Azure-platform, DBMS, Hallo en SAP-toepassing zijn ontworpen toominimize Hallo impact van dergelijke opnieuw wordt opgestart.

In de volgorde toosuccessfully een SAP-systeem naar Azure implementeert, Hallo on-premises SAP systemen, besturingssysteem, Database, en SAP-toepassingen op Hallo SAP Azure ondersteuningsmatrix, past binnen Hallo resources hello Azure-infrastructuur kunt opgeven en die moeten worden weergegeven kunt werken met Hallo die beschikbaarheid serviceovereenkomsten Microsoft Azure biedt. Deze systemen worden aangeduid, moet u toodecide op een van de Hallo twee implementatiescenario's te volgen.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Alleen in de cloud - implementaties van virtuele machines in Azure zonder afhankelijkheden op Hallo lokale klantnetwerk
![Één virtuele machine met SAP-demo of training scenario geïmplementeerd in Azure][planning-guide-figure-100]

Dit scenario is gebruikelijk om trainingen of demo-systemen, waarop alle Hallo-onderdelen van SAP en niet-SAP software binnen een enkele virtuele machine zijn geïnstalleerd. Productie SAP-systemen worden niet ondersteund in dit implementatiescenario. Dit scenario aan in het algemeen Hallo volgens de vereisten voldoet:

* Hallo-VM's zelf zijn toegankelijk via Hallo openbaar netwerk. Rechtstreekse netwerkverbinding voor Hallo toepassingen die worden uitgevoerd binnen Hallo VMs toohello on-premises netwerk van beide Hallo bedrijf die eigenaar is van Hallo demo's of trainingen inhoud of Hallo klant is niet nodig.
* In geval van meerdere virtuele machines die Hallo trainingen of demo scenario moet de communicatie en naamomzetting netwerk toowork tussen Hallo VM's. Maar de communicatie tussen de Hallo set van virtuele machines moeten toobe geïsoleerd, zodat verschillende sets van virtuele machines naast elkaar kunnen worden geïmplementeerd zonder tussenkomst.  
* Verbinding met Internet is vereist voor Hallo eindgebruiker tooremote aanmelding in toohello die virtuele machines worden gehost in Azure. Afhankelijk van Hallo gastbesturingssysteem, Terminal RDS-Services of VNC/ssh wordt gebruikt tooaccess Hallo VM tooeither Hallo training taken wordt voldoen of Hallo demo's uit te voeren. Als SAP zoals 3200, 3300 & 3600 kan poorten ook worden blootgesteld Hallo SAP-toepassingsexemplaar toegankelijk zijn vanaf elke Internet verbonden desktop.
* Hallo SAP systemen (en VM(s)) vertegenwoordigen een zelfstandige scenario in Azure, waardoor alleen openbare verbinding met internet vereist voor toegang door eindgebruikers en vereist niet dat een verbinding tooother virtuele machines in Azure.
* SAPGUI en een browser zijn geïnstalleerd en deze direct op Hallo VM uitvoeren.
* Snel opnieuw instellen van een oorspronkelijke status van virtuele machine toohello en nieuwe implementatie van die oorspronkelijke status opnieuw is vereist.
* In geval van demo en scenario's voor training Hallo die gerealiseerde in meerdere virtuele machines, een Active Directory-OpenLDAP en/of de DNS-service is vereist voor elke set van virtuele machines.

![Groep van de virtuele machine die een demo of training scenario in een Azure Cloud Service][planning-guide-figure-200]

Het is belangrijk tookeep er rekening mee dat VM('s) in elk Hallo Hallo ingesteld nodig toobe geïmplementeerd parallel waar Hallo VM-namen in elk van de set Hallo zijn Hallo dezelfde.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Cross-Premises - implementatie van één of meerdere SAP-virtuele machines in Azure met de vereiste Hallo van volledig geïntegreerd in Hallo on-premises netwerk
![VPN met Site-naar-Site-connectiviteit (cross-premises)][planning-guide-figure-300]

Dit scenario is een scenario voor cross-premises met veel mogelijke implementaties. Het kan zijn beschreven zo eenvoudig als het uitvoeren van sommige onderdelen van Hallo SAP liggend lokale en andere onderdelen van Hallo SAP Liggend op Azure. Alle aspecten van Hallo feit die deel uitmaken van Hallo SAP-onderdelen worden uitgevoerd op Azure moet transparant voor eindgebruikers. Daarom Hallo SAP Transport correctie System (STM's), RFC communicatie, afdrukken, beveiliging, (zoals SSO), enz. naadloos werken voor Hallo SAP-systemen is uitgevoerd op Azure. Maar Hallo cross-premises scenario wordt ook beschreven voor een scenario waarbij Hallo voltooid SAP Liggend wordt uitgevoerd in Azure met van de klant Hallo domein en DNS uitgebreid naar Azure.

> [!NOTE]
> Dit is de implementatiescenario hello, die wordt ondersteund voor het uitvoeren van productief SAP-systemen.
>
>

Lees [in dit artikel] [ vpn-gateway-create-site-to-site-rm-powershell] voor meer informatie over het tooconnect uw on-premises netwerk tooMicrosoft Azure

> [!IMPORTANT]
> Wanneer we wordt gesproken over cross-premises-scenario's tussen Azure en on-premises implementaties van klanten, bekijkt we hello granulatie van de gehele SAP-systemen. Scenario's worden *niet ondersteund* voor cross-premises scenario's:
>
> * Verschillende lagen van SAP-toepassingen in verschillende implementatiemethoden uitgevoerd. Hallo DBMS laag lokale, maar Hallo SAP toepassingslaag bijvoorbeeld uitgevoerd in de virtuele machines die worden geïmplementeerd als Azure virtuele machines of vice versa.
> * Sommige onderdelen van een laag SAP in Azure en een on-premises. Bijvoorbeeld splitsen exemplaren van Hallo SAP toepassingslaag tussen on-premises en Azure VM's.
> * Distributie van virtuele machines met SAP-exemplaren van een systeem over meerdere Azure-regio's wordt niet ondersteund.
>
> Hallo reden voor deze beperkingen is Hallo vereiste voor een zeer lage latentie krachtige netwerk binnen een SAP-systeem, met name tussen toepassingsexemplaren Hallo en Hallo DBMS laag van een SAP-systeem.
>
>

### <a name="supported-os-and-database-releases"></a>Ondersteund besturingssysteem en versies van de Database
* Microsoft-serversoftware ondersteund voor Services van Azure virtuele Machine wordt vermeld in dit artikel: <http://support.microsoft.com/kb/2721672>.
* Ondersteund besturingssysteem system releases, database system releases in combinatie met SAP-software wordt ondersteund door Azure virtuele Machine Services zijn gedocumenteerd in SAP-notitie [1928533].
* SAP-toepassingen en versies die worden ondersteund op Azure Virtual Machine-Services zijn gedocumenteerd in SAP-notitie [1928533].
* Alleen 64-bits installatiekopieën zijn ondersteunde toorun als gast virtuele machines in Azure voor SAP-scenario's. Dit betekent ook dat alleen 64-bits SAP-toepassingen en databases worden ondersteund.

## <a name="microsoft-azure-virtual-machine-services"></a>Services van Microsoft Azure-virtuele Machine
Hallo Microsoft Azure-platform is een internet-scale cloud services-platform gehost en beheerd in Microsoft data centers. Hallo-platform omvat Hallo Microsoft Azure Services op virtuele Machine (infrastructuur als een Service of IaaS) en een aantal uitgebreide Platform als een Service (PaaS)-mogelijkheden.

Hello Azure-platform vermindert de behoefte aan Hallo voor vooraf technologie en infrastructuur koopt. Het vereenvoudigt onderhouden en toepassingen functioneren door te geven op aanvraag berekenings- en toohost schalen en webtoepassing en verbonden toepassingen beheren. Beheer van infrastructuur is geautomatiseerde met een platform dat is ontworpen voor hoge beschikbaarheid en dynamische schaling toomatch gebruik behoeften Hallo optie een betalen naar gebruik prijsmodel.

![Plaatsing van de Services van Microsoft Azure-virtuele Machine][planning-guide-figure-400]

Met Azure Virtual Machine-Services, is Microsoft zodat u toodeploy server met een aangepaste installatiekopieën tooAzure als IaaS-instanties (Zie afbeelding 4). Hallo virtuele Machines in Azure zijn gebaseerd op Hyper-V virtuele harde schijven (VHD) en kunnen toorun zijn verschillende besturingssystemen worden uitgevoerd als het Gastbesturingssysteem.

Van een operationeel perspectief ervaringen hello die Azure virtuele Machine Service vergelijkbare biedt als virtuele machines die on-premises worden geïmplementeerd. Dit heeft echter Hallo aanzienlijke voordeel dat u hoeft niet tooprocure, te beheren en te beheren Hallo-infrastructuur. Ontwikkelaars en beheerders hebben volledig beheer van de installatiekopie van besturingssysteem Hallo binnen deze virtuele machines. Beheerders kunnen zich aanmelden op afstand in toothose virtuele machines tooperform onderhoud en probleemoplossing van taken, evenals de taken van software-implementatie. In inachtneming van toodeployment zijn alleen beperkingen Hallo Hallo grootten en mogelijkheden van Azure Virtual machines. Deze mogelijk niet als fijn gedetailleerde in configuratie, zoals dit on-premises kan worden uitgevoerd. Er is een keuze uit de VM-typen die een combinatie van vertegenwoordigen:

* Aantal Vcpu,
* Geheugen,
* Aantal virtuele harde schijven die kunnen worden gekoppeld,
* Netwerk en opslag bandbreedten.

Hallo grootte en beperkingen van verschillende grootten voor verschillende virtuele machines die worden aangeboden kunnen worden weergegeven in een tabel in [in dit artikel (Linux)] [ virtual-machines-sizes-linux] en [in dit artikel (Windows)] [ virtual-machines-sizes-windows].

Als u beseft, zijn er verschillende families of reeks van virtuele machines. U kunt onderscheiden Hallo families van virtuele machines te volgen:

* A0 A7 VM typen: niet alle die zijn gecertificeerd voor SAP. Eerste VM-reeks die Azure IaaS is geïntroduceerd in.
* A8-A11-VM-typen: High Performance computing-exemplaren. Wordt uitgevoerd voor het uitvoeren van verschillende betere compute hosts dan andere virtuele machines van A-serie.
* Dv2-D-reeks VM typen: beter dan A0 A7 uitvoeren. Niet alle Hallo VM typen zijn gecertificeerd met SAP.
* DS-DSv2-serie VM typen: vergelijkbare tooD/Dv2-serie, maar kunnen tooconnect tooAzure Premium-opslag zijn (Zie hoofdstuk [Azure Premium-opslag] [ planning-guide-3.3.2] van dit document). Opnieuw niet alle VM-typen zijn gecertificeerd met SAP.
* G-serie VM typen: veel geheugen VM typen.
* Typen GS-serie VM: G-serie, zoals maar inclusief Hallo optie toouse Azure Premium-opslag (Zie hoofdstuk [Azure Premium-opslag] [ planning-guide-3.3.2] van dit document). Wanneer u virtuele machines GS-serie als databaseservers, is verplicht toouse Premium-opslag voor DB gegevens en transactie-logboekbestanden

U vindt Hallo dezelfde configuraties van CPU en geheugen in andere VM-reeks. Echter, wanneer u opzoeken Hallo doorvoer prestaties van deze virtuele machines buiten Hallo andere reeks die ze aanzienlijk verschillen. Hallo ondanks met dezelfde configuratie van CPU en geheugen. Reden is dat Hallo onderliggende host serverhardware op Hallo inleiding Hallo verschillende soorten VM verschillende doorvoer had.  Meestal Hallo verschil in prestaties van de netwerkdoorvoer weergegeven ook worden weerspiegeld in Hallo prijs Hallo andere virtuele machines.

Niet alle andere VM-reeks kan worden aangeboden in elk criterium van hello Azure-regio's (voor Azure-gebieden Zie volgende hoofdstuk). Zich bewust te zijn dat niet alle virtuele machines of VM-serie zijn gecertificeerd voor SAP.

> [!IMPORTANT]
> Voor het gebruik van de Hallo van SAP NetWeaver op basis van toepassingen, alleen Hallo subset van de VM-typen en configuraties die worden vermeld in SAP-notitie [1928533] worden ondersteund.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Azure-regio 's
Microsoft kan toodeploy virtuele Machines in zogenaamde Azure gebieden. Een Azure-regio is mogelijk een of meerdere datacenters die zich dicht bevinden. Geopolitieke regio's in Hallo wereld Microsoft heeft voor de meeste Hallo ten minste twee Azure-regio's. In Europa is er bijvoorbeeld een Azure-regio, Noord-Europa, en een van de 'West-Europa'. Deze twee Azure-regio's binnen een geopolitieke regio worden gescheiden door aanzienlijke genoeg afstand zodat natuurlijke of technische noodsituaties hebben geen invloed op zowel Azure-gebieden in Hallo dezelfde geopolitieke regio. Omdat Microsoft gestaag uit nieuwe Azure-regio's in andere geopolitieke regio's globaal bouwt, Hallo van deze gebieden gestaag groeit en vanaf december 2015 Hallo aantal 20 Azure-regio's met extra gebieden aangekondigd al is bereikt. In alle deze gebieden, waaronder Hallo twee Azure-gebieden in China, kunt u als klant SAP-systemen implementeren. Zie voor de huidige actuele informatie over Azure-regio's deze website: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Hallo Concept van Microsoft Azure virtuele Machine
Microsoft Azure biedt een infrastructuur als een Service (IaaS)-oplossing toohost virtuele Machines met vergelijkbare functionaliteit als een on-premises-oplossing voor netwerkvirtualisatie. U zijn kunt toocreate virtuele Machines van binnen hello Azure-portal, PowerShell of CLI, die ook implementatie en beheermogelijkheden bieden.

Azure Resource Manager kunt u tooprovision uw toepassingen met behulp van een declaratief sjabloon. U kunt in één enkele sjabloon meerdere services plus de bijbehorende afhankelijkheden implementeren. U hello gebruiken dezelfde sjabloon toorepeatedly uw toepassing tijdens elke fase van de levenscyclus van de toepassing hello implementeren.

Meer informatie over het gebruik van Resource Manager-sjablonen vindt u hier:

* [Implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en hello Azure CLI] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Virtuele machines beheren met Azure Resource Manager en PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://Azure.Microsoft.com/Documentation/templates/>

Een andere interessante functie is Hallo mogelijkheid toocreate installatiekopieën van virtuele Machines, waarmee u tooprepare bepaalde opslagplaatsen van waaruit u kunt tooquickly zijn implementeren instanties van de virtuele machine, die voldoen aan uw vereisten.

Meer informatie over het maken van installatiekopieën van virtuele Machines kunt u vinden [in dit artikel (Linux)] [ virtual-machines-linux-capture-image-resource-manager] en [in dit artikel (Windows)] [ virtual-machines-windows-capture-image-resource-manager].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domeinen met fouten
Domeinen met fouten vertegenwoordigen een fysieke eenheid mislukt, de fysieke infrastructuur nauw verwante toohello opgenomen in datacenters en een fysieke blade of rack kan weliswaar worden beschouwd als een domein met fouten, is er geen rechtstreekse-op-een koppeling tussen twee Hallo.

Wanneer u meerdere virtuele Machines als onderdeel van een SAP-systeem in de Services van Microsoft Azure-virtuele Machine implementeert, kunt u bepalen hello Azure-Infrastructuurcontroller toodeploy uw toepassing in verschillende domeinen met fouten, waardoor voldoen aan vereisten Hallo Hallo Microsoft Azure SLA. Hallo echter distributie van domeinen met fouten over een Azure-schaaleenheid (verzameling van honderden rekenknooppunten of opslagknooppunten en netwerken) of op Hallo toewijzing van virtuele machines tooa specifieke Foutdomein iets waarover u geen hebt directe besturingselement. In de volgorde toodirect hello Azure-infrastructuur controller toodeploy een set van virtuele machines via verschillende domeinen met fouten moet u tooassign een toohello Beschikbaarheidsset is ingesteld op Azure VM's tijdens de implementatie. Zie voor meer informatie over Azure Beschikbaarheidssets hoofdstuk [Beschikbaarheidssets van Azure] [ planning-guide-3.2.3] in dit document.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Upgradedomeinen
Upgradedomeinen vertegenwoordigen een logische eenheid waarmee toodetermine hoe een virtuele machine binnen een SAP-systeem, die uit een SAP-instanties die actief zijn in meerdere virtuele machines bestaat, wordt bijgewerkt. Wanneer een upgrade optreedt, doorloopt Microsoft Azure Hallo-proces voor het bijwerken van deze Upgradedomeinen één voor één. Door virtuele machines tijdens de implementatie spreiden over verschillende domeinen upgraden, kunt u uw systeem SAP beveiligen gedeeltelijk uit de mogelijke downtime. In order tooforce Azure toodeploy Hallo VM's van een SAP-systeem verdeeld over verschillende domeinen upgraden, moet u een specifiek kenmerk tooset tijdens de implementatie van elke virtuele machine. Vergelijkbare tooFault domeinen, een Azure-schaaleenheid is onderverdeeld in meerdere domeinen upgraden. In de volgorde toodirect hello Azure-infrastructuur controller toodeploy een set van virtuele machines via verschillende domeinen upgraden moet u tooassign een toohello Beschikbaarheidsset is ingesteld op Azure VM's tijdens de implementatie. Zie voor meer informatie over Azure Beschikbaarheidssets hoofdstuk [Beschikbaarheidssets van Azure] [ planning-guide-3.2.3] hieronder.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Azure Beschikbaarheidssets
Azure virtuele Machines in de Beschikbaarheidsset van een Azure worden door hello Azure-Infrastructuurcontroller verdeeld over verschillende domeinen met fouten en domeinen upgraden. Hallo-doel van Hallo verdeling over de verschillende domeinen met fouten en domeinen upgraden is tooprevent die alle virtuele machines van een SAP-systeem wordt afgesloten in geval van Hallo van onderhoud van infrastructuur of een storing in een domein met fouten. Virtuele machines zijn standaard niet deel uit van een Beschikbaarheidsset. Hallo deelname van een virtuele machine in een Beschikbaarheidsset is gedefinieerd tijdens de implementatie of hoger op door een herconfiguratie en een nieuwe implementatie van een virtuele machine.

toounderstand hello concept van Beschikbaarheidssets van Azure en Hallo manier Beschikbaarheidssets betrekking tooFault en -domeinen upgraden hebben lezen [in dit artikel][virtual-machines-manage-availability]

Zie toodefine beschikbaarheidssets voor ARM via een json-sjabloon [Hallo rest-api-specificaties](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) en zoek naar 'beschikbaarheid'.

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Opslag: De Microsoft Azure Storage en de gegevensschijven
Microsoft Azure Virtual Machines gebruikmaken van verschillende opslagtypen. Bij het implementeren van SAP op Azure Virtual Machine-Services, is het belangrijk toounderstand Hallo verschillen tussen deze twee typen opslag:

* Niet-permanente, vluchtige opslag.
* Permanente opslag.

niet-permanente opslag Hallo is rechtstreeks gekoppelde toohello virtuele Machines worden uitgevoerd en bevindt zich op de rekenknooppunten Hallo zelf – Hallo lokaal exemplaar opslag (tijdelijke opslag). Hallo-grootte is afhankelijk van Hallo grootte van Hallo virtuele Machine hebt gekozen bij het Hallo-implementatie is gestart. Dit opslagtype is vluchtige en daarom Hallo schijf wordt geïnitialiseerd wanneer een exemplaar van de virtuele Machine opnieuw wordt opgestart. Hallo wisselbestand voor Hallo besturingssysteem bevindt zich doorgaans op deze tijdelijke schijf.

- - -
> ![Windows][Logo_Windows] Windows
>
> Op Windows-VM's is Hallo tijdelijke station gekoppeld als station D:\ in een geïmplementeerde virtuele machine.
>
> ![Linux][Logo_Linux] Linux
>
> Het gekoppeld op Linux virtuele machines, als /mnt/resource of mnt. Zie hier voor meer informatie:
>
> * [Hoe tooAttach een gegevensschijf tooa virtuele Linux-Machine][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.Microsoft.com/Azure/Storage/Storage-About-Disks-and-vhds-Linux#Temporary-Disk>
>
>

- - -
Hallo feitelijke station is vluchtige omdat deze ophalen op Hallo host-server zelf opgeslagen is. Als Hallo VM in een opnieuw implementeren verplaatst (bijvoorbeeld vanwege toomaintenance Hallo host of afsluiten en opnieuw opstarten) Hallo inhoud van het Hallo-station is verbroken. Het is daarom niet een optie toostore alle belangrijke gegevens op dit station. Hallo type media dat wordt gebruikt voor dit type opslag verschilt voor andere VM-reeks met zeer verschillende prestatiekenmerken die vanaf juni 2015 er als volgt uitzien:

* A5-A7: Zeer beperkt prestaties. Niet aanbevolen voor alles afgezien van wisselbestand
* A8-A11: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde.
* D-reeks: Kenmerken, zeer goede prestaties met sommige vervolgens duizenden IOPS en > doorvoer van 1GB per seconde.
* DS-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde.
* G-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde.
* GS-serie: Kenmerken met een aantal IOPS tienduizend zeer goede prestaties en > doorvoer van 1GB per seconde.

Instructies hierboven zijn toohello VM typen die zijn gecertificeerd met SAP toepassen. Hallo VM-serie met uitstekende IOPS en doorvoerlimieten in aanmerking voor gebruik door sommige DBMS-functies. Zie voor meer informatie, Hallo [DBMS Deployment Guide][dbms-guide].

Microsoft Azure Storage biedt permanente opslag en Hallo typische niveaus van beveiliging en redundantie weergegeven op de SAN-opslag. Schijven op basis van Azure Storage zijn virtuele harde schijf (VHD's) zich in hello Azure Storage-Services. Hallo lokale OS-schijf (C: Windows\, Linux/dev/sda1) wordt opgeslagen op Hallo Azure Storage en extra Volumes/schijven gekoppelde toohello VM ophalen, opgeslagen te.

Het is mogelijk tooupload een bestaande VHD on-premises of lege mappen uit in Azure maken en koppelen van deze VMs toodeployed.

Na het maken of een VHD uploaden naar Azure Storage, is mogelijk toomount en koppel deze tooan bestaande virtuele Machine en toocopy bestaande VHD (ontkoppeld).

Als deze VHD's zijn persistent hebt gemaakt, zijn gegevens en wijzigingen in de veilige wanneer opnieuw opstarten en opnieuw maken van een exemplaar van de virtuele Machine. Zelfs als een exemplaar wordt verwijderd, kunnen deze VHD's veilig en kunnen worden geïmplementeerd of in geval van een niet-OS schijven gekoppelde tooother virtuele machines.

Binnen het Hallo kan-netwerk van Azure Storage redundantie van de verschillende niveaus worden geconfigureerd:

* Minimaal niveau hebben die kan worden geselecteerd 'lokale redundantie', wat toothree replica Hallo gegevens binnen Hallo equivalent is hetzelfde datacenter van een Azure-regio (Zie hoofdstuk [Azure-gebieden][planning-guide-3.1]).
* Zone redundante opslag, welke installatiekopieën van de drie Hallo verspreidt zich via verschillende datacenters binnen Hallo hetzelfde Azure-gebied.
* Redundantie standaardniveau is geografische redundantie, wat Hallo inhoud asynchroon gerepliceerd in een andere drie afbeeldingen van gegevens in een andere Azure-regio, die wordt gehost in Hallo Hallo dezelfde geopolitieke regio.

Zie ook Hallo tabel boven in dit artikel met betrekking tot Hallo redundantie van de verschillende opties op: <https://azure.microsoft.com/pricing/details/storage/>

Meer informatie over Azure Storage vindt u hier:

* <https://Azure.Microsoft.com/Documentation/Services/Storage/>
* <https://Azure.Microsoft.com/Services/site-Recovery>
* <https://docs.Microsoft.com/rest/API/storageservices/Understanding-Block-blobs--Append-blobs--and-Page-blobs>
* <https://blogs.msdn.com/b/azuresecurity/Archive/2015/11/17/Azure-Disk-Encryption-for-Linux-and-Windows-Virtual-machines-Public-Preview.aspx>

#### <a name="azure-standard-storage"></a>Azure Standard-opslag
Azure Standard-opslag is Hallo type opslag beschikbaar bij Azure IaaS werd uitgebracht. Er zijn IOPS quota per één schijf worden afgedwongen. Latentie heeft ondergaan heeft niet dezelfde klasse als SAN/NAS-apparaten doorgaans geïmplementeerd voor geavanceerde SAP-systemen lokale gehoste Hallo. Niettemin hello Azure Standard-opslag voldoende voor veel honderden bewezen SAP-systemen ondertussen geïmplementeerd in Azure.

Schijven die zijn opgeslagen op Azure Storage-Accounts worden in rekening gebracht op basis van Hallo de feitelijke gegevens die zijn opgeslagen, Hallo volume opslagtransacties en uitgaande gegevensoverdracht redundantie-optie gekozen. Veel schijven kunnen worden gemaakt op Hallo maximaal 1 TB groot, maar als deze leeg blijft er zijn geen kosten. Als u een VHD met 100GB vervolgens vult, u in rekening worden gebracht voor het opslaan van 100GB en niet voor Hallo nominaal grootte Hallo die VHD met gemaakt.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure Premium-opslag
In April 2015 geïntroduceerd Microsoft Azure Premium-opslag. Premium-opslag is geïntroduceerd met Hallo doel tooprovide:

* Betere i/o-latentie.
* Betere doorvoer.
* Minder variabiliteit in i/o-latentie.

Daartoe zijn veel wijzigingen van welke Hallo twee belangrijkste zijn geïntroduceerd:

* Informatie over het gebruik van SSD-schijven in hello Azure-configuratie voor opslagknooppunten
* Een nieuwe leescache dat wordt ondersteund door Hallo lokale SSD van een Azure computerknooppunt

In de tegengestelde tooStandard opslag waar mogelijkheden is niet veranderd afhankelijk van het Hallo-grootte of Hallo schijf (VHD), Premium-opslag heeft momenteel drie andere schijf categorieën, die worden weergegeven in dit artikel: <https://azure.microsoft.com/ prijzen/details / / zonder begeleiding-opslagschijven />

U ziet dat IOPS/en de schijf doorvoer/schijf afhankelijk Hallo grootte categorie van het Hallo-schijven

Kosten basis in geval van Hallo van Premium-opslag is geen Hallo actuele gegevensvolume opgeslagen in een dergelijke disks, maar Hallo grootte categorie van dergelijke een schijf, onafhankelijk van Hallo hoeveelheid Hallo-gegevens die zijn opgeslagen in het Hallo-schijf.

U kunt schijven maken op Premium-opslag die niet rechtstreeks wilt toewijzen in Hallo grootte categorieën weergegeven. Kan dit Hallo geval, vooral wanneer u schijven uit de Standard-opslag kopiëren naar de Premium-opslag. In dergelijke gevallen wordt een toewijzing toohello volgende grootste Premium-opslag-schijfoptie uitgevoerd.

Let erop dat alleen bepaalde VM-reeks van hello Azure Premium-opslag profiteren kunt. Vanaf december 2015 zijn deze Hallo DS - en GS-serie. Hallo DS-serie is in feite Hallo dezelfde D-reeks met Hallo uitzondering dat DS-serie Hallo mogelijkheid toomount Premium-opslag heeft op basis van virtuele machines ook toodisks die worden gehost op Azure Standard-opslag. Hetzelfde geldt voor G-serie vergeleken tooGS-serie.

Als u Hallo-onderdeel van de DS-serie Hallo VM's in zijn uitgecheckt [in dit artikel (Linux)] [ virtual-machines-sizes-linux] en [in dit artikel (Windows)][virtual-machines-sizes-windows], zult u ontdekken Er zijn die gegevens volume beperkingen tooPremium opslagschijven op Hallo granulatie van Hallo VM-niveau. Andere DS-serie- of GS-serie VM's hebben andere beperkingen in groet toohello aantal gegevensschijven dat kan worden gekoppeld. Deze limieten zijn gedocumenteerd in Hallo artikel ook hierboven vermeld. Maar in wezen betekent dat als u bijvoorbeeld 32 x P30 schijven tooa koppelen één DS14 VM u niet 32 x Hallo maximale doorvoer van een schijf P30 downloaden kunt. In plaats daarvan Hallo maximale doorvoer op VM-niveau, zoals beschreven in Hallo artikel limieten gegevensdoorvoer.

Meer informatie over het Premium-opslag vindt u hier: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>Beheerde schijven
Beheerde schijven zijn een nieuwe brontype in Azure Resource Manager die kunnen worden gebruikt in plaats van VHD's die zijn opgeslagen in Azure Storage-Accounts. Beheerde schijven wordt automatisch uitgelijnd met de Hallo Beschikbaarheidsset van Hallo virtuele machine die ze zijn gekoppeld tooand daarom toename Hallo beschikbaarheid van uw virtuele machine en het Hallo-services die worden uitgevoerd op Hallo virtuele machine. Lees voor meer informatie, Hallo [overzichtsartikel](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

Gebruik tooyou beheerd schijf, wordt aangeraden omdat ze eenvoudiger Hallo-implementatie en beheer van uw virtuele machines.
SAP ondersteunt momenteel alleen Premium-schijven worden beheerd. Lees voor meer informatie, SAP-notitie [1928533].

#### <a name="azure-storage-accounts"></a>Azure Storage Accounts
Bij het implementeren van services of virtuele machines in Azure, kan de implementatie van virtuele harde schijven en VM-installatiekopieën worden ingedeeld in eenheden Azure Storage-Accounts die worden genoemd. Bij het plannen van een Azure-implementatie, moet u toocarefully Overweeg Hallo beperkingen van Azure. Hallo een-zijde is er een beperkt aantal Storage-Accounts per Azure-abonnement. Hoewel elke Azure Storage-Account een groot aantal VHD-bestanden bevatten kan, er is een vaste limiet op Hallo totale IOP's per Storage-Account. Wanneer u honderden SAP virtuele machines implementeren met DBMS-systemen voor het maken van belangrijke i/o-aanroepen, is het aanbevolen toodistribute hoge IOPS DBMS VMs tussen meerdere Azure Storage-Accounts. Wees voorzichtig niet tooexceed Hallo huidige limiet van Azure Storage-Accounts per abonnement. Omdat opslag een essentieel onderdeel van de implementatie van de database voor een SAP hello, dit concept wordt besproken in Hallo al verwezen nader [DBMS Deployment Guide][dbms-guide].

Meer informatie over Azure Storage-Accounts kunt u vinden [in dit artikel][storage-scalability-targets]. Dit artikel leest, zult u ontdekken dat er verschillen in Hallo beperkingen tussen Azure Storage-Accounts en Premium Storage-Accounts zijn. Belangrijke verschillen zijn Hallo hoeveelheid gegevens die kunnen worden opgeslagen in een Opslagaccount. In de Standard-opslag is Hallo volume een grootte die groter is dan met Premium-opslag. Op Hallo andere kant Hallo standaard Opslagaccount ernstige problemen in IOPS (Zie de kolom 'Totale snelheid van aanvragen voor'), beperkt dat hello Azure Premium Storage-Account beperking bestaat niet is. Wanneer u Hallo implementaties van SAP-systemen, met name Hallo DBMS servers wordt details en de resultaten van deze verschillen besproken.

U hebt Hallo mogelijkheid toocreate verschillende containers Hallo doel te organiseren en te categoriseren verschillende VHD's binnen een Opslagaccount. Deze containers worden meestal gebruikt om, bijvoorbeeld afzonderlijke VHD's van andere virtuele machines. Er zijn geen gevolgen voor prestaties bij het gebruik van een container of meerdere containers onder één Azure Storage-Account.

De naam van een VHD volgt binnen Azure Hallo naming verbinding die u een unieke naam voor de VHD in Azure Hallo tooprovide moet te volgen:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Als hierboven genoemde Hallo-tekenreeks moet toouniquely Hallo VHD die is opgeslagen op Azure Storage identificeren.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Microsoft Azure-netwerken
Microsoft Azure biedt een infrastructuur van het netwerk, waardoor Hallo toewijzing van alle scenario's die we willen toorealize met SAP-software. Hallo-mogelijkheden zijn:

* Toegang vanaf Hallo buiten rechtstreeks toohello VM's via Windows Terminal Services of ssh/VNC
* Toegang tooservices en bepaalde poorten gebruikt door toepassingen binnen Hallo virtuele machines
* Interne communicatie en naamomzetting tussen een groep van virtuele machines die worden geïmplementeerd als Azure virtuele machines
* Cross-premises-connectiviteit tussen de on-premises netwerk en hello Azure-netwerk van de klant
* Over Azure-regio of data center-verbindingen tussen Azure websites

Meer informatie vindt u hier: <https://azure.microsoft.com/documentation/services/virtual-network/>

Er zijn veel verschillende mogelijkheden tooconfigure naam en IP-oplossing in Azure. In dit document is alleen-scenario's zijn afhankelijk van Hallo standaard gebruik van Azure DNS (in contrast toodefining een eigen DNS-service). Er is ook een nieuwe Azure DNS-service, die kan worden gebruikt in plaats van het instellen van uw eigen DNS-server. Meer informatie vindt u in [in dit artikel] [ virtual-networks-manage-dns-in-vnet] en klik op [deze pagina](https://azure.microsoft.com/services/dns/).

Voor scenario's met cross-premises we Hallo feit afhankelijk dat Hallo lokale AD en OpenLDAP/DNS-is uitgebreid via VPN of een particuliere verbinding tooAzure. Voor bepaalde scenario's zoals hier wordt beschreven, is mogelijk noodzakelijk toohave een geïnstalleerd in Azure AD/OpenLDAP-replica.

Omdat de netwerken en naamomzetting is een essentieel onderdeel van de implementatie van de database voor een SAP hello, dit concept wordt besproken in Hallo nader [DBMS Deployment Guide][dbms-guide].

##### <a name="azure-virtual-networks"></a>Virtuele netwerken van Azure
Opbouw van een Azure-netwerk, kunt u definiëren Hallo-adresbereik van Hallo privé IP-adressen toegewezen door Azure DHCP-functionaliteit. In scenario's voor cross-premises, Hallo IP-adresbereik gedefinieerd nog is toegewezen via DHCP door Azure. Echter domein naamomzetting lokale (ervan uitgaande dat Hallo virtuele machines deel uitmaken van een lokaal domein) wordt uitgevoerd en daarom adressen afgezien van andere Azure-Cloud-Services kunt oplossen.

Elke virtuele Machine in Azure behoeften toobe verbonden tooa virtueel netwerk.

Meer informatie vindt u in [in dit artikel] [ resource-groups-networking] en klik op [deze pagina](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (Een artikel waaronder Hallo OpenLDAP onderwerp + ARM; vinden MShermannd TODO niet)
[comment]: <> (MSSedusch < https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Nadat een virtuele machine wordt geïmplementeerd wijzigen niet u standaard Hallo Virtual Network-configuratie. Hallo TCP/IP-instellingen moeten toohello Azure DHCP-server worden gelaten. Standaard wordt de dynamische IP-toewijzing.
>
>

Hallo MAC-adres van de virtuele netwerkkaart Hallo kan worden gewijzigd, bijvoorbeeld na het aanpassen en Hallo Windows of Linux Gast OS Hallo nieuwe netwerkkaart wordt opgehaald en gebruikt automatisch DHCP tooassign Hallo IP-adres en DNS-serveradressen in dit geval.

##### <a name="static-ip-assignment"></a>Toewijzing van vaste IP-adres
Het is mogelijk tooassign vaste of gereserveerde IP-adressen tooVMs binnen een Azure-netwerk. Hallo VM's worden uitgevoerd in een Azure-netwerk, wordt een kans groot tooleverage geopend die deze functionaliteit of die nodig zijn vereist voor sommige scenario's. toewijzing van IP-adres Hallo blijft geldig in de gehele Hallo bestaan Hallo VM, onafhankelijk van de vraag of Hallo VM wordt uitgevoerd of afsluiten. Als gevolg hiervan moet u tootake Hallo totale aantal virtuele machines (actieve en gestopte VM's) in aanmerking bij het definiëren van Hallo bereik van IP-adressen voor Hallo virtueel netwerk. tot Hallo VM en de netwerkinterface is verwijderd of totdat Hallo IP-adres opgehaald ongedaan opnieuw toegewezen, blijft de Hallo IP-adres toegewezen. Lees voor meer informatie [in dit artikel][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Meerdere NIC's per VM
U kunt meerdere virtuele netwerkinterfacekaarten (vNIC) definiëren voor een virtuele Machine van Azure. Met de Hallo mogelijkheid toohave meerdere vNICs kunt u tooset up scheiding van verkeer voor netwerk waar, bijvoorbeeld clientverkeer wordt doorgestuurd via één vNIC en back-end-verkeer wordt doorgestuurd via een tweede vNIC starten. Afhankelijk van Hallo-type van de virtuele machine er zijn verschillende beperkingen in wat betreft het aantal vNICs toohello. Exacte details, functionaliteit en beperkingen vindt in deze artikelen:

* [Maak een Windows-VM met meerdere NIC 's][virtual-networks-multiple-nics-windows]
* [Maak een Linux-VM met meerdere NIC 's][virtual-networks-multiple-nics-linux]
* [Meerdere NIC VMs met een sjabloon implementeren][virtual-network-deploy-multinic-arm-template]
* [Implementeren van meerdere NIC virtuele machines met behulp van PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Implementeren van meerdere NIC VMs hello Azure CLI gebruiken][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Site-naar-Site-connectiviteit
Cross-premises is Azure VM's en On-Premises gekoppeld met een transparante en permanente VPN-verbinding. Het is verwachte toobecome Hallo meest voorkomende SAP-implementatie patroon in Azure. Hallo veronderstelling is operationele procedures en processen met SAP-exemplaren in Azure transparant moeten werken. Dit betekent dat u moet kunnen tooprint buiten deze systemen worden evenals Hallo SAP Transport Management System (TMS) tootransport wordt gewijzigd van een ontwikkelsysteem in Azure tooa testsysteem geïmplementeerde on-premises gebruiken. Meer documentatie om site-naar-site vindt u in [in dit artikel][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>VPN-Tunnel-apparaat
In volgorde van toocreate een site-naar-site-verbinding (on-premises gegevens center tooAzure Datacenter), moet u tooeither verkrijgen en configureren van een VPN-apparaat of Routing and Remote Access Service (RRAS) dat werd geïntroduceerd als softwareonderdeel met Windows Server gebruiken 2012.

* [Een virtueel netwerk maken met een site-naar-site VPN-verbinding met behulp van PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [Informatie over VPN-apparaten voor Site-naar-Site-VPN-gatewayverbindingen][vpn-gateway-about-vpn-devices]
* [VPN-Gateway Veelgestelde vragen][vpn-gateway-vpn-faq]

![Site-naar-site-verbinding tussen on-premises en Azure][planning-guide-figure-600]

Hallo in bovenstaande afbeelding ziet u twee Azure-abonnementen zijn gereserveerd voor gebruik van IP-adres subbereiken in virtuele netwerken in Azure. Hallo-verbinding tussen Hallo lokale netwerk tooAzure tot stand is gebracht via VPN.

#### <a name="point-to-site-vpn"></a>Punt-naar-Site VPN
Punt-naar-site VPN moet elke client machine tooconnect met een eigen VPN in Azure. Punt-naar-site-connectiviteit is geen praktische voor Hallo SAP scenario's met die we kijken. Daarom geen verdere verwijzingen toopoint-naar-site VPN-verbinding krijgen.

Meer informatie vindt u hier
* [Een punt-naar-Site-verbinding tooa VNet configureren met behulp van hello Azure-portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [Een punt-naar-Site-verbinding tooa VNet configureren met behulp van PowerShell](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>Multi-site-VPN
Azure biedt ook tegenwoordig Hallo mogelijkheid toocreate multi-site-VPN-verbinding voor een Azure-abonnement. Een abonnement van één was eerder beperkt tooone site-naar-site VPN-verbinding. Deze beperking verdwenen met multi-site-VPN-verbindingen voor één abonnement. Dit maakt het mogelijk tooleverage meer dan één Azure-regio voor een specifiek abonnement via cross-premises configuraties.

Zie voor meer documentatie [in dit artikel][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO geen ARM docu koppeling gevonden)

#### <a name="vnet-toovnet-connection"></a>VNet tooVNet verbinding
Met multi-site-VPN, moet u een afzonderlijke Azure Virtual Network in alle regio's Hallo tooconfigure. U hebt echter vaak Hallo vereiste dat software-onderdelen in verschillende regio's Hallo Hallo moeten met elkaar communiceren. In het ideale geval deze communicatie moet niet worden gerouteerd uit een Azure-regio tooon-premises en er toohello andere Azure-regio. tooshortcut, Azure biedt Hallo mogelijkheid tooconfigure verbinding van een virtuele Azure-netwerk in één regio tooanother die Azure Virtual Network in een andere regio gehost. Deze functionaliteit wordt VNet-naar-VNet-verbinding genoemd. Meer informatie over deze functie vindt u hier: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>Persoonlijke verbinding tooAzure – ExpressRoute
Microsoft Azure ExpressRoute kunt Hallo maken van een particuliere verbindingen tussen Azure-datacenters en van de klant van beide Hallo on-premises infrastructuur of in een omgeving met CO-locatie. ExpressRoute wordt aangeboden door verschillende MPLS (geschakeld pakket) VPN-providers of andere serviceproviders netwerk. ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. ExpressRoute-verbindingen bieden betere beveiliging, meer betrouwbaarheid via meerdere parallelle circuits, hogere snelheden en lagere latenties dan gewone verbindingen via Internet Hallo.

Meer informatie over Azure ExpressRoute en de offerings hier vinden:

* <https://Azure.Microsoft.com/Documentation/Services/expressroute/>
* <https://Azure.Microsoft.com/Pricing/details/expressroute/>
* <https://Azure.Microsoft.com/Documentation/articles/expressroute-faqs/>

Express Route kan meerdere Azure-abonnementen via één ExpressRoute-circuit, zoals hier wordt beschreven

* <https://Azure.Microsoft.com/Documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://Azure.Microsoft.com/Documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Geforceerde tunneling in geval van een cross-premises
Voor virtuele machines het lidmaatschap van lokale domeinen via site-naar-site, punt-naar-site of ExpressRoute, moet u toomake u ervoor zorgen dat Hallo Internet proxy-instellingen voor alle Hallo gebruikers in die virtuele machines ook worden ophalen geïmplementeerd. Standaard-software in deze virtuele machines of gebruikers via een browser tooaccess Hallo internet Hallo bedrijf proxy niet wilt doorlopen, maar via Azure toohello rechtstreeks verbinding te maken met internet. Maar zelfs Hallo proxy-instellingen is niet een oplossing voor 100% toodirect Hallo-verkeer via Hallo bedrijf proxy, omdat het is de verantwoordelijkheid van de software en services toocheck voor Hallo proxy. Als software die wordt uitgevoerd in Hallo VM die niet actief of een beheerder Hallo instellingen bewerkt, verkeer toohello Internet opnieuw kunt detoured rechtstreeks via Azure toohello Internet.

In de volgorde tooavoid dit, u kunt geforceerde Tunneling configureren met site-naar-site-connectiviteit tussen on-premises en Azure. Hallo gedetailleerde beschrijving van geforceerde Tunneling Hallo-functie is gepubliceerd hier <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Geforceerde Tunneling met ExpressRoute wordt ingeschakeld door klanten kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies.

#### <a name="summary-of-azure-networking"></a>Overzicht van Azure-netwerken
In dit hoofdstuk bevat veel belangrijke punten over Azure-netwerken. Hier volgt een samenvatting van de belangrijkste punten Hallo:

* Virtuele netwerken van Azure kunt tooset Hallo netwerk volgens tooyour eigen behoeften
* Virtuele netwerken van Azure kunnen worden overgenomen tooassign IP-adresbereiken tooVMs of toewijzen van vaste IP-adressen tooVMs
* tooset u een Site-naar-Site of u eerst toocreate een Azure-netwerk moet punt-naar-Site-verbinding
* Wanneer een virtuele machine is geïmplementeerd, is het niet meer mogelijk toochange Hallo die virtueel netwerk toohello VM toegewezen

### <a name="quotas-in-azure-virtual-machine-services"></a>Quota's in de virtuele Machine van Azure Services
We moeten toobe wissen over Hallo feit die Hallo-opslag en infrastructuur van het netwerk wordt gedeeld tussen VM's met verschillende services in hello Azure-infrastructuur. En net zoals in Hallo van klant-datacenters overprovisioning van een aantal Hallo infrastructuur bronnen vindt plaats tooa mate. Hallo Microsoft Azure-Platform maakt gebruik van schijf, CPU, netwerk, en andere quota toolimit Hallo brongebruik en toopreserve consistent en deterministisch prestaties.  Hallo verschillende VM-typen (A5, A6, enzovoort) hebben verschillende quota's voor het aantal schijven, CPU, RAM, Hallo en netwerk.

> [!NOTE]
> CPU en geheugen resources van Hallo VM die worden ondersteund door SAP zijn vooraf toegewezen op Hallo hostknooppunten. Dit betekent dat zodra Hallo VM is geïmplementeerd, Hallo resources op Hallo host beschikbaar zijn, zoals gedefinieerd door Hallo VM-type zijn.
>
>

Wanneer planning en vergroten/verkleinen SAP op Azure-oplossingen Hallo quota's voor de grootte van elke virtuele machine moeten worden overwogen. Hallo VM quota worden beschreven [hier (Linux)] [ virtual-machines-sizes-linux] en [hier (Windows)][virtual-machines-sizes-windows].

Hallo quota's beschreven vertegenwoordigen Hallo theoretische maximale waarden.  Hallo-limiet van IOP's per schijf kan worden bereikt met kleine IOs (8kb), maar mogelijk niet kan worden bereikt met grote IOs (1Mb).  Hallo IOPS limiet wordt afgedwongen op Hallo granulatie van één schijf.

Als een ruwe decision tree toodecide kan of een SAP-systeem in Azure Services op virtuele Machine en de mogelijkheden ervan past of of een bestaand systeem toobe anders geconfigureerd in volgorde toodeploy Hallo systeem op Azure, moet Hallo beslissingsstructuur onderstaande worden gebruikt:

![Decision tree toodecide mogelijkheid toodeploy SAP op Azure][planning-guide-figure-700]

**Stap 1**: Hallo belangrijkste informatie toostart met is Hallo SAP's vereiste voor een bepaald SAP-systeem. Hallo SAP's vereisten nodig toobe gescheiden in Hallo DBMS onderdeel en Hallo SAP-toepassingsonderdeel, zelfs als Hallo SAP-systeem al is geïmplementeerd op lokale in een configuratie met 2-laag. Voor bestaande systemen Hallo SAP's gerelateerde toohello computerhardware vaak kan worden bepaald of geschatte gebaseerd op bestaande SAP benchmarks. Hallo resultaten vindt u hier: <http://global.sap.com/campaigns/benchmark/index.epx>.
Voor geïmplementeerde SAP-systemen, moet u hebben doorlopen een oefening sizing Hallo SAP's vereisten van Hallo system moet vast te stellen.
Zie ook deze blog en bijgevoegde document voor SAP sizing op Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Stap 2**: Hallo van bestaande systemen i/o-volume en i/o-bewerkingen per seconde op Hallo DBMS-server moeten worden gemeten. Voor nieuwe geplande systemen geeft Hallo dat oefening voor het nieuwe systeem Hallo ook sizing ruwe ideeën Hallo i/o-vereisten op Hallo DBMS aan clientzijde. Als u niet zeker, moet u uiteindelijk tooconduct een bewijs van Concept.

**Stap 3**: vergelijken Hallo SAP's vereiste voor Hallo DBMS-server met Hallo SAP's Hallo VM soorten Azure biedt. Hallo-informatie over SAP's Hallo verschillende soorten virtuele machine in Azure wordt beschreven in SAP-notitie [1928533]. Hallo focus moet zich op Hallo DBMS VM eerst omdat databaselaag Hallo Hallo laag in een SAP NetWeaver-systeem dat komt niet in de meeste Hallo-implementaties worden uitgebreid. Daarentegen kan aan Hallo SAP toepassingslaag worden uitgebreid. Als Hallo SAP worden niet ondersteund Azure VM typen Hallo vereist SAP's kunnen leveren, Hallo werkbelasting voor de geplande Hallo SAP-systeem kan niet worden uitgevoerd op Azure. Moet u ofwel toodeploy Hallo system lokale of moet u toochange Hallo werkbelasting volume voor Hallo-systeem.

**Stap 4**: zoals beschreven [hier (Linux)] [ virtual-machines-sizes-linux] en [hier (Windows)][virtual-machines-sizes-windows], Azure dwingt een quotum IOP's per schijf onafhankelijke of u Standard-opslag- of Premium-opslag gebruiken. Afhankelijk van Hallo VM-type, varieert van Hallo aantal gegevensschijven dat kan worden gekoppeld. Als gevolg hiervan kunt u het maximum aantal IOPS dat kan worden bereikt met elk van de andere VM-typen Hallo berekenen. Afhankelijk van bestandsopmaak Hallo-database, u kunt stripe schijven toobecome één volume in Hallo gastbesturingssysteem. Echter, als huidige IOPS volume van een geïmplementeerde SAP-systeem Hallo Hallo berekend limieten van het grootste VM-type Hallo van Azure en als er geen toocompensate kans meer geheugen overschrijdt, Hallo werkbelasting Hallo SAP-systeem kan worden beïnvloed ernstige problemen. In dergelijke gevallen kunt u een punt waar moet u niet Hallo systeem in Azure implementeren bereikt.

**Stap 5**: met name in SAP-systemen, lokale in laag 2-configuraties die zijn geïmplementeerd, zijn Hallo kans op Hallo system die mogelijk nodig hebt geconfigureerd in Azure in een configuratie met 3-Laagse toobe. In deze stap moet u toocheck of er een onderdeel in Hallo SAP toepassingslaag is, die niet worden uitgebreid en die niet in Hallo CPU en geheugen resources Hallo andere virtuele machine van Azure typen aanbieding zou passen. Als er inderdaad een dergelijke component, kunnen niet Hallo SAP-systeem en de werkbelasting worden geïmplementeerd in Azure. Maar als u Hallo SAP-toepassingsonderdelen in meerdere virtuele machines van Azure uitbreiden kunt, Hallo-systeem kan worden geïmplementeerd in Azure.

**Stap 6**: als Hallo DBMS en SAP-toepassingsonderdelen laag kunnen worden uitgevoerd in Azure VM's, Hallo configuratie moet toobe gedefinieerd met betrekking tot:

* Aantal virtuele machines in Azure
* VM-typen voor de afzonderlijke onderdelen Hallo
* Het aantal virtuele harde schijven DBMS VM tooprovide voldoende IOP's

## <a name="managing-azure-assets"></a>Azure activa te beheren
### <a name="azure-portal"></a>Azure Portal
Hello Azure-portal is een van drie interfaces toomanage Azure VM-implementaties. Hallo basic beheertaken, zoals het implementeren van virtuele machines van afbeeldingen, kunnen worden uitgevoerd via hello Azure-portal. Bovendien Hallo maken van Opslagaccounts, virtuele netwerken en andere Azure-onderdelen zijn ook taken hello Azure-portal uitstekend kan verwerken. Functionaliteit zoals VHD's vanuit het lokale tooAzure te uploaden of kopiëren van een VHD in Azure zijn echter taken, die de hulpprogramma's van derden of via PowerShell of CLI beheer vereist.

![Microsoft Azure portal - overzicht van virtuele machines][planning-guide-figure-800]

[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Beheer- en configuratietaken voor de instantie van de virtuele Machine Hallo zijn mogelijk van binnen hello Azure-portal.

Naast het opnieuw opstarten of afsluiten van een virtuele Machine kunt u ook koppelen, los te koppelen, en gegevensschijven voor Hallo-exemplaar voor virtuele Machine, toocapture Hallo-exemplaar voor de voorbereiding van de installatiekopie maken en configureren Hallo grootte van de instantie van de virtuele Machine Hallo.

Hello Azure-portal biedt basisfunctionaliteit toodeploy en virtuele machines en vele andere Azure-services configureren. Maar niet alle beschikbare functionaliteit wordt gedekt door hello Azure-portal. In hello Azure-portal is het niet mogelijk tooperform taken, zoals:

* VHD's tooAzure uploaden
* Kopiëren van virtuele machines

[comment]: <> (MShermannd TODO wat over automatisering in service voor SAP VM's?)
[comment]: <> (Implementatie van meerdere virtuele machines os ondertussen mogelijk MSSedusch)
[comment]: <> (Elk type automatisering met betrekking tot implementatie is MSSedusch ook niet mogelijk met hello Azure-portal. Taken, zoals implementatie van meerdere virtuele machines met scripts is niet mogelijk via hello Azure-portal.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Beheer via Microsoft Azure PowerShell-cmdlets
Windows PowerShell is een krachtig en uitbreidbaar framework dat veel is vastgesteld door klanten groot aantal systemen in Azure implementeren. Na de installatie van PowerShell-cmdlets op een desktop-, laptop- of toegewezen management station Hallo worden Hallo PowerShell-cmdlets op afstand uitgevoerd.

Hallo proces tooenable een lokale bureaublad/laptop Hallo gebruik van Azure PowerShell-cmdlets en de wijze waarop tooconfigure die voor gebruik met Hallo hello Azure abonnementen is beschreven in [in dit artikel][powershell-install-configure].

Meer gedetailleerde stappen over hoe tooinstall, bijwerken en configureren van hello Azure PowerShell-cmdlets kunnen worden gevonden [in dit hoofdstuk Hallo Deployment Guide][deployment-guide-4.1].

Ervaring van de klant is tot nu toe PowerShell (PS) is gewoon Hallo krachtige hulpprogramma toodeploy VM's en aangepaste toocreate stappen in Hallo-implementatie van virtuele machines. Alle Hallo klanten SAP-exemplaren in Azure wordt uitgevoerd met behulp van PS cmdlets toosupplement beheertaken zij in hello Azure-portal of zelfs PS-cmdlets gebruikt uitsluitend toomanage implementaties in Azure. Aangezien hello Azure-specifieke cmdlets share hello dezelfde naamgevingsconventie als Hallo meer dan 2000 Windows-gerelateerde cmdlets, is een eenvoudig de taak voor Windows-beheerders tooleverage die cmdlets.

Zie het voorbeeld hier: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO beschrijven nieuwe CLI-opdracht wanneer getest)
Implementatie van hello Azure extensie Monitoring voor SAP (Zie hoofdstuk [Azure Monitoring Solution voor SAP] [ planning-guide-9.1] in dit document) is alleen mogelijk via PowerShell of CLI. Daarom is verplicht tooset en PowerShell of CLI bij het implementeren of beheren van een systeem SAP NetWeaver in Azure te configureren.  

Als Azure meer functionaliteit biedt, gaan nieuwe PS-cmdlets toobe toegevoegd die moet worden bijgewerkt van Hallo-cmdlets. Daarom is het zin toocheck hello Azure downloaden site ten minste eenmaal Hallo maand <https://azure.microsoft.com/downloads/> voor een nieuwe versie van het Hallo-cmdlets. Hallo nieuwe versie is boven op Hallo oudere versie geïnstalleerd.

Voor een algemeen overzicht van Azure-gerelateerde PowerShell opdrachten hier controleren: <https://docs.microsoft.com/powershell/azure/overview>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Beheer via Microsoft Azure CLI-opdrachten
Voor klanten die Linux gebruiken en wilt toomanage Azure Powershell resources mogelijk niet een optie. Als alternatief biedt Microsoft Azure CLI.
Hello Azure CLI biedt een set van open-source platformoverschrijdende opdrachten voor het werken met hello Azure-Platform. Hello Azure CLI biedt vrijwel Hallo dezelfde functionaliteit in hello Azure-portal gevonden.

Zie voor informatie over de installatie, configuratie en hoe toouse CLI-opdrachten tooaccomplish Azure taken

* [Hello Azure CLI installeren][xplat-cli]
* [Implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en hello Azure CLI] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager gebruiken][xplat-cli-azure-resource-manager]

Lees ook hoofdstuk [Azure CLI voor virtuele Linux-machines] [ deployment-guide-4.5.2] in Hallo [Deployment Guide] [ planning-guide] op hoe toouse Azure CLI toodeploy hello Azure-bewaking De extensie voor SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Verschillende manieren toodeploy virtuele machines voor SAP in Azure
In dit hoofdstuk leert u Hallo verschillende manieren toodeploy een virtuele machine in Azure. Extra voorbereiding procedures, evenals de verwerking van VHD's en virtuele machines in Azure worden besproken in dit hoofdstuk.

### <a name="deployment-of-vms-for-sap"></a>Implementatie van virtuele machines voor SAP
Microsoft Azure biedt verschillende manieren toodeploy virtuele machines en gekoppelde schijven. Het is dus zeer belangrijk toounderstand Hallo verschillen sinds de voorbereiding van de virtuele machines Hallo mogelijk verschillen afhankelijk van Hallo implementatiemethode. We nemen in het algemeen bekijkt hello volgen scenario's:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Verplaatsen van een virtuele machine van de lokale tooAzure met een niet-gegeneraliseerd schijf
U van plan bent een specifiek systeem SAP van lokale tooAzure toomove. Dit kan worden gedaan door Hallo VHD waarin Hallo OS uploaden, Hallo SAP binaire bestanden en binaire bestanden DBMS plus Hallo VHD's met de gegevens en logboekbestanden bestanden Hallo van Hallo DBMS tooAzure. Daarentegen te[scenario #2 hieronder][planning-guide-5.1.2], houdt u Hallo hostnaam, SAP-SID en SAP gebruikersaccounts in Azure VM Hallo zoals ze zijn geconfigureerd in Hallo on-premises omgeving. Hallo installatiekopie generaliseren is daarom niet nodig. Zie de hoofdstukken [voorbereiding voor het verplaatsen van een virtuele machine van de lokale tooAzure met een schijf niet gegeneraliseerd] [ planning-guide-5.2.1] van dit document voor de voorbereidende stappen op lokale en uploaden van niet-gegeneraliseerde virtuele machines of VHD's tooAzure. Lees hoofdstuk [Scenario 3: een virtuele machine verplaatsen van on-premises met een VHD Azure niet gegeneraliseerd met SAP] [ deployment-guide-3.4] in Hallo [Deployment Guide] [ deployment-guide] voor gedetailleerde stappen voor het implementeren van dergelijke een installatiekopie in Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Een virtuele machine met een installatiekopie klantspecifieke implementeren
Vervaldatum toospecific patch vereisten van uw besturingssysteem of DBMS-versie, mogelijk Hallo opgegeven afbeeldingen in hello Azure Marketplace niet aansluiten bij uw behoeften. Daarom moet u mogelijk toocreate een VM die gebruikmaakt van uw eigen 'persoonlijke' OS/DBMS VM-installatiekopie, die verschillende keren daarna kan worden geïmplementeerd. een 'persoonlijke' installatiekopie voor duplicatie tooprepare, Hallo volgende items hebt toobe beschouwd als:

- - -
> ![Windows][Logo_Windows] Windows
>
> Hier voor meer informatie: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> Hallo Windows-instellingen (zoals Windows SID en de hostnaam) moeten worden gescheiden/gegeneraliseerd op Hallo on-premises Virtuele machine via de opdracht sysprep Hallo.
>
>
> ![Linux][Logo_Linux] Linux
>
> Hallo stappen wordt beschreven in deze artikelen voor [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], of [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooprepare een VHD-toobe tooAzure geüpload.
>
>

- - -
Als u al SAP-inhoud in uw lokale virtuele machine (vooral voor laag 2-systemen) hebt geïnstalleerd, kunt u Hallo SAP-systeeminstellingen aanpassen nadat het Hallo-implementatie van hello Azure VM via Hallo instantie naam van procedure ondersteund door Hallo SAP softwarelevering Manager (SAP-notitie [1619720]). Zie de hoofdstukken [voorbereiding voor het implementeren van een virtuele machine met een installatiekopie klantspecifieke voor SAP] [ planning-guide-5.2.2] en [uploaden van een VHD van lokale tooAzure] [ planning-guide-5.3.2]van dit document voor de voorbereidende stappen op lokale en uploaden van een gegeneraliseerde VM tooAzure. Lees hoofdstuk [Scenario 2: een virtuele machine met een aangepaste installatiekopie implementeren voor SAP] [ deployment-guide-3.3] in Hallo [Deployment Guide] [ deployment-guide] voor gedetailleerde stappen voor het implementeren van dergelijke een installatiekopie in Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Implementatie van een virtuele machine buiten hello Azure Marketplace
U wilt, toouse een Microsoft of derden opgegeven VM-installatiekopie uit hello Azure Marketplace toodeploy uw virtuele machine. Nadat u uw virtuele machine in Azure hebt geïmplementeerd, volgt u Hallo dezelfde richtlijnen en hulpprogramma's voor tooinstall SAP-software en/of DBMS in uw virtuele machine Hallo zoals u in een on-premises omgeving doen zou. Voor een beschrijving van de implementatie gedetailleerde, Zie hoofdstuk [Scenario 1: implementatie van een virtuele machine buiten hello Azure Marketplace voor SAP] [ deployment-guide-3.2] in Hallo [Deployment Guide] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Virtuele machines met SAP voorbereiden voor Azure
U moet toomake ervoor Hallo virtuele machines en VHD's te voldoen aan bepaalde vereisten voordat u virtuele machines in Azure uploadt. Er zijn kleine verschillen, afhankelijk van de implementatiemethode Hallo die wordt gebruikt.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Voorbereiding voor het verplaatsen van een virtuele machine van de lokale tooAzure met een niet-gegeneraliseerd schijf
Een algemene implementatiemethode is een bestaande virtuele machine die wordt uitgevoerd een SAP-systeem van lokale tooAzure toomove. Virtuele machine en Hallo SAP-systeem in Hallo VM alleen moet worden uitgevoerd in Azure met behulp Hallo van dezelfde hostnaam en zeer waarschijnlijk Hallo dezelfde SAP-SID. In dit geval Hallo Gast OS van virtuele machine niet worden gegeneraliseerd voor meerdere implementaties. Als de Hallo on-premises netwerk in Azure hebt uitgebreid (Zie hoofdstuk [cross-premises - implementatie van één of meerdere SAP-virtuele machines in Azure met de vereiste Hallo van volledig geïntegreerd in Hallo on-premises netwerk] [ planning-guide-2.2] in dit document), vervolgens zelfs Hallo dezelfde domeinaccounts kunnen worden gebruikt binnen Hallo VM zoals die zijn gebruikt voor lokale.

Vereisten voor het voorbereiden van uw eigen Azure VM-schijf zijn:

* Hallo VHD met Hallo besturingssysteem wellicht oorspronkelijk alleen een maximale grootte van 127GB. Deze beperking is geëlimineerd aan Hallo einde van maart 2015. Nu mag hello VHD Hallo-besturingssysteem met up too1TB in grootte als andere Azure-Storage VHD ook gehoste.
* Het moet toobe in Hallo vaste VHD-indeling. Dynamische virtuele harde schijven of VHD's in de VHDx-indeling zijn nog niet ondersteund in Azure. Dynamische virtuele harde schijven worden geconverteerd toostatic VHD's tijdens het uploaden van Hallo VHD met commandlets PowerShell of CLI
* VHD's die zijn gekoppeld toohello VM en opnieuw in Azure toohello VM nodig toobe in een vaste VHD-indeling ook moeten worden gekoppeld. Lees [in dit artikel (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) en [in dit artikel (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) voor de maximale grootte van gegevensschijven. Dynamische virtuele harde schijven worden geconverteerd toostatic VHD's tijdens het uploaden van Hallo VHD met commandlets PowerShell of CLI
* Voeg een andere lokale account met administrator-bevoegdheden die kunnen worden gebruikt door de Microsoft-ondersteuning of die kunnen worden toegewezen als context voor services en toepassingen toorun in tot Hallo die VM is geïmplementeerd en geschiktere gebruikers kan worden gebruikt.
* Voor Hallo-aanvraag van het gebruik van een scenario alleen in de Cloud-implementaties (Zie hoofdstuk [alleen in de Cloud - implementaties van virtuele machines in Azure zonder afhankelijkheden op Hallo lokale klantnetwerk] [ planning-guide-2.1] van deze -document) in combinatie met deze methode-implementatie domein accounts niet werken mogelijk zodra hello Azure-schijf is geïmplementeerd in Azure. Dit geldt met name voor accounts die gebruikt toorun services zoals Hallo DBMS of SAP-toepassingen zijn. Daarom moet tooreplace dergelijke domeinaccounts met lokale accounts VM en Hallo lokale domeinaccounts in Hallo VM te verwijderen. On-premises domeingebruikers houden in Hallo VM-installatiekopie is niet een probleem bij het Hallo VM is geïmplementeerd in Hallo cross-premises scenario zoals beschreven in hoofdstuk [Cross-Premises - implementatie van één of meerdere SAP-virtuele machines in Azure met de vereiste Hallo is volledig geïntegreerd in Hallo on-premises netwerk] [ planning-guide-2.2] in dit document.
* Als domeinaccounts zijn gebruikt als DBMS aanmeldingen of gebruikers bij het uitvoeren van Hallo system on-premises en deze VMs toobe in scenario's alleen in de Cloud worden geïmplementeerd mogen, moeten Hallo domeingebruikers toobe verwijderd. U moet toomake of de lokale beheerder Hallo plus een andere VM lokale gebruiker is toegevoegd als een aanmeldingsgebruiker in Hallo DBMS als beheerder.
* Add andere lokale accounts kunnen die nodig zijn voor de specifieke implementatiescenario Hallo.

- - -
> ![Windows][Logo_Windows] Windows
>
> In dit scenario is geen generaliseren (sysprep) Hallo VM tooupload vereist is, en implementeren van Hallo VM op Azure.
> Zorg ervoor dat station die d:\ wordt niet gebruikt.
> Schijf automount voor gekoppelde schijven ingesteld zoals beschreven in hoofdstuk [instelling automount voor gekoppelde schijven] [ planning-guide-5.5.3] in dit document.
>
> ![Linux][Logo_Linux] Linux
>
> In dit scenario geen generaliseren (waagent-deprovision) Hallo VM is vereist tooupload en implementeren van Hallo VM op Azure.
> Zorg ervoor dat mnt/resourcegroep niet wordt gebruikt en dat alle schijven zijn gekoppeld via de uuid. Zorg ervoor dat Hallo bootloader vermelding ook Hallo uuid gebaseerde koppelpunt weerspiegelt Hallo OS-schijf.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Voorbereiding voor het implementeren van een virtuele machine met een installatiekopie klantspecifieke voor SAP
VHD-bestanden met een gegeneraliseerde OS worden opgeslagen in de containers op Azure Storage-Accounts of als schijfkopieën beheerd. U kunt een nieuwe virtuele machine van een dergelijke installatiekopie implementeren die verwijzen naar Hallo VHD of beheerd schijfkopie als een bron in uw implementatie sjabloonbestanden zoals beschreven in hoofdstuk [Scenario 2: een virtuele machine met een aangepaste installatiekopie implementeren voor SAP] [ deployment-guide-3.3]Hallo [Deployment Guide][deployment-guide].

Vereisten bij het voorbereiden van uw eigen Azure VM-installatiekopie zijn:

* Hallo VHD met Hallo besturingssysteem wellicht oorspronkelijk alleen een maximale grootte van 127GB. Deze beperking is geëlimineerd aan Hallo einde van maart 2015. Nu mag hello VHD Hallo-besturingssysteem met up too1TB in grootte als andere Azure-Storage VHD ook gehoste.
* Het moet toobe in Hallo vaste VHD-indeling. Dynamische virtuele harde schijven of VHD's in de VHDx-indeling zijn nog niet ondersteund in Azure. Dynamische virtuele harde schijven worden geconverteerd toostatic VHD's tijdens het uploaden van Hallo VHD met commandlets PowerShell of CLI
* VHD's die zijn gekoppeld toohello VM en opnieuw in Azure toohello VM nodig toobe in een vaste VHD-indeling ook moeten worden gekoppeld. Lees [in dit artikel (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) en [in dit artikel (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) voor de maximale grootte van gegevensschijven. Dynamische virtuele harde schijven worden geconverteerd toostatic VHD's tijdens het uploaden van Hallo VHD met commandlets PowerShell of CLI
* Aangezien alle domeingebruikers geregistreerd als gebruikers in Hallo VM niet in een scenario alleen in de Cloud bestaat Hallo (Zie hoofdstuk [alleen in de Cloud - implementaties van virtuele machines in Azure zonder afhankelijkheden op Hallo lokale klantnetwerk] [ planning-guide-2.1] van dit document), gebruik van dergelijke accounts niet werken mogelijk als Hallo installatiekopie wordt geïmplementeerd in Azure-domein services. Dit geldt met name voor accounts die gebruikt toorun services zoals DBMS of SAP-toepassingen zijn. Daarom moet tooreplace dergelijke domeinaccounts met lokale accounts VM en Hallo lokale domeinaccounts in Hallo VM te verwijderen. On-premises domeingebruikers houden in Hallo VM-installatiekopie niet mogelijk een probleem wanneer Hallo VM is geïmplementeerd in Hallo cross-premises scenario zoals beschreven in hoofdstuk [Cross-Premises - implementatie van één of meerdere SAP-virtuele machines in Azure met de vereiste Hallo van volledig geïntegreerd in Hallo on-premises netwerk] [ planning-guide-2.2] in dit document.
* Voeg een andere lokale account met administrator-bevoegdheden die kan worden gebruikt door de Microsoft-ondersteuning in probleem onderzoeken of die kunnen worden toegewezen als context voor services en toepassingen toorun in tot Hallo die VM is geïmplementeerd en geschiktere gebruikers kan worden gebruikt.
* In de Cloud-implementaties en domeinaccounts zijn gebruikt als DBMS aanmeldingen of gebruikers bij het uitvoeren van systeem lokale Hallo moeten Hallo domeingebruikers worden verwijderd. U moet toomake ervoor dat de lokale beheerder Hallo plus een andere VM lokale gebruiker is toegevoegd als een aanmeldingsgebruiker Hallo DBMS als beheerder.
* Add andere lokale accounts kunnen die nodig zijn voor de specifieke implementatiescenario Hallo.
* Als Hallo afbeelding een installatie van SAP NetWeaver bevat en het hernoemen van Hallo hostnaam op uit de oorspronkelijke naam Hallo bij Hallo hello Azure-implementatie is het waarschijnlijk, is het aanbevolen toocopy Hallo nieuwste versies van Hallo SAP Software inrichten Manager DVD in Hallo-sjabloon. Hierdoor kunt u tooeasily gebruik Hallo SAP mits hernoemen functionaliteit tooadapt Hallo gewijzigd hostnaam en/of wijziging Hallo SID Hallo SAP-systeem binnen Hallo VM-installatiekopie worden geïmplementeerd als een nieuw exemplaar wordt gestart.

- - -
> ![Windows][Logo_Windows] Windows
>
> Zorg ervoor dat station D:\ niet is ingesteld schijf automount voor de gekoppelde schijven gebruikt zoals beschreven in hoofdstuk [instelling automount voor gekoppelde schijven] [ planning-guide-5.5.3] in dit document.
>
> ![Linux][Logo_Linux] Linux
>
> Zorg ervoor dat mnt/resourcegroep niet wordt gebruikt en dat alle schijven zijn gekoppeld via de uuid. Zorg ervoor Hallo bootloader vermelding weerspiegelt ook Hallo uuid gebaseerde koppelpunt Hallo OS-schijf.
>
>

- - -
* SAP-GUI (voor administratieve en doeleinden setup) vooraf in deze sjabloon kan worden geïnstalleerd.
* Andere software nodig toorun Hallo VM's is in de cross-premises scenario's kunnen worden geïnstalleerd, zolang deze software met Hallo werken kunt Hallo VM wijzigen.

Als Hallo VM voldoende is voorbereid toobe generieke en uiteindelijk onafhankelijk van accounts/gebruikers niet beschikbaar in hello Azure implementatiescenario gericht, Hallo laatste voorbereiding stap van het generaliseren van dergelijke een afbeelding wordt uitgevoerd.

##### <a name="generalizing-a-vm"></a>Het generaliseren van een virtuele machine
- - -
> ![Windows][Logo_Windows] Windows
>
> de laatste stap Hallo is toolog in tooa VM met een administratoraccount. Open een opdrachtvenster Windows als 'administrator'. Ga too%windir%\windows\system32\sysprep en sysprep.exe uitvoeren.
> Een klein venster wordt weergegeven. Het is belangrijk toocheck Hallo 'Generalize' optie (Hallo is standaard uitgeschakeld) en wijzig Hallo optie afsluiten van de standaardinstelling 'Opnieuw opstarten' too'Shutdown'. Deze procedure wordt ervan uitgegaan dat de sysprep-proces Hallo uitgevoerde lokale in Hallo Gastbesturingssysteem van een virtuele machine.
> Als u wilt dat tooperform Hallo procedure met een VM die al worden uitgevoerd in Azure, stappen Hallo beschreven in [in dit artikel](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource).
>
> ![Linux][Logo_Linux] Linux
>
> [Hoe toocapture een toouse Linux virtuele machine als Resource Manager-sjabloon][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Virtuele machines en VHD's overbrengen tussen lokale tooAzure
Omdat de VM-installatiekopieën en schijven tooAzure uploaden is niet mogelijk via hello Azure-portal, moet u Azure PowerShell-cmdlets voor toouse of CLI. Een andere mogelijkheid is Hallo gebruik van hulpprogramma Hallo 'AzCopy'. Hallo hulpprogramma kunt VHD's kopiëren tussen on-premises en Azure (in beide richtingen). Het kan ook VHD's tussen Azure-gebieden kopiëren. Neem contact op met [deze documentatie] [ storage-use-azcopy] voor download en gebruik van AzCopy.

Een derde alternatieve zou worden toouse verschillende grafische gebruikersinterface gebaseerde hulpprogramma's van derden. Echter, zorg dat deze hulpprogramma's zijn ondersteuning van Azure-pagina-Blobs. Voor het opslaan van onze toepassing moet toouse Azure-pagina-Blob (Hallo verschillen worden hier beschreven: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). Hallo-hulpprogramma's van Azure zijn ook zeer efficiënt voor het comprimeren van Hallo virtuele machines en VHD's die toobe geüpload moeten. Dit is belangrijk omdat deze efficiëntie in compressie Hallo-tijd voor uploaden vermindert (die toch varieert, afhankelijk van Hallo uploaden koppeling toohello internet vanaf Hallo lokale faciliteit en hello Azure-implementatie regio gericht). Het is een evenwichtige veronderstelling dat een virtuele machine of een VHD uploaden vanaf de locatie van de Europese toohello VS gebaseerde Azure data centers duurt langer dan het uploaden van dezelfde virtuele machines/VHD's toohello Europese Azure-datacenters Hallo.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Uploaden van een VHD van lokale tooAzure
een bestaande virtuele machine of de VHD van Hallo lokale VHD moet toomeet Hallo vereisten zoals vermeld in hoofdstuk of via het netwerk van een virtuele machine tooupload [voorbereiding voor het verplaatsen van een virtuele machine van de lokale tooAzure met een schijf niet gegeneraliseerd] [ planning-guide-5.2.1] van dit document.

Een virtuele machine hoeft niet toobe gegeneraliseerd en kan worden geüpload in Hallo status en vorm heeft na afsluiten op Hallo lokale aan clientzijde. Hallo geldt voor extra virtuele harde schijven die niet elk besturingssysteem bevatten.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Een VHD uploaden en waardoor het een Azure-schijf
In dit geval we tooupload een VHD, met of zonder een besturingssysteem, wilt tooa virtuele machine als een gegevensschijf koppelen en gebruiken als de besturingssysteemschijf. Dit is een proces met meerdere stappen

**Powershell**

* Meld u bij tooyour abonnement met *Login-AzureRmAccount*
* Hallo-abonnement van uw context met ingesteld *Set-AzureRmContext* en parameter abonnements-id of SubscriptionName - Zie <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Uploaden Hallo VHD met *toevoegen AzureRmVhd* tooan Azure Storage-Account - Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Optioneel) Maken van een schijf beheerd vanuit Hallo VHD met *nieuw AzureRmDisk* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* Stel Hallo OS-schijf van een nieuwe VM config toohello VHD of beheerd met *Set AzureRmVMOSDisk* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* Een nieuwe virtuele machine maken van VM-configuratie met Hallo *New-AzureRmVM* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* Voeg een schijf gegevens tooa nieuwe virtuele machine met *toevoegen AzureRmVMDataDisk* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Azure CLI 2.0**

* Meld u bij tooyour abonnement met *az aanmelding*
* Selecteer uw abonnement met *az account set--abonnement`<subscription name or id`>*
* Uploaden Hallo VHD met *uploaden van blob storage az* -Zie [Using hello Azure CLI met Azure Storage][storage-azure-cli]
* (Optioneel) Maken van een schijf beheerd vanuit Hallo VHD met *az schijf maken* -Zie https://docs.microsoft.com/cli/azure/disk#create
* Maak een nieuwe VM geven Hallo geüpload VHD- of schijf beheerd als besturingssysteemschijf met *az vm maken* en parameter *--koppelen-os-schijf*
* Voeg een schijf gegevens tooa nieuwe virtuele machine met *az vm schijf koppelen* en parameter *--nieuwe*

**Sjabloon**

* Hallo VHD met Powershell of Azure CLI uploaden
* (Optioneel) Maken van een schijf beheerd van Hallo VHD met Powershell, Azure CLI of hello Azure-portal
* Hallo VM implementeren met een JSON-sjabloon die verwijzen naar Hallo VHD, zoals wordt weergegeven in [in dit voorbeeld JSON-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) of met behulp van schijven worden beheerd, zoals wordt weergegeven in [in dit voorbeeld JSON-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Implementatie van een VM-installatiekopie
een bestaande virtuele machine of de VHD van Hallo lokale netwerk in volgorde toouse deze als een installatiekopie van een virtuele machine in Azure een virtuele machine of de VHD moet toomeet Hallo vereisten in hoofdstuk tooupload [voorbereiding voor het implementeren van een virtuele machine met een installatiekopie klantspecifieke voor SAP] [ planning-guide-5.2.2] van dit document.

* Gebruik *sysprep* op Windows of *waagent-deprovision* op Linux toogeneralize uw VM - Zie [technische documentatie van Sysprep](https://technet.microsoft.com/library/cc766049.aspx) voor Windows of [hoe toocapture een Linux-virtuele machine toouse als Resource Manager-sjabloon] [ capture-image-linux-step-2-create-vm-image] voor Linux
* Meld u bij tooyour abonnement met *Login-AzureRmAccount*
* Hallo-abonnement van uw context met ingesteld *Set-AzureRmContext* en parameter abonnements-id of SubscriptionName - Zie <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Uploaden Hallo VHD met *toevoegen AzureRmVhd* tooan Azure Storage-Account - Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Optioneel) Maken van de installatiekopie van een beheerd schijf vanuit Hallo VHD met *nieuw AzureRmImage* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* Hallo OS-schijf van een nieuwe VM-config toothe instellen
  * VHD met *Set AzureRmVMOSDisk - SourceImageUri - CreateOption fromImage* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
  * Beheerde schijfimage *Set AzureRmVMSourceImage* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>
* Een nieuwe virtuele machine maken van VM-configuratie met Hallo *New-AzureRmVM* -Zie <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Azure CLI 2.0**

* Gebruik *sysprep* op Windows of *waagent-deprovision* op Linux toogeneralize uw VM - Zie [technische documentatie van Sysprep](https://technet.microsoft.com/library/cc766049.aspx) voor Windows of [hoe toocapture een Linux-virtuele machine toouse als Resource Manager-sjabloon] [ capture-image-linux-step-2-create-vm-image] voor Linux
* Meld u bij tooyour abonnement met *az aanmelding*
* Selecteer uw abonnement met *az account set--abonnement`<subscription name or id`>*
* Uploaden Hallo VHD met *uploaden van blob storage az* -Zie [Using hello Azure CLI met Azure Storage][storage-azure-cli]
* (Optioneel) Maken van de installatiekopie van een beheerd schijf vanuit Hallo VHD met *az installatiekopie maken* -Zie https://docs.microsoft.com/cli/azure/image#create
* Maak een nieuwe VM geven Hallo geüpload VHD- of schijfimage beheerd als besturingssysteemschijf met *az vm maken* en parameter *--installatiekopie*

**Sjabloon**

* Gebruik *sysprep* op Windows of *waagent-deprovision* op Linux toogeneralize uw VM - Zie [technische documentatie van Sysprep](https://technet.microsoft.com/library/cc766049.aspx) voor Windows of [hoe toocapture een Linux-virtuele machine toouse als Resource Manager-sjabloon] [ capture-image-linux-step-2-create-vm-image] voor Linux
* Hallo VHD met Powershell of Azure CLI uploaden
* (Optioneel) Maken van de installatiekopie van een beheerd schijf vanuit Hallo VHD met Powershell, Azure CLI of hello Azure-portal
* Hallo VM implementeren met een JSON-sjabloon die verwijzen naar Hallo installatiekopie VHD, zoals wordt weergegeven in [in dit voorbeeld JSON-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) of met behulp van Hallo schijfimage beheerd zoals in [in dit voorbeeld JSON-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>VHD's of schijven beheerd tooon lokale downloaden
Azure-infrastructuur als een Service is niet een eenzijdige straat worden alleen kunnen tooupload VHD's en SAP-systemen. U kunt verplaatsen SAP systemen van Azure weer naar Hallo lokale wereld ook.

Tijdens Hallo van Hallo kan downloaden Hallo VHD's of schijven beheerd niet actief. Zelfs bij het downloaden van de schijven die gekoppeld tooVMs zijn Hallo VM behoeften toobe afsluiten en de toewijzing ongedaan gemaakt. Als u wilt dat alleen inhoud waarvan dan gebruikte tooset van een nieuw systeem on-premises en als het is acceptabel dat tijdens Hallo van Hallo downloaden en installatie van nieuwe Hallo Hallo systeem dat systeem in Azure Hallo kan nog steeds operationeel toodownload Hallo-database , u kunt een lange uitvaltijd voorkomen door het uitvoeren van een gecomprimeerde databaseback-up naar een schijf en alleen downloaden die schijf in plaats van gedownload ook Hallo OS base VM.

#### <a name="powershell"></a>PowerShell

  * Downloaden van een beheerde schijf  
  U moet eerst tooget toegang toohello onderliggende blob Hallo beheerd schijf. Vervolgens kunt u kopiëren Hallo onderliggende blob tooa nieuwe storage-account en Hallo blob downloaden van dit opslagaccount.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * Downloaden van een VHD  
  Als Hallo SAP-systeem wordt gestopt en hello VM wordt afgesloten, kunt u Hallo PowerShell-cmdlet opslaan AzureRmVhd op Hallo lokale back-doel toodownload Hallo VHD schijven toohello lokale wereld. In de volgorde toodo, moet u Hallo-URL van de VHD die u in Hallo 'Opslagsectie vinden kunt' Hallo Hallo moet Azure-portal (nodig toonavigate toohello Storage-Account en Hallo storage-container waarin hello VHD is gemaakt) en u tooknow waar hello VHD moet worden gekopieerd naar.

  Vervolgens kunt u gebruikmaken van Hallo opdracht als u gewoon Hallo parameter SourceUri als URL van Hallo VHD toodownload en Hallo LocalFilePath Hallo door als te definiëren Hallo fysieke locatie van Hallo VHD (inclusief de naam). Hallo-opdracht kan eruitzien als:

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Voor meer details van de cmdlet Hallo opslaan AzureRmVhd Controleer hier <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>.

#### <a name="cli-20"></a>CLI 2.0
  * Downloaden van een beheerde schijf  
  U moet eerst tooget toegang toohello onderliggende blob Hallo beheerd schijf. Vervolgens kunt u kopiëren Hallo onderliggende blob tooa nieuwe storage-account en Hallo blob downloaden van dit opslagaccount.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * Downloaden van een VHD   
  Zodra de Hallo SAP-systeem wordt gestopt en hello VM wordt afgesloten, kunt u hello Azure CLI opdracht _downloaden van de azure-opslag-blob_ op Hallo lokale doel toodownload Hallo VHD back toohello lokale world schijven. In de volgorde toodo, moet u Hallo naam en het Hallo-container van VHD die u in Hallo 'Opslagsectie vinden kunt' Hallo Hallo Azure-portal (nodig toonavigate toohello Storage-Account en Hallo storage-container waarin hello VHD is gemaakt) en u moet tooknow waar Hallo VHD moet worden gekopieerd naar.

  Vervolgens kunt u de opdracht Hallo gebruikmaken door te definiëren gewoon Hallo parameters blobs en containers van Hallo VHD toodownload en Hallo bestemming als fysieke doellocatie Hallo Hallo VHD (inclusief de naam). Hallo-opdracht kan eruitzien als:

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>Overdracht van virtuele machines en de schijven in Azure
#### <a name="copying-sap-systems-within-azure"></a>SAP-systemen binnen Azure kopiëren
Een SAP-systeem of zelfs een speciale DBMS-server een SAP-toepassingslaag ondersteunende wordt waarschijnlijk bestaan uit meerdere schijven die beide Hallo OS met Hallo binaire bestanden bevatten of gegevens Hallo en logbestanden van Hallo SAP-database. Hallo Azure functionaliteit van het kopiëren van schijven noch hello Azure functionaliteit van schijven tooa lokale schijf opslaan is een mechanisme voor synchronisatie, die meerdere schijven synchroon momentopname wilt maken. Daarom Hallo status Hallo gekopieerd of schijven opgeslagen, zelfs als die zijn gekoppeld tegen Hallo dezelfde virtuele machine zou afwijken. Dit betekent dat in concrete geval hebben verschillende gegevens en logfile(s) opgenomen in de verschillende schijven Hallo HALLO hallo-database in Hallo-end zou inconsistent.

**Conclusie: In volgorde toocopy of sla de schijven die deel uitmaken van een systeemconfiguratie SAP u nodig hebt toostop Hallo SAP-systeem en moet ook geïmplementeerd tooshut omlaag Hallo VM. En u kunt kopiëren of downloaden van de reeks schijven tooeither Hallo maakt u een kopie van Hallo SAP-systeem in Azure of on-premises.**

Gegevensschijven kunnen kunnen worden opgeslagen als VHD-bestanden in een Azure Storage-Account en rechtstreeks gekoppelde tooa virtuele machine of worden gebruikt als een afbeelding. In dit geval is Hallo VHD gekopieerde tooanother locatie voordat het wordt aangesloten toohello virtuele machine. volledige naam van VHD-bestand in Azure Hallo Hallo moet uniek zijn binnen Azure. Zoals al eerder vermeld, is Hallo type een driedelige naam die lijkt op:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Gegevensschijven kunnen ook worden beheerd schijven. Hallo beheerd schijf is in dit geval gebruikte toocreate nieuwe Managed schijf voordat het wordt aangesloten toohello virtuele machine. Hallo-naam van Hallo beheerd schijf moet uniek zijn binnen een resourcegroep.

##### <a name="powershell"></a>PowerShell
U kunt Azure PowerShell-cmdlets toocopy een VHD gebruiken zoals wordt weergegeven in [in dit artikel][storage-powershell-guide-full-copy-vhd]. toocreate een nieuwe schijf van de beheerde nieuw AzureRmDiskConfig en nieuw AzureRmDisk gebruiken zoals wordt weergegeven in het volgende voorbeeld Hallo.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>CLI 2.0
U kunt Azure CLI toocopy een VHD gebruiken zoals wordt weergegeven in [in dit artikel][storage-azure-cli-copy-blobs]. een nieuwe schijf van de beheerde toocreate gebruiken *az schijf maken* zoals weergegeven in Hallo voorbeeld te volgen.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Hulpprogramma's van Azure Storage
* <http://storageexplorer.com/>

Professional editions van Azure Storage Explorers vindt u hier:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

Hallo-kopie van een VHD zelf binnen een opslagaccount is een proces duurt slechts enkele seconden (vergelijkbaar tooSAN hardware bij het maken van momentopnamen met vertraagde kopiëren en een kopie op schrijven). Nadat u een kopie van de VHD-bestand Hallo hebt kunt u het koppelen tooa virtuele machine of gebruik het als een installatiekopie tooattach Hallo VHD toovirtual machines gekopieerd.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>CLI 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Kopiëren van schijven tussen Azure Storage-Accounts
Deze taak kan niet worden uitgevoerd op Hallo Azure-portal. U kunt Azure PowerShell-cmdlets, Azure CLI of een derde partij opslag browser gebruiken. Hallo PowerShell-cmdlets of de CLI-opdrachten kunnen maken en beheren van blobs, waaronder Hallo mogelijkheid tooasynchronously kopie BLOB's tussen Opslagaccounts en regio's binnen hello Azure-abonnement.

##### <a name="powershell"></a>PowerShell
U kunt ook virtuele harde schijven kopiëren tussen abonnementen. Lees voor meer informatie [in dit artikel][storage-powershell-guide-full-copy-vhd].

Hallo-basisstroom Hallo PS cmdlet logica ziet er als volgt:

* Een storage account context maken voor Hallo **bron** storage-account met *nieuw AzureStorageContext* -Zie <https://msdn.microsoft.com/library/dn806380.aspx>
* Een storage account context maken voor Hallo **doel** storage-account met *nieuw AzureStorageContext* -Zie <https://msdn.microsoft.com/library/dn806380.aspx>
* Hallo-exemplaar bij starten

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Controleer de status van Hallo kopie in een lus met Hallo

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Hallo nieuwe VHD tooa virtuele machine koppelen zoals hierboven beschreven.

Voor Zie voor voorbeelden [in dit artikel][storage-powershell-guide-full-copy-vhd].

##### <a name="cli-20"></a>CLI 2.0
* Hallo-exemplaar bij starten

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* Hallo-status controleren als hello kopiëren in een lus met

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Hallo nieuwe VHD tooa virtuele machine koppelen zoals hierboven beschreven.

Voor Zie voor voorbeelden [in dit artikel][storage-azure-cli-copy-blobs].

### <a name="disk-handling"></a>Verwerking van de schijf
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Structuur van een VM/schijf voor SAP-implementaties
In het ideale geval Hallo afhandeling van Hallo-structuur van een virtuele machine en Hallo gekoppeld schijven moeten zeer eenvoudig. Klanten ontwikkeld in on-premises installaties tal van manieren van structureren van een server-installatie.

* Een basisschijf die Hallo besturingssysteem bevat en alle Hallo binaire bestanden van Hallo DBMS en/of SAP. Sinds maart 2015 mag deze schijf up too1TB in grootte in plaats van eerdere beperkingen beperkt het too127GB.
* Een of meerdere schijven met Hallo DBMS logboekbestand van Hallo SAP-database als logboekbestand Hallo Hallo DBMS tijdelijke opslaggebied (als Hallo DBMS dit ondersteunt). Als het logboek Hallo-IOPS Databasevereisten hoog zijn, moet u toostripe meerdere schijven in de volgorde tooreach hello IOPS volume dat vereist is.
* Een aantal schijven met één of twee databasebestanden van Hallo SAP-database en Hallo DBMS tijdelijke gegevensbestanden ook (als Hallo DBMS dit ondersteunt).

![Verwijzing configuratie van Azure IaaS VM voor SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO beschrijven Linux-structuur)

- - -
> ![Windows][Logo_Windows] Windows
>
> Met veel klanten zagen we configuraties waar, bijvoorbeeld SAP en DBMS binaire bestanden zijn niet geïnstalleerd op de station c:\ Hallo waar hello besturingssysteem is geïnstalleerd. Er zijn diverse redenen hiervoor, maar toen we terug toohello hoofdmap probeerden, meestal was dat Hallo stations kort zijn en upgrades voor het besturingssysteem nodig extra ruimte 10-15 jaar geleden. Beide voorwaarden te vaak meer tegenwoordig niet van toepassing. Vandaag de dag kan Hallo c:\ station worden toegewezen op grote volumes schijven of virtuele machines. In de volgorde tookeep implementaties eenvoudige in de structuur, is het aanbevolen toofollow het volgende patroon van de implementatie voor SAP NetWeaver systemen in Azure
>
> Hallo Windows-besturingssysteem wisselbestand moet zich op Hallo D: station (niet-permanente schijf)
>
> ![Linux][Logo_Linux] Linux
>
> Hallo Linux swapfile onder mnt/mnt/resource plaats op Linux, zoals beschreven in [in dit artikel][virtual-machines-linux-agent-user-guide]. Hallo wisselbestand kan worden geconfigureerd in het configuratiebestand Hallo Hallo /etc/waagent.conf Linux-Agent. Toevoegen of wijzigen van Hallo volgende instellingen:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello wijzigingen, moet u toorestart Hallo met Linux-Agent

```
sudo service waagent restart
```

Lees SAP-notitie [1597355] voor meer informatie over Hallo aanbevolen grootte van wisselbestand

- - -
Hallo aantal schijven gebruikt Hallo DBMS gegevensbestanden en Hallo-type van deze schijven worden gehost op Azure-opslag moet worden bepaald door Hallo IOPS vereisten en Hallo latentie is vereist. Exacte quota worden beschreven in [in dit artikel (Linux)] [ virtual-machines-sizes-linux] en [in dit artikel (Windows)][virtual-machines-sizes-windows].

Ervaring van SAP implementaties via Hallo afgelopen 2 jaar geleerd ons enkele opgedane die kunnen worden samengevat als:

* IOPS verkeer toodifferent gegevensbestanden is niet altijd Hallo dezelfde omdat bestaande klantsystemen hebben anders gegevens grootte kunnen bestanden die hun SAP-database (s) vertegenwoordigt. Als gevolg hiervan bleek deze toobe beter gebruik van een RAID-configuratie via meerdere schijven tooplace Hallo gegevensbestanden die LUN 's oppervlaktevariaties buiten die. Er zijn situaties, met name Azure Standard-opslag waar de snelheid van een IOPS Hallo quotum van één schijf tegen Hallo DBMS transactielogboek bereikt. In dergelijke gevallen Hallo gebruik van Premium-opslag wordt aanbevolen of schijven met een software-RAID ook aggregeren meerdere Standard-opslag.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Best practices prestaties for SQL Server in Azure Virtual Machines][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Configureren van Software-RAID op Linux][virtual-machines-linux-configure-raid]
> * [LVM configureren op een virtuele Linux-machine in Azure][virtual-machines-linux-configure-lvm]
> * [Azure Storage-geheimen en Linux-i/o-optimalisatie](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Premium-opslag is aanzienlijk betere prestaties, met name voor kritieke transactie logboekschrijfbewerkingen weergegeven. Voor SAP scenario's die verwachte toodeliver productie zoals prestaties zijn, is het raadzaam toouse VM-serie, die u van Azure Premium-opslag gebruikmaken kunt.

Houd er rekening mee die schijf Hallo die Hallo OS bevat en als het is raadzaam, Hallo binaire bestanden van SAP en Hallo-database (base VM), is niet meer beperkt too127GB. Deze kan nu hebben up too1TB in grootte. Dit moet worden voldoende ruimte tookeep die alle benodigde bestand inclusief bijvoorbeeld hello, SAP-logboeken voor batch-taak.

Voor meer suggesties en meer informatie, specifiek voor virtuele machines DBMS, raadpleeg dan Hallo [DBMS Deployment Guide][dbms-guide]

#### <a name="disk-handling"></a>Verwerking van de schijf
In de meeste gevallen moet u extra schijven toocreate in volgorde toodeploy Hallo SAP-database in Hallo VM. We Hallo overwegingen voor het aantal schijven in hoofdstuk besproken [VM/schijf structuur voor SAP-implementaties] [ planning-guide-5.5.1] van dit document. Hello Azure-portal kunt tooattach en schijven loskoppelen zodra een base VM is geïmplementeerd. Hallo-schijven kunnen zijn gekoppeld/losgekoppeld wanneer Hallo virtuele machine actief is en wordt uitgevoerd en wanneer deze wordt gestopt. Bij het toevoegen van een schijf hello Azure-portal biedt tooattach een lege schijf of een bestaande schijf die op dit moment niet tooanother VM gekoppeld.

**Opmerking**: schijven kunnen alleen worden aangesloten tooone VM op elk moment.

![Koppelen / loskoppelen van schijven met Azure Standard-opslag][planning-guide-figure-1400]

Tijdens het Hallo-implementatie van een nieuwe virtuele machine, kunt u beslissen of u toouse beheerd schijven wilt of plaats de schijven op Azure Storage-Accounts. Als u toouse Premium-opslag wilt, wordt u aangeraden schijven beheerd.

Vervolgens moet u toodecide of u wilt dat een nieuwe en lege schijf toocreate of toohello VM nu of het gewenste tooselect een bestaande schijf die eerder is geüpload en moet worden gekoppeld.

**BELANGRIJKE**: U **DO NOT** wilt toouse Host cachebewerkingen met Azure Standard-opslag. Op de standaardinstelling van geen Hallo laat u Hallo hostcache voorkeur. Met Azure Premium-opslag moet u inschakelen Lees-Caching als Hallo i/o-kenmerk voornamelijk zoals typische i/o-verkeer op basis van de gegevensbestanden van de database wordt gelezen. In geval van een database transactielogbestand wordt cache niet aanbevolen.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Hoe tooattach een schijf in hello Azure-portal][virtual-machines-linux-attach-disk-portal]
>
> Als de schijven zijn gekoppeld, moet u toolog in toohello VM tooopen Hallo Windows Schijfbeheer. Als automount niet is ingeschakeld zoals aanbevolen in hoofdstuk [instelling automount voor gekoppelde schijven][planning-guide-5.5.3], hello zojuist gekoppelde volume moet toobe online gemaakt en geïnitialiseerd.
>
> ![Linux][Logo_Linux] Linux
>
> Als de schijven zijn gekoppeld, u toolog in toohello VM nodig hebt en Hallo schijven initialiseren, zoals beschreven in [in dit artikel][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Als de nieuwe schijf Hallo een lege schijf is, moet u ook tooformat Hallo-schijf. Voor de indeling Hallo gegevens en logboekbestanden met name voor DBMS dezelfde aanbevelingen als voor bare-metal implementaties Hallo dat DBMS toepassen.

Zoals vermeld in hoofdstuk [Hallo van Microsoft Azure virtuele Machine Concept][planning-guide-3.2], een Azure Storage-account biedt geen oneindige resources in termen van i/o-volume, volume IOPS en gegevens. Meestal zijn DBMS VMs meest betrokken bij deze. Aanbevolen toouse een afzonderlijke Opslagaccount voor elke virtuele machine kan zijn als er enkele hoge i/o-volume VMs toodeploy in volgorde toostay binnen de limiet Hallo Hallo volume Azure Storage-Account. Anders moet u toosee hoe u balans vinden tussen deze virtuele machines tussen verschillende Storage-accounts zonder Hallo-limiet van elk één Opslagaccount op. Meer details worden besproken in Hallo [DBMS Deployment Guide][dbms-guide]. U moet ook rekening houden deze beperkingen voor pure SAP-toepassing server-VM's of andere virtuele machines die uiteindelijk mogelijk extra virtuele harde schijven. Deze beperkingen niet van toepassing als u schijf beheerd. Als u van plan toouse Premium-opslag bent, raden wij met schijf beheerd.

Een ander onderwerp dat relevant is voor de Storage-Accounts is of Hallo VHD's in een Opslagaccount wel Geo-replicatie. Geo-replicatie is ingeschakeld of uitgeschakeld op Hallo Opslagaccount niveau en niet op Hallo VM-niveau. Als geo-replicatie is ingeschakeld, Hallo Hallo VHD's binnen Hallo die opslagaccount zou worden gerepliceerd naar een andere Azure-Datacenter binnen dezelfde regio. Voordat u besluit dit, moet u nadenken over Hallo beperking te volgen:

Azure Geo-replicatie werkt lokaal op elke VHD op een virtuele machine en repliceert niet Hallo IOs in chronologische volgorde tussen meerdere VHD's op een virtuele machine. Hallo VHD dat vertegenwoordigt Hallo base VM, evenals een extra virtuele harde schijven gekoppeld toohello VM gerepliceerd daarom onafhankelijk van elkaar. Dit betekent dat er vindt geen synchronisatie tussen Hallo wijzigingen in Hallo verschillende VHD's. Hallo feit dat IOs Hallo gerepliceerd onafhankelijk van Hallo volgorde in dat ze zijn geschreven betekent dat geo-replicatie is niet van de waarde voor de databaseservers waarop hun databases verdeeld over meerdere VHD's. In aanvulling toohello DBMS, kunnen ook er andere toepassingen waarbij processen schrijven of manipuleren van gegevens in verschillende virtuele harde schijven en wanneer het is belangrijk tookeep Hallo volgorde van wijzigingen. Als dat een vereiste is, moet geo-replicatie in Azure niet worden ingeschakeld. Afhankelijk van of u moet of wilt geo-replicatie voor een set van virtuele machines, maar niet voor een andere set, kunt u al categoriseren virtuele machines en hun verwante VHD's in verschillende Storage-Accounts waarvoor geo-replicatie ingeschakeld of uitgeschakeld.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Automount voor gekoppelde schijven instellen
- - -
> ![Windows][Logo_Windows] Windows
>
> Voor virtuele machines die worden gemaakt uit eigen installatiekopieën of schijven, is het nodig toocheck en mogelijk Hallo automount parameter instellen. Als deze parameter kunt Hallo VM na het opnieuw opstarten of opnieuw implementeren in Azure toomount Hallo gekoppeld / schijven automatisch opnieuw gekoppelde.
> Hallo-parameter is ingesteld voor Hallo afbeeldingen geleverd door Microsoft in hello Azure Marketplace.
>
> Schakel Hallo documentatie van Hallo opdrachtregelprogramma uitvoerbare diskpart.exe hier in volgorde tooset Hallo automount:
>
> * [Opdrachtregelopties voor DiskPart](https://technet.microsoft.com/library/bb490893.aspx)
> * [Automount](http://technet.microsoft.com/library/cc753703.aspx)
>
> Windows Hello-opdrachtregelvenster moet worden geopend als administrator.
>
> Als de schijven zijn gekoppeld, moet u toolog in toohello VM tooopen Hallo Windows Schijfbeheer. Als automount niet is ingeschakeld zoals aanbevolen in hoofdstuk [instelling automount voor gekoppelde schijven][planning-guide-5.5.3], Hallo zojuist gekoppeld volume > moet toobe online gemaakt en geïnitialiseerd.
>
> ![Linux][Logo_Linux] Linux
>
> U moet een zojuist gekoppelde lege schijf tooinitialize zoals beschreven in [in dit artikel][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> U moet ook tooadd nieuwe schijven toohello /etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Laatste implementatie
Voor Hallo laatste implementatie en de exacte stappen, met name met betrekking toohello implementatie van het SAP uitgebreide bewaking, raadpleegt u toohello [Deployment Guide][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Toegang tot SAP-systemen die zijn uitgevoerd in Azure Virtual machines
Voor scenario's alleen in de Cloud, kunt u tooconnect toothose SAP-systemen via Hallo openbare internet met SAP-gebruikersinterface. Voor deze gevallen moeten hello volgende procedures toobe toegepast.

Hallo andere belangrijke scenario, verbindende tooSAP systemen in de cross-premises implementaties die een site-naar-site-verbinding (VPN-tunnel) of Azure ExpressRoute-verbinding tussen Hallo on-premises systemen en Azure systemen verderop in Hallo document die worden besproken.

### <a name="remote-access-toosap-systems"></a>Externe toegang tooSAP systemen
Met Azure Resource Manager zijn er geen Standaardeindpunten meer zoals in Hallo voormalige klassieke model. Alle poorten van een Azure ARM VM zijn geopend, zolang:

1. Er is geen Netwerkbeveiligingsgroep is gedefinieerd voor het Hallo-subnet of Hallo-netwerkinterface. Netwerkverkeer tooAzure virtuele machines kan worden beveiligd via zogenaamde 'Netwerkbeveiligingsgroepen'. Zie voor meer informatie [wat is er een Netwerkbeveiligingsgroep (NSG)?][virtual-networks-nsg]
2. Er is geen Azure Load Balancer is gedefinieerd voor de netwerkinterface Hallo   

Zie Hallo architectuur verschil tussen het klassieke model en ARM in zoals beschreven in [in dit artikel][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configuratie van Hallo SAP-systeem en SAP-GUI connectiviteit voor alleen-scenario
Raadpleeg dit artikel waarin details toothis onderwerp wordt beschreven: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Wijzigen van firewallinstellingen in VM
Kan het benodigde tooconfigure Hallo firewall op uw virtuele machines tooallow zijn inkomend verkeer tooyour SAP-systeem.

- - -
> ![Windows][Logo_Windows] Windows
>
> Hallo Windows Firewall in een Azure geïmplementeerde VM is standaard ingeschakeld. U moet nu tooallow Hallo SAP-poort toobe geopend, anders Hallo SAP-GUI niet kunnen tooconnect.
> toodo dit:
>
> * Open configuratiescherm\systeem en beveiliging\windows Firewall too'Advanced instellingen.
> * Nu met de rechtermuisknop op de regels voor binnenkomende verbindingen en kies 'Nieuwe regel'.
> * In Hallo gekozen toocreate voor volgende Wizard een nieuwe regel voor 'Poort'.
> * Laat Hallo-instelling op TCP- en typ in het gewenste poortnummer Hallo tooopen in de volgende stap van de wizard Hallo Hallo. Omdat de exemplaar-ID van onze SAP 00, duurde we 3200. Als uw exemplaar een ander exemplaar getal heeft, moet Hallo poort die u gedefinieerd eerder op basis van Hallo exemplaarnummer worden geopend.
> * Hallo volgende deel van de wizard hello moet u tooleave Hallo item 'Toestaan dat Connection' gecontroleerd.
> * In de volgende stap van de wizard Hallo Hallo moet u toodefine of Hallo regel van toepassing voor het domein, persoonlijke en openbare netwerk is. Wijzig deze indien nodig tooyour moet. Een verbinding met SAP-GUI van Hallo buiten via Hallo openbaar netwerk, moet u echter toohave Hallo regel van toepassing toohello openbaar netwerk.
> * In de laatste stap van de wizard Hallo HALLO hallo regel naam geven en opslaan door op 'Voltooid' te drukken
>
> Hallo-regel wordt onmiddellijk van kracht.
>
> ![De regeldefinitie poort][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> Hallo Linux afbeeldingen in hello Azure Marketplace doen Hallo iptables firewall niet standaard ingeschakeld en Hallo verbinding tooyour SAP-systeem moet werken. Als u iptables of een andere firewall hebt ingeschakeld, Raadpleeg de documentatie van iptables toohello of Hallo gebruikt firewall tooallow binnenkomend TCP-verkeer te poort 32xx (waarbij xx systeemnummer op Hallo van uw systeem SAP is).
>
>

- - -
#### <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
Hallo SAP-GUI maakt geen verbinding onmiddellijk tooany van Hallo SAP exemplaren (poort 32xx) die worden uitgevoerd, maar eerst verbinding maakt via Hallo poort geopend toohello SAP bericht server-proces (poort 36xx). In Hallo Hallo zeer dezelfde poort uit het verleden is gebruikt door Hallo message server voor Hallo interne communicatie toohello toepassingsexemplaren. tooprevent lokale toepassingsservers per ongeluk communiceert met een message-server in Azure Hallo interne communicatiepoorten kunnen worden gewijzigd. Het is raadzaam toochange Hallo interne communicatie tussen Hallo SAP berichtenserver en de toepassing exemplaren tooa ander poortnummer op systemen die hebben is gekloond van on-premises systemen, zoals een kloon van ontwikkeling voor het project testen enz. Dit kan worden gedaan met de standaardparameter profiel Hallo:

> rdisp/msserv_internal
>
>

zoals beschreven in [beveiligingsinstellingen voor Hallo SAP Message Server](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Concepten van Cloud-implementatie van SAP-exemplaren
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Met SAP NetWeaver demo/training scenario één virtuele machine
![Uitvoeren van één VM SAP demo-systemen met Hallo hetzelfde VM-namen, geïsoleerd in Azure Cloud Services][planning-guide-figure-1700]

In dit scenario (Zie hoofdstuk [Cloudconfiguratie] [ planning-guide-2.1] van dit document) we bij het implementeren van een typische training/demo-systeem scenario waarbij Hallo voltooid training/demo-scenario is opgenomen in een enkele virtuele machine. Er wordt ervan uitgegaan dat Hallo-implementatie wordt gedaan door VM-sjablonen voor de installatiekopie. We ook wordt ervan uitgegaan dat meerdere van deze demo/trainingen virtuele machines nodig toobe geïmplementeerd met Hallo VMs gelet Hallo dezelfde naam.

Hallo verondersteld wordt dat u een VM-installatiekopie gemaakt zoals beschreven in sommige secties van hoofdstuk [voorbereiden van virtuele machines met SAP voor Azure] [ planning-guide-5.2] in dit document.

Hallo reeks gebeurtenissen tooimplement Hallo scenario ziet er als volgt:

##### <a name="powershell"></a>PowerShell
* Maak een nieuwe resourcegroep voor elke training/demo-liggend

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Een nieuw opslagaccount maken als u niet dat toouse beheerd schijven wilt

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Een nieuw virtueel netwerk maken voor elke training/demo liggend tooenable Hallo gebruik Hallo dezelfde hostnaam en IP-adressen. Hallo virtueel netwerk wordt beveiligd door een Netwerkbeveiligingsgroep waarmee alleen toegang tot verkeer tooport 3389 tooenable extern bureaublad- en -poort 22 voor SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Maak een nieuw openbaar IP-adres dat gebruikt tooaccess Hallo virtuele machine van Hallo worden kan internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Een nieuwe netwerkinterface voor Hallo virtuele machine maken

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Maak een virtuele machine. Hallo Cloudconfiguratie scenario voor elke VM Hallo hebben dezelfde naam. Hallo SAP-SID van Hallo SAP NetWeaver-exemplaren in die virtuele machines worden Hallo dezelfde ook. Hallo binnen Azure-resourcegroep, Hallo naam Hallo VM moet toobe unieke, maar in verschillende Azure-resourcegroepen kunt u virtuele machines uitvoeren met Hallo dezelfde naam. Standaard 'Administrator'-account van Windows hello of 'root' voor Linux zijn niet geldig. Daarom moet de gebruikersnaam van een nieuwe beheerder toobe gedefinieerd samen met een wachtwoord. Hallo-grootte van Hallo VM moet ook toobe gedefinieerd.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Eventueel extra schijven toevoegt en herstellen van de benodigde inhoud. Let erop dat alle blobnamen (URL's toohello BLOB's) uniek zijn binnen Azure moeten.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Hallo voorbeeldcode volgende kan worden gebruikt op Linux. Voor Windows, ofwel gebruik PowerShell zoals hierboven is beschreven of Hallo voorbeeld toouse % rgName % in plaats van $rgName aanpassen en Hallo omgevingsvariabele met behulp van Windows-opdracht Hallo *ingesteld*.

* Maak een nieuwe resourcegroep voor elke training/demo-liggend

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* Een nieuw opslagaccount maken

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* Een nieuw virtueel netwerk maken voor elke training/demo liggend tooenable Hallo gebruik Hallo dezelfde hostnaam en IP-adressen. Hallo virtueel netwerk wordt beveiligd door een Netwerkbeveiligingsgroep waarmee alleen toegang tot verkeer tooport 3389 tooenable extern bureaublad- en -poort 22 voor SSH.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Maak een nieuw openbaar IP-adres dat gebruikt tooaccess Hallo virtuele machine van Hallo worden kan internet

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Een nieuwe netwerkinterface voor Hallo virtuele machine maken

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* Maak een virtuele machine. Hallo Cloudconfiguratie scenario voor elke VM Hallo hebben dezelfde naam. Hallo SAP-SID van Hallo SAP NetWeaver-exemplaren in die virtuele machines worden Hallo dezelfde ook. Hallo binnen Azure-resourcegroep, Hallo naam Hallo VM moet toobe unieke, maar in verschillende Azure-resourcegroepen kunt u virtuele machines uitvoeren met Hallo dezelfde naam. Standaard 'Administrator'-account van Windows hello of 'root' voor Linux zijn niet geldig. Daarom moet de gebruikersnaam van een nieuwe beheerder toobe gedefinieerd samen met een wachtwoord. Hallo-grootte van Hallo VM moet ook toobe gedefinieerd.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* Eventueel extra schijven toevoegt en herstellen van de benodigde inhoud. Let erop dat alle blobnamen (URL's toohello BLOB's) uniek zijn binnen Azure moeten.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>Template
U kunt Hallo voorbeeldsjablonen op Hallo azure-snelstartsjablonen opslagplaats op github.

* [Eenvoudige Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Eenvoudige Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [VM van de installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementeren van een set van virtuele machines die toocommunicate in Azure nodig
Dit scenario alleen in de Cloud is een typisch scenario voor trainings- en demo doeleinden waar hello software die vertegenwoordigt Hallo demo/training scenario is verspreid over meerdere virtuele machines. Hallo verschillende onderdelen geïnstalleerd Hallo andere virtuele machines nodig toocommunicate met elkaar. Opnieuw, in dit scenario geen on-premises netwerkcommunicatie of cross-premises scenario nodig is.

Dit scenario is een uitbreiding van Hallo installatie beschreven in hoofdstuk [één VM met SAP NetWeaver demo/training scenario] [ planning-guide-7.1] van dit document. In dit geval worden meer virtuele machines toegevoegd tooan bestaande resourcegroep. In Hallo bestaat volgende voorbeeld Hallo training liggend uit een SAP ASC's / SCS VM, een virtuele machine met een DBMS en een exemplaar van de toepassingsserver SAP VM.

Voordat u dit scenario u toothink over basisinstellingen al uitgeoefend in Hallo scenario voordat moet bouwen.

#### <a name="resource-group-and-virtual-machine-naming"></a>Naamgeving van de virtuele Machine en resourcegroep
Alle namen van resourcegroepen moet uniek zijn. Uw eigen schematische naam van uw resources, zoals ontwikkelen `<rg-name`>-achtervoegsel.

naam van de virtuele machine Hallo heeft toobe uniek zijn binnen de resourcegroep Hallo.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>Netwerk instellen voor de communicatie tussen verschillende virtuele machines Hallo
![Set van virtuele machines binnen een virtuele Azure-netwerk][planning-guide-figure-1900]

tooprevent naamconflicten met klonen Hallo dezelfde training/demo landschappen, moet u een Azure Virtual Network toocreate voor elke Liggend. DNS-naamomzetting wordt aangeboden door Azure of u kunt uw eigen DNS-server buiten Azure (geen toobe nader besproken hier) configureren. In dit scenario doen we ons eigen DNS niet configureren. Voor alle virtuele machines binnen een Azure Virtual Network worden communicatie via hostnamen ingeschakeld.

Hallo redenen tooseparate training of demo landschappen door virtuele netwerken en kan niet alleen resource groepen zijn:

* Hallo SAP liggend zoals ingesteld moet een eigen AD/OpenLDAP en domeinserver behoeften toobe onderdeel van elk van de Hallo landschappen.  
* Hallo SAP liggend zoals instellen van de onderdelen die nodig toowork met vaste IP-adressen heeft.

Meer informatie over virtuele netwerken van Azure en hoe toodefine ze kunnen worden gevonden [in dit artikel][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>SAP virtuele machines implementeren met de zakelijke netwerkverbinding (Cross-Premises)
Een SAP-liggend uit te voeren en toodivide Hallo implementatie tussen bare-metal voor geavanceerde DBMS-servers wilt, on-premises gevirtualiseerde omgevingen voor toepassingslagen en kleinere 2-Tier SAP-systemen en Azure IaaS geconfigureerd. Hallo base veronderstelling is dat SAP-systemen binnen één SAP liggend toocommunicate met elkaar en met veel andere softwareonderdelen geïmplementeerd in bedrijf hello, onafhankelijk van de vorm van de implementatie moeten. Ook moet er geen verschillen geïntroduceerd door Hallo implementatie formulier voor eindgebruiker Hallo verbinden met SAP-GUI of andere interfaces. Deze voorwaarden kunnen alleen worden voldaan wanneer we hebben Hallo on-premises Active Directory/OpenLDAP en DNS-services uitgebreide toohello Azure systemen via site-naar-site/meerdere-on-site verbroken of particuliere verbindingen zoals Azure ExpressRoute.

In de volgorde tooget meer op de achtergrond op Hallo implementatiegegevens van SAP op Azure, raden we u tooread hoofdstuk [implementatie van de concepten van Cloud-Only SAP-exemplaren van] [ planning-guide-7] van dit document waarin wordt uitgelegd aantal Hallo basisbeginselen van Azure en hoe deze moeten worden gebruikt met SAP-toepassingen in Azure vormt.

### <a name="scenario-of-an-sap-landscape"></a>Scenario met een liggend SAP
Hallo kan cross-premises scenario worden ongeveer beschreven zoals Hallo Graphics hieronder:

![Site-naar-Site-connectiviteit tussen on-premises en Azure activa][planning-guide-figure-2100]

Hallo scenario bovenstaande beschrijft een scenario waarbij Hallo on-premises AD/OpenLDAP en DNS tooAzure zijn uitgebreid. Zijde van de lokale hello, is een bepaalde IP-adresbereik gereserveerd per Azure-abonnement. Hallo IP-adresbereik worden tooan Azure Virtual Network op Hallo Azure aan clientzijde toegewezen.

#### <a name="security-considerations"></a>Beveiligingsoverwegingen
Hallo minimumvereiste is Hallo gebruik van beveiligde communicatie-protocollen, zoals SSL/TLS voor toegang tot de browser of op basis van VPN-verbindingen voor systeem toegang krijgen tot toohello Azure services. Hallo verondersteld wordt dat bedrijven Hallo VPN-verbinding tussen hun bedrijfsnetwerk en Azure heel anders afgehandeld. Sommige bedrijven mogelijk blankly alle Hallo poorten geopend. Sommige andere bedrijven kunt toobe zeer nauwkeurig in welke poorten moeten tooopen, enzovoort.

In de tabel hieronder typische SAP Hallo worden communicatiepoorten weergegeven. Het is in feite voldoende tooopen Hallo SAP-gateway-poort.

| Service | Poortnaam | Voorbeeld `<nn`> = 01 | Standaard-bereik (min-max.) | Opmerking |
| --- | --- | --- | --- | --- |
| Dispatcher |sapdp`<nn>` Zie * |3201 |3200 – 3299 |SAP-Dispatcher, die wordt gebruikt door SAP GUI voor Windows en Java |
| Berichtenserver |sapms`<sid`> Zie ** |3600 |gratis sapms`<anySID`> |SID SAP-systeem-ID = |
| Gateway |sapgw`<nn`> Zie * |3301 |Gratis |SAP-gateway, die wordt gebruikt voor CPIC en RFC communicatie |
| SAP-router |sapdp99 |3299 |Gratis |Namen van alleen CI (centrale exemplaar)-Service kunnen opnieuw worden toegewezen in /etc/services tooan willekeurige waarde na de installatie. |

*) nn SAP exemplaarnummer =

*) sid SAP-systeem-ID =

Gedetailleerde informatie over de poorten die nodig zijn voor verschillende SAP-producten of services door SAP producten vindt u hier <http://scn.sap.com/docs/DOC-17124>.
U moet aan dit document kunnen tooopen toegewezen poorten in Hallo VPN-apparaat nodig zijn voor specifieke SAP-producten en scenario's.

Andere veiligheidsmaatregelen bij het implementeren van virtuele machines in een dergelijk scenario kan toocreate een [Netwerkbeveiligingsgroep] [ virtual-networks-nsg] toodefine toegangsregels.

### <a name="dealing-with-different-virtual-machine-series"></a>Omgaan met andere virtuele Machine-reeks
In de loop van de afgelopen 12 maanden Hallo toegevoegd Microsoft veel meer typen van de virtuele machine die in aantal vcpu's, geheugen verschillen of belangrijker op hardware wordt uitgevoerd. Niet alle die virtuele machines worden ondersteund met SAP (Zie ondersteund VM typen in SAP-notitie [1928533]). Sommige van deze VMs worden uitgevoerd op een andere host hardware generaties. Deze host hardware generaties worden in Hallo samenvattingen van een Azure-schaaleenheid ophalen geïmplementeerd. Betekent gevallen kunnen ontstaan waarin Hallo andere VM-grootten gekozen kan niet worden uitgevoerd op dezelfde schaaleenheid Hallo. Een Beschikbaarheidsset beperkte Hallo mogelijkheid toospan-schaaleenheden op basis van andere hardware.  Voor als u wilt dat toorun Hallo DBMS op A5 A11-VM's en hello toepassingslaag SAP op virtuele machines G-serie, u zou bijvoorbeeld geforceerd toodeploy één SAP-systeem of andere SAP-systemen binnen andere Beschikbaarheidssets.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Afdrukken op een lokale netwerkprinter uit SAP-exemplaar in Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Afdrukken via TCP/IP in Cross-Premises-scenario
Instellen van uw lokale TCP/IP op basis van netwerkprinters in een Azure VM is algehele Hallo net als in uw bedrijfsnetwerk, ervan uitgaande dat u beschikt over een Site-naar-Site VPN-tunnel of ExpressRoute-verbinding tot stand gebracht.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo dit:
>
> * Sommige netwerkprinters worden geleverd met een configuratiewizard dit het eenvoudig tooset van de printer in een Azure VM maakt. Als er geen wizardsoftware heeft is met de printer Hallo 'handmatig' manier tooset Hallo printer een nieuwe TCP/IP-printerpoort toocreate is gedistribueerd.
> * Open Configuratiescherm -> apparaten en Printers -> een printer toevoegen
> * Kies toevoegen een printer met een TCP/IP-adres of de hostnaam
> * Typ in Hallo IP-adres van Hallo printer
> * Standaard 9100-printerpoort
> * Indien nodig handmatig de juiste printerstuurprogramma Hallo installeren.
>
> ![Linux][Logo_Linux] Linux
>
> * Net als voor Windows just Volg Hallo standaardprocedure tooinstall een netwerkprinter
> * Volg Hallo openbare Linux handleidingen voor [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) of [Red Hat en Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) over het tooadd een printer.
>
>

- - -
![Afdrukken via het netwerk][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Printer op de host via SMB (gedeelde printer) in de Cross-Premises-scenario
Printers op de host zijn niet netwerk compatibel is met opzet. Maar een printer op de host kan worden gedeeld met computers in een netwerk, zolang Hallo printer verbonden tooa ingeschakeld op de computer is. Verbinding maken met uw bedrijfsnetwerk via Site-naar-Site of ExpressRoute en delen van de lokale printer. Hallo SMB-protocol maakt gebruik van NetBIOS in plaats van DNS als name-service. Hallo NetBIOS-hostnaam kan afwijken van de DNS-hostnaam Hallo. Hallo wordt standaard Hallo NetBIOS-hostnaam en Hallo DNS-hostnaam identiek zijn. Hallo DNS-domein is niet verstandig in Hallo NetBIOS-naamruimte. Hallo dienovereenkomstig, volledig gekwalificeerde DNS-hostnaam die bestaan uit Hallo DNS-hostnaam en DNS-domein moet niet worden gebruikt in Hallo NetBIOS-naamruimte.

Hallo printershare wordt geïdentificeerd door een unieke naam in Hallo netwerk:

* De hostnaam van Hallo SMB host (altijd nodig).
* Naam van het Hallo-share (altijd nodig).
* Naam van het Hallo-domein als printershare zich niet in Hallo hetzelfde domein als SAP-systeem.
* Bovendien kunnen een gebruikersnaam en een wachtwoord vereist tooaccess Hallo printershare zijn.

Procedure:

- - -
> ![Windows][Logo_Windows] Windows
>
> De lokale printer delen.
> Open in hello Azure VM, Hallo Windows Verkenner en type in de sharenaam Hallo Hallo printer.
> Een printer-installatiewizard leidt u door het installatieproces Hallo.
>
> ![Linux][Logo_Linux] Linux
>
> Hier volgen enkele voorbeelden van documentatie over het configureren van netwerkprinters in Linux of een hoofdstuk waaronder met betrekking tot afdrukken in Linux. Werkt het Hallo in een zolang VM hello Azure Linux VM op dezelfde manier maakt deel uit van een VPN:
>
> * SLES <_Share_or_Windows_Share https://en.opensuse.org/SDB:Printing_via_SMB_ (Samba)>
> * RHEL- of Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>USB-Printer (printer doorsturen)
De mogelijkheid Azure Hallo Hallo extern bureaublad-Services tooprovide Hallo toegang tootheir lokale printer apparaten in een externe sessie is niet beschikbaar.

- - -
> ![Windows][Logo_Windows] Windows
>
> Meer informatie over het afdrukken met Windows vindt u hier: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integratie van SAP Azure systemen in correctie en -Transport-systeem (TMS) in de Cross-Premises
Hallo SAP wijzigings- en Transport-systeem (TMS) behoeften toobe geconfigureerd tooexport en transport aanvraag verschillende systemen Hallo liggend importeren. We gaan ervan uit dat Hallo ontwikkeling exemplaren van een SAP-systeem (DEV) bevinden zich in Azure dat Hallo quality assurance (QA) en productief systemen (PRD) zich on-premises. Bovendien veronderstellen we dat er een centrale transportmap is.

##### <a name="configuring-hello-transport-domain"></a>Hallo Transport domein configureren
Configureren van uw domein Transport op Hallo systeem u aangewezen als het Hallo-Transport-domeincontroller, zoals beschreven in [configureren Hallo Transport domeincontroller](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Een systeemgebruiker die TMSADM wordt gemaakt en Hallo vereist RFC bestemming wordt gegenereerd. U kunt deze RFC-verbindingen met de Hallo transactie SM59 kan controleren. Hostnaamomzetting moet zijn ingeschakeld in uw domein transport.

Procedure:

* In ons scenario besloten we Hallo lokale QAS system Hallo CTS domeincontroller zijn. Transactie stm-aanroep. Hallo TMS dialoogvenster wordt weergegeven. Een dialoogvenster Transport-domein configureren wordt weergegeven. (Dit dialoogvenster wordt alleen weergegeven als u een transport-domein nog niet hebt geconfigureerd.)
* Zorg ervoor dat de gebruiker Hallo automatisch gemaakt TMSADM is geautoriseerd (SM59 -> ABAP verbinding -> TMSADM@E61.DOMAIN_E61 -> Details -> Utilities(M)-autorisatie Test >). initiële welkomstscherm van transactie STM moet blijken dit systeem SAP functioneert als domeincontroller Hallo van Hallo transport domein als volgt te werk:

![Startscherm van transactie stm op Hallo-domeincontroller][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Inclusief SAP-systemen in Hallo Transport-domein
Hallo met inbegrip van een SAP-systeem in een domein transport reeks ziet er als volgt uit:

* Op Hallo DEV-systeem in Azure, gaat u toohello transport system (Client 000) en transactie stm aanroepen. Kies andere configuratie in het dialoogvenster Hallo en doorgaan met systeem opnemen in een domein. Hallo-domeincontroller opgeven als de doelhost ([SAP-systemen inclusief in Hallo Transport domein](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Hallo-systeem is nu wachten toobe opgenomen in Hallo transport-domein.
* Uit veiligheidsoverwegingen vervolgens hebt toogo back toohello domain controller tooconfirm uw aanvraag. Kies Systeemoverzicht en goedkeuren van Hallo wachten systeem. Bevestig het Hallo-prompt en Hallo configuratie worden gedistribueerd.

Dit systeem SAP bevat nu Hallo nodige informatie over alle Hallo andere systemen SAP in Hallo transport-domein. Op Hallo dezelfde tijdstip, Hallo adres gegevens van de nieuwe SAP-systeem Hallo tooall Hallo andere SAP-systemen en Hallo SAP-systeem wordt ingevoerd in Hallo transport profiel van Hallo transport besturingsprogramma worden verzonden. Controleer of RFC's en toegang toohello transport directory van Hallo domein werken.

Ga door met de Hallo configuratie van uw systeem transport gewoon zoals beschreven in de documentatie Hallo [wijzigings- en Transport System](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Procedure:

* Zorg ervoor dat uw stm on-premises correct is geconfigureerd.
* Zorg ervoor dat het Hallo-hostnaam van Hallo Transport-domeincontroller kan worden opgelost door de virtuele machine op Azure en andersom visa.
* Aanroep transactie stm -> andere configuratie -> systeem opnemen in een domein.
* Hallo-verbinding in Hallo op lokale TMS systeem bevestigen.
* Gewoon transport routes, groepen en lagen configureren.

In de site-naar-site verbonden cross-premises scenario's, Hallo latentie tussen on-premises en Azure kunnen nog steeds worden aanzienlijke. Als we volgen Hallo reeks objecten door de ontwikkeling en tests systemen tooproduction transport of nadenkt over het toepassen van transporten of ondersteuning toohello verschillende systemen pakketten, zult u ontdekken die, afhankelijk van de locatie van centrale transport Hallo Hallo Directory tegenkomt Hallo systemen met hoge latentie lezen of schrijven van gegevens in Hallo transport centrale map. Hallo situatie is soortgelijke tooSAP liggend configuraties waar Hallo verschillende systemen worden verspreid via verschillende datacenters met aanzienlijke afstand tussen het Hallo-datacenters.

In volgorde toowork rond dergelijke latentie en Hallo-systemen werken snel in lezen of schrijven tooor uit Hallo transport directory, kunt u twee stm transport domeinen (één voor on-premises. en één met de Hallo systemen instellen in Azure en koppeling Hallo transport-domeinen Controleer of deze documentatie waarin wordt uitgelegd Hallo principes achter dit concept in Hallo SAP TMS: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/frameset.htm>.

Procedure:

* Stel een domein transport op elke locatie (on-premises en Azure) met de transactie stm <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Koppeling Hallo domeinen met een domein koppelen en Hallo koppeling tussen de twee domeinen Hallo bevestigen.
  <http://Help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Het configuratiesysteem toohello gekoppeld Hallo distribueren.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>RFC-verkeer tussen SAP-exemplaren die zich in Azure en on-premises (Cross-Premises)
RFC-verkeer tussen de systemen die zich on-premises en in Azure moet toowork. tooset om een verbinding aanroep transactie SM59 in een bronsysteem waarin u toodefine moet een RFC-verbinding naar het doelsysteem Hallo. Hallo-configuratie is vergelijkbaar toohello standaardinstellingen van een RFC-verbinding.

We gaan ervan uit dat de Hallo VMs welke run SAP-systemen die toocommunicate met elkaar moeten beschikbaar zijn in Hallo cross-premises scenario hetzelfde domein Hallo. Daarom hello installatie van een RFC-verbinding tussen SAP-systemen niet verschillen van Hallo instellingsstappen en invoer in lokale scenario's.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Toegang tot 'local' fileshares van SAP-exemplaren in Azure of andersom
SAP-exemplaren die zich in Azure nodig tooaccess bestandsshares die binnen Hallo zakelijke premises. Bovendien moeten de lokale SAP exemplaren tooaccess bestandsshares die in Azure bevinden zich. tooenable moet u configureren Hallo machtigingen en delen van de opties op het lokale systeem Hallo Hallo bestandsshares. Ervoor tooopen Hallo poorten op Hallo VPN of ExpressRoute-verbinding tussen Azure en uw datacenter te maken.

## <a name="supportability"></a>Ondersteuning
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Azure Bewakingsoplossing voor SAP
In de volgorde tooenable Hallo bewaking van bedrijfskritieke SAP systemen op Azure Hallo SAP ophalen controlehulpmiddelen SAPOSCOL of de Hostagent SAP uit hello Azure virtuele Machine ServiceHost via een extensie Azure Monitoring voor SAP. Aangezien Hallo eisen door SAP zeer specifieke tooSAP toepassingen zijn, Microsoft besloten geen toogenerically implementeren Hallo vereist functionaliteit in Azure, maar laat u het voor klanten toodeploy Hallo nodig bewaking onderdelen en configuraties tootheir Virtuele Machines in Azure wordt uitgevoerd. Implementatie levenscyclusbeheer Hallo bewaking van onderdelen wordt echter meestal automatisch door Azure.

#### <a name="solution-design"></a>Ontwerp van de oplossing
Hallo oplossing ontwikkeld tooenable die SAP bewaking is gebaseerd op Hallo-architectuur van Azure VM-Agent en Extension framework. Hallo idee van de Azure VM-Agent en de extensie framework Hallo is tooallow installatie van software-toepassingen die beschikbaar zijn in de galerie van Azure VM-extensie Hallo binnen een virtuele machine. Hallo principe idee achter dit concept is tooallow (in gevallen zoals hello Azure extensie Monitoring voor SAP), Hallo implementatie van speciale functionaliteit in een virtuele machine en Hallo configuratie van dergelijke software tijdens de implementatie.

Hallo 'Azure VM-Agent' waarmee de verwerking van specifieke Azure VM-extensies binnen Hallo die VM is opgenomen in Windows-VM's standaard op het maken van de VM in hello Azure-portal. In geval van een SUSE, Red Hat of Oracle Linux uitmaakt Hallo VM-agent al deel van de Azure Marketplace-installatiekopie. Als een zou een Linux-VM uit uploaden beschikt lokale tooAzure Hallo VM-agent toobe handmatig geïnstalleerd.

Hallo bouwstenen van Hallo bewaking oplossing in Azure voor SAP uitziet:

![Onderdelen van de uitbreiding voor Microsoft Azure][planning-guide-figure-2400]

Zoals u in de bovenstaande Hallo blokdiagram, wordt een deel van de bewaking van de oplossing voor SAP Hallo gehost in hello Azure VM-installatiekopie en de extensie-galerie van Azure een globaal gerepliceerde opslagplaats die wordt beheerd door de Azure-bewerkingen. Het is de verantwoordelijkheid Hallo van Hallo gezamenlijke SAP/MS-team werkt aan hello Azure-implementatie van SAP toowork met Azure Operations toopublish nieuwe versies van hello Azure extensie Monitoring voor SAP.

Wanneer u een nieuwe Windows VM implementeert, wordt 'Azure VM-Agent' hello automatisch toegevoegd aan Hallo VM. Hallo-functie van deze agent is toocoordinate Hallo laden en de configuratie van hello Azure-extensies voor de bewaking van SAP NetWeaver-systemen. Voor virtuele Linux-machines uitmaakt hello Azure VM-Agent al deel van hello Azure Marketplace-installatiekopie.

Er is echter een stap die u nog steeds uitgevoerd door de klant Hallo toobe moet. Dit is het Hallo-activering en configuratie van Hallo prestatieverzameling. Hallo proces gerelateerd toohello 'configuration' wordt automatisch uitgevoerd door een PowerShell-script of opdracht CLI. Hallo PowerShell-script kan worden gedownload in Microsoft Azure Script Center hello, zoals beschreven in Hallo [Deployment Guide][deployment-guide].

Hallo algehele architectuur van hello Azure bewakingsoplossing voor SAP ziet eruit als:

![Bewaking van de oplossing voor SAP NetWeaver Azure][planning-guide-figure-2500]

**Ga als volgt Hallo instructies in Hallo voor Hallo exacte hoe-tooand voor gedetailleerde stappen voor het gebruik van deze PowerShell-cmdlets of de CLI opdracht tijdens implementaties van, [Deployment Guide][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integratie van Azure bevinden SAP-exemplaar in SAProuter
SAP-exemplaren die worden uitgevoerd in Azure nodig toobe toegankelijk is vanaf SAProuter ook.

![SAP-Router-netwerkverbinding][planning-guide-figure-2600]

Een SAProuter kunt Hallo TCP/IP-communicatie tussen de deelnemende systemen als er geen directe IP-verbinding. Dit biedt Hallo voordeel dat er geen end-to-end-verbinding tussen Hallo communicatie partners nodig op netwerkniveau is. Hallo SAProuter luistert op poort 3299 standaard.
via een SAProuter tooconnect SAP-exemplaren moet u toogive hello SAProuter tekenreeks en de hostnaam met eventuele tooconnect poging.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Tot nu toe Hallo focus van Hallo document SAP NetWeaver in het algemeen is of Hallo SAP NetWeaver ABAP stack. In deze sectie kort worden specifieke aandachtspunten voor het Hallo SAP Java stack weergegeven. Een van de belangrijkste dat SAP NetWeaver Java gebaseerde uitsluitend toepassingen Hallo is Hallo SAP Enterprise Portal. Andere SAP NetWeaver gebaseerde toepassingen, zoals SAP-PI en SAP-oplossing Manager Hallo SAP NetWeaver ABAP en Java-stacks gebruiken. Daarom zeker een noodzaak tooconsider specifieke aspecten gerelateerde toohello SAP NetWeaver Java de stack is ook.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
Hallo-installatie van een SAP-Portal in een virtuele Machine van Azure niet afwijken van de installatie van een on premises als u in scenario's voor cross-premises implementeert. Sinds Hallo die DNS wordt gedaan door on-premises, kunnen geconfigureerde lokale Hallo poortinstellingen van Hallo afzonderlijke exemplaren worden uitgevoerd. Hallo-aanbevelingen en beperkingen tot nu toe die worden beschreven in dit document voor een toepassing zoals SAP Enterprise Portal of Hallo SAP NetWeaver Java-stack in het algemeen gelden.

![Blootgestelde SAP-Portal][planning-guide-figure-2700]

Een speciale implementatiescenario door sommige klanten is Hallo rechtstreekse blootstelling van Hallo SAP Enterprise Portal toohello Internet terwijl Hallo virtuele machinehost verbonden toohello bedrijfsnetwerk via site-naar-site VPN-tunnel of ExpressRoute is. Voor een scenario moet u zorgen dat bepaalde poorten geopend en niet wordt geblokkeerd door een firewall of netwerk beveiligingsgroep zijn toomake hebben. Hallo moet dezelfde mechanismen toobe toegepast wanneer u wilt dat tooconnect tooan SAP-Java-exemplaar van on-premises in een scenario alleen in de Cloud.

Hallo initiële portal URI is http (s):`<Portalserver`>: 5XX00/irj waar Hallo poort wordt gevormd door 50000 plus (Systemnumber × 100). Hallo standaard portal URI van SAP-systeem 00 is `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Voor meer informatie, hebt u kijken <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Endpoint-configuratie][planning-guide-figure-2800]

Als u wilt dat toocustomize Hallo URL en/of poorten van uw SAP Enterprise Portal, controleert u in deze documentatie:

* [De URL van de Portal wijzigen](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Standaardpoortnummers, Portal-poortnummers wijzigen](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Hoge beschikbaarheid (HA) en Disaster Recovery (DR) voor SAP NetWeaver uitgevoerd op Azure Virtual Machines
### <a name="definition-of-terminologies"></a>Definitie van de terminologie
Hallo term **hoge beschikbaarheid (HA)** is doorgaans gerelateerde tooa set technologieën waarmee IT-onderbrekingen minimaliseert door zakelijke continuïteit van de IT-services via redundante en fouttolerantie of failover beveiligde onderdelen binnen Hallo **dezelfde** Datacenter. In ons geval binnen een Azure-regio.

**Herstel na noodgeval (DR)** is ook gericht Minimalisatie van het aantal onderbreking van de IT-services en hun herstel maar meerdere **verschillende** datacenters, die meestal zich honderden kilometers verwijderd. In ons geval meestal tussen verschillende Azure-regio's binnen Hallo dezelfde geopolitieke regio of zoals ingesteld door u als klant.

### <a name="overview-of-high-availability"></a>Overzicht van hoge beschikbaarheid
We kunnen gescheiden Hallo discussie over SAP hoge beschikbaarheid in Azure uit twee delen:

* **Hoge beschikbaarheid van Azure-infrastructuur**, bijvoorbeeld HA van compute (VM's), netwerk, opslag, enz. en de voordelen voor de beschikbaarheid van de SAP verhogen.
* **Hoge beschikbaarheid voor SAP-toepassing**, bijvoorbeeld HA van SAP-software-onderdelen:
  * SAP-toepassingsservers
  * SAP ASC's / SCS-exemplaar
  * Databaseserver

en hoe deze kan worden gecombineerd met de Azure-infrastructuur HA.

SAP hoge beschikbaarheid in Azure heeft enkele verschillen tooSAP hoge beschikbaarheid in een on-premises fysieke of virtuele omgeving. Hallo volgende papier uit SAP beschrijft standaardconfiguraties SAP hoge beschikbaarheid in gevirtualiseerde omgevingen in Windows: <http://scn.sap.com/docs/DOC-44415>. Er is geen sapinst geïntegreerd SAP-HA configuratie voor Linux zoals deze voor Windows bestaat. Met betrekking tot SAP HA on-premises voor Linux hier voor meer informatie kunt vinden: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Hoge beschikbaarheid van Azure-infrastructuur
Er is een enkel VM SLA van 99,9%. tooget een idee hoe Hallo beschikbaarheid van één VM uitzien zoals u kunt gewoon opbouwen Hallo product van andere beschikbare Azure serviceovereenkomsten Hallo: <https://azure.microsoft.com/support/legal/sla/>.

Hallo berekend op basis van Hallo is 30 dagen per maand of 43200 minuten. Daarom 0,05% uitvaltijd komt overeen met too21.6 minuten. Hallo beschikbaarheid van andere services hello wordt gewoon, Vermenigvuldig in de volgende manieren Hallo:

(Beschikbaarheidservice #1/100) * (beschikbaarheidservice #2/100) * (beschikbaarheidservice #3/100) *...

Zoals:

(99,95/100) * (99,9/100) * (99,9/100) = 0.9975 of een algemene beschikbaarheid van 99.75%.

#### <a name="virtual-machine-vm-high-availability"></a>Hoge beschikbaarheid van virtuele Machine (VM)
Er zijn twee soorten gebeurtenissen van Azure-platform die kunnen invloed hebben op Hallo van beschikbaarheid van uw virtuele machines: gepland onderhoud en niet-gepland onderhoud.

* Gebeurtenissen voor gepland onderhoud zijn periodieke updates die zijn gemaakt door Microsoft toohello onderliggende Azure-platform tooimprove algehele betrouwbaarheid, prestaties en beveiliging van Hallo platforminfrastructuur die op uw virtuele machines worden uitgevoerd.
* Niet-gepland onderhoud gebeurtenissen optreden wanneer Hallo hardware of fysieke infrastructuur onderliggende uw virtuele machine een fout in een bepaalde manier opgetreden is. Voorbeelden hiervan zijn lokale netwerkproblemen, lokale schijfdefecten of andere defecten op rack-niveau. Wanneer een dergelijke fout wordt gedetecteerd, wordt hello Azure-platform automatisch de virtuele machine migreren van Hallo slecht fysieke server die als host fungeert voor uw virtuele machine tooa orde fysieke server. Dergelijke gebeurtenissen zijn zeldzame, maar kunnen ook leiden tot uw virtuele machine tooreboot.

Meer informatie vindt u in deze documentatie: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Azure Storage redundantie
Hallo-gegevens in uw Microsoft Azure Storage-Account is altijd gerepliceerde tooensure duurzaamheid en hoge beschikbaarheid, voldoen aan de SERVICEOVEREENKOMST van Azure Storage Hallo zelfs in Hallo vlak van tijdelijke hardwarefouten.

Omdat Azure Storage is het houden van drie afbeeldingen van Hallo gegevens standaard, zijn RAID 5- of RAID1 over meerdere Azure-schijven niet nodig.

Meer informatie vindt u in dit artikel: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Met behulp van Azure-infrastructuur VM starten tooAchieve 'Hogere beschikbaarheid' van SAP-toepassingen
Als u geen toouse functies zoals Windows Server Failover Clustering (WSFC)- of pacemaker heeft op Linux besluit (momenteel alleen ondersteund voor SLES 12 en hoger), gebruikte tooprotect een SAP-systeem tegen de geplande en ongeplande uitval van hello Azure virtuele machine opnieuw opstarten is Fysieke server Azure-infrastructuur en algemene onderliggende Azure-platform.

> [!NOTE]
> Het is belangrijk toomention dat voornamelijk Azure VM opnieuw virtuele machines en geen toepassingen beveiligt. VM starten biedt geen hoge beschikbaarheid voor SAP-toepassingen, maar het biedt een zekere mate van beschikbaarheid van de infrastructuur en daarom indirect 'hogere beschikbaarheid' van SAP-systemen. Er is ook geen SLA voor Hallo lang die het duurt toorestart een virtuele machine na een onderbreking gepland of ongepland host. Deze methode van 'hoge beschikbaarheid' is daarom niet geschikt voor belangrijke onderdelen van een systeem SAP zoals (A) SCS of DBMS.
>
>

Een ander belangrijk infrastructuur element voor hoge beschikbaarheid is opslag. Voorbeeld is Azure Storage SLA 99,9% beschikbaarheid. Als er een implementeert alle virtuele machines met de schijven in één Azure Storage-Account, potentiële Azure Storage is niet beschikbaar zijn, wordt er geen beschikbaar zijn voor alle virtuele machines die in die Azure Storage-Account worden geplaatst en ook alle SAP onderdelen die op deze virtuele machines worden uitgevoerd.  

In plaats van alle virtuele machines in één enkele Azure Storage-Account te stellen, kunt u ook speciale opslag gebruiken accounts voor elke virtuele machine en op deze manier algemene beschikbaarheid van virtuele machine en SAP verhogen met behulp van meerdere onafhankelijke Azure Storage-Accounts.

Azure-schijven die beheerd worden automatisch in Hallo Foutdomein van Hallo virtuele machine die deze zijn gekoppeld aan geplaatst. Als u twee virtuele machines in een beschikbaarheidsset instellen en gebruiken van schijven beheerd, Hallo platform zorgt voor het distribueren van Hallo beheerd schijven in verschillende domeinen met fouten ook. Als u van plan toouse Premium-opslag bent, ten zeerste aangeraden schijven beheren en gebruiken.

Een voorbeeldarchitectuur voor een SAP NetWeaver-systeem dat gebruikmaakt van Azure-infrastructuur HA en storage-accounts kan er als volgt uitzien:

![Met behulp van Azure-infrastructuur HA tooachieve SAP 'hoger-knooppunt beschikbaarheid][planning-guide-figure-2900]

Een voorbeeldarchitectuur voor een SAP NetWeaver-systeem dat gebruikmaakt van Azure-infrastructuur HA en schijven beheerd kan er als volgt uit:

![Met behulp van Azure-infrastructuur HA tooachieve SAP 'hoger-knooppunt beschikbaarheid][planning-guide-figure-2901]

We bereikt Hallo volgen tot nu toe voor kritieke SAP-onderdelen:

* Hoge beschikbaarheid van SAP-toepassingsservers (AS)

  SAP-toepassingsexemplaren server zijn redundante componenten. Elk SAP omdat exemplaar wordt geïmplementeerd op een eigen virtuele machine die wordt uitgevoerd in een andere Azure-fouten en het upgraden van domein (Zie hoofdstukken [Foutdomeinen] [ planning-guide-3.2.1] en [domeinen upgraden][planning-guide-3.2.2]). Dit is gewaarborgd met behulp van Beschikbaarheidssets van Azure (Zie hoofdstuk [Beschikbaarheidssets van Azure][planning-guide-3.2.3]). Mogelijke gepland of ongepland ontbreken van een Azure-fout of het upgraden van domein, wordt niet beschikbaar zijn van een beperkt aantal virtuele machines met hun SAP-AS exemplaren.

  Elk omdat exemplaar wordt geplaatst in een eigen Azure Storage-account: potentiële ontbreken van een Azure Storage-Account wordt niet beschikbaar zijn van slechts één virtuele machine met de SAP-AS SAP-exemplaar. Let echter is er een limiet van Azure Storage-Accounts binnen een Azure-abonnement. tooensure automatisch wordt gestart (A) SCS exemplaar nadat Hallo VM opnieuw opstarten, zorg ervoor dat tooset Hallo Autostart parameter in (A) SCS-exemplaar starten profiel beschreven in hoofdstuk [met behulp van Autostart voor SAP-exemplaren] [ planning-guide-11.5].
  Lees ook hoofdstuk [hoge beschikbaarheid voor SAP-toepassingsservers] [ planning-guide-11.4.1] voor meer informatie.

  Zelfs als u schijven beheerd gebruikt, wordt deze schijven worden ook opgeslagen in een Azure Storage-Account en mag niet beschikbaar in een gebeurtenis van een onderbreking van de opslag.

* *Hogere* SCS beschikbaarheid van SAP (A)-exemplaar

  Hier maken we gebruik van Azure VM starten tooprotect Hallo VM met geïnstalleerde SCS SAP (A)-exemplaar. In hello geval van een geplande of niet-geplande uitvaltijd van Azure-servers, virtuele machines op een andere beschikbare server wordt opnieuw gestart. Zoals eerder gezegd, voornamelijk Azure VM opnieuw beveiligt virtuele machines en geen toepassingen, in dit geval Hallo (A) SCS-exemplaar. Via Hallo VM starten je we bereiken indirect 'hogere beschikbaarheid' van SCS SAP (A)-exemplaar. tooinsure automatisch wordt gestart (A) SCS exemplaar nadat Hallo VM opnieuw opstarten, zorg ervoor dat tooset Autostart parameter in (A) SCS-exemplaar dat wordt beschreven in hoofdstuk profiel starten [met behulp van Autostart voor SAP-exemplaren][planning-guide-11.5]. Dit betekent hello (A) SCS-exemplaar als een fouttolerantie (SPOF) in één VM Hallo doorslaggevend factor voor Hallo beschikbaarheid van de gehele SAP-liggend Hallo.

* *Hogere* beschikbaarheid van de DBMS-Server

  Hier gebruiksvoorbeeld vergelijkbare toohello SCS SAP (A)-exemplaar, maken we gebruik van Azure VM starten tooprotect Hallo VM met geïnstalleerde software die DBMS en wij bereiken 'hogere beschikbaarheid' DBMS software via de virtuele machine opnieuw opstarten.
  DBMS uitgevoerd in een enkele virtuele machine is ook een SPOF en het Hallo doorslaggevend factor voor Hallo beschikbaarheid van de gehele SAP-liggend Hallo is.

### <a name="sap-application-high-availability-on-azure-iaas"></a>SAP-toepassing voor hoge beschikbaarheid op Azure IaaS
tooachieve volledige SAP hoge beschikbaarheid van het systeem, moeten we tooprotect alle essentiële SAP-systeemonderdelen, voor toepassingsservers van voorbeeld redundante SAP, en unieke onderdelen (bijvoorbeeld fouttolerantie), zoals SAP (A) SCS-exemplaar en DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Hoge beschikbaarheid voor SAP-toepassingsservers
Voor Hallo SAP toepassingsexemplaren servers/dialoogvenster is het niet nodig toothink over een oplossing voor specifieke hoge beschikbaarheid. Hoge beschikbaarheid gewoon wordt gerealiseerd door redundantie en zodoende met voldoende hiervan in verschillende virtuele machines. Ze moeten alle worden geplaatst in dezelfde Beschikbaarheidsset Azure tooavoid die Hallo van virtuele machines worden op Hallo bijgewerkt mogelijk Hallo hetzelfde moment tijdens gepland onderhoud uitval. Hallo basisfunctionaliteit die is gebaseerd op andere Upgrade en domeinen met fouten binnen een Azure-schaaleenheid al is geïntroduceerd in hoofdstuk [domeinen upgraden][planning-guide-3.2.2]. Azure Beschikbaarheidssets in hoofdstuk gepresenteerd [Beschikbaarheidssets van Azure] [ planning-guide-3.2.3] van dit document.

Er is geen oneindig aantal probleem- en Upgrade-domeinen die kunnen worden gebruikt door een Azure-Beschikbaarheidsset binnen een Azure-schaaleenheid. Dit betekent dat als een aantal virtuele machines in een Beschikbaarheidsset, sneller of later meer dan één VM in Hallo dezelfde fout of het upgraden van domein belandt.

Implementatie van een paar SAP-toepassingsserver exemplaren in hun toegewezen virtuele machines en ervan uitgaande dat wij vijf domeinen upgraden, Hallo volgende afbeelding Hallo achter ontstaat. Hallo werkelijke maximum aantal fouten en update domeinen binnen een beschikbaarheidsset kan worden gewijzigd in toekomstige Hallo:

![HA van SAP-toepassingsservers in Azure][planning-guide-figure-3000]

Meer informatie vindt u in deze documentatie: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Hoge beschikbaarheid voor Hallo SCS SAP (A)-instantie op Windows
Windows Server Failover Cluster (WSFC) is een veelgebruikte oplossing tooprotect Hallo SCS SAP (A)-exemplaar. Het is ook geïntegreerd in sapinst in de vorm van een "HA-installatie. Hello Azure-infrastructuur is op dit moment niet kunnen tooprovide Hallo functionaliteit tooset up Hallo vereist Windows Server Failover Cluster Hallo dezelfde manier zoals deze wordt uitgevoerd op lokale.

Vanaf januari 2016 biedt hello Azure-cloud-platform met Hallo Windows-besturingssysteem geen mogelijkheid Hallo van het gebruik van een gedeeld clustervolume op een schijf die wordt gedeeld tussen twee virtuele Azure-machines.

Een geldige oplossing is echter Hallo gebruik van derden 3rd software waarmee u een gedeeld volume door synchrone en transparante schijfreplicatie die kan worden geïntegreerd in WSFC. Deze aanpak geeft aan dat alleen Hallo actieve clusterknooppunt is kunnen tooaccess één Hallo schijf op een punt in tijd opgehaald. Configuratie is vanaf januari 2016 deze HA ondersteunde tooprotect Hallo SCS SAP (A)-exemplaar op Windows gastbesturingssysteem op Azure VM's in combinatie met software van derden 3rd SIOS DataKeeper.

Hallo SIOS DataKeeper oplossing biedt een gedeelde schijf cluster resource tooWindows failoverclusters door:

* Een extra Azure-VHD die is gekoppeld tooeach van Hallo virtuele machines (VM's) die zich in een Cluster van Windows-configuratie
* SIOS DataKeeper Cluster Edition is uitgevoerd op beide knooppunten VM
* Met SIOS DataKeeper Cluster Edition is geconfigureerd op een manier die het Hallo-inhoud van aanvullende Hallo synchroon weerspiegelt VHD die is gekoppeld volume van bron VMs tooadditional VHD gekoppeld volume van de doel-virtuele machine.
* SIOS DataKeeper wordt onttrokken Hallo bron en doel lokale volumes en presenteren ze tooWindows Failover-Cluster als één gedeelde schijf.

U vindt alle informatie over het tooinstall een Windows-failovercluster met SIOS DataKeeper en SAP in Hallo [Clustering SAP ASC's exemplaar met gebruikmaking van Windows Server Failover Cluster in Azure met SIOS DataKeeper] [ ha-guide-classic]witboek.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Hoge beschikbaarheid voor Hallo SCS SAP (A)-instantie op Linux
Vanaf december 2015 is er ook geen equivalente tooshared schijf WSFC voor virtuele Linux-machines in Azure. Alternatieve oplossingen met behulp van software 3rd van derden zoals SIOS voor Windows zijn nog niet gevalideerde voor het uitvoeren van SAP op Linux op Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Hoge beschikbaarheid voor Hallo SAP-database-exemplaar
Hallo SAP DBMS HA standaardinstallatie is op basis van twee DBMS VMs waarbij DBMS hoge beschikbaarheid-functionaliteit wordt gebruikt tooreplicate gegevens van Hallo active DBMS exemplaar toohello tweede VM naar een passieve DBMS-instantie.

Hoge beschikbaarheid en noodherstel herstelfunctionaliteit voor DBMS in zowel algemeen als specifieke DBMS worden beschreven in Hallo [DBMS Deployment Guide][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Hoge beschikbaarheid voor end-to-End Hallo volledige SAP-systeem
Hier vindt u twee voorbeelden van een volledige SAP NetWeaver HA-architectuur in Azure - een voor Windows en een voor Linux.

Alleen schijven zonder begeleiding: Hallo concepten zoals hieronder wordt uitgelegd wellicht toobe iets geknoeid wanneer u veel SAP-systemen en implementeert Hallo aantal geïmplementeerde virtuele machines het maximum Hallo van Storage-Accounts per abonnement overschrijdt. In dergelijke gevallen moet de VHD's van VM's toobe gecombineerd binnen een Opslagaccount. Meestal zou u doen door een combinatie van VHD's van SAP toepassingslaag virtuele machines van verschillende SAP-systemen.  We gecombineerd ook andere VHD's van verschillende DBMS-virtuele machines van verschillende SAP-systemen in een Azure Storage-Account. Hallo IOPS-limieten van Azure Storage-Accounts waardoor Houd in gedachten (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] HA in Windows
![SAP NetWeaver HA toepassingsarchitectuur met SQL Server in Azure IaaS][planning-guide-figure-3200]

Hello Azure constructies na worden gebruikt voor Hallo SAP NetWeaver systeem, op het milieu toominimize op problemen van de infrastructuur en patchen host:

* Hallo volledige systeem wordt geïmplementeerd in Azure (vereist - DBMS laag, (A) SCS-exemplaar en de volledige toepassing laag nodig toorun in dezelfde locatie Hallo).
* Hallo volledige systeem wordt uitgevoerd binnen een Azure-abonnement (vereist).
* Hallo volledige systeem uitgevoerd binnen een Azure Virtual Network (vereist).
* Hallo scheiding van virtuele machines van één SAP-systeem Hallo in drie Beschikbaarheidssets is mogelijk zelfs met alle Hallo VM's die horen toohello hetzelfde virtuele netwerk.
* Alle exemplaren van een SAP-systeem DBMS actieve VM's zijn in een Beschikbaarheidsset. Er wordt ervan uitgegaan dat er meer dan één VM DBMS exemplaren per systeem wordt uitgevoerd sinds hoge beschikbaarheid van systeemeigen DBMS functies worden gebruikt, zoals SQL Server AlwaysOn- of Oracle Data Guard.
* Alle actieve exemplaren DBMS VM's gebruiken hun eigen opslagaccount. DBMS gegevens en logboekbestanden bestanden worden gerepliceerd van één account tooanother opslag opslagaccount met DBMS hoge beschikbaarheid functies waarmee Hallo gegevens worden gesynchroniseerd. Niet beschikbaar zijn van een opslagaccount zorgt ervoor dat er geen beschikbaar zijn van een SQL-Windows-clusterknooppunt, maar niet Hallo hele SQL Server-service.
* Alle virtuele machines (A) SCS-exemplaar van een SAP-systeem uitgevoerd, zijn in een Beschikbaarheidsset. Een Windows Server Failover Cluster (WSFC) is geconfigureerd op deze virtuele machines tooprotect hello (A) SCS-exemplaar.
* Alle virtuele machines (A) SCS exemplaren met hun eigen opslagaccount gebruiken. (A) SCS exemplaarbestanden en SAP globale map worden gerepliceerd van een storage account tooanother storage-account met behulp van SIOS DataKeeper replicatie. Niet beschikbaar zijn van een opslagaccount, wordt er geen beschikbaar zijn van een (A) SCS Windows clusterknooppunt, maar niet Hallo hele (A) SCS-service.
* ALLE Hallo VM's die vertegenwoordigt Hallo SAP toepassingslaag server zijn in een derde Beschikbaarheidsset.
* ALLE actieve SAP-toepassingsservers Hallo VM's gebruiken hun eigen opslagaccount. Niet beschikbaar zijn van een opslagaccount wordt niet beschikbaar zijn van een SAP-toepassingsserver, waar andere SAP-AS toorun gaan.

Hallo volgende afbeelding geïllustreerde Hallo die dezelfde liggend schijven beheerd.

![SAP NetWeaver HA toepassingsarchitectuur met SQL Server in Azure IaaS][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] HA op Linux
Hallo-architectuur voor SAP HA op Linux in Azure is in feite Hallo hetzelfde als die voor Windows als hierboven beschreven. Vanaf januari 2016 er is geen SAP (A) SCS HA oplossing nog ondersteund op Linux op Azure

Als gevolg hiervan januari 2016 een SAP-Linux-Azure-systeem niet kan bereiken Hallo dezelfde beschikbaarheid als een SAP Windows Azure-systeem verbroken vanwege ontbrekende HA voor hello (A) SCS exemplaar en Hallo single instance SAP-as-omgeving database.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Met behulp van Autostart voor SAP-exemplaren
SAP aangeboden Hallo functionaliteit toostart SAP exemplaren onmiddellijk na de start Hallo Hallo OS binnen Hallo VM. Hallo exacte stappen zijn beschreven in Knowledge Base-artikel SAP [1909114]. Echter, SAP is niet aanbevelen toouse Hallo instelling meer omdat er geen controle in de volgorde Hallo van exemplaar opnieuw is opgestart, ervan uitgaande dat meer dan één VM heeft invloed op een of meerdere exemplaren per virtuele machine is uitgevoerd. Ervan uitgaande dat een Azure standaardscenario van één SAP application server-exemplaar in een virtuele machine en Hallo geval van één VM uiteindelijk ophalen opnieuw wordt opgestart, Hallo Autostart is niet echt kritiek en kan worden ingeschakeld door deze parameter toe te voegen:

    Autostart = 1

Start in Hallo profiel van Hallo SAP ABAP en/of Java-exemplaar.

> [!NOTE]
> Hallo Autostart parameter kan ook bepaalde downfalls hebben. In meer detail Hallo Hallo parameter triggers begin van een SAP ABAP of Java-exemplaar als Hallo gerelateerd Windows of Linux-service van het Hallo-exemplaar is gestart. Dat gewoon Hallo geval is wanneer Hallo-besturingssysteem wordt opgestart. Echter opnieuw opstarten van SAP-services zijn ook een algemene ding voor SAP Software levenscyclusbeheer functionaliteit zoals som of andere updates of upgrades. Deze functies zijn niet verwacht voor een exemplaar toobe helemaal opnieuw opgestart. Hallo Autostart parameter moet daarom worden uitgeschakeld voordat u taken uitvoert. Hallo Autostart parameter mag ook niet worden gebruikt voor SAP-exemplaren die zijn geclusterd, zoals SCS-ASC's / CI.
>
>

Zie voor aanvullende informatie met betrekking tot autostart voor SAP hier exemplaren:

* [SAP samen met uw Unix-Server starten/stoppen, starten/stoppen](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Starten en stoppen SAP NetWeaver Beheeragents](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Hoe tooenable automatisch starten van HANA-Database](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Grotere 3-Laagse SAP-systemen
Aspecten van hoge beschikbaarheid van 3-Laagse SAP-configuraties is al in de vorige secties beschreven. Maar wat over systemen waarbij Hallo DBMS serververeisten zijn te groot toohave dat deze zich in Azure, maar Hallo SAP toepassingslaag kan worden geïmplementeerd in Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Locatie van 3-Laagse SAP-configuraties
Het is niet de ondersteunde toosplit Hallo toepassingslaag zelf of de toepassing hello of DBMS tussen on-premises en Azure. Een SAP-systeem is volledig geïmplementeerde on-premises of in Azure. Het is ook niet ondersteunde toohave aantal toepassingsservers Hallo on-premises en andere uitvoeren in Azure. Beginpunt van Hallo discussie Hallo is. We ook ondersteunt geen toohave Hallo DBMS onderdelen van een SAP-systeem en Hallo SAP server toepassingslaag geïmplementeerd in twee verschillende Azure-regio's. Bijvoorbeeld DBMS in VS-West en SAP toepassingslaag in VS-midden. Reden voor ondersteunt geen dergelijke configuraties is Hallo latentie gevoeligheid van Hallo SAP NetWeaver architectuur.

In de loop Hallo van vorig jaar data ontwikkeld center partners echter CO-locaties tooAzure regio's. Deze CO-locaties zijn vaak in heel dicht toohello fysieke Azure data centers binnen een Azure-regio. Hallo korte afstand en activa in Hallo CO-locatie via ExpressRoute in Azure-verbinding kunnen resulteren in een latentie van minder dan 2 MS. In dergelijke gevallen kan toolocate Hallo DBMS laag (inclusief opslag SAN/NAS) in die een CO-locatie en Hallo SAP toepassingslaag in Azure. Vanaf december 2015, er zijn momenteel geen implementaties die. Maar verschillende klanten met implementaties van toepassingen niet SAP dergelijke benaderingen al gebruikt.

### <a name="offline-backup-of-sap-systems"></a>Offline back-up van SAP-systemen
Afhankelijk van Hallo SAP-configuratie (laag 2 of 3-Laagse) er gekozen mogelijk een tooback nodig. Hallo-inhoud van virtuele machine zelf Hallo plus toohave een back-up van database Hallo. Hallo DBMS-gerelateerde back-ups zijn verwachte toobe klaar met de database-methoden. Een gedetailleerde beschrijving voor de verschillende databases hello, vindt u in [DBMS handleiding][dbms-guide]. Op Hallo daarentegen, Hallo SAP-gegevens kan een back-up op een offline manier (inclusief ook Hallo database-inhoud) zoals beschreven in deze sectie of online zoals beschreven in de volgende sectie Hallo.

Hallo offline back-ups in feite vereist afsluiten Hallo VM via hello Azure-portal en een kopie van Hallo basisschijf VM plus alle gekoppelde schijven toohello VM. Dit zou een punt in tijd installatiekopie Hallo VM en de bijbehorende schijf behouden. Back-ups' toocopy Hallo' wordt aangeraden in een andere Azure-Opslagaccount. Daarom Hallo procedure beschreven in hoofdstuk [kopiëren van schijven tussen Azure Storage-Accounts] [ planning-guide-5.4.2] van dit document wilt toepassen.
Naast het Hallo afsluiten met hello Azure portal een kunt ook dit doen via Powershell of CLI zoals hier wordt beschreven: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Kan bestaan uit een herstelpunt van die staat van het verwijderen van Hallo base VM ook als de oorspronkelijke schijven Hallo Hallo baseren VM en gekoppelde schijven, terug kopiëren Hallo opgeslagen schijven toohello oorspronkelijke Storage-Account of de resource-groep voor beheerde schijven en het vervolgens opnieuw Hallo systeem te implementeren.
In dit artikel ziet u een voorbeeld het tooscript dit proces Powershell: <http://www.westerndevs.com/azure-snapshots/>

Zorg ervoor dat tooinstall een nieuwe SAP-licentie omdat een virtuele machine back-up herstellen als hierboven beschreven een nieuwe hardwaresleutel maakt.

### <a name="online-backup-of-an-sap-system"></a>Online back-up van een SAP-systeem
Back-up van Hallo DBMS wordt uitgevoerd met DBMS-specifieke methoden, zoals beschreven in Hallo [DBMS handleiding][dbms-guide].

Andere virtuele machines binnen Hallo SAP-systeem kunnen back-up met functionaliteit voor Azure virtuele Machine back-up worden gemaakt. Azure virtuele Machine back-up is geïntroduceerd vroeg in 2015 en ondertussen is een standaardmethode tooback van een volledige virtuele machine in Azure. Azure Backup Hallo back-ups opslaat in Azure en Hiermee kunt een herstel van een virtuele machine opnieuw.

> [!NOTE]
> Vanaf december 2015 met VM-back-up houdt geen Hallo unieke ID van VM die wordt gebruikt voor SAP-licentieverlening. Dit betekent dat een herstelbewerking voor een VM-back-installatie van een nieuwe SAP-licentiecode as Hallo herstel-VM wordt beschouwd als toobe een nieuwe virtuele machine vereist en niet als vervanging van de voormalige die is opgeslagen.
>
> ![Windows][Logo_Windows] Windows
>
> Theorie, de virtuele machines die uitvoeren databases kunnen een back-up op een consistente manier ook als Hallo DBMS-systeem Hallo Windows VSS ondersteunt (Volume Shadow Copy Service <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >) als, bijvoorbeeld SQL Server heeft.
> Let echter die op basis van de virtuele machine van Azure back-ups punt in tijd worden hersteld van de databases zijn niet mogelijk. Daarom is de aanbeveling tooperform back-ups van databases met DBMS-functionaliteit in plaats van te vertrouwen op Azure VM Backup.
>
> tooget bekend bent met de back-up van Azure virtuele Machine start hier: <https://docs.microsoft.com/azure/backup/backup-azure-vms>.
>
> Andere mogelijkheden zijn toouse een combinatie van Microsoft Data Protection Manager geïnstalleerd in een virtuele machine van Azure en Azure back-up naar back-up/herstel databases. Meer informatie vindt u hier: <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>.  
>
> ![Linux][Logo_Linux] Linux
>
> Er is geen equivalent tooWindows VSS in Linux. Alleen bestandsconsistente back-ups zijn daarom mogelijk, maar geen toepassingsconsistente back-ups. Hallo SAP DBMS back-up moet worden gedaan met behulp van de DBMS-functionaliteit. Hallo bestandssysteem waaronder Hallo SAP-gerelateerde gegevens kan worden opgeslagen, bijvoorbeeld met tar zoals beschreven hier: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure als DR-site voor productie SAP landschappen
Sinds Mid 2014 inschakelen extensies toovarious onderdelen om Hyper-V, System Center en Azure Hallo gebruik van Azure als DR-site voor VM's die lokaal op basis van Hyper-V wordt uitgevoerd.

Een blog met gedetailleerde informatie over hoe toodeploy deze oplossing is ze hier zijn beschreven: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>.

## <a name="summary"></a>Samenvatting
Hallo belangrijke punten van hoge beschikbaarheid voor SAP-systemen in Azure zijn:

* Op dit moment, Hallo SAP storingspunt niet kan worden beveiligd exact dezelfde Hallo zoals deze kan worden uitgevoerd in de on-premises implementaties. Hallo reden is dat gedeelde schijfclusters op nog Azure zonder het gebruik van 3e software van derden Hallo kunnen niet worden gemaakt.
* U moet toouse DBMS-functionaliteit die niet afhankelijk van de gedeelde schijf cluster technologie voor Hallo DBMS laag. Details worden gedocumenteerd in Hallo [DBMS handleiding][dbms-guide].
* toominimize hello invloed van problemen binnen domeinen met fouten in hello Azure-infrastructuur of host onderhoud, moet u Beschikbaarheidssets van Azure gebruiken:
  * Het verdient aanbeveling toohave een Beschikbaarheidsset voor Hallo SAP toepassingslaag.
  * Het wordt aanbevolen een afzonderlijke beschikbaarheid instellen voor Hallo SAP DBMS laag toohave.
  * Het is niet raadzaam tooapply Hallo die dezelfde voor virtuele machines van verschillende SAP-systemen beschikbaarheidsset.
  * Het verdient aanbeveling toouse Premium-beheerde schijven.
* Controleer voor de doeleinden van de back-up van Hallo SAP DBMS laag, Hallo [DBMS handleiding][dbms-guide].
* Een back-up SAP dialoogvenster exemplaren zinvol weinig omdat het is doorgaans sneller tooredeploy eenvoudig dialoogvenster exemplaren.
* Een back-up Hallo VM waarin Hallo globale directory Hallo SAP-systeem en daarmee alle Hallo profielen van de verschillende exemplaren hello, zinvol zijn en moet worden uitgevoerd met Windows back-up of bijvoorbeeld tar op Linux. Omdat er verschillen tussen Windows Server 2008 (R2) en Windows Server 2012 (R2), zodat het eenvoudiger tooback met behulp van Hallo recentere Windows Server-versies, is het raadzaam toorun Windows Server 2012 (R2) als gastbesturingssysteem voor Windows.
