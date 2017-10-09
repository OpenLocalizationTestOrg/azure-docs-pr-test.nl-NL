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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="5ecc4-103">Een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen</span><span class="sxs-lookup"><span data-stu-id="5ecc4-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="5ecc4-104">Dit artikel wordt beschreven hoe toosecure Hallo communicatie tussen Hallo verschillende knooppunten van uw zelfstandige Windows-cluster, evenals hoe tooauthenticate clients die verbinding maken toothis cluster x.509-certificaten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="5ecc4-105">Dit zorgt ervoor dat alleen gemachtigde gebruikers toegang cluster hello tot hebben, geïmplementeerde toepassingen Hallo en beheertaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="5ecc4-106">Certificaatbeveiliging moet worden ingeschakeld op Hallo cluster als Hallo cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="5ecc4-107">Zie voor meer informatie over clusterbeveiliging zoals knooppunt naar beveiliging en beveiliging van de client naar het knooppunt toegangsbeheer op basis van rollen [security scenario's](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="5ecc4-108">Welke certificaten hebt u nodig?</span><span class="sxs-lookup"><span data-stu-id="5ecc4-108">Which certificates will you need?</span></span>
<span data-ttu-id="5ecc4-109">toostart, [Hallo zelfstandige clusterpakket downloaden](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone van Hallo knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="5ecc4-110">In Hallo pakket hebt gedownload, vindt u een **ClusterConfig.X509.MultiMachine.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="5ecc4-111">Hallo-bestand openen en het Hallo-sectie van **beveiliging** onder Hallo **eigenschappen** sectie:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

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

<span data-ttu-id="5ecc4-112">Deze sectie beschrijft Hallo-certificaten die u nodig hebt voor het beveiligen van uw zelfstandige Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="5ecc4-113">Als u een cluster-certificaat opgeeft, stelt u de waarde Hallo van **ClusterCredentialType** too_**X509**_. Als u een servercertificaat voor externe verbindingen opgeeft, stelt u Hallo **ServerCredentialType** te_**X509**_. Hoewel niet verplicht, raden wij aan toohave beide deze certificaten voor een cluster met goed beveiligd. Als u deze waarden te instellen*X509* en vervolgens moet u ook overeenkomstige certificaten Hallo of Service Fabric wordt Veroorzaak een exception opgeven. In sommige gevallen wilt u misschien alleen toospecify hello _ClientCertificateThumbprints_ of _ReverseProxyCertificate_. In deze scenario's, u niet nodig hebt ingesteld _ClusterCredentialType_ of _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="5ecc4-114">Een [vingerafdruk](https://en.wikipedia.org/wiki/Public_key_fingerprint) Hallo primaire identiteit van een certificaat is.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="5ecc4-115">Lees [hoe tooretrieve vingerafdruk van een certificaat](https://msdn.microsoft.com/library/ms734695.aspx) toofind uit Hallo-vingerafdruk van het Hallo-certificaten die u maakt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="5ecc4-116">Hallo bevat volgende tabel Hallo-certificaten die u nodig van uw cluster-instellingen hebt:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="5ecc4-117">**CertificateInformation instelling**</span><span class="sxs-lookup"><span data-stu-id="5ecc4-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="5ecc4-118">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="5ecc4-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5ecc4-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="5ecc4-119">ClusterCertificate</span></span> |<span data-ttu-id="5ecc4-120">Aanbevolen voor de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-120">Recommended for test environment.</span></span> <span data-ttu-id="5ecc4-121">Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="5ecc4-122">U kunt twee verschillende certificaten, een primaire en een secundaire voor een upgrade.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="5ecc4-123">Vingerafdruk van het primaire certificaat Hallo Hallo ingesteld in Hallo **vingerafdruk** sectie en die van de secundaire in Hallo Hallo **ThumbprintSecondary** variabelen.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="5ecc4-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5ecc4-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="5ecc4-125">Aanbevolen voor productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-125">Recommended for production environment.</span></span> <span data-ttu-id="5ecc4-126">Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="5ecc4-127">U kunt één of twee cluster certificaat algemene namen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="5ecc4-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="5ecc4-128">ServerCertificate</span></span> |<span data-ttu-id="5ecc4-129">Aanbevolen voor de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-129">Recommended for test environment.</span></span> <span data-ttu-id="5ecc4-130">Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="5ecc4-131">Voor het gemak kunt u toouse Hallo hetzelfde certificaat voor *ClusterCertificate* en *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="5ecc4-132">U kunt twee verschillende servercertificaten, een primaire en een secundaire voor een upgrade.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="5ecc4-133">Vingerafdruk van het primaire certificaat Hallo Hallo ingesteld in Hallo **vingerafdruk** sectie en die van de secundaire in Hallo Hallo **ThumbprintSecondary** variabelen.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="5ecc4-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5ecc4-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="5ecc4-135">Aanbevolen voor productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-135">Recommended for production environment.</span></span> <span data-ttu-id="5ecc4-136">Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="5ecc4-137">Voor het gemak kunt u toouse Hallo hetzelfde certificaat voor *ClusterCertificateCommonNames* en *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="5ecc4-138">U kunt één of twee algemene servercertificaatnamen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="5ecc4-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="5ecc4-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="5ecc4-140">Dit is een set van certificaten die u tooinstall op Hallo geverifieerde clients wilt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="5ecc4-141">U kunt een aantal verschillende clientcertificaten op Hallo-machines dat u wilt dat tooallow toegang toohello cluster geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="5ecc4-142">Hallo vingerafdruk van elk certificaat ingesteld in Hallo **CertificateThumbprint** variabele.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="5ecc4-143">Als u Hallo instelt **IsAdmin** te*true*, en vervolgens Hallo-client met dit certificaat geïnstalleerd op deze beheerder beheeractiviteiten op Hallo-cluster doen kan.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="5ecc4-144">Als hello **IsAdmin** is *false*, Hallo-client met dit certificaat kan alleen Hallo toegestane acties voor gebruikerstoegangsrechten doorgaans alleen-lezen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="5ecc4-145">Lees voor meer informatie over functies [op rollen gebaseerde toegangsbeheer (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="5ecc4-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="5ecc4-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5ecc4-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="5ecc4-147">Set Hallo algemene naam van de eerste clientcertificaat Hallo voor Hallo **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="5ecc4-148">Hallo **CertificateIssuerThumbprint** Hallo vingerafdruk is voor Hallo verlener van dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="5ecc4-149">Lees [werken met certificaten](https://msdn.microsoft.com/library/ms731899.aspx) tooknow meer informatie over algemene namen en Hallo verlener.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="5ecc4-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="5ecc4-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="5ecc4-151">Aanbevolen voor de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-151">Recommended for test environment.</span></span> <span data-ttu-id="5ecc4-152">Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="5ecc4-153">Zorg ervoor dat reverseProxyEndpointPort is ingesteld in nodeTypes als u dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="5ecc4-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5ecc4-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="5ecc4-155">Aanbevolen voor productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-155">Recommended for production environment.</span></span> <span data-ttu-id="5ecc4-156">Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="5ecc4-157">Zorg ervoor dat reverseProxyEndpointPort is ingesteld in nodeTypes als u dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="5ecc4-158">Hier volgt clusterconfiguratie voorbeeld waarbij Hallo Cluster Server en Client-certificaten zijn verleend.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="5ecc4-159">Houd er rekening mee dat voor cluster / server / reverseProxy certificaten, de vingerafdruk en de algemene naam zijn niet toegestaan toobe geconfigureerd samen voor Hallo dezelfde certificaattype.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

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

## <a name="certificate-roll-over"></a><span data-ttu-id="5ecc4-160">Certificaat rollover</span><span class="sxs-lookup"><span data-stu-id="5ecc4-160">Certificate roll over</span></span>
<span data-ttu-id="5ecc4-161">Wanneer u de algemene certificaatnaam in plaats van een vingerafdruk, vereist geen certificaat rollover upgraden van cluster configuratie.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="5ecc4-162">Als het certificaat rollover omvat verlener overschakelen, houd de oude verlener cert Hallo Hallo certificaatarchief ten minste 2 uur na de installatie van het nieuwe verlener cert Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="5ecc4-163">Hallo X.509-certificaten verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5ecc4-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="5ecc4-164">toosecure communicatie binnen Hallo-cluster, moet u eerst tooobtain X.509-certificaten voor de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="5ecc4-165">Bovendien toolimit verbinding toothis cluster tooauthorized machines/gebruikers, u moet tooobtain en certificaten voor Hallo clientcomputers installeren.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="5ecc4-166">Voor clusters die productie-workloads worden uitgevoerd, moet u een [certificeringsinstantie (CA)](https://en.wikipedia.org/wiki/Certificate_authority) x.509-certificaat toosecure Hallo cluster ondertekend.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="5ecc4-167">Voor meer informatie over het verkrijgen van deze certificaten gaat te[procedure: een certificaat verkrijgen](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="5ecc4-168">Voor clusters die u voor testdoeleinden gebruikt, kunt u toouse een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="5ecc4-169">Optioneel: Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="5ecc4-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="5ecc4-170">Eenzijdige toocreate een zelfondertekend certificaat die correct kan worden beveiligd is toouse hello *CertSetup.ps1* script in Hallo Service Fabric SDK-map in de directory Hallo *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="5ecc4-171">Bewerk deze toochange Hallo standaard bestandsnaam van het Hallo-certificaat (Hallo-waarde zoekt *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="5ecc4-172">Voer dit script als `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="5ecc4-173">Nu exporteren Hallo tooa PFX-certificaatbestand met een wachtwoord beveiligd.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="5ecc4-174">Vingerafdruk van certificaat Hallo Hallo eerst ophalen.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="5ecc4-175">Van Hallo *Start* menu uitvoeren Hallo *computercertificaten beheren*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="5ecc4-176">Navigeer toohello **Local Computer\Personal** map en zoeken Hallo certificaat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="5ecc4-177">Dubbelklik op Hallo certificaat tooopen ervan, selecteer Hallo *Details* tabblad en schuif omlaag toohello *vingerafdruk* veld.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="5ecc4-178">Kopieer Hallo vingerafdrukwaarde in Hallo PowerShell-opdracht, na het verwijderen van Hallo spaties.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="5ecc4-179">Wijziging Hallo `String` waarde tooa geschikte beveiligd wachtwoord tooprotect deze en Voer Hallo in PowerShell te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="5ecc4-180">toosee hello details van een certificaat geïnstalleerd op Hallo machine u Hallo volgende PowerShell-opdracht kan worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="5ecc4-181">Ook als u een Azure-abonnement hebt, voert u de Hallo sectie [certificaten tooKey kluis toevoegen](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="5ecc4-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="5ecc4-182">Hallo-certificaten installeren</span><span class="sxs-lookup"><span data-stu-id="5ecc4-182">Install hello certificates</span></span>
<span data-ttu-id="5ecc4-183">Zodra u certificaten hebt, kunt u deze installeren op Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="5ecc4-184">Uw knooppunten moeten toohave nieuwste Windows PowerShell Hallo 3.x daarop geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="5ecc4-185">U moet toorepeat deze stappen uit op elk knooppunt voor zowel de Cluster als de Server en alle secundaire certificaten.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="5ecc4-186">Hallo pfx-bestanden toohello knooppunt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="5ecc4-187">Open een PowerShell-venster als beheerder en Voer Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="5ecc4-188">Vervang Hallo *$pswd* met Hallo wachtwoord dat u toocreate dit certificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="5ecc4-189">Vervang Hallo *$PfxFilePath* met het volledige pad van de Hallo van Hallo .pfx gekopieerde toothis knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="5ecc4-190">Hallo-toegangsbeheer voor dit certificaat nu instellen zodat Hallo Service Fabric-proces, die wordt uitgevoerd onder Hallo account Netwerkservice gebruikt, kan worden gebruikt door het uitvoeren van script volgen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="5ecc4-191">Geef Hallo vingerafdruk van certificaat Hallo en 'Netwerkservice' voor Hallo-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="5ecc4-192">U kunt controleren dat Hallo ACL's op Hallo certificaat juist zijn door het openen van Hallo-certificaat in *Start* > *computercertificaten beheren* en kijken *alle taken*  >  *Persoonlijke sleutels beheren*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
4. <span data-ttu-id="5ecc4-193">Hallo bovenstaande stappen herhalen voor elk servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="5ecc4-194">Ook kunt u deze stappen tooinstall Hallo clientcertificaten op Hallo machines dat u wilt dat tooallow toegang toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="5ecc4-195">Hallo beveiligde cluster maken</span><span class="sxs-lookup"><span data-stu-id="5ecc4-195">Create hello secure cluster</span></span>
<span data-ttu-id="5ecc4-196">Na het configureren van Hallo **beveiliging** sectie Hallo **ClusterConfig.X509.MultiMachine.json** -bestand, kunt u doorgaan te[maken van het cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) sectie tooconfigure Hallo knooppunten en Hallo zelfstandige cluster maken.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="5ecc4-197">Houd er rekening mee toouse hello **ClusterConfig.X509.MultiMachine.json** bestand tijdens het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="5ecc4-198">De opdracht kan er bijvoorbeeld Hallo volgende uitzien:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="5ecc4-199">Zodra u beveiligd Hallo hebt zelfstandige Windows cluster waarop wordt uitgevoerd en dat setup Hallo geverifieerde clients tooconnect tooit, voert u de sectie Hallo [Connect tooa beveiligde cluster met behulp van PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="5ecc4-200">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="5ecc4-201">Vervolgens kunt u andere toowork PowerShell-opdrachten uitvoeren met dit cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="5ecc4-202">Bijvoorbeeld: [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow een lijst met knooppunten op dit beveiligde cluster.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="5ecc4-203">tooremove hello cluster verbinding toohello knooppunt op Hallo cluster waar u Hallo Service Fabric-pakket hebt gedownload, open een opdrachtregel en navigeer toohello pakketmap.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="5ecc4-204">Voer nu Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5ecc4-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="5ecc4-205">Een onjuist certificaat-configuratie kan verhinderen dat Hallo cluster komende tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="5ecc4-206">tooself-vaststellen van beveiligingsproblemen met, Zie in groep viewer *logboeken toepassingen en Services* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="5ecc4-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

