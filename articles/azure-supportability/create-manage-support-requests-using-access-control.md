---
title: aaaAzure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van ondersteuningsaanvragen | Microsoft Docs
description: Azure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van aanvragen voor ondersteuning
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="92eff-103">Azure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van aanvragen voor ondersteuning</span><span class="sxs-lookup"><span data-stu-id="92eff-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="92eff-104">[Op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) kunt Geavanceerd toegangsbeheer voor Azure.</span><span class="sxs-lookup"><span data-stu-id="92eff-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="92eff-105">Ondersteuning voor het maken van de aanvraag in hello Azure-portal [portal.azure.com](https://portal.azure.com), maakt gebruik van Azure RBAC-model toodefine die maken en beheren van aanvragen voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="92eff-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="92eff-106">Toegang is verleend door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen op een bepaalde scope, kan dit een abonnement, resourcegroep of een resource.</span><span class="sxs-lookup"><span data-stu-id="92eff-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="92eff-107">Voorbeeld: als een eigenaar van de groep resource met leesmachtigingen op Hallo abonnementsbereik u alle Hallo resources onder de resourcegroep hello, zoals websites, virtuele machines en subnetten kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="92eff-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="92eff-108">Echter, wanneer u een ondersteuningsaanvraag in voor de bron van de virtuele machine Hallo toocreate, u tegenkomt Hallo volgende fout</span><span class="sxs-lookup"><span data-stu-id="92eff-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Abonnement-fout](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="92eff-110">In het beheer van de aanvraag van ondersteuning u moet de machtiging schrijven of een rol heeft die over Hallo actie Microsoft.Support/* Hallo abonnement bereik toobe kunnen toocreate ondersteunen en ondersteuningsaanvragen beheren.</span><span class="sxs-lookup"><span data-stu-id="92eff-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="92eff-111">Hallo volgende artikel wordt uitgelegd hoe u Azure aangepaste op rollen gebaseerde toegangsbeheer (RBAC) toocreate gebruiken en beheren ondersteuningsaanvragen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92eff-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="92eff-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="92eff-112">Getting Started</span></span>

<span data-ttu-id="92eff-113">Hallo bovenstaande voorbeeld gebruikt, zou u kunnen toocreate een verzoek om ondersteuning voor uw resource als u een aangepaste RBAC-rol op Hallo abonnement zijn toegewezen door de eigenaar van de Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="92eff-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="92eff-114">[Aangepaste RBAC-rollen](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) kunnen worden gemaakt met Azure PowerShell, Azure-opdrachtregelinterface (CLI) en Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="92eff-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="92eff-115">Hallo acties eigenschap van een aangepaste rol geeft hello Azure-bewerkingen toowhich Hallo rol toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="92eff-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="92eff-116">een aangepaste rol voor het beheer van de aanvraag ondersteuning toocreate, Hallo rol moet beschikken over Hallo actie Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="92eff-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="92eff-117">Hier volgt een voorbeeld van een aangepaste rol die u kunt toocreate gebruiken en beheren ondersteuning aanvragen.</span><span class="sxs-lookup"><span data-stu-id="92eff-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="92eff-118">We deze rol 'Ondersteuning vragen Inzender' hebt genoemd en dat is hoe we de aangepaste rol toohello in dit artikel verwijzen.</span><span class="sxs-lookup"><span data-stu-id="92eff-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="92eff-119">Hallo stappen die worden beschreven in [in deze video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn hoe toocreate een aangepaste beveiligingsrol voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="92eff-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="92eff-120">Maken en beheren van ondersteuningsaanvragen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="92eff-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="92eff-121">Voorbeeld: u bent Hallo eigenaar van het abonnement "Visual Studio MSDN-abonnement."</span><span class="sxs-lookup"><span data-stu-id="92eff-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="92eff-122">Jan is de peer die is een resource-eigenaar toosome van resourcegroepen Hallo in dit abonnement en machtiging toohello abonnement is gelezen.</span><span class="sxs-lookup"><span data-stu-id="92eff-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="92eff-123">U wilt toogive toegang tooyour peer, Jan, Hallo mogelijkheid toocreate en ondersteuningstickets voor Hallo resources onder dit abonnement beheren.</span><span class="sxs-lookup"><span data-stu-id="92eff-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="92eff-124">de eerste stap Hallo is toogo toohello abonnement en onder 'Instellingen' ziet u een lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="92eff-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="92eff-125">Klik op Hallo gebruiker Jan die leestoegang hebben op Hallo abonnement en gaan we een nieuwe aangepaste rol toohim toewijzen.</span><span class="sxs-lookup"><span data-stu-id="92eff-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Functie toevoegen](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="92eff-127">Klik op "Toevoegen" onder Hallo 'Gebruikers' blade.</span><span class="sxs-lookup"><span data-stu-id="92eff-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="92eff-128">Selecteer Hallo aangepaste rol 'Ondersteuning vragen Inzender' in hello lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="92eff-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Ondersteuning voor de rol van Inzender toevoegen](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="92eff-130">Na het selecteren van de rolnaam hello, klik op 'Gebruikers toevoegen' en Voer Hallo Joe's e-referenties.</span><span class="sxs-lookup"><span data-stu-id="92eff-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="92eff-131">Klik op 'Selecteren'</span><span class="sxs-lookup"><span data-stu-id="92eff-131">Click "Select"</span></span>

    ![Gebruikers toevoegen](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="92eff-133">Klik op 'Ok' tooproceed</span><span class="sxs-lookup"><span data-stu-id="92eff-133">Click "Ok" tooproceed</span></span>

    ![Toegang toevoegen](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="92eff-135">U ziet nu Hallo-gebruiker met Hallo toegevoegde aangepaste rol 'Ondersteuning vragen Inzender' Hallo-abonnement waarvoor u Hallo eigenaar bent</span><span class="sxs-lookup"><span data-stu-id="92eff-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Toegevoegde gebruiker](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="92eff-137">Wanneer de Hallo portal Jan zich aanmeldt, ziet hij Hallo abonnement toowhich die hij is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="92eff-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="92eff-138">Jan klikt op 'Nieuw ondersteuningsverzoek' Hallo 'Help en ondersteuning voor' blade en ondersteuningsaanvragen kunt maken voor 'Visual Studio Ultimate met MSDN'</span><span class="sxs-lookup"><span data-stu-id="92eff-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nieuw ondersteuningsverzoek](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="92eff-140">Te klikken op 'Alle ondersteunen aanvragen' Jan overzicht Hallo van ondersteuningsaanvragen gemaakt voor dit abonnement ![Aanvraagdetails weergeven](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="92eff-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="92eff-141">Toegang voor ondersteuning aanvragen in hello Azure-portal verwijderen</span><span class="sxs-lookup"><span data-stu-id="92eff-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="92eff-142">Omdat deze mogelijk toogrant toegang tooa gebruiker toocreate en ondersteuningsaanvragen beheren, is het mogelijk tooremove-toegang voor ook Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92eff-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="92eff-143">tooremove mogelijkheid toocreate Hallo ondersteuningsaanvragen beheren, gaat u toohello abonnement, klik op 'Instellingen' en op Hallo gebruiker (in dit geval Jan).</span><span class="sxs-lookup"><span data-stu-id="92eff-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="92eff-144">Met de rechtermuisknop op Hallo rolnaam, 'Ondersteuning vragen Inzender' en klik op 'Verwijderen'</span><span class="sxs-lookup"><span data-stu-id="92eff-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Ondersteuning aanvragen voor toegang verwijderen](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="92eff-146">Wanneer Jan toohello portal aanmeldt en toocreate ondersteuning aan te vragen probeert, hij Hallo volgende fout aangetroffen</span><span class="sxs-lookup"><span data-stu-id="92eff-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Abonnement fout-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="92eff-148">Jan niet zien alle aanvragen ondersteunen wanneer hij klikt op "Alle ondersteuning aanvragen"</span><span class="sxs-lookup"><span data-stu-id="92eff-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Aanvraagdetails weergave-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
