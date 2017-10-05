---
title: Identiteit voor Azure-app maken in de portal | Microsoft Docs
description: Beschrijft hoe u maakt een nieuwe Azure Active Directory-toepassing en service-principal die kan worden gebruikt met de op rollen gebaseerde toegangsbeheer in Azure Resource Manager voor het beheren van toegang tot bronnen.
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
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="1ae5a-103">Portal gebruiken voor het maken van een Azure Active Directory-toepassing en service-principal die toegang bronnen tot</span><span class="sxs-lookup"><span data-stu-id="1ae5a-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="1ae5a-104">Wanneer u een toepassing die behoeften openen of wijzigen van resources hebt, moet u een Azure Active Directory (AD)-toepassing instellen en de vereiste machtigingen toewijzen aan deze.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="1ae5a-105">Deze aanpak is voorkeur boven het uitvoeren van de app met uw eigen referenties, omdat:</span><span class="sxs-lookup"><span data-stu-id="1ae5a-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="1ae5a-106">U kunt machtigingen toewijzen aan de identiteit van de app die anders zijn dan uw eigen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="1ae5a-107">Deze machtigingen zijn meestal beperkt tot precies wat de app moet doen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="1ae5a-108">U hoeft niet te wijzigen van de app referenties als uw verantwoordelijkheden wijzigt.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="1ae5a-109">U kunt een certificaat gebruiken voor het automatiseren van verificatie bij het uitvoeren van een onbewaakt script.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="1ae5a-110">Dit onderwerp leest u hoe u deze stappen uitvoert via de portal.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="1ae5a-111">Het is gericht op een één-tenant-toepassing waarin de toepassing is bedoeld om uit te voeren binnen één organisatie.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="1ae5a-112">Doorgaans gebruikt toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd binnen uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="1ae5a-113">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="1ae5a-113">Required permissions</span></span>
<span data-ttu-id="1ae5a-114">Als u dit onderwerp, moet u voldoende rechten hebt voor een toepassing registreren met uw Azure AD-tenant en de toepassing toewijzen aan een rol in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="1ae5a-115">Zorg ervoor dat de juiste machtigingen deze stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="1ae5a-116">Controleer de machtigingen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ae5a-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="1ae5a-117">Aanmelden bij uw Azure-Account via de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1ae5a-118">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-118">Select **Azure Active Directory**.</span></span>

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="1ae5a-120">Selecteer in Azure Active Directory, **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-120">In Azure Active Directory, select **User settings**.</span></span>

     ![gebruikersinstellingen voor de selecteren](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="1ae5a-122">Controleer de **App registraties** instelling.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="1ae5a-123">Indien ingesteld op **Ja**, niet-beheerders kunnen zich registreren AD-apps.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="1ae5a-124">Deze instelling betekent dat elke gebruiker in de Azure AD-tenant een app kunt registreren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="1ae5a-125">U kunt verdergaan naar [controleren Azure-abonnement machtigingen](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![app-registraties weergeven](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="1ae5a-127">Als de app-registraties instelling is ingesteld op **Nee**, alleen de beheerder gebruikers apps kunnen registreren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="1ae5a-128">U moet controleren of uw account een beheerder voor de Azure AD-tenant is.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="1ae5a-129">Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="1ae5a-131">Zoek uw account en selecteren wanneer u deze vinden.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-131">Search for your account, and select it when you find it.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="1ae5a-133">Selecteer voor uw account **functie Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-133">For your account, select **Directory role**.</span></span> 

     ![Directory-rol](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="1ae5a-135">De functie toegewezen directory weergeven in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="1ae5a-136">Als uw account is toegewezen aan de gebruikersrol, maar de registratie van app-instelling (van de voorgaande stappen) beperkt tot beheergebruikers is, vraag uw beheerder op een toewijzen aan een administrator-rol of waarmee gebruikers om apps te registreren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![de rol weergeven](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="1ae5a-138">Controleer de machtigingen van de Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="1ae5a-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="1ae5a-139">In uw Azure-abonnement, uw account moet hebben `Microsoft.Authorization/*/Write` toegang tot een AD-app aan een rol toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="1ae5a-140">Deze actie wordt verleend via de [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) rol of [beheerder voor gebruikerstoegang](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="1ae5a-141">Als uw account is toegewezen aan de **Inzender** rol, u hebt niet de juiste machtiging.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="1ae5a-142">U ontvangt een fout opgetreden bij een poging de service-principal toewijzen aan een rol.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="1ae5a-143">Uw abonnement om machtigingen te controleren:</span><span class="sxs-lookup"><span data-stu-id="1ae5a-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="1ae5a-144">Als u niet al uw Azure AD-account van de voorgaande stappen hebt uitgevoerd bekijkt, selecteert u **Azure Active Directory** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="1ae5a-145">Uw Azure AD-account vinden.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-145">Find your Azure AD account.</span></span> <span data-ttu-id="1ae5a-146">Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="1ae5a-148">Zoek uw account en selecteren wanneer u deze vinden.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-148">Search for your account, and select it when you find it.</span></span>

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="1ae5a-150">Selecteer **Azure-resources**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-150">Select **Azure resources**.</span></span>

     ![Selecteer resources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="1ae5a-152">Bekijk uw toegewezen rollen en bepalen of u onvoldoende machtigingen hebt voor het toewijzen van een AD-app aan een rol.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="1ae5a-153">Als dat niet het geval is, vraagt de abonnementsbeheerder van uw u toe te voegen aan de rol beheerder voor gebruikerstoegang.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="1ae5a-154">In de volgende afbeelding wordt de gebruiker toegewezen aan de rol van eigenaar voor twee abonnementen, wat betekent dat die de gebruiker heeft onvoldoende machtigingen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![machtigingen weergeven](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="1ae5a-156">Een Azure Active Directory-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="1ae5a-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="1ae5a-157">Aanmelden bij uw Azure-Account via de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1ae5a-158">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-158">Select **Azure Active Directory**.</span></span>

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="1ae5a-160">Selecteer **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-160">Select **App registrations**.</span></span>   

     ![Selecteer de app-registraties](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="1ae5a-162">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-162">Select **Add**.</span></span>

     ![app toevoegen](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="1ae5a-164">Geef een naam en de URL voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="1ae5a-165">Selecteer een **Web-app / API** of **systeemeigen** voor het type van de toepassing die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="1ae5a-166">Na het instellen van de waarden, selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-166">After setting the values, select **Create**.</span></span>

     ![de naam van toepassing](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="1ae5a-168">U kunt uw toepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="1ae5a-169">Ophalen van de sleutel-ID en verificatie van toepassing</span><span class="sxs-lookup"><span data-stu-id="1ae5a-169">Get application ID and authentication key</span></span>
<span data-ttu-id="1ae5a-170">Wanneer u programmatisch zich aanmeldt, moet u de ID voor uw toepassing en een verificatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="1ae5a-171">Als u deze waarden, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1ae5a-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="1ae5a-172">Van **App registraties** in Azure Active Directory, selecteer uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![toepassing selecteren](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="1ae5a-174">Kopieer de **toepassings-ID** en op te slaan in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="1ae5a-175">De toepassingen in de [voorbeeldtoepassingen](#sample-applications) sectie verwijzen naar deze waarde als de client-id.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![client-id](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="1ae5a-177">Selecteer voor het genereren van een verificatiesleutel **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-177">To generate an authentication key, select **Keys**.</span></span>

     ![Selecteer sleutels](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="1ae5a-179">Geef een beschrijving van de sleutel en een duur voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="1ae5a-180">Wanneer u klaar bent, selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-180">When done, select **Save**.</span></span>

     ![sleutel opslaan](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="1ae5a-182">Na het opslaan van de sleutel, wordt de waarde van de sleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="1ae5a-183">Deze waarde niet kopiëren omdat u niet kan ophalen van de sleutel later.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="1ae5a-184">U kunt de sleutelwaarde opgeven met de toepassings-ID aan te melden als de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="1ae5a-185">Slaat de waarde van de sleutel waar uw toepassing deze kan worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-185">Store the key value where your application can retrieve it.</span></span>

     ![sleutel wordt opgeslagen](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="1ae5a-187">Tenant-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="1ae5a-187">Get tenant ID</span></span>
<span data-ttu-id="1ae5a-188">Wanneer u programmatisch zich aanmeldt, moet u de tenant-ID met de verificatieaanvraag doorgeven.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="1ae5a-189">Als u de tenant-ID, selecteer **eigenschappen** voor uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Azure AD-eigenschappen selecteren](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="1ae5a-191">Kopieer de **map-ID**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="1ae5a-192">Deze waarde is uw tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-192">This value is your tenant ID.</span></span>

     ![tenant-id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="1ae5a-194">Toepassing toewijzen aan rol</span><span class="sxs-lookup"><span data-stu-id="1ae5a-194">Assign application to role</span></span>
<span data-ttu-id="1ae5a-195">Voor toegang tot resources in uw abonnement, moet u de toepassing aan een rol toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="1ae5a-196">Bepaal welke rol vertegenwoordigt de juiste machtigingen voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="1ae5a-197">Zie voor meer informatie over de beschikbare rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="1ae5a-198">U kunt het bereik instellen op het niveau van het abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="1ae5a-199">Machtigingen worden overgenomen op lagere niveaus van het bereik.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="1ae5a-200">Bijvoorbeeld, een toepassing met de rol Lezer voor een resourcegroep toe te voegen dat kan de resourcegroep en alle resources die deze bevat gelezen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="1ae5a-201">Ga naar het niveau van het bereik dat u wilt toewijzen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="1ae5a-202">Selecteer bijvoorbeeld als een rol bij het abonnementsbereik wilt toewijzen, **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="1ae5a-203">U kunt in plaats daarvan een resourcegroep of resource selecteren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-203">You could instead select a resource group or resource.</span></span>

     ![Abonnement selecteren](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="1ae5a-205">Selecteer het bepaald abonnement (resourcegroep of resource) de toepassing toewijzen aan.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![Selecteer het abonnement voor de toewijzing](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="1ae5a-207">Selecteer **toegangsbeheer (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-207">Select **Access Control (IAM)**.</span></span>

     ![Selecteer toegang](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="1ae5a-209">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-209">Select **Add**.</span></span>

     ![Selecteer toevoegen](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="1ae5a-211">Selecteer de rol die u wilt toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="1ae5a-212">De volgende afbeelding toont de **lezer** rol.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-212">The following image shows the **Reader** role.</span></span>

     ![rol selecteren](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="1ae5a-214">Zoeken naar uw toepassing en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-214">Search for your application, and select it.</span></span>

     ![Zoek app](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="1ae5a-216">Selecteer **OK** voltooid de rol toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="1ae5a-217">Ziet u uw toepassing in de lijst met gebruikers die zijn toegewezen aan een rol voor deze scope.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="1ae5a-218">Meld u aan als de toepassing</span><span class="sxs-lookup"><span data-stu-id="1ae5a-218">Log in as the application</span></span>

<span data-ttu-id="1ae5a-219">Uw toepassing is nu ingesteld in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="1ae5a-220">U hebt een ID en -sleutel moet worden gebruikt voor aanmelden als de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="1ae5a-221">De toepassing is toegewezen aan een rol die hieraan bepaalde acties die kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1ae5a-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="1ae5a-222">Zie voor informatie over logboekregistratie in als de toepassing via verschillende platforms:</span><span class="sxs-lookup"><span data-stu-id="1ae5a-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="1ae5a-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ae5a-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="1ae5a-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1ae5a-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="1ae5a-225">REST</span><span class="sxs-lookup"><span data-stu-id="1ae5a-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="1ae5a-226">.NET</span><span class="sxs-lookup"><span data-stu-id="1ae5a-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="1ae5a-227">Java</span><span class="sxs-lookup"><span data-stu-id="1ae5a-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="1ae5a-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="1ae5a-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="1ae5a-229">Python</span><span class="sxs-lookup"><span data-stu-id="1ae5a-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="1ae5a-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="1ae5a-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="1ae5a-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ae5a-231">Next steps</span></span>
* <span data-ttu-id="1ae5a-232">Als u een multitenant-toepassing instelt, Zie [Ontwikkelaarshandleiding voor autorisatie met de Azure Resource Manager-API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="1ae5a-233">Zie voor meer informatie over het opgeven van beveiligingsbeleid [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="1ae5a-234">Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd voor gebruikers, [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="1ae5a-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
