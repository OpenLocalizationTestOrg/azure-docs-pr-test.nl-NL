---
title: Cloud App Discovery-registerinstellingen voor proxyservices | Microsoft Docs
description: Het doel van dit onderwerp is om te voorzien van de stappen die u moet uitvoeren om in te stellen de vereiste poort op de computers waarop de Cloud App Discovery-agent wordt uitgevoerd.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="745b0-103">Cloud App Discovery-registerinstellingen voor proxyservices</span><span class="sxs-lookup"><span data-stu-id="745b0-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="745b0-104">De Cloud App Discovery-agent is standaard geconfigureerd om alleen de poorten 80 of 443 te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="745b0-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="745b0-105">Als u van plan bent over het installeren van Cloud App Discovery in een omgeving met een proxyserver die van een aangepaste poort (geen 80 of 443 gebruikmaakt), moet u de agents voor het gebruik van deze poort configureren.</span><span class="sxs-lookup"><span data-stu-id="745b0-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="745b0-106">De configuratie is gebaseerd op een registersleutel.</span><span class="sxs-lookup"><span data-stu-id="745b0-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="745b0-107">Het doel van dit onderwerp is om te voorzien van de stappen die u moet uitvoeren om in te stellen de vereiste poort op de computers waarop de Cloud App Discovery-agent wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="745b0-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="745b0-108">**Voor het wijzigen van de poort die wordt gebruikt door de computer waarop de Cloud App Discovery-agent wordt uitgevoerd, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="745b0-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="745b0-109">Start de Registereditor.</span><span class="sxs-lookup"><span data-stu-id="745b0-109">Start the registry editor.</span></span> <br> ![Uitvoeren](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="745b0-111">Ga naar of maak de volgende registersleutel:</span><span class="sxs-lookup"><span data-stu-id="745b0-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="745b0-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="745b0-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="745b0-113">Maak een nieuwe **met meerdere tekenreeksen** waarde met de naam **poorten**.</span><span class="sxs-lookup"><span data-stu-id="745b0-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="745b0-114">![Nieuw](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="745b0-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="745b0-115">Openen van de **met meerdere tekenreeksen bewerken** dialoogvenster, dubbelklik op de waarde van de poorten.</span><span class="sxs-lookup"><span data-stu-id="745b0-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="745b0-116">Typ de volgende waarden in het tekstvak voor waarde-gegevens en alle aangepaste poorten die worden gebruikt door uw organisatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="745b0-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="745b0-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="745b0-117">
   **80**</span></span> <br><span data-ttu-id="745b0-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="745b0-118">
   **8080**</span></span> <br><span data-ttu-id="745b0-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="745b0-119">
   **8118**</span></span> <br><span data-ttu-id="745b0-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="745b0-120">
   **8888**</span></span> <br><span data-ttu-id="745b0-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="745b0-121">
   **81**</span></span> <br><span data-ttu-id="745b0-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="745b0-122">
   **12080**</span></span> <br><span data-ttu-id="745b0-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="745b0-123">
**6999**</span></span> <br><span data-ttu-id="745b0-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="745b0-124">
**30606**</span></span> <br><span data-ttu-id="745b0-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="745b0-125">
**31595**</span></span> <br><span data-ttu-id="745b0-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="745b0-126">
**4080**</span></span> <br><span data-ttu-id="745b0-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="745b0-127">
**443**</span></span> <br><span data-ttu-id="745b0-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="745b0-128">
**1110**</span></span> <br><br><span data-ttu-id="745b0-129">
![Met meerdere tekenreeksen bewerken](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="745b0-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="745b0-130">Klik op **OK** sluiten de **met meerdere tekenreeksen bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="745b0-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="745b0-131">**Aanvullende resources**</span><span class="sxs-lookup"><span data-stu-id="745b0-131">**Additional Resources**</span></span>

* [<span data-ttu-id="745b0-132">Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren</span><span class="sxs-lookup"><span data-stu-id="745b0-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

