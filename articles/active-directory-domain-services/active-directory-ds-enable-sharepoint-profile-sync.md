---
title: 'Azure Active Directory Domain Services: Ondersteuning voor het gebruikersprofiel SharePoint-service inschakelen | Microsoft Docs'
description: Azure Active Directory Domain Services beheerde domeinen toosupport profielsynchronisatie voor SharePoint-Server configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Een beheerd domein toosupport profielsynchronisatie voor SharePoint-Server configureren
SharePoint Server bevat een User Profile-Service die wordt gebruikt voor synchronisatie van het profiel. tooset up Hallo User Profile-Service, gemachtigd moeten toobe toegekend op Active Directory-domein. Zie voor meer informatie [Active Directory Domain Services-machtigingen voor synchronisatie van het profiel in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

Dit artikel wordt uitgelegd hoe u Azure AD Domain Services beheerde domeinen toodeploy Hallo synchronisatie van SharePoint Server gebruikersprofielen service kunt configureren.

## <a name="hello-aad-dc-service-accounts-group"></a>Hallo AAD DC serviceaccounts groep
Een beveiligingsgroep aangeroepen '**AAD DC-serviceaccounts**' Hallo 'Gebruikers' organisatie-eenheid op uw beheerde domein beschikbaar is. U kunt deze groep in Hallo zien **Active Directory: gebruikers en Computers** MMC-module op uw beheerde domein.

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Leden van deze beveiligingsgroep zijn gedelegeerd Hallo volgende bevoegdheden:
- Hallo 'directorywijzigingen repliceren'-bevoegdheden op Hallo hoofdmap DSE Hallo beheerd domein.
- Hallo 'directorywijzigingen repliceren'-bevoegdheden op Hallo configuratienaamgevingscontext (cn = configuratiecontainer) Hallo beheerd domein.

Deze beveiligingsgroep is ook lid zijn van de ingebouwde groep Hallo **Pre-Windows 2000-compatibele toegang**.

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Uw beheerde domein toosupport synchronisatie van gebruikersprofielen SharePoint-Server inschakelen
U kunt toevoegen Hallo-serviceaccount gebruikt voor SharePoint gebruiker profiel synchronisatie toohello **AAD DC-serviceaccounts** groep. Hallo-account voor synchronisatie opgehaald als gevolg hiervan voldoende bevoegdheden tooreplicate wijzigingen toohello directory. Deze stap in de configuratie kunt SharePoint Server gebruiker profiel sync toowork correct.

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Gerelateerde inhoud
* [Technische documentatie - machtigingen verlenen Active Directory Domain Services voor synchronisatie van het profiel in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
