---
title: aaaGetting gestart - Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: Dit is een beter overzicht Hallo Threat Modeling hulpprogramma in de actie is gemarkeerd.
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Aan de slag met Hallo Threat Modeling hulpprogramma

Hallo-Cloud en Enterprise beveiligingsprogramma's team uitgebracht Hallo Threat Modeling hulpprogramma Preview eerder dit jaar als een gratis  **[Klik hier om te downloaden](https://aka.ms/tmtpreview)**. Hallo wijziging in bezorgingsmechanisme, kunnen wij toopush Hallo nieuwste verbeteringen en oplossingen voor problemen toocustomers telkens wanneer die ze gemakkelijker toomaintain en gebruik Hallo hulpprogramma opent.
Dit artikel leert u Hallo proces van het aan de slag met Hallo Microsoft SDL threat modeling benadering en ziet u hoe toouse Hallo hulpprogramma toodevelop geweldige threat modellen als een backbone van uw beveiliging.

In dit artikel is gebaseerd op bestaande kennis over Hallo SDL threat modeling benadering. Voor een kort overzicht verwijzen te**[Threat Modeling webtoepassingen](https://msdn.microsoft.com/library/ms978516.aspx)**  en een gearchiveerde versie van  **[onthullen beveiligingsfouten met behulp van Hallo STRIDE benadering](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  MSDN-artikel gepubliceerd in 2006.

tooquickly samenvatten, Hallo benadering omvat het maken van een diagram, bedreigingen te identificeren, beperkende ze en elke risicobeperking valideren. Hier volgt een diagram dit proces illustreert:

![SDL-proces](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Hallo threat modeling proces wordt gestart

Wanneer u Hallo Threat Modeling hulpprogramma start, ziet u een aantal dingen, zoals in afbeelding Hallo:

![Lege startpagina](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Sectie Threat-model

| Onderdeel                                   | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Feedback, suggesties en problemen knop** | Vindt u Hallo  **[MSDN-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  voor alle zaken SDL. Dit biedt u een kans tooread via wat andere gebruikers, samen met tijdelijke oplossingen en aanbevelingen doen. Als u nog steeds niet kunt vinden wat u zoekt, e- tmtextsupport@microsoft.com voor onze support team toohelp u                                                                                                                            |
| **Een Model maken**                          | Hiermee opent u een leeg canvas voor toodraw u het diagram. Zorg ervoor dat tooselect welke sjabloon gewenst toouse voor uw model                                                                                                                                                                                                                                                                                                                                                                       |
| **Sjabloon voor nieuwe modellen**                 | U moet welke toouse sjabloon selecteren voordat het maken van een model. Onze belangrijkste sjabloon is hello Azure Threat Model sjabloon waarin de Azure-specifieke stencils, bedreigingen en oplossingen. Selecteer Hallo SDL TM Knowledge Base uit de vervolgkeuzelijst Hallo voor algemene modellen. Toocreate wilt uw eigen sjabloon of een nieuwe voor alle gebruikers verzenden? Bekijk onze  **[sjabloon opslagplaats](https://github.com/Microsoft/threat-modeling-templates)**  GitHub-Page toolearn meer                              |
| **Een Model openen**                            | <p>Wordt geopend eerder opgeslagen threat modellen. Hallo modellen onlangs geopend functie is handig als u uw meest recente bestanden tooopen nodig. Wanneer u de muisaanwijzer op Hallo selectie, vindt u 2 manieren tooopen modellen:</p><p><ul><li>Open vanaf deze Computer – klassieke manier van het openen van een bestand met behulp van lokale opslag</li><li>Openen van OneDrive-teams kunnen mappen in OneDrive toosave gebruiken en delen alle hun threat modellen in een enkele locatie toohelp de productiviteit te verhogen en samenwerking</li></ul></p> |
| **Getting Started Guide**                   | Hallo wordt geopend  **[Microsoft Threat Modeling Tool](./azure-security-threat-modeling-tool.md)**  hoofdpagina                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Sjabloonsectie

| Onderdeel               | Details                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nieuwe sjabloon maken** | Hiermee opent u een lege sjabloon voor u toobuild op. Tenzij u uitgebreide kennis bij het maken van sjablonen helemaal hebt, wordt aanbevolen om toobuild uit bestaande groepen. |
| **Sjabloon openen**       | Hiermee opent u de sjablonen te bestaande voor u toomake wijzigingen                                                                                                             |

Hallo Threat Modeling hulpprogramma team werkt voortdurend tooimprove hulpprogramma functionaliteit en ervaring. Enkele kleine wijzigingen in de loop Hallo van Hallo jaar kunnen plaatsvinden, maar alle belangrijke wijzigingen vereisen regeneraties in Hallo handleiding. Raadpleeg tooit vaak tooensure ophalen van de meest recente aankondigingen Hallo.

## <a name="building-a-model"></a>Een model bouwen

In deze sectie we Ga als volgt:

- Cristina (developer)
- Ricardo (een programmamanager) en
- Ashish (tester)

Ze moeten Hallo-proces voor de ontwikkeling van hun eerste risicomodel worden doorlopen.

> Ricardo: Hallo Cristina, op Hallo threat modeldiagram is gegaan en wilden toomake ervoor dat wij Hallo details rechts. Kan u helpen mij via zoeken?
> Cristina: volkomen. Laten we.
> Ricardo Hallo hulpprogramma geopend en zijn scherm deelt met Cristina.

![Basic risicomodel](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: OK klikt, ziet er eenvoudig, maar kunt u doorlopen mij deze?
> Ricardo: zeker! Hier volgt Hallo uitsplitsing:
> - Onze menselijke gebruiker wordt getekend als een externe entiteit: een vierkant
> - Deze opdrachten tooour webserver verzendt: Hallo cirkel
> - Hallo-webserver is een database (twee parallelle lijnen) advies

Wat Ricardo net hebt u geleerd Cristina is een GSD, afkorting voor  **[gegevensstroom-Diagram](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Hallo Threat Modeling hulpprogramma kan gebruikers toospecify grenzen van vertrouwensrelaties, aangegeven door Hallo rode stippellijn, tooshow waarop andere entiteiten in besturingselement zijn. IT-beheerders vereisen bijvoorbeeld een Active Directory-systeem voor verificatiedoeleinden zodat Hallo Active Directory buiten hun besturingselement is.

> Cristina: Rechts toome gezocht. Hoe zit het Hallo bedreigingen?
> Ricardo: Ik laat zien.

## <a name="analyzing-threats"></a>Bedreigingen analyseren

Nadat hij op Hallo analyseweergave uit Hallo pictogram menuselectie (bestand met Vergrootglas), hij weergeven van de tooa gegenereerde bedreigingen Hallo Threat Modeling hulpprogramma gevonden op basis van de standaardsjabloon Hallo ondernomen dat gebruikmaakt van Hallo SDL benadering aangeroepen klikt  **[ STRIDE (vervalsing, knoeien, vrijgeven van informatie, DOS-aanval en bevoegdheden)](https://en.wikipedia.org/wiki/STRIDE_(security))**. Hallo idee is dat software onder een voorspelbare set van bedreigingen die u kunt vinden met behulp van deze categorieën 6 afkomstig is.

Deze benadering is dat uw huis beveiligen door ervoor te zorgen elke deur- en beschikt over een vergrendelingsfout mechanisme voordat een waarschuwing-systeem toevoegen of chasing na Hallo dief.

![Basic bedreigingen](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo begint met het eerste item in de lijst Hallo Hallo selecteren. Dit is wat er gebeurt:

Eerst is Hallo interactie tussen de twee stencils Hallo verbeterd

![Interactie](./media/azure-security-threat-modeling-tool/interaction.png)

Tweede, aanvullende informatie over het Hallo-bedreiging wordt weergegeven in Hallo Threat eigenschappenvenster

![Interactie Info](./media/azure-security-threat-modeling-tool/interactioninfo.png)

Hallo gegenereerd threat helpt hem potentiële fouten met ontwerp begrijpen. Hallo STRIDE categorisatie geeft hij een idee op potentiële aanvalsvectoren, tijdens het Hallo extra beschrijving toegangsinformatie precies wat is onjuist, samen met mogelijke manieren toomitigate deze. Hij kan prioriteit classificaties, afhankelijk van zijn organisatie bug-balk wijzigen of bewerkbare velden toowrite opmerkingen gebruikt Hallo reden meer informatie.

Azure-sjablonen hebben extra details toohelp gebruikers begrijpen niet alleen wat is het probleem, maar ook hoe toofix deze door beschrijvingen, voorbeelden en hyperlinks tooAzure-specifieke documentatie toe te voegen.

Hallo beschrijving aangebracht hij zich ervan bewust Hallo belangrijk voor het toevoegen van een verificatie mechanisme tooprevent gebruikers uit wordt vervalst, weer te geven Hallo eerste threat toobe gewerkt. Een paar minuten in Hallo discussie met Cristina, begrepen ze Hallo belang van de implementatie van toegangsbeheer en rollen. Ricardo gevuld in sommige toomake snelle notities zeker van te zijn dat deze zijn geïmplementeerd.

Als Ricardo is een in Hallo bedreigingen onder openbaarmaking van informatie fout, gerealiseerde hij Hallo dit plan sommige alleen-lezen accounts vereist voor controle en rapportage. Hij zich wel eens afgevraagd of is een nieuwe bedreiging dit, maar Hallo oplossingen zijn Hallo dezelfde zijn, zodat hij Hallo threat dienovereenkomstig hebt genoteerd.
Hij ook iets meer over het vrijgeven van informatie wordt beschouwd en de back-uptapes Hallo ging tooneed versleuteling, een taak voor het operationele team van hello gerealiseerde.

Bedreigingen wordt gegarandeerd dat niet van toepassing toohello ontwerp vervaldatum tooexisting oplossingen of beveiliging te kunnen worden gewijzigd 'niet van toepassing"van Hallo Status vervolgkeuzelijst. Er zijn drie andere opties: niet gestart: standaardselectie onderzoek moet – gebruikt toofollow up voor artikelen en Mitigated – nadat het volledig is gegaan op.

## <a name="reports--sharing"></a>Rapporten en delen

Zodra Ricardo doorloopt Hallo lijst met Cristina en belangrijke opmerkingen worden toegevoegd, oplossingen/redenen, prioriteit en de status verandert, hij selecteert rapporten -> volledige rapport -> opslaan welke afdrukken leuk een rapport voor hem toogo via met rapport maken collega's tooensure Hallo correcte beveiliging werk is geïmplementeerd.

![Interactie Info](./media/azure-security-threat-modeling-tool/report.png)

Als Ricardo wil in plaats daarvan tooshare Hallo-bestand, kunt hij eenvoudig doen door op te slaan in de organisatie OneDrive-account. Nadat hij dat doet, kan hij Hallo documentkoppeling kopiëren en delen met zijn collega's. 

## <a name="threat-modeling-meetings"></a>Threat modellering vergaderingen

Wanneer Ricardo zijn threat model toohis collega met OneDrive, Ashish, Hallo tester verzonden, is underwhelmed. Leek zoals Ricardo en Cristina ontbreekt een aantal belangrijke complexere cases, die kunnen worden gegarandeerd. Zijn telefoontjes is een aanvulling toothreat-modellen.

In dit scenario nadat Ashish via risicomodel hello, heeft hij aangeroepen voor twee threat modellering vergaderingen: één vergadering toosynchronize op Hallo-proces en doorloop Hallo diagrammen en vervolgens een tweede vergadering voor beoordeling van bedreigingen en afmelden.

In de eerste vergadering hello gespendeerd Ashish 10 minuten roulatie van iedereen via Hallo SDL threat modeling proces. Hij vervolgens Hallo threat model-diagram opgehaald en uit te leggen in detail gestart. Binnen vijf minuten waren een belangrijk onderdeel van de ontbrekende geïdentificeerd.

Een paar minuten later, Ashish en Ricardo is in een uitgebreide bespreking van hoe Hallo-webserver is opgebouwd. Is niet ideaal manier voor een vergadering tooproceed hello, maar iedereen uiteindelijk overeengekomen dat vroeg Hallo discrepantie detecteren zou deze in de toekomst Hallo periode toosave.

In Hallo tweede vergadering, Hallo team doorlopen Hallo bedreigingen, een aantal manieren tooaddress ze en ondertekende besproken op Hallo risicomodel uitgeschakeld. Deze Hallo document ingecheckt in broncodebeheer en voortgezet met ontwikkeling.

## <a name="thinking-about-assets"></a>Nadenken over activa

Sommige lezers die beschikken over de bedreiging gemodelleerd merkt dat we nog niet is besproken activa helemaal. We hebben gedetecteerd dat veel softwareontwikkelaars hun software beter dan ze Hallo concept van assets begrijpen en welke activa een aanvaller mogelijk geïnteresseerd in begrijpen.

Als u toothreat gaat een huis model, kunt u beginnen met nadenken over uw familie, onvervangbare foto's of waardevolle illustratie. Mogelijk kunt u beginnen met nadenken over wie in mogelijk verbroken en Hallo huidige beveiligingssysteem. Of kunt u beginnen met het Hallo fysieke functies, zoals de groep op Hallo of Hallo front porch overwegen. Dit zijn vergelijkbaar toothinking over activa, aanvallers of softwareontwerp. Een van deze drie methoden werken.

Hallo benadering toothreat modellering we hebt die hier wordt gepresenteerd is aanzienlijk eenvoudiger is dan wat Microsoft in de afgelopen Hallo heeft gedaan. We vinden Hallo software ontwerpbenadering geschikt is voor veel teams. We hopen dat die jouw e-mailadres bevatten.

## <a name="next-steps"></a>Volgende stappen

Stuur uw vragen, opmerkingen en problemen tootmtextsupport@microsoft.com. **[Download](https://aka.ms/tmtpreview)**  Hallo Threat Modeling hulpprogramma tooget gestart.
