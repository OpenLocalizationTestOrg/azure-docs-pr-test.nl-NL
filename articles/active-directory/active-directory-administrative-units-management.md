---
title: Voorbeeld van aaaAdministrative eenheden management in Azure Active Directory
description: Administratieve eenheden gebruiken voor meer gedetailleerd overdracht van machtigingen in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Beheer van beheereenheden in Azure AD - openbare preview
In dit artikel beschrijft administratieve eenheden – een nieuwe Azure Active Directory-container van bronnen die kunnen worden gebruikt voor het overdragen van beheerdersmachtigingen via subsets van gebruikers en toepassen van beleid tooa subset van gebruikers. In Azure Active Directory inschakelen administratieve eenheden centrale beheerders toodelegate machtigingen tooregional beheerders of tooset beleid op een gedetailleerd niveau.

Dit is handig in organisaties met onafhankelijke divisies, bijvoorbeeld een grote universiteit bestaat uit veel autonome scholen (Business school, school Engineering, enzovoort) die onafhankelijk van elkaar. Dergelijke afdelingen hebben hun eigen IT-beheerders die toegang te beheren, gebruikers beheren en beleidsregels die specifiek is voor hun deling instellen. Centrale beheerders kunnen verlenen toobe deze afdelingen beheerders machtigingen wilt via Hallo gebruikers in hun specifieke afdelingen. Meer specifiek, kunt het volgende voorbeeld de beheerder van een centrale, bijvoorbeeld een administratieve eenheid voor een bepaalde school (Business school) maken en deze vullen met alleen Hallo zakelijke school gebruikers. Vervolgens kunt de beheerder van een centrale Hallo Business school IT-personeel tooa binnen het bereik van functie, met andere woorden, grant Hallo IT-personeel van Business school-beheerdersmachtigingen alleen via Hallo school beheerdersrechten bedrijfseenheid toevoegen.

> [!IMPORTANT]
> Alleen als u Azure Active Directory Premium inschakelt, kunt u administratieve eenheid bereik beheerdersrollen toewijzen. Zie voor meer informatie [aan de slag met Azure AD Premium](active-directory-get-started-premium.md).
>


Uit oogpunt van Hallo centrale beheerder is een administratieve eenheid een directoryobject dat kan worden gemaakt en gevuld met resources. **In deze preview-versie, kunnen deze resources worden alleen gebruikers.** Zodra u hebt gemaakt en ingevuld, kan Hallo administratieve eenheid worden gebruikt als een bereik toorestrict Hallo gemachtigd alleen via de bronnen die zich bevinden in Hallo administratieve eenheid.

## <a name="managing-administrative-units"></a>Het beheren van administratieve eenheden
U kunt maken en beheren van administratieve eenheden met hello Azure Active Directory-Module voor Windows PowerShell-cmdlets in deze preview-versie. meer informatie over hoe toolearn toodo die Zie [werken met administratieve eenheden](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Zie voor meer informatie over installeren hello Azure AD-module- en softwarevereisten en voor informatie over hello Azure AD-Module-cmdlets voor het beheren van administratieve eenheden, inclusief syntaxis, beschrijvingen van parameters en voorbeelden [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Volgende stappen
[Azure Active Directory-edities](active-directory-editions.md)
