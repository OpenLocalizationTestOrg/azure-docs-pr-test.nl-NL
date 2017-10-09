---
title: Connector voor toepassingsproxy-Agent installeren aaaProblem Hallo | Microsoft Docs
description: Hoe tootroubleshoot problemen die u mogelijk Hallo face bij het installeren van Connector voor toepassingsproxy-Agent
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problemen bij het Hallo-Connector voor toepassingsproxy-Agent installeren

Microsoft AAD Application Proxy Connector is een onderdeel van het interne domein die gebruikmaakt van uitgaande verbindingen tooestablish Hallo connectiviteit uit Hallo cloud beschikbare eindpunt toohello interne domein.

## <a name="general-problem-areas-with-connector-installation"></a>Algemene probleemgebieden met installatie van de Connector

Wanneer Hallo-installatie van een connector is mislukt, is Hallo hoofdoorzaak meestal een Hallo gebieden te volgen:

1.  **Connectiviteit** – toocomplete een geslaagde installatie Hallo nieuwe connector behoeften tooregister en toekomstige vertrouwensgegevens tot stand brengen. Dit wordt gedaan door verbinding te maken toohello AAD Application Proxy-cloudservice.

2.  **Vertrouwensrelatie tot stand brengen** – Hallo nieuwe connector maakt u een zelfondertekend certificaat en toohello cloudservice geregistreerd.

3.  **Verificatie van Hallo beheerder** – tijdens de installatie Hallo gebruiker referenties moet opgeven admin installatie toocomplete Hallo-Connector.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Controleer of connectivity toohello Cloud Application Proxy-service en Microsoft Login pagina

**Doelstelling:** controleren die connector Hallo machine toohello AAD Application Proxy registratie eindpunt, evenals een aanmeldingspagina voor Microsoft verbinding kan maken.

1.  Open een browser en Ga naar toohello webpagina's te volgen: <https://aadap-portcheck.connectorporttest.msappproxy.net> , en controleert u dat Hallo connectiviteit tooCentral VS en VS-Oost datacenters met poort 9090 en 9091 werkt.

2.  Als een van deze poorten is niet geslaagd (geen een groen vinkje), Controleer of dat Hallo Firewall of back-end-proxy heeft \*. msappproxy.net met poort 9090 en 9091 correct gedefinieerd.

3.  Open een browser (door tabs gescheiden) en Ga na webpagina toohello: <https://login.microsoftonline.com>, zorg ervoor dat u zich toothat pagina aanmelden kunt.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Controleer of de Machine- en back-end-onderdelen ondersteund voor toepassingsproxy vertrouwensrelatie cert

**Doelstelling:** controleren of Hallo connector machine, back-end-proxy en firewall Hallo certificaat dat is gemaakt door de connector Hallo voor toekomstige vertrouwensrelatie kunnen ondersteunen.

>[!NOTE]
>Hallo-connector probeert een SHA512-certificaat dat wordt ondersteund door TLS1.2 toocreate. Als het Hallo-machine of Hallo back-endfirewall en proxy wordt niet ondersteund voor TLS1.2, Hallo installatie mislukken.
>
>

**probleem met de Hallo tooresolve:**

1.  Controleer of de machine Hallo ondersteunt TLS1.2 – TLS 1.2 moeten ondersteuning voor alle Windows-versies na 2012 R2. Als de computer van de connector van een versie van 2012 R2 of vóór is, zorg ervoor dat Hallo volgende KB op Hallo computer zijn geïnstalleerd: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Neem contact op met de beheerder van uw netwerk en vraag tooverify dat Hallo back-end-proxy- en firewallservers niet SHA512 voor uitgaand verkeer blokkeren.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Controleer of admin gebruikte tooinstall Hallo-connector

**Doelstelling:** controleren die Hallo-gebruiker die tooinstall Hallo-connector probeert is een beheerder met de juiste referenties. Hallo-gebruiker moet op dit moment een globale beheerder voor Hallo installatie toosucceed.

**tooverify hello referenties zijn juist:**

Verbinding te maken met<https://login.microsoftonline.com> en Hallo dezelfde referenties gebruiken. Zorg ervoor dat het Hallo-aanmelding is geslaagd. U kunt Hallo gebruikersrol controleren door te gaan**Azure Active Directory**  - &gt; **gebruikers en groepen**  - &gt; **alle gebruikers**. 

Selecteer uw gebruikersaccount, klikt u vervolgens 'Directory rol' in de resulterende Hallo-menu. Controleer of die geselecteerde rol Hallo 'Globale beheerder'. Als u tooaccess van Hallo-pagina's langs deze stappen bent, bent u niet een globale beheerder.

## <a name="next-steps"></a>Volgende stappen
[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
