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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="9f9aa-104">Voer een installatie zonder toezicht van Azure Backup-Server v2</span><span class="sxs-lookup"><span data-stu-id="9f9aa-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="9f9aa-105">Meer informatie over hoe toorun een installatie zonder toezicht van v2 voor Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="9f9aa-106">Deze stappen zijn niet van toepassing als u v1 Azure Backup-Server installeert.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="9f9aa-107">Back-upserver v2 installeren</span><span class="sxs-lookup"><span data-stu-id="9f9aa-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="9f9aa-108">Maak een tekstbestand op Hallo-server die als host fungeert voor v2 voor Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="9f9aa-109">(U kunt maken Hallo-bestand in Kladblok of in een andere tekst editor.) Hallo-bestand opslaan als MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="9f9aa-110">Hallo na de code in Hallo MABSSetup.ini bestand plakken.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="9f9aa-111">Vervang de tekst hello binnen Hallo vierkante haken (\< \>) met waarden uit uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="9f9aa-112">na de tekst Hello volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9f9aa-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="9f9aa-113">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-113">Save hello file.</span></span> <span data-ttu-id="9f9aa-114">Bij een opdrachtprompt met verhoogde bevoegdheid op de server voor installatie op Hallo Voer deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="9f9aa-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="9f9aa-115">U kunt deze vlaggen gebruiken voor de installatie van Hallo:</span><span class="sxs-lookup"><span data-stu-id="9f9aa-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="9f9aa-116">
**/f**: pad naar INI-bestand</span><span class="sxs-lookup"><span data-stu-id="9f9aa-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="9f9aa-117">
**/ l**: logboekpad</span><span class="sxs-lookup"><span data-stu-id="9f9aa-117">
**/l**: Log path</span></span></br><span data-ttu-id="9f9aa-118">
**/i**: installatiepad</span><span class="sxs-lookup"><span data-stu-id="9f9aa-118">
**/i**: Installation path</span></span></br><span data-ttu-id="9f9aa-119">
**/x**: pad verwijderen</span><span class="sxs-lookup"><span data-stu-id="9f9aa-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="9f9aa-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f9aa-120">Next steps</span></span>
<span data-ttu-id="9f9aa-121">Nadat u de back-up-Server hebt geïnstalleerd, informatie over hoe tooprepare uw server, of met het beveiligen van een werkbelasting beginnen.</span><span class="sxs-lookup"><span data-stu-id="9f9aa-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="9f9aa-122">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9f9aa-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="9f9aa-123">Back-upserver tooback van een VMware-server gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f9aa-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="9f9aa-124">Back-upserver tooback van SQL Server gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f9aa-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="9f9aa-125">Moderne Backup Storage tooBackup Server toevoegen</span><span class="sxs-lookup"><span data-stu-id="9f9aa-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
