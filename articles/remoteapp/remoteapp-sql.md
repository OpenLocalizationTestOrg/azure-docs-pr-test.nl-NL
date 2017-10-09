---
title: aaaSQL Azure met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toouse SQL Azure met Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Vaak wanneer klanten ervoor toohost hun Windows-toepassingen in de cloud met Azure RemoteApp hello kiezen wilt ze ook hun gegevens, zoals SQL-servers in Hallo cloud toomigrate voor een volledige cloudimplementatie. Hiermee ontstaat een volledige in de cloud gehoste oplossing die altijd en overal kan worden gebruikt door elk apparaat waarop Azure RemoteApp is geïnstalleerd. Hieronder vindt u koppelingen en verwijzingen samen met richtlijnen toohelp u met dit proces.  

## <a name="migrate-your-sql-data"></a>Uw SQL-gegevens migreren
Beginnen met [migreren van een SQL Server-database tooAzure SQL-Database](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Azure RemoteApp configureren
Een Windows-toepassing hosten in Azure RemoteApp. Hieronder volgt een zeer globaal stappenplan:

1. Hallo maken [Azure RemoteApp-sjabloon VM](remoteapp-imageoptions.md). 
2. Hallo vereiste toepassing op Hallo VM installeren.
3. Hallo toepassing configureren zodat deze verbinding maakt met toohello SQL DB en controleer of deze werkt.
4. Sysprep en afsluiten hello VM. Leg dit vast als een installatiekopie voor gebruik met Azure. **Opmerking:** moet u tooensure dat Hallo toepassing gegevens over kunnen tooretain Hallo DB connectiviteit via Hallo sysprep-proces is. Als Hallo toepassing kan niet tooretain Hallo DB-verbindingsgegevens, kunt u tooengage Hallo leverancier van Hallo toepassing toocheck hoe we Hallo verbindingsreeks kunt opgeven.
5. Hallo aangepaste installatiekopie importeren naar uw Azure RemoteApp-bibliotheek selecteren Hallo juiste geografische locatie van uw Azure SQL-implementatie zich bevindt. 
6. Implementeer een RemoteApp-verzameling in hello dezelfde gegevens als uw Azure SQL-implementatie met behulp van Hallo hierboven sjabloon centreren en Hallo toepassing publiceren. Implementatie van Azure RemoteApp in Hallo hetzelfde Datacenter als uw Azure SQL-implementatie helpt zorg Hallo hoogste verbindingssnelheden en de latentie te verminderen. 

## <a name="app-and-sql-configuration-considerations"></a>Overwegingen voor app- en SQL-configuratie:
Er zijn enkele punten tooconsider bij gebruik van Azure SQL met RemoteApp:

Meer informatie over [hoe tooconfigure een Azure SQL database-firewall](../sql-database/sql-database-firewall-configure.md). Een fragment van hello artikel staat 'in eerste instantie is alle toegang tooyour Azure SQL Database-server wordt geblokkeerd door Hallo firewall. In de volgorde toobegin met behulp van uw Azure SQL Database-server, moet u toohello klassieke Portal gaan en een of meer serverniveau firewallregels waarmee toegang tooyour Azure SQL Database-server opgeven. Gebruik Hallo firewall-regels toospecify welk IP-adres een bereik van Hallo Internet zijn toegestaan en of Azure-toepassingen tooconnect tooyour Azure SQL Database-server kunnen proberen."

Ook wanneer een computer tooconnect tooyour-databaseserver van Hallo Internet probeert, Hallo firewall controleert die afkomstig zijn van IP-adres van het Hallo-aanvraag in voor de volledige set serverniveau Hallo Hallo en (indien nodig) databaseniveau firewallregels. 'Als Hallo IP-adres van de aanvraag Hallo binnen één van de opgegeven in het niveau van de server-firewallregels Hallo Hallo-bereiken, Hallo verbinding krijgt tooyour Azure SQL Database-server.' Daarom kunnen we IP-bereiken gebruiken en niet alleen afzonderlijke bron-IP-adressen.

Volg Hallo Stapsgewijze instructies in [procedure: firewall-instellingen configureren in SQL Database via Azure Portal Hallo](../sql-database/sql-database-configure-firewall-settings.md) toospecify Hallo IP-adresbereik. Wanneer u de SQL-firewallregels Hallo configureert, geef dan een Hallo IP-adresbereik van Hallo-subnet dat is opgegeven voor hello Azure RemoteApp-verzameling. Dit moet Hallo ARA-servers tooconnect toohello SQL DB toestaan zelfs als deze dynamisch-IP-adressen toegewezen wordt.

## <a name="troubleshooting"></a>Problemen oplossen
Als Hallo ondervindt van het gebruik van een clienttoepassing gehost in Azure RemoteApp die verbinding tooa SQL maakt-database wanneer deze wordt gehost op Azure of lokale is traag kan er een aantal redenen waarom.  

* Netwerklatentie tussen uw apparaat tooAzure is hoog. Verplaats toohello best en snelst mogelijke netwerkverbinding u voor de beste prestaties kunt. Gebruik [azurespeed.com](http://azurespeed.com/) als een algemeen hulpprogramma tootest voor uw apparaten latentie tooAzure data center.  
* Client-app, gehost in Azure RemoteApp, is zwaar belast. U kunt de prestaties verbeteren wanneer u een ander abonnement kiest, bijvoorbeeld Premium. Een andere manier is toomonitor Hallo resources die uw toepassing worden verbruikt: tijdens een actieve sessie uitvoeren van een toetsencombinatie ctrl-alt-end die Hallo SAS-scherm, selecteert u Taakbeheer en Observeer het resourceverbruik voor uw app wordt gestart.
* SQL-server wordt zwaar belast of is niet geoptimaliseerd. Volg de SQL-richtlijnen voor probleemoplossing. 

