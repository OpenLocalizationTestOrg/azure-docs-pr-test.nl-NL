---
title: Aan de slag met SQL Data Warehouse met detectie van dreigingen
description: Hoe u aan de slag met detectie van dreigingen
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="06c11-103">Aan de slag met detectie van dreigingen</span><span class="sxs-lookup"><span data-stu-id="06c11-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06c11-104">Controle</span><span class="sxs-lookup"><span data-stu-id="06c11-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="06c11-105">Detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="06c11-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="06c11-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="06c11-106">Overview</span></span>
<span data-ttu-id="06c11-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op beveiligingsdreigingen voor de database.</span><span class="sxs-lookup"><span data-stu-id="06c11-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="06c11-108">Detectie van dreigingen is Preview-versie en wordt ondersteund voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06c11-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="06c11-109">Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarmee klanten om te detecteren en op mogelijke bedreigingen reageert wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="06c11-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="06c11-110">Gebruikers kunnen de verdachte gebeurtenissen met verkennen [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) om te bepalen of ze het gevolg zijn van een poging om te openen, inbreuk of misbruik van gegevens in het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="06c11-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="06c11-111">Detectie van dreigingen kunt u eenvoudig op mogelijke bedreigingen adres naar het datawarehouse hoeft te worden van een deskundige beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="06c11-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="06c11-112">Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="06c11-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="06c11-113">SQL-injectie is een van de algemene Web application beveiligingsproblemen op het Internet worden gebruikt voor aanvallen op gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="06c11-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="06c11-114">Aanvallers te profiteren van de toepassing zwakke plekken in het injecteren schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="06c11-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="06c11-115">Detectie van dreigingen voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="06c11-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="06c11-116">Starten van de Azure Portal op [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06c11-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="06c11-117">Navigeer naar de blade van de configuratie van de SQL Data Warehouse die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="06c11-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="06c11-118">Selecteer in de blade instellingen **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="06c11-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Navigatiedeelvenster][1]
3. <span data-ttu-id="06c11-120">In de **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die de Threat detectie-instellingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="06c11-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="06c11-122">Schakel **ON** Bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="06c11-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="06c11-123">Configureer de lijst met e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende activiteiten datawarehouse ontvangt.</span><span class="sxs-lookup"><span data-stu-id="06c11-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="06c11-124">Klik op **opslaan** in de **controle en detectie van bedreigingen** blade van de configuratie op te slaan de nieuwe of bijgewerkte controle dreiging van beleid.</span><span class="sxs-lookup"><span data-stu-id="06c11-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Navigatiedeelvenster][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="06c11-126">Verken afwijkende datawarehouse activiteiten na detectie van een verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="06c11-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="06c11-127">U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="06c11-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="06c11-128">Het e-mailadres bevatten informatie over de verdachte-gebeurtenis met inbegrip van de aard van de afwijkende activiteiten, databasenaam, de servernaam van de en de tijd van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="06c11-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="06c11-129">Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties te onderzoeken en de mogelijke bedreiging voor de database te verminderen.</span><span class="sxs-lookup"><span data-stu-id="06c11-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Navigatiedeelvenster][4]
2. <span data-ttu-id="06c11-131">Klik in de e-mail op de **Azure SQL-controle logboek** koppeling waarmee u de klassieke Azure Portal te starten en de relevante records controle rond de tijd van de verdachte gebeurtenis wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="06c11-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Navigatiedeelvenster][5]
3. <span data-ttu-id="06c11-133">Klik op de controlerecords naar meer details weergeven over de op verdachte databaseactiviteiten zoals SQL-instructie is mislukt reden en client-IP.</span><span class="sxs-lookup"><span data-stu-id="06c11-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Navigatiedeelvenster][6]
4. <span data-ttu-id="06c11-135">Klik op de blade controle Records **openen in Excel** openen van een vooraf geconfigureerde excel sjabloon importeren en uitvoeren van de diepgaande analyse van het controlelogboek rond de tijd van de verdachte activiteit.</span><span class="sxs-lookup"><span data-stu-id="06c11-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="06c11-136">
   **Opmerking:** In Excel 2010 of hoger, Power Query en de **snel combineren** instelling is vereist</span><span class="sxs-lookup"><span data-stu-id="06c11-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Navigatiedeelvenster][7]
5. <span data-ttu-id="06c11-138">Voor het configureren van de **snel combineren** instellen - In de **POWER QUERY** linttabblad, selecteer **opties** om het dialoogvenster opties weer te geven.</span><span class="sxs-lookup"><span data-stu-id="06c11-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="06c11-139">Selecteer de sectie Privacy en kiest u de tweede optie - 'Negeren van de privacyniveaus en mogelijk verbeterde prestaties':</span><span class="sxs-lookup"><span data-stu-id="06c11-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Navigatiedeelvenster][8]
6. <span data-ttu-id="06c11-141">Als u wilt laden controlelogboeken SQL, zorg ervoor dat de parameters in de instellingen juist zijn ingesteld en selecteer vervolgens het lint 'Data' en klik op de knop Alles vernieuwen tabblad.</span><span class="sxs-lookup"><span data-stu-id="06c11-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Navigatiedeelvenster][9]
7. <span data-ttu-id="06c11-143">De resultaten worden weergegeven de **SQL controlelogboeken** blad waarmee u meer gedetailleerde analyse van de afwijkende activiteiten die zijn gedetecteerd uitvoeren, en het effect van de beveiligingsgebeurtenis in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="06c11-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
