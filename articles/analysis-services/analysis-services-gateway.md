---
title: de gegevensgateway aaaOn-premises | Microsoft Docs
description: Een On-premises gateway is nodig als uw Analysis Services-server in Azure maakt verbinding met tooon-premises gegevensbronnen.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Tooon-premises gegevensbronnen verbinden met Azure On-premises Data Gateway
Hallo lokale gegevensgateway fungeert als een brug, bieden veilige gegevensoverdracht tussen uw Azure Analysis Services-servers in Hallo cloud en on-premises gegevensbronnen. Toevoeging tooworking met meerdere Azure Analysis Services-servers in Hallo werkt dezelfde regio, de meest recente versie van gateway Hallo Hallo ook met Azure Logic Apps, Power BI, Power-Apps en Microsoft-Flow. U kunt meerdere services in Hallo koppelen dezelfde regio met een enkele gateway. 

 Azure Analysis Services is een gateway-bron in Hallo vereist dezelfde regio. Als u Azure Analysis Services-servers in de regio VS-Oost 2 Hallo hebt, moet u bijvoorbeeld een gateway-bron in de regio VS-Oost 2 Hallo. Meerdere servers in VS-Oost 2 Hallo kunnen gebruiken dezelfde gateway.

Uitvoeren van setup Hallo gateway Hello eerst is een vierdelige proces:

- **Downloaden en uitvoeren van setup** -deze stap installeert u een gatewayservice op een computer in uw organisatie.

- **Registreren van uw gateway** - In deze stap maakt u een naam opgeven en herstel van belangrijke voor uw gateway, en selecteer een regio, uw gateway registreren met Hallo Gateway-Cloudservice.

- **Een gateway-resource maken in Azure** -In deze stap maakt u een gateway-bron in uw Azure-abonnement.

- **Verbinding maken met uw servers tooyour gateway resource** -zodra u een gateway-bron in uw abonnement hebt, kunt u beginnen uw tooit servers verbinding te maken.

Zodra u een resource gateway is geconfigureerd voor uw abonnement hebt, kunt u meerdere servers en andere services tooit. U alleen een andere gateway tooinstall nodig hebt en aanvullende gatewayresources maken als u servers of andere services in een andere regio.

Zie tooget meteen gestart [installeren en configureren van lokale gegevensgateway](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Hoe het werkt
Hallo-gateway die u op een computer in uw organisatie installeert wordt uitgevoerd als een Windows-service **On-premises gegevensgateway**. Deze lokale service is geregistreerd bij Hallo Gateway Cloud Service via Azure Service Bus. Vervolgens maakt u een gateway resource Gateway-Cloudservice voor uw Azure-abonnement. Uw Azure analyseservices-servers zijn vervolgens verbonden tooyour gateway resource. Wanneer modellen op uw server nodig tooconnect tooyour on-premises gegevensbronnen voor query's of verwerking wordt een query's en stroom traverses Hallo gateway resource, Azure Service Bus Hallo gatewayservice voor lokale lokale gegevens en uw gegevensbronnen. 

![Hoe werkt het?](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Query's en gegevensstroom:

1. Een query is gemaakt door Hallo-cloudservice met de Hallo versleuteld referenties voor Hallo on-premises gegevensbron. Deze heeft vervolgens tooa wachtrij voor Hallo gateway tooprocess verzonden.
2. Hallo gateway-cloudservice Hallo query analyseert en duwt Hallo aanvraag toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. Hallo lokale gegevensgateway hello Azure Service Bus voor aanvragen in behandeling worden opgevraagd.
4. Hallo gateway Hallo query opgehaald, ontsleutelt Hallo referenties en gegevensbronnen toohello is verbonden met deze referenties.
5. Hallo gateway verzendt Hallo toohello querygegevensbron voor uitvoering.
6. Hallo resultaten worden verzonden in gegevensbron hello, toohello back-gateway, en klik vervolgens op het Hallo-cloudservice en de server.

## <a name="windows-service-account"></a>Windows-serviceaccount
Hallo lokale gegevensgateway is geconfigureerde toouse *NT SERVICE\PBIEgwService* voor de aanmeldingsreferenties voor Hallo Windows-service. Deze heeft standaard Hallo rechts aanmelden als service; in de context van de Hallo van Hallo-machine die u installeert Hallo-gateway op. Deze referentie wordt niet Hallo dezelfde account die wordt gebruikt tooconnect tooon-premises gegevensbronnen of uw Azure-account.  

Als u problemen met de proxyserver vanwege ondervindt tooauthentication, kunt u toochange Windows hello service account tooa domeingebruiker of beheerd serviceaccount.

## <a name="ports"></a>Poorten
Hallo-gateway maakt een uitgaande verbinding tooAzure Service Bus. Deze communiceert op uitgaande poorten: TCP 443 (standaard), 5671, 5672, 9350 via 9354.  Hallo-gateway vereist geen poorten voor inkomend verkeer.

We raden u geaccepteerde Hallo IP-adressen voor de regio van uw gegevens in uw firewall. U kunt downloaden Hallo [lijst met Microsoft Azure Datacenter IP](https://www.microsoft.com/download/details.aspx?id=41653). Deze lijst is wekelijks bijgewerkt.

> [!NOTE]
> Hallo IP-adressen die worden vermeld in de lijst met hello Azure Datacenter IP zijn in CIDR-notatie. 10.0.0.0/24 betekent bijvoorbeeld niet 10.0.0.0 via 10.0.0.24. Meer informatie over Hallo [CIDR-notatie](http://whatismyipaddress.com/cidr).
>
>

Hallo volgen Hallo volledig gekwalificeerde domeinnamen gebruikt door Hallo-gateway.

| Domeinnamen | Uitgaande poorten | Beschrijving |
| --- | --- | --- |
| *. powerbi.com |80 |HTTP gebruikt toodownload Hallo installatieprogramma. |
| *. powerbi.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *. login.windows.net |443 |HTTPS |
| *. servicebus.windows.net |5671-5672 |Geavanceerde Message Queuing-Protocol (AMQP) |
| *. servicebus.windows.net |443, 9350-9354 |Listeners op Service Bus Relay via TCP (443 voor toegangsbeheer token aanschaf vereist) |
| *. frontend.clouddatahub.net |443 |HTTPS |
| *. core.windows.net |443 |HTTPS |
| Login.microsoftonline.com |443 |HTTPS |
| *. msftncsi.com |443 |Verbinding met internet tootest gebruikt als Hallo-gateway onbereikbaar via Hallo Power BI-service is. |
| *.microsoftonline p.com |443 |Gebruikt voor verificatie, afhankelijk van de configuratie. |

### <a name="force-https"></a>HTTPS-communicatie met Azure Service Bus forceren
U kunt Hallo gateway toocommunicate met Azure Service Bus afdwingen met behulp van HTTPS in plaats van rechtstreekse TCP; echter, doen dus aanzienlijk vermindert de prestaties. U kunt wijzigen Hallo *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* bestand door het wijzigen van de waarde op Hallo van `AutoDetect` te`Https`. Dit bestand bevindt zich doorgaans in *C:\Program Files\On-premises gegevensgateway*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Veelgestelde vragen

### <a name="general"></a>Algemeen

**Q**: moet ik een gateway voor gegevensbronnen in de cloud hello, zoals Azure SQL Database? <br/>
**Een**: Nee. Een gateway maakt verbinding alleen tooon-premises gegevensbronnen.

**Q**: heeft Hallo gateway geïnstalleerd op dezelfde computer als de gegevensbron Hallo Hallo toobe? <br/>
**Een**: Nee. Hallo-gateway wordt verbonden toohello-gegevensbron Hallo verbindingsgegevens die is opgegeven. Hallo gateway beschouwen als een client-toepassing in deze zin. Hallo gateway alleen moet Hallo mogelijkheid tooconnect toohello servernaam die is opgegeven, doorgaans op Hallo hetzelfde netwerk.

<a name="why-azure-work-school-account"></a>

**Q**: Waarom moet toouse werk of school account toosign in ik? <br/>
**Een**: U kunt alleen een Azure werk- of schoolaccount wanneer u Hallo lokale gegevensgateway installeert. Uw account wordt opgeslagen in een tenant die wordt beheerd door Azure Active Directory (Azure AD). Uw Azure AD-account UPN (user Principal name) normaal gesproken komt overeen met Hallo e-mailadres.

**Q**: waar mijn referenties worden opgeslagen? <br/>
**Een**: Hallo-referenties die u voor een gegevensbron opgeeft zijn versleuteld en opgeslagen in Hallo Gateway-Cloudservice. Hallo-referenties worden op Hallo lokale gegevensgateway ontsleuteld.

**Q**: zijn er vereisten voor de bandbreedte van het netwerk? <br/>
**Een**: dit is uw netwerk het beste verbinding bevat goede doorvoer. Elke omgeving is verschillend en Hallo hoeveelheid verzonden gegevens heeft op Hallo resultaten. Met behulp van ExpressRoute kan helpen bij het tooguarantee een mate van doorvoer tussen on-premises en hello Azure-datacenters.
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
**Een**: In de Services Hallo gateway gatewayservice voor On-premises gegevens wordt genoemd.

**Q**: kunt Hallo gateway Windows-service uitvoert met een Azure Active Directory-account? <br/>
**Een**: Nee. Hallo Windows-service moet een geldige Windows-account hebben. Standaard is Hallo-service wordt uitgevoerd met Hallo Service-SID NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Hoge beschikbaarheid en herstel na noodgevallen

**Q**: welke opties zijn beschikbaar voor herstel na noodgevallen? <br/>
**Een**: U kunt gebruiken Hallo herstel sleutel toorestore of verplaatsen van een gateway. Wanneer u Hallo-gateway installeert, geef Hallo herstelsleutel.

**Q**: Wat is Hallo voordeel van de herstelsleutel Hallo? <br/>
**Een**: Hallo herstelsleutel biedt een manier toomigrate of de gateway-instellingen herstellen na een noodgeval.

## <a name="troubleshooting"></a>Probleemoplossing

**Q**: hoe kan ik zien welke query toohello on-premises gegevensbron worden verzonden? <br/>
**Een**: U kunt inschakelen querytracering, waaronder het Hallo-query's die worden verzonden. Houd er rekening mee toochange query tracering van de oorspronkelijke waarde toohello gedaan bij het oplossen van problemen. Querytracering ingeschakeld verlaten maakt grotere Logboeken.

U kunt ook hulpprogramma's die de gegevensbron voor tracering van query's heeft bekijken. U kunt bijvoorbeeld de Extended Events of SQL Profiler gebruiken voor SQL Server en Analysis Services.

**Q**: waar zich de gateway-logboeken Hallo? <br/>
**Een**: Zie de logboeken verderop in dit onderwerp.

### <a name="update"></a>Meest recente versie van de update toohello

Veel problemen kunnen surface wanneer Hallo gatewayversie verouderd. Zorg ervoor dat u met de meest recente versie Hallo als goed over het algemeen. Als u dit nog niet hebt Hallo gateway voor een maand of langer bijgewerkt, kunt u Overweeg de installatie van de meest recente versie van gateway Hallo Hallo en zien als u Hallo probleem kan reproduceren.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Fout: Kan tooadd gebruiker toogroup. (-2147463168 PBIEgwService Prestatielogboekgebruikers)

U kunt deze fout kan ophalen, als u probeert tooinstall Hallo gateway op een domeincontroller wordt niet ondersteund. Zorg ervoor dat u Hallo-gateway op een computer die een domeincontroller niet implementeert.

## <a name="logs"></a>Logboeken

Logboekbestanden zijn een belangrijke bron wanneer het oplossen van problemen.

#### <a name="enterprise-gateway-service-logs"></a>Enterprise gateway-service-Logboeken

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Configuratielogboeken

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Gebeurtenislogboeken

U vindt Hallo Data Management Gateway en PowerBIGateway Logboeken onder **servicelogboeken voor toepassingen en**.


## <a name="telemetry"></a>Telemetrie
Telemetrie kan worden gebruikt voor bewaking en probleemoplossing. Standaard

**tooturn telemetrie**

1.  Controleer Hallo On-premises gateway client gegevensmap op Hallo-computer. Dit is meestal **%systemdrive%\Program Files\On-premises gegevensgateway**. Of u kunt een servicesconsole opent en controleer of Hallo pad tooexecutable: een eigenschap van Hallo On-premises data gateway-service.
2.  In de Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config-bestand Hallo van client-directory. Hallo SendTelemetry instelling tootrue wijzigen.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  De wijzigingen opslaan en Hallo Windows-service opnieuw starten: On-premises data gateway-service.




## <a name="next-steps"></a>Volgende stappen
* [Analyseservices beheren](analysis-services-manage.md)
* [Gegevens ophalen uit Azure Analysis Services](analysis-services-connect.md)
