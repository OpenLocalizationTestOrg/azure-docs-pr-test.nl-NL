---
title: aaaHow tooAssign gebruikers tooapplications | Microsoft Docs
description: Begrijpen hoe gebruikers tooan toepassing in uw tenant worden toegewezen
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Hoe tooassign gebruikers tooapplications

In dit artikel kunt u toounderstand hoe gebruikers tooan toepassing in uw tenant worden toegewezen.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Hoe gebruikers worden toegewezen tooan toepassing in Azure AD?

Voor een gebruiker tooaccess een toepassing, moet eerst worden toegewezen tooit op een bepaalde manier. Toewijzing kan worden uitgevoerd door een beheerder, een zakelijke gemachtigde of soms Hallo gebruiker zelf. Hieronder worden beschreven Hallo manieren gebruikers tooapplications kunnen worden toegewezen:

1.  Een beheerder [wijst een gebruiker](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) rechtstreeks toohello-toepassing

2.  Een beheerder [wijst een groep](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) die Hallo gebruiker lid is van toepassing toohello, met inbegrip van:

  * Een groep die on-premises is gesynchroniseerd

  * Een statische beveiligingsgroep gemaakt in de cloud Hallo

  * Een [dynamische beveiligingsgroep](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) gemaakt in de cloud Hallo

  * Een Office 365-groep gemaakt in de cloud Hallo

  * Hallo [alle gebruikers](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) groep

3.  Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow een gebruiker tooadd wordt gebruikt door een toepassing hello [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** functie **zonder goedkeuring van bedrijven**

4.  Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow een gebruiker tooadd wordt gebruikt door een toepassing hello [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** onderdeel, maar alleen toestaan **ith voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**

5.  Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow de toojoin van een gebruiker een groep die een toepassing is toegewezen, te**zonder goedkeuring van bedrijven**

6.  Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow de toojoin van een gebruiker een groep die een toepassing is toegewezen aan, maar alleen **met voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**

7.  Een beheerder wijst een gebruiker van de licentie tooa rechtstreeks voor een eerste toepassing van derden, zoals [Microsoft Office 365](http://products.office.com/)

8.  Een beheerder wijst een licentiegroep tooa die Hallo gebruiker lid is van tooa eerste of een toepassing, zoals [Microsoft Office 365](http://products.office.com/)

9.  Een [beheerder instemt tooan toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe gebruikt door alle gebruikers en vervolgens een gebruiker zich aanmeldt toohello toepassing

10. Een gebruiker [tooan toepassing instemt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) zelf wanneer u zich aanmeldt in toohello toepassing

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)
