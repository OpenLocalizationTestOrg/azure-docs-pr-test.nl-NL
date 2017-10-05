---
title: Het migreren van een RemoteApp VNET een Azure vnet | Microsoft Docs
description: Meer informatie over het migreren van een RemoteApp VNET naar een Azure-VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="e1ff5-103">Een hybride verzameling van een RemoteApp-VNET migreren naar een Azure-VNET</span><span class="sxs-lookup"><span data-stu-id="e1ff5-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1ff5-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e1ff5-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e1ff5-106">Goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="e1ff5-106">Good news!</span></span> <span data-ttu-id="e1ff5-107">We hebben u hybride RemoteApp-verzamelingen rechtstreeks in uw bestaande virtuele Azure-netwerken (vnet's) in plaats van het maken van RemoteApp-specifieke VNETs implementeren ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="e1ff5-108">Hiermee kunt u profiteren van de nieuwste functies van VNET (zoals ExpressRoute) en uw hybride verzamelingen met directe netwerktoegang geven tot andere Azure-services en virtuele machines die aan dit VNET zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="e1ff5-109">(Hiermee haalt u betere prestaties en eenvoudiger instellen dan VNET-naar-VNET-configuraties).</span><span class="sxs-lookup"><span data-stu-id="e1ff5-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="e1ff5-110">Stel dat u hebt al een hybride RemoteApp-collectie aangeroepen gemaakt *OriginalCollection* aangeroepen met een RemoteApp-VNET *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="e1ff5-111">Hier volgen de stappen voor het migreren naar een nieuwe Azure VNET aangeroepen *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="e1ff5-112">Op de **netwerken** tabblad de [beheerportal](http://manage.windowsazure.com/), maak een VNET aangeroepen *AzureVNET*, met behulp van de dezelfde locatie, de DNS-configuratie en -adresruimte (voor ten minste één van de *AzureVNET* subnetten) als u hebt gebruikt voor *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="e1ff5-113">Configureer *AzureVNET* hosten of netwerkverbinding met de Active Directory-implementatie hebt die *OriginalCollection* domein wordt gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="e1ff5-114">Op de **instellen om RemoteApps** tabblad, maakt u een nieuwe RemoteApp-collectie aangeroepen *nieuwe verzameling*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="e1ff5-115">(Gebruik de **maken met VNET** optie niet **snelle invoer**.)</span><span class="sxs-lookup"><span data-stu-id="e1ff5-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="e1ff5-116">Configureer *NewCollection* worden geïmplementeerd voor een subnet in *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="e1ff5-117">Configureer *NewCollection* de dezelfde installatiekopie en de gegevens voor domeindeelname te gebruiken als u hebt gebruikt voor *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="e1ff5-118">Na enkele uren *NewCollection* wordt weergegeven in de verzamelingenlijst met een actieve status heeft.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="e1ff5-119">Nu, als u hoeft niet te migreren van gebruikersgegevens uit de oorspronkelijke verzameling naar de nieuwe verzameling, gaat u als volgt vervolgens:</span><span class="sxs-lookup"><span data-stu-id="e1ff5-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="e1ff5-120">Verwijder *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="e1ff5-121">Verwijder *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="e1ff5-122">En u klaar bent!</span><span class="sxs-lookup"><span data-stu-id="e1ff5-122">And, you’re done!</span></span>

<span data-ttu-id="e1ff5-123">Ook als u migreren van gebruikersgegevens uit de oorspronkelijke verzameling naar de nieuwe verzameling wilt, gaat u als volgt naast:</span><span class="sxs-lookup"><span data-stu-id="e1ff5-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="e1ff5-124">Een e-mail sturen naar [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) met uw Azure-abonnement-ID, de naam van uw oorspronkelijke verzameling en de naam van de nieuwe verzameling en vraag om uw gebruikersgegevens te migreren.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="e1ff5-125">Binnen 2 dagen verplaatst de RemoteApp-team de lijst met gebruikers toegang tot alle gebruikersdocumenten en gebruikersinstellingen uit de oorspronkelijke verzameling naar de nieuwe verzameling.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="e1ff5-126">Verwijder *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="e1ff5-127">Verwijder *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e1ff5-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="e1ff5-128">En u bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="e1ff5-128">And now, you’re done!</span></span>

<span data-ttu-id="e1ff5-129">Als u vragen hebt of speciale hulp nodig hebt, kunt u een e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="e1ff5-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

