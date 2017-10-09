---
title: aaaAzure CDN realtime-waarschuwingen | Microsoft Docs
description: Realtime-waarschuwingen in Microsoft Azure CDN. Realtime waarschuwingen bevatten meldingen over de prestaties van Hallo van Hallo-eindpunten in uw CDN-profiel.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Realtime-waarschuwingen in Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overzicht
Dit document wordt uitgelegd in Microsoft Azure CDN realtime-waarschuwingen. Deze functionaliteit biedt realtime meldingen over de prestaties van Hallo van Hallo-eindpunten in uw CDN-profiel.  U kunt e-mailadres of op basis van HTTP-waarschuwingen instellen:

* Bandbreedte
* Statuscodes
* Cache-statussen
* Verbindingen

## <a name="creating-a-real-time-alert"></a>Maken van een realtime waarschuwing
1. In Hallo [Azure Portal](https://portal.azure.com), bladeren tooyour CDN-profiel.
   
    ![Blade CDN-profiel](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
3. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **realtime statistieken** doel.  Klik op **realtime-waarschuwingen**.
   
    ![CDN-beheerportal](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    Hallo-lijst met bestaande waarschuwing configuraties (indien aanwezig) wordt weergegeven.
4. Klik op Hallo **waarschuwing toevoegen** knop.
   
    ![Knop Waarschuwing toevoegen](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Een formulier voor het maken van een nieuwe waarschuwing wordt weergegeven.
   
    ![Nieuwe waarschuwing formulier](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Als u wilt dat deze waarschuwing toobe active wanneer u klikt op **opslaan**, Controleer Hallo **waarschuwing ingeschakeld** selectievakje.
6. Voer een beschrijvende naam voor de waarschuwing in Hallo **naam** veld.
7. In Hallo **mediatype** vervolgkeuzelijst **HTTP Large Object**.
   
    ![Het mediatype met HTTP-Large Object geselecteerd](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > U moet selecteren **HTTP Large Object** als Hallo **mediatype**.  Hallo andere opties worden niet gebruikt door **Azure CDN van Verizon**.  Fout tooselect **HTTP Large Object** , wordt de waarschuwing toonever worden geactiveerd.
   > 
   > 
8. Maakt een **expressie** toomonitor door het selecteren van een **metriek**, **Operator**, en **activeren waarde**.
   
   * Voor **metriek**, Hallo type bewaakte gewenste voorwaarde selecteren.  **Mbps bandbreedte** is Hallo hoeveelheid bandbreedtegebruik in megabits per seconde.  **Totaal aantal verbindingen** is het aantal gelijktijdige HTTP-verbindingen tooour Hallo edge-servers.  Zie voor definities van Hallo verschillende cache statussen en statuscodes, [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx) en [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Operator** Hallo rekenkundige operator die zorgt voor de relatie tussen Hallo metriek en Hallo trigger waarde Hallo is.
   * **Activeren van de waarde** is Hallo drempelwaarde in die moet worden voldaan voordat een melding wordt verzonden uit.
     
     Hallo onderstaand voorbeeld wijst Hallo expressie die ik heb gemaakt dat ik wil een melding krijgen wanneer Hallo 404 statuscodes aantal groter dan 25 is toobe.
     
     ![Realtime waarschuwing voorbeeldexpressie](./media/cdn-real-time-alerts/cdn-expression.png)
9. Voor **Interval**, opgeven hoe vaak u graag Hallo expressie, geëvalueerd.
10. In Hallo **meldingen op basis van** vervolgkeuzelijst, selecteer deze optie als u wilt toobe een melding krijgen wanneer hello expressie waar is.
    
    * **Start-voorwaarde** geeft aan dat een melding wordt verzonden wanneer Hallo opgegeven voorwaarde voor het eerst wordt gedetecteerd.
    * **End-voorwaarde** geeft aan dat een melding wordt verzonden wanneer Hallo opgegeven voorwaarde wordt niet meer gedetecteerd. Deze melding kan alleen worden geactiveerd nadat ons netwerk bewakingssysteem gedetecteerd die Hallo opgegeven veroorzaakt.
    * **Continue** geeft aan dat een melding wordt verzonden elke keer dat netwerk bewakingssysteem Hallo detecteert Hallo opgegeven voorwaarde. Houd er rekening mee dat Hallo netwerk bewaking van systeem wordt alleen controle eenmaal per interval voor Hallo voorwaarde opgegeven.
    * **Voorwaarde begin- en** geeft aan dat een melding wordt verzonden hello eerste keer is dat Hallo opgegeven voorwaarde wordt gedetecteerd en nog een keer wanneer Hallo voorwaarde wordt niet meer gedetecteerd.
11. Als u wilt dat tooreceive meldingen via e-mail, controleert u Hallo **melden via E-mail** selectievakje.  
    
    ![Delen per E-mail formulier](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    In Hallo **naar** Voer Hallo e-mailadres u waar u meldingen verzonden. Voor **onderwerp** en **hoofdtekst**, u Hallo standaard laten of kunt u aanpassen op het Hallo-bericht met Hallo **beschikbare trefwoorden** lijst toodynamically invoegen waarschuwingsgegevens wanneer Hallo-bericht is verzonden.
    
    > [!NOTE]
    > U kunt e-mailmelding Hallo testen door te klikken op Hallo **testen melding** knop, maar alleen als Hallo configuratie van de waarschuwing is opgeslagen.
    > 
    > 
12. Als u wilt dat meldingen toobe geboekt tooa webserver, controleert u Hallo **hoogte door HTTP Post** selectievakje.
    
    ![Melden door HTTP Post-formulier](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    In Hallo **Url** Voer Hallo-URL die u waar u het Hallo HTTP-bericht verzonden. In Hallo **Headers** textbox Voer Hallo HTTP-headers toobe in Hallo-aanvraag verzonden.  Voor **hoofdtekst** kunt u aanpassen op het Hallo-bericht met Hallo **beschikbare trefwoorden** lijst toodynamically invoegen waarschuwingsgegevens wanneer het Hallo-bericht wordt verzonden.  **Headers** en **hoofdtekst** standaard tooan XML-nettolading vergelijkbare toohello onderstaand voorbeeld.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > U kunt Hallo HTTP Post-melding testen door te klikken op Hallo **testen melding** knop, maar alleen als Hallo configuratie van de waarschuwing is opgeslagen.
    > 
    > 
13. Klik op Hallo **opslaan** knop toosave uw configuratie van de waarschuwing.  Als u dit selectievakje inschakelt **waarschuwing ingeschakeld** in stap 5, de waarschuwing is nu actief.

## <a name="next-steps"></a>Volgende stappen
* Analyseren [realtime statistieken in Azure CDN](cdn-real-time-stats.md)
* Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)
* Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)

