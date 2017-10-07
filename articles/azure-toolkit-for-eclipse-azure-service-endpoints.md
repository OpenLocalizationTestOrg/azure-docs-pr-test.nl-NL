---
title: aaaAzure Service-eindpunten
description: Beschrijft hello Azure Service-eindpunt instellingen in hello Azure Toolkit voor Eclipse.
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="60bd0-103">Azure Service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="60bd0-103">Azure Service Endpoints</span></span>
<span data-ttu-id="60bd0-104">Azure service-eindpunten die bepalen dat of uw toepassing geïmplementeerd tooand beheerd door Hallo globale Azure-platform wordt, door Azure worden beheerd door 21Vianet in China, of een persoonlijk die door Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="60bd0-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="60bd0-105">Hallo **Service-eindpunten** dialoogvenster kunt u toospecify die service-eindpunten die u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="60bd0-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="60bd0-106">Hallo tooopen **Service-eindpunten** dialoogvenster in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op **Service-eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="60bd0-107">Instelling Hallo **Active ingesteld** veld bepaalt welke Azure-service eindpunten wordt gebruikt voor hello Azure projecten in uw huidige werkruimte.</span><span class="sxs-lookup"><span data-stu-id="60bd0-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="60bd0-108">Hallo hieronder vindt u Hallo **Service-eindpunten** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="60bd0-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="60bd0-109">tooset hello service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="60bd0-109">tooset hello service endpoints</span></span>
<span data-ttu-id="60bd0-110">In Hallo **Service-eindpunten** dialoogvenster, nemen Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="60bd0-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="60bd0-111">Als u wilt dat toouse Hallo globale Azure-platform, van Hallo **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.com** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="60bd0-112">Als u wilt dat Azure beheerd door 21Vianet in China, van Hallo toouse **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.cn (China)** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="60bd0-113">Als u wilt dat toouse persoonlijke Azure-platform:</span><span class="sxs-lookup"><span data-stu-id="60bd0-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="60bd0-114">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="60bd0-115">Een dialoogvenster wordt geopend, waarin wordt gemeld dat Hallo **Service-eindpunten** dialoogvenster wordt gesloten en Hallo voorkeur sets bestand wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="60bd0-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="60bd0-116">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-116">Click **OK**.</span></span>

  3. <span data-ttu-id="60bd0-117">Hallo preferencesets.xml bestand, maak een nieuwe `preferenceset` element.</span><span class="sxs-lookup"><span data-stu-id="60bd0-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="60bd0-118">Voor deze nieuwe element maken `name`, `blob`, `management`, `portalURL` en `publishsettings` kenmerken en waarden toevoegen voor hen die overeenkomen met tooyour persoonlijke Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="60bd0-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="60bd0-119">U kunt Hallo waarden opgegeven voor bestaande hello gebruiken `preferenceset` elementen als sjabloon.</span><span class="sxs-lookup"><span data-stu-id="60bd0-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="60bd0-120">**Opmerking**: waarde gebruikt voor Hallo Hallo `blob` kenmerk Hallo tekst 'blob' hello URL moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="60bd0-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="60bd0-121">Opslaan en sluiten preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="60bd0-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="60bd0-122">Open Hallo **Service-eindpunten** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="60bd0-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="60bd0-123">Van Hallo **Active ingesteld** vervolgkeuzelijst, selecteer Hallo active instellen die u gemaakt en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="60bd0-124">Als u uw persoonlijke Azure-platform hebt gemaakt `preferenceset` element, kunt u Hallo waarden toegewezen tooit wijzigen door te klikken op Hallo **bewerken** knop in Hallo **Services-eindpunt** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="60bd0-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="60bd0-125">U kunt ook meerdere persoonlijke Azure-platform maken `preferenceset` elementen, als u wenst.</span><span class="sxs-lookup"><span data-stu-id="60bd0-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="60bd0-126">Zie ook</span><span class="sxs-lookup"><span data-stu-id="60bd0-126">See Also</span></span>
<span data-ttu-id="60bd0-127">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60bd0-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="60bd0-128">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60bd0-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="60bd0-129">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60bd0-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="60bd0-130">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="60bd0-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
