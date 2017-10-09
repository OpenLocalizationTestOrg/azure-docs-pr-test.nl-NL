---
title: aaaSecure een Azure Service Fabric-cluster van Windows met behulp van certificaten voor het | Microsoft Docs
description: Dit artikel wordt beschreven hoe toosecure communicatie binnen Hallo zelfstandige of persoonlijke cluster ook tussen clients en het Hallo-cluster.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen
Dit artikel wordt beschreven hoe toosecure Hallo communicatie tussen Hallo verschillende knooppunten van uw zelfstandige Windows-cluster, evenals hoe tooauthenticate clients die verbinding maken toothis cluster x.509-certificaten gebruiken. Dit zorgt ervoor dat alleen gemachtigde gebruikers toegang cluster hello tot hebben, geïmplementeerde toepassingen Hallo en beheertaken uitvoeren.  Certificaatbeveiliging moet worden ingeschakeld op Hallo cluster als Hallo cluster wordt gemaakt.  

Zie voor meer informatie over clusterbeveiliging zoals knooppunt naar beveiliging en beveiliging van de client naar het knooppunt toegangsbeheer op basis van rollen [security scenario's](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Welke certificaten hebt u nodig?
toostart, [Hallo zelfstandige clusterpakket downloaden](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone van Hallo knooppunten in het cluster. In Hallo pakket hebt gedownload, vindt u een **ClusterConfig.X509.MultiMachine.json** bestand. Hallo-bestand openen en het Hallo-sectie van **beveiliging** onder Hallo **eigenschappen** sectie:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

Deze sectie beschrijft Hallo-certificaten die u nodig hebt voor het beveiligen van uw zelfstandige Windows-cluster. Als u een cluster-certificaat opgeeft, stelt u de waarde Hallo van **ClusterCredentialType** too_**X509**_. Als u een servercertificaat voor externe verbindingen opgeeft, stelt u Hallo **ServerCredentialType** te_**X509**_. Hoewel niet verplicht, raden wij aan toohave beide deze certificaten voor een cluster met goed beveiligd. Als u deze waarden te instellen*X509* en vervolgens moet u ook overeenkomstige certificaten Hallo of Service Fabric wordt Veroorzaak een exception opgeven. In sommige gevallen wilt u misschien alleen toospecify hello _ClientCertificateThumbprints_ of _ReverseProxyCertificate_. In deze scenario's, u niet nodig hebt ingesteld _ClusterCredentialType_ of _ServerCredentialType_ too_X509_.


> [!NOTE]
> Een [vingerafdruk](https://en.wikipedia.org/wiki/Public_key_fingerprint) Hallo primaire identiteit van een certificaat is. Lees [hoe tooretrieve vingerafdruk van een certificaat](https://msdn.microsoft.com/library/ms734695.aspx) toofind uit Hallo-vingerafdruk van het Hallo-certificaten die u maakt.
> 
> 

Hallo bevat volgende tabel Hallo-certificaten die u nodig van uw cluster-instellingen hebt:

| **CertificateInformation instelling** | **Beschrijving** |
| --- | --- |
| ClusterCertificate |Aanbevolen voor de testomgeving. Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster. U kunt twee verschillende certificaten, een primaire en een secundaire voor een upgrade. Vingerafdruk van het primaire certificaat Hallo Hallo ingesteld in Hallo **vingerafdruk** sectie en die van de secundaire in Hallo Hallo **ThumbprintSecondary** variabelen. |
| ClusterCertificateCommonNames |Aanbevolen voor productie-omgeving. Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster. U kunt één of twee cluster certificaat algemene namen gebruiken. |
| ServerCertificate |Aanbevolen voor de testomgeving. Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster. Voor het gemak kunt u toouse Hallo hetzelfde certificaat voor *ClusterCertificate* en *ServerCertificate*. U kunt twee verschillende servercertificaten, een primaire en een secundaire voor een upgrade. Vingerafdruk van het primaire certificaat Hallo Hallo ingesteld in Hallo **vingerafdruk** sectie en die van de secundaire in Hallo Hallo **ThumbprintSecondary** variabelen. |
| ServerCertificateCommonNames |Aanbevolen voor productie-omgeving. Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster. Voor het gemak kunt u toouse Hallo hetzelfde certificaat voor *ClusterCertificateCommonNames* en *ServerCertificateCommonNames*. U kunt één of twee algemene servercertificaatnamen gebruiken. |
| ClientCertificateThumbprints |Dit is een set van certificaten die u tooinstall op Hallo geverifieerde clients wilt. U kunt een aantal verschillende clientcertificaten op Hallo-machines dat u wilt dat tooallow toegang toohello cluster geïnstalleerd hebben. Hallo vingerafdruk van elk certificaat ingesteld in Hallo **CertificateThumbprint** variabele. Als u Hallo instelt **IsAdmin** te*true*, en vervolgens Hallo-client met dit certificaat geïnstalleerd op deze beheerder beheeractiviteiten op Hallo-cluster doen kan. Als hello **IsAdmin** is *false*, Hallo-client met dit certificaat kan alleen Hallo toegestane acties voor gebruikerstoegangsrechten doorgaans alleen-lezen uitvoeren. Lees voor meer informatie over functies [op rollen gebaseerde toegangsbeheer (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Set Hallo algemene naam van de eerste clientcertificaat Hallo voor Hallo **CertificateCommonName**. Hallo **CertificateIssuerThumbprint** Hallo vingerafdruk is voor Hallo verlener van dit certificaat. Lees [werken met certificaten](https://msdn.microsoft.com/library/ms731899.aspx) tooknow meer informatie over algemene namen en Hallo verlener. |
| ReverseProxyCertificate |Aanbevolen voor de testomgeving. Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](service-fabric-reverseproxy.md). Zorg ervoor dat reverseProxyEndpointPort is ingesteld in nodeTypes als u dit certificaat. |
| ReverseProxyCertificateCommonNames |Aanbevolen voor productie-omgeving. Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](service-fabric-reverseproxy.md). Zorg ervoor dat reverseProxyEndpointPort is ingesteld in nodeTypes als u dit certificaat. |

Hier volgt clusterconfiguratie voorbeeld waarbij Hallo Cluster Server en Client-certificaten zijn verleend. Houd er rekening mee dat voor cluster / server / reverseProxy certificaten, de vingerafdruk en de algemene naam zijn niet toegestaan toobe geconfigureerd samen voor Hallo dezelfde certificaattype.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Certificaat rollover
Wanneer u de algemene certificaatnaam in plaats van een vingerafdruk, vereist geen certificaat rollover upgraden van cluster configuratie.
Als het certificaat rollover omvat verlener overschakelen, houd de oude verlener cert Hallo Hallo certificaatarchief ten minste 2 uur na de installatie van het nieuwe verlener cert Hallo.

## <a name="acquire-hello-x509-certificates"></a>Hallo X.509-certificaten verkrijgen
toosecure communicatie binnen Hallo-cluster, moet u eerst tooobtain X.509-certificaten voor de clusterknooppunten. Bovendien toolimit verbinding toothis cluster tooauthorized machines/gebruikers, u moet tooobtain en certificaten voor Hallo clientcomputers installeren.

Voor clusters die productie-workloads worden uitgevoerd, moet u een [certificeringsinstantie (CA)](https://en.wikipedia.org/wiki/Certificate_authority) x.509-certificaat toosecure Hallo cluster ondertekend. Voor meer informatie over het verkrijgen van deze certificaten gaat te[procedure: een certificaat verkrijgen](http://msdn.microsoft.com/library/aa702761.aspx).

Voor clusters die u voor testdoeleinden gebruikt, kunt u toouse een zelfondertekend certificaat.

## <a name="optional-create-a-self-signed-certificate"></a>Optioneel: Een zelfondertekend certificaat maken
Eenzijdige toocreate een zelfondertekend certificaat die correct kan worden beveiligd is toouse hello *CertSetup.ps1* script in Hallo Service Fabric SDK-map in de directory Hallo *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Bewerk deze toochange Hallo standaard bestandsnaam van het Hallo-certificaat (Hallo-waarde zoekt *CN = ServiceFabricDevClusterCert*). Voer dit script als `.\CertSetup.ps1 -Install`.

Nu exporteren Hallo tooa PFX-certificaatbestand met een wachtwoord beveiligd. Vingerafdruk van certificaat Hallo Hallo eerst ophalen. Van Hallo *Start* menu uitvoeren Hallo *computercertificaten beheren*. Navigeer toohello **Local Computer\Personal** map en zoeken Hallo certificaat u zojuist hebt gemaakt. Dubbelklik op Hallo certificaat tooopen ervan, selecteer Hallo *Details* tabblad en schuif omlaag toohello *vingerafdruk* veld. Kopieer Hallo vingerafdrukwaarde in Hallo PowerShell-opdracht, na het verwijderen van Hallo spaties.  Wijziging Hallo `String` waarde tooa geschikte beveiligd wachtwoord tooprotect deze en Voer Hallo in PowerShell te volgen:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

toosee hello details van een certificaat geïnstalleerd op Hallo machine u Hallo volgende PowerShell-opdracht kan worden uitgevoerd:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Ook als u een Azure-abonnement hebt, voert u de Hallo sectie [certificaten tooKey kluis toevoegen](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Hallo-certificaten installeren
Zodra u certificaten hebt, kunt u deze installeren op Hallo clusterknooppunten. Uw knooppunten moeten toohave nieuwste Windows PowerShell Hallo 3.x daarop geïnstalleerd. U moet toorepeat deze stappen uit op elk knooppunt voor zowel de Cluster als de Server en alle secundaire certificaten.

1. Hallo pfx-bestanden toohello knooppunt kopiëren.
2. Open een PowerShell-venster als beheerder en Voer Hallo opdrachten te volgen. Vervang Hallo *$pswd* met Hallo wachtwoord dat u toocreate dit certificaat gebruikt. Vervang Hallo *$PfxFilePath* met het volledige pad van de Hallo van Hallo .pfx gekopieerde toothis knooppunt.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Hallo-toegangsbeheer voor dit certificaat nu instellen zodat Hallo Service Fabric-proces, die wordt uitgevoerd onder Hallo account Netwerkservice gebruikt, kan worden gebruikt door het uitvoeren van script volgen Hallo. Geef Hallo vingerafdruk van certificaat Hallo en 'Netwerkservice' voor Hallo-serviceaccount. U kunt controleren dat Hallo ACL's op Hallo certificaat juist zijn door het openen van Hallo-certificaat in *Start* > *computercertificaten beheren* en kijken *alle taken*  >  *Persoonlijke sleutels beheren*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Hallo bovenstaande stappen herhalen voor elk servercertificaat. Ook kunt u deze stappen tooinstall Hallo clientcertificaten op Hallo machines dat u wilt dat tooallow toegang toohello cluster.

## <a name="create-hello-secure-cluster"></a>Hallo beveiligde cluster maken
Na het configureren van Hallo **beveiliging** sectie Hallo **ClusterConfig.X509.MultiMachine.json** -bestand, kunt u doorgaan te[maken van het cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) sectie tooconfigure Hallo knooppunten en Hallo zelfstandige cluster maken. Houd er rekening mee toouse hello **ClusterConfig.X509.MultiMachine.json** bestand tijdens het Hallo-cluster maken. De opdracht kan er bijvoorbeeld Hallo volgende uitzien:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Zodra u beveiligd Hallo hebt zelfstandige Windows cluster waarop wordt uitgevoerd en dat setup Hallo geverifieerde clients tooconnect tooit, voert u de sectie Hallo [Connect tooa beveiligde cluster met behulp van PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Bijvoorbeeld:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Vervolgens kunt u andere toowork PowerShell-opdrachten uitvoeren met dit cluster. Bijvoorbeeld: [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow een lijst met knooppunten op dit beveiligde cluster.


tooremove hello cluster verbinding toohello knooppunt op Hallo cluster waar u Hallo Service Fabric-pakket hebt gedownload, open een opdrachtregel en navigeer toohello pakketmap. Voer nu Hallo volgende opdracht:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Een onjuist certificaat-configuratie kan verhinderen dat Hallo cluster komende tijdens de implementatie. tooself-vaststellen van beveiligingsproblemen met, Zie in groep viewer *logboeken toepassingen en Services* > *Microsoft Service Fabric*.
> 
> 

