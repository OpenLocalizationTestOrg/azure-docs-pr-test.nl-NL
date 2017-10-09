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
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="38056-103">Hoe toocreate en gebruik groepen toomanage developer accounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="38056-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="38056-104">Groepen zijn in API Management gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="38056-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="38056-105">Producten zijn eerste aangebracht zichtbaar toogroups, en vervolgens ontwikkelaars in deze groepen kunnen weergeven en zich abonneren toohello producten die gekoppeld aan het Hallo-groepen zijn.</span><span class="sxs-lookup"><span data-stu-id="38056-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="38056-106">API Management heeft Hallo volgende onveranderbare systeemgroepen.</span><span class="sxs-lookup"><span data-stu-id="38056-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="38056-107">**Beheerders** - Azure-abonnementbeheerders zijn lid van deze groep.</span><span class="sxs-lookup"><span data-stu-id="38056-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="38056-108">Beheerders beheren service-exemplaren van API Management, maken Hallo-API's, bewerkingen en producten die worden gebruikt door ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38056-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="38056-109">**Ontwikkelaars** - Geverifieerde gebruikers van de ontwikkelaarsportal vallen in deze groep.</span><span class="sxs-lookup"><span data-stu-id="38056-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="38056-110">Ontwikkelaars zijn Hallo-klanten die toepassingen bouwen met uw API's.</span><span class="sxs-lookup"><span data-stu-id="38056-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="38056-111">Ontwikkelaars krijgen toegang toohello ontwikkelaarsportal en bouwen toepassingen waarmee Hallo bewerkingen van een API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="38056-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="38056-112">**Gasten** -niet-geverifieerde gebruikers van de ontwikkelaarsportal, zoals potentiële klanten bezoeken Hallo-portal voor ontwikkelaars een API Management-exemplaar vallen in deze groep.</span><span class="sxs-lookup"><span data-stu-id="38056-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="38056-113">Ze kunnen bepaalde alleen-lezen toegang zoals Hallo mogelijkheid tooview API's worden verleend, maar deze niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="38056-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="38056-114">In aanvulling toothese systeemgroepen kunnen beheerders aangepaste groepen maken of [gebruikmaken van externe groepen in gekoppelde Azure Active Directory-tenants][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="38056-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="38056-115">Aangepaste en externe groepen kunnen worden gebruikt naast systeemgroepen waardoor ontwikkelaars zichtbaarheid en toegang tot tooAPI producten.</span><span class="sxs-lookup"><span data-stu-id="38056-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="38056-116">U kunt bijvoorbeeld één aangepaste groep maken voor ontwikkelaars die zijn gekoppeld aan een specifieke bronpartnerorganisatie en toegang toestaan toohello API's van een product dat alleen relevante API's bevat.</span><span class="sxs-lookup"><span data-stu-id="38056-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="38056-117">Een gebruiker kan lid zijn van meerdere groepen.</span><span class="sxs-lookup"><span data-stu-id="38056-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="38056-118">Deze handleiding wordt getoond hoe beheerders van een exemplaar van API Management kunnen nieuwe groepen toevoegen en koppel deze aan de producten en -ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38056-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="38056-119">Bovendien toocreating en groepen beheren in de publicatieportal hello, u kunt groepen maken en beheren uw Hallo API Management REST-API met [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.</span><span class="sxs-lookup"><span data-stu-id="38056-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="38056-120"><a name="create-group"></a>Een groep maken</span><span class="sxs-lookup"><span data-stu-id="38056-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="38056-121">toocreate een nieuwe groep, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="38056-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="38056-122">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="38056-122">This takes you toohello API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="38056-124">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38056-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="38056-125">Klik op **groepen** van Hallo **API Management** menu op Hallo links en klik vervolgens op **groep toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="38056-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Nieuwe groep toevoegen][api-management-add-group]

<span data-ttu-id="38056-127">Voer een unieke naam voor de groep van Hallo en een optionele beschrijving en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38056-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Nieuwe groep toevoegen][api-management-add-group-window]

<span data-ttu-id="38056-129">Hallo nieuwe groep wordt weergegeven in Hallo groepen tabblad tooedit hello **naam** of **beschrijving** van Hallo-groep, klikt u op Hallo-naam van groep in de lijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="38056-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="38056-130">toodelete hello groep, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="38056-130">toodelete hello group, click **Delete**.</span></span>

![Groep toegevoegd][api-management-new-group]

<span data-ttu-id="38056-132">Nu dat hello groep is gemaakt, kan het worden gekoppeld aan de producten en -ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38056-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="38056-133"><a name="associate-group-product"></a>Koppelen van een groep aan een product</span><span class="sxs-lookup"><span data-stu-id="38056-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="38056-134">tooassociate een groep met een product, klikt u op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op Hallo-naam van de gewenste product Hallo.</span><span class="sxs-lookup"><span data-stu-id="38056-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Zichtbaarheid instellen][api-management-add-group-to-product]

<span data-ttu-id="38056-136">Selecteer Hallo **zichtbaarheid** tooadd tabblad en verwijdert u groepen en tooview Hallo huidige groepen voor Hallo product.</span><span class="sxs-lookup"><span data-stu-id="38056-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="38056-137">groepen tooadd of verwijderen, inschakelen of uitschakelen van Hallo selectievakjes uit voor Hallo gewenste groepen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38056-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Zichtbaarheid instellen][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="38056-139">tooadd Azure Active Directory-groepen, Zie [hoe tooauthorize developer gebruikersaccounts via Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="38056-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="38056-140">groepen van Hallo tooconfigure **zichtbaarheid** tabblad voor een product **groepen beheren**.</span><span class="sxs-lookup"><span data-stu-id="38056-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="38056-141">Wanneer een product gekoppeld aan een groep is, kunnen ontwikkelaars in die groep weergeven en toohello product abonneren.</span><span class="sxs-lookup"><span data-stu-id="38056-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="38056-142"><a name="associate-group-developer"></a>Groepen koppelen aan ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="38056-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="38056-143">tooassociate groepen met ontwikkelaars, klikt u op **gebruikers** van Hallo **API Management** menu op Hallo links en Hallo selectievakje naast Hallo ontwikkelaars u tooassociate desgewenst met een groep.</span><span class="sxs-lookup"><span data-stu-id="38056-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Developer toogroup toevoegen][api-management-add-group-to-developer]

<span data-ttu-id="38056-145">Zodra Hallo ontwikkelaars zijn geselecteerd gewenst, klikt u op de gewenste groep Hallo in Hallo **tooGroup toevoegen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38056-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="38056-146">Ontwikkelaars kunnen worden verwijderd uit groepen met Hallo **verwijderen uit groep** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38056-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Ontwikkelaars][api-management-add-group-to-developer-saved]

<span data-ttu-id="38056-148">Zodra het Hallo-koppeling tussen Hallo ontwikkelaars en Hallo groep wordt toegevoegd, kunt u deze bekijken in Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="38056-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="38056-149"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38056-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="38056-150">Als een ontwikkelaar kan tooa groep is toegevoegd, kunnen ze bekijken en zich abonneren toohello producten die zijn gekoppeld aan die groep.</span><span class="sxs-lookup"><span data-stu-id="38056-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="38056-151">Zie voor meer informatie [maken en een product publiceren in Azure API Management][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="38056-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="38056-152">Bovendien toocreating en groepen beheren in de publicatieportal hello, u kunt groepen maken en beheren uw Hallo API Management REST-API met [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.</span><span class="sxs-lookup"><span data-stu-id="38056-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
