---
title: Bedreigingendetectie - Azure SQL Database | Microsoft Docs
description: Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op beveiligingsdreigingen voor de database.
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="089a3-103">Detectie van dreigingen van SQL Database</span><span class="sxs-lookup"><span data-stu-id="089a3-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="089a3-104">Detectie van dreigingen SQL detecteert afwijkende activiteiten die ongebruikelijke en potentieel schadelijke probeert te openen of misbruik van databases aangeeft.</span><span class="sxs-lookup"><span data-stu-id="089a3-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="089a3-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="089a3-105">Overview</span></span>

<span data-ttu-id="089a3-106">Detectie van dreigingen SQL biedt een nieuwe laag van beveiliging, waarmee klanten om te detecteren en op mogelijke bedreigingen reageert wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="089a3-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="089a3-107">Gebruikers ontvangt een waarschuwing bij verdachte databaseactiviteiten, mogelijke beveiligingsproblemen en SQL-injectieaanvallen, evenals database afwijkende toegangspatronen.</span><span class="sxs-lookup"><span data-stu-id="089a3-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="089a3-108">Detectie van dreigingen SQL waarschuwingen Geef details op van de verdachte activiteit en actie voor het onderzoeken en het risico dat het beste.</span><span class="sxs-lookup"><span data-stu-id="089a3-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="089a3-109">Gebruikers kunnen de verdachte gebeurtenissen met verkennen [SQL Database Auditing](sql-database-auditing.md) om te bepalen of ze het gevolg zijn van een poging om te openen, inbreuk of misbruik van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="089a3-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="089a3-110">Detectie van dreigingen kunt u eenvoudig op mogelijke bedreigingen adres met de database hoeft te worden van een deskundige beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="089a3-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="089a3-111">SQL-injectie is bijvoorbeeld een van de algemene Web application beveiligingsproblemen op het Internet worden gebruikt voor aanvallen op gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="089a3-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="089a3-112">Aanvallers te profiteren van de toepassing zwakke plekken in het injecteren schadelijke SQL-instructies in de toepassing invoervelden, schendingen veroorzaken of wijzigen van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="089a3-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="089a3-113">Detectie van dreigingen SQL integreert waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), en elke beveiligde SQL Database-server wordt gefactureerd op dezelfde prijs als Azure Security Center Standard-laag op $15/knooppunt/maand, waar elke SQL beveiligd Database-server worden geteld als één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="089a3-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="089a3-114">U wordt van harte uitgenodigd deze gedurende 60 dagen gratis te proberen.</span><span class="sxs-lookup"><span data-stu-id="089a3-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="089a3-115">Detectie van dreigingen voor uw database in de Azure portal instellen</span><span class="sxs-lookup"><span data-stu-id="089a3-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="089a3-116">Starten van de Azure portal op [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="089a3-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="089a3-117">Navigeer naar de blade van de configuratie van de SQL-Database die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="089a3-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="089a3-118">Selecteer in de blade instellingen **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="089a3-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="089a3-119">![Navigatiedeelvenster][1]</span><span class="sxs-lookup"><span data-stu-id="089a3-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="089a3-120">In de **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, waarin de threat detectie-instellingen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="089a3-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="089a3-122">Schakel **ON** Bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="089a3-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="089a3-123">Configureer de lijst met e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="089a3-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="089a3-124">Klik op **opslaan** in de **controle en detectie van bedreigingen** blade nieuwe of bijgewerkte controle- en threat detectie-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="089a3-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![Navigatiedeelvenster][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="089a3-126">Detectie van dreigingen met behulp van PowerShell instellen</span><span class="sxs-lookup"><span data-stu-id="089a3-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="089a3-127">Zie voor een scriptvoorbeeld van een, [configureren van controle en detectie van bedreigingen met behulp van PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="089a3-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="089a3-128">Verken afwijkende databaseactiviteiten na detectie van een verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="089a3-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="089a3-129">U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="089a3-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="089a3-130">Het e-mailadres bevatten informatie over de verdachte-gebeurtenis met inbegrip van de aard van de afwijkende activiteiten, databasenaam, servernaam, toepassingsnaam en de tijd van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="089a3-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="089a3-131">Bovendien wordt het e-mailbericht bevatten informatie over mogelijke oorzaken en aanbevolen acties te onderzoeken en de mogelijke bedreiging voor de database te verkleinen.</span><span class="sxs-lookup"><span data-stu-id="089a3-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![Navigatiedeelvenster][4]
2. <span data-ttu-id="089a3-133">De e-mailmelding bevat een directe koppeling naar het SQL-logboek.</span><span class="sxs-lookup"><span data-stu-id="089a3-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="089a3-134">Op deze koppeling te klikken, start de Azure-portal en Hiermee opent u de SQL-controlerecords rond de tijd van de verdachte activiteit.</span><span class="sxs-lookup"><span data-stu-id="089a3-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="089a3-135">Klik op een controlerecord meer details weergeven over de verdachte databaseactiviteiten, waardoor het gemakkelijker vinden van de SQL-instructies die zijn uitgevoerd (die toegankelijk zijn, wat ze hebben gedaan en wanneer) en bepalen of de gebeurtenis legitieme of schadelijke is (bijvoorbeeld een toepassing kwetsbaarheid voor SQL-injectie misbruik wordt gemaakt, iemand geschonden gevoelige gegevens, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="089a3-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="089a3-136">
   ![Navigatiedeelvenster][5]</span><span class="sxs-lookup"><span data-stu-id="089a3-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="089a3-137">Verken dagelijks geconstateerde waarschuwingen voor uw database in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="089a3-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="089a3-138">Detectie van SQL Database dreigingen integreert de waarschuwingen met [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="089a3-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="089a3-139">Een live SQL beveiligingstegel binnen de databaseblade in de Azure portal houdt de status van actieve bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="089a3-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![Navigatiedeelvenster][6]
   
1. <span data-ttu-id="089a3-141">Beveiligingstegel te klikken op de SQL wordt gestart van de waarschuwingen-blade van Azure Security Center en biedt een overzicht van actieve SQL bedreigingen die zijn gedetecteerd op de database.</span><span class="sxs-lookup"><span data-stu-id="089a3-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![Navigatiedeelvenster][7]

2. <span data-ttu-id="089a3-143">Te klikken op een specifieke waarschuwing biedt aanvullende informatie en acties voor deze bedreiging onderzoeken en oplossen van problemen met toekomstige bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="089a3-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Navigatiedeelvenster][8]


## <a name="next-steps"></a><span data-ttu-id="089a3-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="089a3-145">Next steps</span></span>

* <span data-ttu-id="089a3-146">Meer informatie over detectie van dreigingen, gaat u naar de [Azure-blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="089a3-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="089a3-147">Meer informatie over [Azure SQL Database Auditing](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="089a3-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="089a3-148">Meer informatie over [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="089a3-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="089a3-149">Zie voor meer informatie over prijzen de [pagina met prijzen van SQL-Database](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="089a3-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="089a3-150">Zie voor een voorbeeld van de PowerShell-script, [controle en detectie van bedreigingen met behulp van PowerShell configureren](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="089a3-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


