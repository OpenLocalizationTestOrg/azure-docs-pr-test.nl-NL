---
title: Service Fabric-cluster maken in de Azure portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe u een beveiligde Service Fabric-cluster in Azure met behulp van de Azure portal en Azure Key Vault instelt.
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
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="70734-103">Maken van een Service Fabric-cluster in Azure met Azure portal</span><span class="sxs-lookup"><span data-stu-id="70734-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70734-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70734-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="70734-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="70734-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="70734-106">Dit is een stapsgewijze handleiding die u bij de stappen helpt voor het instellen van een beveiligde Service Fabric-cluster in Azure met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="70734-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="70734-107">Deze handleiding doorloopt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="70734-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="70734-108">Sleutelkluis instellen voor het beheren van sleutels voor de clusterbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="70734-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="70734-109">Een beveiligde cluster in Azure maken via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70734-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="70734-110">Beheerders met behulp van certificaten verifiëren.</span><span class="sxs-lookup"><span data-stu-id="70734-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="70734-111">Voor meer geavanceerde beveiligingsopties, zoals gebruikersverificatie met Azure Active Directory en het instellen van certificaten voor Toepassingsbeveiliging, [maken van het cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="70734-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="70734-112">Een beveiligde cluster is een cluster dat voorkomt onbevoegde toegang tot beheertaken uit te voeren, waaronder implementeren, bijwerken en verwijderen van toepassingen, services en de gegevens die ze bevatten.</span><span class="sxs-lookup"><span data-stu-id="70734-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="70734-113">Een niet-beveiligde cluster is een cluster iedereen kan verbinding maken met op elk gewenst moment en beheerbewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70734-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="70734-114">Hoewel het is mogelijk om een niet-beveiligde cluster te maken, is het **ten zeerste aangeraden om een beveiligde cluster te maken**.</span><span class="sxs-lookup"><span data-stu-id="70734-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="70734-115">Een niet-beveiligde cluster **later niet kan worden beveiligd** -een nieuw cluster moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70734-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="70734-116">De concepten zijn hetzelfde voor het maken van beveiligde clusters, ongeacht of de clusters Linux-clusters of Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="70734-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="70734-117">Zie voor meer informatie en helper scripts voor het maken van beveiligde Linux-clusters, [maken van beveiligde clusters onder Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="70734-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="70734-118">De parameters die zijn verkregen door het Help-script dat kunnen worden invoer rechtstreeks in de portal, zoals beschreven in de sectie [een cluster maken in de Azure portal](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="70734-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="70734-119">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="70734-119">Log in to Azure</span></span>
<span data-ttu-id="70734-120">Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="70734-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="70734-121">Bij het starten van een nieuwe PowerShell-sessie aanmelden bij uw Azure-account en selecteer uw abonnement voordat u Azure opdrachten uitvoert.</span><span class="sxs-lookup"><span data-stu-id="70734-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="70734-122">Aanmelden bij uw azure-account:</span><span class="sxs-lookup"><span data-stu-id="70734-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="70734-123">Selecteer uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="70734-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="70734-124">Key Vault instellen</span><span class="sxs-lookup"><span data-stu-id="70734-124">Set up Key Vault</span></span>
<span data-ttu-id="70734-125">Dit deel van de handleiding helpt u bij het maken van een Sleutelkluis voor een Service Fabric-cluster in Azure en voor Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="70734-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="70734-126">Zie voor een volledige handleiding op Sleutelkluis de [Sleutelkluis instructiehandleiding][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="70734-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="70734-127">Service Fabric gebruikt x.509-certificaten voor het beveiligen van een cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="70734-128">Azure Sleutelkluis wordt gebruikt voor het beheren van certificaten voor Service Fabric-clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="70734-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="70734-129">Wanneer een cluster is geïmplementeerd in Azure, wordt de Azure-resourceprovider verantwoordelijk voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op het cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="70734-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="70734-130">Het volgende diagram illustreert de relatie tussen de Sleutelkluis, een Service Fabric-cluster en de Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in de Sleutelkluis bij het maken van een cluster:</span><span class="sxs-lookup"><span data-stu-id="70734-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installatie van het certificaat][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="70734-132">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="70734-132">Create a Resource Group</span></span>
<span data-ttu-id="70734-133">De eerste stap is het maken van een nieuwe resourcegroep specifiek voor Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="70734-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="70734-134">Sleutelkluis in een eigen resourcegroep stellen wordt aanbevolen, zodat u kunt resourcegroepen berekenings- en - zoals de resourcegroep die uw Service Fabric-cluster heeft - zonder verlies van uw sleutels en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="70734-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="70734-135">De resourcegroep met uw Sleutelkluis moet in dezelfde regio bevinden als het cluster dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70734-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="70734-136">Sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="70734-136">Create Key Vault</span></span>
<span data-ttu-id="70734-137">Een Sleutelkluis maken in de nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="70734-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="70734-138">De Sleutelkluis **moet zijn ingeschakeld voor de implementatie van** om toe te staan van de Service Fabric-resourceprovider certificaten van het verkrijgen en installeren op clusterknooppunten:</span><span class="sxs-lookup"><span data-stu-id="70734-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="70734-139">Als u een bestaande Sleutelkluis hebt, kunt u dit inschakelen voor implementatie met behulp van Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="70734-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="70734-140">Voeg certificaten aan Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="70734-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="70734-141">Er worden in Service Fabric certificaten gebruikt voor verificatie en versleuteling om verschillende aspecten van een cluster en de bijbehorende toepassingen te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="70734-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="70734-142">Zie voor meer informatie over hoe de certificaten worden gebruikt in Service Fabric, [scenario's voor beveiliging van Service Fabric-cluster][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="70734-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="70734-143">Cluster en de server-certificaat (vereist)</span><span class="sxs-lookup"><span data-stu-id="70734-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="70734-144">Dit certificaat is vereist voor het beveiligen van een cluster en onbevoegde toegang tot deze voorkomen.</span><span class="sxs-lookup"><span data-stu-id="70734-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="70734-145">Biedt clusterbeveiliging in een aantal manieren:</span><span class="sxs-lookup"><span data-stu-id="70734-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="70734-146">**Cluster-verificatie:** knooppunt naar communicatie voor cluster federation verifieert.</span><span class="sxs-lookup"><span data-stu-id="70734-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="70734-147">Alleen knooppunten die u hun identiteit met dit certificaat bewijzen kunnen kunnen deelnemen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="70734-148">**Server-verificatie:** verifieert de eindpunten van het cluster-beheer met een management-client, zodat de management-client, weet deze communiceert met het echte cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="70734-149">Dit certificaat biedt ook SSL voor de HTTPS-API en voor Service Fabric Explorer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="70734-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="70734-150">Het certificaat moet voldoen aan de volgende vereisten voor deze doeleinden:</span><span class="sxs-lookup"><span data-stu-id="70734-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="70734-151">Het certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="70734-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="70734-152">Het certificaat moet worden gemaakt voor sleuteluitwisseling, geëxporteerd naar een bestand Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="70734-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="70734-153">De onderwerpnaam van het certificaat moet overeenkomen met het domein dat wordt gebruikt voor toegang tot de Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="70734-154">Dit is vereist voor SSL voor het HTTPS-eindpunten voor beheer en de Service Fabric Explorer van het cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="70734-155">U kunt een SSL-certificaat van een certificeringsinstantie (CA) kan niet ophalen voor de `.cloudapp.azure.com` domein.</span><span class="sxs-lookup"><span data-stu-id="70734-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="70734-156">Verkrijgen van een aangepaste domeinnaam voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="70734-157">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt moet de onderwerpnaam van het certificaat overeenkomen met de aangepaste domeinnaam voor uw cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70734-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="70734-158">Certificaten voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="70734-158">Client authentication certificates</span></span>
<span data-ttu-id="70734-159">Aanvullende clientcertificaten verifiëren van beheerders voor beheertaken cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="70734-160">Service Fabric heeft twee toegangsniveaus: **admin** en **alleen-lezengebruiker**.</span><span class="sxs-lookup"><span data-stu-id="70734-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="70734-161">Ten minste moet één certificaat voor beheerderstoegang worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70734-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="70734-162">Voor extra beveiliging op gebruikersniveau toegang, moet u een afzonderlijk certificaat opgegeven.</span><span class="sxs-lookup"><span data-stu-id="70734-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="70734-163">Zie voor meer informatie over toegang tot rollen [toegangsbeheer op basis van rollen voor Service Fabric-clients][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="70734-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="70734-164">U hoeft niet voor het uploaden van certificaten voor clientverificatie voor Sleutelkluis voor gebruik met Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70734-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="70734-165">Deze certificaten hoeft alleen te worden opgegeven voor gebruikers die gemachtigd zijn voor Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="70734-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="70734-166">Azure Active Directory is de aanbevolen manier om clients voor clusterbeheerbewerkingen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="70734-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="70734-167">Voor het gebruik van Azure Active Directory, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="70734-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="70734-168">Toepassingscertificaten (optioneel)</span><span class="sxs-lookup"><span data-stu-id="70734-168">Application certificates (optional)</span></span>
<span data-ttu-id="70734-169">Een willekeurig aantal extra certificaten kan worden geïnstalleerd op een cluster om beveiligingsredenen toepassing.</span><span class="sxs-lookup"><span data-stu-id="70734-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="70734-170">Voordat u uw cluster maakt, houd rekening met de scenario's voor Toepassingsbeveiliging waarvoor een certificaat worden geïnstalleerd op de knooppunten, zoals:</span><span class="sxs-lookup"><span data-stu-id="70734-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="70734-171">Versleuteling en ontsleuteling van configuratiewaarden die van toepassing</span><span class="sxs-lookup"><span data-stu-id="70734-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="70734-172">Versleuteling van gegevens over knooppunten tijdens de replicatie</span><span class="sxs-lookup"><span data-stu-id="70734-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="70734-173">Toepassingscertificaten kunnen niet worden geconfigureerd wanneer u een cluster via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70734-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="70734-174">Voor het configureren van toepassingscertificaten tijdens de installatie cluster, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="70734-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="70734-175">U kunt ook toepassingscertificaten toevoegen aan het cluster nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70734-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="70734-176">Certificaten voor Azure-resource provider opmaak</span><span class="sxs-lookup"><span data-stu-id="70734-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="70734-177">Bestanden met persoonlijke sleutel (.pfx) kunnen worden toegevoegd en gebruikt rechtstreeks via de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="70734-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="70734-178">De Azure-resourceprovider vereist echter sleutels worden opgeslagen in een speciale JSON-indeling met het .pfx als een Base64-gecodeerde tekenreeks en het wachtwoord van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="70734-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="70734-179">Om te voldoen deze vereisten, sleutels moeten worden geplaatst in een JSON-tekenreeks en vervolgens opgeslagen als *geheimen* in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="70734-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="70734-180">Om dit proces gemakkelijker te maken, een PowerShell-module is [beschikbaar op GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="70734-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="70734-181">Volg deze stappen voor het gebruik van de module:</span><span class="sxs-lookup"><span data-stu-id="70734-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="70734-182">De volledige inhoud van de opslagplaats downloaden naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="70734-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="70734-183">Importeer de module in uw PowerShell-venster:</span><span class="sxs-lookup"><span data-stu-id="70734-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="70734-184">De `Invoke-AddCertToKeyVault` opdracht in deze PowerShell-module automatisch de persoonlijke sleutel van een certificaat in een JSON-tekenreeks indelingen en geüpload naar de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="70734-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="70734-185">Gebruik dit voor het certificaat van het cluster en eventuele extra toepassingscertificaten toevoegen aan de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="70734-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="70734-186">Herhaal deze stap voor elke extra certificaten die u wilt installeren in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="70734-187">Dit zijn de Sleutelkluis-vereisten voor het configureren van een Service Fabric-cluster Resource Manager-sjabloon die certificaten voor verificatie, eindpuntbeveiliging management en verificatie en eventuele aanvullende Toepassingsbeveiliging installeert functies die gebruikmaken van X.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="70734-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="70734-188">Nu hebt u nu de volgende instellingen in Azure:</span><span class="sxs-lookup"><span data-stu-id="70734-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="70734-189">Sleutelkluis-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="70734-189">Key Vault resource group</span></span>
  * <span data-ttu-id="70734-190">Key Vault</span><span class="sxs-lookup"><span data-stu-id="70734-190">Key Vault</span></span>
    * <span data-ttu-id="70734-191">Certificaat voor serververificatie cluster</span><span class="sxs-lookup"><span data-stu-id="70734-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="70734-192">< /a "maken-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="70734-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="70734-193">Cluster maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="70734-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="70734-194">Zoeken naar de Service Fabric-cluster-bron</span><span class="sxs-lookup"><span data-stu-id="70734-194">Search for the Service Fabric cluster resource</span></span>
![zoeken naar Service Fabric-cluster sjabloon op de Azure-portal.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="70734-196">Meld u aan bij [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="70734-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="70734-197">Klik op **nieuw** toevoegen van een nieuwe resource-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="70734-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="70734-198">Zoeken naar de sjabloon Service Fabric-Cluster in de **Marketplace** onder **Alles**.</span><span class="sxs-lookup"><span data-stu-id="70734-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="70734-199">Selecteer **Service Fabric-Cluster** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="70734-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="70734-200">Navigeer naar de **Service Fabric-Cluster** blade, klikt u op **maken**,</span><span class="sxs-lookup"><span data-stu-id="70734-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="70734-201">De **maken Service Fabric-cluster** blade bevat de volgende vier stappen.</span><span class="sxs-lookup"><span data-stu-id="70734-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="70734-202">1. Basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="70734-202">1. Basics</span></span>
![Schermopname van het maken van een nieuwe resourcegroep.][CreateRG]

<span data-ttu-id="70734-204">In de blade grondbeginselen moet u de algemene informatie opgeven voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="70734-205">Voer de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="70734-206">Voer een **gebruikersnaam** en **wachtwoord** voor extern bureaublad voor de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="70734-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="70734-207">Zorg ervoor dat u selecteert de **abonnement** dat het cluster worden geïmplementeerd op, met name als u meerdere abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="70734-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="70734-208">Maak een **nieuwe resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="70734-208">Create a **new resource group**.</span></span> <span data-ttu-id="70734-209">Het is raadzaam zodat deze dezelfde naam als het cluster, omdat het helpt bij het vinden ze later, vooral wanneer u probeert te wijzigingen aanbrengen in uw implementatie of verwijder uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="70734-210">Hoewel u een bestaande resourcegroep gebruiken kunt, is het raadzaam om een nieuwe resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="70734-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="70734-211">Hierdoor kunt gemakkelijk clusters die u niet hoeft verwijderen.</span><span class="sxs-lookup"><span data-stu-id="70734-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="70734-212">Selecteer de **regio** in waarop u wilt maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="70734-213">U moet dezelfde regio als uw Sleutelkluis is in.</span><span class="sxs-lookup"><span data-stu-id="70734-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="70734-214">2. Configuratie van het cluster</span><span class="sxs-lookup"><span data-stu-id="70734-214">2. Cluster configuration</span></span>
![Een knooppunttype maken][CreateNodeType]

<span data-ttu-id="70734-216">Configureer de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="70734-216">Configure your cluster nodes.</span></span> <span data-ttu-id="70734-217">Knooppunttypen definiëren de VM-grootten, het aantal virtuele machines en hun eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="70734-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="70734-218">Het cluster kan meer dan één knooppunttype hebben moet, maar het primaire knooppunttype (de eerste optie die u in de portal definieert) ten minste vijf virtuele machines, omdat dit het knooppunttype waar de Service Fabric-systeemservices worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="70734-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="70734-219">Configureer geen **plaatsingseigenschappen** omdat een standaardeigenschap van de plaatsing van 'NodeTypeName' wordt automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="70734-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="70734-220">Een veelvoorkomend scenario voor typen met meerdere knooppunten is een toepassing met een front-end-service en een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="70734-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="70734-221">U wilt de front-end-service plaatsen op kleinere virtuele machines (VM-grootten zoals D2) met poorten openen met het Internet, maar u wilt de back-endservice plaatsen op grotere virtuele machines (met VM-grootten zoals D4, D6 en D15) zonder internetverbinding poorten geopend.</span><span class="sxs-lookup"><span data-stu-id="70734-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="70734-222">Kies een naam voor uw knooppunttype (1-12 tekens die alleen letters en cijfers bevatten).</span><span class="sxs-lookup"><span data-stu-id="70734-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="70734-223">De minimale **grootte** van virtuele machines voor het primaire knooppunt type wordt aangedreven door de **duurzaamheid** laag die u voor het cluster kiest.</span><span class="sxs-lookup"><span data-stu-id="70734-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="70734-224">De standaardwaarde voor de laag duurzaamheid is Brons.</span><span class="sxs-lookup"><span data-stu-id="70734-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="70734-225">Zie voor meer informatie over duurzaamheid [het kiezen van de Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="70734-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="70734-226">Selecteer het VM-grootte en de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="70734-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="70734-227">D-reeks VMs SSD-stations hebben en worden sterk aanbevolen voor stateful toepassingen.</span><span class="sxs-lookup"><span data-stu-id="70734-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="70734-228">Geen gebruik van een VM SKU gedeeltelijke kernen heeft of kleiner zijn dan 7 GB aan beschikbare schijfruimte capaciteit.</span><span class="sxs-lookup"><span data-stu-id="70734-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="70734-229">De minimale **getal** van virtuele machines voor het primaire knooppunt type wordt aangedreven door de **betrouwbaarheid** laag die u kiest.</span><span class="sxs-lookup"><span data-stu-id="70734-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="70734-230">De standaardwaarde voor de betrouwbaarheidslaag is Zilver.</span><span class="sxs-lookup"><span data-stu-id="70734-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="70734-231">Zie voor meer informatie over de betrouwbaarheid, [het kiezen van de Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="70734-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="70734-232">Het aantal virtuele machines voor het knooppunttype kiezen.</span><span class="sxs-lookup"><span data-stu-id="70734-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="70734-233">U kunt omhoog of omlaag het aantal virtuele machines in een knooppunttype later op schalen, maar op het primaire knooppunttype minimaal wordt aangedreven door het niveau van betrouwbaarheid die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="70734-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="70734-234">Andere knooppunttypen kunnen een minimum van 1 VM hebben.</span><span class="sxs-lookup"><span data-stu-id="70734-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="70734-235">Aangepaste eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="70734-235">Configure custom endpoints.</span></span> <span data-ttu-id="70734-236">Dit veld kunt u een door komma's gescheiden lijst met poorten die u wilt weergeven via de Azure Load Balancer met het openbare Internet voor uw toepassingen invoeren.</span><span class="sxs-lookup"><span data-stu-id="70734-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="70734-237">Bijvoorbeeld als u een webtoepassing met uw cluster implementeert wilt, voert u '80' hier voor verkeer op poort 80 in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="70734-238">Zie voor meer informatie over eindpunten [communiceren met toepassingen][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="70734-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="70734-239">Configureren van cluster **diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="70734-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="70734-240">Diagnostische gegevens zijn standaard ingeschakeld op het cluster om te helpen bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="70734-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="70734-241">Als u wilt uitschakelen, wijziging van diagnostische gegevens van de **Status** in-of uitschakelen op **uit**.</span><span class="sxs-lookup"><span data-stu-id="70734-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="70734-242">Het uitschakelen van diagnostische gegevens is **niet** aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="70734-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="70734-243">Selecteer de Fabric upgrade modus die u instellen van uw cluster wilt op.</span><span class="sxs-lookup"><span data-stu-id="70734-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="70734-244">Selecteer **automatische**, als u wilt dat het systeem automatisch kunnen worden opgepikt de meest recente versie en probeer het bijwerken van uw cluster naar het.</span><span class="sxs-lookup"><span data-stu-id="70734-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="70734-245">De modus instellen op **handmatige**, als u wilt kiezen van een ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="70734-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="70734-246">Wij ondersteunen alleen clusters die met een ondersteunde versie van service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70734-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="70734-247">U selecteert de **handmatige** modus u onderneemt op de verantwoordelijkheid voor het upgraden van uw cluster naar een ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="70734-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="70734-248">Voor meer informatie over de Fabric-modus Zie upgrade de [service fabric-cluster upgrade-document.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="70734-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="70734-249">3. Beveiliging</span><span class="sxs-lookup"><span data-stu-id="70734-249">3. Security</span></span>
![Schermopname van beveiligingsconfiguraties op Azure-portal.][SecurityConfigs]

<span data-ttu-id="70734-251">De laatste stap is het certificaat informatie als u wilt beveiligen van het cluster met behulp van de Sleutelkluis en een certificaat informatie eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70734-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="70734-252">Vul de velden van het primaire certificaat voor de uitvoer die is verkregen van het uploaden van de **cluster certificaat** Sleutelkluis via de `Invoke-AddCertToKeyVault` PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="70734-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="70734-253">Controleer de **geavanceerde instellingen configureren** vak in te voeren voor clientcertificaten voor **Beheerclient** en **alleen-lezen client**.</span><span class="sxs-lookup"><span data-stu-id="70734-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="70734-254">Voer de vingerafdruk van het clientcertificaat admin en de vingerafdruk van het certificaat alleen-lezengebruiker in, indien van toepassing in deze velden.</span><span class="sxs-lookup"><span data-stu-id="70734-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="70734-255">Wanneer beheerders probeert verbinding maken met het cluster, krijgen ze toegang alleen als ze beschikken over een certificaat met een vingerafdruk die overeenkomt met de vingerafdruk waarden die u hier opgeeft.</span><span class="sxs-lookup"><span data-stu-id="70734-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="70734-256">4. Samenvatting</span><span class="sxs-lookup"><span data-stu-id="70734-256">4. Summary</span></span>
![<span data-ttu-id="70734-257">Schermopname van de start board weergeven "Deploying Service Fabric-Cluster."</span><span class="sxs-lookup"><span data-stu-id="70734-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="70734-258">Als u wilt maken van het cluster hebt voltooid, klikt u op **samenvatting** zien van de configuraties die u hebt opgegeven of download de Azure Resource Manager-sjabloon die die gebruikt voor het implementeren van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="70734-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="70734-259">Nadat u hebt opgegeven dat de instellingen verplicht de **OK** knop wordt groen en u kunt het proces voor het cluster maken starten door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="70734-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="70734-260">U kunt de voortgang van het maken in de meldingen bekijken.</span><span class="sxs-lookup"><span data-stu-id="70734-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="70734-261">(Klik op het belpictogram bij de statusbalk rechtsboven in uw scherm.) Als u hebt geklikt **vastmaken aan Startboard** tijdens het maken van het cluster, ziet u **Service Fabric-Cluster implementeren** vastgemaakt aan de **Start** mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="70734-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="70734-262">De clusterstatus van uw bekijken</span><span class="sxs-lookup"><span data-stu-id="70734-262">View your cluster status</span></span>
![Schermopname van het clusterdetails in het dashboard.][ClusterDashboard]

<span data-ttu-id="70734-264">Als uw cluster is gemaakt, kunt u uw cluster in de portal controleren:</span><span class="sxs-lookup"><span data-stu-id="70734-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="70734-265">Ga naar **Bladeren** en klik op **Service Fabric-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="70734-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="70734-266">Zoek uw cluster en klik erop.</span><span class="sxs-lookup"><span data-stu-id="70734-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="70734-267">U kunt de gegevens van uw cluster nu bekijken op het dashboard, waaronder het openbare eindpunt van het cluster en een koppeling naar Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="70734-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="70734-268">De **knooppunt Monitor** gedeelte van het cluster dashboard blade geeft het aantal virtuele machines die in orde is en niet in orde zijn.</span><span class="sxs-lookup"><span data-stu-id="70734-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="70734-269">U vindt meer informatie over de status van het cluster op [Service Fabric health model inleiding][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="70734-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="70734-270">Service Fabric-clusters vereisen een bepaald aantal knooppunten voor altijd voor beschikbaarheid onderhouden en het behouden van status - aangeduid als 'onderhouden quorum'.</span><span class="sxs-lookup"><span data-stu-id="70734-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="70734-271">Therfore, het is doorgaans niet veilig afsluiten alle machines in het cluster tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="70734-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="70734-272">Extern verbinding maken met een virtuele-Machineschaalset-exemplaar of een clusterknooppunt</span><span class="sxs-lookup"><span data-stu-id="70734-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="70734-273">Elk van de NodeTypes geeft u in uw cluster resultaten in een virtuele-Machineschaalset ophalen van de installatie.</span><span class="sxs-lookup"><span data-stu-id="70734-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="70734-274">Zie [extern verbinding maken met een exemplaar van virtuele-Machineschaalset] [ remote-connect-to-a-vm-scale-set] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="70734-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70734-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70734-275">Next steps</span></span>
<span data-ttu-id="70734-276">U hebt op dit moment een beveiligde cluster dat gebruik van certificaten voor beheer-verificatie.</span><span class="sxs-lookup"><span data-stu-id="70734-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="70734-277">Vervolgens [verbinding maken met uw cluster](service-fabric-connect-to-secure-cluster.md) en meer informatie over hoe [toepassing geheimen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="70734-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="70734-278">Ook meer informatie over [Service Fabric-ondersteuningsopties](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="70734-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
