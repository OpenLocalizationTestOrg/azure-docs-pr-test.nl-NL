---
title: aaaHow toouse hello Azure Active Directory Power BI-inhoudspakket | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure Active Directory Power BI-inhoudspakket
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Hoe toouse hello Azure Active Directory Power BI-inhoudspakket

Voor u als IT-beheerder is het enorm belangrijk om te weten hoe uw gebruikers functies van Azure Active Directory implementeren en gebruiken. Hiermee kunt u uw IT-infrastructuur en communicatie tooincrease gebruiks- en tooget Hallo meest buiten het AAD-functies tooplan. Power BI-inhoud Pack voor Azure Active Directory biedt u de mogelijkheid toofurther Hallo analyseren van uw gegevens toounderstand hoe u deze gegevens toogather uitgebreidere inzicht te krijgen kunt in wat er gebeurt met Azure Active Directory voor Hallo verschillende mogelijkheden u sterk afhankelijk van.  Hallo de integratie van Azure Active Directory-API's met Power BI, kunt u eenvoudig hello vooraf samengestelde inhoudspakketten downloaden en Verkrijg inzicht tooall Hallo activiteiten binnen uw Azure Active Directory met Power BI biedt uitgebreide visualisatie-ervaring. U kunt uw eigen dashboard maken en dit dashboard vervolgens eenvoudig delen met andere personen binnen uw organisatie. 

In dit onderwerp vindt u stapsgewijze instructies over hoe tooinstall en gebruik inhoud Hallo pack in uw omgeving.

## <a name="installation"></a>Installeren  

**tooinstall hello Power BI-inhoudspakket:**

1. Meld u aan bij [Power BI](https://app.powerbi.com/groups/me/getdata/services) met uw Power BI-Account (dit is Hallo hetzelfde account zijn als uw O365- of Azure AD-Account).

2. Selecteer onderaan Hallo Hallo linkernavigatiedeelvenster, **gegevens ophalen**.

    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. In Hallo **Services** Klik **ophalen**.
   
    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Zoek naar **Azure Active Directory**.

    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Als u daarom wordt gevraagd, typt u de id van uw Azure AD-tenant en klikt u vervolgens op **Volgende**.

    > [!TIP] 
    > Een snelle manier tooget hello Tenant-Id voor uw Office 365 / Azure AD-tenant is toologin toohello Azure AD-Portal, toohello directory inzoomen en Hallo-ID van de URL na Hallo kopiëren: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension en demap/<tenantid>/directoryQuickStart

    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Klik op **Aanmelden**. 
 
    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Voer uw gebruikersnaam en wachtwoord in en klik vervolgens op **Aanmelden**.
 
    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  Klik op Hallo app toestemming dialoogvenster **accepteren**.
 
9.  Wanneer het dashboard Activiteitenlogboeken van Azure Active Directory is gemaakt, klikt u erop.
 
    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>Wat kan ik doen met dit inhoudspakket?

Voordat we naar wat u met dit inhoudspakket doen kunt gaan, hier snel voorbeeld van Hallo diverse rapporten in Hallo inhoud pack. Rapport gegevens terug toohello **afgelopen 30 dagen**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Rapporten die zijn opgenomen in deze versie van het inhoudspakket met Azure Active Directory-logboeken

**App-gebruik en Trend rapport**: Verkrijg inzicht in het Hallo-apps gebruikt in welke worden gebruikt en uw organisatie meest Hallo en wanneer. U kunt gebruiken in dit rapport toogather inzicht in hoe een app die u onlangs uitgerold in uw organisatie wordt gebruikt of welke apps populaire zijn weten. Op deze manier kunt u informatie over het gebruik verbeteren als u ziet als Hallo-app niet wordt gebruikt.

**Aanmeldingen per locatie en gebruikers**: Verkrijg inzicht in alle Hallo aanmeldingen uitgevoerd met behulp van Azure identiteits- en biedt inzicht in Hallo identiteit van Hallo gebruikers. U kunt zo gedetailleerde informatie verkrijgen over afzonderlijke aanmeldingen en vragen beantwoorden zoals:

- Vanaf welke locatie hebben deze gebruikers zich aangemeld?
- Welke gebruiker Hallo meeste aanmeldingen en waar ze aanmelden uit? 
- Geslaagd Hallo aanmelden?  
 
U kunt inzoomen op details door op een bepaalde datum of locatie te klikken.

**Unieke gebruikers per app**: bekijk een weergave van alle unieke gebruikers die een bepaalde app gebruiken. Het betreft hier alleen gebruikers die *het* gelukt is om zich aan te melden bij een toepassing.

**Apparaat aanmeldingen**: ophalen van een weergave van het Hallo-type van het besturingssysteem en browsers worden gebruikt door gebruikers in uw organisatie, met gedetailleerde informatie over het Hallo-gebruikers met inbegrip van:

- Gebruikersnaam
- IP-adres
- Locatie 
- Aanmeldingsstatus 

Met dit rapport kunt u inzicht in Hallo profielen voor verschillende apparaten binnen uw organisatie gebruikt en bepalen op basis van wat wordt gebruikt beleidsregels voor apparaten

**SSPR-trechter**: bekijk informatie over de manier waarop wachtwoorden opnieuw worden ingesteld in uw organisatie. Een peek krijgen in hoe vaak een wachtwoord opnieuw instellen via Hallo SSPR hulpprogramma zijn geprobeerd en hoeveel ze is gelukt. Verdiepen in Hallo wachtwoord opnieuw instellen fout met Hallo SSPR trechter en begrijpen waarom bepaalde fouten zijn opgetreden. Dit rapport geeft een beter begrip van hoe Hallo SSPR hulpprogramma wordt gebruikt binnen uw organisatie, zodat u Hallo rechts beslissingen kunt nemen.

## <a name="customizing-azure-ad-activity-content-pack"></a>Het inhoudspakket Azure AD-activiteit aanpassen

**Visualisatie wijzigen**: U kunt een rapport visualisatie wijzigen door te klikken op **rapport bewerken** en Hallo visualisatie die u wilt selecteren.
 
![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Aanvullende velden bevatten**: U kunt een veld toohello rapport toevoegen of verwijderen met de Hallo visual toowhich die u wilt verwijderen tooadd Hallo veld te selecteren. Ik toevoeg 'aanmeldingsstatus' veld toohello tabelweergave in Hallo onderstaande voorbeeld. 
 
![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Pincode visualisaties tooyour dashboard**: U kunt het dashboard aanpassen en uw eigen visualisaties toohello rapport opnemen en toohello dashboard vastmaken. In onderstaande Hallo voorbeeld, ik toegevoegd een nieuw filter 'aanmeldingsstatus' genoemd en het Hallo-rapport bevat. Ik ook gewijzigd Hallo visualisatie van staafdiagram tooa lijndiagram en u kunt deze nieuwe visual toohello dashboard vastmaken.

![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Uw dashboard delen**: nadat u de gewenste Hallo inhoud hebt gemaakt, kunt u Hallo dashboard delen met Hallo gebruikers in uw organisatie. Houd er rekening mee dat zodra u Hallo rapport deelt, zien ze Hallo velden die u hebt geselecteerd in het Hallo-rapport.
 
![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Dagelijks vernieuwen van het Power BI-rapport plannen

tooschedule dagelijkse vernieuwen van uw Power BI-rapport te gaan**gegevenssets > Instellingen > schema vernieuwen** en in te stellen, zoals hieronder wordt weergegeven.
 
![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Toonewer-versie van het inhoudspakket bijwerken

Als u wilt dat tooupdate pack uw inhoud tooget een nieuwere versie:

- Nieuwe inhoud pack Hallo downloaden en instellen volgens de instructies in dit artikel.

- Als u dit hebt ingesteld, gaat u te**Data Source > Instellingen > gegevensbronreferenties** en voer uw referenties opnieuw zoals hieronder wordt weergegeven

    ![Azure Active Directory Power BI Content Pack](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Als u de nieuwe versie van het inhoudspakket Hallo Hallo werkt, kunt u de oude versie Hallo verwijderen indien nodig door Hallo onderliggende rapporten en gegevenssets die zijn gekoppeld aan dit inhoudspakket te verwijderen.

## <a name="still-having-issues"></a>Nog steeds problemen? 

Raadpleeg onze [handleiding voor het oplossen van problemen](active-directory-reporting-troubleshoot-content-pack.md). Voor algemene hulp met Power BI raadpleegt u deze [Help-artikelen](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Volgende stappen

Zie voor een overzicht van reporting Hallo [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md).
