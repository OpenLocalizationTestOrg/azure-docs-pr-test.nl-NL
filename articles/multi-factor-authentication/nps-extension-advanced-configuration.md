---
title: aaaConfigure hello Azure MFA NPS extensie | Microsoft Docs
description: "Nadat u Hallo NPS uitbreiding hebt geïnstalleerd, moet u deze stappen gebruiken voor geavanceerde configuratie zoals IP-whitelisting en UPN vervanging."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Geavanceerde configuratieopties voor Hallo NPS-extensie voor multi-factor Authentication

Hallo Network Policy Server (NPS)-extensie breidt uw cloud-gebaseerde Azure multi-factor Authentication-functies in uw on-premises infrastructuur. In dit artikel wordt ervan uitgegaan dat u al geïnstalleerd Hallo-extensie hebt en tooknow hoe toocustomize Hallo-extensie voor u moet een goed idee. 

## <a name="alternate-login-id"></a>Alternatieve aanmeldings-ID

Aangezien Hallo NPS extensie tooboth uw on-premises en cloud verbindt-adreslijsten, kunnen er een probleem waarbij uw lokale UPN-namen (UPN's) Hallo namen in de cloud Hallo niet overeenkomen. toosolve dit probleem op door gebruik alternatieve aanmeldings-id's. 

Binnen Hallo NPS-extensie, kunt u een Active Directory-kenmerk toobe gebruikt in plaats van Hallo UPN voor Azure multi-factor Authentication aanwijzen. Hierdoor kan uw lokale bronnen met verificatie in twee stappen u tooprotect zonder te wijzigen van uw lokale UPN's. 

tooconfigure alternatieve aanmeldings-id's, gaat u te`HKLM\SOFTWARE\Microsoft\AzureMfa` en bewerken van de volgende registerwaarden Hallo:

| Naam | Type | Standaardwaarde | Beschrijving |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | Tekenreeks | leeg | Hallo-naam van Active Directory-kenmerk dat u wilt dat toouse in plaats van Hallo UPN aanwijzen. Dit kenmerk wordt gebruikt als Hallo AlternateLoginId kenmerk. Als deze registerwaarde is ingesteld tooa [geldig Active Directory-kenmerk](https://msdn.microsoft.com/library/ms675090.aspx) (voor bijvoorbeeld e-mail of weergavenaam), vervolgens Hallo kenmerkwaarde wordt gebruikt in plaats van de UPN van de gebruiker Hallo voor verificatie. Als deze registerwaarde leeg of niet is is geconfigureerd, klikt u vervolgens AlternateLoginId is uitgeschakeld en de UPN van de gebruiker hello wordt gebruikt voor verificatie. |
| LDAP_FORCE_GLOBAL_CATALOG | Booleaanse waarde | False | Gebruik deze vlag tooforce Hallo gebruik van globale catalogus voor LDAP-zoekopdrachten bij het opzoeken van AlternateLoginId. Een domeincontroller configureren als een globale catalogus toevoegen Hallo AlternateLoginId kenmerk toohello globale catalogus en schakelt u deze vlag. <br><br> Als LDAP_LOOKUP_FORESTS is geconfigureerd (geen lege) **deze vlag wordt afgedwongen als waar**, ongeacht van Hallo-waarde van de registerinstelling Hallo. In dit geval vereist Hallo NPS-uitbreiding Hallo globale catalogus toobe geconfigureerd met Hallo AlternateLoginId kenmerk voor elke forest. |
| LDAP_LOOKUP_FORESTS | Tekenreeks | leeg | Geef een puntkomma's gescheiden lijst van forests toosearch. Bijvoorbeeld: *contoso.com;foobar.com*. Als deze registerwaarde is geconfigureerd, zoekt Hallo NPS-extensie alle Hallo forests iteratief in Hallo volgorde waarin ze zijn vermeld en Hallo eerste geslaagde AlternateLoginId waarde retourneert. Als deze registerwaarde niet is geconfigureerd, is het Hallo AlternateLoginId lookup beperkt toohello huidige domein.|

tootroubleshoot problemen met alternatieve aanmeldings-id's, Hallo aanbevolen stappen voor het gebruik [alternatieve aanmeldings-ID fouten](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>IP-uitzonderingen

Als u toomonitor beschikbaarheid van de server, zoals als netwerktaakverdelers welke servers worden uitgevoerd controleren voor het verzenden van werkbelastingen, moet wilt u niet dat deze controles toobe wordt geblokkeerd door de verificatie-aanvragen. In plaats daarvan een lijst met IP-adressen die u kent worden gebruikt door de service-accounts maken en vereisten van de multi-factor Authentication voor die lijst uitschakelen. 

tooconfigure een goedgekeurde IP-adressen te gaan`HKLM\SOFTWARE\Microsoft\AzureMfa` en Hallo registerwaarde volgende configureren: 

| Naam | Type | Standaardwaarde | Beschrijving |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | Tekenreeks | leeg | Geef een puntkomma's gescheiden lijst van IP-adressen. Hallo IP-adressen van computers waar serviceaanvragen afkomstig zijn, zoals Hallo NAS/VPN-server bevatten. IP-adresbereiken zijn subnetten worden niet ondersteund. <br><br> Bijvoorbeeld: *10.0.0.1;10.0.0.2;10.0.0.3*.

Wanneer een aanvraag afkomstig is van een IP-adres die in goedgekeurde lijst hello voorkomt, wordt verificatie in twee stappen overgeslagen. Hallo goedgekeurde IP-adressen is vergeleken toohello IP-adres dat is opgegeven in Hallo *ratNASIPAddress* kenmerk van Hallo RADIUS-aanvraag. Als een RADIUS-aanvraag wordt geleverd zonder Hallo ratNASIPAddress kenmerk, Hallo waarschuwing na vastgelegd: 'P_WHITE_LIST_WARNING::IP geaccepteerde wordt genegeerd als de bron-IP ontbreekt in de RADIUS-aanvraag in NasIpAddress-kenmerk.'

## <a name="next-steps"></a>Volgende stappen

[Foutberichten van Hallo NPS-extensie voor Azure multi-factor Authentication oplossen](multi-factor-authentication-nps-errors.md)
