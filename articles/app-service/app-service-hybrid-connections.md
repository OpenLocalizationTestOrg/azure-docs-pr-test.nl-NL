---
title: aaa "-Azure App Service hybride verbindingen | Microsoft Docs'
description: Hoe toocreate en gebruik hybride verbindingen tooaccess resources in verschillende netwerken
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Azure App Service hybride verbindingen #

## <a name="overview"></a>Overzicht ##

Hybride verbindingen is zowel een service in Azure als een functie in hello Azure App Service.  Als een service heeft het gebruik en mogelijkheden die worden gebruikt in hello Azure App Service.  meer informatie over hybride verbindingen en hun gebruik buiten hello Azure App Service kunt u hier starten toolearn [Azure Relay hybride verbindingen][HCService]

Hybride verbindingen mag binnen hello Azure App Service, gebruikte tooaccess application-resources in andere netwerken. Deze kunt openen vanuit uw app tooan toepassingseindpunt.  Deze kunnen een alternatieve mogelijkheid tooaccess niet uw toepassing.  Zoals in het Hallo-App Service gebruikt, correleert elke hybride verbinding tooa één TCP-host en poort combinatie.  Dit betekent dat eindpunt Hallo hybride verbinding kan worden op elk besturingssysteem en elke toepassing opgegeven u zijn kunt u door een TCP-luisterpoort. Hybride verbindingen niet weet of gelet op welke toepassingsprotocol Hallo is of als u opent.  Het levert gewoon toegang tot het netwerk.  


## <a name="how-it-works"></a>Hoe werkt het? ##
Hallo hybride verbindingen functie bestaat uit twee uitgaande aanroepen tooService Bus Relay.  Er is een verbinding van een bibliotheek op Hallo host waar uw app wordt uitgevoerd in Hallo-app service en vervolgens is er een verbinding tussen Hallo hybride verbinding Manager(HCM) tooService Bus relay.  Hallo HCM is een relayservice die u binnen het hosten van Hallo-netwerk implementeert 

Twee gekoppelde verbindingen met uw app heeft een TCP-tunnel tooa vaste combinatie van hostnaam: poort op Hallo andere kant van Hallo HCM via Hallo.  Hallo verbinding maakt gebruik van TLS 1.2 op beveiligings- en SAS-sleutels voor verificatie/autorisatie.    

![][1]

Wanneer uw app een DNS-aanvraag maakt die overeenkomt met een eindpunt van de hybride verbinding configureren en vervolgens Hallo uitgaande TCP-verkeer wordt omgeleid naar beneden Hallo hybride verbinding.  

> [!NOTE]
> Dit betekent dat u tooalways gebruik een DNS-naam voor uw hybride-verbinding proberen moet.  Sommige clientsoftware doet een DNS-zoekopdracht als Hallo eindpunt maakt gebruik van een IP-adres in plaats daarvan.
>
>

Er zijn twee soorten hybride verbindingen, het nieuwe hybride verbindingen hello, die worden aangeboden als een Azure-Relay-service en Hallo oudere BizTalk hybride verbindingen.  Hallo zijn oudere BizTalk hybride verbindingen waarnaar wordt verwezen tooas klassieke hybride verbindingen in Hallo-portal.  Er is meer informatie verderop in dit document informatie hierover.

### <a name="app-service-hybrid-connection-benefits"></a>Voordelen van App Service hybride verbinding ###

Er zijn een aantal voordelen toohello hybride verbindingen mogelijkheid inclusief

- Apps veilig toegang tot op premises systemen en services veilig
- Hallo functie vereist niet dat een internet toegankelijk eindpunt
- het is snel en eenvoudig tooset up  
- elke hybride verbinding overeenkomt met tooa één hostnaam: poort combinatie waarmee een uitstekende beveiliging aspect is
- Normaal gesproken hoeft niet firewall gaten zoals Hallo verbindingen alle uitgaande via standaard webpoorten zijn
- omdat de functie Hallo netwerkniveau die ook betekent dat deze agnostisch toohello taal wordt gebruikt door uw app en het Hallo-technologie gebruikt door Hallo-eindpunt
- kan tooprovide toegang in meerdere netwerken in een enkele app gebruikt 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Wat u niet kunt doen met hybride verbindingen ###

Er zijn enkele dingen die u niet kunt met hybride verbindingen doen en ze omvatten:

- koppelen van een station
- met behulp van UDP
- toegang tot TCP op basis van services die gebruikmaken van dynamische poorten zoals passieve modus van FTP of uitgebreide passieve modus
- LDAP-ondersteuning, zoals deze soms UDP is vereist
- Active Directory-ondersteuning

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Toe te voegen en een hybride verbinding te maken in uw App ##

Hybride verbindingen kunnen worden gemaakt via Hallo app portal of via Hallo hybride verbinding serviceportal.  Het is raadzaam dat u Hallo app portal toocreate Hallo hybride verbindingen die u wenst dat toouse met uw app.  een hybride verbinding toocreate gaat toohello [Azure-portal] [ portal] en Ga naar Hallo UI voor uw app.  Selecteer **Networking > uw hybride-verbindingseindpunten configureren**.  Hier ziet u Hallo hybride verbindingen die zijn geconfigureerd met uw app  

![][2]

tooadd een nieuwe hybride verbinding, klikt u op de hybride verbinding toevoegen.  Hallo gebruikersinterface die wordt geopend bevat Hallo hybride verbindingen die u al hebt gemaakt.  tooadd een of meer van deze tooyour app, klik op Hallo die u wilt gebruiken en klik op **toevoegen geselecteerd hybride verbinding**.  

![][3]

Als u een nieuwe hybride verbinding toocreate wilt, klikt u op **nieuwe hybride verbinding maken**.  Vanaf hier geeft u de: 

- naam van het eindpunt
- hostnaam van het eindpunt
- Eindpuntpoort
- Service Bus-naamruimte gewenst toouse

![][4]

Elke hybride verbinding is gebonden tooa service bus-naamruimte en elke service bus-naamruimte is in een Azure-regio.  Het is belangrijk tootry en gebruikt een service bus-naamruimte in Hallo dezelfde regio bevinden als uw app zodat tooavoid netwerk veroorzaakte latentie.

Als u uw hybride verbinding tooremove van uw app wilt, klik hierop en selecteer **Disconnect**.  

Wanneer een hybride verbinding is tooyour web-app toegevoegd, ziet u details op het door erop te klikken.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Hybride verbindingen en App Service-abonnementen ##

Hallo alleen hybride verbindingen die kunt u nu wel zijn Hallo nieuwe hybride verbindingen.  Ze zijn alleen beschikbaar in Basic, Standard, Premium en geïsoleerd prijzen SKU's.  Er zijn limieten gebonden toohello plan prijzen.  

| Plan prijzen | Aantal hybride verbindingen kan worden gebruikt in Hallo plannen |
|----|----|
| Basic | 5 |
| Standard | 25 |
| Premium | 200 |
| Isolated | 200 |

Omdat er beperkingen App Service-Plan is er ook gebruikersinterface in Hallo App Service-Plan dat toont hoe veel hybride verbindingen worden gebruikt en door welke apps.  

![][6]

Net zoals met Hallo app weergave ziet u details op uw hybride-verbinding door erop te klikken.  Dezelfde App Service-Plan gebruikt die hybride verbinding in de hier weergegeven, u kunt alle Hallo-gegevens in Hallo app weergave bekijken maar ziet ook hoe veel apps in Hallo Hallo-eigenschappen.

![][7]

Terwijl er een limiet van het aantal hybride-verbindingseindpunten die kunnen worden gebruikt in een App Service-Plan hello geldt, kan elke hybride verbinding die wordt gebruikt in een willekeurig aantal apps in deze App Service-Plan worden gebruikt.  Dat toosay dat als ik had 1 hybride verbinding die ik in 5 afzonderlijke apps in mijn App Service-Plan gebruikt, die is zich nog steeds 1 hybride verbinding is.

Er is een extra kosten toohybrid verbindingen wordt alleen gebruikt in een Basic, Standard, Premium of geïsoleerde SKU.  Voor meer informatie over prijzen voor hybride verbinding hier gaat: [Service Bus prijzen][sbpricing].

## <a name="hybrid-connection-manager"></a>Hybride Verbindingsbeheer ##

Voor hybride verbindingen toowork moet u een relay-agent in Hallo netwerk die als host fungeert voor uw eindpunt van hybride verbinding.  Hallo hybride Connection Manager (HCM), die relay-agent wordt genoemd.  Dit hulpprogramma kan worden gedownload vanaf Hallo **Networking > uw hybride-verbindingseindpunten configureren** gebruikersinterface die beschikbaar zijn vanuit uw app in Hallo [Azure-portal][portal].  

Dit hulpprogramma wordt uitgevoerd op WindowsServer 2008 R2 en latere versies van Windows.  Eenmaal geïnstalleerd Hallo HCM als een service wordt uitgevoerd.  Deze service verbindt tooAzure service bus relay op basis van eindpunten Hallo geconfigureerd.  Hallo-verbindingen van Hallo HCM zijn uitgaande tooports 80 en 443.    

Hallo HCM heeft een UI-tooconfigure deze.  Na Hallo die HCM is geïnstalleerd kunt u Hallo UI dan door het uitvoeren van Hallo HybridConnectionManagerUi.exe die zich in de installatiemap van Hallo hybride Verbindingsbeheer.  Deze ook eenvoudig op Windows 10 wordt bereikt door op te geven *hybride Verbindingsbeheer UI* in het zoekvak.  

Wanneer Hallo HCM UI wordt gestart, Hallo eerst te beginnen u is Zie een tabel waarin alle Hallo hybride verbindingen die zijn geconfigureerd met dit exemplaar van Hallo HCM.  U kunt eventueel toomake wijzigingen moet u tooauthenticate met Azure. 

tooadd een of meer hybride verbindingen tooyour HCM:

1. Hallo HCM UI starten
1. Klik op een andere hybride verbinding configureren![][8]

1. Meld u aan met uw Azure-account
1. Een abonnement kiezen
1. Klik op Hallo hybride verbindingen die u wilt deze toorelay HCM![][9]

1. Op Opslaan klikken

U ziet nu de Hallo hybride verbindingen die u hebt toegevoegd.  U kunt ook op Hallo geconfigureerd hybride verbinding en Zie voor meer informatie over Hallo verbinding.

![][10]

Voor uw HCM toobe kunnen toosupport Hallo hybride verbindingen die hiervoor is geconfigureerd, moet:

- TCP-toegang tooAzure poorten 80 en 443
- TCP-toegang toohello hybride verbindingseindpunt
- mogelijkheid toodo DNS-uiterlijk-ups op Hallo eindpunt host en hello azure service bus-naamruimte

Hallo HCM ondersteunt zowel nieuwe hybride verbindingen als Hallo oudere BizTalk hybride verbindingen.

### <a name="redundancy"></a>Redundantie ###

Elke HCM kan meerdere hybride verbindingen ondersteunen.  Opgegeven hybride verbindingen kan ook worden ondersteund door meerdere HCMs.  Hallo standaardgedrag is tooround robin verkeer via Hallo HCMs geconfigureerd voor een willekeurig eindpunt opgegeven.  Desgewenst kunt u hoge beschikbaarheid voor uw hybride verbindingen vanaf het netwerk eenvoudig exemplaar maken van meerdere HCMs op afzonderlijke computers. 

### <a name="manually-adding-a-hybrid-connection"></a>Handmatig toevoegen van een hybride verbinding ###

Als u wilt dat iemand buiten uw abonnement toohost een HCM-exemplaar voor een bepaalde hybride verbinding, kunt u delen met deze verbindingsreeks voor de gateway voor hybride verbinding voor Hallo Hallo.  U kunt dit zien in de eigenschappen voor een hybride verbinding in Hallo Hallo [Azure-portal][portal]. toouse die tekenreeks, klikt u op Hallo **handmatig configureren** knop op Hallo HCM en plak in verbindingsreeks Hallo-gateway.


## <a name="troubleshooting"></a>Problemen oplossen ##

Wanneer uw hybride verbinding is ingesteld met een actieve toepassing en er ten minste één HCM die hybride verbinding geconfigureerd heeft, wordt Hallo status dicteert **verbonden** in Hallo-portal.  Als u niet de tekst **verbonden** betekent dat dat uw app niet actief is of uw HCM kan geen verbinding uit tooAzure op poort 80 of 443 maken.  

Hallo van de belangrijkste reden dat clients geen verbinding tootheir-eindpunt maken is omdat het Hallo-eindpunt is opgegeven met een IP-adres in plaats van een DNS-naam.  Als uw app Hallo gewenst eindpunt niet bereiken en u een IP-adres gebruikt, schakelt u toousing een DNS-naam die is ongeldig op Hallo host waarop hello HCM wordt uitgevoerd.  Andere toocheck dingen zijn die Hallo DNS-naam wordt omgezet naar behoren op Hallo host waar hello HCM wordt uitgevoerd en dat er een verbinding van Hallo host waarop hello HCM wordt uitgevoerd toohello hybride verbindingseindpunt is.  

Er is een hulpprogramma in Hallo App-Service waarmee kan worden aangeroepen vanuit Hallo console tcpping aangeroepen.  Dit hulpprogramma kunt u zien als u toegang tooa TCP-eindpunt hebt, maar geeft niet aan als u toegang tooa hybride verbindingseindpunt hebben.  Wanneer gebruikt in de console voor een hybride verbindingseindpunt hello, de opdracht ping slaagt alleen laat u weten dat er een hybride verbinding geconfigureerd voor uw app die gebruikmaakt van deze combinatie van hostnaam: poort.  

## <a name="biztalk-hybrid-connections"></a>Hybrid Connections van BizTalk ##

Hallo oudere BizTalk hybride verbindingen mogelijkheid is gesloten uit toofurther BizTalk hybride verbinding maken.  U kunt blijven gebruiken van uw bestaande BizTalk hybride verbindingen met uw apps, maar u moet de nieuwe service toohello migreren.  Voordelen van de nieuwe service Hallo via Hallo BizTalk-versie zijn onder andere Hallo:

- Er is geen aanvullende BizTalk-account is vereist
- TLS is 1.2 in plaats van 1.0 zoals in BizTalk hybride verbindingen
- Er is een communicatie via poorten 80 en 443 met behulp van een DNS-naam tooreach Azure in plaats van IP-adressen en een aantal extra andere poorten.  

tooadd een app BizTalk hybride verbinding tooyour Ga tooyour-app in Hallo [Azure-portal] [ portal] en klik op **Networking > uw hybride-verbindingseindpunten configureren**.  In de Hallo klassieke hybride verbindingen tabel op **klassieke hybride verbinding toevoegen**.  Hier ziet u een lijst met uw BizTalk hybride verbindingen.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

