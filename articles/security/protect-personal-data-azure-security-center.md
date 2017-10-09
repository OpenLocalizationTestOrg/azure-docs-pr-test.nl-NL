---
title: aaaProtect persoonlijke gegevens met Azure Security Center | Microsoft Docs
description: beveiligen van persoonlijke gegevens met Azure security center
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
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Persoonlijke gegevens beschermen tegen aanvallen en inbreuken op: Azure Security Center

In dit artikel helpt u begrijpen hoe toouse Azure Security Center tooprotect persoonlijke gegevens van kiezen oplossingen en aanvallen.

## <a name="scenario"></a>Scenario 

Een bedrijf grote cruise, gevestigd in de Verenigde Staten Hallo breidt de bewerkingen toooffer routes in Hallo Middellandse, en Baltische veiligheid, evenals Hallo Florida. toohelp bij deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en Hallo VK verkregen

Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud. Dit omvat persoonlijk identificeerbare informatie zoals namen, adressen, telefoonnummers en creditcardgegevens. Het bevat ook informatie Human Resources, zoals:

- Adressen
- telefoonnummers
- BTW-id 's
- medische informatie

Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden. Zakelijke werknemers toegang tot het Hallo netwerk van de externe kantoren en reizen agents van het bedrijf Hallo wereld Hallo zich toegang tot toosome bedrijfsbronnen hebben.
Persoonlijke gegevens die tussen deze locaties en Hallo Microsoft Datacenter via Hallo-netwerk is verzonden.

## <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf maakt zich zorgen over Hallo dreiging van aanvallen op Azure-resources. Ze willen tooprevent blootstelling van werknemers en klanten persoonsgegevens toounauthorized personen. Ze willen richtlijnen op zowel voorkomen en antwoord/herstel, evenals een effectieve manier toomonitor Hallo actieve beveiliging van hun cloudbronnen.
Ze moeten een sterke line-of beveiliging tegen kwaadwillende personen de hedendaagse geavanceerde en geordend.

## <a name="company-goal"></a>Bedrijf-doel

Een van de doelstellingen van het bedrijf Hallo is tooensure Hallo privacy van klanten en werknemers persoonlijke gegevens te beveiligen tegen bedreigingen. Een van hun doelstellingen is toorespond onmiddellijk toosigns van inbreuk op de toomitigate Hallo impact. Een manier tooassess Hallo huidige status van de beveiliging is vereist, kwetsbaar configuraties te identificeren en ze herstellen.

## <a name="solutions"></a>Oplossingen

Microsoft Azure Security Center (ASC) biedt een geïntegreerde beveiliging en beleidsbeheer beheeroplossing. Het biedt eenvoudig te gebruiken en effectieve bedreiging mogelijkheden voor preventie, detectie en reactie.

### <a name="prevention"></a>Preventie

ASC helpt u bij schendingen doordat u beveiligingsbeleid tooset just-in-time-toegang bieden, voorkomen van en aanbevelingen voor beveiliging te implementeren.

Een beveiligingsbeleid bepaalt Hallo set besturingselementen die worden aanbevolen voor resources binnen Hallo opgegeven abonnement. In de tijd kan toegang worden gebruikte toolock omlaag binnenkomend verkeer tooyour Azure Virtual machines blootstelling tooattacks verminderen. Aanbevelingen voor beveiliging worden gemaakt door ASC na het analyseren van Hallo beveiligingsstatus van uw Azure-resources.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Hoe Stel beleidsregels voor veiligheid in ASC?

U kunt voor elk abonnement beveiligingsbeleid configureren. toomodify een beveiligingsbeleid, moet u een eigenaar of bijdrager van het abonnement. In hello Azure-portal, Hallo te volgen:

1. Selecteer **beleid** in Hallo ASC-dashboard.

2. Selecteer Hallo abonnement waarop tooenable Hallo beleid.

3. Kies **preventiebeleid** tooconfigure beleid per abonnement. **Verzamel gegevens van virtuele machines** te moet worden ingesteld**op.**

4. In Hallo **preventiebeleid** opties, dient u **op** tooenable Hallo aanbevelingen voor beveiliging die relevant voor het Hallo-abonnement zijn.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Zie voor meer gedetailleerde instructies en een uitleg van Hallo beleid aanbevelingen die kunnen worden ingeschakeld, [beveiligingsbeleid instellen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Hoe configureer ik Just in Time toegang (Just in time)?

Wanneer JIT is ingeschakeld, wordt in Security Center binnenkomend verkeer tooyour Azure Virtual machines vergrendelt door het maken van een NSG-regel. U selecteert Hallo poorten op Hallo VM toowhich binnenkomend verkeer wordt worden vergrendeld. toouse JIT krijgen, Hallo te volgen:

1. Selecteer Hallo **Just in time VM toegang tegel** op Hallo ASC blade.

2. Selecteer Hallo **aanbevolen** tabblad.

3. Onder **VMs**, Hallo virtuele machines die u tooenable wilt selecteren. Hiermee wordt een vinkje volgende tooa VM geplaatst. 
4. Selecteer **inschakelen JIT** op virtuele machines.
5. Selecteer **Opslaan**.

Hallo-standaardpoorten die ASC aanbeveelt wordt ingeschakeld voor JIT, kunt u zien. U kunt ook toevoegen en configureren van een nieuwe poort waarop tooenable Hallo NET in tijdoplossing. Hallo **Just in time VM toegang** tegel in Hallo Security Center bevat Hallo-nummer van virtuele machines die zijn geconfigureerd voor JIT-toegang. U ziet ook Hallo aantal goedgekeurde toegangsaanvragen in Hallo afgelopen week.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Voor instructies over het toodo, en aanvullende informatie over Just in Time-toegang, Zie [beheren via in de tijd toegang tot een virtuele machine.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>Hoe ik ASC beveiligingsaanbevelingen implementeren?

Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan. Hallo aanbevelingen helpt u bij Hallo Hallo nodig-besturingselementen configureren. 
1. Selecteer Hallo **aanbevelingen** tegel op Hallo ASC dashboard.

2. Hallo-aanbevelingen die worden weergegeven in een tabel waarin elke regel een aanbeveling vertegenwoordigt weergeven.

3. toofilter aanbevelingen, selecteer **Filter** en selecteer Hallo ernst en status waarden voor toosee.

4. toodismiss een aanbeveling die niet van toepassing, die u kunt met de rechtermuisknop op en selecteer **sluiten.**

5. Denk na over welke aanbeveling eerst moet worden toegepast.

6. Hallo aanbevelingen in volgorde van prioriteit toepassen.

Voor een lijst met mogelijke aanbevelingen en de zelfstudies over het tooapply, Zie [aanbevelingen voor beveiliging in Azure Security Center beheren.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Detectie van en reactie

Detectie- en Ga samen als u zo snel mogelijk toorespond wilt nadat een bedreiging is gedetecteerd.
Detectie van dreigingen ASC werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen. ASC kunt snel de detectiealgoritmen bijwerken als aanvallers release nieuwe en steeds meer geavanceerde aanvallen. Zie voor meer informatie gedetailleerde over de werking van de detectie van dreigingen van ASC [Azure Security Center detectiemogelijkheden](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Hoe ik beheren en toosecurity waarschuwingen reageren?

Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly Hallo probleem onderzoeken. Security Center bevat ook aanbevelingen voor het tooremediate een aanval. toomanage uw beveiligingswaarschuwingen, Hallo volgende doen:

1. Selecteer Hallo **beveiligingswaarschuwingen** -tegel in Hallo ASC dashboard. Hiermee worden de details voor elke waarschuwing weergegeven.

2. toofilter waarschuwingen op basis van datum, status en ernst, selecteer **Filter** en selecteer vervolgens de gewenste toosee Hallo-waarden.

3. toorespond tooan waarschuwing, selecteert u deze en Hallo informatie bekijken, en selecteer vervolgens Hallo resource die is aangevallen.

4. In Hallo **beschrijving** veld, ziet u informatie, zoals aanbevolen herstel.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Zie voor meer instructies voor het reageert toosecurity waarschuwingen, [beheren en reageert toosecurity waarschuwingen in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Voor verdere hulp bij het onderzoeken van beveiligingswaarschuwingen Hallo bedrijf ASC waarschuwingen kunt integreren met een eigen SIEM-oplossing met behulp van [Azure Log integratie](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Hoe beheer ik beveiligingsincidenten?

In ASC is een beveiligingsincident voordoet een aggregatie van alle waarschuwingen voor een resource uitgelijnd met de kill-keten patronen. Een Incident onthullen Hallo lijst met verwante waarschuwingen, waarmee u tooobtain meer informatie over elk exemplaar. Incidenten verschijnen in de tegel beveiligingswaarschuwingen Hallo en blade.

tooreview en beveiligingsincidenten, Hallo te volgen:

1. Selecteer Hallo **beveiligingswaarschuwingen** tegel. Als een beveiligingsincident voordoet wordt gedetecteerd, wordt weergegeven onder Hallo beveiliging waarschuwingen grafiek. Er is een pictogram dat verschilt van andere waarschuwingen.

2. Selecteer Hallo incident toosee meer informatie over deze beveiligingsincident voordoet. Aanvullende gegevens bevatten een volledige beschrijving, de ernst, de huidige status, Hallo aangevallen resources, Hallo herstelstappen voor Hallo incident en Hallo waarschuwingen die zijn opgenomen in dit incident.

U kunt filteren toosee **alleen incidenten**, **alleen waarschuwingen**, of **beide**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Hoe krijg ik toegang tot Hallo Threat Intelligence-rapport?

ASC analyseert gegevens uit meerdere bronnen tooidentify bedreigingen. tooassist respons op incidenten teams onderzoeken en bedreigingen te herstellen, Security Center bevat een bedreiging intelligence-rapport dat informatie bevat over Hallo threat die is gedetecteerd.

Security Center heeft drie soorten threat rapporten die per aanval kunnen variëren.
Hallo rapporten zijn beschikbaar:

- Activiteitengroep rapport: biedt verdiepen in aanvallers, hun doelstellingen en -tactieken.

- Campagne rapport: Er is gericht op gegevens van specifieke aanval campagnes.

- Het overzichtsrapport voor Threat: bevat informatie over alle items in de vorige twee rapporten Hallo.

Dit type gegevens is zeer nuttig tijdens Hallo respons op incidenten, wanneer er een bron lopende onderzoek toounderstand Hallo Hallo aanval, Hallo aanvaller beweegredenen, en welke toomitigate toodo dit probleem zwevend doorsturen.

1. tooaccess Hallo dreigingen rapporteren, Hallo te volgen:

2. Selecteer Hallo **beveiligingswaarschuwingen** tegel op Hallo ASC dashboard.

3. Selecteer Hallo beveiligingswaarschuwing waarvoor u tooobtain wilt meer informatie.

4. In Hallo **rapporten** veld, klikt u op Hallo koppeling toohello threat intelligence-rapport.

5. Hiermee opent u Hallo PDF-bestand, die u kunt downloaden.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Zie voor meer informatie over Hallo ASC threat intelligence-rapport [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Evaluatie

toohelp met testen, beoordelen en evalueren van uw beveiligingspostuur ASC biedt voor het evalueren van de geïntegreerde beveiligingsproblemen met Qualys cloud agents, als onderdeel van het onderdeel van de aanbevelingen voor virtuele machine.

Hallo Qualys agent rapporteert beveiligingslek toohello Qualys platform voor gegevensbeheer, die vervolgens verzendt beveiligingslek en health bewakingsgegevens weer tooASC. aanbeveling tooadd oplossing voor een beveiligingsprobleem wordt weergegeven in Hallo Hallo **aanbevelingen** blade op Hallo ASC dashboard.

Nadat Hallo vulnerability assessment oplossing op Hallo doel VM is geïnstalleerd, wordt in Security Center scans VM toodetect Hallo en systeem- en kwetsbaarheden identificeren. Gevonden problemen worden vermeld in de Hallo **aanbevelingen voor virtuele Machines** optie.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Hoe ik een vulnerability assessment oplossing implementeren? 

Als een virtuele Machine geen een geïntegreerde vulnerability assessment oplossing is al geïmplementeerd Security Center raadt aan om te worden geïnstalleerd.

1. In Hallo ASC dashboard Hallo **aanbevelingen** blade Selecteer **een vulnerability assessment oplossing toevoegen.**

2. Selecteer Hallo VMs waar u tooinstall Hallo vulnerability assessment oplossing.

3. Klik op **installeren op virtuele machines [aantal].**

4. Selecteer een partneroplossing in hello Azure Marketplace of onder **bestaande oplossing gebruiken** Selecteer **Qualys.**

5. Kunt u Hallo automatische update-instellingen in- of uitschakelen in Hallo **partneroplossingen** blade.

Voor verdere instructies voor het tooimplement een oplossing voor vulnerability assessment, Zie [controle op beveiligingslekken in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Volgende stappen

- [Snelstartgids voor Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Inleiding tooAzure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Waarschuwingen van Azure Security Center integreren met Azure-logboekanalyse-integratie](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Versterking Azure Security Center met geïntegreerde Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
