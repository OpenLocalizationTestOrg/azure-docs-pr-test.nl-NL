---
title: aaaIntegrate Sleutelkluis met SQL Server op Windows-machines in Azure (Resource Manager) | Microsoft Docs
description: Meer informatie over hoe tooautomate Hallo configuratie van SQL Server-versleuteling voor gebruik met Azure Sleutelkluis. Dit onderwerp wordt uitgelegd hoe toouse Azure Sleutelkluis-integratie met SQL Server virtuele machines met Resource Manager gemaakt.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configureren van Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual Machines (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-ps-sql-keyvault.md)
> * [Klassiek](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Overzicht
Er zijn meerdere onderdelen van SQL Server-versleuteling, zoals [transparante gegevensversleuteling (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [kolom: versleuteling op bestandsniveau (wissen)](https://msdn.microsoft.com/library/ms173744.aspx), en [back-upversleuteling](https://msdn.microsoft.com/library/dn449489.aspx). Deze vormen van versleuteling vereisen dat u toomanage en slaan Hallo cryptografische sleutels die u voor versleuteling gebruikt. Hello Azure Key Vault (Azure Sleutelkluis)-service is ontworpen tooimprove Hallo beveiliging en beheer van deze sleutels op een locatie met veilige en maximaal beschikbaar. Hallo [SQL Server-Connector](http://www.microsoft.com/download/details.aspx?id=45344) kunt SQL Server-toouse deze sleutels van Azure Sleutelkluis.

Als u met SQL Server met on-premises machines, er zijn [stappen kunt u tooaccess Azure Key Vault volgen uit uw on-premises SQL Server-machine](https://msdn.microsoft.com/library/dn198405.aspx). Maar voor SQL Server in Azure VM's, kunt u tijd besparen met behulp van Hallo *Azure Sleutelkluis-integratie* functie.

Wanneer deze functie is ingeschakeld, installeert en deze automatisch Hallo SQL Server-Connector, configureert u Hallo EKM-provider tooaccess Azure Sleutelkluis, Hallo referentie tooallow maakt u tooaccess uw kluis. Als u het hebt bekeken Hallo stappen in Hallo genoemde lokale documentatie, ziet u dat deze functie automatiseert stap 2 en 3. Hallo enige dat u nog moet toodo handmatig is toocreate hello sleutelkluis en de sleutels. Van daaruit wordt Hallo volledige installatie van de SQL-VM geautomatiseerd. Zodra deze functie kan voor deze installatie is voltooid, kunt u de T-SQL-instructies toobegin normaal versleutelen van uw databases of back-ups uitvoeren.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Inschakelen en configureren van Azure Sleutelkluis-integratie
U kunt Azure Sleutelkluis-integratie tijdens het inrichten of configureren voor een bestaande virtuele machines.

### <a name="new-vms"></a>Nieuwe virtuele machines
Als u een nieuwe virtuele SQL Server-machine met Resource Manager inricht, biedt hello Azure-portal een stap tooenable Azure Sleutelkluis-integratie. Hello Azure Sleutelkluis-functie is alleen beschikbaar voor Hallo Enterprise, Developer, en evaluatie-editie van SQL Server.

![Integratie van Azure Sleutelkluis in SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Zie voor een gedetailleerd overzicht van de inrichting [een SQL Server-machine inrichten in Azure Portal Hallo](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Bestaande virtuele machines
Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines. Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.

![SQL Azure Sleutelkluis-integratie voor bestaande virtuele machines](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo sectie geautomatiseerde Sleutelkluis-integratie.

![SQL Azure Sleutelkluis-integratie voor bestaande virtuele machines configureren](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.

> [!NOTE]
> U kunt ook Azure Sleutelkluis-integratie met een sjabloon configureren. Zie voor meer informatie [Azure quickstart-sjabloon voor Azure Sleutelkluis-integratie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

