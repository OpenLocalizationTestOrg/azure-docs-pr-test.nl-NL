---
title: aaaSQL Server op virtuele Machines Veelgestelde vragen over Azure | Microsoft Docs
description: In dit artikel vindt u antwoorden op veelgestelde vragen over SQL Server wordt uitgevoerd op Azure Virtual machines toofrequently.
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Veelgestelde vragen over SQL Server op Azure Virtual Machines
Dit onderwerp vindt u antwoorden toosome Hallo Veelgestelde vragen over uitgevoerd [SQL Server op Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

1. **Hoe maak ik een virtuele machine van Azure met SQL Server**

    Hallo gemakkelijke oplossing is toocreate een virtuele Machine met SQL Server. Zie voor een zelfstudie over het aanmelden voor Azure en een SQL-VM maken vanuit de portal hello, [een SQL Server-machine inrichten in Azure Portal Hallo](virtual-machines-windows-portal-sql-server-provision.md). U kunt de installatiekopie van een virtuele machine die gebruikmaakt van betalen per minuut SQL Server-licentieverlening selecteren of kunt u een installatiekopie die toobring, u kunt uw eigen SQL Server-licentie. U hebt ook Hallo optie handmatig installeren van SQL Server op een virtuele machine en een licentie lokale hergebruiken. Als u uw eigen licentie zetten, hebt u [License Mobility through Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Zie [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Prijsrichtlijnen voor SQL Server Azure VM's) voor meer informatie.

1. **Wat is Hallo verschil tussen de SQL-VM's en Hallo SQL Database-service?**

    Conceptueel gezien die SQL Server op Azure een virtuele machine niet die verschilt van het SQL Server wordt uitgevoerd in een externe datacenter. Daarentegen [SQL-Database](../../../sql-database/sql-database-technical-overview.md) database-as-a-service biedt. Met SQL-Database, hoeft u geen toegang tot toohello machines die hosten van uw databases. Zie voor een volledige vergelijking [een cloud SQL Server-optie kiezen: Azure SQL (PaaS) Database of SQL Server op Azure Virtual machines (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Hoe kan ik mijn lokale SQL Server-database toohello Cloud migreren?**

    Eerst een virtuele machine van Azure maken met een SQL Server-exemplaar. Vervolgens migreert u uw lokale databases toothat-exemplaar. Zie voor strategieën voor migratie van gegevens, [migreren van een SQL Server-database tooSQL Server in een Azure VM](virtual-machines-windows-migrate-sql.md).

1. **Kan ik een tweede exemplaar van SQL Server installeren op Hallo dezelfde virtuele machine? Kan ik geïnstalleerde functies van het standaardexemplaar Hallo wijzigen?**

    Ja. Hallo SQL Server-installatiemedia bevindt zich in een map op Hallo **C** station. Voer **Setup.exe** van die locatie tooadd nieuwe SQL Server-exemplaren of -toochange andere geïnstalleerd functies van SQL Server op Hallo-machine. Houd er rekening mee dat sommige functies, zoals automatische back-up automatisch patchen en integratie van Azure Sleutelkluis, alleen op basis van het standaardexemplaar Hallo werken.

1. **Kan ik het Hallo-standaardexemplaar van SQL Server verwijderen?**

    Ja. Maar er zijn enkele overwegingen. Zoals vermeld in de vorige antwoord hello, functies die van Hallo gebruikmaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md) werkt alleen voor het standaardexemplaar Hallo. Als u het standaardexemplaar Hallo verwijdert, wordt Hallo extensie toolook blijft voor en kan er fouten optreden gebeurtenislogboek. Deze fouten zijn van de volgende twee bronnen Hallo: **Microsoft SQL Server-Referentiebeheer** en **Microsoft SQL Server IaaS Agent**. Een van Hallo fouten vergelijkbare toohello volgende mogelijk:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Als u toouninstall Hallo-standaardexemplaar besluit, verwijdert u ook Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md) ook.

1. **Hoe voer ik een upgrade tooa nieuwe versie /-editie van SQL Server in een Azure VM Hallo?**

    Er is momenteel geen in-place upgrade voor SQL Server wordt uitgevoerd in een Azure VM. Een nieuwe virtuele machine van Azure maken met de gewenste Hallo SQL Server versie /-editie, en vervolgens migreren uw databases toohello nieuwe server met behulp van standaard [gegevens migratie technieken](virtual-machines-windows-migrate-sql.md).

1. **Hoe kan ik mijn gelicentieerd exemplaar van SQL Server installeren op een Azure VM?**

    Er zijn twee manieren toodo dit. U kunt een van de Hallo inrichten [installatiekopieën van virtuele machines die ondersteuning biedt voor licenties](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Een andere optie is toocopy Hallo SQL Server-installatie media tooa VM van Windows Server installeer SQL Server op Hallo VM. Voor licentieverlening redenen, moet er [License Mobility through Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Zie [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Prijsrichtlijnen voor SQL Server Azure VM's) voor meer informatie.

1. **Kan ik wijzigen een VM-toouse mijn eigen SQL Server-licentie als deze is gemaakt vanuit een Hallo betalen naar gebruik afbeeldingen?**

    Nee. U kunt niet overschakelen van betalen per minuut licentieverlening toousing uw eigen licentie. Maak een nieuwe Azure virtuele machine met behulp van een Hallo [BYOL installatiekopieën](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), en vervolgens migreren van uw databases toohello nieuwe server met behulp van standaard [gegevens migratie technieken](virtual-machines-windows-migrate-sql.md).

1. **Worden Failover Cluster exemplaren (FCI) voor SQL Server op Azure Virtual machines ondersteund?**

   Ja. U kunt [maken van een Failover-Cluster van Windows op Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) en opslagruimten Direct (S2D) gebruiken voor Hallo clusteropslag. U kunt ook de clustering of opslag oplossingen van derden gebruiken zoals beschreven in [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Heb ik toopay toolicense SQL Server op een virtuele machine van Azure als deze alleen wordt gebruikt voor stand-by/failover?**

    U hebt geen toopay toolicense één SQL Server die als deelneemt passieve secundaire replica in een implementatie van een HA als u Software Assurance en License Mobility zoals beschreven in [virtuele Machine Veelgestelde vragen over licenties](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Hoe worden updates en servicepacks toegepast op een virtuele machine van SQL Server?**

    Virtuele machines kunt u bepalen Hallo hostmachine, inclusief wanneer en hoe u updates wilt toepassen. Hallo-besturingssysteem, kunt u windows-updates handmatig toepassen, of u kunt een Scheduler-service aangeroepen inschakelen [automatisch patchen](virtual-machines-windows-sql-automated-patching.md). Automated Patching installeert alle updates die als belangrijk zijn aangeduid, met inbegrip van SQL Server-updates in deze categorie. Andere optionele updates tooSQL die server moet handmatig worden geïnstalleerd.

1. **Is het mogelijk tooset van configuraties niet weergegeven in de galerie met virtuele machines hello (voor + SQL Server 2012 bijvoorbeeld Windows 2008 R2)?**

    Nee. Voor installatiekopieën van galerie met virtuele machine met SQL Server, moet u een van de Hallo geleverde installatiekopieën.

1. **Hoe installeer hulpprogramma's voor SQL-gegevens op mijn Azure VM?**

     Download en installeer de hulpprogramma's voor SQL-gegevens Hallo van [Microsoft SQL Server Data Tools - Business Intelligence voor Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Resources

Voor een overzicht van SQL Server op Azure Virtual Machines Hallo video bekijken [Azure VM is de beste platform voor SQL Server 2016 Hallo](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). U kunt ook een goede inleiding opvragen in Hallo onderwerp [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

Andere resources zijn onder andere:

* [Een SQL Server-machine inrichten in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md)
* [Migreren van een Database tooSQL Server op een Azure VM](virtual-machines-windows-migrate-sql.md)
* [Hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure virtuele Machines](virtual-machines-windows-sql-high-availability-dr.md)
* [Aanbevolen procedures voor prestaties voor SQL Server op virtuele machines van Azure](virtual-machines-windows-sql-performance.md)
* [Toepassing patronen en ontwikkelingsstrategieën voor SQL Server in Azure virtuele Machines](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 