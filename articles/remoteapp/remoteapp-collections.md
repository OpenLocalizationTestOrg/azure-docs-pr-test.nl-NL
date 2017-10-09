---
title: aaaWhat soort verzameling komen dat u nodig hebt voor Azure RemoteApp? | Microsoft Docs
description: Meer informatie over Hallo typen beschikbaar met Azure RemoteApp-collecties.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>What kind of collection do you need for Azure RemoteApp? (Wat voor verzameling hebt u nodig voor Azure RemoteApp?)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp kunt u apps en resources delen met gebruikers op elk apparaat. We dit doen door verzamelingen toohold Hallo apps en resources te maken en vervolgens het delen van deze verzamelingen met gebruikers. Er zijn 2 andere verzameling opties, met andere netwerk- en verificatieopties - geschikt is voor u?

We doorlopen Hallo andere overwegingen en opties moet u toomake tooget Hallo meest buiten uw Azure RemoteApp-collectie. 

## <a name="quick-differences-between-hello-collection-types"></a>Snelle verschillen tussen Hallo verzamelingtypen
|  | Cloud | Hybride |
| --- | --- | --- |
| Een bestaande VNET gebruiken |Ja |Ja |
| Zijn verbonden met een AD-accounts (DirSync) vereist |Nee |Ja |
| Domein is vereist |Nee |Ja |
| Domain controller toegankelijk tooVNET vereist |Nee |Ja |

## <a name="cloud-collections"></a>Cloudverzamelingen
* Snelle toocreate - Hallo verzameling is snel ingericht, wat betekent dat uw apps ophalen toousers sneller.
* Breng uw eigen apps of onze delen. U kunt een aangepaste installatiekopie (gebouwd op basis van een Azure VM) of een van Hallo installatiekopieën die zijn opgenomen in uw abonnement gebruiken.
* U hoeft niet tooconfigure een verbinding tussen uw verzameling en het lokale domein.
* Maar u kunt desgewenst uw eigen Azure VNET tooprovide toegang in uw on-premises omgeving gebruiken voor gegevens delen of toouse niet-Windows-verificatie in bronnen zoals SQL Server (met behulp van de database-verificatie).

OK klikt, hoe maak ik een?

* Alleen cloud? Maak Hello **snelle invoer** optie in Hallo-portal.
* Cloud + VNET? Maak met behulp van Hallo **maken met VNET** optie, maar geen gekozen toojoin een domein.

## <a name="hybrid-collections"></a>Hybride verzamelingen
* Geef de volledige toegang tooon-premises netwerk + Azure VNET.
* Domain join-toegang voor apps en gegevens bevat. Externe toepassingen kunnen verificatie op basis van uw lokale Active Directory - ze vervolgens toegang krijgen tot bronnen in uw domein.
* Geavanceerde bewaking en beheer met bestaande System Center-oplossingen en het Windows-groepsbeleid (via een aangepaste installatiekopie die is gebaseerd op Windows Server 2012 R2) inschakelen
* Ondersteuning voor [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect uw Azure VNET tooyour lokale VNET.

Maak met behulp van Hallo **maken met VNET** optie en kies toojoin een domein.

## <a name="authentication-options"></a>Verificatieopties
Azure RemoteApp biedt ondersteuning voor zowel Microsoft-accounts en Azure Active Directory-accounts, maar niet alle verzamelingen bieden ondersteuning voor alle methoden. 

| Accounttype |  | Cloud | Cloud + VNET | Hybride |
| --- | --- | --- | --- | --- |
| Microsoft-account | |Ja |Ja |Nee |
| Azure Active Directory (Azure AD) | | | | |
| Alleen Azure AD |Ja |Ja |Nee | |
| AD Connect met Wachtwoordsynchronisatie |Ja |Ja |Ja | |
| AD Connect zonder Wachtwoordsynchronisatie |Ja |Ja |Nee | |
| AD Connect met AD FS |Ja |Ja |Ja | |
| 3rd van derden door Azure ondersteunde identiteitsproviders (zoals Ping) |Ja |Ja |Ja | |
| Meervoudige verificatie | |Ja |Ja |Ja |

### <a name="cloud-and-cloud--vnet"></a>Cloud- en Cloud- + VNET
U kunt Microsoft-accounts, Azure AD-accounts of een combinatie van twee hello gebruiken met cloudverzamelingen. Hallo-accounts die geschikt zijn voor uw gebruikers gebruiken.

Er zijn geen specifieke vereisten voor het gebruik van Microsoft-accounts. 

Als u toouse Azure AD-accounts wilt, moet u ervoor dat uw Azure AD-tenant overeenkomt met Hallo die is gekoppeld aan uw abonnement toomake. Wanneer u uw Azure RemoteApp-abonnement hebt gemaakt, is Hallo u Azure AD-tenant automatisch gekoppeld aan uw abonnement. Een Azure AD-gebruiker geeft u toestemming tooneeds toobe diezelfde tenant. Indien nodig, kunt u [hello Azure AD-tenant wijzigen](remoteapp-changetenant.md) gekoppeld aan uw abonnement.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Hybride (of cloud + Azure AD + AD)
Met behulp van Azure AD + lokale Active Directory is een vereiste voor een hybride verzameling. U moet toouse AD Connect toointegrate Hallo twee directory's. Maar u hebt een keuze bij het configureren van AD Connect toohow. 

Er zijn 2 AD Connect-scenario's - met Wachtwoordsynchronisatie of Federatie met AD. Bekijk Hallo [AD Connect informatie](../active-directory/active-directory-aadconnect.md) toofigure uit die deze het meest geschikt voor u.

U kunt ook Azure AD + AD met een cloudverzameling gebruiken. Zorg ervoor dat u dezelfde stappen instellen Hallo volgen.

Bekijk [Azure AD + Active Directory-vereisten voor Azure RemoteApp](remoteapp-ad.md) voor Hallo stappen vereist tooconfigure Azure AD en Active Directory.

## <a name="go-create-your-collection"></a>Aan de slag uw verzameling maken
Ik denk OK klikt, dat we hebt gekeken deze hoe nu, zodat er slechts één ding links toodo: uw eerste Azure RemoteApp-collectie maken.

[Een cloudverzameling maken](remoteapp-create-cloud-deployment.md) of [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) -ophalen maken.

