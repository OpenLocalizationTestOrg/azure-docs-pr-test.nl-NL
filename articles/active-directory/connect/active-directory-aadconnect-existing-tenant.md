---
title: 'Azure AD Connect: Wanneer u al hebt Azure AD | Microsoft Docs'
description: Dit onderwerp wordt beschreven hoe toouse verbinding maken als er een bestaande Azure AD-tenant.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: Wanneer u hebt een bestaande tenant
Hallo-onderwerpen voor hoe toouse Azure AD Connect wordt ervan uitgegaan u dat de meeste beginnen met een nieuwe Azure AD-tenant en dat er geen gebruikers of er andere objecten zijn. Als u hebt gestart met een Azure AD-tenant gevuld zijn met gebruikers en andere objecten maar nu wil toouse Connect, en dit onderwerp is voor u.

## <a name="hello-basics"></a>Hallo-basisbeginselen
Een object in Azure AD heeft ofwel als master in het Hallo-cloud (Azure AD) of on-premises. Voor een enkel object, kunt u bepaalde kenmerken on-premises en sommige andere kenmerken niet beheren in Azure AD. Elk object heeft een vlag die aangeeft waar Hallo-object wordt beheerd.

In de cloud Hallo kunt u sommige gebruikers on-premises en andere beheren. Een veelvoorkomend scenario voor deze configuratie is een organisatie met een combinatie van accounting werknemers en verkoop. Hallo accounting werknemers hebben een on-premises AD-account, maar Hallo verkoop werknemers niet, ze hebben een account in Azure AD. Sommige gebruikers on-premises en sommige in Azure AD beheren.

Als u gebruikers toomanage gestart in Azure AD die zich ook in on-premises AD en later wilt toouse Connect, worden er enkele aanvullende problemen moet u tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Synchroniseren met bestaande gebruikers in Azure AD
Wanneer u Azure AD Connect installeert en u begint met het synchroniseren, hello Azure AD sync-service (in Azure AD) biedt een controle op elk nieuw object en probeer het een bestaand object toomatch toofind. Er zijn drie kenmerken die worden gebruikt voor dit proces: **userPrincipalName**, **proxyAddresses**, en **sourceAnchor**/**onveranderbare id genoemd**. Een overeenkomst op **userPrincipalName** en **proxyAddresses** wordt ook wel een **zachte overeen**. Een overeenkomst op **sourceAnchor** staat bekend als **harde overeen**. Voor Hallo **proxyAddresses** alleen Hallo waarde met het kenmerk **SMTP:**, die Hallo primaire e-mailadres is, wordt gebruikt voor het Hallo-evaluatie.

Hallo overeenkomst wordt alleen voor nieuwe objecten die afkomstig zijn van Connect geëvalueerd. Als u een bestaande object wijzigen zodat deze met een van deze kenmerken overeen komt, klikt u vervolgens ziet u een fout in plaats daarvan.

Als Azure AD vindt een object waar kenmerkwaarden Hallo Hallo zijn dezelfde voor een object dat afkomstig is van Connect en dat deze is al aanwezig in Azure AD en hello object in Azure AD wordt overgenomen Connect. Hallo is eerder cloud beheerde object gemarkeerd als lokale beheerd. Alle kenmerken in Azure AD met een waarde in de lokale AD overschreven met de Hallo lokale waarde. Hallo-uitzondering is wanneer een kenmerk heeft een **NULL** lokale waarde. In dit geval kunt nog steeds Hallo-waarde in Azure AD blijft, maar u deze alleen wijzigen lokale toosomething anders.

> [!WARNING]
> Omdat alle kenmerken in de Azure AD toobe overschreven door Hallo lokale waarde gaat, moet u goed gegevens lokaal. Bijvoorbeeld zo hebt u alleen e-mailadres in Office 365 beheerd en niet bewaard bijgewerkt on-premises AD DS en u eventuele waarden in Azure AD/Office 365 niet aanwezig is in AD DS verliest.

> [!IMPORTANT]
> Als u Wachtwoordsynchronisatie, altijd door de express-instellingen gebruikt wordt, worden Hallo-wachtwoord in Azure AD wordt overschreven met Hallo-wachtwoord in de lokale AD. Als uw gebruikers gebruikte toomanage verschillende wachtwoorden, zijn moet u tooinform Hallo ze die moeten worden gebruikt voor on-premises wachtwoord, wanneer u verbinding hebt geïnstalleerd.

de vorige sectie Hallo en waarschuwing moeten worden overwogen in de planning. Als u veel wijzigingen hebt aangebracht in Azure AD niet doorgevoerd in lokale AD DS, moet u tooplan voor hoe in AD DS Hello toopopulate waarden worden bijgewerkt voordat u uw objecten met Azure AD Connect synchroniseert.

Als u uw objecten met een soft-overeenkomst overeenkomen, Hallo **sourceAnchor** wordt toegevoegd toohello object zodat een vaste overeenkomst later kan worden gebruikt in Azure AD.

### <a name="hard-match-vs-soft-match"></a>Harde-match tegenover Soft-match
Er is geen praktische verschil tussen een soft- en een vaste overeenkomst voor een nieuwe installatie van Connect. Hallo verschil is in een situatie met een herstel na noodgevallen. Als uw server met Azure AD Connect is verbroken, kunt u een nieuw exemplaar opnieuw installeren zonder verlies van gegevens. Een object met een sourceAnchor verzonden tooConnect tijdens de eerste installatie. Hallo overeen kan vervolgens worden geëvalueerd door Hallo-client (Azure AD Connect), die veel sneller dan doen is Hallo dezelfde in Azure AD. Een vaste overeenkomst wordt geëvalueerd door Connect zowel door Azure AD. Een voorlopig overeenkomst wordt alleen geëvalueerd door Azure AD.

### <a name="other-objects-than-users"></a>Andere objecten dan gebruikers
Gebruikers hebben meestal userPrincipalName zowel proxyAddresses, zodat u eenvoudig hello overeen. Maar andere objecten, zoals beveiligingsgroepen, die niet zijn. U kunt in dit geval wordt alleen op een vaste overeenkomst met Hallo sourceAnchor vergelijken. Hallo sourceAnchor is altijd Hallo Base64 geconverteerd **objectGUID** op locatie, dus moet u Hallo-waarde in Azure AD wanneer u twee objecten toomatch moet bijwerken. Hallo sourceAnchor/onveranderbare id genoemd. kan alleen worden bijgewerkt met PowerShell en niet via Hallo portals.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Een nieuwe lokale Active Directory gemaakt van gegevens in Azure AD
Sommige klanten beginnen met een cloud-only-oplossing met Azure AD en hebben geen een on-premises AD. Later ze tooconsume lokale bronnen en toobuild een on-premises AD op basis van Azure AD-gegevens. Azure AD Connect helpen u niet voor dit scenario. Maakt geen gebruikers lokale en hoeft niet elke mogelijkheid tooset Hallo wachtwoord lokale toohello gelijk aan die in Azure AD.

Als Hallo alleen reden waarom u van plan tooadd bent lokale AD toosupport LOB's (Line-of-Business-apps) is, wordt mogelijk moet u rekening houden toouse [Azure AD domain services](../../active-directory-domain-services/index.md) in plaats daarvan.

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
