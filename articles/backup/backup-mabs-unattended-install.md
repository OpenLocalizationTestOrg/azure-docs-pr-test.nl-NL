---
title: installatie van Azure Backup-Server v2 aaaSilent | Microsoft Docs
description: Gebruik een PowerShell-script toosilently v2 voor Azure Backup-Server installeren. Dit soort installatie is een afkorting van een installatie zonder toezicht.
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Voer een installatie zonder toezicht van Azure Backup-Server v2

Meer informatie over hoe toorun een installatie zonder toezicht van v2 voor Azure Backup-Server. 

Deze stappen zijn niet van toepassing als u v1 Azure Backup-Server installeert.

## <a name="install-backup-server-v2"></a>Back-upserver v2 installeren

1. Maak een tekstbestand op Hallo-server die als host fungeert voor v2 voor Azure Backup-Server. (U kunt maken Hallo-bestand in Kladblok of in een andere tekst editor.) Hallo-bestand opslaan als MABSSetup.ini. 

2. Hallo na de code in Hallo MABSSetup.ini bestand plakken. Vervang de tekst hello binnen Hallo vierkante haken (\< \>) met waarden uit uw omgeving. na de tekst Hello volgt een voorbeeld:

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Hallo-bestand opslaan. Bij een opdrachtprompt met verhoogde bevoegdheid op de server voor installatie op Hallo Voer deze opdracht:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

U kunt deze vlaggen gebruiken voor de installatie van Hallo:</br>
**/f**: pad naar INI-bestand</br>
**/ l**: logboekpad</br>
**/i**: installatiepad</br>
**/x**: pad verwijderen</br>

## <a name="next-steps"></a>Volgende stappen
Nadat u de back-up-Server hebt geïnstalleerd, informatie over hoe tooprepare uw server, of met het beveiligen van een werkbelasting beginnen.

- [Back-upserver van werkbelastingen voorbereiden](backup-azure-microsoft-azure-backup.md)
- [Back-upserver tooback van een VMware-server gebruiken](backup-azure-backup-server-vmware.md)
- [Back-upserver tooback van SQL Server gebruiken](backup-azure-sql-mabs.md)
- [Moderne Backup Storage tooBackup Server toevoegen](backup-mabs-add-storage.md)
