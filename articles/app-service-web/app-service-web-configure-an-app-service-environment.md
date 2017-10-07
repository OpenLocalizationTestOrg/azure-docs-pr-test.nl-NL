---
title: aaaHow tooConfigure een App Service-omgeving v1
description: Configuratie, beheer en bewaking van App Service-omgeving v1 Hallo
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Configureren van een App Service-omgeving v1

> [!NOTE]
> In dit artikel gaat over het Hallo v1 App Service-omgeving.  Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Overzicht
Op hoog niveau, wordt een Azure App Service-omgeving bestaat uit diverse belangrijke onderdelen:

* De rekenresources die worden uitgevoerd in App Service-omgeving Hallo gehoste service
* Storage
* Een database
* Een virtueel netwerk Classic(V1) of Resource Manager(V2) Azure (VNet) 
* Een subnet met Hallo App Service-omgeving gehoste service wordt uitgevoerd op het

### <a name="compute-resources"></a>Bronnen berekenen
U rekenresources hello gebruiken voor uw vier resourcegroepen.  Elke as-omgeving (App Service omgeving) heeft een set van front-ends en drie mogelijke werknemersgroepen. U hoeft niet toouse alle drie werknemersgroepen--als u wilt, kunt u alleen gebruiken een of twee.

Hallo-hosts in Hallo resourcegroepen (front-ends en werknemers) zijn niet rechtstreeks toegankelijk tootenants. U kan geen Remote Desktop Protocol (RDP) tooconnect toothem gebruiken, wijzigen de inrichtingen of fungeren als een beheerder op deze.

U kunt resource pool hoeveelheid en grootte instellen. In een as-omgeving hebt u vier grootteopties, die zijn gelabeld P1 via P4. Zie voor meer informatie over deze grootten en de prijscategorie [App Service-prijzen](../app-service/app-service-value-prop-what-is.md).
Hallo hoeveelheid of grootte wijzigen wordt een schaalaanpassing genoemd.  Slechts één schaalaanpassing kan worden uitgevoerd op een tijdstip.

**FrontPage-ends**: Hallo-front-ends zijn Hallo HTTP/HTTPS-eindpunten voor de apps die zijn ondergebracht in uw as-omgeving. U uitvoeren niet werkbelastingen in Hallo-front-ends.

* Een as-omgeving begint met twee P2s die voldoende is voor ontwikkel-/ testwerkbelastingen en op laag niveau productie-workloads. Wij raden P3s voor gemiddeld tooheavy productie-workloads.
* Voor productieworkloads gemiddeld tooheavy, is het raadzaam dat u hebt ten minste vier P3s tooensure er zijn onvoldoende front-ends gepland onderhoud plaatsvindt. Gepland onderhoudsactiviteiten verschijnt omlaag één front-end tegelijk. Hierdoor worden de algemene beschikbare front-capaciteit tijdens onderhoudsactiviteiten.
* Front-ends kunnen tooprovision van tooan uur duren. 
* Voor verdere schaal aan te passen, moet u Hallo CPU-percentage, geheugenpercentage en actieve aanvragen metrische gegevens voor de front-Hallo-toepassingen bewaken. Als de CPU of geheugen percentages Hallo dan 70 procent zijn wanneer P3s wordt uitgevoerd, voegt u meer front-ends. Als het gemiddelde van Hallo actieve aanvragen waarde uit too15, 000 too20, 000 aanvragen per front-end, moet u ook meer front-ends toevoegen. Hallo is algemene doelstelling tookeep CPU en geheugen percentages minder dan 70% en actieve aanvragen gemiddelde uit toobelow 15.000 aanvragen per front-end wanneer u P3s uitvoert.  

**Werknemers**: Hallo werknemers zijn waar uw apps daadwerkelijk worden uitgevoerd. Wanneer u opschalen uw App Service-plannen, maakt gebruik van werknemers in Hallo werknemersgroep die zijn gekoppeld.

* U kunt geen werknemers onmiddellijk toevoegen. Ze kunnen tooprovision van tooan uur duren.
* Hallo-grootte van een berekeningsresource voor elke groep schalen duurt < 1 uur per updatedomein. Er zijn 20 update domeinen in een as-omgeving. Als u Hallo compute grootte van een werknemersgroep met 10 exemplaren uitgebreide, kan het toocomplete van too10 uren duren.
* Als u Hallo formaat Hallo rekenresources die worden gebruikt in een werknemersgroep wijzigt, wordt u koude startprocedures van Hallo-apps die worden uitgevoerd in die worker-groep.

de snelste manier Hallo toochange Hallo compute resourcegrootte van een worker-groep die alle apps niet actief is:

* Aantal werknemers too2 Hallo terugschroeven.  Hallo minimale schalen omlaag grootte in de portal Hallo is 2. Het duurt enkele minuten toodeallocate uw exemplaren. 
* Selecteer Hallo nieuwe compute-grootte en het aantal exemplaren. Hier wordt het toocomplete van too2 uren duren.

Als uw apps een groter formaat van de compute-resource vereist, kan niet u profiteren van de vorige Hallo-richtlijnen. U kunt in plaats van Hallo grootte wijzigen van Hallo worker-groep die fungeert als voor deze apps host, een andere worker-groep met werknemers met een grootte van de gewenste Hallo vullen en uw apps via toothat van toepassingen verplaatsen.

* Hallo extra exemplaren van Hallo nodig compute grootte in een andere worker-groep maken. Dit duurt up tooan uur toocomplete.
* Uw App Service-abonnementen die als host Hallo-apps die een grotere grootte toohello zojuist geconfigureerd werknemersgroep toewijzen. Dit is een snelle bewerking moet kleiner zijn dan een minuut toocomplete nemen.  
* De eerste werknemersgroep Hallo terugschroeven als u niet meer nodig hebt die ongebruikte exemplaren. Deze bewerking duurt een paar minuten toocomplete.

**Automatisch schalen**: een Hallo-hulpprogramma's waarmee u kunt toomanage uw compute-brongebruik wordt geschaald. U kunt automatisch schalen voor front-end- of worker-groepen. U kunt doen zoals verhoging van uw exemplaren van elk type groep in de ochtend Hallo en kleiner Hallo buiten kantooruren. Of misschien kunt u instanties toevoegen wanneer het aantal werknemers die beschikbaar in een werknemersgroep zijn Hallo onder een bepaalde drempelwaarde komt zakt.

Als u tooset automatisch schalen regels rond compute resource pool metrische gegevens wilt en houd in gedachten Hallo tijd die wordt ingericht vereist. Zie voor meer informatie over automatisch schalen App Service-omgevingen [hoe tooconfigure automatisch schalen in een App-serviceomgeving][ASEAutoscale].

### <a name="storage"></a>Storage
Elke as-omgeving is geconfigureerd met 500 GB aan opslagruimte. Deze ruimte wordt gebruikt voor alle Hallo-apps op Hallo as-omgeving. Deze opslagruimte deel uitmaakt van Hallo as-omgeving en momenteel kan niet worden uitgeschakeld toouse uw opslagruimte. Als u aanpassingen tooyour virtueel netwerkroutering of beveiligingsgroep doorvoeren wilt, moet u toostill toegang tooAzure opslag--toestaan of Hallo as-omgeving, kan niet werken.

### <a name="database"></a>Database
Hallo-database bevat Hallo-informatie die definieert Hallo-omgeving, evenals Hallo informatie over Hallo-apps die erin worden uitgevoerd. Dit is te deel uit van Hallo ondergebracht Azure abonnement. Het is niet iets dat u een directe mogelijkheid toomanipulate hebt. Als u aanpassingen tooyour virtueel netwerkroutering of beveiligingsgroep doorvoeren wilt, moet u toostill toegang tooSQL Azure--toestaan of Hallo as-omgeving, kan niet werken.

### <a name="network"></a>Netwerk
Hallo VNet dat wordt gebruikt met uw as-omgeving kan worden één die u hebt aangebracht tijdens het maken van Hallo as-omgeving of die u hebt aangebracht tevoren. Wanneer u Hallo subnet tijdens het maken van de as-omgeving maakt, het Hallo as-omgeving toobe in Hallo forceert dezelfde resourcegroep als Hallo virtuele netwerk. Als u Hallo resourcegroep die wordt gebruikt door uw toobe as-omgeving anders dan die van uw VNet moet, moet u toocreate uw as-omgeving met een resource manager-sjabloon.

Er zijn enkele beperkingen op Hallo virtueel netwerk dat wordt gebruikt voor een as-omgeving:

* Hallo virtueel netwerk moet een regionaal virtueel netwerk.
* Er moet toobe een subnet met 8 of meer adressen waarop Hallo as-omgeving wordt geïmplementeerd.
* Nadat een subnet gebruikte toohost een as-omgeving is, kan niet Hallo-adresbereik van Hallo subnet worden gewijzigd. Daarom is het raadzaam dat subnet Hallo bevat ten minste 64 adressen tooaccommodate een eventuele toekomstige groei van de as-omgeving.
* Er is niets anders in Hallo subnet maar Hallo as-omgeving.

In tegenstelling tot Hallo gehoste service met Hallo as-omgeving, Hallo [virtueel netwerk] [ virtualnetwork] en subnet onder het Gebruikersbeheer zijn.  U kunt uw virtuele netwerk via Hallo virtuele netwerk-gebruikersinterface of PowerShell beheren.  Een as-omgeving kan worden geïmplementeerd in een klassiek of Resource Manager VNet.  Hallo-portal en API-ervaringen zijn enigszins verschillen tussen het klassieke en het Resource Manager VNets maar Hallo as-omgeving ervaring wordt dezelfde Hallo.

Hallo VNet dat is gebruikt toohost een as-omgeving kunt beide particuliere RFC1918 IP-adressen of openbare IP-adressen kunnen worden gebruikt.  Als u wenst toouse een IP-adresbereik dat niet wordt gedekt door RFC1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) moet u toocreate uw VNet en subnet toobe die wordt gebruikt door uw as-omgeving voor het maken van de as-omgeving.

Omdat deze mogelijkheid hello Azure App Service in uw virtueel netwerk worden geplaatst, betekent dit dat de apps die worden gehost in uw as-omgeving hebt nu toegang tot resources die rechtstreeks via ExpressRoute of site-naar-site virtuele particuliere netwerken (VPN's) beschikbaar worden gesteld. Hallo-apps die binnen uw App Service-omgeving hebben geen extra netwerken functies tooaccess resources beschikbaar toohello virtueel netwerk die als host voor uw App Service-omgeving fungeert nodig. Dit betekent dat u niet toouse VNET-integratie of hybride verbindingen tooget tooresources in of verbonden tooyour virtueel netwerk hoeft. U kunt beide van deze functies nog steeds gebruiken hoewel tooaccess bronnen in netwerken die geen tooyour virtueel netwerk is verbonden.

U kunt bijvoorbeeld VNET integratie toointegrate gebruiken met een virtueel netwerk dat zich in uw abonnement, maar is niet verbonden toohello virtueel netwerk dat u uw as-omgeving in. U kunt ook nog steeds hybride verbindingen tooaccess bronnen die zich in andere netwerken, net zoals u normaal gesproken kunt gebruiken.  

Als u het virtuele netwerk dat is geconfigureerd met een VPN ExpressRoute hebt, moet u zich bewust zijn van een aantal Hallo routering behoeften met een as-omgeving. Er zijn enkele gebruiker gedefinieerde route (UDR)-configuraties die incompatibel met een as-omgeving zijn. Zie voor meer informatie over het uitvoeren van een as-omgeving in een virtueel netwerk met ExpressRoute [met een App Service-omgeving in een virtueel netwerk met ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Binnenkomend verkeer beveiligen
Er zijn twee primaire methoden toocontrol inkomend verkeer tooyour as-omgeving.  U kunt Network Security Groups(NSGs) toocontrol welk IP-adressen heeft toegang tot uw as-omgeving zoals hier wordt beschreven [hoe toocontrol binnenkomend verkeer in een App-serviceomgeving](app-service-app-service-environment-control-inbound-traffic.md) en u kunt ook uw as-omgeving configureren met een interne Load Balancer(ILB).  Deze functies kunnen ook samen worden gebruikt als u wilt dat toorestrict toegang met nsg's tooyour ILB as-omgeving.

Wanneer u een as-omgeving maakt, maakt deze een VIP-adres in uw VNet.  Er zijn twee VIP typen externe en interne.  Wanneer u een as-omgeving met een externe VIP maakt vervolgens zijn uw apps in uw as-omgeving toegankelijk via internet routeerbare IP-adres. Wanneer u uw as-omgeving intern selecteert, wordt geconfigureerd met een ILB en worden niet rechtstreeks toegankelijk internet.  Een as ILB-omgeving een externe VIP nog steeds vereist, maar wordt alleen gebruikt voor toegang tot Azure beheer en onderhoud.  

Tijdens het maken van de as-ILB omgeving Hallo subdomein gebruikt door Hallo ILB as-omgeving te bieden en hebben toomanage uw eigen DNS voor Hallo subdomein die u opgeeft.  Omdat u de subdomeinnaam Hallo ingesteld moet u ook toomanage Hallo certificaat gebruikt voor HTTPS-toegang.  Na het as-omgeving gevraagd maken dat u bent tooprovide Hallo certificaat.  toolearn meer informatie over het maken en gebruiken van een as ILB-omgeving gelezen [met behulp van een interne Load Balancer met een App-serviceomgeving][ILBASE]. 

## <a name="portal"></a>Portal
U kunt beheren en bewaken van uw App Service-omgeving met behulp van Hallo gebruikersinterface in hello Azure-portal. Als u een as-omgeving hebt, klikt u vervolgens bent u waarschijnlijk toosee Hallo symbool App Service op de zijbalk. Dit symbool is gebruikte toorepresent App Service-omgevingen in hello Azure-portal:

![Symbool van App Service-omgeving][1]

tooopen Hallo gebruikersinterface met een lijst met alle van uw App Service-omgevingen, kunt u Hallo-pictogram of selecteer Hallo punthaak (' > ' symbool) onderaan Hallo Hallo zijbalk tooselect App Service-omgevingen. Als u een van de Hallo ASEs vermeld, Hallo gebruikersinterface die gebruikte toomonitor openen en beheren.

![Gebruikersinterface voor het controleren en beheren van uw App Service-omgeving][2]

Deze eerste blade ziet u enkele eigenschappen van de as-omgeving, samen met een metrische grafiek per resourcegroep. Aantal Hallo-eigenschappen die worden weergegeven in Hallo **Essentials** blok ook hyperlinks zijn die Hallo-blade die is gekoppeld aan deze wordt geopend. Bijvoorbeeld, kunt u Hallo **virtueel netwerk** naam tooopen up Hallo UI Hallo virtueel netwerk dat uw as-omgeving wordt uitgevoerd in de gekoppeld. **App Service-plannen** en **Apps** elke open bladen die een lijst van deze items die in uw as-omgeving.  

### <a name="monitoring"></a>Bewaking
Hallo grafieken kunnen u toosee verschillende maatstaven voor prestaties in elke resourcegroep. Hallo front-groep, kunt u Hallo gemiddelde CPU en geheugen bewaken. Voor werknemersgroepen, kunt u bewaken Hallo die wordt gebruikt en Hallo hoeveelheid die beschikbaar is.

Meerdere App Service plan kunnen maken gebruik van de werknemers in een werknemersgroep Hallo. Hallo werkbelasting wordt niet gedistribueerd in Hallo dezelfde wijze net als bij Hallo-front-endservers, zodat de CPU- en geheugengebruik Hallo ongeveer Hallo manier van nuttige informatie niet leveren. Het is belangrijker tootrack hoeveel werknemers die u hebt gebruikt en zijn beschikbaar--met name als u dit systeem voor andere beheert toouse.  

U kunt ook alle Hallo metrische gegevens die kunnen worden bijgehouden in Hallo grafieken tooset van waarschuwingen. Instellen van waarschuwingen hier werkt hetzelfde als elders Hallo in App Service. U kunt een waarschuwing instellen van beide Hallo **waarschuwingen** UI-onderdeel of van dieper ingegaan op parameters gebruikersinterface en het selecteren van **waarschuwing toevoegen**.

![Metrische gegevens gebruikersinterface][3]

Hallo metrische gegevens die alleen werden besproken zijn metrische gegevens Hallo-App Service-omgeving. Er zijn ook metrische gegevens die beschikbaar op Hallo niveau van App Service-plan zijn. Dit is waar controle van CPU en geheugen maakt een groot aantal zin.

In een as-omgeving zijn alle Hallo die App Service-abonnementen speciale App Service-abonnementen. Dat betekent dat alleen Hallo-apps die worden uitgevoerd op Hallo hosts toegewezen toothat App Service-abonnement Hallo apps in App Service plan. toosee meer informatie over uw App Service-abonnement online zetten van uw App Service-abonnement vanaf elke Hallo lijsten in Hallo as-omgeving UI of van **bladeren App Service-plannen** (die een lijst met alle mappen).   

### <a name="settings"></a>Instellingen
In de blade Hallo as-omgeving, er is een **instellingen** sectie met verschillende belangrijke mogelijkheden:

**Instellingen** > **eigenschappen**: Hallo **instellingen** blade automatisch wordt geopend wanneer u online van de blade van het as-omgeving zetten. Hallo top is **eigenschappen**. Er zijn een aantal items hier redundante toowhat u ziet in **Essentials**, maar wat is zeer nuttig is **virtueel IP-adres**, evenals **uitgaande IP-adressen**.

![Instellingenblade en eigenschappen][4]

**Instellingen** > **IP-adressen**: wanneer u een IP-Secure Sockets Layer (SSL)-app in uw as-omgeving maken, moet u een SSL IP-adres. In de volgorde tooobtain een moet uw as-omgeving SSL IP-adressen waarvan deze eigenaar is die kunnen worden toegewezen. Wanneer een as-omgeving is gemaakt, heeft één SSL IP-adres voor dit doel, maar u kunt meer toevoegen. Er is een kosten voor extra IP SSL adressen, zoals wordt weergegeven in [App Service-prijzen] [ AppServicePricing] (in de sectie Hallo op SSL-verbindingen). Hallo extra prijs is Hallo IP SSL prijs.

**Instellingen** > **Front-End-Pool** / **werknemersgroepen**: elk van deze groep resourceblades Hallo mogelijkheid toosee informatie alleen op deze bronnengroep biedt , Daarnaast tooproviding bepaalt toofully scale die resourcegroep.  

Hallo base blade voor elke resourcegroep wordt een grafiek met metrische gegevens voor deze resourcegroep. Net als met Hallo grafieken blade Hallo as-omgeving, kunt u gaat u in de grafiek Hallo en waarschuwingen naar wens instellen. Een waarschuwing instellen uit Hallo as-omgeving blade voor een specifieke resourcegroep hetzelfde effect als dit te doen vanuit resourcegroep Hallo Hallo. Van Hallo werknemersgroep **instellingen** blade hebt u toegang tooall Hallo Apps of App Service-abonnementen die worden uitgevoerd in deze worker-groep.

![Groepsinstellingen worker gebruikersinterface][5]

### <a name="portal-scale-capabilities"></a>Mogelijkheden van de portal schaal
Er zijn drie schaalbewerkingen:

* Het wijzigen van het aantal IP-adressen in Hallo as-omgeving die beschikbaar voor gebruik van IP SSL zijn Hallo.
* Hallo grootte wijzigen van Hallo berekeningsresource die wordt gebruikt in een resourcegroep.
* Het wijzigen van het aantal rekenresources die worden gebruikt in een resourcegroep, hetzij handmatig, hetzij via automatisch schalen Hallo.

In de portal hello zijn er drie manieren toocontrol hoeveel servers die u in uw resourcegroepen hebt:

* Een schaalaanpassing van Hallo as-omgeving hoofdblade Hallo bovenaan. Kunt u meerdere scale configuratiewijzigingen toohello front-end- en werknemersgroepen. Ze worden toegepast als een enkele bewerking.
* Een handmatige schaalaanpassing van de afzonderlijke resourcegroep Hallo **Scale** blade die zich onder **instellingen**.
* Automatisch schalen die u tijdens het instellen van de afzonderlijke resourcegroep Hallo **Scale** blade.

toouse hello schaalaanpassing op Hallo as-omgeving blade Sleep Hallo schuifregelaar toohello hoeveelheid en sla. Deze gebruikersinterface ondersteunt ook veranderende Hallo-grootte.  

![Schaal gebruikersinterface][6]

toouse hello handmatig of automatisch schalen mogelijkheden in een specifieke resourcegroep te gaan**instellingen** > **Front-End-Pool** / **werknemersgroepen** als van toepassing. Vervolgens opent u het Hallo-groep die u toochange wilt. Ga te**instellingen** > **uitschalen** of **instellingen** > **omhoog schalen**. Hallo **uitschalen** blade kunt u toocontrol exemplaar hoeveelheid. **Omhoog schalen** kunt u toocontrol resourcegrootte.  

![Schaalinstellingen gebruikersinterface][7]

## <a name="fault-tolerance-considerations"></a>Overwegingen voor fouttolerantie
U kunt een toouse App Service-omgeving van het totale aantal rekenresources too55 configureren. Alleen 50 kan gebruikte toohost werkbelastingen zijn die 55 compute-bronnen. Hallo reden hiervoor is tweeledig. Er is minimaal 2 front-rekenresources.  Die laat up too53 toosupport Hallo werknemersgroep toewijzing. In de volgorde tooprovide fouttolerantie moet u een extra Reken-resource die is toegewezen op basis van regels voor toohello toohave:

* Elke worker-groep moet ten minste 1 extra Reken-resource die geen beschikbare toobe toegewezen een werkbelasting.
* Wanneer het aantal rekenresources in een werknemersgroep Hallo boven een bepaalde waarde gaat, klikt u vervolgens is een andere compute resource vereist voor fouttolerantie. Dit is geen Hallo geval in Hallo front-groep.

Binnen een enkele werknemersgroep zijn Hallo fouttolerantie vereisten dat de bronnen voor een bepaalde waarde van X tooa werknemersgroep toegewezen:

* Als X tussen 2 en 20 ligt, is het Hallo hoeveelheid bruikbare rekenresources die u voor werkbelastingen gebruiken kunt X-1.
* Als X tussen 21 en 40, is Hallo hoeveelheid bruikbare rekenresources die u voor werkbelastingen gebruiken kunt X-2.
* Als X tussen 41 en 53, is Hallo hoeveelheid bruikbare rekenresources die u voor werkbelastingen gebruiken kunt X-3.

minimale footprint Hallo heeft 2-front-endservers en twee 2 werkers beschikken.  Hello hierboven instructies vervolgens volgen hier enkele voorbeelden tooclarify:  

* Als u 30 werknemers in een van de toepassingen hebt, kan 28 hiervan gebruikte toohost werkbelastingen zijn.
* Als u twee 2 werkers beschikken in een van de toepassingen hebt, kan 1 gebruikte toohost werkbelastingen zijn.
* Als u 20 werknemers in een van de toepassingen hebt, kan 19 gebruikte toohost werkbelastingen zijn.  
* Hebt u 21 werknemers in een één groep, wordt nog steeds alleen 19 gebruikte toohost werkbelastingen.  

Hallo fouttolerantie aspect is belangrijk, maar u moet tookeep in gedachten als u bepaalde drempels schalen. Als u tooadd wilt meer capaciteit van 20 exemplaren en ga too22 of hoger omdat 21 eventuele meer capaciteit niet toevoegen. Hallo geldt ook gaan boven 40, waarbij Hallo volgende nummer dat wordt toegevoegd capaciteit 42 is.  

## <a name="deleting-an-app-service-environment"></a>Verwijderen van een App Service-omgeving
Als u een App-serviceomgeving toodelete wilt, vervolgens gewoon gebruiken Hallo **verwijderen** actie aan de resourceblade Hallo van Hallo App Service-omgeving. Als u dit doet, moet u na vragen aan gebruiker tooenter Hallo-naam van uw App Service-omgeving tooconfirm dat u toch toodo dit. Houd er rekening mee dat wanneer u een App Service-omgeving hebt verwijderd, u alle Hallo inhoud binnen deze ook verwijdert.  

![Verwijderen van een App Service-omgeving gebruikersinterface][9]  

## <a name="getting-started"></a>Aan de slag
tooget de slag met App Service-omgevingen, Zie [hoe toocreate een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md).

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
