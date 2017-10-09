---
title: Quick Start aaaAzure-Cloud-Shell (Preview) | Microsoft Docs
description: Quick Start voor hello Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="a3ad3-103">Quick Start voor het gebruik van hello Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a3ad3-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="a3ad3-104">Dit document beschrijft hoe toouse Azure Cloud Shell in Hallo Hallo [Azure-portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="a3ad3-105">Cloud-Shell starten</span><span class="sxs-lookup"><span data-stu-id="a3ad3-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="a3ad3-106">Start **Cloud Shell** van de bovenste navigatiebalk Hallo Hallo Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a3ad3-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="a3ad3-107">Selecteer een abonnement toocreate een opslagaccount en een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="a3ad3-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="a3ad3-108">Selecteer 'Opslag maken'</span><span class="sxs-lookup"><span data-stu-id="a3ad3-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="a3ad3-109">U bent automatisch geverifieerd voor Azure CLI 2.0 in elke sesssion.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="a3ad3-110">Stel uw abonnement</span><span class="sxs-lookup"><span data-stu-id="a3ad3-110">Set your subscription</span></span>
1. <span data-ttu-id="a3ad3-111">Lijst met abonnementen u toegang tot hebt:</span><span class="sxs-lookup"><span data-stu-id="a3ad3-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="a3ad3-112">Stel uw voorkeur abonnement:</span><span class="sxs-lookup"><span data-stu-id="a3ad3-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="a3ad3-113">Uw abonnement worden opgeslagen voor toekomstige sessies met behulp van `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="a3ad3-114">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a3ad3-114">Create a resource group</span></span>
<span data-ttu-id="a3ad3-115">Maak een nieuwe resourcegroep in WestUS met de naam 'MyRG':</span><span class="sxs-lookup"><span data-stu-id="a3ad3-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="a3ad3-116">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="a3ad3-116">Create a Linux VM</span></span>
<span data-ttu-id="a3ad3-117">Maak een VM Ubuntu in uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="a3ad3-118">Hello Azure CLI 2.0 maakt SSH-sleutels en setup Hallo VM mee.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="a3ad3-119">Hallo tooauthenticate van openbare en persoonlijke sleutels die worden gebruikt in uw virtuele machine worden geplaatst `/User/.ssh/id_rsa` en `/User/.ssh/id_rsa.pub` door Azure CLI 2.0 standaard.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="a3ad3-120">De SSH-map wordt bewaard in de gekoppelde Azure-bestandsshare van 5 GB installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="a3ad3-121">Uw gebruikersnaam op deze virtuele machine worden uw gebruikersnaam die wordt gebruikt in de Cloud-Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="a3ad3-122">SSH in uw virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="a3ad3-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="a3ad3-123">Zoeken naar de naam van uw VM in Hallo zoekbalk met Azure portal</span><span class="sxs-lookup"><span data-stu-id="a3ad3-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="a3ad3-124">Klik op "Connect" en voer:`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="a3ad3-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="a3ad3-125">Bij het tot stand brengen van SSH-verbinding hello, ziet u Hallo Ubuntu Welkom prompt.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="a3ad3-126">Opschonen</span><span class="sxs-lookup"><span data-stu-id="a3ad3-126">Cleaning up</span></span> 
<span data-ttu-id="a3ad3-127">De resourcegroep en alle resources binnen deze verwijderen:</span><span class="sxs-lookup"><span data-stu-id="a3ad3-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="a3ad3-128">Voer `az group delete -n MyRG` uit.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3ad3-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3ad3-129">Next Steps</span></span>
[<span data-ttu-id="a3ad3-130">Meer informatie over persistent maken van de opslag op Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="a3ad3-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="a3ad3-131">
[Meer informatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="a3ad3-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="a3ad3-132">
[Meer informatie over Azure File storage](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a3ad3-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>