---
title: Application Insights tootroubleshoot aangepast beleid dat is - Azure AD B2C | Microsoft Docs
description: hoe toosetup Application Insights tootrace Hallo uitvoering van een aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Verzamelen van Logboeken

Dit artikel bevat stappen voor het verzamelen van Logboeken van Azure AD B2C, zodat u met uw eigen beleid problemen kunt.

>[!NOTE]
>Op dit moment hello gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** tooaid in ontwikkeling van aangepast beleid. Gebruik geen Ontwikkelingsmodus in productie.  Logboeken verzamelen van alle claims tooand van Hallo id-providers verzonden tijdens de ontwikkeling.  Als dit wordt gebruikt in productie, verantwoordelijkheid Hallo developer voor PII (privé identificeerbare informatie) verzameld in Hallo App Insights logboek waarvan ze eigenaar.  Deze gedetailleerde logboeken worden alleen verzameld wanneer de Hallo beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.


## <a name="use-application-insights"></a>Application Insights gebruiken

Azure AD B2C ondersteunt de functie voor het verzenden van gegevens tooApplication Insights.  Application Insights biedt een manier toodiagnose uitzonderingen en prestatieproblemen toepassing visualiseren.

### <a name="setup-application-insights"></a>Application Insights instellen

1. Ga toohello [Azure-portal](https://portal.azure.com). Zorg ervoor dat u zich in Hallo-tenant met uw Azure-abonnement (niet uw Azure AD B2C-tenant).
1. Klik op **+ nieuw** in Hallo links navigatiemenu.
1. Zoek en selecteer **Application Insights**, klikt u vervolgens op **maken**.
1. Vul Hallo formulier in en klik op **maken**. Selecteer **algemene** voor Hallo **toepassingstype**.
1. Zodra het Hallo-resource is gemaakt, opent u Hallo Application Insights-resource.
1. Zoeken naar **eigenschappen** in Hallo links menu en klik erop.
1. Kopiëren Hallo **Instrumentatiesleutel** en voor de volgende sectie Hallo op te slaan.

### <a name="set-up-hello-custom-policy"></a>Hallo aangepast beleid instellen

1. Hallo RP-bestand (bijvoorbeeld SignUpOrSignin.xml) openen.
1. Hallo na toohello kenmerken toevoegen `<TrustFrameworkPolicy>` element:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Als deze niet al bestaat, een onderliggend knooppunt toevoegen `<UserJourneyBehaviors>` toohello `<RelyingParty>` knooppunt. Het moet zich onmiddellijk na Hallo`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Toevoegen op het knooppunt als een onderliggend element van Hallo volgt Hallo `<UserJourneyBehaviors>` element. Zorg ervoor dat tooreplace `{Your Application Insights Key}` Hello **Instrumentatiesleutel** die u hebt verkregen via de Application Insights in de vorige sectie Hallo.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`Hiermee geeft u ApplicationInsights tooexpedite Hallo telemetrie via Hallo verwerking pipeline, goed voor ontwikkeling, maar beperkte op hoge volumes.
  * `ClientEnabled="true"`verzendt Hallo ApplicationInsights clientscript voor het bijhouden van pagina-fouten weergeven en clientzijde (niet nodig).
  * `ServerEnabled="true"`verzendt Hallo bestaande UserJourneyRecorder JSON als een aangepaste gebeurtenis tooApplication Insights.
Voorbeeld:

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. Hallo beleid uploaden.

### <a name="see-hello-logs-in-application-insights"></a>Zie hello wordt geregistreerd in Application Insights

>[!NOTE]
> Er is een korte vertraging (minder dan vijf minuten) voordat u nieuwe logboeken in Application Insights kunt zien.

1. Open Hallo Application Insights-resource die u hebt gemaakt in Hallo [Azure-portal](https://portal.azure.com).
1. In Hallo **overzicht** menu, klik op **Analytics**.
1. Open een nieuw tabblad in Application Insights.
1. Hier volgt een lijst van query's dat kunt u toosee Hallo Logboeken

| Query’s uitvoeren | Beschrijving |
|---------------------|--------------------|
Traceringen | Zie al Hallo-logboeken die worden gegenereerd door Azure AD B2C |
traceringen \| waar tijdstempel > ago(1d) | Zie al Hallo-logboeken die zijn gegenereerd door Azure AD B2C voor Hallo laatste dag

Hallo vermeldingen mogelijk lang.  Exporteer tooCSV voor nader bekijken.

Voor meer informatie over het hulpprogramma voor analyse van Hallo [hier](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Hallo-community heeft een gebruiker reis viewer toohelp identiteit ontwikkelaars ontwikkeld.  Niet wordt ondersteund door Microsoft en beschikbaar gesteld strikt als-is.  Het leest uit uw Application Insights-exemplaar en biedt een weergave ook structuur van Hallo gebruiker reis gebeurtenissen.  U Hallo broncode downloaden en deze implementeren in uw eigen oplossing.

>[!NOTE]
>Op dit moment hello gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** tooaid in ontwikkeling van aangepast beleid. Gebruik geen Ontwikkelingsmodus in productie.  Logboeken verzamelen van alle claims tooand van Hallo id-providers verzonden tijdens de ontwikkeling.  Als dit wordt gebruikt in productie, verantwoordelijkheid Hallo developer voor PII (privé identificeerbare informatie) verzameld in Hallo App Insights logboek waarvan ze eigenaar.  Deze gedetailleerde logboeken worden alleen verzameld wanneer de Hallo beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.

[Github-opslagplaats voor niet-ondersteunde aangepast beleid voor voorbeelden en bijbehorende hulpprogramma 's](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Volgende stappen

Hallo-gegevens in Application Insights toohelp u begrijpt hoe Hallo identiteit ervaring Framework onderliggende B2C toodeliver optreedt in uw eigen identiteit werkt.
