---
title: Een gebruiker toevoegen aan uw Azure RemoteApp-collectie | Microsoft Docs
description: Informatie over het toevoegen van gebruikers aan uw Azure RemoteApp-verzameling
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>Een gebruiker toevoegen aan uw Azure RemoteApp-verzameling
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Voordat u uw gebruikers kunnen zien en gebruiken van uw apps in Azure RemoteApp, die u moet ze toegang verlenen tot uw verzameling. Dit is het eenvoudig gedeelte: op de **gebruikerstoegang** tabblad, voer de accountgegevens voor de gebruiker en klik vervolgens op het vinkje.

Welke accountgegevens hebt u nodig? Die afhankelijk is van het type van verzameling u hebt gemaakt (cloud of hybride) en of u gebruikmaakt van Office 365 ProPlus in die verzameling.

## <a name="supported-user-identities"></a>Ondersteunde gebruikers-id 's
De van verschillende verzamelingtypen (cloud versus hybride) ondersteuning voor het gebruik van andere gebruikers-id's voor toegang tot toepassingen.  

Voor een hybride verzameling van RemoteApp moet u een Active Directory-domein-infrastructuur lokale en een Azure Active Directory-tenant met Active Directory-integratie instellen (en desgewenst eenmalige aanmelding). Bovendien moet u enkele Active Directory-objecten maken in de on-premises directory.  

Voor een cloudverzameling van RemoteApp, kan elke gebruiker met Azure Active Directory ondersteuning voor identiteiten gebruikerstoegang worden toegekend aan RemoteApp om op te nemen van Microsoft-Accounts.  Zie de onderstaande tabel.

Office 365-gebruikers zijn Azure Active Directory-gebruikers. Als ze hybride Azure Active Directory hebt, kunnen Directory-accounts gesynchroniseerd ze gebruikerstoegang krijgen in een hybride implementatie van RemoteApp.   

U kunt deze tabel gebruiken als naslag waarvoor de identiteit die wordt ondersteund in de verzameling en wat de vereisten voor Active Directory zijn.

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
> De Azure Active Directory-gebruikers moeten afkomstig zijn van de tenant die aan uw abonnement is gekoppeld. (U kunt uw abonnement bekijken en wijzigen op het tabblad **Instellingen** in de portal. Zie [De Azure Active Directory-tenant wijzigen die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informatie over Office 365 ProPlus gebruikersaccount
Als u de Office 365 ProPlus-sjablooninstallatiekopie in uw verzameling gebruikt *of* als u een aangepaste installatiekopie die gebruikmaakt van Office 365 hebt gemaakt, mogen u alleen Azure Active Directory-gebruikers met Office 365-abonnementen voor het standaarddomein van uw abonnement toe te voegen. Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie.

