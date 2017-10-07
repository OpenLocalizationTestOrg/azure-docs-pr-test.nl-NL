---
title: aaaAuthenticate met een Azure container registry | Microsoft Docs
description: Hoe toolog in tooan Azure container register met een Azure Active Directory service-principal of een beheerdersaccount te gebruiken
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="5e2b5-103">Verificatie met een persoonlijke Docker-container register</span><span class="sxs-lookup"><span data-stu-id="5e2b5-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="5e2b5-104">toowork met afbeeldingen in het register van een Azure container container u zich aanmelden met behulp van Hallo `docker login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="5e2b5-105">U kunt aanmelden met behulp van een  **[Azure Active Directory-service-principal](../active-directory/active-directory-application-objects.md)**  of een register-specifieke **beheerdersaccount**.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="5e2b5-106">Dit artikel vindt meer informatie over deze identiteiten.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="5e2b5-107">Service-principal</span><span class="sxs-lookup"><span data-stu-id="5e2b5-107">Service principal</span></span>

<span data-ttu-id="5e2b5-108">U kunt [toewijzen van een service-principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour register en deze gebruiken voor eenvoudige Docker-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="5e2b5-109">Met behulp van een service-principal wordt aanbevolen voor de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="5e2b5-110">Hallo app-ID en wachtwoord van Hallo service principal toohello `docker login` opdracht, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5e2b5-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="5e2b5-111">Nadat u bent aangemeld, Docker in de cache opgeslagen referenties hello, dus u hoeft tooremember Hallo app-ID.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="5e2b5-112">Als u wilt, kunt u Hallo-wachtwoord van een service-principal opnieuw genereren door het uitvoeren van Hallo `az ad sp reset-credentials` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="5e2b5-113">Service-principals toestaan [toegangsgroepen op basis van](../active-directory/role-based-access-control-configure.md) tooa register.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="5e2b5-114">Beschikbare rollen zijn:</span><span class="sxs-lookup"><span data-stu-id="5e2b5-114">Available roles are:</span></span>
  * <span data-ttu-id="5e2b5-115">Lezer (alleen pull-toegang).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="5e2b5-116">Inzender (pull-abonnementen en push).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="5e2b5-117">Eigenaar (pull-, push- en toewijzen rollen tooother gebruikers).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="5e2b5-118">Anonieme toegang is niet beschikbaar op Azure Container registers.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="5e2b5-119">U kunt gebruiken voor openbare afbeeldingen [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="5e2b5-120">U kunt meerdere service-principals tooa register, waarmee u toegang tot toodefine voor verschillende gebruikers of toepassingen kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="5e2b5-121">Service-principals ook inschakelen 'headless' connectiviteit tooa register in ontwikkelaar of DevOps-scenario's zoals Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="5e2b5-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="5e2b5-122">Containerimplementaties van een register tooorchestration systemen zoals DC/OS, Docker Swarm en Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="5e2b5-123">U kunt ook pull-container registers toorelated Azure-services zoals [Containerservice](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), en andere.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="5e2b5-124">Continue integratie en implementatie-oplossingen (zoals Visual Studio Team Services of Jenkins) die container images maken en toepassen tooa register.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="5e2b5-125">Beheerdersaccount</span><span class="sxs-lookup"><span data-stu-id="5e2b5-125">Admin account</span></span>
<span data-ttu-id="5e2b5-126">Een beheerdersaccount opgehaald met elke register die u maakt, automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="5e2b5-127">Hallo-account is standaard uitgeschakeld, maar u kunt deze inschakelen en Hallo referenties beheren, bijvoorbeeld via Hallo [portal](container-registry-get-started-portal.md#manage-registry-settings) of met behulp van Hallo [Azure CLI 2.0 opdrachten](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="5e2b5-128">Elke beheerdersaccount wordt geleverd met twee wachtwoorden, die beide kunnen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="5e2b5-129">Hallo twee wachtwoorden kunnen u toomaintain verbindingen toohello register met een wachtwoord tijdens het genereren van Hallo andere wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="5e2b5-130">Als het Hallo-account is ingeschakeld, kunt u doorgeven Hallo-gebruikersnaam en een wachtwoord toohello `docker login` opdracht voor basisverificatie toohello register.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="5e2b5-131">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5e2b5-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="5e2b5-132">Hallo-beheerdersaccount is ontworpen voor een register één gebruiker tooaccess hello, hoofdzakelijk voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="5e2b5-133">Het is niet raadzaam tooshare Hallo beheerder accountreferenties met andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="5e2b5-134">Alle gebruikers worden weergegeven als een enkele gebruiker toohello-register.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="5e2b5-135">Hiermee schakelt u toegang tot het register voor alle gebruikers die gebruikmaken van Hallo referenties wijzigen of dit account uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="5e2b5-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="5e2b5-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e2b5-136">Next steps</span></span>
* <span data-ttu-id="5e2b5-137">[Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="5e2b5-138">Zie voor meer informatie over verificatie in voorbeeld van het register van de Container Hallo Hallo [blogbericht](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="5e2b5-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
