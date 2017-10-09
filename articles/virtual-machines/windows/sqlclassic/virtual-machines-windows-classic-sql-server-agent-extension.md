---
title: aaaAutomate beheertaken op SQL-machines (klassiek) | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toomanage Hallo voor SQL Server agent-extensie, die specifieke SQL Server-beheertaken worden geautomatiseerd. Het gaat hierbij om automatische back-up automatisch patchen en integratie van Azure Sleutelkluis. In dit onderwerp maakt gebruik van de klassieke implementatiemodus Hallo.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatiseren beheertaken op Azure Virtual Machines Hello SQL Server Agent-extensie (klassiek)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Klassiek](../classic/sql-server-agent-extension.md)
> 
>
 
Hallo uitbreiding IaaS-Agent voor SQL Server (SQLIaaSAgent) wordt uitgevoerd op virtuele machines in Azure tooautomate beheertaken. Dit onderwerp bevat een overzicht van Hallo-services wordt ondersteund door het Hallo-extensie, evenals de instructies voor installatie, status en verwijdering.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. tooview hello Resource Manager-versie van dit artikel, Zie [SQL Server Agent-extensie voor SQL Server VM's Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Ondersteunde services
Hallo uitbreiding voor SQL Server IaaS-Agent ondersteunt Hallo beheertaken te volgen:

| Beheer-functie | Beschrijving |
| --- | --- |
| **Automatische back-up van SQL** |Automatiseert Hallo planning van de back-ups voor alle databases voor het standaardexemplaar van SQL Server in Hallo VM Hallo. Zie voor meer informatie [automatische back-up voor SQL Server in Azure Virtual Machines (klassiek)](../classic/sql-automated-backup.md). |
| **Automatisch patchen van SQL** |Hiermee configureert u een onderhoudsvenster tijdens welke updates plaatsen tooyour VM kan duren, zodat u voorkomen de updates tijdens piektijden voor uw workload dat kunt. Zie voor meer informatie [automatisch patchen voor SQL Server in Azure Virtual Machines (klassiek)](../classic/sql-automated-patching.md). |
| **Integratie van Azure Key Vault** |Hiermee schakelt u tooautomatically installeren en configureren van Azure Sleutelkluis op uw SQL Server-VM. Zie voor meer informatie [configureren Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual machines (klassiek)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Vereisten
Vereisten toouse Hallo uitbreiding van SQL Server IaaS-Agent op de virtuele machine:

### <a name="operating-system"></a>Besturingssysteem:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>SQL Server-versies:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell:
[Downloaden en configureren van de meest recente Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).

Start Windows PowerShell en tooyour Azure-abonnement verbinden met de Hallo **Add-AzureAccount** opdracht.

    Add-AzureAccount

Als u meerdere abonnementen hebt, gebruikt u **Select-AzureSubscription** tooselect Hallo abonnement met het doel-klassieke VM.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

Op dit moment kunt u een lijst van Hallo klassieke virtuele machines en hun bijbehorende servicenamen Hello opvragen **Get-AzureVM** opdracht.

    Get-AzureVM

## <a name="installation"></a>Installeren
Voor klassieke virtuele machines, moet u PowerShell tooinstall Hallo uitbreiding voor IaaS-Agent van SQL Server gebruiken en configureren van de gekoppelde services. Gebruik Hallo **Set AzureVMSqlServerExtension** PowerShell cmdlet tooinstall Hallo-extensie. Hallo volgende opdracht wordt bijvoorbeeld Hallo extensie installeert op een Windows Server-VM (klassiek) en naam 'SQLIaaSExtension'.

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Als u de meest recente versie van de toohello Hallo SQL IaaS-agentextensie bijwerkt, moet u uw virtuele machine opnieuw opstarten na het bijwerken van Hallo-extensie.

> [!NOTE]
> Klassieke virtuele machines niet op een optie tooinstall hebben en Hallo SQL IaaS-Agent uitbreiding via Hallo portal configureren.
> 
> 

## <a name="status"></a>Status
Eenzijdige tooverify dat Hallo-uitbreiding is geïnstalleerd is tooview hello agentstatus in hello Azure-Portal. Selecteer een virtuele machine die worden vermeld in de blade van Hallo virtuele machine en klik vervolgens op **extensies**. U ziet Hallo **SQLIaaSAgent** extensie vermeld.

![SQL Server IaaS-Agent-extensie in de Azure-Portal](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

U kunt ook Hallo **Get-AzureVMSqlServerExtension** Azure Powershell-cmdlet.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Verwijderen
U kunt in Azure Portal Hallo, Hallo extensie verwijderen door te klikken op Hallo weglatingsteken op Hallo **extensies** blade van de eigenschappen van de virtuele machine. Klik vervolgens op **verwijderen**.

![Hallo SQL Server IaaS-agentextensie in de Azure Portal verwijderen](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

U kunt ook Hallo **verwijderen AzureVMSqlServerExtension** Powershell-cmdlet.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Volgende stappen
Beginnen met een Hallo-services worden ondersteund door Hallo extension. Zie voor meer informatie, Hallo onderwerpen waarnaar wordt verwezen in Hallo [ondersteunde services](#supported-services) sectie van dit artikel.

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

