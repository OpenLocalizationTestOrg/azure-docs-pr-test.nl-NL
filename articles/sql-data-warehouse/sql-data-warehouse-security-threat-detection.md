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
# <a name="get-started-with-threat-detection"></a>Aan de slag met detectie van dreigingen
> [!div class="op_single_selector"]
> * [Controle](sql-data-warehouse-auditing-overview.md)
> * [Detectie van bedreigingen](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Overzicht
Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met. Detectie van dreigingen is Preview-versie en wordt ondersteund voor SQL Data Warehouse.

Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd. Gebruikers kunnen verkennen Hallo verdachte gebeurtenissen met [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine als ze het gevolg zijn van een tooaccess poging schenden of misbruik van gegevens in het datawarehouse Hallo.
Detectie van dreigingen maakt het eenvoudig tooaddress mogelijke bedreigingen toohello gegevens datawarehouse zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.

Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft. SQL-injectie is een van de Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen. Aanvallers te profiteren van de toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database Hallo.

## <a name="set-up-threat-detection-for-your-database"></a>Detectie van dreigingen voor uw database instellen
1. Start de Azure-Portal op Hallo [https://portal.azure.com](https://portal.azure.com).
2. Navigeer toohello configuratie blade Hallo SQL Data Warehouse gewenste toomonitor. Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.
   
    ![Navigatiedeelvenster][1]
3. In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die Hallo Threat detectie-instellingen weergegeven.
   
    ![Navigatiedeelvenster][2]
4. Schakel **ON** Bedreigingendetectie.
5. Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende activiteiten datawarehouse ontvangt.
6. Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** configuratie blade toosave Hallo nieuwe of bijgewerkte controle en threat beleid.
   
    ![Navigatiedeelvenster][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Verken afwijkende datawarehouse activiteiten na detectie van een verdachte activiteit
1. U ontvangt een e-mailmelding na detectie van afwijkende databaseactiviteiten. <br/>
   Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, server-naam en het Hallo gebeurtenistijd inclusief. Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken.<br/>
   
    ![Navigatiedeelvenster][4]
2. Hallo e-mail, klik op Hallo **Azure SQL-controle logboek** koppeling waarmee u Hallo klassieke Azure-Portal te starten en Hallo relevante controle records rond de tijd Hallo van Hallo verdachte activiteit weer te geven.
   
    ![Navigatiedeelvenster][5]
3. Klik op Hallo audit records tooview meer informatie over Hallo database verdachte activiteiten zoals SQL-instructie is mislukt reden en client-IP.
   
    ![Navigatiedeelvenster][6]
4. Klik op Hallo controle Records blade **openen in Excel** tooopen een vooraf geconfigureerde excel sjabloon tooimport en uitvoeren diepgaande analyse van Hallo controlelogboek rond de tijd Hallo van verdachte Hallo-gebeurtenis.<br/>
   **Opmerking:** In Excel 2010 of hoger, Power Query en Hallo **snel combineren** instelling is vereist
   
    ![Navigatiedeelvenster][7]
5. Hallo tooconfigure **snel combineren** instelling - In Hallo **POWER QUERY** linttabblad, selecteer **opties** dialoogvenster toodisplay Hallo-opties. Selecteer Hallo privacysectie en kies Hallo tweede optie - 'Negeren Hallo privacyniveaus en mogelijk verbeterde prestaties':
   
    ![Navigatiedeelvenster][8]
6. controlelogboeken tooload SQL, zorg ervoor dat Hallo-parameters in tabblad Hallo-instellingen juist zijn ingesteld en selecteer Hallo 'Data' lint en klikt u op Hallo Alles vernieuwen.
   
    ![Navigatiedeelvenster][9]
7. Hallo resultaten worden weergegeven in Hallo **SQL controlelogboeken** blad waarmee u toorun diepgaande analyse van Hallo afwijkende activiteiten die zijn gedetecteerd en verhelpen van Hallo gevolgen van het beveiligingslogboek Hallo in uw toepassing.

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
