---
title: Azure AD + Active Directory-vereisten voor Azure RemoteApp | Microsoft Docs
description: Informatie over het instellen van Active Directory om te werken met Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure AD + Active Directory-vereisten voor Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Voor uw Azure RemoteApp hybride verzameling of voor een cloudverzameling die u wilt federeren met AD Connect, moet u het volgende te doen.

### <a name="connect-azure-ad-and-active-directory"></a>Azure AD Connect en Active Directory
Als u verbinding maken met uw Azure AD-tenant en uw on-premises Active Directory-omgevingen wilt, gebruikt u AD Connect. Het duurt u alleen [4 klikken](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) verbinding van de twee directory's.

Houd er rekening mee - Directory-synchronisatie is vereist voor hybride verzamelingen.

### <a name="make-sure-your-domaincom-match"></a>Zorg ervoor dat uw '@domain.com' overeen met
Voordat u begint, controleert u of de UPN voor het lokale forest overeenkomt met het achtervoegsel van uw Azure AD-domein. 

Na het instellen van het domein UPN-achtervoegsel in Azure AD alle gebruikers aan te melden bij Azure RemoteApp wordt aanmelden als ' gebruiker @<the suffix you set up>. " Zorg ervoor dat gebruikers zich ook met dezelfde aanmelden kunnen user@suffix in het lokale domein. In bepaalde gevallen kunt u een domeinnaam instellen in Azure AD tijdens het opgeven van een ander domeinachtervoegsel voor de gebruiker op-premises. In dit geval uw gebruikers niet mogelijk verbinding maken met alle domeincomputers of resources via Azure RemoteApp.

Bijvoorbeeld, als u uw domein UPN-achtervoegsel in van AAD als contoso.com hebt ingesteld, maar sommige gebruikers op lokale/AD zijn geconfigureerd voor logboekregistratie met @contoso.uk, kan die gebruikers niet correct aanmelden bij de ARA-verzameling. Gebruikers UPN in AAD en AD moet hetzelfde zijn voor de aanmelding mogelijk'

### <a name="create-objects-for-azure-remoteapp"></a>Maken van objecten voor Azure RemoteApp
U moet ook de volgende on-premises Active Directory-objecten maken:

* Een serviceaccount om toegang te bieden tot domeinbronnen voor RemoteApp-programma's door RDSH-eindpunten toevoegen aan het lokale-domein.
* Een organisatie-eenheid (OE) RemoteApp machineobjecten bevatten. Gebruik van de organisatie-eenheid wordt aanbevolen (maar niet vereist) voor het isoleren van de accounts en beleidsregels die u met RemoteApp gebruiken wilt.

U moet deze beide objecten bij het maken van uw RemoteApp-collectie moet deze stappen eerst doen.

