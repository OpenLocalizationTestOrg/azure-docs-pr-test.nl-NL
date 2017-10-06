---
title: aaaApp registratie Portal Help-onderwerpen | Microsoft Docs
description: Een beschrijving van verschillende functies in Hallo-portal voor registratie van Microsoft-app.
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Verwijzing van App-registratie
Dit document bevat context en beschrijvingen van de verschillende functies van Microsoft App-Portal voor Wachtwoordregistratie hello [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Mijn toepassingen
Deze lijst bevat alle van de toepassingen die zijn geregistreerd voor gebruik met hello Azure AD v2.0-eindpunt.  Deze toepassingen hebben Hallo mogelijkheid toosign in gebruikers met beide persoonlijke accounts van Microsoft-account en werk/schoolaccounts van Azure Active Directory.  toolearn meer informatie over hello Azure AD v2.0-eindpunt, Zie onze [v2.0 overzicht](active-directory-appmodel-v2-overview.md).  Deze toepassingen kunnen ook worden gebruikt toointegrate met Hallo Microsoft-account verificatie eindpunt `https://login.live.com`.

## <a name="live-sdk-applications"></a>Live SDK-Apps
Deze lijst bevat alle van de toepassingen die zijn geregistreerd voor gebruik uitsluitend met Microsoft-account.  Ze zijn niet ingeschakeld voor gebruik met Azure Active Directory beeïndigen.  Dit is waar vindt u alle toepassingen die eerder was geregistreerd bij Hallo MSA developer-portal op `https://account.live.com/developers/applications`.  Alle functies die u eerder hebt uitgevoerd op `https://account.live.com/developers/applications` kunnen nu worden uitgevoerd in deze nieuwe portal `https://apps.dev.microsoft.com`.  Als u meer vragen over uw toepassingen van Microsoft-account hebt, neem dan contact met ons.

## <a name="application-secrets"></a>Toepassing geheimen
Toepassing geheimen zijn referenties waarmee uw toepassing tooperform betrouwbare [clientverificatie](http://tools.ietf.org/html/rfc6749#section-2.3) met Azure AD.  OAuth & OpenID Connect, een toepassing geheimen is vaak waarnaar wordt verwezen tooas een `client_secret`.  In alle toepassingen die u een beveiligingstoken voor een adresseerbare weblocatie ontvangt-protocol v2.0 hello (met behulp van een `https` schema) een toepassing geheime tooidentify zelf tooAzure AD bij inwisseling die beveiligingstoken moet gebruiken.  Bovendien een native client dat tokens ontvangen op een apparaat niet kunnen worden toegestaan van het gebruik van een toepassing geheime tooperform clientverificatie toodiscourage Hallo opslag van geheimen in onbeveiligde omgevingen.

Elke app kan twee geldige aanvraag-geheimen op elk gewenst moment in de tijd bevatten.  Door twee geheimen, hebt u Hallo ablilty tooperform periodieke sleutelrollover in de gehele omgeving van uw toepassing.  Zodra u Hallo geheel van uw toepassing tooa nieuwe geheim hebt gemigreerd, kunt u deze kunt verwijderen van oude geheim Hallo en inrichten van een nieuwe.

Op dit moment worden slechts twee soorten toepassing geheimen zijn toegestaan in Hallo app-portal voor wachtwoordregistratie.  Kiezen **nieuw wachtwoord genereren** gaat genereren en opslaan van een gedeeld geheim in Hallo respectieve gegevensarchief, dat u in uw toepassing gebruiken kunt.  Kiezen **sleutelpaar genereren** maakt een nieuw openbaar/persoonlijk sleutelpaar sleutel die kan worden gedownload en kan worden gebruikt voor client verificatie tooAzure AD.

## <a name="profile"></a>Profiel
Hallo profiel gedeelte van de portal voor registratie van Hallo app toocustomize Hallo aanmelding op de pagina voor uw toepassing gebruikt.  Op dit moment kunt u wijzigen Hallo aanmelden van pagina toepassing logo, voorwaarden van de service-URL en privacyverklaring.  Hallo logo moet een transparante 48 x 48 of 50 x 50 pixels afbeelding in een GIF, PNG of JPEG-bestand dat 15 kB of kleiner.  Wijzig Hallo waarden en weer te geven Hallo resulterende aanmeldingspagina!

## <a name="live-sdk-support"></a>Ondersteuning voor Live SDK
Als u 'Live SDK Support' inschakelt, wordt elke toepassing die u maakt geheimen worden ingericht in hello Azure AD en gegevens van Microsoft-Account worden opgeslagen.  Hierdoor kan uw toepassing toointegrate rechtstreeks met de Hallo service van Microsoft-Account (login.live.com).  Als u een app met behulp van Microsoft-Account (als tegengestelde toousing hello Azure AD v2.0-eindpunt) rechtstreeks toobuild wilt, moet u ervoor zorgen dat de ondersteuning van Live SDK is ingeschakeld.

Ondersteuning voor Live SDK uitschakelen, zorgt u ervoor dat toepassingsgeheim Hallo in hello Azure AD-gegevensarchief is opgesteld.  Hello Azure AD-gegevensarchief opgenomen bedrijfsniveau voorschriften die van toe te staan toomeet bepaalde standaarden, zoals FISMA naleving.  Als u ondersteuning voor Live SDK inschakelt, kan uw toepassing compatibiliteit met enkele van deze standaarden niet bereiken.

Als u alleen ooit toouse hello Azure AD v2.0-eindpunt plant, kunt u veilig ondersteuning voor Live SDK uitschakelen.

