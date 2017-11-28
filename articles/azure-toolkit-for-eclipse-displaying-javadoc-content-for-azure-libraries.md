---
title: aaaDisplaying Javadoc-inhoud in Eclipse voor Hallo pakket van de Azure-bibliotheken voor Java
description: Hoe hello toodisplay Javadoc-inhoud voor hello Azure-bibliotheken in Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="3f3aa-103">Javadoc-inhoud weergeven in Eclipse voor Hallo pakket van de Azure-bibliotheken voor Java</span><span class="sxs-lookup"><span data-stu-id="3f3aa-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="3f3aa-104">Hallo Javadoc-inhoud voor hello Azure-beheerbibliotheken voor Java kan worden weergegeven in uw omgeving Eclipse door te koppelen Hallo Javadoc inhoud toohello Azure-beheerbibliotheken voor Java.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="3f3aa-105">Hallo volgende stappen ziet u hoe toouse deze functionaliteit in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="3f3aa-106">Deze procedure wordt ervan uitgegaan dat u al hello Azure-bibliotheek voor Java tooyour build pad hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="3f3aa-107">toodisplay Javadoc-inhoud in Eclipse voor hello Azure-beheerbibliotheken voor Java</span><span class="sxs-lookup"><span data-stu-id="3f3aa-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="3f3aa-108">In de Projectverkenner van Eclipse in Hallo **bibliotheken waarnaar wordt verwezen** gedeelte van uw project, open Hallo contextmenu voor hello Azure-bibliotheek voor Java JAR.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="3f3aa-109">Bijvoorbeeld: **microsoft-windowsazure-api-0.1.0.jar** (Hallo versienummer mogelijk verschillen, afhankelijk van welke versie u hebt geïnstalleerd).</span><span class="sxs-lookup"><span data-stu-id="3f3aa-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="3f3aa-110">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-110">Click **Properties**.</span></span>

* <span data-ttu-id="3f3aa-111">Binnen Hallo **eigenschappen** dialoogvenster in het linkerdeelvenster hello, klikt u op **Javadoc locatie**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="3f3aa-112">Hallo **Javadoc locatie** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="3f3aa-113">Kunt u een **Javadoc URL**, of een **Javadoc in archief**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="3f3aa-114">Als u ervoor toospecify kiest een **Javadoc URL**, Hallo URL's gebruiken zoals **http://dl.windowsazure.com/javadoc** of **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="3f3aa-115">Als u ervoor toouse kiest **Javadoc in archief**, kunt u een extern bestand of een bestand in de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="3f3aa-116">Maken van uw keuze en zo nodig bladeren/valideren.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="3f3aa-117">Hallo volgende voorbeeld worden gekoppeld aan hello Azure-beheerbibliotheken voor Java Hallo lokaal tooa map met de naam bijbehorende Javadoc JAR die is gedownload **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="3f3aa-118">*Optionele stap*: klik op **valideren**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="3f3aa-119">Mogelijke problemen met Hallo Javadoc JAR kunnen hier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="3f3aa-120">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-120">Click **OK**.</span></span>

<span data-ttu-id="3f3aa-121">Eenmaal gekoppeld met Hallo-bibliotheek, moet Hallo Javadoc inhoud binnen uw Eclipse IDE worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f3aa-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="3f3aa-122">Bijvoorbeeld, als `blob` van het type is gedefinieerd `CloudBlockBlob` binnen uw code Hallo volgt een voorbeeld van Javadoc-inhoud die wordt weergegeven wanneer u typt `blob.acquireLease` in code:</span><span class="sxs-lookup"><span data-stu-id="3f3aa-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="3f3aa-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3f3aa-123">See Also</span></span>
<span data-ttu-id="3f3aa-124">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3aa-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="3f3aa-125">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3aa-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="3f3aa-126">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3aa-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="3f3aa-127">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3f3aa-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
