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
# <a name="connect-tooa-secure-cluster"></a>Verbinding maken met de beveiligde cluster tooa

Wanneer een client verbinding tooa Service Fabric-clusterknooppunt maakt, kan de client Hallo geverifieerde en beveiligde communicatie tot stand gebracht via certificaat beveiligings- of Azure Active Directory (AAD) zijn. Deze verificatie zorgt ervoor dat alleen geautoriseerde gebruikers Hallo cluster kunnen openen en toepassingen geïmplementeerde en beheertaken uitvoeren.  Certificaat of AAD-beveiliging moet zijn eerder ingeschakeld op Hallo cluster als Hallo-cluster is gemaakt.  Zie voor meer informatie over scenario's voor Toepassingsbeveiliging cluster [beveiliging Cluster](service-fabric-cluster-security.md). Als u verbinding tooa cluster beveiligd met certificaten maakt, [Hallo clientcertificaat instellen](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) op Hallo-computer die verbinding toohello cluster maakt. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Verbinding maken met veilige tooa-cluster met behulp van Azure Service Fabric CLI (sfctl)

Er zijn een aantal verschillende manieren tooconnect tooa beveiligde cluster met behulp van Hallo Service Fabric CLI (sfctl). Wanneer u een certificaat voor verificatie, geïmplementeerd Hallo certificaat details moeten overeenkomen met een certificaat toohello clusterknooppunten. Als uw certificaat heeft certificeringsinstanties (CA's), moet u tooadditionally opgeven Hallo vertrouwde CA's.

U kunt verbinding maken met Hallo tooa-cluster `sfctl cluster select` opdracht.

Clientcertificaten kunnen worden opgegeven in twee verschillende manieren, als een certificaat en het sleutelpaar, of als een enkel pem-bestand. Voor een wachtwoord beveiligd `pem` bestanden, kunt u zich automatisch tooenter Hallo wachtwoord gevraagd.

toospecify hello clientcertificaat als een pem-bestand Hallo-bestandspad opgeven in Hallo `--pem` argument. Bijvoorbeeld:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Pem-bestanden beveiligd met een wachtwoord gevraagd wachtwoord voorafgaande toorunning elke opdracht.

een certificaat toospecify, sleutelpaar gebruiken Hallo `--cert` en `--key` toospecify Hallo paden tooeach respectieve bestand met argumenten.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Soms certificaten toosecure test gebruikt of clusters dev certificaat validatie is mislukt. toobypass certificaatverificatie Hallo opgeven `--no-verify` optie. Bijvoorbeeld:

> [!WARNING]
> Gebruik geen Hallo `no-verify` optie bij het verbinden van tooproduction Service Fabric-clusters.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

U kunt bovendien toodirectories van vertrouwde CA-certificaten of certificaten voor afzonderlijke paden opgeven. toospecify deze paden gebruiken Hallo `--ca` argument. Bijvoorbeeld:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Nadat u verbinding maakt, moet u kunnen te[uitvoeren van andere opdrachten sfctl](service-fabric-cli.md) toointeract met Hallo-cluster.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Verbinding maken met behulp van PowerShell tooa-cluster
Voordat u bewerkingen op een cluster via PowerShell uitvoeren, moet u eerst een verbinding toohello cluster maken. Hallo cluster verbinding wordt gebruikt voor alle volgende opdrachten in Hallo opgegeven PowerShell-sessie.

### <a name="connect-tooan-unsecure-cluster"></a>Verbinding maken met niet-beveiligde cluster tooan

tooconnect tooan onbeveiligde cluster, bieden Hallo cluster eindpunt adres toohello **Connect-ServiceFabricCluster** opdracht:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Verbinding maken met de beveiligde cluster tooa met Azure Active Directory

tooconnect tooa beveiligde cluster dat gebruik maakt van Azure Active Directory tooauthorize cluster beheerderstoegang Hallo cluster certificaatvingerafdruk biedt en gebruiken van Hallo *AzureActiveDirectory* vlag.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat
Voer Hallo volgende PowerShell-opdracht tooconnect tooa beveiligde cluster maakt gebruik van certificaten tooauthorize beheerder clienttoegang. Geef Hallo cluster certificaatvingerafdruk en Hallo-vingerafdruk van het Hallo-clientcertificaat dat voor Clusterbeheer machtigingen heeft. details van Hallo certificaat moeten overeenkomen met een certificaat op de clusterknooppunten Hallo.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* Hallo vingerafdruk van het Hallo-servercertificaat is geïnstalleerd op de clusterknooppunten Hallo. *FindValue* Hallo vingerafdruk van Hallo beheerder clientcertificaat.
Hallo-parameters zijn ingevuld, ziet er Hallo opdracht Hallo voorbeeld te volgen: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Verbinding maken met veilige tooa-cluster met Windows Active Directory
Als uw zelfstandige cluster wordt geïmplementeerd met behulp van AD-beveiligingsgroep, sluit u toohello cluster door Hallo switch 'WindowsCredential' toe te voegen.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Verbinding maken met behulp van Hallo FabricClient APIs tooa-cluster
Hallo Service Fabric SDK bevat Hallo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) klasse voor Clusterbeheer. toouse hello FabricClient APIs's ophalen Hallo Microsoft.ServiceFabric NuGet-pakket.

### <a name="connect-tooan-unsecure-cluster"></a>Verbinding maken met niet-beveiligde cluster tooan

tooconnect tooa externe onbeveiligde-cluster, maak een exemplaar FabricClient en Hallo clusteradres bieden:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Voor de code die wordt uitgevoerd binnen een cluster, bijvoorbeeld in een betrouwbare Service maakt een FabricClient *zonder* Hallo clusteradres opgeven. FabricClient verbindt toohello lokale gateway op Hallo knooppunt Hallo code op wordt uitgevoerd, waardoor een extra netwerk-hop voorkomen.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat

Hallo-knooppunten in cluster Hallo moeten geldige certificaten waarvan de algemene naam of DNS-naam in de SAN wordt weergegeven in Hallo [RemoteCommonNames eigenschap](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ingesteld op [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Dit proces, schakelt u wederzijdse verificatie tussen Hallo-client en Hallo clusterknooppunten.

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Verbinding maken met de beveiligde cluster tooa interactief met Azure Active Directory

Hallo volgende voorbeeld maakt gebruik van Azure Active Directory voor identiteits- en clientcertificaat voor de identiteit van server.

Dialoogvenster verschijnt een venster automatisch voor interactieve aanmelding wanneer verbinding wordt gemaakt toohello cluster.

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Verbinding maken met de beveiligde cluster tooa niet-interactief met Azure Active Directory

Hallo volgende voorbeeld is afhankelijk van Microsoft.IdentityModel.Clients.ActiveDirectory, versie: 2.19.208020213.

Zie voor meer informatie over AAD-token verkrijgen [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Verbinding maken met de beveiligde cluster tooa zonder voorafgaande metagegevens kennis met Azure Active Directory

Hallo volgende voorbeeld maakt gebruik van niet-interactieve token verkrijgen kan, maar hello dezelfde manier gebruikte toobuild een aangepaste interactieve token overname-ervaring. Hello Azure Active Directory-metagegevens die nodig zijn voor de aanschaf van token worden gelezen uit de configuratie van het cluster.

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Verbinding maken met veilige tooa-cluster met behulp van Service Fabric Explorer
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) voor een bepaald cluster, wijst u uw browser:

`http://<your-cluster-endpoint>:19080/Explorer`

Hallo volledige URL is ook beschikbaar in Hallo cluster essentials deelvenster Hallo Azure-portal.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Verbinding maken met de beveiligde cluster tooa met Azure Active Directory

tooconnect tooa cluster dat is beveiligd met AAD, wijst u uw browser:

`https://<your-cluster-endpoint>:19080/Explorer`

U bent automatisch na vragen aan gebruiker toolog met AAD zijn.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Verbinding maken met veilige tooa-cluster met behulp van een clientcertificaat

tooconnect tooa cluster dat is beveiligd met certificaten, wijst u uw browser:

`https://<your-cluster-endpoint>:19080/Explorer`

U wordt automatisch na vragen aan gebruiker tooselect een clientcertificaat zijn.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Een certificaat op de externe computer Hallo instellen
Ten minste twee certificaten moeten worden gebruikt voor het beveiligen van Hallo-cluster, één voor het cluster en beheerserver certificaat Hallo en één voor clienttoegang.  U wordt aangeraden ook aanvullende secundaire certificaten en client access certificaten te gebruiken.  toosecure hello communicatie tussen een client en een cluster met behulp van het certificaat beveiliging kunt u eerst tooobtain moet en Hallo clientcertificaat installeren. Hallo-certificaat kan worden geïnstalleerd in Hallo persoonlijke (Mijn) archief van de lokale computer Hallo of Hallo-huidige gebruiker.  U moet ook Hallo vingerafdruk van het servercertificaat Hallo zodat hello client kan worden geverifieerd Hallo-cluster.

Hallo volgende PowerShell-cmdlet tooset up Hallo clientcertificaat op Hallo computer van waaruit u toegang Hallo cluster tot worden uitgevoerd.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Als het een zelfondertekend certificaat, moet u deze van de machine tooyour 'vertrouwde personen"opslaan voordat u kunt dit certificaat tooconnect tooa beveiligde cluster tooimport.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Volgende stappen

* [Het upgradeproces service Fabric-Cluster en de verwachtingen van u](service-fabric-cluster-upgrade.md)
* [Het beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Status van de Fabric-service model Inleiding](service-fabric-health-introduction.md)
* [Toepassingsbeveiliging en RunAs](service-fabric-application-runas-security.md)
* [Aan de slag met de Service Fabric-CLI](service-fabric-cli.md)
