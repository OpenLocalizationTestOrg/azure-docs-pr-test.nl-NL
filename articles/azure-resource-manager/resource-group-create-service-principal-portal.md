---
title: aaaCreate identiteit voor Azure portal-app | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate een nieuwe Azure Active Directory-toepassing en service-principal die kan worden gebruikt met Hallo rollen gebaseerd toegangsbeheer in Azure Resource Manager toomanage toegang tooresources tot.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="d6811-103">Gebruik van toocreate portal een Azure Active Directory-toepassing en service-principal die toegang bronnen tot</span><span class="sxs-lookup"><span data-stu-id="d6811-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="d6811-104">Wanneer u een toepassing die moet tooaccess of wijzigen van resources hebt, moet u een Azure Active Directory (AD)-toepassing instellen en Hallo vereist machtigingen tooit toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d6811-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="d6811-105">Deze aanpak is beter toorunning Hallo app met uw eigen referenties, omdat:</span><span class="sxs-lookup"><span data-stu-id="d6811-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="d6811-106">U kunt machtigingen toohello app identiteit die anders zijn dan uw eigen machtigingen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d6811-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="d6811-107">Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.</span><span class="sxs-lookup"><span data-stu-id="d6811-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="d6811-108">U hebt geen toochange Hallo app referenties als uw verantwoordelijkheden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d6811-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="d6811-109">U kunt een tooautomate certificaatverificatie gebruiken bij het uitvoeren van een onbewaakt script.</span><span class="sxs-lookup"><span data-stu-id="d6811-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="d6811-110">Dit onderwerp leest u hoe tooperform die stapsgewijs Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d6811-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="d6811-111">Het is gericht op een één-tenant-toepassing waarbij de toepassing hello beoogde toorun binnen één organisatie is.</span><span class="sxs-lookup"><span data-stu-id="d6811-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="d6811-112">Doorgaans gebruikt toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd binnen uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="d6811-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="d6811-113">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="d6811-113">Required permissions</span></span>
<span data-ttu-id="d6811-114">toocomplete in dit onderwerp, moet u voldoende machtigingen tooregister een toepassing hebt met uw Azure AD-tenant en de toepassingsrol tooa Hallo toewijzen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6811-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="d6811-115">Zorg ervoor dat u deze stappen tooperform van Hallo juiste machtigingen hebt.</span><span class="sxs-lookup"><span data-stu-id="d6811-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="d6811-116">Controleer de machtigingen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6811-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="d6811-117">Meld u bij tooyour Azure-Account via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6811-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6811-118">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6811-118">Select **Azure Active Directory**.</span></span>

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="d6811-120">Selecteer in Azure Active Directory, **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="d6811-120">In Azure Active Directory, select **User settings**.</span></span>

     ![gebruikersinstellingen voor de selecteren](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="d6811-122">Controleer de Hallo **App registraties** instelling.</span><span class="sxs-lookup"><span data-stu-id="d6811-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="d6811-123">Als instellen te**Ja**, niet-beheerders kunnen zich registreren AD-apps.</span><span class="sxs-lookup"><span data-stu-id="d6811-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="d6811-124">Deze instelling betekent dat elke gebruiker in Azure AD-tenant Hallo een app kunt registreren.</span><span class="sxs-lookup"><span data-stu-id="d6811-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="d6811-125">U kunt verdergaan te[controleren Azure-abonnement machtigingen](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="d6811-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![app-registraties weergeven](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="d6811-127">Als Hallo app registraties instellen te is ingesteld**Nee**, alleen de beheerder gebruikers apps kunnen registreren.</span><span class="sxs-lookup"><span data-stu-id="d6811-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="d6811-128">U moet toocheck of uw account een beheerder voor hello Azure AD-tenant is.</span><span class="sxs-lookup"><span data-stu-id="d6811-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="d6811-129">Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.</span><span class="sxs-lookup"><span data-stu-id="d6811-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="d6811-131">Zoek uw account en selecteren wanneer u deze vinden.</span><span class="sxs-lookup"><span data-stu-id="d6811-131">Search for your account, and select it when you find it.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="d6811-133">Selecteer voor uw account **functie Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6811-133">For your account, select **Directory role**.</span></span> 

     ![Directory-rol](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="d6811-135">De functie toegewezen directory weergeven in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6811-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="d6811-136">Als uw account toohello gebruikersrol is toegewezen, maar hello app registratie-instelling (Hallo vorige stappen) beperkt tooadmin gebruikers is, vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d6811-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![de rol weergeven](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="d6811-138">Controleer de machtigingen van de Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="d6811-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="d6811-139">In uw Azure-abonnement, uw account moet hebben `Microsoft.Authorization/*/Write` toegang tot een rol AD app tooa tooassign.</span><span class="sxs-lookup"><span data-stu-id="d6811-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="d6811-140">Deze actie wordt verleend via Hallo [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) rol of [beheerder voor gebruikerstoegang](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol.</span><span class="sxs-lookup"><span data-stu-id="d6811-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="d6811-141">Als uw account is toegewezen toohello **Inzender** rol, u hebt niet de juiste machtiging.</span><span class="sxs-lookup"><span data-stu-id="d6811-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="d6811-142">U ontvangt een fout opgetreden tijdens een poging de functie tooassign Hallo service-principal tooa.</span><span class="sxs-lookup"><span data-stu-id="d6811-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="d6811-143">toocheck machtigingen voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="d6811-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="d6811-144">Als u niet al op uw Azure AD-account van de vorige stappen hello, selecteer **Azure Active Directory** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6811-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="d6811-145">Uw Azure AD-account vinden.</span><span class="sxs-lookup"><span data-stu-id="d6811-145">Find your Azure AD account.</span></span> <span data-ttu-id="d6811-146">Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.</span><span class="sxs-lookup"><span data-stu-id="d6811-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="d6811-148">Zoek uw account en selecteren wanneer u deze vinden.</span><span class="sxs-lookup"><span data-stu-id="d6811-148">Search for your account, and select it when you find it.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="d6811-150">Selecteer **Azure-resources**.</span><span class="sxs-lookup"><span data-stu-id="d6811-150">Select **Azure resources**.</span></span>

     ![Selecteer resources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="d6811-152">De toegewezen rollen weergeven en bepalen of u onvoldoende machtigingen tooassign een AD-app tooa rol hebt.</span><span class="sxs-lookup"><span data-stu-id="d6811-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="d6811-153">Als dit niet het geval is, vraagt u uw abonnement beheerder tooadd u tooUser toegang beheerdersrol.</span><span class="sxs-lookup"><span data-stu-id="d6811-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="d6811-154">Hallo installatiekopie te volgen, is Hallo gebruiker toegewezen toohello rol van eigenaar voor twee abonnementen, wat betekent dat die de gebruiker heeft onvoldoende machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d6811-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![machtigingen weergeven](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="d6811-156">Een Azure Active Directory-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="d6811-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="d6811-157">Meld u bij tooyour Azure-Account via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6811-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6811-158">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6811-158">Select **Azure Active Directory**.</span></span>

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="d6811-160">Selecteer **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="d6811-160">Select **App registrations**.</span></span>   

     ![Selecteer de app-registraties](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="d6811-162">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d6811-162">Select **Add**.</span></span>

     ![app toevoegen](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="d6811-164">Geef een naam en de URL voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d6811-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="d6811-165">Selecteer een **Web-app / API** of **systeemeigen** Hallo type toepassing dat u wilt toocreate.</span><span class="sxs-lookup"><span data-stu-id="d6811-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="d6811-166">Na het Hallo-waarden instellen, selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="d6811-166">After setting hello values, select **Create**.</span></span>

     ![de naam van toepassing](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="d6811-168">U kunt uw toepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d6811-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="d6811-169">Ophalen van de sleutel-ID en verificatie van toepassing</span><span class="sxs-lookup"><span data-stu-id="d6811-169">Get application ID and authentication key</span></span>
<span data-ttu-id="d6811-170">Wanneer u programmatisch zich aanmeldt, moet u Hallo-ID voor uw toepassing en een verificatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="d6811-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="d6811-171">tooget deze waarden, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6811-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="d6811-172">Van **App registraties** in Azure Active Directory, selecteer uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6811-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![toepassing selecteren](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="d6811-174">Kopiëren Hallo **toepassings-ID** en op te slaan in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="d6811-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="d6811-175">toepassingen in Hallo Hallo [voorbeeldtoepassingen](#sample-applications) sectie toothis-waarde als de client-id Hallo verwijzen.</span><span class="sxs-lookup"><span data-stu-id="d6811-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![client-id](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="d6811-177">Selecteer een verificatiesleutel toogenerate **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="d6811-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![Selecteer sleutels](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="d6811-179">Geef een beschrijving van het Hallo-sleutel en een duur voor het Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="d6811-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="d6811-180">Wanneer u klaar bent, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d6811-180">When done, select **Save**.</span></span>

     ![sleutel opslaan](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="d6811-182">Na het opslaan van sleutel Hallo wordt Hallo-waarde van Hallo-sleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6811-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="d6811-183">Deze waarde niet kopiëren omdat u niet kunnen tooretrieve Hallo sleutel later bent.</span><span class="sxs-lookup"><span data-stu-id="d6811-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="d6811-184">U geeft sleutelwaarde Hallo Hallo toepassing ID toolog in als de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d6811-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="d6811-185">Opslaan Hallo sleutelwaarde waar uw toepassing deze kan worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d6811-185">Store hello key value where your application can retrieve it.</span></span>

     ![sleutel wordt opgeslagen](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="d6811-187">Tenant-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="d6811-187">Get tenant ID</span></span>
<span data-ttu-id="d6811-188">Wanneer u programmatisch zich aanmeldt, moet u toopass hello tenant-ID bij uw verificatieaanvraag.</span><span class="sxs-lookup"><span data-stu-id="d6811-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="d6811-189">tooget hello tenant-ID, selecteer **eigenschappen** voor uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d6811-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Azure AD-eigenschappen selecteren](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="d6811-191">Kopiëren Hallo **map-ID**.</span><span class="sxs-lookup"><span data-stu-id="d6811-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="d6811-192">Deze waarde is uw tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="d6811-192">This value is your tenant ID.</span></span>

     ![tenant-id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="d6811-194">Toepassing toorole toewijzen</span><span class="sxs-lookup"><span data-stu-id="d6811-194">Assign application toorole</span></span>
<span data-ttu-id="d6811-195">tooaccess resources in uw abonnement, moet u de toepassingsrol tooa Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d6811-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="d6811-196">Bepaal welke rol Hallo juiste machtigingen voor de toepassing hello vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="d6811-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="d6811-197">toolearn over de beschikbare functies hello, Zie [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d6811-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="d6811-198">U kunt Hallo bereik instellen op Hallo niveau van het Hallo-abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="d6811-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="d6811-199">Machtigingen zijn overgenomen toolower niveaus van het bereik.</span><span class="sxs-lookup"><span data-stu-id="d6811-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="d6811-200">Bijvoorbeeld, vindt het toevoegen van dat een toepassing toohello lezersrol voor een resourcegroep betekent dat Hallo-resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="d6811-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="d6811-201">Toohello niveau van scope tooassign Hallo toepassing om te gewenst gaan.</span><span class="sxs-lookup"><span data-stu-id="d6811-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="d6811-202">Bijvoorbeeld tooassign een rol op Hallo abonnementsbereik, selecteert u **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="d6811-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="d6811-203">U kunt in plaats daarvan een resourcegroep of resource selecteren.</span><span class="sxs-lookup"><span data-stu-id="d6811-203">You could instead select a resource group or resource.</span></span>

     ![Abonnement selecteren](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="d6811-205">Hallo bepaald abonnement (resourcegroep of resource) tooassign Hallo toepassing te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d6811-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![Selecteer het abonnement voor de toewijzing](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="d6811-207">Selecteer **toegangsbeheer (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="d6811-207">Select **Access Control (IAM)**.</span></span>

     ![Selecteer toegang](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="d6811-209">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d6811-209">Select **Add**.</span></span>

     ![Selecteer toevoegen](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="d6811-211">Selecteer desgewenst tooassign toohello toepassing hello-rol.</span><span class="sxs-lookup"><span data-stu-id="d6811-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="d6811-212">Hallo volgende afbeelding toont Hallo **lezer** rol.</span><span class="sxs-lookup"><span data-stu-id="d6811-212">hello following image shows hello **Reader** role.</span></span>

     ![rol selecteren](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="d6811-214">Zoeken naar uw toepassing en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="d6811-214">Search for your application, and select it.</span></span>

     ![Zoek app](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="d6811-216">Selecteer **OK** toofinish Hallo rol toewijst.</span><span class="sxs-lookup"><span data-stu-id="d6811-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="d6811-217">Ziet u uw toepassing in de lijst Hallo tooa rol voor deze scope toegewezen aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d6811-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="d6811-218">Meld u aan als de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="d6811-218">Log in as hello application</span></span>

<span data-ttu-id="d6811-219">Uw toepassing is nu ingesteld in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6811-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="d6811-220">U hebt een ID en sleutel toouse voor aanmelden als Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6811-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="d6811-221">de toepassing Hello is tooa-rol die bepaalde acties die kan uitvoeren, krijgt het toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d6811-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="d6811-222">Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:</span><span class="sxs-lookup"><span data-stu-id="d6811-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="d6811-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6811-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="d6811-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6811-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="d6811-225">REST</span><span class="sxs-lookup"><span data-stu-id="d6811-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="d6811-226">.NET</span><span class="sxs-lookup"><span data-stu-id="d6811-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d6811-227">Java</span><span class="sxs-lookup"><span data-stu-id="d6811-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d6811-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6811-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d6811-229">Python</span><span class="sxs-lookup"><span data-stu-id="d6811-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d6811-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="d6811-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="d6811-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6811-231">Next steps</span></span>
* <span data-ttu-id="d6811-232">Zie tooset van een toepassing met meerdere tenants [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d6811-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d6811-233">toolearn over het opgeven van beveiligingsbeleid, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d6811-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="d6811-234">Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d6811-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
