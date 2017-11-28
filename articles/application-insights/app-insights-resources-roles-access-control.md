---
title: aaaResources, rollen en -toegangsbeheer in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="5ebd6-103">Resources, rollen en toegangsbeheer in Application Insights</span><span class="sxs-lookup"><span data-stu-id="5ebd6-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="5ebd6-104">U kunt bepalen wie heeft lees- en toegang tooyour gegevens bijwerken in Azure [Application Insights][start], met behulp van [toegangsbeheer op basis van rollen in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd6-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ebd6-105">Toewijzen van toegang toousers in Hallo **resourcegroep of abonnement** toowhich die uw toepassingsresource - niet in Hallo resource zelf behoort.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="5ebd6-106">Hallo toewijzen **Application Insights-onderdeelinzender** rol.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="5ebd6-107">Dit zorgt ervoor uniform beheer van toegang tooweb tests en waarschuwingen samen met de bron van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="5ebd6-108">[Meer informatie](#access).</span><span class="sxs-lookup"><span data-stu-id="5ebd6-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="5ebd6-109">Bronnen, groepen en abonnementen</span><span class="sxs-lookup"><span data-stu-id="5ebd6-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="5ebd6-110">Eerste, sommige definities:</span><span class="sxs-lookup"><span data-stu-id="5ebd6-110">First, some definitions:</span></span>

* <span data-ttu-id="5ebd6-111">**Resource** : een exemplaar van een Microsoft Azure-service.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="5ebd6-112">Uw Application Insights-resource verzamelt, analyseert en Hallo telemetriegegevens verzonden van uw toepassing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="5ebd6-113">Andere soorten Azure-resources zijn web-apps, databases en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="5ebd6-114">uw resources, opent u toosee hello [Azure Portal][portal], aanmelden en alle Resources op.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="5ebd6-115">toofind een resource, typ een gedeelte van de naam in het filterveld Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Lijst met Azure-resources](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="5ebd6-117">[**Resourcegroep** ] [ group] -elke resource tooone groep behoort.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="5ebd6-118">Een groep is een handige manier toomanage verwante resources, met name voor toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="5ebd6-119">In één resource bijvoorbeeld geëxporteerde groep kan u een Web-App, een Application Insights resource toomonitor Hallo-app en een resource opslag tookeep geplaatst gegevens.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Kies Bladeren, resourcegroepen, en vervolgens kiest u een groep](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="5ebd6-121">[**Abonnement** ](https://manage.windowsazure.com) -toouse Application Insights of andere Azure-resources, u zich aanmeldt tooan Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="5ebd6-122">Elke resourcegroep hoort tooone Azure-abonnement, waar u kiest uw pakket prijs en, als het een organisatie-abonnement, kiest u Hallo-leden en hun machtigingen voor toegang.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="5ebd6-123">[**Microsoft-account** ] [ account] -Hallo gebruikersnaam en het wachtwoord dat u toosign in tooMicrosoft Azure-abonnementen, XBox Live, Outlook.com en andere Microsoft-services.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="5ebd6-124"><a name="access"></a>Toegang beheren in de resourcegroep Hallo</span><span class="sxs-lookup"><span data-stu-id="5ebd6-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="5ebd6-125">Het is belangrijk toounderstand dat in de toevoeging toohello bron die u voor uw toepassing hebt gemaakt, er zijn ook afzonderlijke verborgen bronnen voor waarschuwingen en webtests.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="5ebd6-126">Ze zijn aangesloten toohello dezelfde [resourcegroep](#resource-group) als uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="5ebd6-127">Mogelijk hebt u andere Azure-services in, zoals websites of opslag is er ook plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Resources in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="5ebd6-129">toegang tot toocontrol toothese-bronnen die daarom het raadzaam naar:</span><span class="sxs-lookup"><span data-stu-id="5ebd6-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="5ebd6-130">Toegangsbeheer op Hallo **resourcegroep of abonnement** niveau.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="5ebd6-131">Hallo toewijzen **Application Insights-onderdeelinzender** toousers rol.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="5ebd6-132">Hierdoor kunnen ze tooedit webtests, waarschuwingen en Application Insights-resources, zonder dat toegang tooany andere services in Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="5ebd6-133">tooprovide toegang tooanother gebruiker</span><span class="sxs-lookup"><span data-stu-id="5ebd6-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="5ebd6-134">U moet de eigenaar van rechten toohello abonnement of resourcegroep Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="5ebd6-135">Hallo-gebruiker moet beschikken over een [Microsoft-Account][account], of u toegang tot tootheir [organisatie Microsoft-Account](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd6-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="5ebd6-136">U kunt opgeven toegang tooindividuals en toouser groepen gedefinieerd in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="5ebd6-137">Navigeer toohello resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5ebd6-137">Navigate toohello resource group</span></span>
<span data-ttu-id="5ebd6-138">Er Hallo gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-138">Add hello user there.</span></span>

![In de resourceblade van uw toepassing, Essentials openen, open Hallo resourcegroep en er instellingen/gebruikers te selecteren.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="5ebd6-141">Of u kan hoofdmap en Hallo gebruiker toohello abonnement toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="5ebd6-142">Rol selecteren</span><span class="sxs-lookup"><span data-stu-id="5ebd6-142">Select a role</span></span>
![Selecteer een rol voor de nieuwe gebruiker Hallo](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="5ebd6-144">Rol</span><span class="sxs-lookup"><span data-stu-id="5ebd6-144">Role</span></span> | <span data-ttu-id="5ebd6-145">In de resourcegroep Hallo</span><span class="sxs-lookup"><span data-stu-id="5ebd6-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="5ebd6-146">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="5ebd6-146">Owner</span></span> |<span data-ttu-id="5ebd6-147">Alles, waaronder gebruikerstoegang kunt wijzigen</span><span class="sxs-lookup"><span data-stu-id="5ebd6-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="5ebd6-148">Inzender</span><span class="sxs-lookup"><span data-stu-id="5ebd6-148">Contributor</span></span> |<span data-ttu-id="5ebd6-149">Alles zijn, met inbegrip van alle resources kunt bewerken</span><span class="sxs-lookup"><span data-stu-id="5ebd6-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="5ebd6-150">Application Insights-onderdeelinzender</span><span class="sxs-lookup"><span data-stu-id="5ebd6-150">Application Insights Component contributor</span></span> |<span data-ttu-id="5ebd6-151">Application Insights-resources, webtests en waarschuwingen kunt bewerken</span><span class="sxs-lookup"><span data-stu-id="5ebd6-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="5ebd6-152">Lezer</span><span class="sxs-lookup"><span data-stu-id="5ebd6-152">Reader</span></span> |<span data-ttu-id="5ebd6-153">Kunt bekijken maar niet van belang.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-153">Can view but not change anything</span></span> |

<span data-ttu-id="5ebd6-154">De bewerking' omvat het maken, verwijderen en bijwerken:</span><span class="sxs-lookup"><span data-stu-id="5ebd6-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="5ebd6-155">Resources</span><span class="sxs-lookup"><span data-stu-id="5ebd6-155">Resources</span></span>
* <span data-ttu-id="5ebd6-156">Webtests</span><span class="sxs-lookup"><span data-stu-id="5ebd6-156">Web tests</span></span>
* <span data-ttu-id="5ebd6-157">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="5ebd6-157">Alerts</span></span>
* <span data-ttu-id="5ebd6-158">Continue export</span><span class="sxs-lookup"><span data-stu-id="5ebd6-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="5ebd6-159">Hallo gebruiker selecteren</span><span class="sxs-lookup"><span data-stu-id="5ebd6-159">Select hello user</span></span>

<span data-ttu-id="5ebd6-160">Als Hallo gebruiker die zich niet in Hallo directory, kunt u iedereen met een Microsoft-account kunt uitnodigen.</span><span class="sxs-lookup"><span data-stu-id="5ebd6-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="5ebd6-161">(Als deze services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, beschikken over een Microsoft-account.)</span><span class="sxs-lookup"><span data-stu-id="5ebd6-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="5ebd6-162">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="5ebd6-162">Related content</span></span>

* [<span data-ttu-id="5ebd6-163">Op rollen gebaseerde toegangsbeheer in Azure</span><span class="sxs-lookup"><span data-stu-id="5ebd6-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
