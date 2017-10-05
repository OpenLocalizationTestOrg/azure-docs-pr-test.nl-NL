---
title: Azure op rollen gebaseerde toegangsbeheer (RBAC) om toegangsrechten te maken en beheren van ondersteuningsaanvragen | Microsoft Docs
description: Azure op rollen gebaseerde toegangsbeheer (RBAC) om toegangsrechten te maken en beheren van aanvragen voor ondersteuning
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="2056b-103">Azure op rollen gebaseerde toegangsbeheer (RBAC) om toegangsrechten te maken en beheren van aanvragen voor ondersteuning</span><span class="sxs-lookup"><span data-stu-id="2056b-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="2056b-104">[Op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) kunt Geavanceerd toegangsbeheer voor Azure.</span><span class="sxs-lookup"><span data-stu-id="2056b-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="2056b-105">Ondersteuning voor het maken van de aanvraag in de Azure portal [portal.azure.com](https://portal.azure.com), maakt gebruik van Azure RBAC-model om te definiëren die kunt maken en beheren van aanvragen voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2056b-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="2056b-106">Toegang wordt verleend door de juiste RBAC-rol toewijzen aan gebruikers, groepen en toepassingen op een bepaalde scope, kan dit een abonnement, resourcegroep of een resource.</span><span class="sxs-lookup"><span data-stu-id="2056b-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="2056b-107">Voorbeeld: als een eigenaar van de groep resource met leesmachtigingen voor de scope abonnement kunt u alle resources onder de resourcegroep, zoals websites, virtuele machines en subnetten beheren.</span><span class="sxs-lookup"><span data-stu-id="2056b-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="2056b-108">Echter, wanneer u probeert om een ondersteuningsaanvraag op basis van de bron van de virtuele machine te maken, de volgende fout optreedt</span><span class="sxs-lookup"><span data-stu-id="2056b-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Abonnement-fout](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="2056b-110">U moet in het beheer van de aanvraag van ondersteuning machtiging of een functie die de actie ondersteuning Microsoft.Support/* bij het abonnementsbereik heeft te kunnen maken en beheren van ondersteuningsaanvragen schrijven.</span><span class="sxs-lookup"><span data-stu-id="2056b-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="2056b-111">Het volgende artikel wordt uitgelegd hoe u Azure aangepaste op rollen gebaseerde toegangsbeheer (RBAC) maken en beheren van aanvragen voor ondersteuning in de Azure portal kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2056b-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2056b-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2056b-112">Getting Started</span></span>

<span data-ttu-id="2056b-113">In het bovenstaande voorbeeld zou u een ondersteuningsaanvraag wilt indienen voor uw resource maken als u een aangepaste RBAC-rol op het abonnement zijn toegewezen door de eigenaar van het abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="2056b-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="2056b-114">[Aangepaste RBAC-rollen](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) kunnen worden gemaakt met Azure PowerShell, Azure-opdrachtregelinterface (CLI) en de REST-API.</span><span class="sxs-lookup"><span data-stu-id="2056b-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="2056b-115">De eigenschap acties van een aangepaste beveiligingsrol Hiermee geeft u de Azure-bewerkingen waarvoor de rol toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2056b-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="2056b-116">Voor het maken van een aangepaste rol voor het beheer van de aanvraag ondersteuning, moet de rol de actie Microsoft.Support/* hebben.</span><span class="sxs-lookup"><span data-stu-id="2056b-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="2056b-117">Hier volgt een voorbeeld van een aangepaste rol die u kunt maken en beheren van aanvragen voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2056b-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="2056b-118">We deze rol 'Ondersteuning vragen Inzender' hebt genoemd en hoe we verwijzen naar de aangepaste rol die in dit artikel is.</span><span class="sxs-lookup"><span data-stu-id="2056b-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="2056b-119">Volg de stappen die worden beschreven in [in deze video](https://www.youtube.com/watch?v=-PaBaDmfwKI) voor informatie over het maken van een aangepaste beveiligingsrol voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2056b-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="2056b-120">Maken en beheren van aanvragen voor ondersteuning in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="2056b-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="2056b-121">Voorbeeld: u bent de eigenaar van het abonnement "Visual Studio MSDN-abonnement."</span><span class="sxs-lookup"><span data-stu-id="2056b-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="2056b-122">Jan is uw peer wie de eigenaar van een resource op sommige van de resourcegroepen in dit abonnement is en leesrechten heeft voor het abonnement.</span><span class="sxs-lookup"><span data-stu-id="2056b-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="2056b-123">U wilt toegang geven tot uw peer, Jan, de mogelijkheid om te maken en beheren van ondersteuningstickets voor de resources onder dit abonnement.</span><span class="sxs-lookup"><span data-stu-id="2056b-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="2056b-124">De eerste stap is om naar het abonnement te gaan en onder 'Instellingen' ziet u een lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2056b-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="2056b-125">Klik op de gebruiker Jan die lezerstoegang heeft tot het abonnement en gaan we een nieuwe aangepaste beveiligingsrol aan hem toewijzen.</span><span class="sxs-lookup"><span data-stu-id="2056b-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Functie toevoegen](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="2056b-127">Klik op "Toevoegen" onder de blade 'Gebruikers'.</span><span class="sxs-lookup"><span data-stu-id="2056b-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="2056b-128">Selecteer de aangepaste rol 'Ondersteuning vragen Inzender' uit de lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="2056b-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Ondersteuning voor de rol van Inzender toevoegen](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="2056b-130">Klik op 'Gebruikers toevoegen' en voer de Jan e referenties na het selecteren van de naam van de rol.</span><span class="sxs-lookup"><span data-stu-id="2056b-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="2056b-131">Klik op 'Selecteren'</span><span class="sxs-lookup"><span data-stu-id="2056b-131">Click "Select"</span></span>

    ![Gebruikers toevoegen](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="2056b-133">Klik op 'Ok' om door te gaan</span><span class="sxs-lookup"><span data-stu-id="2056b-133">Click "Ok" to proceed</span></span>

    ![Toegang toevoegen](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="2056b-135">U ziet nu de gebruiker met de zojuist toegevoegde aangepaste rol 'Ondersteuning vragen Inzender' onder het abonnement waarvoor u de eigenaar bent</span><span class="sxs-lookup"><span data-stu-id="2056b-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Toegevoegde gebruiker](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="2056b-137">Wanneer Jan zich in de portal aanmeldt, ziet hij het abonnement waaraan hij is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2056b-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="2056b-138">Jan klikt op 'Nieuw ondersteuningsverzoek' op de blade 'Help en ondersteuning voor' en ondersteuningsaanvragen kunt maken voor 'Visual Studio Ultimate met MSDN'</span><span class="sxs-lookup"><span data-stu-id="2056b-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nieuw ondersteuningsverzoek](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="2056b-140">Te klikken op 'Alle ondersteunen aanvragen' Jan bevat een overzicht van ondersteuningsaanvragen gemaakt voor dit abonnement ![Aanvraagdetails weergeven](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="2056b-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="2056b-141">Toegang voor ondersteuning aanvragen in de Azure portal verwijderen</span><span class="sxs-lookup"><span data-stu-id="2056b-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="2056b-142">Net zoals het is mogelijk om toegang te verlenen aan een gebruiker maken en beheren van ondersteuningsaanvragen, is het mogelijk om toegang voor de gebruiker ook te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2056b-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="2056b-143">Om te kunnen maken en beheren van ondersteuningsaanvragen, gaat u naar het abonnement verwijderen, klik op 'Instellingen' en klik op de gebruiker (in dit geval Jan).</span><span class="sxs-lookup"><span data-stu-id="2056b-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="2056b-144">Met de rechtermuisknop op de naam van de rol, 'Ondersteuning vragen Inzender' en klik op 'Verwijderen'</span><span class="sxs-lookup"><span data-stu-id="2056b-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Ondersteuning aanvragen voor toegang verwijderen](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="2056b-146">Wanneer Jan zich bij de portal aanmeldt en probeert om een ondersteuningsaanvraag te maken, wordt hij de volgende fout aangetroffen</span><span class="sxs-lookup"><span data-stu-id="2056b-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Abonnement fout-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="2056b-148">Jan niet zien alle aanvragen ondersteunen wanneer hij klikt op "Alle ondersteuning aanvragen"</span><span class="sxs-lookup"><span data-stu-id="2056b-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Aanvraagdetails weergave-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
