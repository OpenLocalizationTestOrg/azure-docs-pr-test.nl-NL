---
title: ontwikkelaarsaccounts aaaManage met behulp van groepen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toomanage developer gebruikersaccounts via groepen in Azure API Management
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Hoe toocreate en gebruik groepen toomanage developer accounts in Azure API Management
Groepen zijn in API Management gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers. Producten zijn eerste aangebracht zichtbaar toogroups, en vervolgens ontwikkelaars in deze groepen kunnen weergeven en zich abonneren toohello producten die gekoppeld aan het Hallo-groepen zijn. 

API Management heeft Hallo volgende onveranderbare systeemgroepen.

* **Beheerders** - Azure-abonnementbeheerders zijn lid van deze groep. Beheerders beheren service-exemplaren van API Management, maken Hallo-API's, bewerkingen en producten die worden gebruikt door ontwikkelaars.
* **Ontwikkelaars** - Geverifieerde gebruikers van de ontwikkelaarsportal vallen in deze groep. Ontwikkelaars zijn Hallo-klanten die toepassingen bouwen met uw API's. Ontwikkelaars krijgen toegang toohello ontwikkelaarsportal en bouwen toepassingen waarmee Hallo bewerkingen van een API aanroepen.
* **Gasten** -niet-geverifieerde gebruikers van de ontwikkelaarsportal, zoals potentiële klanten bezoeken Hallo-portal voor ontwikkelaars een API Management-exemplaar vallen in deze groep. Ze kunnen bepaalde alleen-lezen toegang zoals Hallo mogelijkheid tooview API's worden verleend, maar deze niet aanroepen.

In aanvulling toothese systeemgroepen kunnen beheerders aangepaste groepen maken of [gebruikmaken van externe groepen in gekoppelde Azure Active Directory-tenants][leverage external groups in associated Azure Active Directory tenants]. Aangepaste en externe groepen kunnen worden gebruikt naast systeemgroepen waardoor ontwikkelaars zichtbaarheid en toegang tot tooAPI producten. U kunt bijvoorbeeld één aangepaste groep maken voor ontwikkelaars die zijn gekoppeld aan een specifieke bronpartnerorganisatie en toegang toestaan toohello API's van een product dat alleen relevante API's bevat. Een gebruiker kan lid zijn van meerdere groepen.

Deze handleiding wordt getoond hoe beheerders van een exemplaar van API Management kunnen nieuwe groepen toevoegen en koppel deze aan de producten en -ontwikkelaars.

> [!NOTE]
> Bovendien toocreating en groepen beheren in de publicatieportal hello, u kunt groepen maken en beheren uw Hallo API Management REST-API met [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.
> 
> 

## <a name="create-group"></a>Een groep maken
toocreate een nieuwe groep, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **groepen** van Hallo **API Management** menu op Hallo links en klik vervolgens op **groep toevoegen**.

![Nieuwe groep toevoegen][api-management-add-group]

Voer een unieke naam voor de groep van Hallo en een optionele beschrijving en klik op **opslaan**.

![Nieuwe groep toevoegen][api-management-add-group-window]

Hallo nieuwe groep wordt weergegeven in Hallo groepen tabblad tooedit hello **naam** of **beschrijving** van Hallo-groep, klikt u op Hallo-naam van groep in de lijst Hallo Hallo. toodelete hello groep, klikt u op **verwijderen**.

![Groep toegevoegd][api-management-new-group]

Nu dat hello groep is gemaakt, kan het worden gekoppeld aan de producten en -ontwikkelaars.

## <a name="associate-group-product"></a>Koppelen van een groep aan een product
tooassociate een groep met een product, klikt u op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op Hallo-naam van de gewenste product Hallo.

![Zichtbaarheid instellen][api-management-add-group-to-product]

Selecteer Hallo **zichtbaarheid** tooadd tabblad en verwijdert u groepen en tooview Hallo huidige groepen voor Hallo product. groepen tooadd of verwijderen, inschakelen of uitschakelen van Hallo selectievakjes uit voor Hallo gewenste groepen en klik op **opslaan**.

![Zichtbaarheid instellen][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd Azure Active Directory-groepen, Zie [hoe tooauthorize developer gebruikersaccounts via Azure Active Directory in Azure API Management](api-management-howto-aad.md).
> 
> groepen van Hallo tooconfigure **zichtbaarheid** tabblad voor een product **groepen beheren**.
> 
> 

Wanneer een product gekoppeld aan een groep is, kunnen ontwikkelaars in die groep weergeven en toohello product abonneren.

## <a name="associate-group-developer"></a>Groepen koppelen aan ontwikkelaars
tooassociate groepen met ontwikkelaars, klikt u op **gebruikers** van Hallo **API Management** menu op Hallo links en Hallo selectievakje naast Hallo ontwikkelaars u tooassociate desgewenst met een groep.

![Developer toogroup toevoegen][api-management-add-group-to-developer]

Zodra Hallo ontwikkelaars zijn geselecteerd gewenst, klikt u op de gewenste groep Hallo in Hallo **tooGroup toevoegen** vervolgkeuzelijst. Ontwikkelaars kunnen worden verwijderd uit groepen met Hallo **verwijderen uit groep** vervolgkeuzelijst. 

![Ontwikkelaars][api-management-add-group-to-developer-saved]

Zodra het Hallo-koppeling tussen Hallo ontwikkelaars en Hallo groep wordt toegevoegd, kunt u deze bekijken in Hallo **gebruikers** tabblad.

## <a name="next-steps"> </a>Volgende stappen
* Als een ontwikkelaar kan tooa groep is toegevoegd, kunnen ze bekijken en zich abonneren toohello producten die zijn gekoppeld aan die groep. Zie voor meer informatie [maken en een product publiceren in Azure API Management][How create and publish a product in Azure API Management],
* Bovendien toocreating en groepen beheren in de publicatieportal hello, u kunt groepen maken en beheren uw Hallo API Management REST-API met [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
