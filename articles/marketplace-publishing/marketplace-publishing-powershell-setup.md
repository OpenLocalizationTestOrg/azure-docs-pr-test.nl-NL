---
title: aaaSet up PowerShell toocreate een VM voor Hallo Marketplace | Microsoft Docs
description: "Instructies voor het instellen van Azure PowerShell en gebruiken als een optioneel proces toocreate VM-installatiekopieën toodeploy, stroom en verkopen op, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="5198a-103">Azure PowerShell toocreate instellen met een aanbieding voor hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5198a-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="5198a-104">Voor gedetailleerde informatie over het tooset van PowerShell in Azure, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5198a-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5198a-105">Een eenvoudige benadering is toouse Hallo certificaat methode, gedownload en importeert een certificaat nodig voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5198a-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="5198a-106">Hallo tooobtain nodig van het certificaat, gebruikt u Hallo **Get-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5198a-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="5198a-107">Hallo-bestand opslaan wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="5198a-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="5198a-108">tooimport hello certificaat in een PowerShell-sessie gebruik Hallo **importeren AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5198a-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="5198a-109">tooconfigure en store Hallo algemene Microsoft Azure-abonnement-instellingen voor Hallo PowerShell-sessie gebruiken Hallo **Set-AzureSubscription** en **Select-AzureSubscription** cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5198a-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="5198a-110">de eerste opdracht Hallo koppelt een standaardopslagaccount aan Hallo-abonnement (nodig voor bepaalde bewerkingen van VM-inrichting).</span><span class="sxs-lookup"><span data-stu-id="5198a-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="5198a-111">Hallo maakt tweede Hallo abonnement Hallo huidige abonnement (herkend door andere cmdlets).</span><span class="sxs-lookup"><span data-stu-id="5198a-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="5198a-112">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5198a-112">See also</span></span>
* [<span data-ttu-id="5198a-113">Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5198a-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="5198a-114">Maken van de installatiekopie van een virtuele machine voor Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="5198a-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

