---
title: aaaAzure Mobile Engagement instructiehandleiding met aanbevolen procedures
description: Instructiehandleiding voor Azure Mobile Engagement en aanbevolen procedures voor onboarding
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - Instructiehandleiding met aanbevolen procedures
## <a name="overview"></a>Overzicht
**Hallo mobiele scherm staat vol:** In 2013 uitgevoerde studie bleek Hallo gemiddelde mobiele apparaat 27 toepassingen zijn geïnstalleerd. Gebruikers brachten doorgaans 30 uur per maand door in hun apps. De meeste tijd werd doorgebracht op sociale netwerken en met gamen (ongeveer 20 uur). Begin 2014 waren Hallo Android-markt circa 1,5 miljoen toepassingen voor gebruikers toochoose van. Hallo Apple store bevatte ongeveer 1,2 miljoen apps. Het gebruik van mobiele apps neemt nog steeds toe en ontwikkelaars blijven concurreren op deze groeiende markt. 

Hallo gemiddelde mobiele gebruiker installeert en verwijdert apps vaak, afhankelijk van veranderende interesses en in-app-ervaringen. In de volgorde toodetermine Hallo succes van een app wordt deze essentieel tooknow meer dan alleen het aantal gebruikers dat uw app installeert. Het is belangrijk tooknow hoe nuttig uw app en als dat de mening hierover verandert. Hallo volgende vragen worden steeds belangrijker:

* Uw gebruikers komen toofind uw app niet-interessante of verouderd? 
* Hoeveel gebruikers zijn al gestopt met het gebruik van uw app? 
* Neemt het aantal in-app-aankopen toe of af?
* Gebruikers mislukken toocomplete werkstromen vanwege problemen met het Hallo-app of gebrek aan interesse? 
* Kan u blijft uw app nuttig en relevant door te pushen nieuwe inhoud tooyour-gebruiker basis? 
* Zou zijn deze nieuwe inhoud Hallo hetzelfde voor alle gebruikers of gericht zijn op gebruikerssegmenten op basis van gedrag in uw app? 

Antwoorden tooquestions vergelijkbare toothese kan helpen Hallo levensduur en omzet uitbreiden van uw app. Daarnaast kunnen ze u helpen bij het definiëren en behouden van uw gebruikersgroep. 

Mediagerelateerde apps vaak toohave aantal Hallo langst bewaard door gebruikers. Een reden hiervoor is dat ze voortdurend nieuwe inhoud toousers bieden. Vroege acceptatie van nuttige pushmeldingen omgeleid gebruikerssegment tooa doorgaans toohave een grote invloed op app-retentie. 

Hello Azure Mobile Engagement programma is ontworpen toohelp u Hallo levensduur en retentie van uw app door op te geven van een methode toogather uitbreidt en analyseren van gedetailleerde informatie over Hallo gebruik van uw app. Deze methode kunt u uw gebruikersgroep volgens toobehavior classificeren en gerichte campagnes maken voor het leveren van pushmeldingen en in-app-berichten tooidentified gebruikerssegmenten. Key Performance Indicators (KPI's) meten hoe actief uw gebruikers zijn met verschillende aspecten van uw app. Azure Mobile Engagement biedt Hallo methoden u deze KPI's toodetermine nodig. Het helpt verhogen Hallo return op uw investering (ROI) doordat Hallo infrastructuur moet u tooincrease engagement met uw mobiele app. 

In de volgorde tooget Hallo optimaal gebruik van Azure Mobile Engagement moet u toostart met een goed ontworpen gebruiksplan. Uw abonnement kunt u identificeren Hallo gedetailleerde gegevens, moet u kunnen toosegment toobe uw gebruiker basis. U kunt segmenten maken op basis van gedrag en op basis van in-app-ervaringen. In de volgorde voor uw abonnement toobe geslaagd is een best practice tooclearly definiëren Hallo KPI die Hallo doelstellingen van uw app wilt meten. Met de gedefinieerde wissen prestatie-indicatoren kunt u eenvoudig hello benodigde logica insluiten in uw app toocollect fijn gedetailleerde gegevens die u gaat gebruiken tooanalyze en voor het evalueren van uw KPI's. In dit onderwerp is een handleiding met aanbevolen procedures voor het definiëren van KPI's Hallo die u in uw plan gebruiken wilt. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Stap 1: Uw KPI's toofit Hallo BET-model definiëren
Het correct definiëren van KPI's, kan een toocomplete lastig zijn. Apps die zijn bestemd voor verschillende branches, hebben hun eigen specificaties en doelstellingen. Dit kan tooconfuse vaak een benadering. toohelp kunt dit voorkomen, moeten doelstellingen en KPI's worden ingedeeld in drie hoofdcategorieën: **Business**, **Engagement**, en **technische**. Dit is zogeheten Hallo **BET-model**.

Een goed plan hebben doorgaans doelstellingen en KPI's Hallo die Hallo uitkomsten in elk van de volgende categorieën van Hallo BET-model Hallo meten.

#### <a name="business-kpis"></a>Zakelijke KPI's
Zakelijke KPI's Hallo eenvoudigste onderdeel toobuild zijn. U hebt deze waarschijnlijk al op een bepaalde manier gedefinieerd toen u uw mobiele app plande. Deze KPI's zijn in het algemeen nuttig bij het meten van de omzet en het rendement van uw app. Hallo biedt volgende lijst een aantal voorbeelden van zakelijke KPI's die u helpen kunnen bij het definiëren van de prestatie-indicatoren:

* Zakelijke KPI's voor media
  * Aantal advertenties waarop is geklikt
  * Aantal bezoeken per gebruiker
  * Aantal bestaande abonnementen
* Zakelijke KPI's voor gaming
  * Aantal in-app-aankopen
  * Gemiddelde omzet per gebruiker (ARPU)
  * Tijd besteed per sessie
  * Aantal dagen gespeeld en huidige niveau in de game
* Zakelijke KPI's voor e-commerce
  * Aantal dagen dat de app is gebruikt
  * Gemiddelde omzet per gebruiker (ARPU)
  * Gemiddeld bedrag in winkelwagen bij afrekenen
  * Productcategorie voor de meeste weergaven en aankopen
* Zakelijke KPI's voor de bank- en verzekeringssector
  * Aantal accounts
  * Geactiveerde functies
  * Bezochte aanbiedingenpagina's
  * Meldingen waarop is geklikt of die zijn geactiveerd       

#### <a name="engagement-kpis"></a>Betrokkenheids-KPI's
Een Betrokkenheids-KPI is een prestatie-indicator toomeasure Hallo betrokkenheid van uw gebruikers. Trends op dit gebied kunnen u bepalen Hallo retentie van uw app. Hier volgen enkele voorbeelden van prestatie-indicatoren voor dit type KPI:

* Actieve gebruikers in Hallo afgelopen 7 dagen
* Aantal inactieve gebruikers Hallo afgelopen 7 dagen
* Telling van gebruikers die Hallo-app niet in 30 dagen gebruikt hebben  

Op deze betrokkenheidsindicatoren kunnen ook bepaalde voor de hand liggende externe factoren van invloed zijn. U kunt bijvoorbeeld een mobiel apparaat toobe aan een gebruiker te allen tijde overwegen. Dit kan wel of niet het geval zijn. Een gaming-app vaak een hoger gebruik toohave rond de feestdagen wanneer heeft speelt meer tijdens het werk of school.   

Goed gedefinieerde KPI's in deze categorie kunt u Hallo relatie tussen uw app en uw klanten meten.

#### <a name="technical-kpis"></a>Technische KPI's
Aan de hand van de prestatie-indicatoren in deze categorie kunt u bepalen of uw app goed werkt, of juist vaak vastloopt of crasht. Deze indicatoren kunnen meten Hallo status van uw app en gebruiksproblemen die voorkomen gebruikers dat kunnen via Hallo app bepalen. In deze categorie verzamelde gegevens kan ook informatie over de prestaties die relevant toomarketing teams bevatten. Hallo-gegevens kan ook worden nuttig voor het oplossen van problemen door IT en ondersteuning voor teams toohelp gebruikers gemelde fouten te identificeren. 

Hier volgen enkele voorbeelden van technische KPI's:

* Informatie over onverwerkte of verwerkte uitzonderingen en over het aantal uitzonderingen 
* Tijdstempel voor laatste crash
* Knop waarop het laatst is geklikt of de laatst bezochte webpagina
* Geheugengebruik van het Hallo-app
* Framesnelheid van app
* Versie van het besturingssysteem die Hallo app wordt uitgevoerd op
* App-versie

Definieer deze KPI's toohelp meting van app-prestaties en het detecteren van mogelijke fouten. Deze indicatoren kunnen helpen verminderen Hallo tijd toodeliver een oplossing voor uw klanten. Daarnaast kunnen ze u helpen bij het afbakenen van gebruikerssegmenten die bepaalde problemen ondervinden. U kunt gebruiken dat segmentering toocreate campagnes toodeliver meldingen voor gebruikers over beschikbare oplossingen en potentiële promoties toohelp klanttevredenheid herstellen. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Draaiboekoefening 1: uw KPI-dashboard maken
In uw marketingstrategie moeten uw KPI's elk van uw hoofddoelen inzichtelijk maken. Ze moeten duidelijk gedefinieerde gegevenspunten die zorgen uw app en Hallo gedrag van eindgebruikers Hallo aan u toocollect essentiële informatie toomonitor dat ervoor.

Een KPI-dashboard waarin Hallo onderstaande informatie bouwen

1. Wat zijn Hallo KPI's voor Hallo app?
2. Welke gegevenspunten gaat ik toorepresent elke KPI gebruiken?
3. Waar bevinden zich deze gegevens voor de toepassing (scherm, instellingen, systeem, enz.)?
4. Kan ik voor deze KPI een betrokkenheidsreeks afspelen?

U kunt Hallo **KPI Builder** werkblad in onze [Media Playbook-sjabloon] [ Media Playbook link] voor voorbeelden en richtlijnen.

## <a name="step-2-your-engagement-program"></a>Stap 2: uw betrokkenheidsprogramma
Een doordacht programma voor mobiele betrokkenheid vormt een belangrijk onderdeel van uw app. Essentieel hierin is een aantrekkelijk welkomstprogramma dat voor een gebruiker wordt uitgevoerd tijdens het Hallo eerste dagen van app-gebruik. Dit heeft vaak toohave een zeer positieve invloed op de betrokkenheid bij en retentie van uw app. Uit onderzoek is gebleken dat Hallo meerderheid van gebruikers stoppen met behulp van een app Hallo eerste paar dagen na de installatie. U wilt toostrive toomeet of verwachting vroeg overschrijden terwijl Hallo gebruiker nog steeds is gericht op uw app. Zorg ervoor dat u de presentatie Hallo belangrijkste waarde en voordelen van uw app tooyour klanten. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Pushmeldingen zijn Hallo aanbevolen benadering tooearly betrokkenheid met gebruikers van mobiele apparaten. Maar u moet uiterst voorzichtig zijn met het indelen van gebruikers in segmenten voor pushmeldingen. Wanneer een gebruiker het idee heeft spam of niet-interessante meldingen te ontvangen, kan dit zeer nadelige gevolgen hebben. In enkele klikken kan een gebruiker uw toepassing verwijderen en nooit tooreturn. Hallo Bied gebruikers daarom sterk gepersonaliseerde in-app-waarde in plaats van algemene spam.

Zodra gebruikers actief zijn ingeschakeld, klikt u vervolgens kunt uw betrokkenheidsprogramma andere aspecten van de app Hallo station.

Bijvoorbeeld, u een campagne instellen waarin uw actieve gebruikers toorate uw app. Aangezien dit gebruikerssegment Hallo meest actief is en Hallo de meeste ervaring met uw app heeft, u verwachten dat zij toogive Hallo meest nauwkeurige beoordeling. Zodra u een classificatie van hoge app hebt, kunt u station up Hallo aantal organische downloads van uw app stimuleren en de kosten voor aanschaf van nieuwe klant.

#### <a name="engagement-sequence"></a>Betrokkenheidsreeks
Een universeel betrokkenheidsprogramma bevat verschillende betrokkenheidsreeksen. Elke reeks probeert verschillende doelstellingen tooreach uit.

###### <a name="life-push-sequence"></a>Levenscyclusgerelateerde pushreeks
Hallo doelstellingen voor een Levenscyclusgerelateerde pushreeks zijn verschillend, afhankelijk van Hallo levenscyclus van engagement Hallo van de gebruiker met Hallo-app. Een bepaalde gebruiker kan nieuw zijn, inactief of zeer actief. Gebruikers kunnen in verschillende stadia van de betrokkenheidslevenscyclus profiteren van uw nieuwe inhoud in de vorm van tips of koppelingen toodocumentation Hallo. 

Een nieuwe gebruiker kan bijvoorbeeld moet helpen bij het ophalen van objectgeoriënteerde tooan app of profiteren van een nieuwe gebruiker incentive vergelijkbare toohello na Hallo eerst die Hallo mailapp starten...

*' Fijn dat toohave u vrijgeven! Houd er rekening mee toologin tooget de 1e maand gratis! '*

###### <a name="behavioral-push-sequence"></a>Gedragsgerelateerde pushreeks
Hallo gedragsgerelateerde pushreeks is erop gericht tooincrease-gebruik op basis van gebruikersgedrag verzameld voor Hallo-app.  

Bijvoorbeeld, een zeer actieve gebruiker van een fantasy football-app mogelijk voordeel hebben met de volgende pushmelding Hallo...

*'Jan, je bent een echte fan! Meld u bij tooour NFL-sectie en win kaartjes toohello SuperBowl!'*

###### <a name="alerting-push-sequence"></a>Pushreeks voor meldingen
Gebruikers waarderen relevant nieuws dat te maken heeft met hun interesses. Een pushreeks voor meldingen verhoogt de betrokkenheid door meldingen te sturen op basis van duidelijk afgebakende interesses van de gebruiker. Interesses kunnen expliciet worden, wanneer een gebruiker hun eigen interesses in Hallo-app selecteert. Ook kan worden vastgesteld impliciet op basis van gegevens die tijdens gebruikersinteractie met de app Hallo verzameld.

Hallo gebruiker van een E-Commerce-app kan bijvoorbeeld regelmatig kopen voor een specifiek merk koffie dat u hebt vastgelegd met een zakelijke KPI. Hallo kunt volgende waarschuwing verbeteren door deze gebruiker betrokkenheid bij Hallo-app.

*' Hallo Frank, een van uw favoriete merk koffie worden uitgevoerd in verkoop 25% korting op Hallo eerste week van September 2015. Bedankt dat u als klant en wilden toomake zeker dat u zich bewust was.'*

###### <a name="rentention-push-sequence"></a>Retentiegerelateerde pushreeks
Deze reeks doelstellingen tooretain gebruikers met behulp van een terugkerende melding campagnes toohelp station pushmeldingcampagnes van aanmoedigen Hallo-app. Zo kunt u app-retentie verhogen als gebruiker Hallo Hallo interacties leuk vindt. 

Hallo gebruiker van een sport-app ontvangt bijvoorbeeld Hallo volgende pushmelding wekelijks op basis van Hallo haar favoriete teams:

*'Voor een toowin kans op 200 punten voorspel of Hallo New York Yankees de wedstrijd tegen de Toronto Blue Jays van deze week winnen gaan!'*

#### <a name="hello-3w-approach"></a>Hallo 3W-methode
Hallo verschillende push reeksen mastering helpt u betrokkenheid van eindgebruikers. U moet echter nog steeds toouse Hallo 3W-methode voor het personaliseren van uw meldingen. Hallo 3W-methode dient te houden wie, wat en wanneer van elke melding. Als u hier op de juiste wijze invulling aan geeft, zijn uw meldingen optimaal gericht op betrokkenheid.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Wie: Hallo gebruikerssegment dat berichten ontvangt
Meldingen tooyour gebruikers te pushen moet worden beschouwd als een zeer vertrouwelijk communicatiekanaal. Controleer of Hallo meldingen gericht van toosend tooa gebruikerssegment goed bereik toohello interesses van dat gebruikerssegment. Onjuist gerouteerde meldingen is zeer waarschijnlijk toohave een negatieve invloed op een gebruiker. Ze overwegen deze spam voorloopspaties tooyour app wordt verwijderd. 

Gebruik een combinatie van specifieke technische en gedragscriteria bij het definiëren van de gebruikerssegmenten die meldingen ontvangen. Een eenvoudig voorbeeld een nauwkeurig afgebakend gebruikerssegment mogelijk vergelijkbare toohello-instructie:

'Alle gebruikers die gestart Hallo van een mobiele toepassing voor Hallo eerst drie dagen geleden en Hallo aanmeldingspagina tweemaal vervolgens niet daadwerkelijk een aanmelding hebben bezocht'.

Deze instructie kunt identificeren Hallo-gegevens die u moet toocollect toosupport een specifiek scenario.

###### <a name="what-hello-message-that-you-will-send"></a>Wat: het Hallo-bericht dat u wilt verzenden
**Toon**

Gebruik in uw communicatie een toon die past bij uw gebruikerssegment. Dit is zeker een uitstekende manier tooconnect met uw eindgebruikers en promoveren van een gebruiker interesse in uw app. 

**Omleiding**

Een pushmelding kan worden gebruikt voor het openen van meer dan u Hallo-toepassing. Als hello biedt bericht op een specifieke context, zoals een nieuwsbericht of een productpromotie, deze melding kan de dieptekoppeling naar direct toohello rechtermuisknop inhoud in de toepassing hello. toosupport, moet u een URL schema toolet Hallo toepassing hello omleiding beheren. Tijdens het maken van uw betrokkenheidsreeksen is dit een belangrijke stap die u niet moet vergeten.

Er kunnen ook omleidingen worden beheerd voor andere systemen. Bijvoorbeeld, met een actie-URL is mogelijk tooredirect eindgebruikers toomany andere systemen, zoals Hallo volgende:

* Een website
* Een postvak met ingesteld e-mailadres
* Een sms-vak
* Een beldienst
* Rechtstreeks toohello toepassingsarchief voor het beoordelen van de toepassing hello. 

Dit biedt veel mogelijkheden tooengage eindgebruikers en automatische regels tooimprove prestaties maken.

**Indeling/inhoud**

Er zijn diverse typen en indelingen voor pushmeldingen:

1. **Aankondigingen** : Hiermee kunt u toosend reclame berichten toousers op verschillende momenten (buiten de app in de app of op willekeurige momenten).
2. **Polls** : Hiermee kunt u toogather gegevens van eindgebruikers door vragen aan hen te vragen. De antwoorden zijn vervolgens beschikbaar bij het maken van criteria tootarget eindgebruikers.
3. **Gegevens-Pushes** : Hiermee kunt u toosend een binair of base64-bestand tooupdate Hallo-app. Hallo-gegevens in een gegevens-push tooyour toepassing toopersonalize Hallo gebruikerservaring in uw app verzonden. Uw toepassing moet toobe ontworpen toosupport Hallo gegevens in een gegevens-push.
4. **Tegels (alleen Windows Phone)** : Hiermee kunt u toouse Hallo Microsoft Push Notification Service (MPNS) toosend Native Pushmeldingen met XML-gegevens (dit wordt ondersteund vanaf SDK-versie 0.9.0. Hallo uiteindelijke nettolading voor tegels kan niet groter zijn dan 32 kB.). Hallo-bericht verschijnt rechtstreeks op het mededelingenbord van uw tegel.
5. **Webweergave**: een webweergave is een pop-upvenster met webinhoud. Dit pop-upvenster wordt weergegeven wanneer Hallo door eindgebruikers op Hallo pushmelding heeft geklikt. Een webweergave kunt toohave meer interactie met Hallo door eindgebruikers.

> [!NOTE]
> Zorg ervoor dat dat u pushmeldingen verzendt Hallo-inhoud Hallo het desbetreffende platform (iOS, Android, Windows) richtlijnen voldoet voor het ontwikkelen van apps en het verzenden van pushmeldingen.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Wanneer: de timing van uw campagne Hallo
Wanneer is het beste moment tooactivate Hallo een campagne pushmeldingen te starten? Wordt de campagne handmatig uitgevoerd of automatisch? Moet het een terugkerende campagne worden? Bepalende Hallo juiste moment en de frequentie is essentieel tooengage gebruikers met de beste resultaten Hallo. Voor elke betrokkenheidsreeks en elk scenario moet u opgeven wanneer het beste moment toosend hello pushmeldingen zijn. Hier zijn enkele voorbeelden:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Als u dagelijks veel meldingen verzendt, moet u er rekening mee houden dat uw gebruikers uw communicatie als spam zien. 

Azure Mobile Engagement biedt twee manieren toohelp te voorkomen dat uw communicatie als spam worden beschouwd. Gebruik verfijnde segmentering tooensure u geen doel Hallo dezelfde gebruikers doen. Azure Mobile Engagement biedt bovendien een quotumfunctie. Met deze functie kan het aantal meldingen in een campagne worden beperkt. Bijvoorbeeld, zorgt een standaard quotum too5 per week instellen u dat een gebruiker die is opgenomen als onderdeel van Hallo campagne gebruikerssegment niet meer dan 5 meldingen week ontvangt.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Draaiboekoefening 2: uw betrokkenheidsprogramma maken
Besteed voldoende tijd samenvatten van uw doelstellingen en Hallo campagnes die u tooplay met specifieke reeksen te definiëren. Zorg ervoor dat u Hallo 3W benadering toohello meldingen in uw campagnes toepassen. 

Gebruik Hallo **Betrokkenheidsprogramma** werkblad in Hallo [Media Playbook-sjabloon] [ Media Playbook link] voor voorbeelden en richtlijnen.

## <a name="step-3-app-integration"></a>Stap 3: app-integratie
#### <a name="create-a-tag-plan"></a>Een tagplan maken
toointegrate Azure Mobile Engagement in uw app moet u een tagplan toocreate. Hallo tagplan vormt de basis Hallo van Hallo-project. Het definieert Hallo-relatie tussen de marketingspecificaties, Hallo werkstroom van de toepassing hello en Hallo feitelijke Taggegevens die worden verzameld in Hallo app toomeasure KPI's. Hiermee wordt aangegeven welke analyses u zich toosee in Hallo-portal. Hiermee kunt u ook gebruikerssegmenten te definiëren en gerichte push notifications tooengage uw eindgebruikers verzenden. Zodra u Hallo tagplan gedefinieerd hebt, is toe te voegen Hallo code toointegrate in uw app eenvoudig hello Azure Mobile Engagement SDK gebruiken.

Het is niet de bedoeling dat u met uw tagplan alles in uw toepassing tagt. Alleen taggegevens die onderdeel uitmaken van uw strategie voor mobiele betrokkenheid, moeten hierin worden opgenomen. Wat u wel opneemt en wat niet, verschilt per toepassing. Hallo [Media Playbook-sjabloon] [ Media Playbook link] die Azure Mobile Engagement biedt, helpt u het maken van een tagplan op basis van een bepaalde methode. Gebruik Hallo **Tagplan** werkblad als een handleiding toobuilding uw tagplan.

Bij het definiëren van een tagsectie in Hallo werkblad, Wees zeer specifiek. Dit is erg belangrijk tooavoid verwarring. Werk elk verwacht scenario waarin elke tag wordt verzonden, tot in detail uit. Hallo-naam van het Hallo-activiteit waarin elke tag is ingesloten bevatten. Deze moet allemaal worden opgenomen in Hallo **Informative** deel uit van Hallo werkblad. Hallo tag plan werkblad moet Hallo belangrijkste referentiepunt voor de testverificatie. 

In Hallo **gegevens toocollect** vindt uw ontwikkelteam moet worden Hallo typen, namen, waarden en extra informatie sleutel/waarde-paren die zijn vereist voor elke tag die in de toepassing hello ingesloten.

U wordt aangeraden Hallo tagplan controleren door alle teams die zijn gekoppeld aan het Hallo-project. Breng alle noodzakelijke wijzigingen aan en controleer of alles duidelijk is voor de marketing- en ontwikkelteams.

Hallo **overzicht van de werkzaamheden** werkblad kan worden gebruikt toohelp handleiding iedereen die in Hallo-project is betrokken.

#### <a name="data-types"></a>Gegevenstypen
Dit zijn veelvoorkomende gegevenstypen die door Azure Mobile Engagement worden ondersteund.

###### <a name="devices-and-users"></a>Apparaten en gebruikers
Azure Mobile Engagement identificeert gebruikers door voor elk apparaat een unieke id te genereren. Deze id heet de apparaat-id hello (of de apparaat-id). Deze wordt zodanig dat alle toepassingen op hetzelfde apparaat share Hallo dezelfde apparaat-id gegenereerd.

###### <a name="sessions-and-activities"></a>Sessies en activiteiten
Een sessie is een exemplaar van Hallo-app wordt uitgevoerd door een gebruiker. Hallo-sessie begint op Hallo tijd Hallo gebruiker Hallo-app begint stopt.

Een activiteit is een logische groepering van een aantal dingen Hallo app tijdens een sessie doen mogelijk. Meestal is dit een bepaald scherm in Hallo-app, maar het kan ook dat iets door Hallo logica van de toepassing hello gedefinieerd. U moet in uw app in ieder geval elk venster en elke activiteit taggen. Hierdoor kunt u toounderstand hello gebruikerspad.

###### <a name="events"></a>Gebeurtenissen
Gebeurtenissen zijn gebruikte tooreport gebruikersinteractie met Hallo-app. Ze hebben betrekking op directe bewerkingen, zoals het delen van inhoud of het starten van een video. Taggen van gebeurtenissen biedt u gegevenssets die laten zien hoe gebruikers interacteren met Hallo-app. 

###### <a name="jobs"></a>Taken
Taken zijn gebruikte tooreport acties die een bepaalde duur. Enkele voorbeelden:

* Uitvoering van de API-aanroepen
* Weergavetijd van advertenties
* Duur van achtergrondtaken 
* Duur van het aankoopproces
* Een video bekijken

###### <a name="errors"></a>Fouten
Fouten zijn gebruikte tooreport problemen gedetecteerd door Hallo-app. Denk aan onjuiste gebruikersacties of mislukte API-aanroepen.

###### <a name="application-information"></a>Toepassingsgegevens
Informatie over de toepassing (App-Info) wordt gebruikt tootag gegevens gerelateerd tooa gebruikerservaring met een toepassing. Deze wordt gegenereerd door een gebruikersinteractie met de toepassing hello. 

Voor een sleutel opgegeven app-info Azure Mobile Engagement alleen houdt van Hallo laatste waarde (geen geschiedenis). Toepassingsgegevens geven inzicht in Hallo status van uw app of uw eindgebruikers. Bijvoorbeeld Hallo aanmelden status of de favoriete productgroep van een gebruiker.

###### <a name="crash-data"></a>Crashgegevens
Crashgegevens automatisch worden verzameld door Hallo Mobile Engagement SDK melden toepassingsfouten die niet door de toepassing hello behandeld. Voorbeeld: een onverwerkte uitzondering.

###### <a name="extra-data"></a>Extra gegevens
Gebeurtenissen, fouten, activiteiten en taken kunnen worden uitgebreid met parameters. Dit is een ontwikkelaar als specifieke gegevens van de toepassing hello bieden kan van extra gegevens. Deze gegevens zijn belangrijk voor het definiëren van verfijnde segmentering. 

Bijvoorbeeld, kunt Hallo-waarde van een 'article'-tag u toosegment eindgebruikers op basis van die bepaald artikel heeft bekeken. Mogelijk is dit echter niet voldoende. Wellicht is het beter als deze 'article'-tag ook extra informatie, zoals 'news_category', binnen een activiteit bevat. Dit kan handig zijn toodetermine Hallo dynamisch favoriete categorieën van Hallo-gebruiker. 

Extra gegevens worden doorgegeven als sleutel-/waardepaar. In voorbeeld Hallo voor deze mediatoepassing zou Hallo extra gegevens voor 'news_category' Hallo-waarde voor die categorie zijn. Bijvoorbeeld 'sport', 'economie' of 'politiek'.

#### <a name="tag-and-sdk-integration"></a>Tag- en SDK-integratie
Voor stapsgewijze instructies voor het integreren van hello Azure Mobile Engagement SDK in uw app, volg Hallo [Engagement SDK-integratie](mobile-engagement-windows-store-integrate-engagement.md) documentatie op Azure-website. Kies uw doelplatform in koppelingen Hallo Hallo boven aan deze pagina.

Het is raadzaam om projecten te maken voor twee apps gebouwd op Azure Mobile Engagement. Een voor ontwikkeling en testfase en Hallo andere voor de productiefase. Uw IT-team kunt vervolgens promoveren test tooproduction voor fasering als gebruikersacceptatietests Hallo geslaagd is.

#### <a name="user-acceptance-testing-uat"></a>Gebruikersacceptatietests
Gebruikersacceptatietests zijn bedoeld om ervoor te zorgen dat alles werkt zoals ontworpen. Werkstromen kunnen worden voltooid en alle vereiste gegevens kunnen op basis van uw tagplan worden verzameld:

* Codering van gegevens moet worden voldaan volgens toodocumented AZME-concepten
* Alle benodigde gegevens worden verzameld (inclusief extra gegevens en toepassingsgegevens)
* Naamgeving volgt de namen overeenkomen met volgens tooyout Tagplan
* Er worden geen dubbele tags verzonden

Alle Hallo soorten meldingsgedrag die u in uw app hebt ingesloten grondig te testen

* Aankondigingen, polls, gegevens-pushes buiten en in de app
* Tekst-/webweergaven
* Badge-update, categorieën

#### <a name="setup"></a>Instellen
Het instellen van Azure Mobile Engagement is zeer eenvoudig. Alle Hallo documentatie gerelateerde toohello gebruikersinterface is beschikbaar op Hallo Azure Mobile Engagement-website: [hoe toonavigate gebruikersinterface Hallo](mobile-engagement-user-interface-home.md).

Het wordt aanbevolen dat u door het instellen van de juiste Hallo-rollen en rollidmaatschappen voor gebruikers van uw project Hallo start. Zo kunt u de juiste toegangsrechten toohello platform voor alle gebruikers beheren. De rollen kunnen zijn:

* Beheerders
* Ontwikkelaars
* Kijkers 

Daarna:

* Registreer uw apparaat-id tootest op uw eigen apparaat.
* Ga toohello-instellingen van uw account en stel Hallo tijdzone toohave grafieken en leveringstijd melding instellen voor uw eigen tijdzone.
* Ga toohello-instellingen van uw toepassing en registreer Hallo 'App-info' moet u tootarget eindgebruikers binnen handbereik.

Voor meer informatie over hoe toorun uw eerste push-melding campagne, Bekijk [hoe tooget gestart met en het beheer van pushmeldingen tooreach uit tooyour eindgebruikers](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusie
Betrokkenheidsprogramma's zijn niet eenmalig. Experimenteer daarom met wat het beste voor uw app werkt en verbeter uw programma continu op basis hiervan. 

In eerste instantie wordt tijdens de ontwikkeling van ervaring met engagement probeer strategieën niet toobuild een overkoepelende betrokkenheidsstrategie. Een stapsgewijze benadering voor het identificeren van de KPI's en hoe tooleverage ze. Voor elke app maakt u een unieke betrokkenheidsstrategie.

U kunt overwegen Hallo volgende tooyour engagement programma's toevoegen nadat u hebt enige ervaring met ontwikkeld:

* Prestaties bijhouden: u krijgt gebruikers en u definieert waarschijnlijk bronnen voor gegevensverzameling. Azure mobile Engagement kan worden bronnen gekoppeld toodata-verzameling. Hiermee kunt u toomonitor prestaties van elke bron. Deze informatie worden interessante toomaximize uw investering. 
* A/B-tests: dit is een essentieel onderdeel van het betrokkenheidsprogramma. Elke app heeft zijn eigen specificaties. Met A/B-tests kunt u uw betrokkenheidsprogramma verbeteren.
* Geografische locatie: dit is een grote kans voor merken. Met vriendelijke groet toothis functie die u kunt bereiken op de juiste plaats Hallo en tijd. U wordt aangeraden verifiëren dat u voldoende gegevens voor het gedrag van eindgebruikers voordat u begint toouse geografische locatie hebt verzameld.
* Gegevens-push: een gegevens-push is een onzichtbare push. Met een gegevens-push kunt u uw toepassingen aanpassen op basis van het gedrag van eindgebruikers. Als een gebruikerssegment vaak high tech-producten raadpleegt, kan de eigenaar van de app Hallo een gegevens-push die haar startpagina met hightechinhoud wordt aangepast verzenden.

## <a name="next-steps"></a>Volgende stappen
* [Een Azure Mobile Engagement-account maken](mobile-engagement-create.md).
* Ga naar [uw Mobile Engagement-strategie definiëren](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn meer over het definiëren van uw Mobile Engagement-strategie.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
