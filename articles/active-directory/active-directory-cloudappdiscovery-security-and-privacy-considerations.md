---
title: aaaCloud App detectie beveiligings- en privacyoverwegingen | Microsoft Docs
description: Dit onderwerp beschrijft Hallo beveiliging en privacy overwegingen gerelateerde tooCloud App Discovery.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Cloud App Discovery beveiligings- en privacyoverwegingen
Microsoft is doorgevoerd tooprotecting uw privacy en beveiliging van uw gegevens tijdens de levering van software en services die u helpen Hallo beveiliging van uw organisatie beheren.  
We erkennen dat wanneer u uw gegevens tooothers belasten, vertrouwensrelatie strengere beveiliging engineering investeringen en expertise tooback vereist deze.
Microsoft voldoet toostrict compatibiliteit en richtlijnen voor beveiliging van beveiligde software development lifecycle procedures toooperating een service.  
Beveiliging en bescherming van gegevens is een topprioriteit bij Microsoft.

Dit onderwerp wordt uitgelegd hoe gegevens die worden verzameld, verwerkt en beveiligd binnen Azure Active Directory Cloud App Discovery

## <a name="overview"></a>Overzicht
Cloud App Discovery is een functie van Azure AD en wordt gehost in Microsoft Azure.  
Hallo Cloud App Discovery endpoint agent is gebruikte toocollect toepassing discovery-gegevens van beheerde IT-machines.  
Hallo verzamelde gegevens worden verzonden veilig via een versleuteld kanaal toohello Azure AD Cloud App Discovery-service.  
Hallo Cloud App Discovery-gegevens voor een organisatie is zichtbaar in hello Azure-portal. 

![De werking van Cloud App Discovery](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Hallo volgende secties Volg Hallo stroom van gegevens en wordt beschreven hoe deze worden beveiligd omdat het van uw organisatie toohello Cloud App Discovery-service en uiteindelijk toohello Cloud App Discovery-portal wordt verplaatst.

## <a name="collecting-data-from-your-organization"></a>Verzamelen van gegevens van uw organisatie
In de volgorde toouse Azure Active Directory van Cloud App discovery functie tooget inzichten in Hallo-toepassingen die worden gebruikt door werknemers in uw organisatie moet u toofirst hello Azure AD Cloud App Discovery endpoint agent toomachines in uw organisatie te implementeren.

Beheerders van Azure Active Directory-tenant hello (of hun gemachtigde) kunnen Hallo agent-installatiepakket downloaden van hello Azure-portal. Hallo-agent kan worden handmatig geïnstalleerd of geïnstalleerd via meerdere computers in Hallo organisatie via SCCM of Groepsbeleid.

Zie voor meer instructies voor de implementatie-opties [Cloud App Discovery Groepsbeleid Deployment Guide](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Gegevens die worden verzameld door Hallo-agent
Hallo-gegevens die worden beschreven in de onderstaande lijst van Hallo worden verzameld door Hallo agent als een verbinding tooa webtoepassing is gemaakt. Hallo gegevens worden alleen verzameld voor deze toepassingen of Hallo beheerder is geconfigureerd voor detectie.  
U kunt de lijst Hallo van cloud-apps die agent monitors via Hallo Cloud App Discovery-blade in Hallo Microsoft hello bewerken [Azure-portal](https://portal.azure.com/)onder **instellingen**->**gegevens Verzameling**->**App-verzameling lijst**. Zie voor meer informatie [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Informatie categorie**: gebruikersgegevens  
**Beschrijving**:  
Hallo Windows-gebruikersnaam van Hallo-proces dat een aanvraag toohello doel webtoepassing gemaakt (bijvoorbeeld: DOMEIN\gebruikersnaam) en de Windows SID (Security Identifier) van de gebruiker Hallo Hallo.

**Informatie categorie**: de verwerking van gegevens  
**Beschrijving**:  
Hallo-naam van Hallo-proces dat Hallo aanvraag toohello doelwebtoepassing gemaakt (bijvoorbeeld: 'iexplore.exe')

**Informatie categorie**: computerinformatie  
**Beschrijving**:  
Hallo NetBIOS-computernaam op welke Hallo-agent is geïnstalleerd.

**Informatie categorie**: informatie over App-verkeer  
**Beschrijving**: 

Hallo verbindingsgegevens te volgen:

* Hallo bron (lokale computer) en doel-IP-adressen en poortnummers
* Hallo openbare IP-adres van Hallo organisatie via welke Hallo aanvraag uitvalt.
* Hallo-tijd van aanvraag Hallo
* Hallo verkeersvolume verzonden en ontvangen
* Hallo IP-versie (4 of 6)
* Voor de TLS-verbindingen: Hallo doel-hostnaam van Hallo Servernaamindicatie extensie of Hallo-servercertificaat.

Hallo HTTP-gegevens te volgen:

* Methode (GET, POST, enz.)
* Protocol (HTTP/1.1, enz.)
* Tekenreeks van de gebruikersagent
* Hostnaam
* Doel-URI (met uitzondering van querytekenreeks)
* Informatie over inhoudstype
* Verwijzende site URL-gegevens (met uitzondering van de query-tekenreeks)

> [!NOTE]
> Hallo bovenstaande HTTP-gegevens worden verzameld voor alle niet-versleutelde verbindingen.
> TLS-verbindingen, wordt deze informatie alleen vastgelegd, wanneer Hallo 'Diepe inspectie' is ingeschakeld in Hallo-portal. 'ON' is Hallo-instelling standaard.
> Zie voor meer informatie hieronder en [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Bovendien toohello gegevens die Hallo agent verzamelt over netwerkactiviteit hello, verzamelt ook anonieme gegevens over het Hallo-software en hardware-configuratie, foutenrapporten en informatie over hoe Hallo-agent wordt gebruikt.


### <a name="how-hello-agent-works"></a>De werking van Hallo-agent
installatie van de agent Hallo bevat twee onderdelen:

* Een onderdeel van de gebruikersmodus
* Een onderdeel in kernelmodus stuurprogramma (Windows Filtering Platform stuurprogramma)

Toen Hallo-agent is geïnstalleerd een vertrouwd certificaat voor computer-specifieke worden opgeslagen op Hallo machine waarin het gebruikt vervolgens tooestablish een beveiligde verbinding met de Hallo Cloud App Discovery-service.  
Hallo agent haalt periodiek beleidsconfiguratie van Hallo Cloud App Discovery-service via deze beveiligde verbinding.  
Hallo beleid bevat informatie over welke cloud-toepassingen toomonitor en Hiermee wordt aangegeven of Automatische updates moet worden ingeschakeld, onder andere.

Als het internetverkeer wordt verzonden en ontvangen op de machine Hallo van Internet Explorer en Chrome, Hallo Cloud App Discovery agent Hallo verkeer analyseert en uitgepakt Hallo relevante metagegevens (Zie Hallo **gegevens verzameld door de agent Hallo** sectie hierboven).  
Elke minuut bestandsuploads Hallo agent Hallo verzamelde metagegevens toohello Cloud App Discovery-service via een versleuteld kanaal.

Hallo stuurprogramma onderdeel intercepts Hallo versleuteld verkeer en voegt zelf in gecodeerde Hallo-stroom. Meer informatie in Hallo **gegevens van de versleutelde verbindingen (met diepe inspectie) onderscheppen** hieronder.

### <a name="respecting-user-privacy"></a>Privacy van gebruikers te respecteren
Ons doel is tooprovide beheerders Hallo extra tooset Hallo balans tussen gedetailleerde beeldverwerkingstoepassingen in toepassing gebruiks- en privacy geschikt is voor hun organisatie. einde toothat, bieden we Hallo knoppen in de instellingenpagina Hallo in Hallo Portal volgen:

* **Gegevensverzameling**: beheerders kunnen toospecify kiezen welke toepassingen of toepassingscategorieën ze willen tooget discovery-gegevens op.
* **Met diepe inspectie**: beheerders kunnen toospecify gekozen als Hallo agent verzamelt HTTP-verkeer voor SSL/TLS-verbindingen (aka **'Diepe inspectie'**). Meer informatie over dit in de volgende sectie Hallo.
* **Toestemming geven opties**: beheerders kunnen gebruikmaken van Hallo Cloud App Discovery portal toochoose of toonotify gebruikers Hallo verzamelen van gegevens door Hallo-agent en of toorequire gebruiker toestemming geven voordat het Hallo-agent wordt gestart met het verzamelen van gebruikersgegevens.

Hallo Cloud App Discovery endpoint agent verzamelt alleen Hallo informatie die wordt beschreven in Hallo **gegevens verzameld door de agent Hallo** sectie hierboven.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Gegevens van de versleutelde verbindingen (met diepe inspectie) onderscheppen
Zoals eerder vermeld, kunnen beheerders Hallo agent toomonitor gegevens van de versleutelde verbindingen ('diepe inspectie') configureren. TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) is een van de Hallo vandaag meest gangbare protocollen op Hallo Internet gebruikt. Door het versleutelen van communicatie met TLS, kan een client een vertrouwelijk communicatiekanaal met een webserver; maken. TLS bevat essentiële beveiliging voor het doorgeven van referenties voor verificatie en voorkomen dat Hallo openbaarmaking van gevoelige informatie.

Tijdens het Hallo-end-to-end veilig versleutelde kanaal geleverd door TLS kunt belangrijke beveiligings- en privacy, is vaak het Hallo-protocol doelwit voor schadelijke of slechte doeleinden. Zoveel dus in feite TLS wordt vaak aangeduid tooas Hallo "universal firewall-bypass protocol". Hallo-hoofdmap van het Hallo-probleem is dat de meeste firewalls niet kan tooinspect TLS communicatie omdat Hallo toepassingslaag gegevens worden versleuteld met SSL. Weten, aanvallers vaak maken gebruik van TLS toodeliver schadelijke nettoladingen tooa gebruiker erop vertrouwen dat zelfs Hallo meest intelligent toepassingslaag firewalls volledig blind tooTLS zijn en moeten de TLS-communicatie tussen hosts gewoon relay. Eindgebruikers kunnen gebruikmaken van vaak afgedwongen door hun zakelijke firewalls en proxyservers bevinden, met het tooconnect toopublic-proxy's en voor niet-TLS tunnelingprotocollen via Hallo firewall die anders mogelijk geblokkeerd door het beleid voor toegangsbeheer van toobypass van TLS.

Met diepe inspectie kan Hallo Cloud App Discovery agent tooact als een vertrouwde man-in-the-middle. Wanneer een clientaanvraag wordt gedaan tooaccess een HTTPS beveiligde resource, Hallo Endpoint Agent stuurprogramma Hallo verbinding onderschept en er wordt een nieuwe verbinding toohello bestemming server tooretrieves de SSL-certificaat namens Hallo-client. Hallo-agent vervolgens controleert of Hallo certificaat kan worden vertrouwd (door te controleren of deze niet is ingetrokken en er andere certificaat controles worden uitgevoerd), en als deze slaagt, Hallo Endpoint Agent vervolgens Hallo informatie opgehaald van het servercertificaat Hallo en maakt een eigen servercertificaat--bekend als een certificaat worden onderschept--die gegevens. Hallo onderschept certificaat is ondertekend op het moment door Hallo endpoint agent met een basiscertificaat dat in het vertrouwde certificaatarchief voor Windows hello is geïnstalleerd. Dit zelfondertekende basiscertificaat is niet exporteerbaar gemarkeerd en ACL tooadministrators was. Is het beoogde toonever laat Hallo machine waarop deze is gemaakt. Wanneer de clienttoepassing Hallo eindgebruiker Hallo onderschept certificaat ontvangt, wordt deze het vertrouwen omdat deze kan met succes Hallo certificaatketen alle Hallo toohello manier basiscertificaat. Dit proces is voornamelijk transparant uit oogpunt van een eindgebruiker met enkele aanvullende opmerkingen zoals hieronder wordt beschreven.

Doordat diepe inspectie Hallo Cloud App Discovery Endpoint Agent kunt ontsleutelen en TLS versleutelde communicatie, zodat Hallo service tooreduce ruis controleren en inzicht bieden over Hallo informatie over het gebruik van cloud-apps Hallo versleuteld.

#### <a name="a-word-of-caution"></a>Waarschuwing
Voordat u met diepe inspectie inschakelt, wordt sterk aangeraden dat u uw bedoelingen tooyour juridische en HR afdelingen communiceren en hun toestemming verkrijgen. Persoonlijke gecodeerde communicatie van de eindgebruiker te bekijken, kan een gevoelige onderwerp, zijn voor de hand. Tooindicate die versleuteld communicatie worden gecontroleerd voordat een productie uitrollen van grondige inspectie, Controleer of de beveiliging van uw bedrijf en beleidsregels voor aanvaardbaar gebruik zijn bijgewerkt. Melding voor gebruikers en uitsluiting van sites geacht gevoelige (bijvoorbeeld Bank- en medische sites) kunnen ook nodig zijn als u Cloud App Discovery toomonitor configureert deze. Zoals eerder vermeld, kunnen beheerders gebruiken Hallo Cloud App Discovery portal toochoose of toonotify gebruikers Hallo verzamelen van gegevens door Hallo-agent en of toorequire gebruiker toestemming geven voordat het Hallo-agent wordt gestart met het verzamelen van gebruikersgegevens.

### <a name="known-issues-and-drawbacks"></a>Bekende problemen en nadelen
Er zijn enkele gevallen waarbij de eindgebruiker Hallo mogelijk van invloed op TLS onderschept:

* De adresbalk Hallo van Hallo web browser groen tooact weergegeven uitgebreide validatie EV) certificaten (als een visuele aanwijzing dat u een vertrouwde website bezoeken. TLS-inspectie EV in deze toohello client, uitgeeft zodat de websites die gebruikmaken van validatiecertificaten werken normaal Hallo-certificaat niet dupliceren maar Hallo adresbalk geen groen weergegeven.  
* Openbare sleutel vastmaken (ook wel bekend als het certificaat vastmaken) zijn ontworpen toohelp om gebruikers te beschermen tegen man-in-the-middle-aanvallen en rogue certificeringsinstanties. Wanneer Hallo-basiscertificaat voor een vastgezette site komt niet overeen met een bekende goede CA hello, weigert Hallo browser Hallo verbinding met een fout. Omdat TLS worden onderschept, in feite een man-in-the-middle, mislukken deze verbindingen.
* Als gebruikers op Hallo vergrendelingspictogram in Hallo browser adres balk browser tooinspect Hallo site-informatie, zien ze een keten eindigt op de certificeringsinstantie Hallo toosign Hallo websitecertificaat gebruikt, maar in plaats daarvan een certificaatketen eindigt met Windows hello vertrouwde certificaatarchief.

tooreduce hello instanties van deze problemen, we bijhouden cloudservices en clienttoepassingen toouse bekend uitgebreide validatie of vastmaken van openbare sleutel en instrueert u Hallo Endpoint Agent tooavoid betrokken verbindingen onderscheppen. Zelfs in dergelijke gevallen echter nog steeds ontvangt u meldingen van Hallo gebruik van deze cloud-apps en Hallo hoeveelheid gegevens die worden overgedragen, maar omdat ze niet grondige geïnspecteerd geen details over het gebruik Hallo apps zijn beschikbaar zullen zijn.

## <a name="sending-data-toocloud-app-discovery"></a>Verzenden van gegevens tooCloud App Discovery
Als metagegevens zijn verzameld door Hallo-agent, het opgeslagen in de cache op de machine Hallo voor up tooone minuut of tot Hallo een grootte van 5MB gegevens in de cache heeft bereikt. Het is vervolgens gecomprimeerd en verzonden via een beveiligde verbinding toohello Cloud App Discovery-service.

Als Hallo-agent kan geen toocommunicate Hello Cloud App Discovery-service om welke reden, hello verzamelde metagegevens worden opgeslagen in een lokaal bestandscache die alleen toegankelijk zijn voor bevoegde gebruikers op Hallo-machine (zoals de groep Administrators Hallo).  
Hallo-agent automatisch pogingen tooresend Hallo in cache opgeslagen metagegevens totdat deze is ontvangen door Hallo Cloud App Discovery-service.

## <a name="receiving-hello-data-at-hello-service-end"></a>Ontvangen van gegevens aan Hallo service einde Hallo
Hallo-agents verifiëren toohello Cloud App Discovery-service gebruikt Hallo machine specifieke certificaat voor clientverificatie bovengenoemde en stuurt gegevens via een versleuteld kanaal.  
Hallo Cloud App Discovery service analysepijplijn processen metagegevens voor elke klant afzonderlijk door het partitioneren van het logisch via alle fasen van het Hallo-analysepijplijn.
Hallo geanalyseerd metagegevens stations Hallo diverse rapporten in Hallo-portal.

niet-verwerkte metagegevens Hallo en geanalyseerd Hallo metagegevens worden opgeslagen voor too180 dagen. Klanten kunnen bovendien toocapture hallo geanalyseerd metagegevens kiezen in een Azure blob storage-account van hun keuze.
Dit is handig voor offline-analyse van metagegevens, evenals langer bewaren van gegevens van Hallo.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Toegang tot Hallo-gegevens met behulp van hello Azure-portal
In een inspanning tookeep Hallo metagegevens verzameld veilige, alleen globale beheerders van Hallo tenant hebben standaard toegang toohello Cloud App Discovery-functie in hello Azure-portal.  
Beheerders kunnen echter toodelegate kiezen deze toegang tooother gebruikers of groepen.

> [!NOTE]
> Zie voor meer informatie [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Geen toegang tot Hallo gebruikersgegevens in Hallo-portal, moet beschikken over een Azure AD Premium-licentie.

## <a name="additional-resources"></a>Aanvullende resources
* [Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren](active-directory-cloudappdiscovery-whatis.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

