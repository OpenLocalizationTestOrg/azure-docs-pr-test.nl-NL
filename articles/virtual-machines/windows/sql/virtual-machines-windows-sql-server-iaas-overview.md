---
title: aaaOverview van SQL Server op Azure Virtual Machines | Microsoft Docs
description: "Meer informatie over hoe toorun volledige edities van SQL Server op Azure Virtual machines. Directe koppelingen tooall SQL Server VM-installatiekopieën en verwante inhoud opvragen."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Overzicht van SQL Server op virtuele machines in Azure
In dit onderwerp beschrijft uw opties voor het uitvoeren van SQL Server op Azure virtuele machines (VM's), samen met [tooportal installatiekopieën koppelingen](#option-1-create-a-sql-vm-with-per-minute-licensing) en een overzicht van [algemene taken](#manage-your-sql-vm).

> [!NOTE]
> Als u al bekend met SQL Server bent en alleen wilt toosee hoe een virtuele machine van SQL Server toodeploy zien [een SQL Server-machine inrichten in hello Azure-portal](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Overzicht
Als u een databasebeheerder of een ontwikkelaar, bevatten Azure VM's een toomove manier uw lokale SQL Server werkbelastingen en toepassingen toohello Cloud. Hallo biedt volgende video een technisch overzicht van Azure VM's van SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hallo video heeft betrekking op Hallo gebieden te volgen:

| Time | Onderwerp |
| --- | --- |
| 00:21 |Wat zijn VM's in Azure? |
| 01:45 |Beveiliging |
| 02:50 |Connectiviteit |
| 03:30 |Betrouwbaarheid en prestaties van de opslag |
| 05:20 |Formaten van virtuele machines |
| 05:54 |Hoge beschikbaarheid en SLA |
| 07:30 |Configuratieondersteuning |
| 08:00 |Bewaking |
| 08:32 |Demo: een virtuele machine met SQL Server 2016 maken |

> [!NOTE]
> Hallo video legt de nadruk op SQL Server 2016, maar Azure biedt een VM-installatiekopieën voor meerdere versies van SQL Server, inclusief 2012, 2014 en 2016. 
> 
> 

## <a name="scenarios"></a>Scenario's
Er zijn diverse redenen die u ervoor toohost uw gegevens in Azure kiezen kunt. Als uw toepassing tooAzure verplaatst is, verbetert het tooalso verplaatsen Hallo prestatiegegevens. Maar er zijn nog andere voordelen. U hebt automatisch toegang toomultiple datacenters voor een wereldwijde aanwezigheid en herstel na noodgevallen. Hallo-gegevens is ook maximaal beveiligde en duurzame.

SQL Server dat wordt uitgevoerd op virtuele machines in Azure is één mogelijkheid om relationele gegevens in Azure op te slaan. Het is een goede keuze voor verschillende scenario's. Bijvoorbeeld, kunt u tooconfigure hello Azure VM zo mogelijk tooan lokale SQL Server-machine. Of u kunt aanvullende toorun-toepassingen en services op Hallo dezelfde databaseserver. Er zijn twee belangrijke informatiebronnen die u helpen nog meer scenario's en overwegingen te bedenken:

* [SQL Server op virtuele machines in Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) biedt een overzicht van Hallo beste scenario's voor het gebruik van SQL Server op Azure Virtual machines. 
* Zie [Een SQL Server-optie voor de cloud kiezen: Azure SQL (PaaS) Database of SQL Server op virtuele machines in Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) voor een gedetailleerde vergelijking tussen SQL Database en SQL Server dat wordt uitgevoerd op een virtuele machine.

## <a name="create-a-new-sql-vm"></a>Een nieuwe SQL-VM maken
Hallo volgende secties bieden rechtstreekse koppelingen toohello Azure-portal voor Hallo SQL Server-virtuele machine afbeeldingen. Afhankelijk van het Hallo-installatiekopie die u selecteert, kunt u beide betaalt licentiekosten per minuut op basis van een SQL Server of u kunt uw eigen license (BYOL) zetten.

Stapsgewijze instructies voor het maken van een nieuwe SQL-VM in Hallo zelfstudie vinden [een SQL Server-machine inrichten in hello Azure-portal](virtual-machines-windows-portal-sql-server-provision.md). Bekijk ook Hallo [best practices prestaties for SQL Server-VM's](virtual-machines-windows-sql-performance.md), waarin wordt uitgelegd hoe tooselect Hallo juiste machine grootte en andere functies beschikbaar tijdens het inrichten.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Optie 1: een SQL-VM maken met licentiekosten per minuut
Hallo bevat volgende tabel een matrix met de meest recente SQL Server-installatiekopieën Hallo in de galerie met virtuele machines Hallo. Klik op een koppeling toobegin maken van een nieuwe SQL-VM met de opgegeven versie, de editie en het besturingssysteem. 

> [!TIP]
> Zie toounderstand Hallo VM en SQL prijzen voor deze installatiekopieën [richtlijnen voor Azure VM's van SQL Server-prijzen](virtual-machines-windows-sql-server-pricing-guidance.md).

| Versie | Besturingssysteem | Editie |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Bovendien toothis lijst andere combinaties van besturingssystemen en versies van SQL Server zijn beschikbaar. Andere installatiekopieën via een zoekopdracht in de marketplace niet vinden in hello Azure-portal. 

## <a id="BYOL"></a> Optie 2: een SQL-VM maken met een bestaande licentie
U kunt ook uw eigen licentie gebruiken (Bring Your Own Licence, BYOL). In dit scenario betaalt u alleen voor Hallo VM zonder eventuele extra kosten voor SQL Server-licentieverlening. toouse uw eigen licentie, gebruik Hallo matrix van SQL Server-versies, edities en besturingssystemen die hieronder. In Hallo-portal, de namen van deze afbeeldingen worden voorafgegaan door **{BYOL}**.

> [!TIP]
> Als u uw eigen licentie hebt, kan dit u in de loop van de tijd geld besparen voor doorlopende productieworkloads. Zie [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Prijsrichtlijnen voor SQL Server Azure VM's) voor meer informatie.

| Version | Besturingssysteem | Editie |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Bovendien toothis lijst andere combinaties van besturingssystemen en versies van SQL Server zijn beschikbaar. Andere installatiekopieën via een zoekopdracht in de marketplace niet vinden in hello Azure-portal (zoek 'SQL-Server {BYOL}').

> [!IMPORTANT]
> toouse BYOL VM-installatiekopieën, moet u een Enterprise-overeenkomst met hebben [License Mobility through Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). U moet ook een geldige licentie voor Hallo versie /-editie van SQL Server die u wilt toouse. U moet [bieden Hallo benodigde BYOL informatie tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) binnen **10** dagen na inrichting van uw virtuele machine. 

> [!NOTE]
> Het is niet mogelijk toochange Hallo licentieverlening model van een SQL Server VM betalen per minuut toouse uw eigen licentie. In dit geval moet u een nieuwe BYOL VM maken en migreren van uw databases toohello nieuwe virtuele machine. 

## <a name="manage-your-sql-vm"></a>Uw virtuele SQL-machine beheren
Na het inrichten van uw virtuele SQL Server-machine zijn er verschillende optionele beheertaken die u kunt uitvoeren. Met betrekking tot bepaalde aspecten kunt u SQL Server op exact dezelfde manier configureren en beheren als u met een on-premises SQL Server-exemplaar zou doen. Sommige taken zijn echter specifieke tooAzure. Hallo Markeer volgende secties sommige van deze gebieden met koppelingen toomore informatie.

### <a name="connect-toohello-vm"></a>Verbinding maken met toohello VM
Een van de meest eenvoudige stappen die management Hallo is tooconnect tooyour SQL Server VM via hulpprogramma's, zoals SQL Server Management Studio (SSMS). Voor instructies over hoe tooconnect tooyour nieuwe SQL Server VM, Zie [verbinding maken met virtuele Machine van SQL Server op Azure tooa](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Uw gegevens migreren
Als u een bestaande database hebt, moet u toomove die toohello zojuist SQL VM ingericht. Zie voor een lijst met migratieopties en begeleiding, [migreren van een Database tooSQL Server op een Azure VM](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Hoge beschikbaarheid configureren
Als u hoge beschikbaarheid nodig hebt, overweeg dan SQL Server-beschikbaarheidsgroepen te configureren. Hierbij combineert u meerdere virtuele machines in Azure tot een virtueel netwerk. Hello Azure-portal heeft een sjabloon die deze configuratie voor u ingesteld. Zie [Een AlwaysOn-beschikbaarheidsgroep configureren op virtuele machines in Azure Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie. Als u wilt toomanually configureert de beschikbaarheidsgroep en de bijbehorende listener Zie [AlwaysOn-beschikbaarheidsgroepen configureren in Azure VM](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Raadpleeg voor andere overwegingen met betrekking tot hoge beschikbaarheid [Hoge beschikbaarheid en herstel na een noodgeval voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Een back-up maken van uw gegevens
Virtuele machines in Azure kunnen profiteren van [automatische back-up](virtual-machines-windows-sql-automated-backup.md), die regelmatig back-ups van uw database tooblob-opslag maakt. U kunt deze techniek ook handmatig gebruiken. Zie [Azure Storage gebruiken voor back-up en herstel van SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md) voor meer informatie. Zie [Back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md) voor een overzicht van alle opties voor back-up en herstel.

### <a name="automate-updates"></a>Updates automatiseren
Virtuele machines in Azure kunt [automatisch patchen](virtual-machines-windows-sql-automated-patching.md) tooschedule een onderhoudsvenster voor het installeren van belangrijke windows- en SQL Server wordt automatisch bijgewerkt.

### <a name="customer-experience-improvement-program-ceip"></a>Programma voor kwaliteitsverbetering (CEIP)
Hallo Customer Experience Improvement Program (CEIP) is standaard ingeschakeld. Dit periodiek verzendt rapporten tooMicrosoft toohelp verbeteren SQL Server. Er is geen beheertaak vereist met het programma voor Kwaliteitsverbetering, tenzij u toodisable wilt deze na het inrichten. U kunt aanpassen of uitschakelen van Hallo CEIP toohello VM verbinding met extern bureaublad. Voer Hallo **SQL Server-fout- en gebruiksrapportage** hulpprogramma. Ga als volgt Hallo instructies toodisable reporting. 

Zie voor meer informatie de sectie CEIP van Hallo Hallo [licentievoorwaarden accepteren](https://msdn.microsoft.com/library/ms143343.aspx) onderwerp. 

## <a name="next-steps"></a>Volgende stappen

Zie voor vragen over prijzen [richtlijnen voor Azure VM's van SQL Server-prijzen](virtual-machines-windows-sql-server-pricing-guidance.md) en Hallo [Azure pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Selecteer de doeleditie van SQL Server in Hallo **OS-Software** lijst. Bekijk vervolgens Hallo prijzen voor virtuele machines die anders grootte.

Nog vragen? Kijk eerst Hallo [SQL Server op virtuele Machines Veelgestelde vragen over Azure](virtual-machines-windows-sql-server-iaas-faq.md). Maar ook uw vragen of opmerkingen toohello onderaan alle onderwerpen SQL VM toointeract toevoegen met Microsoft en Hallo-community.
