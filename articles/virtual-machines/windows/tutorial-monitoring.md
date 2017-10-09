---
title: aaaAzure bewaking en virtuele Machines van Windows | Microsoft Docs
description: Zelfstudie - Monitor voor een virtuele Windows-Machine met Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Een virtuele Windows-Machine met Azure PowerShell bewaken

Agents toocollect opstarten Azure bewaking gebruikt en prestatiegegevens van de virtuele Azure-machines, deze gegevens opslaan in Azure-opslag en om het programma toegankelijk via de portal, Azure PowerShell-module Hallo en hello Azure CLI. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Diagnostische gegevens over opstarten op een virtuele machine inschakelen
> * Diagnostische gegevens over opstarten bekijken
> * Metrische gegevens weergeven VM-host
> * Hallo-extensie voor diagnostische gegevens installeren
> * Metrische gegevens weergeven VM
> * Maken van een waarschuwing
> * Geavanceerde controle instellen

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben. Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u. Als u werkt Hallo zelfstudie, vervangen, VM-naam en locatie van resourcegroep Hallo waar nodig.

## <a name="view-boot-diagnostics"></a>Diagnostische gegevens over opstarten bekijken

Als Windows virtuele machines opstarten, vastgelegd Hallo boot diagnoseagent schermuitvoer die kan worden gebruikt voor het oplossen van doel. Deze mogelijkheid is standaard ingeschakeld. Hallo vastgelegd scherm schermafbeeldingen worden opgeslagen in een Azure storage-account wordt ook standaard gemaakt. 

U krijgt Hallo opstarten diagnostische gegevens met Hallo [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) opdracht. Diagnostische gegevens over opstarten zijn Hallo voorbeeld te volgen, gedownloade toohello hoofdmap Hallo * c:\* station. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Metrische gegevens weergeven host

Een virtuele machine van Windows heeft een specifieke Host-virtuele machine in Azure die deze met samenwerkt. Metrische gegevens worden automatisch verzameld voor Hallo Host, en kunnen worden weergegeven in hello Azure-portal.

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
2. Klik op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de Host metrische gegevens Hallo onder **beschikbare metrische gegevens** toosee hoe Hallo VM-Host wordt uitgevoerd.

    ![Metrische gegevens weergeven host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Installeren van de extensie voor diagnostische gegevens

Hallo basic host metrische gegevens beschikbaar zijn, maar meer gedetailleerd toosee en VM-specifieke metrische gegevens en u tooneed tooinstall hello Azure extensie voor diagnostische gegevens op Hallo VM. Hello Azure diagnostics-extensie kan aanvullende controle en diagnostische gegevens toobe opgehaald uit Hallo VM. U kunt deze maatstaven voor prestaties weergeven en waarschuwingen op basis van hoe Hallo VM wordt uitgevoerd. Hallo diagnostische uitbreiding wordt geïnstalleerd via hello Azure-portal als volgt:

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
2. Klik op **diagnose instellingen**. Hallo lijst ziet u dat *opstarten diagnostics* al uit de vorige sectie Hallo zijn ingeschakeld. Klik op het selectievakje Hallo voor *basismetrieken*.
3. Klik op Hallo **gastniveau bewaking inschakelen** knop.

    ![Diagnostische metrische gegevens weergeven](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Metrische gegevens weergeven VM

U kunt Hallo VM metrische gegevens weergeven in Hallo dezelfde manier dat Hallo host VM metrische gegevens:

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
2. toosee het Hallo VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de diagnostische gegevens metrische gegevens Hallo onder **beschikbare metrische gegevens**.

    ![Metrische gegevens weergeven VM](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Waarschuwingen maken

U kunt waarschuwingen op basis van specifieke prestatiewaarden kunt maken. Waarschuwingen kunnen bijvoorbeeld gebruikte toonotify u wanneer het gemiddelde CPU-gebruik overschrijdt een bepaalde drempelwaarde of beschikbare vrije schijfruimte onder een bepaalde hoeveelheid zakt. Waarschuwingen worden weergegeven in hello Azure-portal of kunnen worden verzonden via e-mail. U kunt ook Azure Automation-runbooks of Azure Logic Apps activeren in het antwoord tooalerts wordt gegenereerd.

Hallo wordt volgende voorbeeld een waarschuwing voor het gemiddelde CPU-gebruik.

1. In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.
2. Klik op **waarschuwing regels** op Hallo VM blade en klik vervolgens op **metrische waarschuwing toevoegen** aan de bovenkant Hallo van Hallo waarschuwingen-blade.
4. Geef een **naam** voor de waarschuwing, zoals *myAlertRule*
5. een waarschuwing wanneer CPU-percentage 1.0 gedurende vijf minuten overschrijdt tootrigger standaardinstellingen laten staan alle Hallo andere geselecteerd.
6. Eventueel selectievakje Hallo in voor *e-eigenaren, bijdragers en lezers* toosend e-mailmeldingen. Hallo standaardactie is toopresent een melding in Hallo-portal.
7. Klik op Hallo **OK** knop.

## <a name="advanced-monitoring"></a>Geavanceerde controle 

U kunt doen meer geavanceerde bewaking van uw virtuele machine met behulp van [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Als u dit nog niet hebt gedaan, kunt u zich aanmelden voor een [gratis proefversie](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) van Operations Management Suite.

Wanneer u toegang toohello OMS-portal hebt, kunt u Hallo werkruimte sleutel en de werkruimte-id vinden op de blade instellingen Hallo. Gebruik Hallo [Set AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd Hallo OMS-extensie toohello VM. Update Hallo variabele waarden in Hallo hieronder voorbeeld tooreflect u werkruimtesleutel OMS en werkruimte-id.  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Na een paar minuten ziet u nieuwe virtuele machine in de OMS-werkruimte Hallo Hallo. 

![OMS-blade](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt geconfigureerd en virtuele machines in Azure Security Center gecontroleerd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een virtueel netwerk maken
> * Een resourcegroep en de virtuele machine maken 
> * Diagnostische gegevens over opstarten op Hallo VM inschakelen
> * Diagnostische gegevens over opstarten bekijken
> * Metrische gegevens weergeven host
> * Hallo-extensie voor diagnostische gegevens installeren
> * Metrische gegevens weergeven VM
> * Maken van een waarschuwing
> * Geavanceerde controle instellen

Ga toohello volgende zelfstudie toolearn over Azure security center.

> [!div class="nextstepaction"]
> [VM-beveiliging beheren](./tutorial-azure-security.md)