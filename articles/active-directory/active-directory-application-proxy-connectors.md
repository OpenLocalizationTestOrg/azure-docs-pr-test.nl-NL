---
title: Klassieke portal toepassingsproxy van Azure AD-connectors | Microsoft Docs
description: Bevat informatie over het maken en beheren van groepen van connectors in Azure AD-toepassingsproxy.
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
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="0624c-103">Publiceren van toepassingen op afzonderlijke netwerken en locaties met groepen van de connector</span><span class="sxs-lookup"><span data-stu-id="0624c-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0624c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0624c-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="0624c-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0624c-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="0624c-106">Connector-groepen zijn handig voor verschillende scenario's, waaronder:</span><span class="sxs-lookup"><span data-stu-id="0624c-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="0624c-107">-Sites met meerdere onderling verbonden datacenters.</span><span class="sxs-lookup"><span data-stu-id="0624c-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="0624c-108">In dit geval u zoveel verkeer binnen het datacenter mogelijk behouden omdat cross-datacenter koppelingen dure en traag zijn.</span><span class="sxs-lookup"><span data-stu-id="0624c-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="0624c-109">U kunt implementeren connectors in elk datacenter te bedienen alleen de toepassingen die zich in het datacenter bevinden.</span><span class="sxs-lookup"><span data-stu-id="0624c-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="0624c-110">Deze aanpak cross-datacenter koppelingen wordt geminimaliseerd en een volledig transparant ervaring voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0624c-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="0624c-111">Het beheren van toepassingen die zijn geïnstalleerd op de geïsoleerde netwerken die geen deel uitmaken van de belangrijkste bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="0624c-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="0624c-112">Connector-groepen kunt u specifieke connectors installeren op geïsoleerde netwerken ook om toepassingen te isoleren met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0624c-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="0624c-113">Toepassingen die zijn geïnstalleerd op IaaS voor toegang tot de cloud, bieden connector groepen een algemene service de toegang tot alle apps beveiligen.</span><span class="sxs-lookup"><span data-stu-id="0624c-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="0624c-114">Groepen van de connector geen extra afhankelijkheid in uw bedrijfsnetwerk maken of fragment van de appervaring.</span><span class="sxs-lookup"><span data-stu-id="0624c-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="0624c-115">Connectors kunnen worden geïnstalleerd op elke clouddatacenter en dienen alleen toepassingen die zich in dit netwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="0624c-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="0624c-116">U kunt verschillende connectors om te zorgen voor hoge beschikbaarheid installeren.</span><span class="sxs-lookup"><span data-stu-id="0624c-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="0624c-117">Ondersteuning voor meerdere forests omgevingen waarin specifieke connectors kunnen worden geïmplementeerd per forest en instellen voor specifieke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0624c-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="0624c-118">Connector-groepen kunnen worden gebruikt in herstel na noodgevallen sites voor het detecteren van een failover of als back-up voor de primaire site.</span><span class="sxs-lookup"><span data-stu-id="0624c-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="0624c-119">Groepen van de connector kunnen ook worden gebruikt voor meerdere bedrijven van een enkele tenant.</span><span class="sxs-lookup"><span data-stu-id="0624c-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="0624c-120">Voorwaarde: Uw connectors maken</span><span class="sxs-lookup"><span data-stu-id="0624c-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="0624c-121">Voor het groeperen van uw connectors [meerdere connectors installeren](active-directory-application-proxy-enable.md), geef de naam en ze te groeperen.</span><span class="sxs-lookup"><span data-stu-id="0624c-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="0624c-122">Tot slot moet u deze toewijzen aan specifieke apps.</span><span class="sxs-lookup"><span data-stu-id="0624c-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="0624c-123">Stap 1: Connector groepen maken</span><span class="sxs-lookup"><span data-stu-id="0624c-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="0624c-124">U kunt zoveel connector groepen als u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="0624c-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="0624c-125">Het maken van connector wordt uitgevoerd in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0624c-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="0624c-126">Selecteer uw directory en klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="0624c-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="0624c-127">![Toepassingsproxy, schermafbeelding configureren: klik op de connector-groepen beheren](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="0624c-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="0624c-128">Klik onder Application Proxy op **Connector groepen beheren** en een groep connector maken door de groep een naam geven.</span><span class="sxs-lookup"><span data-stu-id="0624c-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="0624c-129">![Connector voor toepassingsproxy schermafbeelding - groep voor de nieuwe groepen](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="0624c-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="0624c-130">Stap 2: Connectors toewijzen aan uw groepen</span><span class="sxs-lookup"><span data-stu-id="0624c-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="0624c-131">Als de connector-groepen zijn gemaakt, verplaatst u de connectors aan de juiste groep.</span><span class="sxs-lookup"><span data-stu-id="0624c-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="0624c-132">Onder **toepassingsproxy**, klikt u op **Connectors beheren**.</span><span class="sxs-lookup"><span data-stu-id="0624c-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="0624c-133">Onder **groep**, selecteer de groep die u voor elke connector.</span><span class="sxs-lookup"><span data-stu-id="0624c-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="0624c-134">Het duurt maximaal 10 minuten actief is in de nieuwe groep de connectors.</span><span class="sxs-lookup"><span data-stu-id="0624c-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="0624c-135">![Schermafbeelding van Application proxy connectors - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="0624c-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="0624c-136">Stap 3: Toepassingen aan de connector-groepen toewijzen</span><span class="sxs-lookup"><span data-stu-id="0624c-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="0624c-137">De laatste stap is het instellen van de connector-groepen die aan deze elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="0624c-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="0624c-138">Selecteer de toepassing die u wilt toewijzen aan de groep en klikt u op in de klassieke Azure-portal in uw directory **configureren**.</span><span class="sxs-lookup"><span data-stu-id="0624c-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="0624c-139">Onder **Connector groep**, selecteer de groep die u wilt dat de toepassing te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0624c-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="0624c-140">Deze wijziging wordt onmiddellijk toegepast.</span><span class="sxs-lookup"><span data-stu-id="0624c-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="0624c-141">![Application proxy connector groep schermafbeelding - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="0624c-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="0624c-142">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0624c-142">See also</span></span>
* [<span data-ttu-id="0624c-143">Toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="0624c-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="0624c-144">Eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="0624c-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="0624c-145">Voorwaardelijke toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="0624c-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="0624c-146">Oplossen van problemen met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="0624c-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="0624c-147">Ga naar het [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/) voor nieuws en updates.</span><span class="sxs-lookup"><span data-stu-id="0624c-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
