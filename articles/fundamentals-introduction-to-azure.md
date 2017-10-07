---
title: aaaIntro tooMicrosoft Azure | Microsoft Docs
description: Nieuwe tooMicrosoft Azure? Een eenvoudig overzicht van Hallo Get services deze aanbiedingen met voorbeelden van hoe ze handig zijn.
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Inleiding tot Microsoft Azure
Microsoft Azure is Microsoft toepassingsplatform voor Hallo openbare cloud.  Hallo-doel van dit artikel is toogive u een basis voor het begrijpen van Hallo grondbeginselen van Azure, zelfs als u niets weet over cloudcomputing.

**Hoe tooread in dit artikel**

Azure groeit alle Hallo tijd zodat u eenvoudig tooget overbelast.  Beginnen met Hallo basisservices, waardoor eerst in dit artikel worden vermeld en ga vervolgens verder tooadditional services. Dat betekent niet dat u zojuist hebt Hallo extra services niet gebruiken op zichzelf, maar Hallo basisservices gezamenlijk Hallo kern van een toepassing in Azure wordt uitgevoerd.

**Feedback geven**

Uw feedback is van belang. In dit artikel geeft u een effectieve overzicht van Azure. Als dit niet het geval is, laat ons weten gedeelte met opmerkingen Hallo HALLO hallo pagina onderaan in. Sommige details geeft op wat u verwacht toosee en hoe tooimprove Hallo artikel.  

## <a name="hello-components-of-azure"></a>Hallo-onderdelen van Azure
Azure services worden gegroepeerd in categorieën op Hallo-beheerportal en in verschillende visuele hulpmiddelen zoals Hallo [Wat Is Azure Infographic](https://azure.microsoft.com/documentation/infographics/azure/) . Hallo-beheerportal is wat u toomanage meest (maar niet alle)-services in Azure.

In dit artikel gebruikt een **andere organisatie** tootalk over services op basis van vergelijkbare functie en toocall belangrijke onderliggende services die deel van grotere die uitmaken uit.  

![Azure-onderdelen](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Afbeelding: Azure biedt Internet toegankelijke toepassingsservices in Azure-datacenters wordt uitgevoerd.*

## <a name="management-portal"></a>Management Portal
Azure heeft een webinterface die is aangeroepen Hallo [beheerportal](http://manage.windowsazure.com) waarmee beheerders tooaccess en het beheren van de meeste, maar niet alle Azure-functies.  Hallo nieuwere UI-portal in beta versies Microsoft doorgaans vóór buiten gebruik stellen oudere. Hallo nieuwere heet Hallo ["Azure Preview Portal"](https://portal.azure.com/).

Er is meestal een lange overlapping wanneer beide portals actief zijn. Terwijl basisservices wordt weergegeven in beide portals, is het mogelijk dat niet alle functionaliteit beschikbaar in beide. Nieuwere services worden weergegeven in Hallo nieuwere portal eerste en de oudere-services en functionaliteit mag alleen bestaan in Hallo oudere.  hier het Hallo-bericht is dat als u iets niet in oudere Hallo-portal vinden controleren Hallo nieuwere en vice versa.

## <a name="compute"></a>Compute
Hallo meest eenvoudige manieren die een cloudplatform biedt is voor het uitvoeren van toepassingen. Elk hello Azure compute-modellen heeft zijn eigen tooplay rol.

U kunt deze technologieën afzonderlijk gebruiken of deze waar nodig toocreate Hallo rechts foundation combineren voor uw toepassing. Hallo-benadering die u kiest is afhankelijk van welke problemen u toosolve probeert.

### <a name="azure-virtual-machines"></a>Azure Virtual Machines
![Virtuele Machines in Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Afbeelding: Virtuele Machines in Azure hebt u volledige controle over virtuele machine-exemplaren in Hallo cloud.*

Hallo mogelijkheid toocreate een virtuele machine op aanvraag kan of van een standaardinstallatiekopie of van een die u opgeeft, zeer nuttig zijn. Deze benadering gewoonlijk bekend als infrastructuur als een Service (IaaS), is wat Azure Virtual Machines biedt. Afbeelding 2 ziet u een combinatie van hoe een virtuele Machine (VM) wordt uitgevoerd en hoe toocreate vanaf een VHD.  

toocreate een virtuele machine, kunt u opgeven welke VHD toouse en Hallo van VM-grootte.  Vervolgens betaalt u voor Hallo tijd die Hallo die VM wordt uitgevoerd. U betaalt van Hallo minuut en alleen terwijl deze wordt uitgevoerd, maar er een minimale opslag kosten is voor het bewaren van Hallo VHD beschikbaar. Azure biedt tal van stock VHD's ('afbeeldingen' genoemd) die een opstartbare besturingssysteem toostart van bevatten. Deze omvatten Microsoft en haar partners opties, zoals Windows Server- en Linux-, SQL Server-, Oracle en nog veel meer. U bent gratis toocreate VHD's en afbeeldingen en vervolgens uploaden zelf. U kunt zelfs uploaden VHD's die alleen gegevens bevatten en deze vervolgens kunt openen vanaf de actieve virtuele machines.

Waar Hallo VHD afkomstig zijn van, kunt u alle wijzigingen terwijl een virtuele machine wordt uitgevoerd permanent opslaan. Hallo volgende keer dat u een virtuele machine van die VHD maken dingen worden opgepikt waar u gebleven was. Hallo VHD's terug Hallo virtuele Machines worden opgeslagen in Azure Storage-blobs, die we later over hebben.  Dit betekent dat u redundantie tooensure die uw virtuele machines vanwege fouten toohardware en de schijf verdwijnen Won't. Het ook mogelijk toocopy Hallo gewijzigd VHD buiten Azure, lokaal uitvoeren.

Uw toepassing binnen een of meer virtuele Machines, afhankelijk van hoe u het eerder gemaakt of toocreate besluit het helemaal wordt nu uitgevoerd.

Deze aanpak vrij algemeen toocloud computing gebruikte tooaddress veel verschillende problemen kunnen worden.

**Scenario's voor virtuele Machine**

1. **Ontwikkelen en testen** -kunt u ze toocreate een goedkope ontwikkel- en -platform die u afsluiten kunt wanneer u klaar bent met het gebruik van maken. U kunt ook maken en toepassingen die gebruikmaken van welke talen en bibliotheken die u wilt uitvoeren. Deze toepassingen kunnen u elk Hallo gegevens beheeropties die Azure biedt en u kunt ook toouse SQL Server of een ander DBMS uitgevoerd op een of meer virtuele machines.
2. **Verplaats toepassingen tooAzure (Lift-en-shift)** -'Lift-en-shift' verwijst toomoving uw toepassing veel zoals wanneer u een vorkheftruck toomove een large object.  U 'lift' Hallo VHD vanuit uw lokale datacentrum en 'verschuiven' deze tooAzure en er uitvoeren.  Gewoonlijk hebt u toodo enkele werk tooremove afhankelijkheden op andere systemen. Als er te veel, kunt u in plaats daarvan optie 3.  
3. **Uw Datacenter uitbreiden** -gebruik Azure VM's als een uitbreiding van uw on-premises datacentrum met SharePoint of andere toepassingen. toosupport dit is mogelijk toocreate Windows-domeinen in de cloud Hallo door Active Directory in Azure Virtual machines. U kunt Azure Virtual Network (later wordt vermeld) tootie uw lokale netwerk en het netwerk in Azure samen.

### <a name="web-apps"></a>Web Apps
![Azure-Web-Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Afbeelding: Azure Web Apps wordt uitgevoerd een websitetoepassing in Hallo cloud zonder onderliggende toomanage Hallo-webserver.*

Een van de Hallo meest voorkomende dingen die mensen in de cloud Hallo doen wordt websites en webtoepassingen uitgevoerd. Virtuele Machines in Azure dit toestaat, maar nog steeds laat u Hallo verantwoordelijkheid voor het beheren van een of meer VM's en onderliggende besturingssystemen Hallo van. Cloud services-web-functies kunnen dit doen, maar implementeren en onderhouden van ze nog steeds beheertaken duurt.  Wat gebeurt er als u alleen wilt een website waar iemand anders zorgt voor Hallo administratieve werk voor u?

Dit is precies wat Web Apps biedt. Dit model compute biedt een beheerde omgeving met hello Azure Management portal, alsmede de API's. U kunt een bestaande websitetoepassing naar ongewijzigd Web-Apps verplaatsen of kunt u een nieuwe rechtstreeks in de cloud Hallo. Wanneer een website wordt uitgevoerd, kunt u toevoegen of exemplaren dynamisch verwijderen vertrouwen op Azure Web Apps van aanvragen verdelen over tooload ertussen. Apps van Azure biedt zowel een gedeelde optie, waar uw website wordt uitgevoerd in een virtuele machine met andere sites, en een standaard optie waarmee de toorun van een site in een eigen virtuele machine. Hallo standaard optie kunt u ook vergroot hello (rekenkracht) van uw exemplaren indien nodig.

Web-Apps biedt voor ontwikkeling, .NET, PHP, Node.js, Java en Python samen met de SQL-Database en MySQL (van ClearDB, een Microsoft-partner) ondersteuning voor relationele opslag. Het biedt ook ingebouwde ondersteuning voor verschillende veelgebruikte toepassingen, zoals WordPress, Joomla en Drupal. Hallo-doel is een goedkope, schaalbaar, tooprovide en veelzijdige, handige platform voor het maken van websites en webtoepassingen in de openbare cloud Hallo.

**Web-Apps-scenario 's**

Web-Apps is bedoeld toobe handig voor bedrijven, ontwikkelaars en instanties van web-ontwerp. Voor ondernemingen is het een gemakkelijk te beheren, schaalbare, maximaal beveiligde en maximaal beschikbare oplossing voor het uitvoeren van de aanwezigheid websites. Wanneer u tooset van een Website, wordt aanbevolen toostart met Azure-Web-Apps en Services tooCloud gaan als u moet een functie die niet beschikbaar. Zie Hallo einde van Hallo 'Compute' sectie voor meer koppelingen die kunnen helpen bij toochoose tussen Hallo-opties.

### <a name="cloud-services"></a>Cloudservices
![Azure-Cloudservice](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Afbeelding: Azure Cloud Services biedt een plaats toorun uiterst schaalbare aangepaste code op een Platform als een Service (PaaS)-omgeving*

Stel dat u wilt dat toobuild een cloudtoepassing die veel gelijktijdige gebruikers ondersteunen, hoeft niet veel beheer en nooit uitvalt. U mogelijk een tot stand gebrachte softwareleverancier, bijvoorbeeld dat besloten tooembrace Software als een Service (SaaS) door het maken van een versie van een van uw toepassingen in de cloud Hallo. Of u mogelijk een beginnend bedrijf bent het maken van een consumer-toepassing die u verwacht snel zal toenemen. Als u in Azure maakt, welk model uitvoeren moet u gebruiken?

Azure-Web-Apps kunnen maken van dit soort webtoepassing, maar er zijn enkele beperkingen. U hebt geen beheerderstoegang, bijvoorbeeld, wat betekent dat u kunt willekeurige software niet installeren. Virtuele Machines van Azure kunt u veel flexibiliteit, met inbegrip van beheerderstoegang en zeker kunt u een toepassing zeer schaalbare toobuild, maar hebt u toohandle veel aspecten van betrouwbaarheid en beheer van uzelf. Wat u wilt dat is een optie waarmee u Hallo besturingselement u nodig hebt, maar ook voert het grootste deel van Hallo werk dat nodig is voor de betrouwbaarheid en beheer.

Dit is precies wat wordt verstrekt door Azure Cloud Services. Deze technologie is ontworpen uitdrukkelijk toosupport schaalbare, betrouwbare en lage-beheerder toepassingen en is een voorbeeld van wat is genoemd Platform als een Service (PaaS). toouse, hebt u een toepassing met de Hallo-technologie die u, zoals C#, Java, PHP, Python, Node.js, of iets anders kiest. Uw code wordt vervolgens uitgevoerd op virtuele machines (waarnaar wordt verwezen tooas exemplaren) met een versie van Windows Server.

Maar deze virtuele machines zijn verschillend van Hallo die u met Azure Virtual Machines maken. Voor één ding, Azure zelf beheert ze doen, zoals het installeren van patches voor besturingssysteem en installatiekopieën automatisch nieuwe rolt hersteld. Dit betekent dat de toepassing mag niet worden gebruikt voor het onderhouden van de status in web- of worker-rolexemplaren; Deze moet in plaats daarvan worden opgeslagen in een van de beheeropties voor hello Azure gegevens die worden beschreven in de volgende sectie Hallo. Azure bewaakt ook deze virtuele machines, opnieuw starten van ieder die mislukken. U kunt instellen dat cloud services tooautomatically meer of minder exemplaren in antwoord toodemand maken. Hiermee kunt u toohandle toegenomen gebruik en schalen terug zodat u zo veel mogelijk worden niet betaalt wanneer er minder informatie over het gebruik.

U hebt twee functies toochoose wanneer u een exemplaar maakt, zowel op basis van Windows Server. Hallo belangrijkste verschil tussen Hallo twee is dat een exemplaar van een Webrol IIS uitvoert, maar niet door een exemplaar van een werkrol. Beide worden beheerd in Hallo dezelfde manier echter en het gebruikelijk dat een toepassing toouse die beide's. Een exemplaar van de functie web kan bijvoorbeeld accepteer aanvragen van gebruikers en ze tooa worker rolinstantie voor verwerking doorgeven. tooscale uw toepassing omhoog of omlaag, u kunt aanvragen dat Azure meer exemplaren van de rol maken of bestaande exemplaren afgesloten. En vergelijkbare tooAzure virtuele Machines u bent in rekening gebracht alleen Hallo tijd dat elk exemplaar van de functie web- of worker wordt uitgevoerd.

**Cloud Services-scenario 's**

Cloudservices zijn ideaal toosupport enorme scale-out wanneer u moet meer controle over de Hallo platform dan door Azure Web Apps, maar geen controle over het onderliggende besturingssysteem Hallo hoeft.

#### <a name="choosing-a-compute-model"></a>Een Compute-Model kiezen
Hallo pagina [vergelijking van Azure Web Apps, Cloudservices en virtuele Machines](app-service-web/choose-web-site-cloud-service-vm.md) voorziet in gedetailleerde informatie over het toochoose een Compute-model.

## <a name="data-management"></a>Gegevensbeheer
Toepassingen gegevens nodig en verschillende soorten toepassingen moeten verschillende soorten gegevens. Als gevolg hiervan Azure biedt verschillende manieren toostore en gegevens beheren. Azure biedt veel opslagopties, maar alle zijn ontworpen voor zeer duurzaam opslag.  Met een van deze opties zijn altijd 3 kopieën van uw gegevens gesynchroniseerd tussen een Azure-datacenter--6 als u Azure toouse geografische redundantie tooback up tooanother datacenter ten minste 300 mijl afwezig toestaat.     

### <a name="in-virtual-machines"></a>In de virtuele Machines
Hallo mogelijkheid toorun SQL Server of een ander DBMS in een virtuele machine gemaakt met Azure Virtual Machines heeft al genoemde. Houd er rekening mee dat deze optie is niet beperkt toorelational systemen; u kunt ook gratis toorun NoSQL-technologieën zoals MongoDB en Cassandra. Eenvoudige it repliceren voor het uitvoeren van uw eigen databasesysteem is wat we tooin gebruikt de eigen datacenters- maar het ook Hallo beheer van die DBMS verwerking vereist.  Andere opties verwerkt Azure meer of alle Hallo beheer voor u.

Opnieuw worden Hallo status van de virtuele Machine Hallo en eventuele aanvullende gegevensschijf u maakt of uploadt ondersteund door blob-opslag (die we later over hebben).  

### <a name="azure-sql-database"></a>Azure SQL Database
![Azure Storage SQL-Database](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Afbeelding: Azure SQL Database biedt een beheerde relationele databaseservice in de cloud Hallo.*

Azure biedt voor relationele opslag Hallo functie SQL-Database. Laat u niet Hallo naming u te misleiden. Dit is anders dan een typische SQL-Database geleverd door SQL Server wordt uitgevoerd boven op Windows Server.  

Voorheen SQL Azure, bevat Azure SQL Database alle Hallo belangrijke functies van een relationeel databasebeheersysteem, met inbegrip van atomische transacties gelijktijdige toegang door meerdere gebruikers met integriteit van gegevens, ANSI SQL-query's en een bekend programmering model. Zoals SQL Server, SQL-Database toegankelijk is met behulp van Entity Framework, access ADO.NET, JDBC en andere bekende data-technologieën. Het ondersteunt ook de meeste Hallo T-SQL-taal, samen met SQL Server-hulpprogramma's, zoals SQL Server Management Studio. Voor iedereen bekend zijn met SQL Server (of een andere relationele database) met behulp van SQL-Database is eenvoudig.

Maar SQL-Database niet alleen een DBMS in Hallo de cloud-it een PaaS-service. U nog steeds uw gegevens en wie toegang heeft tot het beheren, maar SQL Database zorgt Hallo beheerdersrechten knorvis werk, zoals Hallo hardware infrastructuur beheren en het Hallo-database en het besturingssysteem software up toodate automatisch te houden. SQL-Database biedt ook hoge beschikbaarheid, automatische back-ups, punt in tijd herstelmogelijkheden en exemplaren kunnen repliceren tussen de geografische regio's.  

**Scenario's voor SQL-Database**

Als u een Azure-toepassing (met behulp van een Hallo compute-modellen) die relationele archief behoeften maakt, zijn SQL-Database een goede optie. Toepassingen die worden uitgevoerd buiten Hallo cloud kunnen deze service ook echter gebruiken zodat er tal van andere scenario's zijn. Bijvoorbeeld: gegevens die zijn opgeslagen in SQL-Database toegankelijk zijn vanuit andere clientsystemen, met inbegrip van desktops, laptops, tablets en telefoons. En omdat het biedt ingebouwde hoge beschikbaarheid door middel van replicatie, met behulp van SQL-Database kunt uitvaltijd te minimaliseren.

### <a name="tables"></a>Tabellen
![Azure Storage-tabellen](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Afbeelding: Azure-tabellen bevat een platte NoSQL manier toostore-gegevens.*

Deze functie wordt soms verschillende condities als onderdeel van een grotere functie met de naam 'Azure Storage' genoemd. Als u 'tabellen', 'Azure-tabellen' of 'opslagtabellen' ziet, is het alle Hallo hetzelfde is.  

En niet te verwarren met de naam van de Hallo: deze technologie niet relationele opslag bieden. Het is in feite een voorbeeld van een NoSQL-methode een sleutel/waarde-archief genoemd. Azure-tabellen kunnen een toepassing voor het opslaan van eigenschappen van verschillende typen, zoals tekenreeksen, gehele getallen en datums. Een toepassing kunt vervolgens een groep met eigenschappen ophalen door een unieke sleutel voor de groep. Tijdens het complexe bewerkingen zoals joins worden niet ondersteund, tabellen bieden snel toegang tot tootyped gegevens. Ze zijn ook zeer schaalbaar, met een enkele tabel kunnen toohold zoveel een terabyte van gegevens. En die overeenkomt met hun eenvoud, tabellen zijn meestal goedkoper toouse dan relationele SQL-Database-opslag.

**Scenario's voor tabellen**

Stel dat u wilt dat toocreate een Azure-toepassing waarvoor u snel toegang tot tootyped gegevens, mogelijk veel ervan, maar tooperform complexe SQL-query's op deze gegevens niet nodig. Stel dat u bij het maken van een consumer-toepassing die toostore profiel klantgegevens voor elke gebruiker moet. Uw app gaat toobe zeer populair is, zodat u tooallow voor grote hoeveelheden gegevens nodig, maar u u niet veel met deze gegevens na het opslaan hebt, klikt u vervolgens bij het ophalen van het op eenvoudige manieren. Dit is precies Hallo soort scenario waarbij Azure-tabellen zinvol is.

### <a name="blobs"></a>Blobs
![Azure Storage-Blobs](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Afbeelding: Azure Blobs bevat niet-gestructureerde binaire gegevens.*  

Azure-Blobs (opnieuw 'Blob Storage' en alleen 'Storage-Blobs' hello zijn hetzelfde) is ontworpen toostore ongestructureerde binaire gegevens. Zoals tabellen, kan Blobs biedt goedkope opslag, en één blob even groot zijn als 1TB (één terabyte). Azure-toepassingen kunnen ook gebruiken voor Azure stations waarmee blobs permanente opslag bieden voor een Windows-bestandssysteem gekoppeld in een Azure-instantie. Hallo-toepassing ziet gewone Windows-bestanden, maar Hallo inhoud daadwerkelijk worden opgeslagen in een blob.

BLOB-opslag wordt gebruikt door veel andere Azure-functies (inclusief virtuele Machines), zodat uw workloads kan zeker te verwerken.

**Scenario's voor Blobs**

Een toepassing die wordt opgeslagen video, grote bestanden of andere binaire gegevens kunt blobs gebruiken voor eenvoudige, goedkope opslag. BLOB's worden ook vaak gebruikt in combinatie met andere services, zoals Content Delivery Network, die we later over zal hebben.  

### <a name="import--export"></a>Import/export
![Azure Import Export-Service](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Afbeelding: Azure Import / Export biedt Hallo mogelijkheid tooship een tooor fysieke harde schijf van Azure voor sneller en goedkoper bulksgewijs gegevens importeren of exporteren.*  

Soms wilt u toomove grote hoeveelheden gegevens in Azure. Die zou lang duren, mogelijk dagen en veel bandbreedte gebruiken. In dergelijke gevallen kunt u Azure Import/Export, waarmee u tooship Bitlocker-versleuteling 3.5" SATA harde schijven rechtstreeks tooAzure datacenters, waarbij Microsoft hello gegevens wordt overgebracht naar de blobopslag voor u.  Nadat het uploaden van Hallo is voltooid, wordt Hallo stations back tooyou geleverd door Microsoft.  U kunt ook aanvragen dat grote hoeveelheden gegevens uit Blob Storage worden geëxporteerd naar harde schijven en vorige tooyou via e-mail verzonden.

**Scenario's voor Import / Export**

* **Grote gegevensmigratie** - telkens wanneer er grote hoeveelheden gegevens (Terabytes) die u tooupload tooAzure, Hallo Import/Export-service is vaak sneller en mogelijk goedkoper dan overdragen via Hallo internet. Nadat gegevens Hallo BLOB's is, kunt u deze kunt verwerken in andere formulieren zoals Table storage of een SQL-Database.
* **Gegevensherstel gearchiveerd** -kunt u voor importeren/exporteren toohave Microsoft overdracht grote hoeveelheden gegevens opgeslagen in Azure Blob Storage tooa opslagapparaat die u verzendt en vervolgens dat apparaat hebt bezorgd back tooa locatie die u wenst. Omdat dit enige tijd duurt, is het niet een goede optie voor noodherstel. Het is raadzaam voor gearchiveerde gegevens die u snel toegang tot niet nodig.

### <a name="file-service"></a>File-Service
![Azure File-Service](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Afbeelding: Azure Bestandsservices biedt SMB \\ \\server\share paden voor toepassingen die worden uitgevoerd in de cloud Hallo.*

On-premises algemene toohave grote hoeveelheden toegankelijk via Hallo Server Message Block (SMB) protocol met behulp van bestandsopslag is een \\ \\Server\share-indeling. Azure heeft nu een service waarmee u toouse dit protocol in Hallo cloud. Toepassingen die worden uitgevoerd in Azure kunnen tooshare bestanden tussen virtuele machines met bekend bestandssysteem API's zoals ReadFile en WriteFile gebruiken. Bovendien Hallo bestanden kunnen ook worden geopend op Hallo hetzelfde moment via een REST-interface waarmee u tooaccess Hallo shares on-premises u ook een virtueel netwerk instellen. Azure Files is ingebouwd in Hallo blob-service, zodat de overgenomen Hallo dezelfde beschikbaarheid, duurzaamheid, schaalbaarheid en geografische redundantie ingebouwd in Azure Storage.

**Scenario's voor Azure Files**

* **Migreren bestaande apps toohello cloud** -de eenvoudiger toomigrate lokale toepassingen toohello cloud waarin bestand tooshare gegevens tussen onderdelen van de toepassing hello deelt. Elke virtuele machine verbinding toohello bestandsshare maakt en vervolgens het kan bestanden lezen en schrijven net zoals het zou tegen een lokaal bestand delen.
* **Gedeelde toepassingsinstellingen** -een algemene patroon voor gedistribueerde toepassingen toohave configuratiebestanden op een centrale locatie waar ze toegankelijk zijn vanuit vele verschillende virtuele machines is. Deze configuratiebestanden kunnen worden opgeslagen in een Azure-bestandsshare en worden gelezen door alle exemplaren van een toepassing. Hallo-instellingen kunnen ook worden beheerd via de REST-interface hello, waarmee u wereldwijd toegang krijgt toohello configuratiebestanden.
* **Diagnostische Share** : U kunt bestanden opslaan en delen diagnostische zoals Logboeken, metrische gegevens, en crashdumps. Deze bestanden beschikbaar via SMB Hallo en REST-interface kunt toepassingen toouse tal van hulpprogramma's voor analyse voor het verwerken en analyseren van Hallo diagnostische gegevens.
* **Dev/testen/Debug** : wanneer ontwikkelaars of beheerders op virtuele machines in de cloud hello werkt, moeten vaak een set hulpprogramma's of hulpprogramma's. Installatie en distributie van deze hulpprogramma's op elke virtuele machine is tijdrovend. Met Azure-bestanden, kan een ontwikkelaar of beheerder hun favoriete tools opslaan op een bestandsshare en verbinding maken toothem van een virtuele machine.

## <a name="networking"></a>Netwerken
Azure voert vandaag veel datacenters verdeeld over Hallo wereld. Als u een toepassing uitvoeren of opslaan van gegevens, selecteert u een of meer van deze toouse datacenters. U kunt ook toothese datacenters op verschillende manieren met Hallo services onderstaande verbinden.

### <a name="virtual-network"></a>Virtual Network
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Afbeelding: Virtuele netwerken biedt een particulier netwerk in de cloud Hallo zodat verschillende services kunnen praten tooeach andere of tooon-premises resources als u een cross-premises VPN-verbinding instelt.*  

Een handige manier toouse een openbare cloud is tootreat als een uitbreiding van uw eigen datacenter.

Omdat u virtuele machines op aanvraag maken kunt, klikt u vervolgens verwijder ze (en betaalt stoppen) wanneer ze niet meer nodig zijn, kunt u rekenkracht alleen als u wilt dat deze te laten. En omdat de virtuele Machines van Azure kunt u virtuele machines met SharePoint, Active Directory en andere vertrouwde lokale software maken, deze benadering kunt werken met Hallo-toepassingen die u al hebt.

toomake deze heel handig echter uw gebruikers zou kunnen tootreat toobe deze toepassingen alsof ze in uw eigen datacenter uitvoert. Dit is precies wat Azure Virtual Network is toegestaan. Een beheerder kunt een VPN-gateway-apparaat gebruikt, instellen van een virtueel particulier netwerk (VPN) tussen uw lokale netwerk en uw virtuele machines die geïmplementeerd tooa virtuele netwerk in Azure zijn. Omdat u uw eigen IP-v4-adressen toohello cloud VMs toewijst, worden deze weergegeven toobe op uw eigen netwerk. Gebruikers in uw organisatie hebben toegang tot toepassingen Hallo deze VMs bevatten alsof ze lokaal uitvoert.

Zie voor meer informatie over het plannen en maken van een virtueel netwerk dat voor u geschikt [virtueel netwerk](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>ExpressRoute
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Afbeelding: ExpressRoute maakt gebruik van een Azure-netwerk, maar verbindingen via routes sneller speciale regels in plaats van Hallo openbare Internet.*  

Als u moet meer bandbreedte of beveiliging dan een Azure-netwerk verbinding kan bieden, kunt u zoeken naar ExpressRoute. In sommige gevallen kunt ExpressRoute ook u geld besparen. Hebt u nog steeds een virtueel netwerk in Azure nodig, maar Hallo koppeling tussen Azure en uw site maakt gebruik van een speciale verbinding die verloopt niet Hallo via openbaar Internet. In order toouse deze service, moet u toohave een overeenkomst met een netwerkserviceprovider of een exchange-provider.

Het instellen van een ExpressRoute-verbinding vereist meer tijd en plannen, zodat u toostart kunt met een site-naar-site VPN, en vervolgens migreren tooan ExpressRoute-verbinding.

Zie voor meer informatie over ExpressRoute [technisch overzicht van ExpressRoute](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Traffic Manager
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Afbeelding: Azure Traffic Manager kunt u tooroute globale verkeer tooyour service op basis van intelligent regels.*

Als uw Azure-toepassing wordt uitgevoerd in meerdere datacenters, kunt u Azure Traffic Manager tooroute aanvragen van gebruikers op intelligente wijze over exemplaren van de toepassing hello. U kunt ook verkeer routeren tooservices niet wordt uitgevoerd in Azure, zolang ze toegankelijk vanaf zijn internet Hallo.  

Een Azure-toepassing met gebruikers in slechts één deel uit van Hallo wereld in slechts één Azure-datacenter mogelijk uitgevoerd. Een toepassing met gebruikers verspreid over Hallo wereld, echter, is geneigd toorun in meerdere datacenters mogelijk zelfs al deze. In dit tweede geval kunt u een probleem wordt geconfronteerd: hoe u op intelligente wijze directe gebruikers tooapplication exemplaren? Meestal hello, wilt u waarschijnlijk elke gebruiker tooaccess Hallo datacenter dichtstbijzijnde tooher, aangezien waarschijnlijk haar Hallo best reactietijd krijgt. Maar wat gebeurt er als dat exemplaar van de toepassing hello is overbelast of niet beschikbaar? In dit geval zou worden nice toodirect haar aanvraag automatisch tooanother datacenter. Dit is precies wat door Azure Traffic Manager wordt uitgevoerd.

Hallo-eigenaar van een toepassing definieert de regels die opgeeft hoe aanvragen van gebruikers gerichte toodatacenters moeten worden vervolgens is afhankelijk van het Traffic Manager toocarry uit deze regels. Bijvoorbeeld gebruikers gerichte toohello dichtstbijzijnde Azure-datacenter normaal gesproken misschien, maar tooanother een verzonden wanneer Hallo reactietijd van hun datacenter standaard Hallo reactietijd van andere datacentra overschrijdt. Voor globaal gedistribueerde toepassingen met veel gebruikers is het nuttig een ingebouwde service toohandle problemen zoals deze.

Het Traffic manager gebruikt de Directory Name Service (DNS) tooroute gebruikers tooservice eindpunten, maar meer verkeer gaat niet via het Traffic Manager wanneer deze verbinding wordt gemaakt. Zo voorkomt Traffic Manager wordt een knelpunt dat uw service-communicatie mogelijk vertragen.

## <a name="developer-services"></a>Ontwikkelaarsservices
Azure biedt een aantal extra toohelp ontwikkelaars en IT-professionals maken en onderhouden van toepassingen in de cloud Hallo.  

### <a name="azure-sdk"></a>Azure SDK
Terug in 2008 ondersteund hello allereerste voorlopige versie van Azure .NET-ontwikkeling. Vandaag de dag, kunt u Azure-toepassingen in vrijwel elke taal. Microsoft biedt momenteel taalspecifieke SDK voor .NET, Java, PHP, Node.js, Ruby en Python. Er is een algemene Azure-SDK die basic ondersteuning voor een andere taal, zoals C++ biedt.  

Deze SDK's te maken, implementeren en beheren van Azure-toepassingen. Ze zijn beschikbaar ofwel van [www.microsoftazure.com](https://azure.microsoft.com/downloads/) of GitHub, en ze kunnen worden gebruikt met Visual Studio en Eclipse. Azure biedt ook opdrachtregelprogramma's waarmee ontwikkelaars kunnen met een editor of ontwikkelings-omgeving, waaronder hulpprogramma's voor het implementeren van toepassingen tooAzure van Linux- en Macintosh-systemen.

Samen met bijdragen aan Azure-toepassingen te ontwikkelen, bieden deze SDK's ook het clientbibliotheken waarmee u software maken die gebruikmaakt van Azure-services. U kan bijvoorbeeld een toepassing bouwt die leest en schrijft Azure blobs of maken van een hulpprogramma dat Azure-toepassingen via de beheerinterface van hello Azure implementeert.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services is een marketing naam die betrekking hebben op een aantal services waarmee toodevelop toepassingen in hello Azure.

tooavoid verwarring - biedt geen een gehoste of Web gebaseerde versie van Visual Studio. U moet nog steeds op uw lokale kopie van de Visual Studio die wordt uitgevoerd. Maar het biedt veel andere hulpprogramma's die handig kunnen zijn.

Dit omvat een gehoste bronbeheersysteem aangeroepen Team Foundation-Service versiebeheer en work item bijhouden biedt.  U kunt zelfs Git voor versiebeheer gebruiken als u liever die. En u kunt u door project gebruiken Hallo bronbeheersysteem variëren. U kunt maken onbeperkte persoonlijke teamprojecten toegankelijk is vanaf een willekeurige plaats in Hallo wereld.  

Visual Studio Team Services biedt een service voor het testen van belasting. U kunt de load-tests die zijn gemaakt in Visual Studio op VM's in de cloud Hallo uitvoeren. Geef van totaal aantal gebruikers die u testen met tooload wilt Hallo en Visual Studio Team Services automatisch bepalen hoeveel agents nodig zijn, ronddraaien van Hallo vereist virtuele machines en de load-tests uitvoeren. Als u een MSDN-abonnee bent, krijgt u duizenden gebruikersminuten belast testen van elke maand gratis.

Visual Studio Team Services biedt ook ondersteuning voor het flexibel ontwikkelen met functies zoals continue integratie bouwt, kanbanborden en virtueel team ruimten.

**Visual Studio Team Services-scenario 's**

Visual Studio Team Services is een goede optie voor bedrijven die toocollaborate wereldwijd nodig hebben nog geen Hallo-infrastructuur in place toodo dus. U kunt setup ophalen in minuten, kiest u een bronbeheersysteem en beginnen met het schrijven van code en bouwen van die dag.  Hallo team's bieden een plaats voor coördinatie en samenwerking en aanvullende hulpprogramma's voor Hallo Hallo analyse nodig tootest bieden en snel optimaliseren van uw toepassing.

Maar organisaties die al een on-premises systeem nieuwe projecten in Visual Studio Team Services toosee kunnen testen of is het efficiënter.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Afbeelding: Application Insights monitors prestaties en het gebruik van uw live web- of app.*

Wanneer u uw app - hebt gepubliceerd of deze wordt uitgevoerd op mobiele apparaten, bureaubladen of webbrowsers - Application Insights geeft aan hoe deze wordt uitgevoerd en wat gebruikers doen met het. Het aantal crashes en trage reactie behoudt, waarschuwing of Hallo cijfers cross onaanvaardbaar drempelwaarden en helpt u eventuele problemen wilt onderzoeken.

Wanneer u een nieuwe functie ontwikkelt, plan toomeasure zijn geslaagd en gebruikers. Door het analyseren van gebruikspatronen begrijpen wat het beste werkt voor uw klanten en uw app in elke ontwikkelingscyclus verbeteren.

Hoewel deze wordt gehost in Azure, werkt de Application Insights voor een breed en groeien scala aan apps, zowel in en uit Azure. J2EE- en ASP.NET web apps worden beschreven, evenals iOS, Android, OS x en Windows-toepassingen. Telemetrie is verzonden via een SDK al ingebouwd met Hallo-app toobe geanalyseerd en weergegeven in Hallo Application Insights-service in Azure.

Als u meer gespecialiseerde analytics wilt, exporteren Hallo telemetrie stroom tooa database of tooPower BI of andere hulpprogramma's.

**Application Insights-scenario 's**

U ontwikkelt een app. Het is mogelijk een web-app of een apparaat-app of een apparaat-app met een web-back-end.

* Hallo-prestaties van uw app optimaliseren nadat deze is gepubliceerd of terwijl het laden testen.  Application Insights cumuleert de telemetrie van alle exemplaren van Hallo geïnstalleerd en biedt u de grafieken van reactietijden, aanvraag en aantal uitzonderingen is afhankelijkheid reactietijden en andere prestatie-indicatoren. Dit kunnen u uw app-prestaties afstemmen. U kunt de code tooreport invoegen om specifieke gegevens als u deze nodig hebt.
* Detecteren en onderzoeken van problemen in uw app live. Ontvang waarschuwingen per e-mail als prestatie-indicatoren cross acceptabele drempelwaarden. Specifieke gebruikerssessies, bijvoorbeeld toosee Hallo van een aanvraag heeft een uitzondering veroorzaakt, kunt u onderzoeken.
* Gebruik tooassess Hallo succes van elke nieuwe functie bijhouden. Wanneer u een nieuwe gebruiker-artikel ontwerpt, plant u toomeasure hoeveel wordt gebruikt en of gebruikers hun verwachte doelstellingen te realiseren. Application Insights biedt u algemene gebruiksgegevens zoals Webpaginaweergaven en kunt u code tootrack Hallo gebruikerservaring invoegen in meer detail.

### <a name="automation"></a>Automatisering
Niemand graag toowaste tijd Hallo voeren dezelfde handmatige steeds verwerkt. Azure Automation biedt een manier voor u toocreate bewaken, beheren en implementeren van resources in uw Azure-omgeving.  

Automation maakt gebruik van 'runbooks', dat gebruikmaakt van Windows PowerShell-werkstromen (versus NET reguliere PowerShell) onder Hallo behandelt. Runbooks zijn bedoeld toobe uitgevoerd zonder dat tussenkomst van de gebruiker. PowerShell-werkstromen kunnen Hallo status van een script toobe opgeslagen op controlepunten langs Hallo manier. Als er een fout optreedt, hebt u geen toostart een script vanaf Hallo begin. U kunt deze opnieuw starten op Hallo laatste controlepunt. Dit bespaart u veel werk probeert toomake Hallo script ingang elke mislukken.

**Automatiseringsscenario 's**

Azure Automation is een goede keuze tooautomate Hallo handmatige, langlopende, foutgevoelige, en regelmatig herhaalde taken in Azure.

### <a name="api-management"></a>API Management
Maken en publiceren van Application programmeurs Interfaces (API's) op Hallo is internet een algemene manier tooprovide services tooapplications. Als deze services zijn resellable (bijvoorbeeld weergegevens), een organisatie andere partijen kunt toestaan tooaccess dezelfde services voor een vast bedrag. Terwijl u toomore partners schaalt, zult u meestal toooptimize nodig hebt en toegangsbeheer.  Sommige partners wellicht zelfs Hallo-gegevens in een andere indeling.

Azure API Management gemakkelijk voor organisaties toopublish API's toopartners, werknemers en ontwikkelaars van derden veilig en op schaal. Biedt een andere API-eindpunt en besluiten als een proxy-toocall Hallo echt eindpunt bij services zoals caching, transformatie, beperking, toegang tot beheer en analytics aggregatie.

**API Management-scenario 's**

Stel dat uw bedrijf beschikt over een reeks apparaten dat alle toocall back tooa centrale tooget servicegegevens--moet bijvoorbeeld een back-ups van bedrijf met apparaten in elke vrachtwagen op Hallo weg.  Hallo bedrijf zult zeker tooset van een systeem tootrack is eigen vrachtwagens zodat betrouwbaar kunnen voorspellen en leveringstijden bijwerken. Het kan weet hoeveel vrachtwagens heeft en op de juiste wijze plannen.  Elke vrachtwagen moet een apparaat dat teruggebeld tooa centrale locatie met de plaatsing en snelheid gegevens, en mogelijk meer.

Een klant Hallo back-upfunctie bedrijf zou waarschijnlijk ook profiteren van deze plaatsing gegevens ophalen.  Hallo klant kan het tooknow hoe ver de producten tootravel hebben, waar ze hangen, hoeveel ze betalende langs bepaalde routes (indien dit wordt gecombineerd met wat ze tooship betaald) gebruiken. Als back-upfunctie bedrijf Hallo al deze gegevens aggregeert, mogelijk veel klanten betalen voor.  Maar vervolgens Hallo back-upfunctie bedrijf moet tooprovide een manier toogive klanten Hallo gegevens. Nadat ze toegang toocustomers bieden, ze mogelijk geen controle over hoe vaak hello gegevens een query wordt uitgevoerd. Hebben ze tooprovide regels die bepalen wie toegang heeft tot welke gegevens. Al deze regels zou toobe ingebouwd in hun externe API hebben. Dit is waar API Management kan helpen.  

## <a name="identity-and-access"></a>Identiteit en toegang
Werken met de identiteit is onderdeel van de meeste toepassingen. Weten wie een gebruiker is, kunt een toepassing die bepalen hoe het met die gebruiker moet werken. Azure biedt services toohelp bijhouden identiteit evenals integreren met identiteitsopslag kunt u al gebruikt.

### <a name="active-directory"></a>Active Directory
Als de meeste directoryservices, Azure Active Directory informatie opgeslagen over gebruikers en Hallo organisaties waartoe ze behoren. Hiermee kunnen gebruikers zich kunnen aanmelden, vervolgens verstrekt u ze met tokens kunnen ze tooapplications tooprove hun identiteit opleveren. Daarnaast kunt u gebruikersgegevens synchroniseren met Windows Server Active Directory met on-premises in uw lokale netwerk. Hallo mechanismen en gegevensopmaak die wordt gebruikt door Azure Active Directory niet identiek zijn met die worden gebruikt in Windows Server Active Directory, zijn Hallo-functies worden uitgevoerd vergelijkbaar.

De belangrijke toounderstand dat Azure Active Directory voornamelijk voor gebruik door cloudtoepassingen ontworpen is. Het kan worden gebruikt door toepassingen die worden uitgevoerd op Azure, bijvoorbeeld of op andere cloudplatforms. Dit wordt ook gebruikt door de Microsoft cloud-toepassingen, zoals die in Office 365. Als u uw datacenter tooextend in Hallo cloud met Azure Virtual Machines en Azure Virtual Network wilt, echter Azure Active Directory is niet de juiste keuze Hallo. In plaats daarvan moet u toorun Windows Server Active Directory in virtuele Machines.

toolet toepassingen toegang tot Hallo informatie bevat, Azure Active Directory biedt een RESTful-API aangeroepen Azure Active Directory Graph. Deze API kan toepassingen die op elk platform toegang directory-objecten en verbanden Hallo uitgevoerd.  Bijvoorbeeld, een geautoriseerde toepassing gebruiken deze API toolearn over een gebruiker, Hallo groepen die hij tot deel uitmaakt en andere informatie. Toepassingen relaties tussen gebruikers hun sociale graph-waarin ze meer op intelligente wijze met Hallo-verbindingen tussen mensen werken ook worden weergegeven.

Een andere functionaliteit van deze service, Azure Active Directory-toegangsbeheer gemakkelijker voor informatie over de identiteit van een toepassing tooaccept van Facebook, Google, Windows Live ID en andere populaire id-providers. In plaats van vereist Hallo toepassing toounderstand Hallo gegevens van diverse indelingen en protocollen die door elk van deze providers worden gebruikt, zet toegangsbeheer allemaal in één algemene indeling. Ook kunt u een toepassing accepteren aanmeldingen vanaf een of meer Active Directory-domeinen. Bijvoorbeeld, een leverancier een SaaS-toepassing biedt Azure Active Directory-toegangsbeheer toogive gebruikers in elk van de toepassing van klanten toohello voor eenmalige aanmelding gebruiken.

Directory-services worden een core basis van de lokale computer. Mag niet het verrassend dat ze zich ook belangrijk in Hallo cloud.

### <a name="multi-factor-authentication"></a>Meervoudige verificatie
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Afbeelding: Multi-Factor Authentication biedt functionaliteit voor uw toepassing tooverify Hallo meer dan één vorm van identificatie*

Beveiliging is altijd belangrijk. Multi-factor authentication (MFA) kunt u ervoor zorgen dat alleen gebruikers zelf toegang hebben tot hun account. MFA (ook wel bekend als tweeledige verificatie of '2FA') moet gebruikers twee van deze drie methoden voor verificatie van de identiteit voor gebruikersaanmeldingen en transacties.

* Iets u weet (doorgaans een wachtwoord)
* Iets er (een vertrouwd apparaat die niet eenvoudig wordt gedupliceerd, zoals een telefoon)
* Iets dat u (biometrie)

Dus wanneer een gebruiker zich aanmeldt, kunt u ze kunt vereisen tooalso hun identiteit bevestigen met een mobiele app, een telefonische oproep of een tekstbericht in combinatie met hun wachtwoord. Azure Active Directory ondersteunt standaard Hallo gebruik van wachtwoorden als verificatiemethode voor gebruikersaanmelding. U kunt MFA samen met Azure AD of met aangepaste toepassingen en mappen met behulp van Hallo MFA-SDK. U kunt deze ook gebruiken met on-premises toepassingen met behulp van multi-factor Authentication-Server.

**MFA-scenario 's**

De beveiliging van de aanmelding op gevoelige accounts zoals bank aanmeldingen en code toegang tot de gegevensbron waarop onbevoegde toegang kan er met een hoge financiële of intellectueel-eigenschap kosten.   

## <a name="mobile"></a>Mobiele telefoon
Als u een app voor een mobiel apparaat maakt, is Azure kunt opslaan van gegevens in de cloud hello, gebruikers verifiëren en om pushmeldingen te verzenden zonder dat u toowrite hoeft een grote hoeveelheid aangepaste code.

Terwijl u gewoon Hallo back-end voor een mobiele app met virtuele Machines, Cloud Services of Web-Apps bouwen kunt, kunt u besteden veel minder tijd schrijven Hallo serviceonderdelen onderliggende met behulp van Azure services.

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Afbeelding: Mobiele Apps biedt functionaliteit die zijn doorgaans vereist voor toepassingen die de interface met mobiele apparaten.*

Mobiele Apps van Azure biedt veel handige functies waarmee u bespaart tijd bij het bouwen van een back-end van een mobiele toepassing. Hiermee kunt u toodo eenvoudige inrichting en beheer van gegevens die zijn opgeslagen in een SQL-Database. U kunt opties voor het opslaan van aanvullende gegevens zoals blob-opslag of MongoDB gebruiken met servercode. Mobiele Apps biedt ondersteuning voor meldingen, hoewel in bepaalde gevallen u in plaats daarvan Notification Hubs gebruiken kunt zoals hieronder wordt beschreven.  Hallo-service heeft ook een REST-API dat uw mobiele App tooget werk kunt aanroepen. Mobiele Apps biedt ook Hallo mogelijkheid tooauthenticate gebruikers via Microsoft- en Active Directory en andere bekende id-providers zoals Facebook, Twitter en Google.   

U kunt andere Azure-Services zoals Service Bus- en werkrollen, en koppel tooon-premises systemen. U kunt zelfs 3e partij invoegtoepassingen van hello Azure Store (zoals SendGrid voor e-mailadres) tooprovide aanvullende functionaliteit verbruiken.

Native clientbibliotheken voor Android-, iOS-, HTML/JavaScript-, Windows Phone- en Windows Store maken het gemakkelijker toodevelop voor apps op alle veelgebruikte mobiele platforms. Een REST-API maakt toouse Mobile Services-gegevens en functionaliteit van verificatie met apps op verschillende platforms. Een mobiele service kunt back-meerdere client-apps zodat u een consistente gebruikerservaring verschillende apparaten bieden kunt.

Omdat Azure al grootschalige ondersteunt, kunt u Hallo-verkeer verwerken als uw app steeds populairder wordt.  Controle en logboekregistratie worden ondersteund toohelp oplossen van problemen en beheer de prestaties.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Afbeelding: Notification Hubs bevat functies die nodig zijn vaak door toepassingen die de interface met mobiele apparaten.*

Kunt u code schrijven toodo meldingen in Azure Mobile Apps, is Notification Hubs geoptimaliseerd toobroadcast miljoenen sterk gepersonaliseerde pushmeldingen binnen enkele minuten.  U hebt geen tooworry over gegevens, zoals mobiele operator of de fabrikant van apparaat. U kunt richt de persoon die of het miljoenen gebruikers met één API-aanroep.

Notification Hubs is ontworpen toowork met elke back-end. U kunt Azure Mobile Apps, een aangepaste back-end in de cloud van Hallo uitgevoerd op elke provider of een lokale back-end.

**Notification Hub-scenario's** als u was bezig met het schrijven van een mobiele spel waar spelers schakelt heeft, moet u mogelijk toonotify speler 2 die speler 1 haar inschakelen is voltooid. U kunt dat is alles wat dat u toodo nodig, alleen Mobile Apps te gebruiken. Maar als u had 100.000 gebruikers spelen uw en gewenste toosend een tijdstip gevoelige gratis aanbieding tooeveryone, Notification Hubs Hallo betere keuze is.

U kunt belangrijk nieuws, sport gebeurtenissen en product aankondiging meldingen toomillions van gebruikers met een lage latentie verzenden. Ondernemingen kunnen melden bij hun werknemers over nieuwe tijd gevoelige communicatie, zoals verkoopkansen, zodat werknemers hoeft tooconstantly e-mailadres of andere toepassingen toostay op de hoogte te controleren. U kunt ook een eenmalige wachtwoorden vereist voor multi-factor authentication verzenden.

## <a name="back-up"></a>Een back-up
Elke enterprise moet toobackup en terugzetten van gegevens. U kunt Azure toobackup gebruiken en het herstellen van uw toepassing in Hallo cloud of on-premises. Azure biedt verschillende opties toohelp, afhankelijk van Hallo type back-up.

### <a name="site-recovery"></a>Site Recovery
Azure Site Recovery (voorheen Hyper-V Recovery Manager) kunt u belangrijke toepassingen beveiligen door het coördineren van Hallo replicatie en herstel in meerdere sites. Site Recovery biedt de mogelijkheid tooprotect toepassingen op basis van de Hyper-v, VMWare of SAN tooyour eigen secundaire site, de site van de hoster tooa of tooAzure en Hallo kosten en complexiteit van het maken en beheren van uw eigen secundaire locatie voorkomen. Azure versleutelt gegevens en communicatie en u hebt Hallo optie versleuteling voor gegevens in rust te schakelen.

Het Hallo-status van uw services continu bewaakt en helpt om Hallo normaal herstel van services in geval van een onderbreking van de site op het primaire datacenter Hallo Hallo te automatiseren. Virtuele machines kunnen worden gezet in een service geregiseerde wijze toohelp terugzetten snel, zelfs voor complexe werkbelastingen van meerdere lagen.

Site Recovery werkt met bestaande technologieën zoals Hyper-V Replica, System Center en SQL Server Always On. Bekijk [Azure Site Recovery-overzicht](site-recovery/site-recovery-overview.md) voor meer informatie.

### <a name="azure-backup"></a>Azure Backup
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Afbeelding: Azure back-up waarin gegevens van lokale Windows-Servers in de cloud Hallo.*  

Azure Backup back-ups van gegevens van lokale servers met Windows Server Hallo cloud. U kunt uw back-ups rechtstreeks vanuit de back-uphulpprogramma's in Windows Server 2012, Windows Server 2012 Essentials of System Center 2012 - Data Protection Manager Hallo beheren. U kunt ook een gespecialiseerde back-upagent gebruiken.

Gegevens is veiliger omdat back-ups worden versleuteld voor verzending en versleuteld in Azure opgeslagen en beveiligd door een certificaat dat u uploadt. Hallo-service gebruikt dezelfde redundante en maximaal beschikbare gegevensbeveiliging in Azure Storage gevonden Hallo.  U kunt back-up bestanden en mappen op een regelmatige of direct volledige of incrementele back-ups uitgevoerd. Nadat de back-up toohello cloud, kunnen geautoriseerde gebruikers eenvoudig back-ups tooany server herstellen. Biedt ook bewaarbeleid voor gegevens kunnen worden geconfigureerd, compressie van gegevens en gegevens overbrengen beperking zodat u Hallo toostore en overdracht kostengegevens kunt beheren.

**Scenario's voor Azure Backup**

Als u al gebruikmaakt van Windows Server of System Center, Azure back-up een natuurlijke oplossing is voor back-ups van uw bestandssysteem voor servers, virtuele machines en SQL Server-databases.  Dit proces werkt met versleutelde, sparse en gecomprimeerde bestanden. Er zijn enkele beperkingen, moet u [hello Azure Backup-vereisten controleren](http://technet.microsoft.com/library/dn296608.aspx) eerste.

## <a name="messaging-and-integration"></a>Berichten en integratie
Ongeacht wat het doet, moet de code vaak toointeract met andere code.  In sommige gevallen is alles wat nodig is in de wachtrij basisberichten. In andere gevallen zijn meer complexe interacties vereist. Azure biedt een aantal verschillende manieren toosolve deze problemen. Afbeelding 5 ziet u Hallo-opties.

### <a name="queues"></a>Wachtrijen
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Afbeelding: Wachtrijen toestaan of koppeling tussen de onderdelen van een toepassing en vergemakkelijken schalen.*  

Queuing is een eenvoudige idee: bericht uiteindelijk wordt gelezen door een andere toepassing en één toepassing een bericht in een wachtrij geplaatst. Als uw toepassing alleen deze eenvoudige service moet, zijn wachtrijen Azure Hallo beste keuze.

Bieden vergelijkbare Queuing-services vanwege Hallo manier hello die Azure klein gedurende een bepaalde periode, Azure Storage-wachtrijen en Service Bus-wachtrijen. Hallo redenen waarom u toouse via Hallo andere willen zou worden behandeld in Hallo redelijk technische document [Azure wachtrijen en Service Bus-wachtrijen - vergeleken en tegenstelling tot](http://msdn.microsoft.com/library/azure/hh767287.aspx).  In veel scenario's werkt ofwel.

**Wachtrij-scenario 's**

Een algemene gebruik van wachtrijen is vandaag de dag toolet een exemplaar van de rol web communiceren met een werknemer rolinstantie in dezelfde Cloudservices-toepassing hello.

Stel bijvoorbeeld dat u maakt een Azure-toepassing voor het delen van video. Hallo toepassing bestaat uit PHP code die wordt uitgevoerd in een Webrol die kiest, kunnen gebruikers uploaden en video samen met een werkrol die is geïmplementeerd in C# die vertaalt geüpload video in verschillende indelingen.

Wanneer een exemplaar van de rol web ontvangt een nieuwe video van een gebruiker, het kan Hallo video opslaan in een blob, en vervolgens verzenden van een bericht tooa werkrol via een wachtrij geeft u op waar dit nieuwe toofind video. Een exemplaar worker-rol-en biedt geen belang welk Hallo-bericht van één wordt vervolgens lezen uit de wachtrij Hallo en video vertalingen Hallo vereist op de achtergrond Hallo verricht.

Asynchrone verwerking structureren van een toepassing op deze manier kunt en is het ook eenvoudiger tooscale van toepassing, Hallo omdat Hallo aantal rolexemplaren web en rolinstanties worker onafhankelijk kan worden gewijzigd. U kunt ook de wachtrijgrootte hello gebruiken als een trigger tooscale Hallo aantal werkrollen omhoog en omlaag. Te hoog is, en het toevoegen van meer functies. Bij het ophalen van lagere, kunt u Hallo aantal uitgevoerde functies toosave geld reduceren.  

Zelfs als ze geen web-en werkrollen, kunt u dit patroon tussen veel verschillende onderdelen van uw toepassing.  Hiermee kunt u tooscale Hallo onderdelen aan beide zijden van de wachtrij Hallo omhoog en omlaag als vraag en verwerkingstijd vereist.

### <a name="service-bus"></a>Service Bus
Of ze worden uitgevoerd in de cloud Hallo in uw datacenter, op een mobiel apparaat of ergens anders, moeten toepassingen toointeract. Hallo-doel van Azure Service Bus is toolet servertoepassingen vrijwel elke locatie uitwisselen van gegevens.

In aanvulling toohello wachtrijen (-op-een) die eerder zijn beschreven, biedt Service Bus ook tooother communicatiemethoden.

#### <a name="service-bus-relay"></a>Service Bus Relay
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Afbeelding: Service Bus Relay kunt communicatie tussen toepassingen op verschillende kanten van een firewall.*

Service Bus kunt rechtstreekse communicatie via de relay-service biedt een veilige manier toointeract via firewalls. Service Bus relays inschakelen toepassingen toocommunicate door het uitwisselen van berichten via een gehost in de cloud Hallo in plaats van lokaal eindpunt.

**Service Bus Relay-scenario 's**

Toepassingen die via Service Bus communiceren mogelijk op Azure-toepassingen of software die wordt uitgevoerd op een andere cloud-platform. Ze kunnen ook toepassingen die worden uitgevoerd buiten de Hallo cloud, maar worden. Een luchtvaartmaatschappij dat reserveringsinformatie op computers in een eigen datacenter implementeert bijvoorbeeld zien. Hallo luchtvaartmaatschappij moet tooexpose deze services toomany clients, waaronder incheckbalies in luchthavens, reservering agent aansluitingen en mogelijk zelfs klanten telefoons. Deze mogelijk gebruik Service Bus toodo dit losse interactie tussen Hallo verschillende toepassingen maken.

#### <a name="service-bus-topics-and-subscriptions"></a>Service Bus-onderwerpen en -abonnementen
![Azure Service Bus-onderwerpen](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Afbeelding: Service Bus-onderwerpen kunnen meerdere apps toopost berichten en andere toepassingen toosubscribe tooreceive berichten die voldoen aan bepaalde criteria voldoen.*

Service Bus biedt een mechanisme voor publiceren en abonneren aangeroepen onderwerpen en abonnementen. Met publish-subscribe, kan een toepassing berichten tooa onderwerp verzenden terwijl een andere toepassingen abonnementen toothis onderwerp kunnen maken. Hierdoor kan een-op-veel-communicatie tussen een set met toepassingen, waardoor Hallo hetzelfde bericht worden gelezen door meerdere ontvangers.

**Service Bus-onderwerpen en abonnementen scenario 's**

Telkens wanneer u instelt waarbij er zijn veel berichten die alle belangrijke zijn, maar verschillende downstream systemen hoeft alleen toolisten toodiffering subsets van die communicatie, zijn Service Bus-onderwerp en abonnementen een goede optie.

### <a name="biztalk-services"></a>BizTalk Services
![BizTalk Services](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Afbeelding: BizTalk Services biedt Hallo mogelijkheid tootransform XML-berichten indelingen in Hallo cloud.*

Soms moet u systemen die communiceren met behulp van verschillende-indelingen. Het is gebruikelijk voor zakelijke toohave andere database schema's en XML-messaging-indelingen, zelfs als een algemene standaard beschikbaar. In plaats van een groot aantal aangepaste code schrijven, kunt u BizTalk Server lokale toointegrate verschillende systemen.  Azure BizTalk Services biedt Hallo hetzelfde type van de service, maar Hallo cloud. U kunt alleen wat u gebruikt en u geen zorgen over schalen zoals u tooon-premises hebt betalen.

**BizTalk Services-scenario 's**

Dit type vertaling voor bedrijven vereisen meestal interacties Business-to-Business (B2B).  Een bouwen vliegtuigen behoeften tooorder onderdelen van het bedrijf is bijvoorbeeld verschillende onderdelen leveranciers. Er is veel leveranciers van onderdelen.  Deze orders moet geautomatiseerde toogo rechtstreeks vanuit Hallo vliegtuig opbouwfuncties systemen in Hallo leveranciers systemen.  Geen van beide bedrijven wil toochange hun core systemen en berichtindelingen en is zeer onwaarschijnlijk dat deze indelingen zijn Hallo dezelfde. BizTalk Services kan duren voordat de berichten en vertalen tussen Hallo nieuwe indelingen beide richtingen. Beide Hallo vliegtuig leverancier kunt Hallo werk tootranslate of Hallo van verschillende leveranciers kunnen afhankelijk van die wil meer controle en Hallo hoeveelheid vertaling nodig.     

## <a name="compute-assistance"></a>Rekenuren voor hulp
Azure biedt ondersteuning voor services die niet toorun alle Hallo tijd hoeven.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Afbeelding: Azure Scheduler biedt een manier tooschedule taken op een bepaald tijdstip gedurende een bepaalde periode.*

Toepassingen moeten toorun soms alleen op een bepaald moment. In Azure, kunt u geld met dit type app in plaats van een toepassing alleen 24 x 7 wachten op gegevens tooprocess blijven uitvoeren laten opslaan. Azure Scheduler kunt u tooschedule wanneer een toepassing moet worden uitgevoerd op basis van het interval van tijd of een kalender. Het is betrouwbare en controleert of dat een proces wordt uitgevoerd zelfs als er netwerk, machine en data center-fouten. U Hallo Scheduler REST API toomanage deze acties.

Wanneer een geplande waarschuwing wordt Scheduler verzendt HTTP of HTTPS-berichten tooa specifieke eindpunt of een bericht in een wachtrij opslag kunt plaatsen.  Daarom toohave wordt uw toepassing een toegankelijk eindpunt hebt of laat het bewaken van een opslagwachtrij. Wanneer deze het Hallo-bericht ontvangt, kunt het ongeacht deze geprogrammeerd actie uitvoeren.

**Scheduler-scenario 's**

* Terugkerende acties van toepassingen: als u bijvoorbeeld een service mogelijk periodiek gegevens ophalen uit twitter en Hallo gegevens verzamelen in een reguliere feed.
* Dagelijks onderhoud: logboek verwerken of weghalen, presterende back-ups en andere afwisselend taken plannen.
* Taken die 's nachts uitvoeren.
* Web applications taken zoals het dagelijks verwijderen van Logboeken, het uitvoeren van back-ups en overige onderhoudstaken. Een beheerder kan toobackup haar database om 1 uur, dagelijks op Hallo volgende negen maanden, bijvoorbeeld kiezen.

Hallo Scheduler API kunt u toocreate, bijwerken, verwijderen, weergeven en jobverzamelingen en geplande taken beheren via een programma.

## <a name="performance"></a>Prestaties
Prestaties is altijd belangrijk voor een toepassing. Toepassingen vaak tooaccess telkens dezelfde gegevens Hallo. Eenzijdige tooimprove prestaties tookeep een kopie van die gegevens dichter toohello toepassing is, Minimalisatie van het aantal Hallo tijd die nodig is tooretrieve deze. Azure biedt verschillende services om dit te doen.

### <a name="azure-caching"></a>Azure Caching
![Azure Caching](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Afbeelding: Een Azure-toepassing kunt gegevens in het geheugen in de cache en zelfs van splitsen over veel werkrollen**

Toegang tot gegevens die zijn opgeslagen in een Azure gegevens management services-SQL-Database, tabellen of BLOB's-erg snel. Nog toegang tot gegevens die zijn opgeslagen in het geheugen is zelfs sneller. Bewaren van een kopie in het geheugen van veelgebruikte gegevens verbeteren de prestaties van toepassingen als gevolg hiervan. U kunt Azure in-memory Caching toodo deze gebruiken.

Een Cloud Services-toepassing kunt gegevens in de cache opslaan en vervolgens deze ophalen zonder tooaccess permanente opslag. Hallo-cache kan worden beheerd in uw toepassing de virtuele machines of geleverd worden door virtuele machines uitsluitend toocaching toegewezen. In beide gevallen Hallo-cache kan worden verdeeld, met Hallo gegevens deze verspreid over meerdere virtuele machines in een Azure-datacenter bevat.

Azure heeft een aantal verschillende cache-technologieën die gedurende een bepaalde periode hebt verplaatst. Hallo zorgen dat ze zijn geïntroduceerd, er is een gedeelde in de rol, beheerd en Redis-cache. Hallo gedeeld opslaan in cache is een oudere technologie en u nieuwe implementaties aan mag niet maken. Hallo heeft beheerd Cache Hallo dezelfde functies van Hallo In-Role cache, maar als beheerde service buiten hello Azure Management Portal. Hallo Redis-Cache is een Preview-versie. Hallo Redis-implementatie heeft Hallo kunt u het grootste aantal onderdelen en wordt aanbevolen als u nieuwe cache code schrijft.

**Azure-Cache-scenario 's**

Een toepassing die herhaaldelijk een productcatalogus leest kan profiteren van het gebruik van dit soort caching, wordt bijvoorbeeld sinds Hallo gegevens deze nodig beschikbaar sneller. Hallo-technologie ondersteunt ook vergrendelen, zodat deze worden gebruikt met zowel lezen/schrijven als alleen-lezen gegevens. En ASP.NET-toepassingen Hallo service toostore sessiegegevens kunnen gebruiken met alleen een configuratiewijziging.

### <a name="content-delivery-network"></a>CDN (Content Delivery Network)
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Afbeelding: Kopieën van een blob kunnen worden opgeslagen in de cache op sites Hallo wereld.**

Stel dat u moet toostore blob-gegevens die wordt geopend door gebruikers Hallo wereld. Het is mogelijk een video van Hallo nieuwste WK overeenkomen, bijvoorbeeld of updates voor stuurprogramma's, of een populaire e-book. Een kopie van Hallo gegevens opslaan in meerdere Azure-datacenters krijgt, maar als er veel gebruikers, het is mogelijk niet voldoende. U kunt hello Azure CDN gebruiken voor zelfs betere prestaties.

Hallo CDN heeft tientallen sites wereld Hallo, elke geschikt is voor het opslaan van kopieën van Azure blobs. Hallo eerst een gebruiker in een bepaald deel van Hallo wereld naar een bepaalde blob Hallo informatie bevat wordt gekopieerd van een Azure-datacenter naar de lokale opslag van CDN in die Geografie. Daarna gebruikt toegang uit het deel van Hallo wereld Hallo blob kopiëren in de cache opgeslagen in Hallo CDN-ze hoeft niet toogo alle Hallo manier toohello dichtstbijzijnde Azure-datacenter. Hallo-resultaat is sneller toegang tot toofrequently toegang krijgen tot gegevens door gebruikers overal ter wereld Hallo.

**CDN-scenario 's**

Het is algemene toouse CDN met Media Services toodeliver video wereldwijd. Video is gewoonlijk lang en vereist een grote bandbreedte.  Media Services is elders besproken op deze pagina.

## <a name="big-data-and-big-compute"></a>BIG Data en Big Compute
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Afbeelding: HDInsight helpt bij het Hallo bulksgewijs verwerking van grote hoeveelheden gegevens**

Jaren, is Hallo bulksgewijs van data-analyse uitgevoerd op relationele gegevens die zijn opgeslagen in een datawarehouse gebouwd met een relationele DBMS. Dit soort business analytics is nog steeds belangrijk zal, en deze voor een lange tijd toocome. Maar wat gebeurt er als gewenste tooanalyze Hallo-gegevens zo groot dat relationele databases NET kunnen niet; het verwerkt is? En stel Hallo gegevens zijn niet relationele? Server worden vastgelegd in een datacenter, bijvoorbeeld of historische gebeurtenisgegevens van sensoren of iets anders kan zijn. In gevallen als volgt hebt u wel een big data-probleem. U moet een andere benadering.

Hallo verwerkingsflexibiliteit technologie vandaag voor het analyseren van grote gegevens is Hadoop. Een Apache open source-project, deze technologie Hallo Hadoop Distributed File System (HDFS)-gegevens opslaat en vervolgens kan ontwikkelaars maken tooanalyze voor MapReduce-taken die gegevens. HDFS verspreid gegevens over meerdere servers, en vervolgens voert reeksen Hallo MapReduce-taak op elke service laten Hallo big data parallel worden verwerkt.

HDInsight is Hallo-naam van hello Azure gebaseerde Apache Hadoop-service. HDInsight kunt HDFS gegevens worden opgeslagen op Hallo-cluster en het verdelen over meerdere virtuele machines. Deze ook verspreid Hallo logica van een MapReduce-taak over de VM's. Net zoals met lokale Hadoop, gegevens verwerkte lokaal-Hallo logica en gegevens van Hallo werkt op zich in dezelfde virtuele machine Hallo- en parallel voor betere prestaties. HDInsight kan ook opgeslagen in Azure Storage kluis (ASV), dat gebruikmaakt van blobs.  Met ASV kunt u toosave geld omdat u kunt uw HDInsight-cluster als deze niet in gebruik verwijderen, maar nog steeds uw gegevens in de cloud Hallo blijven.

HDinsight biedt ondersteuning voor andere onderdelen van Hallo Hadoop-ecosysteem, waaronder Hive en Pig. Microsoft heeft ook onderdelen waarmee eenvoudiger toowork met gegevens die door HDInsight worden geproduceerd met traditionele BI-hulpprogramma's, zoals Hallo HiveODBC adapter- en Data Explorer die werken met Excel worden gemaakt.

### <a name="high-performance-computing-big-compute"></a>High-Performance Computing (Big Compute)
Een van Hallo meest aantrekkelijk manieren toouse een cloudplatform is toorun high performance computing (HPC) en andere toepassingen 'Big Compute'. Voorbeelden zijn gespecialiseerde engineering toepassingen die zijn ontwikkeld toouse Hallo industriestandaard Message Passing Interface (MPI), evenals zogenaamde perfect parallelle toepassingen, zoals financiële risico-modellen.

Hallo essentie van Big Compute code wordt uitgevoerd op meerdere computers op Hallo hetzelfde moment. Op Azure betekent dit veel virtuele machines gelijktijdig uitgevoerd, alle werkt in parallelle toosolve een probleem. Hiervoor moet de enige manier tooresources en tooschedule toepassingen, dat wil zeggen, toodistribute hun werk over deze exemplaren. Het gratis HPC Pack van Microsoft en andere compute clusteroplossingen kunnen goed in Azure, profiteert van Azure services voor berekeningen en infrastructuur tooadd capaciteit op aanvraag tooan lokale Reken-cluster of Big Compute-toepassingen uitvoeren volledig in Hallo uitvoeren cloud.

Azure biedt een bereik van de virtuele machine exemplaar grootten met verschillende configuraties van CPU-kernen, geheugen, schijfcapaciteit en andere kenmerken toomeet Hallo vereisten van verschillende toepassingen. Hallo onlangs geïntroduceerd A8 en A9 exemplaren werken goed bij veel compute intensieve werkbelastingen en parallelle MPI-toepassingen met name omdat ze hoge snelheid, multicore processors en grote hoeveelheden geheugen. In bepaalde configuraties profiteren Hallo exemplaren van een lage latentie en hoge gegevensdoorvoer toepassingsnetwerk in Hallo cloud met remote direct memory access (RDMA)-technologie voor maximale efficiëntie van parallelle MPI-toepassingen.

Azure biedt ook Big Compute ontwikkelaars en partners een volledige set van compute-mogelijkheden, services, architectuurkeuzen en ontwikkelingsprogramma's. Azure ondersteunt aangepaste Big Compute-werkstromen met betrekking tot gespecialiseerde gegevens werkstromen en taak en planning patronen die kunnen worden geschaald toothousands van compute kernen.

## <a name="media"></a>Media
![Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Afbeelding: Mediaservices is een platform voor toepassingen die video en andere tooclients media Hallo wereld bieden.**

Video maakt een groot deel van het internetverkeer vandaag de dag en dat percentage morgen nog groter worden. Nog waarbij video op Hallo web is niet eenvoudig. Er zijn veel variabelen, zoals Hallo codering algoritme en Hallo resolutie van het scherm van de gebruiker Hallo weergegeven. Video doorgaans ook toohave bursts in vraag, zoals een piek zaterdag nacht wanneer veel mensen beslist dat ze graag toowatch een online-film.

Gezien de populariteit, is een kluis relevante treffers dat veel nieuwe toepassingen die video gebruik wordt gemaakt. Maar ze allemaal toosolve sommige moet Hallo dezelfde problemen en maken van elk criterium oplossen van deze problemen op een eigen zinvol is geen. Een betere benadering is een platform waarmee u algemene oplossingen veel toepassingen toouse toocreate. En bouwen van dit platform in Hallo cloud heeft enkele voordelen wissen. Kan algemeen beschikbaar is op basis van betalen naar gebruik, en ook Hallo variabiliteit van de vraag die vaak met video toepassingen dezelfde kan verwerken.

Azure Media Services lost dit probleem. Dit biedt een set van cloud-onderdelen die leven eenvoudiger voor gebruikers maken en uitvoeren van toepassingen met media video en andere.

Zoals Hallo afbeelding kunt zien, biedt Media Services een reeks onderdelen voor toepassingen die met video's en andere media werken. Het bevat bijvoorbeeld een medium onderdeel tooupload video opnemen in Media Services (waar deze wordt opgeslagen in Azure Blobs), een onderdeel van het codering die ondersteuning biedt voor verschillende video en audio-indelingen, een onderdeel van de beveiliging van inhoud waarmee beheer van digitale rechten een onderdeel voor het invoegen van advertenties in een videostream en -onderdelen voor streaming. Microsoft-partners kunnen ook onderdelen opgeven voor Hallo-platform en vervolgens dat Microsoft deze onderdelen te distribueren en namens hen in rekening brengen.

Toepassingen die gebruikmaken van dit platform kunnen uitvoeren op Azure of ergens anders. Bijvoorbeeld, een bureaubladtoepassing voor een video productie huis kunt mogelijk de uploaden video tooMedia Services, gebruikers vervolgens verwerken op verschillende manieren. Een cloud-gebaseerde inhoudsbeheer service uitgevoerd op Azure mogelijk ook afhankelijk zijn van Media Services tooprocess en distribueren van video. Waar deze wordt uitgevoerd en wat het doet, elke toepassing welke onderdelen u kiest moet toouse, toegang hebben tot deze via RESTful-interfaces.

toodistribute wat is het resultaat, een toepassing hello Azure CDN van een andere CDN kan gebruiken of alleen verzenden bits rechtstreeks toousers. Echter er krijgt, video gemaakt met behulp van Media Services kan worden gebruikt door verschillende clientsystemen, met inbegrip van Windows, Macintosh HTML 5, iOS, Android, Windows Phone, Flash en Silverlight. Hallo doel toomake is het eenvoudiger toocreate media moderne toepassingen.

**Verwijzingen**

Voor een meer visuele weergave van de werking van Media Services, downloaden Hallo [Azure Media Services Poster][Azure Media Services Poster].

## <a name="commerce"></a>Commerce
Hallo stijging van de Software als een Service worden getransformeerd hoe we toepassingen maken. Dit wordt ook transformeren hoe we toepassingen verkopen. Omdat een SaaS-toepassing in de cloud hello woont, is het zinvol die de potentiële klanten er voor online-oplossingen ziet. En deze wijziging geldt toodata, evenals tooapplications. Waarom mag niet mensen toohello cloud er voor de handel verkrijgbaar gegevenssets Microsoft houdt zowel deze problemen Hello [Azure Marketplace](https://azure.microsoft.com/marketplace/).

![Azure-Commerce](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Afbeelding: Azure Marketplace en Azure Store kunt u vinden en kopen van Azure-toepassingen en in de commerciële gegevenssets en ze als onderdeel van uw Azure-toepassingen gebruiken.**

Hallo verschil tussen twee Hallo is dat Marketplace bevindt zich buiten het hello Azure Management Portal, maar Hallo Store is toegankelijk vanuit binnen Hallo-portal. Potentiële klanten kunnen zoeken toofind Azure toepassingen die hun behoeften. Klanten kunnen zoeken voor commerciële gegevenssets, met inbegrip van demografische gegevens, financiële gegevens en geografische gegevens. Wanneer ze iets dat die ze graag wilt vinden, toegang te krijgen tot deze vanaf Hallo leverancier, rechtstreeks via Hallo Marketplace of weblocaties Store of in sommige gevallen van Hallo-beheerportal. Toepassingen kunnen ook gebruikmaken van Hallo Bing zoeken-API via Hallo Marketplace, zodat ze toegang krijgen tot toohello resultaten van zoekacties op het web.

**Commerce scenario 's**

SendGrid is een toepassing in hello Azure Store waarmee u toosend e-mailbericht. Biedt aanvullende functionaliteit, zoals de levering van betrouwbare en statistieken.  U kunt kopen van deze toepassing en verwante services plaats toobuild dergelijke infrastructuur Probeer zelf.  

## <a name="getting-started"></a>Aan de slag
Nu u hebt Hallo grote afbeelding Hallo volgende stap is toowrite uw eerste Azure-toepassing. Kies uw taal [ophalen Hallo juiste SDK](/downloads/), en Ga daarvoor. Cloud computing Hallo nieuwe standaard--is nu aan de slag.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
