---
title: aaaMigrating BizTalk Server EDI-oplossingen tooBizTalk technische handleiding Services | Microsoft Docs
description: Migreren van EDI-tooMABS; Microsoft Azure BizTalk Services
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Migreren van BizTalk Server EDI-oplossingen tooBizTalk Services: technische handleiding

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Auteur: Tim Wieman en Mirchandani Mehrotra

Revisoren: Karthik Bharthy

Geschreven met behulp van: Microsoft Azure BizTalk Services – februari 2014-release.

## <a name="introduction"></a>Inleiding
Elektronische Data Interchange (EDI) is een van de Hallo meest gangbare manier waarop bedrijven uitwisselen van gegevens elektronisch, ook als Business-to-Business- of B2B genoemd. BizTalk Server heeft EDI-ondersteuning voor via een tien jaar sinds Hallo initiële BizTalk Server-versie. Met BizTalk Services blijft Microsoft hello ondersteuning voor EDI-oplossingen op Hallo Microsoft Azure-platform. B2B-transacties zijn voornamelijk externe tooan organisatie, en daarom is eenvoudiger tooimplement als deze is geïmplementeerd op een cloudplatform. Microsoft Azure biedt deze mogelijkheid via BizTalk Services.

Terwijl sommige klanten BizTalk Services als een platform 'greenfield' voor nieuwe EDI-oplossingen bekijkt, hebben veel klanten dat ze wil toomigrate tooAzure huidige BizTalk Server EDI-oplossingen. Omdat BizTalk Services EDI architectuur op basis van Hallo sleutel entiteiten zoals BizTalk Server EDI-architectuur (handelspartners, entiteiten, overeenkomsten), het is mogelijk toomigrate BizTalk Server EDI-artefacten tooBizTalk Services.

Dit document wordt besproken Hallo verschillen bij migratie BizTalk Server EDI-artefacten tooBizTalk Services. Dit document wordt ervan uitgegaan dat een praktische kennis van de BizTalk Server EDI-verwerking en Trading Partner overeenkomsten. Zie voor meer informatie over BizTalk Server EDI [Trading Partner met behulp van BizTalk beheerserver](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>Welke versie van BizTalk Server EDI-artefacten kan worden gemigreerd tooBizTalk Services?
Hallo BizTalk Server EDI-module is aanzienlijk verbeterd voor BizTalk Server 2010, werd tooinclude opnieuw gemodelleerd partners, profielen en overeenkomsten. BizTalk Services gebruikt hetzelfde model tooorganize hello handelspartners Hallo en zakelijke afdelingen binnen die handelspartners Hallo. Als gevolg hiervan migreren EDI artefacten uit BizTalk Server 2010 en nieuwere versies tooBizTalk Services, is een veel meer eenvoudig proces. toomigrate EDI-artefacten die zijn gekoppeld aan versies voorafgaande tooBizTalk Server 2010, moet u eerst een upgrade uitvoeren tooBizTalk Server 2010 en Migreer uw artefacten EDI tooBizTalk Services.

## <a name="scenariosmessage-flow"></a>Scenario's / berichtenstroom
Als met BizTalk Server is EDI verwerking van BizTalk Services gebaseerd op een oplossing Trading Partner Management (TPM). Hallo TPM-oplossing heeft Hallo volgende hoofdonderdelen:

* Handelspartners, die de organisatie in een transactie B2B vertegenwoordigen.
* Profielen die afdelingen binnen een trading partner vertegenwoordigen.
* Trading partner overeenkomsten (of overeenkomsten) die staan voor Hallo zakelijke overeenkomst tussen de twee partners/profielen.

Hallo volgende afbeelding ziet u Hallo overeenkomsten, evenals de verschillen tussen een BizTalk Server EDI-oplossing en de BizTalk Services EDI-oplossing:

![][EDImessageflow]

Hallo belangrijke verschillen en overeenkomsten tussen een stroom EDI-oplossing in BizTalk Server en BizTalk Services zijn:

* Net zoals BizTalk Server gebruikmaakt van een pijplijn EDIReceive tooreceive EDI-bericht en een EDISend pijplijn toosend EDI-bericht, gebruikt de BizTalk Services een brug tooreceive EDI ontvangen en verzenden EDI-brug toosend EDI-berichten. BizTalk Server Hallo pijplijnen zijn gekoppeld aan een overeenkomst met behulp van verzenden of ontvangen van poorten. Hallo-overeenkomst zelf geeft Hallo verzenden of ontvangen over de sitekoppelingsbrug in BizTalk Services.
* BizTalk Server nadat Hallo EDIReceive pijplijn processen Hallo EDI-bericht, is het Hallo-bericht het gedumpte tooa SQL Server-database. Hallo EdiSend pijplijn hervat vervolgens Hallo-bericht van Hallo SQL Server-database, verwerkt en verzendt het vervolgens toohello trading partner.
  
    In BizTalk Services nadat Hallo EDI bridge processen Hallo EDI-bericht, wordt stuurt deze Hallo-bericht tooan extern proces. Hallo extern proces kan worden uitgevoerd op Microsoft Azure of on-premises. Hallo extern proces moet routeren Hallo-bericht toohello EDI verzenden bridge; Hallo verzenden brug pull inherent niet wordt gemaakt van het Hallo-bericht. Na de verwerking van het Hallo-bericht routeert Hallo EDI verzenden bridge Hallo-bericht toohello trading partner.

BizTalk Services biedt een gemakkelijk te gebruiken configuratie ervaring tooquickly maken en implementeren van een B2B-overeenkomst tussen handelspartners zonder configureren van een Microsoft Azure Compute-exemplaren (Web- of Worker rollen), een Microsoft Azure SQL-Databases of een Microsoft Azure storage-accounts. Complexere scenario's verbinden in werkstromen of andere service-verwerking is vereist 'randen Hallo' van een Trading Partner-overeenkomst, dat wil zeggen vóór of na de verwerking van Trading Partner Agreement EDI-bridge. In detail hello volgende reeks gebeurtenissen zich voordoen tijdens een EDI-berichtverwerking in BizTalk Services.

1. Een EDI-bericht is ontvangen van trading partner Fabrikam.  Voor EDI-berichten ontvangen van handelspartners, ondersteunt BizTalk Services transportprotocollen zoals FTP-, SFTP AS2 en HTTP-/ S.
2. Hallo trading partner agreement ontvangstzijde verwerking worden ontleed Hallo EDI-berichtindeling tooXML.  U kunt versturen Hallo ontleed EDI-bericht (in XML-indeling) tooService Bus eindpunten zoals een Service Bus Relay-eindpunt, Service Bus-onderwerp, Service Bus-wachtrij of een brug BizTalk Services.
3. Hallo kunnen XML-berichten vervolgens worden ontvangen van Hallo-eindpunt voor verdere aangepaste verwerking.  Deze eindpunten kunnen bijvoorbeeld worden verwerkt door het onderdeel van een lokale of een Microsoft Azure Compute-exemplaar toofurther proces Hallo-bericht in een Windows-werkstroom (WF) of Windows Communication Foundation (WCF)-service.
4. Hallo ' verzendkant ' hello handelspartnerovereenkomst vervolgens ophaalprotocol XML het Hallo-bericht naar EDI-indeling bewerken en verzendt het Contoso-tootrading partner.  BizTalk Services ondersteunt voor het verzenden van berichten EDI tootrading partners, Hallo dezelfde als die worden gebruikt voor het ontvangen van berichten EDI protocollen.

Dit document verder bevat algemene richtlijnen over migreren van sommige Hallo andere BizTalk Server EDI-artefacten tooBizTalk Services.

## <a name="sendreceive-ports-tootrading-partners"></a>Verzenden/ontvangen poorten tooTrading Partners
BizTalk Server u locaties ontvangen en instellen ontvangen poorten tooreceive EDI/XML-berichten van handelspartners, en u Send poorten toosend EDI/XML-berichten tootrading partner instellen. U bezighouden deze poorten tooa trading partner agreement met behulp van Hallo BizTalk-beheerconsole op de Server vervolgens. In BizTalk Services Hallo Hallo locaties waar het ontvangen van berichten handelspartners en waar u verzendt berichten tootrading partners zijn geconfigureerd als onderdeel van Hallo trading partner agreement zelf (als onderdeel van Transport-instellingen) in BizTalk Services-Portal .  Zodat u echt geen Hallo concept van 'send poorten' en 'ontvangen locaties', per definitie in BizTalk Services. Zie voor meer informatie [overeenkomsten maken](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Pijplijnen (bruggen)
In de BizTalk Server EDI zijn pijplijnen bericht verwerking entiteiten die u kunnen ook aangepaste regels voor de van de specifieke verwerkingsmogelijkheden, zoals vereist door de toepassing hello opnemen. Hallo gelijkwaardige zou voor BizTalk Services een EDI-bridge. Maar in BizTalk Services op dit moment Hallo EDI bruggen 'gesloten'.  U kunt uw eigen aangepaste activiteiten tooan EDI-bridge dat wil zeggen, niet toevoegen. De aangepaste verwerking moet worden uitgevoerd buiten Hallo EDI bridge in uw toepassing voordat of nadat het Hallo-bericht Hallo bridge geconfigureerd als onderdeel van Hallo Trading Partner agreement invoert. EAI-bruggen hebben Hallo optie toodo aangepaste verwerking. Als u aangepaste verwerking wilt, kunt u EAI-bruggen voordat of nadat het Hallo-bericht is verwerkt door Hallo EDI bridge is ingesteld. Zie voor meer informatie [hoe tooInclude aangepaste Code in bruggen](https://msdn.microsoft.com/library/azure/dn232389.aspx).

U kunt een stroom publiceren/abonneren met aangepaste code en/of met behulp van Service Bus-wachtrijen en onderwerpen messaging voordat Hallo trading partner agreement Hallo-bericht ontvangt, of nadat Hallo overeenkomst Hallo-bericht verwerkt en stuurt deze tooa Service Bus-eindpunt kunt invoegen.

Zie **scenario's / berichtenstroom** in dit onderwerp voor Hallo-bericht stroom patroon.

## <a name="agreements"></a>Overeenkomsten
Als u bekend met Hallo die BizTalk Server 2010 handel Partner overeenkomsten gebruikt voor EDI verwerken bent, zijn BizTalk Services handelspartnerovereenkomsten zoekt bekend. De meeste instellingen zijn dezelfde Hallo Hallo-overeenkomst en gebruik Hallo dezelfde terminologie. Hallo instellingen van de overeenkomst in sommige gevallen zijn veel eenvoudiger vergeleken toohello dezelfde instellingen in BizTalk Server. Microsoft Azure BizTalk Services ondersteunt X12, EDIFACT en AS2-transport.

Microsoft Azure BizTalk Services biedt ook een **TPM gegevensmigratie** hulpprogramma toomigrate handelspartners en overeenkomsten uit BizTalk Server Trading Partner module tooBizTalk Services-Portal. Hallo TPM gegevens Migratiehulpmiddel is beschikbaar als onderdeel van een pakket hulpprogramma's, die kan worden gedownload vanaf Hallo [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). Hallo-pakket bevat ook een Leesmij-bestand dat vindt u instructies voor hoe toouse Hallo hulpprogramma en elementaire informatie over probleemoplossing voor Hallo hulpprogramma.

## <a name="schemas"></a>Schema 's
BizTalk Services biedt EDI-schema's die kunnen worden gebruikt in BizTalk Services-oplossingen.  BizTalk Server EDI-schema's kunnen bovendien ook worden gebruikt met BizTalk Services omdat hoofdknooppunt Hallo van Hallo EDI-schema hetzelfde voor BizTalk Server, evenals BizTalk Services is. U wordt dus worden kunnen toodirectly nemen uw BizTalk Server EDI-schema's en deze gebruiken in Hallo EDI-oplossingen die u ontwikkelt met behulp van BizTalk Services. U kunt ook Hallo schema's downloaden van Hallo [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Maps (transformaties)
Toewijzingen in BizTalk Server heten transformaties in BizTalk Services. Toewijzingen migreren van Services mogelijk een van de BizTalk Server-tooBizTalk Hallo complexere taken tooachieve (afhankelijk van de complexiteit van de kaart). Hallo toewijzing hulpprogramma dat wordt gebruikt voor BizTalk Services wijkt af van Hallo BizTalk toewijzen. Ook al lijkt Hallo mapper voornamelijk Hallo dezelfde, onderliggende toewijzingsindeling Hallo verschilt. Hallo functoids (aangeroepen **kaart Operations** in BizTalk Services) beschikbaar toohello gebruikers zijn ook verschillend.  In feite kan niet rechtstreeks u een BizTalk-kaart in BizTalk Services. Niet alle Hallo functoids in BizTalk Server beschikbaar zijn ook beschikbaar als de bewerkingen van de kaart in BizTalk Services.

### <a name="new-transform-operations"></a>Nieuwe transformatiebewerkingen
Tijdens het Hallo-lijst van de kaart transformatiebewerkingen beschikbaar lijkt heel anders dan Hallo BizTalk Server toewijzen, hebben transformeert van BizTalk Services nieuwe manieren voor het uitvoeren van dezelfde taken Hallo. BizTalk Services transformeert bijvoorbeeld **bewerkingen na opvragen** beschikbaar. Dit is niet beschikbaar in Hallo BizTalk toewijzen.  Hallo **bewerkingen na opvragen** kunt u toocreate en wordt uitgevoerd op een 'List', waarbij een lijst met een reeks items (ook wel bekend als ' rijen') en waarbij elk item kan meerdere leden (ook wel bekend als ' kolommen') hebben.  U kunt sorteren Hallo lijst items selecteren op basis van een voorwaarde, enzovoort.

Een ander voorbeeld van de nieuwe functionaliteit in BizTalk Services transformeert zijn Hallo **lus Operations**.  Het is moeilijk toocreate geneste lussen in Hallo BizTalk Server toewijzen.  Hallo lus kaart bewerkingen zijn dus toegevoegd voor Hallo BizTalk Services transformaties.

Nog een ander voorbeeld Hallo is **If vervolgens Else** expressie kaart bewerking.  Met een if-then-else bewerking is mogelijk in Hallo BizTalk toewijzen, maar het vereist dat meerdere functoids tooaccomplish schijnbaar eenvoudige taak.

### <a name="migrating-biztalk-server-maps"></a>Toegewezen BizTalk-Server migreren
Microsoft Azure BizTalk Services biedt dat een hulpprogramma toomigrate BizTalk Server toegewezen tooBizTalk Services transformaties. Hallo **BTMMigrationTool** is beschikbaar als onderdeel van Hallo **extra** pakket voorzien Hallo [BizTalk Services SDK downloaden](http://go.microsoft.com/fwlink/p/?LinkId=235057). Zie voor meer informatie over Hallo hulpprogramma [converteren van een BizTalk-kaart tooa BizTalk Services transformeren](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

U kunt ook zoeken op een voorbeeld van een door Sandro Pereira, MVP BizTalk, op hoe te[migreren BizTalk Server maps tooBizTalk Services transformaties](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Integraties
Als u BizTalk Server orchestration verwerking tooMicrosoft Azure toomigrate nodig hebt, moet Hallo integraties toobe herschreven omdat actieve BizTalk Server integraties biedt geen ondersteuning voor Microsoft Azure.  U kunt Hallo orchestration functies in een Windows Workflow Foundation 4.0 (WF4)-service kan herschrijven.  Dit is een volledig herschreven omdat er momenteel geen migratie van BizTalk Server integraties tooWF4. Hier volgen enkele resources voor Windows-werkstroom:

* [*Hoe toointegrate een werkstroom WCF-Service met Service Bus-wachtrijen en onderwerpen* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) door Paolo Salvatori. 
* [*Het bouwen van apps met Windows Workflow Foundation en Azure* sessie](http://go.microsoft.com/fwlink/p/?LinkId=237314) van Hallo Build 2011 vergaderruimte.
* [*Windows Workflow Foundation Developer Center* ](http://go.microsoft.com/fwlink/p/?LinkId=237315) op MSDN.
* [*Documentatie van Windows Workflow Foundation 4 (WF4)* ](https://msdn.microsoft.com/library/dd489441.aspx) op MSDN.

## <a name="other-considerations"></a>Andere overwegingen
Hieronder volgen enkele overwegingen die u aanbrengen moet tijdens het gebruik van BizTalk Services.

### <a name="fallback-agreements"></a>Alternatieve overeenkomsten
BizTalk Server EDI-bewerking heeft Hallo concept van 'Terugval overeenkomsten'.  BizTalk Services biedt **niet** een concept terugval overeenkomst tot nu toe hebben.  Zie BizTalk documentatie onderwerpen [Hallo rol overeenkomsten bij het verwerken van EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) en [terugval overeenkomst eigenschappen of configureren van algemene](https://msdn.microsoft.com/library/bb245981.aspx) voor meer informatie over hoe terugval overeenkomsten worden gebruikt in BizTalk -Server.

### <a name="routing-toomultiple-destinations"></a>Routering toomultiple bestemmingen
BizTalk Services bruggen, in de huidige status biedt geen ondersteuning voor routering berichten toomultiple bestemmingen met behulp van een publiceren-abonneren model. In plaats daarvan kunt u berichten van een BizTalk Services bridge tooa Service Bus-onderwerp, dat kan meerdere abonnementen tooreceive Hallo-bericht klikt u vervolgens op meer dan één eindpunt hebben versturen.

## <a name="conclusion"></a>Conclusie
Microsoft Azure BizTalk Services is bijgewerkt op reguliere mijlpalen tooadd meer functies en mogelijkheden. Bij elke update hopen wij toosupporting verhoogd functionaliteit toofacilitate end-to-end-oplossingen met behulp van BizTalk Services en andere technologieën voor Azure maken.

## <a name="see-also"></a>Zie ook
[Ontwikkelen van toepassingen met Azure Enterprise](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
