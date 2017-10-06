---
title: Problemen oplossen van Azure Active Directory-activiteit inhoudspakket fouten-Logboeken | Microsoft Docs
description: Biedt u een lijst met foutberichten van hello Azure Active Directory-activiteit inhoud Inpakken en stappen toofix ze.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Het oplossen van Azure Active Directory-activiteit registreert inhoudspakket fouten 


Als u werkt met Hallo Power BI-inhoudspakket voor Azure Active Directory-Preview, is het mogelijk dat u uitvoert in Hallo volgende fouten: 

- [Vernieuwen is mislukt](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Mislukte tooupdate referenties voor gegevensbron](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Importeren van gegevens duurt te lang is](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Dit onderwerp vindt u informatie over de mogelijke oorzaken Hallo en hoe toofix deze fouten.
 
## <a name="refresh-failed"></a>Vernieuwen is mislukt 
 
**Hoe deze fout wordt opgehaald**: e-mailbericht met Power BI- of mislukte status in de geschiedenis van Hallo vernieuwen. 


| Oorzaak | Hoe toofix |
| ---   | ---        |
| Fout fouten kunnen worden veroorzaakt wanneer de referenties op Hallo van Hallo gebruikers verbinding maken met het inhoudspakket toohello zijn opnieuw ingesteld, maar niet bijgewerkt in de verbindingsinstellingen Hallo Hallo van Hallo-inhoudspakket worden vernieuwd. | Hallo gegevensset bijbehorende toohello Azure Active Directory-activiteit logboeken dashboard (Azure Active Directory-activiteit Logboeken) vinden in Power BI, kies schema vernieuwen en voer uw Azure AD-referenties. |
| Vernieuwen kan mislukken vanwege toodata problemen in Hallo onderliggende inhoudspakket. | Een ondersteuningsticket-bestand. Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Mislukte tooupdate referenties voor gegevensbron 
 
**Hoe deze fout wordt opgehaald**: In Power BI, wanneer u verbinding toohello Azure Active Directory-activiteit Logboeken (preview)-inhoudspakket maakt. 

| Oorzaak | Hoe toofix |
| ---   | ---        |
| de gebruiker verbinding maakt Hallo is een globale beheerder noch een lezer beveiliging of een beheerder beveiliging. | Gebruik een account dat een globale beheerder of een lezer beveiliging of een beveiliging admin tooaccess Hallo inhoudspakketten. |
| Uw tenant is niet een Premium-tenant of beschikt niet over ten minste één gebruiker met Premium-licentie bestand. | Een ondersteuningsticket-bestand. Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>Importeren van gegevens duurt te lang is 
 
**Hoe deze fout wordt opgehaald**: In Power BI zodra u verbinding hebt gemaakt met uw inhoudspakket importproces Hallo gestart tooprepare uw dashboard voor Azure Active Directory-logboek. U ziet het Hallo-bericht: '*importeren van gegevens...* '  

| Oorzaak | Hoe toofix |
| ---   | ---        |
| Afhankelijk van de grootte van de Hallo van uw tenant, kan deze stap duren een paar minuten too30 minuten. | NET worden geduld. Als het Hallo-bericht niet tooshowing uw dashboard binnen een uur verandert, moet u een ondersteuningsticket bestand. Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Volgende stappen

tooinstall hello Power BI-inhoudspakket voor Azure Active Directory-Preview, klikt u op [hier](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


