---
title: aaaStorage configuratie voor SQL Server-VM's | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe Azure storage voor VM's van SQL Server tijdens het inrichten (Resource Manager-implementatiemodel) configureert. Ook wordt uitgelegd hoe u opslag kunt configureren voor uw bestaande SQL Server-VM's.
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Configuratie van de opslag voor virtuele machines van SQL Server
Wanneer u een installatiekopie van de virtuele machine SQL Server in Azure configureren, helpt Hallo Portal tooautomate opslagconfiguratie. Dit omvat het koppelen van opslag toohello VM, zodat deze toegankelijk tooSQL van storage Server en toooptimize voor uw specifieke vereisten te configureren.

Dit onderwerp wordt uitgelegd hoe Azure configureert opslag voor uw VM's van SQL Server tijdens het inrichten, en ook voor bestaande virtuele machines. Deze configuratie is gebaseerd op Hallo [best practices prestaties](virtual-machines-windows-sql-performance.md) voor Azure virtuele machines waarop SQL Server wordt uitgevoerd.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Vereisten
toouse hello automatische configuratie-instellingen voor opslag, de virtuele machine vereist Hallo volgende kenmerken:

* Ingericht met een [image in SQL Server-galerie](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Maakt gebruik van Hallo [Resource Manager-implementatiemodel](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Maakt gebruik van [Premium-opslag](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Nieuwe virtuele machines
Hallo volgende secties wordt beschreven hoe tooconfigure opslag voor de nieuwe virtuele machines van de SQL Server.

### <a name="azure-portal"></a>Azure Portal
Bij het inrichten van een virtuele machine met de installatiekopie van een SQL Server-galerie van Azure, kunt u tooautomatically Hallo opslag configureren voor uw nieuwe virtuele machine. U geeft opslaggrootte hello, prestatielimieten en type werkbelasting. Hallo volgende schermafbeelding ziet u Hallo opslag configuratie blade die wordt gebruikt tijdens SQL VM-inrichting.

![SQL Server VM-opslag-configuratie tijdens het inrichten](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

Op basis van uw keuze, voert Azure Hallo opslagconfiguratietaken na het maken van Hallo VM te volgen:

* Maakt en koppelt premium-opslag gegevens schijven toohello virtuele machine.
* Hallo gegevens schijven toobe toegankelijk tooSQL Server configureert.
* Hallo gegevensschijven configureert in een storage pool op basis van Hallo opgegeven grootte en de prestaties (IOPS en doorvoerlimieten)-vereisten.
* Hallo opslaggroep koppelt aan een nieuw station op Hallo virtuele machine.
* Deze nieuwe station op basis van het type van de opgegeven werkbelasting (datawarehousing, transactionele verwerking of algemeen) worden geoptimaliseerd.

Zie voor meer informatie over hoe Azure storage-instellingen configureert Hallo [opslag configuratiesectie](#storage-configuration). Voor een overzicht van hoe toocreate een SQL Server VM in Azure Portal Hallo zien [Hallo zelfstudie inrichting](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Sjablonen voor resource beheren
Als u Hallo Resource Manager-sjablonen te volgen, worden twee premium gegevensschijven met geen opslaggroepconfiguratie wordt standaard gekoppeld. U kunt echter deze sjablonen toochange Hallo aantal premium-schijven voor gegevens die zijn aangesloten toohello virtuele machine aanpassen.

* [Virtuele machine met automatische back-up maken](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Virtuele machine maken met automatisch patchen](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Virtuele machine maken met Azure Sleutelkluis-integratie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>Bestaande virtuele machines
U kunt een aantal instellingen voor de opslag in hello Azure-portal wijzigen voor bestaande SQL Server-VM's. Selecteer uw virtuele machine, gaat u gebied toohello-instellingen en selecteer SQL Server-configuratiebestand. Hallo SQL Server-configuratiebestand blade ziet Hallo huidige gebruik van opslag van uw virtuele machine. Alle stations die bestaan op de virtuele machine worden weergegeven in deze grafiek. Voor elk station wordt Hallo opslagruimte weergegeven in vier secties:

* SQL-gegevens
* SQL-logboek
* Andere (niet-SQL-opslag)
* Beschikbaar

![Opslag configureren voor een bestaande SQL Server VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure Hallo opslag tooadd een nieuw station of een bestaand station uitbreiden, klik op Hallo bewerken boven Hallo-diagram.

Hallo-configuratieopties die u ziet, is afhankelijk van of u deze functie voordat hebt gebruikt. Wanneer u voor Hallo eerst, kunt u uw opslagvereisten voor een nieuw station opgeven. Als u deze functie toocreate een station eerder gebruikt, kunt u tooextend opslag dat station.

### <a name="use-for-hello-first-time"></a>Gebruik voor de eerste keer Hallo
Als de eerste keer dat u deze functie is, kunt u opgeven Hallo grootte en de prestaties opslaglimieten voor een nieuwe schijf. Deze ervaring is vergelijkbaar toowhat u ziet bij het inrichten van tijd. Hallo belangrijkste verschil is dat u toospecify Hallo werkbelasting type niet zijn toegestaan. Deze beperking wordt voorkomen dat een bestaande SQL Server-configuraties op Hallo virtuele machine onderbreken.

![SQL Server-opslag schuifregelaars configureren](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure maakt een nieuw station op basis van uw specificaties. In dit scenario voert Azure Hallo opslagconfiguratietaken te volgen:

* Maakt en koppelt premium-opslag gegevens schijven toohello virtuele machine.
* Hallo gegevens schijven toobe toegankelijk tooSQL Server configureert.
* Hallo gegevensschijven configureert in een storage pool op basis van Hallo opgegeven grootte en de prestaties (IOPS en doorvoerlimieten)-vereisten.
* Hallo opslaggroep koppelt aan een nieuw station op Hallo virtuele machine.

Zie voor meer informatie over hoe Azure storage-instellingen configureert Hallo [opslag configuratiesectie](#storage-configuration).

### <a name="add-a-new-drive"></a>Voeg een nieuw station
Als u al opslag hebt geconfigureerd op uw SQL Server VM, wordt het uitbreiden van de opslag twee nieuwe opties. de eerste optie Hallo is tooadd een nieuwe schijf, waarvoor een prestatieniveau Hallo van uw virtuele machine kunt verhogen.

![Voeg een nieuw station tooa SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Na het Hallo-station toevoegen, moet u echter bepaalde extra handmatige configuratie tooachieve Hallo prestaties toename uitvoeren.

### <a name="extend-hello-drive"></a>Hallo schijf uitbreiden
Hallo is andere optie voor het uitbreiden van de opslag tooextend Hallo bestaande station. Deze optie verhoogt Hallo beschikbare opslag voor de schijf, maar niet wordt verhoogd tot prestaties. Met opslaggroepen wijzigen u het aantal kolommen Hallo niet nadat het Hallo-opslaggroep wordt gemaakt. Hallo aantal kolommen bepaalt het aantal parallelle schrijfbewerkingen, die worden striped op verschillende gegevensschijven Hallo opgeslagen kan Hallo. Eventuele extra gegevensschijven kunnen daarom niet prestaties verhogen. Ze kunnen alleen meer opslag bieden voor Hallo gegevens die worden geschreven. Deze beperking wordt ook betekent dat, wanneer u Hallo schijf uitbreidt, het aantal kolommen Hallo bepaalt de Hallo minimum aantal gegevensschijven die u kunt toevoegen. Als u een opslaggroep met vier gegevensschijven maakt, dus het aantal kolommen Hallo ook vier. Elk gewenst moment uitbreiden van Hallo opslag, moet u ten minste vier gegevensschijven toevoegen.

![Uitbreiden van een station voor een SQL-VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Opslagconfiguratie
Deze sectie bevat een verwijzing voor Hallo opslag configuratiewijzigingen die door Azure worden automatisch uitgevoerd tijdens de configuratie in hello Azure Portal of SQL VM-inrichting.

* Als u minder dan twee TBs van opslag voor uw virtuele machine hebt geselecteerd, wordt in Azure een opslaggroep niet maken.
* Als u ten minste twee TBs van opslag voor uw virtuele machine hebt geselecteerd, configureert Azure een opslaggroep. Hallo volgende sectie van dit onderwerp biedt Hallo details van de opslaggroepconfiguratie Hallo.
* Maakt gebruik van automatische opslagconfiguratie altijd [premium-opslag](../../../storage/common/storage-premium-storage.md) P30 gegevensschijven. Als gevolg daarvan kan een 1:1-koppeling tussen het geselecteerde aantal terabyte en het aantal gegevensschijven Hallo tooyour VM gekoppeld.

Zie voor informatie over prijzen, Hallo [prijzen Storage](https://azure.microsoft.com/pricing/details/storage) pagina op Hallo **schijfopslag** tabblad.

### <a name="creation-of-hello-storage-pool"></a>Het maken van de opslaggroep Hallo
Azure maakt gebruik van Hallo instellingen toocreate Hallo opslaggroep op SQL Server-VM's te volgen.

| Instelling | Waarde |
| --- | --- |
| Stripe-grootte |256 KB (gegevensopslag); 64 KB (transactionele) |
| Schijfformaten |1 TB |
| Cache |Lezen |
| Toegewezen grootte |De clustergrootte van 64 KB NTFS |
| Initialisatie van de directe bestanden |Ingeschakeld |
| Pagina's in het geheugen vergrendelen |Ingeschakeld |
| Herstel |Eenvoudig herstel (geen tolerantie) |
| Aantal kolommen |Aantal gegevensschijven<sup>1</sup> |
| TempDB-locatie |Opgeslagen op gegevensschijven<sup>2</sup> |

<sup>1</sup> nadat Hallo opslaggroep is gemaakt, het aantal kolommen in de opslaggroep Hallo Hallo kan niet worden gewijzigd.

<sup>2</sup> deze instelling geldt alleen toohello eerste schijf die u maakt met de functie Hallo-opslag-configuratie.

## <a name="workload-optimization-settings"></a>Werkbelasting optimalisatie-instellingen
Hallo volgende tabel staan Hallo drie werkbelasting type beschikbare opties en hun bijbehorende optimalisaties:

| Type werkbelasting | Beschrijving | Optimalisaties |
| --- | --- | --- |
| **Algemeen** |Standaardinstelling die ondersteuning biedt voor de meeste werkbelastingen |Geen |
| **Transactionele verwerking** |Hallo-opslag voor OLTP-workloads van traditionele databases geoptimaliseerd |Traceringsvlag 1117<br/>Traceringsvlag 1118 |
| **Gegevensopslag** |Optimaliseert de opslag voor analyse- en rapportageworkloads Hallo |Traceringsvlag 610<br/>Traceringsvlag 1117 |

> [!NOTE]
> U kunt alleen een type van de werkbelasting Hallo opgeven wanneer u een virtuele SQL-machine inrichten door deze te selecteren in Hallo opslag configuratiestap.
>
>

## <a name="next-steps"></a>Volgende stappen
Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).
