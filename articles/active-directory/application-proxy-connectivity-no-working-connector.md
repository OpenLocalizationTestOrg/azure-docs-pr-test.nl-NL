---
title: aaaNo-werkgroep connector gevonden voor een toepassing toepassingsproxy | Microsoft Docs
description: Oplossingen voor problemen die optreden mogelijk wanneer er geen be-Connector in een groep Connector voor uw toepassing Hello Azure AD-toepassingsproxy
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="9db18-103">Er is geen werkgroep connector gevonden voor een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="9db18-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="9db18-104">Dit artikel Help-onderwerp u tooresolve Hallo veelvoorkomende problemen wanneer er geen een gedetecteerd voor een toepassing Application Proxy connector geïntegreerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9db18-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="9db18-105">Overzicht van stappen</span><span class="sxs-lookup"><span data-stu-id="9db18-105">Overview of steps</span></span>
<span data-ttu-id="9db18-106">Als er geen be-Connector in een groep Connector voor uw toepassing, moet u er een aantal manieren tooresolve Hallo probleem zijn:</span><span class="sxs-lookup"><span data-stu-id="9db18-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="9db18-107">Als u geen connectors in de groep Hallo hebt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="9db18-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="9db18-108">Een nieuwe Connector op Hallo rechts on-premises server downloaden en deze toothis groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="9db18-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="9db18-109">Een actieve Connector naar Hallo groep verplaatsen</span><span class="sxs-lookup"><span data-stu-id="9db18-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="9db18-110">Als u geen actieve connectors in Hallo groep hebt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="9db18-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="9db18-111">Hallo reden die de Connector niet actief is identificeren en oplossen</span><span class="sxs-lookup"><span data-stu-id="9db18-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="9db18-112">Een actieve Connector naar Hallo groep verplaatsen</span><span class="sxs-lookup"><span data-stu-id="9db18-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="9db18-113">tooknow welke van de volgende Hallo-probleem is met de Hallo 'Application Proxy' menu openen in uw toepassing en bekijkt hello Connector groep waarschuwingsbericht staan aangegeven.</span><span class="sxs-lookup"><span data-stu-id="9db18-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="9db18-114">Er worden opgegeven die Hallo-groep moet ten minste één Connector (u hebt geen zijn in de groep Hallo) of als er geen actieve Connectors (Hoewel u waarschijnlijk inactieve Connectors hebt).</span><span class="sxs-lookup"><span data-stu-id="9db18-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![De selectie van connector in Azure Portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="9db18-116">Zie voor meer informatie over elk van deze opties Hallo overeenkomstige sectie hieronder.</span><span class="sxs-lookup"><span data-stu-id="9db18-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="9db18-117">Elk van deze wordt ervan uitgegaan dat u op pagina Hallo Connector-beheer begint.</span><span class="sxs-lookup"><span data-stu-id="9db18-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="9db18-118">Als u bovenstaande Hallo foutbericht bekijkt, gaat u toothis pagina door te klikken op de waarschuwing het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="9db18-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="9db18-119">Anders dit kunt u vinden door te gaan**Azure Active Directory**, te klikken op **bedrijfstoepassingen**, klikt u vervolgens **Application Proxy.**</span><span class="sxs-lookup"><span data-stu-id="9db18-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Connector-groepsbeheer in Azure Portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="9db18-121">Een nieuwe Connector downloaden</span><span class="sxs-lookup"><span data-stu-id="9db18-121">Download a new Connector</span></span>

<span data-ttu-id="9db18-122">een nieuwe Connector toodownload gebruik Hallo 'Connector downloaden' knop bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="9db18-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="9db18-123">Opmerking Hallo Connector behoeften toobe geïnstalleerd op een computer met rechtstreeks toohello back-end-toepassing en meestal wordt geplaatst op dezelfde server als de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="9db18-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="9db18-124">Nadat u hebt gedownload, wordt in dit menu Hallo Connector weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9db18-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="9db18-125">Klik op Hallo Connector, en Hallo 'Connector groep' vervolgkeuzelijst toomake ervoor dat het juiste toohello-groep behoort.</span><span class="sxs-lookup"><span data-stu-id="9db18-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="9db18-126">Hallo wijziging opslaan.</span><span class="sxs-lookup"><span data-stu-id="9db18-126">Save hello change.</span></span>

   ![Hallo connector downloaden van hello Azure Portal](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="9db18-128">Verplaatsen van een actieve Connector</span><span class="sxs-lookup"><span data-stu-id="9db18-128">Move an Active Connector</span></span>

<span data-ttu-id="9db18-129">Als er een actieve Connector die moet deel uitmaken van de groep toohello en onbelemmerd zicht toohello doeltoepassing back-end heeft, kunt u Hallo Connector verplaatsen in de groep Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9db18-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="9db18-130">toodo is dus, klikt u op Hallo Connector.</span><span class="sxs-lookup"><span data-stu-id="9db18-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="9db18-131">Hallo vervolgkeuzelijst tooselect Hallo juiste groep gebruiken in Hallo ' Connector ' groepsveld, en klik op opslaan.</span><span class="sxs-lookup"><span data-stu-id="9db18-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="9db18-132">Een inactieve Connector oplossen</span><span class="sxs-lookup"><span data-stu-id="9db18-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="9db18-133">Als hello alleen Connectors in Hallo-groep niet actief zijn, zijn waarschijnlijk op een computer die niet zijn alle Hallo nodig poorten dan gedeblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="9db18-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="9db18-134">Zie Hallo poorten document voor meer informatie over het onderzoeken van dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="9db18-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db18-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9db18-135">Next steps</span></span>
[<span data-ttu-id="9db18-136">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="9db18-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


