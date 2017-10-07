---
title: aaaAzure gebruikersinterface van de Mobile Engagement - analyses
description: Meer informatie over hoe tooanalyze historische gegevens over uw toepassing met behulp van Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Hoe tooanalyze historische gegevens over uw toepassing
Dit artikel wordt beschreven Hallo **ANALYTICS** tabblad Hallo **Mobile Engagement** portal. Gebruik van Hallo **Mobile Engagement** portal toomonitor en beheren van uw mobiele apps. Houd er rekening mee dat toostart met Hallo portal toocreate moet u eerst een **Azure Mobile Engagement** account.

Hallo Analytics sectie Hallo gebruikersinterface biedt verzamelde informatie over uw toepassing die is gebaseerd op historische gegevens die wordt elke 24 uur bijgewerkt. Hallo-informatie wordt weergegeven op de verschillende dashboards bestaat uit staaf-lijn-cirkel grafieken, rasters en maps. Hallo-gegevens kunnen ook worden gedownload als CSV-bestanden. De meeste van deze informatie is beschikbaar in realtime in Hallo Monitor sectie Hallo gebruikersinterface en deze kan ook worden geopend op Hallo Analytics-API.

> [!NOTE]
> Veel secties Hallo **Mobile Engagement** gebruikersinterface portal bevatten Hallo **HELP weergeven** knop. Druk op deze knop tooget meer contextuele informatie over een sectie.

## <a name="standard-and-custom-analytics"></a>Standaard- en aangepaste Analytics
Azure Mobile Engagement biedt een set basic, standard analytische gegevens over uw toepassingen die kunnen worden diagram weergegeven aan als u uw app met Hallo SDK integreren. Azure Mobile Engagement biedt ook Hallo mogelijkheid toogather aanvullende aangepaste analyses gewenste informatie over de werking van uw eindgebruikers. U kunt dit doen door het maken van een tagplan op basis van aangepaste 'labels (app-info)', gemaakt op basis van **instellingen** zodat Azure Mobile Engagement van deze extra gegevens voor u verzamelen kunt.

## <a name="analytics"></a>Analytische gegevens
* Dashboard: Bevat algemene informatie over nieuwe en u gebruikers en hun trends.
* Gebruikers: Gebruikers worden geïdentificeerd door hun apparaat-id: deze id is uniek voor elk apparaat (een nieuwe gebruiker is een nieuw apparaat). Een gebruiker wordt beschouwd als nieuwe op een bepaald tijdsinterval als hij gedurende dit tijdsinterval eerste sessie heeft uitgevoerd. Een gebruiker wordt beschouwd als terugkerend als hij ten minste één sessie tijdens Hallo afgelopen 7 dagen is uitgevoerd. Actieve gebruikers zijn gebruikers die ten minste één sessie gedurende een bepaalde periode. U kunt sorteren, maandelijks, wekelijks, dagelijks of per uur perioden. Alle Hallo grafieken lijken, maar kunt u toofilter door verschillende functies, zoals Hallo-versie van uw toepassing en toosort door een bepaalde periode. Hallo standaardgegevens verzameld door de integratie van Hallo SDK omvat Hallo volgende: actieve gebruikers, nieuwe gebruiker, het aantal sessies, lengte van elke sessie, technische informatie over Hallo land, lokale variabelen, locatie, taal carrier, apparaten, firmware, netwerk (Wi-Fi), versies van het Hallo-app en SDK, die wordt gebruikt door klanten. Deze informatie kan worden bekeken in realtime van Hallo monitor-sectie.

> [!NOTE]
> Hallo is periode gebaseerd op Hallo datum van de apparaatinstellingen Hallo gebruikers, zodat een gebruiker waarvan telefoon heeft Hallo datum onjuist ingestelde in Hallo verkeerde periode weergegeven kan.

* Bewaartermijn: Een gebruiker wordt beschouwd als terugkerend binnen een bepaald tijdsinterval als hij gedurende dit tijdsinterval eerste sessie heeft uitgevoerd. U kunt wijzigen Hallo tijdsintervallen waarover terugkerende gebruikers (en nieuwe gebruikers), worden geteld toohours, dagen, weken of maanden. Hallo gebruiker bewaren analytics is ingebouwd in cohorten. Een cohort is Hallo verzameling nieuwe gebruikers van alle Hallo gedetecteerd voor een bepaalde periode (dat wil zeggen, Hallo set gebruikers die hun eerste sessie tijdens deze periode uitvoeren). We gebruiken cohorten van 1 dag, 2 dagen, 4 dagen, 7 dagen of 1 maand. Gegeven een set cohort, elke dag 1, 2 dagen, 4 dagen, 7 dagen of 1 maand Azure Mobile Engagement berekent Hallo van alle gebruikers die deel uitmaken van toohello cohort en er wordt nog steeds actief (dat wil zeggen, Hallo set gebruikers die minimaal één sessie Hallo periode op wordt uitgevoerd). Deze groep gebruikers, heet een cohort-versie. (Azure Mobile Engagement kunt u zien hoeveel van uw gebruikers zijn nog steeds gebruik van uw app, maar alleen Hallo platform-specifieke archief kunt u hoeveel van uw gebruikers verwijderd uit de iTunes app - bijvoorbeeld GooglePlay, de Windows Store, enz.).
* Sessies: Een gebruik van de toepassing hello door een gebruiker. Sessies zijn gegenereerd op basis van het Hallo-volgorde van activiteiten uitgevoerd door gebruikers (een activiteit is meestal gekoppeld toohello gebruik van één scherm van de toepassing hello, maar dit kan variëren, afhankelijk van Hallo manier Hallo SDK is geïntegreerd in de toepassing hello). Een gebruiker alleen één activiteit tegelijk uitvoeren: een sessie begint zodra Hallo gebruiker de eerste activiteit Start en stopt wanneer de laatste activiteit is voltooid. Als een gebruiker meer dan een paar seconden blijft zonder dat een activiteit die u uitvoert, is de volgorde van activiteiten opgedeeld in twee verschillende sessies.
* Activiteiten: namen van elk scherm in uw toepassing hello en Hallo lengte gebruikers besteden aan elk scherm. Activiteiten zijn een aangepaste analytische optie behorend toohello 'app-info' labels die u hebt ingesteld voor uw eigen app:
* Pad naar de gebruiker: Ziet u hoe uw gebruikers navigeren door uw toepassing activiteiten (schermen). U kunt Hallo schuifregelaar tooadjust Hallo detailniveau verplaatsen. Blauwe knooppunten geven de activiteiten van uw toepassing weer. Hun grootte is proportioneel toohello gebruikers eraan besteden. Witte knooppunten geven het begin en einde van een sessie weer. Rode knooppunten geven crashes weer. Koppelingen geven de transities tussen de activiteiten van uw toepassing weer (of tussen activiteiten en crashes). Klik op een knooppunt of een koppeling toodisplay knopinfo met meer informatie over uw gegevens: Hallo tijd besteed aan een bepaald scherm Hallo aantal transities en Hallo percentage transities van Hallo activiteit toohello bestemming bronactiviteit. (Een---60%---> B betekent dat gebruikers op activiteit een gaan tooactivity B 60% Hallo tijd.) Hallo grafiek opnieuw indelen gewenste tooclarify; de positie wordt telkens opgeslagen zodra u een wijziging aanbrengt. U kunt weergeven of verbergen Hallo crashes toolighten Hallo grafiek.
* Gebeurtenissen: Specifieke acties die door een gebruiker in de toepassing hello. Hallo-distributie van gebeurtenissen wordt weergegeven als Hallo aantal gebeurtenissen per gebruiker per sessie. Een gebeurtenis geeft een directe actie, bijvoorbeeld een klik op de ontvangst van een knop of Hallo van een melding. (Hallo betekenis van gebeurtenissen is afhankelijk van hoe Hallo SDK is geïntegreerd in de toepassing hello.) Een gebeurtenis kan optreden tijdens een sessie of een taak of kan onafhankelijk zijn.
* Taken: Vergelijkbare tooevents tenzij ze zich richten op Hallo lengte van Hallo actie. Bijvoorbeeld: taken kunnen vertelt u technische informatie over hoe lang het duurt inhoud tooload of een aanroep van tooweb-service. Het kan ook hoe lang het duurt voordat een gebruiker toofill van een formulier weergeven, een account maken of kopen. Een taak Hallo duur van een taak vertegenwoordigt, voor het voorbeeld, Hallo duur van een downloadopdracht duurt of Hallo tijd een banner wordt weergegeven op het welkomstscherm. (Hallo betekenis van taken is afhankelijk van hoe Hallo SDK is geïntegreerd in de toepassing hello.) Taken worden meestal in verband gebracht met achtergrondtaken die buiten het bereik van een sessie (d.w.z. zonder gebruikersactiviteit) Hallo worden uitgevoerd.
* Technicals: Technische informatie over apparaten Hallo Hallo gebruikers van uw app, die u volgen kunt, zoals Hallo landinstellingen, Carrier, netwerk, apparaat, Firmware en scherm grootte van de apparaten van gebruikers Hallo en Hallo versie van uw App en het Hallo SDK-versie die wordt gebruikt in uw app.
* Fouten: Informatie over technische fouten in toepassing hello die geen Hallo toepassing toocrash veroorzaken. Een fout geeft een direct probleem, bijvoorbeeld een netwerkstoring of een onjuiste manipulatie. (Hallo betekenis van gebeurtenissen is afhankelijk van hoe Hallo SDK is geïntegreerd in de toepassing hello.) Een fout kan optreden tijdens een sessie of een taak of kan onafhankelijk zijn.
* Crashes: Informatie over fouten die ertoe leiden uw toepassing toocrash dat. Een crash is een onverwachte status waarbij de toepassing hello stopt de verwachte functies uitvoert en moet worden gestopt. Een crash wordt meestal vanwege fout in de toepassing hello tooa.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Toegang tot Hallo retentie-overzicht
![Analytics3][12]

Hallo bewaren overzicht is onderverdeeld in Hallo midden in meerdere kaarten, elke weergeeft Hallo-overzicht voor een bepaalde bewaartermijn. Hallo 2 dagen bewaarperiode is zichtbaar in Hallo-voorbeeld. Hallo weergeven andere kaarten Hallo 4 en 7 dagen bewaarperiode.

## <a name="understanding-hello-retention-overview-cards"></a>Understanding Hallo bewaren overzicht kaarten
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Elke kaart bestaat uit 3 hoofdonderdelen:
1. 1: Hallo cohort en Hallo periode beschouwd als
2. 2-4: Hallo bewaren voor Hallo huidige periode
3. 5: een Sparkline Hallo-geschiedenis

### <a name="here-is-detailed-information-about-each-element"></a>Hier wordt gedetailleerde informatie over elk element:
1. Cohort en periode: deze kop Hallo type cohort biedt. Hier houdt '2 dagen' in dat kijken we Hallo gedrag van gebruikers meer dan 2 dagen gebruikers dat is ontvangen gedurende een periode van 2 dagen, en of ze verbinding maken in blokken van 2 dagen na Hallo. Hallo in bovenstaand voorbeeld acht Hallo activiteit van gebruikers tussen Hallo 21 en 22 november.
2. Hiermee geeft u Hallo bewaren snelheid via Hallo 21 en 22 november voor Hallo gebruikers die binnenkomen in 19 en 20 november. Hier is 1 actieve gebruiker tussen Hallo 21 en de 22e, via Hallo 3 dat nieuwe gebruikers tussen zijn Hallo 19e en 20e.
3. Dit biedt visuele indicator hello dezelfde informatie als hierboven grafisch weergegeven. (derde Hallo Hallo cirkel van Hallo 33% getal is.) Hallo kleur bevat aanvullende informatie: groen geeft aan dit nummer van de vorige berekening Hallo groeit. Geel betekent stabiel en rood betekent verlagen.
4. Hiermee wordt aangegeven Hallo waarden voor Hallo berekening.
5. Dit is een Sparkline Hallo geschiedenis van Hallo bewaren waarden. Hiermee kunt u toosee Hallo waarden in Hallo voorbij toohave uitgebreid bekijken hoe deze ontwikkeld.

## <a name="see-also"></a>Zie ook
* [Concepten][Link 6]
* [Troubleshooting Guide-Service][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
