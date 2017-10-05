---
title: Azure IoT Suite en Azure Active Directory | Microsoft Docs
description: Hierin wordt beschreven hoe Azure IoT Suite maakt gebruik van Azure Active Directory om machtigingen te beheren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="8c72e-103">Machtigingen op de site azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="8c72e-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="8c72e-104">Wat gebeurt er wanneer u zich aanmeldt</span><span class="sxs-lookup"><span data-stu-id="8c72e-104">What happens when you sign in</span></span>

<span data-ttu-id="8c72e-105">De eerste keer dat u zich aanmeldt bij [azureiotsuite.com][lnk-azureiotsuite], de site bepaalt aan de machtigingsniveaus die u hebt op basis van de momenteel geselecteerde tenant van Azure Active Directory (AAD) en de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8c72e-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="8c72e-106">Eerst om in te vullen in de lijst met tenants gezien naast uw gebruikersnaam, vindt de site uit van Azure welke AAD tenants u deel uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="8c72e-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="8c72e-107">Op dit moment wordt de site, kan alleen gebruikerstokens verkrijgen voor één tenant tegelijk.</span><span class="sxs-lookup"><span data-stu-id="8c72e-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="8c72e-108">Daarom wanneer u tenants met behulp van de vervolgkeuzelijst in de rechterbovenhoek overschakelt, registreert de site u naar die tenant verkrijgen van de tokens voor deze tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="8c72e-109">De site vindt vervolgens uit vanuit Azure welke abonnementen u hebt gekoppeld aan de geselecteerde tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="8c72e-110">Wanneer u een nieuwe vooraf geconfigureerde oplossing maakt ziet u de beschikbare abonnementen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="8c72e-111">Ten slotte wordt haalt de site alle bronnen in de abonnementen en resourcegroepen gelabeld als vooraf geconfigureerde oplossingen en de tegels op de startpagina wordt gevuld.</span><span class="sxs-lookup"><span data-stu-id="8c72e-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="8c72e-112">De volgende secties worden de functies waarmee de toegang tot de vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="8c72e-113">AAD-functies</span><span class="sxs-lookup"><span data-stu-id="8c72e-113">AAD roles</span></span>

<span data-ttu-id="8c72e-114">De AAD-rollen beheren de mogelijkheid inrichten van de vooraf geconfigureerde oplossingen en beheren van gebruikers in een vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="8c72e-115">U vindt meer informatie over beheerdersrollen in AAD in [beheerdersrollen toewijzen in Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="8c72e-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="8c72e-116">Het huidige artikel is gericht op de **hoofdbeheerder** en de **gebruiker** directory-functies gebruikt door de vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="8c72e-117">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="8c72e-117">Global administrator</span></span>

<span data-ttu-id="8c72e-118">Er zijn veel globale beheerders per AAD-tenant:</span><span class="sxs-lookup"><span data-stu-id="8c72e-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="8c72e-119">Wanneer u een AAD-tenant maakt, bent u standaard de globale beheerder van deze tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="8c72e-120">De globale beheerder kan een vooraf geconfigureerde oplossing inricht en krijgt een **Admin** rol voor de toepassing binnen de AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="8c72e-121">Als een andere gebruiker in dezelfde AAD-tenant wordt gemaakt van een toepassing, de standaard-rol te krijgen tot de globale beheerder is **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="8c72e-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="8c72e-122">Een globale beheerder gebruikers toewijzen aan rollen voor toepassingen die gebruikmaken van de [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="8c72e-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="8c72e-123">Domeingebruiker</span><span class="sxs-lookup"><span data-stu-id="8c72e-123">Domain user</span></span>

<span data-ttu-id="8c72e-124">Er zijn veel domeingebruikers per AAD-tenant:</span><span class="sxs-lookup"><span data-stu-id="8c72e-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="8c72e-125">Een domeingebruiker kan inrichten met een vooraf geconfigureerde oplossing via de [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="8c72e-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="8c72e-126">Standaard de domeingebruiker is verleend de **Admin** rol in de betreffende toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="8c72e-127">Een domeingebruiker kan een toepassing maken met het script build.cmd in de [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo], of [azure-iot-verbonden-factory] [ lnk-cf-github-repo] opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8c72e-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="8c72e-128">De standaard-rol te krijgen tot de domeingebruiker is echter **ReadOnly**, omdat een domeingebruiker geen machtiging heeft voor het toewijzen van rollen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="8c72e-129">Als een andere gebruiker in de AAD-tenant wordt gemaakt van een toepassing, de domeingebruiker is toegewezen de **ReadOnly** rol standaard voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="8c72e-130">Rollen voor toepassingen, kan niet worden toegewezen door een domeingebruiker Daarom toevoegen een domeingebruiker niet gebruikers of rollen voor gebruikers voor een toepassing zelfs als ze deze ingericht.</span><span class="sxs-lookup"><span data-stu-id="8c72e-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="8c72e-131">Gastgebruiker</span><span class="sxs-lookup"><span data-stu-id="8c72e-131">Guest User</span></span>

<span data-ttu-id="8c72e-132">Er zijn veel gastgebruikers per AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="8c72e-133">Gastgebruikers hebben een beperkte set rechten in de AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="8c72e-134">Gastgebruikers kunnen niet als gevolg hiervan voorzien in een vooraf geconfigureerde oplossing in de AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="8c72e-135">Zie voor meer informatie over gebruikers en rollen in AAD, de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="8c72e-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="8c72e-136">[Gebruikers maken in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="8c72e-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="8c72e-137">[Gebruikers toewijzen aan apps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="8c72e-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="8c72e-138">Beheerdersrollen van Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="8c72e-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="8c72e-139">De Azure-beheerdersrollen bepalen de mogelijkheid een Azure-abonnement toewijzen aan een AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="8c72e-140">Meer informatie over de Azure-beheerdersrollen in het artikel [toevoegen of wijzigen Medebeheerder van Azure, servicebeheerder en accountbeheerder][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="8c72e-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="8c72e-141">Toepassingsrollen</span><span class="sxs-lookup"><span data-stu-id="8c72e-141">Application roles</span></span>

<span data-ttu-id="8c72e-142">De rollen van de toepassing toegang tot apparaten in uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="8c72e-143">Er zijn twee gedefinieerde rollen en één impliciete rol gedefinieerd in een ingerichte toepassing:</span><span class="sxs-lookup"><span data-stu-id="8c72e-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="8c72e-144">**Admin:** heeft volledig beheer wilt toevoegen, beheren, verwijderen van apparaten en instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="8c72e-145">**Alleen-lezen:** apparaten, regels, taken, acties en telemetrie kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="8c72e-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="8c72e-146">U vindt de machtigingen worden toegewezen aan elke rol in de [RolePermissions.cs] [ lnk-resource-cs] bronbestand.</span><span class="sxs-lookup"><span data-stu-id="8c72e-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="8c72e-147">Het wijzigen van de rollen van de toepassing voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="8c72e-147">Changing application roles for a user</span></span>

<span data-ttu-id="8c72e-148">U kunt de volgende procedure om een gebruiker in uw Active Directory een beheerder van uw vooraf geconfigureerde oplossing maken.</span><span class="sxs-lookup"><span data-stu-id="8c72e-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="8c72e-149">U moet een globale beheerder van de AAD functies voor een gebruiker te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="8c72e-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="8c72e-150">Ga naar [Azure Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="8c72e-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="8c72e-151">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c72e-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="8c72e-152">Zorg ervoor dat u de map die u hebt gekozen bij het inrichten van uw oplossing op azureiotsuite.com werkt.</span><span class="sxs-lookup"><span data-stu-id="8c72e-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="8c72e-153">Als u meerdere mappen die zijn gekoppeld aan uw abonnement hebt, kunt u schakelen tussen deze als u de naam van uw account in de rechterbovenhoek van de portal op.</span><span class="sxs-lookup"><span data-stu-id="8c72e-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="8c72e-154">Klik op **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8c72e-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="8c72e-155">Weergeven **alle toepassingen** met **eventuele** status.</span><span class="sxs-lookup"><span data-stu-id="8c72e-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="8c72e-156">Zoek vervolgens naar een toepassing met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="8c72e-157">Klik op de naam van de toepassing die overeenkomt met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="8c72e-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="8c72e-158">Klik op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8c72e-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="8c72e-159">Selecteer de gebruiker die u wilt overschakelen van rollen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="8c72e-160">Klik op **toewijzen** en selecteer de rol (zoals **Admin**) u wilt toewijzen aan de gebruiker, klikt u op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="8c72e-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="8c72e-161">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="8c72e-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="8c72e-162">Ik ben een servicebeheerder en ik wil de directory toewijzing tussen mijn abonnement en een specifieke AAD-tenant wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="8c72e-163">Hoe worden deze taak voltooien?</span><span class="sxs-lookup"><span data-stu-id="8c72e-163">How do I complete this task?</span></span>

1. <span data-ttu-id="8c72e-164">Ga naar de [klassieke Azure-portal][lnk-classic-portal], klikt u op **instellingen** in de lijst met services aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="8c72e-165">Selecteer het abonnement dat u wilt de toewijzing van de map te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8c72e-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="8c72e-166">Klik op **Directory bewerken**.</span><span class="sxs-lookup"><span data-stu-id="8c72e-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="8c72e-167">Selecteer de **Directory** u wilt gebruiken in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8c72e-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="8c72e-168">Klik op de pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="8c72e-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="8c72e-169">Bevestig de toewijzing van de map en van invloed op een CO-beheerders.</span><span class="sxs-lookup"><span data-stu-id="8c72e-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="8c72e-170">Als u van een andere map verplaatst, worden alle medebeheerders uit de oorspronkelijke directory verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8c72e-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="8c72e-171">Ik ben gebruiker/lid van een domein op de AAD-tenant en ik een vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c72e-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="8c72e-172">Hoe ik ophalen een bepaalde rol voor de toepassing?</span><span class="sxs-lookup"><span data-stu-id="8c72e-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="8c72e-173">Vraag een globale beheerder moet u een globale beheerder op de AAD-tenant en vervolgens rollen toewijzen aan gebruikers zelf.</span><span class="sxs-lookup"><span data-stu-id="8c72e-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="8c72e-174">U kunt ook vragen om toe te wijzen u rechtstreeks een rol globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="8c72e-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="8c72e-175">Als u de AAD-tenant wijzigen uw vooraf geconfigureerde oplossing is geïmplementeerd als u wilt, Zie de volgende vraag.</span><span class="sxs-lookup"><span data-stu-id="8c72e-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="8c72e-176">Hoe schakel ik mijn vooraf geconfigureerde oplossing voor externe controle en de toepassing zijn toegewezen aan de AAD-tenant?</span><span class="sxs-lookup"><span data-stu-id="8c72e-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="8c72e-177">U kunt een cloudimplementatie uit uitvoeren <https://github.com/Azure/azure-iot-remote-monitoring> en implementeren met een nieuwe AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="8c72e-178">Omdat u bent, standaard een globale beheerder bij het maken van een AAD-tenant, hebt u machtigingen voor het toevoegen van gebruikers en rollen voor deze gebruikers toewijst.</span><span class="sxs-lookup"><span data-stu-id="8c72e-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="8c72e-179">Maak een AAD-directory in de [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="8c72e-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="8c72e-180">Ga naar <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="8c72e-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="8c72e-181">Voer `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (bijvoorbeeld `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="8c72e-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="8c72e-182">Als u wordt gevraagd, stelt de **tenantid** worden de nieuwe tenant in plaats van uw vorige tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="8c72e-183">Ik wil een servicebeheerder of Medebeheerder wanneer aangemeld met een organisatorische account wijzigen</span><span class="sxs-lookup"><span data-stu-id="8c72e-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="8c72e-184">Zie het ondersteuningsartikel [wijzigen servicebeheerder en Medebeheerder wanneer aangemeld met een account organisatorische][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="8c72e-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="8c72e-185">Waarom krijg ik deze fout te zien?</span><span class="sxs-lookup"><span data-stu-id="8c72e-185">Why am I seeing this error?</span></span> <span data-ttu-id="8c72e-186">'Uw account heeft niet de juiste machtigingen om een oplossing te maken.</span><span class="sxs-lookup"><span data-stu-id="8c72e-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="8c72e-187">Neem contact op met uw accountbeheerder of probeer met een ander account."</span><span class="sxs-lookup"><span data-stu-id="8c72e-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="8c72e-188">Bekijk het volgende diagram voor richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="8c72e-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="8c72e-189">Als u doorgaat om te zien de fout na de validatie u een globale beheerder op de AAD-tenant en medebeheerder voor het abonnement zijn, de beheerder van uw account de gebruiker te verwijderen en opnieuw toewijzen van benodigde machtiging in deze volgorde hebben.</span><span class="sxs-lookup"><span data-stu-id="8c72e-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="8c72e-190">Eerst de gebruiker als een globale beheerder toevoegen en vervolgens gebruiker toevoegen als medebeheerder van het Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8c72e-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="8c72e-191">Als de problemen zich blijven voordoen, neem dan contact op met [Help en ondersteuning voor][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="8c72e-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="8c72e-192">Waarom krijg ik deze fout zien wanneer ik een Azure-abonnement hebben?</span><span class="sxs-lookup"><span data-stu-id="8c72e-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="8c72e-193">"Een Azure-abonnement is vereist om vooraf geconfigureerde oplossingen te maken.</span><span class="sxs-lookup"><span data-stu-id="8c72e-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="8c72e-194">U kunt een gratis proefaccount maken binnen een paar minuten."</span><span class="sxs-lookup"><span data-stu-id="8c72e-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="8c72e-195">Als u zeker weet dat u hebt een Azure-abonnement valideren van de huurder toewijzen voor uw abonnement en zorg ervoor dat de juiste tenant is geselecteerd in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8c72e-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="8c72e-196">Als u hebt gevalideerd de gewenste tenant juist is, volgt u de voorgaande diagram en valideren van de toewijzing van uw abonnement en deze AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8c72e-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c72e-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c72e-197">Next steps</span></span>
<span data-ttu-id="8c72e-198">Zie hoe u kunt om door te gaan leren over IoT Suite [aanpassen van een vooraf geconfigureerde oplossing][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="8c72e-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
