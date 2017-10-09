---
title: een Azure-cloud service-project met Visual Studio aaaConfigure | Microsoft Docs
description: Meer informatie over hoe tooconfigure een Azure cloud service-project in Visual Studio, afhankelijk van uw vereisten voor dat project.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="1ae66-103">Een Azure-cloud service-project met Visual Studio configureren</span><span class="sxs-lookup"><span data-stu-id="1ae66-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="1ae66-104">U kunt een Azure-cloud service-project, afhankelijk van uw vereisten voor dat project configureren.</span><span class="sxs-lookup"><span data-stu-id="1ae66-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="1ae66-105">U kunt eigenschappen instellen voor Hallo-project voor Hallo volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="1ae66-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="1ae66-106">**Publiceren van een cloud service tooAzure** -u kunt instellen dat een eigenschap toomake of dat een bestaande cloud service geïmplementeerd tooAzure niet per ongeluk is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1ae66-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="1ae66-107">**Uitvoeren of fouten opsporen in een cloudservice op de lokale computer Hallo** -kunt u een service configuration toouse selecteren en aangeven of u wilt dat toostart hello Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="1ae66-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="1ae66-108">**Valideren van een pakket met cloud-service wanneer deze wordt gemaakt** -u kunt ervoor kiezen eventuele waarschuwingen als fouten zodat u kunt ervoor zorgen dat Hallo cloud service-pakket wordt geïmplementeerd zonder problemen tootreat.</span><span class="sxs-lookup"><span data-stu-id="1ae66-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="1ae66-109">Stappen tooconfigure een Azure-cloud service-project</span><span class="sxs-lookup"><span data-stu-id="1ae66-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="1ae66-110">Open of maak een cloudserviceproject in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ae66-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="1ae66-111">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="1ae66-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="1ae66-112">Selecteer in de pagina eigenschappen van het project Hallo Hallo **ontwikkeling** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1ae66-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menu Project-eigenschappen](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="1ae66-114">Stel **vragen voor het verwijderen van een bestaande implementatie** te**True**.</span><span class="sxs-lookup"><span data-stu-id="1ae66-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="1ae66-115">Deze instelling helpt tooensure u per ongeluk een bestaande implementatie in Azure niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="1ae66-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="1ae66-116">Selecteer Hallo gewenst **serviceconfiguratie** tooindicate welke serviceconfiguratie toouse gewenste tijdens het uitvoeren of fouten opsporen in uw cloudservice lokaal.</span><span class="sxs-lookup"><span data-stu-id="1ae66-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="1ae66-117">Voor meer informatie over het toomodify een serviceconfiguratie voor een rol, Zie [hoe tooconfigure Hallo rollen voor een Azure cloud service met Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="1ae66-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="1ae66-118">Stel **Start Azure-opslagemulator** te**True** toostart hello Azure-opslagemulator tijdens het uitvoeren of fouten opsporen in uw cloudservice lokaal.</span><span class="sxs-lookup"><span data-stu-id="1ae66-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="1ae66-119">Stel **waarschuwingen als fouten behandelen** te**True** toomake zeker dat u als er validatiefouten pakket niet publiceren.</span><span class="sxs-lookup"><span data-stu-id="1ae66-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="1ae66-120">Stel **web project poorten** te**True** toomake ervoor wordt gezorgd dat uw Webrol Hallo dezelfde elke poort keer dat er begint lokaal in IIS Express.</span><span class="sxs-lookup"><span data-stu-id="1ae66-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="1ae66-121">Selecteer in de werkbalk van de Visual Studio hello, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1ae66-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ae66-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ae66-122">Next steps</span></span>
- [<span data-ttu-id="1ae66-123">Een Azure-project met behulp van serviceconfiguraties met meerdere configureren</span><span class="sxs-lookup"><span data-stu-id="1ae66-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

