---
title: aaaAutomate beheertaken op SQL-machines (Resource Manager) | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toomanage Hallo voor SQL Server agent-extensie, die specifieke SQL Server-beheertaken worden geautomatiseerd. Het gaat hierbij om automatische back-up automatisch patchen en integratie van Azure Sleutelkluis. In dit onderwerp maakt gebruik van modus Hallo Resource Manager-implementatie.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatiseren beheertaken op Azure Virtual Machines Hello SQL Server Agent-extensie (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Klassiek](../classic/sql-server-agent-extension.md)
> 
> 

Hallo uitbreiding IaaS-Agent voor SQL Server (SQLIaaSExtension) wordt uitgevoerd op virtuele machines in Azure tooautomate beheertaken. Dit onderwerp bevat een overzicht van Hallo-services wordt ondersteund door het Hallo-extensie, evenals de instructies voor installatie, status en verwijdering.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello klassieke versie van dit artikel, Zie [SQL Server Agent-extensie voor SQL Server-machines klassieke](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Ondersteunde services
Hallo uitbreiding voor SQL Server IaaS-Agent ondersteunt Hallo beheertaken te volgen:

| Beheer-functie | Beschrijving |
| --- | --- |
| **Automatische back-up van SQL** |Automatiseert Hallo planning van de back-ups voor alle databases voor het standaardexemplaar van SQL Server in Hallo VM Hallo. Zie voor meer informatie [automatische back-up voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Automatisch patchen van SQL** |Hiermee configureert u een onderhoudsvenster tijdens welke updates plaatsen tooyour VM kan duren, zodat u voorkomen de updates tijdens piektijden voor uw workload dat kunt. Zie voor meer informatie [automatisch patchen voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Integratie van Azure Key Vault** |Hiermee schakelt u tooautomatically installeren en configureren van Azure Sleutelkluis op uw SQL Server-VM. Zie voor meer informatie [configureren Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual machines (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Eenmaal geïnstalleerd en uitgevoerd, maakt Hallo uitbreiding voor SQL Server IaaS-Agent deze beheerfuncties beschikbaar in SQL Server-paneel Hallo van Hallo virtuele machine in Azure Portal Hallo en via Azure PowerShell voor SQL Server marketplace-installatiekopieën en via Azure PowerShell voor handmatige installaties van Hallo-uitbreiding. 

## <a name="prerequisites"></a>Vereisten
Vereisten toouse Hallo uitbreiding van SQL Server IaaS-Agent op de virtuele machine:

**Besturingssysteem**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server-versies**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Downloaden en configureren van de meest recente Azure PowerShell-opdrachten Hallo](/powershell/azure/overview)

## <a name="installation"></a>Installeren
Hallo uitbreiding voor SQL Server IaaS-Agent wordt automatisch geïnstalleerd wanneer u een van de Hallo SQL Server-virtuele machine afbeeldingen inricht. Als u tooreinstall Hallo uitbreiding handmatig op een van deze VM's van SQL Server moet, gebruikt u Hallo volgende PowerShell-opdracht:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Het is ook mogelijk tooinstall Hallo uitbreiding voor SQL Server IaaS-Agent op de virtuele machine van een alleen-OS Windows-Server. Dit wordt alleen ondersteund als u SQL Server ook handmatig hebt geïnstalleerd op deze machine. En vervolgens installeren Hallo extensie handmatig met behulp van dezelfde Hallo **Set AzureVMSqlServerExtension** PowerShell-cmdlet.

> [!NOTE]
> Als u Hallo uitbreiding voor SQL Server IaaS-Agent handmatig op een alleen-besturingssysteem Windows Server-VM installeren, kunt u geen Hallo SQL Server-configuratie-instellingen via hello Azure-portal beheren. In dit scenario moet u alle wijzigingen met PowerShell.

## <a name="status"></a>Status
Eenzijdige tooverify dat Hallo-uitbreiding is geïnstalleerd is tooview hello agentstatus in hello Azure-Portal. Selecteer **alle instellingen** in Hallo blade van de virtuele machine en klik vervolgens op **extensies**. U ziet Hallo **SQLIaaSExtension** extensie vermeld.

![SQL Server IaaS-Agent-extensie in de Azure-Portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

U kunt ook Hallo **Get-AzureVMSqlServerExtension** Azure Powershell-cmdlet.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

vorige opdracht Hallo bevestigt Hallo-agent is geïnstalleerd en vindt u algemene statusinformatie. U kunt ook specifieke statusinformatie ophalen over automatische back-up en Patching Hello opdrachten te volgen.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Verwijderen
U kunt in Azure Portal Hallo, Hallo extensie verwijderen door te klikken op Hallo weglatingsteken op Hallo **extensies** blade van de eigenschappen van de virtuele machine. Klik vervolgens op **verwijderen**.

![Hallo SQL Server IaaS-agentextensie in de Azure Portal verwijderen](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

U kunt ook Hallo **verwijderen AzureRmVMSqlServerExtension** Powershell-cmdlet.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Volgende stappen
Beginnen met een Hallo-services worden ondersteund door Hallo extension. Zie voor meer informatie, Hallo onderwerpen waarnaar wordt verwezen in Hallo [ondersteunde services](#supported-services) sectie van dit artikel.

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

