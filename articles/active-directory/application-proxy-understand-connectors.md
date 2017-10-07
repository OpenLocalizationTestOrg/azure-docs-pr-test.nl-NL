---
title: aaaUnderstand Azure AD-toepassingsproxy connectors | Microsoft Docs
description: Bevat informatie over Hallo basisbeginselen van Azure AD-toepassingsproxy connectors.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Azure AD-toepassingsproxy connectors begrijpen

Connectors zijn wat Azure AD-toepassingsproxy mogelijk maken. Ze zijn eenvoudige, gemakkelijk toodeploy onderhouden en super krachtige. Dit artikel wordt beschreven welke connectors zijn, hoe deze werken, en enkele suggesties voor toooptimize uw implementatie. 

## <a name="what-is-an-application-proxy-connector"></a>Wat is een connector voor toepassingsproxy

Verbindingslijnen zijn lichtgewicht agents die zich bevinden op lokale en het faciliteren van Hallo uitgaande verbinding toohello toepassingsproxy service. Connectors moeten worden geïnstalleerd op een Windows-Server die toegang toohello back-end van toepassing is. U kunt connectors indelen in groepen van de connector, met elke groep verwerken van verkeer toospecific toepassingen. Connectors verdelen automatisch, en kunt toooptimize de netwerkstructuur van uw. 

## <a name="requirements-and-deployment"></a>Vereisten en implementatie

toodeploy toepassingsproxy is, moet u ten minste één connector, maar het is raadzaam twee of meer voor groter tolerantie. Hallo-connector installeren op een Windows Server 2012 R2 of 2016 machine. Hallo-connector moet toobe kunnen toocommunicate met service voor toepassingsproxy hello, evenals Hallo on-premises toepassingen die u publiceert. 

Zie voor meer informatie over Hallo netwerkvereisten voor de server-connector Hallo [aan de slag met Application Proxy en het installeren van een connector](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Onderhoud
Hallo behandelen connectors en Hallo service van alle taken van Hallo hoge beschikbaarheid. Ze kunnen worden toegevoegd of verwijderd dynamisch. Telkens wanneer die een nieuwe aanvraag ontvangt wordt gerouteerd tooone van Hallo connectors die momenteel beschikbaar is. Als een verbindingslijn tijdelijk niet beschikbaar is, reageert niet toothis verkeer.

Hallo-connectors zijn staatloze en er geen configuratiegegevens op Hallo-machine. Hallo is alleen gegevens die ze opslaan Hallo-instellingen voor het verbinden van Hallo-service en het certificaat voor clientverificatie. Wanneer ze toohello service verbinden, deze pull-configuratiegegevens voor alle Hallo vereist en deze elke paar minuten vernieuwt.

Connectors pollen ook Hallo server toofind nagaan of er is een nieuwere versie van het Hallo-connector. Als er een is gevonden, Hallo connectors worden bijgewerkt.

U kunt uw connectors van Hallo machine die ze worden uitgevoerd, controleren met Hallo-gebeurtenislogboek en prestatiemeteritems. Of u kunt de status van Hallo toepassingsproxy pagina Hallo Azure-portal bekijken:

 ![AzureAD Application Proxy Connectors](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

U hebt geen toomanually verwijderen van connectors die niet gebruikt worden. Wanneer een connector wordt uitgevoerd, blijft het actief tijdens het verbinden van toohello-service. Ongebruikte connectors zijn gelabeld als _inactieve_ en na 10 dagen inactief zijn verwijderd. Als u dat toouninstall een connector wilt, echter Verwijder zowel Hallo-connectorservice en Hallo Updater service van Hallo-server. Start uw computer toofully verwijderen Hallo-service opnieuw.

## <a name="automatic-updates"></a>Automatische updates

Azure AD levert de automatische updates voor alle Hallo-connectors die u implementeert. Zolang Hallo Application Proxy Connector Updater service wordt uitgevoerd, wordt uw connectors automatisch bijgewerkt. Als er geen Hallo Connector Updater-service op uw server, moet u te[de connector opnieuw installeren](active-directory-application-proxy-enable.md) tooget eventuele updates. 

Als u geen toowait bij een automatische update toocome tooyour-connector wilt, kunt u een handmatige upgrade kunt uitvoeren. Ga toohello [connector downloadpagina](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) op Hallo server waarin de connector gevonden en selecteer is **downloaden**. Dit proces is serversysteemstatus van een upgrade voor de lokale connector Hallo. 

Voor tenants met meerdere connectors richten Hallo automatische updates één connector op een tijd in elke groep tooprevent downtime in uw omgeving. 

U kunt uitvaltijd kan optreden wanneer uw connector bijgewerkt als:  
- U hoeft slechts één connector. tooavoid deze uitvaltijd en verbeteren van hoge beschikbaarheid, wordt aangeraden een tweede connector te installeren en [maakt u een groep connector](active-directory-application-proxy-connectors-azure-portal.md).  
- Een connector is in het midden van een transactie Hallo aanvang Hallo-update. Hoewel Hallo initiële transactie verloren gegaan is, uw browser automatisch probeert opnieuw Hallo of kunt u uw pagina vernieuwen. Bij het Hallo-aanvraag is verzonden, is Hallo verkeer gerouteerd tooa back-connector.

## <a name="creating-connector-groups"></a>Connector-groepen maken

Groepen van de Connector inschakelen tooassign specifieke connectors tooserve specifieke toepassingen. U kunt een aantal connectors te groeperen en wijs vervolgens elke groep van toepassingen tooa toe. 

Connector-groepen maken het gemakkelijker toomanage grote implementaties. Bovendien de latentie voor tenants die toepassingen die worden gehost in verschillende regio's, omdat u kunt groepen op basis van locatie-connector tooserve alleen lokale toepassingen maken. 

toolearn meer informatie over groepen, connector, Zie [publiceren van toepassingen op afzonderlijke netwerken en locaties met connector groepen](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Beveiliging en netwerken

Connectors kunnen overal worden geïnstalleerd op Hallo-netwerk waarmee ze toosend aanvragen toohello Webtoepassingsproxy-service. Wat is het belangrijk is dat Hallo computers Hallo connector ook heeft toegang tooyour apps. U kunt connectors binnen uw bedrijfsnetwerk of op een virtuele machine die wordt uitgevoerd in de cloud Hallo installeren. Connectors kunnen worden uitgevoerd binnen een gedemilitariseerde zone (DMZ), maar het is niet nodig omdat het al het verkeer uitgaand is, zodat uw netwerk beveiligd blijft.

Connectors alleen verzenden uitgaande aanvragen. Hallo uitgaand verkeer wordt verzonden toohello Application Proxy-service en toohello gepubliceerde toepassingen. U hebt geen tooopen binnenkomende poorten omdat beide manieren verkeersstromen wanneer een sessie tot stand is gebracht. U niet hebt tooset u taakverdeling tussen Hallo verbindingslijnen of binnenkomende toegang via uw firewalls configureren. 

Zie voor meer informatie over het configureren van uitgaande firewallregels [werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md).

Gebruik Hallo [Azure AD Application Proxy Connector poorten hulpprogramma Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify dat uw connector Hallo-service voor toepassingsproxy kunt bereiken. Ten minste Zorg ervoor dat de regio VS-midden Hallo en Hallo regio dichtstbijzijnde tooyou alle een groen vinkje. Daarna betekent meer een groen vinkje groter tolerantie. 

## <a name="performance-and-scalability"></a>Prestaties en schaalbaarheid

Schaal voor Hallo service voor toepassingsproxy is transparant, maar de schaal is een factor voor connectors. U moet voldoende piekverkeer van connectors toohandle toohave. Echter, u hoeft niet tooconfigure taakverdeling omdat alle connectors binnen een connector-groep automatisch worden verdeeld.

Aangezien connectors staatloze, zijn ze niet beïnvloed door Hallo aantal gebruikers of -sessies. Ze reageren in plaats daarvan toohello aantal aanvragen en hun nettolading. Met standaard internetverkeer, kan een gemiddelde machine enkele duizenden aanvragen per seconde verwerken. Hallo specifieke capaciteit is afhankelijk van Hallo exacte machine kenmerken. 

Hallo connectorprestaties afhankelijk is van de CPU en netwerken. CPU-prestaties is vereist voor SSL-versleuteling en ontsleuteling, terwijl netwerken belangrijk tooget snelle verbinding toohello toepassingen en Hallo onlineservice in Azure is.

Daarentegen is geheugen kleiner van een probleem voor connectors. Hallo-onlineservice zorgt voor veel Hallo verwerking en alle niet-geverifieerd verkeer. Alles dat kan worden uitgevoerd in de cloud Hallo Hallo cloud doet. 

Een andere factor die van invloed op prestaties is Hallo kwaliteit van Hallo-netwerken tussen Hallo connectors, inclusief: 

* **Hallo onlineservice**: trage of hoge latentie verbindingen toohello service voor toepassingsproxy in de prestaties van Azure invloed Hallo-connector. Voor de beste prestaties Hallo verbinding maken met uw organisatie tooAzure met Express Route. Anders hebben uw netwerken team ervoor te zorgen dat verbindingen tooAzure zo efficiënt mogelijk worden verwerkt. 
* **back-end-toepassingen Hallo**: In sommige gevallen zijn aanvullende proxy's tussen Hallo-connector en Hallo back-end voor toepassingen die kunnen trage of verbindingen voorkomen. tootroubleshoot dit scenario wordt een browser openen vanuit server-connector Hallo en probeer het tooaccess Hallo-toepassing. Als u connectors Hallo in Azure uitvoeren, maar Hallo toepassingen zich on-premises, Hallo ervaring mogelijk niet wat uw gebruikers verwachten.
* **Hallo-domeincontrollers**: als Hallo connectors met behulp van Kerberos-beperkte overdracht SSO uitvoert, ze contact opnemen met Hallo-domeincontrollers voor het verzenden van Hallo aanvraag toohello back-end. Hallo connectors een cache van Kerberos-tickets hebben, maar in een omgeving met bezet Hallo reactiesnelheid van Hallo-domeincontrollers kan invloed hebben op prestaties. Dit probleem is vaker voor connectors die worden uitgevoerd in Azure, maar communicatie met domeincontrollers die zich on-premises. 

Zie voor meer informatie over het optimaliseren van uw netwerk [aandachtspunten voor topologie netwerk bij gebruik van Azure Active Directory-toepassingsproxy](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Lid worden van domein

Connectors kunnen uitvoeren op een computer die is geen lid van een domein. Als u wilt dat eenmalige aanmelding (SSO) tooapplications die gebruikmaken van geïntegreerde Windows-verificatie (IWA), moet u een domein-machine. In dit geval Hallo connector machines moeten zijn van een domein gekoppelde tooa die kunt uitvoeren [Kerberos](https://web.mit.edu/kerberos) beperkte overdracht namens gebruikers voor Hallo Hallo gepubliceerde toepassingen.

Connectors kunnen ook worden gekoppelde toodomains of forests die u een gedeeltelijk vertrouwen of tooread alleen-lezen domeincontrollers hebt.

## <a name="connector-deployments-on-hardened-environments"></a>Connector-implementaties op beperkte omgevingen

Normaal gesproken implementatie van de connector is eenvoudig en is geen speciale configuratie vereist. Er zijn echter een aantal unieke voorwaarden die u moeten overwegen:

* Organisaties die Hallo uitgaand verkeer beperkt moeten [vereiste poorten openen](active-directory-application-proxy-enable.md#open-your-ports).
* FIPS-compatibele computers mogelijk vereist toochange hun configuratie tooallow Hallo connector processen toogenerate en een certificaat wordt opgeslagen.
* Organisaties die hun omgeving op basis van Hallo processen vergrendelen met die probleem Hallo toegang aanvragen hebben toomake ervoor dat beide connectorservices ingeschakelde tooaccess alle vereiste poorten en IP-adressen zijn.
* In sommige gevallen kunnen uitgaande forward proxy's Hallo wederzijdse certificaatverificatie opsplitsen en Hallo communicatie toofail veroorzaken.

## <a name="connector-authentication"></a>Connector-verificatie

tooprovide een beveiligde service, connectors hebben tooauthenticate naar Hallo-service en Hallo-service heeft tooauthenticate naar Hallo-connector. Deze verificatie wordt gedaan met behulp van de client en server certificaten wanneer het Hallo-connectors Hallo verbinding starten. Deze manier Hallo beheerder gebruikersnaam en wachtwoord worden niet opgeslagen op Hallo connector machine.

Hallo-certificaten gebruikt zijn specifieke toohello Application Proxy-service. Ze worden gemaakt tijdens de initiële registratie Hallo en worden automatisch vernieuwd door Hallo connectors elke aantal maanden. 

Als een connector niet is verbonden toohello service voor enkele maanden, de certificaten is mogelijk verouderd. In dit geval verwijderen en opnieuw installeren van de registratie van de tootrigger connector Hallo. U kunt Hallo volgende PowerShell-opdrachten kunt uitvoeren:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Achter de schermen Hallo

Connectors zijn gebaseerd op Windows Server Web Application Proxy, zodat zij de meeste Hallo dezelfde beheertools, waaronder Windows-gebeurtenislogboeken

 ![Gebeurtenislogboeken Hello logboeken beheren](./media/application-proxy-understand-connectors/event-view-window.png)

en Windows-prestatiemeteritems. 

 ![Toevoegen van items toohello connector met Hallo Prestatiemeter](./media/application-proxy-understand-connectors/performance-monitor.png)

Hallo connectors admin en sessie hebt Logboeken. Hallo beheerder logboeken bevatten belangrijke gebeurtenissen en hun fouten. Hallo sessielogboeken bevatten alle Hallo transacties en de bijbehorende verwerkingsgegevens. 

toosee hello Logboeken, gaat u toohello Logboeken openen Hallo **weergave** menu en schakel **logboeken en foutopsporing weergeven analytische**. Schakel vervolgens deze toostart verzamelen van gebeurtenissen. Deze logboeken worden niet weergegeven in de Web Application Proxy in Windows Server 2012 R2, zoals Hallo connectors zijn gebaseerd op een meer recente versie.

U kunt nagaan Hallo status van Hallo-service in het venster Hallo-Services. Hallo-connector bestaat uit twee Windows-Services: Hallo werkelijke connector en Hallo updater. Alle Hallo-tijd van beide moeten worden uitgevoerd.

 ![AzureAD Services lokale](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Volgende stappen


* [Publiceren van toepassingen op afzonderlijke netwerken en locaties met groepen van de connector](active-directory-application-proxy-connectors-azure-portal.md)
* [Werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md)
* [Toepassingsproxy en connector fouten oplossen](active-directory-application-proxy-troubleshoot.md)
* [Hoe toosilently hello Azure AD-Application Proxy Connector installeren](active-directory-application-proxy-silent-installation.md)

