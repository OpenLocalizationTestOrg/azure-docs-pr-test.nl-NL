---
title: een gebruiker tooyour Azure RemoteApp-verzameling aaaAdd | Microsoft Docs
description: Meer informatie over hoe tooadd gebruikers tooyour Azure RemoteApp-verzameling
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Hoe tooadd een gebruiker tooyour Azure RemoteApp-verzameling
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Voordat u uw gebruikers kunnen zien en gebruiken van uw apps in Azure RemoteApp, hebben ze toegang krijgen tot tooyour verzameling toogrant. Dit is een eenvoudig onderdeel Hallo: op Hallo **gebruikerstoegang** tabblad, Voer Hallo accountgegevens voor de gebruiker Hallo en klik vervolgens op het vinkje Hallo.

Welke accountgegevens hebt u nodig? Dat hangt Hallo type verzameling u hebt gemaakt (cloud of hybride) en of u gebruikmaakt van Office 365 ProPlus in die verzameling.

## <a name="supported-user-identities"></a>Ondersteunde gebruikers-id 's
Hallo verschillende verzamelingtypen (cloud versus hybride) ondersteuning voor het gebruik van andere gebruikers-id's voor toegang tot tooapplications.  

Voor een hybride verzameling van RemoteApp, u moet tooset van een infrastructuur voor Active Directory-domein lokale en een Azure Active Directory-tenant met Active Directory-integratie (en desgewenst eenmalige aanmelding). Bovendien moet u toocreate sommige Active Directory-objecten in Hallo on-premises adreslijst.  

Voor een cloudverzameling van RemoteApp, kan elke gebruiker met Azure Active Directory ondersteuning voor identiteiten gebruiker toegang tooRemoteApp tooinclude Microsoft-Accounts worden verleend.  Zie de onderstaande tabel voor Hallo.

Office 365-gebruikers zijn Azure Active Directory-gebruikers. Als ze hybride Azure Active Directory hebt, kunnen Directory-accounts gesynchroniseerd ze gebruikerstoegang krijgen in een hybride implementatie van RemoteApp.   

U kunt deze tabel gebruiken als naslag waarvoor de identiteit die wordt ondersteund in de verzameling en wat Hallo Active Directory-vereisten zijn.

| Gebruikersaccounts | Cloud | Hybride |
| --- | --- | --- |
| Microsoft-account |Ja |Nee |
| Azure Active Directory (Azure AD) | | |
| Azure AD cloud |Ja |Nee |
| ADsync met Wachtwoordsynchronisatie |Ja |Ja |
| ADsync zonder Wachtwoordsynchronisatie |Ja |Nee |
| ADsync met AD FS |Ja |Ja |
| [3rd van derden door Azure ondersteunde identiteitsproviders](https://msdn.microsoft.com/library/azure/jj679342.aspx) (voorbeeld Ping) |Ja |Ja |
| Meervoudige verificatie |Ja |Ja |

Bekijk [meer informatie](remoteapp-ad.md) over het configureren van Active Directory voor RemoteApp.

> [!NOTE]
> Hello Azure Active Directory-gebruikers moeten uit Hallo-tenant die gekoppeld is aan uw abonnement. (U kunt bekijken en wijzigen van uw abonnement op Hallo **instellingen** tabblad in Hallo-portal. Zie [wijziging hello Azure Active Directory-tenant die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informatie over Office 365 ProPlus gebruikersaccount
Als u Office 365 ProPlus Hallo-sjablooninstallatiekopie in uw verzameling gebruikt *of* als u een aangepaste installatiekopie die gebruikmaakt van Office 365 hebt gemaakt, u mogen alleen tooadd Azure Active Directory-gebruikers die Office 365-abonnementen voor Hallo hebben standaarddomein van uw abonnement. Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie.

