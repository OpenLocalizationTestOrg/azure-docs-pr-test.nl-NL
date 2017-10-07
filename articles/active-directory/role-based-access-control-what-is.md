---
title: aaaManage toegang en machtigingen met RBAC - Azure RBAC | Microsoft Docs
description: In het beheer van toegang aan de slag met op rollen gebaseerde toegangsbeheer van Azure in hello Azure-Portal. Gebruik de rol toewijzingen tooassign machtigingen in uw directory.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Aan de slag met toegangsbeheer op basis van rollen in hello Azure-portal
Beveiliging gerichte bedrijven moeten zich richten op uw werknemers Hallo exacte machtigingen die ze nodig hebben. Te veel machtigingen kunnen een account tooattackers worden blootgesteld. Te weinig machtigingen betekent dat werknemers hun werk efficiënt kunnen niet ophalen. Azure op rollen gebaseerde toegangsbeheer (RBAC) kunt u dit probleem oplossen door het aanbieden van Geavanceerd toegangsbeheer voor Azure.

Met RBAC kunt u taken scheiden binnen uw team en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk. In plaats van iedereen geven onbeperkte machtigingen in uw Azure-abonnement of de bronnen, kunt u alleen bepaalde acties. Bijvoorbeeld gebruik RBAC toolet één werknemer virtuele machines in een abonnement beheren, terwijl andere kunt beheren van SQL-databases binnen Hallo hetzelfde abonnement.

## <a name="basics-of-access-management-in-azure"></a>Basisprincipes van toegangsbeheer in Azure
Elk Azure-abonnement is gekoppeld aan één map op Azure Active Directory (AD). Gebruikers, groepen en toepassingen van die directory kunnen resources in hello Azure-abonnement te beheren. Deze toegangsrechten met hello Azure-portal, Azure-opdrachtregelprogramma's en Azure Management-API's toewijzen.

Toegang verlenen door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen op een bepaalde scope. Hallo-bereik van een roltoewijzing kan dit een abonnement, een resourcegroep of één resource. Een rol die is toegewezen aan een bovenliggend bereik verleent toegang ook toohello onderliggende items erin opgenomen. Een gebruiker met toegang tooa resourcegroep kunt bijvoorbeeld alle Hallo resources, zoals websites, virtuele machines en subnetten bevat te beheren.

![Relatie tussen de elementen van de Azure Active Directory - diagram](./media/role-based-access-control-what-is/rbac_aad.png)

Hallo RBAC-rol die u toewijst, bepaalt welke resources Hallo gebruiker, groep of toepassing binnen dat bereik kunt beheren.

## <a name="built-in-roles"></a>Ingebouwde rollen
Azure RBAC heeft drie basic rollen die tooall brontypen die van toepassing:

* **Eigenaar** heeft volledige toegang tooall bronnen, met inbegrip van Hallo rechts toodelegate toegang tooothers.
* **Inzender** kunt maken en beheren van alle soorten Azure-resources, maar kan geen tooothers toegang verlenen.
* **Lezer** bestaande Azure-resources kunt weergeven.

Hallo rest van Hallo RBAC-rollen in Azure toestaan van beheer van specifieke Azure-resources. Bijvoorbeeld, Hallo rol van inzender van de virtuele Machine kunt Hallo gebruiker toocreate en beheren van virtuele machines. Deze geeft geen ze toegang tot het virtuele netwerk toohello of Hallo-subnet dat Hallo van virtuele machine verbinding maakt. 

[Ingebouwde RBAC-rollen](role-based-access-built-in-roles.md) lijsten Hallo functies die beschikbaar zijn in Azure. Deze geeft Hallo bewerkingen en het bereik dat elke ingebouwde rol toousers verleent. Als u op zoek bent toodefine uw eigen rollen voor nog meer controle, Zie hoe toobuild [aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Resource-hiërarchie en de toegang overname
* Elke **abonnement** behoort tooonly één map in Azure. (Maar elke directory kan meer dan één abonnement hebt.)
* Elke **resourcegroep** tooonly één abonnement behoort.
* Elke **resource** tooonly één resourcegroep behoort.

Toegang waarmee u op de bovenliggende scopes wordt verleend wordt op een onderliggend bereik overgenomen. Bijvoorbeeld:

* U toewijzen Hallo lezer rol tooan Azure AD-groep op Hallo abonnementsbereik. Hallo-leden van die groep kunnen elk van de resourcegroep en resource weergeven in Hallo-abonnement.
* U toewijzen Hallo Inzender rol tooan toepassing op Hallo resource groepsbereik. Deze kunt resources van alle typen in die resourcegroep, maar geen andere resourcegroepen in Hallo abonnement beheren.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Azure RBAC versus klassieke abonnementbeheerders
Klassieke abonnementsbeheerders mensen en co-beheerders hebben volledige toegang toohello Azure-abonnement. Ze kunnen resources met behulp van Hallo beheren [Azure-portal](https://portal.azure.com) met Azure Resource Manager-API's of Hallo [klassieke Azure-portal](https://manage.windowsazure.com) en Azure klassieke implementatiemodel. In Hallo RBAC-model, klassieke administrators rol van eigenaar Hallo bij Hallo abonnementsbereik toegewezen.

Alleen hello Azure-portal en nieuwe Azure Resource Manager-API's ondersteuning Azure RBAC Hallo. Gebruikers en toepassingen die zijn toegewezen RBAC-rollen Hallo-classic-beheerportal en hello Azure klassieke implementatiemodel niet gebruiken.

## <a name="authorization-for-management-vs-data-operations"></a>Autorisatie voor het beheer van versus gegevensbewerkingen
Azure RBAC alleen ondersteunt beheerbewerkingen van Azure-resources in Hallo hello Azure portal en Azure Resource Manager-API's. Deze kan niet toestaan dat alle gegevens niveau bewerkingen voor Azure-resources. Bijvoorbeeld, kunt u autoriseren iemand toomanage Storage-Accounts, maar niet toohello blobs of tabellen binnen een Opslagaccount. Op deze manier een SQL-database kan worden beheerd, maar niet Hallo tabellen in deze.

## <a name="next-steps"></a>Volgende stappen
* Aan de slag met [toegangsbeheer op basis van rollen in Azure-portal Hallo](role-based-access-control-configure.md).
* Zie Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md)
* Definieer uw eigen [Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)
