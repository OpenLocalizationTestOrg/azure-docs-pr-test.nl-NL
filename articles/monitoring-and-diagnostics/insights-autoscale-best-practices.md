---
title: aaaBest procedures voor automatisch schalen | Microsoft Docs
description: Patronen voor automatisch schalen in Azure voor Web-Apps, Virtual Machine-schaalsets en Cloud-Services
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Aanbevolen procedures voor Automatisch schalen
In dit artikel leert best practices tooautoscale in Azure. Monitor voor automatisch schalen die Azure geldt alleen te[virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloudservices](https://azure.microsoft.com/services/cloud-services/), en [App Service - Web-Apps](https://azure.microsoft.com/services/app-service/web/). Andere Azure-services verschillende schalen methoden gebruiken.

## <a name="autoscale-concepts"></a>Concepten voor automatisch schalen
* Een resource kan alleen hebben *één* instelling voor automatisch schalen
* Een instelling voor automatisch schalen kan een of meer profielen en elk profiel zijn een of meer regels voor automatisch schalen.
* Een instelling voor automatisch schalen schaalt exemplaren horizontaal, namelijk *uit* doordat Hallo exemplaren en *in* door te verlagen Hallo aantal exemplaren.
  Een instelling voor automatisch schalen heeft een maximale, minimale en standaardwaarde van exemplaren.
* Een taak voor automatisch schalen leest altijd Hallo metrische tooscale controleren door gekoppeld als het geconfigureerde drempelwaarde Hallo voor scale-out of de schaal is gepasseerd. U kunt een lijst weergeven van metrische gegevens die automatisch schalen kunt schalen door op [Azure Monitor automatisch schalen algemene metrische gegevens](insights-autoscale-common-metrics.md).
* Alle drempelwaarden zijn berekend op het niveau van een exemplaar. Bijvoorbeeld ' scale door 1 exemplaar wanneer gemiddelde CPU > 80% wanneer het aantal exemplaren is 2 ', scale-out betekent dat als de gemiddelde CPU Hallo over alle exemplaren groter dan 80 is %.
* U ontvangt altijd fout meldingen via e-mail. In het bijzonder ontvangen Hallo eigenaar, bijdrager en lezers van Hallo doelbron e-mail. U ontvangt ook altijd een *herstel* Stuur een e-mail wanneer automatisch schalen vanuit een fout herstelt en begint met het normaal functioneert.
* U kunt aanmelden tooreceive een geslaagde scale actie-melding via e-mail en webhooks.

## <a name="autoscale-best-practices"></a>Aanbevolen procedures voor automatisch schalen
Gebruik Hallo volgende aanbevolen procedures als u automatisch schalen.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Zorg ervoor dat Hallo maximale en minimale waarden zijn verschillend en een voldoende marge tussen deze twee hebben
Als u een instelling van minimaal hebt = 2, maximale = 2 en het huidige aantal exemplaren Hallo 2 is geen schaalactie kan optreden. Houd een voldoende marge tussen Hallo maximale en minimale exemplaar aantallen, inclusief zijn. Automatisch schalen schaalt altijd tussen deze limieten.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>Handmatig schalen wordt opnieuw ingesteld door automatisch schalen min en max
Als u handmatig werk Hallo exemplaar aantal tooa waarde boven of onder Hallo-maximum Hallo engine voor het automatisch schalen automatisch wordt geschaald back toohello minimale (indien hieronder) of Hallo maximale (indien hierboven). Bijvoorbeeld, opgeven u Hallo waarde tussen 3 en 6. Als u een actief exemplaar hebt, schaalt Hallo automatisch schalen engine too3 instanties op de volgende keer wordt uitgevoerd. Ook kan het zou schaal in 8 exemplaren back-too6 op de volgende keer wordt uitgevoerd.  Handmatig schalen is zeer tijdelijk tenzij u Hallo automatisch schalen regels ook opnieuw instellen.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Gebruik altijd een combinatie van scale-out en schaal in regel waarmee een verhogen en de afname
Als u slechts één deel van de combinatie hello, is automatisch schalen scale-dat in enkele uit of in, tot Hallo maximum of minimum, bereikt.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Niet overschakelen tussen hello Azure-portal en de klassieke Azure-portal Hallo bij het beheren van automatisch schalen
Hello Azure-portal (portal.azure.com) toocreate gebruiken en beheren van instellingen voor automatisch schalen voor Cloudservices en App-Services (Web-Apps). Gebruik voor de virtuele-Machineschaalsets toocreate PowerShell, CLI of REST-API en beheren van de instelling voor automatisch schalen. Niet schakelen tussen Hallo klassieke Azure-portal (manage.windowsazure.com) en hello Azure-portal (portal.azure.com) bij het beheren van configuraties voor automatisch schalen. Hallo klassieke Azure-portal en de onderliggende back-end heeft beperkingen. Verplaats toohello Azure portal toomanage automatisch schalen met een grafische gebruikersinterface. Hallo-opties zijn toouse Hallo automatisch schalen PowerShell, CLI of REST-API (via Azure Resource Explorer).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>De juiste statistiek Hallo voor uw metriek diagnostische gegevens kiezen
Voor de metrische gegevens voor diagnostische gegevens, kunt u kiezen uit *gemiddelde*, *Minimum*, *maximale* en *totale* als een metrische tooscale door. de meest voorkomende statistieken Hallo *gemiddelde*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Hallo drempelwaarden zorgvuldig voor alle metrische typen kiezen
Het is raadzaam om verschillende drempelwaarden voor scale-out en schaal in op basis van praktische situaties zorgvuldig te kiezen.

We *wordt niet aanbevolen* de instellingen voor automatisch schalen zoals Hallo voorbeelden hieronder met dezelfde of een vergelijkbaar drempelwaarden voor out en in situaties Hallo:

* Exemplaren verhoogd met 1 tellen wanneer aantal threads < = 600
* Exemplaren verlagen door 1 tellen wanneer aantal threads > = 600

Bekijk een voorbeeld van wat kan leiden tooa gedrag ontstaan. Houd rekening met Hallo sequence te volgen.

1. Wordt ervan uitgegaan dat er 2 exemplaren toobegin met en vervolgens Hallo kunt u het gemiddelde aantal threads per exemplaar too625 groeit.
2. Automatisch schalen uitgeschaald een 3e exemplaar toe te voegen.
3. Vervolgens wordt ervan uitgegaan dat Hallo gemiddelde threads tussen exemplaar too575 valt.
4. Voordat het verkleinen, probeert automatisch schalen tooestimate welke eindstatus Hallo worden als deze aangepast. Voorbeeld: 575 x 3 (huidige aantal exemplaren) = 1,725 / 2 (definitieve aantal exemplaren als verkleind) = 862.5 threads. Dit betekent dat automatisch schalen zou tooimmediately scale-out opnieuw zelfs nadat deze wordt geschaald als Hallo gemiddelde thread aantal blijft Hallo dezelfde of zelfs slechts een kleine hoeveelheid valt. Als deze opgeschaald opnieuw het hele proces hello wilt herhalen, leidt echter tooan oneindige lus.
5. tooavoid deze situatie ('flapping' genoemd), automatisch schalen niet kan worden uitgebreid naar beneden op alle. In plaats daarvan wordt overgeslagen en reevaluates Hallo voorwaarde opnieuw Hallo volgende time Hallo-service de taak wordt uitgevoerd. Dit kan veel mensen verwarrend omdat automatisch schalen wouldn't toowork wordt weergegeven wanneer het gemiddelde aantal threads Hallo 575 is.

Schatting tijdens een scale-in is beoogde tooavoid 'op en neer' situaties waarbij schaal in en scale-out acties voortdurend heen en weer gaat. Houd rekening met dit gedrag wanneer u dezelfde drempels voor scale-out en in Hallo kiest.

U wordt aangeraden een voldoende marge tussen Hallo scale-out en in de drempelwaarden te kiezen. Een voorbeeld kunt u beter Hallo betere combinatie van de regel te volgen.

* Exemplaren verhoogd met 1 tellen wanneer CPU-percentage > = 80
* Exemplaren verlagen door 1 tellen wanneer CPU-percentage < = 60

In dit geval  

1. Wordt ervan uitgegaan dat er 2 exemplaren toostart met zijn.
2. Als de gemiddelde CPU-percentage Hallo over exemplaren gaat too80, schaalt automatisch schalen uit het toevoegen van een derde exemplaar.
3. Nu wordt ervan uitgegaan dat de % via tijd Hallo CPU too60 valt.
4. Automatisch schalen van schaal in regel maakt een schatting van de eindstatus Hallo alsof het tooscale in. Voorbeeld: 60 x 3 (huidige aantal exemplaren) = 180 / 2 (definitieve aantal exemplaren als verkleind) = 90. Dus voor automatisch schalen biedt niet schaal aan omdat deze zou tooscale-out onmiddellijk opnieuw. In plaats daarvan overgeslagen bij het verkleinen.
5. Hallo volgende tijd automatisch schalen Hallo CPU blijft toofall too50 wordt gecontroleerd. Schat opnieuw - exemplaar 50 x 3 = 150 / 2 exemplaren = 75, dat zich onder de drempelwaarde voor het scale-out van 80, Hallo zodat het schalen in is too2 exemplaren.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Overwegingen voor het schalen van drempelwaarden voor speciale metrische gegevens
 Hallo-drempelwaarde is voor speciale metrieken zoals opslag- of Service Bus-wachtrij lengte metriek Hallo kunt u het gemiddelde aantal berichten per huidige aantal exemplaren van beschikbaar. Kies zorgvuldig Hallo Hallo drempelwaarde voor deze metrische gegevens kiezen.

Wordt toegelicht aan deze met een voorbeeld tooensure u Hallo gedrag beter begrijpt.

* Exemplaren verhogen door 1 aantal wanneer Opslagwachtrij bericht count > = 50
* Exemplaren met 1 aantal verlagen als Opslagwachtrij mailbericht aantal < = 10

Houd rekening met Hallo volgende volgorde:

1. Er zijn exemplaren van de wachtrij 2 opslag.
2. Berichten houden afkomstig is en wanneer u hello opslagwachtrij bekijkt, het totale aantal Hallo 50 leest. U kunt wordt ervan uitgegaan dat automatisch schalen een scale-out-actie moet worden gestart. Echter, houd er rekening mee dat het nog steeds 50/2 = 25-berichten per exemplaar. Scale-out wordt dus niet uitgevoerd. Voor de eerste een scale-out toohappen Hallo moet Hallo totale aantal berichten in wachtrij voor Hallo opslag 100.
3. Vervolgens wordt ervan uitgegaan dat Hallo totale aantal berichten gelijk is aan 100.
4. Een 3e exemplaar van de storage-wachtrij is toegevoegd vanwege tooa scale-out actie.  Hallo volgende scale-out actie gebeurt niet totdat Hallo totaal aantal berichten in wachtrij Hallo 150 bereikt omdat 150/3 = 50.
5. Nu wordt het aantal berichten in wachtrij Hallo Hallo verkleind. Met 3 exemplaren eerste Hallo schaal in actie gebeurt er wanneer hello totaal aantal berichten in alle wachtrijen too30 optellen omdat 30/3 = 10 berichten per instantie Hallo schaal in de drempelwaarde.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Overwegingen voor het schalen van wanneer er meerdere profielen worden geconfigureerd in een instelling voor automatisch schalen
U kunt een standaard-profiel altijd zonder een afhankelijkheid op schema of tijd toegepast wordt, in een instelling voor automatisch schalen, of kunt u een terugkerende profiel of een profiel voor een bepaalde periode met een bereik van de datum en tijd.

Als de service automatisch schalen verwerkt, controleert deze altijd in Hallo volgorde:

1. Vaste datum profiel
2. Terugkerende profiel
3. Standaard-profiel ("Always")

Als een profiel voorwaarde wordt voldaan, wordt automatisch schalen Hallo volgende profiel voorwaarde eronder niet gecontroleerd. Automatisch schalen verwerkt alleen één profiel tegelijk. Dit betekent dat als u wilt dat tooalso omvatten een verwerkingsvoorwaarde van een lagere lagen-profiel, moet u deze regels ook opnemen in het huidige profiel Hallo.

Laten we Controleer dit met een voorbeeld:

Hallo in onderstaande afbeelding ziet u een instelling voor automatisch schalen met een standaardprofiel met minimale exemplaren = 2- en maximumaantal exemplaren = 10. In dit voorbeeld zijn regels geconfigureerd tooscale-out als aantal voor Hallo-berichten in wachtrij Hallo groter dan 10 en de schaal is als aantal voor Hallo-berichten in wachtrij Hallo minder dan 3 is. Hallo resource kan nu worden geschaald tussen 2 en 10 exemplaren.

Er is bovendien een terugkerende profiel instellen voor maandag. Deze waarde is ingesteld voor minimale exemplaren = 2- en maximumaantal exemplaren = 12. Dit betekent dat op maandag, Hallo eerste tijd automatisch schalen voor deze voorwaarde controleert als Hallo exemplaren 2 is, het nieuwe minimum van 3 toohello schalen. Zolang automatisch schalen blijft toofind deze voorwaarde profiel overeenkomende (maandag), wordt alleen verwerkt Hallo op basis van CPU scale-out/in regels die zijn geconfigureerd voor dit profiel. Deze controleert op dit moment niet op Hallo wachtrijlengte. Echter als u ook Hallo wachtrij lengte voorwaarde toobe is ingeschakeld wilt, u moet deze regels opnemen uit Hallo standaardprofiel ook in uw profiel maandag.

Op dezelfde manier als voor automatisch schalen back toohello standaardprofiel verandert, controleert eerst deze als Hallo minimum en maximum voorwaarden wordt voldaan. Als Hallo aantal exemplaren op Hallo moment 12, schalen het in too10, Hallo maximaal is toegestaan voor Hallo standaardprofiel.

![instellingen voor automatisch schalen](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Overwegingen voor het schalen van wanneer meerdere regels zijn geconfigureerd in een profiel
Er zijn ook gevallen waarbij u tooset meerdere regels in een profiel wellicht. Hallo volgende reeks regels voor automatisch schalen die worden gebruikt door services gebruikt wanneer meerdere regels worden ingesteld.

Op *uitschalen*, automatisch schalen die wordt uitgevoerd als alle regels is voldaan.
Op *schaal in*, automatisch schalen is vereist voor alle regels toobe voldaan.

tooillustrate, wordt ervan uitgegaan dat u hebt Hallo 4 regels voor automatisch schalen:

* Als CPU < 30% schaal in met 1
* Als geheugen < 50% schaal in met 1
* Als CPU > 75%, scale-out van 1
* Als geheugen > 75%, scale-out van 1

Vervolgens vindt plaats Hallo volgen:

* Als geheugen is 50% CPU is 76% we scale-out.
* Als is 50% van CPU en geheugen 76% we scale is-out.

Daarentegen op Hallo als is 25% van CPU en geheugen 51% automatisch schalen biedt **niet** schaal in. In volgorde tooscale in moet CPU 29% en geheugen 49%.

### <a name="always-select-a-safe-default-instance-count"></a>Altijd een veilige standaardexemplaren selecteren
Hallo standaardexemplaren is belangrijk voor automatisch schalen uw aantal toothat wordt geschaald wanneer metrische gegevens niet beschikbaar zijn. Selecteer daarom een standaard-exemplaren die voor uw werkbelastingen veilig is.

### <a name="configure-autoscale-notifications"></a>Meldingen over automatisch schalen configureren
Automatisch schalen waarschuwt Hallo-beheerders en medewerkers van de resource Hallo per e-mail als een van de volgende voorwaarden Hallo optreedt:

* de service automatisch schalen mislukt tootake een actie.
* Metrische gegevens zijn niet beschikbaar voor automatisch schalen service toomake een beslissing schaal.
* Metrische gegevens zijn beschikbaar (herstelserver) opnieuw toomake een beslissing schaal.
  Bovendien toohello voorwaarden bovenstaande, kunt u e-mailadres of webhook meldingen tooget de hoogte gesteld van geslaagde scale acties.
  
U kunt ook een activiteitenlogboek waarschuwing toomonitor Hallo gezondheid van de engine voor het automatisch schalen hello gebruiken. Hier volgen voorbeelden te[maken van een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) of te[maken van een activiteit logboek waarschuwing toomonitor alle is mislukt voor automatisch schalen schaal / operations uitbreiden op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Volgende stappen
- [Maak een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Een activiteit logboek waarschuwing toomonitor alle is mislukt voor automatisch schalen schaal / uitschalen bewerkingen op uw abonnement maken](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
