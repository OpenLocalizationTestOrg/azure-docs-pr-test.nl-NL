---
title: aaaGet inzicht in Azure Security Center-gegevens met Power BI | Microsoft Docs
description: Hello Azure Security Center Power BI-inhoudspakket maakt het eenvoudig toofind beveiligingswaarschuwingen, aanbevelingen, aangevallen resources en trends, op basis van een gegevensset die is gemaakt voor uw rapportage.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Inzichten verkrijgen van Azure Security Center-gegevens met Power BI
Hallo [Power BI-Dashboard](http://aka.ms/azure-security-center-power-bi) voor Azure Security Center u toovisualize kunt, analyseren en filteren van aanbevelingen en beveiligingswaarschuwingen vanaf elke locatie, inclusief uw mobiele apparaat. Gebruik Hallo Power BI-dashboard tooreveal trends en aanvalspatronen - Bekijk beveiligingswaarschuwingen op resource of IP-bronadres en niet-opgeloste beveiligingsrisico's op resource of ouderdom.

U kunt ook adviezen van het Security Center en beveiligingswaarschuwingen met andere data op interessante manieren combineren, bijvoorbeeld om data van [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) en [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/) te gebruiken. Beide Power BI-Dashboards bieden, en kunt u deze gegevens tooExcel voor eenvoudige rapportage over Hallo beveiligingsstatus van uw cloudresources exporteren.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Met behulp van Azure Security Center-dashboard tooaccess Power BI
U kunt ook hello Azure Security Center-dashboard tooaccess Power BI-rapporten gebruiken. Ga als volgt Hallo stappen tooperform deze taak:

1. In Hallo **Azure Security Center** dashboard, klikt u op **Power BI** knop.

    ![Verbinding maken met tooAzure Security Center via Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Hallo **Power BI** blade wordt geopend aan de rechterkant Hallo zoals weergegeven in het volgende scherm Hallo:

    ![Verbinding maken met tooAzure Security Center via Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Als u Power BI-dashboard voor Hallo Hallo eerst maakt, kunt u een van de volgende Hallo opties in Hallo **verkennen in Power BI** blade:

   * **Dashboard voor beveiligingsinzichten**: Selecteer deze optie als u wilt dat toocreate een dashboard dat beveiligingsstatus, threads en detecties bevat. Dit is een meer algemene optie voor personen met de DevOps-rol die verantwoordelijk zijn voor het analyseren van de beveiligingsstatus en gedetecteerde waarschuwingen voor alle abonnementen.
   * **Policy management dashboard**: Kies deze optie als u beleid voor het beheer en afdwinging van tooexplore.  Dit is een meer algemene optie voor de centrale IT-afdeling die meer gericht is op governance. Ze kunnen dit dashboard toogain zichtbaarheid en inzichten beveiligingsbeleid gebruiken in hun organisatie.
   * Als u al een Power BI-dashboard hebt, klikt u op **Ga tooyour huidige Power BI-dashboard**.
4. Klik voor dit voorbeeld op de optie **Beveiligingsinzichten dashboard**. Als dit Hallo eerst, maakt u een Power BI-dashboard voor het Beveiligingscentrum u worden gevraagd tooinstall Hallo-inhoudspakket. Klik op **ophalen** knop in Hallo **packs inhoud voor Power BI** venster zoals weergegeven in het volgende scherm Hallo:

    ![Dashboard voor beveiligingsinzichten van Azure Security Center](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Hallo **tooAzure Security Center Security Insights verbinding** venster weergegeven. Zorg ervoor dat Hallo **verificatie** methode is **oAuth2** zoals hieronder wordt weergegeven en klik op **aanmelden** knop.

    ![Authentication](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. U wordt mogelijk gevraagd tooauthenticate opnieuw met uw Azure-referenties. Na verificatie wordt uw dashboard gemaakt. Zodra Hallo dashboard is gemaakt ziet u een rapport met vergelijkbare Hallo-structuur, zoals weergegeven in het volgende scherm Hallo:

    ![Power BI Dashboard](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Een vernieuwing van het Hallo-rapport is de plaats geplande tootake dagelijks. Als er een fout bij het vernieuwen, lezen [potentiële problemen met vernieuwen Hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), voor meer informatie over het tootroubleshoot.
>
>

Hier ziet u Hallo aantal beveiligingswaarschuwingen en aanbevelingen, evenals Hallo aantal VM's, Azure SQL-databases en netwerkresources die worden bewaakt door Azure Security Center.

Een koppeling tooAzure Security Center wordt omgeleid toohello Azure-portal. Hallo grafieken maken het gemakkelijk toovisualize informatie over beveiligingsaanbevelingen en waarschuwingen, waaronder:

* Beveiligingsstatus van de resource
* In behandeling zijnde aanbevelingen
* VM Recommendations (Aanbevelingen voor VM's)
* Waarschuwingen gedurende een periode
* Aangevallen resources
* Aangevallen IP-adressen

Achter elke grafiek wordt meer inzicht geboden. Selecteer een tegel toosee meer informatie. Bijvoorbeeld, Hallo **Resource beveiligingsstatus** tegel ziet u aanvullende details over in behandeling zijnde aanbevelingen op resources zoals weergegeven in het volgende scherm Hallo:

![Aanbevelingen](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Als u op elke regel van deze grafiek klikt, gaat hello anderen toogray uit en u richten u alleen op Hallo die één u hebt geselecteerd. tooreturn toohello dashboard, klikt u op **Azure Security Center** onder Hallo **Dashboards** optie in het linkerdeelvenster Hallo aan deze pagina.

> [!NOTE]
> Als u toocustomize wilt uw rapporten door extra velden toe te voegen of bestaande visuele elementen te wijzigen, kunt u Hallo rapport bewerken. Zie [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) (Met een rapport in de bewerkingsweergave in Power BI werken) voor meer informatie.
>
>

Hallo **waarschuwingen gedurende een periode, aangevallen Resources** en **aanvaller IP-adressen** tegels hebben Hallo vergelijkbare uitvoer wanneer u op de tegels klikt. Dit gebeurt omdat Hallo rapport informatie met betrekking tot deze drie variabelen samenvoegt en deze **Resources aangevallen** zoals weergegeven in het volgende scherm Hallo:

![Resources die worden aangevallen](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

Op dit moment u kunt ook een kopie van dit rapport opslaan, afdrukken of publiceren op web Hallo Hallo beschikbare opties in Hallo met **bestand** menu.

![Menu Bestand](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Uw Azure Security Center-gegevens verkennen met Power BI-services
Verbinding maken met toohello [Power BI-Inhoudspakketservices](https://msit.powerbi.com/groups/me/getdata/services) in Power BI en Hallo stappen uitvoeren:

1. In Hallo **inhoudspakket voor Power BI** venster ziet u twee opties zoals hieronder wordt weergegeven.

    ![Inhoudspakket voor Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Als al uitgevoerd Hallo eerste deel van dit artikel ziet u slechts één optie, die Azure Security Center-beleidsbeheer is.
   >
   >
2. Hallo-doel van dit voorbeeld, klikt u op **ophalen** in Hallo **Azure Security Center-beleidsbeheer** tegel.
3. In Hallo **tooAzure Security Center-beleidsbeheer verbinding** venster, zorg ervoor dat tooselect **oAuth2** onder **verificatiemethode** vervolgkeuzelijst zoals hieronder wordt weergegeven en klik op **Aanmelden** knop.

    ![Venster Beleidsbeheer](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. U zult omgeleid tooan verificatiepagina waar u dat u van tooconnect tooAzure Security Center gebruikmaakt Hallo-referenties moet invoeren. Nadat het verificatieproces Hallo voltooid is, wordt Power BI gestart voor het importeren van gegevens toobuild uw rapporten. Gedurende deze tijd ziet u Hallo volgende bericht op Hallo rechterhoek van uw browser:

    ![Verbinding maken met tooAzure Security Center via Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Wanneer Hallo dashboard wordt gemaakt voor Hallo eerst duurt het langer dan normaal, hoofdzakelijk voor scenario's waarin u meerdere abonnementen hebt.
   >
   >
5. Zodra het Hallo-proces is voltooid, uw Azure Security Center Power BI-dashboard laadt Hello **beleidsbeheer** rapporteren vergelijkbare toohello voorbeeld hieronder:

    ![Dashboard Beleidsbeheer](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe toouse Power BI in Azure Security Center. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Azure Security Center Planning- en Bedieningsgids](security-center-planning-and-operations-guide.md) : meer informatie hoe tooplan overstap op Azure Security Center.
* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsinstellingen in Azure Security Center
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure
