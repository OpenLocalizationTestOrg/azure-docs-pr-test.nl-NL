---
title: aaaCloud App Discovery-registerinstellingen voor Proxy Services | Microsoft Docs
description: Hallo-doel van dit onderwerp is tooperform tooset Hallo vereist poort op Hallo van computers Hallo Cloud App Discovery agent tooprovide u Hello stappen die u nodig hebt.
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="9255c-103">Cloud App Discovery-registerinstellingen voor proxyservices</span><span class="sxs-lookup"><span data-stu-id="9255c-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="9255c-104">Hallo Cloud App Discovery agent is standaard geconfigureerd toouse alleen Hallo poorten 80 of 443.</span><span class="sxs-lookup"><span data-stu-id="9255c-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="9255c-105">Als u van plan bent over het installeren van Cloud App Discovery in een omgeving met een proxyserver die van een aangepaste poort (geen 80 of 443 gebruikmaakt), moet u tooconfigure uw agents toouse deze poort.</span><span class="sxs-lookup"><span data-stu-id="9255c-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="9255c-106">Hallo-configuratie is gebaseerd op een registersleutel.</span><span class="sxs-lookup"><span data-stu-id="9255c-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="9255c-107">Hallo-doel van dit onderwerp is tooperform tooset Hallo vereist poort op Hallo van computers Hallo Cloud App Discovery agent tooprovide u Hello stappen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="9255c-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="9255c-108">**toomodify Hallo poort wordt gebruikt door het Hallo-computers Hallo Cloud App Discovery agent, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9255c-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="9255c-109">Start Hallo Register-editor.</span><span class="sxs-lookup"><span data-stu-id="9255c-109">Start hello registry editor.</span></span> <br> ![Voer](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="9255c-111">Navigeer tooor maken Hallo volgende registersleutel:</span><span class="sxs-lookup"><span data-stu-id="9255c-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="9255c-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="9255c-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="9255c-113">Maak een nieuwe **met meerdere tekenreeksen** waarde met de naam **poorten**.</span><span class="sxs-lookup"><span data-stu-id="9255c-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="9255c-114">![Nieuw](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="9255c-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="9255c-115">Hallo tooopen **met meerdere tekenreeksen bewerken** dialoogvenster, dubbelklik op Hallo poorten waarde.</span><span class="sxs-lookup"><span data-stu-id="9255c-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="9255c-116">In Hallo waarde gegevens textbox, typt u Hallo waarden te volgen en voeg alle aangepaste poorten die worden gebruikt door uw organisatie:</span><span class="sxs-lookup"><span data-stu-id="9255c-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="9255c-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="9255c-117">
   **80**</span></span> <br><span data-ttu-id="9255c-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="9255c-118">
   **8080**</span></span> <br><span data-ttu-id="9255c-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="9255c-119">
   **8118**</span></span> <br><span data-ttu-id="9255c-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="9255c-120">
   **8888**</span></span> <br><span data-ttu-id="9255c-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="9255c-121">
   **81**</span></span> <br><span data-ttu-id="9255c-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="9255c-122">
   **12080**</span></span> <br><span data-ttu-id="9255c-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="9255c-123">
**6999**</span></span> <br><span data-ttu-id="9255c-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="9255c-124">
**30606**</span></span> <br><span data-ttu-id="9255c-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="9255c-125">
**31595**</span></span> <br><span data-ttu-id="9255c-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="9255c-126">
**4080**</span></span> <br><span data-ttu-id="9255c-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="9255c-127">
**443**</span></span> <br><span data-ttu-id="9255c-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="9255c-128">
**1110**</span></span> <br><br><span data-ttu-id="9255c-129">
![Met meerdere tekenreeksen bewerken](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="9255c-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="9255c-130">Klik op **OK** tooclose hello **met meerdere tekenreeksen bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9255c-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="9255c-131">**Aanvullende resources**</span><span class="sxs-lookup"><span data-stu-id="9255c-131">**Additional Resources**</span></span>

* [<span data-ttu-id="9255c-132">Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren</span><span class="sxs-lookup"><span data-stu-id="9255c-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

