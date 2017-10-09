---
title: aaaUse Azure Automation tootrigger een taak | Microsoft Docs
description: Meer informatie over hoe Azure Automation toouse voor activering van StorSimple Data Manager-taken (afgeschermd voorbeeld)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Gebruik Azure Automation tootrigger een taak (afgeschermd voorbeeld)

Dit artikel wordt beschreven hoe toouse Azure Automation tootrigger een taak StorSimple Data Manager.

## <a name="prerequisites"></a>Vereisten

Zorg ervoor dat u hebt voordat u begint:

*   Azure Powershell is geïnstalleerd. [Download de Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuratie-instellingen tooinitialize Hallo gegevenstransformatie taak (instructies tooobtain deze instellingen zijn opgenomen hier).
*   De taakdefinitie van een die correct is geconfigureerd in een hybride Gegevensresource binnen een resourcegroep.
*   Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) bestand van Hallo github-opslagplaats.
*   Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) van Hallo github-opslagplaats.
*   Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) van Hallo github-opslagplaats.

## <a name="step-by-step"></a>Stapsgewijs

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Azure Active Directory-machtigingen voor de taakdefinitie Hallo automation-taak toorun Hallo ophalen

1. tooretrieve Hallo-configuratieparameters voor Active Directory, Hallo volgende stappen:

    1. Open Windows PowerShell in uw lokale computer. Zorg ervoor dat [Azure PowerShell](https://azure.microsoft.com/downloads/) is geïnstalleerd.
    1. Voer Hallo `Get-ConfigurationParams.ps1` script (in de map Hallo hierboven gedownloade). Typ de volgende opdracht in de PowerShell-venster Hallo Hallo:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Hallo ActiveDirectoryKey is een wachtwoord dat u later gebruiken. Voer een wachtwoord van uw keuze. AppName kan een willekeurige tekenreeks zijn.

2. Dit script levert de volgende waarden op die moeten worden gebruikt tijdens de activering van automation-runbook Hallo Hallo. Noteer deze waarden.

    - Client-ID
    - Tenant-id
    - Active Directory-sleutel (hetzelfde als Hallo een dat hierboven is opgegeven)
    - Abonnements-id

### <a name="set-up-hello-automation-account"></a>Hallo Automation-Account instellen

1. Meld u aan tooAzure en open uw Automation-account.
2. Klik op **activa** tegel tooopen Hallo lijst van activa.
3. Klik op **Modules** tegel tooopen Hallo lijst met modules.
4. Klik op **+ toevoegen van een module** knop en Hallo toevoegen module blade wordt gestart.

    ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Nadat u hebt geselecteerd Hallo `DataTransformationApp.zip` bestand vanaf uw lokale computer, klikt u op **OK** tooimport Hallo-module.

   Als een module tooyour-account voor Azure Automation wordt geïmporteerd, pakt deze metagegevens over Hallo-module. Deze bewerking kan enkele minuten duren.

   ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. U ontvangt een melding die module hello wordt geïmplementeerd en een andere melding wanneer het Hallo-proces is voltooid.  U kunt ook Hallo status controleren **Modules** tegel.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport hello runbook waarmee de taakdefinitie hello wordt geactiveerd

1. Open uw Automation-account in hello Azure-portal.
2. Klik op **Runbooks** tegel tooopen Hallo lijst van runbooks.
3. Klik op **+ een runbook toevoegen** en vervolgens **een bestaand runbook importeren**.

   ![Een bestaand runbook importeren](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Klik op **Runbook bestand** en selecteer Hallo bestand tooimport `Trigger-DataTransformation-Job.ps1`.
5. Klik op **maken** tooimport hello runbook. Hallo nieuw runbook wordt weergegeven in de lijst Hallo van runbooks voor Hallo Automation-account.
7. Klik op **Trigger-DataTransformation-Job** runbook en klik vervolgens op **bewerken**.
8. Klik op **publiceren** en vervolgens **Ja** wanneer u om bevestiging wordt gevraagd.


### <a name="toorun-hello-runbook"></a>toorun hello runbook:
1. Open uw Automation-account in hello Azure-portal.
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.
3. Klik op **Trigger-DataTransformation-Job**.
4. Klik op **Start** toostart hello runbook.

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. In Hallo **runbook starten** blade alle Hallo parameters opgeven. Klik op **OK** toosubmit Hallo gegevenstransformatie taak.

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Volgende stappen

[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md).
