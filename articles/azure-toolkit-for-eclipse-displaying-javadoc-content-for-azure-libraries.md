---
title: Javadoc-inhoud weergeven in Eclipse voor het pakket Azure-bibliotheken voor Java
description: Klik hier voor meer informatie over het weergeven van de Javadoc-inhoud voor de Azure-bibliotheken in Eclipse.
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
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="e4ebe-103">Javadoc-inhoud weergeven in Eclipse voor het pakket Azure-bibliotheken voor Java</span><span class="sxs-lookup"><span data-stu-id="e4ebe-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="e4ebe-104">De Javadoc-inhoud voor de Azure-beheerbibliotheken voor Java kan worden weergegeven in uw omgeving Eclipse door te koppelen van de Javadoc-inhoud naar de Azure-beheerbibliotheken voor Java.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="e4ebe-105">De volgende stappen ziet u hoe u deze functionaliteit in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="e4ebe-106">Deze procedure wordt ervan uitgegaan dat u de Azure-bibliotheek voor Java al hebt toegevoegd aan uw build-pad.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="e4ebe-107">Javadoc-inhoud in Eclipse weergeven voor de Azure-beheerbibliotheken voor Java</span><span class="sxs-lookup"><span data-stu-id="e4ebe-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="e4ebe-108">Binnen de Eclipse-Project Explorer, in de **bibliotheken waarnaar wordt verwezen** gedeelte van uw project, opent u het contextmenu voor de Azure-bibliotheek voor Java JAR.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="e4ebe-109">Bijvoorbeeld: **microsoft-windowsazure-api-0.1.0.jar** (het versienummer mogelijk verschillen, afhankelijk van welke versie u hebt geïnstalleerd).</span><span class="sxs-lookup"><span data-stu-id="e4ebe-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="e4ebe-110">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-110">Click **Properties**.</span></span>

* <span data-ttu-id="e4ebe-111">Binnen de **eigenschappen** dialoogvenster in het linkerdeelvenster klikt u op **Javadoc locatie**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="e4ebe-112">De **Javadoc locatie** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="e4ebe-113">Kunt u een **Javadoc URL**, of een **Javadoc in archief**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="e4ebe-114">Als u ervoor kiest om op te geven een **Javadoc URL**, gebruikt u de URL's, zoals **http://dl.windowsazure.com/javadoc** of **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="e4ebe-115">Als u wilt gebruiken **Javadoc in archief**, kunt u een extern bestand of een bestand in de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="e4ebe-116">Maken van uw keuze en zo nodig bladeren/valideren.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="e4ebe-117">Het volgende voorbeeld wordt de Azure-beheerbibliotheken voor Java met de bijbehorende Javadoc JAR die lokaal is gedownload naar een map met de naam **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="e4ebe-118">*Optionele stap*: klik op **valideren**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="e4ebe-119">Mogelijke problemen met de Javadoc JAR kunnen hier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="e4ebe-120">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-120">Click **OK**.</span></span>

<span data-ttu-id="e4ebe-121">Eenmaal gekoppeld aan de bibliotheek, moet de inhoud Javadoc binnen uw Eclipse IDE worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4ebe-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="e4ebe-122">Bijvoorbeeld, als `blob` van het type is gedefinieerd `CloudBlockBlob` binnen uw code volgt een voorbeeld van Javadoc-inhoud die wordt weergegeven wanneer u typt `blob.acquireLease` in code:</span><span class="sxs-lookup"><span data-stu-id="e4ebe-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="e4ebe-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e4ebe-123">See Also</span></span>
<span data-ttu-id="e4ebe-124">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e4ebe-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="e4ebe-125">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e4ebe-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="e4ebe-126">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e4ebe-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="e4ebe-127">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="e4ebe-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
