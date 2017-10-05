---
title: Resources, rollen en toegang beheren in Azure Application Insights | Microsoft Docs
description: Eigenaren, bijdragers en lezers van inzicht in uw organisatie.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="5fc8c-103">Resources, rollen en toegangsbeheer in Application Insights</span><span class="sxs-lookup"><span data-stu-id="5fc8c-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="5fc8c-104">U kunt bepalen wie heeft lezen en bijwerken van toegang tot uw gegevens in Azure [Application Insights][start], met behulp van [toegangsbeheer op basis van rollen in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5fc8c-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fc8c-105">Toewijzen van toegang voor gebruikers in de **resourcegroep of abonnement** die uw toepassingsresource behoort - niet in de bron zelf.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="5fc8c-106">Wijs de **Application Insights-onderdeelinzender** rol.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="5fc8c-107">Dit zorgt ervoor uniform beheer van toegang tot webtests en waarschuwingen samen met de bron van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="5fc8c-108">[Meer informatie](#access).</span><span class="sxs-lookup"><span data-stu-id="5fc8c-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="5fc8c-109">Bronnen, groepen en abonnementen</span><span class="sxs-lookup"><span data-stu-id="5fc8c-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="5fc8c-110">Eerste, sommige definities:</span><span class="sxs-lookup"><span data-stu-id="5fc8c-110">First, some definitions:</span></span>

* <span data-ttu-id="5fc8c-111">**Resource** : een exemplaar van een Microsoft Azure-service.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="5fc8c-112">Uw Application Insights-resource verzamelt, analyseert en geeft de telemetriegegevens van uw toepassing verzonden.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="5fc8c-113">Andere soorten Azure-resources zijn web-apps, databases en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="5fc8c-114">Overzicht van uw resources, opent u de [Azure Portal][portal], aanmelden en alle Resources op.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="5fc8c-115">Typ een resource vindt deel van de naam in het filterveld.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Lijst met Azure-resources](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="5fc8c-117">[**Resourcegroep** ] [ group] -elke resource behoort tot één groep.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="5fc8c-118">Een groep is een handige manier om verwante resources, met name voor toegangsbeheer te beheren.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="5fc8c-119">Bijvoorbeeld, in één resourcegroep kan u zetten een Web-App, een Application Insights-resource voor het bewaken van de app en een opslagresource als geëxporteerde gegevens wilt behouden.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Kies Bladeren, resourcegroepen, en vervolgens kiest u een groep](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="5fc8c-121">[**Abonnement** ](https://manage.windowsazure.com) - met Application Insights of andere Azure-resources, u zich aanmeldt bij een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="5fc8c-122">Elke resourcegroep behoort tot één Azure-abonnement, waar u kiest uw pakket prijs en, als het een organisatie-abonnement, kiest u leden en hun machtigingen voor toegang.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="5fc8c-123">[**Microsoft-account** ] [ account] -de gebruikersnaam en het wachtwoord dat u aan te melden bij Microsoft Azure-abonnementen, XBox Live, Outlook.com en andere Microsoft-services.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="5fc8c-124"><a name="access"></a>Toegang beheren in de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5fc8c-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="5fc8c-125">Het is belangrijk te weten dat naast de bron die u voor uw toepassing hebt gemaakt, er ook afzonderlijke verborgen bronnen voor waarschuwingen en webtests zijn.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="5fc8c-126">Deze zijn gekoppeld aan dezelfde [resourcegroep](#resource-group) als uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="5fc8c-127">Mogelijk hebt u andere Azure-services in, zoals websites of opslag is er ook plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Resources in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="5fc8c-129">Toegang tot deze bronnen die daarom het raadzaam om te beheren:</span><span class="sxs-lookup"><span data-stu-id="5fc8c-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="5fc8c-130">Toegangsbeheer op de **resourcegroep of abonnement** niveau.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="5fc8c-131">Wijs de **Application Insights-onderdeelinzender** rol aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="5fc8c-132">Hierdoor kunnen ze webtests, waarschuwingen en Application Insights-resources, zonder dat toegang biedt tot alle andere services in de groep bewerken.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="5fc8c-133">Om toegang te bieden aan een andere gebruiker</span><span class="sxs-lookup"><span data-stu-id="5fc8c-133">To provide access to another user</span></span>
<span data-ttu-id="5fc8c-134">U moet de eigenaar van rechten voor het abonnement of de resourcegroep hebben.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="5fc8c-135">De gebruiker moet beschikken over een [Microsoft-Account][account], of de toegang tot hun [organisatie Microsoft-Account](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="5fc8c-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="5fc8c-136">U kunt bieden toegang tot personen en gebruikersgroepen die zijn gedefinieerd in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="5fc8c-137">Navigeer naar de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5fc8c-137">Navigate to the resource group</span></span>
<span data-ttu-id="5fc8c-138">De gebruiker er toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-138">Add the user there.</span></span>

![In de resourceblade van uw toepassing, Essentials openen, opent u de resourcegroep en er instellingen/gebruikers te selecteren.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="5fc8c-141">Of u kan hoofdmap en de gebruiker toevoegen aan het abonnement.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="5fc8c-142">Rol selecteren</span><span class="sxs-lookup"><span data-stu-id="5fc8c-142">Select a role</span></span>
![Selecteer een rol voor de nieuwe gebruiker](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="5fc8c-144">Rol</span><span class="sxs-lookup"><span data-stu-id="5fc8c-144">Role</span></span> | <span data-ttu-id="5fc8c-145">In de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5fc8c-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="5fc8c-146">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="5fc8c-146">Owner</span></span> |<span data-ttu-id="5fc8c-147">Alles, waaronder gebruikerstoegang kunt wijzigen</span><span class="sxs-lookup"><span data-stu-id="5fc8c-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="5fc8c-148">Inzender</span><span class="sxs-lookup"><span data-stu-id="5fc8c-148">Contributor</span></span> |<span data-ttu-id="5fc8c-149">Alles zijn, met inbegrip van alle resources kunt bewerken</span><span class="sxs-lookup"><span data-stu-id="5fc8c-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="5fc8c-150">Application Insights-onderdeelinzender</span><span class="sxs-lookup"><span data-stu-id="5fc8c-150">Application Insights Component contributor</span></span> |<span data-ttu-id="5fc8c-151">Application Insights-resources, webtests en waarschuwingen kunt bewerken</span><span class="sxs-lookup"><span data-stu-id="5fc8c-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="5fc8c-152">Lezer</span><span class="sxs-lookup"><span data-stu-id="5fc8c-152">Reader</span></span> |<span data-ttu-id="5fc8c-153">Kunt bekijken maar niet van belang.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-153">Can view but not change anything</span></span> |

<span data-ttu-id="5fc8c-154">De bewerking' omvat het maken, verwijderen en bijwerken:</span><span class="sxs-lookup"><span data-stu-id="5fc8c-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="5fc8c-155">Resources</span><span class="sxs-lookup"><span data-stu-id="5fc8c-155">Resources</span></span>
* <span data-ttu-id="5fc8c-156">Webtests</span><span class="sxs-lookup"><span data-stu-id="5fc8c-156">Web tests</span></span>
* <span data-ttu-id="5fc8c-157">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="5fc8c-157">Alerts</span></span>
* <span data-ttu-id="5fc8c-158">Continue export</span><span class="sxs-lookup"><span data-stu-id="5fc8c-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="5fc8c-159">Selecteer de gebruiker</span><span class="sxs-lookup"><span data-stu-id="5fc8c-159">Select the user</span></span>

<span data-ttu-id="5fc8c-160">Als de gebruiker die u wilt dat niet in de map, kunt u iedereen met een Microsoft-account kunt uitnodigen.</span><span class="sxs-lookup"><span data-stu-id="5fc8c-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="5fc8c-161">(Als deze services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, beschikken over een Microsoft-account.)</span><span class="sxs-lookup"><span data-stu-id="5fc8c-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="5fc8c-162">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="5fc8c-162">Related content</span></span>

* [<span data-ttu-id="5fc8c-163">Op rollen gebaseerde toegangsbeheer in Azure</span><span class="sxs-lookup"><span data-stu-id="5fc8c-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
