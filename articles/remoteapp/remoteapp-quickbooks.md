---
title: aaaDeploy QuickBooks in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooshare QuickBooks met Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="6286b-103">Hoe implementeer u QuickBooks in Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="6286b-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6286b-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="6286b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6286b-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6286b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6286b-106">Hallo informatie tooshare QuickBooks volgen als een app in Azure RemoteApp gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6286b-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="6286b-107">U kunt QuickBooks 2015 Enterprise delen met Azure RemoteApp in verzameling voor een hybride of de cloud.</span><span class="sxs-lookup"><span data-stu-id="6286b-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="6286b-108">Hallo-bedrijfsbestand moet zich bevinden op een virtuele machine met QuickBooks databaseserver die is gescheiden van hello Azure RemoteApp-servers.</span><span class="sxs-lookup"><span data-stu-id="6286b-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="6286b-109">Nooit Hallo bedrijfsbestand opslaat op uw Azure RemoteApp image - gegevens verloren gaan als u dit doet wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="6286b-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="6286b-110">Alleen de QuickBooks Enterprise ondersteunt hosting Hallo QuickBooks bestand op een externe share met QuickBooks databaseserver toegankelijk via de standaard Windows-netwerken.</span><span class="sxs-lookup"><span data-stu-id="6286b-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="6286b-111">Hallo QuickBooks databaseserver die als host voor Hallo bedrijfsbestand fungeert moet zich bevinden op een afzonderlijke virtuele machine binnen Hallo hetzelfde VNET als hello Azure RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="6286b-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="6286b-112">Stappen toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="6286b-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="6286b-113">Maken van een virtuele machine van Azure en QuickBooks, databaseserver QuickBooks, installeren en plaats Hallo bedrijfsbestand op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="6286b-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="6286b-114">Zorg ervoor dat tooproperly firewallregels configureren.</span><span class="sxs-lookup"><span data-stu-id="6286b-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="6286b-115">QuickBooks installeren op een [aangepaste installatiekopie](remoteapp-imageoptions.md) en maak een [Azure RemoteApp-verzameling](remoteapp-collections.md), cloud of hybride binnen Hallo exact hetzelfde VNET waar Hallo VM hosting Hallo QuickBooks database-server met bedrijfsbestanden zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="6286b-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="6286b-116">[Publiceren](remoteapp-publish.md) QuickBooks app toousers</span><span class="sxs-lookup"><span data-stu-id="6286b-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="6286b-117">Hallo QuickBooks gehost Azure RemoteApp-client start, navigeren met behulp van standaard Windows-toohello VM hosting Hallo QuickBooks databaseserver en Hallo bedrijfsbestand opent.</span><span class="sxs-lookup"><span data-stu-id="6286b-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="6286b-118">Documentatie-verwijzingen</span><span class="sxs-lookup"><span data-stu-id="6286b-118">Documentation references</span></span>
* <span data-ttu-id="6286b-119">QuickBooks [ondersteunde configuraties](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="6286b-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="6286b-120">QuickBooks [implementatieopties](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="6286b-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="6286b-121">U kunt ook controleren uit mijn presentatie Ignite [basisprincipes van Microsoft Azure RemoteApp-Management en beheer](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -vooruit too1:02:45 tooget toohello QuickBooks onderdeel.</span><span class="sxs-lookup"><span data-stu-id="6286b-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="6286b-122">Architectuur voor implementatie</span><span class="sxs-lookup"><span data-stu-id="6286b-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp-implementatie](./media/remoteapp-quickbooks/ra-quickbooks.png)

