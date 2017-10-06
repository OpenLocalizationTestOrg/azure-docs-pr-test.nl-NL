---
title: overzicht van de verbindingen aaaHybrid | Microsoft Docs
description: Meer informatie over hybride verbindingen, beveiliging, TCP-poorten en ondersteunde configuraties. MABS, WABS.
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Overzicht van hybride verbindingen

> [!IMPORTANT]
> Hybrid Connections van BizTalk is buiten gebruik gesteld en vervangen door App Service Hybrid Connections. Voor meer informatie, inclusief hoe toomanage uw bestaande BizTalk hybride verbindingen, Zie [Azure App Service hybride verbindingen](../app-service/app-service-hybrid-connections.md).

Inleiding tooHybrid verbindingen, ziet u de Hallo ondersteunde configuraties en lijsten Hallo vereiste TCP-poorten.

## <a name="what-is-a-hybrid-connection"></a>Wat is een hybride verbinding?
Hybride verbindingen zijn een functie van Azure BizTalk Services. Hybride verbindingen bieden een eenvoudige en handige manier tooconnect Hallo Web-Apps functies in Azure App Service (voorheen Websites) en Hallo Mobile Apps in Azure App Service (voorheen Mobile Services) tooon-premises resources achter de firewall.

![Hybride verbindingen][HCImage]

De voordelen van hybride verbindingen zijn onder andere:

* Web-apps en mobiele apps hebben beveiligde toegang tot bestaande on-premises gegevens en services.
* Meerdere Web-Apps of mobiele Apps kunnen een hybride verbinding tooaccess een on-premises resource delen.
* Minimale TCP-poorten zijn vereist tooaccess uw netwerk.
* Toepassingen die gebruikmaken van hybride verbindingen toegang tot alleen Hallo specifieke on-premises resource die is gepubliceerd via Hallo hybride verbinding.
* Verbinding kunnen maken tooany on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices.
  
  > [!NOTE]
  > TCP-services die gebruikmaken van dynamische poorten (zoals de passieve modus van FTP of de uitgebreide passieve modus), worden momenteel niet ondersteund. LDAP wordt evenmin ondersteund. LDAP gebruikt een statische TCP-poort, maar kan ook UDP gebruiken. Als gevolg hiervan wordt LDAP niet ondersteund.
  > 
  > 
* Geschikt voor gebruik met alle frameworks die worden ondersteund door web-apps (.NET, PHP, Java, Python, Node.js) en mobiele apps (Node.js, .NET).
* Web-Apps en mobiele Apps toegang krijgen tot lokale bronnen in exact Hallo dezelfde manier als Hallo Web of mobiele Apps bevindt zich op uw lokale netwerk. Hallo bijvoorbeeld dezelfde verbindingsreeks gebruikte lokale kunnen ook worden gebruikt in Azure.

Hybride verbindingen bieden ook Ondernemingsadministrators met besturingselement en de zichtbaarheid van bedrijfsbronnen Hallo waartoe hybride toepassingen, waaronder:

* Met instellingen voor Groepsbeleid,-beheerders kunnen hybride verbindingen toestaan op Hallo netwerk en bronnen die toegankelijk zijn voor hybride toepassingen ook aanwijzen.
* Gebeurtenis- en auditlogboeken logboeken op Hallo bedrijfsnetwerk bieden inzicht in Hallo resources waartoe hybride verbindingen.

## <a name="example-scenarios"></a>Voorbeeldscenario 's
Hybride verbindingen ondersteunen de volgende combinaties van framework en toepassing hello:

* .NET framework toegang tooSQL Server
* .NET framework toegang tooHTTP/HTTPS-services met WebClient
* PHP toegang tooSQL Server, MySQL
* Java toegang tooSQL Server, MySQL en Oracle
* Java-toegang tooHTTP/HTTPS-services

Overweeg bij het gebruik hybride verbindingen tooaccess on-premises SQL Server, Hallo volgende:

* Exemplaren van SQL Express met de naam moet geconfigureerde toouse statische poorten. Standaard gebruiken benoemde exemplaren van SQL Express dynamische poorten.
* Benoemde exemplaren van SQL Express gebruiken een statische poort, maar TCP moet zijn ingeschakeld. TCP is standaard niet ingeschakeld.
* Wanneer u clusters of beschikbaarheidsgroepen gebruikt, Hallo `MultiSubnetFailover=true` modus wordt momenteel niet ondersteund.
* Hallo `ApplicationIntent=ReadOnly` wordt momenteel niet ondersteund.
* SQL-verificatie mogelijk vereist als Hallo end-to-end-autorisatiemethode ondersteund door Azure-toepassing hello en Hallo lokale SQL server.

## <a name="security-and-ports"></a>Beveiliging en poorten
Hybride verbindingen gebruiken een Shared Access Signature (SAS) autorisatie toosecure Hallo verbindingen van hello Azure-toepassingen en Hallo on-premises hybride Verbindingsbeheer toohello hybride verbinding. Aparte verbindingssleutels worden gemaakt voor de toepassing hello en Hallo on-premises hybride Verbindingsbeheer. Deze verbindingssleutels kunnen onafhankelijk van elkaar worden geactiveerd en ingetrokken.

Hybride verbindingen zorgen voor naadloze en veilige distributie van Hallo sleutels toohello toepassingen en Hallo on-premises hybride Verbindingsbeheer.

Zie [Hybride verbindingen maken en beheren](integration-hybrid-connection-create-manage.md).

*Autorisatie van toepassingen verloopt gescheiden van hybride verbinding Hallo*. U kunt elke willekeurige geschikte autorisatiemethode gebruiken. Hallo-autorisatiemethode is afhankelijk van Hallo end-to-end-autorisatiemethoden ondersteund tussen hello Azure-cloud- en Hallo on-premises onderdelen. Stel dat uw Azure-toepassing toegang heeft tot een on-premises SQL Server. In dit scenario mogelijk SQL-autorisatie Hallo autorisatiemethode die ondersteunde end-to-end.

#### <a name="tcp-ports"></a>TCP-poorten
Hybride verbindingen vereisen alleen een uitgaande TCP- of HTTP-verbinding vanuit uw privénetwerk. U geen tooopen hoeft geen firewallpoorten of wijzigen van uw netwerk perimeter configuratie tooallow binnenkomende verbindingen in uw netwerk.

Hallo volgende TCP-poorten worden gebruikt door hybride verbindingen:

| Poort | Waarom u het nodig hebt |
| --- | --- |
| 9350 - 9354 |Deze poorten worden gebruikt voor gegevensoverdracht. Hallo Service Bus relay-manager test poort 9350 toodetermine als TCP-verbinding beschikbaar is. Als deze beschikbaar is, wordt ervan uitgegaan dat ook poort 9352 beschikbaar is. Het gegevensverkeer wordt via poort 9352 geleid. <br/><br/>Sta uitgaande verbindingen toothese poorten toe. |
| 5671 |Wanneer poort 9352 wordt gebruikt voor gegevensverkeer, wordt poort 5671 gebruikt als besturingskanaal Hallo. <br/><br/>Sta uitgaande verbindingen toothis poort toe. |
| 80, 443 |Deze poorten worden gebruikt voor een aantal gegevens aanvragen tooAzure. Ook als de poorten 9352 en 5671 zijn niet beschikbaar zijn, *vervolgens* poorten 80 en 443 Hallo alternatieve poorten die worden gebruikt voor gegevensoverdracht en het besturingskanaal Hallo zijn.<br/><br/>Sta uitgaande verbindingen toothese poorten toe. <br/><br/>**Opmerking** niet toouse aanbevolen deze als alternatieve poorten in plaats van Hallo Hallo TCP-poorten. Hallo HTTP/WebSocket gebruikt als Hallo-protocol in plaats van systeemeigen TCP voor gegevenskanalen. Dit kan leiden tot lagere prestaties. |

## <a name="next-steps"></a>Volgende stappen
[Hybride verbindingen maken en beheren](integration-hybrid-connection-create-manage.md)<br/>
[Verbinding maken met Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Verbinding maken met tooon lokale SQL Server uit een Azure-web-app](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Zie ook
[REST-API voor het beheren van BizTalk Services op Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md)<br/>
[Een BizTalk-service maken met Azure Portal](biztalk-provision-services.md)<br/>
[BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
