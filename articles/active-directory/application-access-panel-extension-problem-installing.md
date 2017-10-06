---
title: aaaProblem hello toegang Configuratiescherm browser toepassingsextensie installeren | Microsoft Docs
description: Hoe toofix veelvoorkomende fouten aangetroffen bij het installeren van de Browseruitbreiding van Hallo toegang Configuratiescherm
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problemen bij het installeren van de Browseruitbreiding van Hallo toepassing toegang Configuratiescherm

Hallo Toegangspaneel is een portal op Internet zodat een gebruiker met een werk- of school-account in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen of hello Azure AD-beheerder heeft deze toegang verleend tot. Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en beheermogelijkheden van de app via Hallo Toegangsvenster. Hallo Toegangspaneel is gescheiden van hello Azure-portal en vereist geen gebruikers toohave een Azure-abonnement.

toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker. Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Vergadering Browservereisten voor Hallo Toegangsvenster

Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld. toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker. Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.

Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:

-   Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger

-   Rand verjaardagseditie van Windows 10 of hoger 

-   Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger

-   Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo

tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:

1.  Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.

2.  Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.

3.  Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.

4.  Op basis van uw browser zijn u gerichte toohello downloadkoppeling. **Voeg** Hallo extensie tooyour browser.

5.  Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.

6.  Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.

7.  Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen

U kunt ook Hallo-extensie voor Chrome en de rand van Hallo rechtstreekse koppelingen hieronder downloaden:

-   [Uitbreiding van chrome toegang Configuratiescherm](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Uitbreiding van de rand toegang Configuratiescherm](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Instellen van een groepsbeleid voor Internet Explorer

U kunt een groepsbeleid waarmee u tooremotely installeren Hallo Toegangsvenster extensie voor Internet Explorer op computers van uw gebruikers instellen.

Hallo-vereisten zijn:

-   U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u uw gebruikers machines tooyour domein hebt toegevoegd.

-   Hallo 'Instellingen bewerken' machtiging tooedit Hallo groepsbeleidsobject (GPO), moet u hebben. Standaard hebben leden van beveiligingsgroepen na Hallo deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid. [Meer informatie](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Volg de zelfstudie Hallo [hoe tooDeploy Configuratiescherm-uitbreiding voor toegang voor Internet Explorer met behulp van Groepsbeleid Hallo](active-directory-saas-ie-group-policy.md) voor stapsgewijze instructies over hoe tooconfigure Hallo Groepsbeleid en het toousers implementeren.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Hallo Toegangsvenster in Internet Explorer oplossen

Ga als volgt Hallo [oplossen Hallo Configuratiescherm-uitbreiding voor toegang voor Internet Explorer](active-directory-saas-ie-troubleshooting.md) geleid voor toegang tot een diagnostische hulpprogramma's en stapsgewijze instructies over het configureren van Hallo-extensie voor IE.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Als u deze stappen voor probleemoplossing Hallo probleem niet verhelpen

Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:

-   Correlatie fout-ID

-   UPN (e-mailadres van de gebruiker)

-   TenantID

-   Browsertype

-   Tijdzone en de tijd/tijdsbestek tijdens fout optreedt

-   Fiddler traceringen

## <a name="next-steps"></a>Volgende stappen
[Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
