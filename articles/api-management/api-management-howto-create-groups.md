---
title: Ontwikkelaarsaccounts met behulp van groepen in Azure API Management beheren | Microsoft Docs
description: Informatie over het gebruik van groepen in Azure API Management ontwikkelaarsaccounts beheren
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="38a24-103">Het maken en groepen gebruiken voor het beheren van de ontwikkelaarsaccounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="38a24-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="38a24-104">In API Management worden groepen gebruikt voor het beheren van de zichtbaarheid van producten voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38a24-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="38a24-105">Producten voor het eerst zichtbaar aan groepen zijn gemaakt en vervolgens de ontwikkelaars van die groepen kunnen weergeven en zich abonneren op de producten die gekoppeld aan de groepen zijn.</span><span class="sxs-lookup"><span data-stu-id="38a24-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="38a24-106">API Management heeft de volgende onveranderbare systeemgroepen.</span><span class="sxs-lookup"><span data-stu-id="38a24-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="38a24-107">**Beheerders** - Azure-abonnementbeheerders zijn lid van deze groep.</span><span class="sxs-lookup"><span data-stu-id="38a24-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="38a24-108">Beheerders beheren service-exemplaren van API Management, door het maken van de API's, bewerkingen en producten die door ontwikkelaars worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38a24-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="38a24-109">**Ontwikkelaars** - Geverifieerde gebruikers van de ontwikkelaarsportal vallen in deze groep.</span><span class="sxs-lookup"><span data-stu-id="38a24-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="38a24-110">Ontwikkelaars zijn de klanten die toepassingen bouwen met uw API's.</span><span class="sxs-lookup"><span data-stu-id="38a24-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="38a24-111">Ontwikkelaars krijgen toegang tot de ontwikkelaarsportal en bouwen toepassingen waarmee de bewerkingen van een API worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="38a24-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="38a24-112">**Gasten** - Niet-geverifieerde gebruikers van de ontwikkelaarsportal, zoals potentiële klanten die de ontwikkelaarsportal van een API Management-exemplaar bezoeken, vallen in deze groep.</span><span class="sxs-lookup"><span data-stu-id="38a24-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="38a24-113">Ze kunnen bepaalde alleen-lezentoegang krijgen, zoals de mogelijkheid om API's te bekijken maar niet om ze aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="38a24-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="38a24-114">Naast deze systeemgroepen kunnen beheerders aangepaste groepen maken of [gebruikmaken van externe groepen in gekoppelde Azure Active Directory-tenants][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="38a24-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="38a24-115">Aangepaste en externe groepen kunnen naast systeemgroepen worden gebruikt om ontwikkelaars zichtbaarheid van en toegang tot API-producten te geven.</span><span class="sxs-lookup"><span data-stu-id="38a24-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="38a24-116">U kunt bijvoorbeeld één aangepaste groep maken voor ontwikkelaars die zijn gekoppeld aan een specifieke partnerorganisatie en hen toegang geven tot de API's vanuit een product dat alleen relevante API's bevat.</span><span class="sxs-lookup"><span data-stu-id="38a24-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="38a24-117">Een gebruiker kan lid zijn van meerdere groepen.</span><span class="sxs-lookup"><span data-stu-id="38a24-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="38a24-118">Deze handleiding wordt getoond hoe beheerders van een exemplaar van API Management kunnen nieuwe groepen toevoegen en koppel deze aan de producten en -ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38a24-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="38a24-119">Naast het maken en beheren van groepen in de publicatieportal bevindt, kunt u maken en beheren van uw groepen met de REST-API van API Management [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.</span><span class="sxs-lookup"><span data-stu-id="38a24-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="38a24-120"><a name="create-group"></a>Een groep maken</span><span class="sxs-lookup"><span data-stu-id="38a24-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="38a24-121">Klik op om een nieuwe groep **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="38a24-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="38a24-122">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="38a24-122">This takes you to the API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="38a24-124">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="38a24-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="38a24-125">Klik op **groepen** van de **API Management** menu aan de linkerkant en klik vervolgens op **groep toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="38a24-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Nieuwe groep toevoegen][api-management-add-group]

<span data-ttu-id="38a24-127">Voer een unieke naam voor de groep en een optionele beschrijving in en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38a24-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Nieuwe groep toevoegen][api-management-add-group-window]

<span data-ttu-id="38a24-129">De nieuwe groep wordt weergegeven in het tabblad groepen.</span><span class="sxs-lookup"><span data-stu-id="38a24-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="38a24-130">Bewerken de **naam** of **beschrijving** van de groep, klikt u op de naam van de groep in de lijst.</span><span class="sxs-lookup"><span data-stu-id="38a24-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="38a24-131">Als u wilt verwijderen van de groep, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="38a24-131">To delete the group, click **Delete**.</span></span>

![Groep toegevoegd][api-management-new-group]

<span data-ttu-id="38a24-133">Nu dat de groep is gemaakt, kan het worden gekoppeld aan de producten en -ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="38a24-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="38a24-134"><a name="associate-group-product"></a>Koppelen van een groep aan een product</span><span class="sxs-lookup"><span data-stu-id="38a24-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="38a24-135">U kunt een groep koppelen met een product, **producten** van de **API Management** menu aan de linkerkant en klik vervolgens op de naam van de gewenste product.</span><span class="sxs-lookup"><span data-stu-id="38a24-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Zichtbaarheid instellen][api-management-add-group-to-product]

<span data-ttu-id="38a24-137">Selecteer de **zichtbaarheid** tabblad toevoegen en verwijderen van groepen en om de huidige groepen voor het product te bekijken.</span><span class="sxs-lookup"><span data-stu-id="38a24-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="38a24-138">Als u wilt toevoegen of verwijderen van groepen, Controleer of schakel de selectievakjes uit voor de gewenste groepen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38a24-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Zichtbaarheid instellen][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="38a24-140">Zie het toevoegen van Azure Active Directory-groepen [hoe autoriseren ontwikkelaarsaccounts met Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="38a24-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="38a24-141">Voor het configureren van groepen van de **zichtbaarheid** tabblad voor een product **groepen beheren**.</span><span class="sxs-lookup"><span data-stu-id="38a24-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="38a24-142">Wanneer een product gekoppeld aan een groep is, kunnen ontwikkelaars in die groep weergeven en zich abonneren op het product.</span><span class="sxs-lookup"><span data-stu-id="38a24-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="38a24-143"><a name="associate-group-developer"></a>Groepen koppelen aan ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="38a24-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="38a24-144">U kunt groepen koppelen aan ontwikkelaars, **gebruikers** van de **API Management** menu aan de linkerkant en vervolgens het selectievakje naast de ontwikkelaars die u wilt koppelen aan een groep.</span><span class="sxs-lookup"><span data-stu-id="38a24-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Ontwikkelaar toevoegen aan groep][api-management-add-group-to-developer]

<span data-ttu-id="38a24-146">Nadat de gewenste ontwikkelaars zijn geselecteerd en klikt u op de gewenste groep in de **toevoegen aan groep** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38a24-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="38a24-147">Ontwikkelaars kunnen worden verwijderd uit groepen met behulp van de **verwijderen uit groep** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38a24-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Ontwikkelaars][api-management-add-group-to-developer-saved]

<span data-ttu-id="38a24-149">Als de koppeling tussen de ontwikkelaar en de groep wordt toegevoegd, kunt u het bekijken in de **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="38a24-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="38a24-150"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38a24-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="38a24-151">Als een ontwikkelaar is toegevoegd aan een groep, kunnen ze bekijken en zich abonneren op de producten die zijn gekoppeld aan die groep.</span><span class="sxs-lookup"><span data-stu-id="38a24-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="38a24-152">Zie voor meer informatie [maken en een product publiceren in Azure API Management][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="38a24-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="38a24-153">Naast het maken en beheren van groepen in de publicatieportal bevindt, kunt u maken en beheren van uw groepen met de REST-API van API Management [groep](https://msdn.microsoft.com/library/azure/dn776329.aspx) entiteit.</span><span class="sxs-lookup"><span data-stu-id="38a24-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
