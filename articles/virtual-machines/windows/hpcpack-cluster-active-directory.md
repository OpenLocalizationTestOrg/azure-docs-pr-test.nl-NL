---
title: HPC Pack cluster met Azure Active Directory | Microsoft Docs
description: Meer informatie over het integreren van een HPC Pack 2016-cluster in Azure met Azure Active Directory
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
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="9d074-103">Een HPC Pack cluster in Azure met Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="9d074-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="9d074-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ondersteunt de integratie met [Azure Active Directory](../../active-directory/index.md) (Azure AD) voor beheerders die een HPC Pack cluster in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="9d074-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="9d074-105">Volg de stappen in dit artikel voor de volgende taken op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="9d074-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="9d074-106">Uw cluster HPC Pack handmatig te integreren met uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="9d074-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="9d074-107">Beheren en plannen van taken in uw cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="9d074-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="9d074-108">Een clusteroplossing HPC Pack integreren met Azure AD volgt standaard stappen voor het integreren van andere toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="9d074-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="9d074-109">In dit artikel wordt ervan uitgegaan dat u bekend bent met basisgebruiker management in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d074-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="9d074-110">Zie voor meer informatie en achtergrond, de [Azure Active Directory-documentatie](../../active-directory/index.md) en de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="9d074-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="9d074-111">Voordelen van de integratie</span><span class="sxs-lookup"><span data-stu-id="9d074-111">Benefits of integration</span></span>


<span data-ttu-id="9d074-112">Azure Active Directory (Azure AD) is een multitenant cloud-gebaseerde directory en identity management-service dat eenmalige aanmelding (SSO) toegang tot cloudoplossingen biedt.</span><span class="sxs-lookup"><span data-stu-id="9d074-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="9d074-113">Integratie van een cluster HPC Pack met Azure AD kunt u de volgende drie doelen te bereiken:</span><span class="sxs-lookup"><span data-stu-id="9d074-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="9d074-114">Verwijder de traditionele Active Directory-domeincontroller uit het cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9d074-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="9d074-115">Zo kunt u de kosten van het onderhoud van het cluster als dit niet nodig zijn voor uw bedrijf en versnellen het implementatieproces is te verlagen.</span><span class="sxs-lookup"><span data-stu-id="9d074-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="9d074-116">Gebruikmaken van de volgende voordelen die worden uitgevoerd door Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9d074-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="9d074-117">Eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d074-117">Single sign-on</span></span> 
    *   <span data-ttu-id="9d074-118">Met behulp van een lokale AD-identiteit voor het cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="9d074-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory-omgeving](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="9d074-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d074-120">Prerequisites</span></span>
* <span data-ttu-id="9d074-121">**HPC Pack 2016 cluster is geïmplementeerd in virtuele machines in Azure** - voor de stappen, Zie [een HPC Pack 2016-cluster in Azure implementeren](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9d074-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="9d074-122">U moet de DNS-naam van het hoofdknooppunt en de referenties van de Clusterbeheerder van een om de stappen in dit artikel te voltooien.</span><span class="sxs-lookup"><span data-stu-id="9d074-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9d074-123">Azure Active Directory-integratie wordt niet ondersteund in versies van HPC Pack vóór HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="9d074-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="9d074-124">**Clientcomputer** -moet u een clientcomputer Windows of Windows Server voor het uitvoeren van HPC Pack client-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9d074-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="9d074-125">Als u alleen de HPC Pack web-portal of REST-API gebruiken om taken te verzenden wilt, kunt u elke clientcomputer van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="9d074-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="9d074-126">**Hulpprogramma's voor HPC Pack client** -de hulpprogramma's voor HPC Pack client installeren op de clientcomputer, met behulp van de beschikbare vrije installatiepakket van het Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="9d074-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="9d074-127">Stap 1: De HPC-cluster-server geregistreerd met uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="9d074-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="9d074-128">Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9d074-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9d074-129">Klik op **Active Directory** in het menu links en klik vervolgens op de gewenste map in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d074-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="9d074-130">U moet gemachtigd zijn voor toegang tot bronnen in de directory.</span><span class="sxs-lookup"><span data-stu-id="9d074-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="9d074-131">Klik op **gebruikers**, en controleer of er gebruikersaccounts al gemaakt of geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9d074-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="9d074-132">Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9d074-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="9d074-133">Voer de volgende gegevens in de wizard:</span><span class="sxs-lookup"><span data-stu-id="9d074-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="9d074-134">**Naam** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="9d074-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="9d074-135">**Type** : Selecteer **Web-toepassing en/of Web-API**</span><span class="sxs-lookup"><span data-stu-id="9d074-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="9d074-136">**Eenmalige aanmelding URL**-de basis-URL voor de steekproef die standaard is`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="9d074-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="9d074-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="9d074-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="9d074-138">Vervang `<Directory_name`> met de volledige naam van uw Azure AD-tenant, bijvoorbeeld `hpclocal.onmicrosoft.com`, en vervang `<application_name>` met de naam die u eerder hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="9d074-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="9d074-139">Nadat de app wordt toegevoegd, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="9d074-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="9d074-140">Configureer de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="9d074-140">Configure the following properties:</span></span>
    * <span data-ttu-id="9d074-141">Selecteer **Ja** voor **toepassing multitenant is**</span><span class="sxs-lookup"><span data-stu-id="9d074-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="9d074-142">Selecteer **Ja** voor **Gebruikerstoewijzing vereist voor toegang tot app**.</span><span class="sxs-lookup"><span data-stu-id="9d074-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="9d074-143">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9d074-143">Click **Save**.</span></span> <span data-ttu-id="9d074-144">Wanneer opslaan is voltooid, klikt u op **beheren Manifest**.</span><span class="sxs-lookup"><span data-stu-id="9d074-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="9d074-145">Deze actie downloadt van uw toepassing JavaScript object notation (JSON) manifestbestand.</span><span class="sxs-lookup"><span data-stu-id="9d074-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="9d074-146">Het gedownloade manifest bewerken door het zoeken naar de `appRoles` instellen en de volgende toepassingsrol toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9d074-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
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
7. <span data-ttu-id="9d074-147">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="9d074-147">Save the file.</span></span> <span data-ttu-id="9d074-148">Klik in de portal **beheren Manifest** > **uploaden Manifest**.</span><span class="sxs-lookup"><span data-stu-id="9d074-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="9d074-149">Vervolgens kunt u het bewerkte manifest uploaden.</span><span class="sxs-lookup"><span data-stu-id="9d074-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="9d074-150">Klik op **gebruikers**, selecteert u een gebruiker en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="9d074-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="9d074-151">Een van de beschikbare rollen (HpcUsers of HpcAdminMirror) toewijzen aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d074-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="9d074-152">Herhaal deze stap met extra gebruikers in de map.</span><span class="sxs-lookup"><span data-stu-id="9d074-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="9d074-153">Zie voor achtergrondinformatie over cluster gebruikers, [Cluster gebruikers beheren](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="9d074-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="9d074-154">Voor het beheren van gebruikers, wordt u aangeraden de Azure Active Directory-preview-blade in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d074-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="9d074-155">Stap 2: De client HPC-cluster registreren bij uw Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="9d074-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="9d074-156">Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9d074-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9d074-157">Klik op **Active Directory** in het menu links en klik vervolgens op de gewenste map in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d074-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="9d074-158">U moet gemachtigd zijn voor toegang tot bronnen in de directory.</span><span class="sxs-lookup"><span data-stu-id="9d074-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="9d074-159">Klik op **toepassingen** > **toevoegen**, en klik vervolgens op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9d074-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="9d074-160">Voer de volgende gegevens in de wizard:</span><span class="sxs-lookup"><span data-stu-id="9d074-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="9d074-161">**Naam** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="9d074-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="9d074-162">**Type** : Selecteer **Native Client-toepassing**</span><span class="sxs-lookup"><span data-stu-id="9d074-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="9d074-163">**Omleidings-URI** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="9d074-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="9d074-164">Nadat de app wordt toegevoegd, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="9d074-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="9d074-165">Kopieer de **Client-ID** waarde en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9d074-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="9d074-166">U nodig dit later bij het configureren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d074-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="9d074-167">In **machtigingen voor andere toepassingen**, klikt u op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9d074-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="9d074-168">Zoeken en toevoegen aan de HpcPackClusterServer-toepassing (gemaakt in stap 1).</span><span class="sxs-lookup"><span data-stu-id="9d074-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="9d074-169">In de **gedelegeerde machtigingen** vervolgkeuzelijst **toegang HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="9d074-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="9d074-170">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9d074-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="9d074-171">Stap 3: De HPC-cluster configureren</span><span class="sxs-lookup"><span data-stu-id="9d074-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="9d074-172">Verbinding maken met het hoofdknooppunt van HPC Pack 2016 in Azure.</span><span class="sxs-lookup"><span data-stu-id="9d074-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="9d074-173">Start HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d074-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="9d074-174">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="9d074-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="9d074-175">waar</span><span class="sxs-lookup"><span data-stu-id="9d074-175">where</span></span>

    * <span data-ttu-id="9d074-176">`AADTenant`Hiermee geeft u de naam van de Azure AD-tenant, zoals`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="9d074-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="9d074-177">`AADClientAppId`Hiermee geeft u de client-ID voor de app gemaakt in stap 2.</span><span class="sxs-lookup"><span data-stu-id="9d074-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="9d074-178">Start de service HpcSchedulerStateful.</span><span class="sxs-lookup"><span data-stu-id="9d074-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="9d074-179">In een cluster met meerdere hoofdknooppunten, kunt u de volgende PowerShell-opdrachten uitvoeren op het hoofdknooppunt overschakelen van de primaire replica voor de service HpcSchedulerStateful:</span><span class="sxs-lookup"><span data-stu-id="9d074-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="9d074-180">Stap 4: Beheren en verzenden van taken van de client</span><span class="sxs-lookup"><span data-stu-id="9d074-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="9d074-181">Voor het installeren van de hulpprogramma's voor HPC Pack client op uw computer, de HPC Pack 2016 setup-bestanden (volledige installatie) te downloaden vanaf het Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="9d074-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="9d074-182">Wanneer u de installatie begint, selecteer de installatieoptie voor de **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="9d074-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="9d074-183">Als u met het voorbereiden van de clientcomputer, installeert u het certificaat wordt gebruikt tijdens [HPC cluster setup](hpcpack-2016-cluster.md) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="9d074-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="9d074-184">Windows certificate management standaardprocedures gebruiken voor het installeren van het openbare certificaat naar de **certificaten-huidige gebruiker** > **Trusted Root Certification Authorities** opslaan.</span><span class="sxs-lookup"><span data-stu-id="9d074-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="9d074-185">U kunt nu de HPC Pack opdrachten uitvoeren of HPC Pack Job manager GUI gebruiken voor het verzenden en cluster taken beheren met behulp van de Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="9d074-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="9d074-186">Zie voor de opties voor het indienen van taak [taken op een HPC Pack indienen HPC-cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="9d074-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="9d074-187">Wanneer u een verbinding met het cluster HPC Pack in Azure voor het eerst uitvoert, verschijnt een pop-upvensters.</span><span class="sxs-lookup"><span data-stu-id="9d074-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="9d074-188">Voer uw Azure AD-referenties aan te melden.</span><span class="sxs-lookup"><span data-stu-id="9d074-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="9d074-189">Het token wordt vervolgens in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9d074-189">The token is then cached.</span></span> <span data-ttu-id="9d074-190">Hoger verbindingen met het cluster in Azure gebruiken de token in cache tenzij gewijzigde verificatie of de cache is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d074-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="9d074-191">Bijvoorbeeld, na het voltooien van de vorige stappen u kunt een query voor de taken van een on-premises client als volgt:</span><span class="sxs-lookup"><span data-stu-id="9d074-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="9d074-192">Handig cmdlets taak te verzenden met Azure AD-integratie</span><span class="sxs-lookup"><span data-stu-id="9d074-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="9d074-193">De lokale tokencache beheren</span><span class="sxs-lookup"><span data-stu-id="9d074-193">Manage the local token cache</span></span>

<span data-ttu-id="9d074-194">HPC Pack 2016 biedt twee nieuwe HPC PowerShell-cmdlets voor het beheren van de lokale cache van de token.</span><span class="sxs-lookup"><span data-stu-id="9d074-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="9d074-195">Deze cmdlets zijn handig voor het verzenden van taken niet-interactief.</span><span class="sxs-lookup"><span data-stu-id="9d074-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="9d074-196">Zie het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d074-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="9d074-197">Stel de referenties voor het indienen van taken met behulp van de Azure AD-account</span><span class="sxs-lookup"><span data-stu-id="9d074-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="9d074-198">Soms wilt u de taak onder de gebruiker HPC-cluster (voor een domein HPC-cluster, voert u als een domeingebruiker; voor een niet-domein HPC-cluster moet uitvoeren als een lokale gebruiker op het hoofdknooppunt) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9d074-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="9d074-199">Gebruik de volgende opdrachten de referenties in te stellen:</span><span class="sxs-lookup"><span data-stu-id="9d074-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="9d074-200">Vervolgens dient u de taak als volgt.</span><span class="sxs-lookup"><span data-stu-id="9d074-200">Then submit the job as follows.</span></span> <span data-ttu-id="9d074-201">De taak wordt uitgevoerd onder $localUser op de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="9d074-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="9d074-202">Als `–Credential` niet wordt opgegeven met `Submit-HpcJob`, de functie of de taak wordt uitgevoerd onder een lokale toegewezen gebruiker als de Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="9d074-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="9d074-203">(De HPC-cluster maakt een lokale gebruiker met dezelfde naam als de Azure AD-account voor de taak).</span><span class="sxs-lookup"><span data-stu-id="9d074-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="9d074-204">Uitgebreide gegevens voor de Azure AD-account instellen.</span><span class="sxs-lookup"><span data-stu-id="9d074-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="9d074-205">Dit is handig wanneer een MPI-taak wordt uitgevoerd op Linux-knooppunten met behulp van de Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="9d074-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="9d074-206">Uitgebreide gegevens voor de Azure AD-account zelf instellen</span><span class="sxs-lookup"><span data-stu-id="9d074-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="9d074-207">Uitgebreide gegevens instellen en uitvoeren als gebruiker met HPC-cluster</span><span class="sxs-lookup"><span data-stu-id="9d074-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

