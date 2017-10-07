---
title: aaaCreate Service Fabric-cluster in hello Azure-portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset een beveiligde Service Fabric-cluster in Azure worden verkregen met hello Azure portal en Azure Sleutelkluis.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="6d44f-103">Een Service Fabric-cluster maken in Azure met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6d44f-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d44f-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d44f-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="6d44f-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6d44f-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="6d44f-106">Dit is een stapsgewijze handleiding die u bij het Hallo-stappen helpt voor het instellen van een beveiligde Service Fabric-cluster in Azure met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6d44f-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="6d44f-107">Deze handleiding wordt u begeleid bij Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6d44f-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="6d44f-108">Sleutelkluis toomanage sleutels voor clusterbeveiliging instellen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="6d44f-109">Een beveiligde cluster in Azure maken via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6d44f-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="6d44f-110">Beheerders met behulp van certificaten verifiëren.</span><span class="sxs-lookup"><span data-stu-id="6d44f-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="6d44f-111">Voor meer geavanceerde beveiligingsopties, zoals gebruikersverificatie met Azure Active Directory en het instellen van certificaten voor Toepassingsbeveiliging, [maken van het cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="6d44f-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="6d44f-112">Een beveiligde cluster is een cluster waarmee wordt voorkomen dat onbevoegde toegang toomanagement bewerkingen, waaronder implementeren, bijwerken en verwijderen van toepassingen, services en Hallo gegevens die ze bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d44f-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="6d44f-113">Een niet-beveiligde cluster is een cluster iedereen kan verbinding maken met tooat elk gewenst moment en beheerbewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6d44f-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="6d44f-114">Hoewel het mogelijk toocreate een niet-beveiligde cluster, is **toocreate sterk aanbevolen een beveiligde cluster**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="6d44f-115">Een niet-beveiligde cluster **later niet kan worden beveiligd** -een nieuw cluster moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="6d44f-116">Hallo concepten zijn hetzelfde voor het maken van beveiligde clusters of Hallo clusters Linux-clusters of clusters met Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6d44f-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="6d44f-117">Zie voor meer informatie en helper scripts voor het maken van beveiligde Linux-clusters, [maken van beveiligde clusters onder Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="6d44f-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="6d44f-118">Hallo parameters die zijn verkregen door het Hallo helper-script dat kunnen worden ingevoerd rechtstreeks in de portal Hallo zoals beschreven in de sectie Hallo [een cluster maken in Azure-portal Hallo](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="6d44f-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="6d44f-119">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d44f-119">Log in tooAzure</span></span>
<span data-ttu-id="6d44f-120">Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="6d44f-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="6d44f-121">Bij het starten van een nieuwe PowerShell-sessie tooyour aanmelden met Azure-account en selecteer uw abonnement voordat u Azure opdrachten uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6d44f-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="6d44f-122">Meld u bij tooyour azure-account:</span><span class="sxs-lookup"><span data-stu-id="6d44f-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6d44f-123">Selecteer uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="6d44f-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="6d44f-124">Key Vault instellen</span><span class="sxs-lookup"><span data-stu-id="6d44f-124">Set up Key Vault</span></span>
<span data-ttu-id="6d44f-125">Dit deel van Hallo handleiding helpt u bij het maken van een Sleutelkluis voor een Service Fabric-cluster in Azure en voor Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="6d44f-126">Zie voor een volledige handleiding op Sleutelkluis hello [Sleutelkluis instructiehandleiding][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="6d44f-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="6d44f-127">Service Fabric maakt gebruik van x.509-certificaten toosecure een cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="6d44f-128">Azure Sleutelkluis is toomanage gebruikte certificaten voor Service Fabric-clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="6d44f-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="6d44f-129">Wanneer een cluster wordt geïmplementeerd in Azure, hello Azure resourceprovider verantwoordelijk voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op Hallo cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6d44f-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="6d44f-130">Hallo illustreert volgende diagram Hallo relatie tussen de Sleutelkluis, een Service Fabric-cluster en hello Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in de Sleutelkluis bij het maken van een cluster:</span><span class="sxs-lookup"><span data-stu-id="6d44f-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installatie van het certificaat][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="6d44f-132">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6d44f-132">Create a Resource Group</span></span>
<span data-ttu-id="6d44f-133">de eerste stap Hallo is toocreate een nieuwe resourcegroep specifiek voor Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6d44f-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="6d44f-134">Als Sleutelkluis in een eigen resourcegroep wordt aanbevolen zodat u kunt resourcegroepen berekenings- en - zoals de resourcegroep die uw Service Fabric-cluster heeft Hallo - verwijderen zonder verlies van uw sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="6d44f-135">Hallo-resourcegroep met uw Sleutelkluis moet Hallo dezelfde regio bevinden als het Hallo-cluster dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="6d44f-136">Sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="6d44f-136">Create Key Vault</span></span>
<span data-ttu-id="6d44f-137">Een Sleutelkluis maken in de nieuwe resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d44f-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="6d44f-138">Hallo Sleutelkluis **moet zijn ingeschakeld voor de implementatie van** tooallow Service Fabric resource provider tooget certificaten van het Hallo en installeren op clusterknooppunten:</span><span class="sxs-lookup"><span data-stu-id="6d44f-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

<span data-ttu-id="6d44f-139">Als u een bestaande Sleutelkluis hebt, kunt u dit inschakelen voor implementatie met behulp van Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="6d44f-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="6d44f-140">Certificaten tooKey kluis toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d44f-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="6d44f-141">Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="6d44f-142">Zie voor meer informatie over hoe de certificaten worden gebruikt in Service Fabric, [scenario's voor beveiliging van Service Fabric-cluster][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="6d44f-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="6d44f-143">Cluster en de server-certificaat (vereist)</span><span class="sxs-lookup"><span data-stu-id="6d44f-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="6d44f-144">Dit certificaat is vereist toosecure een cluster en te voorkomen dat onbevoegde toegang tooit.</span><span class="sxs-lookup"><span data-stu-id="6d44f-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="6d44f-145">Biedt clusterbeveiliging in een aantal manieren:</span><span class="sxs-lookup"><span data-stu-id="6d44f-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="6d44f-146">**Cluster-verificatie:** knooppunt naar communicatie voor cluster federation verifieert.</span><span class="sxs-lookup"><span data-stu-id="6d44f-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="6d44f-147">Alleen knooppunten die u hun identiteit met dit certificaat bewijzen kunnen kunnen Hallo-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="6d44f-148">**Server-verificatie:** verifieert Hallo cluster management eindpunten tooa management-client, zodat hello Beheerclient weet het echte cluster toohello communiceert.</span><span class="sxs-lookup"><span data-stu-id="6d44f-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="6d44f-149">Dit certificaat biedt ook SSL voor Hallo HTTPS beheer-API en voor Service Fabric Explorer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6d44f-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="6d44f-150">tooserve deze doeleinden Hallo certificaat moet voldoen aan Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="6d44f-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="6d44f-151">Hallo-certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d44f-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="6d44f-152">Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.</span><span class="sxs-lookup"><span data-stu-id="6d44f-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="6d44f-153">Hallo onderwerpnaam van het certificaat moet overeenkomen met Hallo domein gebruikt tooaccess Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="6d44f-154">Dit is vereiste tooprovide SSL voor het HTTPS-eindpunten voor beheer en de Service Fabric Explorer Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="6d44f-155">U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo `.cloudapp.azure.com` domein.</span><span class="sxs-lookup"><span data-stu-id="6d44f-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="6d44f-156">Verkrijgen van een aangepaste domeinnaam voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="6d44f-157">Wanneer u aanvragen hebben een certificaat van de onderwerpnaam van een CA Hallo-certificaat moet overeenkomen met aangepaste domeinnaam Hallo gebruikt voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="6d44f-158">Certificaten voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="6d44f-158">Client authentication certificates</span></span>
<span data-ttu-id="6d44f-159">Aanvullende clientcertificaten verifiëren van beheerders voor beheertaken cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="6d44f-160">Service Fabric heeft twee toegangsniveaus: **admin** en **alleen-lezengebruiker**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="6d44f-161">Ten minste moet één certificaat voor beheerderstoegang worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="6d44f-162">Voor extra beveiliging op gebruikersniveau toegang, moet u een afzonderlijk certificaat opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6d44f-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="6d44f-163">Zie voor meer informatie over toegang tot rollen [toegangsbeheer op basis van rollen voor Service Fabric-clients][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="6d44f-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="6d44f-164">U hoeft niet tooupload Client verificatie certificaten tooKey kluis toowork met Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d44f-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="6d44f-165">Deze certificaten moeten alleen toobe opgegeven toousers die zijn gemachtigd voor Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="6d44f-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="6d44f-166">Azure Active Directory is Hallo aanbevolen manier tooauthenticate clients voor cluster beheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="6d44f-167">toouse Azure Active Directory, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="6d44f-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="6d44f-168">Toepassingscertificaten (optioneel)</span><span class="sxs-lookup"><span data-stu-id="6d44f-168">Application certificates (optional)</span></span>
<span data-ttu-id="6d44f-169">Een willekeurig aantal extra certificaten kan worden geïnstalleerd op een cluster om beveiligingsredenen toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d44f-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="6d44f-170">Voordat u uw cluster maakt, overweeg Hallo scenario's voor Toepassingsbeveiliging waarvoor een certificaat toobe geïnstalleerd op Hallo knooppunten, zoals:</span><span class="sxs-lookup"><span data-stu-id="6d44f-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="6d44f-171">Versleuteling en ontsleuteling van configuratiewaarden die van toepassing</span><span class="sxs-lookup"><span data-stu-id="6d44f-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="6d44f-172">Versleuteling van gegevens over knooppunten tijdens de replicatie</span><span class="sxs-lookup"><span data-stu-id="6d44f-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="6d44f-173">Toepassingscertificaten kunnen niet worden geconfigureerd wanneer u een cluster via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6d44f-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="6d44f-174">tooconfigure toepassingscertificaten tijdens de installatie cluster, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="6d44f-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="6d44f-175">U kunt ook een toepassing certificaten toohello cluster toevoegen nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="6d44f-176">Certificaten voor Azure-resource provider opmaak</span><span class="sxs-lookup"><span data-stu-id="6d44f-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="6d44f-177">Bestanden met persoonlijke sleutel (.pfx) kunnen worden toegevoegd en gebruikt rechtstreeks via de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6d44f-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="6d44f-178">Hello Azure-resourceprovider vereist echter sleutels toobe opgeslagen in een speciale JSON-indeling die Hallo .pfx als een Base64-gecodeerde tekenreeks en Hallo wachtwoord voor persoonlijke sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="6d44f-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="6d44f-179">tooaccommodate deze vereisten, sleutels moeten worden geplaatst in een JSON-tekenreeks en vervolgens wordt opgeslagen als *geheimen* in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6d44f-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="6d44f-180">toomake dit eenvoudiger verwerken, een PowerShell-module is [beschikbaar op GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="6d44f-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="6d44f-181">Volg deze stappen toouse Hallo-module:</span><span class="sxs-lookup"><span data-stu-id="6d44f-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="6d44f-182">Hallo volledige inhoud van de opslagplaats Hallo downloaden naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="6d44f-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="6d44f-183">Hallo-module in uw PowerShell-venster importeren:</span><span class="sxs-lookup"><span data-stu-id="6d44f-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="6d44f-184">Hallo `Invoke-AddCertToKeyVault` opdracht in deze PowerShell-module automatisch de persoonlijke sleutel van een certificaat in een JSON-tekenreeks indelingen en tooKey kluis geüpload.</span><span class="sxs-lookup"><span data-stu-id="6d44f-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="6d44f-185">Gebruik deze tooadd Hallo cluster certificaat en een extra toepassing certificaten tooKey kluis.</span><span class="sxs-lookup"><span data-stu-id="6d44f-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="6d44f-186">Herhaal deze stap voor elke extra certificaten tooinstall in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="6d44f-187">Dit zijn alle Hallo Sleutelkluis-vereisten voor het configureren van een Service Fabric-cluster Resource Manager-sjabloon die certificaten voor verificatie, eindpuntbeveiliging management en verificatie en eventuele aanvullende Toepassingsbeveiliging installeert functies die gebruikmaken van X.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="6d44f-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="6d44f-188">U hebt op dit moment nu Hallo na de installatie in Azure:</span><span class="sxs-lookup"><span data-stu-id="6d44f-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="6d44f-189">Sleutelkluis-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="6d44f-189">Key Vault resource group</span></span>
  * <span data-ttu-id="6d44f-190">Key Vault</span><span class="sxs-lookup"><span data-stu-id="6d44f-190">Key Vault</span></span>
    * <span data-ttu-id="6d44f-191">Certificaat voor serververificatie cluster</span><span class="sxs-lookup"><span data-stu-id="6d44f-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="6d44f-192">< /a "maken-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="6d44f-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="6d44f-193">Cluster maken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6d44f-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="6d44f-194">Zoeken naar Hallo Service Fabric-cluster-bron</span><span class="sxs-lookup"><span data-stu-id="6d44f-194">Search for hello Service Fabric cluster resource</span></span>
![zoeken naar Service Fabric-cluster sjabloon op Hallo Azure-portal.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="6d44f-196">Meld u aan toohello [Azure-portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6d44f-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="6d44f-197">Klik op **nieuw** tooadd een nieuwe resource-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6d44f-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="6d44f-198">Zoeken naar Hallo Service Fabric-Cluster sjabloon in Hallo **Marketplace** onder **Alles**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="6d44f-199">Selecteer **Service Fabric-Cluster** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="6d44f-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="6d44f-200">Navigeer toohello **Service Fabric-Cluster** blade, klikt u op **maken**,</span><span class="sxs-lookup"><span data-stu-id="6d44f-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="6d44f-201">Hallo **maken Service Fabric-cluster** blade bevat Hallo vier stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="6d44f-202">1. Basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="6d44f-202">1. Basics</span></span>
![Schermopname van het maken van een nieuwe resourcegroep.][CreateRG]

<span data-ttu-id="6d44f-204">In de blade grondbeginselen Hallo moet u tooprovide Hallo basisdetails voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="6d44f-205">Voer Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="6d44f-206">Voer een **gebruikersnaam** en **wachtwoord** voor extern bureaublad voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6d44f-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="6d44f-207">Zorg ervoor dat tooselect hello **abonnement** dat uw cluster toobe geïmplementeerd, met name als u meerdere abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="6d44f-208">Maak een **nieuwe resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-208">Create a **new resource group**.</span></span> <span data-ttu-id="6d44f-209">Het is aanbevolen toogive het Hallo dezelfde naam als het Hallo-cluster, omdat het helpt bij het vinden ze later, vooral wanneer u toomake wijzigingen tooyour implementatie probeert of verwijder uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d44f-210">U kunt ervoor kiezen een bestaande resourcegroep toouse, is maar het een toocreate raadzaam om een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6d44f-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="6d44f-211">Dit maakt het eenvoudig toodelete-clusters die u niet nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="6d44f-212">Selecteer Hallo **regio** waarin u toocreate Hallo cluster wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="6d44f-213">Hallo dezelfde regio die uw sleutel Vault heeft, moet u gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d44f-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="6d44f-214">2. Configuratie van het cluster</span><span class="sxs-lookup"><span data-stu-id="6d44f-214">2. Cluster configuration</span></span>
![Een knooppunttype maken][CreateNodeType]

<span data-ttu-id="6d44f-216">Configureer de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="6d44f-216">Configure your cluster nodes.</span></span> <span data-ttu-id="6d44f-217">Knooppunttypen definiëren Hallo VM-grootten, Hallo aantal virtuele machines en hun eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="6d44f-218">Uw cluster kan er meer dan één knooppunttype, maar het primaire knooppunttype hello (eerste is die u op Hallo portal definieert Hallo) moet ten minste vijf virtuele machines, omdat dit knooppunttype Hallo waar de Service Fabric-systeemservices worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="6d44f-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="6d44f-219">Configureer geen **plaatsingseigenschappen** omdat een standaardeigenschap van de plaatsing van 'NodeTypeName' wordt automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d44f-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="6d44f-220">Een veelvoorkomend scenario voor typen met meerdere knooppunten is een toepassing met een front-end-service en een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="6d44f-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="6d44f-221">Gewenste tooput Hallo front-end-service op kleinere virtuele machines (VM-grootten zoals D2) met poorten open toohello Internet, maar u tooput Hallo back-end-service op grotere virtuele machines (met VM-grootten zoals D4, D6 en D15) zonder internetverbinding poorten geopend.</span><span class="sxs-lookup"><span data-stu-id="6d44f-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="6d44f-222">Kies een naam voor uw knooppunttype (1 too12 tekens die alleen letters en cijfers bevatten).</span><span class="sxs-lookup"><span data-stu-id="6d44f-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="6d44f-223">Hallo minimale **grootte** van virtuele machines voor het primaire knooppunt Hallo type wordt aangedreven door Hallo **duurzaamheid** laag die u voor Hallo-cluster kiest.</span><span class="sxs-lookup"><span data-stu-id="6d44f-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="6d44f-224">Hallo standaard voor Hallo duurzaamheid laag is Brons.</span><span class="sxs-lookup"><span data-stu-id="6d44f-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="6d44f-225">Zie voor meer informatie over duurzaamheid [hoe toochoose Hallo Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="6d44f-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="6d44f-226">Selecteer Hallo VM-grootte en de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="6d44f-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="6d44f-227">D-reeks VMs SSD-stations hebben en worden sterk aanbevolen voor stateful toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="6d44f-228">Geen gebruik van een VM SKU gedeeltelijke kernen heeft of kleiner zijn dan 7 GB aan beschikbare schijfruimte capaciteit.</span><span class="sxs-lookup"><span data-stu-id="6d44f-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="6d44f-229">Hallo minimale **getal** van virtuele machines voor het primaire knooppunt Hallo type wordt aangedreven door Hallo **betrouwbaarheid** laag die u kiest.</span><span class="sxs-lookup"><span data-stu-id="6d44f-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="6d44f-230">Hallo standaardwaarde voor de betrouwbaarheidslaag Hallo is Zilver.</span><span class="sxs-lookup"><span data-stu-id="6d44f-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="6d44f-231">Zie voor meer informatie over de betrouwbaarheid, [hoe toochoose Hallo Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="6d44f-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="6d44f-232">Hallo aantal virtuele machines voor het knooppunttype Hallo kiezen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="6d44f-233">U kunt omhoog of omlaag Hallo aantal virtuele machines in een knooppunttype later op schalen, maar op het primaire knooppunttype hello, minimale hello wordt aangedreven door Hallo betrouwbaarheid niveau dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="6d44f-234">Andere knooppunttypen kunnen een minimum van 1 VM hebben.</span><span class="sxs-lookup"><span data-stu-id="6d44f-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="6d44f-235">Aangepaste eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="6d44f-235">Configure custom endpoints.</span></span> <span data-ttu-id="6d44f-236">Dit veld kunt u een door komma's gescheiden lijst met poorten die u wilt dat tooexpose via hello Azure Load Balancer toohello tooenter openbare Internet voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="6d44f-237">Bijvoorbeeld, als u van plan een cluster met web application tooyour toodeploy bent, typt u '80' hier tooallow verkeer op poort 80 in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6d44f-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="6d44f-238">Zie voor meer informatie over eindpunten [communiceren met toepassingen][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="6d44f-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="6d44f-239">Configureren van cluster **diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="6d44f-240">Diagnostische gegevens zijn standaard ingeschakeld op uw cluster tooassist met het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="6d44f-241">Als u wilt dat toodisable diagnostics wijzigen Hallo **Status** te schakelen**uit**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="6d44f-242">Het uitschakelen van diagnostische gegevens is **niet** aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="6d44f-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="6d44f-243">Selecteer Hallo Fabric upgrademodus u wilt instellen van uw cluster op.</span><span class="sxs-lookup"><span data-stu-id="6d44f-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="6d44f-244">Selecteer **automatische**, als u wilt dat Hallo system tooautomatically ophalen Hallo meest recente versie en probeer het tooupgrade uw cluster tooit.</span><span class="sxs-lookup"><span data-stu-id="6d44f-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="6d44f-245">Hallo-modus te instellen**handmatige**, als u wilt dat toochoose een ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="6d44f-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="6d44f-246">Wij ondersteunen alleen clusters die met een ondersteunde versie van service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d44f-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="6d44f-247">Door het selecteren van Hallo **handmatige** modus u onderneemt op Hallo verantwoordelijkheid tooupgrade uw versie van cluster tooa ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6d44f-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="6d44f-248">Zie voor meer informatie op Hallo Fabric upgrademodus Hallo [service fabric-cluster upgrade-document.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="6d44f-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="6d44f-249">3. Beveiliging</span><span class="sxs-lookup"><span data-stu-id="6d44f-249">3. Security</span></span>
![Schermopname van beveiligingsconfiguraties op Azure-portal.][SecurityConfigs]

<span data-ttu-id="6d44f-251">de laatste stap Hallo is tooprovide certificaat informatie toosecure Hallo cluster Hallo Sleutelkluis en certificaat informatie eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="6d44f-252">Hallo primaire certificaat voor velden te vullen met Hallo uitvoer ontleend aan het uploaden van Hallo **cluster certificaat** tooKey met behulp van kluis Hallo `Invoke-AddCertToKeyVault` PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="6d44f-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="6d44f-253">Controleer Hallo **geavanceerde instellingen configureren** tooenter voor clientcertificaten voor vak **Beheerclient** en **alleen-lezen client**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="6d44f-254">Voer in deze velden Hallo vingerafdruk van het clientcertificaat admin en Hallo vingerafdruk van het certificaat alleen-lezengebruiker in, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d44f-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="6d44f-255">Wanneer beheerders tooconnect toohello cluster proberen, krijgen ze toegang alleen als ze beschikken over een certificaat met een vingerafdruk die overeenkomt met de Hallo vingerafdruk waarden die u hier opgeeft.</span><span class="sxs-lookup"><span data-stu-id="6d44f-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="6d44f-256">4. Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6d44f-256">4. Summary</span></span>
![<span data-ttu-id="6d44f-257">Schermopname van Hallo start board weergeven "Deploying Service Fabric-Cluster."</span><span class="sxs-lookup"><span data-stu-id="6d44f-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="6d44f-258">toocomplete hello cluster maken, klikt u op **samenvatting** toosee Hallo configuraties die u hebt opgegeven of downloaden hello Azure Resource Manager-sjabloon dat die toodeploy uw cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6d44f-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="6d44f-259">Nadat u de instellingen verplicht voor Hallo hebt opgegeven, Hallo **OK** knop wordt groen en kunt u Hallo cluster maken van het proces starten door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="6d44f-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="6d44f-260">Voortgang van het Hallo maken in kennisgevingen hello, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="6d44f-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="6d44f-261">(Klik op Hallo ' ' belpictogram bijna Hallo statusbalk Hallo rechterbovenhoek van het scherm). Als u hebt geklikt **pincode tooStartboard** tijdens het Hallo-cluster maken, ziet u **Service Fabric-Cluster implementeren** vastgemaakt toohello **Start** mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="6d44f-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="6d44f-262">De clusterstatus van uw bekijken</span><span class="sxs-lookup"><span data-stu-id="6d44f-262">View your cluster status</span></span>
![Schermopname van het clusterdetails in Hallo-dashboard.][ClusterDashboard]

<span data-ttu-id="6d44f-264">Als uw cluster is gemaakt, kunt u uw cluster in Hallo portal controleren:</span><span class="sxs-lookup"><span data-stu-id="6d44f-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="6d44f-265">Ga te**Bladeren** en klik op **Service Fabric-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="6d44f-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="6d44f-266">Zoek uw cluster en klik erop.</span><span class="sxs-lookup"><span data-stu-id="6d44f-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="6d44f-267">U ziet nu Hallo details van het cluster in Hallo-dashboard, met inbegrip van het cluster Hallo openbaar eindpunt en een koppeling tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6d44f-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="6d44f-268">Hallo **knooppunt Monitor** sectie op Hallo van het cluster dashboard blade Hallo aantal virtuele machines die in orde en niet in orde zijn aangeeft.</span><span class="sxs-lookup"><span data-stu-id="6d44f-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="6d44f-269">U vindt meer informatie over de status van het cluster Hallo op [Service Fabric health model inleiding][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="6d44f-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="6d44f-270">Service Fabric-clusters vereisen van een bepaald aantal knooppunten toobe altijd toomaintain beschikbaar en het behouden van status - waarnaar wordt verwezen tooas 'onderhouden quorum'.</span><span class="sxs-lookup"><span data-stu-id="6d44f-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="6d44f-271">Therfore, het is doorgaans niet veilig tooshut omlaag alle machines in de cluster Hallo tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="6d44f-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="6d44f-272">Extern verbinding maken met virtuele-Machineschaalset tooa-exemplaar of een clusterknooppunt</span><span class="sxs-lookup"><span data-stu-id="6d44f-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="6d44f-273">Elk Hallo NodeTypes geeft u in uw cluster resultaten in een virtuele-Machineschaalset ophalen van de installatie.</span><span class="sxs-lookup"><span data-stu-id="6d44f-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="6d44f-274">Zie [extern verbinding tooa virtuele-Machineschaalset exemplaar] [ remote-connect-to-a-vm-scale-set] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d44f-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d44f-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d44f-275">Next steps</span></span>
<span data-ttu-id="6d44f-276">U hebt op dit moment een beveiligde cluster dat gebruik van certificaten voor beheer-verificatie.</span><span class="sxs-lookup"><span data-stu-id="6d44f-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="6d44f-277">Vervolgens [tooyour cluster verbinding](service-fabric-connect-to-secure-cluster.md) en meer informatie over hoe te[toepassing geheimen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="6d44f-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="6d44f-278">Ook meer informatie over [Service Fabric-ondersteuningsopties](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="6d44f-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
