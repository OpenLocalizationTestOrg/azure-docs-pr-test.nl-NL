---
title: aaaSecurity overwegingen voor gegevensverplaatsing in Azure Data Factory | Microsoft Docs
description: Meer informatie over het beveiligen van gegevensverplaatsing in Azure Data Factory.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory - beveiligingsoverwegingen voor gegevensverplaatsing
## <a name="introduction"></a>Inleiding
In dit artikel beschrijft de infrastructuur van de basisprincipes van beveiliging dat services voor gegevensverplaatsing in Azure Data Factory toosecure uw gegevens gebruiken. Azure Data Factory-management-resources zijn gebouwd op Azure beveiligingsinfrastructuur en alle mogelijke veiligheidsmaatregelen, die worden aangeboden door Azure gebruiken.

In een Data Factory-oplossing maakt u een of meer gegevens[pijplijnen](data-factory-create-pipelines.md). Een pijplijn is een logische groep activiteiten die samen een taak uitvoeren. Deze pijplijnen zich bevinden in Hallo regio waarin Hallo gegevensfactory is gemaakt. 

Hoewel Data Factory is alleen beschikbaar in **VS-West**, **VS-Oost**, en **Noord-Europa** regio's, Hallo data movement service is beschikbaar [globaal in verschillende regio's](data-factory-data-movement-activities.md#global). Data Factory-service zorgt ervoor dat gegevens een geografisch gebied niet laat / regio tenzij expliciet instrueren Hallo service toouse een andere regio als Hallo data movement service is niet geïmplementeerd nog toothat regio. 

Azure Data Factory zelf slaat geen gegevens, met uitzondering van referenties van de gekoppelde service voor cloud-gegevensarchieven, die zijn gecodeerd met behulp van certificaten. Hiermee kunt u gegevensgestuurde werkstromen tooorchestrate verplaatsing van gegevens tussen maken [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) en het verwerken van gegevens met [compute-services](data-factory-compute-linked-services.md) in andere regio's of in een on-premises -omgeving. U kunt er ook te[bewaken en beheren van werkstromen](data-factory-monitor-manage-pipelines.md) met zowel programmatische als gebruikersinterfacemechanismen.

Verplaatsing van gegevens met behulp van Azure Data Factory is **gecertificeerd** voor:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STER](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Als u geïnteresseerd in Azure compatibiliteit en hoe Azure de eigen infrastructuur beveiligt bent, gaat u naar Hallo [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

In dit artikel controleert u beveiligingsoverwegingen in Hallo na twee data movement-scenario's: 

- **Cloudscenario**-In dit scenario wordt de bron- en doelserver zijn openbaar toegankelijk zijn via internet. Het gaat hierbij om services zoals Azure Storage, Azure SQL Data Warehouse, Azure SQL Database, Azure Data Lake Store, Amazon S3, Amazon-Redshift SaaS-services zoals Salesforce en web-protocollen, zoals FTP en OData beheerde cloudopslag. U vindt een volledige lijst met ondersteunde gegevensbronnen [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- **Hybride scenario**: In dit scenario wordt de bron- of doelserver zich achter een firewall of binnen een lokaal netwerk of Hallo bedrijfsgegevens store is in een particulier netwerk / virtuele netwerk (meestal Hallo bron) en is niet openbaar toegankelijk . Databaseservers die worden gehost op virtuele machines vallen ook onder dit scenario.

## <a name="cloud-scenarios"></a>Cloud-scenario 's
###<a name="securing-data-store-credentials"></a>Referenties opslaan, het beveiligen van gegevens
Azure Data Factory beveiligt uw referenties voor gegevensopslag door **versleutelen** ze met behulp van **certificaten die worden beheerd door Microsoft**. Deze certificaten worden gedraaid elke **twee jaar** (waaronder migratie van referenties en vernieuwen van certificaat). Deze versleutelde referenties zijn veilig opgeslagen in een **Azure Storage beheerd door Azure Data Factory-beheerservices**. Raadpleeg voor meer informatie over Azure Storage beveiliging [beveiligingsoverzicht van Azure Storage](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Gegevensversleuteling onderweg
Hallo cloud gegevensarchief ondersteunt HTTPS of TLS, alle gegevens worden overgedragen tussen services voor gegevensverplaatsing in Data Factory als een gegevensarchief cloud zijn via een beveiligde HTTPS- of TLS-kanaal.

> [!NOTE]
> Alle verbindingen te**Azure SQL Database** en **Azure SQL Data Warehouse** altijd versleuteling (SSL/TLS) vereisen wanneer deze worden in transit tooand uit Hallo-database. Tijdens het ontwerpen van een pijplijn met een JSON-editor toevoegen Hallo **versleuteling** eigenschap en stel deze in te**true** in Hallo **verbindingsreeks**. Wanneer u Hallo gebruikt [Wizard kopiëren](data-factory-azure-copy-wizard.md), Hallo wizard stelt u deze eigenschap standaard. Voor **Azure Storage**, kunt u **HTTPS** in Hallo-verbindingsreeks.

### <a name="data-encryption-at-rest"></a>Versleuteling van inactieve gegevens
Sommige gegevens worden opgeslagen ondersteuning voor versleuteling van gegevens in rust. Het is raadzaam om de gegevens versleuteling mechanisme voor deze opgeslagen gegevens in te schakelen. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Transparent Data Encryption (TDE) in Azure SQL Data Warehouse kunt beveiligen tegen Hallo dreiging van schadelijke activiteiten door realtime versleuteling en ontsleuteling van uw gegevens in rust in te voeren. Dit gedrag is transparant toohello client. Zie voor meer informatie [beveiligen van een database in SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL Database biedt ook ondersteuning voor transparante gegevensversleuteling (TDE), die helpt bij het beveiligen tegen Hallo dreiging van schadelijke activiteiten door het uitvoeren van realtime versleuteling en ontsleuteling van gegevens Hallo zonder wijzigingen toohello toepassing. Dit gedrag is transparant toohello client. Zie voor meer informatie [Transparent Data Encryption met Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Azure Data Lake store biedt ook codering voor gegevens die zijn opgeslagen in het Hallo-account. Wanneer ingeschakeld, wordt Data Lake store automatisch versleutelt gegevens voordat het behouden blijven en ontsleutelt voordat ophalen, waardoor het transparante toohello client Hallo gegevenstoegang. Zie voor meer informatie [beveiliging in Azure Data Lake Store](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Azure Blob Storage en Azure-tabelopslag
Azure Blob Storage en Azure Table storage ondersteunt opslag Service versleuteling (SSE), waarmee uw gegevens voordat persisting toostorage en ontsleuteld voordat ophalen automatisch worden versleuteld. Zie voor meer informatie [Azure Storage Service: versleuteling van gegevens in rust](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 ondersteunt zowel client als server versleuteling van gegevens in rust. Zie voor meer informatie [gegevens beveiligen met behulp van versleuteling](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Data Factory biedt momenteel geen ondersteuning voor Amazon S3 binnen een virtuele privécloud (VPC).

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift ondersteunt cluster versleuteling voor gegevens in rust. Zie voor meer informatie [Amazon Redshift Databaseversleuteling](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html). Data Factory biedt momenteel geen ondersteuning voor Amazon Redshift binnen een VPC. 

#### <a name="salesforce"></a>SalesForce
SalesForce ondersteunt Shield Platform versleuteling waarmee versleuteling van bestanden, bijlagen en aangepaste velden. Zie voor meer informatie [Understanding Hallo Web Server OAuth-verificatie stromen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Hybride scenario's (met behulp van Data Management Gateway)
Hybride scenario's moet Data Management Gateway toobe geïnstalleerd in een on-premises netwerk of in een virtueel netwerk (Azure) of een virtuele privécloud (Amazon). Hallo-gateway moet kunnen tooaccess Hallo lokale gegevensarchieven. Zie voor meer informatie over gateway-Hallo [Data Management Gateway](data-factory-data-management-gateway.md). 

![Data Management Gateway kanalen](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Hallo **opdrachtkanaal** communicatie tussen services voor gegevensverplaatsing in Data Factory- en Data Management Gateway. Hallo communicatie bevat informatie gerelateerd toohello activiteit. Hallo-gegevenskanaal wordt gebruikt voor het overbrengen van gegevens tussen on-premises gegevensopslagexemplaren en cloud-gegevensarchieven.    

### <a name="on-premises-data-store-credentials"></a>On-premises gegevens opslaan van referenties
Hallo-referenties voor uw on-premises gegevensopslagexemplaren worden lokaal opgeslagen (niet in de cloud Hallo). Ze kunnen worden ingesteld op drie verschillende manieren. 

- Met behulp van **tekst zonder opmaak** (minder veilig) via HTTPS van Azure Portal / Wizard kopiëren. Hallo-referenties worden doorgegeven in tekst zonder opmaak toohello lokale gateway.
- Met behulp van **cryptografie met JavaScript-bibliotheek van de Wizard kopiëren**.
- Met behulp van **Klik-zodra op basis van referenties manager app**. Klik op Hallo-zodra de toepassing wordt uitgevoerd op Hallo lokale machine die toegang toohello gateway en Hiermee stelt u referenties voor gegevensopslag Hallo. Deze optie en Hallo naast een weet Hallo veiligste opties. Hallo referentie manager-app, gebruikt standaard Hallo poort 8050 op Hallo-machine met de gateway voor veilige communicatie.  
- Gebruik [nieuw AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) PowerShell cmdlet tooencrypt-referenties. Hallo-cmdlet gebruikt Hallo-certificaat-gateway die is geconfigureerd toouse tooencrypt Hallo referenties. U kunt Hallo versleuteld referenties die zijn geretourneerd door deze cmdlet gebruiken en te toevoegen**EncryptedCredential** element Hallo **connectionString** in Hallo JSON-bestand dat u met Hallo gebruikt [ Nieuwe AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet of in de JSON-codefragment Hallo in Hallo Data Factory-Editor in Hallo-portal. Deze optie en Hallo Klik-als de toepassing hello veiligste opties zijn. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Versleuteling op basis van een bibliotheek met JavaScript cryptografie
U kunt met behulp van referenties voor gegevensopslag versleutelen [cryptografie met JavaScript-bibliotheek](https://www.microsoft.com/download/details.aspx?id=52439) van Hallo [Wizard kopiëren](data-factory-copy-wizard.md). Wanneer u deze optie selecteert, wordt Hallo Wizard kopiëren haalt Hallo openbare sleutel van de gateway en gebruikt deze referenties voor gegevensopslag Hallo tooencrypt. Hallo-referenties worden ontsleuteld door Hallo gatewaycomputer en beveiligd door Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Ondersteunde browsers:** IE8, IE9, IE10, IE11, Microsoft Edge en meest recente Firefox, Chrome, Opera, Safari-browser. 

#### <a name="click-once-credentials-manager-app"></a>Klik op-één keer referenties manager-app
U kunt starten klikt u op Hallo-zodra op basis van de app voor de referentie van een Azure-portal/kopie Wizard bij het ontwerpen van pijplijnen. Deze toepassing zorgt ervoor dat referenties niet worden overgezet als tekst zonder opmaak via Hallo-kabel. Standaard wordt poort Hallo **8050** op Hallo-machine met de gateway voor veilige communicatie. Indien nodig, kan deze poort kan worden gewijzigd.  
  
![HTTPS-poort voor Hallo-gateway](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Data Management Gateway gebruikt momenteel, één **certificaat**. Dit certificaat is gemaakt tijdens de installatie van de gateway hello (geldt tooData Management Gateway na November 2016 gemaakt en versie 2.4.xxxx.x of hoger). U kunt dit certificaat vervangen door uw eigen certificaat voor SSL/TLS. Dit certificaat wordt gebruikt door te klikken op Hallo-als referentie manager toepassing toosecurely toohello gatewaycomputer voor het instellen van referenties voor gegevensopslag verbinding hebt gemaakt. Gegevens worden opgeslagen referenties voor gegevensopslag veilig on-premises door gebruik van Windows hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) op Hallo-machine met de gateway. 

> [!NOTE]
> Oudere gateways die zijn geïnstalleerd voordat November 2016 of van versie 2.3.xxxx.x blijven toouse referenties versleuteld en opgeslagen in de cloud. Zelfs als u een Hallo gateway toohello nieuwste versie upgrade, zijn Hallo referenties niet gemigreerde tooan lokale machine    
  
| Gatewayversie (tijdens het maken van) | Referenties die zijn opgeslagen | Versleuteling van referenties / beveiliging | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | In de cloud | Versleuteld met certificaat (anders dan Hallo gebruikt door de app voor de referentie) | 
| > = 2.4.xxxx.x | On-premises | Beveiligd via DPAPI | 
  

### <a name="encryption-in-transit"></a>Codering in transit
Alle gegevensoverdrachten zijn via een beveiligd kanaal **HTTPS** en **TLS via TCP** tooprevent man-in-the-middle-aanvallen tijdens de communicatie met Azure-services.
 
U kunt ook [IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md) of [Express Route](../expressroute/expressroute-introduction.md) toofurther beveiligde Hallo communicatiekanaal tussen uw on-premises netwerk en Azure.

Virtueel netwerk is een logische representatie van uw netwerk in Hallo cloud. U kunt een lokaal netwerk tooyour Azure-netwerk (VNet) verbinding maken door het instellen van IPSec-VPN (site-naar-site) of Express Route (Privépeering)       

Hallo volgende tabel ziet u Hallo netwerk- en gateway aanbevelingen voor de configuratie op basis van verschillende combinaties van bron- en doellocaties voor hybride gegevensverplaatsing.

| Bron | Doel | Netwerkconfiguratie | Gatewayinstallatie |
| ------ | ----------- | --------------------- | ------------- | 
| On-premises | Virtuele machines en cloudservices die zijn geïmplementeerd in virtuele netwerken | IPSec VPN (punt-naar-site of site-naar-site) | Gateway kan worden geïnstalleerd van on-premises of in een Azure virtuele machine u (VM) in VNet | 
| On-premises | Virtuele machines en cloudservices die zijn geïmplementeerd in virtuele netwerken | ExpressRoute (Privépeering) | Gateway kan worden on-premises geïnstalleerd of op een virtuele machine van Azure in VNet | 
| On-premises | Azure-services waarvoor een openbaar eindpunt | ExpressRoute (openbare Peering) | Gateway moet geïnstalleerde on-premises worden | 

Hallo volgende afbeeldingen ziet u Hallo informatie over het gebruik van Data Management Gateway voor het verplaatsen van gegevens tussen een on-premises database en de Azure-services met behulp van Express route- en IPSec-VPN (met een virtueel netwerk):

**Express Route:**
 
![Gebruik Express Route met gateway](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**IPSec-VPN:**

![IPSec VPN met gateway](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Firewall-configuraties en whitelisting IP-adres van gateway

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Firewallvereisten voor voor-premises/particulier netwerk  
In een onderneming, een **bedrijfsfirewall** wordt uitgevoerd op de centrale router Hallo van Hallo-organisatie. En, **Windows firewall** wordt uitgevoerd als een daemon op Hallo van de lokale computer op welke Hallo gateway is geïnstalleerd. 

Hallo volgende tabel bevat **uitgaande poort** en vereisten voor het domein voor Hallo **bedrijfsfirewall**.

| Domeinnamen | Uitgaande poorten | Beschrijving |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Vereist door Hallo gateway tooconnect toodata-services voor gegevensverplaatsing in Data Factory |
| `*.core.windows.net` | 443 | Door Hallo gateway tooconnect tooAzure Storage-Account wordt gebruikt wanneer u Hallo [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) functie. | 
| `*.frontend.clouddatahub.net` | 443 | Vereist door Hallo gateway tooconnect toohello Azure Data Factory-service. | 
| `*.database.windows.net` | 1433   | (Optioneel) als bestemming voor de Azure SQL-Database nodig / Azure SQL Data Warehouse. Gebruik Hallo gefaseerde kopiëren functie toocopy gegevens tooAzure SQL Database/Azure SQL Data Warehouse zonder het Hallo-poort 1433 openen. | 
| `*.azuredatalakestore.net` | 443 | (Optioneel) nodig hebt bij het doel Azure Data Lake store is | 

> [!NOTE] 
> Wellicht hebt u toomanage poorten / whitelisting domeinen op Hallo bedrijfsfirewall niveau zoals vereist door de respectieve gegevensbronnen. Deze tabel alleen maakt gebruik van Azure SQL Database, Azure SQL Data Warehouse, Azure Data Lake Store als voorbeelden.   

Hallo volgende tabel bevat **binnenkomende poort** vereisten voor Hallo **windows firewall**.

| Poorten voor inkomend verkeer | Beschrijving | 
| ------------- | ----------- | 
| 8050 (TCP) | Hallo referentie manager toepassing toosecurely set referenties voor on-premises gegevensopslagexemplaren op Hallo-gateway vereist. | 

![Vereisten voor de gateway-poort](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>IP-configuraties / whitelisting in gegevens opslaan
Sommige gegevensarchieven Hallo cloud, ook verplichten whitelisting van IP-adres van deze Hallo-machine. Zorg ervoor dat Hallo IP-adres van de gatewaycomputer Hallo goedgekeurde lijst is / correct zijn geconfigureerd in de firewall.

Hallo vereisen volgende cloud gegevensarchieven whitelisting van IP-adres van de gatewaycomputer Hallo. Sommige van deze gegevensarchieven standaard vereist geen whitelisting van Hallo IP-adres. 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

**Vraag:** kan Hallo Gateway worden gedeeld door andere data Factory?
**Antwoord:** wij bieden geen ondersteuning voor deze functie nog. Er wordt gewerkt erop.

**Vraag:** wat Hallo Poortvereisten voor Hallo gateway toowork zijn?
**Antwoord:** Gateway maakt op basis van HTTP-verbindingen tooopen internet. Hallo **uitgaande poorten 443 en 80** moeten worden geopend voor gateway toomake deze verbinding. Open **binnenkomende poort 8050** alleen op computerniveau hello (niet op het niveau van de firewall van het bedrijf) voor de toepassing Referentiebeheer. Als Azure SQL Database- of Azure SQL Data Warehouse wordt gebruikt als bron / bestemming, dan hebt u nodig hebt tooopen **1433** ook poort. Zie voor meer informatie [Firewall-configuraties en whitelisting IP-adressen](#firewall-configurations-and-whitelisting-ip-address-of gateway) sectie. 

**Vraag:** wat zijn certificaten vereist voor de Gateway?
**Antwoord:** huidige gateway vereist een certificaat dat wordt gebruikt door Hallo referentie manager-toepassing voor het veilig instellen van referenties voor gegevensopslag. Dit certificaat is een zelfondertekend certificaat gemaakt en geconfigureerd door Hallo gateway setup. U kunt uw eigen TLS / SSL-certificaat in plaats daarvan. Zie voor meer informatie [klikt u op-één keer credential manager-toepassing](#click-once-credentials-manager-app) sectie. 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de prestaties van de kopieeractiviteit [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).

 
