---
title: aaaDetection mogelijkheden in Azure Security Center | Microsoft Docs
description: Dit document helpt u de werking van Azure Security Center detectiemogelijkheden toounderstand.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Detectiemogelijkheden van Azure Security Center
Dit document wordt beschreven mogelijkheden voor geavanceerde detectie Azure Security Center, waardoor kan actieve bedreigingen die gericht is op uw Microsoft Azure-resources geïdentificeerd en waarmee dat u met Hallo insights toorespond snel nodig.

> [!NOTE]
> Geavanceerde detecties zijn beschikbaar in Standard-laag van Azure Security Center Hallo. Er is een gratis proefversie voor 60 dagen beschikbaar. U kunt upgraden Hallo prijscategorie selectie in Hallo [beveiligingsbeleid](security-center-policies.md). Ga naar [Security Center pagina](https://azure.microsoft.com/pricing/details/security-center/) toolearn meer informatie over prijzen. 
> 
> 

## <a name="responding-tootodays-threats"></a>Tootoday van bedreigingen reageert
Er zijn belangrijke wijzigingen in Hallo threat liggend via Hallo laatste 20 jaar. In de afgelopen hello had bedrijven meestal alleen tooworry over website defacement door afzonderlijke aanvallers die voornamelijk geïnteresseerd zijn in zien 'wat ze kunnen doen'. Vandaag de dag gaan aanvallers veel genuanceerder te werk en zijn ze beter georganiseerd. Ze hebben vaak specifieke financiële en strategische doelstellingen. Ze hebben meer resources beschikbaar toothem, ook als ze kunnen worden basis van statussen voor land of georganiseerde crime.

Deze methode heeft tooan ongekende niveau tintje in Hallo aanvaller posities geleid. Ze zijn niet langer geïnteresseerd in het beschadigen van websites. Ze zijn nu geïnteresseerd zijn in het stelen van informatie, financiële accounts en persoonlijke gegevens die ze kunnen gebruiken op Hallo openmarkt of tooleverage betalen toogenerate een bepaalde zakelijke, politieke of militaire positie. Nog meer betreffende dan die aanvallers met een financiële doelstelling Hallo aanvallers die in strijd is met netwerken toodo schade tooinfrastructure en personen.

Organisaties implementeren als antwoord wordt vaak verschillende punt oplossingen, die zich richten op het bedrijfsnetwerk Hallo of eindpunten te beschermen door te zoeken naar de handtekeningen van bekende aanvallen. Deze oplossingen vaak toogenerate een groot aantal lage fidelity waarschuwingen, die een analist beveiliging tootriage vereisen en onderzoeken. De meeste organisaties hebben geen Hallo tijd en expertise vereist toorespond toothese waarschuwingen – dus veel niet-opgeloste gaat.  Ondertussen aanvallers hebt ontwikkeld hun toosubvert methoden veel handtekening gebaseerde beveiliging en [toocloud omgevingen aanpassen](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Nieuwe methoden zijn vereiste toomore snel opkomende bedreigingen identificeren en detectie- en versnellen. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Hoe Azure Security Center detecteert en toothreats reageert
Beveiligingsonderzoekers van Microsoft zijn voortdurend op Hallo lookout voor bedreigingen. Ze hebben toegang tot tooan uitbreidbare set telemetrie verkregen van wereldwijde aanwezigheid van Microsoft in Hallo cloud en on-premises. In deze verzameling wide bereiken en diverse gegevenssets kan Microsoft toodiscover nieuwe aanvalspatronen en trends in de lokale producten voor consumenten en bedrijven, evenals de bijbehorende online services. Als gevolg hiervan kan Security Center de detectie-algoritmen snel bijwerken wanneer aanvallers met nieuwe en steeds meer geavanceerde aanvallen komen. Met deze benadering kunt u de snel veranderende bedreigingen bijhouden. 

Detectie van dreigingen Security Center werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen. Deze informatie kunt vaak correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen wordt geanalyseerd. Beveiligingswaarschuwingen worden samen met aanbevelingen voor hoe tooremediate threat Hallo prioriteit in Security Center.

![Gegevensverzameling en -presentatie in Security Center](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Security Center maakt gebruik van geavanceerde beveiligingsanalyses die veel verder gaan dan op handtekeningen gebaseerde benaderingen. Doorbraken in big data en [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologieën zijn overgenomen tooevaluate gebeurtenissen op Hallo gehele cloud-infrastructuurresources – bedreigingen die onmogelijk tooidentify handmatige benaderingen en het voorspellen van Hallo detecteren evolutie van aanvallen. Deze beveiligingsanalyses omvatten: 

* **Geïntegreerd dreigingen**: lijkt voor bekende ongewenste actoren dankzij het gebruik van wereldwijde dreigingen van Microsoft-producten en services, Microsoft Digital Crimes Unit (DCU), Hallo Hallo Microsoft Security Response Center (MSRC) en externe -feeds.
* **Gedragsanalyse**: bekende patronen toodiscover schadelijke gedrag van toepassing is. 
* **Afwijkingsdetectie**: maakt gebruik van statistische profilering toobuild historische basislijn. Deze waarschuwing op afwijkingen van vastgestelde basislijnen die potentiële aanvalsvector tooa voldoen.

### <a name="threat-intelligence"></a>Informatie over bedreigingen
Microsoft heeft een gigantische hoeveelheid informatie over wereldwijde bedreigingen. Telemetrie loopt in uit meerdere bronnen, zoals Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, Hallo Microsoft Digital Crimes Unit (DCU) en Microsoft Security Response Center (MSRC). Onderzoekers ook ontvangen threat intelligence-informatie die wordt gedeeld door grote cloudserviceproviders en toothreat intelligence feeds is lid van een derde partij. Azure Security Center kunt gebruiken deze informatie tooalert u toothreats van bekende ongewenste actoren. Voorbeelden zijn:

* **Uitgaande communicatie tooa schadelijke IP-adres**: uitgaand verkeer tooa bekend botnet of darknet waarschijnlijk geeft aan dat uw resource er inbreuk is gemaakt en dat een aanvaller deze tooexecute probeert van die gegevens systeem- of exfiltrate opdrachten. Azure Security Center vergelijkt netwerkverkeer tooMicrosoft globale threat database en waarschuwt u als wordt gedetecteerd dat communicatie tooa schadelijke IP-adres.

## <a name="behavioral-analytics"></a>Gedragsanalyse
Behavior analytics is een techniek die geanalyseerd en vergeleken tooa gegevensverzameling van bekende patronen. Deze patronen zijn echter geen eenvoudige handtekeningen. Deze zijn bepaald door middel van complexe machine learning-algoritmen die toegepast toomassive gegevenssets zijn. Ze worden ook vastgesteld via de zorgvuldige analyse van schadelijk gedrag door deskundige analisten. Azure Security Center kunnen gedragsanalyse tooidentify geknoeid met resources op basis van de analyse van Logboeken van de virtuele machine, apparaatlogboeken virtueel netwerk, infrastructuur Logboeken, crashdumps en andere bronnen gebruiken. 

Daarnaast is de correlatie met andere signalen toocheck voor ondersteunend bewijs van een wijdverbreid campagne. Deze correlatie kan tooidentify gebeurtenissen die consistent met het tot stand gebrachte indicatoren van inbreuk zijn. Voorbeelden zijn:

* **Uitvoering van verdachte**: aanvallers gebruiken verschillende technieken tooexecute schadelijke software zonder detectie. Bijvoorbeeld een aanvaller mogelijk geven malware Hallo dezelfde naam als legitieme systeembestanden, maar deze bestanden in een andere locatie te plaatsen, gebruik een naam die is heel vergelijkbaar tooa onschadelijk bestand of masker Hallo true bestandsextensie. Security Center modellen processen gedrag en monitors verwerken uitvoeringen toodetect uitschieters zoals deze.  
* **Verborgen kwaadaardige software en misbruik pogingen**: geavanceerde schadelijke software is de traditionele antimalwareproducten kunnen tooevade door nooit toodisk schrijven of software-onderdelen die zijn opgeslagen op schijf te versleutelen.  Echter kan dergelijke schadelijke software worden gedetecteerd met behulp van de geheugenanalyse, zoals Hallo malware traceringen in het geheugen van de volgorde toofunction laat moet. Wanneer software vastloopt, bevat een crashdump een gedeelte van het geheugen tijdens het Hallo Hallo crash.  Door te analyseren Hallo geheugen in Hallo crashdump, Azure Security Center kunt detecteren technieken tooexploit beveiligingslekken in software gebruikt, toegang krijgen tot vertrouwelijke gegevens en ongemerkt behouden met in een machine waarmee is geknoeid zonder enige impact op de prestaties van Hallo uw computer verwijderd.
* **Lateral movement en interne reconnaissance**: toopersist in een waarmee is geknoeid netwerk- en zoeken/oogst waardevolle gegevens aanvallers proberen vaak toomove lateraal van Hallo geknoeid machine tooothers binnen Hallo hetzelfde netwerk. Security Center bewaakt proces en aanmelding activiteiten in de volgorde toodiscover tooexpand probeert een kwaadwillende persoon voet achter de deur binnen Hallo-netwerk, zoals de externe opdracht uitvoering netwerk scannen en accountinventarisatie.
* **Schadelijke Scripts met PowerShell**: PowerShell wordt gebruikt door aanvallers tooexecute schadelijke code op de virtuele doelmachines voor verschillende doeleinden. Security Center inspecteert PowerShell-activiteit op tekenen van verdachte activiteiten. 
* **Uitgaande aanvallen**: aanvallers vaak cloudresources met Hallo doel van het gebruik van deze resources toomount extra aanvallen zijn gericht. Geïnfecteerde virtuele machines, bijvoorbeeld mogelijk gebruikte toolaunch beveiligingsaanvallen op andere virtuele machines worden, verzenden van SPAM of open poorten scannen en andere apparaten op internet Hallo. Door het toepassen van machine learning toonetwork verkeer Beveiligingscentrum kan detecteren wanneer uitgaande netwerkcommunicatie Hallo-norm overschrijden. In geval van SPAM Hallo Beveiligingscentrum ook correleert ongebruikelijke e-verkeer met intelligence van Office 365 toodetermine of Hallo mail waarschijnlijk is slechte of Hallo resultaat van een geldig e-campagne.  

### <a name="anomaly-detection"></a>Afwijkingsdetectie
Azure Security Center gebruikt ook afwijkingsdetectie detectie tooidentify bedreigingen. In contrast toobehavioral analytics (die afhankelijk is van bekende patronen die zijn afgeleid van grote gegevenssets), anomaliedetectie is meer 'aangepast' en legt de nadruk op basislijnen die specifieke tooyour implementaties. Machine learning toegepaste toodetermine normale activiteiten voor uw implementaties en vervolgens regels gegenereerde toodefine uitschieter voorwaarden die een beveiligingsgebeurtenis kunnen vertegenwoordigen. Hier volgt een voorbeeld:

* **Inkomende RDP/SS-beveiligingsaanvallen**: uw implementaties hebben mogelijk drukke virtuele machines met een groot aantal aanmeldingen per dag en andere virtuele machines met maar weinig of geen aanmeldingen. Azure Security Center kunt bepalen basislijn Aanmeldingsactiviteit voor deze virtuele machines en gebruikt machine learning toodefine wat bevindt zich buiten het normale aanmeldingsactiviteit. Als Hallo aantal aanmeldingen of Hallo-tijd van de dag van Hallo aanmeldingen of Hallo locatie vanaf welke Hallo aanmeldingen worden aangevraagd of andere kenmerken aanmeldingsgerelateerde aanzienlijk verschillen van basislijn hello, kan een waarschuwing worden gegenereerd. Ook hier weer wordt door machine learning bepaald wat een aanzienlijk verschil is.

## <a name="continuous-threat-intelligence-monitoring"></a>Doorlopende controle van informatie over bedreigingen
Azure Security Center werkt beveiliging onderzoeks- en wetenschappelijke teams die voortdurend op wijzigingen in Hallo threat liggend controleren. Dit omvat het Hallo-initiatieven te volgen:

* **Controleren van informatie over bedreigingen**: informatie over bedreigingen omvat mechanismen, indicatoren, implicaties en gericht advies over bestaande of nieuwe bedreigingen. Deze informatie wordt gedeeld in Hallo security-community en Microsoft bewaakt continu threat intelligence feeds van interne en externe bronnen.
* **Signalen delen**: inzichten van beveiligingsteams overal uit Microsofts brede portfolio van cloud- en on-premises services, servers en client-endpointapparaten worden gedeeld en geanalyseerd. 
* **Microsoft-beveiligingsspecialisten**: continue inzet van teams overal bij Microsoft die op gespecialiseerde beveiligingsgebieden werken, zoals forensisch onderzoek en webaanvaldetectie.
* **Detectie afstemmen**: algoritmen voor bestaande klanten gegevenssets worden uitgevoerd en beveiligingsonderzoekers werken met klanten toovalidate Hallo resultaten. True en false positieven zijn gebruikte toorefine machine learning-algoritmen.

Deze gecombineerde inspanningen moet resulteren in nieuwe en verbeterde detecties die u van onmiddellijk profiteren kunt: Er is geen actie voor u tootake.

## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe tooAzure Security Center detectiemogelijkheden werken. toolearn meer informatie over Security Center Hallo ziet:

* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md)
* [Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)
* [Beveiligingswaarschuwingen per type in Azure Security Center](security-center-alerts-type.md)
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.

