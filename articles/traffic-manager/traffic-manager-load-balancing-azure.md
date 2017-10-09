---
title: aaaUsing load balancing-services in Azure | Microsoft Docs
description: 'Deze zelfstudie laat zien hoe toocreate een scenario met behulp van Azure load balancing portfolio Hallo: Traffic Manager en Application Gateway Load Balancer.'
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Gebruik van taakverdeling services in Azure

## <a name="introduction"></a>Inleiding

Microsoft Azure biedt meerdere services voor het beheren van het netwerkverkeer wordt gedistribueerd en taakverdeling. U kunt deze services afzonderlijk gebruiken of hun methoden, afhankelijk van uw behoeften, toobuild Hallo optimale oplossing combineren.

In deze zelfstudie we eerst een gebruiksvoorbeeld klant definiëren en hoe deze kan worden gemaakt krachtiger en weergegeven zodat met behulp van de volgende Azure load balancing portfolio Hallo: Traffic Manager en Application Gateway Load Balancer. Vervolgens bieden stapsgewijze instructies voor het maken van een implementatie die is geografisch redundante tooVMs verkeer gedistribueerd en kunt u verschillende soorten aanvragen beheren.

Elk van deze services speelt een afzonderlijke rol in Hallo-taakverdeling hiërarchie op een conceptuele niveau.

* **Traffic Manager** biedt globale DNS taakverdeling. Het wordt gekeken naar binnenkomende aanvragen van de DNS- en reageert met een goede eindpunt, in overeenstemming met Hallo routering beleid Hallo klant is geselecteerd. Opties voor methoden zijn:
  * Prestaties routering toosend Hallo aanvrager toohello dichtstbijzijnde eindpunt in termen van latentie.
  * Prioriteit routering toodirect alle verkeer tooan eindpunt, met andere eindpunten als back-up.
  * Gewogen round robin routering, die wordt verkeer dat is gebaseerd op Hallo weging die tooeach-eindpunt is toegewezen.

  Hallo-client verbinding rechtstreeks toothat eindpunt. Azure Traffic Manager detecteert wanneer een eindpunt niet in orde is en vervolgens omleidingen Hallo clients tooanother orde exemplaar. Raadpleeg te[Azure Traffic Manager-documentatie](traffic-manager-overview.md) toolearn meer over Hallo-service.
* **Toepassingsgateway** toepassing levering controller (ADC) biedt een service en biedt verschillende laag 7 taakverdeling mogelijkheden voor uw toepassing. Klanten kunnen toooptimize web farm productiviteit door het offloaden van CPU-intensief SSL-beëindiging toohello toepassingsgateway. Andere mogelijkheden voor het doorsturen van laag 7 bevatten round-robin distributie van inkomend verkeer, sessie cookies gebaseerde affiniteit URL-pad gebaseerde routering en Hallo mogelijkheid toohost meerdere websites achter een gateway één toepassing. Application Gateway kan worden geconfigureerd als een gateway internetgerichte, een gateway interne alleen-lezen of een combinatie van beide. Toepassingsgateway is volledig Azure beheerde, schaalbare en maximaal beschikbaar. Het biedt een uitgebreide verzameling diagnostische gegevens en functies voor logboekregistratie voor betere beheersbaarheid.
* **De Load Balancer** is een integraal onderdeel van hello Azure SDN stack, hoge prestaties, lage latentie laag 4-taakverdeling die services levert voor alle UDP en TCP-protocollen. Het beheert binnenkomende en uitgaande verbindingen. U kunt openbare en interne eindpunten voor netwerktaakverdeling configureren en definiëren regels toomap inkomende verbindingen tooback-end-pool bestemmingen via TCP- en HTTP-status probing opties toomanage beschikbaarheid van de service.

## <a name="scenario"></a>Scenario

In dit voorbeeldscenario gebruiken we een eenvoudige website die twee typen inhoud fungeert: installatiekopieën en dynamisch gerenderde webpagina's. Hallo-website moet geografisch redundante en deze moet de gebruikers van Hallo dichtstbijzijnde (laagste latentie) dienen toothem locatie. Hallo toepassingsontwikkelaar heeft besloten dat Hallo alle URL's die overeenkomen met patroon/installatiekopieën / * uit een specifieke groep van virtuele machines die afwijken van de rest van de webfarm Hallo Hallo worden behandeld.

Bovendien moet Hallo VM standaardgroep Hallo dynamische inhoud tootalk tooa back-end-database die wordt gehost op een cluster met hoge beschikbaarheid. Hallo volledige implementatie is ingesteld via Azure Resource Manager.

Met Traffic Manager en Application Gateway Load Balancer kunt deze website tooachieve deze doelstellingen te ontwerpen:

* **Multi-geografische redundantie**: als één regio uitvalt, Traffic Manager routes verkeer naadloos toohello dichtstbijzijnde regio zonder tussenkomst van de eigenaar van de toepassing hello.
* **Kortere wachttijd**: omdat Traffic Manager wordt automatisch omgeleid Hallo klant toohello dichtstbijzijnde regio, Hallo klant lagere latentie optreedt bij het aanvragen van Hallo webpagina inhoud.
* **Onafhankelijke schaalbaarheid**: omdat Hallo web toepassing werklast wordt gescheiden door het type inhoud, de eigenaar van de toepassing hello Hallo aanvraag werkbelastingen onafhankelijk van elkaar kan worden geschaald. Toepassingsgateway zorgt ervoor dat verkeer Hallo gerouteerde toohello van de juiste groepen op basis van opgegeven Hallo Hallo status van de toepassing hello en -regels.
* **Interne load balancing**: omdat de Load Balancer voor Hallo cluster met hoge beschikbaarheid, is de enige Hallo active en in goede orde endpoint voor een database blootgestelde toohello toepassing is. Bovendien kan een databasebeheerder Hallo werkbelasting optimaliseren door het actieve en passieve replica's over Hallo cluster onafhankelijk van de front-toepassing hello verdeeld. Load Balancer biedt verbindingen toohello cluster met hoge beschikbaarheid en zorgt ervoor dat alleen orde databases verbindingsaanvragen ontvangen.

Hallo toont volgende diagram de architectuur Hallo van dit scenario:

![Diagram van de taakverdelings-architectuur](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> In dit voorbeeld is alleen een van de vele mogelijke configuraties van Hallo-taakverdeling services die Azure biedt. Traffic Manager en Application Gateway Load Balancer kunnen worden gecombineerd en overeenkomende toobest behoeften van uw load balancing. Bijvoorbeeld, als SSL-offload of laag 7 verwerking niet nodig is, kan Load Balancer kan worden gebruikt in plaats van Application Gateway.

## <a name="setting-up-hello-load-balancing-stack"></a>Hallo-taakverdeling stack instellen

### <a name="step-1-create-a-traffic-manager-profile"></a>Stap 1: Een Traffic Manager-profiel maken

1. Klik in hello Azure-portal, op **nieuw**, en vervolgens zoeken Hallo marketplace voor 'Traffic Manager-profiel'.
2. Op Hallo **maken Traffic Manager-profiel** blade Hallo basisinformatie volgende invoeren:

  * **Naam**: naam van uw Traffic Manager-profiel een DNS-voorvoegsel geven.
  * **Routeringsmethode voor**: Selecteer Hallo beleid voor verkeersroutering methode. Zie voor meer informatie over methoden Hallo [verkeersrouteringsmethoden voor Traffic Manager over](traffic-manager-routing-methods.md).
  * **Abonnement**: Hallo-abonnement met Hallo profiel selecteren.
  * **Resourcegroep**: Selecteer Hallo resourcegroep die Hallo profiel bevat. Het kan zijn dat een nieuwe of bestaande resourcegroep.
  * **Locatie voor resourcegroep**: Traffic Manager-service is globale en is niet gebonden tooa locatie. U moet echter opgeven dat een regio voor Hallo groep waarin Hallo metagegevens die zijn gekoppeld aan het Traffic Manager-profiel Hallo zich bevindt. Deze locatie heeft geen invloed op Hallo runtime-beschikbaarheid van Hallo-profiel.

3. Klik op **maken** toogenerate Hallo Traffic Manager-profiel.

  ![Blade 'Traffic Manager maken'](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Stap 2: Maak Hallo Toepassingsgateways

1. Klik in de Azure-portal in het linkerdeelvenster Hallo Hallo op **nieuw** > **Networking** > **Application Gateway**.
2. Voer Hallo basisinformatie over Hallo toepassingsgateway te volgen:

  * **Naam**: naam van de toepassingsgateway Hallo Hallo.
  * **SKU-grootte**: grootte van beschikbaar als een klein, middelgroot of groot Hallo-toepassingsgateway Hallo.
  * **Aantal exemplaar**: het aantal exemplaren hello, een waarde van 2 tot en met 10.
  * **Resourcegroep**: Hallo-resourcegroep van de toepassingsgateway Hallo. Het kan een bestaande resourcegroep of een nieuwe map zijn.
  * **Locatie**: Hallo regio voor de toepassingsgateway hello, die is Hallo dezelfde locatie als Hallo resourcegroep. Hallo-locatie is belangrijk, omdat Hallo virtueel netwerk en openbare IP-adres moeten zich op Hallo dezelfde locatie als Hallo-gateway.
3. Klik op **OK**.
4. Hallo virtueel netwerk, subnet, front-end-IP- en listener-configuraties voor de toepassingsgateway Hallo definiëren. In dit scenario Hallo front-end-IP-adres is **openbare**, waardoor ze toobe toegevoegd als een eindpunt toohello Traffic Manager-profiel later op.
5. Hallo-listener configureren met een Hallo volgende opties:
    * Als u HTTP gebruikt, er is niets tooconfigure. Klik op **OK**.
    * Als u HTTPS gebruikt, verdere is configuratie vereist. Raadpleeg te[een toepassingsgateway maken](../application-gateway/application-gateway-create-gateway-portal.md), te beginnen bij stap 9. Wanneer u Hallo configuratie hebt voltooid, klikt u op **OK**.

#### <a name="configure-url-routing-for-application-gateways"></a>URL voor Toepassingsgateways routering configureren

Wanneer u een back-end-pool kiest, wordt een application gateway die geconfigureerd met een regel op basis van het pad naar een patroon pad van de aanvraag-URL Hallo in toevoeging tooround-robin distributie. In dit scenario we toevoegen een regel op basis van het pad toodirect elke URL met ' /images/\*' toohello installatiekopie-servergroep. Raadpleeg voor meer informatie over het configureren van URL-pad gebaseerde routering voor een toepassingsgateway te[maakt u een regel op basis van het pad voor een toepassingsgateway](../application-gateway/application-gateway-create-url-route-portal.md).

![Application Gateway weblaag diagram](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. Ga in de resourcegroep toohello exemplaar van Hallo application gateway die u hebt gemaakt in de voorgaande sectie Hallo.
2. Onder **instellingen**, selecteer **back-endpools**, en selecteer vervolgens **toevoegen** tooadd Hallo virtuele machines die u tooassociate met Hallo weblaag back-end-adresgroepen wilt.
3. Op Hallo **toevoegen van de back-endpool** blade Hallo-naam van back-end-pool Hallo en alle Hallo IP-adressen van Hallo-machines die zich in de groep Hallo bevinden invoeren. In dit scenario zijn er twee back-endserver pools van virtuele machines verbinding.

  ![Application Gateway 'Back-endpool toevoegen' blade](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. Onder **instellingen** van toepassingsgateway hello, selecteer **regels**, en klik vervolgens op Hallo **pad basis** knop tooadd een regel.

  ![Application Gateway regels 'pad op basis van knop](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Op Hallo **toevoegen op basis van een pad regel** blade Hallo regel dankzij de volgende informatie Hallo configureren.

   Basisinstellingen:

   + **Naam**: Hallo beschrijvende naam van regel Hallo die toegankelijk is in Hallo-portal.
   + **Listener**: Hallo-listener die wordt gebruikt voor het Hallo-regel.
   + **Standaard back-endpool**: back-end-pool toobe gebruikt met de standaardregel Hallo Hallo.
   + **Standaardinstellingen voor HTTP-**: Hallo HTTP instellingen toobe gebruikt met de standaardregel Hallo.

   Pad gebaseerde regels:

   + **Naam**: Hallo beschrijvende naam van een regel op basis van een pad Hallo.
   + **Paden**: Hallo padregel die wordt gebruikt voor het doorsturen van verkeer.
   + **Back-Endpool**: Hallo back-end-pool toobe gebruikt in combinatie met deze regel.
   + **HTTP-instelling**: Hallo HTTP instellingen toobe gebruikt in combinatie met deze regel.

   > [!IMPORTANT]
   > Paden: Geldige paden moeten beginnen met '/'. jokertekens Hallo '\*' alleen aan Hallo einde is toegestaan. Voorbeelden van geldige/xyz, / XYZ zijn\*, of /xyz/\*.

   ![Application Gateway 'Toevoegen op basis van een pad regel' blade](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Stap 3: De gateways toohello Traffic Manager eindpunten toevoegen

In dit scenario is het Traffic Manager verbonden tooapplication gateways (zoals geconfigureerd in de vorige stappen Hallo) die zich in verschillende regio's bevinden. Nu Hallo Toepassingsgateways zijn geconfigureerd, Hallo volgende stap is het tooconnect ze tooyour Traffic Manager-profiel.

1. Open uw Traffic Manager-profiel. toodo dus zoeken in de resourcegroep of zoeken naar Hallo-naam van Hallo Traffic Manager-profiel van **alle Resources**.
2. Selecteer in het linkerdeelvenster Hallo **eindpunten**, en klik vervolgens op **toevoegen** tooadd een eindpunt.

  ![Traffic Manager-eindpunten "toevoegen" knop](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Op Hallo **eindpunt toevoegen** blade een eindpunt maken door te voeren van Hallo volgende informatie:

  * **Type**: Hallo type eindpunt tooload-saldo selecteren. Selecteer in dit scenario **Azure-eindpunt** omdat er verbinding wordt toohello gatewayexemplaren van een toepassing die eerder zijn geconfigureerd.
  * **Naam**: Voer Hallo naam van het Hallo-eindpunt.
  * **Resource doeltype**: Selecteer **openbaar IP-adres** en klik vervolgens onder **Doelresource**, selecteer Hallo openbare IP-adres van de toepassingsgateway Hallo die eerder is geconfigureerd.

   ![Traffic Manager-blade 'Eindpunt toevoegen'](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Nu u uw instellingen testen kunt door deze te openen met Hallo DNS van uw Traffic Manager-profiel (in dit voorbeeld: TrafficManagerScenario.trafficmanager.net). U kunt aanvragen verzenden, online zetten van of virtuele machines en de webservers die zijn gemaakt in verschillende regio's brengen en Hallo Traffic Manager-profiel instellingen tootest uw instellingen te wijzigen.

### <a name="step-4-create-a-load-balancer"></a>Stap 4: Een load balancer maken

In dit scenario distribueert de Load Balancer verbindingen van Hallo web laag toohello databases binnen een cluster met hoge beschikbaarheid.

Als uw databasecluster met hoge beschikbaarheid-van SQL Server AlwaysOn gebruikmaakt, raadpleeg dan te[configureren van een of meer altijd op beschikbaarheid Beschikbaarheidsgroeplisteners](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) voor stapsgewijze instructies.

Zie voor meer informatie over het configureren van een interne load balancer [maken van een interne load balancer in hello Azure-portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. Klik in de Azure-portal in het linkerdeelvenster Hallo Hallo op **nieuw** > **Networking** > **Load balancer**.
2. Op Hallo **maken load balancer** blade, kies een naam voor de load balancer.
3. Set Hallo **Type** te**intern**, en kies Hallo juiste virtueel netwerk en subnet voor Hallo load balancer tooreside in.
4. Onder **IP-adrestoewijzing**, selecteert u **dynamische** of **statische**.
5. Onder **resourcegroep**, Hallo resourcegroep voor Hallo load balancer kiezen.
6. Onder **locatie**, kies de juiste regio Hallo voor Hallo load balancer.
7. Klik op **maken** toogenerate Hallo load balancer.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Verbinding maken met een back-enddatabase laag toohello load balancer

1. Vinden van de resourcegroep Hallo load balancer die is gemaakt in de vorige stappen Hallo.
2. Onder **instellingen**, klikt u op **back-endpools**, en klik vervolgens op **toevoegen** tooadd een back-end-pool.

  ![Load Balancer-blade 'Back-endpool toevoegen'](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Op Hallo **toevoegen van de back-endpool** blade Geef Hallo-naam van Hallo back-end-adresgroep.
4. Afzonderlijke computers of een beschikbaarheid set toohello back-end van toepassingen toevoegen.

#### <a name="configure-a-probe"></a>Een test configureren

1. In de load balancer, onder **instellingen**, selecteer **Probes**, en klik vervolgens op **toevoegen** tooadd een test.

 ![Load Balancer "Add-test" blade](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Op Hallo **toevoegen test** blade Hallo-naam voor de test Hallo invoeren.
3. Selecteer Hallo **Protocol** voor de Hallo test. Voor een database kunt u een TCP-controle in plaats van een HTTP-test. toolearn meer informatie over de load balancer-tests te verwijzen[Understand load balancer tests](../load-balancer/load-balancer-custom-probe-overview.md).
4. Voer Hallo **poort** van uw database toobe gebruikt voor toegang tot Hallo test.
5. Onder **Interval**, opgeven hoe vaak tooprobe toepassing hello.
6. Onder **drempelwaarde voor onjuiste status**, geef Hallo aantal continue testfouten dat moet worden uitgevoerd voor Hallo back-end VM toobe niet in orde beschouwd.
7. Klik op **OK** toocreate Hallo test.

#### <a name="configure-hello-load-balancing-rules"></a>Hallo-taakverdeling regels configureren

1. Onder **instellingen** van de load balancer, selecteer **Taakverdelingsregels**, en klik vervolgens op **toevoegen** toocreate een regel.
2. Op Hallo **toevoegen taakverdelingsregel** blade Voer Hallo **naam** voor Hallo-taakverdeling regel.
3. Kies Hallo **Frontend-IP-adres** Hallo netwerktaakverdeler **Protocol**, en **poort**.
4. Onder **backendpoort**, Hallo poort toobe gebruikt in Hallo back-end-pool opgeven.
5. Selecteer Hallo **back-endpool** en Hallo **Probe** die zijn gemaakt in de Hallo vorige stappen tooapply Hallo regel.
6. Onder **sessiepersistentie**, kiezen hoe u Hallo sessies toopersist.
7. Onder **inactief time-outs**, geef het aantal minuten voordat een time-out voor inactiviteit Hallo.
8. Onder **zwevend IP**, selecteert u **uitgeschakelde** of **ingeschakeld**.
9. Klik op **OK** toocreate Hallo regel.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Stap 5: Verbinding maken met de weblaag VMs toohello load balancer

Nu we Hallo IP-adres en de load balancer front-endpoort in Hallo-toepassingen die worden uitgevoerd op uw weblaag virtuele machines voor de databaseverbindingen configureren. Deze configuratie is specifiek toohello toepassingen die worden uitgevoerd op deze virtuele machines. Raadpleeg de documentatie van de toepassing toohello tooconfigure Hallo doel-IP-adres en poort. toofind hello IP-adres van de front-end Hallo in hello Azure-portal, gaat u de front-end-IP-adresgroep toohello Hallo **instellingen netwerkverdeler** blade.

![Load Balancer 'Frontend-IP-adresgroep' navigatiedeelvenster](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van Traffic Manager](traffic-manager-overview.md)
* [Overzicht van Application Gateway](../application-gateway/application-gateway-introduction.md)
* [Overzicht van Azure Load Balancer](../load-balancer/load-balancer-overview.md)
