---
title: aaaAzure IoT Hub IP-verbindingsfilters | Microsoft Docs
description: Hoe toouse IP filteren tooblock verbindingen van specifieke IP-adressen voor tooyour Azure IoT hub. U kunt de verbindingen van afzonderlijke of bereiken van IP-adressen blokkeren.
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
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="edcde-104">IP-filters gebruiken</span><span class="sxs-lookup"><span data-stu-id="edcde-104">Use IP filters</span></span>

<span data-ttu-id="edcde-105">Beveiliging is een belangrijk aspect van een IoT-oplossing op basis van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="edcde-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="edcde-106">Soms moet u tooexplicitly Hallo IP-adressen waaruit apparaten verbinding maken als onderdeel van de beveiligingsconfiguratie opgeven.</span><span class="sxs-lookup"><span data-stu-id="edcde-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="edcde-107">Hallo _IP-filter_ functie kunt u tooconfigure regels voor weigeren of verkeer van specifieke IPv4-adressen accepteren.</span><span class="sxs-lookup"><span data-stu-id="edcde-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="edcde-108">Wanneer toouse</span><span class="sxs-lookup"><span data-stu-id="edcde-108">When toouse</span></span>

<span data-ttu-id="edcde-109">Er zijn twee specifieke gebruiksvoorbeelden wanneer het is nuttig tooblock Hallo Iothub eindpunten voor bepaalde IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="edcde-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="edcde-110">Uw IoT-hub moet ontvangen verkeer alleen via een opgegeven IP-adressen en alle andere afwijzen.</span><span class="sxs-lookup"><span data-stu-id="edcde-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="edcde-111">Bijvoorbeeld, het gebruik van uw IoT-hub met [Azure Express Route] toocreate particuliere verbindingen tussen een IoT-hub en uw on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="edcde-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="edcde-112">U moet tooreject verkeer van IP-adressen die zijn geïdentificeerd als verdacht door Hallo IoT hub-beheerder.</span><span class="sxs-lookup"><span data-stu-id="edcde-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="edcde-113">Hoe filterregels worden toegepast</span><span class="sxs-lookup"><span data-stu-id="edcde-113">How filter rules are applied</span></span>

<span data-ttu-id="edcde-114">Hallo IP-filterregels worden toegepast op Hallo serviceniveau IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="edcde-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="edcde-115">Daarom toepassing hello IP-filterregels tooall verbindingen van apparaten en back-end-apps met behulp van een ondersteund protocol.</span><span class="sxs-lookup"><span data-stu-id="edcde-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="edcde-116">Elke verbindingspoging van een IP-adres dat overeenkomt met een rejecting IP-regel in uw IoT-hub ontvangt een niet-geautoriseerde 401-statuscode en de beschrijving.</span><span class="sxs-lookup"><span data-stu-id="edcde-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="edcde-117">Hallo IP-regel niet wordt vermeld in het antwoord Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="edcde-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="edcde-118">Standaardinstelling</span><span class="sxs-lookup"><span data-stu-id="edcde-118">Default setting</span></span>

<span data-ttu-id="edcde-119">Standaard Hallo **IP-Filter** raster in Hallo-portal voor een IoT-hub is leeg.</span><span class="sxs-lookup"><span data-stu-id="edcde-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="edcde-120">Deze instelling betekent dat uw hub verbindingen elk IP-adres aanvaardt.</span><span class="sxs-lookup"><span data-stu-id="edcde-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="edcde-121">Deze instelling is gelijkwaardig tooa regel die Hallo 0.0.0.0/0 IP-adresbereik accepteert.</span><span class="sxs-lookup"><span data-stu-id="edcde-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![IoT Hub standaard IP-filter-instellingen][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="edcde-123">De regel van een IP-filter toevoegen of bewerken</span><span class="sxs-lookup"><span data-stu-id="edcde-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="edcde-124">Wanneer u een IP-filterregel toevoegt, wordt u gevraagd Hallo volgende waarden op te geven:</span><span class="sxs-lookup"><span data-stu-id="edcde-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="edcde-125">Een **IP-filter regelnaam** die moet een unieke, niet-hoofdlettergevoelige, alfanumerieke tekenreeks van too128 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="edcde-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="edcde-126">Alleen ASCII-7-bits Hallo alfanumerieke tekens plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="edcde-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="edcde-127">Selecteer een **afwijzen** of **accepteren** als Hallo **actie** voor Hallo IP-filterregel.</span><span class="sxs-lookup"><span data-stu-id="edcde-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="edcde-128">Geef één IPv4-adres of een blok IP-adressen in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="edcde-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="edcde-129">Bijvoorbeeld, in CIDR notatie 192.168.100.0/22 vertegenwoordigt Hallo 1024 IPv4-adressen van 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="edcde-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Toevoegen van een IP-filter regel tooan IoT-hub][img-ip-filter-add-rule]

<span data-ttu-id="edcde-131">Nadat u de regel Hallo opslaat, ziet u een waarschuwing meegedeeld dat Hallo-update wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="edcde-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Meldingen over het opslaan van een regel voor IP-filter][img-ip-filter-save-new-rule]

<span data-ttu-id="edcde-133">Hallo **toevoegen** optie wordt uitgeschakeld wanneer u Hallo maximaal 10 filterregels voor de IP-bereiken.</span><span class="sxs-lookup"><span data-stu-id="edcde-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="edcde-134">U kunt een bestaande regel bewerken door te dubbelklikken op Hallo rij die Hallo regel bevat.</span><span class="sxs-lookup"><span data-stu-id="edcde-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="edcde-135">Weigeren IP adressen kunnen voorkomen dat andere Azure-Services (zoals Azure Stream Analytics, Azure Virtual Machines of Hallo apparaat Explorer in de portal Hallo) interactie met Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="edcde-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="edcde-136">Als u Azure Stream Analytics (ASA) tooread berichten van een iothub met IP-filtering is ingeschakeld, gebruikt u Hallo Event Hub-compatibele naam en het eindpunt van uw IoT-Hub in Hallo ASA-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="edcde-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="edcde-137">Een IP-filter-regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="edcde-137">Delete an IP filter rule</span></span>

<span data-ttu-id="edcde-138">toodelete een filterregel IP-Selecteer een of meer regels in Hallo raster en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="edcde-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Een IoT Hub IP-filter-regel verwijderen][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="edcde-140">IP-filter Regeltoepassing</span><span class="sxs-lookup"><span data-stu-id="edcde-140">IP filter rule evaluation</span></span>

<span data-ttu-id="edcde-141">IP-filterregels in volgorde worden toegepast en Hallo van de eerste regel die overeenkomt met Hallo IP-adres Hallo bepaalt accepteren of weigeren actie.</span><span class="sxs-lookup"><span data-stu-id="edcde-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="edcde-142">Als u wilt dat de adressen tooaccept in Hallo bereik 192.168.100.0/22 en alle andere weigeren, moet de eerste regel Hallo in raster Hallo Hallo adresbereik 192.168.100.0/22 accepteren.</span><span class="sxs-lookup"><span data-stu-id="edcde-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="edcde-143">de volgende regel Hallo moet alle adressen weigeren met behulp van Hallo bereik 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="edcde-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="edcde-144">U kunt Hallo volgorde van uw IP-filterregels in Hallo raster wijzigen door Hallo drie verticale punten aan Hallo begin van een rij te klikken en slepen en neerzetten.</span><span class="sxs-lookup"><span data-stu-id="edcde-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="edcde-145">toosave voor uw nieuwe IP-filter regel volgorde, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="edcde-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Hallo-volgorde van uw IoT Hub IP-filterregels wijzigen][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="edcde-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edcde-147">Next steps</span></span>

<span data-ttu-id="edcde-148">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="edcde-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="edcde-149">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="edcde-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="edcde-150">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="edcde-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md