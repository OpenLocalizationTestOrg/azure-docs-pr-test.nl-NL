---
title: " Beheren van een processerver worden uitgevoerd in Azure (Resource Manager) | Microsoft Docs"
description: Dit artikel wordt beschreven hoe de server (Resource Manager) voor het verwerken van tooset van een failback In Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Beheren van een processerver worden uitgevoerd in Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Klassieke](./site-recovery-vmware-setup-azure-ps-classic.md)

Tijdens de failback, wordt aangeraden toodeploy processerver in Azure als er hoge latentie tussen hello Azure Virtual Network- en uw on-premises netwerk. Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo processervers worden uitgevoerd in Azure.

> [!NOTE]
> In dit artikel wordt gebruikt als u gebruikt toobe **Resource Manager** als Hallo implementatiemodel voor Hallo virtuele machines tijdens de failover. Als u hebt gebruikt **klassieke** als Hallo-implementatiemodel, stappen Hallo in [hoe tooset omhoog & Failback processerver (klassiek) configureren](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Vereisten

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Processerver op Azure implementeren
1. In de kluis Hallo > **Site Recovery-infrastructuur** (onder de kop van de 'Beheren' hello) > **configuratieservers** (onder 'Voor VMware en fysieke Machines' post), selecteer Hallo configuratieserver.
2. Klik in het Hallo configuratieserver detailpagina die wordt geopend op plusteken (+ verwerken server)

  ![Proces Servergalerie toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Op Hallo **toevoegen processerver** pagina, selecteer Hallo na waarden

  ![Proces server galerie-item toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Veldnaam**|**Waarde**|
|-|-|
|Kies waar u toodeploy uw processerver|Selecteer Hallo waarde **een failback processerver in Azure implementeren** |
|Abonnement|Selecteer hello Azure-abonnement waarbij u failover Hallo virtuele machines|
|Resourcegroep|U kunt maken van een resourcegroep toodeploy deze processerver of toodeploy Hallo processerver in een bestaande resourcegroep kiezen|
|Locatie|Selecteer hello Azure-datacenter in welke Hallo virtuele machines wanneer failover in|
|Azure-netwerk|Selecteer hello Azure virtuele Network(VNet) die virtuele machines Hallo wanneer failover in. Als u virtuele machines in meerdere Azure VNets failover, moet u een processerver geïmplementeerd per VNet|

4. Vul Hallo overige eigenschappen voor de processerver Hallo Hallo

  ![Samenvatting processerver toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Veldnaam**|**Waarde**|
|-|-|
|Servernaam|De naam van & hostnaam voor de virtuele machine van de proces-server weergeven|
| Gebruikersnaam|De naam van een gebruiker die een beheerder op deze virtuele machine wordt|
|Storage-Account|Naam van Hallo Opslagaccount waar Hallo virtuele machine virtuele schijf worden geplaatst|
|Subnet|Hallo-subnet van hello Azure VNet toowhich Hallo virtuele machine is verbonden.|
| IP-adres|IP-adres dat u Hallo proces server tooassume wilt zodra deze wordt opgestart|
5. Klik op Hallo knop OK toostart Hallo proces server virtuele machine is geïmplementeerd.

> [!NOTE]
> toobe kunnen toouse deze processerver voor failback, moet u tooregister met Hallo lokale configuratie-server.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Hallo proces server (die in Azure) tooa configuratieserver (met lokale) registreren

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Hallo versie toolatest processerver worden bijgewerkt.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Hallo processerver (uitgevoerd in Azure) van de registratie van een configuratie-Server (lokaal worden uitgevoerd)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
