---
title: Azure IoT Hub IP-verbindingsfilters | Microsoft Docs
description: Het gebruik van IP-filtering om verbindingen te blokkeren van specifieke IP-adressen voor uw Azure-IoT-hub. U kunt de verbindingen van afzonderlijke of bereiken van IP-adressen blokkeren.
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="919a9-104">IP-filters gebruiken</span><span class="sxs-lookup"><span data-stu-id="919a9-104">Use IP filters</span></span>

<span data-ttu-id="919a9-105">Beveiliging is een belangrijk aspect van een IoT-oplossing op basis van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="919a9-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="919a9-106">Soms moet u expliciet opgeven van de IP-adressen waaruit apparaten verbinding maken als onderdeel van uw beveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="919a9-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="919a9-107">De _IP-filter_ functie kunt u regels voor weigeren of accepteren van verkeer van specifieke IPv4-adressen te configureren.</span><span class="sxs-lookup"><span data-stu-id="919a9-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="919a9-108">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="919a9-108">When to use</span></span>

<span data-ttu-id="919a9-109">Er zijn twee specifieke gebruiksvoorbeelden wanneer dit is handig om te blokkeren van de eindpunten van IoT Hub voor bepaalde IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="919a9-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="919a9-110">Uw IoT-hub moet ontvangen verkeer alleen via een opgegeven IP-adressen en alle andere afwijzen.</span><span class="sxs-lookup"><span data-stu-id="919a9-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="919a9-111">Bijvoorbeeld, het gebruik van uw IoT-hub met [Azure Express Route] naar particuliere verbindingen maken tussen een IoT-hub en uw on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="919a9-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="919a9-112">U moet verkeer van IP-adressen die als verdacht zijn geïdentificeerd door de beheerder van de IoT-hub afwijzen.</span><span class="sxs-lookup"><span data-stu-id="919a9-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="919a9-113">Hoe filterregels worden toegepast</span><span class="sxs-lookup"><span data-stu-id="919a9-113">How filter rules are applied</span></span>

<span data-ttu-id="919a9-114">De IP-filter-regels worden toegepast op het niveau van de service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="919a9-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="919a9-115">Daarom de IP-filterregels van toepassing op alle verbindingen vanaf apparaten en back-end-apps met behulp van een ondersteund protocol.</span><span class="sxs-lookup"><span data-stu-id="919a9-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="919a9-116">Elke verbindingspoging van een IP-adres dat overeenkomt met een rejecting IP-regel in uw IoT-hub ontvangt een niet-geautoriseerde 401-statuscode en de beschrijving.</span><span class="sxs-lookup"><span data-stu-id="919a9-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="919a9-117">De IP-regel niet wordt vermeld in het antwoordbericht.</span><span class="sxs-lookup"><span data-stu-id="919a9-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="919a9-118">Standaardinstelling</span><span class="sxs-lookup"><span data-stu-id="919a9-118">Default setting</span></span>

<span data-ttu-id="919a9-119">Standaard de **IP-Filter** raster in de portal voor een IoT-hub is leeg.</span><span class="sxs-lookup"><span data-stu-id="919a9-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="919a9-120">Deze instelling betekent dat uw hub verbindingen elk IP-adres aanvaardt.</span><span class="sxs-lookup"><span data-stu-id="919a9-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="919a9-121">Deze instelling komt overeen met een regel die de 0.0.0.0/0 IP-adresbereik accepteert.</span><span class="sxs-lookup"><span data-stu-id="919a9-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![IoT Hub standaard IP-filter-instellingen][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="919a9-123">De regel van een IP-filter toevoegen of bewerken</span><span class="sxs-lookup"><span data-stu-id="919a9-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="919a9-124">Wanneer u een IP-filterregel toevoegt, wordt u gevraagd de volgende waarden op te geven:</span><span class="sxs-lookup"><span data-stu-id="919a9-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="919a9-125">Een **IP-filter regelnaam** die moet een unieke, niet-hoofdlettergevoelige alfanumerieke tekenreeks van maximaal 128 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="919a9-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="919a9-126">Alleen de ASCII-7-bits alfanumerieke tekens plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="919a9-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="919a9-127">Selecteer een **afwijzen** of **accepteren** als de **actie** voor de IP-filter-regel.</span><span class="sxs-lookup"><span data-stu-id="919a9-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="919a9-128">Geef één IPv4-adres of een blok IP-adressen in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="919a9-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="919a9-129">Bijvoorbeeld, in CIDR vertegenwoordigt notatie 192.168.100.0/22 de 1024 IPv4-adressen van 192.168.100.0 tot 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="919a9-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Een IP-filter-regel toevoegen aan een IoT-hub][img-ip-filter-add-rule]

<span data-ttu-id="919a9-131">Nadat u de regel opslaat, ziet u een waarschuwing dat de update uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="919a9-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Meldingen over het opslaan van een regel voor IP-filter][img-ip-filter-save-new-rule]

<span data-ttu-id="919a9-133">De **toevoegen** optie wordt uitgeschakeld wanneer u het maximum van 10 filterregels voor de IP-bereiken.</span><span class="sxs-lookup"><span data-stu-id="919a9-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="919a9-134">U kunt een bestaande regel bewerken door te dubbelklikken op de rij waarin de regel.</span><span class="sxs-lookup"><span data-stu-id="919a9-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="919a9-135">Weigeren IP adressen kunnen voorkomen dat andere Azure-Services (zoals Azure Stream Analytics, Azure Virtual Machines of de Explorer-apparaat in de portal) interactie met de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="919a9-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="919a9-136">Als u Azure Stream Analytics (ASA) gebruikt om berichten te lezen van een iothub met IP-filtering is ingeschakeld, gebruikt u de Event Hub-compatibele naam en het eindpunt van uw IoT-Hub in de ASA-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="919a9-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="919a9-137">Een IP-filter-regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="919a9-137">Delete an IP filter rule</span></span>

<span data-ttu-id="919a9-138">Een IP-filter als regel wilt verwijderen, selecteert u een of meer regels in het raster en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="919a9-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Een IoT Hub IP-filter-regel verwijderen][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="919a9-140">IP-filter Regeltoepassing</span><span class="sxs-lookup"><span data-stu-id="919a9-140">IP filter rule evaluation</span></span>

<span data-ttu-id="919a9-141">IP-filterregels in volgorde worden toegepast en de eerste regel die overeenkomt met het IP-adres bepaalt de actie accepteren of weigeren.</span><span class="sxs-lookup"><span data-stu-id="919a9-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="919a9-142">Als u wilt adressen in het bereik 192.168.100.0/22 accepteren en weigeren alle andere, moet de eerste regel in het raster het adresbereik 192.168.100.0/22 accepteren.</span><span class="sxs-lookup"><span data-stu-id="919a9-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="919a9-143">De volgende regel moet alle adressen weigeren met behulp van de 0.0.0.0/0 bereik.</span><span class="sxs-lookup"><span data-stu-id="919a9-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="919a9-144">U kunt de volgorde van de regels van uw IP-filter in het raster wijzigen door de drie verticale punten aan het begin van een rij te klikken en slepen en neerzetten.</span><span class="sxs-lookup"><span data-stu-id="919a9-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="919a9-145">Klik voor het opslaan van uw nieuwe IP-filter regel order **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="919a9-145">To save your new IP filter rule order, click **Save**.</span></span>

![De volgorde van uw IoT Hub IP-filterregels wijzigen][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="919a9-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="919a9-147">Next steps</span></span>

<span data-ttu-id="919a9-148">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="919a9-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="919a9-149">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="919a9-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="919a9-150">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="919a9-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="919a9-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="919a9-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md