---
title: Service Fabric-container beveiliging aaaAzure | Microsoft Docs
description: Meer informatie over nu toosecure containerservices.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="ea277-103">Beveiliging van de container</span><span class="sxs-lookup"><span data-stu-id="ea277-103">Container security</span></span>

<span data-ttu-id="ea277-104">Service Fabric biedt een mechanisme voor services binnen een container tooaccess een certificaat dat is geïnstalleerd op het Hallo-knooppunten in een Windows- of Linux-cluster (versie 5.7 of hoger).</span><span class="sxs-lookup"><span data-stu-id="ea277-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="ea277-105">Service Fabric ondersteunt bovendien ook gMSA (groep beheerde serviceaccounts) voor Windows-containers.</span><span class="sxs-lookup"><span data-stu-id="ea277-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="ea277-106">Certificaatbeheer voor containers</span><span class="sxs-lookup"><span data-stu-id="ea277-106">Certificate management for containers</span></span>

<span data-ttu-id="ea277-107">U kunt uw containerservices beveiligen door te geven van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="ea277-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="ea277-108">Hallo-certificaat moet worden geïnstalleerd op Hallo knooppunten van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ea277-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="ea277-109">Hallo certificaatinformatie vindt u in het toepassingsmanifest Hallo onder Hallo `ContainerHostPolicies` label als Hallo volgende codefragment bevat:</span><span class="sxs-lookup"><span data-stu-id="ea277-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="ea277-110">Bij het starten van de toepassing hello wordt Hallo runtime Hallo certificaten leest en genereert een PFX-bestand en het wachtwoord voor elk certificaat.</span><span class="sxs-lookup"><span data-stu-id="ea277-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="ea277-111">Deze PFX-bestand en het wachtwoord zijn toegankelijk binnen Hallo-container met Hallo omgevingsvariabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ea277-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="ea277-112">**Certificate_ [CodePackageName] _ [CertName] _PFX**</span><span class="sxs-lookup"><span data-stu-id="ea277-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="ea277-113">**Certificate_ [CodePackageName] _ [CertName] _Password**</span><span class="sxs-lookup"><span data-stu-id="ea277-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="ea277-114">Hallo containerservice of het proces is verantwoordelijk voor het importeren van Hallo PFX-bestand in container Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea277-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="ea277-115">tooimport hello certificaat, kunt u `setupentrypoint.sh` scripts of aangepaste code binnen Hallo container proces uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ea277-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="ea277-116">Hier volgt de voorbeeldcode in C# voor het importeren van Hallo PFX-bestand:</span><span class="sxs-lookup"><span data-stu-id="ea277-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="ea277-117">Dit PFX-certificaat kan worden gebruikt voor verificatie Hallo toepassing of service of beveiligde commmunication met andere services.</span><span class="sxs-lookup"><span data-stu-id="ea277-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="ea277-118">Instellen van gMSA voor Windows-containers</span><span class="sxs-lookup"><span data-stu-id="ea277-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="ea277-119">tooset van gMSA (groep beheerde serviceaccounts), een referentie specification-bestand (`credspec`) op alle knooppunten in cluster hello wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ea277-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="ea277-120">Hallo-bestand kan worden gekopieerd op alle knooppunten met behulp van een VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="ea277-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="ea277-121">Hallo `credspec` bestand moet Hallo gMSA-accountgegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ea277-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="ea277-122">Voor meer informatie over Hallo `credspec` bestand, Zie [serviceaccounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="ea277-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="ea277-123">Hallo referentie-specificatie en Hallo `Hostname` label in het toepassingsmanifest Hallo zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ea277-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="ea277-124">Hallo `Hostname` label moet overeenkomen met de Hallo gMSA accountnaam op die Hallo onder container wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ea277-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="ea277-125">Hallo `Hostname` tag kan Hallo container tooauthenticate zelf tooother services in Hallo domein Kerberos-verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea277-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="ea277-126">Een voorbeeld voor het opgeven van Hallo `Hostname` en Hallo `credspec` in Hallo toepassingsmanifest wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="ea277-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="ea277-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea277-127">Next steps</span></span>

* [<span data-ttu-id="ea277-128">Een Windows-container tooService Fabric op Windows Server 2016 implementeren</span><span class="sxs-lookup"><span data-stu-id="ea277-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="ea277-129">Implementeert een Docker-container tooService Fabric op Linux</span><span class="sxs-lookup"><span data-stu-id="ea277-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
