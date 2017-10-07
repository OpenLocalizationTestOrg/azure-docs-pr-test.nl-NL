---
title: aaaHow tooconfigure eenmalige aanmelding tooan toepassingsproxy-toepassing | Microsoft Docs
description: "Hoe u snel één aanmelding tooyour application proxy toepassing kunt configureren"
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
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Hoe tooconfigure eenmalige aanmelding tooan toepassingsproxy-toepassing

Eenmalige aanmelding (SSO) kunt uw tooaccess gebruikers een toepassing zonder verificatie van meerdere keren. Deze kunt Hallo eenmalige toooccur in Hallo cloud, op basis van Azure Active Directory en Hallo service of de Connector tooimpersonate Hallo gebruiker toocomplete eventuele aanvullende verificatiecontroles van Hallo-toepassing.

## <a name="how-tooconfigure-single-sign-on"></a>Hoe tooconfigure eenmalige aanmelding
tooconfigure SSO, eerst voor zorgen dat uw toepassing is geconfigureerd voor verificatie vooraf via Azure Active Directory. toodo deze, ga te**Azure Active Directory**  - &gt; **bedrijfstoepassingen**  - &gt; **alle toepassingen**  - &gt; Uw toepassing  **- &gt; toepassingsproxy**. Op deze pagina ziet u Hallo 'Vooraf-verificatie' veld en zorg ervoor dat te wordt ingesteld 'Azure Active Directory. 

Zie voor meer informatie over Hallo verificatie vooraf methoden stap 4 van Hallo [app publishing document](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![De methode vooraf-verificatie in Azure Portal](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Modi voor eenmalige aanmelding configureren voor Application Proxy toepassingen
Vervolgens configureert we Hallo specifiek type eenmalige aanmelding. Hallo aanmelding methoden worden geclassificeerd op basis van het type verificatie Hallo back-end-toepassing wordt gebruikt. Toepassingsproxy van toepassingen ondersteunt drie typen van eenmalige aanmelding:

-   **Op basis van wachtwoorden aanmelding**: op basis van wachtwoorden eenmalige aanmelding kan worden gebruikt voor andere toepassingen die gebruikmaken van de velden gebruikersnaam en wachtwoord toosign op. Configuratiestappen vindt u in onze [wachtwoord SSO configuratiedocumentatie](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Geïntegreerde Windows-verificatie**: voor toepassingen met geïntegreerde Windows-verificatie (IWA), eenmalige aanmelding is ingeschakeld via Kerberos-beperkt delegatie (KCD). Dit wordt Application Proxy Connectors gemachtigd in Active Directory: gebruikers tooimpersonate en toosend en tokens namens hen ontvangen. Meer informatie over het configureren van KCD vindt u in Hallo [eenmalige aanmelding met KCD documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Op basis van een koptekst aanmelding**: Header gebaseerde aanmelding via een verbinding is ingeschakeld en is aanvullende configuratie vereist. Zie voor informatie over Hallo samenwerking en stapsgewijze instructies voor het configureren van eenmalige aanmelding tooan-toepassing die gebruikmaakt van headers voor de verificatie, Hallo [PingAccess voor Azure AD-documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Elk van deze opties kunt u vinden door te gaan tooyour toepassing in 'Bedrijfstoepassingen' en openen Hallo **Single Sign-On** pagina op Hallo linkermenu. Houd er rekening mee dat als uw toepassing is gemaakt in de oude portal hello, u niet al deze opties ziet mogelijk.

Op deze pagina ook ziet u een extra optie voor eenmalige aanmelding: gekoppelde aanmelding. Dit wordt ook ondersteund door de toepassingsproxy. Let echter op deze optie voegt geen eenmalige aanmelding toohello toepassing. Die deze toepassing hello mogelijk al eenmalige aanmelding geïmplementeerd met een andere service zoals Active Directory Federation Services. 

Deze optie kunt een beheerder toocreate een koppeling tooan-toepassing die de gebruikers eerst land op bij het openen van de toepassing hello. Bijvoorbeeld als er een toepassing die is geconfigureerd met behulp van Active Directory Federation Services 2.0 tooauthenticate-gebruikers, kan een beheerder Hallo ' gekoppelde aanmelding ' optie toocreate een tooit koppeling gebruiken op Hallo Toegangsvenster.

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
