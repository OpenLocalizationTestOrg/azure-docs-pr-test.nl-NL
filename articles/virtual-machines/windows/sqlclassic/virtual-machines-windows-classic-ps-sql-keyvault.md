---
title: aaaIntegrate Sleutelkluis met SQL Server op Windows-machines in Azure (klassiek) | Microsoft Docs
description: Meer informatie over hoe tooautomate Hallo configuratie van SQL Server-versleuteling voor gebruik met Azure Sleutelkluis. Dit onderwerp wordt uitgelegd hoe toouse Azure Sleutelkluis-integratie met SQL Server virtuele machines in het klassieke implementatiemodel Hallo maken.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configureren van Azure Sleutelkluis-integratie voor SQL Server op virtuele Machines in Azure (klassiek)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Klassiek](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Overzicht
Er zijn meerdere onderdelen van SQL Server-versleuteling, zoals [transparante gegevensversleuteling (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [kolom: versleuteling op bestandsniveau (wissen)](https://msdn.microsoft.com/library/ms173744.aspx), en [back-upversleuteling](https://msdn.microsoft.com/library/dn449489.aspx). Deze vormen van versleuteling vereisen dat u toomanage en slaan Hallo cryptografische sleutels die u voor versleuteling gebruikt. Hello Azure Key Vault (Azure Sleutelkluis)-service is ontworpen tooimprove Hallo beveiliging en beheer van deze sleutels op een locatie met veilige en maximaal beschikbaar. Hallo [SQL Server-Connector](http://www.microsoft.com/download/details.aspx?id=45344) kunt SQL Server-toouse deze sleutels van Azure Sleutelkluis.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Als u SQL Server met lokale virtuele machines uitvoert, zijn er [stappen kunt u tooaccess Azure Key Vault volgen uit uw on-premises SQL Server-machine](https://msdn.microsoft.com/library/dn198405.aspx). Maar voor SQL Server in Azure VM's, kunt u tijd besparen met behulp van Hallo *Azure Sleutelkluis-integratie* functie. Met een paar Azure PowerShell-cmdlets tooenable deze functie kunt u automatiseren Hallo configuratie nodig is voor een SQL VM tooaccess de sleutelkluis.

Wanneer deze functie is ingeschakeld, installeert en deze automatisch Hallo SQL Server-Connector, configureert u Hallo EKM-provider tooaccess Azure Sleutelkluis, Hallo referentie tooallow maakt u tooaccess uw kluis. Als u het hebt bekeken Hallo stappen in Hallo genoemde lokale documentatie, ziet u dat deze functie automatiseert stap 2 en 3. Hallo enige dat u nog moet toodo handmatig is toocreate hello sleutelkluis en de sleutels. Van daaruit wordt Hallo volledige installatie van de SQL-VM geautomatiseerd. Zodra deze functie kan voor deze installatie is voltooid, kunt u de T-SQL-instructies toobegin normaal versleutelen van uw databases of back-ups uitvoeren.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configureren van Azure Sleutelkluis-integratie
Gebruik PowerShell tooconfigure Azure Sleutelkluis-integratie. Hallo volgende secties bieden een overzicht van Hallo vereiste parameters en vervolgens een voorbeeld van een PowerShell-script.

### <a name="install-hello-sql-server-iaas-extension"></a>Hallo IaaS-uitbreiding voor SQL-Server installeren
Eerst [installeren Hallo uitbreiding van SQL Server IaaS](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Hallo invoerparameters begrijpen
Hallo volgende Hallo parameters van de tabel lijsten vereist toorun Hallo PowerShell-script in de volgende sectie Hallo.

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| **$akvURL** |**Hallo sleutelkluis-URL** |'https://contosokeyvault.vault.azure.net/' |
| **$spName** |**Service-Principal-naam** |'fde2b411 - 33d 5-4e11-af04eb07b669ccf2' |
| **$spSecret** |**Service-Principal-geheim** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM =" |
| **$credName** |**Referentienaam**: Azure Sleutelkluis-integratie maakt u een referentie binnen SQL Server, zodat Hallo VM toohave toegang toohello sleutelkluis. Kies een naam voor deze referentie. |'mycred1' |
| **$vmName** |**Naam van virtuele machine**: Hallo-naam van een eerder gemaakte SQL-VM. |'myvmname' |
| **$serviceName** |**Servicenaam**: Hallo Cloud Service-naam die is gekoppeld aan Hallo SQL VM. |'mycloudservicename' |

### <a name="enable-akv-integration-with-powershell"></a>Inschakelen van Azure Sleutelkluis-integratie met PowerShell
Hallo **nieuw AzureVMSqlServerKeyVaultCredentialConfig** cmdlet maakt een configuratieobject voor hello Azure Sleutelkluis-integratie-functie. Hallo **Set AzureVMSqlServerExtension** configureert deze integratie met Hallo **KeyVaultCredentialSettings** parameter. Hallo van de volgende stappen tonen hoe toouse deze opdrachten.

1. In Azure PowerShell eerst configureren Hallo invoerparameters met uw specifieke waarden zoals beschreven in de vorige secties Hallo van dit onderwerp. Hallo script volgen is een voorbeeld.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Vervolgens gebruik Hallo volgende tooconfigure script en inschakelen van Azure Sleutelkluis-integratie.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Hallo SQL IaaS-Agent uitbreiding wordt Hallo SQL VM bijgewerkt met deze nieuwe configuratie.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

