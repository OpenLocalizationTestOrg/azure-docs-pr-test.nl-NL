---
title: Endpoint Protection installeren in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** installeren Endpoint Protection **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="ba7d9-103">Endpoint Protection installeren in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ba7d9-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="ba7d9-104">Azure Security Center raadt endpoint protection op uw virtuele Azure-machines (VM's) te installeren als endpoint protection nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="ba7d9-105">Deze aanbeveling is alleen van toepassing op Windows-VM's.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="ba7d9-106">Deze voorbeeldimplementatie maakt gebruik van Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="ba7d9-107">Zie [Partner-integratie in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) voor een lijst met partners die is geïntegreerd met Security Center.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ba7d9-108">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="ba7d9-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="ba7d9-109">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ba7d9-110">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="ba7d9-111">In de **aanbevelingen** blade Selecteer **Endpoint Protection installeren**.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="ba7d9-112">![Selecteer de Endpoint Protection installeren][1]</span><span class="sxs-lookup"><span data-stu-id="ba7d9-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="ba7d9-113">De **Endpoint Protection installeren** blade wordt geopend met een lijst van virtuele machines zonder endpoint protection.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="ba7d9-114">Selecteer in de lijst van de virtuele machines die u wilt installeren van endpoint protection op en klik op **installeren op virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="ba7d9-115">![Selecteer de virtuele machines voor het installeren van Endpoint Protection op][2]</span><span class="sxs-lookup"><span data-stu-id="ba7d9-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="ba7d9-116">De **Selecteer Endpoint Protection** er wordt een blade geopend zodat u kunt selecteren van de endpoint protection-oplossing die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="ba7d9-117">In dit voorbeeld gaan we selecteren **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="ba7d9-118">![Selecteer de Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="ba7d9-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="ba7d9-119">Meer informatie over de oplossing voor eindpuntbeveiliging wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="ba7d9-120">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-120">Select **Create**.</span></span>
   <span data-ttu-id="ba7d9-121">![Maken van anti-malwareoplossing][4]</span><span class="sxs-lookup"><span data-stu-id="ba7d9-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="ba7d9-122">Voer de vereiste configuratie-instellingen op de **Add Extension** blade en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="ba7d9-123">Zie voor meer informatie over de configuratie-instellingen, [standaard en aangepaste Antimalware configuratie](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="ba7d9-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="ba7d9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is nu actief zijn op de geselecteerde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba7d9-125">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ba7d9-125">See also</span></span>
<span data-ttu-id="ba7d9-126">In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center "Endpoint Protection installeren."</span><span class="sxs-lookup"><span data-stu-id="ba7d9-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="ba7d9-127">Zie voor meer informatie over het inschakelen van Microsoft Antimalware in Azure, het volgende document:</span><span class="sxs-lookup"><span data-stu-id="ba7d9-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="ba7d9-128">[Microsoft Antimalware voor Cloudservices en virtuele Machines](../security/azure-security-antimalware.md) --informatie over het implementeren van Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="ba7d9-129">Zie de volgende documenten voor meer informatie over Security Center:</span><span class="sxs-lookup"><span data-stu-id="ba7d9-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="ba7d9-130">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --informatie over het configureren van beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="ba7d9-131">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ba7d9-132">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ba7d9-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ba7d9-134">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ba7d9-135">[Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ba7d9-136">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="ba7d9-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
