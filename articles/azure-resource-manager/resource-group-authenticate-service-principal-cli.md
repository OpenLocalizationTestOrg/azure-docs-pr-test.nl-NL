---
title: aaaCreate identiteit voor Azure-app met Azure CLI | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure CLI toocreate een Azure Active Directory-toepassing en service-principal en verleen deze toegang hebben tot tooresources via op rollen gebaseerde toegang beheren. Er wordt weergegeven hoe tooauthenticate toepassing met een wachtwoord of certificaat.
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
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="d2b15-104">Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="d2b15-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="d2b15-105">Wanneer u een app of een script dat tooaccess resources moet hebt, kunt u een identiteit voor het Hallo-app instellen en Hallo-app met een eigen referenties verifiëren.</span><span class="sxs-lookup"><span data-stu-id="d2b15-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="d2b15-106">Deze identiteit staat bekend als een service-principal.</span><span class="sxs-lookup"><span data-stu-id="d2b15-106">This identity is known as a service principal.</span></span> <span data-ttu-id="d2b15-107">Deze aanpak kunt u:</span><span class="sxs-lookup"><span data-stu-id="d2b15-107">This approach enables you to:</span></span>

* <span data-ttu-id="d2b15-108">Wijs machtigingen toe toohello app identiteit die anders zijn dan uw eigen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="d2b15-109">Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.</span><span class="sxs-lookup"><span data-stu-id="d2b15-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="d2b15-110">Een certificaat voor verificatie gebruiken bij het uitvoeren van een onbewaakt script.</span><span class="sxs-lookup"><span data-stu-id="d2b15-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="d2b15-111">Dit artikel ziet u hoe toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset van een toepassing toorun onder een eigen referenties en identiteit.</span><span class="sxs-lookup"><span data-stu-id="d2b15-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="d2b15-112">Installeer de nieuwste versie Hallo van [Azure CLI 1.0](../cli-install-nodejs.md) toomake ervoor dat uw omgeving overeenkomt met de Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d2b15-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d2b15-113">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="d2b15-113">Required permissions</span></span>
<span data-ttu-id="d2b15-114">toocomplete in dit onderwerp, moet u voldoende machtigingen in uw Azure Active Directory en uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="d2b15-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="d2b15-115">In het bijzonder moeten kunnen toocreate een app in Azure Active Directory hello, en Hallo service principal tooa rol toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="d2b15-116">Hallo gemakkelijkste manier toocheck of uw account de juiste machtigingen heeft, is via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d2b15-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="d2b15-117">Zie [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions) (Vereiste machtigingen controleren in de portal).</span><span class="sxs-lookup"><span data-stu-id="d2b15-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="d2b15-118">Nu gaan tooa sectie voor [wachtwoord](#create-service-principal-with-password) of [certificaat](#create-service-principal-with-certificate) verificatie.</span><span class="sxs-lookup"><span data-stu-id="d2b15-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="d2b15-119">Service-principal maken met wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d2b15-119">Create service principal with password</span></span>
<span data-ttu-id="d2b15-120">In deze sectie uitvoeren Hallo stappen toocreate Hallo AD-toepassing met een wachtwoord en Hallo lezer rol toohello service-principal toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="d2b15-121">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="d2b15-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="d2b15-122">toocreate een identiteit app bieden Hallo-naam van Hallo-app en een wachtwoord, zoals wordt weergegeven in de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d2b15-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="d2b15-123">Hallo nieuwe service-principal wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d2b15-123">hello new service principal is returned.</span></span> <span data-ttu-id="d2b15-124">Hallo Object-Id is vereist bij het verlenen van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d2b15-125">Hallo-guid worden weergegeven met de Service Principal Names Hallo is nodig wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="d2b15-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d2b15-126">Deze guid is Hallo dezelfde waarde als Hallo app-id. Deze waarde is Hallo voorbeeldtoepassingen waarnaar wordt verwezen tooas Hallo `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="d2b15-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="d2b15-127">Machtigingen Hallo service principal op uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d2b15-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="d2b15-128">In dit voorbeeld moet u Hallo service principal toohello lezer functie, die machtiging tooread alle resources in het Hallo-abonnement verleent toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="d2b15-129">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d2b15-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d2b15-130">Hallo object-id-parameter, bieden Hallo Object-Id die u hebt gebruikt bij het maken van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d2b15-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="d2b15-131">Voordat u deze opdracht uitvoert, moet u even totdat Hallo nieuwe service principal toopropagate in Azure Active Directory toestaan.</span><span class="sxs-lookup"><span data-stu-id="d2b15-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d2b15-132">Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken.</span><span class="sxs-lookup"><span data-stu-id="d2b15-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d2b15-133">In een script, moet u een stap toosleep tussen opdrachten Hallo toevoegen (zoals `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d2b15-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="d2b15-134">Als er dat een fout vermelden Hallo principal bestaat niet in de directory hello, moet u de opdracht Hallo opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d2b15-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="d2b15-135">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="d2b15-135">That's it!</span></span> <span data-ttu-id="d2b15-136">Uw AD-toepassing en service-principal worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d2b15-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="d2b15-137">de volgende sectie Hallo ziet u hoe toolog met Hallo referenties via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d2b15-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="d2b15-138">Als u wilt dat toouse Hallo referentie in uw toepassing code, hoeft u geen toocontinue met dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="d2b15-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="d2b15-139">U kunt gaan toohello [voorbeeldtoepassingen](#sample-applications) voor voorbeelden van aangemeld met uw toepassings-id en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d2b15-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="d2b15-140">Geef referenties op via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d2b15-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="d2b15-141">Nu moet u toolog in als Hallo toepassing tooperform bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="d2b15-142">Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="d2b15-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="d2b15-143">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2b15-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d2b15-144">tooretrieve hello tenant-id voor uw huidige geverifieerde abonnement, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b15-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d2b15-145">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d2b15-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="d2b15-146">Als u tooget hello tenant-id van een ander abonnement moet, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d2b15-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d2b15-147">Als u tooretrieve Hallo client-id toouse voor logboekregistratie in nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="d2b15-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="d2b15-148">Hallo waarde toouse voor aanmelden is vermeld in de SPN-namen Hallo Hallo-guid.</span><span class="sxs-lookup"><span data-stu-id="d2b15-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="d2b15-149">Aanmelden als service-principal Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2b15-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="d2b15-150">U wordt gevraagd om Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d2b15-150">You are prompted for hello password.</span></span> <span data-ttu-id="d2b15-151">U hebt opgegeven bij het maken van de toepassing hello AD Hallo-wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="d2b15-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="d2b15-152">U bent nu geautoriseerd als Hallo service-principal voor Hallo service-principal die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2b15-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="d2b15-153">U kunt ook de REST-bewerkingen van het Hallo opdrachtregel toolog in aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="d2b15-154">U kunt van antwoord Hallo-verificatie, Hallo toegangstoken voor gebruik met andere bewerkingen ophalen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="d2b15-155">Zie voor een voorbeeld van het toegangstoken Hallo ophalen door aan te roepen REST-bewerkingen [genereren van een Token toegang](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="d2b15-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="d2b15-156">Service-principal maken met certificaat</span><span class="sxs-lookup"><span data-stu-id="d2b15-156">Create service principal with certificate</span></span>
<span data-ttu-id="d2b15-157">In deze sectie kunt u Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d2b15-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="d2b15-158">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="d2b15-158">create a self-signed certificate</span></span>
* <span data-ttu-id="d2b15-159">Hallo AD-toepassing maken met het Hallo-certificaat en Hallo service-principal</span><span class="sxs-lookup"><span data-stu-id="d2b15-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="d2b15-160">Hallo lezer rol toohello service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="d2b15-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="d2b15-161">toocomplete deze stappen, hebt u [OpenSSL](http://www.openssl.org/) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d2b15-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="d2b15-162">Een zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="d2b15-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="d2b15-163">Hallo vóór stap gemaakt twee bestanden - privkey.pem en cert.pem.</span><span class="sxs-lookup"><span data-stu-id="d2b15-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="d2b15-164">Hallo openbare en persoonlijke sleutels worden gecombineerd tot één bestand.</span><span class="sxs-lookup"><span data-stu-id="d2b15-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="d2b15-165">Open Hallo **examplecert.pem** bestand en zoek naar zeer lange reeks tekens tussen Hallo **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---**.</span><span class="sxs-lookup"><span data-stu-id="d2b15-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="d2b15-166">Hallo certificaatgegevens kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d2b15-166">Copy hello certificate data.</span></span> <span data-ttu-id="d2b15-167">U kunt deze gegevens als een parameter doorgeven bij het Hallo-service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="d2b15-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="d2b15-168">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="d2b15-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="d2b15-169">toocreate hello service-principal bieden Hallo-naam van het Hallo-app en de certificaatgegevens van Hallo, zoals wordt weergegeven in de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d2b15-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="d2b15-170">Hallo nieuwe service-principal wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d2b15-170">hello new service principal is returned.</span></span> <span data-ttu-id="d2b15-171">Hallo Object-Id is vereist bij het verlenen van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d2b15-172">Hallo-guid worden weergegeven met de Service Principal Names Hallo is nodig wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="d2b15-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d2b15-173">Deze guid is Hallo dezelfde waarde als Hallo app-id. Deze waarde is Hallo voorbeeldtoepassingen waarnaar wordt verwezen tooas Hallo Client-ID.</span><span class="sxs-lookup"><span data-stu-id="d2b15-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="d2b15-174">Machtigingen Hallo service principal op uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d2b15-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="d2b15-175">In dit voorbeeld moet u Hallo service principal toohello lezer functie, die machtiging tooread alle resources in het Hallo-abonnement verleent toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="d2b15-176">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d2b15-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d2b15-177">Hallo object-id-parameter, bieden Hallo Object-Id die u hebt gebruikt bij het maken van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d2b15-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="d2b15-178">Voordat u deze opdracht uitvoert, moet u even totdat Hallo nieuwe service principal toopropagate in Azure Active Directory toestaan.</span><span class="sxs-lookup"><span data-stu-id="d2b15-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d2b15-179">Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken.</span><span class="sxs-lookup"><span data-stu-id="d2b15-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d2b15-180">In een script, moet u een stap toosleep tussen opdrachten Hallo toevoegen (zoals `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d2b15-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="d2b15-181">Als er dat een fout vermelden Hallo principal bestaat niet in de directory hello, moet u de opdracht Hallo opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d2b15-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="d2b15-182">Geef het certificaat via automatische Azure CLI-script</span><span class="sxs-lookup"><span data-stu-id="d2b15-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="d2b15-183">Nu moet u toolog in als Hallo toepassing tooperform bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="d2b15-184">Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="d2b15-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="d2b15-185">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2b15-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d2b15-186">tooretrieve hello tenant-id voor uw huidige geverifieerde abonnement, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b15-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d2b15-187">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d2b15-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="d2b15-188">Als u tooget hello tenant-id van een ander abonnement moet, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d2b15-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d2b15-189">tooretrieve Hallo certificaatvingerafdruk en verwijder overbodige tekens, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b15-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="d2b15-190">Die een vingerafdrukwaarde retourneert vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="d2b15-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="d2b15-191">Als u tooretrieve Hallo client-id toouse voor logboekregistratie in nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="d2b15-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="d2b15-192">Hallo waarde toouse voor aanmelden is vermeld in de SPN-namen Hallo Hallo-guid.</span><span class="sxs-lookup"><span data-stu-id="d2b15-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="d2b15-193">Aanmelden als service-principal Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2b15-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="d2b15-194">U bent nu geautoriseerd als Hallo service-principal voor hello Azure Active Directory-toepassing die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2b15-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="d2b15-195">Referenties wijzigen</span><span class="sxs-lookup"><span data-stu-id="d2b15-195">Change credentials</span></span>

<span data-ttu-id="d2b15-196">toochange hello referenties voor een AD-app, hetzij vanwege een beveiligingsinbreuk of een vervaldatum referentie gebruiken `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="d2b15-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="d2b15-197">een wachtwoord, toochange gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b15-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="d2b15-198">de waarde van een certificaat toochange gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b15-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="d2b15-199">Fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="d2b15-199">Debug</span></span>

<span data-ttu-id="d2b15-200">Hallo volgende fouten bij het maken van een service-principal kunnen optreden:</span><span class="sxs-lookup"><span data-stu-id="d2b15-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="d2b15-201">**'Authentication_Unauthorized'** of **'geen abonnement gevonden in de context van Hallo'.**</span><span class="sxs-lookup"><span data-stu-id="d2b15-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="d2b15-202">-U hebt deze fout te zien wanneer uw account geen Hallo [vereist machtigingen](#required-permissions) op Hallo Azure Active Directory tooregister een app.</span><span class="sxs-lookup"><span data-stu-id="d2b15-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="d2b15-203">Normaal gesproken u deze fout te zien wanneer alleen admin gebruikers in uw Azure Active Directory apps registreren kunnen en uw account niet een beheerder is. Vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d2b15-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="d2b15-204">Uw account **"heeft geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik/subscriptions / {guid}."**  -Deze fout te zien wanneer uw account geen voldoende machtigingen tooassign tooan identiteit van een rol.</span><span class="sxs-lookup"><span data-stu-id="d2b15-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="d2b15-205">Vraag uw beheerder abonnement tooadd u tooUser toegang beheerdersrol.</span><span class="sxs-lookup"><span data-stu-id="d2b15-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="d2b15-206">Voorbeeldtoepassingen</span><span class="sxs-lookup"><span data-stu-id="d2b15-206">Sample applications</span></span>
<span data-ttu-id="d2b15-207">Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:</span><span class="sxs-lookup"><span data-stu-id="d2b15-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="d2b15-208">.NET</span><span class="sxs-lookup"><span data-stu-id="d2b15-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d2b15-209">Java</span><span class="sxs-lookup"><span data-stu-id="d2b15-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d2b15-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="d2b15-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d2b15-211">Python</span><span class="sxs-lookup"><span data-stu-id="d2b15-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d2b15-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="d2b15-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="d2b15-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2b15-213">Next steps</span></span>
* <span data-ttu-id="d2b15-214">Zie voor gedetailleerde stappen voor het integreren van een toepassing in Azure voor het beheren van resources [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d2b15-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d2b15-215">tooget meer informatie over het gebruik van certificaten en Azure CLI, Zie [certificaat gebaseerde verificatie met Azure Service-Principals vanaf de opdrachtregel Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2b15-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="d2b15-216">Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d2b15-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
