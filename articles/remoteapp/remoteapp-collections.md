---
title: What kind of collection do you need for Azure RemoteApp? (Wat voor verzameling hebt u nodig voor Azure RemoteApp?) | Microsoft Docs
description: Meer informatie over de typen beschikbaar zijn met Azure RemoteApp verzamelingen.
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
ms.openlocfilehash: 10f6c0533027767b6635ebff1e6a9872bde06a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>What kind of collection do you need for Azure RemoteApp? (Wat voor verzameling hebt u nodig voor Azure RemoteApp?)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp kunt u apps en resources delen met gebruikers op elk apparaat. We dit doen door het maken van verzamelingen voor het opslaan van de apps en resources en vervolgens het delen van deze verzamelingen met gebruikers. Er zijn 2 andere verzameling opties, met andere netwerk- en verificatieopties - geschikt is voor u?

Laten we helpt u stapsgewijs door de andere overwegingen en de keuzes die u nemen moet voor Haal het meeste uit uw Azure RemoteApp-collectie. 

## <a name="quick-differences-between-the-collection-types"></a>Snelle verschillen tussen deze verzamelingtypen
|  | Cloud | Hybride |
| --- | --- | --- |
| Een bestaande VNET gebruiken |Ja |Ja |
| Zijn verbonden met een AD-accounts (DirSync) vereist |Nee |Ja |
| Domein is vereist |Nee |Ja |
| Domeincontroller toegankelijk is voor VNET vereist |Nee |Ja |

## <a name="cloud-collections"></a>Cloudverzamelingen
* Snel maken - de verzameling snel is ingericht, wat betekent dat uw apps ophalen voor gebruikers sneller.
* Breng uw eigen apps of onze delen. U kunt een aangepaste installatiekopie (gebouwd op basis van een Azure VM) of een van de installatiekopieën die zijn opgenomen in uw abonnement gebruiken.
* U hoeft niet te configureren van een verbinding tussen uw verzameling en het lokale domein.
* Maar u kunt desgewenst uw eigen Azure VNET gebruiken om toegang te bieden in uw on-premises omgeving voor het delen van gegevens of voor het gebruik van niet-Windows-verificatie in bronnen zoals SQL Server (met behulp van de database-verificatie).

OK klikt, hoe maak ik een?

* Alleen cloud? Maak met de **snelle invoer** optie in de portal.
* Cloud + VNET? Maakt met behulp van de **maken met VNET** optie, maar niet wilt toevoegen aan een domein.

## <a name="hybrid-collections"></a>Hybride verzamelingen
* Geef de volledige toegang tot on-premises netwerk + Azure VNET.
* Domain join-toegang voor apps en gegevens bevat. Externe toepassingen kunnen verificatie op basis van uw lokale Active Directory - ze vervolgens toegang krijgen tot bronnen in uw domein.
* Geavanceerde bewaking en beheer met bestaande System Center-oplossingen en het Windows-groepsbeleid (via een aangepaste installatiekopie die is gebaseerd op Windows Server 2012 R2) inschakelen
* Ondersteuning voor [ExpressRoute](https://azure.microsoft.com/services/expressroute/) verbinding maken met uw Azure VNET uw lokale VNET.

Maakt met behulp van de **maken met VNET** optie en kies toevoegen aan een domein.

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
U kunt Microsoft-accounts, Azure AD-accounts of een combinatie van beide gebruiken met cloudverzamelingen. Gebruik de accounts die geschikt zijn voor uw gebruikers.

Er zijn geen specifieke vereisten voor het gebruik van Microsoft-accounts. 

Als u gebruiken van Azure AD-accounts wilt, moet u ervoor zorgen dat uw Azure AD-tenant, overeenkomt met de naam gekoppeld aan uw abonnement. Wanneer u uw Azure RemoteApp-abonnement hebt gemaakt, is de Azure AD-tenant die u gebruikte automatisch gekoppeld aan uw abonnement. Een Azure AD-gebruiker om op te machtigen moet diezelfde tenant. Indien nodig, kunt u [wijzigen van de Azure AD-tenant](remoteapp-changetenant.md) gekoppeld aan uw abonnement.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Hybride (of cloud + Azure AD + AD)
Met behulp van Azure AD + lokale Active Directory is een vereiste voor een hybride verzameling. U moet AD Connect gebruiken voor het integreren van de twee directory's. Maar u hebt een keuze als het gaat om de configuratie van AD Connect. 

Er zijn 2 AD Connect-scenario's - met Wachtwoordsynchronisatie of Federatie met AD. Bekijk de [AD Connect informatie](../active-directory/active-directory-aadconnect.md) om te achterhalen welke van deze works best voor u.

U kunt ook Azure AD + AD met een cloudverzameling gebruiken. Zorg ervoor dat u volgt dezelfde stappen instellen.

Bekijk [Azure AD + Active Directory-vereisten voor Azure RemoteApp](remoteapp-ad.md) voor de stappen die zijn vereist voor het configureren van Azure AD en Active Directory.

## <a name="go-create-your-collection"></a>Aan de slag uw verzameling maken
OK klikt, wordt volgens mij dat hebben we nu uit doorberekend zodat er slechts één ding om te doen: uw eerste Azure RemoteApp-collectie maken.

[Een cloudverzameling maken](remoteapp-create-cloud-deployment.md) of [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) -ophalen maken.

