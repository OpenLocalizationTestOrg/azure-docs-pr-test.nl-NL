---
title: implementatie van virtuele Machines voor SAP op Windows aaaAzure | Microsoft Docs
description: Meer informatie over hoe toodeploy SAP-software op Windows virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>SAP op Windows-machines in Azure implementeren
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
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
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
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
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

Virtuele Machines in Azure is Hallo-oplossing voor organisaties die berekenings-en opslagbronnen nodig in de minimale tijd en zonder langdurige inkoop cycli. U kunt Azure Virtual Machines toodeploy klassieke toepassingen, zoals SAP NetWeaver gebaseerde toepassingen in Azure gebruiken. Uitbreiden van een toepassing betrouwbaarheid en beschikbaarheid zonder dat extra on-premises resources. Virtuele Machines in Azure ondersteunt cross-premises connectiviteit, zodat u kunt Azure Virtual Machines integreren in uw organisatie lokale domeinen, privéclouds en SAP system Liggend.

In dit artikel komen we Hallo stappen toodeploy SAP-toepassingen op virtuele machines (VM's) in Azure. In dit artikel is gebaseerd op informatie Hallo in [Azure Virtual Machines planning en implementatie voor SAP op Windows][planning-guide]. Ook als aanvulling SAP installatie documentatie en SAP-opmerkingen, de primaire bronnen voor het installeren en implementeren van software voor SAP Hallo op.

## <a name="prerequisites"></a>Vereisten
Instellen van een virtuele machine van Azure voor SAP-software-implementatie omvat meerdere stappen en bronnen. Zorg voordat u begint, dat u voldoet aan de Hallo-vereisten voor het SAP-software installeren op Windows virtuele machines in Azure.

### <a name="local-computer"></a>Lokale computer
toomanage Windows of Linux-machines, kunt u een PowerShell-script en hello Azure-portal. Voor beide hulpprogramma's moet u een lokale computer met Windows 7 of een latere versie van Windows. Als u wilt dat toomanage alleen virtuele Linux-machines en u wilt dat toouse een Linux-computer om deze taak kunt u Azure CLI.

### <a name="internet-connection"></a>Internetverbinding
toodownload en Voer Hallo-hulpprogramma's en scripts die vereist voor software-SAP-implementatie zijn, moet u toohello Internet is verbonden. virtuele machine van Azure met Azure verbeterde extensie Monitoring voor SAP Hallo Hallo moet ook toegang toohello Internet. Als hello Azure virtuele machine deel van een virtuele Azure-netwerk of het lokale domein uitmaakt, zorg ervoor dat Hallo relevante proxy-instellingen zijn ingesteld, zoals beschreven in [Hallo proxy configureren][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Microsoft Azure-abonnement
U moet een actief Azure-account.

### <a name="topology-and-networking"></a>Topologie en netwerken
U moet toodefine Hallo topologie en architectuur van Hallo SAP-implementatie in Azure:

* Azure storage-accounts toobe gebruikt
* Virtueel netwerk waar u toodeploy Hallo SAP-systeem
* Resource group toowhich gewenste toodeploy Hallo SAP-systeem
* Azure-regio waar u toodeploy Hallo SAP-systeem
* SAP-configuratie (twee lagen of drie lagen)
* VM-grootten en Hallo aantal extra virtuele harde schijven (VHD's) toobe gekoppeld toohello virtuele machines
* Configuratie van SAP correctie en Transport-systeem (CTS)

Maak en configureer Azure storage-accounts of Azure virtual networks voordat u begint met Hallo SAP software-implementatieproces. Voor informatie over het toocreate en configureren van deze resources, zien [Azure Virtual Machines planning en implementatie voor SAP op Windows][planning-guide].

### <a name="sap-sizing"></a>SAP-schaling
Hallo volgende informatie voor SAP sizing weten:

* Geprojecteerd SAP-werkbelasting, bijvoorbeeld met behulp van Hallo SAP snelle Sizer tool en Hallo SAP toepassing prestaties Standard (SAP's) getal
* Vereiste resource en geheugen processorgebruik van Hallo SAP-systeem
* Vereiste input/output (I/O)-bewerkingen per seconde
* Netwerkbandbreedte van uiteindelijke communicatie tussen virtuele machines in Azure vereist
* Vereiste netwerkbandbreedte tussen lokale activa en hello Azure geïmplementeerd SAP-systeem

### <a name="resource-groups"></a>Resourcegroepen
In Azure Resource Manager kunt u resource groepen toomanage alle Hallo toepassingsresources in uw Azure-abonnement. Zie voor meer informatie [overzicht van Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Resources

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP-resources
Wanneer u uw SAP-software-implementatie instelt, moet u Hallo SAP-resources te volgen:

* SAP-notitie [1928533], die is:
  * Lijst met Azure VM-grootten die worden ondersteund voor de implementatie van Hallo van SAP-software
  * Informatie over belangrijke capaciteit voor Azure VM-grootten
  * Ondersteunde SAP-software en besturingssysteem (OS) en combinaties van de database
  * Vereiste SAP-kernel-versie voor Windows en Linux op Microsoft Azure

* SAP-notitie [2015553] bevat vereisten voor software-implementaties SAP SAP ondersteund in Azure.
* SAP-notitie [2178632] bevat gedetailleerde informatie over alle bewaking metrische gegevens die zijn gerapporteerd voor SAP in Azure.
* SAP-notitie [1409604] heeft Hallo SAP Host Agent-versie vereist voor Windows in Azure.
* SAP-notitie [2191498] Hallo vereist SAP Host Agent-versie voor Linux in Azure.
* SAP-notitie [2243692] bevat informatie over SAP licentieverlening op Linux in Azure.
* SAP-notitie [1984787] heeft algemene informatie over SUSE Linux Enterprise Server 12.
* SAP-notitie [2002167] heeft algemene informatie over Red Hat Enterprise Linux 7.x.
* SAP-notitie [1999351] bevat aanvullende informatie over probleemoplossing voor hello Azure verbeterde extensie Monitoring voor SAP.
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) heeft alle SAP-opmerkingen voor Linux vereist.
* SAP-specifieke PowerShell-cmdlets die deel van uitmaken [Azure PowerShell][azure-ps].
* SAP-specifieke Azure CLI-opdrachten die deel van uitmaken [Azure CLI][azure-cli].

[comment]: <> (Het patchniveau MSSedusch TODO toevoegen ARM voor SAP Host Agent in SAP-notitie 1409604)

### <a name="microsoft-resources"></a>Microsoft-bronnen
Deze artikelen Microsoft omvatten SAP-implementaties in Azure:

* [Azure virtuele Machines, planning en implementatie voor SAP in Windows][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP in Windows (in dit artikel)][deployment-guide]
* [Voor SAP in Windows Azure virtuele Machines DBMS-implementatie][dbms-guide]
* [Azure-portal][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Implementatiescenario's voor SAP-software op Azure Virtual machines
U hebt meerdere mogelijkheden voor het implementeren van virtuele machines en gekoppelde schijven in Azure. Het is belangrijk toounderstand Hallo verschillen tussen implementatieopties, omdat u mogelijk verschillende stappen tooprepare nemen uw VM's voor implementatie op basis van implementatietype Hallo die u kiest.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Implementatie van een virtuele machine uit Azure Marketplace voor SAP Hallo
U kunt een installatiekopie van een geleverd door Microsoft gebruiken of door een derde partij in hello Azure Marketplace toodeploy uw virtuele machine. Hallo Marketplace biedt een aantal standaard installatiekopieën van het besturingssysteem van Windows Server en verschillende Linux-distributies. U kunt een installatiekopie die database-beheer bevat ook implementeren system (DBMS) SKU's, bijvoorbeeld Microsoft SQL Server. Zie voor meer informatie over het gebruik van afbeeldingen met DBMS SKU's [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide].

Hallo toont volgende stroomdiagram Hallo SAP-specifieke volgorde van de stappen voor het implementeren van een virtuele machine uit Azure Marketplace Hallo:

![Stroomdiagram van VM-implementatie voor SAP-systemen met behulp van een VM-installatiekopie uit hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Een virtuele machine maken met behulp van hello Azure-portal
Hallo gemakkelijkste manier toocreate een nieuwe virtuele machine met een installatiekopie van hello Azure Marketplace is via hello Azure-portal.

1.  Ga te<https://portal.azure.com/#create>.  Of Selecteer in het menu van Azure portal hello, **+ nieuw**.
2.  Selecteer **Compute**, en selecteer vervolgens Hallo-type van het besturingssysteem die u wilt dat toodeploy. Bijvoorbeeld, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) of Red Hat Enterprise Linux 7.2 (RHEL 7.2). Hallo lijst standaardweergave wordt niet weergegeven voor dat alle ondersteunde besturingssystemen. Selecteer **alle** voor een volledige lijst. Zie voor meer informatie over ondersteunde besturingssystemen voor software-implementatie voor SAP SAP-notitie [1928533].
3.  Controleer op de volgende pagina Hallo voorwaarden en bepalingen.
4.  In Hallo **een implementatiemodel selecteren** Selecteer **Resource Manager**.
5.  Selecteer **Maken**.

Hallo wizard begeleidt u bij het instellen van Hallo vereist parameters toocreate Hallo virtuele machine, moet bovendien tooall bronnen, zoals netwerkinterfaces en storage-accounts. Enkele van deze parameters zijn:

1. **Basisprincipes**:
  * **Naam**: Hallo-naam van Hallo bron (naam Hallo virtuele machine).
 * **Gebruikersnaam en wachtwoord** of **openbare SSH-sleutel**: Hallo gebruikersnaam en wachtwoord van Hallo-gebruiker die is gemaakt tijdens het inrichten van Hallo invoeren. Voor een virtuele Linux-machine, kunt u Hallo openbare Secure Shell (SSH) sleutel toosign in toohello machine te gebruiken.
 * **Abonnement**: Selecteer Hallo-abonnement dat u wilt dat toouse tooprovision Hallo nieuwe virtuele machine.
 * **Resourcegroep**: Hallo-naam van resourcegroep Hallo voor Hallo VM. U kunt beide Hallo-naam van een nieuwe groep of Hallo resourcenaam van een resourcegroep die al bestaat.
 * **Locatie**: waar toodeploy Hallo nieuwe virtuele machine. Als u tooconnect Hallo virtuele machine tooyour on-premises netwerk wilt, zorg ervoor dat u selecteert Hallo-locatie van het virtuele netwerk Hallo die Azure tooyour on-premises netwerk verbindt. Zie voor meer informatie [Microsoft Azure-netwerken] [ planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide].
2. **De grootte van**:

     Zie voor een lijst van ondersteunde VM typen SAP-notitie [1928533]. Zorg ervoor dat u Hallo juiste VM-type selecteren als u wilt dat toouse Azure Premium-opslag. Niet alle VM-typen bieden ondersteuning voor Premium-opslag. Zie voor meer informatie [opslag: Microsoft Azure Storage- en gegevensschijven] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] en [Azure Premium-opslag] [ planning-guide-azure-premium-storage] in [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide].

3. **Instellingen**:
   * **Storage-account**: Selecteer een bestaand opslagaccount of maak een nieuwe. Niet alle opslagtypen werken voor SAP-toepassingen. Zie voor meer informatie over opslagtypen [Microsoft Azure Storage] [ dbms-guide-2.3] in [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide].
   * **Virtueel netwerk** en **Subnet**: toointegrate Hallo virtuele machine met het intranet, selecteer Hallo virtueel netwerk dat is verbonden tooyour on-premises netwerk.
   * **Openbaar IP-adres**: Selecteer Hallo openbare IP-adres dat u toouse wilt, of Geef parameters toocreate een nieuw openbaar IP-adres. U kunt een openbare IP-adres tooaccess uw virtuele machine via Hallo Internet. Zorg ervoor dat ook een network security groep toohelp veilige toegang tooyour virtuele machine te maken.
   * **Netwerkbeveiligingsgroep**: Zie voor meer informatie [beheren van netwerkverkeer met netwerkbeveiligingsgroepen][virtual-networks-nsg].
   * **Beschikbaarheid**: een beschikbaarheidsset selecteren of Voer Hallo parameters toocreate een nieuwe beschikbaarheid instellen. Zie voor meer informatie [Azure beschikbaarheidssets][planning-guide-3.2.3].
   * **Bewaking**: U kunt selecteren **uitschakelen** voor het bewaken van diagnostische gegevens. Er wordt automatisch ingeschakeld tijdens het uitvoeren van Hallo opdrachten tooenable hello Azure verbeterde extensie Monitoring, zoals beschreven in [configureren bewaking][deployment-guide-configure-monitoring-scenario-1].

4. **Samenvatting**:

  Bekijk uw selecties en selecteer vervolgens **OK**.

De virtuele machine wordt geïmplementeerd in Hallo-resourcegroep die u hebt geselecteerd.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Een virtuele machine met behulp van een sjabloon maken
U kunt een virtuele machine maken met behulp van een Hallo SAP sjablonen zijn gepubliceerd in Hallo [GitHub-opslagplaats voor azure-snelstartsjablonen][azure-quickstart-templates-github]. U kunt ook handmatig maken een virtuele machine met behulp van Hallo [Azure-portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], of [Azure CLI ][virtual-machines-linux-tutorial].

* [**Met twee lagen (slechts één virtuele machine) configuratiesjabloon** (sap-2-laag-marketplace-installatiekopie)][sap-templates-2-tier-marketplace-image]

  toocreate een systeem met twee lagen met behulp van slechts één virtuele machine, gebruik deze sjabloon.
* [**Configuratie met drie lagen (meerdere virtuele machines) sjabloon** (sap-3-tier-marketplace-installatiekopie)][sap-templates-3-tier-marketplace-image]

  een systeem met drie lagen met behulp van meerdere virtuele machines toocreate deze sjabloon gebruiken.

Voer in hello Azure-portal, Hallo parameters voor de sjabloon hello te volgen:

1. **Basisprincipes**:
  * **Abonnement**: Hallo abonnement toouse toodeploy Hallo sjabloon.
  * **Resourcegroep**: Hallo resource groep toouse toodeploy Hallo-sjabloon. U kunt een nieuwe resourcegroep maken of u kunt een bestaande resourcegroep in Hallo abonnement selecteren.
  * **Locatie**: waar toodeploy Hallo sjabloon. Als u een bestaande resourcegroep hebt geselecteerd, wordt Hallo-locatie van die resourcegroep gebruikt.

2. **Instellingen**:
  * **ID van het systeem SAP**: Hallo SAP systeem-ID (SID).
  * **Type besturingssysteem**: Hallo besturingssysteem die u wilt dat toodeploy, bijvoorbeeld, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) of Red Hat Enterprise Linux 7.2 (RHEL 7.2).

    Hallo lijst standaardweergave wordt niet weergegeven voor dat alle ondersteunde besturingssystemen. Selecteer **alle** voor een volledige lijst. Zie voor meer informatie over ondersteunde besturingssystemen voor software-implementatie voor SAP SAP-notitie [1928533].
  * **Grootte van het SAP**: Hallo grootte van Hallo SAP-systeem.

    aantal nieuwe systeem voor SAP's Hallo Hallo biedt. Als u niet zeker hoeveel SAP's Hallo systeem vereist is weet, vraagt u uw SAP-technologie Partner of System Integrator.
  * **Beschikbaarheid van het systeem** (alleen drie lagen-sjabloon): Hallo beschikbaarheid van het systeem.

    Selecteer **HA** voor een configuratie die geschikt is voor de installatie van een hoge beschikbaarheid. Twee databaseservers en twee servers voor ABAP SAP centrale Services (ASC's) worden gemaakt.
  * **Opslagtype** (alleen twee lagen-sjabloon): type opslag toouse Hallo.

    Voor grotere systemen ten zeerste aangeraden Azure Premium-opslag. Zie de volgende bronnen voor meer informatie over opslagtypen:
      * [Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] in [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]
      * [Premium-opslag: Krachtige opslag voor Azure Virtual Machine-werkbelasting][storage-premium-storage-preview-portal]
      * [Inleiding tooMicrosoft Azure Storage][storage-introduction]
  * **Gebruikersnaam van de beheerder** en **beheerderswachtwoord**: een gebruikersnaam en wachtwoord.
    Een nieuwe gebruiker is gemaakt voor het aanmelden toohello virtuele machine.
  * **Nieuwe of bestaande subnet**: bepaalt of een nieuw virtueel netwerk en subnet worden gemaakt of een bestaand subnet wordt gebruikt. Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.
  * **Subnet-ID**: Hallo-ID van Hallo subnet Hallo virtuele machines verbinding maken. Selecteer subnet Hallo van uw virtueel particulier netwerk (VPN) of Azure ExpressRoute virtueel netwerk toouse tooconnect Hallo virtuele machine tooyour on-premises netwerk. Hallo-ID meestal uitziet: /subscriptions/&lt;abonnements-id > /resourceGroups/&lt;Resourcegroepnaam > /providers/Microsoft.Network/virtualNetworks/&lt;virtuele-netwerknaam > /subnets/&lt;subnetnaam >

3. **Voorwaarden en bepalingen**:  
    Lees en accepteer de juridische voorwaarden Hallo.

4.  Selecteer **aankoop**.

Hello Azure VM-Agent wordt geïmplementeerd standaard, wanneer u een installatiekopie van hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Proxy-instellingen configureren
Afhankelijk van hoe uw on-premises netwerk is geconfigureerd, moet u mogelijk tooset up Hallo proxy op de virtuele machine. Als uw VM verbonden tooyour on-premises netwerk via VPN- of ExpressRoute is, Hallo VM mogelijk niet worden kunnen tooaccess Hallo Internet, en won't kunnen toodownload Hallo vereist extensies of bewakingsgegevens verzamelen. Zie voor meer informatie [Hallo proxy configureren][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Lid worden van een domein (alleen Windows)
Als uw Azure-implementatie verbonden tooan lokale Active Directory- of DNS-exemplaar is via een Azure site-naar-site VPN-verbinding of ExpressRoute (dit heet *cross-premises* in [Azure Virtual Machines plannen en de implementatie voor SAP op Linux][planning-guide]), wordt verwacht dat Hallo VM lid wordt van een lokaal domein. Zie voor meer informatie over overwegingen voor deze taak [toevoegen aan een VM tooan lokale domein (alleen Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Bewaking configureren
controleren of uw omgeving ondersteunt SAP, hello Azure extensie Monitoring voor SAP ingesteld zoals beschreven toobe [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5]. Hallo-vereisten voor SAP controle en de vereiste minimale versie van SAP Kernel en SAP-Agent Host in Hallo bronnen in [SAP resources][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Bewaking van selectievakje
Controleer of bewaking werkt, zoals beschreven in [controles en het oplossen van problemen voor het instellen van het end-to-end bewaking][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Stappen na de implementatie
Nadat u hebt gemaakt Hallo VM en Hallo VM is geïmplementeerd, moet u tooinstall Hallo vereist softwareonderdelen in Hallo VM. Vanwege Hallo implementatie/software-installatie sequence in dit type implementatie VM moet Hallo software toobe geïnstalleerd al beschikbaar zijn, in Azure, op een andere virtuele machine of als een schijf die kan worden gekoppeld. Of u kunt met behulp van een cross-premises-scenario in welke connectiviteit toohello lokale activa (installatie shares) krijgt.

Nadat u uw virtuele machine in Azure implementeert, volg dezelfde Hallo richtlijnen en hulpprogramma's voor tooinstall Hallo SAP-software op uw virtuele machine als u zou doen in een on-premises omgeving. tooinstall SAP-software op een virtuele machine in Azure, beide SAP en Microsoft u het beste uploaden en Hallo SAP-installatiemedia op Azure VHD's opslaan, of dat u maakt een virtuele machine van Azure die geschikt is als een bestandsserver met alle Hallo vereist SAP-installatiemedia.

[comment]: <> (MSSedusch TODO waarom ik een Bestandsbeheer toorecommend bijvoorbeeld moet, bestands- of VHD? Is dit dus verschillende on-premises?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Een virtuele machine met een aangepaste installatiekopie voor SAP implementeren
Omdat er verschillende versies van een besturingssysteem of DBMS patch verschillende behoeften hebben, u in Azure Marketplace Hallo vindt Hallo-afbeeldingen mogelijk niet voldoet aan uw behoeften. U kunt in plaats daarvan toocreate een virtuele machine met behulp van uw eigen OS/DBMS VM-installatiekopie, die u later opnieuw kunt implementeren.
U verschillende stappen toocreate een installatiekopie van een persoonlijke voor Linux dan toocreate voor Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> een Windows-installatiekopie die u toodeploy meerdere virtuele machines, Hallo Windows-instellingen (zoals Windows SID en de hostnaam kunt) moeten worden gescheiden of gegeneraliseerd op Hallo tooprepare lokale VM. U kunt [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo dit.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare een Linux-installatiekopie die u toodeploy meerdere virtuele machines gebruiken kunt, sommige instellingen Linux moet abstracte of gegeneraliseerde op Hallo lokale VM. U kunt `waagent -deprovision` toodo dit. Zie voor meer informatie [vastleggen van een virtuele Linux-machine uitgevoerd op Azure] [ virtual-machines-linux-capture-image] en Hallo [gebruikershandleiding voor Azure Linux agent][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
U kunt voorbereiden en een aangepaste installatiekopie maken en gebruik vervolgens toocreate meerdere nieuwe virtuele machines. Dit wordt beschreven in [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide]. Instellen van uw database inhoud met behulp van SAP Software inrichting Manager tooinstall een nieuw SAP-systeem (u herstelt een databaseback-up van een VHD die is aangesloten toohello virtuele machine) of door rechtstreeks een back-up van de database herstellen naar Azure storage als het DBMS ondersteuning voor biedt. Zie voor meer informatie [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]. Als u al een SAP-systeem op uw lokale virtuele machine (vooral voor systemen met twee lagen) hebt geïnstalleerd, kunt u Hallo SAP-systeeminstellingen na de implementatie van hello Azure VM Hallo aanpassen met behulp van Hallo System wijzigen procedure ondersteund door de SAP softwarelevering Manager (SAP-notitie [1619720]). U kunt anders Hallo SAP-software installeren nadat u hello Azure VM implementeren.

Hallo toont volgende stroomdiagram Hallo SAP-specifieke volgorde van de stappen voor het implementeren van een virtuele machine van een aangepaste installatiekopie:

![Stroomdiagram van VM-implementatie voor SAP-systemen met behulp van een VM-installatiekopie in Marketplace persoonlijke][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Hallo virtuele machine maken
toocreate een implementatie met behulp van een persoonlijke installatiekopie van het besturingssysteem van hello Azure-portal, gebruikt u een Hallo SAP-sjablonen te volgen. Deze sjablonen zijn gepubliceerd in Hallo [GitHub-opslagplaats voor azure-snelstartsjablonen][azure-quickstart-templates-github]. U kunt ook handmatig maken een virtuele machine, met behulp van [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Met twee lagen (slechts één virtuele machine) configuratiesjabloon** (sap-2-laag-gebruiker-installatiekopie)][sap-templates-2-tier-user-image]

  toocreate een systeem met twee lagen met behulp van slechts één virtuele machine, gebruik deze sjabloon.
* [**Configuratie met drie lagen (meerdere virtuele machines) sjabloon** (sap-3-tier-gebruiker-installatiekopie)][sap-templates-3-tier-user-image]

  toocreate een systeem met drie lagen met meerdere virtuele machines of uw eigen installatiekopie van het besturingssysteem deze sjabloon gebruiken.

Voer in hello Azure-portal, Hallo parameters voor de sjabloon hello te volgen:

1. **Basisprincipes**:
  * **Abonnement**: Hallo abonnement toouse toodeploy Hallo sjabloon.
  * **Resourcegroep**: Hallo resource groep toouse toodeploy Hallo-sjabloon. U kunt een nieuwe resourcegroep maken of een bestaande resourcegroep selecteren in het Hallo-abonnement.
  * **Locatie**: waar toodeploy Hallo sjabloon. Als u een bestaande resourcegroep hebt geselecteerd, wordt Hallo-locatie van die resourcegroep gebruikt.
2. **Instellingen**:
  * **ID van het systeem SAP**: Hallo SAP-systeem-ID.
  * **Type besturingssysteem**: Hallo van het besturingssysteemtype u wilt dat toodeploy (Windows of Linux).
  * **Grootte van het SAP**: Hallo grootte van Hallo SAP-systeem.

    aantal nieuwe systeem voor SAP's Hallo Hallo biedt. Als u niet zeker hoeveel SAP's Hallo systeem vereist is weet, vraagt u uw SAP-technologie Partner of System Integrator.
  * **Beschikbaarheid van het systeem** (alleen drie lagen-sjabloon): Hallo beschikbaarheid van het systeem.

    Selecteer **HA** voor een configuratie die geschikt is voor de installatie van een hoge beschikbaarheid. Twee databaseservers en twee servers voor ASC's worden gemaakt.
  * **Opslagtype** (alleen twee lagen-sjabloon): type opslag toouse Hallo.

    Voor grotere systemen ten zeerste aangeraden Azure Premium-opslag. Zie voor meer informatie over opslagtypen Hallo resources te volgen:
      * [Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] in [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]
      * [Premium-opslag: Krachtige opslag voor workloads van de virtuele machine van Azure][storage-premium-storage-preview-portal]
      * [Inleiding tooMicrosoft Azure Storage][storage-introduction]
  * **Gebruikersinstallatiekopie VHD-URI**: de URI van persoonlijke besturingssysteemkopie Hallo VHD, bijvoorbeeld https:// Hallo&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Opslag van de gebruikersaccount installatiekopie**: Hallo-naam van Hallo storage-account waarin Hallo persoonlijke OS-installatiekopie is opgeslagen, bijvoorbeeld &lt;accountname > in https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Gebruikersnaam van de beheerder** en **beheerderswachtwoord**: Hallo gebruikersnaam en wachtwoord.

    Een nieuwe gebruiker is gemaakt voor het aanmelden toohello virtuele machine.
  * **Nieuwe of bestaande subnet**: bepaalt of een nieuw virtueel netwerk en subnet wordt gemaakt of een bestaand subnet wordt gebruikt. Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.
  * **Subnet-ID**: Hallo-ID van Hallo subnet toowhich Hallo virtuele machines verbinding maken. Selecteer subnet Hallo van uw VPN- of ExpressRoute virtueel netwerk toouse tooconnect Hallo virtuele machine tooyour on-premises netwerk. Hallo-ID ziet er meestal als volgt uit:

    /Subscriptions/&lt;abonnements-id > /resourceGroups/&lt;Resourcegroepnaam > /providers/Microsoft.Network/virtualNetworks/&lt;virtuele-netwerknaam > /subnets/&lt;subnetnaam >

3. **Voorwaarden en bepalingen**:  
    Lees en accepteer de juridische voorwaarden Hallo.

4.  Selecteer **aankoop**.

#### <a name="install-hello-vm-agent-linux-only"></a>Hallo VM-Agent (alleen voor Linux) installeren
toouse hello sjablonen wordt beschreven in voorgaande sectie Hallo Hallo die Linux-Agent moet al zijn geïnstalleerd in de gebruikersinstallatiekopie Hallo of Hallo implementatie mislukt. Download en installeer Hallo VM-Agent in Hallo gebruikersinstallatiekopie zoals beschreven in [downloaden, installeren en inschakelen van hello Azure VM-Agent][deployment-guide-4.4]. Als u geen Hallo sjablonen gebruikt, kunt u ook later Hallo VM-Agent installeren.

#### <a name="join-a-domain-windows-only"></a>Lid worden van een domein (alleen Windows)
Als uw Azure-implementatie verbonden tooan lokale Active Directory- of DNS-exemplaar is via een Azure site-naar-site VPN-verbinding of Azure ExpressRoute (dit heet *cross-premises* in [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide]), wordt verwacht dat Hallo VM lid wordt van een lokaal domein. Zie voor meer informatie over overwegingen voor deze stap [toevoegen aan een VM tooan lokale domein (alleen Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Proxy-instellingen configureren
Afhankelijk van hoe uw on-premises netwerk is geconfigureerd, moet u mogelijk tooset up Hallo proxy op de virtuele machine. Als uw VM verbonden tooyour on-premises netwerk via VPN- of ExpressRoute is, Hallo VM mogelijk niet worden kunnen tooaccess Hallo Internet, en won't kunnen toodownload Hallo vereist extensies of bewakingsgegevens verzamelen. Zie voor meer informatie [Hallo proxy configureren][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Bewaking configureren
controleren of uw omgeving ondersteunt SAP, hello Azure extensie Monitoring voor SAP ingesteld zoals beschreven toobe [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5]. Hallo-vereisten voor SAP controle en de vereiste minimale versie van SAP Kernel en SAP-Agent Host in Hallo bronnen in [SAP resources][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Bewaking van selectievakje
Controleer of bewaking werkt, zoals beschreven in [controles en het oplossen van problemen voor het instellen van het end-to-end bewaking][deployment-guide-troubleshooting-chapter].




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Het verplaatsen van een lokale virtuele machine met behulp van een VHD Azure niet gegeneraliseerd met SAP
In dit scenario plant u een specifiek SAP-systeem van een lokale omgeving tooAzure toomove. U kunt dit doen door Hallo VHD die Hallo OS Hallo SAP binaire bestanden is, uploaden en uiteindelijk Hallo DBMS binaire bestanden, plus Hallo VHD's met Hallo gegevens en logboekbestanden Hallo DBMS, tooAzure. In tegenstelling tot Hallo scenario wordt beschreven in [Scenario 2: een virtuele machine met een aangepaste installatiekopie implementeren voor SAP][deployment-guide-3.3], in dit geval blijven Hallo hostnaam, SAP-SID en SAP gebruikersaccounts in hello Azure VM, omdat ze zijn geconfigureerd in Hallo on-premises omgeving. U hoeft niet toogeneralize Hallo OS. Dit scenario geldt meestal toocross-premises scenario's waarbij deel uit van Hallo SAP liggend lokaal wordt uitgevoerd en deel ervan wordt uitgevoerd op Azure.

In dit scenario Hallo VM-Agent wordt niet automatisch geïnstalleerd tijdens de implementatie. Omdat Hallo VM-Agent en Hallo Azure verbeterde extensie Monitoring voor SAP voor toorun SAP vereist, moet u toodownload, installeren en schakelt u beide onderdelen handmatig nadat u Hallo virtuele machine hebt gemaakt.

Zie voor meer informatie over hello Azure VM-Agent Hallo resources te volgen.

[comment]: <> (Onderstaande MSSedusch TODO Update Windows-koppeling)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/Archive/2014/02/17/bginfo-Guest-agent-Extension-for-Azure-VMS.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Gebruikershandleiding voor Azure Linux-Agent][virtual-machines-linux-agent-user-guide]
>
>

- - -

Hallo volgende stroomdiagram ziet Hallo-volgorde van de stappen voor het verplaatsen van een lokale virtuele machine met behulp van een Azure niet gegeneraliseerd VHD:

![Stroomdiagram van VM-implementatie voor SAP-systemen met behulp van een VM-schijf][deployment-guide-figure-400]

Ervan uitgaande dat hello schijf is al geüpload en gedefinieerd in Azure (Zie [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide]), doen Hallo taken hieronder wordt beschreven in Hallo enkele secties.

#### <a name="create-a-virtual-machine"></a>Een virtuele machine maken
toocreate een implementatie met behulp van een persoonlijke besturingssysteemschijf via hello Azure-portal Hallo SAP-sjabloon is gepubliceerd in hello gebruiken [GitHub-opslagplaats voor azure-snelstartsjablonen][azure-quickstart-templates-github]. U kunt ook handmatig maken een virtuele machine, met behulp van PowerShell.

* [**Met twee lagen (slechts één virtuele machine) configuratiesjabloon** (sap-2-laag-gebruiker-disk)][sap-templates-2-tier-os-disk]

  toocreate een systeem met twee lagen met behulp van slechts één virtuele machine, gebruik deze sjabloon.

Voer in hello Azure-portal, Hallo parameters voor de sjabloon hello te volgen:

1. **Basisprincipes**:
  * **Abonnement**: Hallo abonnement toouse toodeploy Hallo sjabloon.
  * **Resourcegroep**: Hallo resource groep toouse toodeploy Hallo-sjabloon. U kunt een nieuwe resourcegroep maken of een bestaande resourcegroep selecteren in het Hallo-abonnement.
  * **Locatie**: waar toodeploy Hallo sjabloon. Als u een bestaande resourcegroep hebt geselecteerd, wordt Hallo-locatie van die resourcegroep gebruikt.
2. **Instellingen**:
  * **ID van het systeem SAP**: Hallo SAP-systeem-ID.
  * **Type besturingssysteem**: Hallo van het besturingssysteemtype u wilt dat toodeploy (Windows of Linux).
  * **Grootte van het SAP**: Hallo grootte van Hallo SAP-systeem.

    aantal nieuwe systeem voor SAP's Hallo Hallo biedt. Als u niet zeker hoeveel SAP's Hallo systeem vereist is weet, vraagt u uw SAP-technologie Partner of System Integrator.
  * **Opslagtype** (alleen twee lagen-sjabloon): type opslag toouse Hallo.

    Voor grotere systemen ten zeerste aangeraden Azure Premium-opslag. Zie voor meer informatie over opslagtypen Hallo resources te volgen:
      * [Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] in [Azure virtuele Machine DBMS-implementatie voor SAP op Linux][dbms-guide]
      * [Premium-opslag: Krachtige opslag voor Azure Virtual Machine-werkbelasting][storage-premium-storage-preview-portal]
      * [Inleiding tooMicrosoft Azure Storage][storage-introduction]
  * **VHD-URI op besturingssysteemschijf**: de URI van Hallo persoonlijke besturingssysteemschijf, bijvoorbeeld https:// Hallo&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Nieuwe of bestaande subnet**: bepaalt of een nieuw virtueel netwerk en subnet worden gemaakt of een bestaand subnet wordt gebruikt. Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.
  * **Subnet-ID**: Hallo-ID van Hallo subnet toowhich Hallo virtuele machines verbinding maken. Selecteer subnet Hallo van uw VPN- of Azure ExpressRoute virtueel netwerk toouse tooconnect Hallo virtuele machine tooyour on-premises netwerk. Hallo-ID ziet er meestal als volgt uit:

    /Subscriptions/&lt;abonnements-id > /resourceGroups/&lt;Resourcegroepnaam > /providers/Microsoft.Network/virtualNetworks/&lt;virtuele-netwerknaam > /subnets/&lt;subnetnaam >

3. **Voorwaarden en bepalingen**:  
    Lees en accepteer de juridische voorwaarden Hallo.

4.  Selecteer **aankoop**.

#### <a name="install-hello-vm-agent"></a>Hallo VM-Agent installeren
toouse hello sjablonen die zijn beschreven in voorgaande sectie hello, hello VM-Agent moet worden geïnstalleerd op Hallo OS-schijf of Hallo implementatie mislukt. Download en installeer Hallo VM-Agent in Hallo VM, zoals beschreven in [downloaden, installeren en inschakelen van hello Azure VM-Agent][deployment-guide-4.4].

Als u niet beschreven in voorgaande sectie Hallo Hallo-sjablonen gebruikt, kunt u Hallo VM-Agent ook later installeren.

#### <a name="join-a-domain-windows-only"></a>Lid worden van een domein (alleen Windows)
Als uw Azure-implementatie verbonden tooan lokale Active Directory- of DNS-exemplaar is via een Azure site-naar-site VPN-verbinding of ExpressRoute (dit heet *cross-premises* in [Azure Virtual Machines plannen en de implementatie voor SAP op Linux][planning-guide]), wordt verwacht dat Hallo VM lid wordt van een lokaal domein. Zie voor meer informatie over overwegingen voor deze taak [toevoegen aan een VM tooan lokale domein (alleen Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Proxy-instellingen configureren
Afhankelijk van hoe uw on-premises netwerk is geconfigureerd, moet u mogelijk tooset up Hallo proxy op de virtuele machine. Als uw VM verbonden tooyour on-premises netwerk via VPN- of ExpressRoute is, Hallo VM mogelijk niet worden kunnen tooaccess Hallo Internet, en won't kunnen toodownload Hallo vereist extensies of bewakingsgegevens verzamelen. Zie voor meer informatie [Hallo proxy configureren][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Bewaking configureren
controleren of uw omgeving ondersteunt SAP, hello Azure extensie Monitoring voor SAP ingesteld zoals beschreven toobe [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5]. Hallo-vereisten voor SAP controle en de vereiste minimale versie van SAP Kernel en SAP-Agent Host in Hallo bronnen in [SAP resources][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Bewaking van selectievakje
Controleer of bewaking werkt, zoals beschreven in [controles en het oplossen van problemen voor het instellen van het end-to-end bewaking][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Hallo controleconfiguratie voor SAP bijwerken
Hallo SAP controleconfiguratie in een van de volgende scenario's Hallo bijwerken:
* Hallo gezamenlijke Microsoft/SAP-team breidt de Hallo bewakingsmogelijkheden en meer of minder items-aanvragen.
* Microsoft introduceert een nieuwe versie van Hallo onderliggende Azure-infrastructuur die zorgt voor Hallo bewakingsgegevens en hello Azure uitgebreide bewaking extensie voor SAP behoeften toobe toothose wijzigingen aangepast.
* U extra virtuele harde schijven tooyour Azure VM koppelen of te verwijderen van een VHD. In dit scenario bijwerken Hallo-verzameling van gegevens met betrekking tot opslag. U kunt de configuratie wijzigt door toevoegen of verwijderen van eindpunten of door het toewijzen van IP-adressen tooa VM heeft geen invloed op Hallo bewakingsconfiguratie.
* U wijzigen Hallo grootte van uw Azure VM, bijvoorbeeld van grootte A5 tooany andere VM-grootte.
* U toevoegen nieuwe netwerkinterfaces tooyour virtuele Azure-machine.

controle-instellingen, update Hallo infrastructuur bewaking door de volgende Hallo tooupdate stappen in [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Gedetailleerde taken voor SAP software-implementatie op een virtuele machine van Windows
In deze sectie bevat gedetailleerde stappen voor het uitvoeren van specifieke taken in de configuratie en implementatie proces Hallo.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell-cmdlets implementeren
1.  Ga te[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).
2.  Onder **opdrachtregelprogramma's**onder **PowerShell**, selecteer **Windows installeren**.
3.  Hallo Microsoft Download Manager in het dialoogvenster voor Hallo gedownload bestand (bijvoorbeeld WindowsAzurePowershellGet.3f.3f.3fnew.exe), selecteer **uitvoeren**.
4.  toorun Microsoft Web Platform Installer (Microsoft Web PI), selecteer **Ja**.
5.  Een pagina die lijkt erop dat deze wordt weergegeven:

  ![De installatiepagina voor Azure PowerShell-cmdlets][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecteer **installeren**, en accepteer de licentievoorwaarden voor Microsoft-Software Hallo.
7.  PowerShell is geïnstalleerd. Selecteer **voltooien** tooclose Hallo-installatiewizard.

Controleer regelmatig de voor updates toohello PowerShell-cmdlets die meestal maandelijks worden bijgewerkt. Hallo gemakkelijkste manier toocheck voor updates is toodo Hallo voorafgaand aan de installatiestappen up toohello installatiepagina weergegeven in stap 5. Hallo release datum- en release aantal Hallo-cmdlets zijn opgenomen op Hallo pagina wordt weergegeven in stap 5. Tenzij anders vermeld in SAP-notitie [1928533] of SAP-notitie [2015553], het is raadzaam dat u met Hallo meest recente versie van Azure PowerShell-cmdlets werkt.

toocheck hello versie van hello Azure PowerShell-cmdlets die zijn geïnstalleerd op uw computer, deze PowerShell-opdracht uitvoeren:
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
Hallo resultaat ziet er als volgt:

![Resultaat van controle van versie van Azure PowerShell-cmdlet][deployment-guide-figure-600]
<a name="figure-6"></a>

Als hello Azure cmdlet versie is geïnstalleerd op uw computer de huidige versie hello is, eerste pagina van de installatiewizard Hallo Hallo aangeeft dat ze door toe te voegen **(geïnstalleerd)** toohello Producttitel (Zie de volgende schermafbeelding Hallo). Uw PowerShell Azure-cmdlets zijn bijgewerkt. tooclose hello installatiewizard selecteert **afsluiten**.

![De installatiepagina voor Azure PowerShell-cmdlets waarmee wordt aangegeven die Hallo meest recente versie van Azure PowerShell-cmdlets zijn geïnstalleerd][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI implementeren
1.  Ga te[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).
2.  Onder **opdrachtregelprogramma's**onder **Azure-opdrachtregelinterface**, selecteer Hallo **installeren** koppeling voor uw besturingssysteem.
3.  Hallo Microsoft Download Manager in het dialoogvenster voor Hallo gedownload bestand (bijvoorbeeld WindowsAzureXPlatCLI.3f.3f.3fnew.exe), selecteer **uitvoeren**.
4.  toorun Microsoft Web Platform Installer (Microsoft Web PI), selecteer **Ja**.
5.  Een pagina die lijkt erop dat deze wordt weergegeven:

  ![De installatiepagina voor Azure PowerShell-cmdlets][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecteer **installeren**, en accepteer de licentievoorwaarden voor Microsoft-Software Hallo.
7.  Azure CLI is geïnstalleerd. Selecteer **voltooien** tooclose Hallo-installatiewizard.

Controleer regelmatig de voor updates tooAzure CLI, die meestal maandelijks wordt bijgewerkt. Hallo gemakkelijkste manier toocheck voor updates is toodo Hallo voorafgaand aan de installatiestappen up toohello installatiepagina weergegeven in stap 5.


toocheck hello versie van Azure CLI die is geïnstalleerd op uw computer, wordt deze opdracht uitvoeren:
```
azure --version
```

Hallo resultaat ziet er als volgt:

![Resultaat van controle van versie van Azure CLI][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Lid worden van een VM tooan lokale domein (alleen Windows)
Als u virtuele machines SAP in een cross-premises-scenario implementeert, wordt waarin lokale Active Directory en DNS zijn uitgebreid in Azure, verwacht dat Hallo VM's zijn worden gebruikt voor het lidmaatschap van een lokaal domein. gedetailleerde stappen toojoin een VM tooan lokale domein Hallo en hello extra software nodig toobe lid is van een lokale domein, hangt af van de klant. Meestal toojoin een VM-tooan lokale domein, moet u tooinstall aanvullende software zoals antimalware-software en back-up of controle-software.

In dit scenario moet u ook toomake ervoor dat als InternetProxy-instellingen worden afgedwongen wanneer een virtuele machine lid van een domein in uw omgeving, Hallo Hallo Windows lokale systeemaccount (S-1-5-18) in Hallo Gast-VM heeft dezelfde proxy-instellingen. de eenvoudigste optie Hallo is tooforce Hallo proxy met behulp van Groepsbeleid, die van toepassing toosystems in Hallo domein is van een domein.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Downloaden, installeren en inschakelen van hello Azure VM-Agent
Voor virtuele machines die vanuit een installatiekopie van het besturingssysteem die niet is gegeneraliseerd (bijvoorbeeld een afbeelding die niet afkomstig zijn uit Hallo Windows System Preparation of sysprep, hulpprogramma) worden geïmplementeerd, moet u toomanually downloaden, installeren en inschakelen hello Azure VM-Agent.

Als u een virtuele machine uit Azure Marketplace Hallo implementeert, is deze stap niet vereist. Installatiekopieën van hello Azure Marketplace al hello Azure VM-Agent.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Hello Azure VM-Agent downloaden:
  1.  Hallo downloaden [Azure VM-Agent-installatiepakket](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Hallo VM-Agent-MSI-pakket lokaal opslaan op een pc of de server.
2.  Hello Azure VM-Agent installeren:
  1.  Verbinding maken met toohello Azure VM geïmplementeerd met behulp van Remote Desktop Protocol (RDP).
  2.  Open een venster van Windows Verkenner op Hallo VM en selecteer Hallo doelmap voor de MSI-bestand Hallo Hallo VM-Agent.
  3.  Sleep hello Azure VM-Agent-installatieprogramma MSI-bestand van uw lokale computer of de server toohello doelmap Hallo VM-Agent op Hallo VM.
  4.  Dubbelklik op Hallo MSI-bestand op Hallo VM.
3.  Voor virtuele machines die gekoppeld tooon-premises domeinen zijn, zorg ervoor dat eventuele InternetProxy-instellingen ook van toepassing toohello Windows lokale systeemaccount (S-1-5-18) in Hallo VM, zoals beschreven in [Hallo proxy configureren] [ deployment-guide-configure-proxy]. Hallo VM-Agent wordt uitgevoerd in deze context en moet toobe kunnen tooconnect tooAzure.

Er geen gebruikersinteractie is vereist tooupdate hello Azure VM-Agent. Hallo VM-Agent wordt automatisch bijgewerkt en vereist geen virtuele machine opnieuw opstarten.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Gebruik Hallo deze opdrachten tooinstall Hallo VM-Agent voor Linux:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

Als het Hallo-agent al is geïnstalleerd, tooupdate hello Azure Linux Agent in beschreven stappen Hallo [Update hello Azure Linux Agent op een VM toohello meest recente versie van GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Hallo proxy configureren
Hallo u stappen tooconfigure Hallo proxy in Windows ondernemen zijn anders dan Hallo manier u Hallo proxy in Linux configureert.

#### <a name="windows"></a>Windows
Proxy-instellingen moeten correct worden ingesteld voor Hallo lokale systeemaccount tooaccess Hallo Internet. Als de proxy-instellingen niet zijn ingesteld door Groepsbeleid, kunt u Hallo-instellingen voor Hallo lokale systeemaccount configureren.

1. Ga te**Start**, voer **gpedit.msc**, en selecteer vervolgens **Enter**.
2. Selecteer **Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen** > **Internet Explorer**. Zorg ervoor dat deze instelling Hallo **proxy maken instellingen per computer (in plaats per gebruiker)** is uitgeschakeld of niet is geconfigureerd.
3. In **Configuratiescherm**, gaat u te**Netwerkcentrum** > **Internetopties**.
4. Op Hallo **verbindingen** tabblad, selecteer Hallo **LAN-instellingen** knop.
5. Schakel Hallo **-instellingen automatisch detecteren** selectievakje.
6. Selecteer Hallo **een proxyserver gebruiken voor uw LAN** selectievakje en voer vervolgens Hallo proxy-adres en poort.
7. Selecteer Hallo **Geavanceerd** knop.
8. In Hallo **uitzonderingen** Voer Hallo IP-adres **168.63.129.16**. Selecteer **OK**.


#### <a name="linux"></a>Linux
Hallo juiste proxy configureren in het configuratiebestand Hallo Hallo Microsoft Azure Guest-Agent, dat zich op \\enzovoort\\waagent.conf.

Hallo volgende parameters instellen:

1.  **HTTP-proxyhost**. Bijvoorbeeld, te ingesteld**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **HTTP-proxypoort**. Bijvoorbeeld, te ingesteld**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Hallo-agent opnieuw opstarten

  ```
  sudo service waagent restart
  ```

proxy-instellingen in Hallo \\enzovoort\\waagent.conf toohello vereiste VM-extensies ook van toepassing. Als u wilt dat toouse Hallo Azure-opslagplaatsen, zorg ervoor dat Hallo verkeer toothese opslagplaatsen niet wordt verzonden via het lokale intranet. Als u hebt gemaakt gebruiker gedefinieerde routes tooenable geforceerde tunneling, zorg ervoor dat u een route die verkeer toohello opslagplaatsen van routes toevoegen rechtstreeks toohello Internet, en niet via uw site-naar-site VPN-verbinding.

* **SLES**

  U moet ook tooadd routes voor Hallo IP-adressen die worden vermeld \\enzovoort\\regionserverclnt.cfg. Hallo toont volgende afbeelding een voorbeeld:

  ![Geforceerde tunneling][deployment-guide-figure-50]


* **RHEL**

  U moet ook tooadd routes voor Hallo IP-adressen van hosts Hallo vermeld in \\enzovoort\\yum.repos.d\\rhui netwerktaakverdelers. Zie voor een voorbeeld Hallo voorgaande afbeelding.

Zie voor meer informatie over de gebruiker gedefinieerde routes [gebruiker gedefinieerde routes en doorsturen via IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Hello Azure verbeterde extensie Monitoring voor SAP configureren
Wanneer u Hallo VM hebt voorbereid, zoals beschreven in [implementatiescenario's van virtuele machines voor SAP op Azure][deployment-guide-3], hello Azure VM-Agent is geïnstalleerd op Hallo virtuele machine. de volgende stap Hallo is toodeploy hello Azure verbeterde extensie Monitoring voor SAP, die beschikbaar in hello Azure-opslagplaats voor uitbreiding in Hallo globale Azure-datacenters is. Zie voor meer informatie [Azure Virtual Machines planning en implementatie voor SAP op Linux][planning-guide-9.1].

U kunt gebruik PowerShell of Azure CLI tooinstall en hello Azure verbeterde extensie Monitoring voor SAP configureren. Zie tooinstall Hallo-extensie op een Windows- of Linux-VM met behulp van een Windows-computer [Azure PowerShell][deployment-guide-4.5.1]. Zie tooinstall Hallo-extensie op een Linux-VM met behulp van een bureaublad Linux [Azure CLI][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell voor Linux en Windows-VM 's
tooinstall hello Azure verbeterde extensie Monitoring voor SAP met behulp van PowerShell:

1. Zorg ervoor dat u de meest recente versie van Azure PowerShell-cmdlet Hallo Hallo hebt geïnstalleerd. Zie voor meer informatie [implementeren van Azure PowerShell-cmdlets][deployment-guide-4.1].  
2. Hallo volgende PowerShell-cmdlet uitvoeren.
  Voor een lijst met beschikbare omgevingen, voert u `commandlet Get-AzureRmEnvironment`. Als u wilt dat toouse openbare Azure, uw omgeving is **AzureCloud**. Selecteer voor Azure China **AzureChinaCloud**.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

Nadat u de accountgegevens van uw invoeren en hello Azure virtuele machine te identificeren, wordt Hallo script Hallo vereist extensies implementeert en maakt Hallo vereist functies. Dit kan enkele minuten duren.
Voor meer informatie over `Set-AzureRmVMAEMExtension`, Zie [Set AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![Voltooiing van uitvoering van SAP-specifieke Azure-cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Hallo `Set-AzureRmVMAEMExtension` configuratie biedt alle Hallo stappen tooconfigure host bewaking voor SAP.

Hallo-scriptuitvoer bevat Hallo volgende informatie:

* Bevestiging die bewaking voor Hallo base VHD (met Hallo OS) en alle aanvullende VHD's gekoppelde toohello die VM is geconfigureerd.
* de volgende twee berichten Hallo Bevestig Hallo configuratie van Storage metrische gegevens voor een specifieke storage-account.
* Een line-of-uitvoer geeft Hallo-status van de werkelijke update Hallo van Hallo controleconfiguratie.
* Een andere line-of-uitvoer wordt bevestigd dat Hallo de configuratie zijn geïmplementeerd of bijgewerkt.
* Hallo laatste regel van uitvoer is informatief. Uw opties voor het testen Hallo controleconfiguratie weergeven

toocheck dat alle stappen van de Azure-uitgebreide bewaking met succes zijn uitgevoerd en die hello Azure-infrastructuur Hallo gegevens die nodig zijn biedt, doorgaan met de gereedheidscontrole Hallo voor hello Azure verbeterde extensie Monitoring voor SAP, zoals beschreven in [Gereedheidscontrole voor Azure-uitgebreide bewaking voor SAP][deployment-guide-5.1]. Wacht 15-30 minuten tot Azure Diagnostics toocollect Hallo relevante gegevens.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI voor virtuele Linux-machines
tooinstall hello Azure verbeterde extensie Monitoring voor SAP met Azure CLI:

1. Azure CLI installeren zoals is beschreven in [installeren hello Azure CLI][azure-cli].
2. Aanmelden met uw Azure-account:

  ```
  azure login
  ```

3. De modus Resource Manager tooAzure switch:

  ```
  azure config mode arm
  ```

4. Azure uitgebreide bewaking inschakelen:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Controleer of dat Hallo-extensie voor Azure verbeterde Monitoring op Hallo Azure Linux VM actief is. Controleer of bestand Hallo \\var\\lib\\AzureEnhancedMonitor\\PerfCounters bestaat. Voer deze opdracht toodisplay gegevens worden verzameld door hello Azure verbeterde Monitor indien aanwezig, bij een opdrachtprompt:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

Hallo-uitvoer ziet er als volgt:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Controles en het oplossen van problemen voor het bewaken van end-to-end
Nadat u hebt uw Azure-virtuele machine wordt geïmplementeerd en Hallo relevante Azure bewakingsinfrastructuur instellen, moet u controleren of alle onderdelen van Hallo Hallo extensie voor Azure verbeterde Monitoring werkt zoals verwacht.

Controle op Hallo gereedheid voor hello Azure verbeterde extensie Monitoring voor SAP uitvoeren, zoals beschreven in [gereedheidscontrole voor hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-5.1]. Als alle resultaten van de gereedheid van positieve en alle relevante prestatiemeteritems weergegeven OK, Azure bewaking is ingesteld. U kunt doorgaan met installatie van de Hallo van SAP Host Agent dat wordt beschreven in de opmerkingen bij de Hallo SAP in [SAP resources][deployment-guide-2.2]. Als de gereedheidscontrole Hallo aangeeft dat prestatiemeteritems ontbreken zijn, Hallo Statuscontrole voor hello Azure bewakingsinfrastructuur uitvoeren, zoals beschreven in [Statuscontrole voor Azure infrastructuur controleconfiguratie] [ deployment-guide-5.2]. Zie voor meer opties voor probleemoplossing, [probleemoplossing voor Azure-bewaking voor SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Gereedheidscontrole voor hello Azure verbeterde extensie Monitoring voor SAP
Deze controle zorgt ervoor dat alle maatstaven voor prestaties die worden gebruikt in uw toepassing SAP worden geleverd door Hallo onderliggende Azure-infrastructuur bewaken.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Hallo-gereedheidscontrole op een virtuele machine van Windows worden uitgevoerd

1.  Meld u aan de virtuele machine van Azure toohello (met behulp van een beheerdersaccount is niet nodig).
2.  Open een opdrachtpromptvenster.
3.  Bij de opdrachtprompt Hallo Hallo directory toohello-installatiemap van hello Azure verbeterde extensie Monitoring voor SAP wijzigen: C:\\pakketten\\Plugins\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versie >\\verwijderen

  Hallo *versie* in Hallo pad toohello extensie bewaking kan variëren. Als u mappen voor meerdere versies van Hallo bewaking van de extensie in de installatiemap hello, Controleer de configuratie van de Hallo Hallo AzureEnhancedMonitoring Windows-service, bekijken en vervolgens switch toohello map als aangegeven *pad tooexecutable* .

  ![Eigenschappen van de service wordt uitgevoerd hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-figure-1000]

4.  Bij de opdrachtprompt Hallo uitvoeren **azperflib.exe** zonder parameters.

  > [!NOTE]
  > Azperflib.exe wordt uitgevoerd in een lus en updates Hallo verzameld tellers elke 60 seconden. tooend hello lus sluiten Hallo-opdrachtpromptvenster.
  >
  >

Als het Hallo-extensie voor Azure verbeterde Monitoring is niet geïnstalleerd of Hallo AzureEnhancedMonitoring service niet wordt uitgevoerd, is Hallo-extensie niet goed geconfigureerd. Zie voor gedetailleerde informatie over hoe toodeploy extensie Hallo [probleemoplossing hello Azure bewakingsinfrastructuur voor SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Hallo-uitvoer van azperflib.exe controleren
Azperflib.exe uitvoer toont dat alle Azure-prestatiemeteritems voor SAP ingevuld. Hallo onderaan Hallo lijst met items die worden verzameld in een indicator samenvatting en health weergeven Hallo status van de Azure-bewaking

![Uitvoer van de statuscontrole van de door het uitvoeren van azperflib.exe waarmee wordt aangegeven dat er geen problemen aanwezig][deployment-guide-figure-1100]
<a name="figure-11"></a>

Controleer Hallo resultaat geretourneerd voor Hallo **tellers totaal** uitvoer, die wordt gerapporteerd als leeg en voor **gezondheidsstatus**, weergegeven in de voorgaande afbeelding Hallo.

Interpreteren Hallo resulterende waarden als volgt:

| Waarden van Azperflib.exe | Azure health-status controleren |
| --- | --- |
| **API-aanroepen - niet beschikbaar** | Items die niet beschikbaar zijn mogelijk de configuratie van de virtuele machine niet van toepassing toohello, of zijn fouten opgetreden. Zie **gezondheidsstatus**. |
| **Prestatiemeteritems van de totale - leeg** |Hallo na twee prestatiemeteritems van Azure-opslag kan niet leeg zijn: <ul><li>Opslag Op latentie lezen Server msec</li><li>Opslag Op latentie lezen E2E msec</li></ul>Alle andere items moeten waarden hebben. |
| **Health-status** |Alleen OK als retourneren status bevat **OK**. |
| **Diagnostics** |Gedetailleerde informatie over de status. |

Als hello **gezondheidsstatus** -waarde is niet **OK**, volg de instructies in Hallo [Statuscontrole voor Azure infrastructuur controleconfiguratie] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>De Gereedheidscontrole uitvoeren Hallo op een Linux-VM

1.  Verbinding toohello Azure virtuele Machine via SSH.

2.  Hallo-uitvoer van de extensie voor Azure verbeterde Monitoring Hallo controleren.

  a.  Voer `more /var/lib/AzureEnhancedMonitor/PerfCounters` uit.

   **Resultaat verwacht**: lijst met prestatiemeteritems retourneert. Hallo-bestand mag niet leeg zijn.

 b. Voer `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` uit.

   **Resultaat verwacht**: retourneert één regel waar Hallo fout **geen**, bijvoorbeeld **3; config; Fout; 0; 0; geen; 0; 1456416792; tst-servercs;**

  c. Voer `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` uit.

    **Resultaat verwacht**: retourneert als leeg of bestaat niet.

Als hello voorgaande selectievakje niet geslaagd is, voert u deze extra controles:

1.  Zorg ervoor dat waagent Hallo is geïnstalleerd en ingeschakeld.

  a.  Voer `sudo ls -al /var/lib/waagent/` uit.

      **Resultaat verwacht**: Hallo inhoud van het Hallo waagent directory bevat.

  b.  Voer `ps -ax | grep waagent` uit.

   **Resultaat verwacht**: één vermelding strekking weergegeven:`python /usr/sbin/waagent -daemon`

2. Zorg ervoor dat Hallo diagnostische Linux-uitbreiding is geïnstalleerd en ingeschakeld.

  a.  Voer `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` uit.

   **Resultaat verwacht**: Hallo inhoud van het Hallo Linux diagnostische map_uitbreiding bevat.

 b. Voer `ps -ax | grep diagnostic` uit.

   **Resultaat verwacht**: één vermelding strekking weergegeven:`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   Zorg ervoor dat hello Azure uitgebreide bewaking uitbreiding is geïnstalleerd en wordt uitgevoerd.

  a.  Voer `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` uit.

    **Resultaat verwacht**: geeft een lijst van Hallo inhoud van het Hallo-extensie voor Azure verbeterde Monitoring-directory.

  b. Voer `ps -ax | grep AzureEnhanced` uit.

     **Resultaat verwacht**: één vermelding strekking weergegeven:`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. SAP Host-Agent installeren zoals is beschreven in SAP-notitie [1031096], en controleer de uitvoer van Hallo `saposcol`.

  a.  Voer `/usr/sap/hostctrl/exe/saposcol -d` uit.

  b.  Voer `dump ccm` uit.

  c.  Controleer of Hallo **Virtualization_Configuration\Enhanced bewaking toegang** meetwaarde is **true**.

Als u al een SAP NetWeaver ABAP application server geïnstalleerd hebt, transactie ST06 openen en controleer of de uitgebreide bewaking is ingeschakeld.

Als een van deze controles mislukken, en Zie voor gedetailleerde informatie over hoe tooredeploy extensie Hallo [probleemoplossing hello Azure bewakingsinfrastructuur voor SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Serverstatus controleren voor hello Azure infrastructuur controleconfiguratie
Als sommige Hallo bewakingsgegevens niet correct zoals aangegeven door bezorgd Hallo test beschreven in [gereedheidscontrole voor Azure-uitgebreide bewaking voor SAP][deployment-guide-5.1], voert hello `Test-AzureRmVMAEMExtension` cmdlet toocheck Hiermee wordt aangegeven of hello Azure-infrastructuur en controle-extensie voor SAP Hallo bewaking correct zijn geconfigureerd.

1.  Zorg ervoor dat u de nieuwste versie Hallo van hello Azure PowerShell-cmdlet hebt geïnstalleerd, zoals beschreven in [implementeren van Azure PowerShell-cmdlets][deployment-guide-4.1].
2.  Hallo volgende PowerShell-cmdlet uitvoeren. Voor een lijst van beschikbare omgevingen Hallo cmdlet uitvoeren `Get-AzureRmEnvironment`. openbare Azure, selecteer toouse hello **AzureCloud** omgeving. Selecteer voor Azure China **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Voer de gegevens van uw account en identificeren hello Azure virtuele machine.

  ![Invoer pagina van de SAP-specifieke Azure cmdlet Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. Hallo script tests Hallo configuratie van Hallo virtuele machine die u selecteert.

  ![Uitvoer van een geslaagde test Hallo Azure bewakingsinfrastructuur voor SAP][deployment-guide-figure-1300]

Zorg ervoor dat elke status resultaat **OK**. Als u een aantal controles worden niet weergegeven **OK**, Hallo update cmdlet uitvoeren, zoals beschreven in [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5]. Wacht 15 minuten en herhaaldelijk Hallo controles wordt beschreven in [gereedheidscontrole voor Azure-uitgebreide bewaking voor SAP] [ deployment-guide-5.1] en [Statuscontrole voor Azure-infrastructuur configuratie van de bewaking] [deployment-guide-5.2]. Als Hallo controles nog steeds een probleem met enkele of alle items blijkt, Zie [probleemoplossing hello Azure bewakingsinfrastructuur voor SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Hello Azure bewakingsinfrastructuur voor probleemoplossing voor SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Azure prestatiemeteritems worden niet weergegeven op alle
Hallo AzureEnhancedMonitoring Windows-service verzamelt maatstaven voor prestaties in Azure. Als het Hallo-service is niet juist geïnstalleerd of als deze niet wordt uitgevoerd in uw virtuele machine, kunnen geen prestatiegegevens worden verzameld.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>Hallo-installatiemap van hello Azure uitgebreide bewaking uitbreiding is leeg

###### <a name="issue"></a>Probleem
Hallo-installatiemap C:\\pakketten\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versie >\\vervolgkeuzelijst is leeg.

###### <a name="solution"></a>Oplossing
Hallo-extensie is niet geïnstalleerd. Bepalen of dit een probleem met de proxy (zoals eerder beschreven). Mogelijk moet u toorestart Hallo machine of Voer Hallo `Set-AzureRmVMAEMExtension` configuratiescript.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Service voor Azure-uitgebreide bewaking bestaat niet

###### <a name="issue"></a>Probleem
Hallo AzureEnhancedMonitoring Windows-service bestaat niet.

Azperflib.exe uitvoer is een fout genereert:

![De uitvoering van azperflib.exe geeft aan dat Hallo-service van het Hallo-extensie voor Azure verbeterde Monitoring voor SAP niet wordt uitgevoerd][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Oplossing
Als Hallo-service niet bestaat, heeft hello Azure verbeterde extensie Monitoring voor SAP niet goed is geïnstalleerd. Hallo-extensie implementeren met behulp van Hallo stappen beschreven voor het implementatiescenario in [implementatiescenario's van virtuele machines voor SAP in Azure][deployment-guide-3].

Nadat u Hallo-extensie geïmplementeerd na een uur, controleer opnieuw of hello Azure prestatiemeteritems u in hello Azure VM vindt.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Service voor Azure-uitgebreide bewaking bestaat, maar toostart is mislukt

###### <a name="issue"></a>Probleem
Hallo AzureEnhancedMonitoring Windows-service bestaat en is ingeschakeld, maar toostart is mislukt. Controleer de Hallo toepassingslogboek voor meer informatie.

###### <a name="solution"></a>Oplossing
Hallo-configuratie is onjuist. Hallo-extensie voor Hallo VM, bewaking starten zoals beschreven in [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Sommige Azure prestatiemeters ontbreken.
Hallo AzureEnhancedMonitoring Windows-service verzamelt maatstaven voor prestaties in Azure. Hallo-service ontvangt gegevens van diverse bronnen. Sommige configuratiegegevens lokaal worden verzameld en bepaalde maatstaven voor prestaties van Azure Diagnostics worden gelezen. Tellers voor opslag worden van uw abonnement Hallo-opslag-Logboeken gebruikt.

Als u problemen oplossen met behulp van SAP-notitie [1999351] niet los Hallo probleem moet Hallo opnieuw `Set-AzureRmVMAEMExtension` configuratiescript. U hebt mogelijk toowait uur omdat storage analytics of diagnostics items mogelijk niet worden gemaakt, onmiddellijk nadat ze zijn ingeschakeld. Als Hallo probleem zich blijft voordoen, opent u een bericht SAP klant ondersteuning op Hallo onderdeel BC-OP-NT-AZR voor Windows of BC-OP-LNX-AZR voor een virtuele Linux-machine.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Azure prestatiemeteritems worden niet weergegeven op alle
Maatstaven voor prestaties in Azure worden door een daemon verzameld. Als het Hallo-daemon niet wordt uitgevoerd, kunnen geen prestatiegegevens worden verzameld.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>Hallo-installatiemap van de extensie Azure verbeterde Monitoring Hallo is leeg

###### <a name="issue"></a>Probleem
Hallo directory \\var\\lib\\waagent\\ heeft geen submap voor Hallo extensie Azure verbeterde Monitoring.

###### <a name="solution"></a>Oplossing
Hallo-extensie is niet geïnstalleerd. Bepalen of dit een probleem met de proxy (zoals eerder beschreven). Mogelijk moet u toorestart Hallo apparaat en/of Voer Hallo `Set-AzureRmVMAEMExtension` configuratiescript.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Sommige Azure prestatiemeters ontbreken.
Maatstaven voor prestaties in Azure worden door een daemon die gegevens uit diverse bronnen ontvangt verzameld. Sommige configuratiegegevens lokaal worden verzameld en bepaalde maatstaven voor prestaties van Azure Diagnostics worden gelezen. Tellers voor opslag is afkomstig van Hallo Logboeken in uw opslagabonnement.

Zie voor een volledige en bijgewerkte lijst met bekende problemen, SAP-notitie [1999351], die extra informatie over probleemoplossing voor verbeterde Azure-bewaking voor SAP heeft.

Als u problemen oplossen met behulp van SAP-notitie [1999351] niet Hallo oplossen, opnieuw uitvoeren Hallo `Set-AzureRmVMAEMExtension` configuratiescript zoals beschreven in [configureren hello Azure verbeterde extensie Monitoring voor SAP][deployment-guide-4.5]. U wellicht toowait een uur omdat storage analytics of diagnostics items mogelijk niet worden gemaakt, onmiddellijk nadat ze zijn ingeschakeld. Als Hallo probleem zich blijft voordoen, opent u een bericht SAP klant ondersteuning op Hallo onderdeel BC-OP-NT-AZR voor Windows of BC-OP-LNX-AZR voor een virtuele Linux-machine.
