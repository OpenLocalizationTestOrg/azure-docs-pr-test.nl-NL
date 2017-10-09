---
title: de slag met SQL Data Warehouse met detectie van dreigingen aaaGet
description: Hoe tooget de slag met detectie van dreigingen
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
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="3f304-103">Aan de slag met detectie van dreigingen</span><span class="sxs-lookup"><span data-stu-id="3f304-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f304-104">Controle</span><span class="sxs-lookup"><span data-stu-id="3f304-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="3f304-105">Detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="3f304-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3f304-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3f304-106">Overview</span></span>
<span data-ttu-id="3f304-107">Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met.</span><span class="sxs-lookup"><span data-stu-id="3f304-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="3f304-108">Detectie van dreigingen is Preview-versie en wordt ondersteund voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3f304-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="3f304-109">Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="3f304-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="3f304-110">Gebruikers kunnen verkennen Hallo verdachte gebeurtenissen met [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine als ze het gevolg zijn van een tooaccess poging schenden of misbruik van gegevens in het datawarehouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f304-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="3f304-111">Detectie van dreigingen maakt het eenvoudig tooaddress mogelijke bedreigingen toohello gegevens datawarehouse zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="3f304-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="3f304-112">Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="3f304-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="3f304-113">SQL-injectie is een van de Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3f304-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="3f304-114">Aanvallers te profiteren van de toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f304-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="3f304-115">Detectie van dreigingen voor uw database instellen</span><span class="sxs-lookup"><span data-stu-id="3f304-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="3f304-116">Start de Azure-Portal op Hallo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f304-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f304-117">Navigeer toohello configuratie blade Hallo SQL Data Warehouse gewenste toomonitor.</span><span class="sxs-lookup"><span data-stu-id="3f304-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="3f304-118">Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="3f304-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Navigatiedeelvenster][1]
3. <span data-ttu-id="3f304-120">In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die Hallo Threat detectie-instellingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f304-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Navigatiedeelvenster][2]
4. <span data-ttu-id="3f304-122">Schakel **ON** Bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="3f304-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="3f304-123">Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende activiteiten datawarehouse ontvangt.</span><span class="sxs-lookup"><span data-stu-id="3f304-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="3f304-124">Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** configuratie blade toosave Hallo nieuwe of bijgewerkte controle en threat beleid.</span><span class="sxs-lookup"><span data-stu-id="3f304-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Navigatiedeelvenster][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="3f304-126">Verken afwijkende datawarehouse activiteiten na detectie van een verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="3f304-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="3f304-127">U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="3f304-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="3f304-128">Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, server-naam en het Hallo gebeurtenistijd inclusief.</span><span class="sxs-lookup"><span data-stu-id="3f304-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="3f304-129">Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken.</span><span class="sxs-lookup"><span data-stu-id="3f304-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Navigatiedeelvenster][4]
2. <span data-ttu-id="3f304-131">Hallo e-mail, klik op Hallo **Azure SQL-controle logboek** koppeling waarmee u Hallo klassieke Azure-Portal te starten en Hallo relevante controle records rond de tijd Hallo van Hallo verdachte activiteit weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3f304-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Navigatiedeelvenster][5]
3. <span data-ttu-id="3f304-133">Klik op Hallo audit records tooview meer informatie over Hallo database verdachte activiteiten zoals SQL-instructie is mislukt reden en client-IP.</span><span class="sxs-lookup"><span data-stu-id="3f304-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Navigatiedeelvenster][6]
4. <span data-ttu-id="3f304-135">Klik op Hallo controle Records blade **openen in Excel** tooopen een vooraf geconfigureerde excel sjabloon tooimport en uitvoeren diepgaande analyse van Hallo controlelogboek rond de tijd Hallo van verdachte Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="3f304-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="3f304-136">
   **Opmerking:** In Excel 2010 of hoger, Power Query en Hallo **snel combineren** instelling is vereist</span><span class="sxs-lookup"><span data-stu-id="3f304-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Navigatiedeelvenster][7]
5. <span data-ttu-id="3f304-138">Hallo tooconfigure **snel combineren** instelling - In Hallo **POWER QUERY** linttabblad, selecteer **opties** dialoogvenster toodisplay Hallo-opties.</span><span class="sxs-lookup"><span data-stu-id="3f304-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="3f304-139">Selecteer Hallo privacysectie en kies Hallo tweede optie - 'Negeren Hallo privacyniveaus en mogelijk verbeterde prestaties':</span><span class="sxs-lookup"><span data-stu-id="3f304-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Navigatiedeelvenster][8]
6. <span data-ttu-id="3f304-141">controlelogboeken tooload SQL, zorg ervoor dat Hallo-parameters in tabblad Hallo-instellingen juist zijn ingesteld en selecteer Hallo 'Data' lint en klikt u op Hallo Alles vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="3f304-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Navigatiedeelvenster][9]
7. <span data-ttu-id="3f304-143">Hallo resultaten worden weergegeven in Hallo **SQL controlelogboeken** blad waarmee u toorun diepgaande analyse van Hallo afwijkende activiteiten die zijn gedetecteerd en verhelpen van Hallo gevolgen van het beveiligingslogboek Hallo in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f304-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
