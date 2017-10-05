---
title: Identiteit voor Azure-app maken met Azure CLI | Microsoft Docs
description: "Beschrijft hoe Azure CLI gebruiken voor het maken van een Azure Active Directory-toepassing en service-principal en toegang tot resources via toegangsbeheer op basis van rollen. Er wordt weergegeven hoe toepassing met een wachtwoord of certificaat te verifiëren."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="b8350-104">Azure CLI gebruiken om een service-principal te maken voor toegang tot resources</span><span class="sxs-lookup"><span data-stu-id="b8350-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="b8350-105">Wanneer u een app of een script dat nodig heeft voor toegang tot resources hebt, kunt u een identiteit voor de app instellen en de app met een eigen referenties verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b8350-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="b8350-106">Deze identiteit staat bekend als een service-principal.</span><span class="sxs-lookup"><span data-stu-id="b8350-106">This identity is known as a service principal.</span></span> <span data-ttu-id="b8350-107">Deze aanpak kunt u:</span><span class="sxs-lookup"><span data-stu-id="b8350-107">This approach enables you to:</span></span>

* <span data-ttu-id="b8350-108">Machtigingen toekennen aan de identiteit van de app die anders zijn dan uw eigen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="b8350-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="b8350-109">Deze machtigingen zijn meestal beperkt tot precies wat de app moet doen.</span><span class="sxs-lookup"><span data-stu-id="b8350-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="b8350-110">Een certificaat voor verificatie gebruiken bij het uitvoeren van een onbewaakt script.</span><span class="sxs-lookup"><span data-stu-id="b8350-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="b8350-111">Dit artikel laat zien hoe u [Azure CLI 1.0](../cli-install-nodejs.md) voor het instellen van een toepassing wilt uitvoeren onder een eigen referenties en identiteit.</span><span class="sxs-lookup"><span data-stu-id="b8350-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="b8350-112">Installeer de nieuwste versie van [Azure CLI 1.0](../cli-install-nodejs.md) om ervoor te zorgen dat uw omgeving overeenkomt met de voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b8350-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="b8350-113">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="b8350-113">Required permissions</span></span>
<span data-ttu-id="b8350-114">Als u dit onderwerp, moet u voldoende machtigingen in uw Azure Active Directory en uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="b8350-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="b8350-115">In het bijzonder moet u een app maken in de Azure Active Directory en de service-principal toewijzen aan een rol.</span><span class="sxs-lookup"><span data-stu-id="b8350-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="b8350-116">De eenvoudigste manier om te controleren of uw account over de juiste machtigingen beschikt, verloopt via de portal.</span><span class="sxs-lookup"><span data-stu-id="b8350-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="b8350-117">Zie [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions) (Vereiste machtigingen controleren in de portal).</span><span class="sxs-lookup"><span data-stu-id="b8350-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="b8350-118">Nu gaat u verder met een sectie voor [wachtwoord](#create-service-principal-with-password) of [certificaat](#create-service-principal-with-certificate) verificatie.</span><span class="sxs-lookup"><span data-stu-id="b8350-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="b8350-119">Service-principal maken met wachtwoord</span><span class="sxs-lookup"><span data-stu-id="b8350-119">Create service principal with password</span></span>
<span data-ttu-id="b8350-120">In deze sectie maakt u de stappen voor het maken van de AD-toepassing met een wachtwoord en de rol Lezer toegewezen aan de service-principal.</span><span class="sxs-lookup"><span data-stu-id="b8350-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="b8350-121">Aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="b8350-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="b8350-122">Voor het maken van een app-identiteit bieden u de naam van de app en een wachtwoord, zoals wordt weergegeven in de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b8350-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="b8350-123">De nieuwe service-principal wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b8350-123">The new service principal is returned.</span></span> <span data-ttu-id="b8350-124">De Object-Id is vereist bij het verlenen van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="b8350-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="b8350-125">De guid worden weergegeven met de Service Principal Names is nodig wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="b8350-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="b8350-126">Deze guid is dezelfde waarde als de app-id.</span><span class="sxs-lookup"><span data-stu-id="b8350-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="b8350-127">In de voorbeeldtoepassingen deze waarde wordt aangeduid als de `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="b8350-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="b8350-128">Aan de service principal machtigingen verlenen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b8350-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="b8350-129">In dit voorbeeld kunt u de service-principal toevoegen aan de rol lezer die machtiging toekent voor het lezen van alle resources in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="b8350-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="b8350-130">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b8350-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="b8350-131">Geef de Object-Id die u hebt gebruikt bij het maken van de toepassing voor de object-id-parameter.</span><span class="sxs-lookup"><span data-stu-id="b8350-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="b8350-132">Voordat u deze opdracht uitvoert, moet u even totdat de nieuwe service-principal worden doorgegeven in Azure Active Directory toestaan.</span><span class="sxs-lookup"><span data-stu-id="b8350-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="b8350-133">Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken.</span><span class="sxs-lookup"><span data-stu-id="b8350-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="b8350-134">In een script, moet u een stap in de slaapstand tussen de opdrachten toevoegen (zoals `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="b8350-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="b8350-135">Als u een foutmelding weergegeven dat de principal bestaat niet in de map ziet, voert u de opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="b8350-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="b8350-136">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="b8350-136">That's it!</span></span> <span data-ttu-id="b8350-137">Uw AD-toepassing en service-principal worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b8350-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="b8350-138">De volgende sectie leest u hoe aanmelden met de referentie via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b8350-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="b8350-139">Als u de referentie gebruiken in uw toepassing code wilt, hoeft u niet om door te gaan met dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b8350-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="b8350-140">U kunt naar gaan de [voorbeeldtoepassingen](#sample-applications) voor voorbeelden van aangemeld met uw toepassings-id en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b8350-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="b8350-141">Geef referenties op via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8350-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="b8350-142">Nu moet u zich aanmelden als de toepassing bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8350-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="b8350-143">Wanneer u zich aanmeldt als een service-principal, moet u voor de tenant-id van de map voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="b8350-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="b8350-144">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8350-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="b8350-145">Voor het ophalen van de tenant-id voor uw abonnement op dat moment geverifieerde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b8350-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="b8350-146">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b8350-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="b8350-147">Als u de tenant-id van een ander abonnement ophalen moet, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b8350-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="b8350-148">Als u ophalen van de client-id moet worden gebruikt wilt voor aanmelden, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b8350-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="b8350-149">De waarde moet worden gebruikt voor het aanmelden is de guid die worden vermeld in de SPN-namen.</span><span class="sxs-lookup"><span data-stu-id="b8350-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="b8350-150">Aanmelden als service-principal.</span><span class="sxs-lookup"><span data-stu-id="b8350-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="b8350-151">U wordt gevraagd om het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b8350-151">You are prompted for the password.</span></span> <span data-ttu-id="b8350-152">Geef het wachtwoord die u hebt opgegeven bij het maken van de AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8350-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="b8350-153">U bent nu geautoriseerd als de service-principal voor de service-principal die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b8350-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="b8350-154">U kunt ook de REST-bewerkingen aan te melden vanaf de opdrachtregel aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b8350-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="b8350-155">U kunt het toegangstoken voor gebruik met andere bewerkingen ophalen uit het verificatieantwoord.</span><span class="sxs-lookup"><span data-stu-id="b8350-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="b8350-156">Zie voor een voorbeeld van het ophalen van het toegangstoken door aan te roepen REST-bewerkingen [genereren van een Token toegang](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="b8350-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="b8350-157">Service-principal maken met certificaat</span><span class="sxs-lookup"><span data-stu-id="b8350-157">Create service principal with certificate</span></span>
<span data-ttu-id="b8350-158">In deze sectie kunt u de stappen voor het uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b8350-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="b8350-159">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="b8350-159">create a self-signed certificate</span></span>
* <span data-ttu-id="b8350-160">de AD-toepassing maken met het certificaat en de service-principal</span><span class="sxs-lookup"><span data-stu-id="b8350-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="b8350-161">de rol Lezer toegewezen aan de service-principal</span><span class="sxs-lookup"><span data-stu-id="b8350-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="b8350-162">Deze stappen uit te voeren, moet u hebben [OpenSSL](http://www.openssl.org/) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b8350-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="b8350-163">Een zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="b8350-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="b8350-164">De voorgaande stap twee bestanden - privkey.pem en cert.pem hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b8350-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="b8350-165">De openbare en persoonlijke sleutels worden gecombineerd tot één bestand.</span><span class="sxs-lookup"><span data-stu-id="b8350-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="b8350-166">Open de **examplecert.pem** -bestand en zoek naar de lang reeks tekens tussen **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---**.</span><span class="sxs-lookup"><span data-stu-id="b8350-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="b8350-167">Kopieer de gegevens van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="b8350-167">Copy the certificate data.</span></span> <span data-ttu-id="b8350-168">U kunt deze gegevens als een parameter doorgeven bij het maken van de service principal.</span><span class="sxs-lookup"><span data-stu-id="b8350-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="b8350-169">Aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="b8350-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="b8350-170">Voor het maken van de service-principal bieden u de naam van de app en de gegevens van het certificaat, zoals wordt weergegeven in de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b8350-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="b8350-171">De nieuwe service-principal wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b8350-171">The new service principal is returned.</span></span> <span data-ttu-id="b8350-172">De Object-Id is vereist bij het verlenen van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="b8350-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="b8350-173">De guid worden weergegeven met de Service Principal Names is nodig wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="b8350-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="b8350-174">Deze guid is dezelfde waarde als de app-id.</span><span class="sxs-lookup"><span data-stu-id="b8350-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="b8350-175">In de voorbeeldtoepassingen wordt deze waarde aangeduid als de Client-ID.</span><span class="sxs-lookup"><span data-stu-id="b8350-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="b8350-176">Aan de service principal machtigingen verlenen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b8350-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="b8350-177">In dit voorbeeld kunt u de service-principal toevoegen aan de rol lezer die machtiging toekent voor het lezen van alle resources in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="b8350-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="b8350-178">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b8350-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="b8350-179">Geef de Object-Id die u hebt gebruikt bij het maken van de toepassing voor de object-id-parameter.</span><span class="sxs-lookup"><span data-stu-id="b8350-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="b8350-180">Voordat u deze opdracht uitvoert, moet u even totdat de nieuwe service-principal worden doorgegeven in Azure Active Directory toestaan.</span><span class="sxs-lookup"><span data-stu-id="b8350-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="b8350-181">Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken.</span><span class="sxs-lookup"><span data-stu-id="b8350-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="b8350-182">In een script, moet u een stap in de slaapstand tussen de opdrachten toevoegen (zoals `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="b8350-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="b8350-183">Als u een foutmelding weergegeven dat de principal bestaat niet in de map ziet, voert u de opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="b8350-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="b8350-184">Geef het certificaat via automatische Azure CLI-script</span><span class="sxs-lookup"><span data-stu-id="b8350-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="b8350-185">Nu moet u zich aanmelden als de toepassing bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8350-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="b8350-186">Wanneer u zich aanmeldt als een service-principal, moet u voor de tenant-id van de map voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="b8350-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="b8350-187">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8350-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="b8350-188">Voor het ophalen van de tenant-id voor uw abonnement op dat moment geverifieerde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b8350-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="b8350-189">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b8350-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="b8350-190">Als u de tenant-id van een ander abonnement ophalen moet, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b8350-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="b8350-191">Vingerafdruk van het certificaat ophalen en verwijder overbodige tekens, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b8350-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="b8350-192">Die een vingerafdrukwaarde retourneert vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="b8350-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="b8350-193">Als u ophalen van de client-id moet worden gebruikt wilt voor aanmelden, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b8350-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="b8350-194">De waarde moet worden gebruikt voor het aanmelden is de guid die worden vermeld in de SPN-namen.</span><span class="sxs-lookup"><span data-stu-id="b8350-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="b8350-195">Aanmelden als service-principal.</span><span class="sxs-lookup"><span data-stu-id="b8350-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="b8350-196">U bent nu geautoriseerd als de service-principal voor de Azure Active Directory-toepassing die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b8350-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="b8350-197">Referenties wijzigen</span><span class="sxs-lookup"><span data-stu-id="b8350-197">Change credentials</span></span>

<span data-ttu-id="b8350-198">U kunt de referenties voor een AD-app, hetzij vanwege een beveiligingsinbreuk of een vervaldatum referentie wijzigen met `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="b8350-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="b8350-199">Een wachtwoord wilt wijzigen, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="b8350-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="b8350-200">De waarde van een certificaat wilt wijzigen, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="b8350-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="b8350-201">Fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="b8350-201">Debug</span></span>

<span data-ttu-id="b8350-202">De volgende fouten kunnen optreden bij het maken van een service-principal:</span><span class="sxs-lookup"><span data-stu-id="b8350-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="b8350-203">**'Authentication_Unauthorized'** of **'geen abonnement gevonden in de context.'**</span><span class="sxs-lookup"><span data-stu-id="b8350-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="b8350-204">-U hebt deze fout te zien wanneer uw account beschikt niet over de [vereist machtigingen](#required-permissions) op de Azure Active Directory om een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="b8350-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="b8350-205">Normaal gesproken u deze fout te zien wanneer alleen admin gebruikers in uw Azure Active Directory apps registreren kunnen en uw account niet een beheerder is.</span><span class="sxs-lookup"><span data-stu-id="b8350-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="b8350-206">Vraag uw beheerder u ofwel toewijzen aan een beheerdersrol of waarmee gebruikers om apps te registreren.</span><span class="sxs-lookup"><span data-stu-id="b8350-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="b8350-207">Uw account **"heeft geen autorisatie om uit te voeren van de actie 'Microsoft.Authorization/roleAssignments/write' bereik/subscriptions / {guid}."**  -Deze fout te zien wanneer uw account beschikt niet over voldoende machtigingen aan een rol toewijzen aan een identiteit.</span><span class="sxs-lookup"><span data-stu-id="b8350-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="b8350-208">Vraag de abonnementsbeheerder u toe te voegen aan de rol beheerder voor gebruikerstoegang.</span><span class="sxs-lookup"><span data-stu-id="b8350-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="b8350-209">Voorbeeldtoepassingen</span><span class="sxs-lookup"><span data-stu-id="b8350-209">Sample applications</span></span>
<span data-ttu-id="b8350-210">Zie voor informatie over logboekregistratie in als de toepassing via verschillende platforms:</span><span class="sxs-lookup"><span data-stu-id="b8350-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="b8350-211">.NET</span><span class="sxs-lookup"><span data-stu-id="b8350-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="b8350-212">Java</span><span class="sxs-lookup"><span data-stu-id="b8350-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="b8350-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="b8350-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="b8350-214">Python</span><span class="sxs-lookup"><span data-stu-id="b8350-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="b8350-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="b8350-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="b8350-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8350-216">Next steps</span></span>
* <span data-ttu-id="b8350-217">Zie voor gedetailleerde stappen voor het integreren van een toepassing in Azure voor het beheren van resources [Ontwikkelaarshandleiding voor autorisatie met de Azure Resource Manager-API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b8350-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="b8350-218">Zie voor meer informatie over het gebruik van certificaten en Azure CLI, [certificaat gebaseerde verificatie met Azure Service-Principals vanaf de opdrachtregel Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8350-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="b8350-219">Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd voor gebruikers, [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="b8350-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
