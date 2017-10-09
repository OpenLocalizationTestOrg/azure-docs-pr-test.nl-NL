---
title: aaaData classificatie voor Azure | Microsoft Docs
description: In dit artikel biedt een inleiding toohello grondbeginselen van gegevensclassificatie en markeert de waarde in het bijzonder in Hallo context van de cloud computing en het gebruik van Microsoft Azure
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Gegevensclassificatie voor Azure
In dit artikel biedt een inleiding toohello grondbeginselen van gegevensclassificatie en markeert u de waarde in het bijzonder in Hallo context van de cloud computing en het gebruik van Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Grondbeginselen van gegevens classificatie
Geslaagde gegevensclassificatie in een organisatie vereist uitgebreide kennis van de behoeften van uw organisatie en een goed begrip van waar de activa van uw gegevens zich bevinden.  

Gegevens aanwezig in een van drie basic statussen: 

* In rust 
* In proces 
* Onderweg 

Alle drie statussen unieke technische oplossingen voor gegevensclassificatie vereist, maar hello toegepaste beginselen gegevensclassificatie moet worden Hallo dezelfde voor elk. Gegevens die wordt geclassificeerd als vertrouwelijk moeten toostay vertrouwelijk wanneer ze zijn opgeslagen, in proces en bij verzending. 

Gegevens kunnen ook worden gestructureerde of ongestructureerde. Typische processen voor Hallo gestructureerde gegevens gevonden in de databases en spreadsheets minder complexe en tijdrovende toomanage dan die voor ongestructureerde gegevens, zoals documenten, broncode en e-mailadres zijn. 

> [!TIP]
> Lees voor meer informatie over de mogelijkheden van Azure en best practices voor gegevensversleuteling [Azure Data Encryption Best Practices](azure-security-data-encryption-best-practices.md)
> 
> 

In het algemeen organisaties hebben meer niet-gestructureerde gegevens dan gestructureerde gegevens. Ongeacht of gegevens gestructureerde of ongestructureerde is, is het belangrijk voor u toomanage gegevens gevoeligheid. Wanneer de juiste wijze wordt geïmplementeerd, helpt gegevensclassificatie activa worden beheerd met toezicht is groter dan de gegevensassets die worden beschouwd als openbare of gratis toodistribute gevoelige of vertrouwelijke gegevens. 

### <a name="controlling-access-toodata"></a>Toegang toodata beheren
Verificatie en autorisatie worden vaak verward met elkaar en hun rollen verkeerd begrepen. In werkelijkheid zijn ze heel anders, zoals wordt weergegeven in de volgende afbeelding Hallo.  

![Toegang tot gegevens en beheer](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Authentication
Verificatie bestaat gewoonlijk uit ten minste twee delen: een gebruikersnaam of het gebruikers-ID tooidentify een gebruiker en een token, zoals een wachtwoord, tooconfirm die Hallo gebruikersnaam referentie geldig is. Hallo-proces biedt geen Hallo geverifieerde gebruiker met toegang tooany items of services; Er wordt gecontroleerd dat die gebruiker Hallo is wie hij of zij beweren te zijn.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) identiteit cloud-gebaseerde services die u tooauthenticate toestaan en autoriseren van gebruikers. 
> 
> 

### <a name="authorization"></a>Autorisatie
Autorisatie is Hallo proces van het bieden van een geverifieerde gebruiker Hallo mogelijkheid tooaccess een toepassing, gegevensset, bestand of een ander object. Geverifieerde gebruikers Hallo rechten toouse toewijzen wijzigen of verwijderen van items die toegang te krijgen tot aandacht toodata classificatie vereist. 

Geslaagde autorisatie vereist de implementatie van een mechanisme toovalidate afzonderlijke gebruikers moet tooaccess bestanden en gegevens die zijn gebaseerd op een combinatie van functies, beveiligingsbeleid en overwegingen bij het beleid van de risico's. Bijvoorbeeld: gegevens van specifieke line-of-business (LOB)-toepassingen mogelijk geen rekening hoeven toobe toegankelijk is voor alle werknemers en slechts een kleine subset van werknemers waarschijnlijk moet toegang hebben tot toohuman resources (uur)-bestanden. Maar voor organisaties toocontrol wie toegang heeft tot gegevens, zoals alsmede wanneer en hoe, een doeltreffend systeem voor het verifiëren van gebruikers voldaan worden moet. 

> [!TIP]
> Controleer in Microsoft Azure ervoor tooleverage gebaseerd toegangsbeheer (RBAC) toogrant alleen Hallo mate van toegang dat gebruikers tooperform hun werk moeten. Lees [rol toewijzingen toomanage toegang tooyour Azure Active Directory-bronnen gebruiken](../active-directory/role-based-access-control-configure.md) voor meer informatie. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Rollen en verantwoordelijkheden in cloud computing
Hoewel cloudproviders kunt risico's beheren, die klanten nodig tooensure die gegevens Classificatiebeheer en afdwingen voor de juiste wijze wordt geïmplementeerd Hallo tooprovide passend niveau van data management-services.  

Gegevensclassificatie verantwoordelijkheden varieert op basis van het welke cloud-servicemodel geïmplementeerd is, zoals wordt weergegeven in de volgende afbeelding Hallo. Hallo drie primaire cloud servicemodellen zijn infrastructuur als een dienst (IaaS), platform als een service (PaaS), en software als een service (SaaS). Implementatie van de gegevens classificatie mechanismen ook variëren, afhankelijk van Hallo de afhankelijkheid van en de verwachtingen van Hallo cloudprovider. 

![Rollen](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Hoewel u zelf verantwoordelijk bent voor het classificeren van uw gegevens, moeten cloudproviders geschreven verbintenissen over hoe ze wordt beveiligd en onderhouden van Hallo privacy van klantgegevens Hallo opgeslagen in de cloud maken.  

* **IaaS providers** vereisten zijn beperkt tooensuring die virtuele omgeving Hallo aankan mogelijkheden voor classificatie van gegevens en nalevingsvereisten van de klant. IaaS providers hebben een kleinere rol in gegevensclassificatie omdat ze alleen tooensure dat klantgegevens nalevingsvereisten adressen nodig. Providers moet echter nog steeds dat hun virtuele omgevingen ingaat op de classificatievereisten gegevens in de toevoeging toosecuring hun datacenters.
* **PaaS-providers** verantwoordelijkheden mogen worden vermengd omdat Hallo platform kan worden gebruikt in een gelaagde benadering tooprovide beveiliging voor een classificatie-hulpprogramma. PaaS-providers mogelijk die verantwoordelijk is voor verificatie en mogelijk enkele autorisatieregels en beveiliging en classificatie mogelijkheden tootheir toepassing gegevenslaag moeten opgeven. Veel zoals IaaS-providers moeten PaaS-providers tooensure die hun platform voldoet aan alle vereisten van de classificatie relevante gegevens.
* **Aanbieders van SaaS** vaak worden beschouwd als onderdeel van een autorisatieketen, en wordt moet tooensure die gegevens die zijn opgeslagen in de SaaS-toepassing hello Hallo kan worden beheerd door het type van de classificatie. SaaS-toepassingen kunnen worden gebruikt voor LOB-toepassingen en door hun aard tooprovide moet Hallo betekent tooauthenticate en autoriseren van gegevens die wordt gebruikt en worden opgeslagen. 

## <a name="classification-process"></a>Classificatieproces
Veel organisaties die Hallo begrijpen moet voor gegevensclassificatie en wilt hebben uit te maken op een basic uitdaging tooimplement: waar toobegin?

Een effectieve en eenvoudige manier tooimplement gegevensclassificatie toouse Hallo PLAN is, doet, controle, ACT model van [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). Hallo volgende figuur grafieken Hallo-taken die vereist toosuccessfully implementeren gegevensclassificatie in dit model zijn.  

1. **PLAN**. Identificeren van gegevensassets, een gegevens vallen toodeploy Hallo classificatie programma en ontwikkelen van profielen voor beveiliging. 
2. **VOER**. Nadat gegevens classificatiebeleidsregels zijn gegaan, Hallo programma implementeren en afdwingen technologieën implementeren naar behoefte voor vertrouwelijke gegevens.  
3. **CONTROLEER**. Controleer en tooensure die Hallo hulpprogramma's en methoden wordt effectief adresseert Hallo classificatiebeleidsregels rapporten te valideren. 
4. **ACT**. Hallo-status van de toegang tot gegevens bekijken en controleren van bestanden en gegevens die nodig hebt met een nieuwe classificatie en revisie methodologie tooadopt wijzigingen en nieuwe risico's tooaddress revisie.  

![Plan,, controleren, fungeren](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Selecteer een model terminologie die zijn gericht op de behoeften van uw
Verschillende soorten processen bestaan voor het classificeren van gegevens, inclusief handmatige processen, op basis van locatie processen die gegevens op basis van locatie van een gebruiker of systeem, op basis van een toepassing processen zoals database-specifieke classificatie en geautomatiseerde classificeren processen die worden gebruikt door verschillende technologieën, waarvan sommige in Hallo 'Vertrouwelijke gegevens beveiligt' sectie verderop in dit artikel worden beschreven.  

Dit artikel bevat twee algemene terminologie modellen die zijn gebaseerd op modellen goed gebruikt en bedrijfstak in acht genomen. Deze modellen terminologie die drie niveaus van classificatie gevoeligheid opgeeft, worden weergegeven in de volgende tabel Hallo.  

> [!NOTE]
> Wanneer een bestand of bron dat gegevens die doorgaans zou worden geclassificeerd op verschillende niveaus, Hallo hoogste niveau van classificatie aanwezig zijn vastgesteld combineert algehele classificatie Hallo classificeren. Bijvoorbeeld, een bestand met gevoelige en beperkte gegevens moet worden ingedeeld als beperkt.  
> 
> 

| **Gevoeligheid** | **Terminologie model 1** | **Terminologie model 2** |
| --- | --- | --- |
| Hoog |Vertrouwelijk |Beperkt |
| Middelgroot |Alleen voor intern gebruik |Gevoelige |
| Laag |Openbaar |Onbeperkte |

#### <a name="confidential-restricted"></a>Vertrouwelijk (beperkt)
Informatie die is geclassificeerd als vertrouwelijk of beperkte bevat gegevens die worden kunnen onherstelbare tooone of meer personen en/of organisaties als geknoeid of verloren. Dergelijke informatie wordt vaak op basis van de 'nodig tooknow' verstrekt en kan onder andere: 

* Persoonlijke gegevens, inclusief persoonlijke gegevens zoals Social Security of nationale identificatienummers passport getallen, creditcardnummers, van stuurprogramma licentie getallen, medische gegevens en health insurance beleid voor id-nummers.  
* Financiële records, met inbegrip van financiële rekeningnummers, zoals het controleren of de rekeningnummers investering. 
* Zakelijke gegevens, zoals documenten of gegevens die zijn unieke of specifieke intellectueel eigendom.  
* Juridische gegevens, inclusief potentiële advocaat bevoegdheden materiaal. 
* Verificatiegegevens, met inbegrip van persoonlijke cryptografiesleutels, gebruikersnaam wachtwoord paren of andere reeksen identificatie zoals persoonlijke biometrische sleutelbestanden. 

Gegevens die wordt ingedeeld als vertrouwelijk vaak heeft regelgeving en nalevingsvereisten voor de verwerking van gegevens. 

#### <a name="for-internal-use-only-sensitive"></a>Voor intern gebruik alleen (gevoelig)
Informatie die wordt ingedeeld als van Gemiddeld Gevoeligheid bevat bestanden en gegevens die geen ernstige gevolgen voor een persoon of organisatie bij verlies of vernietigd. Deze gegevens zijn onder andere: 

* E-mailadres waarmee de meeste worden verwijderd of worden verdeeld zonder dat een crisis (met uitzondering van postvakken of e-mailadres van de personen die worden geïdentificeerd in Hallo vertrouwelijke classificatie).  
* Documenten en bestanden die geen vertrouwelijke gegevens bevatten.

Deze categorie omvat in het algemeen alles wat niet vertrouwelijk is. Deze classificatie kan de meeste zakelijke gegevens bevatten, omdat de meeste bestanden die worden beheerd of dagelijkse gebruikt kunnen worden geclassificeerd als gevoelig. Hallo, met uitzondering van gegevens die openbaar wordt gemaakt of vertrouwelijke kunnen alle gegevens binnen de organisatie van een zakelijke worden geclassificeerd als vertrouwelijk standaard. 

#### <a name="public-unrestricted"></a>Openbaar (onbeperkte)
Informatie die wordt ingedeeld als openbaar omvat gegevens en bestanden die niet essentieel toobusiness behoeften of bewerkingen. Deze classificatie kan ook gegevens die opzettelijk uitgebrachte toohello openbare voor hun gebruik is, zoals aankondigingen van materiaal of druk op marketing bevatten. Deze classificatie kan bovendien gegevens zoals e-mailberichten spam opgeslagen door een e-mailservice bevatten. 

### <a name="define-data-ownership"></a>Gegevenseigendom definiëren
Het is belangrijk tooestablish een duidelijke custodial keten van eigendom van alle gegevensassets. Hallo volgende tabel bevat verschillende gegevens eigendom rollen in gegevens classificatie inspanningen en hun respectieve rechten.  

| **Rol** | **Maken** | **Wijzigen en verwijderen** | **Gemachtigde** | **Lezen** | **Archief maken en terugzetten** |
| --- | --- | --- | --- | --- | --- |
| Eigenaar |X |X |X |X |X |
| Vallen | | |X | | |
| Beheerder | | | | |X |
| Gebruiker\* | |X | |X | |

**Gebruikers kunnen worden verleend aanvullende rechten zoals bewerken en verwijderen door vallen* 

> [!NOTE]
> Deze tabel biedt een uitgebreide lijst met functies en rechten, maar alleen een representatieve steekproef geen. 
> 
> 

Hallo **activumeigenaar gegevens** Hallo oorspronkelijke maker van Hallo-gegevens die kunnen overdragen en vallen toewijzen. Wanneer een bestand is gemaakt, moet de eigenaar van de Hallo kunnen tooassign een classificatie, betekent dat ze hebben een toounderstand verantwoordelijkheid wat toobe geclassificeerd als vertrouwelijk moet op basis van de beleidsregels van hun organisatie. Alle gegevens van een gegevens-activumeigenaar kan automatisch worden geclassificeerd als voor intern gebruik alleen (gevoelig) worden tenzij ze verantwoordelijk zijn voor die eigenaar of vertrouwelijk (beperkt) gegevenstypen maken. Rol van eigenaar Hallo wordt vaak niet wijzigen nadat het Hallo-gegevens worden geclassificeerd. Hallo eigenaar mogelijk bijvoorbeeld een database van geclassificeerde gegevens maken en hun rechten toohello gegevens vallen afstaat.  

> [!NOTE]
> eigenaren van asset gebruik vaak een combinatie van services, apparaten en media, sommige hiervan zijn persoonlijke en sommige van deze organisatie toohello behoren. Schakel organisatiebeleid kan ervoor te zorgen dat informatie over het gebruik van apparaten zoals laptops en smart-apparaten in overeenstemming met gegevens classificatie richtlijnen.  
> 
> 

Hallo **gegevens asset vallen** wordt toegewezen door activumeigenaar hello (of hun gemachtigde) toomanage Hallo asset volgens tooagreements met Hallo activumeigenaar of volgens de vereisten van toepassing. Hallo beheerder rol kan in het ideale geval worden geïmplementeerd in een geautomatiseerd systeem. Een asset vallen zorgt ervoor dat noodzakelijk toegangsbeheer worden geleverd en is verantwoordelijk voor het beheren van tootheir voorzichtig beschermen van bedrijfsmiddelen die worden overgedragen. Hallo-verantwoordelijkheden van Hallo asset vallen kunnen omvatten:  

* Hallo asset in overeenstemming met Hallo asset eigenaar richting of in overeenstemming met de Hallo activumeigenaar beveiligen 
* Ervoor te zorgen dat de classificatiebeleidsregels wordt voldaan 
* Tooagreed asset eigenaren van een mededeling wordt gewijzigd-na-besturingselementen en/of beveiliging procedures voorafgaande toothose wijzigingen die van kracht 
* Reporting toohello activumeigenaar over wijzigingen tooor verwijdering van Hallo asset vallen verantwoordelijkheden 
* Een **beheerder** vertegenwoordigt een gebruiker die verantwoordelijk is voor gezorgd dat de integriteit, maar ze niet een asset gegevenseigenaar, vallen of gebruiker zijn. In feite bieden veel beheerdersrollen gegevens container management services zonder de toegang tot toohello gegevens. Hallo beheerdersrol omvat back-up en herstel van Hallo gegevens, records van Hallo activa, onderhouden en te kiezen, ophalen en werken met Hallo apparaten en opslag die house Hallo activa. 
* Hallo asset gebruiker omvat iedereen toegang toodata of een bestand wordt verleend. Toegang tot de toewijzing is vaak overgedragen door Hallo eigenaar toohello asset vallen.  

### <a name="implementation"></a>Implementatie
Overwegingen met betrekking tot tooall classificatie methoden van toepassing. Deze overwegingen moeten tooinclude meer informatie over wie, wat, waar en wanneer en waarom een gegevensasset zou worden gebruikt, geopend, gewijzigd of verwijderd. Alle asset management moet worden uitgevoerd met een goed begrip van hoe een organisatie de risico's bekijkt, maar een eenvoudige methode kan worden toegepast zoals gedefinieerd in Hallo gegevens classificatie processen. Aanvullende overwegingen voor gegevensclassificatie omvatten Hallo introductie van nieuwe toepassingen en hulpprogramma's en wijzigingen beheren nadat een classificatiemethode is geïmplementeerd.  

### <a name="reclassification"></a>Opnieuw indelen
Herindelen of Hallo classificatie status van een gegevensasset te wijzigen moet toobe uitgevoerd als een gebruiker of systeem dat Hallo gegevensasset belang bepaalt of risicoprofiel is gewijzigd. Deze inspanningen is belangrijk om ervoor te zorgen dat Hallo classificatie status toobe huidige blijft en geldig. De meeste inhoud die niet handmatig is geclassificeerd kan automatisch worden geclassificeerd of op basis van gebruik door een beheerder van de gegevens of de eigenaar van gegevens. 

### <a name="manual-data-reclassification"></a>Gegevens handmatig opnieuw indelen
Deze inspanningen zou in het ideale geval ervoor zorgen dat Hallo details van een wijziging vastgelegd en gecontroleerd. Omwille van de gevoeligheid, of voor registratie in papierformaat, of een vereiste tooreview-gegevens die oorspronkelijk verkeerd is geclassificeerd, zou de meest waarschijnlijke reden voor het handmatige herindelen Hallo zijn. Omdat dit artikel gegevensclassificatie en zwevend gegevens toohello cloud acht, handmatige nieuwe classificatie inspanningen aandacht op per geval zou vereisen en een risico Beheercontrole niet ideaal tooaddress classificatievereisten. Dergelijke waarmee wordt geprobeerd zou in het algemeen Houd rekening met het beleid van de organisatie van de Hallo over wat er toobe geclassificeerd moet, Hallo standaardstatus van classificatie (alle gegevens en worden gevoelige maar geen vertrouwelijke bestanden) en uitzonderingen voor met een hoog risico gegevens nemen. 

### <a name="automatic-data-reclassification"></a>Automatische gegevens opnieuw indelen
Hallo dezelfde algemene regel opnieuw indelen van gegevens automatisch kunnen worden gebruikt als handmatige classificatie. Hallo-uitzondering is dat geautomatiseerde oplossingen ervoor te zorgen dat de regels worden gevolgd en toegepast zoals die nodig zijn. Gegevensclassificatie kan worden uitgevoerd als onderdeel van een afdwingen van beleid voor gegevensclassificatie, die kan worden afgedwongen wanneer gegevens worden opgeslagen in gebruik en in overdracht met behulp van technologie voor autorisatie.

* Op basis van toepassing. Met behulp van bepaalde toepassingen standaard stelt een classificatieniveau. Bijvoorbeeld: gegevens van de software customer relationship management (CRM), HR en health record beheerhulpprogramma's standaard vertrouwelijk is. 
* Op basis van locatie. Locatie van gegevens identificeren gevoeligheid van gegevens. Gegevens die zijn opgeslagen door een HR of financiële afdeling is bijvoorbeeld waarschijnlijker toobe vertrouwelijke aard.  

### <a name="data-retention-recovery-and-disposal"></a>Bewaren van gegevens, herstel en verwijdering
Herstel van gegevens en -verwijdering, zoals nieuwe classificatie gegevens, is een essentieel aspect van het beheer van gegevensassets. Hallo principes voor gegevensherstel en buitengebruikstelling zou worden gedefinieerd door een bewaarbeleid voor gegevens en afgedwongen op Hallo dezelfde manier als de gegevens opnieuw indelen; een dergelijke inspanning zou worden uitgevoerd door Hallo vallen en beheerdersrollen als een gezamenlijke taak.  

Fout toohave een bewaarbeleid voor gegevens kan betekenen verlies of fout toocomply met detectie van regelgeving en wettelijke vereisten. De meeste organisaties waarvoor geen een bewaarbeleid voor duidelijk gedefinieerde gegevens vaak toouse een bewaarbeleid standaard 'Alles behouden'. Een bewaarbeleid heeft echter extra risico's in de cloud services-scenario's. 

Een bewaarbeleid voor gegevens voor cloudserviceproviders kan bijvoorbeeld worden beschouwd als 'hello duur van het abonnement Hallo' (zo lang Hallo-service wordt betaald voor Hallo gegevens behouden blijven). Bedrijfs- of regelgeving bewaarbeleid kan niet omgaan met die een overeenkomst voor betalen voor bewaren. De definitie van een beleid voor vertrouwelijke gegevens kunt controleren of gegevens worden opgeslagen en is verwijderd op basis van best practices. Een beleid voor archivering kan bovendien de gemaakt tooformalize kennis over welke gegevens moet worden verwijderd en wanneer. 

Bewaarbeleid voor gegevens dient te houden Hallo vereist regelgeving en nalevingsvereisten, evenals zakelijke wettelijke bewaarplicht. Geclassificeerde gegevens mogelijk leiden tot vragen over de duur van de retentie en uitzonderingen voor gegevens die zijn opgeslagen met een provider; deze vragen zijn geneigd voor gegevens die niet correct zijn geclassificeerd. 

> [!TIP]
> meer informatie over Azure-bewaarbeleid voor gegevens en meer Hallo [Microsoft Online Subscription overeenkomst](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Beveiligen van vertrouwelijke gegevens
Nadat de gegevens worden geclassificeerd, wordt zoeken en implementeren van manieren tooprotect vertrouwelijke gegevens een integraal onderdeel van een strategie voor gegevensbescherming implementatie. Beveiligen van vertrouwelijke gegevens, moet extra aandacht toohow gegevens worden opgeslagen en verzonden in conventionele architecturen ook als in de cloud Hallo. 

Deze sectie bevat algemene informatie over een aantal technologieën die afdwinging inspanningen kunt automatiseren toohelp gegevens beveiligen die als vertrouwelijk zijn geclassificeerd. 

Als Hallo volgende afbeelding ziet, kunnen deze technologieën als on-premises of cloud gebaseerde oplossingen worden geïmplementeerd, of in een hybride wijze, met enkele van deze geïmplementeerde lokale en sommige in Hallo cloud. (Bij sommige technologieën, zoals versleuteling en rechtenbeheer, ook uitbreiden toouser apparaten.)  

![Technologieën](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Rights management-software
Een oplossing voor het voorkomen van gegevensverlies is software voor beheer van rechten. In tegenstelling tot benaderingen waarbij wordt geprobeerd toointerrupt Hallo stroom van gegevens op afsluiten punten in een organisatie, werkt rights management-software op grondige niveaus binnen gegevens opslagtechnologieën. Documenten worden versleuteld en controle over die kunnen worden gedecodeerd toegangsbeheer die zijn gedefinieerd in een oplossing voor het beheer van verificatie zoals Active Directory gebruikt.  

> [!TIP]
> u kunt Azure Rights Management (Azure RMS) gebruiken als Hallo information protection oplossing tooprotect gegevens in verschillende scenario's. Lees [wat is Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) voor meer informatie over deze oplossing met Azure.
> 
> 

Hallo voordelen van software voor beheer van rechten onder andere: 

* Beveiligde gevoelige informatie. Gebruikers kunnen hun gegevens direct met rights management-toepassingen beveiligen. Er zijn geen extra stappen vereist: documenten ontwerpen, verzenden van e-mail en gegevens publiceren een consistente gegevens protection-ervaring bieden. 
* Beveiliging met Hallo gegevens wordt verzonden. Klanten blijven controle over wie toegang tot tootheir gegevens heeft in de cloud hello, bestaande IT-infrastructuur, of op het bureaublad van de gebruiker Hallo. Organisaties kunnen tooencrypt hun gegevens te selecteren en beperken van toegang op basis van tootheir zakelijke vereisten. 
* Standaardbeleidsregels voor gegevensbeveiliging. Beheerders en gebruikers kunnen standaard beleidsregels gebruiken voor algemene zakelijke scenario's, zoals ' Bedrijf vertrouwelijk – alleen-lezen' en "Niet doorsturen." Een uitgebreide set van gebruiksrechten zoals lezen, kopiëren, afdrukken, opslaan, bewerken en voorwaarts tooallow flexibiliteit bij het definiëren van aangepaste gebruiksrechten worden ondersteund. 

> [!TIP]
> u kunt gegevens in Azure Storage beveiligen met behulp van [Azure Storage-Service: versleuteling](../storage/storage-service-encryption.md) voor gegevens in rust. U kunt ook [Azure Disk Encryption](azure-security-disk-encryption.md) toohelp beveiligen gegevens op virtuele schijven die voor Azure Virtual Machines gebruikt.
> 
> 

### <a name="encryption-gateways"></a>Versleuteling gateways
Versleuteling gateways werken in hun eigen lagen tooprovide versleuteling services door het omleiden van de gegevens voor alle toocloud op basis van toegang. Deze aanpak moet niet verwarren met die van een virtueel particulier netwerk (VPN). Versleuteling gateways zijn ontworpen tooprovide een transparante laag toocloud-oplossingen.   

Gateways voor de versleuteling kunnen bieden een manier toomanage en de beveiligde gegevens waarvan als vertrouwelijk zijn geclassificeerd door Hallo gegevens onderweg evenals gegevens in rust te versleutelen.  

Versleuteling gateways worden geplaatst in de gegevensstroom Hallo tussen apparaten van gebruikers en toepassing datacenters tooprovide tokenversleuteling /-ontsleuteling services. Deze oplossingen, zoals VPN-verbindingen, zijn voornamelijk oplossingen on-premises. Ze zijn ontworpen tooprovide een derde partij controle over versleutelingssleutels, waarmee Hallo risico's van zowel Hallo gegevens en sleutelbeheer met één provider brengen te beperken. Dergelijke oplossingen zijn ontworpen, net als versleuteling, toowork naadloos en transparant tussen gebruikers en het Hallo-service. 

> [!TIP]
> u kunt Azure ExpressRoute tooextend uw on-premises netwerken in Hallo Microsoft cloud via een speciale persoonlijke verbinding. Lees [technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) voor meer informatie over deze mogelijkheid. Andere opties voor cross-premises-connectiviteit tussen uw on-premises netwerk en [Azure is een site-naar-site VPN-](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Preventie van gegevensverlies
Verlies van gegevens (soms waarnaar wordt verwezen tooas gegevenslekken) is een belangrijk aandachtspunt en Hallo preventie van gegevensverlies externe gegevens via schadelijke en onbedoeld insiders is vooral gekeken naar voor veel organisaties.  

Gegevens gegevensverlies voorkomen (DLP)-technologieën kunt ervoor te zorgen dat oplossingen zoals e-mail services niets verzenden gegevens die als vertrouwelijk zijn geclassificeerd. Organisaties kunnen profiteren van DLP-functies in bestaande producten toohelp gegevensverlies voorkomen. Dergelijke functies beleid die eenvoudig kunnen worden gemaakt vanaf het begin of met behulp van een sjabloon die wordt geleverd door de softwareleverancier hello gebruiken.  

DLP-technologieën kunnen grondige Inhoudsanalyse basis van overeenkomende sleutelwoorden, woordenboeken, evaluatie van reguliere expressies en andere inhoud onderzoek toodetect inhoud die in strijd met DLP organisatiebeleid uitvoeren. Bijvoorbeeld, kunt DLP Hallo verlies van Hallo volgende soorten gegevens te voorkomen: 

* Social Security en nationale ID-nummers 
* Bankgegevens 
* Creditcardnummers  
* IP-adressen 

Bij sommige technologieën DLP bieden ook Hallo mogelijkheid toooverride Hallo DLP-configuratie (bijvoorbeeld als een organisatie tootransmit sociaal-fiscaal nummer informatie tooa salarissen processor moet). Bovendien is het mogelijk tooconfigure DLP zodat gebruikers worden gewaarschuwd voordat ze zelfs toosend vertrouwelijke informatie die niet moet worden verzonden. 

> [!TIP]
> u kunt Office 365 DLP mogelijkheden tooprotect uw documenten te gebruiken. Lees [besturingselementen voor Office 365-naleving: preventie van gegevensverlies](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) voor meer informatie.
> 
> 

## <a name="see-also"></a>Zie ook
* [Azure Data Encryption Best Practices](azure-security-data-encryption-best-practices.md)
* [Azure voor identiteits- en toegang beheren best practices voor beveiliging](azure-security-identity-management-best-practices.md)
* [Blog van het Azure-beveiligingsteam](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

