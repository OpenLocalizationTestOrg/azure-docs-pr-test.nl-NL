---
title: aaaDebugging een gepubliceerde een Azure-cloudservice met Visual Studio en IntelliTrace | Microsoft Docs
description: Meer informatie over hoe toodebug een cloud service met Visual Studio en IntelliTrace
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="f7670-103">Een gepubliceerde Azure-cloudservice met Visual Studio en IntelliTrace-foutopsporing</span><span class="sxs-lookup"><span data-stu-id="f7670-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="f7670-104">U kunt uitgebreide foutopsporingsinformatie voor een rolexemplaar van met IntelliTrace registreren wanneer deze wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7670-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="f7670-105">Als u toofind Hallo oorzaak van een probleem moet, kunt u Hallo IntelliTrace-logboeken toostep via uw code vanuit Visual Studio als in Azure werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7670-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="f7670-106">In feite replay IntelliTrace records sleutel code kan worden uitgevoerd en de omgeving gegevens wanneer uw Azure-toepassing wordt uitgevoerd als een cloudservice in Azure, en u kunt gegevens Hallo vastgelegd vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7670-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="f7670-107">U kunt IntelliTrace hebt u Visual Studio Enterprise geïnstalleerd en de doelen van uw Azure-toepassing .NET Framework 4 of hoger gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7670-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="f7670-108">IntelliTrace verzamelt gegevens voor uw Azure-functies.</span><span class="sxs-lookup"><span data-stu-id="f7670-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="f7670-109">Hallo virtuele machines voor deze rollen altijd 64-bits besturingssystemen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7670-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="f7670-110">Als alternatief kunt u [foutopsporing op afstand](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach rechtstreeks tooa cloudservice die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7670-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7670-111">IntelliTrace is bedoeld voor foutopsporing scenario's alleen en mag niet worden gebruikt voor een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="f7670-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="f7670-112">Een Azure-toepassing voor IntelliTrace configureren</span><span class="sxs-lookup"><span data-stu-id="f7670-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="f7670-113">tooenable IntelliTrace voor een Azure-toepassing, moet u maken en publiceren van de toepassing hello uit een Azure met Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="f7670-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="f7670-114">Voordat u deze tooAzure publiceert, moet u de IntelliTrace configureren voor uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7670-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="f7670-115">Als u uw toepassing publiceert zonder IntelliTrace configureren, moet u toorepublish Hallo project.</span><span class="sxs-lookup"><span data-stu-id="f7670-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="f7670-116">Zie voor meer informatie [publiceren van een Azure cloud services-projecten met Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="f7670-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="f7670-117">Wanneer u bent klaar toodeploy uw Azure-toepassing, Controleer of de doelen van uw project build te worden ingesteld**Debug**.</span><span class="sxs-lookup"><span data-stu-id="f7670-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="f7670-118">In **Solution Explorer**, met de rechtermuisknop op het project en selecteer in het contextmenu hello, **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f7670-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="f7670-119">In Hallo **Publish Azure Application** dialoogvenster, selecteer hello Azure-abonnement en selecteert u **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7670-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="f7670-120">In Hallo **instellingen** pagina, selecteer Hallo **geavanceerde instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7670-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="f7670-121">Hallo inschakelen **IntelliTrace inschakelen** optie toocollect IntelliTrace-logboeken voor uw toepassing wanneer het wordt gepubliceerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7670-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="f7670-122">toocustomize hello IntelliTrace basisconfiguratie, selecteer **instellingen** volgende te**IntelliTrace inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="f7670-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Koppeling van IntelliTrace-instellingen](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="f7670-124">In Hallo **IntelliTrace instellingen** dialoogvenster kunt u opgeven welke gebeurtenissen toolog, of de informatie voor het aanroepen van toocollect, welke processen en -modules toocollect logboeken voor en hoeveel ruimte tooallocate toohello opnemen.</span><span class="sxs-lookup"><span data-stu-id="f7670-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="f7670-125">Zie voor meer informatie over IntelliTrace [foutopsporing met IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="f7670-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace-instellingen](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="f7670-127">Hallo IntelliTrace-logboek is een circulair logboekbestand van de maximale grootte Hallo opgegeven in de Hallo IntelliTrace-instellingen (standaardgrootte Hallo is 250 MB).</span><span class="sxs-lookup"><span data-stu-id="f7670-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="f7670-128">IntelliTrace-logboeken zijn verzameld tooa-bestand in het bestandssysteem Hallo van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7670-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="f7670-129">Wanneer u Logboeken Hallo aanvraagt, wordt een momentopname is gemaakt op dat moment en de lokale computer tooyour gedownload.</span><span class="sxs-lookup"><span data-stu-id="f7670-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="f7670-130">Nadat u gepubliceerde tooAzure hello Azure-cloudservice hebt, kunt u bepalen als IntelliTrace is ingeschakeld vanaf hello Azure knooppunt in **Server Explorer**, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7670-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Server Explorer - IntelliTrace ingeschakeld](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="f7670-132">IntelliTrace-logboeken voor een rolexemplaar van downloaden</span><span class="sxs-lookup"><span data-stu-id="f7670-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="f7670-133">U kunt met behulp van Visual Studio IntelliTrace-logboeken voor een rolexemplaar van downloaden met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f7670-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="f7670-134">In **Server Explorer**, vouw Hallo **Cloudservices** knooppunt, en zoek rolinstantie waarvan u wilt dat toodownload Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f7670-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="f7670-135">Met de rechtermuisknop op de rolinstantie hello en selecteer in het contextmenu Hallo s, **IntelliTrace-logboeken bekijken**.</span><span class="sxs-lookup"><span data-stu-id="f7670-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Menuoptie voor IntelliTrace-logboeken weergeven](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="f7670-137">Hallo IntelliTrace-logboeken zijn gedownloade tooa bestand in een map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f7670-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="f7670-138">Elke keer dat u Hallo IntelliTrace-logboeken aanvragen, wordt een nieuwe momentopname gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7670-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="f7670-139">Tijdens het Hallo-logboeken worden gedownload, Visual Studio Hallo geeft voortgang weer van Hallo-bewerking in Hallo **Azure Activity Log** venster.</span><span class="sxs-lookup"><span data-stu-id="f7670-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="f7670-140">Zoals u in de volgende afbeelding Hallo, kunt u uitbreiden Hallo regelitem voor Hallo bewerking toosee meer details.</span><span class="sxs-lookup"><span data-stu-id="f7670-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="f7670-142">In Visual Studio kunt u toowork blijven terwijl Hallo IntelliTrace-logboeken worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="f7670-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="f7670-143">Wanneer het Hallo-logboek is gedownload, wordt het geopend in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7670-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="f7670-144">Hallo IntelliTrace-logboeken bevatten mogelijk uitzonderingen die framework Hallo genereert en daarna worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f7670-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="f7670-145">Interne framework code genereert deze uitzonderingen als een normaal onderdeel van het opstarten van een rol, zodat u ze kunt negeren.</span><span class="sxs-lookup"><span data-stu-id="f7670-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f7670-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7670-146">Next steps</span></span>
- [<span data-ttu-id="f7670-147">Opties voor het opsporen van Azure-cloudservices</span><span class="sxs-lookup"><span data-stu-id="f7670-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="f7670-148">Publiceren van een Azure-cloudservice met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7670-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)