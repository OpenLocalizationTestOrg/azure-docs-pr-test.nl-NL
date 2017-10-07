---
title: aaaAzure schijf versleuteling probleemoplossing | Microsoft Docs
description: Dit artikel bevat tips voor probleemoplossing voor Microsoft Azure Disk Encryption for Windows en Linux IaaS VM's.
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Handleiding voor probleemoplossing voor Azure Disk Encryption

Deze handleiding is voor (IT) van IT-professionals, informatie beveiligingsanalisten en problemen met betrekking tot cloudbeheerders waarvan organisaties met behulp van Azure disk encryption en richtlijnen tootroubleshoot schijfversleuteling nodig.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Het oplossen van Linux-besturingssysteem schijfversleuteling

Linux-besturingssysteem schijfversleuteling Hallo OS station voorafgaande toorunning moet ontkoppelen deze via Hallo volledige schijf versleutelingsproces.   Als dit niet, wordt een foutbericht van ' is mislukt toounmount na... " foutbericht is waarschijnlijk toooccur.

Dit is waarschijnlijk bij OS schijfversleuteling wordt toegepast op een doelomgeving VM die is gewijzigd of gewijzigd van de ondersteunde voorraad afbeelding.  Voorbeelden van afwijkingen van Hallo ondersteund installatiekopie, die met Hallo-extensie mogelijkheid toounmount Hallo OS station botsen kan zijn:
- Aangepaste installatiekopieën die niet langer overeenkomen met een ondersteund bestandssysteem en/of -partitieschema.
- Aangepaste installatiekopieën met toepassingen zoals antivirus, Docker, SAP, MongoDB of Apache Cassandra in Hallo OS voorafgaande tooencryption uitgevoerd.  Deze toepassingen zijn moeilijk tooterminate en wanneer ze open bestand ingangen toohello OS station behouden, Hallo station kan niet worden ontkoppeld, ontstaan.
- Aangepaste scripts die worden uitgevoerd in tijd nabijheid toohello versleuteling stap kan leiden tot problemen en dat deze fout te sluiten. Dit kan gebeuren wanneer een Resource Manager-sjabloon definieert meerdere extensies tooexecute tegelijkertijd, of wanneer er een extensie voor aangepaste scripts of een andere actie tegelijkertijd toodisk versleuteling.   Hallo probleem mogelijk worden opgelost door serialiseren en te isoleren van deze stappen.
- Als SELinux is niet uitgeschakeld voorafgaande tooenabling versleuteling, ontkoppel Hallo stap mislukt.  SELinux mag opnieuw worden ingeschakeld nadat de codering is voltooid.
- Hallo OS-schijf gebruikt wanneer een LVM-schema (Hoewel beperkte ondersteuning voor LVM gegevens schijf beschikbaar is, LVM besturingssysteemschijf is niet)
- Wanneer de minimale geheugenvereisten niet wordt voldaan (7GB wordt voorgesteld voor OS schijfversleuteling)
- Wanneer gegevensstations zijn recursief gekoppeld onder /mnt/ directory of elkaar (bijvoorbeeld /mnt/data1, /mnt/data2, /data3 + /data3/data4, enz.)
- Wanneer andere Azure Disk Encryption [vereisten](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) voor Linux wordt niet voldaan

## <a name="unable-tooencrypt"></a>Kan geen tooencrypt

In sommige gevallen verschijnt Hallo Linux schijfversleuteling toobe vastgelopen bij 'OS schijfversleuteling gestart' en SSH is uitgeschakeld. Dit proces kan toocomplete op een vooraf gedefinieerde afbeelding 3 16 uur duren.  Als meerdere TB grootte gegevensschijven worden toegevoegd, kan Hallo duren dagen. Hallo Linux-besturingssysteem schijf versleuteling sequence Hallo OS station tijdelijk ontkoppelt en voert bloksgewijze codering van volledige besturingssysteemschijf hello, voordat deze in de versleutelde status stationseigendom.   In tegenstelling tot Azure Disk Encryption in Windows kunnen Linux-schijfversleuteling niet gelijktijdig gebruik van Hallo VM terwijl Hallo-versleuteling uitgevoerd wordt.  Hallo prestatiekenmerken van de virtuele machine, zoals Hallo Hallo schijf en Hiermee wordt aangegeven of Hallo storage-account wordt ondersteund door standard of premium SSD-opslag, Hallo kunnen Hallo tijd die nodig is toocomplete versleuteling aanzienlijk beïnvloeden.

status van de toocheck hello ProgressMessage veld geretourneerd van Hallo [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) opdracht kan worden gepeild.   Terwijl Hallo OS-schijf wordt versleuteld, Hallo VM een servicing status en SSH ook uitgeschakeld tooprevent is een onderbreking van de toohello er proces.  EncryptionInProgress worden gerapporteerd voor de meeste Hallo Hallo tijd terwijl versleuteling uitgevoerd wordt, enkele uren later gevolgd door een VMRestartPending bericht waarin wordt gevraagd toorestart Hallo VM.  Bijvoorbeeld:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Eenmaal gevraagd tooreboot Hallo VM en na Hallo VM opnieuw te starten en het toekennen van 2-3 minuten voor Hallo opnieuw opstarten en voor de laatste stappen toobe uitgevoerd op het Hallo-doel, Hallo-bericht van status wordt aangegeven dat versleuteling ten slotte is voltooid.   Als dit bericht beschikbaar is, is Hallo versleuteld OS station opnieuw verwachte toobe klaar voor gebruik en voor Hallo VM toobe bruikbaar.

In gevallen waarin deze reeks niet gevonden is, of als opstartgegevens, voortgangsbericht of andere foutindicatoren rapporteren dat OS-versleuteling is mislukt in het midden van de Hallo van dit proces (bijvoorbeeld als u ziet Hallo 'is mislukt toounmount' fout die wordt beschreven in deze handleiding) het wordt aanbevolen toorestore Hallo VM back toohello momentopname of back-up van de direct voorafgaande tooencryption.  Eerdere toohello opnieuw probeert, verdient het voorgestelde toore-kenmerken Hallo Hallo VM evalueren en zorg ervoor dat aan alle vereisten wordt voldaan.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Het oplossen van Azure Disk Encryption achter een Firewall
Wanneer verbinding is beperkt door een firewall, proxy-vereiste of groep (NSG) instellingen voor netwerkbeveiliging, Hallo mogelijkheid van Hallo extensie tooperform nodig taken kunnen worden onderbroken.   Dit kan leiden tot statusberichten zoals 'Status van extensie niet beschikbaar op Hallo VM' en in de verwachte scenario's toofinish mislukken.  Hallo-secties die volgen heeft enkele veelvoorkomende firewallproblemen die u kan onderzoeken.

### <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
Netwerk groep beveiligingsinstellingen toegepast moeten nog steeds Hallo toomeet Hallo gedocumenteerd netwerk eindpuntconfiguratie toestaan [vereisten](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) voor schijfversleuteling.

### <a name="azure-keyvault-behind-firewall"></a>Azure Keyvault achter een firewall
Hallo VM moet kunnen tooaccess sleutelkluis. Raadpleeg tooguidance op toegang tookey veroorzaakt achter een firewall die wordt onderhouden door Hallo [Sleutelkluis](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) team.

### <a name="linux-package-management-behind-firewall"></a>Linux-pakket management achter een firewall
Tijdens runtime, is Azure Disk Encryption voor Linux is afhankelijk van Hallo doel distributie pakket management system tooinstall nodig vereiste componenten voorafgaande tooenabling versleuteling.  Als firewall-instellingen te voorkomen dat Hallo VM kunnen toodownload en deze onderdelen installeert, worden volgende fouten verwacht.    Hallo stappen tooconfigure die dit door verdeling kan variëren.  Op Red Hat is ervoor te zorgen dat abonnement-manager en yum correct zijn ingesteld als een proxy vereist is, essentieel.  Zie [dit](https://access.redhat.com/solutions/189533) Red Hat support-artikel over dit onderwerp.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Het oplossen van Windows Server 2016 Server Core

Hallo bdehdcfg onderdeel is niet standaard beschikbaar op Windows Server 2016 Server Core. Dit onderdeel is vereist voor Azure Disk Encryption.

tooworkaround dit probleem, kopie Hallo volgende 4 bestanden vanuit een virtuele machine van Windows Server 2016 Data Center toohello c:\windows\system32 map Hallo Server Core-installatiekopie:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Voer Hallo volgende opdracht:

```
bdehdcfg.exe -target default
```

Hiermee maakt u een systeempartitie 550MB en vervolgens na opnieuw opstarten, kunt u Diskpart toocheck Hallo volumes gebruiken, en doorgaan.  

Bijvoorbeeld:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd meer informatie over enkele veelvoorkomende problemen in Azure disk encryption toe en hoe tootroubleshoot. Lees voor meer informatie over deze service en de mogelijkheid:

- [Schijfversleuteling in Azure Security Center toepassen](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Een virtuele Machine van Azure versleutelen](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure Data Encryption in rust](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
