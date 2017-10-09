---
title: aaaSecure een cluster met Windows met behulp van Windows-beveiliging | Microsoft Docs
description: Meer informatie over hoe tooconfigure knooppunt naar clientknooppunt beveiliging en op een zelfstandige cluster dat wordt uitgevoerd in Windows met behulp van Windows-beveiliging.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="9d92d-103">Een zelfstandige cluster op Windows beveiligen met behulp van Windows-beveiliging</span><span class="sxs-lookup"><span data-stu-id="9d92d-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="9d92d-104">tooprevent onbevoegde toegang tooa Service Fabric-cluster, moet u Hallo-cluster beveiligen.</span><span class="sxs-lookup"><span data-stu-id="9d92d-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="9d92d-105">Beveiliging is vooral belangrijk bij Hallo cluster productieworkloads wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d92d-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="9d92d-106">Dit artikel wordt beschreven hoe tooconfigure knooppunt naar beveiliging en op client-naar-knooppunt met behulp van Windows-beveiliging in Hallo *ClusterConfig.JSON* bestand.</span><span class="sxs-lookup"><span data-stu-id="9d92d-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="9d92d-107">Hallo proces toohello overeenkomt met configureren van beveiligingsstap van [maken van een zelfstandige cluster waarop Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9d92d-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="9d92d-108">Zie voor meer informatie over hoe Service Fabric Windows-beveiliging gebruikt [security scenario's](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="9d92d-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9d92d-109">U moet zorgvuldig Hallo selectie van knooppunt naar beveiliging omdat er geen cluster-upgrade van één beveiliging keuze tooanother.</span><span class="sxs-lookup"><span data-stu-id="9d92d-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="9d92d-110">toochange Hallo beveiliging selectie, hebt u volledige toorebuild Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d92d-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="9d92d-111">Windows-beveiliging met behulp van gMSA configureren</span><span class="sxs-lookup"><span data-stu-id="9d92d-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="9d92d-112">Hallo voorbeeld *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuratiebestand is gedownload met Hallo [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) zelfstandige clusterpakket bevat een sjabloon voor het configureren van Windows-beveiliging gebruikt [groep beheerde serviceaccounts (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="9d92d-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="9d92d-113">**Configuratie-instelling**</span><span class="sxs-lookup"><span data-stu-id="9d92d-113">**Configuration Setting**</span></span> | <span data-ttu-id="9d92d-114">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="9d92d-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="9d92d-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="9d92d-115">WindowsIdentities</span></span> |<span data-ttu-id="9d92d-116">Hallo-cluster en de client identiteiten bevat.</span><span class="sxs-lookup"><span data-stu-id="9d92d-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="9d92d-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="9d92d-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="9d92d-118">Hiermee configureert u een knooppunt naar beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9d92d-118">Configures node-to-node security.</span></span> <span data-ttu-id="9d92d-119">Een groep beheerd serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="9d92d-119">A group managed service account.</span></span> |  
| <span data-ttu-id="9d92d-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="9d92d-120">ClusterSPN</span></span> |<span data-ttu-id="9d92d-121">FQDN-SPN voor de gMSA-account</span><span class="sxs-lookup"><span data-stu-id="9d92d-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="9d92d-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="9d92d-122">ClientIdentities</span></span> |<span data-ttu-id="9d92d-123">Hiermee configureert u clientknooppunt beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9d92d-123">Configures client-to-node security.</span></span> <span data-ttu-id="9d92d-124">Een matrix van gebruikersaccounts van de client.</span><span class="sxs-lookup"><span data-stu-id="9d92d-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="9d92d-125">Identiteit</span><span class="sxs-lookup"><span data-stu-id="9d92d-125">Identity</span></span> |<span data-ttu-id="9d92d-126">Hallo identiteit van de client, een domeingebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d92d-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="9d92d-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="9d92d-127">IsAdmin</span></span> |<span data-ttu-id="9d92d-128">Waar geeft dat die Hallo domein de gebruiker heeft beheerderstoegang client, false voor clienttoegang van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d92d-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="9d92d-129">[Knooppunt toonode beveiliging](service-fabric-cluster-security.md#node-to-node-security) is geconfigureerd door in te stellen **ClustergMSAIdentity** wanneer het service fabric moet toorun onder gMSA.</span><span class="sxs-lookup"><span data-stu-id="9d92d-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="9d92d-130">In de volgorde toobuild vertrouwensrelaties tussen knooppunten, moeten ze worden aangebracht op de hoogte van elkaar.</span><span class="sxs-lookup"><span data-stu-id="9d92d-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="9d92d-131">Dit op twee verschillende manieren kunt worden bereikt: Hallo groep beheerd serviceaccount gebruiken met alle knooppunten in cluster Hallo opgeven, of Hallo machine domeingroep die alle knooppunten in het Hallo-cluster omvat.</span><span class="sxs-lookup"><span data-stu-id="9d92d-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="9d92d-132">Ten zeerste aangeraden Hallo [groep beheerde serviceaccounts (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) benadering, met name voor grotere clusters (meer dan 10 knooppunten) of voor clusters die zijn waarschijnlijk toogrow of te verkleinen.</span><span class="sxs-lookup"><span data-stu-id="9d92d-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="9d92d-133">Deze aanpak is niet vereist voor Hallo maken van een domeingroep waarvoor clusterbeheerders toegang rechten tooadd hebben gekregen en verwijder leden.</span><span class="sxs-lookup"><span data-stu-id="9d92d-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="9d92d-134">Deze accounts zijn ook nuttig voor het automatisch wachtwoordbeheer.</span><span class="sxs-lookup"><span data-stu-id="9d92d-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="9d92d-135">Zie voor meer informatie [aan de slag met beheerde serviceaccounts voor groepen](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d92d-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="9d92d-136">[De clientbeveiligingssessie toonode](service-fabric-cluster-security.md#client-to-node-security) is geconfigureerd met **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="9d92d-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="9d92d-137">In de volgorde tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow configureren welke client-id's die kunnen worden vertrouwd.</span><span class="sxs-lookup"><span data-stu-id="9d92d-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="9d92d-138">Dit kan op twee verschillende manieren worden gedaan: Geef Hallo groep Domeingebruikers die kunnen verbinding maken of geef Hallo knooppunt domeingebruikers die verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="9d92d-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="9d92d-139">Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d92d-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="9d92d-140">Toegangsbeheer biedt Hallo mogelijkheid voor Hallo beheerder toolimit toegang toocertain clustertypen van bewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="9d92d-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="9d92d-141">Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden).</span><span class="sxs-lookup"><span data-stu-id="9d92d-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="9d92d-142">Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="9d92d-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="9d92d-143">Zie voor meer informatie over toegangsbeheer [toegangsbeheer voor Service Fabric-clients op basis van rollen](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9d92d-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="9d92d-144">Hallo volgende voorbeeld **beveiliging** sectie configureert u Windows-beveiliging met behulp van gMSA en geeft aan dat Hallo machines in *ServiceFabric.clusterA.contoso.com* gMSA maken deel uit van het Hallo-cluster en die *CONTOSO\usera* admin clienttoegang heeft:</span><span class="sxs-lookup"><span data-stu-id="9d92d-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="9d92d-145">Windows-beveiliging met behulp van een machine-beheergroep configureren</span><span class="sxs-lookup"><span data-stu-id="9d92d-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="9d92d-146">Hallo voorbeeld *ClusterConfig.Windows.MultiMachine.JSON* configuratiebestand is gedownload met Hallo [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) zelfstandige clusterpakket bevat een sjabloon voor het configureren van Windows-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9d92d-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="9d92d-147">Windows-beveiliging is geconfigureerd in Hallo **eigenschappen** sectie:</span><span class="sxs-lookup"><span data-stu-id="9d92d-147">Windows security is configured in hello **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="9d92d-148">**Configuratie-instelling**</span><span class="sxs-lookup"><span data-stu-id="9d92d-148">**Configuration setting**</span></span> | <span data-ttu-id="9d92d-149">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="9d92d-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9d92d-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="9d92d-150">ClusterCredentialType</span></span> |<span data-ttu-id="9d92d-151">**ClusterCredentialType** te is ingesteld,*Windows* als ClusterIdentity is opgegeven voor een Active Directory-groep computernaam.</span><span class="sxs-lookup"><span data-stu-id="9d92d-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="9d92d-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="9d92d-152">ServerCredentialType</span></span> |<span data-ttu-id="9d92d-153">Stel te*Windows* tooenable Windows-beveiliging voor clients.</span><span class="sxs-lookup"><span data-stu-id="9d92d-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="9d92d-154">Dit betekent dat clients Hallo van Hallo en Hallo cluster zichzelf worden uitgevoerd binnen een Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="9d92d-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="9d92d-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="9d92d-155">WindowsIdentities</span></span> |<span data-ttu-id="9d92d-156">Hallo-cluster en de client identiteiten bevat.</span><span class="sxs-lookup"><span data-stu-id="9d92d-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="9d92d-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="9d92d-157">ClusterIdentity</span></span> |<span data-ttu-id="9d92d-158">Gebruik een machine groepsnaam, domain\machinegroup, tooconfigure knooppunt naar beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9d92d-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="9d92d-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="9d92d-159">ClientIdentities</span></span> |<span data-ttu-id="9d92d-160">Hiermee configureert u clientknooppunt beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9d92d-160">Configures client-to-node security.</span></span> <span data-ttu-id="9d92d-161">Een matrix van gebruikersaccounts van de client.</span><span class="sxs-lookup"><span data-stu-id="9d92d-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="9d92d-162">Identiteit</span><span class="sxs-lookup"><span data-stu-id="9d92d-162">Identity</span></span> |<span data-ttu-id="9d92d-163">Hallo domeingebruiker, domein\gebruikersnaam voor de identiteit van de client Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9d92d-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="9d92d-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="9d92d-164">IsAdmin</span></span> |<span data-ttu-id="9d92d-165">Set tootrue toospecify die Hallo domeingebruiker heeft clienttoegang als beheerder of ONWAAR voor clienttoegang van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d92d-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="9d92d-166">[Knooppunt toonode beveiliging](service-fabric-cluster-security.md#node-to-node-security) is geconfigureerd met behulp van instelling **ClusterIdentity** als u wilt dat toouse een Machinegroep binnen een Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="9d92d-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="9d92d-167">Zie voor meer informatie [maken van een Machine-groep in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="9d92d-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="9d92d-168">[Beveiliging van de client naar het knooppunt](service-fabric-cluster-security.md#client-to-node-security) is geconfigureerd met behulp van **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="9d92d-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="9d92d-169">tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow Hallo client, identiteiten die Hallo cluster vertrouwen kunnen configureren.</span><span class="sxs-lookup"><span data-stu-id="9d92d-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="9d92d-170">U kunt een vertrouwensrelatie in twee verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="9d92d-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="9d92d-171">Geef Hallo groep Domeingebruikers die verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="9d92d-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="9d92d-172">Geef Hallo knooppunt domeingebruikers die verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="9d92d-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="9d92d-173">Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d92d-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="9d92d-174">Toegangsbeheer kan Hallo beheerder toolimit toegang toocertain clustertypen van clusterbewerkingen voor verschillende groepen gebruikers, waardoor Hallo cluster beter te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="9d92d-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="9d92d-175">Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden).</span><span class="sxs-lookup"><span data-stu-id="9d92d-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="9d92d-176">Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="9d92d-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="9d92d-177">Hallo volgende voorbeeld **beveiliging** sectie Windows-beveiliging configureert, geeft aan dat Hallo machines in *ServiceFabric/clusterA.contoso.com* deel uitmaken van Hallo-cluster en geeft aan dat  *CONTOSO\usera* admin clienttoegang heeft:</span><span class="sxs-lookup"><span data-stu-id="9d92d-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="9d92d-178">Service Fabric moeten niet worden geïmplementeerd op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="9d92d-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="9d92d-179">Zorg ervoor dat ClusterConfig.json niet Hallo IP-adres van de domeincontroller Hallo opnemen wanneer u een Machinegroep of groep beheerde serviceaccounts (gMSA).</span><span class="sxs-lookup"><span data-stu-id="9d92d-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9d92d-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d92d-180">Next steps</span></span>
<span data-ttu-id="9d92d-181">Na het configureren van Windows-beveiliging in Hallo *ClusterConfig.JSON* bestand, hervat Hallo cluster maakproces in [maken van een zelfstandige cluster waarop Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9d92d-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="9d92d-182">Voor meer informatie over hoe naar knooppunten beveiliging, client-naar-node beveiliging en op rollen gebaseerde toegangsbeheer, Zie [security scenario's](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="9d92d-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="9d92d-183">Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor voorbeelden van verbinding maken met behulp van PowerShell of FabricClient.</span><span class="sxs-lookup"><span data-stu-id="9d92d-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
