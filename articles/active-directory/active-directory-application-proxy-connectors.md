---
title: aaaClassic portal Azure AD-toepassingsproxy connectors | Microsoft Docs
description: Dekt hoe toocreate en beheren van groepen van connectors in Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="5144b-103">Publiceren van toepassingen op afzonderlijke netwerken en locaties met groepen van de connector</span><span class="sxs-lookup"><span data-stu-id="5144b-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5144b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5144b-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="5144b-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5144b-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="5144b-106">Connector-groepen zijn handig voor verschillende scenario's, waaronder:</span><span class="sxs-lookup"><span data-stu-id="5144b-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="5144b-107">-Sites met meerdere onderling verbonden datacenters.</span><span class="sxs-lookup"><span data-stu-id="5144b-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="5144b-108">In dit geval u tookeep zoveel verkeer binnen Hallo datacenter mogelijk omdat cross-datacenter koppelingen dure en traag zijn.</span><span class="sxs-lookup"><span data-stu-id="5144b-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="5144b-109">U kunt connectoren in elk datacenter tooserve alleen Hallo toepassingen die zich bevinden in Hallo datacenter kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="5144b-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="5144b-110">Deze aanpak minimaliseert cross-datacenter koppelingen en biedt een volledig transparant ervaring tooyour gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5144b-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="5144b-111">Het beheren van toepassingen die zijn geïnstalleerd op de geïsoleerde netwerken die geen deel uitmaken van de belangrijkste bedrijfsnetwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="5144b-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="5144b-112">U kunt connector groepen tooinstall dedicated connectors in geïsoleerde netwerken tooalso isoleren toepassingen toohello netwerk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5144b-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="5144b-113">Toepassingen die zijn geïnstalleerd op IaaS voor toegang tot de cloud, bieden connector groepen een algemene service toosecure Hallo toegang tooall Hallo-apps.</span><span class="sxs-lookup"><span data-stu-id="5144b-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="5144b-114">Groepen van de connector geen extra afhankelijkheid in uw bedrijfsnetwerk maken of fragment Hallo van apps.</span><span class="sxs-lookup"><span data-stu-id="5144b-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="5144b-115">Connectors kunnen worden geïnstalleerd op elke clouddatacenter en dienen alleen toepassingen die zich in dit netwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="5144b-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="5144b-116">U kunt verschillende connectors tooachieve hoge beschikbaarheid installeren.</span><span class="sxs-lookup"><span data-stu-id="5144b-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="5144b-117">Ondersteuning voor meerdere forests omgevingen waarin specifieke connectors kunnen worden geïmplementeerd per forest en tooserve specifieke toepassingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5144b-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="5144b-118">Connector-groepen kunnen worden gebruikt in herstel na noodgevallen sites tooeither failover detecteren of als back-up voor Hallo belangrijkste site.</span><span class="sxs-lookup"><span data-stu-id="5144b-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="5144b-119">Groepen van de connector kunnen ook worden gebruikt tooserve meerdere bedrijven van een enkele tenant.</span><span class="sxs-lookup"><span data-stu-id="5144b-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="5144b-120">Voorwaarde: Uw connectors maken</span><span class="sxs-lookup"><span data-stu-id="5144b-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="5144b-121">toogroup uw connectors [meerdere connectors installeren](active-directory-application-proxy-enable.md), geef de naam en ze te groeperen.</span><span class="sxs-lookup"><span data-stu-id="5144b-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="5144b-122">Ten slotte het hebben van tooassign ze toospecific apps.</span><span class="sxs-lookup"><span data-stu-id="5144b-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="5144b-123">Stap 1: Connector groepen maken</span><span class="sxs-lookup"><span data-stu-id="5144b-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="5144b-124">U kunt zoveel connector groepen als u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="5144b-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="5144b-125">Het maken van connector wordt uitgevoerd in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5144b-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="5144b-126">Selecteer uw directory en klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="5144b-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="5144b-127">![Toepassingsproxy, schermafbeelding configureren: klik op de connector-groepen beheren](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="5144b-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="5144b-128">Klik onder Application Proxy op **Connector groepen beheren** en maakt u een groep connector door Hallo groep een naam geven.</span><span class="sxs-lookup"><span data-stu-id="5144b-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="5144b-129">![Connector voor toepassingsproxy schermafbeelding - groep voor de nieuwe groepen](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="5144b-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="5144b-130">Stap 2: Toewijzen connectors tooyour groepen</span><span class="sxs-lookup"><span data-stu-id="5144b-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="5144b-131">Als Hallo connector groepen zijn gemaakt, verplaatst u Hallo connectors toohello juiste groep.</span><span class="sxs-lookup"><span data-stu-id="5144b-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="5144b-132">Onder **toepassingsproxy**, klikt u op **Connectors beheren**.</span><span class="sxs-lookup"><span data-stu-id="5144b-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="5144b-133">Onder **groep**, selecteer Hallo groep die u voor elke connector.</span><span class="sxs-lookup"><span data-stu-id="5144b-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="5144b-134">Het kan Hallo connectors up too10 minuten toobecome actief is in de nieuwe groep Hallo duren.</span><span class="sxs-lookup"><span data-stu-id="5144b-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="5144b-135">![Schermafbeelding van Application proxy connectors - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="5144b-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="5144b-136">Stap 3: Toepassingen tooyour connector groepen toewijzen</span><span class="sxs-lookup"><span data-stu-id="5144b-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="5144b-137">de laatste stap Hallo tooset wordt elke toepassing toohello connector groepen die aan deze.</span><span class="sxs-lookup"><span data-stu-id="5144b-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="5144b-138">In de klassieke Azure-portal in uw directory Hallo Selecteer toepassing die u wilt dat tooassign toohello groep en klikt u op Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="5144b-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="5144b-139">Onder **Connector groep**, selecteer gewenste toepassing toouse Hallo Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="5144b-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="5144b-140">Deze wijziging wordt onmiddellijk toegepast.</span><span class="sxs-lookup"><span data-stu-id="5144b-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="5144b-141">![Application proxy connector groep schermafbeelding - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="5144b-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="5144b-142">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5144b-142">See also</span></span>
* [<span data-ttu-id="5144b-143">Toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="5144b-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="5144b-144">Eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="5144b-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="5144b-145">Voorwaardelijke toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="5144b-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="5144b-146">Oplossen van problemen met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="5144b-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="5144b-147">Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="5144b-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
