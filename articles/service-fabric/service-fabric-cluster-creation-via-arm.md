---
title: aaaCreate een Azure Service Fabric-cluster van een sjabloon | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van een beveiligde Service Fabric-cluster in Azure met behulp van Azure Resource Manager en Azure Key Vault Azure Active Directory (Azure AD) voor clientverificatie.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="0fa0c-103">Maken van een Service Fabric-cluster met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0fa0c-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fa0c-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0fa0c-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="0fa0c-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0fa0c-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="0fa0c-106">Deze stapsgewijze handleiding helpt u bij het instellen van een beveiligde Azure Service Fabric-cluster in Azure met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="0fa0c-107">We erkennen dat artikel Hallo lang is.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="0fa0c-108">Tenzij u al grondig bekend met Hallo inhoud bent, worden echter zeker toofollow elke stap zorgvuldig.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="0fa0c-109">Hallo handleiding wordt ingegaan op Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="0fa0c-110">Een Azure sleutelkluis tooupload certificaten voor een cluster en de toepassing beveiliging instellen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="0fa0c-111">Maken van een beveiligde cluster in Azure met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0fa0c-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="0fa0c-112">Verifiëren van gebruikers met behulp van Azure Active Directory (Azure AD) voor Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="0fa0c-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="0fa0c-113">Een beveiligde cluster is een cluster waarmee wordt voorkomen onbevoegde toegang toomanagement bewerkingen dat.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="0fa0c-114">Dit omvat implementeren, bijwerken, en verwijderen toepassingen, services en Hallo gegevens die ze bevatten.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="0fa0c-115">Een niet-beveiligde cluster is een cluster iedereen kan verbinding maken met tooat elk gewenst moment en beheerbewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="0fa0c-116">Hoewel het mogelijk toocreate een niet-beveiligde cluster, raden we u aan een beveiligde cluster te maken van Hallo begin.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="0fa0c-117">Omdat een niet-beveiligde cluster later niet kan worden beveiligd, kan een nieuw cluster moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="0fa0c-118">Hallo-concept van het maken van beveiligde clusters is Hallo hetzelfde, ongeacht of deze Windows- of Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="0fa0c-119">Zie voor meer informatie en helper scripts voor het maken van beveiligde Linux-clusters, [maken van beveiligde clusters onder Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="0fa0c-120">Meld u aan tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="0fa0c-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="0fa0c-121">Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="0fa0c-122">Wanneer u een nieuwe PowerShell-sessie start, meld u aan tooyour Azure-account en uw abonnement te selecteren voordat u Azure-opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="0fa0c-123">Meld u aan tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0fa0c-124">Selecteer uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="0fa0c-125">Een sleutelkluis instellen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-125">Set up a key vault</span></span>
<span data-ttu-id="0fa0c-126">Deze sectie wordt beschreven voor het maken van een sleutelkluis voor een Service Fabric-cluster in Azure en voor Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="0fa0c-127">Raadpleeg voor een volledige handleiding tooAzure Sleutelkluis, toohello [Sleutelkluis instructiehandleiding][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="0fa0c-128">Service Fabric gebruikt x.509-certificaten toosecure een cluster en beveiligingsfuncties van toepassing.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="0fa0c-129">U Sleutelkluis toomanage certificaten gebruiken voor Service Fabric-clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="0fa0c-130">Wanneer een cluster wordt geïmplementeerd in Azure, worden de hello Azure-resourceprovider die verantwoordelijk is voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op Hallo cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="0fa0c-131">Hallo illustreert volgende diagram Hallo relatie tussen Azure Sleutelkluis, een Service Fabric-cluster en hello Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in een sleutelkluis bij het maken van een cluster:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagram van de installatie van het certificaat][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="0fa0c-133">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="0fa0c-133">Create a resource group</span></span>
<span data-ttu-id="0fa0c-134">de eerste stap Hallo is toocreate een resourcegroep specifiek voor uw sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="0fa0c-135">Het is raadzaam dat u de sleutelkluis Hallo in een eigen resourcegroep geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="0fa0c-136">Deze actie kunt u Hallo berekenings- en resourcegroepen, met inbegrip van Hallo resourcegroep die uw Service Fabric-cluster bevat zonder verlies van uw sleutels en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="0fa0c-137">Hallo-resourcegroep met de sleutelkluis _Hallo moet dezelfde regio_ als Hallo-cluster dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="0fa0c-138">Als u van plan toodeploy clusters in meerdere regio's bent, het is raadzaam dat u de resourcegroep Hallo en Hallo sleutelkluis op een manier die welke regio hoort aangeeft bij de naam.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="0fa0c-139">Hallo-uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="0fa0c-140">Een sleutelkluis maken in de nieuwe resourcegroep Hallo</span><span class="sxs-lookup"><span data-stu-id="0fa0c-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="0fa0c-141">Hallo sleutelkluis _moet zijn ingeschakeld voor de implementatie van_ tooallow compute resource provider tooget certificaten van het Hallo en installeer deze op de virtuele machine-exemplaren:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="0fa0c-142">Hallo-uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="0fa0c-143">Gebruik een bestaande sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="0fa0c-143">Use an existing key vault</span></span>

<span data-ttu-id="0fa0c-144">een bestaande sleutelkluis toouse u _moet inschakelen voor de implementatie van_ tooallow Hallo compute resource provider tooget certificaten uit en installeer deze op de clusterknooppunten:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="0fa0c-145">Certificaten tooyour sleutelkluis toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="0fa0c-146">Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="0fa0c-147">Zie voor meer informatie over hoe de certificaten worden gebruikt in Service Fabric, [scenario's voor beveiliging van Service Fabric-cluster][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="0fa0c-148">Cluster en de server-certificaat (vereist)</span><span class="sxs-lookup"><span data-stu-id="0fa0c-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="0fa0c-149">Dit certificaat is vereist toosecure een cluster en te voorkomen dat onbevoegde toegang tooit.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="0fa0c-150">Dit biedt een clusterbeveiliging op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="0fa0c-151">Cluster-verificatie: knooppunt naar communicatie voor cluster federation verifieert.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="0fa0c-152">Alleen knooppunten die u hun identiteit met dit certificaat bewijzen kunnen kunnen Hallo-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="0fa0c-153">Server-verificatie: verifieert Hallo cluster management eindpunten tooa management-client, zodat hello Beheerclient weet het echte cluster toohello communiceert.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="0fa0c-154">Dit certificaat biedt ook een met SSL voor Hallo HTTPS beheer-API en voor Service Fabric Explorer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="0fa0c-155">tooserve deze doeleinden Hallo certificaat moet voldoen aan Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="0fa0c-156">Hallo-certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="0fa0c-157">Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling exporteerbaar tooa Personal Information Exchange (.pfx)-bestand is.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="0fa0c-158">de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="0fa0c-159">Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="0fa0c-160">U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo. cloudapp.azure.com domein.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="0fa0c-161">U moet een aangepaste domeinnaam voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="0fa0c-162">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="0fa0c-163">Toepassingscertificaten (optioneel)</span><span class="sxs-lookup"><span data-stu-id="0fa0c-163">Application certificates (optional)</span></span>
<span data-ttu-id="0fa0c-164">Een willekeurig aantal extra certificaten kan worden geïnstalleerd op een cluster om beveiligingsredenen toepassing.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="0fa0c-165">Voordat u uw cluster maakt, overweeg Hallo scenario's voor Toepassingsbeveiliging waarvoor een certificaat toobe geïnstalleerd op Hallo knooppunten, zoals:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="0fa0c-166">Versleuteling en ontsleuteling van configuratiewaarden die van toepassing.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="0fa0c-167">Codering van gegevens over knooppunten tijdens de replicatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="0fa0c-168">Certificaten voor Azure-resource provider opmaak</span><span class="sxs-lookup"><span data-stu-id="0fa0c-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="0fa0c-169">U kunt toevoegen en gebruiken van persoonlijke sleutel (PFX-bestanden) rechtstreeks via de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="0fa0c-170">Hello Azure compute resourceprovider vereist echter sleutels toobe opgeslagen in een speciale notatie JSON (JavaScript Object)-indeling.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="0fa0c-171">Hallo-indeling bevat Hallo pfx-bestand als een base 64 gecodeerde tekenreeks zijn en Hallo-wachtwoord voor persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="0fa0c-172">tooaccommodate vault voor deze vereisten, Hallo sleutels moeten worden geplaatst in een JSON-tekenreeks en vervolgens als 'geheimen' hello sleutel worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="0fa0c-173">toomake dit eenvoudiger, verwerkt een [PowerShell-module is beschikbaar op GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="0fa0c-174">toouse Hallo-module, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="0fa0c-175">Hallo volledige inhoud van de opslagplaats Hallo downloaden naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="0fa0c-176">Ga toohello lokale map.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="0fa0c-177">Hallo ServiceFabricRPHelpers module in uw PowerShell-venster importeren:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="0fa0c-178">Hallo `Invoke-AddCertToKeyVault` opdracht in deze PowerShell-module automatisch de persoonlijke sleutel van een certificaat in een JSON-tekenreeks indelingen en toohello sleutelkluis geüpload.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="0fa0c-179">Hallo opdracht tooadd Hallo cluster certificaat en een sleutelkluis voor extra toepassing certificaten toohello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="0fa0c-180">Herhaal deze stap voor elke extra certificaten tooinstall in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="0fa0c-181">Een bestaand certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="0fa0c-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="0fa0c-182">Als er een fout optreedt, zoals Hallo een weergegeven, betekent dit meestal dat er een conflict resource-URL.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="0fa0c-183">tooresolve hello conflict Hallo sleutelkluis-naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="0fa0c-184">Nadat het Hallo-conflict is opgelost, er Hallo uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="0fa0c-185">U moet Hallo drie voorgaande tekenreeksen, CertificateThumbprint SourceVault en CertificateURL, tooset van een beveiligde Service Fabric-cluster en de tooobtain toepassingscertificaten die u voor de beveiliging van toepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="0fa0c-186">Als u niet Hallo tekenreeksen opslaat, kan het moeilijk tooretrieve ze een query uitgevoerd op Hallo key later Vault zijn.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="0fa0c-187">Een zelfondertekend certificaat maken en uploaden toohello sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="0fa0c-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="0fa0c-188">Als u al uw certificaten toohello-sleutelkluis hebt geüpload, moet u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="0fa0c-189">Deze stap is voor een nieuw zelfondertekend certificaat genereren en uploaden tooyour sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="0fa0c-190">Nadat u parameters in het volgende script Hallo Hallo wijzigen en vervolgens uit te voeren, moet u worden gevraagd om het wachtwoord voor een certificaat.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="0fa0c-191">Als er een fout optreedt, zoals Hallo een weergegeven, betekent dit meestal dat er een conflict resource-URL.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="0fa0c-192">tooresolve Hallo conflict wijziging Hallo sleutelkluisnaam, de naam van de RG, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="0fa0c-193">Nadat het Hallo-conflict is opgelost, er Hallo uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="0fa0c-194">U moet Hallo drie voorgaande tekenreeksen, CertificateThumbprint SourceVault en CertificateURL, tooset van een beveiligde Service Fabric-cluster en de tooobtain toepassingscertificaten die u voor de beveiliging van toepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="0fa0c-195">Als u niet Hallo tekenreeksen opslaat, kan het moeilijk tooretrieve ze een query uitgevoerd op Hallo key later Vault zijn.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="0fa0c-196">Op dit moment hebt u Hallo elementen in plaats te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="0fa0c-197">Hallo sleutelkluis resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-197">hello key vault resource group.</span></span>
* <span data-ttu-id="0fa0c-198">Hallo sleutelkluis en de URL (SourceVault in Hallo voorafgaand aan de uitvoer van PowerShell genoemd).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="0fa0c-199">Hallo cluster certificaat voor serververificatie en de bijbehorende URL in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="0fa0c-200">Hallo toepassingscertificaten en de URL's in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="0fa0c-201">Azure Active Directory instellen voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="0fa0c-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="0fa0c-202">Azure AD kan organisaties (ook wel tenants) toomanage gebruiker toegang tooapplications.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="0fa0c-203">Toepassingen worden onderverdeeld in die met een webgebaseerde gebruikersinterface voor aanmelding en die een native client-ervaring.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="0fa0c-204">In dit artikel gaan we ervan uit dat u al een tenant hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="0fa0c-205">Als u niet hebt, starten door te lezen [hoe tooget een Azure Active Directory-tenant][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="0fa0c-206">Een Service Fabric-cluster biedt verschillende vermelding punten tooits beheerfunctionaliteit, met inbegrip van Hallo webgebaseerde [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] en [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="0fa0c-207">Als gevolg hiervan, maakt u twee Azure AD-toepassingen toocontrol toegang toohello cluster, een webtoepassing en een systeemeigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="0fa0c-208">toosimplify bepaalde Hallo stappen betrokken bij de Azure AD configureren met een Service Fabric-cluster, hebben wij een set Windows PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa0c-209">Hallo volgende stappen uit voordat u Hallo-cluster maakt, moet u voltooien.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="0fa0c-210">Omdat Hallo scripts verwacht dat de clusternamen van de- en eindpunten, wordt Hallo waarden moeten worden gepland en niet de waarden die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="0fa0c-211">[Hallo-scripts downloaden] [ sf-aad-ps-script-download] tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="0fa0c-212">Klik met de rechtermuisknop Hallo zip-bestand, selecteer **eigenschappen**, selecteer Hallo **blokkering** selectievakje en klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="0fa0c-213">Pak het zip-bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="0fa0c-214">Voer `SetupApplications.ps1`, en geef Hallo TenantId, ClusterName en WebApplicationReplyUrl als parameters.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="0fa0c-215">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="0fa0c-216">U vindt uw TenantId door het uitvoeren van PowerShell-opdracht Hallo `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="0fa0c-217">Uitvoeren van deze opdracht geeft Hallo TenantId voor elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="0fa0c-218">Clusternaam is gebruikte tooprefix hello Azure AD-toepassingen die zijn gemaakt door Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="0fa0c-219">Hoeft niet de naam van de werkelijke cluster Hallo toomatch exact.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="0fa0c-220">Het beoogde alleen toomake is het eenvoudiger toomap Azure AD-artefacten toohello Service Fabric-cluster dat ze worden gebruikt met.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="0fa0c-221">WebApplicationReplyUrl is Hallo standaardeindpunt die Azure AD tooyour gebruikers retourneert nadat ze Voltooi de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="0fa0c-222">Dit eindpunt als Hallo Service Fabric Explorer eindpunt voor uw cluster, dat standaard is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="0fa0c-223">https://&lt;cluster_domain&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="0fa0c-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="0fa0c-224">U bent na vragen aan gebruiker toosign in tooan-account met voor hello Azure AD-tenant beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="0fa0c-225">Nadat u zich aanmeldt, Hallo script maakt Hallo web- en systeemeigen toepassingen toorepresent Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="0fa0c-226">Als u hello-tenant-toepassingen in Hallo bekijkt [klassieke Azure-portal][azure-classic-portal], ziet u twee nieuwe vermeldingen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="0fa0c-227">*Clusternaam*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="0fa0c-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="0fa0c-228">*Clusternaam*\_Client</span><span class="sxs-lookup"><span data-stu-id="0fa0c-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="0fa0c-229">Hallo-script wordt afgedrukt Hallo JSON vereist door hello Azure Resource Manager-sjabloon wanneer u Hallo-cluster in de volgende sectie hello, maakt dus is het een goed idee tookeep Hallo PowerShell-venster openen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="0fa0c-230">Een Service Fabric-cluster Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="0fa0c-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="0fa0c-231">In deze sectie levert Hallo Hallo voorgaande PowerShell-opdrachten in het Resource Manager-sjabloon van een Service Fabric-cluster worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="0fa0c-232">Voorbeeld Resource Manager-sjablonen zijn beschikbaar in Hallo [Azure snel starten-sjablonengalerie op GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="0fa0c-233">Deze sjablonen kunnen worden gebruikt als een beginpunt voor uw cluster-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="0fa0c-234">Hallo Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="0fa0c-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="0fa0c-235">Deze handleiding gebruikt Hallo [beveiligde 5 knooppunten] [ service-fabric-secure-cluster-5-node-1-nodetype] voorbeeldsjabloon en sjabloonparameters.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="0fa0c-236">Download `azuredeploy.json` en `azuredeploy.parameters.json` tooyour computer en opent u beide bestanden in uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="0fa0c-237">Certificaten toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-237">Add certificates</span></span>
<span data-ttu-id="0fa0c-238">U kunt certificaten tooa cluster Resource Manager-sjabloon toevoegen door te verwijzen naar Hallo sleutelkluis waarin de certificaatsleutels Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="0fa0c-239">Het is raadzaam dat u Hallo sleutelkluis waarden in een Resource Manager-sjabloonbestand parameters plaatsen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="0fa0c-240">In dat geval houdt Hallo Resource Manager sjabloonbestand herbruikbare en gratis waarden specifieke tooa implementatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="0fa0c-241">Alle certificaten toohello virtuele-machineschaalset osProfile toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="0fa0c-242">Elk certificaat dat geïnstalleerd in Hallo cluster moet worden geconfigureerd in Hallo osProfile sectie van Hallo scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="0fa0c-243">Deze actie geïnstrueerd Hallo resource provider tooinstall Hallo certificaat op Hallo van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="0fa0c-244">Deze installatie omvat zowel Hallo cluster certificaat als een toepassing beveiligingscertificaten dat u van plan toouse voor uw toepassingen bent:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="0fa0c-245">Hallo Service Fabric-cluster certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="0fa0c-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="0fa0c-246">certificaat voor clientverificatie Hallo-cluster moet worden geconfigureerd in beide Hallo Service Fabric-cluster-bron (Microsoft.ServiceFabric/clusters) en Hallo Service Fabric-extensie voor de virtuele-machineschaalset stelt in Hallo scale set virtuelemachinebron.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="0fa0c-247">Deze benadering kunt Hallo Service Fabric resource provider tooconfigure voor gebruik voor verificatie van de cluster en serververificatie voor eindpunten voor beheer.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="0fa0c-248">Virtuele-machineschaalset resource:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="0fa0c-249">Service Fabric-resource:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="0fa0c-250">Invoegen van de configuratie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa0c-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="0fa0c-251">Hello Azure AD-configuratie die u eerder hebt gemaakt, kan worden ingevoegd rechtstreeks in het Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="0fa0c-252">Echter, raden wij dat u eerst Hallo waarden voor het uitpakken naar een herbruikbare parameters bestand tookeep Hallo Resource Manager-sjabloon en implementatie van de specifieke tooa waarden.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="0fa0c-253">< een ' configureren-arm"></a>Sjabloonparameters Resource Manager configureren</span><span class="sxs-lookup"><span data-stu-id="0fa0c-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="0fa0c-254">Gebruik tot slot Hallo uitvoerwaarden uit de sleutelkluis Hallo en Azure AD PowerShell-opdrachten toopopulate Hallo-parameterbestand:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="0fa0c-255">Op dit moment hebt u Hallo elementen in plaats te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="0fa0c-256">Sleutelkluis-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="0fa0c-256">Key vault resource group</span></span>
  * <span data-ttu-id="0fa0c-257">Key Vault</span><span class="sxs-lookup"><span data-stu-id="0fa0c-257">Key vault</span></span>
  * <span data-ttu-id="0fa0c-258">Certificaat voor serververificatie cluster</span><span class="sxs-lookup"><span data-stu-id="0fa0c-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="0fa0c-259">Gegevens uitwisselen certificaat</span><span class="sxs-lookup"><span data-stu-id="0fa0c-259">Data encipherment certificate</span></span>
* <span data-ttu-id="0fa0c-260">Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="0fa0c-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="0fa0c-261">Azure AD-toepassing voor het web gebaseerde beheer en de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="0fa0c-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="0fa0c-262">Azure AD-toepassing voor beheer van native client</span><span class="sxs-lookup"><span data-stu-id="0fa0c-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="0fa0c-263">Gebruikers en hun rollen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-263">Users and their assigned roles</span></span>
* <span data-ttu-id="0fa0c-264">Service Fabric-cluster Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0fa0c-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="0fa0c-265">Certificaten die zijn geconfigureerd met behulp van de sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="0fa0c-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="0fa0c-266">Azure Active Directory wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="0fa0c-266">Azure Active Directory configured</span></span>

<span data-ttu-id="0fa0c-267">Hallo volgende diagram ziet u waar uw sleutelkluis en de configuratie van Azure AD in uw Resource Manager-sjabloon inpassen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Afhankelijkheidskaart van Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="0fa0c-269">Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="0fa0c-269">Create hello cluster</span></span>
<span data-ttu-id="0fa0c-270">U bent nu klaar toocreate Hallo cluster met behulp van [Azure-resource sjabloonimplementatie][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="0fa0c-271">Testen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-271">Test it</span></span>
<span data-ttu-id="0fa0c-272">Gebruik Hallo volgende PowerShell-opdracht tootest Resource Manager-sjabloon met een parameterbestand:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="0fa0c-273">Implementeren</span><span class="sxs-lookup"><span data-stu-id="0fa0c-273">Deploy it</span></span>
<span data-ttu-id="0fa0c-274">Als Hallo Resource Manager-sjabloon test is geslaagd, gebruikt u Hallo volgende PowerShell-opdracht toodeploy Resource Manager-sjabloon met een parameterbestand met:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="0fa0c-275">Gebruikers tooroles toewijzen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-275">Assign users tooroles</span></span>
<span data-ttu-id="0fa0c-276">Nadat u Hallo toepassingen toorepresent uw cluster hebt gemaakt, uw gebruikers toewijzen toohello rollen die worden ondersteund door Service Fabric: alleen-lezen en de beheerder. U kunt Hallo rollen toewijzen met behulp van Hallo [klassieke Azure-portal][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="0fa0c-277">Ga in de Azure-portal hello, tooyour tenant en selecteer vervolgens **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="0fa0c-278">Selecteer de webtoepassing hello, heeft een naam zoals `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="0fa0c-279">Klik op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="0fa0c-280">Selecteer een gebruiker tooassign en klik vervolgens op Hallo **toewijzen** knop Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Gebruikers tooroles knop toewijzen][assign-users-to-roles-button]
5. <span data-ttu-id="0fa0c-282">Selecteer Hallo rol tooassign toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-282">Select hello role tooassign toohello user.</span></span>

    ![In het dialoogvenster 'Gebruikers toewijzen'][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="0fa0c-284">Zie voor meer informatie over functies in Service Fabric [toegangsbeheer op basis van rollen voor Service Fabric-clients](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="0fa0c-285">Beveiligde clusters onder Linux maken</span><span class="sxs-lookup"><span data-stu-id="0fa0c-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="0fa0c-286">toomake hello proces eenvoudiger, die we hebt opgegeven een [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="0fa0c-287">Voordat u dit script helper gebruiken, zorg ervoor dat u al Azure-opdrachtregelinterface (CLI) geïnstalleerd en is in het pad.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="0fa0c-288">Zorg ervoor dat Hallo script tooexecute machtigingen door te voeren heeft `chmod +x cert_helper.py` nadat deze is gedownload.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="0fa0c-289">de eerste stap Hallo is toosign in tooyour Azure-account met CLI Hello `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="0fa0c-290">Na het aanmelden tooyour Azure-account, gebruik Hallo helper script met de Certificeringsinstantie certificaat heeft ondertekend, als de volgende opdracht toont Hallo:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="0fa0c-291">Hallo - ifile parameter kan duren voordat een pfx-bestand of een .pem-bestand als invoer met Hallo certificaattype (pfx of pem of ss als het een zelf-ondertekend certificaat).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="0fa0c-292">Hallo parameter -h wordt afgedrukt Hallo help-tekst.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="0fa0c-293">Met deze opdracht retourneert Hallo na drie tekenreeksen als Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="0fa0c-294">SourceVaultID die Hallo-id voor Hallo nieuwe KeyVault ResourceGroup deze voor u gemaakt</span><span class="sxs-lookup"><span data-stu-id="0fa0c-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="0fa0c-295">CertificateUrl voor toegang tot Hallo certificaat</span><span class="sxs-lookup"><span data-stu-id="0fa0c-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="0fa0c-296">CertificateThumbprint die wordt gebruikt voor verificatie</span><span class="sxs-lookup"><span data-stu-id="0fa0c-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="0fa0c-297">Hallo volgende voorbeeld ziet u hoe toouse Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="0fa0c-298">Hallo voorafgaand aan de opdracht geeft u drie tekenreeksen als volgt Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="0fa0c-299">de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="0fa0c-300">Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="0fa0c-301">U kunt een SSL-certificaat kan niet verkrijgen van een Certificeringsinstantie voor Hallo `.cloudapp.azure.com` domein.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="0fa0c-302">U moet een aangepaste domeinnaam voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="0fa0c-303">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="0fa0c-304">Deze onderwerpnamen zijn Hallo vermeldingen moet u toocreate beveiligde Service Fabric-cluster (zonder Azure AD), zoals beschreven op [configureren Resource Manager-Sjabloonparameters](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="0fa0c-305">Beveiligde cluster toohello verbinding kan maken door Hallo instructies voor [verificatie van client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="0fa0c-306">Preview-Linux-clusters bieden geen ondersteuning voor Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="0fa0c-307">U kunt admin en client rollen toewijzen, zoals beschreven in Hallo [toewijzen van rollen toousers](#assign-roles) sectie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="0fa0c-308">Wanneer u de beheerder en client rollen voor een Linux-preview-cluster opgeven, hebt u tooprovide certificaatvingerafdrukken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="0fa0c-309">(U bieden geen onderwerpnaam hello, omdat geen validatie van certificaatketen of certificaatintrekkingslijst wordt uitgevoerd in deze preview-versie.)</span><span class="sxs-lookup"><span data-stu-id="0fa0c-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="0fa0c-310">Als u wilt dat toouse een zelfondertekend certificaat voor het testen, kunt u hetzelfde script toogenerate een Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="0fa0c-311">Vervolgens kunt u Hallo tooyour sleutelkluis-certificaat uploaden door Hallo vlag `ss` in plaats van het pad en de certificaat-naam van certificaat Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="0fa0c-312">Zie bijvoorbeeld Hallo opdracht voor het maken en uploaden van een zelfondertekend certificaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="0fa0c-313">Met deze opdracht retourneert Hallo dezelfde drie tekenreeksen: SourceVault CertificateUrl en CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="0fa0c-314">U kunt vervolgens Hallo tekenreeksen toocreate zowel een beveiligde Linux-cluster en een locatie waar de zelf-ondertekend certificaat Hallo is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="0fa0c-315">U moet Hallo zelf-ondertekend certificaat tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="0fa0c-316">Beveiligde cluster toohello verbinding kan maken door Hallo instructies voor [verificatie van client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="0fa0c-317">de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="0fa0c-318">Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="0fa0c-319">U kunt een SSL-certificaat kan niet verkrijgen van een Certificeringsinstantie voor Hallo `.cloudapp.azure.com` domein.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="0fa0c-320">U moet een aangepaste domeinnaam voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="0fa0c-321">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="0fa0c-322">U kunt ook opgeven Hallo parameters van Hallo helper script in hello Azure-portal, zoals beschreven in Hallo [een cluster maken in Azure-portal Hallo](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sectie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa0c-323">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fa0c-323">Next steps</span></span>
<span data-ttu-id="0fa0c-324">U hebt op dit moment een beveiligde cluster met Azure Active Directory verstrekken management-verificatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="0fa0c-325">Vervolgens [tooyour cluster verbinding](service-fabric-connect-to-secure-cluster.md) en meer informatie over hoe te[toepassing geheimen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="0fa0c-326">Problemen met Azure Active Directory in te stellen voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="0fa0c-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="0fa0c-327">Als u een probleem ondervindt terwijl u Azure AD voor clientverificatie instelt, raadpleegt u Hallo mogelijke oplossingen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="0fa0c-328">Service Fabric Explorer vraagt u een certificaat tooselect</span><span class="sxs-lookup"><span data-stu-id="0fa0c-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="0fa0c-329">Probleem</span><span class="sxs-lookup"><span data-stu-id="0fa0c-329">Problem</span></span>
<span data-ttu-id="0fa0c-330">Nadat u zich aanmeldt met succes tooAzure AD in Service Fabric Explorer, Hallo browser retourneert toohello startpagina, maar wordt gevraagd of u een certificaat tooselect.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Dialoogvenster voor SFX certificaat selecteren][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="0fa0c-332">Reden</span><span class="sxs-lookup"><span data-stu-id="0fa0c-332">Reason</span></span>
<span data-ttu-id="0fa0c-333">Hallo-gebruiker is niet een rol in Azure AD-cluster toepassing hello toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="0fa0c-334">Azure AD-verificatie mislukt dus bij Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="0fa0c-335">Service Fabric Explorer terugvalt toocertificate verificatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="0fa0c-336">Oplossing</span><span class="sxs-lookup"><span data-stu-id="0fa0c-336">Solution</span></span>
<span data-ttu-id="0fa0c-337">Hallo-instructies voor het instellen van Azure AD en gebruikersrollen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="0fa0c-338">Ook wordt aangeraden dat u 'Gebruiker toewijzing vereist tooaccess app' inschakelt als `SetupApplications.ps1` biedt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="0fa0c-339">Verbinding met PowerShell mislukt met een fout: 'hello opgegeven referenties zijn ongeldig'</span><span class="sxs-lookup"><span data-stu-id="0fa0c-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="0fa0c-340">Probleem</span><span class="sxs-lookup"><span data-stu-id="0fa0c-340">Problem</span></span>
<span data-ttu-id="0fa0c-341">Wanneer u PowerShell tooconnect toohello cluster met behulp van 'AzureActiveDirectory' beveiligingsmodus, nadat u zich aanmeldt met succes tooAzure AD, Hallo verbinding is mislukt met een fout: "hello opgegeven referenties zijn ongeldig."</span><span class="sxs-lookup"><span data-stu-id="0fa0c-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="0fa0c-342">Oplossing</span><span class="sxs-lookup"><span data-stu-id="0fa0c-342">Solution</span></span>
<span data-ttu-id="0fa0c-343">Deze oplossing is dezelfde zijn als een voorgaande Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="0fa0c-344">Service Fabric Explorer een fout retourneert wanneer u zich aanmeldt: 'AADSTS50011'</span><span class="sxs-lookup"><span data-stu-id="0fa0c-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="0fa0c-345">Probleem</span><span class="sxs-lookup"><span data-stu-id="0fa0c-345">Problem</span></span>
<span data-ttu-id="0fa0c-346">Wanneer u toosign in tooAzure AD in Service Fabric Explorer, Hallo pagina een fout geretourneerd: ' AADSTS50011: Hallo antwoordadres &lt;url&gt; komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="0fa0c-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![Antwoordadres SFX komt niet overeen met][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="0fa0c-348">Reden</span><span class="sxs-lookup"><span data-stu-id="0fa0c-348">Reason</span></span>
<span data-ttu-id="0fa0c-349">Hallo-cluster (web)-toepassing waarmee de Service Fabric Explorer probeert tooauthenticate met Azure AD en als onderdeel van de aanvraag Hallo biedt Hallo omleiding retour-URL.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="0fa0c-350">Maar Hallo-URL wordt niet vermeld in de toepassing hello Azure AD **antwoord-URL** lijst.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="0fa0c-351">Oplossing</span><span class="sxs-lookup"><span data-stu-id="0fa0c-351">Solution</span></span>
<span data-ttu-id="0fa0c-352">Op Hallo **configureren** tabblad Hallo (webtoepassing)-cluster, het toevoegen van Hallo-URL van de Service Fabric Explorer toohello **antwoord-URL** lijst of een van de items in de lijst Hallo Hallo vervangt.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="0fa0c-353">Wanneer u klaar bent, sla de wijziging.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-353">When you have finished, save your change.</span></span>

![Web application antwoord-url][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="0fa0c-355">Hallo-cluster met behulp van Azure AD-verificatie via PowerShell verbinding</span><span class="sxs-lookup"><span data-stu-id="0fa0c-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="0fa0c-356">tooconnect hello Service Fabric-cluster gebruiken Hallo voorbeeld van de PowerShell-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fa0c-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="0fa0c-357">Zie toolearn over Hallo Connect-ServiceFabricCluster cmdlet [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fa0c-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="0fa0c-358">Kan ik Hallo dezelfde Azure AD-tenant in meerdere clusters gebruiken?</span><span class="sxs-lookup"><span data-stu-id="0fa0c-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="0fa0c-359">Ja.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-359">Yes.</span></span> <span data-ttu-id="0fa0c-360">Maar vergeet niet tooadd Hallo-URL van de Service Fabric Explorer tooyour cluster (web)-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="0fa0c-361">Service Fabric Explorer anders werkt niet.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="0fa0c-362">Waarom moet ik een servercertificaat terwijl Azure AD is ingeschakeld?</span><span class="sxs-lookup"><span data-stu-id="0fa0c-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="0fa0c-363">FabricClient en FabricGateway uitvoeren een wederzijdse verificatie.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="0fa0c-364">Tijdens de verificatie van Azure AD, Azure AD-integratie biedt een client toohello identiteitsserver en is de identiteit van de server Hallo gebruikte tooverify Hallo-servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="0fa0c-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="0fa0c-365">Zie voor meer informatie over Service Fabric-certificaten [X.509-certificaten en Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="0fa0c-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

