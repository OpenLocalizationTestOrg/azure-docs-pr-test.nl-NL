---
title: aaaInstall lokale gegevensgateway - Azure Logic Apps | Microsoft Docs
description: Voordat u toegang gegevensbronnen on-premises tot, Hallo lokale gegevensgateway voor snelle gegevensoverdracht en -versleuteling tussen on-premises gegevensbronnen en logic apps installeren
keywords: toegang tot gegevens, op de lokale, gegevensoverdracht, versleuteling en gegevensbronnen
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Installatie Hallo on-premises gegevensgateway voor Azure Logic Apps

Om uw logische apps toegang on-premises gegevensbronnen tot, moet u het installeren en stel Hallo lokale gegevensgateway. Hallo gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen on-premises systemen en uw logische apps. Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus. Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent. Meer informatie over [de werking van de gegevensgateway Hallo](#gateway-cloud-service).

Hallo-gateway ondersteunt verbindingen toothese gegevensbronnen on-premises:

*   BizTalk Server 2016
*   DB2  
*   Bestandssysteem
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   SAP-toepassingsserver 
*   SAP-berichtenserver
*   SharePoint
*   SQL Server
*   Teradata

Deze stappen laten zien hoe toofirst installeren Hallo lokale gegevensgateway voordat u [instellen van een verbinding tussen Hallo-gateway en uw logische apps](./logic-apps-gateway-connection.md). Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list). 

Zie voor informatie over hoe toouse Hallo gateway met andere services, deze artikelen:

*   [Microsoft Power BI lokale gegevensgateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services op locatie gegevensgateway](../analysis-services/analysis-services-gateway.md)
*   [Microsoft-Flow lokale gegevensgateway](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps lokale gegevensgateway](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Vereisten

**Minimale**:

* .NET 4.5 framework
* 64-bits versie van Windows 7 of Windows Server 2008 R2 (of hoger)

**Aanbevolen**:

* 8-core CPU
* 8 GB geheugen
* 64-bits versie van Windows 2012 R2 (of hoger)

**Belangrijke overwegingen**:

* Hallo lokale gegevensgateway alleen op een lokale computer geïnstalleerd.
U kunt Hallo gateway niet installeren op een domeincontroller.

   > [!TIP]
   > U hebt geen tooinstall Hallo gateway op Hallo dezelfde computer als uw gegevensbron. toominimize latentie, kunt u Hallo gateway zo dicht als mogelijke tooyour gegevensbron, of op Hallo dezelfde installeren computer, ervan uitgaande dat u machtigingen hebt.

* Installeer geen Hallo-gateway op een computer die wordt uitgeschakeld, gaat toosleep of toohello Internet geen verbinding worden gemaakt omdat het Hallo-gateway kan niet worden uitgevoerd in deze omstandigheden. Ook de prestaties van de gateway via een draadloos netwerk kan afnemen.

* Tijdens de installatie, moet u zich aanmelden met een [werk- of schoolaccount](https://docs.microsoft.com/azure/active-directory/sign-up-organization) die wordt beheerd door Azure Active Directory (Azure AD), niet in een Microsoft-account. 

  U hebt toouse Hallo hetzelfde werk of school account later in hello Azure portal maken en koppelen van een gateway-resource met de gateway-installatie. U selecteert deze gateway resource vervolgens wanneer u Hallo verbinding tussen uw logica app en Hallo on-premises gegevensbron maken. [Waarom moet ik een Azure AD werk- of schoolaccount?](#why-azure-work-school-account)

  > [!TIP]
  > Als u zich registreerde voor een Office 365-aanbieding en uw werkelijke Werke-mailadres niet opgeven, uw adres aanmelden als volgt uitzien jeff@contoso.onmicrosoft.com. 

* Als u een bestaande gateway die u hebt ingesteld met een installatieprogramma dat ouder is dan versie 14.16.6317.4 hebt, kunt u uw gateway locatie door actieve Hallo nieuwste installer niet wijzigen. U kunt echter Hallo nieuwste installatieprogramma tooset van een nieuwe gateway met Hallo in plaats daarvan de gewenste locatie.
  
  Als u een gateway-installatieprogramma dat ouder is dan versie 14.16.6317.4 hebben, maar u kunt uw gateway nog niet geïnstalleerd nog, kunt u downloaden en de meest recente installatieprogramma hello gebruiken.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Hallo gegevensgateway installeren

1.  [Downloaden en uitvoeren van het installatieprogramma van Hallo gateway op een lokale computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Lees en accepteer de gebruiksvoorwaarden en de privacyverklaring Hallo.

3. Hallo-pad op de lokale computer waar u tooinstall Hallo gateway wilt opgeven.

4. Wanneer u wordt gevraagd, meld u aan met uw Azure werk- of schoolaccount, niet in een Microsoft-account.

   ![Meld u aan met Azure werk- of schoolaccount](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Nu uw geïnstalleerde gateway registreren met Hallo [gateway-cloudservice](#gateway-cloud-service). Kies **registreren van een nieuwe gateway op deze computer**.

   gateway-cloudservice Hallo versleutelt en slaat de referenties van de gegevensbron en de details van de gateway. 
   Hallo-service stuurt ook query's en de bijbehorende resultaten tussen uw logische app, Hallo lokale gegevensgateway en uw gegevensbron on-premises.

6. Geef een naam voor uw gateway-installatie. Een herstelsleutel maken en bevestig vervolgens uw herstelsleutel. 

   > [!IMPORTANT] 
   > De herstelsleutel moet ten minste acht tekens bevatten. Zorg ervoor dat u opslaat en Hallo-sleutel in een veilige plaats bewaren. Ook moet u deze sleutel als u wilt dat toomigrate, herstellen of overnemen van een bestaande gateway.

   1. toochange hello standaard regio voor Hallo gateway-cloudservice en de Azure Service Bus gebruikt door de installatie van de gateway, kiezen **wijziging regio**.

      ![Wijziging regio](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      Hallo standaard regio is Hallo regio die aan uw Azure AD-tenant zijn gekoppeld.

   2. Open op de volgende deelvenster Hallo Hallo **regio selecteren** een andere regio te kiezen.

      ![Selecteer een andere regio](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Bijvoorbeeld: u selecteert Hallo mogelijk dezelfde regio bevinden als uw logische app, of selecteer Hallo regio dichtstbijzijnde tooyour lokale gegevensbron zodat de latentie te verminderen. Uw gateway en logica voor resource app hebben verschillende locaties.

      > [!IMPORTANT]
      > U kunt deze regio niet wijzigen na de installatie. Dit gebied wordt ook bepaalt en Hallo locatie hier u hello Azure-resource voor uw gateway maken kunt worden beperkt. Wanneer u uw gateway-resource in Azure maakt, zorg er dus Hallo Resourcelocatie komt overeen met Hallo regio die u hebt geselecteerd tijdens de installatie van de gateway.
      > 
      > Als u een andere regio toouse voor uw gateway later wilt, moet u een nieuwe gateway instellen.

   3. Als u klaar bent, kiest u **gedaan**.

7. Nu als volgt te werk in Azure-portal Hallo zodat u kunt [maken van een Azure-resource voor uw gateway](../logic-apps/logic-apps-gateway-connection.md). 

Meer informatie over [de werking van de gegevensgateway Hallo](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Migreren, herstellen of overnemen van een bestaande gateway

tooperform u deze taken, moet u de herstelsleutel Hallo die is opgegeven tijdens het Hallo-gateway is geïnstalleerd hebben.

1. Kies in het menu Start uw computer **On-premises gegevensgateway**.

2. Nadat hello installatieprogramma wordt geopend Meld u aan met hello dezelfde Azure werk- of schoolaccount dat eerder tooinstall Hallo gateway gebruikt.

3. Kies **migreren, herstellen of overnemen van een bestaande gateway**.

4. De naam en herstel sleutel Hallo voor Hallo-gateway die u toomigrate, herstellen of nemen via wilt opgeven.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Hallo-gateway opnieuw starten

Hallo-gateway als een Windows-service wordt uitgevoerd. Net als elke andere Windows-service, kunt u starten en stoppen van service Hallo op verschillende manieren. U kunt bijvoorbeeld open een opdrachtprompt met verhoogde machtigingen op Hallo-computer waarop het Hallo-gateway wordt uitgevoerd, en beide deze opdrachten uitvoeren:

* toostop hello service, die deze opdracht uitvoeren:
  
    `net stop PBIEgwService`

* toostart hello service, die deze opdracht uitvoeren:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Windows-serviceaccount

Hallo lokale gegevensgateway is ingesteld op toouse `NT SERVICE\PBIEgwService` voor Windows hello service aanmeldingsreferenties. Hallo gateway heeft standaard Hallo 'Aanmelden als service' rechts voor Hallo machine waarop u Hallo-gateway installeert.

> [!NOTE]
> Hallo Windows-service-account verschilt van Hallo account dat wordt gebruikt voor het verbinden van tooon-premises gegevensbronnen en van hello Azure werk of schoolaccount gebruikt toosign in toocloud services.

## <a name="configure-a-firewall-or-proxy"></a>Een firewall of proxy configureren

Hallo-gateway maakt een uitgaande verbinding te [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). proxy-informatie voor uw gateway tooprovide Zie [proxy-instellingen configureren](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck of uw firewall of proxy, kan verbindingen blokkeren, Controleer of uw machine daadwerkelijk verbinding kunt maken van toohello internet en Hallo [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). Vanuit een PowerShell-prompt, moet u deze opdracht uitvoeren:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Met deze opdracht wordt enkel tests netwerkverbinding en connectiviteit toohello Azure Service Bus. Zodat het Hallo-opdracht heeft niets toodo met Hallo gateway of Hallo gateway-cloudservice die versleutelt en slaat uw referenties en de details van de gateway. 
>
> Ook deze opdracht is alleen beschikbaar op Windows Server 2012 R2 of hoger, en Windows 8.1 of hoger. In eerdere versies van het besturingssysteem, kunt u Telnet-connectiviteit te testen. Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Uw resultaten ziet vergelijkbaar toothis voorbeeld:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Als **TcpTestSucceeded** is niet ingesteld te**True**, u mogelijk geblokkeerd door een firewall. Als u wilt dat uitgebreide toobe, vervangende Hallo **ComputerName** en **poort** waarden met Hallo waarden die worden vermeld onder [poorten configureren](#configure-ports) in dit onderwerp.

Hallo firewall blokkeren mogelijk de ook verbindingen die hello die Azure Service Bus toohello Azure-datacenters maakt. Als u dit scenario gebeurt, goedkeuren (deblokkeren) alle Hallo IP-adressen voor deze datacentra in uw regio. Voor deze IP-adressen [get hello Azure lijst IP-adressen hier](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Poorten configureren

Hallo-gateway maakt een uitgaande verbinding te[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) en op uitgaande poorten communiceert: TCP 443 (standaard), 5671, 5672, 9350 via 9354. Hallo-gateway nodig niet poorten voor inkomend verkeer. Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| DOMEINNAMEN | UITGAANDE POORTEN | BESCHRIJVING |
| --- | --- | --- |
| *. analysis.windows.net | 443 | HTTPS | 
| *. login.windows.net | 443 | HTTPS | 
| *. servicebus.windows.net | 5671-5672 | Geavanceerde Message Queuing-Protocol (AMQP) | 
| *. servicebus.windows.net | 443, 9350-9354 | Listeners op Service Bus Relay via TCP (443 voor toegangsbeheer token aanschaf vereist) | 
| *. frontend.clouddatahub.net | 443 | HTTPS | 
| *. core.windows.net | 443 | HTTPS | 
| Login.microsoftonline.com | 443 | HTTPS | 
| *. msftncsi.com | 443 | Verbinding met internet tootest gebruikt wanneer Hallo gateway onbereikbaar via Hallo Power BI-service is. | 

Als u tooapprove IP-adressen in plaats van Hallo domeinen hebt, kunt u downloaden en gebruiken van Hallo [Microsoft Azure Datacenter IP-adresbereiken lijst](https://www.microsoft.com/download/details.aspx?id=41653). In sommige gevallen bestaan hello Azure Service Bus-verbindingen met IP-adres in plaats van een volledig gekwalificeerde domeinnamen.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Hoe werkt de gegevensgateway Hallo?

Hallo gegevensgateway vergemakkelijkt de snel en veilig communicatie tussen uw logische app, Hallo gateway-cloudservice en uw on-premises gegevensbron. 

![diagram-for-on-premises-Data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Dus als gebruiker in de cloud Hallo Hallo communiceert met een element dat is verbonden tooyour lokale gegevensbron:

1. Hallo gateway-cloudservice maakt van een query, samen met de Hallo versleuteld referenties voor gegevensbron hello, en stuurt Hallo query toohello wachtrij voor Hallo gateway tooprocess.

2. gateway-cloudservice Hallo Hallo query analyseert en pushes Hallo aanvraag toohello Azure Service Bus.

3. Hallo lokale gegevensgateway hello Azure Service Bus voor aanvragen in behandeling worden opgevraagd.

4. Hallo gateway Hallo query opgehaald, ontsleutelt Hallo referenties en toohello-gegevensbron is verbonden met deze referenties.

5. Hallo gateway verzendt Hallo toohello querygegevensbron voor uitvoering.

6. Hallo resultaten worden van de gegevensbron hello, toohello back-gateway en toohello gateway-cloudservice verzonden. Hallo gateway-cloudservice gebruikt vervolgens Hallo resultaten.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="general"></a>Algemeen

**Q**: moet ik een gateway voor gegevensbronnen in de cloud hello, zoals SQL Azure? <br/>
**Een**: Nee. Een gateway maakt verbinding alleen tooon-premises gegevensbronnen.

**Q**: heeft Hallo gateway geïnstalleerd op dezelfde computer als de gegevensbron Hallo Hallo toobe? <br/>
**Een**: Nee. Hallo-gateway wordt verbonden toohello-gegevensbron Hallo verbindingsgegevens die is opgegeven. Hallo gateway beschouwen als een client-toepassing in deze zin. Hallo-gateway moet net Hallo mogelijkheid tooconnect toohello servernaam die is opgegeven.

<a name="why-azure-work-school-account"></a>

**Q**: Waarom moet ik een Azure werk- of schoolaccount account toosign in? <br/>
**Een**: U kunt alleen een Azure werk- of schoolaccount wanneer u Hallo lokale gegevensgateway installeert. Uw account wordt opgeslagen in een tenant die wordt beheerd door Azure Active Directory (Azure AD). Uw Azure AD-account UPN (user Principal name) normaal gesproken komt overeen met Hallo e-mailadres.

**Q**: waar mijn referenties worden opgeslagen? <br/>
**Een**: Hallo-referenties die u voor een gegevensbron opgeeft zijn versleuteld en opgeslagen in Hallo gateway-cloudservice. Hallo-referenties worden op Hallo lokale gegevensgateway ontsleuteld.

**Q**: zijn er vereisten voor de bandbreedte van het netwerk? <br/>
**Een**: het is raadzaam dat de netwerkverbinding goed doorvoer heeft. Elke omgeving is verschillend en Hallo hoeveelheid verzonden gegevens heeft op Hallo resultaten. Met behulp van ExpressRoute kan helpen bij het tooguarantee een mate van doorvoer tussen on-premises en hello Azure-datacenters.
U kunt uw doorvoer Hallo hulpprogramma van derden Azure snelheid testen app toohelp meter.

**Q**: Wat is er Hallo latentie voor actieve query's tooa gegevensbron van Hallo gateway? Wat is de beste architectuur Hallo? <br/>
**Een**: tooreduce netwerklatentie, Hallo-gateway installeren als de gegevensbron sluiten toohello mogelijk. Als u Hallo gateway op de werkelijke gegevensbron hello installeren kunt, minimaliseert deze nabijheid Hallo latentie geïntroduceerd. Hallo datacenters te overwegen. Bijvoorbeeld, als Hallo VS-West datacenter maakt gebruik van uw service en u SQL Server gehost in een virtuele machine in Azure hebt, moet uw virtuele Azure-machine Hallo VS-West te. Deze nabijheid minimaliseert latentie en vermijdt u kosten voor uitgaande op Hallo Azure VM.

**Q**: hoe worden resultaten verzonden back toohello cloud? <br/>
**Een**: resultaten worden verzonden via hello Azure Service Bus.

**Q**: zijn er inkomende verbindingen toohello gateway vanuit de cloud Hallo? <br/>
**Een**: Nee. Hallo-gateway gebruikt uitgaande verbindingen tooAzure Service Bus.

**Q**: Wat gebeurt er als ik uitgaande verbindingen blokkeren? Wat kan ik tooopen nodig? <br/>
**Een**: Zie Hallo poorten en hosts die Hallo gateway gebruikt.

**Q**: de werkelijke Windows-service Hallo zogenaamd?<br/>
**Een**: In de Services Hallo gateway Power BI Enterprise Gateway-Service wordt aangeroepen.

**Q**: kunt Hallo gateway Windows-service uitvoert met een Azure Active Directory-account? <br/>
**Een**: Nee. Hallo Windows-service moet een geldige Windows-account hebben. Standaard is Hallo-service wordt uitgevoerd met Hallo Service-SID NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Hoge beschikbaarheid en herstel na noodgevallen

**Q**: welke opties zijn beschikbaar voor herstel na noodgevallen? <br/>
**Een**: U kunt gebruiken Hallo herstel sleutel toorestore of verplaatsen van een gateway. Wanneer u Hallo-gateway installeert, geef Hallo herstelsleutel.

**Q**: Wat is Hallo voordeel van de herstelsleutel Hallo? <br/>
**Een**: Hallo herstelsleutel biedt een manier toomigrate of de gateway-instellingen herstellen na een noodgeval.

**Q**: zijn er plannen voor het inschakelen van scenario's voor hoge beschikbaarheid met Hallo gateway? <br/>
**Een**: de volgende scenario's op Hallo roadmap, maar we een tijdlijn nog geen hebt.

## <a name="troubleshooting"></a>Problemen oplossen

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Q**: hoe kan ik zien welke query toohello on-premises gegevensbron worden verzonden? <br/>
**Een**: U kunt inschakelen querytracering, waaronder het Hallo-query's die worden verzonden. Houd er rekening mee toochange query tracering van de oorspronkelijke waarde toohello gedaan bij het oplossen van problemen. Querytracering ingeschakeld verlaten maakt grotere Logboeken.

U kunt ook hulpprogramma's die de gegevensbron voor tracering van query's heeft bekijken. U kunt bijvoorbeeld de Extended Events of SQL Profiler gebruiken voor SQL Server en Analysis Services.

**Q**: waar zich de gateway-logboeken Hallo? <br/>
**Een**: Zie's verderop in dit onderwerp.

### <a name="update-toohello-latest-version"></a>Meest recente versie van de update toohello

Veel problemen kunnen surface wanneer Hallo gatewayversie verouderd. Zorg ervoor dat u met de meest recente versie Hallo als goed over het algemeen. Als u dit nog niet hebt Hallo gateway voor een maand of langer bijgewerkt, kunt u Overweeg de installatie van de meest recente versie van gateway Hallo Hallo en zien als u Hallo probleem kan reproduceren.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Fout: Kan tooadd gebruiker toogroup. (-2147463168 PBIEgwService Prestatielogboekgebruikers)

U kunt deze fout kan ophalen, als u probeert tooinstall Hallo gateway op een domeincontroller wordt niet ondersteund. Zorg ervoor dat u Hallo-gateway op een computer die een domeincontroller niet implementeert.

## <a name="tools"></a>Hulpprogramma's

### <a name="collect-logs-from-hello-gateway-configurer"></a>Verzamelen van Logboeken van Hallo gateway configurer

U kunt verschillende logboeken voor Hallo gateway verzamelen. Begin altijd met Hallo Logboeken!

#### <a name="installer-logs"></a>Installatieprogramma Logboeken

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Configuratielogboeken

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Enterprise gateway-service-Logboeken

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Gebeurtenislogboeken

U vindt Hallo Data Management Gateway en PowerBIGateway Logboeken onder **servicelogboeken voor toepassingen en**.

### <a name="fiddler-trace"></a>Fiddler traceren

[Fiddler](http://www.telerik.com/fiddler) is een gratis hulpprogramma uit Telerik die HTTP-verkeer wordt bewaakt. U kunt dit verkeer met Power BI-service vanaf de clientcomputer Hallo Hallo zien. Deze service mogelijk fouten en andere gerelateerde informatie weergeven.

## <a name="next-steps"></a>Volgende stappen
    
* [Verbinding maken met tooon-premises gegevens vanuit logic apps](../logic-apps/logic-apps-gateway-connection.md)
* [Enterprise integration-functies](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Connectors voor Azure Logic Apps](../connectors/apis-list.md)
