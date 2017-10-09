---
title: aaaCreate persoonlijke Docker-register - Azure-portal | Microsoft Docs
description: Maken en beheren van persoonlijke Docker-container registers Hello Azure-portal aan de slag
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="ddd00-103">Maken van een persoonlijke Docker-container register met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ddd00-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="ddd00-104">Hello Azure portal toocreate een register container gebruiken en de instellingen beheren.</span><span class="sxs-lookup"><span data-stu-id="ddd00-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="ddd00-105">U kunt ook maken en beheren van container registers met Hallo [2.0 voor Azure CLI-opdrachten](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="ddd00-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="ddd00-106">Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ddd00-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ddd00-107">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="ddd00-107">Create a container registry</span></span>
1. <span data-ttu-id="ddd00-108">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="ddd00-109">Zoeken Hallo marketplace voor **Azure container register**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="ddd00-110">Selecteer **Azure Container Registry** met als uitgever **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="ddd00-111">![Container Registry-service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="ddd00-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="ddd00-112">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-112">Click **Create**.</span></span> <span data-ttu-id="ddd00-113">Hallo **Azure Container register** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ddd00-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="ddd00-115">In Hallo **Azure Container register** blade Hallo volgende informatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="ddd00-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="ddd00-116">Klik op **Maken** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="ddd00-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="ddd00-117">a.</span><span class="sxs-lookup"><span data-stu-id="ddd00-117">a.</span></span> <span data-ttu-id="ddd00-118">**Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register.</span><span class="sxs-lookup"><span data-stu-id="ddd00-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="ddd00-119">In dit voorbeeld is de naam van Hallo register *myRegistry01*, maar vervangen door een unieke naam van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ddd00-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="ddd00-120">Hallo-naam mag alleen letters en cijfers zijn.</span><span class="sxs-lookup"><span data-stu-id="ddd00-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="ddd00-121">b.</span><span class="sxs-lookup"><span data-stu-id="ddd00-121">b.</span></span> <span data-ttu-id="ddd00-122">**Resourcegroep**: Selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ddd00-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="ddd00-123">c.</span><span class="sxs-lookup"><span data-stu-id="ddd00-123">c.</span></span> <span data-ttu-id="ddd00-124">**Locatie**: Selecteer een Azure-datacenter locatie van Hallo service [beschikbaar](https://azure.microsoft.com/regions/services/), zoals **Zuid-centraal VS**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="ddd00-125">d.</span><span class="sxs-lookup"><span data-stu-id="ddd00-125">d.</span></span> <span data-ttu-id="ddd00-126">**Gebruiker met beheerdersrechten**: als u wilt, schakelt u het register voor een beheerder de gebruiker tooaccess Hallo.</span><span class="sxs-lookup"><span data-stu-id="ddd00-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="ddd00-127">U kunt deze instelling na het maken van Hallo register kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ddd00-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ddd00-128">Bovendien tooproviding via een beheerdersaccount voor de gebruiker toegang krijgen tot, container registers ondersteund door de service-principals Azure Active Directory-verificatie ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="ddd00-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="ddd00-129">Bekijk voor meer informatie [Verifiëren met het containerregister](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ddd00-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="ddd00-130">e.</span><span class="sxs-lookup"><span data-stu-id="ddd00-130">e.</span></span> <span data-ttu-id="ddd00-131">**Storage-account**: Hallo standaard instelling toocreate gebruiken een [opslagaccount](../storage/common/storage-introduction.md), of Selecteer een bestaand opslagaccount in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="ddd00-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="ddd00-132">Premium-opslag wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ddd00-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="ddd00-133">Registerinstellingen beheren</span><span class="sxs-lookup"><span data-stu-id="ddd00-133">Manage registry settings</span></span>
<span data-ttu-id="ddd00-134">Na het maken van Hallo register Hallo zoeken registerinstellingen door op te starten op Hallo **Container registers** blade in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ddd00-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="ddd00-135">Bijvoorbeeld, moet u mogelijk Hallo instellingen toolog in tooyour register of wilt u tooenable of Hallo beheerder gebruiker uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ddd00-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="ddd00-136">Op Hallo **Container registers** blade, klikt u op Hallo-naam van het register.</span><span class="sxs-lookup"><span data-stu-id="ddd00-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Blade Container Registry](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="ddd00-138">Toegangsinstellingen toomanage, klikt u op **toegangssleutel**.</span><span class="sxs-lookup"><span data-stu-id="ddd00-138">toomanage access settings, click **Access key**.</span></span>

    ![Toegang tot Container Registry](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="ddd00-140">Houd er rekening mee Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="ddd00-140">Note hello following settings:</span></span>

   * <span data-ttu-id="ddd00-141">**Aanmeldingsserver** -Hallo volledig gekwalificeerde naam u toolog in register toohello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ddd00-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="ddd00-142">In dit voorbeeld is het `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="ddd00-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="ddd00-143">**Gebruiker met beheerdersrechten** - in-of uitschakelen tooenable of van het register Hallo beheerder gebruikersaccount uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ddd00-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="ddd00-144">**Gebruikersnaam** en **wachtwoord** -referenties van Hallo beheerder gebruikersaccount Hallo (indien ingeschakeld) kunt u toolog in toohello register.</span><span class="sxs-lookup"><span data-stu-id="ddd00-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="ddd00-145">U kunt eventueel Hallo wachtwoorden opnieuw te genereren.</span><span class="sxs-lookup"><span data-stu-id="ddd00-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="ddd00-146">Twee wachtwoorden worden gemaakt, zodat u verbindingen toohello register onderhouden kunt met behulp van een wachtwoord tijdens het genereren van Hallo andere wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ddd00-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="ddd00-147">tooauthenticate met een service-principal in plaats daarvan Zie [verifiëren met een persoonlijke Docker-container register](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ddd00-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd00-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ddd00-148">Next steps</span></span>
* [<span data-ttu-id="ddd00-149">Uw eerste installatiekopie met behulp van Docker CLI Hallo push</span><span class="sxs-lookup"><span data-stu-id="ddd00-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
