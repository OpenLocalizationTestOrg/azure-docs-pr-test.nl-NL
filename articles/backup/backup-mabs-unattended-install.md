---
title: Installatie op de achtergrond van Azure Backup-Server v2 | Microsoft Docs
description: Gebruik een PowerShell-script op de achtergrond installeert v2 voor Azure Backup-Server. Dit soort installatie is een afkorting van een installatie zonder toezicht.
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="08d8e-104">Voer een installatie zonder toezicht van Azure Backup-Server v2</span><span class="sxs-lookup"><span data-stu-id="08d8e-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="08d8e-105">Informatie over het uitvoeren van een installatie zonder toezicht van v2 voor Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="08d8e-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="08d8e-106">Deze stappen zijn niet van toepassing als u v1 Azure Backup-Server installeert.</span><span class="sxs-lookup"><span data-stu-id="08d8e-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="08d8e-107">Back-upserver v2 installeren</span><span class="sxs-lookup"><span data-stu-id="08d8e-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="08d8e-108">Op de server die als host fungeert voor Azure Backup-Server v2, maak een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="08d8e-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="08d8e-109">(U kunt het bestand maken in Kladblok of in een andere teksteditor.) Sla het bestand als MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="08d8e-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="08d8e-110">Plak de volgende code in het bestand MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="08d8e-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="08d8e-111">Vervang de tekst tussen de vierkante haken (\< \>) met waarden uit uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="08d8e-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="08d8e-112">De volgende tekst is een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08d8e-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="08d8e-113">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="08d8e-113">Save the file.</span></span> <span data-ttu-id="08d8e-114">Voer vervolgens bij een opdrachtprompt met verhoogde bevoegdheid op de server voor installatie met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="08d8e-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="08d8e-115">U kunt deze vlaggen gebruiken voor de installatie:</span><span class="sxs-lookup"><span data-stu-id="08d8e-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="08d8e-116">
**/f**: pad naar INI-bestand</span><span class="sxs-lookup"><span data-stu-id="08d8e-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="08d8e-117">
**/ l**: logboekpad</span><span class="sxs-lookup"><span data-stu-id="08d8e-117">
**/l**: Log path</span></span></br><span data-ttu-id="08d8e-118">
**/i**: installatiepad</span><span class="sxs-lookup"><span data-stu-id="08d8e-118">
**/i**: Installation path</span></span></br><span data-ttu-id="08d8e-119">
**/x**: pad verwijderen</span><span class="sxs-lookup"><span data-stu-id="08d8e-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="08d8e-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08d8e-120">Next steps</span></span>
<span data-ttu-id="08d8e-121">Nadat u de back-up-Server hebt geïnstalleerd, informatie over het voorbereiden van uw server of met het beveiligen van een werkbelasting beginnen.</span><span class="sxs-lookup"><span data-stu-id="08d8e-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="08d8e-122">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="08d8e-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="08d8e-123">Back-up-Server gebruiken om back-up van een VMware-server</span><span class="sxs-lookup"><span data-stu-id="08d8e-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="08d8e-124">Back-up-Server gebruiken om back-up van SQL Server</span><span class="sxs-lookup"><span data-stu-id="08d8e-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="08d8e-125">Moderne back-up naar back-upserver toevoegen</span><span class="sxs-lookup"><span data-stu-id="08d8e-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
