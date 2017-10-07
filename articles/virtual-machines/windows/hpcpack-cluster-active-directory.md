---
title: aaaHPC Pack cluster met Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een HPC Pack 2016 toointegrate-cluster in Azure met Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="d3816-103">Een HPC Pack cluster in Azure met Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="d3816-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="d3816-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ondersteunt de integratie met [Azure Active Directory](../../active-directory/index.md) (Azure AD) voor beheerders die een HPC Pack cluster in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="d3816-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="d3816-105">Hallo stappen in dit artikel voor Hallo taken op hoog niveau volgen:</span><span class="sxs-lookup"><span data-stu-id="d3816-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="d3816-106">Uw cluster HPC Pack handmatig te integreren met uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="d3816-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="d3816-107">Beheren en plannen van taken in uw cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="d3816-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="d3816-108">Een clusteroplossing HPC Pack integreren met Azure AD volgt toointegrate standaard stappen, andere toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="d3816-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="d3816-109">In dit artikel wordt ervan uitgegaan dat u bekend bent met basisgebruiker management in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3816-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="d3816-110">Zie voor meer informatie en achtergrond Hallo [Azure Active Directory-documentatie](../../active-directory/index.md) en Hallo de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="d3816-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="d3816-111">Voordelen van de integratie</span><span class="sxs-lookup"><span data-stu-id="d3816-111">Benefits of integration</span></span>


<span data-ttu-id="d3816-112">Azure Active Directory (Azure AD) is een multitenant cloud-gebaseerde directory en identity management-service die toocloud oplossingen voor eenmalige aanmelding (SSO) toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="d3816-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="d3816-113">Integratie van een cluster HPC Pack met Azure AD kunt u Hallo volgende doelstellingen te bereiken:</span><span class="sxs-lookup"><span data-stu-id="d3816-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="d3816-114">Hallo traditionele Active Directory-domeincontroller uit Hallo HPC Pack cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d3816-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="d3816-115">Dit kan helpen om kosten te verlagen Hallo van onderhouden Hallo cluster als dit niet nodig zijn voor uw bedrijf en versnellen Hallo-implementatieproces is.</span><span class="sxs-lookup"><span data-stu-id="d3816-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="d3816-116">Gebruikmaken van Hallo volgende voordelen die worden uitgevoerd door Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d3816-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="d3816-117">Eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d3816-117">Single sign-on</span></span> 
    *   <span data-ttu-id="d3816-118">Met behulp van een lokale AD-identiteit voor Hallo HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="d3816-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory-omgeving](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="d3816-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d3816-120">Prerequisites</span></span>
* <span data-ttu-id="d3816-121">**HPC Pack 2016 cluster is geïmplementeerd in virtuele machines in Azure** - voor de stappen, Zie [een HPC Pack 2016-cluster in Azure implementeren](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d3816-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="d3816-122">U moet Hallo DNS-naam van het hoofdknooppunt Hallo en Hallo referenties van een Clusterbeheerder Hallo stappen in dit artikel uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d3816-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d3816-123">Azure Active Directory-integratie wordt niet ondersteund in versies van HPC Pack vóór HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="d3816-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="d3816-124">**Clientcomputer** -moet u een Windows- of Windows Server client computer te worden uitgevoerd HPC Pack client hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="d3816-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="d3816-125">Als u alleen toouse Hallo HPC Pack web-portal of REST-API toosubmit taken wilt, kunt u elke clientcomputer van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="d3816-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="d3816-126">**Hulpprogramma's voor HPC Pack client** -Hallo HPC Pack client hulpprogramma's installeren op Hallo van de clientcomputer, met behulp van Hallo gratis installatiepakket beschikbaar is via Hallo Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="d3816-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="d3816-127">Stap 1: Hallo HPC clusterserver registreren met uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="d3816-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="d3816-128">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d3816-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d3816-129">Klik op **Active Directory** in Hallo linkermenu en klik op de gewenste map Hallo in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d3816-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="d3816-130">In de map Hallo moet u de machtiging tooaccess resources hebben.</span><span class="sxs-lookup"><span data-stu-id="d3816-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="d3816-131">Klik op **gebruikers**, en controleer of er gebruikersaccounts al gemaakt of geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d3816-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="d3816-132">Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d3816-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="d3816-133">Voer de volgende informatie in de wizard Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="d3816-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="d3816-134">**Naam** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="d3816-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="d3816-135">**Type** : Selecteer **Web-toepassing en/of Web-API**</span><span class="sxs-lookup"><span data-stu-id="d3816-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="d3816-136">**Eenmalige aanmelding URL**- hello basis-URL voor hello, die standaard is`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="d3816-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="d3816-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="d3816-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="d3816-138">Vervang `<Directory_name`> Hello volledige naam van uw Azure AD-tenant, bijvoorbeeld `hpclocal.onmicrosoft.com`, en vervang `<application_name>` met Hallo-naam die u eerder hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="d3816-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="d3816-139">Nadat het Hallo-app wordt toegevoegd, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d3816-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="d3816-140">Configureer Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d3816-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="d3816-141">Selecteer **Ja** voor **toepassing multitenant is**</span><span class="sxs-lookup"><span data-stu-id="d3816-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="d3816-142">Selecteer **Ja** voor **gebruiker toewijzing vereist tooaccess app**.</span><span class="sxs-lookup"><span data-stu-id="d3816-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="d3816-143">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d3816-143">Click **Save**.</span></span> <span data-ttu-id="d3816-144">Wanneer opslaan is voltooid, klikt u op **beheren Manifest**.</span><span class="sxs-lookup"><span data-stu-id="d3816-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="d3816-145">Deze actie downloadt van uw toepassing JavaScript object notation (JSON) manifestbestand.</span><span class="sxs-lookup"><span data-stu-id="d3816-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="d3816-146">Hallo gedownload-manifest bewerken door het zoeken naar Hallo `appRoles` instellen en het toevoegen van Hallo toepassingsrol te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3816-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="d3816-147">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="d3816-147">Save hello file.</span></span> <span data-ttu-id="d3816-148">Klik in het Hallo-portal **beheren Manifest** > **uploaden Manifest**.</span><span class="sxs-lookup"><span data-stu-id="d3816-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="d3816-149">U kunt vervolgens Hallo bewerkte manifest uploaden.</span><span class="sxs-lookup"><span data-stu-id="d3816-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="d3816-150">Klik op **gebruikers**, selecteert u een gebruiker en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="d3816-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="d3816-151">Een Hallo beschikbare rollen (HpcUsers of HpcAdminMirror) toohello gebruiker toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d3816-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="d3816-152">Herhaal deze stap met extra gebruikers in het Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="d3816-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="d3816-153">Zie voor achtergrondinformatie over cluster gebruikers, [Cluster gebruikers beheren](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="d3816-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="d3816-154">toomanage gebruikers, wordt u aangeraden hello Azure Active Directory preview blade in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3816-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="d3816-155">Stap 2: Hallo HPC cluster client registreren bij uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="d3816-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="d3816-156">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d3816-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d3816-157">Klik op **Active Directory** in Hallo linkermenu en klik op de gewenste map Hallo in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d3816-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="d3816-158">In de map Hallo moet u de machtiging tooaccess resources hebben.</span><span class="sxs-lookup"><span data-stu-id="d3816-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="d3816-159">Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d3816-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="d3816-160">Voer de volgende informatie in de wizard Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="d3816-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="d3816-161">**Naam** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="d3816-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="d3816-162">**Type** : Selecteer **Native Client-toepassing**</span><span class="sxs-lookup"><span data-stu-id="d3816-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="d3816-163">**Omleidings-URI** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="d3816-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="d3816-164">Nadat het Hallo-app wordt toegevoegd, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d3816-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="d3816-165">Kopiëren Hallo **Client-ID** waarde en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d3816-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="d3816-166">U nodig dit later bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3816-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="d3816-167">In **machtigingen tooother toepassingen**, klikt u op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d3816-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="d3816-168">Zoeken en Hallo HpcPackClusterServer toepassing is (gemaakt in stap 1) toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d3816-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="d3816-169">In Hallo **gedelegeerde machtigingen** vervolgkeuzelijst **toegang HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="d3816-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="d3816-170">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d3816-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="d3816-171">Stap 3: Hallo HPC-cluster configureren</span><span class="sxs-lookup"><span data-stu-id="d3816-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="d3816-172">Verbinding maken met het hoofdknooppunt toohello HPC Pack 2016 in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3816-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="d3816-173">Start HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3816-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="d3816-174">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d3816-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="d3816-175">waar</span><span class="sxs-lookup"><span data-stu-id="d3816-175">where</span></span>

    * <span data-ttu-id="d3816-176">`AADTenant`Hiermee geeft u hello Azure AD-tenantnaam, zoals`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="d3816-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="d3816-177">`AADClientAppId`Hiermee geeft u Hallo client-ID voor Hallo-app gemaakt in stap 2.</span><span class="sxs-lookup"><span data-stu-id="d3816-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="d3816-178">Hallo HpcSchedulerStateful service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="d3816-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="d3816-179">In een cluster met meerdere hoofdknooppunten, kunt u de volgende PowerShell-opdrachten op Hallo hoofdknooppunt tooswitch Hallo primaire replica voor Hallo HpcSchedulerStateful service Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d3816-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="d3816-180">Stap 4: Beheren en verzenden van taken van Hallo-client</span><span class="sxs-lookup"><span data-stu-id="d3816-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="d3816-181">de HPC Pack 2016 setup-bestanden (volledige installatie) downloaden tooinstall Hallo HPC Pack client hulpprogramma's op uw computer vanaf Microsoft Download Center Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3816-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="d3816-182">Wanneer u Hallo installatie begint, selecteer de installatieoptie Hallo voor Hallo **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="d3816-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="d3816-183">tooprepare Hallo-clientcomputer installeren Hallo certificaat dat wordt gebruikt tijdens [HPC cluster setup](hpcpack-2016-cluster.md) op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="d3816-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="d3816-184">Gebruik standaard Windows certificate management procedures tooinstall Hallo openbaar certificaat toohello **certificaten-huidige gebruiker** > **Trusted Root Certification Authorities** opslaan.</span><span class="sxs-lookup"><span data-stu-id="d3816-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="d3816-185">U kunt nu Hallo HPC Pack opdrachten uitvoeren of Hallo HPC Pack Job manager GUI toosubmit gebruiken en cluster taken beheren met behulp van hello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="d3816-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="d3816-186">Zie voor de opties voor het indienen van taak [HPC verzenden taken tooan HPC Pack-cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="d3816-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="d3816-187">Wanneer u probeert eerst tooconnect toohello HPC Pack cluster in Azure voor hello, verschijnt een pop-upvensters.</span><span class="sxs-lookup"><span data-stu-id="d3816-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="d3816-188">Voer uw Azure AD-referenties toolog in.</span><span class="sxs-lookup"><span data-stu-id="d3816-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="d3816-189">Hallo-token wordt vervolgens in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d3816-189">hello token is then cached.</span></span> <span data-ttu-id="d3816-190">Token in cache opgeslagen hoger verbindingen toohello cluster in Azure gebruik Hallo tenzij verificatie wijzigingen of Hallo in cache is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d3816-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="d3816-191">Bijvoorbeeld, na het voltooien van de vorige stappen hello, u kunt een query voor de taken van een on-premises client als volgt:</span><span class="sxs-lookup"><span data-stu-id="d3816-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="d3816-192">Handig cmdlets taak te verzenden met Azure AD-integratie</span><span class="sxs-lookup"><span data-stu-id="d3816-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="d3816-193">Hallo lokale tokencache beheren</span><span class="sxs-lookup"><span data-stu-id="d3816-193">Manage hello local token cache</span></span>

<span data-ttu-id="d3816-194">HPC Pack 2016 biedt twee nieuwe HPC PowerShell-cmdlets toomanage Hallo lokale tokencache.</span><span class="sxs-lookup"><span data-stu-id="d3816-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="d3816-195">Deze cmdlets zijn handig voor het verzenden van taken niet-interactief.</span><span class="sxs-lookup"><span data-stu-id="d3816-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="d3816-196">Zie Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3816-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="d3816-197">Hallo-referenties voor het indienen van taken met hello Azure AD-account instellen</span><span class="sxs-lookup"><span data-stu-id="d3816-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="d3816-198">U kunt toorun Hallo taak onder Hallo HPC cluster gebruiker soms (voor een domein HPC-cluster moet uitvoeren als een domeingebruiker; voor een niet-domein HPC-cluster moet uitvoeren als een lokale gebruiker op het hoofdknooppunt Hallo).</span><span class="sxs-lookup"><span data-stu-id="d3816-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="d3816-199">Gebruik Hallo opdrachten tooset Hallo referenties te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3816-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="d3816-200">Vervolgens dient als volgt Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="d3816-200">Then submit hello job as follows.</span></span> <span data-ttu-id="d3816-201">Hallo-taak taak wordt uitgevoerd onder $localUser op Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="d3816-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="d3816-202">Als `–Credential` niet wordt opgegeven met `Submit-HpcJob`, Hallo- taak wordt uitgevoerd onder een lokale gebruikersaccount toegewezen als hello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="d3816-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="d3816-203">(Hallo HPC-cluster maakt een lokale gebruiker met dezelfde naam als hello Azure AD-account toorun Hallo taak Hallo.)</span><span class="sxs-lookup"><span data-stu-id="d3816-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="d3816-204">Uitgebreide gegevens voor hello Azure AD-account instellen.</span><span class="sxs-lookup"><span data-stu-id="d3816-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="d3816-205">Dit is handig wanneer een MPI-taak wordt uitgevoerd op Linux-knooppunten met hello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="d3816-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="d3816-206">Uitgebreide gegevens voor Azure AD-account zelf Hallo instellen</span><span class="sxs-lookup"><span data-stu-id="d3816-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="d3816-207">Uitgebreide gegevens instellen en uitvoeren als gebruiker met HPC-cluster</span><span class="sxs-lookup"><span data-stu-id="d3816-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

