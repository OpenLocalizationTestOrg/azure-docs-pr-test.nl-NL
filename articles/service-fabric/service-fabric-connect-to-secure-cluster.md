---
title: aaaConnect veilig tooan Azure Service Fabric-cluster | Microsoft Docs
description: Hierin wordt beschreven hoe tooauthenticate-client toegang heeft tot de Service Fabric-cluster tooa en hoe toosecure communicatie tussen clients en een cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="48f90-103">Verbinding maken met de beveiligde cluster tooa</span><span class="sxs-lookup"><span data-stu-id="48f90-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="48f90-104">Wanneer een client verbinding tooa Service Fabric-clusterknooppunt maakt, kan de client Hallo geverifieerde en beveiligde communicatie tot stand gebracht via certificaat beveiligings- of Azure Active Directory (AAD) zijn.</span><span class="sxs-lookup"><span data-stu-id="48f90-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="48f90-105">Deze verificatie zorgt ervoor dat alleen geautoriseerde gebruikers Hallo cluster kunnen openen en toepassingen geïmplementeerde en beheertaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="48f90-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="48f90-106">Certificaat of AAD-beveiliging moet zijn eerder ingeschakeld op Hallo cluster als Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="48f90-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="48f90-107">Zie voor meer informatie over scenario's voor Toepassingsbeveiliging cluster [beveiliging Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="48f90-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="48f90-108">Als u verbinding tooa cluster beveiligd met certificaten maakt, [Hallo clientcertificaat instellen](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) op Hallo-computer die verbinding toohello cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="48f90-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="48f90-109">Verbinding maken met veilige tooa-cluster met behulp van Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="48f90-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="48f90-110">Er zijn een aantal verschillende manieren tooconnect tooa beveiligde cluster met behulp van Hallo Service Fabric CLI (sfctl).</span><span class="sxs-lookup"><span data-stu-id="48f90-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="48f90-111">Wanneer u een certificaat voor verificatie, geïmplementeerd Hallo certificaat details moeten overeenkomen met een certificaat toohello clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="48f90-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="48f90-112">Als uw certificaat heeft certificeringsinstanties (CA's), moet u tooadditionally opgeven Hallo vertrouwde CA's.</span><span class="sxs-lookup"><span data-stu-id="48f90-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="48f90-113">U kunt verbinding maken met Hallo tooa-cluster `sfctl cluster select` opdracht.</span><span class="sxs-lookup"><span data-stu-id="48f90-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="48f90-114">Clientcertificaten kunnen worden opgegeven in twee verschillende manieren, als een certificaat en het sleutelpaar, of als een enkel pem-bestand.</span><span class="sxs-lookup"><span data-stu-id="48f90-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="48f90-115">Voor een wachtwoord beveiligd `pem` bestanden, kunt u zich automatisch tooenter Hallo wachtwoord gevraagd.</span><span class="sxs-lookup"><span data-stu-id="48f90-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="48f90-116">toospecify hello clientcertificaat als een pem-bestand Hallo-bestandspad opgeven in Hallo `--pem` argument.</span><span class="sxs-lookup"><span data-stu-id="48f90-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="48f90-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="48f90-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="48f90-118">Pem-bestanden beveiligd met een wachtwoord gevraagd wachtwoord voorafgaande toorunning elke opdracht.</span><span class="sxs-lookup"><span data-stu-id="48f90-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="48f90-119">een certificaat toospecify, sleutelpaar gebruiken Hallo `--cert` en `--key` toospecify Hallo paden tooeach respectieve bestand met argumenten.</span><span class="sxs-lookup"><span data-stu-id="48f90-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="48f90-120">Soms certificaten toosecure test gebruikt of clusters dev certificaat validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="48f90-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="48f90-121">toobypass certificaatverificatie Hallo opgeven `--no-verify` optie.</span><span class="sxs-lookup"><span data-stu-id="48f90-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="48f90-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="48f90-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="48f90-123">Gebruik geen Hallo `no-verify` optie bij het verbinden van tooproduction Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="48f90-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="48f90-124">U kunt bovendien toodirectories van vertrouwde CA-certificaten of certificaten voor afzonderlijke paden opgeven.</span><span class="sxs-lookup"><span data-stu-id="48f90-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="48f90-125">toospecify deze paden gebruiken Hallo `--ca` argument.</span><span class="sxs-lookup"><span data-stu-id="48f90-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="48f90-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="48f90-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="48f90-127">Nadat u verbinding maakt, moet u kunnen te[uitvoeren van andere opdrachten sfctl](service-fabric-cli.md) toointeract met Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="48f90-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="48f90-128">Verbinding maken met behulp van PowerShell tooa-cluster</span><span class="sxs-lookup"><span data-stu-id="48f90-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="48f90-129">Voordat u bewerkingen op een cluster via PowerShell uitvoeren, moet u eerst een verbinding toohello cluster maken.</span><span class="sxs-lookup"><span data-stu-id="48f90-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="48f90-130">Hallo cluster verbinding wordt gebruikt voor alle volgende opdrachten in Hallo opgegeven PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="48f90-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="48f90-131">Verbinding maken met niet-beveiligde cluster tooan</span><span class="sxs-lookup"><span data-stu-id="48f90-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="48f90-132">tooconnect tooan onbeveiligde cluster, bieden Hallo cluster eindpunt adres toohello **Connect-ServiceFabricCluster** opdracht:</span><span class="sxs-lookup"><span data-stu-id="48f90-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="48f90-133">Verbinding maken met de beveiligde cluster tooa met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="48f90-134">tooconnect tooa beveiligde cluster dat gebruik maakt van Azure Active Directory tooauthorize cluster beheerderstoegang Hallo cluster certificaatvingerafdruk biedt en gebruiken van Hallo *AzureActiveDirectory* vlag.</span><span class="sxs-lookup"><span data-stu-id="48f90-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="48f90-135">Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="48f90-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="48f90-136">Voer Hallo volgende PowerShell-opdracht tooconnect tooa beveiligde cluster maakt gebruik van certificaten tooauthorize beheerder clienttoegang.</span><span class="sxs-lookup"><span data-stu-id="48f90-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="48f90-137">Geef Hallo cluster certificaatvingerafdruk en Hallo-vingerafdruk van het Hallo-clientcertificaat dat voor Clusterbeheer machtigingen heeft.</span><span class="sxs-lookup"><span data-stu-id="48f90-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="48f90-138">details van Hallo certificaat moeten overeenkomen met een certificaat op de clusterknooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="48f90-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="48f90-139">*ServerCertThumbprint* Hallo vingerafdruk van het Hallo-servercertificaat is geïnstalleerd op de clusterknooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="48f90-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="48f90-140">*FindValue* Hallo vingerafdruk van Hallo beheerder clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="48f90-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="48f90-141">Hallo-parameters zijn ingevuld, ziet er Hallo opdracht Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="48f90-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="48f90-142">Verbinding maken met veilige tooa-cluster met Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="48f90-143">Als uw zelfstandige cluster wordt geïmplementeerd met behulp van AD-beveiligingsgroep, sluit u toohello cluster door Hallo switch 'WindowsCredential' toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="48f90-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="48f90-144">Verbinding maken met behulp van Hallo FabricClient APIs tooa-cluster</span><span class="sxs-lookup"><span data-stu-id="48f90-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="48f90-145">Hallo Service Fabric SDK bevat Hallo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) klasse voor Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="48f90-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="48f90-146">toouse hello FabricClient APIs's ophalen Hallo Microsoft.ServiceFabric NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="48f90-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="48f90-147">Verbinding maken met niet-beveiligde cluster tooan</span><span class="sxs-lookup"><span data-stu-id="48f90-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="48f90-148">tooconnect tooa externe onbeveiligde-cluster, maak een exemplaar FabricClient en Hallo clusteradres bieden:</span><span class="sxs-lookup"><span data-stu-id="48f90-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="48f90-149">Voor de code die wordt uitgevoerd binnen een cluster, bijvoorbeeld in een betrouwbare Service maakt een FabricClient *zonder* Hallo clusteradres opgeven.</span><span class="sxs-lookup"><span data-stu-id="48f90-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="48f90-150">FabricClient verbindt toohello lokale gateway op Hallo knooppunt Hallo code op wordt uitgevoerd, waardoor een extra netwerk-hop voorkomen.</span><span class="sxs-lookup"><span data-stu-id="48f90-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="48f90-151">Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="48f90-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="48f90-152">Hallo-knooppunten in cluster Hallo moeten geldige certificaten waarvan de algemene naam of DNS-naam in de SAN wordt weergegeven in Hallo [RemoteCommonNames eigenschap](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ingesteld op [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="48f90-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="48f90-153">Dit proces, schakelt u wederzijdse verificatie tussen Hallo-client en Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="48f90-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="48f90-154">Verbinding maken met de beveiligde cluster tooa interactief met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="48f90-155">Hallo volgende voorbeeld maakt gebruik van Azure Active Directory voor identiteits- en clientcertificaat voor de identiteit van server.</span><span class="sxs-lookup"><span data-stu-id="48f90-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="48f90-156">Dialoogvenster verschijnt een venster automatisch voor interactieve aanmelding wanneer verbinding wordt gemaakt toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="48f90-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="48f90-157">Verbinding maken met de beveiligde cluster tooa niet-interactief met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="48f90-158">Hallo volgende voorbeeld is afhankelijk van Microsoft.IdentityModel.Clients.ActiveDirectory, versie: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="48f90-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="48f90-159">Zie voor meer informatie over AAD-token verkrijgen [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="48f90-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="48f90-160">Verbinding maken met de beveiligde cluster tooa zonder voorafgaande metagegevens kennis met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="48f90-161">Hallo volgende voorbeeld maakt gebruik van niet-interactieve token verkrijgen kan, maar hello dezelfde manier gebruikte toobuild een aangepaste interactieve token overname-ervaring.</span><span class="sxs-lookup"><span data-stu-id="48f90-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="48f90-162">Hello Azure Active Directory-metagegevens die nodig zijn voor de aanschaf van token worden gelezen uit de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="48f90-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="48f90-163">Verbinding maken met veilige tooa-cluster met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="48f90-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="48f90-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) voor een bepaald cluster, wijst u uw browser:</span><span class="sxs-lookup"><span data-stu-id="48f90-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="48f90-165">Hallo volledige URL is ook beschikbaar in Hallo cluster essentials deelvenster Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="48f90-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="48f90-166">Verbinding maken met de beveiligde cluster tooa met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48f90-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="48f90-167">tooconnect tooa cluster dat is beveiligd met AAD, wijst u uw browser:</span><span class="sxs-lookup"><span data-stu-id="48f90-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="48f90-168">U bent automatisch na vragen aan gebruiker toolog met AAD zijn.</span><span class="sxs-lookup"><span data-stu-id="48f90-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="48f90-169">Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="48f90-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="48f90-170">tooconnect tooa cluster dat is beveiligd met certificaten, wijst u uw browser:</span><span class="sxs-lookup"><span data-stu-id="48f90-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="48f90-171">U wordt automatisch na vragen aan gebruiker tooselect een clientcertificaat zijn.</span><span class="sxs-lookup"><span data-stu-id="48f90-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="48f90-172">Een certificaat op de externe computer Hallo instellen</span><span class="sxs-lookup"><span data-stu-id="48f90-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="48f90-173">Ten minste twee certificaten moeten worden gebruikt voor het beveiligen van Hallo-cluster, één voor het cluster en beheerserver certificaat Hallo en één voor clienttoegang.</span><span class="sxs-lookup"><span data-stu-id="48f90-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="48f90-174">U wordt aangeraden ook aanvullende secundaire certificaten en client access certificaten te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48f90-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="48f90-175">toosecure hello communicatie tussen een client en een cluster met behulp van het certificaat beveiliging kunt u eerst tooobtain moet en Hallo clientcertificaat installeren.</span><span class="sxs-lookup"><span data-stu-id="48f90-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="48f90-176">Hallo-certificaat kan worden geïnstalleerd in Hallo persoonlijke (Mijn) archief van de lokale computer Hallo of Hallo-huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48f90-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="48f90-177">U moet ook Hallo vingerafdruk van het servercertificaat Hallo zodat hello client kan worden geverifieerd Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="48f90-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="48f90-178">Hallo volgende PowerShell-cmdlet tooset up Hallo clientcertificaat op Hallo computer van waaruit u toegang Hallo cluster tot worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="48f90-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="48f90-179">Als het een zelfondertekend certificaat, moet u deze van de machine tooyour 'vertrouwde personen"opslaan voordat u kunt dit certificaat tooconnect tooa beveiligde cluster tooimport.</span><span class="sxs-lookup"><span data-stu-id="48f90-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="48f90-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48f90-180">Next steps</span></span>

* [<span data-ttu-id="48f90-181">Het upgradeproces service Fabric-Cluster en de verwachtingen van u</span><span class="sxs-lookup"><span data-stu-id="48f90-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="48f90-182">Het beheren van uw Service Fabric-toepassingen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48f90-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="48f90-183">Status van de Fabric-service model Inleiding</span><span class="sxs-lookup"><span data-stu-id="48f90-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="48f90-184">Toepassingsbeveiliging en RunAs</span><span class="sxs-lookup"><span data-stu-id="48f90-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="48f90-185">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="48f90-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
