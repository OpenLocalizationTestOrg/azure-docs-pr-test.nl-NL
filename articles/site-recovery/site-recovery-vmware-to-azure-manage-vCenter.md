---
title: " Een VMware vCenter server beheren in Azure Site Recovery | Microsoft Docs"
description: Dit artikel wordt beschreven hoe toevoegen en beheren van VMware vCenter in Azure Site Recovery.
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
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Beheren van VMware vCenter-Server in Azure Site Recovery
Dit artikel wordt beschreven Hallo verschillende Site Recovery-bewerkingen die kunnen worden uitgevoerd op een VMware vCenter.

## <a name="prerequisites"></a>Vereisten

**Ondersteuning van VMware vCenter- en VMware vSphere ESX-Host** | **Details** |
|--- | --- |
|**On-premises VMware-servers** | Een of meer VMware vSphere servers, 6.0, 5.5, 5.1 uitgevoerd met de meest recente updates. Servers moeten zich bevinden in Hallo netwerk als de configuratieserver hello (of een afzonderlijk processerver).<br/><br/> We raden aan een vCenter server toomanage hosts met 6.0 of 5.5 met de nieuwste updates Hallo. Alleen de functies die beschikbaar in 5.5 zijn worden ondersteund bij het implementeren van versie 6.0 zijn.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Voorbereiden van een account voor automatische detectie
Site Recovery moet toegang tooVMware voor virtuele machines Hallo proces server tooautomatically ontdekken en voor de failover en failback van virtuele machines.

* **Migreren**: als u wilt dat alleen toomigrate VMware virtuele machines tooAzure zonder ooit weer mislukt, kunt u een VMware-account gebruiken met een rol alleen-lezen. Een dergelijke rol failover kan worden uitgevoerd, maar kan niet worden beveiligde bronmachines afgesloten. Dit is niet nodig zijn voor migratie.
* **Repliceren/herstellen**: als u toodeploy volledige replicatie (repliceren, failover, failback) Hallo account moet kunnen toorun bewerkingen wilt zoals het maken en verwijderen van schijven, virtuele machine inschakelen.
* **Automatische detectie**: ten minste een alleen-lezen-account is vereist.


|**Taken** | **Vereiste account/functie** | **Machtigingen** | **Details**|
|--- | --- | --- | ---|
|**Processerver detecteert automatisch virtuele VMware-machines** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **doorgegeven toochild** toohello onderliggende objecten (vSphere-hosts, datastores, virtuele machines en netwerken)-object.|
|**Failover** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, virtuele machines en netwerken).<br/><br/> Dit is handig voor migratiedoeleinden, maar niet een volledige replicatie, failover en failback.|
|**Failover en failback** | We raden u een rol (AzureSiteRecoveryRole) met de Hallo vereist machtigingen maken en vervolgens Hallo rol tooa VMware gebruiker of groep toewijzen | Data Center-object doorgeven tooChild Object, –> rol AzureSiteRecoveryRole =<br/><br/> Datastore -> ruimte toewijzen, gegevensopslag, op laag niveau bestandsbewerkingen bladeren, bestand verwijderen, bestanden van virtuele machine bijwerken<br/><br/> Netwerk -> netwerk toewijzen<br/><br/> Resource -> toewijzen VM tooresource pool, migreren van virtuele machine is uitgeschakeld, stroomvoorziening op virtuele machine migreren<br/><br/> Taken maken taak, updatetaak -><br/><br/> Virtuele machine-configuratie ><br/><br/> Virtuele machine -> Interact -> vraag beantwoorden, apparaatverbinding, CD's configureren, configureren van diskettes, uitschakelen, inschakelen, VMware-hulpprogramma's installeren<br/><br/> Virtuele machine -> inventaris -> maken, registreren, registratie<br/><br/> Virtuele machine inrichten -> -> downloaden van de virtuele machine toestaan, toestaan uploaden van bestanden van virtuele machine<br/><br/> Virtuele machine-momentopnamen >-Remove momentopnamen > | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **doorgegeven toochild** toohello onderliggende objecten (vSphere-hosts, datastores, virtuele machines en netwerken)-object.|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Maken van een account tooconnect tooVMware vCenter Server / VMware vSphere EXSi host
1. Aanmelden bij Hallo configuratie server en start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op Hallo bureaublad geplaatst.
2. Klik op **Account toevoegen** op Hallo **Account beheren** tabblad.

  ![account toevoegen](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Geef details op Hallo-account en klik op OK tooadd Hallo-account. Hallo-account moet gemachtigd Hallo die worden vermeld in Hallo [voorbereiden van een account voor automatische detectie](#prepare-an-account-for-automatic-discovery) sectie.

  >[!NOTE]
  Het duurt ongeveer 15 minuten voor Hallo account informatie toobe up gesynchroniseerd met Hallo Site Recovery-service.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Koppelen van een VMware vCenter / vSphere VMware ESX-host (vCenter toevoegen)
* Op Hallo van Azure-portal, te bladeren*YourRecoveryServicesVault* > **Site Recovery-infrastructuur** > **Configuration servers**  >  *ConfigurationServer*
* Klik in de detailpagina Hallo configuratieserver op Hallo + vCenter knop.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Wijzigen van de gebruikte referenties tooconnect toohello vCenter-server / vSphere ESXi-host

1. Aanmelden bij Hallo configuratie server en start Hallo cspsconfigtool.exe
2. Klik op **Account toevoegen** op Hallo **Account beheren** tabblad.

  ![account toevoegen](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. De nieuwe accountgegevens Hallo en klik op OK tooadd Hallo-account. Hallo-account moet gemachtigd Hallo die worden vermeld in Hallo [voorbereiden van een account voor automatische detectie](#prepare-an-account-for-automatic-discovery) sectie.
4. Op Hallo van Azure-portal, te bladeren*YourRecoveryServicesVault* > **Site Recovery-infrastructuur** > **Configuration servers**  >  *ConfigurationServer*
5. Klik in de detailpagina Hallo configuratieserver op Hallo **Server vernieuwen** knop.
6. Eenmaal Hallo vernieuwen servertaak is voltooid, selecteert u Hallo vCenter Server tooopen hello vCenter overzichtspagina.
7. Selecteer Hallo toegevoegde account in Hallo **vCenter-server/vSphere hostaccount** veld en klikt u op Hallo **opslaan** knop.

  ![Wijzig-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Verwijderen van een vCenter in Azure Site Recovery
1. Op Hallo van Azure-portal, te bladeren*YourRecoveryServicesVault* > **Site Recovery-infrastructuur** > **Configuration servers**  >  *ConfigurationServer*
2. Selecteer in de detailpagina Hallo configuratieserver Hallo vCenter Server tooopen hello vCenter overzichtspagina.
3. Klik op Hallo **verwijderen** knop toodelete hello vCenter

  ![Delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Als u toomodify hello Vcenter IP-adres/FQDN-naam, poort details moet u toodelete hello vCenter-Server nodig en deze weer opnieuw toevoegen.
