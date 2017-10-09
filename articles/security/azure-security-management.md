---
title: beveiliging van de aaaEnhance extern beheer in Azure | Microsoft Docs
description: In dit artikel worden de stappen beschreven voor het verbeteren van de beveiliging van extern beheer bij het beheren van Microsoft Azure-omgevingen, inclusief cloudservices, virtuele machines en aangepaste toepassingen.
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Beveiligingsbeheer in Azure
Azure-abonnees kunnen hun cloudomgevingen beheren vanaf meerdere apparaten, waaronder beheerwerkstations, de pc's van ontwikkelaars en zelfs apparaten van bevoegde eindgebruikers met taakspecifieke rechten. In sommige gevallen worden beheerfuncties uitgevoerd via het web gebaseerde consoles zoals Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). In andere gevallen is er mogelijk rechtstreekse verbindingen tooAzure van on-premises systemen via virtuele particuliere netwerken (VPN's), Terminal Services, protocollen van clienttoepassingen of (programmatisch) hello Azure Service Management API (SMAPI). Clienteindpunten kunnen bovendien zowel in een domein zijn samengevoegd als op zichzelf staand en niet-beheerd zijn, zoals tablets en smartphones.

Hoewel meerdere mogelijkheden voor toegang en beheer een groot aantal opties bieden, kan deze verscheidenheid tooa-cloudimplementatie aanzienlijke risico's kunt toevoegen. Het kan zijn moeilijk toomanage volgen en te controleren. Deze verscheidenheid kan ook leiden tot beveiligingsrisico's via ongereglementeerde toegang tooclient eindpunten die worden gebruikt voor het beheer van cloudservices. Het gebruik van algemene of persoonlijke werkstations voor het ontwikkelen en beheren van infrastructuur brengt onvoorspelbare bedreigingen met zich mee voor bijvoorbeeld surfen op internet (denk aan waterhole-aanvallen) of e-mail (zoals social engineering en phishing).

![][1]

Hallo potentiële voor aanvallen verhoogt in dit type omgeving, omdat het lastig tooconstruct beveiligingsbeleid en mechanismen tooappropriately toegang tooAzure interfaces (zoals SMAPI) beheren vanuit uiteenlopende eindpunten.

### <a name="remote-management-threats"></a>Bedreigingen bij extern beheer
Aanvallers proberen vaak bevoegde toogain toegang door accountreferenties (bijvoorbeeld via wachtwoord brute force, phishing en verzamelen van referenties) of door gebruikers in het uitvoeren van schadelijke code (bijvoorbeeld op schadelijke websites met truc station-by downloads of in schadelijke e-mailbijlagen). In een extern beheerde cloudomgeving account schendingen kunnen leiden tot tooan verhoogd risico vanwege tooanywhere, op elk gewenst moment toegang.

Zelfs nauwe besturingselementen op de primaire beheerdersaccounts, gebruikersaccounts lager niveau worden gebruikte tooexploit zwakke punten in de beveiligingsstrategie. Gebrek aan correcte beveiligingstraining kan ook leiden toobreaches via onbedoeld vrijgeven of blootstelling van gegevens van het account.

Wanneer een gebruikerswerkstation ook voor beheertaken wordt gebruikt, kan er op veel verschillende punten inbreuk plaatsvinden. Hiermee wordt aangegeven of een gebruiker is Hallo surfen, met 3rd van derden en open-source hulpprogramma's of openen van een schadelijk document-bestand met een Trojaans paard.

In het algemeen meeste gerichte aanvallen die leiden tot een inbreuk op de gegevens kan worden herleid toobrowser aanvallen, invoegtoepassingen (zoals Flash, PDF, Java) en spear phishing (e-mail) op desktopapparaten. Deze machines wellicht beheerniveau of serviceniveau machtigingen tooaccess live servers of netwerkapparaten gebruikt voor ontwikkeling of beheren van andere assets.

### <a name="operational-security-fundamentals"></a>Grondbeginselen van operationele beveiliging
Voor veiliger beheer en bewerkingen minimaliseert u de kwetsbaarheid van de client door Hallo aantal mogelijke toegangspunten te verminderen. Dit doet u aan de hand van de beveiligingsprincipes 'scheiding van functies' en 'scheiding van omgevingen'.

Scheid gevoelige functies van elkaar toodecrease Hallo kans dat een fout op één niveau tooa inbreuk in een andere leidt. Voorbeelden:

* Beheertaken moeten niet worden gecombineerd met activiteiten die tooa inbreuk (bijvoorbeeld malware in e-mail een beheerder die vervolgens een infrastructuurserver infecteert) kunnen leiden.
* Een werkstation dat wordt gebruikt voor zeer gevoelige bewerkingen mag geen Hallo hetzelfde systeem voor met een hoog risico, zoals surfen Hallo Internet gebruikt.

Verminder de kwetsbaarheid van het systeem Hallo door het verwijderen van onnodige software. Voorbeeld:

* Beheer, ondersteuning of ontwikkeling vereist geen installatie van een e-mailclient of andere productiviteitstoepassingen als het voornaamste doel van het apparaat Hallo toomanage cloudservices.

Clientsystemen die beheerder toegang tooinfrastructure onderdelen moeten worden onderworpen toohello strengst mogelijke beleid tooreduce beveiligingsrisico's. Voorbeelden:

* Beveiligingsbeleid kan instellingen voor Groepsbeleid die geen open internettoegang toestaan van Hallo-apparaat en het gebruik van een beperkende firewallconfiguratie bestaan.
* Gebruik VPN-verbindingen met internetprotocolbeveiliging (IPsec) als u directe toegang nodig hebt.
* Configureer afzonderlijke Active Directory-domeinen voor beheer en voor ontwikkeling.
* Isoleer en filter het netwerkverkeer van werkstations.
* Gebruik antimalwaresoftware.
* Multi-factorauthenticatie tooreduce Hallo risico van gestolen referenties worden geïmplementeerd.

Door toegangsbronnen te consolideren en niet-beheerde eindpunten te verwijderen, vereenvoudigt u ook uw beheertaken.

### <a name="providing-security-for-azure-remote-management"></a>Beveiliging voor extern beheer van Azure
Azure biedt beveiliging mechanismen tooaid beheerders die Azure-cloudservices en virtuele machines beheren. Tot deze methoden behoren onder meer:

* Verificatie en [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-configure.md).
* Bewaking, logboekregistratie en controle.
* Certificaten en gecodeerde communicatie.
* Een webbeheerportal.
* Filteren van netwerkpakketten.

Met de beveiligingsconfiguratie aan clientzijde en de datacenterimplementatie van een management-gateway is het mogelijk toorestrict en monitor beheerder toegang toocloud toepassingen en gegevens.

> [!NOTE]
> Bepaalde aanbevelingen in dit artikel kunnen leiden tot een toegenomen gebruik van gegevens, het netwerk en computerresources, en verhogen mogelijk de kosten van uw licentie of abonnement.
>
>

## <a name="hardened-workstation-for-management"></a>Beperkt werkstation voor beheer
Hallo doel beperking van een werkstation is tooeliminate alle maar Hallo meest essentiële functies nodig zijn voor toooperate, Hallo mogelijkheid op aanvallen zo klein mogelijk te maken. Systeembeveiliging omvat Hallo aantal geïnstalleerde services en toepassingen, uitvoeren van toepassingen, beperken netwerk toegang tooonly noodzakelijk is beperkt tot een minimum beperken en tegelijkertijd Hallo systeem toodate. Daarnaast kunt u door het gebruik van een beperkt werkstation voor beheer de beheertools en -activiteiten scheiden van taken voor eindgebruikers.

Binnen een on-premises bedrijfsomgeving, kunt u de kwetsbaarheid voor aanvallen van de fysieke infrastructuur via speciale beheernetwerken, serverruimten met kaarttoegang en werkstations die worden uitgevoerd in beveiligde gebieden van Hallo netwerk Hallo beperken. In een cloud of hybride IT-model kunnen toegewijd over beveiligde management-services worden veroorzaakt door complexere vanwege Hallo gebrek aan fysieke toegang tooIT resources. Implementatie van veiligheidsoplossingen vereist zorgvuldige softwareconfiguratie, op beveiliging gerichte processen en uitgebreid beleid.

Met behulp van een minimale bevoegdheden mogelijk software-en in een vergrendelde werkstation voor cloudbeheer, en voor toepassingsontwikkeling: Hallo risico op beveiligingsincidenten kan verminderen door te standaardiseren Hallo extern beheer en ontwikkeling omgevingen. Een beperkte werkstationsconfiguratie kan helpen voorkomen dat inbreuk op Hallo van accounts die de kritieke cloudbronnen gebruikte toomanage door te sluiten veel algemene mogelijkheden die worden gebruikt door schadelijke software en aanvallen. U kunt in het bijzonder [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) en Hyper-V-technologie toocontrol en gedrag van clientsystemen te isoleren en bedreigingen te verhelpen, waaronder e-mail en surfen op Internet.

Hallo beheerder een standaardgebruikersaccount (dat uitvoering beheerdersniveau blokkeert) wordt uitgevoerd op een beperkt werkstation en bijbehorende toepassingen worden beheerd door een lijst. Hallo basiselementen van een beperkt werkstation zijn als volgt:

* Actief scannen en patchen. Implementeer antimalwaresoftware, reguliere beveiligingslek-scans uitvoeren en alle werkstations bijwerken met behulp van de meest recente beveiligingsupdate Hallo op tijdige wijze.
* Beperkte functionaliteit. Verwijder alle toepassingen die niet nodig zijn en schakel onnodige (opstart)services uit.
* Beperkte netwerktoegang. Gebruik Windows Firewall-regels tooallow alleen geldige IP-adressen, poorten en URL's gerelateerde tooAzure management. Zorg ervoor dat inkomende externe verbindingen toohello werkstation worden geblokkeerd.
* Beperkte uitvoering van software. Toestaan dat een reeks vooraf gedefinieerde uitvoerbare bestanden die nodig zijn voor management toorun (bedoeld tooas 'standaard ' weigeren). Standaard moeten gebruikers geen machtiging toorun er programma's tenzij expliciet gedefinieerd in Hallo lijst voor toestaan.
* Minimale bevoegdheden. Gebruikers van beheerwerkstations mogen geen beheerdersbevoegdheden op de lokale machine Hallo zelf geen. Deze manier kunnen ze of niet wijzigen systeemconfiguratie Hallo Hallo systeembestanden, opzettelijk of per ongeluk.

U kunt dit afdwingen met behulp van [Group Policy Objects](https://www.microsoft.com/download/details.aspx?id=2612) (GPO's) in Active Directory Domain Services (AD DS) en u deze toepast via uw (lokale) management tooall management domeinaccounts.

### <a name="managing-services-applications-and-data"></a>Services, toepassingen en gegevens beheren
Configuratie van de Azure-cloud-services wordt uitgevoerd via hello Azure-portal of SMAPI, via Windows PowerShell-opdrachtregelinterface hello of een op maat gemaakte toepassing die van deze RESTful-interfaces gebruikmaakt. Services die gebruikmaken van deze methoden, zijn onder meer Azure Active Directory (Azure AD), Azure Storage, Azure Websites en Azure Virtual Network.

Geïmplementeerd op een virtuele Machine toepassingen bieden hun eigen clienthulpprogramma's en interfaces naar behoefte, zoals Hallo Microsoft Management Console (MMC), een enterprise-beheerconsole (zoals Microsoft System Center of Windows Intune) of een andere beheren toepassing: Microsoft SQL Server Management Studio, bijvoorbeeld. Deze hulpprogramma's bevinden zich meestal in een bedrijfsomgeving of clientnetwerk. Ze zijn mogelijk afhankelijk van specifieke netwerkprotocollen, zoals Remote Desktop Protocol (RDP), die directe, stateful verbindingen vereisen. Sommige kan webinterface die niet openbaar worden gepubliceerd of toegankelijk is via Internet Hallo hebben.

U kunt toegang tooinfrastructure en platform beheer van services in Azure beperken met behulp van [multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication.md), [X.509-beheercertificaten](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/), en firewall-regels. Hello Azure-portal en SMAPI vereisen Transport Layer Security (TLS). Services en toepassingen die u in Azure implementeert vereisen echter u tootake van beschermende maatregelen die van toepassing op basis van uw toepassing zijn. Deze methoden kunnen vaak eenvoudiger worden ingeschakeld met behulp van een gestandaardiseerde configuratie voor beperkte werkstations.

### <a name="management-gateway"></a>Beheergateway
toocentralize alle administratieve toegang tot en controle en logboekregistratie te vereenvoudigen, kunt u een speciaal implementeren [extern bureaublad-Gateway](https://technet.microsoft.com/library/dd560672) (RD-Gateway)-server in uw on-premises netwerk, verbonden tooyour Azure-omgeving.

Een Extern bureaublad-gateway is een op beleid gebaseerde RDP-proxyservice die beveiligingsvereisten afdwingt. Door een Extern bureaublad-gateway samen met netwerktoegangsbeveiliging (NAP) voor Windows-servers te implementeren, zorgt u ervoor dat alleen clients die voldoen aan de specifieke criteria voor beveiligingsstatus, tot stand gebracht met groepsbeleidsobjecten (GPO's) van Active Directory Domain Services (AD DS), verbinding kunnen maken. Daarnaast doet u het volgende:

* Inrichten van een [Azure-beheercertificaat](http://msdn.microsoft.com/library/azure/gg551722.aspx) op Hallo RD-Gateway zodat deze alleen Hallo-host toegestane tooaccess hello Azure-portal.
* Deelnemen aan Hallo RD-Gateway toohello dezelfde [beheerdomein](http://technet.microsoft.com/library/bb727085.aspx) zoals Hallo werkstations van beheerders. Dit is nodig wanneer u een site-naar-site IPsec VPN of ExpressRoute gebruikt binnen een domein met een eenzijdige vertrouwensrelatie tooAzure AD, of als u referenties federeert tussen uw on-premises exemplaar van AD DS en Azure AD.
* Configureer een [verificatiebeleid voor clientverbindingen](http://technet.microsoft.com/library/cc753324.aspx) toolet Hallo RD-Gateway controleert of Hallo client machinenaam geldig (domein toegevoegd) en toegestane tooaccess hello Azure-portal.
* Gebruik IPsec voor [Azure VPN](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther beheerverkeer beschermen tegen afluisteren en token diefstal of u kunt een geïsoleerde internetkoppeling tot stand via [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* Schakel Multi-Factor Authentication (via [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) of smartcardverificatie in voor beheerders die zich via de Extern bureaublad-gateway aanmelden.
* Bron configureren [IP-adresbeperkingen](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) of [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) in Azure toominimize Hallo aantal toegestane eindpunten voor beheer.

## <a name="security-guidelines"></a>Richtlijnen voor beveiliging
In het algemeen sluit werkstations van beheerders toosecure voor gebruik met Hallo cloud vergelijkbaar toohello uitgangspunten die gelden voor een is on-premises werkstation, zoals een minimale build en beperkte machtigingen. Sommige unieke aspecten van cloudbeheer zijn meer overeenkomst vertonen tooremote of out-of-band-enterprise management. Het gaat hierbij om hello gebruiken en controleren van referenties, verbeterde beveiliging van externe toegang en detectie van dreigingen en -antwoord.

### <a name="authentication"></a>Authentication
U kunt Azure aanmelding beperkingen tooconstrain bron-IP-adressen gebruiken voor toegang tot Systeembeheer en toegangsaanvragen te controleren. toohelp Azure identificeren beheerclients (werkstations en/of toepassingen), kunt u zowel SMAPI (via de klant ontwikkelde hulpprogramma's zoals Windows PowerShell-cmdlets) en hello Azure portal toorequire clientzijde management certificaten toobe configureren geïnstalleerd bovendien tooSSL certificaten. We raden u ook aan Multi-Factor Authentication verplicht te stellen voor beheerderstoegang.

Sommige toepassingen of services die u in Azure implementeert, hebben wellicht hun eigen verificatiemethoden voor toegang voor zowel eindgebruikers als beheerders, terwijl andere volledig gebruikmaken van de mogelijkheden die Azure AD biedt. Afhankelijk van of u referenties via Active Directory Federation Services (AD FS), federeert zijn adreslijstsynchronisatie gebruikt of gebruikersaccounts uitsluitend in Hallo cloud, met [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (deel van Azure AD Premium) kunt u de levenscycli van identiteiten tussen Hallo resources beheren.

### <a name="connectivity"></a>Connectiviteit
Verschillende mechanismen zijn beschikbaar toohelp beveiligde client verbindingen tooyour virtuele netwerken in Azure. Twee van deze methoden [site-naar-site VPN](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) en [punt-naar-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S) Hallo gebruik van branche inschakelen standaard IPsec (S2S) of Hallo [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) voor codering en tunneling. Wanneer Azure verbinding management toopublic gerichte Azure-services zoals hello Azure-portal maakt, vereist Azure Hypertext Transfer Protocol Secure (HTTPS).

Een zelfstandig, beperkt werkstation dat geen tooAzure verbinding via een extern bureaublad-Gateway moet Hallo op basis van SSTP punt-naar-site VPN-toocreate Hallo initiële verbinding toohello Azure Virtual Network gebruiken en vervolgens tot stand brengen RDP verbinding tooindividual virtuele machines uit met de Hallo VPN-tunnel.

### <a name="management-auditing-vs-policy-enforcement"></a>Beheercontrole versus beleid afdwingen
Er zijn in principe twee methoden voor het toosecure beheerprocessen: controle en beleid afdwingen. Als u beide methoden toepast, beschikt u over uitgebreide beheermogelijkheden, maar dit is wellicht niet in alle gevallen mogelijk. Elke methode biedt bovendien verschillende niveaus van risico's, kosten en tijdsinvestering met het beheren van beveiliging, met name omdat deze zich toohello niveau van vertrouwen dat wordt geplaatst in gebruikers en de systeemarchitectuur verhoudt.

Bewaking, logboekregistratie en controle bieden een basis voor het bijhouden en begrijpen van beheeractiviteiten, maar deze mogelijk niet altijd haalbaar tooaudit alle acties in detail vanwege de hoeveelheid gegevens die zijn gegenereerd toohello voltooien. Is een aanbevolen procedure echter controle Hallo effectiviteit van Hallo management-beleid.

Als u beleid afdwingt dat strikt toegangsbeheer omvat, implementeert u programmatische mechanismen waarmee wordt bepaald welke acties beheerders mogen uitvoeren. Bovendien zorgt dergelijk beleid er mede voor dat alle mogelijke beschermingsmaatregelen worden gebruikt. Logboekregistratie biedt afdwingen in toevoeging tooa record van wie welke vanaf waar en wanneer is. Logboekregistratie ook kunt u informatie over hoe beheerders omgaan met beleidsregels tooaudit en vergelijken en biedt bewijs van activiteiten

## <a name="client-configuration"></a>Clientconfiguratie
Voor beperkte werkstations raden we drie primaire configuraties aan. Hallo grootste differentiators daartussen zijn kosten, bruikbaarheid en toegankelijkheid, terwijl een vergelijkbare beveiligingsprofiel behouden over alle opties. Hallo volgende tabel geeft een korte analyse van de voordelen en risico's tooeach Hallo. (Houd er rekening mee dat 'zakelijke PC' verwijst van tooa standaard PC desktopconfiguratie die wordt geïmplementeerd voor alle domeingebruikers, ongeacht de rol.)

| Configuratie | Voordelen | Nadelen |
| --- | --- | --- |
| Zelfstandig, beperkt werkstation |Strak beheerd werkstation |Hogere kosten voor speciale desktop-pc’s |
| - | Minder risico op misbruik van zwakke plekken in toepassingen |Meer tijd/werk nodig voor beheer |
| - | Duidelijke scheiding van functies | - |
| Zakelijke pc als virtuele machine |Lagere kosten voor hardware | - |
| - | Scheiding van rollen en toepassingen | - |
| Windows-toogo met BitLocker-stationsversleuteling |Compatibiliteit met de meeste pc's |Bijhouden van assets |
| - | Kosteneffectiviteit en draagbaarheid | - |
| - | Geïsoleerde beheeromgeving |- |

Het is belangrijk dat hello beperkt werkstation Hallo host is en niet hello Gast, er is niets tussen Hallo host operationele systeem en het Hallo-hardware. Hallo 'schone bron principe' volgen betekent (ook wel ' veilige oorsprong') dat Hallo-host moet worden Hallo meest gehard. Anders is hello beperkte werkstation (Gast) onderwerp tooattacks op Hallo systeem waarop deze wordt gehost.

U kunt verder scheiden beheerfuncties door speciale systeemkopieën voor alle beperkte werkstations waarvoor alleen Hallo hulpprogramma's en machtigingen die nodig zijn voor het beheren van Azure selecteren en cloudtoepassingen, met specifieke lokale AD DS-groepsbeleidsobjecten voor Hallo taken die nodig zijn.

Voor IT-omgevingen die geen on-premises infrastructuur (bijvoorbeeld geen toegang tot tooa lokaal AD DS-exemplaar voor GPO's omdat alle servers in de cloud Hallo), hebben een service zoals [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) kunt vereenvoudigen implementeren en onderhouden werkstationconfiguraties.

### <a name="stand-alone-hardened-workstation-for-management"></a>Zelfstandig, beperkt werkstation voor beheer
Met een zelfstandig, beperkt werkstation hebben beheerders een pc of laptop die ze voor beheertaken gebruiken en een andere, afzonderlijke pc of laptop voor andere taken. Een werkstation toegewezen toomanaging uw Azure-services hoeft geen andere toepassingen die zijn geïnstalleerd. Daarnaast helpt het gebruik van werkstations die ondersteuning bieden voor een [Trusted Platform Module](https://technet.microsoft.com/library/cc766159) (TPM) of soortgelijke cryptografische technologie op hardwareniveau, bij de apparaatverificatie en het voorkomen van bepaalde aanvallen. Kan TPM bovendien volledig volume beveiliging van het systeemstation Hallo ondersteuning met behulp van [BitLocker-stationsversleuteling](https://technet.microsoft.com/library/cc732774.aspx).

In Hallo zelfstandig, beperkt werkstation scenario (Zie hieronder) Hallo lokaal exemplaar van Windows Firewall (of een niet-Microsoft-clientfirewall) is geconfigureerd tooblock binnenkomende verbindingen, zoals RDP. Hallo beheerder toohello kunt aanmelden beperkt werkstation en start een RDP-sessie die verbinding tooAzure maakt na het tot stand brengen van een VPN verbinding maken met een Azure-netwerk, maar zich niet aanmelden tooa zakelijke PC en gebruik RDP tooconnect toohello gehard werkstation zelf.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Zakelijke pc als virtuele machine
In gevallen waarin een afzonderlijk zelfstandig, beperkt werkstation kosten aan Hallo belemmering vormen of onhandig verbonden zijn, kan beperkte werkstation een virtuele machine tooperform niet-administratieve taken hosten.

![][3]

tooavoid diverse beveiligingsrisico's die voortvloeien uit het gebruik van een werkstation voor Systeembeheer en voor andere dagelijkse taken, u kunt een Windows Hyper-V virtuele machine toohello gehard werkstation. Deze virtuele machine kan worden gebruikt als zakelijke PC Hallo. Hallo bedrijfsomgeving PC kan geïsoleerd blijven van Hallo Host vermindert de kwetsbaarheid voor aanvallen en verwijdert u de dagelijkse activiteiten van Hallo gebruiker (zoals e-mail) uit het hetzelfde systeem worden uitgevoerd als gevoelige beheertaken.

Hallo zakelijke PC virtuele machine wordt uitgevoerd in een beveiligde ruimte en biedt de benodigde gebruikerstoepassingen. Hallo host blijft een 'schone bron' en past strikt netwerkbeleid in Hallo basisbesturingssysteem (bijvoorbeeld het blokkeren van toegang RDP van Hallo virtuele machine).

### <a name="windows-toogo"></a>Windows tooGo
Een andere alternatieve toorequiring een zelfstandig, beperkt werkstation toouse is een [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) station, een functie die ondersteuning biedt voor een functie van de opstarten vanaf USB aan clientzijde. Windows tooGo kan gebruikers een compatibele PC tooboot tooan geïsoleerde installatiekopie uitvoeren vanaf een versleuteld USB-flashstation. Biedt extra gebruiksmogelijkheden voor eindpunten voor extern beheer omdat Hallo installatiekopie volledig kan worden beheerd door een zakelijke IT-groep met strikt beveiligingsbeleid, een minimale build van het besturingssysteem en TPM-ondersteuning.

In onderstaande afbeelding Hallo is Hallo draagbare installatiekopie een domein systeem vooraf geconfigureerde tooconnect alleen tooAzure is, vereist dat multi-factor authentication-server en alle niet-management-verkeer blokkeert. Als een gebruiker opnieuw is opgestart hello dezelfde PC toohello standaard zakelijke installatiekopie en pogingen toegang tot extern bureaublad-Gateway beheerhulpprogramma's van Azure, is Hallo sessie geblokkeerd. Windows tooGo wordt Hallo hoofdniveau besturingssysteem en er zijn geen extra lagen vereist (hostbesturingssysteem system, hypervisor, virtuele machine) zijn die mogelijk kwetsbaarder toooutside aanvallen.

![][4]

Het is belangrijk toonote dat USB-flashstations sneller zoekraakt dan een gemiddelde desktop-PC zijn. Gebruik van BitLocker tooencrypt Hallo gehele volume, samen met een sterk wachtwoord, maakt minder waarschijnlijk dat een aanvaller Hallo station installatiekopie voor schadelijke doeleinden gebruiken kunt. Bovendien, als Hallo USB-flashstation zoekraakt, intrekken en [uitgeven van een nieuw beheercertificaat](https://technet.microsoft.com/library/hh831574.aspx) samen met een snelle wachtwoord opnieuw instellen van blootstelling kan verminderen. Administratieve controlelogboeken opgeslagen in Azure, niet op Hallo-client, verdere vermindering van mogelijk gegevensverlies.

## <a name="best-practices"></a>Aanbevolen procedures
Houd rekening met Hallo aanvullende richtlijnen te volgen bij het beheren van toepassingen en gegevens in Azure.

### <a name="dos-and-donts"></a>Wat u wel en wat u niet moet doen
Niet, wordt ervan uitgegaan dat omdat een werkstation dat is vergrendeld andere algemene beveiligingsvereisten geen toobe voldaan hoeft. Hallo potentieel risico is hoger vanwege de verhoogde toegangsniveaus waarover beheerdersaccounts over het algemeen beschikken. Voorbeelden van risico's en alternatieve veilige handelswijzen worden weergegeven in onderstaande tabel voor Hallo.

| Niet doen | Wel doen |
| --- | --- |
| Verzend referenties voor beheerderstoegang of andere geheime informatie (bijvoorbeeld SSL- of beheercertificaten) niet via e-mail |Waarborg de vertrouwelijkheid door gebruikersnamen en wachtwoorden voor accounts mondeling door te geven (maar spreek ze niet op iemands voicemail in), voer een externe installatie van client/server-certificaten uit (via een gecodeerde sessie), voer downloads uit vanaf een beveiligde netwerkshare of distribueer gegevens handmatig via verwisselbare media. |
| - | Beheer de levenscycli van uw beheercertificaat proactief. |
| Sla wachtwoorden niet op in toepassingsopslag (zoals een spreadsheet, een SharePoint-site of een bestandsshare) als ze niet zijn versleuteld of er geen hash-bewerking op is uitgevoerd. |Stel beveiligingsbeheer en beleid beperken van het systeem en ze tooyour ontwikkelomgeving toepassen. |
| - | Gebruik [Enhanced Mitigation Experience Toolkit 5.5](https://technet.microsoft.com/security/jj653751) certificaat vastmaken regels tooensure toegangsmachtigingen tooAzure SSL/TLS-sites. |
| Deel geen accounts en wachtwoorden tussen beheerders, en gebruik wachtwoorden niet voor meerdere gebruikersaccounts of services, vooral als deze betrekking hebben op sociale media of andere niet-beheeractiviteiten. |Uw Azure-abonnement voor een specifieke toomanage voor Microsoft-account maken: een account dat niet wordt gebruikt voor persoonlijke e-mailadres. |
| Verzend configuratiebestanden niet via e-mail. |Configuratiebestanden en -profielen moeten worden geïnstalleerd vanuit een vertrouwde bron (bijvoorbeeld een gecodeerd USB-flashstation), niet via een methode waarmee gemakkelijk inbreuk kan worden gepleegd, zoals e-mail. |
| Gebruik geen zwakke of eenvoudige wachtwoorden. |Dwing beleid voor sterke wachtwoorden, verloopcycli (changeon-first-use), consoletime-outs en automatische accountvergrendeling af. Gebruik een beheersysteem met clientwachtwoorden met Multi-Factor Authentication voor wachtwoordtoegang tot de kluis. |
| Management poorten toohello Internet niet worden blootgesteld. |Vergrendelen van Azure-poorten en IP-adressen toorestrict management toegang. Zie voor meer informatie, Hallo [Azure Network Security](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) witboek. |
| - | Gebruik voor alle beheerverbindingen firewalls, VPN-verbindingen en NAP. |

## <a name="azure-operations"></a>Azure-bewerkingen
Bij Microsoft gebruiken de technici en ondersteuningsmedewerkers die toegang hebben tot de productiesystemen van Azure, [beperkte werkstation-pc's met virtuele machines](#stand-alone-hardened-workstation-for-management) voor toegang tot het interne bedrijfsnetwerk en toepassingen (zoals e-mail, intranet, enz.). Alle beheerwerkstations hebben TPM's, Hallo hostopstartstation is versleuteld met BitLocker en ze lid tooa speciale organisatie-eenheid (OE) in het primaire bedrijfsdomein van Microsoft zijn.

Systeembeveiliging wordt afgedwongen via groepsbeleid en software wordt centraal bijgewerkt. Voor controle en analyse worden gebeurtenislogboeken (zoals beveiliging en AppLocker) verzameld vanaf de beheerwerkstations en tooa centrale locatie opgeslagen.

Bovendien zijn speciale jumpboxes op het netwerk van Microsoft waarvoor tweeledige verificatie van de gebruikte tooconnect tooAzure productienetwerk.

## <a name="azure-security-checklist"></a>Controlelijst voor Azure-beveiliging
Hallo-aantal taken die beheerders op een beperkt werkstation uitvoeren kunnen minimaliseren helpt de kwetsbaarheid Hallo van uw ontwikkel- en beheeromgeving minimaliseren. Gebruik Hallo technologieën toohelp na uw beperkte werkstation beveiligen:

* Verbeterde beveiliging van Internet Explorer. Hallo Internet Explorer-browser (of een webbrowser eigenlijk) is een belangrijk toegangspunt voor schadelijke code vanwege tooits uitgebreide interactie met externe servers. Neem uw clientbeleid onder de loep en dwing het volgende af: gebruik van de beveiligde modus, uitschakelen van invoegtoepassingen, uitschakelen van bestandsdownloads en toepassing van [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx)-filteren. Zorg ervoor dat er beveiligingswaarschuwingen worden weergegeven. Profiteer van internetzones en maak een lijst met vertrouwde sites waarvoor u afdoende beveiliging hebt geconfigureerd. Blokkeer alle andere sites en code in de browser, zoals ActiveX en Java.
* Standaardgebruiker. Uitvoeren als standaardgebruiker een aantal voordelen heeft, is Hallo belangrijkste voordeel dat het stelen van beheerdersreferenties via schadelijke software moeilijker wordt. Bovendien een standaardgebruikersaccount geen verhoogde bevoegdheden op Hallo basisbesturingssysteem en veel configuratie-opties en API's zijn standaard vergrendeld.
* AppLocker. U kunt [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict Hallo programma's en scripts die gebruikers kunnen uitvoeren. U kunt AppLocker uitvoeren in de controlemodus of in de afdwingingsmodus. Standaard bevat AppLocker een regel voor toestaan waarmee gebruikers die een token toorun admin hebben alle code op Hallo-client. Deze regel tooprevent beheerders zichzelf buitensluiten bestaat en dat alleen tooelevated tokens van toepassing is. Zie ook Code-integriteit als onderdeel van de [kernbeveiliging](http://technet.microsoft.com/library/dd348705.aspx) van Windows Server.
* Programmacode ondertekenen. Ondertekening van de programmacode van alle hulpprogramma's en scripts die door beheerders worden gebruikt, biedt een goed te beheren methode voor het implementeren van beleid voor het vergrendelen van toepassingen. Hashes zich niet aan aan snelle wijzigingen toohello code en bestandspaden bieden geen een hoog niveau van beveiliging. AppLocker-regels moeten worden gecombineerd met een PowerShell [uitvoeringsbeleid](http://technet.microsoft.com/library/ee176961.aspx) die alleen bepaalde ondertekende codes en scripts toobe [uitgevoerd](http://technet.microsoft.com/library/hh849812.aspx).
* Groepsbeleid. Maken van een overkoepelend beheerbeleid dat is toegepast tooany domein werkstation dat wordt gebruikt voor beheer (en blokkeer de toegang vanaf alle overige) en toouser accounts op die werkstations worden geverifieerd.
* Inrichting met verbeterde beveiliging. Beveilig uw beperkte werkstation basisinstallatiekopie toohelp beveiligen tegen knoeien. Gebruik beveiligingsmaatregelen zoals versleuteling en isolatie toostore installatiekopieën, virtuele machines en scripts en beperken van toegang (mogelijk gebruik een controleerbare-in/uitchecken proces).
* Patchen. Waarborg een consistente build (of bewaar afzonderlijke installatiekopieën voor ontwikkeling, bewerkingen en andere beheertaken), scan op wijzigingen en malware regelmatig, Hallo toodate opgebouwd houden en activeer apparaten alleen als dat nodig is.
* Versleuteling. Zorg ervoor dat beheerwerkstations een TPM-toomore veilig inschakelen [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) en BitLocker. Als u van Windows tooGo gebruikmaakt, gebruikt u alleen versleutelde USB-sleutels in combinatie met BitLocker.
* Beheer. Gebruik van AD DS-groepsbeleidsobjecten toocontrol alle Hallo beheerders hun Windows-interfaces, zoals het delen van bestanden. Voer voor beheerwerkstations controle-, bewakings- en logboekregistratieprocessen uit. Houd toegang en gebruik van alle beheerders en ontwikkelaars bij.

## <a name="summary"></a>Samenvatting
Met behulp van een beperkte werkstationconfiguratie voor het beheer van uw Azure-cloudservices, virtuele machines en toepassingen kunt u diverse risico's en bedreigingen voorkomen die het op afstand beheren van kritieke IT-infrastructuur met zich meebrengt. Zowel Azure als Windows bieden dat u van toohelp gebruikmaken kunt mechanismen beschermen en controleren van communicatie, verificatie en clientgedrag.

## <a name="next-steps"></a>Volgende stappen
Hallo volgende resources zijn beschikbaar tooprovide meer algemene informatie over Azure en gerelateerde Microsoft-services in toevoeging toospecific items waarnaar wordt verwezen in dit artikel:

* [Bevoegde toegang beveiligen](https://technet.microsoft.com/library/mt631194.aspx) – Hallo technische informatie ophalen voor het ontwerpen en bouwen van een beveiligd beheerwerkstation voor Azure-beheer
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) : meer informatie over de mogelijkheden van Azure-platform die hello beveiligen Azure-infrastructuur en Hallo werkbelastingen die uitgevoerd op Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) --Microsoft beveiligingsproblemen, met inbegrip van problemen met Azure, worden gerapporteerd of via e-mail te[secure@microsoft.com](mailto:secure@microsoft.com)
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Blijf toodate op Hallo nieuwste van Azure-beveiliging

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
