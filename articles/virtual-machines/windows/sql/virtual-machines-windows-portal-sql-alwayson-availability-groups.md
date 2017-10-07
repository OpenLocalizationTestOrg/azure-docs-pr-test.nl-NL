---
title: aaaSet van hoge beschikbaarheid voor virtuele machines van Azure Resource Manager | Microsoft Docs
description: Deze zelfstudie leert u hoe toocreate geen AlwaysOn-beschikbaarheidsgroep met Azure virtuele machines in de modus Azure Resource Manager groepeert.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Altijd op beschikbaarheidsgroepen automatisch in Azure Virtual Machines configureren: Resource Manager

Deze zelfstudie leert u hoe toocreate de beschikbaarheid van een SQL Server die maakt gebruik van virtuele machines van Azure resourcemanager groepeert. Hallo-zelfstudie maakt gebruik van Azure-blades tooconfigure een sjabloon. U kunt Hallo standaardinstellingen bekijken, typt u vereiste instellingen en Hallo blades in Hallo portal bijwerken als u deze zelfstudie hebt doorlopen.

Hallo voltooid zelfstudie maakt een SQL Server-beschikbaarheidsgroep op Azure Virtual Machines die Hallo volgende elementen bevatten:

* Een virtueel netwerk met meerdere subnetten, met inbegrip van een front-end- en een back-end-subnet
* Twee domeincontrollers waarvoor Active Directory-domein
* Twee virtuele machines waarop SQL Server wordt uitgevoerd en zijn geïmplementeerde toohello back-end-subnet en gekoppelde toohello Active Directory-domein
* Een drie-knooppunt van een failovercluster met Hallo Knooppuntmeerderheid quorummodel
* Een beschikbaarheidsgroep met twee synchrone doorvoer replica's van een beschikbaarheidsdatabase

Hallo volgende illustratie vertegenwoordigt de volledige oplossing Hallo.

![Testlab-architectuur voor beschikbaarheidsgroepen in Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Alle resources in deze oplossing behoren tooa één resourcegroep.

Voordat u deze zelfstudie begint, moet u bevestigen Hallo volgende:

* U hebt al een Azure-account. Als u nog geen hebt, [aanmelden voor een proefaccount](http://azure.microsoft.com/pricing/free-trial/).
* Weet u al hoe toouse Hallo GUI tooprovision een virtuele machine van SQL Server uit de galerie met virtuele machines Hallo. Zie voor meer informatie [inrichten van een virtuele machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).
* U hebt al een goed begrip van beschikbaarheidsgroepen. Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Als u geïnteresseerd bent in het gebruik van beschikbaarheidsgroepen met SharePoint, zien ook de [configureren van SQL Server 2012 Always On beschikbaarheidsgroepen voor SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

In deze zelfstudie gebruikt u hello Azure portal naar:

* Kies sjabloon voor altijd op Hallo van Hallo-portal.
* Hallo sjablooninstellingen controleren en bijwerken van een aantal configuratie-instellingen voor uw omgeving.
* Monitor Azure als het volledige Hallo-omgeving maakt.
* Verbindt tooa domeincontroller en vervolgens tooa-server die SQL Server uitvoert.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Hallo-cluster inrichten vanuit galerie Hallo
Azure biedt een afbeelding voor de hele oplossing Hallo. toolocate hello sjabloon:

1. Meld u toohello Azure-portal met behulp van uw account.
2. Klik in hello Azure-portal, op **+ nieuw** tooopen hello **nieuw** blade.
3. Op Hallo **nieuw** blade, zoekt u **AlwaysOn**.
   ![AlwaysOn-sjabloon zoeken](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Zoek in de zoekresultaten Hallo **SQL Server AlwaysOn-Cluster**.
   ![AlwaysOn-sjabloon](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. Op **een implementatiemodel selecteren**, kies **Resource Manager**.

### <a name="basics"></a>Basisbeginselen
Klik op **basisbeginselen** en Hallo volgende instellingen configureren:

* **Gebruikersnaam van beheerder** is een gebruikersaccount met beheerdersmachtigingen voor domein- en lid is van Hallo SQL Server vaste serverrol sysadmin voor beide exemplaren van SQL Server. Gebruik voor deze zelfstudie **DomainAdmin**.
* **Wachtwoord** Hallo wachtwoord voor Hallo domeinbeheerdersaccount is. Een complex wachtwoord gebruiken. Hallo wachtwoord bevestigen.
* **Abonnement** Hallo-abonnement dat Azure toorun geïmplementeerd resources voor de beschikbaarheidsgroep Hallo stuklijsten. Als uw account meerdere abonnementen heeft, kunt u een ander abonnement.
* **Resourcegroep** is de naam Hallo voor Hallo groep toowhich alle Azure-resources die door deze sjabloon zijn gemaakt behoren. Gebruik voor deze zelfstudie **SQL-HA-RG**. Zie voor meer informatie [Overzicht van Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Locatie** is hello Azure-regio waar Hallo zelfstudie Hallo resources maakt. Kies een Azure-regio.

Hallo volgende schermafbeelding is een voltooide **basisbeginselen** blade:

![Basisbeginselen](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Klik op **OK**.

### <a name="domain-and-network-settings"></a>Domein-en netwerkinstellingen
Deze Azure-galerie-sjabloon maakt een domein en domeincontrollers. Dit leidt ook tot een netwerk en twee subnets. Hallo-sjabloon kan maken van servers in een bestaand domein of een virtueel netwerk. de volgende stap Hallo configureert Hallo domein- en -instellingen.

Op Hallo **domein-en netwerkinstellingen** blade revisie Hallo vooraf ingestelde waarden voor instellingen voor het domein en de netwerkverbinding van Hallo:

* **Foresthoofddomeinnaam** Hallo-domeinnaam voor Hallo Active Directory-domein dat hosts Hallo-cluster is. Gebruik voor Hallo-zelfstudie **contoso.com**.
* **Virtuele-netwerknaam** Hallo netwerknaam voor Hallo virtuele Azure-netwerk. Gebruik voor Hallo-zelfstudie **autohaVNET**.
* **Naam van de domeincontroller subnet** Hallo naam is van een deel van het virtuele netwerk Hallo die hosts Hallo-domeincontroller. Gebruik **subnet 1**. Dit subnet gebruikt adresvoorvoegsel **10.0.0.0/24**.
* **De naam van de SQL Server-subnet** Hallo naam is van een deel van Hallo virtueel netwerk dat hosts Hallo servers met SQL Server en het Hallo-bestand delen met witness. Gebruik **subnet 2**. Dit subnet gebruikt adresvoorvoegsel **10.0.1.0/26**.

toolearn meer informatie over virtuele netwerken in Azure, Zie [Virtual network-overzicht](../../../virtual-network/virtual-networks-overview.md).  

Hallo **domein-en netwerkinstellingen** moet eruit Hallo volgende schermafbeelding:

![Domein-en netwerkinstellingen](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Indien nodig, kunt u deze waarden te wijzigen. Gebruik voor deze zelfstudie Hallo vooraf ingestelde waarden.

Hallo-instellingen bekijken en klik vervolgens op **OK**.

### <a name="availability-group-settings"></a>Instellingen voor beschikbaarheid
Op **beschikbaarheid groepsinstellingen**, bekijk hello vooraf ingestelde waarden voor de beschikbaarheidsgroep Hallo- en listener Hallo.

* **Naam van de beschikbaarheidsgroep** Hallo geclusterde bron naam voor de beschikbaarheidsgroep Hallo. Gebruik voor deze zelfstudie **Contoso ag**.
* **Naam van de beschikbaarheidsgroep-listener** wordt gebruikt door Hallo-cluster en Hallo interne load balancer. Clients die verbinding maken met Server tooSQL kunnen deze naam tooconnect toohello juiste replica van de database Hallo gebruiken. Gebruik voor deze zelfstudie **Contoso-listener**.
* **Poort beschikbaarheidsgroeplistener** geeft Hallo TCP-poort van SQL Server-listener Hallo. Hallo-standaardpoort, gebruikt die voor deze zelfstudie **1433**.

Indien nodig, kunt u deze waarden te wijzigen. Gebruik voor deze zelfstudie Hallo vooraf ingestelde waarden.  

![Instellingen voor beschikbaarheid](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Klik op **OK**.

### <a name="virtual-machine-size-storage-settings"></a>De grootte van de virtuele machine, instellingen voor de opslag
Op **VM-grootte, instellingen voor de opslag**, kies de grootte van de virtuele machine van een SQL Server en bekijk Hallo andere instellingen.

* **De grootte van de SQL Server-virtuele machine** Hallo grootte voor zowel virtuele machines waarop SQL Server wordt uitgevoerd. Kies de grootte van een juiste virtuele machine voor uw workload. Als u deze omgeving voor Hallo zelfstudie bouwt, gebruikt u **DS2**. Kies de grootte van een virtuele machine die ondersteuning voor Hallo werkbelasting biedt voor productieworkloads. Veel productieworkloads vereisen **DS4** of hoger. Hallo-sjabloon maakt twee virtuele machines van deze omvang en installeert SQL Server op elk. Zie voor meer informatie [grootten voor virtuele machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Azure installeert hello, Enterprise Edition van SQL Server. Hallo kosten, is afhankelijk van Hallo edition en de grootte van de virtuele machine Hallo. Zie voor gedetailleerde informatie over de kosten van de huidige [virtuele machines prijzen](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Grootte van de virtuele machine domain controller** Hallo de grootte van de virtuele machine voor het Hallo-domeincontrollers is. Voor deze zelfstudie gebruik **D2**.
* **De grootte van de virtuele machine delen Witness bestand** Hallo de grootte van de virtuele machine voor Hallo bestandsshare-witness is. Gebruik voor deze zelfstudie **A1**.
* **SQL-opslagaccount** heet Hallo Hallo storage-account van de SQL Server-gegevens Hallo en besturingssysteem schijven. Gebruik voor deze zelfstudie **alwaysonsql01**.
* **DC-opslagaccount** is Hallo-naam van het opslagaccount Hallo voor Hallo-domeincontrollers. Gebruik voor deze zelfstudie **alwaysondc01**.
* **SQL Server-gegevens schijfgrootte** in TB is Hallo-grootte van het SQL Server-gegevensschijf Hallo in TB. Geef een getal van 1 tot en met 4. Gebruik voor deze zelfstudie **1**.
* **Opslagoptimalisatie** opslag voor specifieke configuratie-instellingen voor Hallo SQL Server virtuele machines op basis van het type van de werkbelasting Hallo ingesteld. Alle SQL Server-virtuele machines in dit scenario gebruik premium-opslag met Azure host schijfcache tooread alleen-lezen. Bovendien kunt u SQL Server-instellingen voor de werkbelasting van Hallo optimaliseren door een van deze drie instellingen te kiezen:

  * **Algemene werkbelasting** stelt geen specifieke configuratie-instellingen.
  * **Transactionele verwerking** sets vlag 1117 en 1118 traceren.
  * **Gegevensopslag** sets vlag 1117 traceren en 610.

Gebruik voor deze zelfstudie **algemene werkbelasting**.

![Opslaginstellingen voor VM-grootte](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Hallo-instellingen bekijken en klik vervolgens op **OK**.

#### <a name="a-note-about-storage"></a>Een opmerking over opslag
Aanvullende optimaliseringen zijn afhankelijk van Hallo grootte van gegevensschijven Hallo SQL Server. Voor elke status van de gegevensschijf toegevoegd Azure een extra 1 TB premium-opslag. Wanneer een server 2 TB of meer vereist, maakt Hallo-sjabloon u een opslaggroep op elke virtuele machine van SQL Server. Een opslaggroep is een vorm van virtualisatie van opslag waarop meerdere schijven zijn geconfigureerd tooprovide hogere capaciteit, tolerantie en prestaties.  Hallo-sjabloon maakt een opslagruimte op Hallo opslaggroep vervolgens en geeft een besturingssysteem van één schijf toohello. Hallo sjabloon wijst deze schijf als gegevensschijf Hallo voor SQL Server. Hallo sjabloon verbetert de opslaggroep Hallo prestatie voor SQL Server met behulp van Hallo volgende instellingen:

* Stripe-grootte is Hallo-instelling voor de virtuele schijf Hallo interleave. Transactionele werkbelastingen gebruikt 64 KB. Gegevensopslag werkbelastingen gebruiken 256 KB.
* Tolerantie is eenvoudig (geen tolerantie).

> [!NOTE]
> Azure premium-opslag is lokaal redundant en drie kopieën van Hallo gegevens bewaard binnen één regio, zodat u meer tolerantie op Hallo opslaggroep niet vereist.
>
>

* Aantal kolommen is gelijk aan het aantal schijven in de opslaggroep Hallo Hallo.

Zie voor meer informatie over de opslagruimte en opslaggroepen:

* [Overzicht van opslagruimten](http://technet.microsoft.com/library/hh831739.aspx)
* [Windows Server back-up- en opslaggroepen](http://technet.microsoft.com/library/dn390929.aspx)

Zie voor meer informatie over aanbevolen procedures voor SQL Server-configuratie, [best practices prestaties for SQL Server op Azure virtual machines](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>SQL Server-instellingen
Op **SQL Server-instellingen**, controleren en voorvoegsel van virtuele machine Hallo SQL Server, SQL Server-versie, SQL Server-serviceaccount en wachtwoord wijzigen en Hallo van SQL auto patching onderhoudsplanning.

* **SQL Server voorvoegsel** gebruikte toocreate is een naam voor elke virtuele machine van SQL Server. Gebruik voor deze zelfstudie **sqlserver**. Hallo sjabloon namen Hallo virtuele machines van SQL Server *sqlserver 0* en *sqlserver 1*.
* **SQL Server-versie** Hallo-versie van SQL Server is. Voor deze zelfstudie gebruik **SQL Server 2014**. U kunt ook **SQL Server 2012** of **SQL Server 2016**.
* **Gebruikersnaam voor SQL Server serviceaccount** Hallo domeinaccountnaam voor Hallo SQL Server-service is. Gebruik voor deze zelfstudie **sqlservice**.
* **Wachtwoord** Hallo wachtwoord voor SQL Server-serviceaccount Hallo is.  Een complex wachtwoord gebruiken. Hallo wachtwoord bevestigen.
* **Onderhoudsplanning SQL Auto Patching** identificeert Hallo dag van de week van Hallo dat Azure automatisch patches Hallo SQL-Servers. Typ voor deze zelfstudie **zondag**.
* **Beginuur van SQL Auto Patching onderhoud** Hallo tijd voor hello Azure-regio is wanneer automatisch patchen begint.

> [!NOTE]
> Hallo patchen venster voor elke virtuele machine is gespreid van één uur. Slechts één virtuele machine is een patch uitgevoerd op een tijd tooprevent onderbreking van services.
>
>

![SQL Server-instellingen](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Hallo-instellingen bekijken en klik vervolgens op **OK**.

### <a name="summary"></a>Samenvatting
Klik op de overzichtspagina hello valideert Azure Hallo-instellingen. U kunt ook Hallo sjabloon downloaden. Controleer de hello samenvatting. Klik op **OK**.

### <a name="buy"></a>Kopen
Deze laatste blade bevat **gebruiksvoorwaarden**, en **privacybeleid**. Bekijk deze informatie. Wanneer u gereed voor Azure toostart toocreate Hallo virtuele machines bent en alle andere vereiste resources voor de beschikbaarheidsgroep Hallo Hallo, klikt u op **maken**.

Hello Azure-portal maakt Hallo resourcegroep en alle Hallo-resources.

## <a name="monitor-deployment"></a>Monitor voor implementatie
De voortgang Hallo implementatie van hello Azure-portal. Een pictogram dat Hallo-implementatie staat is automatisch vastgemaakt toohello Azure-portaldashboard.

![Azure-Dashboard](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Verbinding maken met Server tooSQL
Hallo nieuwe exemplaren van SQL Server worden uitgevoerd op virtuele machines met internet verbonden IP-adressen. U kunt Extern bureaublad (RDP) rechtstreeks tooeach SQL Server virtuele machine.

tooRDP tooa SQL Server, als volgt te werk:

1. Op Hallo Azure-portaldashboard, moet u controleren dat Hallo-implementatie is geslaagd.
2. Klik op **Resources**.
3. In Hallo **Resources** blade, klikt u op **sqlserver-0**, namelijk Hallo computernaam van een van Hallo virtuele machines waarop SQL Server wordt uitgevoerd.
4. Op de blade Hallo voor **sqlserver 0**, klikt u op **Connect**. U wordt gevraagd of als u wilt dat tooopen of Hallo verbinding met extern object opslaan. Klik op **Open**.
5. **Verbinding met extern bureaublad** worden gewaarschuwd dat Hallo uitgever van deze externe verbinding kan niet worden vastgesteld. Klik op **Verbinden**.
6. Windows-beveiliging wordt u tooenter gevraagd uw referenties tooconnect toohello IP-adres van de primaire domeincontroller Hallo. Klik op **gebruik een ander account**. Voor **gebruikersnaam**, type **contoso\DomainAdmin**. U kunt dit account geconfigureerd bij het instellen van de gebruikersnaam van Hallo beheerder in Hallo sjabloon. Hallo complex wachtwoord dat u hebt gekozen bij het instellen van Hallo-sjabloon gebruiken.
7. **Extern bureaublad** worden gewaarschuwd dat Hallo op externe computer kan niet worden geverifieerd vanwege tooproblems met het beveiligingscertificaat. Hier ziet u certificaatnaam Hallo-beveiliging. Als u Hallo-zelfstudie hebt gevolgd, is de naam van de Hallo **sqlserver 0.contoso.com**. Klik op **Ja**.

U hebt nu verbinding met RDP toohello SQL Server-virtuele machine. U kunt SQL Server Management Studio te openen, verbinding toohello standaardexemplaar van SQL Server en controleren dat die Hallo-beschikbaarheidsgroep is geconfigureerd.
