---
title: statistieken aaaReal tijd in Azure CDN | Microsoft Docs
description: Realtime statistieken biedt realtime-gegevens over de prestaties van Azure CDN Hallo wanneer inhoud tooyour clients leveren.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Realtime statistieken in Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overzicht
Dit document wordt uitgelegd realtime statistieken in Microsoft Azure CDN.  Deze functionaliteit biedt realtime gegevens, zoals bandbreedte, cache statussen en gelijktijdige verbindingen tooyour CDN-profiel voor het leveren van inhoud tooyour clients. Hierdoor kan de doorlopende bewaking van Hallo status van uw service op elk gewenst moment, waaronder Ga live gebeurtenissen.

Hallo na grafieken zijn beschikbaar:

* [Bandbreedte](#bandwidth)
* [Statuscodes](#status-codes)
* [Cache-statussen](#cache-statuses)
* [Verbindingen](#connections)

## <a name="accessing-real-time-stats"></a>Toegang tot realtime statistieken
1. In Hallo [Azure Portal](https://portal.azure.com), bladeren tooyour CDN-profiel.
   
    ![Blade CDN-profiel](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
3. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **realtime statistieken** doel.  Klik op **HTTP Large Object**.
   
    ![CDN-beheerportal](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    Hallo realtime statistieken grafieken worden weergegeven.

Elk van de grafieken Hallo realtime geeft statistieken weer voor de tijdsspanne Hallo geselecteerd, wordt gestart wanneer het Hallo-pagina wordt geladen.  Hallo grafieken automatisch bijgewerkt om de paar seconden.  Hallo **grafiek vernieuwen** knop, indien aanwezig, wordt gewist Hallo grafiek, waarna deze alleen Hallo geselecteerd gegevens weergegeven.

## <a name="bandwidth"></a>Bandbreedte
![Bandbreedte-grafiek](./media/cdn-real-time-stats/cdn-bandwidth.png)

Hallo **bandbreedte** diagram toont de Hallo en de hoeveelheid bandbreedte die wordt gebruikt voor het huidige platform Hallo via tijdsspanne Hallo geselecteerd. Hallo gearceerde gedeelte van de grafiek Hallo geeft bandbreedtegebruik. Hallo exacte hoeveelheid bandbreedte die momenteel wordt gebruikt wordt direct onder Hallo lijndiagram weergegeven.

## <a name="status-codes"></a>Statuscodes
![Status code grafiek](./media/cdn-real-time-stats/cdn-status-codes.png)

Hallo **statuscodes** grafiek geeft aan hoe vaak bepaalde HTTP-antwoordcodes via Hallo geselecteerd tijdsspanne plaatsvinden.

> [!TIP]
> Zie voor een beschrijving van elke optie voor HTTP-status code [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx).
> 
> 

Een lijst met HTTP-statuscodes wordt direct boven Hallo grafiek weergegeven. Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in een lijndiagram Hallo en Hallo kunt u het huidige aantal exemplaren per seconde voor deze statuscode. Standaard wordt een regel voor elk van deze statuscodes in Hallo grafiek weergegeven. U kunt echter tooonly monitor Hallo statuscodes waarvoor speciale betekenis voor uw CDN-configuratie. toodo dit gewenst Hallo statuscodes controleren en wis alle andere opties en klik vervolgens op **grafiek vernieuwen**. 

U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.  Klik Hallo statuscode gewenste toohide Hallo legenda direct onder het Hallo-grafiek. Hallo grafiek verborgen onmiddellijk Hallo-statuscode. Die statuscode opnieuw te klikken, wordt die optie toobe opnieuw weergegeven.

## <a name="cache-statuses"></a>Cache-statussen
![Cache statussen grafiek](./media/cdn-real-time-stats/cdn-cache-status.png)

Hallo **Cache statussen** grafiek geeft aan hoe vaak bepaalde typen statussen van de cache via Hallo geselecteerd tijdsspanne plaatsvinden. 

> [!TIP]
> Zie voor een beschrijving van elke optie cache status code [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx).
> 
> 

Een lijst met de statuscodes cache wordt direct boven Hallo grafiek weergegeven. Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in een lijndiagram Hallo en Hallo kunt u het huidige aantal exemplaren per seconde voor deze statuscode. Standaard wordt een regel voor elk van deze statuscodes in Hallo grafiek weergegeven. U kunt echter tooonly monitor Hallo statuscodes waarvoor speciale betekenis voor uw CDN-configuratie. toodo dit gewenst Hallo statuscodes controleren en wis alle andere opties en klik vervolgens op **grafiek vernieuwen**. 

U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.  Klik Hallo statuscode gewenste toohide Hallo legenda direct onder het Hallo-grafiek. Hallo grafiek verborgen onmiddellijk Hallo-statuscode. Die statuscode opnieuw te klikken, wordt die optie toobe opnieuw weergegeven.

## <a name="connections"></a>Verbindingen
![Verbindingen grafiek](./media/cdn-real-time-stats/cdn-connections.png)

Deze grafiek geeft aan hoeveel verbindingen tot stand gebrachte tooyour randservers zijn. Elke aanvraag voor een asset die wordt doorgegeven via onze CDN resulteert in een verbinding.

## <a name="next-steps"></a>Volgende stappen
* Blijf op de hoogte met [realtime waarschuwingen in Azure CDN](cdn-real-time-alerts.md)
* Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)
* Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)

