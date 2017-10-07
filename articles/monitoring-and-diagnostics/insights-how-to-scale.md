---
title: aaaScale count-instantie handmatig of automatisch schalen met Azure Portal | Microsoft Docs
description: Meer informatie over hoe tooscale uw Azure-services.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Aantal exemplaren handmatig of automatisch schalen
In Hallo [Azure Portal](https://portal.azure.com/), kunt u handmatig Hallo-exemplaren van uw service instellen of, kunt u parameters toohave het automatisch schalen op basis van vraag instellen. Dit is doorgaans waarnaar wordt verwezen tooas *uitschalen* of *schalen*.

Voordat u schalen op basis van exemplaren, moet u overwegen schalen wordt beïnvloed door **prijscategorie** in toevoeging tooinstance aantal. Andere Prijscategorieën kan hebben verschillende aantallen kernen en het geheugen en dus betere prestaties voor Hallo hebben hetzelfde aantal exemplaren (dit is *opschalen* of *omlaag schalen*). Dit artikel behandelt specifiek *schalen* en *uit*.

In de portal Hallo kunnen worden geschaald en u kunt ook Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn931953.aspx) of [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust handmatig of automatisch schalen.

> [!NOTE]
> Dit artikel wordt beschreven hoe toocreate een instelling in de portal op Hallo voor automatisch schalen [http://portal.azure.com](http://portal.azure.com). Instellingen voor automatisch schalen gemaakt in deze portal kunnen niet worden bewerkt het Hallo-classic-portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Handmatig schalen
1. In Hallo [Azure Portal](https://portal.azure.com/), klikt u op **Bladeren**, navigeert u vervolgens toohello-bron die u wilt dat tooscale, zoals een **App Service-abonnement**.
2. Klik op **instellingen > Scale-out (App Service-abonnement).**
3. Hallo boven aan het Hallo **Scale** blade ziet u een geschiedenis van acties voor automatisch schalen van Hallo-service.
   
    ![Scale-blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Alleen de acties die worden uitgevoerd door automatisch schalen wordt in deze grafiek weergegeven. Als u handmatig Hallo exemplaren aanpast, wordt Hallo wijziging niet weerspiegeld in deze grafiek.
   > 
   > 
4. U kunt handmatig Hallo getal aanpassen **exemplaren** met schuifregelaar.
5. Klik op Hallo **opslaan** opdracht en u zult bijna onmiddellijk toothat aantal instanties geschaald.

## <a name="scaling-based-on-a-pre-set-metric"></a>Schalen op basis van een vooraf ingestelde waarde
Als u wilt dat het aantal exemplaren tooautomatically aanpassen op basis van een metriek hello, selecteer metrische gegevens die u in Hallo wilt Hallo **schalen door** vervolgkeuzelijst. Bijvoorbeeld: voor een **App Service-abonnement** kunnen worden geschaald door **CPU-Percentage**.

1. Wanneer u een metriek selecteert u krijgt een schuifregelaar of tekst vakken tooenter Hallo aantal exemplaren van gewenste tooscale tussen:
   
    ![Scale-blade met CPU-Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Automatisch schalen duurt nooit uw service of meer dan Hallo grenzen die u hebt ingesteld, ongeacht de belasting.
2. Ten tweede kunt u Hallo doelbereik voor de metriek Hallo kiezen. Bijvoorbeeld, als u hebt gekozen **CPU-percentage**, u kunt een doel voor Hallo gemiddelde CPU instellen voor alle exemplaren van Hallo in uw service. Een scale-out er gebeurt wanneer de gemiddelde CPU Hallo overschrijdt Hallo die u definiëren, een schaal in gebeurt ook wanneer het gemiddelde CPU Hallo zakt onder Hallo minimale.
3. Klik op Hallo **opslaan** opdracht. Automatisch schalen, elke paar minuten toomake ervoor dat u zich in Hallo exemplaar bereik en doel voor de metriek controleren. Wanneer uw service extra verkeer ontvangt, krijgt u meer exemplaren zonder dat u een actie uitvoert.

## <a name="scale-based-on-other-metrics"></a>Schalen op basis van andere metrische gegevens
U kunt schalen op basis van metrische gegevens dan Hallo standaardinstellingen die worden weergegeven in Hallo **schalen door** vervolgkeuzelijst en kan zelfs een complexe reeks scale-out hebben en schalen in regels.

### <a name="adding-or-changing-a-rule"></a>Het toevoegen of wijzigen van een regel
1. Kies Hallo **planning en prestaties regels** in Hallo **schalen door** dropdown: ![Prestatieregels](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Als u had eerder automatisch schalen, ziet op u een weergave van Hallo exacte regels die u had.
3. tooscale op basis van een andere metrische Klik Hallo **regel toevoegen** rij. U kunt ook klikken op een van de bestaande rijen toochange van Hallo metriek Hallo u toohello metriek gewenste tooscale door eerder had.
   ![Regel toevoegen](./media/insights-how-to-scale/Insights_AddRule.png)
4. Nu moet u tooselect welke waarde u wilt dat tooscale door. Wanneer er een waarde kiezen zijn een aantal dingen tooconsider:
   
   * Hallo *resource* Hallo metriek is afkomstig uit. Normaal gesproken zal dit worden Hallo dezelfde zijn als u bent bezig met het Hallo-resource. Als u tooscale door Hallo diepte van een opslagwachtrij wilt, is Hallo resource Hallo wachtrij die u wilt dat tooscale door.
   * Hallo *metrische naam* zelf.
   * Hallo *tijd aggregatie* van Hallo metrische gegevens. Dit is hoe Hallo gegevens combineren via Hallo *duur*.
5. Nadat u hebt gekozen uw metriek u Hallo drempelwaarde voor Hallo metriek en Hallo operator. U kunt bijvoorbeeld zeggen **groter is dan** **80%**.
6. Kies vervolgens Hallo actie die u tootake wilt. Er zijn een aantal verschillende soorten acties:
   
   * Vergroten of verkleinen door - Hiermee kunt toevoegen of verwijderen van Hallo **waarde** aantal exemplaren dat u definieert
   * Vergroten of verkleinen percentage - hierdoor Hallo-exemplaren wordt gewijzigd door een percentage. U kan bijvoorbeeld 25 geplaatst in Hallo **waarde** veld, en als u momenteel 8 exemplaren had, 2, zou worden toegevoegd.
   * Vergroten of te verkleinen - Hiermee wordt ingesteld Hallo exemplaar aantal toohello **waarde** u definieert.
7. Ten slotte kunt u coolbar omlaag - hoe lang deze regel na Hallo vorige scale actie tooscale opnieuw wachten moet.
8. Klik na het configureren van de regel **OK**.
9. Wanneer u Hallo regels die u hebt geconfigureerd, worden ervoor toohit hello **opslaan** opdracht.

### <a name="scaling-with-multiple-steps"></a>Schaling mogelijk met meerdere stappen
Hallo-voorbeelden die hierboven zijn vrij eenvoudig. Als u wilt toobe agressievere over het schalen van (of omlaag), u kunt echter zelfs toevoegen schalen op meerdere regels voor Hallo dezelfde metrische gegevens. U kunt bijvoorbeeld twee scale regels definiëren op CPU-percentage:

1. Uitbreiden door 1 exemplaar als CPU-percentage hoger dan 60 is %
2. Uitbreiden door 3 exemplaren als CPU-percentage hoger dan 85 is %

![Meerdere schaalregels](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Met deze extra regel als uw load groter is dan 85% voordat een schaalactie krijgt u twee extra exemplaren in plaats van een.

## <a name="scale-based-on-a-schedule"></a>Schalen op basis van een planning
Standaard bij het maken van een scale-regel wordt altijd toegepast. U kunt zien dat wanneer u op Hallo profiel header:

![Profiel](./media/insights-how-to-scale/Insights_Profile.png)

U kunt echter toohave agressievere schalen tijdens Hallo dag of week hello, dan op Hallo weekend. U kan zelfs uw service volledig buiten kantooruren afgesloten.

1. toodo dit, op Hallo profiel die u hebt, selecteert u **terugkeerpatroon** in plaats van **altijd,** en kies Hallo keer dat u wilt dat Hallo profiel tooapply.
2. Bijvoorbeeld, een profiel dat wordt toegepast tijdens het Hallo-week in Hallo toohave **dagen** dropdown schakelt **zaterdag** en **zondag**.
3. een profiel dat wordt toegepast tijdens Hallo tijdens kantooruren, stel Hallo toohave **begintijd** toohello tijd van de dag die u wilt dat toostart op.
   
    ![Standaardterugkeerpatroon](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Klik op **OK**.
5. Vervolgens moet u tooadd Hallo profiel dat u wilt dat tooapply op andere tijden. Klik op Hallo **profiel toevoegen** rij.
    ![Werk](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Naam van uw nieuwe, tweede, profiel, bijvoorbeeld u het kunt aanroepen **uitgeschakeld werk**.
7. Selecteer vervolgens **terugkeerpatroon** opnieuw, en kies Hallo exemplaar aantal bereik u tijdens deze periode.
8. Zoals met Hallo standaardprofiel, kiest Hallo **dagen** u wilt dat deze tooapply profiel op en hello **begintijd** tijdens Hallo dag.
   
   > [!NOTE]
   > Automatisch schalen Hallo Daylight besparingen regels gebruikt voor afhankelijk van wat **tijdzone** u selecteert. Echter tijdens zomertijd Hallo UTC-offset Hallo base tijdzoneverschil, niet Hallo Daylight besparingen UTC-offset wordt weergegeven.
   > 
   > 
9. Klik op **OK**.
10. Nu moet u tooadd regels wat u wilt dat tooapply tijdens uw tweede profiel. Klik op **regel toevoegen**, en vervolgens kunt u dezelfde regel hebt u tijdens het standaardprofiel Hallo Hallo opgeven.
    
    ![Regel toooff werk toevoegen](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Ervoor toocreate beide een regel voor scale-out en schaal worden, of anders tijdens Hallo wordt profiel Hallo-exemplaren alleen vergroten (of verlagen).
12. Tot slot op **opslaan**.

## <a name="next-steps"></a>Volgende stappen
* [Service metrische gegevens controleren](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
* [Inschakelen bewaking en diagnostische gegevens](insights-how-to-use-diagnostics.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.
* [Ontvang waarschuwingsmeldingen](insights-receive-alert-notifications.md) wanneer er operationele gebeurtenissen plaatsvinden of metrische gegevens een drempelwaarde overschrijden.
* [Bewaken van toepassingsprestaties](../application-insights/app-insights-azure-web-apps.md) als u wilt dat toounderstand precies hoe uw code uitvoert in de cloud Hallo.
* [Weergeven van gebeurtenissen en het activiteitenlogboek](insights-debugging-with-events.md) toolearn alles wat u in uw service heeft plaatsgevonden.
* [Beschikbaarheid en reactiesnelheid van een webpagina bewaken](../application-insights/app-insights-monitor-web-app-availability.md) met Application Insights zodat u ontdekken kunt als uw pagina niet beschikbaar is.

