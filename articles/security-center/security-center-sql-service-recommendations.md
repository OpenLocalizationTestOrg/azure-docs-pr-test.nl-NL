---
title: aaaProtecting Azure SQL-service en de gegevens in Azure Security Center | Microsoft Docs
description: Dit document gaat in Azure Security Center aanbevelingen die u helpen beveiligen van uw gegevens en de Azure SQL-service en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="25d83-103">Beveiligen van Azure SQL-service en -gegevens in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="25d83-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="25d83-104">Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="25d83-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="25d83-105">Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze aanbevelingen die u helpt bij Hallo Hallo nodig-besturingselementen configureren.</span><span class="sxs-lookup"><span data-stu-id="25d83-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="25d83-106">Aanbevelingen tooAzure brontypen die van toepassing: virtuele machines (VM's), netwerken, SQL en gegevens en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="25d83-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="25d83-107">In dit artikel biedt de aanbevelingen die van toepassing zijn tooAzure SQL-service en -gegevens.</span><span class="sxs-lookup"><span data-stu-id="25d83-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="25d83-108">Aanbevelingen center rond het inschakelen van controle voor Azure SQL-servers en databases, het inschakelen van versleuteling voor SQL-databases en inschakelen van de versleuteling van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="25d83-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="25d83-109">Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbare SQL-service en -gegevens aanbevelingen en elke eigenschap als u deze toe te passen.</span><span class="sxs-lookup"><span data-stu-id="25d83-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="25d83-110">Beschikbare SQL-service en -gegevens aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="25d83-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="25d83-111">Aanbeveling</span><span class="sxs-lookup"><span data-stu-id="25d83-111">Recommendation</span></span> | <span data-ttu-id="25d83-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="25d83-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="25d83-113">Controle en detectie van bedreigingen op SQL-servers inschakelen</span><span class="sxs-lookup"><span data-stu-id="25d83-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="25d83-114">Raadt aan dat u de controle en detectie van bedreigingen voor Azure SQL-servers (Azure SQL-service alleen; niet opnemen SQL uitgevoerd op uw virtuele machines) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25d83-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="25d83-115">Controle en detectie van bedreigingen op SQL-databases inschakelen</span><span class="sxs-lookup"><span data-stu-id="25d83-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="25d83-116">Raadt aan dat u de controle en detectie van bedreigingen voor Azure SQL-databases (Azure SQL-service alleen; niet opnemen SQL uitgevoerd op uw virtuele machines) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25d83-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="25d83-117">Transparante gegevensversleuteling inschakelt op de SQL-databases</span><span class="sxs-lookup"><span data-stu-id="25d83-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="25d83-118">Raadt aan om versleuteling voor SQL-databases (alleen voor Azure SQL-service) in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="25d83-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="25d83-119">Zie ook</span><span class="sxs-lookup"><span data-stu-id="25d83-119">See also</span></span>
<span data-ttu-id="25d83-120">toolearn meer informatie over de aanbevelingen die van toepassing zijn tooother Azure brontypen, Zie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="25d83-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="25d83-121">Beveiligen van uw virtuele machines in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="25d83-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="25d83-122">Beveiligen van uw toepassingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="25d83-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="25d83-123">Beveiligen van uw netwerk in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="25d83-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="25d83-124">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="25d83-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="25d83-125">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="25d83-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="25d83-126">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="25d83-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="25d83-127">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="25d83-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
