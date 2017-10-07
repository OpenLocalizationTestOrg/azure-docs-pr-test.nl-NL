---
title: aaaUse groepen toomanage toegang tooresources in Azure Active Directory | Microsoft Docs
description: Hoe toouse groepen in Azure Active Directory toomanage gebruiker toegang krijgen tot tooon-premises en cloudtoepassingen en -bronnen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Tooresources toegang beheren met Azure Active Directory-groepen
Azure Active Directory (Azure AD) is een uitgebreide identiteits- en toegangsbeheer-beheeroplossing die een set krachtige mogelijkheden toomanage toegang tooon-premises en cloudtoepassingen en -bronnen biedt, met inbegrip van Microsoft online services, zoals Office 365 en een wereld van Microsoft SaaS-toepassingen. In dit artikel biedt een overzicht, maar als u wilt gebruikmaken van Azure AD toostart nu groepen, volg de instructies in Hallo [beveiligingsgroepen beheren in Azure AD](active-directory-accessmanagement-manage-groups.md). Als u wilt dat toosee hoe kunt u PowerShell toomanage groepen in Azure Active directory vindt u meer in [Azure Active Directory-cmdlets voor groepsbeheer](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Azure Active Directory, moet u een Azure-account. Als u geen account hebt, kunt u [aanmelden voor een gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/).
>
>

In Azure AD is een van de belangrijkste functies Hallo Hallo mogelijkheid toomanage toegang tooresources. Deze resources kunnen deel uitmaken van de directory hello, net als bij Hallo machtigingen toomanage objecten door middel van rollen in Hallo directory of resources die externe toohello directory, zoals SaaS-toepassingen, Azure-services, en SharePoint-sites of on-premises bronnen. Er zijn vier manieren waarop die een gebruiker toegang rechten tooa resource kan worden toegewezen:

1. Rechtstreekse toewijzing

    Gebruikers kunnen worden toegewezen rechtstreeks tooa resource op Hallo eigenaar van de bron.
2. Groepslidmaatschap

    Een groep kan worden toegewezen tooa resource Hallo resource-eigenaar en door dit te doen, Hallo leden van die groep toegang toohello bron verlenen. Lidmaatschap van groep Hallo kan vervolgens worden beheerd door de eigenaar van de Hallo van Hallo-groep. Hallo resource eigenaar gemachtigden Hallo effectief machtiging tooassign gebruikers tootheir resource toohello eigenaar van Hallo-groep.
3. Op basis van een regel

    de resource-eigenaar Hallo kunt een regel tooexpress welke gebruikers toegang tooa resource moeten worden toegewezen. Hallo uitkomst van de regel hello, is afhankelijk van Hallo kenmerken in die regel en hun waarden gebruikt voor specifieke gebruikers en doet, Hallo resource effectief delegeert Hallo rechts toomanage toegang tootheir resource toohello gezaghebbende bron voor de Hallo kenmerken die worden gebruikt in Hallo regel. Hallo regel zelf beheert nog steeds Hallo resource-eigenaar en te bepalen welke kenmerken en waarden toegang tootheir resource bieden.
4. Externe authority

    Hallo toegang tooa resource is afgeleid van een externe bron; bijvoorbeeld, een groep die worden gesynchroniseerd vanuit een gezaghebbende bron, zoals een on-premises adreslijst of een SaaS-app zoals werkdag. de resource-eigenaar Hallo Hallo groep tooprovide toegang toohello resource wordt toegewezen en Hallo externe bron beheert Hallo leden van Hallo groep.

   ![Overzicht van diagram voor het beheren van toegang](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Bekijk een video waarin wordt uitgelegd toegangsbeheer
U kunt een korte video met uitleg over meer over deze bekijken:

**Azure AD: Inleiding toodynamic lidmaatschap voor groepen**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Hoe heeft toegang tot beheer in Azure Active Directory work?
Midden van Hallo oplossing voor het beheer van een Azure AD is Hallo Hallo-beveiligingsgroep. Met behulp van een security group toomanage toegang tooresources is een bekende paradigma, waardoor een flexibele en begrijpelijke manier tooprovide toegang tooa resource voor Hallo bedoeld groep gebruikers. de resource-eigenaar hello (of Hallo beheerder van Hallo directory) kunt toewijzen een groep tooprovide een bepaalde toegang rechts toohello bronnen die ze eigenaar. leden van de groep Hallo HALLO hallo toegang worden verstrekt en Hallo resource-eigenaar kunt Hallo rechts toomanage Hallo ledenlijst van een groep toosomeone anders, zoals een afdeling of een sitebeheerder helpdesk delegeren.

![Azure Active Directory access management-diagram](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

Hallo-eigenaar van een groep kan ook die groep beschikbaar maken voor self-service aanvragen. Hierbij kunt een eindgebruiker zoeken naar en Hallo-groep vinden en kunnen een toojoin aanvraag machtiging tooaccess Hallo resources die worden beheerd via Hallo groep effectief te zoeken. Hallo-eigenaar van Hallo groep kunt Hallo groep instellen zodat join aanvragen automatisch worden goedgekeurd of moeten worden goedgekeurd door de eigenaar van het Hallo van Hallo-groep. Wanneer een gebruiker een aanvraag toojoin een groep, doorgestuurd Hallo deelname-aanvraag toohello eigenaars van Hallo-groep. Als een van de eigenaars Hallo Hallo aanvraag goedkeurt, de aanvragende gebruiker Hallo gewaarschuwd en Hallo gebruiker is lid toohello groep. Als een van de eigenaars Hallo Hallo aanvraag weigert, wordt de aanvragende gebruiker hello wordt geïnformeerd maar toohello groep niet is toegevoegd.

## <a name="getting-started-with-access-management"></a>Aan de slag met toegangsbeheer
Gereed tooget gestart? Probeer een aantal van Hallo basistaken uitvoeren die u met Azure AD-groepen doen kunt. Gebruik deze mogelijkheden tooprovide gespecialiseerde access toodifferent groepen mensen voor verschillende resources in uw organisatie. Een lijst met eerste basisstappen worden hieronder vermeld.

* [Maken van een eenvoudige regel tooconfigure dynamisch lidmaatschap voor een groep](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Met behulp van een groep toomanage access tooSaaS-toepassingen](active-directory-accessmanagement-group-saasapps.md)
* [Een groep maken beschikbaar voor eindgebruikers selfservice](active-directory-accessmanagement-self-service-group-management.md)
* [Synchroniseren van een lokale groep tooAzure met Azure AD Connect](active-directory-aadconnect.md)
* [Eigenaars voor een groep beheren](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt begrepen Hallo basisprincipes van beheer van toegang, zijn hier enkele aanvullende geavanceerde mogelijkheden beschikbaar in Azure Active Directory voor het beheren van toegang tooyour toepassingen en bronnen.

* [Met behulp van geavanceerde regels toocreate kenmerken](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Beveiligingsgroepen beheren in Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Toegewezen groepen instellen in Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Graph API-verwijzing voor groepen](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
