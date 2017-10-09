---
title: aaaAzure AD + Active Directory-vereisten voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooset up toowork Active Directory met Azure RemoteApp.
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure AD + Active Directory-vereisten voor Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Uw hybride Azure RemoteApp-verzameling of voor een cloudverzameling die u wilt dat toofederate via AD Connect, moet u toodo Hallo volgende.

### <a name="connect-azure-ad-and-active-directory"></a>Azure AD Connect en Active Directory
Als u tooconnect uw Azure AD-tenant en uw on-premises Active Directory-omgevingen wilt, gebruikt u AD Connect. Het duurt u alleen [4 klikken](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Hallo twee directory's.

Houd er rekening mee - Directory-synchronisatie is vereist voor hybride verzamelingen.

### <a name="make-sure-your-domaincom-match"></a>Zorg ervoor dat uw '@domain.com' overeen met
Voordat u begint, controleert u dat Hallo UPN voor uw lokale forest komt overeen met Hallo achtervoegsel van uw Azure AD-domein. 

Na het instellen van Hallo UPN domeinachtervoegsel in Azure AD alle gebruikers aan te melden bij Azure RemoteApp wordt aanmelden als ' gebruiker @<hello suffix you set up>. " Zorg ervoor dat gebruikers ook met Hallo dezelfde aanmelden kunnen user@suffix in Hallo lokaal domein. In bepaalde gevallen kunt u een domeinnaam instellen in Azure AD tijdens het opgeven van een ander domeinachtervoegsel voor Hallo gebruiker op-premises. In dit geval uw gebruikers niet kunnen tooconnect tooany Domeincomputers of resources via Azure RemoteApp.

Bijvoorbeeld, als u uw domein UPN-achtervoegsel in van AAD als contoso.com hebt ingesteld, maar sommige gebruikers op lokale/AD zijn geconfigureerde toolog met @contoso.uk, kan die gebruikers niet kunnen toocorrectly Meld u aan bij Hallo ARA-verzameling. Gebruikers die UPN in AAD en AD moet hello dezelfde voor Hallo aanmelding toobe mogelijk"

### <a name="create-objects-for-azure-remoteapp"></a>Maken van objecten voor Azure RemoteApp
U moet ook toocreate Hallo lokale Active Directory-objecten te volgen:

* Een service-account tooprovide toodomain hulpmiddelen voor RemoteApp-programma's door RDSH eindpunten toohello lokaal domein.
* Een organisatie-eenheid (OE) toocontain RemoteApp-machineobjecten. Gebruik van Hallo organisatie-eenheid is aanbevolen (maar niet vereist) tooisolate Hallo accounts en beleidsregels die u met RemoteApp gebruiken wilt.

U moet deze beide objecten bij het maken van uw RemoteApp-collectie, dus wees zeker toodo deze stappen eerst.

