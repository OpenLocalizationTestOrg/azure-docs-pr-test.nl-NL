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
# <a name="sql-database-threat-detection"></a><span data-ttu-id="8cf3b-103">Detectie van dreigingen van SQL Database</span><span class="sxs-lookup"><span data-stu-id="8cf3b-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="8cf3b-104">Detectie van dreigingen SQL detecteert afwijkende activiteiten ongebruikelijke en potentieel schadelijke aanvallen tooaccess of misbruik databases waarmee wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="8cf3b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8cf3b-105">Overview</span></span>

<span data-ttu-id="8cf3b-106">Detectie van dreigingen SQL biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="8cf3b-107">Gebruikers ontvangt een waarschuwing bij verdachte databaseactiviteiten, mogelijke beveiligingsproblemen en SQL-injectieaanvallen, evenals database afwijkende toegangspatronen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="8cf3b-108">Detectie van dreigingen SQL waarschuwingen Geef details op van de verdachte activiteit en actie voor het beste tooinvestigate en Hallo bedreigingen te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="8cf3b-109">Gebruikers kunnen verkennen Hallo verdachte gebeurtenissen met [SQL Database Auditing](sql-database-auditing.md) toodetermine als ze het gevolg zijn van een tooaccess poging schenden of misbruik van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="8cf3b-110">Detectie van dreigingen maakt het eenvoudig tooaddress potentiële bedreigingen toohello database zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="8cf3b-111">SQL-injectie is bijvoorbeeld een Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="8cf3b-112">Aanvallers profiteren van toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing, schendingen veroorzaken of wijzigen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="8cf3b-113">Detectie van dreigingen SQL integreert waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), en elke beveiligde SQL Database-server wordt gefactureerd op dezelfde prijs Hallo als Azure Security Center Standard-laag op $15/knooppunt/maand, waar elke SQL beveiligd Database-server worden geteld als één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="8cf3b-114">We nodigen u tootry uit 60 dagen gratis.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="8cf3b-115">Detectie van dreigingen voor uw database in hello Azure-portal instellen</span><span class="sxs-lookup"><span data-stu-id="8cf3b-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="8cf3b-116">Start hello Azure portal op [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8cf3b-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8cf3b-117">Navigeer toohello configuratie blade Hallo gewenste toomonitor SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="8cf3b-118">Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="8cf3b-119">![Navigatiedeelvenster][1]</span><span class="sxs-lookup"><span data-stu-id="8cf3b-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="8cf3b-120">In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle die Hallo threat detectie-instellingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="8cf3b-122">Schakel **ON** Bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="8cf3b-123">Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="8cf3b-124">Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** blade toosave Hallo nieuwe of bijgewerkte controle en threat detectie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Navigatiedeelvenster][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="8cf3b-126">Detectie van dreigingen met behulp van PowerShell instellen</span><span class="sxs-lookup"><span data-stu-id="8cf3b-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="8cf3b-127">Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8cf3b-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="8cf3b-128">Verken afwijkende databaseactiviteiten na detectie van een verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="8cf3b-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="8cf3b-129">U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="8cf3b-130">Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, servernaam, toepassingsnaam en Hallo gebeurtenistijd inclusief.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="8cf3b-131">Bovendien Hallo e bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Navigatiedeelvenster][4]
2. <span data-ttu-id="8cf3b-133">Hallo e-mailmelding bevat een directe koppeling toohello SQL controlelogboek.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="8cf3b-134">Klikken op deze koppeling wordt gestart hello Azure portal en wordt geopend Hallo SQL controlerecords rond de tijd Hallo van verdachte Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="8cf3b-135">Klik op een audit record tooview meer informatie over Hallo verdachte activiteiten met een database, waardoor het gemakkelijker toofind Hallo SQL-instructies die zijn uitgevoerd (die toegankelijk zijn, wat ze hebben gedaan en wanneer) en bepalen of Hallo gebeurtenis legitieme of schadelijke was (bijvoorbeeld een toepassing beveiligingslek tooSQL injectie misbruik wordt gemaakt, iemand geschonden gevoelige gegevens, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="8cf3b-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="8cf3b-136">
   ![Navigatiedeelvenster][5]</span><span class="sxs-lookup"><span data-stu-id="8cf3b-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="8cf3b-137">Dagelijks geconstateerde waarschuwingen voor uw database in Azure-portal Hallo verkennen</span><span class="sxs-lookup"><span data-stu-id="8cf3b-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="8cf3b-138">Detectie van SQL Database dreigingen integreert de waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="8cf3b-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="8cf3b-139">Een live SQL beveiligingstegel binnen de databaseblade Hallo hello Azure portal houdt Hallo status van actieve bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Navigatiedeelvenster][6]
   
1. <span data-ttu-id="8cf3b-141">Te klikken op Hallo SQL beveiligingstegel hello Azure Security Center waarschuwingen-blade opent en biedt een overzicht van actieve SQL bedreigingen op Hallo database gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Navigatiedeelvenster][7]

2. <span data-ttu-id="8cf3b-143">Te klikken op een specifieke waarschuwing biedt aanvullende informatie en acties voor deze bedreiging onderzoeken en oplossen van problemen met toekomstige bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="8cf3b-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Navigatiedeelvenster][8]


## <a name="next-steps"></a><span data-ttu-id="8cf3b-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8cf3b-145">Next steps</span></span>

* <span data-ttu-id="8cf3b-146">Meer informatie over detectie van dreigingen, gaat u naar Hallo [Azure-blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="8cf3b-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="8cf3b-147">Meer informatie over [Azure SQL Database Auditing](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="8cf3b-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="8cf3b-148">Meer informatie over [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="8cf3b-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="8cf3b-149">Zie voor meer informatie over prijzen Hallo [pagina met prijzen van SQL-Database](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="8cf3b-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="8cf3b-150">Zie voor een voorbeeld van de PowerShell-script, [controle en detectie van bedreigingen met behulp van PowerShell configureren](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8cf3b-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


