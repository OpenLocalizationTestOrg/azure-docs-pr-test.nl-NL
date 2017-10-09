---
title: aaaAzure Site Recovery voor probleemoplossing voor problemen met de replicatie van Azure naar Azure en fouten | Microsoft Docs
description: Het oplossen van fouten en problemen bij het repliceren van virtuele machines voor herstel na noodgevallen in Azure
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Oplossen van problemen met de replicatie van de virtuele machine van Azure naar Azure

Dit artikel worden veelvoorkomende problemen met Hallo in Azure Site Recovery wanneer repliceren en herstellen van virtuele machines in Azure uit één regio tooanother regio en wordt uitgelegd hoe tootroubleshoot ze. Zie voor meer informatie over ondersteunde configuraties Hallo [ondersteuningsmatrix voor het repliceren van virtuele Azure-machines](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problemen met Azure-resource-quotum (foutcode 150097)
Ingeschakelde toocreate Azure VM's in Hallo doelregio dat u van plan toouse als land herstel na noodgevallen bent moet in uw abonnement. Daarnaast uw abonnement te beschikken over voldoende quota is ingeschakeld toocreate virtuele machines met een specifieke grootte. Site Recovery uitgelicht Hallo standaard even groot zijn voor Hallo doel VM zoals Hallo bron-VM. Als de overeenkomende grootte Hallo niet beschikbaar is, wordt Hallo dichtstbijzijnde grootte automatisch gekozen. Als er geen overeenkomende grootte die ondersteuning biedt voor VM-configuratie bron is, wordt dit foutbericht weergegeven:

**Foutcode** | **Mogelijke oorzaken** | **Aanbeveling**
--- | --- | ---
150097<br></br>**Bericht**: replicatie kan niet worden ingeschakeld voor Hallo virtuele machine VmName. | -Uw abonnement-ID kan niet zijn ingeschakeld toocreate alle virtuele machines in de doellocatie regio Hallo.</br></br>-Uw abonnements-ID is mogelijk niet ingeschakeld of geen voldoende quotum toocreate specifieke VM-grootten in Hallo regio doellocatie.</br></br>-Een geschikte doel VM-grootte die overeenkomt met de Hallo bron VM NIC aantal (2) is niet gevonden voor Hallo abonnements-ID in Hallo regio doellocatie.| Neem contact op met [ondersteuning voor facturering aan Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable VM maken voor Hallo VM-grootten in Hallo target-locatie voor uw abonnement vereist. Nadat deze ingeschakeld, geeft opnieuw Hallo bewerking is mislukt.

### <a name="fix-hello-problem"></a>Hallo probleem oplossen
U kunt contact opnemen met [ondersteuning voor facturering aan Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable uw abonnement toocreate virtuele machines van de vereiste grootte in Hallo target-locatie.

Als de doellocatie Hallo een beperking van capaciteit heeft, Schakel replicatie uit en vereist tooa andere locatie waar uw abonnement voldoende quotum toocreate VMs Hallo heeft grootten.

## <a name="trusted-root-certificates-error-code-151066"></a>Vertrouwde basiscertificaten (foutcode 151066)

Als alle Hallo nieuwste vertrouwde basiscertificaten niet aanwezig is op Hallo VM, mislukken de taak 'replicatie inschakelen'. Zonder Hallo certificaten, Hallo verificatie en autorisatie van Site Recovery-service mislukken aanroepen vanuit Hallo VM. Fout bij het Hallo-bericht voor de Site Recovery-taak met 'replicatie inschakelen' hello is mislukt wordt weergegeven:

**Foutcode** | **Mogelijke oorzaak** | **Aanbevelingen**
--- | --- | ---
151066<br></br>**Bericht**: Site Recovery-configuratie is mislukt. | Hallo vereist vertrouwde basiscertificaten gebruikt voor autorisatie en verificatie niet beschikbaar zijn op Hallo-machine. | -Zorg ervoor dat Hallo vertrouwde basiscertificaten aanwezig zijn op de machine Hallo voor een virtuele machine met Windows-besturingssysteem hello. Zie voor informatie [configureren van vertrouwde basiscertificaten en niet-toegestane certificaten](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Volg voor een virtuele machine met Linux-besturingssysteem hello, Hallo richtlijnen voor vertrouwde basiscertificaten gepubliceerd door Hallo Linux-besturingssysteem versie distributor.

### <a name="fix-hello-problem"></a>Hallo probleem oplossen
**Windows**

Installeer alle Hallo meest recente Windows-updates op Hallo VM zodat alle Hallo vertrouwde basiscertificaten aanwezig op de machine Hallo zijn. Als u in een omgeving zonder verbinding, doe Hallo standaard Windows update in uw organisatie tooget Hallo certificaten. Als Hallo vereist certificaten niet beschikbaar zijn op Hallo VM, mislukken Hallo aanroepen toohello Site Recovery-service uit veiligheidsoverwegingen.

Volgen typische Windows hello-updatebeheer of updatebeheerproces certificaat in uw organisatie tooget alle Hallo nieuwste basiscertificaten en intrekken van certificaten Hallo bijgewerkt lijst op Hallo van virtuele machines.

tooverify die Hallo probleem is opgelost, gaat u toologin.microsoftonline.com vanuit een browser op uw virtuele machine.

**Linux**

Ga als volgt Hallo richtlijnen bij uw Linux distributor tooget Hallo nieuwste vertrouwde basiscertificaten en Hallo laatste certificaatintrekkingslijst op Hallo VM.

Omdat SuSE Linux symlinks toomaintain een lijst van certificaten gebruikt, als volgt te werk:

1.  Aanmelden als een hoofdgebruiker.

2.  Voer deze opdracht uit:

      ``# cd /etc/ssl/certs``

3.  toosee als Hallo Symantec basis-CA-certificaat aanwezig is, voert u deze opdracht:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Als het Hallo-bestand is niet gevonden, voert u deze opdrachten:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  een symlink met b204d74a.0 toocreate -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, voert u deze opdracht:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Controleer de toosee als deze opdracht heeft Hallo na uitvoer. Als dat niet het geval is, hebt u toocreate een symlink:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Als symlink 653b494a.0 niet aanwezig is, gebruikt u deze opdracht toocreate een symlink:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Uitgaande verbinding voor de Site Recovery-URL's of het IP-adresbereiken (foutcode 151037 of 151072)

Uitgaande verbinding toospecific URL's of het IP-adresbereiken is voor de Site Recovery replicatie toowork, vereist van Hallo VM. Als uw VM zich achter een firewall of gebruikt netwerkverbinding security group (NSG) regels toocontrol uitgaand, ziet u mogelijk een van deze foutberichten:

**Foutcodes** | **Mogelijke oorzaken** | **Aanbevelingen**
--- | --- | ---
151037<br></br>**Bericht**: tooregister met Site Recovery virtuele Azure-machine is mislukt. | -U NSG toocontrol uitgaande toegang op Hallo VM en Hallo vereist IP bereiken worden niet goedgekeurde lijst voor uitgaande toegang.</br></br>-U hulpprogramma's van derden firewall en Hallo vereiste IP-adresbereiken/URL's zijn niet wilt plaatsen.</br>| -Als u firewall proxy toocontrol uitgaande netwerkverbinding op Hallo VM gebruikt, zorg ervoor dat Hallo vereiste URL's of datacenter IP-adresbereiken zijn goedgekeurde lijst. Zie voor informatie [firewall-proxy richtlijnen](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Als u NSG-regels toocontrol uitgaande netwerkverbinding op Hallo VM gebruikt, zorg ervoor dat Hallo vereiste datacenter IP-adresbereiken wilt plaatsen. Zie voor informatie [groep beveiligingsrichtlijnen netwerk](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Bericht**: Site Recovery-configuratie is mislukt. | Verbinding kan niet tot stand gebrachte tooSite Recovery service-eindpunten. | -Als u firewall proxy toocontrol uitgaande netwerkverbinding op Hallo VM gebruikt, zorg ervoor dat Hallo vereiste URL's of datacenter IP-adresbereiken zijn goedgekeurde lijst. Zie voor informatie [firewall-proxy richtlijnen](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Als u NSG-regels toocontrol uitgaande netwerkverbinding op Hallo VM gebruikt, zorg ervoor dat Hallo vereiste datacenter IP-adresbereiken wilt plaatsen. Zie voor informatie [groep beveiligingsrichtlijnen netwerk](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Hallo probleem oplossen
toowhitelist [Hallo vereist URL's](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) of Hallo [IP-adresbereiken vereist](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), volg de stappen Hallo in Hallo [leidraad voor netwerken](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Schijf niet gevonden in de Hallo-machine (foutcode 150039)

Een nieuwe schijf gekoppeld toohello die VM moet worden geïnitialiseerd.

**Foutcode** | **Mogelijke oorzaken** | **Aanbevelingen**
--- | --- | ---
150039<br></br>**Bericht**: Azure gegevensschijf (DiskName) (DiskURI) met de logische eenheid number (LUN) (LUNValue) is niet toegewezen tooa van de bijbehorende schijf wordt gerapporteerd door binnen Hallo VM die Hallo heeft dezelfde LUN-waarde. | -Een nieuwe gegevensschijf is aangesloten toohello VM, maar deze is niet geïnitialiseerd.</br></br>-Hallo gegevensschijf binnen Hallo VM is niet correct worden gerapporteerd Hallo LUN-waarde op welke Hallo schijf gekoppelde toohello VM is.| Zorg dat Hallo gegevensschijven zijn geïnitialiseerd en probeer vervolgens opnieuw Hallo.</br></br>Voor Windows: [koppelen en een nieuwe schijf initialiseren](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Voor Linux: [initialiseren van een nieuwe gegevensschijf in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Hallo probleem oplossen
Zorg ervoor dat Hallo gegevensschijven geïnitialiseerd, en probeer vervolgens opnieuw Hallo:

- Voor Windows: [koppelen en een nieuwe schijf initialiseren](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Voor Linux: [initialiseren van een nieuwe gegevensschijf in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Als Hallo probleem zich blijft voordoen, moet u contact op met ondersteuning.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Kan geen toosee hello Azure VM voor selectie in "replicatie inschakelen"

U ziet mogelijk niet uw Azure-VM voor selectie in [replicatie inschakelen: stap 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Dit probleem kan zijn vanwege toostale links op Hallo virtuele machine van Azure Site Recovery-configuratie. Hallo verouderde configuratie kan worden links op een virtuele machine van Azure in Hallo volgende gevallen:

- U replicatie voor virtuele Azure-machine Hallo ingeschakeld met behulp van Site Recovery en vervolgens Hallo Site Recovery-kluis verwijderd zonder de replicatie op Hallo VM expliciet uitschakelen.
- U replicatie voor virtuele Azure-machine Hallo ingeschakeld met behulp van Site Recovery en vervolgens verwijderd Hallo resourcegroep met Site Recovery-kluis Hallo zonder de replicatie op Hallo VM expliciet uitschakelen.

### <a name="fix-hello-problem"></a>Hallo probleem oplossen

U kunt [verwijderen van verouderde ASR configuratiescript](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) en verwijder Hallo verouderde Site Recovery-configuratie op Hallo Azure VM. U ziet Hallo VM in [replicatie inschakelen: stap 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) na het verwijderen van verouderde Hallo-configuratie.


## <a name="next-steps"></a>Volgende stappen
[Virtuele Azure-machines repliceren](site-recovery-replicate-azure-to-azure.md)
