---
title: aaaManaging rollen in Azure cloud services met Visual Studio | Microsoft Docs
description: Meer informatie over hoe tooadd en verwijderen van rollen in Azure cloud services met Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="d48a2-103">Het beheren van rollen in Azure cloudservices met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d48a2-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="d48a2-104">Nadat u uw Azure-cloud-service hebt gemaakt, kunt u nieuwe functies tooit toevoegen of verwijderen van bestaande rollen uit.</span><span class="sxs-lookup"><span data-stu-id="d48a2-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="d48a2-105">U kunt ook een bestaand project importeren en converteert u deze rol tooa.</span><span class="sxs-lookup"><span data-stu-id="d48a2-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="d48a2-106">U kunt bijvoorbeeld een ASP.NET-webtoepassing importeren en opgeven dat het een Webrol.</span><span class="sxs-lookup"><span data-stu-id="d48a2-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="d48a2-107">Toevoegen van een rol tooan Azure-cloudservice</span><span class="sxs-lookup"><span data-stu-id="d48a2-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="d48a2-108">Hallo stappen volgen helpt u bij het toevoegen van een web- of worker-rol tooan Azure cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d48a2-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="d48a2-109">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d48a2-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="d48a2-110">In **Solution Explorer**, Hallo projectknooppunt uitvouwen</span><span class="sxs-lookup"><span data-stu-id="d48a2-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="d48a2-111">Klik met de rechtermuisknop Hallo **rollen** knooppunt toodisplay Hallo contextmenu.</span><span class="sxs-lookup"><span data-stu-id="d48a2-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="d48a2-112">Selecteer in het contextmenu hello, **toevoegen**, selecteer vervolgens een bestaande Webrol of functie worker uit de huidige oplossing hello of een web- of worker-rol-project maken.</span><span class="sxs-lookup"><span data-stu-id="d48a2-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="d48a2-113">Ook kunt u een juiste project, zoals een ASP.NET-toepassing-webproject selecteren en deze koppelen aan een rolproject.</span><span class="sxs-lookup"><span data-stu-id="d48a2-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Menu Opties tooadd een rol tooan Azure cloud service-project](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="d48a2-115">Een rol verwijderen uit een Azure cloudservice</span><span class="sxs-lookup"><span data-stu-id="d48a2-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="d48a2-116">Hallo volgende stappen begeleiden u bij een web- of worker-rol verwijderen uit een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d48a2-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="d48a2-117">Maak of open een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d48a2-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="d48a2-118">In **Solution Explorer**, Hallo projectknooppunt uitvouwen</span><span class="sxs-lookup"><span data-stu-id="d48a2-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="d48a2-119">Vouw Hallo **rollen** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d48a2-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="d48a2-120">Klik met de rechtermuisknop Hallo knooppunt u wilt tooremove en, in het contextmenu hello, selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="d48a2-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Menu Opties tooadd een rol tooan Azure-cloudservice](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="d48a2-122">Een rol tooan Azure cloud service-project readding</span><span class="sxs-lookup"><span data-stu-id="d48a2-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="d48a2-123">Als u een rol verwijderen uit uw cloudserviceproject maar later besluit tooadd Hallo-functie weer toohello project alleen Hallo rol declaratie- en basic kenmerken, zoals eindpunten en diagnostische gegevens, worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d48a2-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="d48a2-124">Er is geen aanvullende resources of de verwijzingen worden toegevoegd toohello `ServiceDefinition.csdef` bestand of toohello `ServiceConfiguration.cscfg` bestand.</span><span class="sxs-lookup"><span data-stu-id="d48a2-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="d48a2-125">Als u deze informatie tooadd wilt, moet u toomanually terug naar deze bestanden toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d48a2-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="d48a2-126">Bijvoorbeeld, u mogelijk een Webrol service verwijdert en later besluit van deze rol back tooadd in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="d48a2-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="d48a2-127">Als u dit doet, treedt er een fout op.</span><span class="sxs-lookup"><span data-stu-id="d48a2-127">If you do this, an error occurs.</span></span> <span data-ttu-id="d48a2-128">tooprevent deze fout, hebt u tooadd hello `<LocalResources>` element wordt weergegeven in volgende Hallo XML weer naar Hallo `ServiceDefinition.csdef` bestand.</span><span class="sxs-lookup"><span data-stu-id="d48a2-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="d48a2-129">Gebruik de naam van de Hallo van Hallo-webservicerol die u hebt toegevoegd Hallo project als onderdeel van het naamkenmerk Hallo voor Hallo  **<LocalStorage>**  element.</span><span class="sxs-lookup"><span data-stu-id="d48a2-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="d48a2-130">In dit voorbeeld is de naam van de Hallo van Hallo-webservicerol **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="d48a2-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="d48a2-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d48a2-131">Next steps</span></span>
- [<span data-ttu-id="d48a2-132">Hallo rollen configureert voor een Azure-cloudservice met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d48a2-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
