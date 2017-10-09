---
title: aaaProtect persoonlijke gegevens met Azure-netwerk beveiligingsfuncties | Microsoft Docs
description: Persoonlijke gegevens beschermen met beveiligingsfuncties van Azure-netwerk
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Persoonlijke gegevens beschermen met netwerkbeveiligingsfuncties: Azure Application Gateway en Netwerkbeveiligingsgroepen

Dit artikel bevat informatie en procedures die u kunt Azure Application Gateway en Netwerkbeveiligingsgroepen tooprotect persoonlijke gegevens gebruiken.

Een belangrijk aspect vormt in een meerlaagse beveiliging strategie tooprotect Hallo privacy van persoonlijke gegevens is een beveiliging tegen misbruik van algemene beveiligingsproblemen zoals SQL-injectie of cross-site scripting. Houden ongewenste netwerkverkeer buiten uw virtuele Azure-netwerk biedt bescherming tegen mogelijke inbreuk op gevoelige gegevens en Microsoft Azure biedt u hulpprogramma's voor toohelp uw gegevens beschermen tegen kwaadwillende personen.

## <a name="scenario"></a>Scenario

Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden. Ter bevordering van deze inspanningen deze heeft verkregen verschillende kleinere Blader regels op basis van Italië, Duitsland, Denemarken en Hallo Verenigd Koninkrijk

Hallo bedrijf gebruikmaakt van Microsoft Azure toostore zakelijke gegevens in Hallo cloud en toepassingen worden uitgevoerd op virtuele machines die worden verwerkt en toegang tot deze gegevens. Deze gegevens omvatten persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase. Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties. Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.

Zakelijke werknemers toegang Hallo netwerk van de externe kantoren en reizen agents zich Hallo wereld Hallo van het bedrijf hebben toegang tot toosome bedrijfsbronnen en webtoepassingen die worden gehost in Azure Virtual machines toointeract met het gebruik.

## <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf dient Hallo privacy van klanten te beschermen en persoonlijke gegevens van de werknemers van aanvallers die schadelijke software beveiligingslekken toorun schadelijke code die persoonlijke gegevens worden namelijk blootgesteld opgeslagen of gebruikt door van het bedrijf Hallo cloud-gebaseerde toepassingen.

## <a name="company-goal"></a>Bedrijf-doel

Hallo van bedrijf doel tooensure dat personen onbevoegde geen toegang tot zakelijke Azure virtuele netwerken en Hallo toepassingen en gegevens die door misbruik van veelvoorkomende beveiligingslekken in staan. 

## <a name="solutions"></a>Oplossingen

Microsoft Azure biedt beveiliging mechanismen toohelp wordt voorkomen dat ongewenste verkeer Azure Virtual Networks invoeren. Beheer van binnenkomende en uitgaande verkeer wordt normaal uitgevoerd door firewalls. In Azure, kunt u Hallo Application Gateway met Hallo Web Application Firewall en Netwerkbeveiligingsgroep groepen (NSG), die als een eenvoudige gedistribueerde firewall fungeren. Deze hulpprogramma's kunnen u toodetect en ongewenste netwerkverkeer blokkeren.

### <a name="application-gatewayweb-application-firewall"></a>Application Gateway of Web Application Firewall

Hallo [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) onderdeel Hallo [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) webtoepassingen zijn steeds meer doelen van aanvallen die gebruikmaken van algemene bekende beveiligt beveiligingsproblemen. Een gecentraliseerde WAF wordt beschermd tegen aanvallen via Internet door en beveiligingsbeheer zonder eventuele wijzigingen in de toepassing.

Azure WAF adressen verschillende aanval categorieën inclusief SQL-injectie, cross-site scripting schendingen van HTTP-protocol en afwijkingen, bots, crawlers, scanners, veelvoorkomende onvolkomenheden in de toepassing, HTTP-Denial of Service en andere algemene aanvallen, zoals het invoegen van de opdracht HTTP-aanvraag ' smokkelen ', HTTP-antwoord splitsen en extern bestand insluiting aanvallen. 

U kunt een toepassingsgateway maken met WAF of WAF tooan bestaande toepassingsgateway toevoegen. Azure Application Gateway vereist in beide gevallen moet een eigen subnet.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Hoe maak ik een toepassingsgateway met WAF? 

een nieuwe toepassingsgateway met WAF ingeschakeld, toocreate Hallo te volgen:

1. Log in toohello Azure-portal en in Hallo **Favorieten** deelvenster van de portal hello, klikt u op **nieuw**

2. In Hallo **nieuw** blade, klikt u op **Networking**.

3. Klik op **toepassingsgateway**.

4. Navigeer toohello Azure-portal **klikt u op nieuw \> Networking \> Application Gateway.**

   ![Toepassingsgateways maken](media/protect-netsec/app-gateway-01.png)

5. In Hallo **basisbeginselen** blade die wordt weergegeven, Hallo waarden opgeven voor de volgende velden Hallo: naam, laag SKU (Standard of WAF)-grootte (klein, middelgroot of groot), aantal (2 voor hoge beschikbaarheid)-instantie abonnement, resourcegroep, en Locatie.

6. In Hallo **instellingen** blade die wordt weergegeven onder **virtueel netwerk**, klikt u op **Kies een virtueel netwerk**. Deze stap wordt geopend Voer Hallo de blade virtueel netwerk kiezen.

7. Klik op **nieuw** tooopen hello **virtueel netwerk maken** blade.

8. Voer Hallo volgende waarden: naam, de adresruimte, subnetnaam, adres-subnetbereik. Klik op **OK**.

9. Op Hallo **instellingen** blade onder **Frontend IP-configuratie**, kies type Hallo IP-adres.

10. Klik op **Kies een openbaar IP-adres** vervolgens **nieuwe maken.**

11. Accepteer de standaardwaarde hello, en klik op **OK.**

12. Op Hallo **instellingen** blade onder **listenerconfiguratie**, selecteer toouse HTTP of HTTPS onder **Protocol**. toouse HTTPS, een certificaat is vereist.

13. Configureren met specifieke instellingen Hallo WAF: **Firewall-status** (**ingeschakeld**) en **firewallmodus** (**preventie**). Als u ervoor kiest **detectie** Hallo-modus wordt alleen verkeer vastgelegd.

14. Bekijk Hallo **samenvatting** pagina en klik op **OK**. Hallo application gateway is nu in de wachtrij geplaatst en gemaakt.

Nadat de toepassingsgateway Hallo is gemaakt, kunt u navigeren tooit in Hallo-portal en gaan met de configuratie van de toepassingsgateway Hallo.

![gemaakte toepassingsgateway](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>Hoe kan ik WAF tooan bestaande toepassing toevoegen

een bestaande toepassing gateway toosupport WAF tooupdate in de modus voor preventie Hallo te volgen:

1. In de Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**.

2. Klik op bestaande Application Gateway in Hallo Hallo **alle resources** blade. 
>[!NOTE]
Opmerking: Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u Hallo naam opgeven in Hallo Filter met de naam... vak tooeasily toegang Hallo DNS-zone.
3. Klik op **Web application firewall** en instellingen voor de toepassingsgateway Hallo bijwerken: **tooWAF laag Upgrade** (ingeschakeld) **Firewall-status** (ingeschakeld)  **Firewallmodus** (preventie). U moet ook tooconfigure Hallo regelset en uitgeschakelde regels configureren.

Voor meer informatie over het gedetailleerde toocreate een nieuwe toepassingsgateway met WAF en hoe tooadd WAF tooan bestaande application gateway, Zie [een toepassingsgateway met web application firewall maken met behulp van Hallo-portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen

Een [netwerkbeveiligingsgroep](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources te verbonden[Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet). Nsg's kunnen worden gekoppeld toosubnets of afzonderlijke virtuele machines. Wanneer een NSG gekoppeld tooa subnet is, Hallo regels van toepassing tooall bronnen verbonden toohello subnet. Verkeer kan verder worden beperkt door het ook een NSG tooa VM of NIC koppelen

Nsg's bevatten vier eigenschappen: naam, regio, resourcegroep en regels.
>[!Note]
Hoewel een NSG in een resourcegroep bestaat, gekoppelde tooresources in elke willekeurige resourcegroep kan zijn, zolang het Hallo-resource maakt deel uit van Hallo dezelfde Azure-regio als Hallo NSG.

NSG-regels negen eigenschappen bevatten: naam, het Protocol (TCP, UDP of \*, waaronder ICMP als UDP en TCP), bron poortbereik, doelpoortbereik, bronadres voorvoegsel, doel-adresvoorvoegsel, richting (inkomend of uitgaand), () prioriteit tussen 100 en 4096) en toegang tot type (toestaan of weigeren). Alle nsg's bevatten een set met standaardregels die kan worden verwijderd of overschreven door het Hallo-regels die u maakt.

#### <a name="how-do-i-implement-nsgs"></a>Hoe ik nsg's implementeren?

Nsg's implementeert vereist plannen en er zijn verschillende ontwerpoverwegingen, moet u tootake rekening. Deze omvatten beperkingen met betrekking tot Hallo aantal nsg's per abonnement en -regels per NSG; 'S VNet en subnetten ontwerpen, speciale regels, ICMP-verkeer, isolatie van lagen met subnetten, load balancers en meer.

Zie voor meer richtlijnen bij het plannen en implementeren van nsg's en een voorbeeld implementatiescenario [filteren van netwerkverkeer met netwerkbeveiligingsgroepen.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Hoe maak ik regels in een NSG

toocreate regels in een bestaande NSG voor binnenkomende verbindingen, Hallo te volgen:

1. Klik op **Bladeren**, en vervolgens **Netwerkbeveiligingsgroepen**.

2. Klik in de lijst Hallo van nsg's, op **NSG-FrontEnd**, en vervolgens **inkomende beveiligingsregels voor verbindingen.**

3. Klik in lijst Hallo van inkomende beveiligingsregels op **toevoegen.**

4. Hallo waarden invoeren in de volgende velden Hallo: naam, prioriteit, bron, Protocol, bron-bereik, bestemming bestemming poortbereik en in te grijpen.

Hallo nieuwe regel wordt weergegeven in het NSG Hallo na enkele seconden.

![netwerkbeveiligingsregels](media/protect-netsec/inbound-security.png)

Zie voor meer instructies voor hoe toocreate nsg's op subnetten, regels maken en een NSG koppelen aan een subnet front-end en back-end [netwerkbeveiligingsgroepen met hello Azure-portal maken.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Volgende stappen

[Azure-netwerkbeveiliging](https://azure.microsoft.com/blog/azure-network-security/)

[Aanbevolen beveiligingsprocedures voor Azure-netwerk](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Informatie over een netwerkbeveiligingsgroep ophalen](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
