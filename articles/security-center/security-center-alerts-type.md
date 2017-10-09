---
title: aaaSecurity waarschuwingen per type in Azure Security Center | Microsoft Docs
description: Dit artikel worden de verschillende soorten beveiligingswaarschuwingen die beschikbaar zijn in Azure Security Center Hallo.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Beveiligingswaarschuwingen in Azure Security Center
In dit artikel helpt u bij toounderstand Hallo verschillende soorten beveiligingswaarschuwingen en verwante inzichten die beschikbaar in Azure Security Center zijn. Voor meer informatie over hoe toomanage waarschuwingen en incidenten, Zie [beheren en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset van geavanceerde detecties upgrade tooAzure Security Center Standard. Er is een gratis proefversie voor 60 dagen beschikbaar. tooupgrade, selecteer **prijscategorie** in Hallo [beveiligingsbeleid](security-center-policies.md). meer, Zie Hallo toolearn [pagina met prijzen](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Welk type waarschuwingen zijn er beschikbaar?
Azure Security Center gebruikt diverse [detectiemogelijkheden](security-center-detection-capabilities.md) tooalert klanten toopotential aanvallen die gericht is op hun omgeving. Deze waarschuwingen bevatten waardevolle informatie over Hallo wat geactiveerd Hallo Hallo-resources die zijn gericht, waarschuwing en bron van de aanval Hallo Hallo. Hallo informatie is opgenomen in een waarschuwing varieert op basis van Hallo type analytics gebruikt toodetect Hallo bedreiging. Incidenten kunnen ook aanvullende contextuele informatie bevatten die nuttig kan zijn bij het onderzoeken van een bedreiging.  In dit artikel bevat informatie over Hallo Waarschuwingstypen te volgen:

* VMBA (Virtual Machine Behavioral Analysis)
* Netwerkanalyse
* Resourceanalyse
* Contextuele informatie

## <a name="virtual-machine-behavioral-analysis"></a>VMBA (Virtual Machine Behavioral Analysis)
Azure Security Center kunnen gedragsanalyse tooidentify geknoeid met resources op basis van de analyse van de virtuele machine-gebeurtenislogboeken gebruiken. Bijvoorbeeld procesgebeurtenissen en aanmeldgebeurtenissen. Daarnaast is de correlatie met andere signalen toocheck voor ondersteunend bewijs van een wijdverbreid campagne.

> [!NOTE]
> Lees [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md) voor meer informatie over de werking van de detectiemogelijkheden van Security Center.
>

### <a name="crash-analysis"></a>Crashanalyse
Crashdump geheugenanalyse is een methode waarmee toodetect geavanceerde malware die kunnen tooevade traditionele beveiligingsoplossingen. Verschillende soorten malware probeer tooreduce Hallo kans wordt gedetecteerd door antivirusproducten door nooit toodisk schrijven, of versleutelen softwareonderdelen toodisk geschreven. Hierdoor Hallo malware moeilijk toodetect via traditionele antimalware benaderingen. Dit soort schadelijke software kan echter worden gedetecteerd met behulp van geheugenanalyse, omdat de malware moet traceringen laat in het geheugen van de volgorde toofunction.

Wanneer software vastloopt, bevat een crashdump een gedeelte van het geheugen tijdens het Hallo Hallo crash. Hallo crash kan worden veroorzaakt door schadelijke software, algemene toepassing of problemen met het systeem. Door te analyseren Hallo geheugen in Hallo crashdump, Security Center detecteren technieken tooexploit beveiligingslekken in software gebruikt, toegang krijgen tot vertrouwelijke gegevens en ongemerkt binnen een verdachte computer blijven behouden. Dit wordt bereikt met minimale gevolgen toohosts zoals Hallo analyse wordt uitgevoerd door Hallo Security Center back-end.

Hallo volgende velden zijn algemene toohello crashdump waarschuwing voorbeelden die worden verderop in dit artikel wordt weergegeven:

* DUMPBESTAND: Naam van Hallo crashdumpbestand.
* PROCESNAAM: Naam van Hallo proces gecrasht.
* PROCESSVERSION: Versie van Hallo proces gecrasht.

### <a name="shellcode-discovered"></a>Shellcode gedetecteerd
Shellcode is Hallo nettolading die wordt uitgevoerd nadat de malware gebruikmaakt van een software-kwetsbaarheid. Deze waarschuwing geeft aan dat de crashdumpanalyse uitvoerbare code heeft gedetecteerd dat gedrag vertoont dat gewoonlijk wordt uitgevoerd door schadelijke nettoladingen. Hoewel niet-schadelijke software dit gedrag kan vertonen, is het niet gebruikelijk voor normale softwareontwikkelingsprocedures.

Hallo Shellcode waarschuwing voorbeeld biedt Hallo extra veld te volgen:

* ADRES: Hallo locatie in het geheugen van Hallo shellcode.

Dit is een voorbeeld van dit type waarschuwing:

![Waarschuwing voor shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Module-hijacking gedetecteerd
Windows gebruikt dynamic link libraries (DLL's) tooallow software tooutilize algemene Windows system-functionaliteit. DLL-bestand Kaapt treedt op wanneer wijzigt malware Hallo DLL load volgorde tooload schadelijke nettoladingen in het geheugen, waarbij willekeurige code kan worden uitgevoerd. Deze waarschuwing geeft aan dat Hallo crash-dump analyse een gelijknamige module die is geladen uit twee verschillende paden gedetecteerd. Een van de paden Hallo geladen afkomstig is van een algemene binaire locatie van de Windows-systeem.

Legitieme softwareontwikkelaars wijzigen van tijd tot tijd Hallo DLL laadvolgorde omwille van de niet-schadelijke zoals instrumenteren, het uitbreiden van het Windows-besturingssysteem Hallo of het uitbreiden van een Windows-toepassing. toohelp onderscheid maken tussen schadelijke en mogelijk onschadelijk wijzigingen toohello laadvolgorde van DLL-bestand, Azure Security Center controleert of een module geladen tooa verdachte profiel voldoet. Hallo resultaat van deze controle wordt aangeduid met 'Handtekening'-veld Hallo van Hallo waarschuwing en wordt weergegeven in Hallo ernst van waarschuwing hello, beschrijving van waarschuwing en waarschuwing herstelstappen uit. tooresearch of Hallo module legitieme of schadelijke, analyseren Hallo op schijf kopie van Hallo module kaapt. U kunt bijvoorbeeld controleren of de digitale handtekening van het bestand hello of een antivirusprogramma scan uit te voeren.

Bovendien toohello algemene velden die in eerdere 'Shellcode gedetecteerd' Hallo-sectie beschreven, biedt deze waarschuwing Hallo velden te volgen:

* HANDTEKENING: Hiermee wordt aangegeven als Hallo kaapt module tooa verdacht gedrag profiel voldoet.
* HIJACKEDMODULE: naam Hallo Hallo gehackt module voor Windows-systeem.
* HIJACKEDMODULEPATH: Hallo pad Hallo gehackt module voor Windows-systeem.
* HIJACKINGMODULEPATH: Hallo pad van Hallo hackprogramma module.

Dit is een voorbeeld van dit type waarschuwing:

![Module-hijackingswaarschuwing](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Onechte Windows-module gedetecteerd
Schadelijke software kunt algemene namen van de binaire bestanden Windows-systeem (bijvoorbeeld SVCHOST. EXE) of modules (bijvoorbeeld NTDLL. DLL-bestand) te*overlopen* en Hallo aard van schadelijke software van systeembeheerders Hallo worden verborgen. Deze waarschuwing geeft aan dat Hallo crash-dump analyse dat bestand Hallo crashdump bevat modules die Windows system modulenamen gebruiken detecteert, maar die niet voldoen aan andere criteria die kenmerkend voor Windows-modules zijn. Analyseren van Hallo op schijf kopie van onechte Hallo-module kan bieden meer informatie over Hallo legitieme of schadelijke aard van deze module. De analyse kan het volgende omvatten:

* Bevestig dat betrokken Hallo-bestand wordt geleverd als onderdeel van een legitieme softwarepakket.
* Controleer of de digitale handtekening Hallo-bestand.
* Een antivirusprogramma scan uitvoeren op Hallo-bestand.

Bovendien toohello gemeenschappelijke velden eerder beschreven onder 'Shellcode gedetecteerd' hello, biedt deze waarschuwing Hallo aanvullende velden te volgen:

* DETAILS: Beschrijft of de metagegevens van de module Hallo geldig is en of Hallo-module is geladen uit een systeempad.
* NAAM: naam van Hallo van Hallo onechte Windows-module.
* PAD: Hallo pad toohello onechte Windows-module.

Deze waarschuwing ook worden opgehaald en weergegeven van bepaalde velden op Hallo-module PE-header, zoals 'CONTROLESOM' en 'Tijdstempel'. Deze velden worden alleen weergegeven als Hallo velden aanwezig in Hallo-module zijn. Zie Hallo [Microsoft PE en COFF-specificatie](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) voor meer informatie over deze velden.

Dit is een voorbeeld van dit type waarschuwing:

![Onechte Windows-waarschuwing](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Gewijzigd binair systeembestand gedetecteerd
Schadelijke software kan core system binaire bestanden in de volgorde toocovertly toegang tot gegevens te wijzigen of ongemerkt behouden blijven op een geïnfecteerd systeem. Deze waarschuwing geeft aan dat Hallo crash-dump analyse heeft gedetecteerd dat core Windows-besturingssysteem binaire bestanden zijn gewijzigd in het geheugen of op schijf.

Legitieme softwareontwikkelaars wijzigen van tijd tot tijd systeemmodules in het geheugen voor niet-kwaadwillende redenen, zoals omzeilingen of voor de compatibiliteit van toepassingen. toohelp onderscheid maken tussen schadelijke en mogelijk legitieme modules, Azure Security Center controleert of de gewijzigde module Hallo tooa verdachte profiel voldoet. Hallo-resultaat van deze controle wordt aangegeven door Hallo ernst van waarschuwing hello, beschrijving van waarschuwing en waarschuwing herstelstappen uit.

Bovendien toohello gemeenschappelijke velden eerder beschreven onder 'Shellcode gedetecteerd' hello, biedt deze waarschuwing Hallo aanvullende velden te volgen:

* MODULENAAM: Naam van Hallo gewijzigd binaire systeem.
* MODULEVERSION: Versie van Hallo gewijzigd binaire systeem.

Dit is een voorbeeld van dit type waarschuwing:

![Waarschuwing voor binair systeembestand](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Verdachte processen uitgevoerd
Beveiligingscentrum identificeert een verdachte proces dat wordt uitgevoerd op de virtuele doelmachine Hallo en een waarschuwing. Hallo-detectie niet zoeken naar specifieke Hallo-naam, maar ziet er voor de parameter Hallo uitvoerbaar bestand. Dus zelfs als de aanvaller Hallo wijzigt de naam van uitvoerbare Hallo, kunt Security Center nog steeds detecteren Hallo verdachte proces.

Dit is een voorbeeld van dit type waarschuwing:

![Waarschuwing dat er verdachte processen worden uitgevoerd](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Query's op meerdere domeinaccounts uitgevoerd
Security Center kunt detecteren meerdere probeert tooquery Active Directory-domeinaccounts die iets is doorgaans uitgevoerd door aanvallers tijdens netwerk reconnaissance. Aanvallers kunnen gebruikmaken van deze techniek tooquery hello tooidentify Hallo domeingebruikers, Hallo beheerder domeinaccounts identificeren, Hallo-computers die domeincontrollers en ook identificeren aan de Hallo potentiële domein vertrouwensrelatie heeft met andere domeinen te identificeren.

Dit is een voorbeeld van dit type waarschuwing:

![Waarschuwing over meerdere domeinaccounts](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Leden van de groep Lokale beheerders zijn geïnventariseerd

Security Center gaat tootrigger een waarschuwing wanneer Hallo beveiligingsgebeurtenis 4798, in Windows Server 2016 en Windows 10 is geactiveerd. Dit gebeurt wanneer lokale-beheerdersgroepen worden geïnventariseerd, iets wat aanvallers doorgaans doen om het netwerk te verkennen. Aanvallers kunnen gebruikmaken van deze techniek tooquery Hallo identiteit van gebruikers met beheerdersbevoegdheden.

Dit is een voorbeeld van dit type waarschuwing:

![Lokale beheerder](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Ongebruikelijke combinatie van hoofdletters en kleine letters

Security Center geeft een waarschuwing wanneer gedetecteerd wordt Hallo gebruik van een combinatie van hoofdletters en kleine letters op Hallo-opdrachtregel. Sommige aanvallers kunnen deze techniek toohide van hoofdlettergevoelige gebruiken of hash op basis van machine regel.

Dit is een voorbeeld van dit type waarschuwing:

![Ongebruikelijke combinatie](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Verdachte Golden Ticket Kerberos-aanval

Een waarmee is geknoeid [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) sleutel kan worden gebruikt door een aanvaller toocreate Kerberos 'Golden ticket,' Hallo aanvaller tooimpersonate zodat elke gebruiker die ze willen. Security Center gaat tootrigger een waarschuwing wanneer dit type activiteit wordt gedetecteerd.

> [!NOTE] 
> Meer informatie over Kerberos Golden Tickets vindt u in de [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx) (Handleiding voor beperking van het risico op referentiediefstal in Windows 10).

Dit is een voorbeeld van dit type waarschuwing:

![Golden Ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Verdacht account gemaakt

In Security Center wordt een waarschuwing geactiveerd wanneer er een account wordt gemaakt dat veel overeenkomsten vertoont met een bestaand ingebouwd account met beheerdersbevoegdheden. Deze methode kan worden gebruikt door aanvallers toocreate tooavoid wordt opgemerkt door menselijke verificatie van een rogue-account.
 
Dit is een voorbeeld van dit type waarschuwing:

![Verdacht account](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Verdachte firewallregel gemaakt

Aanvallers proberen toocircumvent hostbeveiliging door het maken van aangepaste firewall-regels tooallow schadelijke toepassingen toocommunicate met de opdracht en controle of toolaunch aanvallen via Hallo netwerk via Hallo geknoeid host. In Security Center wordt een waarschuwing geactiveerd wanneer wordt gedetecteerd dat er een nieuwe firewallregel is gemaakt vanuit een uitvoerbaar bestand op een verdachte locatie.
 
Dit is een voorbeeld van dit type waarschuwing:

![Firewallregel](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Verdachte combinatie van HTA en PowerShell

In Security Center wordt een waarschuwing geactiveerd wanneer wordt gedetecteerd dat door een HTA (Microsoft HTML Application) PowerShell-opdrachten worden gestart. Dit is een techniek die wordt gebruikt door aanvallers toolaunch schadelijke PowerShell-scripts.
 
Dit is een voorbeeld van dit type waarschuwing:

![HTA en PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Netwerkanalyse
Het detecteren van netwerkbedreigingen van Security Center werkt volgens het automatisch verzamelen van beveiligingsgegevens van uw Azure IPFIX-verkeer (Internet Protocol Flow Information Export). Deze informatie kunt vaak correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen wordt geanalyseerd.

### <a name="suspicious-outgoing-traffic-detected"></a>Verdacht uitgaand verkeer gedetecteerd
Netwerkapparaten kunnen worden gedetecteerd en in veel Hallo profiel dezelfde manier als andere soorten systemen. Aanvallers beginnen gewoonlijk met het scannen of sweepen van poorten. In het volgende voorbeeld hello hebt u verdachte Secure Shell (SSH)-verkeer van een virtuele machine. In dit scenario zijn een SSH-beveiligingsaanval of een poortsweep op een externe resource mogelijk.

![Waarschuwing verdacht uitgaand verkeer](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Deze waarschuwing bevat informatie waarmee u kunt tooidentify Hallo resource die gebruikt tooinitiate is deze aanval. Deze waarschuwing bevat ook informatie tooidentify Hallo geknoeid machine, detectietijd hello, plus Hallo-protocol en poort die werd gebruikt. Deze blade biedt u ook een lijst met herstelstappen die kunnen worden gebruikt toomitigate dit probleem.

### <a name="network-communication-with-a-malicious-machine"></a>Netwerkcommunicatie met een kwaadwillende machine
Door gebruik te maken van de feeds van Microsoft met informatie over bedreigingen kan Azure Security Center verdachte computers die met kwaadwillende IP-adressen communiceren identificeren. In veel gevallen is Hallo schadelijke adres een opdracht en control center. In dit geval Security Center gedetecteerd dat Hallo-communicatie is gedaan met onder Loader schadelijke software (ook wel bekend als [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![Waarschuwing over netwerkcommunicatie](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Deze waarschuwing bevat informatie waarmee u tooidentify Hallo resource die gebruikt tooinitiate is deze aanval, Hallo resource, Hallo slachtoffer IP Hallo aanvaller IP- en detectietijd Hallo aangevallen.

> [!NOTE]
> Live IP-adressen zijn verwijderd uit deze schermafbeelding wegens privacydoeleinden.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Mogelijke uitgaande Denial of Service-aanval gedetecteerd
Abnormaal netwerkverkeer dat afkomstig van één virtuele machine is kan leiden tot Security Center tootrigger een mogelijke denial of service type aanval.

Dit is een voorbeeld van dit type waarschuwing:

![Uitgaande DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Resourceanalyse
Security Center resource analyse is gericht op het platform als een service (PaaS)-services, zoals Hallo-integratie met Hallo [Azure SQL Database met detectie van dreigingen](../sql-database/sql-database-threat-detection.md) functie. Op basis van de resultaten van deze gebieden Hallo-analyse, activeert Security Center een resource-gerelateerde waarschuwing.

### <a name="potential-sql-injection"></a>Mogelijke SQL-injectie
SQL-injectie is een aanval waarbij schadelijke code wordt ingevoegd in tekenreeksen die later tooan exemplaar van SQL Server geparseerd en worden uitgevoerd doorgegeven worden. Elke procedure die SQL-instructies construeert, moet worden gecontroleerd op beveiligingsproblemen met injectie omdat SQL Server alle syntactisch geldige query's uitvoert die het ontvangt. Detectie van dreigingen SQL maakt gebruik van machine learning en gedragsanalyse afwijkingsdetectie detectie toodetermine verdachte gebeurtenissen die in uw Azure SQL-databases plaatsvinden mogelijk. Bijvoorbeeld:

* een voormalig medewerker heeft geprobeerd toegang tot een database te krijgen.
* Waarschuwing over SQL-injectieaanvallen
* Ongebruikelijke toegang tooa productiedatabase van een gebruiker bij u thuis

![Waarschuwing over mogelijke SQL-injectie](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

gebruikte tooidentify Hallo aangevallen resource, Hallo detectietijd en Hallo status van de aanval Hallo zijn Hallo-informatie in deze waarschuwing. Het bevat ook een koppeling toofurther onderzoek stappen.

### <a name="vulnerability-toosql-injection"></a>Beveiligingslek tooSQL injectie
Deze waarschuwing wordt geactiveerd wanneer een fout wordt gedetecteerd op een database. Deze waarschuwing kan duiden op dat een mogelijk beveiligingsprobleem tooSQL injectie aanvallen.

![Waarschuwing over mogelijke SQL-injectie](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Ongebruikelijke toegang vanaf onbekende locatie
Deze waarschuwing wordt geactiveerd wanneer een toegangsgebeurtenis vanaf een onbekend IP-adres is gedetecteerd op Hallo-server niet in Hallo laatste periode gevonden is.

![Waarschuwing over ongebruikelijke toegang](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Contextuele informatie
Tijdens een onderzoek moeten analisten extra context tooreach een eindconclusie over Hallo aard van Hallo threat en hoe toomitigate deze.  Bijvoorbeeld, een afwijkingsdetectie netwerk is gedetecteerd, maar zonder informatie over wat er gebeurt op Hallo netwerk of met inachtneming toohello gericht resource deze elke harde toounderstand naast welke acties tootake is. tooaid met die een beveiligingsincident voordoet bevatten artefacten, gerelateerde gebeurtenissen en informatie die Hallo onderzoeker helpen kan. Hallo beschikbaarheid van extra informatie varieert op Hallo type bedreiging is gedetecteerd en configuratie van uw omgeving Hallo en niet meer beschikbaar voor alle beveiligingsincidenten.

Als u meer informatie beschikbaar is, wordt deze weergegeven in Hallo Security Incident onder Hallo lijst met waarschuwingen. Dit kan informatie zijn zoals:

- Wissen van logboekgebeurtenissen
- PNP-apparaat aangesloten vanaf onbekend apparaat
- Waarschuwingen waarop geen actie kan worden uitgevoerd 

![Waarschuwing over ongebruikelijke toegang](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd over de verschillende typen Hallo van beveiligingswaarschuwingen in Security Center. toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsincidenten afhandelen in Azure Security Center](security-center-incident.md)
* [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md)
* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md)
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md): Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.
