---
title: Een Azure-cloud service-project maken met Visual Studio | Microsoft Docs
description: Ontdek hoe u een Azure-cloudserviceproject maken met Visual Studio
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="3d798-103">Een Azure-cloud service-project maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d798-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="3d798-104">De Azure-Tools voor Visual Studio biedt een projectsjabloon waarmee u een Azure-cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="3d798-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="3d798-105">Zodra het project is gemaakt, wordt Visual Studio kunt u configureren en implementeren van de cloudservice in Azure voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="3d798-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="3d798-106">Stappen voor het maken van een Azure-cloud service-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d798-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="3d798-107">Deze sectie helpt u bij het maken van een Azure-cloud service-project in Visual Studio met een of meer webrollen.</span><span class="sxs-lookup"><span data-stu-id="3d798-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="3d798-108">Start Visual Studio als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d798-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="3d798-109">Selecteer in het hoofdmenu **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="3d798-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="3d798-110">Selecteer **Cloud** sjabloon knooppunten van de Visual C# of Visual Basic-project en selecteer **Azure Cloud Service** uit de lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="3d798-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![Nieuwe Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="3d798-112">Geef op welke versie van .NET Framework die u gebruiken wilt voor het ontwikkelen van uw project.</span><span class="sxs-lookup"><span data-stu-id="3d798-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="3d798-113">Voer een naam en locatie voor uw project en een naam voor de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3d798-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="3d798-114">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d798-114">Select **OK**.</span></span>

1. <span data-ttu-id="3d798-115">In de **nieuwe Microsoft Azure Cloud Service** dialoogvenster, selecteer de rollen die u wilt toevoegen en kies de knop pijl naar rechts om toe te voegen aan uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="3d798-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![Selecteer de nieuwe Azure-cloud service-rollen](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="3d798-117">Wijzig de naam van een rol die u hebt toegevoegd, houd de muisaanwijzer op de rol in de **nieuwe Microsoft Azure Cloud Service** dialoogvenster, en selecteer in het contextmenu **naam**.</span><span class="sxs-lookup"><span data-stu-id="3d798-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="3d798-118">U kunt ook een rol wijzigen binnen uw oplossing (in de **Solution Explorer**) nadat deze is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3d798-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![Wijzig de naam van de rol van de Azure-cloud-service](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="3d798-120">Het Azure met Visual Studio-project heeft koppelingen met de functie-projecten in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3d798-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="3d798-121">Het project bevat ook de *servicedefinitiebestand* en *serviceconfiguratiebestand*:</span><span class="sxs-lookup"><span data-stu-id="3d798-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="3d798-122">**Servicedefinitiebestand** -definieert de runtime-instellingen voor uw toepassing, met inbegrip van welke rollen zijn vereist, de eindpunten en de grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3d798-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="3d798-123">**Serviceconfiguratiebestand** -hoeveel exemplaren van een rol worden uitgevoerd en de waarden van de instellingen die zijn gedefinieerd voor een functie configureert.</span><span class="sxs-lookup"><span data-stu-id="3d798-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="3d798-124">Zie voor meer informatie over deze bestanden [de rollen configureert voor een Azure-cloudservice met Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="3d798-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d798-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d798-125">Next steps</span></span>
- [<span data-ttu-id="3d798-126">Het beheren van rollen in Azure cloudserviceprojecten met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d798-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
