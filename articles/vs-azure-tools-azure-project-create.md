---
title: een Azure-cloud service-project met Visual Studio aaaCreating | Microsoft Docs
description: Meer informatie over toocreate nu een Azure-cloud service-project met Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="805cb-103">Een Azure-cloud service-project maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="805cb-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="805cb-104">Hello Azure-Tools voor Visual Studio biedt een projectsjabloon waarmee u een Azure-cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="805cb-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="805cb-105">Zodra het Hallo-project is gemaakt, Visual Studio kunt u tooconfigure, fouten opsporen en Hallo cloud service tooAzure implementeren.</span><span class="sxs-lookup"><span data-stu-id="805cb-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="805cb-106">Stappen toocreate een Azure-cloud service-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="805cb-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="805cb-107">Deze sectie helpt u bij het maken van een Azure-cloud service-project in Visual Studio met een of meer webrollen.</span><span class="sxs-lookup"><span data-stu-id="805cb-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="805cb-108">Start Visual Studio als beheerder.</span><span class="sxs-lookup"><span data-stu-id="805cb-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="805cb-109">Selecteer in het hoofdmenu hello, **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="805cb-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="805cb-110">Selecteer **Cloud** van Hallo Visual C# of Visual Basic project knooppunten van de sjabloon en selecteer **Azure Cloud Service** uit Hallo lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="805cb-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Nieuwe Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="805cb-112">Geef op welke versie van .NET Framework gewenste toouse toodevelop uw project Hallo.</span><span class="sxs-lookup"><span data-stu-id="805cb-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="805cb-113">Voer een naam en locatie voor uw project en een naam voor het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="805cb-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="805cb-114">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="805cb-114">Select **OK**.</span></span>

1. <span data-ttu-id="805cb-115">In Hallo **nieuwe Microsoft Azure Cloud Service** dialoogvenster, selecteer Hallo rollen die u tooadd wilt en kies Hallo pijl naar rechts knop tooadd ze tooyour oplossing.</span><span class="sxs-lookup"><span data-stu-id="805cb-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Selecteer de nieuwe Azure-cloud service-rollen](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="805cb-117">toorename een rol die u hebt toegevoegd, aanwijzen op Hallo-rol in Hallo **nieuwe Microsoft Azure Cloud Service** dialoogvenster, en selecteer in het contextmenu hello, **naam**.</span><span class="sxs-lookup"><span data-stu-id="805cb-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="805cb-118">U kunt ook een rol wijzigen binnen uw oplossing (in Hallo **Solution Explorer**) nadat deze is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="805cb-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Wijzig de naam van de rol van de Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="805cb-120">Hello Azure met Visual Studio-project bevat koppelingen toohello rol projecten Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="805cb-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="805cb-121">Hallo-project bevat ook Hallo *servicedefinitiebestand* en *serviceconfiguratiebestand*:</span><span class="sxs-lookup"><span data-stu-id="805cb-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="805cb-122">**Servicedefinitiebestand** -Hallo runtime-instellingen voor uw toepassing, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="805cb-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="805cb-123">**Serviceconfiguratiebestand** -hoeveel exemplaren van een rol worden uitgevoerd en Hallo waarden van het Hallo-instellingen die zijn gedefinieerd voor een functie configureert.</span><span class="sxs-lookup"><span data-stu-id="805cb-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="805cb-124">Zie voor meer informatie over deze bestanden [Hallo rollen configureert voor een Azure-cloudservice met Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="805cb-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="805cb-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="805cb-125">Next steps</span></span>
- [<span data-ttu-id="805cb-126">Het beheren van rollen in Azure cloudserviceprojecten met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="805cb-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
