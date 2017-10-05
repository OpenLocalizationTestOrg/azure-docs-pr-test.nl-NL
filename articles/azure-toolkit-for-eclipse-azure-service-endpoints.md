---
title: Azure Service-eindpunten
description: Beschrijft de instellingen van Azure Service-eindpunt in de Azure-werkset voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="2b440-103">Azure Service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="2b440-103">Azure Service Endpoints</span></span>
<span data-ttu-id="2b440-104">Azure service-eindpunten die bepalen dat of uw toepassing is geïmplementeerd en beheerd door de globale Azure-platform, door Azure worden beheerd door 21Vianet in China, of een persoonlijk die door Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="2b440-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="2b440-105">De **Service-eindpunten** dialoogvenster kunt u opgeven welke service-eindpunten die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b440-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="2b440-106">Openen van de **Service-eindpunten** dialoogvenster in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op  **Service-eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="2b440-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="2b440-107">Instellen van de **Active ingesteld** veld bepaalt welke Azure-service-eindpunten wordt gebruikt voor de Azure-projecten in uw huidige werkruimte.</span><span class="sxs-lookup"><span data-stu-id="2b440-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="2b440-108">Het volgende bevat de **Service-eindpunten** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b440-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="2b440-109">Instellen van de service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="2b440-109">To set the service endpoints</span></span>
<span data-ttu-id="2b440-110">In de **Service-eindpunten** dialoogvenster, voer een van de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="2b440-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="2b440-111">Als u gebruiken van de globale Azure-platform wilt, van de **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.com** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b440-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="2b440-112">Als u gebruiken van Azure die worden beheerd door 21Vianet in China wilt, uit de **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.cn (China)** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b440-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="2b440-113">Als u gebruiken een persoonlijke Azure-platform wilt:</span><span class="sxs-lookup"><span data-stu-id="2b440-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="2b440-114">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="2b440-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="2b440-115">Een dialoogvenster wordt geopend, waarin wordt gemeld dat de **Service-eindpunten** dialoogvenster wordt gesloten en de voorkeur sets-bestand wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="2b440-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="2b440-116">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b440-116">Click **OK**.</span></span>

  3. <span data-ttu-id="2b440-117">Maak een nieuwe in het bestand preferencesets.xml `preferenceset` element.</span><span class="sxs-lookup"><span data-stu-id="2b440-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="2b440-118">Voor deze nieuwe element maken `name`, `blob`, `management`, `portalURL` en `publishsettings` kenmerken en waarden toevoegen voor hen die overeenkomen met uw persoonlijke Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="2b440-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="2b440-119">U kunt de waarden voor de bestaande `preferenceset` elementen als sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2b440-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="2b440-120">**Opmerking**: de waarde voor de `blob` kenmerk moet de tekst 'blob' in de URL bevatten.</span><span class="sxs-lookup"><span data-stu-id="2b440-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="2b440-121">Opslaan en sluiten preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="2b440-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="2b440-122">Open de **Service-eindpunten** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b440-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="2b440-123">Van de **Active ingesteld** vervolgkeuzelijst, selecteer de actieve instellen die u gemaakt en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b440-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="2b440-124">Als u uw persoonlijke Azure-platform hebt gemaakt `preferenceset` element, kunt u de waarden die zijn toegewezen door te klikken op de **bewerken** knop in de **Services-eindpunt** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b440-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="2b440-125">U kunt ook meerdere persoonlijke Azure-platform maken `preferenceset` elementen, als u wenst.</span><span class="sxs-lookup"><span data-stu-id="2b440-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b440-126">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2b440-126">See Also</span></span>
<span data-ttu-id="2b440-127">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b440-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="2b440-128">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b440-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="2b440-129">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b440-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="2b440-130">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="2b440-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
