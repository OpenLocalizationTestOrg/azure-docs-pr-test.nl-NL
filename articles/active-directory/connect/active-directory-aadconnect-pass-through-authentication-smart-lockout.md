---
title: 'Azure AD Connect: Pass through-verificatie - Smart accountvergrendeling | Microsoft Docs'
description: Dit artikel wordt beschreven hoe Pass-through-verificatie voor Azure Active Directory (Azure AD) beveiligd met uw lokale accounts van wachtwoord beveiligingsaanvallen in Hallo cloud.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Pass-through-verificatie van Azure Active Directory: Smart accountvergrendeling

## <a name="overview"></a>Overzicht

Azure AD biedt bescherming tegen beveiligingsaanvallen wachtwoord en voorkomt dat legitieme gebruikers hun Office 365 en SaaS-toepassingen wordt vergrendeld. Deze mogelijkheid, aangeroepen **Smart accountvergrendeling**, wordt ondersteund als u Pass-through-verificatie als uw contactmethode aanmelden gebruiken. Smartcard-vergrendeling is standaard ingeschakeld voor alle tenants en beveiligt uw gebruikersaccounts alle Hallo tijd; Er is geen tooturn nodig op.

Smart vergrendeling werkt door de mislukte aanmeldpogingen te houden en na een bepaalde **Blokkeringsdrempel**, te beginnen een **vergrendelingsduur**. Alle pogingen aanmelden van de aanvaller Hallo tijdens Hallo vergrendelingsduur worden geweigerd. Als Hallo aanval blijft, aanmeldingspogingen Hallo daaropvolgende mislukte nadat Hallo vergrendelingsduur leiden tot een langere duur van de vergrendeling is beëindigd.

>[!NOTE]
>Hallo standaard Blokkeringsdrempel is 10 mislukte pogingen en Hallo standaard die vergrendelingsduur is 60 seconden.

Smart accountvergrendeling is ook onderscheid gemaakt tussen de aanmeldingen van legitieme gebruikers en tegen kwaadwillende personen en alleen vergrendeld Hallo aanvallers in de meeste gevallen. Deze functionaliteit wordt voorkomen dat aanvallers met kwaadaardige bedoelingen accountvergrendeling legitieme gebruikers. We gebruiken uit het verleden aanmelden gedrag, apparaten en browsers en andere signalen toodistinguish tussen legitieme gebruikers en aanvallers van gebruikers. We zijn voortdurend verbeteren van onze algoritmen.

Omdat Pass through-verificatie stuurt wachtwoord validatie aanvragen naar uw lokale Active Directory (AD), moet u tooprevent aanvallers van uw gebruikers AD-accounts worden vergrendeld. Omdat u uw eigen beleid AD accountvergrendeling hebt (met name [ **Accountvergrendelingsdrempel** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) en [ **beleid voor opnieuw instellen Account Lockout teller na** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), moet u de Blokkeringsdrempel tooconfigure Azure AD en vergrendelingsduur waarden op de juiste wijze toofilter uit aanvallen in Hallo cloud voordat ze bereiken met uw on-premises AD.

>[!NOTE]
>Hallo Smart accountvergrendeling is gratis en is _op_ standaard voor alle klanten. Wijzigen van de Blokkeringsdrempel en de vergrendelingsduur waarden Graph API met Azure AD heeft uw tenant toohave ten minste één Azure AD Premium P2-licentie nodig. U hoeft niet met een licentie voor Azure AD Premium-P2 _per gebruiker_ tooget Hallo Smart accountvergrendeling met Pass through-verificatie.

tooensure dat uw gebruikers on-premises AD-accounts zijn beveiligd, moet u tooensure die:

1.  Azure AD-Blokkeringsdrempel is _minder_ dan de drempelwaarde voor vergrendeling van AD-Account. Wij raden Hallo waarden in te stellen zodat AD van Accountvergrendelingsdrempel ten minste twee is of drie keer Blokkeringsdrempel Azure AD.
2.  Azure AD-vergrendelingsduur (weergegeven in seconden) is _langer_ dan van AD opnieuw Account Lockout teller na (weergegeven in minuten).

## <a name="verify-your-ad-account-lockout-policies"></a>Controleer of uw AD-accountvergrendeling-beleid

Hallo instructies tooverify na een accountvergrendeling AD-beleid gebruiken:

1.  Open het Hallo Group Policy Management-hulpprogramma.
2.  Hallo Groepsbeleid bewerken die is toegepast tooall gebruikers, bijvoorbeeld Hallo standaarddomeinbeleid.
3.  Navigeer tooComputer Computerconfiguratie\Beleid\Windows Settings\Security Instellingen\beveiligingsinstellingen\accountbeleid\accountvergrendelingsbeleid.
4.  Controleer of uw Accountvergrendelingsdrempel en stellen Account Lockout teller na waarden.

![AD accountvergrendeling beleid](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Hallo Graph API toomanage van uw tenant Smart accountvergrendeling waarden gebruiken

>[!IMPORTANT]
>Wijzigen van de Blokkeringsdrempel en de vergrendelingsduur waarden Graph API met Azure AD is een Azure AD Premium P2-functie. Ook moet u toobe een globale beheerder zijn op uw tenant.

U kunt [grafiek Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, ingesteld en Azure AD Smart accountvergrendeling waarden bijwerken. Maar u kunt deze bewerkingen ook programmatisch doen.

### <a name="read-smart-lockout-values"></a>Waarden van de smartcard accountvergrendeling lezen

Volg deze stappen tooread van uw tenant Smart accountvergrendeling waarden:

1. Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant. Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.
2. Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.
3. Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'ophalen' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Klikt u op 'Query uitvoeren' toosee van uw tenant Smart accountvergrendeling waarden. Als u waarden voor uw tenant voordat dit nog niet hebt ingesteld, ziet u een lege set.

### <a name="set-smart-lockout-values"></a>Smart accountvergrendeling waarden instellen

Volg deze stappen tooset van uw tenant Smart accountvergrendeling waarden (voor Hallo alleen de eerste keer):

1. Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant. Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.
2. Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.
3. Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'posten' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Kopieer en plak de volgende JSON-aanvraag naar Hallo 'Aanvraag hoofdtekst' veld Hallo. Hallo Smart accountvergrendeling waarden waar nodig wijzigen en gebruiken van een willekeurige GUID voor `templateId`.
5. Klikt u op 'Query uitvoeren' tooset van uw tenant Smart accountvergrendeling waarden.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Als u deze niet gebruikt, kunt u Hallo laten **BannedPasswordList** en **EnableBannedPasswordCheck** waarden als leeg ("") en 'false' respectievelijk.

Controleer of u van uw tenant Smart accountvergrendeling waarden correct hebt ingesteld [deze stappen](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Smart accountvergrendeling waarden bijwerken

Volg deze stappen tooupdate van uw tenant Smart accountvergrendeling waarden (als u deze voordat u al hebt ingesteld):

1. Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant. Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.
2. Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.
3. [Volg deze stappen tooread van uw tenant Smart accountvergrendeling waarden](#read-smart-lockout-values). Kopiëren Hallo `id` waarde (GUID) van het Hallo-item met 'weergavenaam' als 'PasswordRuleSettings'.
4. Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'PATCH' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -gebruiken Hallo GUID vanaf stap 3 voor `<id>`.
5. Kopieer en plak de volgende JSON-aanvraag naar Hallo 'Aanvraag hoofdtekst' veld Hallo. Hallo Smart accountvergrendeling waarden zo nodig wijzigen.
6. Klikt u op 'Query uitvoeren' tooupdate van uw tenant Smart accountvergrendeling waarden.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Controleer of u hebt uw tenant Smart accountvergrendeling waarden correct met bijgewerkt [deze stappen](#read-smart-lockout-values).

## <a name="next-steps"></a>Volgende stappen
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
