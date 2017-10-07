---
title: aaaAzure opslag controlelijst voor prestaties en schaalbaarheid | Microsoft Docs
description: Een controlelijst met bewezen voor gebruik met Azure Storage zodat toepassingen te ontwikkelen.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage
## <a name="overview"></a>Overzicht
Sinds de release van de Hallo van Hallo Microsoft Azure Storage-services, Microsoft heeft een aantal beproefde procedures voor het gebruik van deze services op een manier zodat ontwikkeld en dit artikel dient tooconsolidate Hallo belangrijkste hiervan in een controlelijst-stijl-lijst. Hallo-doel van dit artikel is toohelp toepassingsontwikkelaars controleren of dat ze bewezen gebruiken met Azure Storage en toohelp ze andere bewezen overstap overweegt identificeren. In dit artikel probeert niet toocover elke mogelijke optimalisatie van prestaties en schaalbaarheid — worden uitgesloten die gevolgen klein of niet algemeen van toepassing zijn. tijdens het ontwerpen, is nuttig tookeep in vroeg stadium rekening kan worden voorspeld toohello zover gedrag van toepassing hello tooavoid ontwerpen die wordt uitgevoerd in prestatieproblemen.  

Elke ontwikkelaar van toepassingen met behulp van Azure Storage moet nemen Hallo tijd tooread in dit artikel en controleer zijn of haar toepassing gevolgd elk Hallo bewezen onderstaande procedures.  

## <a name="checklist"></a>Controlelijst
In dit artikel organiseert Hallo bewezen procedures in Hallo groepen te volgen. Bewezen toepassingen die van toepassing op:  

* Alle Azure Storage-services (blobs, tabellen, wachtrijen en -bestanden)
* Blobs
* Tabellen
* Wachtrijen  

| Klaar | Onderwerp | Category | Vraag |
| --- | --- | --- | --- |
| &nbsp; | Alle services |Schaalbaarheidsdoelen |[Uw toepassing ontworpen tooavoid bijna is bereikt Hallo schaalbaarheidsdoelen?](#subheading1) |
| &nbsp; | Alle services |Schaalbaarheidsdoelen |[Is een uw naming convention ontworpen tooenable betere taakverdeling?](#subheading47) |
| &nbsp; | Alle services |Netwerken |[Hebt side clientapparaten hoog genoeg bandbreedte en lage latentie tooachieve Hallo prestaties die nodig zijn?](#subheading2) |
| &nbsp; | Alle services |Netwerken |[Hebt clientapparaten naast een koppeling hoog genoeg kwaliteit?](#subheading3) |
| &nbsp; | Alle services |Netwerken |[Hallo-clienttoepassing vindt 'aan' hello storage-account?](#subheading4) |
| &nbsp; | Alle services |Inhoudsdistributie |[Gebruikt u de CDN voor distributie van inhoud?](#subheading5) |
| &nbsp; | Alle services |Directe clienttoegang |[Gebruikt u SAS en CORS tooallow directe toegang toostorage in plaats van proxy?](#subheading6) |
| &nbsp; | Alle services |Caching |[Uw cache toepassingsgegevens die herhaaldelijk wordt gebruikt en de wijzigingen zelden is?](#subheading7) |
| &nbsp; | Alle services |Caching |[Is uw toepassing batchverwerking updates (deze clientzijde in cache en vervolgens uploaden in grotere sets)?](#subheading8) |
| &nbsp; | Alle services |.NET-configuratie |[Hebt u uw client-toouse een voldoende aantal gelijktijdige verbindingen geconfigureerd?](#subheading9) |
| &nbsp; | Alle services |.NET-configuratie |[Hebt u .NET toouse een voldoende aantal threads geconfigureerd?](#subheading10) |
| &nbsp; | Alle services |.NET-configuratie |[Gebruikt u de .NET 4.5 of hoger, waarop garbagecollection is verbeterd?](#subheading11) |
| &nbsp; | Alle services |Parallelle uitvoering |[U zorgt dat parallelle uitvoering op de juiste wijze wordt begrensd zodat u niet de clientmogelijkheden of de schaalbaarheidsdoelen Hallo overbelasting?](#subheading12) |
| &nbsp; | Alle services |Hulpprogramma's |[Vindt u de nieuwste versie van Microsoft hello clientbibliotheken en hulpprogramma's?](#subheading13) |
| &nbsp; | Alle services |Nieuwe pogingen |[Weet u exponentieel uitstel met beleid voor beperking van de fouten en time-outs voor opnieuw proberen?](#subheading14) |
| &nbsp; | Alle services |Nieuwe pogingen |[Is uw toepassing waarbij pogingen voor niet-herstelbare fouten?](#subheading15) |
| &nbsp; | Blobs |Schaalbaarheidsdoelen |[Hebt u een groot aantal clients tegelijkertijd toegang krijgen tot een enkel object?](#subheading46) |
| &nbsp; | Blobs |Schaalbaarheidsdoelen |[Is uw toepassing binnen Hallo bandbreedte of operations schaalbaarheid doel voor één blob blijft?](#subheading16) |
| &nbsp; | Blobs |Blobs kopiëren |[Weet u kopiëren blobs op efficiënte wijze?](#subheading17) |
| &nbsp; | Blobs |Blobs kopiëren |[Gebruikt u AzCopy voor bulksgewijs kopieën van BLOB's?](#subheading18) |
| &nbsp; | Blobs |Blobs kopiëren |[Gebruikt u Azure Import/Export tootransfer zeer grote hoeveelheden gegevens?](#subheading19) |
| &nbsp; | Blobs |Met behulp van metagegevens |[Bewaart u veelgebruikte metagegevens over blobs in de metagegevens?](#subheading20) |
| &nbsp; | Blobs |Snel uploaden |[Wanneer u snel probeert tooupload één blob, uploadt u blokken parallel?](#subheading21) |
| &nbsp; | Blobs |Snel uploaden |[Wanneer u probeert tooupload veel blobs snel, uploadt u blobs parallel?](#subheading22) |
| &nbsp; | Blobs |Juiste Blob-Type |[Gebruikt u pagina-blobs of blok-blobs als het nodig?](#subheading23) |
| &nbsp; | Tabellen |Schaalbaarheidsdoelen |[Weet u bijna Hallo schaalbaarheidsdoelen voor entiteiten per seconde?](#subheading24) |
| &nbsp; | Tabellen |Configuratie |[Gebruikt u JSON voor uw tabel aanvragen?](#subheading25) |
| &nbsp; | Tabellen |Configuratie |[Hebt u uitgeschakeld Nagle tooimprove Hallo prestaties van kleine aanvragen?](#subheading26) |
| &nbsp; | Tabellen |Tabellen en partities |[Uw gegevens correct gepartitioneerd?](#subheading27) |
| &nbsp; | Tabellen |Hot partities |[Weet u alleen toevoegen en voeg alleen-lezen patronen voorkomen?](#subheading28) |
| &nbsp; | Tabellen |Hot partities |[Worden uw bijgewerkte voegt verdeeld over veel partities?](#subheading29) |
| &nbsp; | Tabellen |Querybereik |[Hebt u uw schema tooallow voor punt-query's toobe gebruikt in de meeste gevallen en tabel query's toobe spaarzaam ontworpen?](#subheading30) |
| &nbsp; | Tabellen |Query-dichtheid |[Uw query's doorgaans alleen scan doen en retourneert de rijen die door uw toepassing wordt gebruikt?](#subheading31) |
| &nbsp; | Tabellen |Beperkende geretourneerde gegevens |[Gebruikt u filteren tooavoid terugkerende entiteiten die niet nodig zijn?](#subheading32) |
| &nbsp; | Tabellen |Beperkende geretourneerde gegevens |[Gebruikt u projectie tooavoid retourneren van eigenschappen die niet nodig zijn?](#subheading33) |
| &nbsp; | Tabellen |Denormalization |[Hebt u uw gegevens gedenormaliseerd zodat u inefficiënte query's of meerdere leesaanvragen voorkomen bij het tooget gegevens?](#subheading34) |
| &nbsp; | Tabellen |Invoegen, bijwerken, verwijderen |[Zijn batchverwerking aanvragen die moeten toobe transactionele of kunnen plaatsvinden op Hallo dezelfde tooreduce retourbewerkingen tijd?](#subheading35) |
| &nbsp; | Tabellen |Invoegen, bijwerken, verwijderen |[Bent u vermijden bij het ophalen van een entiteit alleen toodetermine of toocall invoegen of bijwerken?](#subheading36) |
| &nbsp; | Tabellen |Invoegen, bijwerken, verwijderen |[Hebt u beschouwd als reeks gegevens dat wordt vaak opgehaald samen in één entiteit opslaan als eigenschappen in plaats van meerdere entiteiten?](#subheading37) |
| &nbsp; | Tabellen |Invoegen, bijwerken, verwijderen |[Voor entiteiten die wordt altijd samen worden opgehaald en kunnen worden geschreven in batches (bijvoorbeeld tijd reeksgegevens), hebt u beschouwd als blobs in plaats van tabellen gebruiken?](#subheading38) |
| &nbsp; | Wachtrijen |Schaalbaarheidsdoelen |[Weet u bijna Hallo schaalbaarheidsdoelen voor berichten die per seconde?](#subheading39) |
| &nbsp; | Wachtrijen |Configuratie |[Hebt u uitgeschakeld Nagle tooimprove Hallo prestaties van kleine aanvragen?](#subheading40) |
| &nbsp; | Wachtrijen |Berichtgrootte |[Zijn uw berichten compact tooimprove Hallo prestaties van de wachtrij Hallo?](#subheading41) |
| &nbsp; | Wachtrijen |Bulksgewijs ophalen |[Weet u bij het ophalen van meerdere berichten in één bewerking 'Ophalen'?](#subheading42) |
| &nbsp; | Wachtrijen |Pollingfrequentie opgeven |[Weet u vaak genoeg tooreduce Hallo waargenomen latentie van uw toepassing polling?](#subheading43) |
| &nbsp; | Wachtrijen |Updatebericht |[Gebruikt u UpdateMessage toostore voortgang in verwerking van berichten, vermijden volledige Hallo-bericht tooreprocess hebben als er een fout optreedt?](#subheading44) |
| &nbsp; | Wachtrijen |Architectuur |[Gebruikt u wachtrijen toomake uw hele toepassing meer schaalbare doordat langlopende werkbelastingen buiten Hallo kritieke pad en de schaal vervolgens onafhankelijk?](#subheading45) |

## <a name="allservices"></a>Alle Services
Deze sectie vindt bewezen toepassingen die van toepassing toohello gebruik van een van de hello Azure Storage-services (blobs, tabellen, wachtrijen of bestanden).  

### <a name="subheading1"></a>Schaalbaarheidsdoelen
Elk hello Azure Storage-services heeft schaalbaarheidsdoelen voor capaciteit (GB), Transactiesnelheid en bandbreedte. Als uw toepassing nadert of hoger is dan een schaalbaarheidsdoelen hello, ondervinden het toegenomen transactie latenties of beperking. Wanneer een opslagservice uw toepassing bandbreedte, begint Hallo service tooreturn '503 Server bezet' of '500 time-out voor de bewerking' foutcodes voor sommige opslagtransacties. Deze sectie besproken in het bijzonder beide Hallo algemeen de aanpak toodealing met schaalbaarheidsdoelen en schaalbaarheidsdoelen van bandbreedte. Latere secties die betrekking op afzonderlijke opslagservices hebben behandeld schaalbaarheidsdoelen in de context van die service Hallo:  

* [BLOB-bandbreedte en aanvragen per seconde](#subheading16)
* [Tabelentiteiten per seconde](#subheading24)
* [Wachtrijberichten per seconde](#subheading39)  

#### <a name="sub1bandwidth"></a>Doel van schaalbaarheid bandbreedte voor alle Services
Op moment van schrijven Hallo Hallo bandbreedte doelen in Hallo VS voor een geografisch redundante opslag (GRS)-account zijn 10 Gigabit per seconde (Gbps) voor inkomend (gegevens verzonden toohello storage-account) en 20 Gbps voor uitgaande (gegevens verzonden van Hallo storage-account). Voor een account lokaal redundante opslag (LRS) Hallo gelden de documentlimieten hoger – 20 Gbps voor inkomend en 30 Gbps voor uitgaande.  Internationale bandbreedtelimieten mogelijk lager en vindt u op onze [schaalbaarheid van de pagina](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Zie voor meer informatie over opties voor opslag redundantie Hallo Hallo-koppelingen in [nuttige informatiebronnen](#sub1useful) hieronder.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Welke toodo als een doel schaalbaarheid bijna bereikt
Als uw toepassing Hallo schaalbaarheidsdoelen voor een enkele storage-account nadert, kunt u overwegen gebruik nemen van een van de volgende benaderingen Hallo:  

* Andere Hallo werkbelasting dat ervoor zorgt uw toepassing tooapproach dat of Hallo schaalbaarheid doel overschrijden. Kunt u een ontwerp anders toouse minder bandbreedte of capaciteit of minder transacties?
* Als een toepassing moet groter zijn dan een van de schaalbaarheidsdoelen hello, moet u meerdere opslagaccounts en partitie uw toepassingsgegevens tussen die meerdere opslagaccounts. Als u dit patroon gebruikt, dan worden toodesign ervoor dat uw toepassing zodat u meer storage-accounts in Hallo toekomstige voor taakverdeling toevoegen kunt. Op het moment van schrijven, kan elk Azure-abonnement hebben up too100 storage-accounts.  Storage-accounts hebben ook geen kosten dan gebruik van uw in termen van de gegevens die zijn opgeslagen, transacties die zijn aangebracht of gegevens die zijn overgebracht.
* Als uw toepassing hello bandbreedte doelen raakt, kunt u overwegen het comprimeren van gegevens in Hallo client tooreduce Hallo bandbreedte vereist toosend Hallo gegevens toohello storage-service.  Houd er rekening mee dat terwijl dit kunt u bandbreedte besparen en verbetering van netwerkprestaties, het kan ook sommige negatieve gevolgen hebben.  Hallo prestatie-invloed van dit vanwege toohello verdere verwerkingsvereisten voor het comprimeren en decomprimeren van gegevens in Hallo-client, moet u evalueren. Bovendien gecomprimeerde gegevens op te slaan, kunt u moeilijker tootroubleshoot problemen omdat het moeilijker tooview opgeslagen gegevens met standaardprogramma's mogelijk.
* Als uw toepassing hello schaalbaarheidsdoelen raakt, Verzeker u ervan dat u van exponentieel uitstel voor nieuwe pogingen gebruikmaakt (Zie [pogingen](#subheading14)).  De betere toomake zeker dat u nooit Hallo schaalbaarheidsdoelen benadert (met behulp van een van de Hallo hierboven methoden), maar dit zorgt ervoor dat uw toepassing won't NET houden snel opnieuw uit te voeren, waardoor Hallo erger beperking.  

#### <a name="useful-resources"></a>Nuttige informatie
Hallo volgende koppelingen bieden aanvullende details voor schaalbaarheidsdoelen:

* Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie over schaalbaarheidsdoelen.
* Zie [Azure Storage-replicatie](storage-redundancy.md) en Hallo blogbericht [opslagopties van Azure voor redundantie en geografisch redundante opslag met leestoegang](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) voor meer informatie over opties voor opslag redundantie.
* Zie voor actuele informatie over prijzen voor Azure-services [Azure-prijzen](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>De naamconventie partitie
Azure-opslag gebruikt een bereik gebaseerde partitionering schema tooscale en de belasting saldo Hallo systeem. Hallo partitiesleutel is gebruikte toopartition gegevens in bereiken en deze bereiken worden verdeeld over Hallo systeem. Dit betekent dat naamconventies zoals lexicale ordenen (bijvoorbeeld msftpayroll, msftperformance, msftemployees, enzovoort) of met behulp van tijdstempels (log20160101, log20160102, log20160102, enzovoort) lenen zelf toohello partities wordt mogelijk CO-locatie op Hallo dezelfde partitie server, totdat een bewerking voor de taakverdeling deze in kleinere bereiken splitst. Alle blobs in een container kunnen bijvoorbeeld worden geleverd door een enkele server totdat hello belasting van deze blobs vereist meer herverdeling van Hallo partitie bereiken. Op dezelfde manier een groep licht geladen accounts met hun namen lexicale volgorde kan worden geleverd door een enkele server tot Hallo laden op een of alle van deze accounts ze toobe splitsen over meerdere partities servers moeten worden. Elke load balancer bewerking mogelijk van invloed op Hallo latentie van storage aanroepen tijdens het Hallo-bewerking. Hallo-systeem mogelijkheid toohandle die een plotselinge toename van verkeer tooa partitie wordt beperkt door Hallo schaalbaarheid van een server met één partitie totdat de bewerking voor taakverdeling Hallo gang in- en rebalances hello partitiesleutelbereik.  

U kunt volgen enkele aanbevolen procedures tooreduce Hallo frequentie van dergelijke bewerkingen.  

* Bekijk Hallo naamconventie die u nauw voor accounts, containers, blobs, tabellen en wachtrijen gebruiken. U kunt de accountnamen Mining met een 3-cijferige hash met een hash-functie die het beste past bij uw behoeften.  
* Als u uw gegevens dankzij tijdstempels of numerieke id's organiseren, hebt u tooensure u geen gebruikmaakt van een verkeerspatronen alleen toevoegen (of alleen-toevoegen). Deze patronen zijn niet geschikt voor een bereik-gebaseerd systeem partitioneren en kunnen lead tooall Hallo verkeer gaat tooa één partitie en beperkende Hallo-systeem van effectief taakverdeling. Als u dagelijks omgeleid bewerkingen die gebruikmaken van een blob-object met een tijdstempel zoals JJJJMMDD, klikt u vervolgens alle Hallo verkeer voor die dagelijks wordt bijvoorbeeld tooa één object dat wordt geleverd door een server met één partitie. Bekijk of Hallo per blob is beperkt en per partitie limieten aan uw behoeften voldoet, en u kunt deze bewerking in meerdere blobs op te splitsen indien nodig. Op dezelfde manier als u een reeksgegevens in de tabellen opslaat, alle Hallo-verkeer kan worden omgeleid toohello laatste deel van de belangrijkste naamruimte Hallo. Als u tijdstempels of numerieke id's gebruiken moet, het voorvoegsel met een 3-cijferige hash of in geval van tijdstempels voorvoegsel Hallo seconden deel van de tijd zoals ssyyyymmdd Hallo HALLO hallo id. Als het weergeven en opvragen bewerkingen worden regelmatig uitgevoerd, kiest u een hash-functie die wordt beperkt het aantal query's. In andere gevallen mogelijk een willekeurige voorvoegsel voldoende.  
* Lees voor meer informatie over Hallo partitieschema gebruikt in Azure Storage Hallo SOSP papier [hier](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Netwerken
Tijdens het Hallo-API aanroept materie, hebben vaak Hallo fysiek netwerk beperkingen van de toepassing hello aanzienlijke gevolgen op prestaties. Hallo hieronder worden enkele beperkingen die gebruikers kunnen ondervinden beschreven.  

#### <a name="client-network-capability"></a>Mogelijkheid via het netwerk van de client
##### <a name="subheading2"></a>Doorvoer
Hallo-probleem is voor bandbreedte, vaak Hallo-mogelijkheden van Hallo-client. Bijvoorbeeld, terwijl een enkele opslagaccount 10 Gbps of meer van de inkomende gegevens kan verwerken (Zie [schaalbaarheidsdoelen van bandbreedte](#sub1bandwidth)), de netwerksnelheid Hallo in een exemplaar van 'Kleine' Azure Worker-rol is alleen geschikt voor ongeveer 100 Mbps. Grotere Azure-exemplaren hebben NIC's met grotere capaciteit, dus u overwegen moet een grotere exemplaar of meer van de virtuele machine als u een hogere netwerk limieten vanaf één computer nodig. Als u een service Storage vanuit een on-premises-toepassing opent, wordt de hello dezelfde regel van toepassing is: netwerkmogelijkheden Hallo van clientapparaat Hallo en Hallo network connectivity toohello Azure-opslaglocatie begrijpen en ofwel te verbeteren, indien nodig of ontwerp van uw toepassing toowork binnen hun mogelijkheden.  

##### <a name="subheading3"></a>Kwaliteit van de verbinding
Net als bij alle netwerkgebruik Bedenk dat netwerkomstandigheden, wat leidt tot fouten en pakketverlies effectieve doorvoer vertragen.  Met behulp van WireShark of NetMon kan helpen bij het oplossen van dit probleem.  

##### <a name="useful-resources"></a>Nuttige informatie
Zie voor meer informatie over grootten van virtuele machines en toegewezen bandbreedte [Windows VM-grootten](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Linux VM-grootten](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Locatie
In de beste prestaties Hallo biedt Hallo-client in de buurt toohello server plaatsen in een gedistribueerde omgeving. Voor toegang tot Azure Storage met de laagste latentie hello, Hallo aanbevolen locatie voor de client zich bevindt binnen Hallo dezelfde Azure-regio. Als u een Azure-website die gebruikmaakt van Azure Storage hebt, moet u bijvoorbeeld beide in één regio (bijvoorbeeld VS-West of Zuidoost-Azië). Dit vermindert Hallo latentie en Hallo kosten — op Hallo moment van schrijven, bandbreedtegebruik binnen één regio is gratis.  

Als uw toepassingen niet in Azure (zoals apps voor mobiele apparaten of op de lokale enterprise-services), klikt u vervolgens opnieuw gehost worden client hello opslagaccount plaatsen in een regio in de buurt van toohello-apparaten die toegang hebben tot, in het algemeen de latentie te verminderen wordt. Als uw clients worden grote schaal gedistribueerd (voor bijvoorbeeld enkele in Noord-Amerika, en sommige in Europa), dan moet u overwegen meerdere opslagaccounts: een zich bevinden in een regio Noord-Amerika en een in een Europese regio. Dit helpt tooreduce latentie voor gebruikers in beide regio's. Deze aanpak is meestal eenvoudiger tooimplement als hello gegevensarchieven Hallo toepassing tooindividual voor specifieke gebruikers en vereist niet dat voor het repliceren van gegevens tussen opslagaccounts.  Voor een brede distributie van inhoud, verdient het aanbeveling een CDN: Zie de volgende sectie Hallo voor meer informatie.  

### <a name="subheading5"></a>Distributie van inhoud
Een toepassing moet tooserve Hallo dezelfde inhoud toomany gebruikers (bijvoorbeeld een product video gebruikt in de startpagina van een website Hallo demo) zich in een Hallo soms dezelfde of verschillende regio's. In dit scenario moet u een Content Delivery Network (CDN) zoals Azure CDN en Hallo CDN zou Azure-opslag gebruiken als Hallo oorsprong van Hallo-gegevens. In tegenstelling tot een Azure-opslagaccount die zich in één regio en die niet afleveren inhoud met een lage latentie tooother regio's, gebruikt Azure CDN servers in meerdere datacenters Hallo wereld. Bovendien kan een CDN doorgaans veel hoger uitgaande limieten dan een enkele opslagaccount ondersteunen.  

Zie voor meer informatie over Azure CDN [Azure CDN](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Met behulp van SAS- en CORS
Wanneer u code tooauthorize zoals JavaScript, in de webbrowser van een gebruiker of een mobiele telefoon-app tooaccess gegevens in Azure Storage, een aanpak is een toepassing in de Webrol als proxy toouse: Hallo gebruikersapparaat wordt geverifieerd met Hallo Webrol, die op hun beurt verifieert met Hallo storage-service. Op deze manier kunt u voorkomen dat blootstellen van uw toegangscodes voor opslag op onbeveiligde apparaten. Dit wordt een grote overhead echter geplaatst op Hallo Webrol omdat alle Hallo gegevens tussen Hallo gebruikersapparaat overgedragen en hello storage-service Hallo Webrol doorgeven moet. U kunt het gebruik van een Webrol als proxy voor Hallo storage-service met behulp van de Shared Access Signatures (SAS), soms in combinatie met koppen Cross-Origin-Resource delen (CORS) voorkomen. Met SAS, kunt u toestaan dat van uw gebruikers apparaat toomake-aanvragen rechtstreeks tooa storage-service met behulp van een token met beperkte toegang. Bijvoorbeeld, als een gebruiker wil tooupload een foto tooyour toepassing, kunt de Webrol genereren en te verzenden toohello gebruikersapparaat een SAS-token die machtiging toowrite tooa specifieke blob of een container voor Hallo komende 30 minuten (waarna hello SAS-token vervalt) verleent.

Een browser wordt normaal gesproken niet JavaScript toestaan op een pagina die wordt gehost door een website op één domein tooperform specifieke bewerkingen zoals een domein tooanother 'Geplaatst'. Bijvoorbeeld, als u een Webrol op 'contosomarketing.cloudapp.net' en de gewenste toouse client side JavaScript tooupload een blob storage-account op 'contosoproducts.blob.core.windows.net' tooyour host, een van de browser Hallo 'dezelfde oorsprong beleid' Dit wordt verbieden de bewerking. CORS is een browser-functie waarmee Hallo domein (in dit geval Hallo opslagaccount) toocommunicate toohello doelbrowser die wordt vertrouwd aanvragen die afkomstig zijn in het brondomein hello (in dit geval Hallo-Webrol).  

Beide technologieën kunt u onnodige laden (en knelpunten) op uw webtoepassing voorkomen.  

#### <a name="useful-resources"></a>Nuttige informatie
Zie voor meer informatie over SAS [handtekeningen voor gedeelde toegang, deel 1: Understanding Hallo SAS-Model](../storage-dotnet-shared-access-signature-part-1.md).  

Zie voor meer informatie over CORS [Cross-Origin-Resource delen (CORS) ondersteuning voor hello Azure Storage-Services](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Caching
#### <a name="subheading7"></a>Ophalen van gegevens
In het algemeen is het beter dan tweemaal aan eenmaal ophalen van gegevens van een service. Bekijk Hallo voorbeeld van een MVC-webtoepassing uitgevoerd in een Webrol die heeft al een blob 50MB opgehaald uit Hallo opslag service tooserve als inhoud tooa gebruiker. Hallo-toepassing kan vervolgens ophalen die dezelfde blob telkens wanneer een gebruiker vraagt of het kan cache plaatsen lokaal toodisk en hergebruik en lokale cache Hallo-versie voor daaropvolgende aanvragen. Bovendien telkens wanneer een gebruiker Hallo gegevens aanvraagt, Hallo toepassing kan probleem verkrijgen met een voorwaardelijke kop voor wijzigingstijd Hallo gehele blob vermijden zou als deze niet is gewijzigd. U kunt dit hetzelfde patroon tooworking met tabelentiteiten toepassen.  

In sommige gevallen kunt u beslissen dat uw toepassing dat Hallo blob geldig blijft gedurende een korte periode bij het ophalen van het bestand en vervullen kan dat tijdens deze periode Hallo toepassing hoeft niet toocheck als Hallo blob is gewijzigd.

Configuratie, opzoeken en andere gegevens die altijd door de toepassing hello gebruikt worden zijn goede kandidaten voor opslaan in cache.  

Zie voor een voorbeeld van hoe tooget een blob eigenschappen toodiscover Hallo datum van laatste wijziging met .NET, [Set eigenschappen ophalen en metagegevens en](../blobs/storage-properties-metadata.md). Zie voor meer informatie over voorwaardelijke downloads [voorwaardelijk vernieuwen van een lokale kopie van een Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Uploaden van gegevens in Batches
In bepaalde situaties toepassing, kunt u statistische gegevens lokaal en periodiek uploaden in een batch in plaats van elk gegevensitem direct te uploaden. Bijvoorbeeld, een webtoepassing ervoor kiezen om een logbestand van activiteiten: toepassing hello kan ofwel uploaden details van elke activiteit als dit als een Tabelentiteit gebeurt (waarvoor veel opslagbewerkingen) of activiteit details tooa lokale logboekbestand, kan worden opgeslagen en vervolgens regelmatig alle details van de activiteit als een bestand met scheidingstekens tooa blob uploaden. Als elke logboekvermelding 1KB groot is, kunt u duizenden in één 'Blob plaatsen' transactie (u kunt een blob van up too64MB in grootte in één transactie uploaden) uploaden. Natuurlijk als Hallo lokale computer voorafgaande toohello uploaden vastloopt, wordt mogelijk verbroken sommige logboekgegevens: Hallo toepassingsontwikkelaar moet ontwerpen voor de mogelijkheid Hallo van client-apparaat of fouten uploaden.  Als de activiteitsgegevens Hallo toobe voor timespans (niet slechts één activiteit) gedownload moet, worden de blobs voorkeur boven tabellen.

### <a name="net-configuration"></a>.NET-configuratie
Als u met behulp van .NET Framework hello, vindt deze sectie u enkele snelle configuratie-instellingen waarmee u de aanzienlijke prestatieverbeteringen toomake kunt.  Als u andere talen, controleert u toosee als vergelijkbare concepten van toepassing is in uw gekozen taal.  

#### <a name="subheading9"></a>Standaard verbindingslimiet verhogen
In .NET Hallo na code Hallo standaard verbindingslimiet bereikt (dit is doorgaans 2 in de clientomgeving van een of 10 in een serveromgeving) verhoogt too100. Normaal gesproken moet u Hallo waarde tooapproximately Hallo aantal threads die worden gebruikt door uw toepassing instellen.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Hallo verbindingslimiet bereikt voor het openen van alle verbindingen, moet u instellen.  

Zie voor andere programmeertalen die taal documentatie toodetermine hoe tooset Hallo verbinding beperken.  

Zie voor meer informatie, Hallo blogbericht [webservices: gelijktijdige verbindingen](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>ThreadPool Min Threads te verhogen als synchrone code met asynchrone taken
Deze code wordt Hallo thread pool min threads te verhogen:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Zie voor meer informatie [ThreadPool.SetMinThreads methode](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Profiteren van de .NET 4.5-garbagecollection
.NET 4.5 of hoger voor Hallo client toepassing tootake profiteren van de prestatieverbeteringen in server garbagecollection gebruiken.

Zie voor meer informatie artikel Hallo [een overzicht van prestatieverbeteringen in .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Ongebonden parallelle uitvoering
Parallelle uitvoering kan zijn ideaal voor prestaties, Wees voorzichtig bij meerdere partities met behulp van unbounded parallelle uitvoering (geen limiet op Hallo aantal threads en/of parallelle aanvragen) tooupload of downloaden van gegevens, met behulp van meerdere werknemers tooaccess (containers, wachtrijen, of tabel partities) in Hallo hetzelfde opslagaccount of tooaccess meerdere items in Hallo dezelfde partitie. Als Hallo parallelle uitvoering unbounded is, kan uw toepassing hoger zijn dan de capaciteit Hallo clientapparaat of Hallo schaalbaarheidsdoelen wat resulteert in langere latentietijden en beperking van storage-account.  

### <a name="subheading13"></a>Opslagclientbibliotheken en hulpprogramma 's
Gebruik altijd de meest recente van Microsoft-clientbibliotheken Hallo en hulpprogramma's. Bij Hallo schrijven zijn beschikbaar voor .NET, Windows Phone, Windows Runtime, Java en C++ clientbibliotheken, evenals de preview-bibliotheken voor andere talen. Microsoft heeft bovendien uitgebracht PowerShell-cmdlets en Azure CLI-opdrachten voor het werken met Azure Storage. Microsoft actief deze hulpprogramma's met het oog op prestaties ontwikkelt, houdt deze up toodate met het nieuwste Serviceversies Hallo en zorgt ervoor dat deze veel Hallo practices prestaties intern bewezen verwerken.  

### <a name="retries"></a>Nieuwe pogingen
#### <a name="subheading14"></a>Beperking/ServerBusy
In sommige gevallen Hallo storage-service mogelijk beperken van uw toepassing of mogelijk gewoon zijn niet kan tooserve Hallo aanvraag vanwege toosome tijdelijke toestand en retourneren een bericht '503 Server bezet' of '500 time-out'.  Dit kan gebeuren als uw toepassing bijna Hallo schaalbaarheidsdoelen is bereikt, of als Hallo system is herverdeling uw tooallow gepartitioneerde gegevens voor een hogere doorvoer.  Hallo-clienttoepassing doorgaans probeert opnieuw Hallo dat ervoor zorgt een dergelijke fout dat: poging Hallo dezelfde later aanvragen kan worden voltooid. Echter, als Hallo opslagservice uw toepassing is beperking, omdat deze schaalbaarheidsdoelen overschrijdt, of zelfs als het Hallo-service kan geen tooserve Hallo aanvraag om een andere reden is, agressieve pogingen meestal ervoor Hallo probleem verergert. Daarom moet u een exponentiële uit (Hallo client bibliotheken toothis standaardgedrag). Uw toepassing kan bijvoorbeeld opnieuw proberen na twee seconden vervolgens 4 seconden vervolgens 10 seconden vervolgens 30 seconden en vervolgens gaven ze volledig. Dit gedrag resulteert in uw toepassing aanzienlijk verminderen van de belasting op Hallo-service in plaats van exacerbating problemen.  

Houd er rekening mee dat connectiviteitsfouten kunnen opnieuw worden geprobeerd onmiddellijk, omdat ze niet Hallo resultaat van bandbreedtebeperking zijn en verwachte toobe tijdelijke zijn.  

#### <a name="subheading15"></a>Niet-herstelbare fouten
Hallo-clientbibliotheken zich bewust zijn van welke fouten opnieuw kunnen zijn en welke niet. Echter als u uw eigen code tegen Hallo storage REST-API schrijft, moet u er zijn enkele fouten die u niet proberen: bijvoorbeeld een 400 (ongeldige aanvraag) antwoord geeft aan dat clienttoepassing Hallo verzonden voor een aanvraag kan niet worden verwerkt omdat deze is niet in een verwachte vorm. Deze aanvraag opnieuw te verzenden leidt tot hetzelfde antwoord Hallo telkens, zodat er geen punt in het opnieuw proberen. Als u uw eigen code tegen Hallo storage REST-API schrijft, zich bewust zijn van welke Hallo foutcodes Hallo gemiddelde en de juiste manier tooretry (of niet) voor elk van deze.  

#### <a name="useful-resources"></a>Nuttige informatie
Zie voor meer informatie over foutcodes opslag [Status en foutcodes](http://msdn.microsoft.com/library/azure/dd179382.aspx) op Hallo Microsoft Azure-website.  

## <a name="blobs"></a>Blobs
In aanvulling toohello bewezen procedures voor [alle Services](#allservices) hierboven beschreven, Hallo volgende bewezen procedures toepassen specifiek toohello blob-service.  

### <a name="blob-specific-scalability-targets"></a>Van de BLOB-specifieke Schaalbaarheidsdoelen
#### <a name="subheading46"></a>Meerdere clients tegelijkertijd toegang krijgen tot een enkel object
Als u een groot aantal clients tegelijkertijd toegang krijgen tot een enkel object hebt, moet u tooconsider per object en opslag schaalbaarheidsdoelen van het account. Hallo exacte aantal clients die toegang een enkel object tot wordt variëren afhankelijk van factoren zoals het aantal clients dat tegelijk, Hallo object aanvraagt Hallo grootte van object Hallo Hallo, netwerk-voorwaarden enzovoort.

Als het Hallo-object kan worden gedistribueerd via de CDN bijvoorbeeld installatiekopieën of video's geleverd vanuit een website en vervolgens moet u een CDN. Zie [hier](#subheading5).

In andere scenario's zoals wetenschappelijke simulaties waar Hallo gegevens vertrouwelijk zijn hebt u twee opties. Hallo is eerst toostagger van uw workload toegang dergelijke die Hallo object wordt geopend via een periode van tegenover tegelijkertijd worden geopend. U kunt ook tijdelijk Hallo object toomultiple opslagaccounts totale IOP's per object en tussen opslagaccounts verhogen Hallo kopiëren. In de beperkte testen we gevonden dat ongeveer 25 virtuele machines tegelijkertijd een blob 100GB parallel (elke virtuele machine is Hallo downloaden met 32 threads parallelizing) kunnen downloaden. Als u had 100 clients hoeven tooaccess Hallo object, eerst kopiëren tooa tweede storage-account hebben eerst 50 virtuele machines toegang Hallo eerste blob Hallo en Hallo tweede 50 virtuele machines toegang Hallo tweede blob. Resultaten varieert afhankelijk van het gedrag van uw toepassingen zodat u dit tijdens het ontwerp moet testen. 

#### <a name="subheading16"></a>Bandbreedte en bewerkingen per Blob
U kunt lezen of schrijven tooa één blob op up tooa maximaal 60 MB per seconde (dit is ongeveer 480 Mbps die groter is dan Hallo-mogelijkheden van meerdere netwerken voor client-side (inclusief fysieke NIC op het clientapparaat Hallo Hallo). Bovendien ondersteunt één blob up too500 aanvragen per seconde. Als u meerdere clients die tooread nodig hebt hello dezelfde blob en u kunt deze beperkingen overschrijden, moet u overwegen een CDN voor het distribueren van Hallo blob.  

Zie voor meer informatie over de doorvoer van het doel voor blobs [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Kopiëren en verplaatsen van BLOB 's
#### <a name="subheading17"></a>Blob kopiëren
Hallo storage REST-API versie 2012-02-12 Hallo nuttig mogelijkheid toocopy blobs accounts geïntroduceerd: een clienttoepassing instrueren Hallo opslag service toocopy een blob uit een andere bron (mogelijk in een ander opslagaccount) en vervolgens laat u Hallo service uitvoeren asynchroon Hallo kopiëren. Dit kan aantasten Hallo bandbreedte nodig voor de toepassing hello wanneer u gegevens migreren van andere storage-accounts zijn, omdat u niet nodig toodownload en Hallo gegevens uploaden.  

Een overweging is echter dat bij het kopiëren tussen opslagaccounts, er geen tijd garantie is op als kopie hello wordt voltooid. Als uw toepassing een blob kopiëren snel onder uw beheer toocomplete moet, wellicht het beter toocopy Hallo blob door tooa VM downloaden en vervolgens uploaden toohello bestemming.  Voor volledige voorspelbaarheid in dit geval moet u zorgen dat Hallo kopie wordt uitgevoerd door een virtuele machine uitgevoerd in de Hallo dezelfde Azure-regio, anders netwerkomstandigheden mogelijk (en mogelijk wordt) invloed hebben op de prestaties van uw exemplaar.  Bovendien kunt u voortgang Hallo van een asynchrone kopie via een programma.  

Opmerking die binnen hetzelfde opslagaccount zichzelf zijn in het algemeen snel voltooid Hallo kopieert.  

Zie voor meer informatie [Blob kopiëren](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>AzCopy gebruiken
Hello Azure Storage-team heeft een opdrachtregelprogramma 'AzCopy' uitgebracht die geschikt toohelp met bulksgewijs overbrengen veel blobs naar, van, en tussen opslagaccounts.  Dit hulpprogramma is geoptimaliseerd voor dit scenario en maximale overdrachtssnelheid kunt bereiken.  Het gebruik ervan wordt aangemoedigd voor bulksgewijs laden, gedownload en kopieer scenario's. meer informatie over het toolearn en downloaden, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Azure Import/Export-Service
Voor zeer grote hoeveelheden gegevens (meer dan 1TB) biedt Azure Storage Hallo Hallo Import/Export-service, die staat voor het uploaden en downloaden van blob-opslag van back-upfunctie harde schijven.  Uw gegevens op een harde schijf te plaatsen en verzenden tooMicrosoft voor het uploaden, of een lege harde schijf tooMicrosoft toodownload gegevens verzenden.  Zie voor meer informatie [Hallo Microsoft Azure Import/Export-Service tooTransfer gegevens tooBlob opslag gebruiken](../storage-import-export-service.md).  Dit kan veel efficiënter dan uploaden/downloaden van dit volume aan gegevens via Hallo netwerk zijn.  

### <a name="subheading20"></a>Met behulp van metagegevens
Hallo blob-service ondersteunt head-aanvragen, met inbegrip van metagegevens over Hallo blob. Bijvoorbeeld als uw toepassing nodig Hallo EXIF gegevens buiten een foto, kan deze Hallo photo ophalen en pakt. toosave bandbreedte en de prestaties verbeteren, uw toepassing kan Hallo EXIF gegevens opslaan in Hallo blobmetagegevens wanneer de toepassing hello Hallo photo geüpload: u kunt vervolgens ophalen Hallo EXIF-gegevens in de metagegevens alleen in een HEAD-aanvraag met opslaan van veel bandbreedte en Hallo verwerkingstijd nodig tooextract Hallo EXIF-gegevens van elke blob tijd hello wordt gelezen. Dit is nuttig in scenario's waarbij u alleen Hallo-metagegevens en de volledige inhoud niet Hallo van een blob hoeft.  Houd er rekening mee dat alleen 8 KB van metagegevens per blob kunnen worden opgeslagen (Hallo service accepteert geen een toostore aanvraag meer dan die), zodat als Hallo gegevens in die grootte niet past, mag u niet kunt toouse worden deze benadering.  

Voor een voorbeeld van hoe tooget metagegevens van een blob met .NET, Zie [Set eigenschappen ophalen en metagegevens en](../blobs/storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Snel uploaden
tooupload BLOB's snel, de eerste vraag tooanswer Hallo is: weet u het uploaden van een blob of veel?  Gebruik Hallo hieronder richtlijnen toodetermine Hallo juiste methode toouse afhankelijk van uw scenario.  

#### <a name="subheading21"></a>Snel uploaden een groot blob
tooupload één grote snel blob, uw clienttoepassing uploaden de blokken of pagina's parallel (met name Houd ook rekening met de Hallo schaalbaarheidsdoelen voor afzonderlijke blobs en Hallo storage-account als geheel).  Houd er rekening mee dat Hallo officiële Microsoft geleverde RTM opslag clientbibliotheken (.NET, Java) Hallo mogelijkheid toodo dit.  Gebruik voor elk van de bibliotheken Hallo Hallo onder opgegeven objecteigenschap tooset Hallo niveau van gelijktijdigheid van taken:  

* .NET: Set ParallelOperationThreadCount op een BlobRequestOptions object toobe gebruikt.
* Java/Android: BlobRequestOptions.setConcurrentRequestCount() gebruiken
* Node.js: Gebruik parallelOperationThreadCount op beide opties Hallo-aanvraag of op Hallo blob-service.
* C++: Hallo blob_request_options::set_parallelism_factor methode gebruiken.

#### <a name="subheading22"></a>Veel blobs uploaden snel
veel snel blobs tooupload blobs parallel uploaden. Dit is sneller dan één BLOB's tegelijk met parallel blok uploads worden geüpload omdat het Hallo uploaden verspreid over meerdere partities van Hallo storage-service. Één blob biedt alleen ondersteuning voor een doorvoer van 60 MB per seconde (ongeveer 480 Mbps). Bij Hallo schrijven, een account op basis van VS LRS biedt ondersteuning voor maximaal too20 Gbps inkomend die veel meer dan een Hallo doorvoer wordt ondersteund door een afzonderlijke blob.  [AzCopy](#subheading18) uploads parallel standaard uitvoert, en wordt aanbevolen voor dit scenario.  

### <a name="subheading23"></a>Hallo juist type blob kiezen
Azure Storage ondersteunt twee typen blobs: *pagina* blobs en *blok* blobs. Uw keuze van het blobtype heeft invloed op Hallo prestaties en schaalbaarheid van uw oplossing voor een bepaalde gebruiksscenario. Blok-blobs geschikt zijn wanneer u grote hoeveelheden gegevens tooupload efficiënt wilt: bijvoorbeeld een clienttoepassing wellicht tooupload foto's of video tooblob opslag. Pagina-blobs zijn geschikt als Hallo toepassing tooperform willekeurige schrijfbewerkingen op Hallo gegevens moet: bijvoorbeeld Azure VHD's worden opgeslagen als pagina-blobs.  

Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tabellen
In aanvulling toohello bewezen procedures voor [alle Services](#allservices) hierboven beschreven, Hallo volgende bewezen procedures specifiek toohello tabelservice toepassen.  

### <a name="subheading24"></a>Tabel-specifieke Schaalbaarheidsdoelen
Tabellen hebben in toohello bandbreedtebeperkingen toevoeging van een volledige storage-account, Hallo specifieke schaalbaarheidslimiet te volgen.  Hallo system taakverdeling van als het verkeer toeneemt, maar als het verkeer onverwachte bursts heeft, mag u niet meteen kunnen tooget dit volume van doorvoer.  Als het patroon bursts is, u kunt toosee bandbreedtebeperking verwachten en/of time-outs tijdens Hallo burst als Hallo storage-service automatisch servertaken laden uit de tabel.  Langzaam doorgaans afhandelen heeft betere resultaten als op de juiste wijze Hallo system tijd tooload saldo kunt.  

#### <a name="entities-per-second-account"></a>Entiteiten per seconde (Account)
Hallo schaalbaarheidslimiet voor toegang tot tabellen is maximaal too20, 000 entiteiten (1KB elke) per seconde voor een account.  In het algemeen elke entiteit die wordt ingevoegd, bijgewerkt, verwijderd of gescand tellingen voor dit doel.  Dus een batchinvoeging met 100 entiteiten geteld als 100 entiteiten.  Een query waarmee 1000 entiteiten wordt gescand en retourneert 5 geteld als 1000 entiteiten.  

#### <a name="entities-per-second-partition"></a>Entiteiten per seconde (partitie)
Binnen een enkele partitie Hallo schaalbaarheid doel voor toegang tot tabellen 2.000 entiteiten (1KB elke) is per seconde, met behulp van Hallo dezelfde tellen zoals beschreven in de vorige sectie Hallo.  

### <a name="configuration"></a>Configuratie
Deze sectie vindt u verschillende snelle configuratie-instellingen die u kunt toomake aanzienlijke prestatieverbeteringen in de tabelservice hello gebruiken:  

#### <a name="subheading25"></a>Gebruik JSON
Vanaf versie van de service storage 2013-08-15, ondersteunt Hallo tabel-service het gebruik van JSON in plaats van Hallo AtomPub op basis van een XML-indeling voor het overbrengen van gegevens in een tabel. Dit bespaart nettolading grootten met zoveel 75% en prestaties van uw toepassing hello aanzienlijk verbeterd.

Zie voor meer informatie, Hallo boeken [Microsoft Azure-tabellen: Introducing JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) en [indeling van nettolading voor tabel servicebewerkingen](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Nagle uitschakelen
Nagle van algoritme is algemeen geïmplementeerd via TCP/IP-netwerken als een manier tooimprove netwerkervaring voor prestaties. Het is echter niet optimaal in alle gevallen (zoals interactieve omgevingen). Voor Azure Storage van Nagle-algoritme heeft een negatieve invloed op Hallo-prestaties van aanvragen toohello table en queue-services en moet u dit indien mogelijk uitschakelen.  

Zie voor meer informatie onze blogbericht [van Nagle-algoritme is niet beschrijvende kleine aanvragen](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), waarin wordt uitgelegd waarom Nagle van algoritme slecht communiceert met table en queue aanvragen en ziet u hoe toodisable in uw client de toepassing.  

### <a name="schema"></a>Schema
Hoe u vertegenwoordigen en uw gegevens opvragen is Hallo grootste één factor die van invloed op prestaties van de tabelservice Hallo Hallo. Terwijl elke toepassing verschilt, is deze sectie geeft een overzicht enkele algemene beproefde procedures die betrekking hebben op:  

* Tabelontwerp
* Efficiënt query 's
* Efficiënte Gegevensupdates  

#### <a name="subheading27"></a>Tabellen en partities
Tabellen worden onderverdeeld in partities. Elke entiteit die is opgeslagen in een partitie shares Hallo dezelfde partitiesleutel en heeft een sleutel tooidentify unieke rij in deze partitie. Partities voordelen bieden, maar ook limieten voor schaalbaarheid veroorzaken.  

* Voordelen: U kunt entiteiten in dezelfde partitie in een enkele, atomaire, batchtransactie met up too100 afzonderlijke opslagbewerkingen (maximaal 4MB totale grootte) Hallo bijwerken. Ervan uitgaande dat hetzelfde nummer Hallo van entiteiten toobe opgehaald, u kunt ook een query gegevens binnen één partitie efficiënter dan gegevens meerdere partities (Hoewel gelezen op voor verdere aanbevelingen voor het opvragen van tabelgegevens).
* Schaalbaarheidslimiet: toegang tooentities opgeslagen in één partitie kan niet worden taakverdeling omdat partities atomic batchtransacties ondersteunen. Om deze reden is Hallo schaalbaarheid doel voor de partitie van een afzonderlijke tabel lager dan voor Hallo tabel-service als geheel.  

Vanwege deze kenmerken van tabellen en partities, moet u overstapt op Hallo richtlijnen te volgen:  

* Gegevens die de clienttoepassing wordt regelmatig bijgewerkt of in dezelfde logische eenheid van werk moet zich bevinden in Hallo opgevraagd Hallo dezelfde partitie.  Dit kan zijn omdat schrijfbewerkingen is aggregeren van uw toepassing, of omdat u wilt profiteren van atomaire batchbewerkingen tootake.  Bovendien kan gegevens in één partitie worden efficiënter doorzocht in één query dan gegevens meerdere partities.
* Gegevens die door de clienttoepassing niet invoegen/bijwerken of -query in Hallo dezelfde logische eenheid van werk (één query of batch-update) moet zich bevinden in afzonderlijke partities.  Een belangrijke opmerking is dat er geen limiet toohello aantal partitiesleutels in één tabel, dus met miljoenen partitiesleutels geen probleem is en heeft geen invloed op prestaties.  Bijvoorbeeld, als uw toepassing een populaire website met gebruikersaanmelding, Hallo gebruikers-Id gebruikt als partitiesleutel Hallo mogelijk een goede keuze.  

#### <a name="hot-partitions"></a>Hot partities
Een hot partitie is een waarin een onevenredige percentage van Hallo verkeer tooan account is ontvangen en kan niet worden met gelijke taakverdeling omdat deze één partitie.  Hot partities gemaakt in het algemeen zijn twee manieren:  

##### <a name="subheading28"></a>Alleen toevoegen en voeg alleen patronen
Hallo 'Alleen toevoegen' patroon is een waar alle (of bijna alle) van Hallo verkeer tooa gegeven PK verhoogt, en vermindert volgens toohello huidige tijd.  Een voorbeeld is als uw toepassing Hallo huidige datum als een partitiesleutel voor logboekgegevens gebruikt.  Dit leidt ertoe dat alle Hallo voegt toohello laatste partitie in de tabel gaan en Hallo-systeem kan saldo niet laden omdat alle Hallo schrijfbewerkingen gaat toohello einde van de tabel zijn.  Als Hallo hoeveelheid verkeer toothat partitie Hallo partitie niveau schaalbaarheid doel overschrijdt, zal klikt u vervolgens het leiden tot beperking.  Het is beter tooensure dat verkeer wordt verzonden toomultiple partities tooenable load balance Hallo-aanvragen via de tabel.  

##### <a name="subheading29"></a>Intensief verkeer gegevens
Als uw partitionering schema resulteert in een enkele partitie die alleen gegevens die veel meer dan andere partities die worden gebruikt, ziet u mogelijk ook beperking als die partitie Hallo schaalbaarheid doel voor één partitie nadert.  Het is beter toomake ervoor dat de resultaten van de partitie-schema in geen enkel naderende Hallo schaalbaarheidsdoelen partitie.  

#### <a name="querying"></a>Uitvoeren van query 's
Deze sectie beschrijft bewezen Hallo tabelservice query's.  

##### <a name="subheading30"></a>Querybereik
Er zijn verschillende manieren toospecify Hallo bereik van entiteiten tooquery.  Hallo Hieronder volgt een bespreking van Hallo maakt gebruik van elke.  

In het algemeen te voorkomen dat scans (query's groter is dan één entiteit), maar als u scannen moet, probeer tooorganize uw gegevens zodat uw scans Hallo-gegevens zonder scannen of het opvragen van grote hoeveelheden entiteiten hoeft u niet ophalen.  

###### <a name="point-queries"></a>Punt-query 's
Een punt query haalt precies één entiteit. Dit gebeurt door zowel de partitiesleutel Hallo en rijsleutel van Hallo entiteit tooretrieve te geven. Deze query's zijn zeer efficiënte en u zoveel mogelijk deze moet gebruiken.  

###### <a name="partition-queries"></a>Partitie-query 's
Een partitiequery is een query waarmee een set gegevens die een algemene partitiesleutel deelt opgehaald. Hallo query bevat meestal een reeks sleutelwaarden rij of een bereik van waarden voor de eigenschap van een entiteit in toevoeging tooa partitiesleutel. Deze zijn minder efficiënt dan punt query's en moeten spaarzaam worden gebruikt.  

###### <a name="table-queries"></a>Tabel-query 's
Een tabelquery is een query waarmee een verzameling entiteiten die een algemene partitiesleutel niet deelt worden opgehaald. Deze query's zijn niet efficiënt en u indien mogelijk moet voorkomen.  

##### <a name="subheading31"></a>Query-dichtheid
Een andere belangrijke factor in de efficiëntie van de query is Hallo aantal entiteiten dat is geretourneerd als vergeleken toohello aantal entiteiten dat gescande toofind Hallo geretourneerd ingesteld. Als uw toepassing wordt een tabelquery met een filter voor een eigenschapswaarde dat slechts 1% van Hallo gegevens shares, Hallo query scant 100 entiteiten voor elke één entiteit wordt uitgevoerd. Hallo tabel schaalbaarheidsdoelen besproken eerder alle betrekking toohello aantal entiteiten dat is gescand, en niet Hallo aantal entiteiten dat is geretourneerd: een dichtheid lage query kan eenvoudig er Hallo tabel service toothrottle uw toepassing omdat deze zo veel moet scannen entiteiten tooretrieve Hallo entiteit die u zoekt.  Zie onderstaande Hallo-sectie op [denormalization](#subheading34) voor meer informatie over het tooavoid dit.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Beperkende Hallo bedrag van gegevens geretourneerd
###### <a name="subheading32"></a>Filteren
Wanneer u een query wordt retourneert entiteiten die u hoeft niet in de clienttoepassing Hallo weet, kunt u overwegen een filter tooreduce Hallo grootte van Hallo set geretourneerd. Tijdens het Hallo-entiteiten niet toohello client geretourneerd nog steeds meetellen voor Hallo-limieten voor schaalbaarheid, toepassingsprestaties van uw wordt vanwege Hallo verminderd nettolading netwerkgrootte verbeteren en Hallo verminderde aantal entiteiten dat is verwerkt door de clienttoepassing .  Zie boven notitie op [Query dichtheid](#subheading31), echter – hello schaalbaarheidsdoelen gerelateerd toohello aantal entiteiten dat is gescand, zodat een query die veel entiteiten gefilterd mogelijk nog steeds in de beperking, zelfs als er enkele entiteiten worden geretourneerd.  

###### <a name="subheading33"></a>Projectie
Als u de clienttoepassing een beperkt aantal eigenschappen van Hallo entiteiten in de tabel moet, kunt u projectie toolimit Hallo grootte van Hallo gegevensset geretourneerd. Net als bij filteren, helpt dit tooreduce netwerkbelasting en client verwerken.  

##### <a name="subheading34"></a>Denormalization
In tegenstelling tot het werken met relationele databases, leiden hello bewezen efficiënt opvragen van tabelgegevens toodenormalizing uw gegevens. Dat wil zeggen, het dupliceren van dezelfde gegevens in meerdere entiteiten Hallo (één voor elke sleutel mag u toofind Hallo gegevens) toominimize Hallo aantal entiteiten dat een query moet scannen toofind Hallo Hallo client gegevensbehoeften, hoeft u geen groot aantal entiteiten toofind tooscan Hallo gegevens moet voor uw toepassing.  Kunt u in een webwinkel toofind een order beide op Hallo klant-ID (Geef me van de klant orders) en op Hallo datum (Geef me orders op een datum).  In Table Storage, is het beste toostore Hallo entiteit (of een verwijzing tooit) tweemaal – eenmaal met de tabelnaam en PK RK toofacilitate zoeken door de klant-ID eenmaal toofacilitate Hallo datum vinden.  

#### <a name="insertupdatedelete"></a>Invoegen, bijwerken, verwijderen
Deze sectie beschrijft bewezen voor het wijzigen van de entiteiten die zijn opgeslagen in de tabelservice Hallo.  

##### <a name="subheading35"></a>Batchverwerking
Batchtransacties bekend als entiteit groep transacties (ETG) in Azure Storage; alle Hallo bewerkingen binnen een ETG moeten zich op één partitie in één tabel. Gebruik indien mogelijk, ETGs tooperform invoegen, bijwerken en verwijderen in batches. Dit vermindert het aantal retouren Hallo van uw client-toepassingsserver toohello vermindert Hallo aantal factureerbare transacties (een ETG telt als een enkele transactie voor facturering en up too100 opslagbewerkingen kan bevatten) en schakelt atomic updates (alle bewerkingen slagen of allemaal binnen een ETG mislukken). Omgevingen met hoge latentie, zoals mobiele apparaten profiteren aanzienlijk ETGs te gebruiken.  

##### <a name="subheading36"></a>Upsert
Gebruik tabel **Upsert** operations waar mogelijk. Er zijn twee soorten **Upsert**, die beide kunnen zijn efficiënter dan een traditionele **invoegen** en **Update** bewerkingen:  

* **InsertOrMerge**: Gebruik deze optie als u wilt dat een subset van Hallo entiteitseigenschappen tooupload, maar niet zeker weet of Hallo entiteit bestaat al. Als Hallo entiteit bestaat, deze aanroep Hallo-eigenschappen die zijn opgenomen in Hallo updates **Upsert** bewerking, en blijven alle bestaande eigenschappen zoals ze zijn, als hello entiteit bestaat niet, Hallo nieuwe entiteit wordt ingevoegd. Dit is vergelijkbaar toousing projectie in een query, hoeft u alleen tooupload Hallo eigenschappen die u wilt wijzigen.
* **InsertOrReplace**: Gebruik deze optie als u een geheel nieuwe entiteit tooupload wilt, maar u niet zeker weet of deze al bestaat. U moet dit alleen gebruiken wanneer u weet dat Hallo geüpload nieuwe entiteit klopt volledig omdat oude entiteit Hallo volledig overschrijft. U kunt bijvoorbeeld tooupdate Hallo entiteit waarmee de huidige locatie van een gebruiker ongeacht Hallo-toepassing al dan niet eerder locatiegegevens voor de gebruiker Hallo opgeslagen heeft; worden opgeslagen de nieuwe locatie entiteit Hallo is voltooid en u hoeft geen gegevens uit een eerdere entiteit.

##### <a name="subheading37"></a>De gegevensreeks opslaan in een enkele entiteit
Een toepassing slaat soms, een reeks vereiste gegevens dat vaak tooretrieve in één keer: bijvoorbeeld een toepassing kan CPU-gebruik gedurende een periode bijhouden in volgorde tooplot een rolling grafiek van Hallo gegevens van Hallo afgelopen 24 uur. Een aanpak is toohave één Tabelentiteit per uur, met elke entiteit die een specifiek uur en Hallo CPU-gebruik op te slaan voor dat uur. tooplot deze gegevens, de toepassing hello moet tooretrieve Hallo entiteiten die Hallo gegevens van Hallo 24 uur van de meest recente.  

U kunt ook uw toepassing hello CPU-gebruik kan opslaan voor elk uur als een afzonderlijke eigenschap van een enkele entiteit: tooupdate elk uur, uw toepassing kunt gebruiken één **InsertOrMerge Upsert** tooupdate Hallo waarde niet aanroepen voor Hallo meest recente uur. tooplot Hallo gegevens, toepassing hello hoeft slechts één entiteit in plaats van 24, maken voor een zeer efficiënte query tooretrieve (Zie hierboven discussie op [bereik query](#subheading30)).

##### <a name="subheading38"></a>Opslaan van gestructureerde gegevens in BLOB 's
Soms gestructureerde gegevens werkt zoals moet worden gegaan in tabellen, maar bereiken van entiteiten worden altijd samen opgehaald en kan worden batch ingevoegd.  Een goed voorbeeld hiervan is een logboekbestand.  In dit geval kunt u enkele minuten aan logboeken batch, voegt u deze, en vervolgens u enkele minuten aan logboeken op een tijdstip ook altijd een ophaalt.  In dit geval voor prestaties is het beter toouse blobs in plaats van tabellen, aangezien u kunt Hallo aantal objecten geschreven/geretourneerd aanzienlijk verminderen, evenals meestal Hallo aantal aanvragen die moeten worden aangebracht.  

## <a name="queues"></a>Wachtrijen
In aanvulling toohello bewezen procedures voor [alle Services](#allservices) hierboven beschreven, Hallo volgende bewezen procedures toepassen specifiek toohello queue-service.  

### <a name="subheading39"></a>Limieten voor schaalbaarheid
Een enkele wachtrij kunt ongeveer 2.000-berichten verwerken (1KB elke) per seconde (elke AddMessage GetMessage en DeleteMessage aantal als hier een bericht). Als dit onvoldoende voor uw toepassing is, moet u meerdere wachtrijen gebruiken en het Hallo-berichten verdeeld over deze.  

Huidige schaalbaarheidsdoelen op weergeven [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).  

### <a name="subheading40"></a>Nagle uitschakelen
Zie sectie Hallo van tabel configuratie die wordt besproken Hallo Nagle algoritme: Hallo Nagle algoritme is doorgaans nadelig voor Hallo prestaties van de wachtrij aanvragen en moet u dit uitschakelen.  

### <a name="subheading41"></a>Grootte van het bericht
Wachtrij afname prestaties en schaalbaarheid als bericht grootte toeneemt. U moet alleen Hallo informatie Hallo ontvanger moet plaatsen in een bericht.  

### <a name="subheading42"></a>Batch ophalen
U kunt ophalen too32 berichten uit een wachtrij in één bewerking. Dit kan Hallo aantal interactie verminderen van de clienttoepassing hello, dit vooral geschikt voor omgevingen, zoals mobiele apparaten is met hoge latentie.  

### <a name="subheading43"></a>Wachtrij Polling-Interval
De meeste toepassingen pollen berichten van een wachtrij, wat kan een van de grootste bronnen Hallo van transacties voor die toepassing. Selecteer uw polling-interval verstandig: polling te vaak kan ervoor zorgen dat uw toepassing tooapproach hello schaalbaarheidsdoelen voor Hallo wachtrij. 200.000 transacties voor $0,01 (op Hallo moment van schrijven) is één processor polling nadat elke seconde gedurende een maand zou u minder dan 15 cent dus kosten echter niet doorgaans een factor die invloed heeft op uw keuze van polling-interval.  

Zie voor kosteninformatie up-to-date [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
U kunt **UpdateMessage** tooincrease hello onzichtbaarheid time-out of tooupdate informatie over de status van een bericht. Dit is een krachtige, houd er rekening mee dat elke **UpdateMessage** bewerking telt naar Hallo schaalbaarheid doel. Dit kan echter zijn dat een benadering veel efficiënter dan wanneer een werkstroom die wordt doorgegeven een taak van een wachtrij toohello vervolgens elke stap van het Hallo-taak is voltooid. Met behulp van Hallo **UpdateMessage** bewerking kunt u uw toepassing toosave taak status toohello welkomstbericht en vervolgens doorgaan met werken in plaats van opnieuw queuing Hallo-bericht voor de volgende stap Hallo van Hallo taak telkens wanneer een stap is voltooid.  

Zie voor meer informatie artikel Hallo [hoe: Hallo inhoud van een bericht in de wachtrij wijzigen](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Toepassingsarchitectuur
Uw van schaalbare toepassingsarchitectuur, moet u wachtrijen toomake gebruiken. Hallo hieronder ziet u enkele manieren kunt u wachtrijen toomake uw toepassing meer schaalbare:  

* U kunt wachtrijen toocreate achterstanden van werk gebruiken voor de verwerking en vloeiend werkbelastingen in uw toepassing. Bijvoorbeeld, u kan in de wachtrij aanvragen van gebruikers tooperform processor intensief werken zoals geüploade afbeeldingen vergroten of verkleinen.
* U kunt wachtrijen toodecouple onderdelen van uw toepassing kunt gebruiken, zodat u afzonderlijk kunt schalen. Een webfront-end kan bijvoorbeeld enquêteresultaten van gebruikers plaatsen in een wachtrij voor latere analyse en opslag. U kunt toevoegen dat meer werkprocessen functie exemplaren tooprocess Hallo wachtrijgegevens naar behoefte.  

## <a name="conclusion"></a>Conclusie
In dit artikel besproken enkele van de meest voorkomende Hallo bewezen procedures voor het optimaliseren van de prestaties bij gebruik van Azure Storage. We raden elke toepassing developer tooassess hun toepassingen met elke Hallo hierboven procedures en overweeg namens Hallo aanbevelingen tooget goede prestaties voor hun toepassingen die gebruikmaken van Azure Storage.
