---
title: "aaaAccessing Azure privéclouds met Visual Studio | Microsoft Docs"
description: "Meer informatie over hoe tooaccess privécloud resources met behulp van Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="2a713-103">Toegang tot persoonlijke Azure-clouds met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a713-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="2a713-104">Visual Studio ondersteunt standaard openbare Azure-cloud REST-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2a713-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="2a713-105">In dit onderwerp leert u hoe toouse uw privécloud de tooaccess certificaat - en communiceren met - Hallo privécloud vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a713-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="2a713-106">tooaccess een persoonlijke Azure-cloud in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a713-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="2a713-107">In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885) download het bestand met publicatie-instellingen voor Hallo privécloud, of neem contact op met uw beheerder voor een bestand met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="2a713-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="2a713-108">Hallo op Hallo openbare-versie van Azure koppeling toodownload dit [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="2a713-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="2a713-109">(het gedownloade bestand Hallo moet een extensie van `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="2a713-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="2a713-110">Open Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a713-110">Open Visual Studio</span></span>

1. <span data-ttu-id="2a713-111">In **Server Explorer**, klik met de rechtermuisknop Hallo **Azure** knooppunt en selecteer in het contextmenu hello, **beheren en Filter abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="2a713-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Opdracht voor abonnementen beheren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="2a713-113">In Hallo **Microsoft Azure-abonnementen beheren** dialoogvenster, selecteer Hallo **certificaten** tabblad en selecteer vervolgens **importeren**.</span><span class="sxs-lookup"><span data-stu-id="2a713-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Azure certificaten importeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="2a713-115">In Hallo **importeren Microsoft Azure-abonnementen** dialoogvenster Selecteer **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="2a713-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Knop op Hallo importeren Microsoft Azure-abonnementen dialoogvenster Bladeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="2a713-117">In Hallo **Open** dialoogvenster Bladeren toohello map waar u opgeslagen Hallo publish-settings-bestand, selecteer Hallo bestand en selecteer vervolgens **Open**.</span><span class="sxs-lookup"><span data-stu-id="2a713-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Hallo publiceren instellingenbestand selecteren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="2a713-119">Wanneer geretourneerd toohello **importeren Microsoft Azure-abonnementen** dialoogvenster Selecteer **importeren**.</span><span class="sxs-lookup"><span data-stu-id="2a713-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Hallo publiceren-settings-bestand importeren](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="2a713-121">Hallo-certificaten van Hallo publiceren instellingenbestand in Visual Studio worden ingevoerd en u kunt nu werken met de resources van uw privécloud.</span><span class="sxs-lookup"><span data-stu-id="2a713-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="2a713-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a713-122">Next steps</span></span>
- [<span data-ttu-id="2a713-123">Publishing tooan Azure Cloud Service vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a713-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="2a713-124">[How to: downloaden en importeren van instellingen en abonnementsgegevens publiceren](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="2a713-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
