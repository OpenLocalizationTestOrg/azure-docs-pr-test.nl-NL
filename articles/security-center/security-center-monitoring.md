---
title: aaaSecurity bewaken in Azure Security Center | Microsoft Docs
description: In dit artikel helpt u tooget gestart met de bewakingsmogelijkheden in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Beveiligingsstatus bewaken in Azure Security Center
In dit artikel helpt u Hallo bewakingsmogelijkheden in Azure Security Center toomonitor naleving van beleid gebruiken.

## <a name="what-is-security-health-monitoring"></a>Wat houdt de bewaking van de beveiligingsstatus in?
We denken dat vaak bewaking te bekijken en te wachten op een gebeurtenis toooccur zodat we toohello situatie kunnen reageren. Beveiligingsbewaking verwijst toohaving een proactieve strategie waarbij uw resources tooidentify systemen die niet voldoen aan de organisatie-standaarden of aanbevolen procedures audits.

## <a name="monitoring-security-health"></a>Beveiligingsstatus bewaken
Nadat u hebt ingeschakeld [beveiligingsbeleid](security-center-policies.md) voor resources van een abonnement, analyseert Security Center Hallo beveiliging van uw resources tooidentify potentiële beveiligingslekken naar voren. Informatie over uw netwerkconfiguratie is onmiddellijk beschikbaar. Kan het een uur duren voordat of meer informatie over de configuratie van de virtuele machine, zoals beveiliging bijwerken, status en configuratie van besturingssysteem, toobecome beschikbaar. U kunt Hallo beveiligingsstatus van uw resources en eventuele problemen weergeven in Hallo **preventie** sectie. U kunt ook een overzicht van die problemen op Hallo **aanbevelingen** tegel.

Voor meer informatie over het tooapply aanbevelingen lezen [beveiligingsaanbevelingen implementeren in Azure Security Center](security-center-recommendations.md).

Onder Hallo **preventie** sectie, kunt u Hallo beveiligingsstatus van uw resources bewaken. In de Hallo voorbeeld te volgen, kunt u bekijken die in elke resource tegel (Compute, netwerken, opslag & gegevens en toepassingen) totaal aantal problemen die zijn geïdentificeerd Hallo heeft.

![De tegel Beveiligingsstatus van de resource](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Berekenen controleren
Wanneer u klikt op **Compute** tegel, hello **Compute** blade die wordt geopend ziet u drie tabbladen:

- **Overzicht**: aanbevelingen voor controle en virtuele machines.
- **Virtuele machines**: lijst met alle virtuele machines en de bijbehorende actuele beveiligingsstatussen.
- **Cloudservices**: lijst met alle web- en worker-rollen gecontroleerd met het beveiligingscentrum.

![Ontbrekende systeemupdate per virtuele machine](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

U kunt meerdere secties hebben op elk tabblad en in elke sectie kunt u een afzonderlijke optie toosee meer informatie over Hallo aanbevolen stappen tooaddress dat specifieke probleem. 

#### <a name="monitoring-recommendations"></a>Aanbevelingen ten aanzien van controle
Deze sectie toont Hallo kunt u het totale aantal virtuele machines die is geïnitialiseerd voor het verzamelen van gegevens en hun huidige status. Nadat alle virtuele machines gegevensverzameling is geïnitialiseerd hebt, worden ze gereed tooreceive Security Center-beveiligingsbeleid. Wanneer u deze vermelding klikt, Hallo **VM-Agent ontbreekt of niet reageert** blade wordt geopend. 

![Ontbrekende systeemupdate per virtuele machine](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Aanbevelingen voor virtuele machines
Dit gedeelte bevat een reeks [aanbevelingen voor elke virtuele machine](security-center-virtual-machine-recommendations.md) die wordt bewaakt door Azure Security Center. de eerste kolom Hallo geeft Hallo aanbeveling. de tweede kolom Hallo toont Hallo kunt u het totale aantal virtuele machines die worden beïnvloed door die aanbeveling. Hallo derde kolom ziet u Hallo ernst van Hallo probleem zoals geïllustreerd in de volgende schermafbeelding Hallo.

![Aanbevelingen voor virtuele machines](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Alleen virtuele machines waarvoor ten minste één openbaar eindpunt worden weergegeven in Hallo **Networking Health** blade in Hallo **netwerktopologie** lijst.
>
>

Elke aanbeveling heeft een set acties die kunnen worden uitgevoerd wanneer u erop klikt. Als u bijvoorbeeld **ontbrekende systeemupdates**, Hallo **ontbrekende systeemupdates** blade wordt geopend. Geeft het Hallo virtuele machines die ontbreken patches en ernst van de ontbrekende update Hallo Hallo zoals weergegeven in de volgende Hallo schermafbeelding.

![Ontbrekende systeemupdates voor virtuele machines](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Hallo **ontbrekende systeemupdates** blade ziet u een tabel met Hallo volgende informatie:

* **VIRTUELE MACHINE**: Hallo-naam van Hallo virtuele machine waarvoor updates ontbreken.
* **SYSTEEMUPDATES**: Hallo aantal systeemupdates dat ontbreekt.
* **TIJD van laatste SCAN**: Hallo tijd dat Security Center voor het laatst gescand Hallo virtuele machine voor updates.
* **STATUS**: huidige status van de aanbeveling Hallo Hallo:
  * **Open**: Hallo aanbeveling is nog niet opgelost.
  * **Bezig**: Hallo aanbeveling wordt momenteel toegepast toothose resources en de door u is geen actie vereist.
  * **Opgelost**: Hallo aanbeveling is al voltooid. (Wanneer het Hallo-probleem is opgelost, Hallo vermelding is beschikbaar).
* **ERNST**: wordt Hallo ernst van deze bepaalde aanbeveling beschreven:
  * **Hoog**: er bestaat een beveiligingsprobleem voor een belangrijke resource (toepassing, virtuele machine, netwerkbeveiligingsgroep) en dit probleem vereist uw aandacht.
  * **Gemiddeld**: niet-kritieke of extra stappen zijn vereist toocomplete een proces of een beveiligingsprobleem elimineren.
  * **Laag**: een beveiligingsprobleem moet worden opgelost, maar dit vereist niet uw onmiddellijke aandacht. (Standaard lage aanbevelingen niet zijn opgenomen, maar u kunt filteren op aanbevelingen als u wilt dat tooview ze.)

tooview hello aanbeveling, klikt u op Hallo-naam van Hallo virtuele machine. Een nieuwe blade voor die virtuele machine wordt geopend Hallo lijst met updates zoals weergegeven in de volgende schermafbeelding Hallo.

![Ontbrekende systeemupdates voor een specifieke virtuele machine](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Hallo hier aanbevelingen voor beveiliging zijn dezelfde als die op Hallo Hallo **aanbevelingen** blade. Zie Hallo [beveiligingsaanbevelingen implementeren in Azure Security Center](security-center-recommendations.md) artikel voor meer informatie over het tooresolve aanbevelingen. Dit is van toepassing is niet alleen voor virtuele machines maar ook voor alle resources die beschikbaar in Hallo zijn **resourcestatus** tegel.
>
>

#### <a name="virtual-machines-section"></a>Sectie voor virtuele machines
Hallo virtuele machines sectie kunt u een overzicht van alle virtuele machines en aanbevelingen. Elke kolom vertegenwoordigt een reeks aanbevelingen, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![Overzicht van alle virtuele machines en aanbevelingen](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

Hallo-pictogram dat wordt weergegeven onder elke aanbeveling helpt u tooquickly identificeren Hallo virtuele machines die aandacht vereisen en het type aanbeveling Hallo.

In het vorige voorbeeld hello heeft één virtuele machine een kritieke aanbeveling met betrekking tot endpoint protection. tooget meer informatie over de virtuele machine hello, klikt u erop. Een nieuwe blade geopend vertegenwoordigt deze virtuele machine, zoals wordt weergegeven in de volgende schermafbeelding Hallo.

![Beveiligingsdetails van virtuele machines](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Deze blade bevat informatie over de beveiliging voor virtuele-machine Hallo Hallo. U kunt zien Hallo aanbevolen actie en de ernst van elk probleem Hallo Hallo onder aan deze blade wordt.

#### <a name="cloud-services-section"></a>Veelgestelde vragen over cloudservices
Een aanbeveling is voor cloud-services gemaakt wanneer Hallo besturingssysteemversie niet actueel is zoals weergegeven in de volgende schermafbeelding Hallo:

![Status van cloudservices](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

In een scenario waar u de aanbeveling (dit is geen aanvraag voor het vorige voorbeeld Hallo Hallo) hebt, moet u toofollow Hallo stappen in Hallo aanbeveling tooupdate Hallo besturingssysteemversie. Wanneer een update beschikbaar is, hebt u een waarschuwing (rood of oranje - afhankelijk Hallo ernst van Hallo probleem). Wanneer u op deze waarschuwing in rijen Hallo WebRole1 (Windows Server wordt uitgevoerd met uw web-app automatisch geïmplementeerd tooIIS) of WorkerRole1 (Windows Server wordt uitgevoerd met uw web-app automatisch geïmplementeerd tooIIS) klikt, wordt een nieuwe blade geopend met meer informatie over deze aanbeveling zoals weergegeven in de volgende schermafbeelding Hallo:

![Details van de cloudservice](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee een meer richtlijnen uitleg over deze aanbeveling, klikt u op **Update besturingssysteemversie** onder Hallo **beschrijving** kolom. Hallo **Update besturingssysteemversie (Preview)** er wordt een blade geopend met meer informatie.

![Aanbevelingen ten aanzien van cloudservices](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Virtuele netwerken bewaken
Wanneer u klikt op **Networking** tegel, hello **Networking** er wordt een blade geopend met meer informatie, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![De blade Netwerken](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Aanbevelingen voor netwerken
Zoals hello statusgegevens van de virtuele machine-resource, biedt deze blade een overzicht van de problemen op Hallo bovenaan de blade Hallo en een lijst met bewaakte netwerken op Hallo onder.

Hallo networking status uitsplitsing sectie geeft een lijst van mogelijke beveiligingsproblemen en biedt [aanbevelingen](security-center-network-recommendations.md). Mogelijke aandachtspunten zijn:

* NGFW (Next Generation Firewall) is niet geïnstalleerd
* De netwerkbeveiligingsgroepen op subnetten zijn niet ingeschakeld
* De netwerkbeveiligingsgroepen op virtuele machines zijn niet ingeschakeld
* Externe toegang via openbaar extern eindpunt beperken
* Status van internetgerichte eindpunten in orde

Wanneer u een aanbeveling klikt, wordt een nieuwe blade geopend met meer informatie over de aanbeveling Hallo zoals weergegeven in het volgende voorbeeld Hallo.

![Details voor een aanbeveling Hallo netwerken blade](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

In dit voorbeeld Hallo **configureren ontbrekende Netwerkbeveiligingsgroepen voor subnetten** blade bevat een lijst met subnetten en virtuele machines die ontbreken-beveiliging voor de groep. Als u Hallo subnet toowhich gewenste tooapply hello netwerkbeveiligingsgroep klikt, wordt er een andere blade geopend.

In Hallo **netwerkbeveiligingsgroep kiezen** blade kunt u Hallo meest geschikte netwerkbeveiligingsgroep voor subnet Hallo selecteren of u kunt een nieuwe netwerkbeveiligingsgroep maken.

#### <a name="internet-facing-endpoints-section"></a>Sectie Internetgerichte eindpunten
In Hallo **internetgerichte eindpunten** sectie ziet u Hallo virtuele machines die momenteel zijn geconfigureerd met een Internetgericht eindpunt en de huidige status.

![Virtuele machines die zijn geconfigureerd met een internetgericht eindpunt en status](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Deze tabel heeft Hallo eindpuntnaam die vertegenwoordigt Hallo virtuele machine, hello Internetgericht IP-adres, en huidige status van de ernst van de netwerkbeveiligingsgroep Hallo Hallo en Hallo NGFW. Hallo-tabel is gesorteerd op ernst:

* Rood (bovenaan): hoge prioriteit en moet onmiddellijk worden opgelost
* Oranje: gemiddelde prioriteit en moet zo snel mogelijk worden opgelost
* Groen (laatste): integriteitsstatus

#### <a name="networking-topology-section"></a>Sectie Netwerktopologie
Hallo **netwerktopologie** sectie heeft een hiërarchische weergave van Hallo resources zoals weergegeven in de volgende schermafbeelding Hallo:

![Hiërarchische weergave van resources in de sectie Netwerktopologie](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Deze tabel is gesorteerd (virtuele machines en subnetten) op ernst:

* Rood (bovenaan): hoge prioriteit en moet onmiddellijk worden opgelost
* Oranje: gemiddelde prioriteit en moet zo snel mogelijk worden opgelost
* Groen (laatste): integriteitsstatus

In deze Topologieweergave bevat het eerste niveau Hallo heeft [virtuele netwerken](../virtual-network/virtual-networks-overview.md), [virtuele netwerkgateways](/vpn-gateway/vpn-gateway-site-to-site-create.md), en [virtuele netwerken (klassiek)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). Hallo tweede niveau bevat subnetten en derde niveau Hallo Hallo virtuele machines die deel uitmaken van toothose subnetten heeft. Hallo rechterkolom heeft Hallo huidige status van netwerkbeveiligingsgroep Hallo voor die resources, zoals aangegeven in Hallo voorbeeld te volgen:

![Status van de netwerkbeveiligingsgroep Hallo in de sectie netwerktopologie](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

Hallo onderste gedeelte van deze blade is Hallo aanbevelingen voor deze virtuele machine die vergelijkbaar is toowhat eerder is beschreven. U kunt een aanbeveling toolearn meer klikt u op of toepassen van beveiligingscontrole Hallo nodig of de configuratie.

### <a name="monitor-storage--data"></a>Opslag en gegevens controleren

Wanneer u klikt op **opslag & gegevens** in Hallo **preventie** sectie hello **gegevensbronnen** er wordt een blade geopend met aanbevelingen voor SQL en opslag. Heeft ook [aanbevelingen](security-center-sql-service-recommendations.md) voor Hallo algemene status van Hallo-database. Lees voor meer informatie over de versleuteling van opslag [Versleuteling inschakelen voor een Azure-opslagaccount in Azure Security Center](security-center-enable-encryption-for-storage-account.md).

![Gegevensbronnen](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

Onder **SQL aanbevelingen**, klikt u op elke aanbeveling en get meer details over verdere actie tooresolve een probleem. Hallo volgende voorbeeld ziet u Hallo uitbreiding van Hallo **Database Auditing en detectie van bedreigingen op SQL-databases** aanbeveling.

![Details over een SQL-aanbeveling](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Hallo **controle inschakelen en detectie van bedreigingen op SQL-databases** blade bevat Hallo volgende informatie:

* Een lijst met SQL-databases
* Hallo-server waarop ze zich bevinden
* Informatie over of deze instelling is overgenomen van Hallo-server of als deze uniek is in deze database is
* de huidige status Hallo
* Hallo ernst van Hallo probleem

Als u deze aanbeveling op Hallo database tooaddress klikt, Hallo **controle en detectie van bedreigingen** blade wordt geopend, zoals weergegeven in het volgende scherm Hallo.

![De blade Controle en detectie van bedreigingen](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

tooenable controle, selecteer **ON** onder Hallo **controle** optie.

### <a name="monitor-applications"></a>Toepassingen bewaken

Als uw Azure-workload toepassingen die zich bevinden [virtuele machines (gemaakt via Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) met ontsloten webpoorten (TCP-poorten 80 en 443), die tooidentify mogelijke beveiligingsproblemen in Security Center worden bewaakt en herstelstappen aan te bevelen. Wanneer u klikt op Hallo **toepassingen** tegel, hello **toepassingen** er wordt een blade geopend met een reeks aanbevelingen in Hallo **toepassing aanbevelingen** sectie. U ziet ook uitsplitsing van de toepassing hello per host/virtueel IP-adres zoals in de volgende schermafbeelding Hallo.

![Beveiligingsstatus van toepassingen](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Net zoals u met hello andere aanbevelingen, klikt u op een aanbeveling toosee meer informatie over Hallo probleem en hoe tooremediate. Hallo voorbeeld in de volgende afbeelding Hallo is een toepassing die als onbeveiligde webtoepassing is geïdentificeerd. Wanneer u Hallo-toepassing die is niet als veilig beschouwd selecteert, wordt een andere blade geopend met Hallo volgende optie die beschikbaar is:

![Meer informatie over een app die is niet beveiligd](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

In deze blade vindt u een lijst met alle aanbevelingen voor deze toepassing. Wanneer u klikt op Hallo **web application firewall toevoegen** aanbeveling, Hallo **Web Application Firewall toevoegen** blade wordt geopend met opties voor u tooinstall web application firewall (WAF) vanaf een partner als weergegeven in de volgende schermafbeelding Hallo.

![Het dialoogvenster Web Application Firewall toevoegen](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe toouse bewakingsmogelijkheden in Azure Security Center. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md): meer informatie over hoe tooconfigure beveiligingsinstellingen in Azure Security Center.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md): meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md): Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.
