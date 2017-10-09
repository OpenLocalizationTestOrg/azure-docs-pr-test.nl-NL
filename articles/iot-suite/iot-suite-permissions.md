---
title: aaaAzure IoT Suite en Azure Active Directory | Microsoft Docs
description: Hierin wordt beschreven hoe Azure IoT Suite maakt gebruik van Azure Active Directory toomanage machtigingen.
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="558d1-103">Machtigingen op Hallo azureiotsuite.com site</span><span class="sxs-lookup"><span data-stu-id="558d1-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="558d1-104">Wat gebeurt er wanneer u zich aanmeldt</span><span class="sxs-lookup"><span data-stu-id="558d1-104">What happens when you sign in</span></span>

<span data-ttu-id="558d1-105">eerste keer dat u zich aanmelden op Hallo [azureiotsuite.com][lnk-azureiotsuite], Hallo site bepaalt aan Hallo machtigingsniveaus hebben op basis van Hallo momenteel geselecteerde tenant van Azure Active Directory (AAD) en Azure abonnement.</span><span class="sxs-lookup"><span data-stu-id="558d1-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="558d1-106">Eerst toopopulate Hallo lijst van de volgende tooyour gebruikersnaam tenants gezien Hallo site vindt uit van Azure welke AAD tenants u deel uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="558d1-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="558d1-107">Hallo site kan op dit moment alleen gebruikerstokens voor één tenant verkrijgen tegelijk.</span><span class="sxs-lookup"><span data-stu-id="558d1-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="558d1-108">Daarom wanneer u tenants met behulp van Hallo vervolgkeuzelijst in de rechterbovenhoek hello overschakelt, registreert Hallo site u in toothat tenant tooobtain Hallo tokens voor deze tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="558d1-109">Hallo-site vindt vervolgens uit vanuit Azure welke abonnementen u hebt gekoppeld aan Hallo tenant geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="558d1-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="558d1-110">Beschikbare abonnementen Hallo ziet u wanneer u een nieuwe vooraf geconfigureerde oplossing maakt.</span><span class="sxs-lookup"><span data-stu-id="558d1-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="558d1-111">Ten slotte Hallo site haalt alle bronnen op Hallo in Hallo abonnementen en resourcegroepen gelabeld als vooraf geconfigureerde oplossingen en Hallo tegels op Hallo-startpagina gevuld.</span><span class="sxs-lookup"><span data-stu-id="558d1-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="558d1-112">Hallo volgende secties beschrijven Hallo-functies waarmee toegang toohello vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="558d1-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="558d1-113">AAD-functies</span><span class="sxs-lookup"><span data-stu-id="558d1-113">AAD roles</span></span>

<span data-ttu-id="558d1-114">Hallo AAD rollen Hallo mogelijkheid inrichten van de vooraf geconfigureerde oplossingen te controleren en beheren van gebruikers in een vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="558d1-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="558d1-115">U vindt meer informatie over beheerdersrollen in AAD in [beheerdersrollen toewijzen in Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="558d1-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="558d1-116">Hallo huidige artikel is gericht op Hallo **hoofdbeheerder** en Hallo **gebruiker** directory-functies gebruikt door Hallo vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="558d1-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="558d1-117">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="558d1-117">Global administrator</span></span>

<span data-ttu-id="558d1-118">Er zijn veel globale beheerders per AAD-tenant:</span><span class="sxs-lookup"><span data-stu-id="558d1-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="558d1-119">Wanneer u een AAD-tenant maakt, bent u door standaard Hallo globale beheerder van deze tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="558d1-120">Hallo-hoofdbeheerder kan een vooraf geconfigureerde oplossing inricht en is toegewezen een **Admin** rol voor de toepassing hello binnen hun AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="558d1-121">Als een andere gebruiker in dezelfde Hallo AAD-tenant wordt gemaakt van een toepassing, Hallo standaardrol verleend toohello globale beheerder is **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="558d1-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="558d1-122">Een globale beheerder tooroles voor toepassingen die gebruikmaken van Hallo gebruikers kunt toewijzen [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="558d1-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="558d1-123">Domeingebruiker</span><span class="sxs-lookup"><span data-stu-id="558d1-123">Domain user</span></span>

<span data-ttu-id="558d1-124">Er zijn veel domeingebruikers per AAD-tenant:</span><span class="sxs-lookup"><span data-stu-id="558d1-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="558d1-125">Een domeingebruiker kan inrichten met een vooraf geconfigureerde oplossing via Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="558d1-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="558d1-126">Standaard krijgt domeingebruiker Hallo Hallo **Admin** rol in Hallo ingericht toepassing.</span><span class="sxs-lookup"><span data-stu-id="558d1-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="558d1-127">Een domeingebruiker kan een toepassing maken met Hallo build.cmd script in Hallo [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance] [ lnk-pm-github-repo], of [azure-iot-verbonden-factory] [ lnk-cf-github-repo] opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="558d1-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="558d1-128">Echter Hallo standaardrol verleend toohello domeingebruiker is **ReadOnly**, omdat een domeingebruiker geen machtiging tooassign rollen heeft.</span><span class="sxs-lookup"><span data-stu-id="558d1-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="558d1-129">Als een andere gebruiker op Hallo AAD-tenant wordt gemaakt van een toepassing, de domeingebruiker Hallo Hallo is toegewezen **ReadOnly** rol standaard voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="558d1-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="558d1-130">Rollen voor toepassingen, kan niet worden toegewezen door een domeingebruiker Daarom toevoegen een domeingebruiker niet gebruikers of rollen voor gebruikers voor een toepassing zelfs als ze deze ingericht.</span><span class="sxs-lookup"><span data-stu-id="558d1-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="558d1-131">Gastgebruiker</span><span class="sxs-lookup"><span data-stu-id="558d1-131">Guest User</span></span>

<span data-ttu-id="558d1-132">Er zijn veel gastgebruikers per AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="558d1-133">Gastgebruikers hebben een beperkte set rechten in Hallo AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="558d1-134">Gastgebruikers kunnen niet als gevolg hiervan voorzien in een vooraf geconfigureerde oplossing in Hallo AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="558d1-135">Zie voor meer informatie over gebruikers en rollen in AAD Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="558d1-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="558d1-136">[Gebruikers maken in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="558d1-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="558d1-137">[Gebruikers tooapps toewijzen][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="558d1-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="558d1-138">Beheerdersrollen van Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="558d1-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="558d1-139">Hello Azure-beheerdersrollen beheren Hallo mogelijkheid toomap een Azure-abonnement tooan AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="558d1-140">Meer informatie over hello Azure beheerdersrollen in Hallo artikel [hoe tooadd of Medebeheerder van Azure, servicebeheerder en accountbeheerder wijzigen][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="558d1-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="558d1-141">Toepassingsrollen</span><span class="sxs-lookup"><span data-stu-id="558d1-141">Application roles</span></span>

<span data-ttu-id="558d1-142">Hallo toepassingsrollen beheren toodevices toegang in uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="558d1-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="558d1-143">Er zijn twee gedefinieerde rollen en één impliciete rol gedefinieerd in een ingerichte toepassing:</span><span class="sxs-lookup"><span data-stu-id="558d1-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="558d1-144">**Admin:** heeft volledig beheer tooadd, beheren, verwijdert u apparaten en instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="558d1-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="558d1-145">**Alleen-lezen:** apparaten, regels, taken, acties en telemetrie kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="558d1-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="558d1-146">U vindt Hallo machtigingen toegewezen tooeach rol in Hallo [RolePermissions.cs] [ lnk-resource-cs] bronbestand.</span><span class="sxs-lookup"><span data-stu-id="558d1-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="558d1-147">Het wijzigen van de rollen van de toepassing voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="558d1-147">Changing application roles for a user</span></span>

<span data-ttu-id="558d1-148">U kunt hello te volgen procedure toomake een gebruiker in uw Active Directory-beheerder van uw vooraf geconfigureerde oplossing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="558d1-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="558d1-149">U moet een AAD globale toochange beheerdersrollen voor een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="558d1-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="558d1-150">Ga toohello [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="558d1-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="558d1-151">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="558d1-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="558d1-152">Zorg ervoor dat u Hallo-directory die u hebt gekozen bij het inrichten van uw oplossing op azureiotsuite.com werkt.</span><span class="sxs-lookup"><span data-stu-id="558d1-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="558d1-153">Als u meerdere mappen die zijn gekoppeld aan uw abonnement hebt, kunt u schakelen tussen deze als u de naam van uw account op Hallo rechtsboven van Hallo-portal op.</span><span class="sxs-lookup"><span data-stu-id="558d1-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="558d1-154">Klik op **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="558d1-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="558d1-155">Weergeven **alle toepassingen** met **eventuele** status.</span><span class="sxs-lookup"><span data-stu-id="558d1-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="558d1-156">Zoek vervolgens naar een toepassing met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="558d1-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="558d1-157">Klik op Hallo-naam van de toepassing hello die overeenkomt met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="558d1-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="558d1-158">Klik op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="558d1-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="558d1-159">Selecteer Hallo gebruiker gewenste tooswitch rollen.</span><span class="sxs-lookup"><span data-stu-id="558d1-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="558d1-160">Klik op **toewijzen** en selecteer Hallo-rol (zoals **Admin**) gewenst tooassign toohello gebruiker, klikt u op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="558d1-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="558d1-161">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="558d1-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="558d1-162">Ik ben een servicebeheerder en toewijzing van toochange Hallo map staat wilt tussen mijn abonnement en een specifieke AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="558d1-163">Hoe worden deze taak voltooien?</span><span class="sxs-lookup"><span data-stu-id="558d1-163">How do I complete this task?</span></span>

1. <span data-ttu-id="558d1-164">Ga toohello [klassieke Azure-portal][lnk-classic-portal], klikt u op **instellingen** in Hallo lijst met services aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="558d1-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="558d1-165">Hallo abonnement toewijzing van toochange Hallo map te gewenst selecteren.</span><span class="sxs-lookup"><span data-stu-id="558d1-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="558d1-166">Klik op **Directory bewerken**.</span><span class="sxs-lookup"><span data-stu-id="558d1-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="558d1-167">Selecteer Hallo **Directory** gewenst toouse Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="558d1-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="558d1-168">Klik op Hallo pijl naar rechts.</span><span class="sxs-lookup"><span data-stu-id="558d1-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="558d1-169">Toewijzing van de map Hallo bevestigen en van invloed op een CO-beheerders.</span><span class="sxs-lookup"><span data-stu-id="558d1-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="558d1-170">Als u van een andere map verplaatst, worden alle Hallo medebeheerders uit de oorspronkelijke directory Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="558d1-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="558d1-171">Ik ben gebruiker/lid van een domein op Hallo AAD-tenant en ik een vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="558d1-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="558d1-172">Hoe ik ophalen een bepaalde rol voor de toepassing?</span><span class="sxs-lookup"><span data-stu-id="558d1-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="558d1-173">Een globale beheerder toomake vraagt u een globale beheerder zijn op Hallo AAD-tenant en rollen toousers uzelf toewijzen.</span><span class="sxs-lookup"><span data-stu-id="558d1-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="558d1-174">U kunt ook een globale beheerder tooassign vragen u rechtstreeks een rol.</span><span class="sxs-lookup"><span data-stu-id="558d1-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="558d1-175">Als u uw vooraf geconfigureerde oplossing is geïmplementeerd dat wilt voor van toochange Hallo AAD-tenant, ziet u Hallo volgende vraag.</span><span class="sxs-lookup"><span data-stu-id="558d1-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="558d1-176">Hoe schakel ik Hallo AAD-tenant die mijn vooraf geconfigureerde oplossing voor externe controle en de toepassing zijn toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="558d1-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="558d1-177">U kunt een cloudimplementatie uit uitvoeren <https://github.com/Azure/azure-iot-remote-monitoring> en implementeren met een nieuwe AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="558d1-178">Omdat u standaard een globale beheerder bent wanneer u een AAD-tenant, maakt u machtigingen tooadd gebruikers en rollen toewijzen toothose gebruikers.</span><span class="sxs-lookup"><span data-stu-id="558d1-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="558d1-179">Maak een AAD-directory in Hallo [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="558d1-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="558d1-180">Ga te<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="558d1-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="558d1-181">Voer `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (bijvoorbeeld `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="558d1-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="558d1-182">Als u wordt gevraagd, stelt u Hallo **tenantid** toobe uw nieuwe tenant in plaats van uw vorige tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="558d1-183">Ik wil toochange een servicebeheerder of Medebeheerder wanneer aangemeld met een account organisatorische</span><span class="sxs-lookup"><span data-stu-id="558d1-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="558d1-184">Zie Hallo ondersteuning-artikel [wijzigen servicebeheerder en Medebeheerder wanneer aangemeld met een account organisatorische][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="558d1-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="558d1-185">Waarom krijg ik deze fout te zien?</span><span class="sxs-lookup"><span data-stu-id="558d1-185">Why am I seeing this error?</span></span> <span data-ttu-id="558d1-186">'Uw account heeft geen Hallo juiste machtigingen toocreate een oplossing.</span><span class="sxs-lookup"><span data-stu-id="558d1-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="558d1-187">Neem contact op met uw accountbeheerder of probeer met een ander account."</span><span class="sxs-lookup"><span data-stu-id="558d1-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="558d1-188">Bekijkt hello diagram voor richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="558d1-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="558d1-189">Als u doorgaat toosee Hallo fout na het valideren van een globale beheerder zijn op Hallo AAD-tenant en medebeheerder op Hallo abonnement, hebt u uw accountbeheerder Hallo gebruiker verwijderen en opnieuw toewijzen van benodigde machtiging in deze volgorde.</span><span class="sxs-lookup"><span data-stu-id="558d1-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="558d1-190">Eerst Hallo gebruiker toevoegen als een globale beheerder bent en vervolgens gebruiker toevoegen als medebeheerder op Hallo Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="558d1-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="558d1-191">Als de problemen zich blijven voordoen, neem dan contact op met [Help en ondersteuning voor][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="558d1-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="558d1-192">Waarom krijg ik deze fout zien wanneer ik een Azure-abonnement hebben?</span><span class="sxs-lookup"><span data-stu-id="558d1-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="558d1-193">"Een Azure-abonnement is vereist toocreate vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="558d1-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="558d1-194">U kunt een gratis proefaccount maken binnen een paar minuten."</span><span class="sxs-lookup"><span data-stu-id="558d1-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="558d1-195">Als u zeker weet dat u hebt een Azure-abonnement, Hallo huurder toewijzen voor uw abonnement te valideren en controleer Hallo juist tenant is geselecteerd in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="558d1-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="558d1-196">Als u hebt gevalideerd Hallo gewenst tenant klopt, volg Hallo voorgaande diagram en valideren van Hallo toewijzing van uw abonnement en deze AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="558d1-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="558d1-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="558d1-197">Next steps</span></span>
<span data-ttu-id="558d1-198">meer informatie over IoT Suite toocontinue Zie hoe u kunt [aanpassen van een vooraf geconfigureerde oplossing][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="558d1-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
