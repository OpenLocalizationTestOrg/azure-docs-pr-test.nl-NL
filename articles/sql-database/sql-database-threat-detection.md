---
title: aaaThreat detectie - Azure SQL Database | Microsoft Docs
description: Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met.
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>Detectie van dreigingen van SQL Database

Detectie van dreigingen SQL detecteert afwijkende activiteiten ongebruikelijke en potentieel schadelijke aanvallen tooaccess of misbruik databases waarmee wordt aangegeven.

## <a name="overview"></a>Overzicht

Detectie van dreigingen SQL biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.  Gebruikers ontvangt een waarschuwing bij verdachte databaseactiviteiten, mogelijke beveiligingsproblemen en SQL-injectieaanvallen, evenals database afwijkende toegangspatronen. Detectie van dreigingen SQL waarschuwingen Geef details op van de verdachte activiteit en actie voor het beste tooinvestigate en Hallo bedreigingen te verhelpen. Gebruikers kunnen verkennen Hallo verdachte gebeurtenissen met [SQL Database Auditing](sql-database-auditing.md) toodetermine als ze het gevolg zijn van een tooaccess poging schenden of misbruik van gegevens in Hallo-database. Detectie van dreigingen maakt het eenvoudig tooaddress potentiële bedreigingen toohello database zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.

SQL-injectie is bijvoorbeeld een Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen. Aanvallers profiteren van toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing, schendingen veroorzaken of wijzigen van gegevens in Hallo-database.

Detectie van dreigingen SQL integreert waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), en elke beveiligde SQL Database-server wordt gefactureerd op dezelfde prijs Hallo als Azure Security Center Standard-laag op $15/knooppunt/maand, waar elke SQL beveiligd Database-server worden geteld als één knooppunt. We nodigen u tootry uit 60 dagen gratis. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Detectie van dreigingen voor uw database in hello Azure-portal instellen
1. Start hello Azure portal op [https://portal.azure.com](https://portal.azure.com).
2. Navigeer toohello configuratie blade Hallo gewenste toomonitor SQL-Database. Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**. 
    ![Navigatiedeelvenster][1]
3. In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle die Hallo threat detectie-instellingen worden weergegeven.
  
    ![Navigatiedeelvenster][2]
4. Schakel **ON** Bedreigingendetectie.
5. Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.
6. Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** blade toosave Hallo nieuwe of bijgewerkte controle en threat detectie-instellingen.
       
    ![Navigatiedeelvenster][3]

## <a name="set-up-threat-detection-using-powershell"></a>Detectie van dreigingen met behulp van PowerShell instellen

Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Verken afwijkende databaseactiviteiten na detectie van een verdachte activiteit
1. U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten. <br/>
   Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, servernaam, toepassingsnaam en Hallo gebeurtenistijd inclusief. Bovendien Hallo e bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken.<br/>
     
    ![Navigatiedeelvenster][4]
2. Hallo e-mailmelding bevat een directe koppeling toohello SQL controlelogboek. Klikken op deze koppeling wordt gestart hello Azure portal en wordt geopend Hallo SQL controlerecords rond de tijd Hallo van verdachte Hallo-gebeurtenis. Klik op een audit record tooview meer informatie over Hallo verdachte activiteiten met een database, waardoor het gemakkelijker toofind Hallo SQL-instructies die zijn uitgevoerd (die toegankelijk zijn, wat ze hebben gedaan en wanneer) en bepalen of Hallo gebeurtenis legitieme of schadelijke was (bijvoorbeeld een toepassing beveiligingslek tooSQL injectie misbruik wordt gemaakt, iemand geschonden gevoelige gegevens, enzovoort).<br/>
   ![Navigatiedeelvenster][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Dagelijks geconstateerde waarschuwingen voor uw database in Azure-portal Hallo verkennen

Detectie van SQL Database dreigingen integreert de waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/). Een live SQL beveiligingstegel binnen de databaseblade Hallo hello Azure portal houdt Hallo status van actieve bedreigingen. 

   ![Navigatiedeelvenster][6]
   
1. Te klikken op Hallo SQL beveiligingstegel hello Azure Security Center waarschuwingen-blade opent en biedt een overzicht van actieve SQL bedreigingen op Hallo database gedetecteerd. 

  ![Navigatiedeelvenster][7]

2. Te klikken op een specifieke waarschuwing biedt aanvullende informatie en acties voor deze bedreiging onderzoeken en oplossen van problemen met toekomstige bedreigingen.

  ![Navigatiedeelvenster][8]


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over detectie van dreigingen, gaat u naar Hallo [Azure-blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Meer informatie over [Azure SQL Database Auditing](sql-database-auditing.md)
* Meer informatie over [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Zie voor meer informatie over prijzen Hallo [pagina met prijzen van SQL-Database](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Zie voor een voorbeeld van de PowerShell-script, [controle en detectie van bedreigingen met behulp van PowerShell configureren](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


