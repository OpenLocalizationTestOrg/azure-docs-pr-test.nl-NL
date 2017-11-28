---
title: hoge beschikbaarheid van de virtuele Machines voor SAP NetWeaver aaaAzure | Microsoft Docs
description: Hoge beschikbaarheid-handleiding voor SAP NetWeaver op Azure Virtual Machines
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="b930e-103">Hoge beschikbaarheid voor SAP NetWeaver op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="b930e-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="b930e-109">Virtuele Machines in Azure is Hallo-oplossing voor organisaties die berekenings-, opslag- en netwerkbronnen, in de minimale tijd en zonder langdurige inkoop cycli moeten.</span><span class="sxs-lookup"><span data-stu-id="b930e-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="b930e-110">U kunt Azure Virtual Machines toodeploy klassieke toepassingen zoals SAP NetWeaver gebaseerde ABAP, Java en een ABAP + Java-stack gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="b930e-111">Betrouwbaarheid en beschikbaarheid zonder dat extra on-premises resources uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="b930e-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="b930e-112">Virtuele Machines in Azure ondersteunt cross-premises connectiviteit, zodat u kunt Azure Virtual Machines integreren in uw organisatie lokale domeinen, privéclouds en SAP system Liggend.</span><span class="sxs-lookup"><span data-stu-id="b930e-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="b930e-113">In dit artikel wordt uitgelegd we Hallo stappen die u toodeploy SAP-systemen voor hoge beschikbaarheid in Azure ondernemen kunt met hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b930e-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b930e-114">We helpt u bij deze belangrijke taken:</span><span class="sxs-lookup"><span data-stu-id="b930e-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="b930e-115">Hallo zoeken rechts SAP-opmerkingen en installatie implementatiehandleidingen, die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie.</span><span class="sxs-lookup"><span data-stu-id="b930e-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="b930e-116">In dit artikel is een aanvulling op de documentatie voor SAP-installatie en SAP-opmerkingen, de primaire Hallo-bronnen waarmee u kunnen installeren en SAP software implementeren op specifieke platforms.</span><span class="sxs-lookup"><span data-stu-id="b930e-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="b930e-117">Meer informatie over Hallo verschillen tussen hello Azure Resource Manager-implementatiemodel en hello Azure klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b930e-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="b930e-118">Meer informatie over Windows Server Failover Clustering quorum-modi, zodat u Hallo model dat geschikt is voor uw Azure-implementatie kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="b930e-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="b930e-119">Meer informatie over Windows Server Failover Clustering gedeelde opslag in Azure-services.</span><span class="sxs-lookup"><span data-stu-id="b930e-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="b930e-120">Meer informatie over hoe de onderdelen van één punt van fout zoals geavanceerde Business Application Programming (ABAP) SAP centrale Services (ASC's) voor het beveiligen van toohelp / SAP centrale Services (SCS) en databasebeheersystemen (DBMS) en redundante componenten zoals SAP Toepassingsserver in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="b930e-121">Ga als volgt een voorbeeld van een stapsgewijze van een installatie en configuratie van een SAP-systeem voor hoge beschikbaarheid in een cluster met Windows Server Failover Clustering in Azure met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b930e-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="b930e-122">Meer informatie over extra stappen vereist toouse Windows Server Failover Clustering in Azure, maar die niet nodig zijn in een on-premises implementatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="b930e-123">toosimplify implementatie en configuratie in dit artikel gebruiken we Hallo SAP drie lagen hoge beschikbaarheid Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b930e-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="b930e-124">Hallo sjablonen automatisering van Hallo gehele infrastructuur die u nodig hebt voor een hoge beschikbaarheid SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="b930e-125">Hallo-infrastructuur ondersteunt ook het formaat van uw systeem SAP SAP toepassing prestaties Standard (SAP's).</span><span class="sxs-lookup"><span data-stu-id="b930e-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="b930e-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="b930e-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="b930e-127">Zorg voordat u begint, dat u voldoet aan de Hallo vereisten die worden beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="b930e-128">Wees ook zeker toocheck alle resources die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie.</span><span class="sxs-lookup"><span data-stu-id="b930e-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="b930e-129">In dit artikel gebruiken we Azure Resource Manager-sjablonen voor [drie lagen SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="b930e-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="b930e-130">Zie voor een handig overzicht van sjablonen [SAP Azure Resource Manager-sjablonen](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="b930e-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="b930e-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Resources</span><span class="sxs-lookup"><span data-stu-id="b930e-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="b930e-132">Deze artikelen omvatten SAP-implementaties in Azure:</span><span class="sxs-lookup"><span data-stu-id="b930e-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="b930e-133">[Azure virtuele Machines, planning en implementatie voor SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="b930e-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="b930e-134">[Azure virtuele Machines-implementatie voor SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="b930e-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="b930e-135">[Azure virtuele Machines DBMS-implementatie voor SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="b930e-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="b930e-136">[Azure virtuele Machines hoge beschikbaarheid voor SAP NetWeaver (deze handleiding)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="b930e-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-137">Waar mogelijk, geven wij u een koppeling toohello SAP installatiehandleiding verwijzen (Zie Hallo [SAP installatiehandleidingen][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="b930e-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="b930e-138">Voor vereisten en informatie over het Hallo-installatieproces, het een goed idee tooread Hallo SAP NetWeaver installatie zorgvuldig leidt.</span><span class="sxs-lookup"><span data-stu-id="b930e-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="b930e-139">Dit artikel behandelt alleen specifieke taken voor SAP NetWeaver-gebaseerde computers die u met Azure Virtual Machines gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="b930e-140">Deze opmerkingen SAP zijn verwante toohello onderwerp van SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="b930e-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="b930e-141">Het nummer</span><span class="sxs-lookup"><span data-stu-id="b930e-141">Note number</span></span> | <span data-ttu-id="b930e-142">Titel</span><span class="sxs-lookup"><span data-stu-id="b930e-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="b930e-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="b930e-143">[1928533]</span></span> |<span data-ttu-id="b930e-144">SAP-toepassingen in Azure: ondersteunde producten en schaling</span><span class="sxs-lookup"><span data-stu-id="b930e-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="b930e-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="b930e-145">[2015553]</span></span> |<span data-ttu-id="b930e-146">SAP op Microsoft Azure: ondersteuning voor vereisten</span><span class="sxs-lookup"><span data-stu-id="b930e-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="b930e-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="b930e-147">[1999351]</span></span> |<span data-ttu-id="b930e-148">Verbeterde Azure bewaking voor SAP</span><span class="sxs-lookup"><span data-stu-id="b930e-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="b930e-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="b930e-149">[2178632]</span></span> |<span data-ttu-id="b930e-150">Sleutel bewaking van metrische gegevens voor SAP op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b930e-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="b930e-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="b930e-151">[1999351]</span></span> |<span data-ttu-id="b930e-152">Virtualisatie in Windows: uitgebreide bewaking</span><span class="sxs-lookup"><span data-stu-id="b930e-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="b930e-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="b930e-153">[2243692]</span></span> |<span data-ttu-id="b930e-154">Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="b930e-155">Meer informatie over Hallo [beperkingen van de Azure-abonnementen][azure-subscription-service-limits-subscription], waaronder algemene standaardbeperkingen en maximale beperkingen.</span><span class="sxs-lookup"><span data-stu-id="b930e-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="b930e-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Hoge beschikbaarheid SAP met Azure Resource Manager versus hello Azure klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="b930e-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="b930e-157">Hello Azure Resource Manager en Azure klassieke implementatiemodel zijn verschillende in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="b930e-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="b930e-158">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="b930e-158">Resource groups</span></span>
- <span data-ttu-id="b930e-159">Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b930e-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="b930e-160">Ondersteuning voor SAP multi-SID-scenario 's</span><span class="sxs-lookup"><span data-stu-id="b930e-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="b930e-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="b930e-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="b930e-162">In Azure Resource Manager kunt u resource groepen toomanage alle Hallo toepassingsresources in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b930e-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="b930e-163">Een geïntegreerde benadering, in een resourcegroep van alle resources hebben Hallo dezelfde levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="b930e-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="b930e-164">Bijvoorbeeld, alle resources worden gemaakt op Hallo dezelfde tijd en ze worden verwijderd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="b930e-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="b930e-165">Meer informatie over [resourcegroepen](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="b930e-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="b930e-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b930e-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="b930e-167">Hello Azure klassieke implementatiemodel is er een afhankelijkheid tussen hello Azure interne load balancer (Azure Load Balancer-service) en groep Hallo cloud-service.</span><span class="sxs-lookup"><span data-stu-id="b930e-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="b930e-168">Elke interne load balancer moet één cloud service-groep.</span><span class="sxs-lookup"><span data-stu-id="b930e-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="b930e-169">In Azure Resource Manager, hoeft u niet een Azure resource group toouse Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="b930e-170">Hallo-omgeving is eenvoudiger en flexibeler.</span><span class="sxs-lookup"><span data-stu-id="b930e-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="b930e-171">Ondersteuning voor SAP multi-SID-scenario 's</span><span class="sxs-lookup"><span data-stu-id="b930e-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="b930e-172">In Azure Resource Manager kunt u meerdere SAP systeem-id (SID) ASC's / SCS exemplaren in één cluster installeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="b930e-173">Multi-SID-exemplaren zijn mogelijk vanwege ondersteuning voor meerdere IP-adressen voor elke Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="b930e-174">toouse hello Azure klassieke implementatiemodel, voert u de procedures op Hallo van [SAP NetWeaver in Azure: Clustering SAP ASC's / SCS exemplaren met behulp van Windows Server Failover Clustering in Azure met SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="b930e-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b930e-175">Het is raadzaam dat u hello Azure Resource Manager-implementatiemodel voor uw SAP-installaties.</span><span class="sxs-lookup"><span data-stu-id="b930e-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="b930e-176">Dit biedt veel voordelen die niet beschikbaar in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b930e-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="b930e-177">Meer informatie over Azure [implementatiemodellen][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="b930e-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="b930e-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Serverfailover Clustering</span><span class="sxs-lookup"><span data-stu-id="b930e-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="b930e-179">Windows Server Failover Clustering is Hallo-basis van een hoge beschikbaarheid SAP ASC's / SCS installatie en DBMS in Windows.</span><span class="sxs-lookup"><span data-stu-id="b930e-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="b930e-180">Een failovercluster is een groep 1 + n onafhankelijke servers (knooppunten) die samenwerken tooincrease Hallo beschikbaarheid van toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="b930e-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="b930e-181">Als een knooppuntfout optreedt, Windows Server Failover Clustering berekent het aantal fouten die zich voordoen kunnen tijdens het onderhoud van een gezonde Hallo cluster tooprovide toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="b930e-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="b930e-182">U kunt kiezen uit andere quorum-modi tooachieve Failoverclustering.</span><span class="sxs-lookup"><span data-stu-id="b930e-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="b930e-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Quorum-modi</span><span class="sxs-lookup"><span data-stu-id="b930e-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="b930e-184">U kunt kiezen uit vier quorum-modi wanneer u Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="b930e-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="b930e-185">**Knooppuntmeerderheid**.</span><span class="sxs-lookup"><span data-stu-id="b930e-185">**Node Majority**.</span></span> <span data-ttu-id="b930e-186">Elk knooppunt van Hallo kunt stemmen.</span><span class="sxs-lookup"><span data-stu-id="b930e-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="b930e-187">Hallo cluster werkt alleen met een meerderheid van stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="b930e-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="b930e-188">U wordt aangeraden deze optie voor clusters met een oneven aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="b930e-189">Bijvoorbeeld drie knooppunten in een cluster met zeven knooppunten kunnen mislukken en Hallo cluster tussen beelden meerderheid bereikt en toorun blijft.</span><span class="sxs-lookup"><span data-stu-id="b930e-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="b930e-190">**Knooppunt en schijfmeerderheid**.</span><span class="sxs-lookup"><span data-stu-id="b930e-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="b930e-191">Elk knooppunt en een aangewezen schijf (een schijfwitness) in de clusteropslag Hallo kunnen stemmen wanneer ze beschikbaar zijn en in de communicatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="b930e-192">Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="b930e-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="b930e-193">Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="b930e-194">Als Hallo schijf en half Hallo knooppunten online zijn, blijft Hallo-cluster in een foutloze toestand bevindt.</span><span class="sxs-lookup"><span data-stu-id="b930e-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="b930e-195">**Knooppunt en de meeste bestandsshare**.</span><span class="sxs-lookup"><span data-stu-id="b930e-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="b930e-196">Elk knooppunt plus een aangewezen bestandsshare (een bestandssharewitness) die Hallo beheerder maakt kunt stemmen, ongeacht of Hallo knooppunten en bestandsshare beschikbaar zijn en bij communicatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="b930e-197">Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="b930e-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="b930e-198">Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="b930e-199">Het is vergelijkbaar toohello knooppunt en schijfmeerderheid modus, maar een witness-bestandsshare wordt gebruikt in plaats van een witness-schijf.</span><span class="sxs-lookup"><span data-stu-id="b930e-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="b930e-200">Deze modus is eenvoudig tooimplement, maar als het Hallo-bestandsshare zelf is niet maximaal beschikbaar, het mogelijk een potentieel risico.</span><span class="sxs-lookup"><span data-stu-id="b930e-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="b930e-201">**Geen meerderheid: Alleen schijf**.</span><span class="sxs-lookup"><span data-stu-id="b930e-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="b930e-202">Hallo-cluster heeft quorum als één knooppunt beschikbaar en communicatie met een specifieke schijf in de clusteropslag Hallo is.</span><span class="sxs-lookup"><span data-stu-id="b930e-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="b930e-203">Alleen Hallo knooppunten die ook in de communicatie met die schijf kunnen Hallo-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b930e-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="b930e-204">Het is raadzaam dat u deze modus niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="b930e-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Serverfailover Clustering van on-premises</span><span class="sxs-lookup"><span data-stu-id="b930e-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="b930e-206">Afbeelding 1 ziet u een cluster met twee knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="b930e-207">Als hello netwerkverbinding tussen de knooppunten Hallo mislukt en beide knooppunten blijven en wordt uitgevoerd, een quorum schijf of bestandsshare bepaalt welk knooppunt blijft tooprovide Hallo cluster toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="b930e-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="b930e-208">Hallo-knooppunt dat toegang toohello quorumschijf of de bestandsshare is Hallo-knooppunt dat ervoor zorgt dat services kunnen blijven.</span><span class="sxs-lookup"><span data-stu-id="b930e-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="b930e-209">Omdat in dit voorbeeld een cluster met twee knooppunten wordt, gebruiken we Hallo knooppunt en bestandssharemeerderheid quorum-modus.</span><span class="sxs-lookup"><span data-stu-id="b930e-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="b930e-210">Hallo knooppunt en schijfmeerderheid is ook een geldige optie.</span><span class="sxs-lookup"><span data-stu-id="b930e-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="b930e-211">U wordt aangeraden dat u een quorumschijf in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b930e-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="b930e-212">U kunt system technologie toomake van netwerk- en deze maximaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-212">You can use network and storage system technology toomake it highly available.</span></span>

![Afbeelding 1: Voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="b930e-214">_**Afbeelding 1:** voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="b930e-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="b930e-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Gedeelde opslag</span><span class="sxs-lookup"><span data-stu-id="b930e-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="b930e-216">Afbeelding 1 wordt ook een cluster met twee knooppunten gedeelde opslag.</span><span class="sxs-lookup"><span data-stu-id="b930e-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="b930e-217">Alle knooppunten in cluster Hallo detecteren in een cluster van de gedeelde opslag lokale gedeelde opslag.</span><span class="sxs-lookup"><span data-stu-id="b930e-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="b930e-218">Een vergrendelingsfout mechanisme beschermt Hallo gegevens tegen beschadiging.</span><span class="sxs-lookup"><span data-stu-id="b930e-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="b930e-219">Alle knooppunten kunnen detecteren als een ander knooppunt mislukt.</span><span class="sxs-lookup"><span data-stu-id="b930e-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="b930e-220">Als een knooppunt is mislukt, wordt het resterende knooppunt hello wordt eigenaar van opslagbronnen Hallo en zorgt ervoor Hallo beschikbaarheid van services.</span><span class="sxs-lookup"><span data-stu-id="b930e-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-221">U hoeft geen gedeelde schijven voor hoge beschikbaarheid bij sommige toepassingen DBMS zoals met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b930e-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="b930e-222">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="b930e-223">Configuratie van het cluster Windows hello hoeft in dat geval niet een gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="b930e-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="b930e-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Netwerk- en naamomzetting</span><span class="sxs-lookup"><span data-stu-id="b930e-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="b930e-225">Clientcomputers bereiken Hallo-cluster via een virtueel IP-adres en de naam van een virtuele host op die Hallo DNS-server biedt.</span><span class="sxs-lookup"><span data-stu-id="b930e-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="b930e-226">Hallo on-premises knooppunten en Hallo DNS-server kan meerdere IP-adressen verwerken.</span><span class="sxs-lookup"><span data-stu-id="b930e-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="b930e-227">In een typische installatie gebruikt u twee of meer netwerkverbindingen:</span><span class="sxs-lookup"><span data-stu-id="b930e-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="b930e-228">Een speciale verbinding toohello opslag</span><span class="sxs-lookup"><span data-stu-id="b930e-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="b930e-229">Een cluster interne netwerkverbinding voor Hallo heartbeat</span><span class="sxs-lookup"><span data-stu-id="b930e-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="b930e-230">Een openbaar netwerk dat clients tooconnect toohello cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="b930e-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="b930e-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Serverfailover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="b930e-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="b930e-232">Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="b930e-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="b930e-233">Als u een gedeelde clusterschijf bouwen, moet u de namen van verschillende IP-adressen en virtuele host tooset voor Hallo SAP ASC's / SCS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="b930e-234">In dit artikel hoofdconcepten bespreken we en Hallo extra stappen vereist toobuild een SAP-services met hoge beschikbaarheid centrale cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="b930e-235">We zien u hoe tooset up Hallo hulpprogramma van derden SIOS DataKeeper en hoe tooconfigure hello Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="b930e-236">U kunt deze hulpprogramma's voor toocreate een failover-cluster van Windows gebruiken met een bestandsshare-witness in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Afbeelding 2: Windows Server Failover Clustering configuratie in Azure zonder een gedeelde schijf][sap-ha-guide-figure-1001]

<span data-ttu-id="b930e-238">_**Afbeelding 2:** configuratie Windows Server Failover Clustering in Azure zonder een gedeelde schijf_</span><span class="sxs-lookup"><span data-stu-id="b930e-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="b930e-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Gedeelde schijf in Azure met SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="b930e-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="b930e-240">U moet gedeelde opslag voor een hoge beschikbaarheid SAP ASC's / SCS-exemplaar in de cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="b930e-241">Zoals van September 2016 Azure niet gedeelde opslag die biedt kunt u toocreate een cluster met gedeelde opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="b930e-242">U kunt software van derden SIOS DataKeeper Cluster Edition toocreate een gespiegelde opslagruimte die gedeelde clusteropslag simuleert.</span><span class="sxs-lookup"><span data-stu-id="b930e-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="b930e-243">Hallo SIOS oplossing biedt realtime synchrone gegevensreplicatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="b930e-244">Dit is hoe u een gedeelde schijfbron voor een cluster kunt maken:</span><span class="sxs-lookup"><span data-stu-id="b930e-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="b930e-245">Koppel een extra Azure virtuele harde schijf (VHD) tooeach van Hallo virtuele machines (VM's) in de configuratie van een Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="b930e-246">SIOS DataKeeper Cluster Edition wordt uitgevoerd op beide knooppunten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b930e-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="b930e-247">SIOS DataKeeper Cluster Edition zodanig configureren dat het Hallo-inhoud van extra VHD gekoppeld volume van Hallo bron virtuele machine toohello extra VHD gekoppeld volume van de virtuele doelmachine Hallo Hallo weerspiegelt.</span><span class="sxs-lookup"><span data-stu-id="b930e-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="b930e-248">SIOS DataKeeper isoleert Hallo bron en doel lokale volumes en geeft ze tooWindows Server Failover Clustering als één gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="b930e-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="b930e-249">Vindt u meer informatie over [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="b930e-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Afbeelding 3: Configuratie van Windows Server Failover Clustering in Azure met SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="b930e-251">_**Afbeelding 3:** configuratie Windows Server Failover Clustering in Azure met SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="b930e-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-252">U hoeft geen gedeelde schijven voor hoge beschikbaarheid met sommige DBMS-producten, zoals SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b930e-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="b930e-253">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="b930e-254">Hallo Windows cluster-configuratie nodig niet in dit geval een gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="b930e-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="b930e-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Naamomzetting in Azure</span><span class="sxs-lookup"><span data-stu-id="b930e-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="b930e-256">Hello Azure-cloud-platform biedt geen Hallo optie tooconfigure virtuele IP-adressen, zoals zwevend IP-adressen te bieden.</span><span class="sxs-lookup"><span data-stu-id="b930e-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="b930e-257">U moet een alternatieve oplossing tooset van een virtueel IP-adres tooreach Hallo clusterbron in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="b930e-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="b930e-258">Azure heeft een interne load balancer in hello Azure Load Balancer-service.</span><span class="sxs-lookup"><span data-stu-id="b930e-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="b930e-259">Met Hallo interne load balancer bereiken clients Hallo cluster via Hallo cluster virtuele IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b930e-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="b930e-260">U moet toodeploy Hallo interne load balancer in Hallo resourcegroep die de clusterknooppunten Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="b930e-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="b930e-261">Configureer vervolgens alle benodigde poorttoewijzing regels met Hallo test poorten van Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="b930e-262">Hallo-clients kunnen verbinding maken via de naam van de virtuele host Hallo.</span><span class="sxs-lookup"><span data-stu-id="b930e-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="b930e-263">Hallo DNS-server wordt omgezet Hallo cluster IP-adres en Hallo interne load balancer-ingangen poorttoewijzing toohello actieve knooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="b930e-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver hoge beschikbaarheid in een Azure-infrastructuur-as-a-Service (IaaS)</span><span class="sxs-lookup"><span data-stu-id="b930e-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="b930e-265">tooachieve SAP-toepassing hoge beschikbaarheid, zoals SAP-softwareonderdelen, moet u tooprotect Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="b930e-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="b930e-266">SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-266">SAP Application Server instance</span></span>
* <span data-ttu-id="b930e-267">SAP ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="b930e-268">DBMS-server</span><span class="sxs-lookup"><span data-stu-id="b930e-268">DBMS server</span></span>

<span data-ttu-id="b930e-269">Zie voor meer informatie over het beveiligen van SAP-onderdelen in scenario's voor hoge beschikbaarheid [Azure Virtual Machines planning en implementatie voor SAP NetWeaver](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b930e-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="b930e-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Hoge beschikbaarheid SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="b930e-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="b930e-271">Normaal gesproken hoeft u niet een bepaalde oplossing voor hoge beschikbaarheid voor Hallo SAP-toepassingsserver en dialoogvenster exemplaren.</span><span class="sxs-lookup"><span data-stu-id="b930e-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="b930e-272">Een maximale beschikbaarheid realiseren door redundantie en configureert u meerdere exemplaren van het dialoogvenster in verschillende exemplaren van Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="b930e-273">U hebt ten minste twee SAP exemplaren van een toepassing in twee exemplaren van Azure Virtual Machines geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Afbeelding 4: Hoge beschikbaarheid SAP-toepassingsserver][sap-ha-guide-figure-2000]

<span data-ttu-id="b930e-275">_**Afbeelding 4:** hoge beschikbaarheid SAP-toepassingsserver_</span><span class="sxs-lookup"><span data-stu-id="b930e-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="b930e-276">U moet alle virtuele machines dat SAP-toepassingsserver instanties van hosts in dezelfde Azure beschikbaarheidsset Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b930e-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="b930e-277">Een Azure beschikbaarheidsset zorgt ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="b930e-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="b930e-278">Alle virtuele machines deel uitmaken van Hallo dezelfde upgradedomein.</span><span class="sxs-lookup"><span data-stu-id="b930e-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="b930e-279">Een upgradedomein bijvoorbeeld zorgt ervoor dat Hallo virtuele machines zijn niet op Hallo bijgewerkt hetzelfde moment tijdens gepland onderhoud uitval.</span><span class="sxs-lookup"><span data-stu-id="b930e-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="b930e-280">Alle virtuele machines deel uitmaken van Hallo hetzelfde foutdomein.</span><span class="sxs-lookup"><span data-stu-id="b930e-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="b930e-281">Een foutdomein bijvoorbeeld ervoor zorgt dat virtuele machines zodat er geen storingspunt is van invloed op Hallo beschikbaarheid van alle virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="b930e-282">Meer informatie over het te[Hallo beschikbaarheid van virtuele machines beheren][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="b930e-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="b930e-283">Omdat hello Azure storage-account een potentieel storingspunt is, is het belangrijk toohave ten minste twee Azure storage-accounts, waarbij ten minste twee virtuele machines worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="b930e-284">In een ideaal setup wordt Hallo schijven van elke virtuele machine die wordt uitgevoerd een SAP-dialoogvenster-exemplaar geïmplementeerd in een ander opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b930e-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="b930e-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Hoge beschikbaarheid SAP ASC's / SCS exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="b930e-286">Afbeelding 5 is een voorbeeld van een exemplaar van de SAP ASC's / SCS hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b930e-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Afbeelding 5: Hoge beschikbaarheid SAP ASC's / SCS exemplaar][sap-ha-guide-figure-2001]

<span data-ttu-id="b930e-288">_**Afbeelding 5:** hoge beschikbaarheid SAP ASC's / SCS-exemplaar_</span><span class="sxs-lookup"><span data-stu-id="b930e-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="b930e-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASC's / SCS exemplaar hoge beschikbaarheid met Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="b930e-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="b930e-290">Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="b930e-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="b930e-291">toobuild een failover-cluster van Windows, moet u een gedeelde clusterschijf, verschillende IP-adressen, verschillende namen van de virtuele host en een Azure interne load balancer voor een exemplaar SAP ASC's / SCS clustering.</span><span class="sxs-lookup"><span data-stu-id="b930e-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="b930e-292">Dit bespreken we in meer detail verderop in Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="b930e-292">We discuss this in more detail later in hello article.</span></span>

![Afbeelding 6: Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met behulp van SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="b930e-294">_**Afbeelding 6:** Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="b930e-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="b930e-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Hoge beschikbaarheid DBMS exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="b930e-296">Hallo DBMS is ook een aanspreekpunt in een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="b930e-297">U moet tooprotect deze met behulp van een oplossing voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b930e-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="b930e-298">Afbeelding 7 toont een hoge beschikbaarheid SQL Server Always On oplossing in Azure, met Windows Server Failover Clustering en hello Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="b930e-299">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden met behulp van een eigen DBMS-replicatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="b930e-300">In dit geval nodig u niet clusteren gedeelde schijven die vereenvoudigt Hallo volledige installatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Afbeelding 7: Voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="b930e-302">_**Afbeelding 7:** voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="b930e-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="b930e-303">Zie voor meer informatie over SQL Server in Azure met Azure Resource Manager-implementatiemodel Hallo clustering deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="b930e-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="b930e-304">[AlwaysOn-beschikbaarheidsgroep in Azure Virtual Machines handmatig configureren met behulp van Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="b930e-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="b930e-305">[Een Azure interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="b930e-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="b930e-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>End-to-end hoge beschikbaarheid implementatiescenario 's</span><span class="sxs-lookup"><span data-stu-id="b930e-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="b930e-307">Implementatiescenario met architectuur sjabloon 1</span><span class="sxs-lookup"><span data-stu-id="b930e-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="b930e-308">Afbeelding 8 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="b930e-309">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="b930e-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="b930e-310">Een speciale cluster wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="b930e-311">Een speciale cluster wordt gebruikt voor Hallo DBMS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="b930e-312">SAP Application Server-exemplaren zijn in hun eigen toegewezen virtuele machines geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Afbeelding 8: Hoge beschikbaarheid architectuur sjabloon 1, met speciale cluster voor ASC's / SCS en DBMS SAP][sap-ha-guide-figure-2004]

<span data-ttu-id="b930e-314">_**Afbeelding 8:** SAP-architectuur sjabloon 1 hoge beschikbaarheid, speciale clusters voor ASC's / SCS en DBMS_</span><span class="sxs-lookup"><span data-stu-id="b930e-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="b930e-315">Implementatiescenario met behulp van architectuur sjabloon 2</span><span class="sxs-lookup"><span data-stu-id="b930e-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="b930e-316">Afbeelding 9 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="b930e-317">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="b930e-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="b930e-318">Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS-instantie en Hallo DBMS.</span><span class="sxs-lookup"><span data-stu-id="b930e-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="b930e-319">SAP Application Server-exemplaren zijn in de eigen toegewezen virtuele machines geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Afbeelding 9: Hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP][sap-ha-guide-figure-2005]

<span data-ttu-id="b930e-321">_**Afbeelding 9:** hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP_</span><span class="sxs-lookup"><span data-stu-id="b930e-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="b930e-322">Implementatiescenario met architectuur sjabloon 3</span><span class="sxs-lookup"><span data-stu-id="b930e-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="b930e-323">Afbeelding 10 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **twee** SAP-systemen, met &lt;SID1&gt; en &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="b930e-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="b930e-324">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="b930e-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="b930e-325">Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS SID1 exemplaar *en* Hallo SAP ASC's / SCS SID2 exemplaar (één cluster).</span><span class="sxs-lookup"><span data-stu-id="b930e-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="b930e-326">Een speciale cluster wordt gebruikt voor DBMS SID1 en een ander toegewezen cluster wordt gebruikt voor DBMS SID2 (twee clusters).</span><span class="sxs-lookup"><span data-stu-id="b930e-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="b930e-327">SAP Application Server-exemplaren voor Hallo SAP-systeem SID1 hebben hun eigen toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="b930e-328">SAP Application Server-exemplaren voor Hallo SAP-systeem SID2 hebben hun eigen toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Afbeelding 10: SAP hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren][sap-ha-guide-figure-6003]

<span data-ttu-id="b930e-330">_**Afbeelding 10:** SAP-hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren_</span><span class="sxs-lookup"><span data-stu-id="b930e-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="b930e-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Hallo-infrastructuur voorbereiden</span><span class="sxs-lookup"><span data-stu-id="b930e-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="b930e-332">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 1</span><span class="sxs-lookup"><span data-stu-id="b930e-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="b930e-333">Azure Resource Manager-sjablonen voor SAP vereenvoudigen implementatie van de vereiste resources.</span><span class="sxs-lookup"><span data-stu-id="b930e-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="b930e-334">Hallo drie lagen sjablonen in Azure Resource Manager ondersteunen ook scenario's met hoge beschikbaarheid, zoals in de architectuur sjabloon 1, met twee clusters.</span><span class="sxs-lookup"><span data-stu-id="b930e-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="b930e-335">Elk cluster is een SAP storingspunt voor SAP ASC's / SCS en DBMS.</span><span class="sxs-lookup"><span data-stu-id="b930e-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="b930e-336">Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor Hallo voorbeeldscenario die in dit artikel worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="b930e-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="b930e-337">Azure Marketplace-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="b930e-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="b930e-338">Aangepaste installatiekopie</span><span class="sxs-lookup"><span data-stu-id="b930e-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="b930e-339">tooprepare hello infrastructuur voor architecturale sjabloon 1:</span><span class="sxs-lookup"><span data-stu-id="b930e-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="b930e-340">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **SYSTEMAVAILABILITY** de optie **HA**.</span><span class="sxs-lookup"><span data-stu-id="b930e-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Afbeelding 11: Stel SAP-parameters voor hoge beschikbaarheid Azure Resource Manager][sap-ha-guide-figure-3000]

<span data-ttu-id="b930e-342">_**Afbeelding 11:** ingesteld SAP-parameters voor hoge beschikbaarheid Azure Resource Manager_</span><span class="sxs-lookup"><span data-stu-id="b930e-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="b930e-343">Hallo-sjablonen maken:</span><span class="sxs-lookup"><span data-stu-id="b930e-343">hello templates create:</span></span>

  * <span data-ttu-id="b930e-344">**Virtuele machines**:</span><span class="sxs-lookup"><span data-stu-id="b930e-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="b930e-345">SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - di - <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="b930e-346">ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - ASC - 's <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="b930e-347">DBMS-cluster: <*SAPSystemSID*> - db - <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="b930e-348">**Netwerkkaarten voor alle virtuele machines met bijbehorende IP-adressen**:</span><span class="sxs-lookup"><span data-stu-id="b930e-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="b930e-349"><*SAPSystemSID*> - nic - di - <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="b930e-350"><*SAPSystemSID*> - nic - ASC's - <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="b930e-351"><*SAPSystemSID*> - nic - db - <*getal*></span><span class="sxs-lookup"><span data-stu-id="b930e-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="b930e-352">**Azure storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="b930e-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="b930e-353">**Beschikbaarheidsgroepen** voor:</span><span class="sxs-lookup"><span data-stu-id="b930e-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="b930e-354">SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - avset - di</span><span class="sxs-lookup"><span data-stu-id="b930e-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="b930e-355">SAP ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - avset - ASC's</span><span class="sxs-lookup"><span data-stu-id="b930e-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="b930e-356">DBMS cluster virtuele machines: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="b930e-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="b930e-357">**Azure interne load balancer**:</span><span class="sxs-lookup"><span data-stu-id="b930e-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="b930e-358">Met alle poorten voor Hallo ASC's / SCS exemplaar en IP-adres <*SAPSystemSID*> - lb - ASC's</span><span class="sxs-lookup"><span data-stu-id="b930e-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="b930e-359">Met alle poorten voor de SQL Server-DBMS en IP-adres Hallo <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="b930e-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="b930e-360">**Netwerkbeveiligingsgroep**: <*SAPSystemSID*> - nsg - ASC's-0</span><span class="sxs-lookup"><span data-stu-id="b930e-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="b930e-361">Met een open externe Remote Desktop Protocol (RDP)-poort toohello <*SAPSystemSID*> - ASC's - 0 virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b930e-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-362">Alle IP-adressen van Hallo netwerkkaarten en Azure interne load balancers zijn **dynamische** standaard.</span><span class="sxs-lookup"><span data-stu-id="b930e-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="b930e-363">Ze ook wijzigen**statische** IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="b930e-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="b930e-364">We beschrijven hoe toodo dit later op Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="b930e-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="b930e-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Virtuele machines implementeren met het bedrijfsnetwerk connectiviteit (cross-premises) toouse in productie</span><span class="sxs-lookup"><span data-stu-id="b930e-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="b930e-366">Voor productiesystemen SAP, Azure virtuele machines implementeren met [bedrijfsnetwerk connectiviteit (cross-premises)] [ planning-guide-2.2] met behulp van Azure Site-naar-Site VPN- of Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b930e-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-367">U kunt uw Azure Virtual Network-exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="b930e-368">Hallo virtueel netwerk en subnet zijn al gemaakt en voorbereid.</span><span class="sxs-lookup"><span data-stu-id="b930e-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="b930e-369">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **bestaande**.</span><span class="sxs-lookup"><span data-stu-id="b930e-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="b930e-370">In Hallo **SUBNETID** Voeg Hallo volledige tekenreeks van het voorbereide Azure netwerk SubnetID waar u van plan toodeploy uw virtuele machines in Azure bent.</span><span class="sxs-lookup"><span data-stu-id="b930e-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="b930e-371">een lijst met alle Azure-netwerksubnetten tooget deze PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b930e-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="b930e-372">Hallo **ID** veld bevat Hallo **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="b930e-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="b930e-373">een lijst met alle tooget **SUBNETID** waarden, deze PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b930e-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="b930e-374">Hallo **SUBNETID** ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b930e-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="b930e-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Alleen in de cloud SAP-exemplaren voor test- en demo implementeren</span><span class="sxs-lookup"><span data-stu-id="b930e-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="b930e-376">U kunt uw SAP-systeem voor hoge beschikbaarheid in een cloudconfiguratie implementatiemodel implementeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="b930e-377">Dit type implementatie is vooral nuttig voor demo en test gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b930e-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="b930e-378">Het niet geschikt voor gebruiksvoorbeelden voor productie.</span><span class="sxs-lookup"><span data-stu-id="b930e-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="b930e-379">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="b930e-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="b930e-380">Hallo laat **SUBNETID** veld leeg.</span><span class="sxs-lookup"><span data-stu-id="b930e-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="b930e-381">Hallo SAP Azure Resource Manager sjabloon automatisch maakt Hallo virtuele Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="b930e-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-382">U moet ook toodeploy ten minste één virtuele machine specifiek zijn voor Active Directory en DNS-server in Hallo hetzelfde exemplaar van Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="b930e-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="b930e-383">Hallo-sjabloon maakt geen deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="b930e-384">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 2</span><span class="sxs-lookup"><span data-stu-id="b930e-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="b930e-385">U kunt deze Azure Resource Manager-sjabloon gebruiken voor toohelp SAP-implementatie van resources van de vereiste infrastructuur voor SAP architectuur sjabloon 2 vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="b930e-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="b930e-386">Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor deze implementatiescenario:</span><span class="sxs-lookup"><span data-stu-id="b930e-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="b930e-387">Azure Marketplace-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="b930e-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="b930e-388">Aangepaste installatiekopie</span><span class="sxs-lookup"><span data-stu-id="b930e-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="b930e-389">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 3</span><span class="sxs-lookup"><span data-stu-id="b930e-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="b930e-390">U kunt Hallo infrastructuur voorbereiden en configureren van SAP voor **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="b930e-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="b930e-391">U kunt bijvoorbeeld een extra exemplaar SAP ASC's / SCS in toevoegen een *bestaande* clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b930e-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="b930e-392">Zie voor meer informatie [configureren van een extra exemplaar SAP ASC's / SCS in een bestaand cluster configuratie toocreate een SAP multi-SID-configuratie in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="b930e-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="b930e-393">Als u een nieuw cluster met meerdere SID toocreate wilt, kunt u Hallo multi-SID [Quick Start-sjablonen op GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="b930e-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="b930e-394">een nieuw cluster met meerdere SID toocreate, moet u toodeploy Hallo drie sjablonen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b930e-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="b930e-395">ASC's / SCS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b930e-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="b930e-396">Database-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b930e-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="b930e-397">Toepassingssjabloon voor servers</span><span class="sxs-lookup"><span data-stu-id="b930e-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="b930e-398">Hallo hebben volgende secties meer informatie over het Hallo-sjablonen en moet u tooprovide in sjablonen Hallo Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="b930e-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="b930e-399"><a name="ASCS-SCS-template"></a>ASC's / SCS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b930e-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="b930e-400">Hallo ASC's / SCS sjabloon implementeert twee virtuele machines dat u een failover-cluster van Windows Server die als host fungeert voor meerdere exemplaren van ASC's / SCS toocreate kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="b930e-401">tooset van de sjabloon Hallo ASC's / SCS multi-SID in Hallo [ASC's / SCS multi-SID sjabloon][sap-templates-3-tier-multisid-xscs-marketplace-image], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="b930e-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="b930e-402">**Resource-voorvoegsel**.</span><span class="sxs-lookup"><span data-stu-id="b930e-402">**Resource Prefix**.</span></span>  <span data-ttu-id="b930e-403">Hallo resource voorvoegsel, namelijk gebruikte tooprefix alle resources die zijn gemaakt tijdens de implementatie van Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b930e-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="b930e-404">Omdat Hallo bronnen geen deel van een SAP-systeem tooonly uitmaken, is Hallo-voorvoegsel van Hallo resource niet Hallo SID van een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="b930e-405">Hallo-voorvoegsel moet liggen tussen **drie tot zes tekens**.</span><span class="sxs-lookup"><span data-stu-id="b930e-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="b930e-406">**Stack is Type**.</span><span class="sxs-lookup"><span data-stu-id="b930e-406">**Stack Type**.</span></span> <span data-ttu-id="b930e-407">Selecteer Hallo stack type Hallo SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="b930e-408">Afhankelijk van het type van de stack hello heeft Azure Load Balancer een (ABAP of alleen Java) of twee (ABAP + Java) privé IP-adressen per SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="b930e-409">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-409">**OS Type**.</span></span> <span data-ttu-id="b930e-410">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="b930e-411">**SAP System aantal**.</span><span class="sxs-lookup"><span data-stu-id="b930e-411">**SAP System Count**.</span></span> <span data-ttu-id="b930e-412">Selecteer Hallo nummer SAP-systemen dat u wilt dat tooinstall in dit cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="b930e-413">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-413">**System Availability**.</span></span> <span data-ttu-id="b930e-414">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="b930e-414">Select **HA**.</span></span>
  -  <span data-ttu-id="b930e-415">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b930e-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="b930e-416">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="b930e-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="b930e-417">**Nieuwe of bestaande Subnet**.</span><span class="sxs-lookup"><span data-stu-id="b930e-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="b930e-418">Instellen of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b930e-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="b930e-419">Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.</span><span class="sxs-lookup"><span data-stu-id="b930e-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="b930e-420">**Subnet-Id**. Set Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="b930e-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="b930e-421">Selecteer subnet Hallo van uw virtueel particulier netwerk (VPN) of ExpressRoute virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="b930e-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="b930e-422">Hallo-ID ziet er meestal als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b930e-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="b930e-423">/Subscriptions/ <*abonnements-id*> /resourceGroups/ <*Resourcegroepnaam*> /providers/Microsoft.Network/virtualNetworks/ <*virtuele-netwerknaam*> /subnets/ <*subnetnaam*></span><span class="sxs-lookup"><span data-stu-id="b930e-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="b930e-424">Hallo sjabloon implementeert één Load Balancer van Azure-instantie, die ondersteuning biedt voor meerdere SAP-systemen.</span><span class="sxs-lookup"><span data-stu-id="b930e-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="b930e-425">Hallo ASC's exemplaren worden geconfigureerd voor exemplaarnummer 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="b930e-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="b930e-426">Hallo SCS exemplaren worden geconfigureerd voor exemplaarnummer 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="b930e-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="b930e-427">Hallo ASC's in de wachtrij plaatsen replicatie Server (gebruikers) (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="b930e-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="b930e-428">Hallo SCS Ebruikers (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="b930e-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="b930e-429">Hallo load balancer bevat 1 (2 voor Linux) VIP(s), 1 x-VIP voor ASC's / SCS en 1 x-VIP voor Ebruikers (alleen voor Linux).</span><span class="sxs-lookup"><span data-stu-id="b930e-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="b930e-430">Hallo bevat volgende lijst alle load-balancingregels (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="b930e-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="b930e-431">Windows-specifieke poorten voor elke SAP-systeem: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="b930e-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="b930e-432">ASC's poorten (exemplaarnummer x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="b930e-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="b930e-433">SCS-poorten (exemplaarnummer x1): 32 x 1 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="b930e-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="b930e-434">ASCS ERS poorten op Linux (exemplaarnummer x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="b930e-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="b930e-435">SCS ERS poorten op Linux (exemplaarnummer x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="b930e-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="b930e-436">Hallo load balancer is geconfigureerde toouse Hallo test-poorten (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...) te volgen:</span><span class="sxs-lookup"><span data-stu-id="b930e-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="b930e-437">ASC's / SCS interne load balancer-testpoort: 620 0 x</span><span class="sxs-lookup"><span data-stu-id="b930e-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="b930e-438">Ebruikers interne load balancer-testpoort (alleen voor Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="b930e-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="b930e-439"><a name="database-template"></a>Database-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b930e-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="b930e-440">Hallo databasesjabloon implementeert een of twee virtuele machines waarmee u tooinstall kunt Hallo relationele databasebeheersysteem (RDBMS) voor een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="b930e-441">Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.</span><span class="sxs-lookup"><span data-stu-id="b930e-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="b930e-442">tooset up Hallo database multi-SID sjabloon in Hallo [multi-SID databasesjabloon][sap-templates-3-tier-multisid-db-marketplace-image], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="b930e-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="b930e-443">**SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="b930e-444">Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="b930e-445">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-445">**Os Type**.</span></span> <span data-ttu-id="b930e-446">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="b930e-447">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="b930e-447">**Dbtype**.</span></span> <span data-ttu-id="b930e-448">Selecteer Hallo type Hallo database dat u wilt dat tooinstall op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="b930e-449">Selecteer **SQL** als u wilt dat tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b930e-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="b930e-450">Selecteer **HANA** als u van plan tooinstall SAP HANA Hallo virtuele machines bent.</span><span class="sxs-lookup"><span data-stu-id="b930e-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="b930e-451">Zorg ervoor dat tooselect Hallo juiste operationele systeemtype: Selecteer **Windows** voor SQL, en selecteer een Linux-distributiepunt voor HANA.</span><span class="sxs-lookup"><span data-stu-id="b930e-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="b930e-452">Hello Azure Load Balancer die is verbonden toohello virtuele machines worden geconfigureerd toosupport Hallo geselecteerd databasetype:</span><span class="sxs-lookup"><span data-stu-id="b930e-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="b930e-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="b930e-453">**SQL**.</span></span> <span data-ttu-id="b930e-454">Hallo load balancer wordt verdelen poort 1433.</span><span class="sxs-lookup"><span data-stu-id="b930e-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="b930e-455">Zorg ervoor dat toouse deze poort voor de installatie van SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="b930e-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="b930e-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="b930e-456">**HANA**.</span></span> <span data-ttu-id="b930e-457">Hallo load balancer wordt verdelen poorten 35015 en 35017.</span><span class="sxs-lookup"><span data-stu-id="b930e-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="b930e-458">Zorg ervoor dat tooinstall SAP HANA met exemplaarnummer **50**.</span><span class="sxs-lookup"><span data-stu-id="b930e-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="b930e-459">Hallo load balancer wordt testpoort 62550 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="b930e-460">**Grootte van het SAP**.</span><span class="sxs-lookup"><span data-stu-id="b930e-460">**Sap System Size**.</span></span> <span data-ttu-id="b930e-461">Set Hallo aantal nieuwe Hallo-systeem SAP's bieden.</span><span class="sxs-lookup"><span data-stu-id="b930e-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="b930e-462">Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.</span><span class="sxs-lookup"><span data-stu-id="b930e-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="b930e-463">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-463">**System Availability**.</span></span> <span data-ttu-id="b930e-464">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="b930e-464">Select **HA**.</span></span>
  -  <span data-ttu-id="b930e-465">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b930e-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="b930e-466">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="b930e-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="b930e-467">**Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="b930e-468"><a name="application-servers-template"></a>Toepassingssjabloon voor servers</span><span class="sxs-lookup"><span data-stu-id="b930e-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="b930e-469">Hallo-toepassingssjabloon servers implementeert twee of meer virtuele machines die kan worden gebruikt als SAP-toepassingsserver exemplaren voor een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="b930e-470">Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.</span><span class="sxs-lookup"><span data-stu-id="b930e-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="b930e-471">tooset up Hallo servers multi-SID toepassingssjabloon, in Hallo [toepassingssjabloon servers multi-SID][sap-templates-3-tier-multisid-apps-marketplace-image], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="b930e-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="b930e-472">**SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="b930e-473">Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="b930e-474">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-474">**Os Type**.</span></span> <span data-ttu-id="b930e-475">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="b930e-476">**Grootte van het SAP**.</span><span class="sxs-lookup"><span data-stu-id="b930e-476">**Sap System Size**.</span></span> <span data-ttu-id="b930e-477">Hallo aantal nieuwe Hallo-systeem SAP's bieden.</span><span class="sxs-lookup"><span data-stu-id="b930e-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="b930e-478">Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.</span><span class="sxs-lookup"><span data-stu-id="b930e-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="b930e-479">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="b930e-479">**System Availability**.</span></span> <span data-ttu-id="b930e-480">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="b930e-480">Select **HA**.</span></span>
  -  <span data-ttu-id="b930e-481">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b930e-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="b930e-482">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="b930e-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="b930e-483">**Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="b930e-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="b930e-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="b930e-485">In ons voorbeeld is de adresruimte Hallo Hallo virtuele Azure-netwerk 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="b930e-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="b930e-486">Er is één subnet met de naam **Subnet**, met een adresbereik van 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="b930e-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="b930e-487">Alle virtuele machines en interne load balancers worden geïmplementeerd in dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="b930e-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b930e-488">Breng geen wijzigingen toohello netwerkinstellingen in het gastbesturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="b930e-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="b930e-489">Dit omvat het IP-adressen, DNS-servers en subnet.</span><span class="sxs-lookup"><span data-stu-id="b930e-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="b930e-490">De netwerkinstellingen configureren in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="b930e-491">Hallo Dynamic Host Configuration Protocol (DHCP)-service geeft uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="b930e-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="b930e-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP-adressen</span><span class="sxs-lookup"><span data-stu-id="b930e-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="b930e-493">Hallo tooset vereist dat DNS IP-adressen, Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="b930e-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="b930e-494">In de Azure-portal op Hallo Hallo **DNS-servers** blade, zorg ervoor dat het virtuele netwerk **DNS-servers** optie is ingesteld, te**aangepaste DNS**.</span><span class="sxs-lookup"><span data-stu-id="b930e-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="b930e-495">Selecteer uw instellingen op basis van Hallo type netwerk die u hebben.</span><span class="sxs-lookup"><span data-stu-id="b930e-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="b930e-496">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b930e-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="b930e-497">[Zakelijke netwerkverbinding (cross-premises)][planning-guide-2.2]: Hallo IP-adressen van Hallo lokale DNS-servers toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b930e-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="b930e-498">U kunt de lokale DNS-servers toohello virtuele machines die worden uitgevoerd in Azure uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="b930e-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="b930e-499">In dit scenario, voegt u toe Hallo IP-adressen van hello Azure virtuele machines waarop u Hallo DNS-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b930e-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="b930e-500">[Cloud-implementatie][planning-guide-2.1]: een extra virtuele machine implementeren in Hallo hetzelfde virtuele netwerk-exemplaar dat als een DNS-server fungeert.</span><span class="sxs-lookup"><span data-stu-id="b930e-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="b930e-501">Toevoegen van Hallo IP-adressen van hello Azure virtuele machines die u toorun DNS-service hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b930e-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Afbeelding 12: DNS-servers configureren voor Azure Virtual Network][sap-ha-guide-figure-3001]

    <span data-ttu-id="b930e-503">_**Afbeelding 12:** configureren DNS-servers voor Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="b930e-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="b930e-504">Als u Hallo IP-adressen van Hallo DNS-servers wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen en propageren Hallo nieuwe DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="b930e-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="b930e-505">Hallo DNS-service is geïnstalleerd en geconfigureerd op deze virtuele machines van Windows in ons voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b930e-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="b930e-506">De rol virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b930e-506">Virtual machine role</span></span> | <span data-ttu-id="b930e-507">Hostnaam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b930e-507">Virtual machine host name</span></span> | <span data-ttu-id="b930e-508">Naam van de netwerk-kaart</span><span class="sxs-lookup"><span data-stu-id="b930e-508">Network card name</span></span> | <span data-ttu-id="b930e-509">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="b930e-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b930e-510">Eerste DNS-server</span><span class="sxs-lookup"><span data-stu-id="b930e-510">First DNS server</span></span> |<span data-ttu-id="b930e-511">domcontr 0</span><span class="sxs-lookup"><span data-stu-id="b930e-511">domcontr-0</span></span> |<span data-ttu-id="b930e-512">PR1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="b930e-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="b930e-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="b930e-513">10.0.0.10</span></span> |
| <span data-ttu-id="b930e-514">Tweede DNS-server</span><span class="sxs-lookup"><span data-stu-id="b930e-514">Second DNS server</span></span> |<span data-ttu-id="b930e-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="b930e-515">domcontr-1</span></span> |<span data-ttu-id="b930e-516">PR1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="b930e-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="b930e-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="b930e-517">10.0.0.11</span></span> |

### <span data-ttu-id="b930e-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Hostnamen en statische IP-adressen voor Hallo SAP ASC's / SCS geclusterde exemplaar en DBMS geclusterd exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="b930e-519">Voor on-premises implementatie moet u deze gereserveerde hostnamen en IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="b930e-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="b930e-520">Virtuele host naam rol</span><span class="sxs-lookup"><span data-stu-id="b930e-520">Virtual host name role</span></span> | <span data-ttu-id="b930e-521">De naam van de virtuele host</span><span class="sxs-lookup"><span data-stu-id="b930e-521">Virtual host name</span></span> | <span data-ttu-id="b930e-522">Virtuele vaste IP-adres</span><span class="sxs-lookup"><span data-stu-id="b930e-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b930e-523">SAP ASC's / SCS eerste virtuele host clusternaam (voor cluster)</span><span class="sxs-lookup"><span data-stu-id="b930e-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="b930e-524">PR1-ASC's-vir</span><span class="sxs-lookup"><span data-stu-id="b930e-524">pr1-ascs-vir</span></span> |<span data-ttu-id="b930e-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="b930e-525">10.0.0.42</span></span> |
| <span data-ttu-id="b930e-526">Naam van de virtuele host op het exemplaar van SAP ASC's / SCS</span><span class="sxs-lookup"><span data-stu-id="b930e-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="b930e-527">PR1 ASC's sap</span><span class="sxs-lookup"><span data-stu-id="b930e-527">pr1-ascs-sap</span></span> |<span data-ttu-id="b930e-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="b930e-528">10.0.0.43</span></span> |
| <span data-ttu-id="b930e-529">SAP DBMS tweede virtuele host clusternaam (cluster management)</span><span class="sxs-lookup"><span data-stu-id="b930e-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="b930e-530">PR1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="b930e-530">pr1-dbms-vir</span></span> |<span data-ttu-id="b930e-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="b930e-531">10.0.0.32</span></span> |

<span data-ttu-id="b930e-532">Wanneer u Hallo-cluster maakt, maakt u Hallo virtuele hostnamen **pr1-ASC's-vir** en **pr1-dbms-vir** en Hallo bijbehorende IP-adressen die Hallo cluster zelf beheren.</span><span class="sxs-lookup"><span data-stu-id="b930e-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="b930e-533">Voor informatie over het toodo deze, Zie [verzamelen clusterknooppunten in een clusterconfiguratie][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="b930e-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="b930e-534">U kunt Hallo handmatig maken andere twee virtuele hostnamen **pr1 ASC's sap** en **pr1 dbms sap**, en Hallo bijbehorende IP-adressen op Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="b930e-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="b930e-535">Hallo geclusterde SAP ASC's / SCS-instantie en Hallo geclusterde DBMS instantie deze resources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="b930e-536">Voor informatie over het toodo deze, Zie [maken van een virtuele host-naam voor een geclusterd exemplaar van de SAP ASC's / SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="b930e-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="b930e-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statische IP-adressen voor virtuele machines die Hallo SAP instellen</span><span class="sxs-lookup"><span data-stu-id="b930e-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="b930e-538">Nadat u Hallo virtuele machines toouse in uw cluster implementeert, moet u tooset statische IP-adressen voor alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="b930e-539">Dit doen in hello Azure Virtual Network-configuratie en niet in het gastbesturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="b930e-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="b930e-540">Selecteer in de Azure-portal hello, **resourcegroep** > **netwerkkaart** > **instellingen** > **IP-adres** .</span><span class="sxs-lookup"><span data-stu-id="b930e-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="b930e-541">Op Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**.</span><span class="sxs-lookup"><span data-stu-id="b930e-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="b930e-542">In Hallo **IP-adres** Voer Hallo IP-adres dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="b930e-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b930e-543">Als u Hallo IP-adres van de netwerkkaart Hallo wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b930e-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Afbeelding 13: Statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen][sap-ha-guide-figure-3002]

  <span data-ttu-id="b930e-545">_**Afbeelding 13:** statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen_</span><span class="sxs-lookup"><span data-stu-id="b930e-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="b930e-546">Herhaal deze stap voor alle netwerkinterfaces, dat wil zeggen, voor alle virtuele machines, met inbegrip van virtuele machines wilt u toouse voor uw Active Directory en DNS-service.</span><span class="sxs-lookup"><span data-stu-id="b930e-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="b930e-547">In ons voorbeeld hebben we deze virtuele machines en statische IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="b930e-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="b930e-548">De rol virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b930e-548">Virtual machine role</span></span> | <span data-ttu-id="b930e-549">Hostnaam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b930e-549">Virtual machine host name</span></span> | <span data-ttu-id="b930e-550">Naam van de netwerk-kaart</span><span class="sxs-lookup"><span data-stu-id="b930e-550">Network card name</span></span> | <span data-ttu-id="b930e-551">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="b930e-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b930e-552">Eerste SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-552">First SAP Application Server instance</span></span> |<span data-ttu-id="b930e-553">PR1-di-0</span><span class="sxs-lookup"><span data-stu-id="b930e-553">pr1-di-0</span></span> |<span data-ttu-id="b930e-554">PR1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="b930e-554">pr1-nic-di-0</span></span> |<span data-ttu-id="b930e-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="b930e-555">10.0.0.50</span></span> |
| <span data-ttu-id="b930e-556">Tweede SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="b930e-557">PR1-di-1</span><span class="sxs-lookup"><span data-stu-id="b930e-557">pr1-di-1</span></span> |<span data-ttu-id="b930e-558">PR1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="b930e-558">pr1-nic-di-1</span></span> |<span data-ttu-id="b930e-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="b930e-559">10.0.0.51</span></span> |
| <span data-ttu-id="b930e-560">...</span><span class="sxs-lookup"><span data-stu-id="b930e-560">...</span></span> |<span data-ttu-id="b930e-561">...</span><span class="sxs-lookup"><span data-stu-id="b930e-561">...</span></span> |<span data-ttu-id="b930e-562">...</span><span class="sxs-lookup"><span data-stu-id="b930e-562">...</span></span> |<span data-ttu-id="b930e-563">...</span><span class="sxs-lookup"><span data-stu-id="b930e-563">...</span></span> |
| <span data-ttu-id="b930e-564">Laatste SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="b930e-565">PR1-di-5</span><span class="sxs-lookup"><span data-stu-id="b930e-565">pr1-di-5</span></span> |<span data-ttu-id="b930e-566">PR1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="b930e-566">pr1-nic-di-5</span></span> |<span data-ttu-id="b930e-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="b930e-567">10.0.0.55</span></span> |
| <span data-ttu-id="b930e-568">Eerste clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="b930e-569">PR1-ASC's-0</span><span class="sxs-lookup"><span data-stu-id="b930e-569">pr1-ascs-0</span></span> |<span data-ttu-id="b930e-570">PR1-nic-ASC's-0</span><span class="sxs-lookup"><span data-stu-id="b930e-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="b930e-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="b930e-571">10.0.0.40</span></span> |
| <span data-ttu-id="b930e-572">Tweede clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="b930e-573">PR1-ASC's-1</span><span class="sxs-lookup"><span data-stu-id="b930e-573">pr1-ascs-1</span></span> |<span data-ttu-id="b930e-574">PR1-nic-ASC's-1</span><span class="sxs-lookup"><span data-stu-id="b930e-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="b930e-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="b930e-575">10.0.0.41</span></span> |
| <span data-ttu-id="b930e-576">Eerste clusterknooppunt voor DBMS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="b930e-577">PR1-db-0</span><span class="sxs-lookup"><span data-stu-id="b930e-577">pr1-db-0</span></span> |<span data-ttu-id="b930e-578">PR1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="b930e-578">pr1-nic-db-0</span></span> |<span data-ttu-id="b930e-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="b930e-579">10.0.0.30</span></span> |
| <span data-ttu-id="b930e-580">Tweede clusterknooppunt voor DBMS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="b930e-581">PR1-db-1</span><span class="sxs-lookup"><span data-stu-id="b930e-581">pr1-db-1</span></span> |<span data-ttu-id="b930e-582">PR1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="b930e-582">pr1-nic-db-1</span></span> |<span data-ttu-id="b930e-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="b930e-583">10.0.0.31</span></span> |

### <span data-ttu-id="b930e-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Een statisch IP-adres instellen voor hello Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="b930e-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="b930e-585">Hallo SAP Azure Resource Manager-sjabloon maakt u een Azure interne load balancer die wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar als Hallo DBMS-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b930e-586">Hallo IP-adres van de naam van de virtuele host Hallo Hallo SAP ASC's / SCS is Hallo dezelfde als de IP-adres Hallo Hallo SAP ASC's / SCS interne load balancer: **pr1-lb-ASC's**.</span><span class="sxs-lookup"><span data-stu-id="b930e-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="b930e-587">Hallo IP-adres van de virtuele naam Hallo Hallo DBMS is Hallo dezelfde als de IP-adres Hallo Hallo DBMS interne load balancer: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="b930e-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="b930e-588">tooset een statisch IP-adres voor hello Azure interne load balancer:</span><span class="sxs-lookup"><span data-stu-id="b930e-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="b930e-589">Hallo initiële implementatie ingesteld Hallo interne load balancer IP-adres te**dynamische**.</span><span class="sxs-lookup"><span data-stu-id="b930e-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="b930e-590">In de Azure-portal op Hallo Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**.</span><span class="sxs-lookup"><span data-stu-id="b930e-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="b930e-591">Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-ASC's** toohello IP-adres van de naam van de virtuele host Hallo van Hallo SAP ASC's / SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="b930e-592">Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Afbeelding 14: Statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen][sap-ha-guide-figure-3003]

  <span data-ttu-id="b930e-594">_**Afbeelding 14:** statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen_</span><span class="sxs-lookup"><span data-stu-id="b930e-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="b930e-595">In ons voorbeeld hebben we twee Azure interne load balancers die deze statische IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="b930e-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="b930e-596">Azure interne load balancer-rol</span><span class="sxs-lookup"><span data-stu-id="b930e-596">Azure internal load balancer role</span></span> | <span data-ttu-id="b930e-597">Naam Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="b930e-597">Azure internal load balancer name</span></span> | <span data-ttu-id="b930e-598">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="b930e-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b930e-599">SAP ASC's / SCS exemplaar interne load balancer</span><span class="sxs-lookup"><span data-stu-id="b930e-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="b930e-600">PR1-lb-ASC 's</span><span class="sxs-lookup"><span data-stu-id="b930e-600">pr1-lb-ascs</span></span> |<span data-ttu-id="b930e-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="b930e-601">10.0.0.43</span></span> |
| <span data-ttu-id="b930e-602">SAP DBMS interne load balancer</span><span class="sxs-lookup"><span data-stu-id="b930e-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="b930e-603">PR1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="b930e-603">pr1-lb-dbms</span></span> |<span data-ttu-id="b930e-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="b930e-604">10.0.0.33</span></span> |


### <span data-ttu-id="b930e-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="b930e-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="b930e-606">Hallo SAP Azure Resource Manager-sjabloon maakt Hallo-poorten die u nodig:</span><span class="sxs-lookup"><span data-stu-id="b930e-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="b930e-607">Een exemplaar ABAP ASCS met Hallo standaard exemplaarnummer **00**</span><span class="sxs-lookup"><span data-stu-id="b930e-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="b930e-608">Een Java-SCS-exemplaar, met Hallo standaard exemplaarnummer **01**</span><span class="sxs-lookup"><span data-stu-id="b930e-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="b930e-609">Wanneer u uw exemplaar SAP ASC's / SCS installeert, moet u Hallo standaard exemplaarnummer **00** voor uw ABAP ASCS exemplaar en het Hallo standaard exemplaar **01** voor uw Java-SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="b930e-610">Vervolgens maakt u een vereiste voor de interne load balancer-eindpunten voor Hallo SAP NetWeaver poorten.</span><span class="sxs-lookup"><span data-stu-id="b930e-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="b930e-611">toocreate vereist interne load balancing eindpunten, maakt u eerst deze taakverdeling eindpunten voor Hallo SAP NetWeaver ABAP ASC's poorten:</span><span class="sxs-lookup"><span data-stu-id="b930e-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="b930e-612">Service/load balancing regelnaam</span><span class="sxs-lookup"><span data-stu-id="b930e-612">Service/load balancing rule name</span></span> | <span data-ttu-id="b930e-613">Standaardpoortnummers</span><span class="sxs-lookup"><span data-stu-id="b930e-613">Default port numbers</span></span> | <span data-ttu-id="b930e-614">Concrete poorten voor (ASC's exemplaar met exemplaarnummer 00) (uit met 10)</span><span class="sxs-lookup"><span data-stu-id="b930e-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b930e-615">In de wachtrij plaatsen Server / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="b930e-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="b930e-616">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-617">3200</span><span class="sxs-lookup"><span data-stu-id="b930e-617">3200</span></span> |
| <span data-ttu-id="b930e-618">ABAP berichtenserver / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="b930e-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="b930e-619">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-620">3600</span><span class="sxs-lookup"><span data-stu-id="b930e-620">3600</span></span> |
| <span data-ttu-id="b930e-621">Interne ABAP bericht / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="b930e-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="b930e-622">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-623">3900</span><span class="sxs-lookup"><span data-stu-id="b930e-623">3900</span></span> |
| <span data-ttu-id="b930e-624">Server-HTTP-bericht / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="b930e-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="b930e-625">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-626">8100</span><span class="sxs-lookup"><span data-stu-id="b930e-626">8100</span></span> |
| <span data-ttu-id="b930e-627">SAP Start Service ASC's HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="b930e-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="b930e-628">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="b930e-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="b930e-629">50013</span><span class="sxs-lookup"><span data-stu-id="b930e-629">50013</span></span> |
| <span data-ttu-id="b930e-630">SAP Start Service ASC's HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="b930e-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="b930e-631">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="b930e-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="b930e-632">50014</span><span class="sxs-lookup"><span data-stu-id="b930e-632">50014</span></span> |
| <span data-ttu-id="b930e-633">Replicatie van de wachtrij plaatsen / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="b930e-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="b930e-634">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="b930e-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="b930e-635">50016</span><span class="sxs-lookup"><span data-stu-id="b930e-635">50016</span></span> |
| <span data-ttu-id="b930e-636">SAP Start Service Ebruikers HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="b930e-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="b930e-637">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="b930e-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="b930e-638">51013</span><span class="sxs-lookup"><span data-stu-id="b930e-638">51013</span></span> |
| <span data-ttu-id="b930e-639">SAP Start Service Ebruikers HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="b930e-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="b930e-640">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="b930e-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="b930e-641">51014</span><span class="sxs-lookup"><span data-stu-id="b930e-641">51014</span></span> |
| <span data-ttu-id="b930e-642">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="b930e-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="b930e-643">5985</span><span class="sxs-lookup"><span data-stu-id="b930e-643">5985</span></span> |
| <span data-ttu-id="b930e-644">Bestandsshare *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="b930e-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="b930e-645">445</span><span class="sxs-lookup"><span data-stu-id="b930e-645">445</span></span> |

<span data-ttu-id="b930e-646">_**Tabel 1:** poortnummers van Hallo SAP NetWeaver ABAP ASC's exemplaren_</span><span class="sxs-lookup"><span data-stu-id="b930e-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="b930e-647">Vervolgens maakt u deze load balancing-eindpunten voor Hallo SAP NetWeaver Java SCS poorten:</span><span class="sxs-lookup"><span data-stu-id="b930e-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="b930e-648">Service/load balancing regelnaam</span><span class="sxs-lookup"><span data-stu-id="b930e-648">Service/load balancing rule name</span></span> | <span data-ttu-id="b930e-649">Standaardpoortnummers</span><span class="sxs-lookup"><span data-stu-id="b930e-649">Default port numbers</span></span> | <span data-ttu-id="b930e-650">Concrete poorten voor (exemplaar met exemplaarnummer 01 SCS) (Ebruikers met 11)</span><span class="sxs-lookup"><span data-stu-id="b930e-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b930e-651">In de wachtrij plaatsen Server / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="b930e-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="b930e-652">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-653">3201</span><span class="sxs-lookup"><span data-stu-id="b930e-653">3201</span></span> |
| <span data-ttu-id="b930e-654">Gateway-Server / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="b930e-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="b930e-655">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-656">3301</span><span class="sxs-lookup"><span data-stu-id="b930e-656">3301</span></span> |
| <span data-ttu-id="b930e-657">Java berichtenserver / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="b930e-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="b930e-658">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-659">3901</span><span class="sxs-lookup"><span data-stu-id="b930e-659">3901</span></span> |
| <span data-ttu-id="b930e-660">Server-HTTP-bericht / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="b930e-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="b930e-661">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="b930e-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="b930e-662">8101</span><span class="sxs-lookup"><span data-stu-id="b930e-662">8101</span></span> |
| <span data-ttu-id="b930e-663">SAP Start Service SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="b930e-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="b930e-664">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="b930e-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="b930e-665">50113</span><span class="sxs-lookup"><span data-stu-id="b930e-665">50113</span></span> |
| <span data-ttu-id="b930e-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="b930e-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="b930e-667">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="b930e-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="b930e-668">50114</span><span class="sxs-lookup"><span data-stu-id="b930e-668">50114</span></span> |
| <span data-ttu-id="b930e-669">Replicatie van de wachtrij plaatsen / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="b930e-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="b930e-670">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="b930e-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="b930e-671">50116</span><span class="sxs-lookup"><span data-stu-id="b930e-671">50116</span></span> |
| <span data-ttu-id="b930e-672">SAP Start Service Ebruikers HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="b930e-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="b930e-673">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="b930e-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="b930e-674">51113</span><span class="sxs-lookup"><span data-stu-id="b930e-674">51113</span></span> |
| <span data-ttu-id="b930e-675">SAP Start Service Ebruikers HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="b930e-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="b930e-676">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="b930e-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="b930e-677">51114</span><span class="sxs-lookup"><span data-stu-id="b930e-677">51114</span></span> |
| <span data-ttu-id="b930e-678">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="b930e-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="b930e-679">5985</span><span class="sxs-lookup"><span data-stu-id="b930e-679">5985</span></span> |
| <span data-ttu-id="b930e-680">Bestandsshare *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="b930e-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="b930e-681">445</span><span class="sxs-lookup"><span data-stu-id="b930e-681">445</span></span> |

<span data-ttu-id="b930e-682">_**Tabel 2:** poortnummers van Hallo SAP NetWeaver Java SCS exemplaren_</span><span class="sxs-lookup"><span data-stu-id="b930e-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Afbeelding 15: Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer][sap-ha-guide-figure-3004]

<span data-ttu-id="b930e-684">_**Afbeelding 15:** standaard ASC's / SCS load-balancingregels voor hello Azure interne load balancer_</span><span class="sxs-lookup"><span data-stu-id="b930e-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="b930e-685">Stel IP-adres Hallo Hallo load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="b930e-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen</span><span class="sxs-lookup"><span data-stu-id="b930e-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="b930e-687">Als u verschillende aantallen toouse voor Hallo SAP ASC's of SCS exemplaren wilt, moet u Hallo namen en waarden van de poorten wijzigen van standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="b930e-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="b930e-688">Selecteer in de Azure-portal hello,  **<* SID*> - lb - ASC's load balancer ** > **Load Balancing regels**.</span><span class="sxs-lookup"><span data-stu-id="b930e-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="b930e-689">Voor alle load-balancingregels die deel uitmaken van toohello SAP ASC's of SCS exemplaar, deze waarden te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="b930e-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="b930e-690">Naam</span><span class="sxs-lookup"><span data-stu-id="b930e-690">Name</span></span>
  * <span data-ttu-id="b930e-691">Poort</span><span class="sxs-lookup"><span data-stu-id="b930e-691">Port</span></span>
  * <span data-ttu-id="b930e-692">Back-end-poort</span><span class="sxs-lookup"><span data-stu-id="b930e-692">Back-end port</span></span>

  <span data-ttu-id="b930e-693">Bijvoorbeeld, als u toochange Hallo ASC's exemplaar standaardnummer van 00 too31 wilt, moet u toomake Hallo wijzigingen voor alle poorten die worden vermeld in tabel 1.</span><span class="sxs-lookup"><span data-stu-id="b930e-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="b930e-694">Hier volgt een voorbeeld van een update voor poort *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="b930e-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Afbeelding 16: Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen][sap-ha-guide-figure-3005]

  <span data-ttu-id="b930e-696">_**Afbeelding 16:** wijziging Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer_</span><span class="sxs-lookup"><span data-stu-id="b930e-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="b930e-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows virtuele machines toohello domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="b930e-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="b930e-698">Nadat u een statisch IP-adres toohello virtuele machines toegewezen, voegt u Hallo virtuele machines toohello domein toe.</span><span class="sxs-lookup"><span data-stu-id="b930e-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Afbeelding 17: Een virtuele machine tooa-domein toevoegen][sap-ha-guide-figure-3006]

<span data-ttu-id="b930e-700">_**Afbeelding 17:** een virtuele machine tooa domein toevoegen_</span><span class="sxs-lookup"><span data-stu-id="b930e-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="b930e-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar toe te voegen</span><span class="sxs-lookup"><span data-stu-id="b930e-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="b930e-702">Azure Load Balancer heeft een interne load balancer die wordt gesloten verbindingen als Hallo verbindingen niet actief gedurende een bepaalde zijn time (niet-actieve time-out).</span><span class="sxs-lookup"><span data-stu-id="b930e-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="b930e-703">SAP werkprocessen in de wachtrij plaatsen van dialoogvenster exemplaren geopende verbindingen toohello SAP verwerken zodra Hallo eerste in de wachtrij plaatsen/in wachtrij behoeften toobe verzonden aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b930e-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="b930e-704">Deze verbindingen meestal blijven tot stand gebrachte tot Hallo werkproces of Hallo in de wachtrij plaatsen proces opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="b930e-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="b930e-705">Echter, als Hallo verbinding gedurende een bepaalde tijd inactief is, hello Azure interne load balancer wordt gesloten Hallo verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b930e-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="b930e-706">Dit geen probleem omdat Hallo SAP-werkproces toohello Hallo-wachtrij plaatsen verbindingsproces herstelt als het niet meer bestaat.</span><span class="sxs-lookup"><span data-stu-id="b930e-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="b930e-707">Deze activiteiten zijn gedocumenteerd in Hallo developer traceringen SAP-processen, maar ze een grote hoeveelheid extra inhoud in deze traceringen maken.</span><span class="sxs-lookup"><span data-stu-id="b930e-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="b930e-708">Het is een goed idee toochange Hallo TCP/IP `KeepAliveTime` en `KeepAliveInterval` op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="b930e-709">Deze wijzigingen in Hallo TCP/IP-parameters met SAP profiel parameters, dat wordt beschreven in artikel hello later worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="b930e-710">op beide clusterknooppunten Windows toevoegen tooadd registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS instantie eerst deze registervermeldingen Windows voor SAP ASC's / SCS:</span><span class="sxs-lookup"><span data-stu-id="b930e-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="b930e-711">Pad</span><span class="sxs-lookup"><span data-stu-id="b930e-711">Path</span></span> | <span data-ttu-id="b930e-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="b930e-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="b930e-713">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="b930e-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="b930e-714">Type variabele</span><span class="sxs-lookup"><span data-stu-id="b930e-714">Variable type</span></span> |<span data-ttu-id="b930e-715">REG_DWORD (decimaal)</span><span class="sxs-lookup"><span data-stu-id="b930e-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="b930e-716">Waarde</span><span class="sxs-lookup"><span data-stu-id="b930e-716">Value</span></span> |<span data-ttu-id="b930e-717">120000</span><span class="sxs-lookup"><span data-stu-id="b930e-717">120000</span></span> |
| <span data-ttu-id="b930e-718">Koppeling toodocumentation</span><span class="sxs-lookup"><span data-stu-id="b930e-718">Link toodocumentation</span></span> |[<span data-ttu-id="b930e-719">https://technet.Microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="b930e-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="b930e-720">_**Tabel 3:** wijziging Hallo eerste TCP/IP-parameter_</span><span class="sxs-lookup"><span data-stu-id="b930e-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="b930e-721">Voegt u deze Windows-registervermeldingen op beide clusterknooppunten Windows voor SAP ASC's / SCS:</span><span class="sxs-lookup"><span data-stu-id="b930e-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="b930e-722">Pad</span><span class="sxs-lookup"><span data-stu-id="b930e-722">Path</span></span> | <span data-ttu-id="b930e-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="b930e-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="b930e-724">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="b930e-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="b930e-725">Type variabele</span><span class="sxs-lookup"><span data-stu-id="b930e-725">Variable type</span></span> |<span data-ttu-id="b930e-726">REG_DWORD (decimaal)</span><span class="sxs-lookup"><span data-stu-id="b930e-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="b930e-727">Waarde</span><span class="sxs-lookup"><span data-stu-id="b930e-727">Value</span></span> |<span data-ttu-id="b930e-728">120000</span><span class="sxs-lookup"><span data-stu-id="b930e-728">120000</span></span> |
| <span data-ttu-id="b930e-729">Koppeling toodocumentation</span><span class="sxs-lookup"><span data-stu-id="b930e-729">Link toodocumentation</span></span> |[<span data-ttu-id="b930e-730">https://technet.Microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="b930e-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="b930e-731">_**Tabel 4:** wijziging Hallo tweede TCP/IP-parameter_</span><span class="sxs-lookup"><span data-stu-id="b930e-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="b930e-732">**tooapply hello verandert, opnieuw opstarten van beide clusterknooppunten**.</span><span class="sxs-lookup"><span data-stu-id="b930e-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="b930e-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-instantie instellen</span><span class="sxs-lookup"><span data-stu-id="b930e-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="b930e-734">Instellen van een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-exemplaar, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b930e-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="b930e-735">Hallo clusterknooppunten in een clusterconfiguratie verzamelen</span><span class="sxs-lookup"><span data-stu-id="b930e-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="b930e-736">Een cluster bestandsshare-witness configureren</span><span class="sxs-lookup"><span data-stu-id="b930e-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="b930e-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Hallo clusterknooppunten in een clusterconfiguratie verzamelen</span><span class="sxs-lookup"><span data-stu-id="b930e-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="b930e-738">In Hallo functie toevoegen en de Wizard Functies toevoegen voor failover clustering tooboth clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="b930e-739">Hallo failover-cluster instellen met behulp van Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="b930e-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="b930e-740">Selecteer in Failoverclusterbeheer **Cluster maken**, en voegt u alleen Hallo naam van de eerste cluster hello, knooppunt A. Voeg het tweede knooppunt Hallo nog; het tweede knooppunt Hallo voegt u in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="b930e-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Afbeelding 18: Hallo-server of de naam van de virtuele machine van de eerste clusterknooppunt Hallo toevoegen][sap-ha-guide-figure-3007]

  <span data-ttu-id="b930e-742">_**Afbeelding 18:** toevoegen Hallo server of de virtuele machine de naam van het eerste clusterknooppunt Hallo_</span><span class="sxs-lookup"><span data-stu-id="b930e-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="b930e-743">Voer Hallo netwerknaam (virtuele host-naam) van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Afbeelding 19: Voer de clusternaam Hallo][sap-ha-guide-figure-3008]

  <span data-ttu-id="b930e-745">_**Afbeelding 19:** Enter Hallo clusternaam_</span><span class="sxs-lookup"><span data-stu-id="b930e-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="b930e-746">Nadat u Hallo cluster hebt gemaakt, voert u een clustervalidatietest.</span><span class="sxs-lookup"><span data-stu-id="b930e-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Afbeelding van 20: Hallo cluster validatiecontrole uitvoeren][sap-ha-guide-figure-3009]

  <span data-ttu-id="b930e-748">_**Afbeelding van 20:** Hallo cluster validatiecontrole uitvoeren_</span><span class="sxs-lookup"><span data-stu-id="b930e-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="b930e-749">U kunt waarschuwingen met betrekking tot schijven op dit moment in Hallo proces negeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="b930e-750">U voegt dat een bestandssharewitness en Hallo SIOS gedeelde schijven later.</span><span class="sxs-lookup"><span data-stu-id="b930e-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="b930e-751">In dit stadium hoeft u geen tooworry over het hebben van een quorum.</span><span class="sxs-lookup"><span data-stu-id="b930e-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Afbeelding 21: Er is geen quorumschijf is gevonden.][sap-ha-guide-figure-3010]

  <span data-ttu-id="b930e-753">_**Afbeelding 21:** geen quorumschijf is gevonden_</span><span class="sxs-lookup"><span data-stu-id="b930e-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Afbeelding 22: Core cluster-bron moet een nieuw IP-adres][sap-ha-guide-figure-3011]

  <span data-ttu-id="b930e-755">_**Afbeelding 22:** Core cluster-bron moet een nieuw IP-adres_</span><span class="sxs-lookup"><span data-stu-id="b930e-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="b930e-756">Hallo IP-adres van Hallo core cluster-service wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b930e-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="b930e-757">Hallo-cluster starten niet totdat u Hallo IP-adres van de clusterservice Hallo-core, wijzigt omdat Hallo IP-adres van de server Hallo tooone van knooppunten van de virtuele machine Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="b930e-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="b930e-758">Dit doen op Hallo **eigenschappen** pagina van Hallo core cluster-service van IP-resource.</span><span class="sxs-lookup"><span data-stu-id="b930e-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="b930e-759">Bijvoorbeeld, moeten we tooassign een IP-adres (in ons voorbeeld **10.0.0.42**) voor de naam van de virtuele host cluster Hallo **pr1-ASC's-vir**.</span><span class="sxs-lookup"><span data-stu-id="b930e-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Afbeelding 23: In Hallo eigenschappen in het dialoogvenster Hallo IP-adres wijzigen][sap-ha-guide-figure-3012]

  <span data-ttu-id="b930e-761">_**Afbeelding 23:** In Hallo **eigenschappen** in het dialoogvenster, wijziging Hallo IP-adres_</span><span class="sxs-lookup"><span data-stu-id="b930e-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Afbeelding 24: Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen][sap-ha-guide-figure-3013]

  <span data-ttu-id="b930e-763">_**Afbeelding 24:** Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen_</span><span class="sxs-lookup"><span data-stu-id="b930e-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="b930e-764">Hallo virtuele host clusternaam online brengen.</span><span class="sxs-lookup"><span data-stu-id="b930e-764">Bring hello cluster virtual host name online.</span></span>

  ![Afbeelding 25: Core de clusterservice actief is en uitgevoerd en Hello Corrigeer IP-adres][sap-ha-guide-figure-3014]

  <span data-ttu-id="b930e-766">_**Afbeelding 25:** core de clusterservice actief is en uitgevoerd, en met Hallo Corrigeer IP-adres_</span><span class="sxs-lookup"><span data-stu-id="b930e-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="b930e-767">De tweede clusterknooppunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b930e-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="b930e-768">Nu Hallo core cluster-service actief is, kunt u de tweede clusterknooppunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b930e-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Afbeelding 26: Hallo tweede clusterknooppunt toevoegen][sap-ha-guide-figure-3015]

  <span data-ttu-id="b930e-770">_**Afbeelding 26:** toevoegen Hallo tweede clusterknooppunt_</span><span class="sxs-lookup"><span data-stu-id="b930e-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="b930e-771">Voer een naam voor Hallo tweede knooppunt clusterhost.</span><span class="sxs-lookup"><span data-stu-id="b930e-771">Enter a name for hello second cluster node host.</span></span>

  ![Afbeelding 27: Voer Hallo tweede hostnaam voor het clusterknooppunt][sap-ha-guide-figure-3016]

  <span data-ttu-id="b930e-773">_**Afbeelding 27:** Enter Hallo tweede hostnaam voor het clusterknooppunt_</span><span class="sxs-lookup"><span data-stu-id="b930e-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b930e-774">Zorg dat Hallo **Voeg alle in aanmerking komende opslag toohello cluster** selectievakje **niet** geselecteerde.</span><span class="sxs-lookup"><span data-stu-id="b930e-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Afbeelding 28: Schakel niet Hallo selectievakje][sap-ha-guide-figure-3017]

  <span data-ttu-id="b930e-776">_**Afbeelding 28:** doen **niet** Selecteer Hallo selectievakje_</span><span class="sxs-lookup"><span data-stu-id="b930e-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="b930e-777">U kunt waarschuwingen over quorum en schijven negeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="b930e-778">Stelt u Hallo quorum en -share Hallo schijf later, zoals beschreven in [SIOS DataKeeper Cluster Edition installeren voor de clusterschijf share SAP ASC's / SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="b930e-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Afbeelding 29: Negeren van waarschuwingen over Hallo schijf quorum][sap-ha-guide-figure-3018]

  <span data-ttu-id="b930e-780">_**Afbeelding 29:** negeren van waarschuwingen over Hallo schijf quorum_</span><span class="sxs-lookup"><span data-stu-id="b930e-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="b930e-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Een cluster bestandsshare-witness configureren</span><span class="sxs-lookup"><span data-stu-id="b930e-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="b930e-782">Een cluster bestandsshare-witness configureren, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b930e-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="b930e-783">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="b930e-783">Creating a file share</span></span>
- <span data-ttu-id="b930e-784">Instelling Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="b930e-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="b930e-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="b930e-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="b930e-786">Selecteer een bestandssharewitness in plaats van een quorumschijf.</span><span class="sxs-lookup"><span data-stu-id="b930e-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="b930e-787">SIOS DataKeeper ondersteunt deze optie.</span><span class="sxs-lookup"><span data-stu-id="b930e-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="b930e-788">In Hallo voorbeelden in dit artikel is het Hallo bestandssharewitness op Hallo Active Directory en DNS-server die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="b930e-789">Hallo bestandsshare-witness wordt aangeroepen **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="b930e-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="b930e-790">Omdat u zou een VPN-verbinding tooAzure (via Site-naar-Site VPN- of Azure ExpressRoute) hebt geconfigureerd, kunt u met uw Active Directory en DNS-service is on-premises en is niet geschikt toorun een bestand witness delen.</span><span class="sxs-lookup"><span data-stu-id="b930e-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b930e-791">Als uw Active Directory en DNS-service wordt uitgevoerd alleen lokale, niet de bestandsshare-witness configureren op Hallo Active Directory en DNS-Windows-besturingssysteem die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="b930e-792">Netwerklatentie tussen clusterknooppunten uitgevoerd in Azure en Active Directory en DNS-on-premises mogelijk te groot zijn en leiden tot problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="b930e-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="b930e-793">Worden ervoor tooconfigure Hallo bestandssharewitness op een virtuele machine van Azure met sluiten toohello clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="b930e-794">Hallo quorumstation moet ten minste 1024 MB vrije ruimte.</span><span class="sxs-lookup"><span data-stu-id="b930e-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="b930e-795">We raden 2048 MB aan vrije ruimte voor Hallo quorum-station aan.</span><span class="sxs-lookup"><span data-stu-id="b930e-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="b930e-796">Hallo clusternaamobject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b930e-796">Add hello cluster name object.</span></span>

  ![Afbeelding 30: Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen][sap-ha-guide-figure-3019]

  <span data-ttu-id="b930e-798">_**Afbeelding 30:** Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen_</span><span class="sxs-lookup"><span data-stu-id="b930e-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="b930e-799">Zorg dat Hallo machtigingen Hallo autoriteit toochange gegevens in Hallo share voor Hallo clusternaamobject bevatten (in ons voorbeeld **pr1-ASC's-vir$**).</span><span class="sxs-lookup"><span data-stu-id="b930e-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="b930e-800">tooadd hello cluster naam toohello objectenlijst, selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b930e-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="b930e-801">Hallo filter toocheck voor computerobjecten in toevoeging toothose wordt weergegeven in afbeelding 31 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b930e-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Afbeelding 31: Hallo objecttypen tooinclude computers wijzigen][sap-ha-guide-figure-3020]

  <span data-ttu-id="b930e-803">_**Afbeelding 31:** Hallo objecttypen tooinclude computers wijzigen_</span><span class="sxs-lookup"><span data-stu-id="b930e-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Afbeelding 32: Selectievakje Hallo Computers][sap-ha-guide-figure-3021]

  <span data-ttu-id="b930e-805">_**Afbeelding 32:** Selecteer Hallo **Computers** selectievakje_</span><span class="sxs-lookup"><span data-stu-id="b930e-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="b930e-806">Voer Hallo clusternaamobject zoals in afbeelding 31.</span><span class="sxs-lookup"><span data-stu-id="b930e-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="b930e-807">Omdat Hallo record al is gemaakt, kunt u Hallo-machtigingen kunt wijzigen, zoals wordt weergegeven in afbeelding 30.</span><span class="sxs-lookup"><span data-stu-id="b930e-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="b930e-808">Selecteer Hallo **beveiliging** tabblad van het Hallo-share- en vervolgens moet u meer gedetailleerde machtigingen voor Hallo clusternaamobject.</span><span class="sxs-lookup"><span data-stu-id="b930e-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Afbeelding 33: Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum][sap-ha-guide-figure-3022]

  <span data-ttu-id="b930e-810">_**Afbeelding 33:** Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum_</span><span class="sxs-lookup"><span data-stu-id="b930e-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="b930e-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Set Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="b930e-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="b930e-812">Open Hallo Wizard configureren Quorum-instelling.</span><span class="sxs-lookup"><span data-stu-id="b930e-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Afbeelding 34: Start Hallo Wizard instelling clusterquorum configureren][sap-ha-guide-figure-3023]

  <span data-ttu-id="b930e-814">_**Afbeelding 34:** Start de Wizard clusterquorum configureren instelling Hallo_</span><span class="sxs-lookup"><span data-stu-id="b930e-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="b930e-815">Op Hallo **quorumconfiguratie selecteren** pagina **hello quorumwitness selecteren**.</span><span class="sxs-lookup"><span data-stu-id="b930e-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Afbeelding 35: Quorumconfiguraties u kunt kiezen uit][sap-ha-guide-figure-3024]

  <span data-ttu-id="b930e-817">_**Afbeelding 35:** quorumconfiguraties kunt u kiezen uit_</span><span class="sxs-lookup"><span data-stu-id="b930e-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="b930e-818">Op Hallo **Quorumwitness selecteren** pagina **een bestandssharewitness configureren**.</span><span class="sxs-lookup"><span data-stu-id="b930e-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Afbeelding 36: Selecteer Hallo bestandsshare-witness][sap-ha-guide-figure-3025]

  <span data-ttu-id="b930e-820">_**Afbeelding 36:** Hallo bestandssharewitness selecteren_</span><span class="sxs-lookup"><span data-stu-id="b930e-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="b930e-821">Voer Hallo UNC-pad toohello bestandsshare (in ons voorbeeld \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="b930e-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="b930e-822">een lijst met Hallo wijzigingen kunt u, selecteer toosee **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b930e-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Afbeelding 37: Hallo bestandsshare-locatie voor de witness-share Hallo definiëren][sap-ha-guide-figure-3026]

  <span data-ttu-id="b930e-824">_**Afbeelding 37:** Hallo bestandsshare-locatie voor de witness-share Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="b930e-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="b930e-825">Selecteer Hallo wijzigingen die u wilt en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b930e-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="b930e-826">U moet toosuccessfully Hallo clusterconfiguratie configureren zoals wordt weergegeven in afbeelding 38.</span><span class="sxs-lookup"><span data-stu-id="b930e-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Afbeelding 38: Bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster][sap-ha-guide-figure-3027]

  <span data-ttu-id="b930e-828">_**Afbeelding 38:** bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster_</span><span class="sxs-lookup"><span data-stu-id="b930e-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="b930e-829">Na de installatie is Windows Failover Cluster hello, moeten de wijzigingen toobe toosome drempelwaarden tooadapt failover detectie tooconditions aangebracht in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="b930e-830">Hallo parameters toobe gewijzigd, worden beschreven in deze blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="b930e-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="b930e-831">Ervan uitgaande dat uw twee virtuele machines die bouwen Hallo zijn Windows Cluster-configuratie voor ASC's / SCS in hetzelfde SubNet hello, hello volgende parameters moeten toobe gewijzigd toothese waarden:</span><span class="sxs-lookup"><span data-stu-id="b930e-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="b930e-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="b930e-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="b930e-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="b930e-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="b930e-834">Deze instellingen zijn getest met klanten en een goede inbreuk toobe robuust genoeg opgegeven Hallo-een-zijde.</span><span class="sxs-lookup"><span data-stu-id="b930e-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="b930e-835">Op Hallo daarentegen deze instellingen zijn bieden snel genoeg failover in een echte foutcondities op SAP-software of het knooppunt/VM-fout.</span><span class="sxs-lookup"><span data-stu-id="b930e-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="b930e-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS clusterschijf delen installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="b930e-837">U hebt nu een werkende configuratie van Windows Server Failover Clustering in Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="b930e-838">Maar tooinstall een SAP ASC's / SCS-exemplaar, moet u een gedeelde schijf-resource.</span><span class="sxs-lookup"><span data-stu-id="b930e-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="b930e-839">U kunt Hallo gedeelde schijfbronnen die u nodig in Azure maken.</span><span class="sxs-lookup"><span data-stu-id="b930e-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="b930e-840">SIOS DataKeeper Cluster Edition is een oplossing van derden, kunt u de schijfbronnen toocreate gedeeld.</span><span class="sxs-lookup"><span data-stu-id="b930e-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="b930e-841">Het installeren van SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS omvat share clusterschijf deze taken:</span><span class="sxs-lookup"><span data-stu-id="b930e-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="b930e-842">Hallo .NET Framework 3.5 toevoegen</span><span class="sxs-lookup"><span data-stu-id="b930e-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="b930e-843">SIOS DataKeeper installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="b930e-844">SIOS DataKeeper instellen</span><span class="sxs-lookup"><span data-stu-id="b930e-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="b930e-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Hallo .NET Framework 3.5 toevoegen</span><span class="sxs-lookup"><span data-stu-id="b930e-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="b930e-846">Hallo Microsoft .NET Framework 3.5 is niet automatisch geactiveerd of Windows Server 2012 R2 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b930e-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="b930e-847">Omdat SIOS DataKeeper Hallo .NET Framework toobe op alle knooppunten die u vereist op DataKeeper installeert, moet u Hallo .NET Framework 3.5 installeren op Hallo gastbesturingssysteem van alle virtuele machines in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="b930e-848">Er zijn twee manieren tooadd Hallo .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="b930e-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="b930e-849">Gebruik Wizard Hallo toevoegen functies en onderdelen in Windows zoals in afbeelding 39.</span><span class="sxs-lookup"><span data-stu-id="b930e-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Afbeelding 39: Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3028]

  <span data-ttu-id="b930e-851">_**Afbeelding 39:** installeren Hallo .NET Framework 3.5 met behulp van de Wizard Hallo toevoegen functies en onderdelen_</span><span class="sxs-lookup"><span data-stu-id="b930e-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Afbeelding 40: Installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3029]

  <span data-ttu-id="b930e-853">_**Afbeelding 40:** installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen_</span><span class="sxs-lookup"><span data-stu-id="b930e-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="b930e-854">Gebruik Hallo opdrachtregelprogramma dism.exe.</span><span class="sxs-lookup"><span data-stu-id="b930e-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="b930e-855">Voor dit type installatie moet u tooaccess Hallo SxS-map op de installatiemedia voor Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b930e-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="b930e-856">Typ bij een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="b930e-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="b930e-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="b930e-858">SIOS DataKeeper Cluster Edition installeren op elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b930e-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="b930e-859">toocreate virtuele gedeelde opslag met SIOS DataKeeper, maakt u een gesynchroniseerde mirror en vervolgens simuleren gedeelde clusteropslag.</span><span class="sxs-lookup"><span data-stu-id="b930e-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="b930e-860">Voordat u Hallo SIOS software installeert, maken de domeingebruiker Hallo **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="b930e-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-861">Hallo toevoegen **DataKeeperSvc** gebruiker toohello **lokale beheerder** groep op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="b930e-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="b930e-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="b930e-863">Hallo SIOS software installeren op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS installatieprogramma][sap-ha-guide-figure-3030]

  ![Afbeelding 41: Eerste pagina van Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3031]

  <span data-ttu-id="b930e-866">_**Afbeelding 41:** eerste pagina van Hallo SIOS DataKeeper installatie_</span><span class="sxs-lookup"><span data-stu-id="b930e-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="b930e-867">Selecteer Hallo in het dialoogvenster wordt weergegeven in afbeelding 42 **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b930e-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Afbeelding 42: DataKeeper informeert u dat een service wordt uitgeschakeld][sap-ha-guide-figure-3032]

  <span data-ttu-id="b930e-869">_**Afbeelding 42:** DataKeeper informeert u dat een service wordt uitgeschakeld_</span><span class="sxs-lookup"><span data-stu-id="b930e-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="b930e-870">Hallo in het dialoogvenster wordt weergegeven in afbeelding 43 wordt aangeraden dat u selecteert **domein of de Server account**.</span><span class="sxs-lookup"><span data-stu-id="b930e-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Afbeelding 43: Selectie van de de gebruiker voor SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="b930e-872">_**Afbeelding 43:** gebruikersselectie voor SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="b930e-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="b930e-873">Voer Hallo account domeingebruikersnaam en wachtwoorden op dat u hebt gemaakt voor SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="b930e-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Afbeelding 44: Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3034]

  <span data-ttu-id="b930e-875">_**Afbeelding 44:** Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie_</span><span class="sxs-lookup"><span data-stu-id="b930e-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="b930e-876">De licentiesleutel Hallo voor uw exemplaar SIOS DataKeeper zoals in afbeelding 45 installeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Afbeelding 45: Voer uw licentiecode SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="b930e-878">_**Afbeelding 45:** uw licentiesleutel SIOS DataKeeper invoeren_</span><span class="sxs-lookup"><span data-stu-id="b930e-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="b930e-879">Wanneer u wordt gevraagd, moet u Hallo virtuele machine opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="b930e-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="b930e-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper instellen</span><span class="sxs-lookup"><span data-stu-id="b930e-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="b930e-881">Nadat u SIOS DataKeeper op beide knooppunten hebt geïnstalleerd, moet u toostart Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="b930e-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="b930e-882">Hallo-doel van Hallo-configuratie is toohave synchrone gegevensreplicatie tussen Hallo extra virtuele harde schijven gekoppeld tooeach van Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="b930e-883">Hallo DataKeeper beheer en hulpprogramma voor serverconfiguratie starten en selecteer vervolgens **verbinding maken met Server**.</span><span class="sxs-lookup"><span data-stu-id="b930e-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="b930e-884">(In de afbeelding 46 deze optie is met een rode cirkel.)</span><span class="sxs-lookup"><span data-stu-id="b930e-884">(In Figure 46, this option is circled in red.)</span></span>

  ![46 afbeelding: De SIOS DataKeeper beheer en het hulpprogramma voor serverconfiguratie][sap-ha-guide-figure-3036]

  <span data-ttu-id="b930e-886">_**Afbeelding 46:** SIOS DataKeeper beheer en de configuratie-hulpprogramma_</span><span class="sxs-lookup"><span data-stu-id="b930e-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="b930e-887">Hallo naam invoeren of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en, in een tweede stap van de tweede Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Afbeelding 47: Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en in een tweede stap van het tweede knooppunt Hallo][sap-ha-guide-figure-3037]

  <span data-ttu-id="b930e-889">_**Afbeelding 47:** Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma verbinding moet maken, en in een tweede stap van het tweede knooppunt Hallo_</span><span class="sxs-lookup"><span data-stu-id="b930e-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="b930e-890">Hallo replicatie taak tussen twee knooppunten Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="b930e-890">Create hello replication job between hello two nodes.</span></span>

  ![Afbeelding van 48: Een replicatie-taak maken][sap-ha-guide-figure-3038]

  <span data-ttu-id="b930e-892">_**Afbeelding van 48:** een replicatie-taak maken_</span><span class="sxs-lookup"><span data-stu-id="b930e-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="b930e-893">Een wizard leidt u door het Hallo-proces voor het maken van een taak voor replicatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="b930e-894">Hallo-naam, de TCP/IP-adres en de schijfvolume van het bronknooppunt Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="b930e-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Afbeelding 49: Hallo-naam van Hallo replicatie taak definiëren][sap-ha-guide-figure-3039]

  <span data-ttu-id="b930e-896">_**Afbeelding 49:** definiëren Hallo-naam van Hallo replicatie taak_</span><span class="sxs-lookup"><span data-stu-id="b930e-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Afbeelding 50: Basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3040]

  <span data-ttu-id="b930e-898">_**Afbeelding 50:** basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="b930e-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="b930e-899">Hallo-naam, de TCP/IP-adres en de schijfvolume van het doelknooppunt Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="b930e-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Afbeelding 51: Basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3041]

  <span data-ttu-id="b930e-901">_**Afbeelding 51:** basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="b930e-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="b930e-902">Hallo compressie algoritmen definiëren.</span><span class="sxs-lookup"><span data-stu-id="b930e-902">Define hello compression algorithms.</span></span> <span data-ttu-id="b930e-903">In ons voorbeeld is het raadzaam dat u Hallo replicatiestroom comprimeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="b930e-904">Met name in situaties hersynchronisatie minder Hallo-compressie van Hallo replicatiestroom aanzienlijk hersynchronisatie-tijd.</span><span class="sxs-lookup"><span data-stu-id="b930e-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="b930e-905">Houd er rekening mee dat compressie Hallo CPU en RAM-geheugen van een virtuele machine verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b930e-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="b930e-906">Als Hallo compressie snelheid toeneemt, dus Hallo volume aan CPU-resources die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b930e-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="b930e-907">Ook kunt u aanpassen deze instelling later.</span><span class="sxs-lookup"><span data-stu-id="b930e-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="b930e-908">Een andere instelling die u moet toocheck is of Hallo replicatie synchroon of asynchroon.</span><span class="sxs-lookup"><span data-stu-id="b930e-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="b930e-909">*Wanneer u SAP ASC's / SCS configuraties beveiligt, moet u synchrone replicatie*.</span><span class="sxs-lookup"><span data-stu-id="b930e-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Afbeelding 52: Replicatiedetails definiëren][sap-ha-guide-figure-3042]

  <span data-ttu-id="b930e-911">_**Afbeelding 52:** replicatiedetails definiëren_</span><span class="sxs-lookup"><span data-stu-id="b930e-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="b930e-912">Definieer of Hallo volume die is gerepliceerd door Hallo taak vertegenwoordigde tooa Windows Server Failover Clustering clusterconfiguratie als gedeelde schijf moet zijn.</span><span class="sxs-lookup"><span data-stu-id="b930e-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="b930e-913">Hallo SAP ASC's / SCS configuratie, selecteert u **Ja** zodat Hallo Windows cluster ziet Hallo gerepliceerde volume als een gedeelde schijf die kan worden gebruikt als een clustervolume.</span><span class="sxs-lookup"><span data-stu-id="b930e-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Afbeelding 53: Selecteer Ja tooset Hallo gerepliceerd volume als een clustervolume][sap-ha-guide-figure-3043]

  <span data-ttu-id="b930e-915">_**Afbeelding 53:** Selecteer **Ja** tooset Hallo gerepliceerd volume als een clustervolume_</span><span class="sxs-lookup"><span data-stu-id="b930e-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="b930e-916">Nadat Hallo volume is gemaakt, ziet u Hallo DataKeeper beheer en de configuratie-hulpprogramma dat taak Hallo-replicatie is actief.</span><span class="sxs-lookup"><span data-stu-id="b930e-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Afbeelding 54: Synchroon spiegelen van DataKeeper voor Hallo SAP ASC's / SCS share schijf actief is.][sap-ha-guide-figure-3044]

  <span data-ttu-id="b930e-918">_**Afbeelding 54:** DataKeeper synchroon spiegelen voor hello SAP ASC's / SCS schijf delen is actief_</span><span class="sxs-lookup"><span data-stu-id="b930e-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="b930e-919">Hallo-schijf als een schijf DataKeeper weergegeven Failoverclusterbeheer nu zoals in afbeelding 55.</span><span class="sxs-lookup"><span data-stu-id="b930e-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Afbeelding 55: Failover Cluster Manager toont Hallo-schijf die DataKeeper gerepliceerd][sap-ha-guide-figure-3045]

  <span data-ttu-id="b930e-921">_**Afbeelding 55:** Failover Cluster Manager toont Hallo schijf die is gerepliceerd DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="b930e-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="b930e-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Hallo SAP NetWeaver systeem installeert</span><span class="sxs-lookup"><span data-stu-id="b930e-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="b930e-923">Hallo DBMS setup won't worden beschreven omdat instellingen variëren, afhankelijk van Hallo DBMS systeem u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b930e-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="b930e-924">Echter, gaan we ervan uit dat hoge beschikbaarheid weergegeven met de Hallo DBMS worden aangepakt met Hallo functionaliteiten Hallo verschillende DBMS leveranciers ondersteuning voor Azure.</span><span class="sxs-lookup"><span data-stu-id="b930e-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="b930e-925">Bijvoorbeeld altijd op of database mirroring voor SQL Server en Oracle Data Guard voor Oracle-databases.</span><span class="sxs-lookup"><span data-stu-id="b930e-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="b930e-926">We toevoegen niet meer bescherming toohello DBMS in Hallo scenario we in dit artikel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b930e-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="b930e-927">Er zijn geen speciale overwegingen bij verschillende DBMS services met dit soort clusterconfiguratie SAP ASC's / SCS in Azure communiceren.</span><span class="sxs-lookup"><span data-stu-id="b930e-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-928">Hallo installatieprocedures van SAP NetWeaver ABAP systemen, Java-systemen en ABAP + Java systemen zijn bijna identiek.</span><span class="sxs-lookup"><span data-stu-id="b930e-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="b930e-929">Hallo belangrijkste verschil is dat een SAP ABAP systeem een exemplaar van de ASC's heeft.</span><span class="sxs-lookup"><span data-stu-id="b930e-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="b930e-930">Hallo SAP Java systeem heeft een SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="b930e-931">Hallo SAP ABAP + Java systeem heeft een exemplaar van de ASC's en één SCS-exemplaar in Hallo dezelfde Microsoft failover cluster-groep.</span><span class="sxs-lookup"><span data-stu-id="b930e-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="b930e-932">Eventuele verschillen installatie voor elke installatie SAP NetWeaver stack worden expliciet vermeld.</span><span class="sxs-lookup"><span data-stu-id="b930e-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="b930e-933">Alle andere onderdelen zijn dezelfde hello, kunt u aannemen.</span><span class="sxs-lookup"><span data-stu-id="b930e-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="b930e-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>SAP installeren met een hoge beschikbaarheid ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b930e-935">Zorg ervoor dat geen tooplace uw pagina bestand op DataKeeper gespiegelde volumes.</span><span class="sxs-lookup"><span data-stu-id="b930e-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="b930e-936">DataKeeper biedt geen ondersteuning voor gespiegelde volumes.</span><span class="sxs-lookup"><span data-stu-id="b930e-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="b930e-937">U kunt uw wisselbestand op Hallo tijdelijke station D van een virtuele machine van Azure, laten Hallo standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="b930e-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="b930e-938">Als deze nog niet is gebeurd, verplaatst u Hallo Windows pagina bestand toodrive D van uw Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="b930e-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="b930e-939">SAP installeren met een exemplaar van de ASC's / SCS hoge beschikbaarheid, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b930e-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="b930e-940">Maken van een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar</span><span class="sxs-lookup"><span data-stu-id="b930e-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="b930e-941">Eerste Hallo SAP-clusterknooppunt installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="b930e-942">Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="b930e-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="b930e-943">Een testpoort toevoegen</span><span class="sxs-lookup"><span data-stu-id="b930e-943">Adding a probe port</span></span>
- <span data-ttu-id="b930e-944">Hallo Windows firewall-testpoort openen</span><span class="sxs-lookup"><span data-stu-id="b930e-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="b930e-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="b930e-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="b930e-946">Maak een DNS-vermelding voor de naam van de virtuele host Hallo van Hallo ASC's / SCS exemplaar in Hallo Windows DNS-beheer.</span><span class="sxs-lookup"><span data-stu-id="b930e-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b930e-947">Hallo IP-adres dat u de naam van de virtuele host toohello Hallo ASC's / SCS-exemplaar moet toewijzen Hallo dezelfde als Hallo IP-adres dat aan u toegewezen tooAzure Load Balancer (**<*SID*> - lb - ASC's **).</span><span class="sxs-lookup"><span data-stu-id="b930e-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="b930e-948">Hallo IP-adres van de virtuele SAP ASC's / SCS Hallo-hostnaam (**pr1 ASC's sap**) is dezelfde als Hallo IP-adres van de Load Balancer van Azure Hallo (**pr1-lb-ASC's**).</span><span class="sxs-lookup"><span data-stu-id="b930e-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Afbeelding 56: Definieer Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres][sap-ha-guide-figure-3046]

  <span data-ttu-id="b930e-950">_**Afbeelding 56:** Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres definiëren_</span><span class="sxs-lookup"><span data-stu-id="b930e-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="b930e-951">toodefine hello IP-adres is toegewezen toohello naam virtuele host op, selecteer **DNS-beheer** > **domein**.</span><span class="sxs-lookup"><span data-stu-id="b930e-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![57 afbeelding: De nieuwe virtuele naam en het TCP/IP-adres voor de clusterconfiguratie SAP ASC's / SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="b930e-953">_**Afbeelding 57:** nieuwe virtuele naam en het TCP/IP-adres voor SAP ASC's / SCS-clusterconfiguratie_</span><span class="sxs-lookup"><span data-stu-id="b930e-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="b930e-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Eerste Hallo SAP-clusterknooppunt installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="b930e-955">Hallo eerste cluster knooppunt optie op clusterknooppunt A. uitvoeren Bijvoorbeeld: op Hallo **pr1-ASC's-0** host.</span><span class="sxs-lookup"><span data-stu-id="b930e-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="b930e-956">tookeep Hallo-standaardpoorten voor hello Azure interne load balancer, selecteren:</span><span class="sxs-lookup"><span data-stu-id="b930e-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="b930e-957">**ABAP system**: **ASC's** exemplaar nummer **00**</span><span class="sxs-lookup"><span data-stu-id="b930e-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="b930e-958">**Java-systeem**: **SCS** exemplaar nummer **01**</span><span class="sxs-lookup"><span data-stu-id="b930e-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="b930e-959">**ABAP + Java system**: **ASC's** exemplaar nummer **00** en **SCS** exemplaar nummer **01**</span><span class="sxs-lookup"><span data-stu-id="b930e-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="b930e-960">toouse exemplaar getallen andere dan 00 voor Hallo ABAP ASCS exemplaar en 01 voor Hallo Java SCS exemplaar, moet u eerst toochange hello Azure interne load balancer standaard load-balancingregels beschreven in [wijziging Hallo ASC's / SCS standaard laden regels voor hello Azure interne load balancer Balancing][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="b930e-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="b930e-961">Hello worden niet volgende enkele taken beschreven in Hallo standaard SAP documentatie voor de installatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-962">Hallo SAP installatie documentatie wordt beschreven hoe tooinstall Hallo eerste ASC's / SCS-clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b930e-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="b930e-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="b930e-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="b930e-964">U moet een nieuwe profiel-parameter tooadd.</span><span class="sxs-lookup"><span data-stu-id="b930e-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="b930e-965">Hallo profiel parameter voorkomt dat verbindingen tussen processen SAP en Hallo in de wachtrij plaatsen server af te sluiten wanneer ze niet actief is te lang zijn.</span><span class="sxs-lookup"><span data-stu-id="b930e-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="b930e-966">Gezegd Hallo probleem scenario in [registervermeldingen toe te voegen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="b930e-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="b930e-967">In deze sectie geïntroduceerd we ook twee wijzigingen toosome eenvoudige TCP/IP-verbindingsparameters.</span><span class="sxs-lookup"><span data-stu-id="b930e-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="b930e-968">In een tweede stap moet u tooset Hallo in de wachtrij plaatsen server toosend een `keep_alive` signaal zodat Hallo verbindingen niet hello Azure interne load balancer niet-actieve drempelwaarde bereikt.</span><span class="sxs-lookup"><span data-stu-id="b930e-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="b930e-969">toomodify hello SAP-profiel van Hallo ASC's / SCS exemplaar:</span><span class="sxs-lookup"><span data-stu-id="b930e-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="b930e-970">Dit profiel parameter toohello SAP ASC's / SCS exemplaar profiel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b930e-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="b930e-971">In ons voorbeeld Hallo pad als volgt:</span><span class="sxs-lookup"><span data-stu-id="b930e-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="b930e-972">Bijvoorbeeld toohello SAP SCS exemplaar profiel en het bijbehorende pad:</span><span class="sxs-lookup"><span data-stu-id="b930e-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="b930e-973">tooapply hello wijzigingen, Hallo SAP ASC's /SCS exemplaar opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="b930e-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="b930e-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Een testpoort toevoegen</span><span class="sxs-lookup"><span data-stu-id="b930e-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="b930e-975">Hallo interne load balancer-test functionaliteit toomake Hallo clusteroplossing configuratiewerk gebruiken met Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b930e-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="b930e-976">Hello Azure interne load balancer distribueert meestal Hallo binnenkomende werkbelasting gelijkmatig tussen deelnemende virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b930e-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="b930e-977">Echter werkt dat niet in bepaalde clusterconfiguraties omdat er slechts één exemplaar actief is.</span><span class="sxs-lookup"><span data-stu-id="b930e-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="b930e-978">Hallo andere exemplaar is passieve en kan niet alle Hallo werkbelasting accepteren.</span><span class="sxs-lookup"><span data-stu-id="b930e-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="b930e-979">Een test-functionaliteit helpt wanneer hello Azure interne load balancer wordt toegewezen alleen tooan actieve sessie werkt.</span><span class="sxs-lookup"><span data-stu-id="b930e-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="b930e-980">Hallo interne load balancer kan met Hallo test functionaliteit detecteren welke exemplaren actief zijn en vervolgens de doelinstantie alleen Hallo met Hallo werklast.</span><span class="sxs-lookup"><span data-stu-id="b930e-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="b930e-981">tooadd een testpoort:</span><span class="sxs-lookup"><span data-stu-id="b930e-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="b930e-982">Controleer de huidige Hallo **ProbePort** instellen door het volgende PowerShell-opdracht Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="b930e-983">Deze niet binnen één Hallo virtuele machines worden uitgevoerd in Hallo clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b930e-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="b930e-984">Definieer een testpoort.</span><span class="sxs-lookup"><span data-stu-id="b930e-984">Define a probe port.</span></span> <span data-ttu-id="b930e-985">Hallo test standaardpoortnummer is **0**.</span><span class="sxs-lookup"><span data-stu-id="b930e-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="b930e-986">In ons voorbeeld gebruiken we de testpoort **62000**.</span><span class="sxs-lookup"><span data-stu-id="b930e-986">In our example, we use probe port **62000**.</span></span>

  ![Afbeelding 58: Hallo cluster configuratie de testpoort is 0 standaard][sap-ha-guide-figure-3048]

  <span data-ttu-id="b930e-988">_**Afbeelding 58:** Hallo cluster configuration test standaardpoort is 0_</span><span class="sxs-lookup"><span data-stu-id="b930e-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="b930e-989">Hallo-poortnummer is gedefinieerd in SAP Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b930e-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="b930e-990">U kunt Hallo poortnummer in PowerShell kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="b930e-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="b930e-991">een nieuwe ProbePort-waarde voor Hallo tooset  **SAP <*SID*> IP-** clusterbron, Hallo volgende PowerShell-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b930e-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="b930e-992">Hallo PowerShell variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b930e-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="b930e-993">Nadat het Hallo-script wordt uitgevoerd, moet u na vragen aan gebruiker toorestart Hallo SAP cluster tooactivate Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b930e-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="b930e-994">Nadat u Hallo brengt  **SAP <*SID*> ** cluster online rol, Controleer **ProbePort** toohello nieuwe waarde is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b930e-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Afbeelding 59: Test Hallo cluster poort nadat u de nieuwe waarde Hallo instellen][sap-ha-guide-figure-3049]

  <span data-ttu-id="b930e-996">_**Afbeelding 59:** Probe Hallo cluster poort nadat u de nieuwe waarde Hallo instellen_</span><span class="sxs-lookup"><span data-stu-id="b930e-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="b930e-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Hallo Windows firewall-testpoort openen</span><span class="sxs-lookup"><span data-stu-id="b930e-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="b930e-998">U moet een Windows firewall-test poort op beide clusterknooppunten tooopen.</span><span class="sxs-lookup"><span data-stu-id="b930e-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="b930e-999">Gebruik Hallo script tooopen een test-poort van Windows firewall te volgen.</span><span class="sxs-lookup"><span data-stu-id="b930e-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="b930e-1000">Hallo PowerShell variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b930e-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="b930e-1001">Hallo **ProbePort** te is ingesteld,**62000**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="b930e-1002">Nu u toegang hebt tot de bestandsshare Hallo  **\\\ascsha-clsap\sapmnt** met andere hosts, zoals als van **ascsha-DBA's**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="b930e-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Hallo-database-exemplaar installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="b930e-1004">tooinstall hello database-exemplaar, voert u de Hallo-proces dat wordt beschreven in Hallo SAP-documentatie voor installatie.</span><span class="sxs-lookup"><span data-stu-id="b930e-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="b930e-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>De tweede clusterknooppunt Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="b930e-1006">tooinstall hello tweede cluster, volg de stappen Hallo in Hallo SAP installatiehandleiding.</span><span class="sxs-lookup"><span data-stu-id="b930e-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="b930e-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Hallo het starttype Hallo SAP Ebruikers Windows service-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="b930e-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="b930e-1008">Het starttype Hallo Hallo SAP Ebruikers Windows-service ook wijzigen**automatisch (vertraagd starten)** op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b930e-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Afbeelding 60: Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen][sap-ha-guide-figure-3050]

<span data-ttu-id="b930e-1010">_**Afbeelding 60:** Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen_</span><span class="sxs-lookup"><span data-stu-id="b930e-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="b930e-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Hallo SAP primaire toepassingsserver installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="b930e-1012">Hallo primaire Application Server (PAS)-exemplaar installeren <*SID*> - di - 0 op Hallo virtuele machine die u hebt opgegeven toohost Hallo Pa's.</span><span class="sxs-lookup"><span data-stu-id="b930e-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="b930e-1013">Er zijn geen afhankelijkheden op Azure of DataKeeper-specifieke instellingen.</span><span class="sxs-lookup"><span data-stu-id="b930e-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="b930e-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Hallo SAP aanvullende toepassingsserver installeren</span><span class="sxs-lookup"><span data-stu-id="b930e-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="b930e-1015">Een SAP aanvullende Application Server (AAS) installeren op alle Hallo virtuele machines dat u hebt aangewezen toohost een SAP Application Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b930e-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="b930e-1016">Bijvoorbeeld: op <*SID*> - di - 1 te <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="b930e-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="b930e-1017">Dit is voltooid Hallo-installatie van een hoge beschikbaarheid SAP NetWeaver-systeem.</span><span class="sxs-lookup"><span data-stu-id="b930e-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="b930e-1018">Vervolgens gaat u verder met het testen van failover.</span><span class="sxs-lookup"><span data-stu-id="b930e-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="b930e-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Hallo SAP ASC's / SCS exemplaar failover en SIOS replicatie testen</span><span class="sxs-lookup"><span data-stu-id="b930e-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="b930e-1020">Het is gemakkelijk tootest en een SAP ASC's / SCS exemplaar failover en SIOS schijfreplicatie bewaken met behulp van Failoverclusterbeheer en Hallo SIOS DataKeeper beheer en de configuratie-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b930e-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="b930e-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASC's / SCS-exemplaar wordt uitgevoerd op een clusterknooppunt A</span><span class="sxs-lookup"><span data-stu-id="b930e-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="b930e-1022">Hallo **SAP PR1** clustergroep wordt uitgevoerd op een clusterknooppunt A. Bijvoorbeeld: op **pr1-ASC's-0**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="b930e-1023">Toewijzen van gedeelde Hallo schijfstation S, die deel uitmaakt van Hallo **SAP PR1** cluster groep en welk Hallo ASC's / SCS-exemplaar gebruikt, toocluster knooppunt A.</span><span class="sxs-lookup"><span data-stu-id="b930e-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Afbeelding 61: Failover Cluster Manager: Hallo SAP < SID > clustergroep wordt uitgevoerd op een clusterknooppunt A][sap-ha-guide-figure-5000]

<span data-ttu-id="b930e-1025">_**Afbeelding 61:** Failoverclusterbeheer: SAP Hallo <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt A_</span><span class="sxs-lookup"><span data-stu-id="b930e-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="b930e-1026">In het Hallo SIOS DataKeeper beheer en hulpprogramma voor serverconfiguratie ziet u dat Hallo gedeelde schijf gegevens synchroon worden gerepliceerd vanaf Hallo bron volume station S op clusterknooppunt een toohello volume doelstation S op clusterknooppunt B. Bijvoorbeeld, worden gerepliceerd van **pr1 ASC's 0 [10.0.0.40]** te**pr1-ASC's-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Afbeelding 62: In SIOS DataKeeper, repliceert u Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="b930e-1028">_**Afbeelding 62:** repliceren In SIOS DataKeeper, Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B_</span><span class="sxs-lookup"><span data-stu-id="b930e-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="b930e-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover van knooppunt A toonode B</span><span class="sxs-lookup"><span data-stu-id="b930e-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="b930e-1030">Kies een van deze opties tooinitiate een failover van Hallo SAP <*SID*> clustergroep van knooppunt A toocluster clusterknooppunt B:</span><span class="sxs-lookup"><span data-stu-id="b930e-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="b930e-1031">Gebruik Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="b930e-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="b930e-1032">Failover-Cluster PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="b930e-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="b930e-1033">Start opnieuw op een van de cluster-knooppunt in Hallo Windows-gastbesturingssysteem (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="b930e-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="b930e-1034">Start opnieuw op een van de cluster-knooppunt van hello Azure-portal (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="b930e-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="b930e-1035">Cluster-knooppunt een starten met Azure PowerShell (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="b930e-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="b930e-1036">Na een failover Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B. Bijvoorbeeld, deze wordt uitgevoerd op **pr1-ASC's-1**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Afbeelding 63: In Failoverclusterbeheer Hallo SAP < SID > clustergroep wordt uitgevoerd op het clusterknooppunt B][sap-ha-guide-figure-5002]

  <span data-ttu-id="b930e-1038">_**Afbeelding 63**: In Failoverclusterbeheer, Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B_</span><span class="sxs-lookup"><span data-stu-id="b930e-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="b930e-1039">Hallo gedeelde schijf is nu gekoppeld op cluster knooppunt B. SIOS DataKeeper is repliceren van gegevens vanaf bron volume station S op knooppunt B tootarget volume clusterstation S op clusterknooppunt A. Bijvoorbeeld, van repliceren **pr1-ASC's-1 [10.0.0.41]** te**pr1 ASC's 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="b930e-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Afbeelding 64: SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A][sap-ha-guide-figure-5003]

  <span data-ttu-id="b930e-1041">_**Afbeelding 64:** SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A_</span><span class="sxs-lookup"><span data-stu-id="b930e-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
