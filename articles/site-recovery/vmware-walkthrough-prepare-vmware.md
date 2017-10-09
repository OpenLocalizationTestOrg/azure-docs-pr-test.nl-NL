---
title: aaaPrepare lokale VMware-resources voor replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt voor het repliceren van workloads die worden uitgevoerd op virtuele VMware-machines tooAzure opslag
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Stap 6: Lokale VMware replicatie tooAzure voorbereiden

Volg Hallo-instructies in dit artikel tooprepare lokale VMware servers toointeract met Azure Site Recovery en virtuele VMWare-machines voorbereiden voor de installatie van Hallo Mobility-service. Hallo Mobility-service-agent moet worden geïnstalleerd op alle lokale VM's die u wilt dat tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Voorbereiden voor automatische detectie

Site Recovery detecteert automatisch virtuele machines waarop vSphere ESXi-hosts (met of zonder een vCenter-server). Voor automatische detectie, Site Recovery moet een account tooaccess hosts en -servers:

1. een specifiek account toouse maakt u een rol (op Hallo vCenter niveau met Hallo machtigingen in Hallo in de volgende tabel beschreven. Geef een naam zoals **Azure_Site_Recovery**.
2. Vervolgens maken van een gebruiker op Hallo vSphere host/vCenter-server en Hallo rol toohello gebruiker toewijzen. U kunt dit gebruikersaccount opgeven tijdens de implementatie van Site Recovery.


### <a name="vmware-account-permissions"></a>Machtigingen van de VMware-account

Site Recovery moet toegang tooVMware voor Hallo proces server tooautomatically VM's detecteren, en voor de failover en failback van virtuele machines.

- **Migreren**: als u wilt dat alleen toomigrate virtuele VMware-machines tooAzure, zonder ooit terug mislukt, kunt u een VMware-account gebruiken met een rol alleen-lezen. Een dergelijke rol failover kan worden uitgevoerd, maar kan niet worden beveiligde bronmachines afgesloten. Dit is niet nodig zijn voor migratie.
- **Repliceren/herstellen**: als u toodeploy volledige replicatie (repliceren, failover, failback) Hallo account moet kunnen toorun bewerkingen wilt zoals het maken en schijven verwijderen, inschakelen aan virtuele machines, enzovoort.
- **Automatische detectie**: ten minste een alleen-lezen-account is vereist.


**Taak** | **Vereiste account/functie** | **Machtigingen** | **Details**
--- | --- | --- | ---
**Processerver detecteert automatisch virtuele VMware-machines** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).
**Failover** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).<br/><br/> Dit is handig voor migratiedoeleinden, maar niet een volledige replicatie, failover en failback.
**Failover en failback** | We raden u een rol (Azure_Site_Recovery) met de Hallo vereist machtigingen maken en vervolgens Hallo rol tooa VMware gebruiker of groep toewijzen | Data Center-object doorgeven tooChild Object, –> rol Azure_Site_Recovery =<br/><br/> Datastore -> ruimte toewijzen, gegevensopslag, op laag niveau bestandsbewerkingen bladeren, bestand verwijderen, bestanden van virtuele machine bijwerken<br/><br/> Netwerk -> netwerk toewijzen<br/><br/> Resource -> toewijzen VM tooresource pool, migreren van virtuele machine is uitgeschakeld, stroomvoorziening op virtuele machine migreren<br/><br/> Taken maken taak, updatetaak -><br/><br/> Virtuele machine-configuratie ><br/><br/> Virtuele machine -> Interact -> vraag beantwoorden, apparaatverbinding, CD's configureren, configureren van diskettes, uitschakelen, inschakelen, VMware-hulpprogramma's installeren<br/><br/> Virtuele machine -> inventaris -> maken, registreren, registratie<br/><br/> Virtuele machine inrichten -> -> downloaden van de virtuele machine toestaan, toestaan uploaden van bestanden van virtuele machine<br/><br/> Virtuele machine-momentopnamen >-Remove momentopnamen > | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Voorbereiden voor de push-installatie van Hallo Mobility-service

Hallo Mobility-service moet worden geïnstalleerd op alle virtuele machines die u wilt tooreplicate. Er zijn een aantal manieren tooinstall Hallo service, inclusief de handmatige installatie, push-installatie van Site Recovery-processerver Hallo en met behulp van methoden zoals System Center Configuration Manager-installatie.

Als u wilt dat toouse push-installatie, moet u tooprepare een account dat Site Recovery tooaccess Hallo VM kunt gebruiken.

- U kunt een domein of lokale account gebruiken
- Voor Windows, als u niet een domeinaccount, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. dit in Hallo registreert onder toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Hallo DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1.
- Als u tooadd Hallo register-item voor Windows vanuit een CLI wilt, typt u:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Voor Linux moet Hallo account basiscertificaat op de bronserver Linux Hallo.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 7: een kluis maken](vmware-walkthrough-create-vault.md)
