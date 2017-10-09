---
title: aaaDeep Duik in vehicle health voorspellen en die zorg draagt gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="b3c41-103">Vehicle telemetrie analytics-oplossing playbook: diepgaand in Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="b3c41-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="b3c41-104">Dit **menu** toohello secties van dit playbook koppelingen:</span><span class="sxs-lookup"><span data-stu-id="b3c41-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="b3c41-105">Deze sectie zoomt in op in elk van de fasen van het Hallo afgebeeld in Hallo oplossingsarchitectuur met instructies en verwijzingen voor aanpassing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="b3c41-106">Gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="b3c41-106">Data Sources</span></span>
<span data-ttu-id="b3c41-107">Hallo-oplossing maakt gebruik van twee verschillende gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="b3c41-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="b3c41-108">**gesimuleerde vehicle signalen en diagnostische gegevensset** en</span><span class="sxs-lookup"><span data-stu-id="b3c41-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="b3c41-109">**vehicle catalogus**</span><span class="sxs-lookup"><span data-stu-id="b3c41-109">**vehicle catalog**</span></span>

<span data-ttu-id="b3c41-110">Er is een vehicle telematica simulator opgenomen als onderdeel van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="b3c41-111">Deze diagnostische gegevens verzendt en signalen bijbehorende toohello status van Hallo vehicle en toohello besturen patroon op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="b3c41-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="b3c41-112">Klik op [Vehicle telematica Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle telematica Simulator Visual Studio-oplossing** voor aanpassingen op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="b3c41-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="b3c41-113">Hallo vehicle catalogus bevat een verwijzingsgegevensset met een Chassisnummer toomodel-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Vehicle telematica simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="b3c41-115">*Afbeelding 1 – Vehicle telematica Simulator*</span><span class="sxs-lookup"><span data-stu-id="b3c41-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="b3c41-116">Dit is een JSON-indeling gegevensset met Hallo schema te volgen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="b3c41-117">Kolom</span><span class="sxs-lookup"><span data-stu-id="b3c41-117">Column</span></span> | <span data-ttu-id="b3c41-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b3c41-118">Description</span></span> | <span data-ttu-id="b3c41-119">Waarden</span><span class="sxs-lookup"><span data-stu-id="b3c41-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3c41-120">CHASSISNUMMER</span><span class="sxs-lookup"><span data-stu-id="b3c41-120">VIN</span></span> |<span data-ttu-id="b3c41-121">Willekeurig gegenereerde Vehicle id-nummer</span><span class="sxs-lookup"><span data-stu-id="b3c41-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="b3c41-122">Hiermee wordt opgehaald uit een master lijst 10.000 willekeurig gegenereerde vehicle-id's.</span><span class="sxs-lookup"><span data-stu-id="b3c41-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="b3c41-123">Externe temperatuur</span><span class="sxs-lookup"><span data-stu-id="b3c41-123">Outside temperature</span></span> |<span data-ttu-id="b3c41-124">Hallo buiten temperatuur waar Hallo vehicle wordt bestuurd</span><span class="sxs-lookup"><span data-stu-id="b3c41-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="b3c41-125">Willekeurig gegenereerd nummer tussen 0-100</span><span class="sxs-lookup"><span data-stu-id="b3c41-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="b3c41-126">Engine temperatuur</span><span class="sxs-lookup"><span data-stu-id="b3c41-126">Engine temperature</span></span> |<span data-ttu-id="b3c41-127">Hallo-engine temperatuur van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="b3c41-128">Willekeurig gegenereerd nummer tussen 0-500</span><span class="sxs-lookup"><span data-stu-id="b3c41-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="b3c41-129">Snelheid</span><span class="sxs-lookup"><span data-stu-id="b3c41-129">Speed</span></span> |<span data-ttu-id="b3c41-130">Hallo-engine snelheid op welke Hallo vehicle wordt bestuurd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="b3c41-131">Willekeurig gegenereerd nummer tussen 0-100</span><span class="sxs-lookup"><span data-stu-id="b3c41-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="b3c41-132">Brandstof</span><span class="sxs-lookup"><span data-stu-id="b3c41-132">Fuel</span></span> |<span data-ttu-id="b3c41-133">Hallo brandstofpeil van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="b3c41-134">Willekeurig gegenereerd nummer tussen 0-100 (geeft brandstof niveau percentage)</span><span class="sxs-lookup"><span data-stu-id="b3c41-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="b3c41-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="b3c41-135">EngineOil</span></span> |<span data-ttu-id="b3c41-136">Hallo-engine olie niveau van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="b3c41-137">Willekeurig gegenereerd nummer tussen 0-100 (geeft engine olie niveau percentage)</span><span class="sxs-lookup"><span data-stu-id="b3c41-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="b3c41-138">Druk band</span><span class="sxs-lookup"><span data-stu-id="b3c41-138">Tire pressure</span></span> |<span data-ttu-id="b3c41-139">Hallo band druk van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="b3c41-140">Willekeurig gegenereerde getal van 0 tot 50 (geeft band zware belasting op het niveau percentage)</span><span class="sxs-lookup"><span data-stu-id="b3c41-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="b3c41-141">Kilometerstand</span><span class="sxs-lookup"><span data-stu-id="b3c41-141">Odometer</span></span> |<span data-ttu-id="b3c41-142">Hallo kilometerstand van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="b3c41-143">Willekeurig gegenereerd nummer van 0 200000</span><span class="sxs-lookup"><span data-stu-id="b3c41-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="b3c41-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="b3c41-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="b3c41-145">Hallo accelerator vorm positie van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="b3c41-146">Willekeurig gegenereerd nummer tussen 0-100 (geeft accelerator niveau percentage)</span><span class="sxs-lookup"><span data-stu-id="b3c41-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="b3c41-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="b3c41-147">Parking_brake_status</span></span> |<span data-ttu-id="b3c41-148">Hiermee wordt aangegeven of Hallo vehicle geparkeerd of niet</span><span class="sxs-lookup"><span data-stu-id="b3c41-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="b3c41-149">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-149">True or False</span></span> |
| <span data-ttu-id="b3c41-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="b3c41-150">Headlamp_status</span></span> |<span data-ttu-id="b3c41-151">Geeft aan waar Hallo licht op of niet</span><span class="sxs-lookup"><span data-stu-id="b3c41-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="b3c41-152">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-152">True or False</span></span> |
| <span data-ttu-id="b3c41-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="b3c41-153">Brake_pedal_status</span></span> |<span data-ttu-id="b3c41-154">Hiermee wordt aangegeven of Hallo rempedaal wordt ingedrukt of niet</span><span class="sxs-lookup"><span data-stu-id="b3c41-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="b3c41-155">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-155">True or False</span></span> |
| <span data-ttu-id="b3c41-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="b3c41-156">Transmission_gear_position</span></span> |<span data-ttu-id="b3c41-157">Hallo transmission tandwielpictogram positie van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="b3c41-158">Statussen: eerste, tweede, derde, vierde vijfde, zesde, zevende, achtste</span><span class="sxs-lookup"><span data-stu-id="b3c41-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="b3c41-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="b3c41-159">Ignition_status</span></span> |<span data-ttu-id="b3c41-160">Hiermee wordt aangegeven of Hallo vehicle uitgevoerd of gestopt</span><span class="sxs-lookup"><span data-stu-id="b3c41-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="b3c41-161">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-161">True or False</span></span> |
| <span data-ttu-id="b3c41-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="b3c41-162">Windshield_wiper_status</span></span> |<span data-ttu-id="b3c41-163">Hiermee wordt aangegeven of Hallo voorruit combinatie of niet is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="b3c41-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="b3c41-164">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-164">True or False</span></span> |
| <span data-ttu-id="b3c41-165">ABS</span><span class="sxs-lookup"><span data-stu-id="b3c41-165">ABS</span></span> |<span data-ttu-id="b3c41-166">Hiermee wordt aangegeven of ABS is ingeschakeld of niet</span><span class="sxs-lookup"><span data-stu-id="b3c41-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="b3c41-167">True of False</span><span class="sxs-lookup"><span data-stu-id="b3c41-167">True or False</span></span> |
| <span data-ttu-id="b3c41-168">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="b3c41-168">Timestamp</span></span> |<span data-ttu-id="b3c41-169">Hallo tijdstempel wanneer Hallo gegevenspunt wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="b3c41-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="b3c41-170">Date</span><span class="sxs-lookup"><span data-stu-id="b3c41-170">Date</span></span> |
| <span data-ttu-id="b3c41-171">Plaats</span><span class="sxs-lookup"><span data-stu-id="b3c41-171">City</span></span> |<span data-ttu-id="b3c41-172">Hallo-locatie van Hallo vehicle</span><span class="sxs-lookup"><span data-stu-id="b3c41-172">hello location of hello vehicle</span></span> |<span data-ttu-id="b3c41-173">4 plaatsen zijn in deze oplossing: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="b3c41-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="b3c41-174">Hallo vehicle model verwijzingsgegevensset bevat VIN toohello modeltoewijzing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="b3c41-175">CHASSISNUMMER</span><span class="sxs-lookup"><span data-stu-id="b3c41-175">VIN</span></span> | <span data-ttu-id="b3c41-176">Model</span><span class="sxs-lookup"><span data-stu-id="b3c41-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="b3c41-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="b3c41-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="b3c41-178">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-178">Sedan</span></span> |
| <span data-ttu-id="b3c41-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="b3c41-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="b3c41-180">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-180">Hybrid</span></span> |
| <span data-ttu-id="b3c41-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="b3c41-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="b3c41-182">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-182">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="b3c41-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="b3c41-184">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-184">Sedan</span></span> |
| <span data-ttu-id="b3c41-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="b3c41-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="b3c41-186">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-186">Hybrid</span></span> |
| <span data-ttu-id="b3c41-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="b3c41-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="b3c41-188">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-188">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="b3c41-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="b3c41-190">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-190">Sedan</span></span> |
| <span data-ttu-id="b3c41-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="b3c41-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="b3c41-192">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-192">Hybrid</span></span> |
| <span data-ttu-id="b3c41-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="b3c41-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="b3c41-194">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-194">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="b3c41-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="b3c41-196">Converteerbaar</span><span class="sxs-lookup"><span data-stu-id="b3c41-196">Convertible</span></span> |
| <span data-ttu-id="b3c41-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="b3c41-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="b3c41-198">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="b3c41-198">Station Wagon</span></span> |
| <span data-ttu-id="b3c41-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="b3c41-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="b3c41-200">Compacte auto</span><span class="sxs-lookup"><span data-stu-id="b3c41-200">Compact Car</span></span> |
| <span data-ttu-id="b3c41-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="b3c41-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="b3c41-202">Kleine standaard</span><span class="sxs-lookup"><span data-stu-id="b3c41-202">Small SUV</span></span> |
| <span data-ttu-id="b3c41-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="b3c41-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="b3c41-204">Sport auto</span><span class="sxs-lookup"><span data-stu-id="b3c41-204">Sports Car</span></span> |
| <span data-ttu-id="b3c41-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="b3c41-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="b3c41-206">Gemiddeld standaard</span><span class="sxs-lookup"><span data-stu-id="b3c41-206">Medium SUV</span></span> |
| <span data-ttu-id="b3c41-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="b3c41-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="b3c41-208">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="b3c41-208">Station Wagon</span></span> |
| <span data-ttu-id="b3c41-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="b3c41-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="b3c41-210">Grote standaard</span><span class="sxs-lookup"><span data-stu-id="b3c41-210">Large SUV</span></span> |
| <span data-ttu-id="b3c41-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="b3c41-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="b3c41-212">Grote standaard</span><span class="sxs-lookup"><span data-stu-id="b3c41-212">Large SUV</span></span> |
| <span data-ttu-id="b3c41-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="b3c41-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="b3c41-214">Coupé</span><span class="sxs-lookup"><span data-stu-id="b3c41-214">Coupe</span></span> |
| <span data-ttu-id="b3c41-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="b3c41-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="b3c41-216">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-216">Sedan</span></span> |
| <span data-ttu-id="b3c41-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="b3c41-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="b3c41-218">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-218">Hybrid</span></span> |
| <span data-ttu-id="b3c41-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="b3c41-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="b3c41-220">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-220">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="b3c41-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="b3c41-222">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-222">Sedan</span></span> |
| <span data-ttu-id="b3c41-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="b3c41-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="b3c41-224">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-224">Hybrid</span></span> |
| <span data-ttu-id="b3c41-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="b3c41-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="b3c41-226">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-226">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="b3c41-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="b3c41-228">Sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-228">Sedan</span></span> |
| <span data-ttu-id="b3c41-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="b3c41-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="b3c41-230">Hybride</span><span class="sxs-lookup"><span data-stu-id="b3c41-230">Hybrid</span></span> |
| <span data-ttu-id="b3c41-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="b3c41-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="b3c41-232">Familie sedan</span><span class="sxs-lookup"><span data-stu-id="b3c41-232">Family Saloon</span></span> |
| <span data-ttu-id="b3c41-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="b3c41-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="b3c41-234">Converteerbaar</span><span class="sxs-lookup"><span data-stu-id="b3c41-234">Convertible</span></span> |
| <span data-ttu-id="b3c41-235">…….</span><span class="sxs-lookup"><span data-stu-id="b3c41-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="b3c41-236">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="b3c41-236">References</span></span>
[<span data-ttu-id="b3c41-237">Vehicle telematica Simulator Visual Studio-oplossing</span><span class="sxs-lookup"><span data-stu-id="b3c41-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="b3c41-238">Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="b3c41-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="b3c41-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b3c41-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="b3c41-240">Opname</span><span class="sxs-lookup"><span data-stu-id="b3c41-240">Ingestion</span></span>
<span data-ttu-id="b3c41-241">Combinaties van Azure Event Hubs, Stream Analytics en Data Factory worden overgenomen tooingest Hallo vehicle signalen, Hallo diagnostische gebeurtenissen, en realtime en analytics batch.</span><span class="sxs-lookup"><span data-stu-id="b3c41-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="b3c41-242">Al deze onderdelen zijn gemaakt en geconfigureerd als onderdeel van de implementatie van Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="b3c41-243">Realtime analyses</span><span class="sxs-lookup"><span data-stu-id="b3c41-243">Real-time analysis</span></span>
<span data-ttu-id="b3c41-244">Hallo gebeurtenissen die worden gegenereerd door Hallo Vehicle telematica Simulator worden gepubliceerd toohello Event Hub gebruiken Hallo Event Hub SDK.</span><span class="sxs-lookup"><span data-stu-id="b3c41-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="b3c41-245">Hallo Stream Analytics-taak opgenomen deze gebeurtenissen van Hallo Event Hub en processen Hallo gegevens in realtime tooanalyze Hallo vehicle health.</span><span class="sxs-lookup"><span data-stu-id="b3c41-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Event hub-dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="b3c41-247">*Afbeelding 4: Event Hub-dashboard*</span><span class="sxs-lookup"><span data-stu-id="b3c41-247">*Figure 4 - Event Hub dashboard*</span></span>

![Stream Analytics-taak verwerken van gegevens](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="b3c41-249">*Afbeelding 5 - Stream Analytics-taak verwerken van gegevens*</span><span class="sxs-lookup"><span data-stu-id="b3c41-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="b3c41-250">Hallo Stream Analytics-taak;</span><span class="sxs-lookup"><span data-stu-id="b3c41-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="b3c41-251">gegevens uit Event Hub Hallo opgenomen</span><span class="sxs-lookup"><span data-stu-id="b3c41-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="b3c41-252">voert een koppeling met Hallo verwijzing toomap Hallo vehicle VIN toohello bijbehorende gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="b3c41-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="b3c41-253">persistente ze in Azure blob storage voor uitgebreide batch analytics.</span><span class="sxs-lookup"><span data-stu-id="b3c41-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="b3c41-254">Hallo na Stream Analytics-query is gebruikt toopersist Hallo gegevens in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b3c41-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Stream Analytics-taak query voor gegevensopname](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="b3c41-256">*Afbeelding 6 - Stream Analytics-taak query voor gegevensopname*</span><span class="sxs-lookup"><span data-stu-id="b3c41-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="b3c41-257">Batchanalyse</span><span class="sxs-lookup"><span data-stu-id="b3c41-257">Batch analysis</span></span>
<span data-ttu-id="b3c41-258">Er zijn ook een extra volume van de gesimuleerde vehicle signalen en diagnostische gegevensset voor uitgebreidere batch analytics genereren.</span><span class="sxs-lookup"><span data-stu-id="b3c41-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="b3c41-259">Dit is vereiste tooensure een goede representatief gegevensvolume voor batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="b3c41-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="b3c41-260">Voor dit doel gebruiken we een pijplijn met de naam 'PrepareSampleDataPipeline' in hello Azure Data Factory werkstroom toogenerate een jaar lang gesimuleerde vehicle signalen en diagnostische gegevensset.</span><span class="sxs-lookup"><span data-stu-id="b3c41-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="b3c41-261">Klik op [Data Factory aangepaste activiteit](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload Hallo Data Factory aangepaste DotNet activiteit Visual Studio-oplossing voor aanpassingen op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="b3c41-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Voorbeeldgegevens voor batchverwerking werkstroom voorbereiden](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="b3c41-263">*Afbeelding 7: voorbeeldgegevens voorbereiden voor de werkstroom voor batch*</span><span class="sxs-lookup"><span data-stu-id="b3c41-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="b3c41-264">Hallo pijplijn bestaat uit een aangepaste ADF .net activiteit, hier weergeven:</span><span class="sxs-lookup"><span data-stu-id="b3c41-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline activiteit](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="b3c41-266">*Afbeelding 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="b3c41-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="b3c41-267">Hallo-pipeline met succes uitgevoerd als 'RawCarEventsTable' dataset is gemarkeerd als 'Gereed' één jaar waard gesimuleerde vehicle signalen en diagnostische worden gegevens geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="b3c41-268">U ziet de volgende Hallo mappen en bestanden die zijn gemaakt in uw opslagaccount onder Hallo 'connectedcar' container:</span><span class="sxs-lookup"><span data-stu-id="b3c41-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![PrepareSampleDataPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="b3c41-270">*Afbeelding 9 - PrepareSampleDataPipeline uitvoer*</span><span class="sxs-lookup"><span data-stu-id="b3c41-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="b3c41-271">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="b3c41-271">References</span></span>
[<span data-ttu-id="b3c41-272">Azure Event Hub SDK voor streamopname</span><span class="sxs-lookup"><span data-stu-id="b3c41-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="b3c41-273">[Mogelijkheden van Azure Data Factory data movement](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet-activiteit](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="b3c41-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="b3c41-274">Azure Data Factory DotNet activiteit visual studio-oplossing voor het voorbereiden van voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="b3c41-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="b3c41-275">Partitie Hallo gegevensset</span><span class="sxs-lookup"><span data-stu-id="b3c41-275">Partition hello dataset</span></span>
<span data-ttu-id="b3c41-276">Hallo onbewerkte semi-gestructureerde vehicle signalen en diagnostische gegevensset worden in Hallo gegevens voorbereiding stap naar een indeling maand/gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="b3c41-277">Deze partitioneren bijdraagt aan het efficiënter uitvoeren van query's en schaalbare langdurige opslag vervolgens als eerste account Hallo doordat fault-over van een blob account toohello vol is.</span><span class="sxs-lookup"><span data-stu-id="b3c41-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="b3c41-278">Deze stap in Hallo-oplossing is van toepassing alleen toobatch verwerking.</span><span class="sxs-lookup"><span data-stu-id="b3c41-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="b3c41-279">Invoer en uitvoer gegevensbeheer gegevens:</span><span class="sxs-lookup"><span data-stu-id="b3c41-279">Input and output data data management:</span></span>

* <span data-ttu-id="b3c41-280">Hallo **uitvoergegevens** (met het label *PartitionedCarEventsTable*) is toobe gedurende een lange periode als Hallo fundamentele / 'rawest' vorm van gegevens in van de klant Hallo 'Data Lake'.</span><span class="sxs-lookup"><span data-stu-id="b3c41-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="b3c41-281">Hallo **invoergegevens** toothis pijplijn zou doorgaans worden verwijderd, omdat de uitvoergegevens Hallo volledige fidelity toohello invoer heeft-alleen wordt opgeslagen (gepartitioneerd) beter voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="b3c41-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Partitie auto gebeurtenissen werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="b3c41-283">*Afbeelding 10 – partitie auto gebeurtenissen werkstroom*</span><span class="sxs-lookup"><span data-stu-id="b3c41-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="b3c41-284">de onbewerkte gegevens Hallo is gepartitioneerd met behulp van een HDInsight Hive-activiteit in 'PartitionCarEventsPipeline'.</span><span class="sxs-lookup"><span data-stu-id="b3c41-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="b3c41-285">Hallo voorbeeldgegevens gegenereerd in stap 1 van een jaar is jaar/maand gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="b3c41-286">Hallo-partities zijn gebruikte toogenerate vehicle signalen en diagnostische gegevens voor elke maand (totaal 12 partities) van een jaar.</span><span class="sxs-lookup"><span data-stu-id="b3c41-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline activiteit](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="b3c41-288">*Afbeelding 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="b3c41-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="b3c41-289">***PartitionConnectedCarEvents Hive-Script***</span><span class="sxs-lookup"><span data-stu-id="b3c41-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="b3c41-290">Hallo volgende Hive-script met de naam 'partitioncarevents.hql' wordt gebruikt voor het partitioneren en bevindt zich in map van '\demo\src\connectedcar\scripts' Hallo van Hallo gedownloade zip.</span><span class="sxs-lookup"><span data-stu-id="b3c41-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="b3c41-291">Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Gepartitioneerde uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="b3c41-293">*Afbeelding 12 - gepartitioneerde uitvoer*</span><span class="sxs-lookup"><span data-stu-id="b3c41-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="b3c41-294">Hallo-gegevens nu is geoptimaliseerd, beter beheerbaar en gereed voor verdere verwerking toogain uitgebreide batch insights.</span><span class="sxs-lookup"><span data-stu-id="b3c41-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="b3c41-295">Data-analyse</span><span class="sxs-lookup"><span data-stu-id="b3c41-295">Data Analysis</span></span>
<span data-ttu-id="b3c41-296">In deze sectie ziet u hoe toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory en Azure HDInsight voor rich geavanceerde analyses op de drager gezondheid en groot gewoonten.</span><span class="sxs-lookup"><span data-stu-id="b3c41-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="b3c41-297">Er zijn drie subsecties hier:</span><span class="sxs-lookup"><span data-stu-id="b3c41-297">There are three subsections here:</span></span>

1. <span data-ttu-id="b3c41-298">**Machine Learning**: in deze subsectie bevat informatie over Hallo afwijkingsdetectie detectie experiment die wordt gebruikt in deze oplossing toopredict voertuigen vereisen onderhoud onderhoud en voertuigen teruggehaald vanwege problemen met toosafety vereisen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="b3c41-299">**Analyse van realtime**: in deze subsectie bevat informatie over Hallo realtime-analyses met behulp van de Stream Analytics Query Language Hallo en operationele Hallo machine learning-experiment in realtime met een aangepaste toepassing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="b3c41-300">**Batch-analyse**: in deze subsectie bevat informatie over Hallo transformeren en verwerking van Hallo batch gegevens met Azure HDInsight en Azure Machine Learning geoperationaliseerd door Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b3c41-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="b3c41-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b3c41-301">Machine Learning</span></span>
<span data-ttu-id="b3c41-302">Ons doel hier is toopredict Hallo voertuigen waarvoor onderhoud of intrekken op basis van bepaalde Health statistieken.</span><span class="sxs-lookup"><span data-stu-id="b3c41-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="b3c41-303">Wij maken Hallo na veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="b3c41-303">We make hello following assumptions</span></span>

* <span data-ttu-id="b3c41-304">Als een van de Hallo na drie voorwaarden voldaan wordt, Hallo voertuigen vereisen **onderhoud onderhoud**:</span><span class="sxs-lookup"><span data-stu-id="b3c41-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="b3c41-305">Band druk is laag</span><span class="sxs-lookup"><span data-stu-id="b3c41-305">Tire pressure is low</span></span>
  * <span data-ttu-id="b3c41-306">Engine olie niveau is laag</span><span class="sxs-lookup"><span data-stu-id="b3c41-306">Engine oil level is low</span></span>
  * <span data-ttu-id="b3c41-307">Engine temperatuur is hoog</span><span class="sxs-lookup"><span data-stu-id="b3c41-307">Engine temperature is high</span></span>
* <span data-ttu-id="b3c41-308">Als een van de Hallo volgende voorwaarden voldaan wordt, Hallo voertuigen wellicht een **veiligheid probleem** en vereisen **intrekken**:</span><span class="sxs-lookup"><span data-stu-id="b3c41-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="b3c41-309">Engine temperatuur hoog is, maar externe temperatuur is laag</span><span class="sxs-lookup"><span data-stu-id="b3c41-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="b3c41-310">Engine temperatuur laag is, maar externe temperatuur is hoog</span><span class="sxs-lookup"><span data-stu-id="b3c41-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="b3c41-311">Op basis van de vorige vereisten hello, hebben we twee afzonderlijke modellen toodetect afwijkingen, één voor de detectie van vehicle onderhoud en één voor vehicle intrekken detectie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3c41-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="b3c41-312">In beide modellen, wordt Hallo ingebouwde Principal onderdeel Analysis (Pso)-algoritme gebruikt voor afwijkingsdetectie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="b3c41-313">**Model voor onderhoud**</span><span class="sxs-lookup"><span data-stu-id="b3c41-313">**Maintenance detection model**</span></span>

<span data-ttu-id="b3c41-314">Als een van drie indicatoren - band druk, engine olie of engine temperatuur - aan de respectieve voorwaarde voldoet, meldt Hallo onderhoud detectie model een afwijkingsdetectie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="b3c41-315">Als gevolg hiervan, alleen moet tooconsider deze drie variabelen bij het bouwen van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="b3c41-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="b3c41-316">In ons experiment in Azure Machine Learning, gebruiken we eerst een **Select Columns in Dataset** module tooextract deze drie variabelen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="b3c41-317">We gebruiken naast Hallo PCA-gebaseerd anomaliedetectie detection module toobuild hello afwijkingsdetectie detectie model.</span><span class="sxs-lookup"><span data-stu-id="b3c41-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="b3c41-318">Principal onderdeel analyse (Pso) is een techniek tot stand gebrachte in machine learning die toegepast toofeature selectie, classificatie en afwijkingsdetectie detectie worden kan.</span><span class="sxs-lookup"><span data-stu-id="b3c41-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="b3c41-319">PCA zet een set krat met mogelijk gecorreleerde variabelen in een set waarden principal onderdelen genoemd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="b3c41-320">Hallo sleutel idee modellering PCA-gebaseerd is tooproject gegevens naar een lager dimensionale ruimte zodat functies en afwijkingen kunnen gemakkelijk worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="b3c41-321">Voor elke nieuwe invoer hello te detectie model, Hallo afwijkingsdetectie detectie eerst de projectie op Hallo eigenvectors wordt berekend en vervolgens berekent de Hallo herstel fout genormaliseerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="b3c41-322">Deze fout genormaliseerde is Hallo afwijkingsdetectie score.</span><span class="sxs-lookup"><span data-stu-id="b3c41-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="b3c41-323">Hallo hoger Hallo fout, hello meer afwijkende Hallo-exemplaar is.</span><span class="sxs-lookup"><span data-stu-id="b3c41-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="b3c41-324">Hallo onderhoud detectie probleem kunt elke record worden beschouwd als een punt in een 3-dimensionale ruimte gedefinieerd door band druk, engine olie en temperatuur motor coördinaten.</span><span class="sxs-lookup"><span data-stu-id="b3c41-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="b3c41-325">toocapture deze afwijkingen kunnen we Hallo oorspronkelijke gegevens in Hallo 3-dimensionale ruimte project naar een 2-dimensionale ruimte met behulp van Pso.</span><span class="sxs-lookup"><span data-stu-id="b3c41-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="b3c41-326">We stellen dus Hallo parameter aantal onderdelen toouse in PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="b3c41-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="b3c41-327">Deze parameter speelt een belangrijke rol bij het toepassen van PCA-gebaseerd anomaliedetectie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="b3c41-328">Na projecteren gegevens met behulp van Pso, kunnen we deze afwijkingen gemakkelijker identificeren.</span><span class="sxs-lookup"><span data-stu-id="b3c41-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="b3c41-329">**Model voor afwijkingsdetectie intrekken** In Hallo intrekken afwijkingsdetectie detectie model gebruiken we Hallo Select Columns in Dataset en PCA-gebaseerd anomaliedetectie detectiemodules op soortgelijke wijze.</span><span class="sxs-lookup"><span data-stu-id="b3c41-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="b3c41-330">In het bijzonder we drie variabelen - engine temperatuur, externe temperatuur en snelheid - hello gebruiken voor het eerst uitpakken **Select Columns in Dataset** module.</span><span class="sxs-lookup"><span data-stu-id="b3c41-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="b3c41-331">We ook Hallo snelheid variabele omdat Hallo engine temperatuur meestal gecorreleerde toohello snelheid.</span><span class="sxs-lookup"><span data-stu-id="b3c41-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="b3c41-332">We gebruiken naast PCA-gebaseerd anomaliedetectie module tooproject Hallo gegevens van 3-dimensionale ruimte Hallo naar een 2-dimensionale ruimte.</span><span class="sxs-lookup"><span data-stu-id="b3c41-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="b3c41-333">Hallo intrekken criteria is voldaan en dus intrekken door Hallo vehicle is vereist wanneer engine temperatuur- en externe temperatuur maximaal negatieve worden gecorreleerd.</span><span class="sxs-lookup"><span data-stu-id="b3c41-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="b3c41-334">PCA-gebaseerd anomaliedetectie-algoritme kunnen we Hallo afwijkingen vastleggen na het uitvoeren van Pso.</span><span class="sxs-lookup"><span data-stu-id="b3c41-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="b3c41-335">Bij het model trainen, moeten we toouse normale gegevens, die geen onderhoud of intrekken als Hallo invoergegevens tootrain Hallo PCA-gebaseerd anomaliedetectie detectie model vereist.</span><span class="sxs-lookup"><span data-stu-id="b3c41-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="b3c41-336">In Hallo score berekenen experiment, gebruiken we Hallo getraind afwijkingsdetectie detectie model toodetect al dan niet Hallo vehicle onderhoud of intrekken vereist.</span><span class="sxs-lookup"><span data-stu-id="b3c41-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="b3c41-337">Realtime analyses</span><span class="sxs-lookup"><span data-stu-id="b3c41-337">Real-time analysis</span></span>
<span data-ttu-id="b3c41-338">Hallo na Stream Analytics SQL-Query wordt gebruikt tooget Hallo gemiddelde van alle belangrijke vehicle parameters zoals vehicle snelheid, brandstofpeil engine temperatuur, kilometerstand, band druk, engine olie niveau en anderen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b3c41-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="b3c41-339">Hallo gemiddelde zijn gebruikte toodetect afwijkingen, waarschuwingen uitgeven, en bepalen Hallo algehele status voorwaarden van voertuigen in specifieke regio worden beheerd en die de correleren in toodemographics.</span><span class="sxs-lookup"><span data-stu-id="b3c41-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Stream Analytics query voor realtime verwerking](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="b3c41-341">*Afbeelding 13-Stream Analytics query voor realtime verwerking*</span><span class="sxs-lookup"><span data-stu-id="b3c41-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="b3c41-342">Alle Hallo gemiddelden worden via een TumblingWindow 3 seconden berekend.</span><span class="sxs-lookup"><span data-stu-id="b3c41-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="b3c41-343">We gebruiken TubmlingWindow in dit geval omdat we is vereist voor niet-overlappende en aaneengesloten tijdsintervallen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="b3c41-344">toolearn meer informatie over alle mogelijkheden van Hallo 'Windowing' in Azure Stream Analytics, klikt u op [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3c41-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="b3c41-345">**Realtime voorspelling**</span><span class="sxs-lookup"><span data-stu-id="b3c41-345">**Real-time prediction**</span></span>

<span data-ttu-id="b3c41-346">Er is een toepassing in realtime opgenomen als onderdeel van Hallo oplossing toooperationalize Hallo machine learning-model.</span><span class="sxs-lookup"><span data-stu-id="b3c41-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="b3c41-347">Deze toepassing met de naam 'RealTimeDashboardApp' is gemaakt en geconfigureerd als onderdeel van Hallo-oplossing implementatie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="b3c41-348">de toepassing Hello voert Hallo uit:</span><span class="sxs-lookup"><span data-stu-id="b3c41-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="b3c41-349">Tooan Event Hub-instantie waar Stream Analytics Hallo gebeurtenissen in een patroon continu publiceert luistert.</span><span class="sxs-lookup"><span data-stu-id="b3c41-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="b3c41-350">![Stream Analytics query voor het publiceren van gegevens Hallo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *afbeelding 14 – Stream Analytics query voor het publiceren van Hallo gegevens tooan uitvoer Event Hub-instantie*</span><span class="sxs-lookup"><span data-stu-id="b3c41-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="b3c41-351">Voor elke gebeurtenis die deze toepassing ontvangt:</span><span class="sxs-lookup"><span data-stu-id="b3c41-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="b3c41-352">Processen Hallo gegevens gebruik van het eindpunt van de Machine Learning aanvragen en antwoorden score berekenen (RR's).</span><span class="sxs-lookup"><span data-stu-id="b3c41-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="b3c41-353">Hallo RRS eindpunt wordt automatisch gepubliceerd als onderdeel van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="b3c41-354">Hallo RRS uitvoer is gepubliceerde tooa Power BI gegevensset Hallo clientpush API's.</span><span class="sxs-lookup"><span data-stu-id="b3c41-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="b3c41-355">Dit patroon is ook van toepassing tooscenarios waaraan u een Line of Business (LoB)-toepassing met het Hallo realtime analyses flow, toointegrate voor scenario's zoals waarschuwingen, meldingen en messaging wilt.</span><span class="sxs-lookup"><span data-stu-id="b3c41-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="b3c41-356">Klik op [RealtimeDashboardApp downloaden](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio-oplossing voor aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="b3c41-357">**tooexecute hello, realtime dashboardtoepassing**</span><span class="sxs-lookup"><span data-stu-id="b3c41-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="b3c41-358">Uitpakken en lokaal opslaan ![RealtimeDashboardApp map](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *afbeelding 16 – RealtimeDashboardApp map*</span><span class="sxs-lookup"><span data-stu-id="b3c41-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="b3c41-359">Hallo toepassing RealtimeDashboardApp.exe uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b3c41-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="b3c41-360">Geldige Power BI-referenties opgeven, meld u aan en klik op accepteren</span><span class="sxs-lookup"><span data-stu-id="b3c41-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Realtime dashboard-app aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Realtime dashboard-app aanmelden tooPower BI voltooien](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="b3c41-363">*Afbeelding 17 – RealtimeDashboardApp: Aanmelden tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="b3c41-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="b3c41-364">Als u tooflush Hallo Power BI gegevensset wilt, uitvoeren Hallo RealtimeDashboardApp met Hallo 'flushdata' parameter:</span><span class="sxs-lookup"><span data-stu-id="b3c41-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="b3c41-365">Batchanalyse</span><span class="sxs-lookup"><span data-stu-id="b3c41-365">Batch analysis</span></span>
<span data-ttu-id="b3c41-366">Hallo dient dit tooshow hoe Contoso motoren hello Azure compute mogelijkheden tooharness big data toogain veel inzichten gerichtheid patroon, gebruik gedrag en vehicle health gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="b3c41-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="b3c41-367">Dit maakt het mogelijk om te:</span><span class="sxs-lookup"><span data-stu-id="b3c41-367">This makes it possible to:</span></span>

* <span data-ttu-id="b3c41-368">Hallo klantervaring te verbeteren en goedkoper maken door op te geven inzicht gerichtheid gewoonten en efficiënte aangedreven gedrag brandstof</span><span class="sxs-lookup"><span data-stu-id="b3c41-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="b3c41-369">Proactief meer over klanten en hun aangedreven patters toogovern zakelijke beslissingen te nemen en het beste Hallo op klasse-producten en services bieden</span><span class="sxs-lookup"><span data-stu-id="b3c41-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="b3c41-370">In deze oplossing ontwikkelt we Hallo metrische gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="b3c41-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="b3c41-371">**Agressief gedrag besturen**: Hallo trend van Hallo modellen, locaties, aangedreven voorwaarden en tijd van Hallo jaar toogain inzicht in agressief aangedreven patronen identificeert.</span><span class="sxs-lookup"><span data-stu-id="b3c41-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="b3c41-372">Contoso motoren kunnen deze inzichten gebruiken voor marketingcampagnes, nieuwe functies voor persoonlijke en verzekering op basis van informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="b3c41-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="b3c41-373">**Efficiënte aangedreven gedrag brandstof**: Hallo trend van Hallo modellen, locaties, aangedreven voorwaarden en tijd van Hallo jaar toogain inzicht op efficiënte aangedreven patronen brandstof identificeert.</span><span class="sxs-lookup"><span data-stu-id="b3c41-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="b3c41-374">Contoso motoren kunt deze inzichten voor marketingcampagnes, kunnen nieuwe functies en proactieve reporting toohello stuurprogramma's voor kosten van kracht worden en de omgeving beschrijvende aangedreven gewoonten.</span><span class="sxs-lookup"><span data-stu-id="b3c41-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="b3c41-375">**Intrekken van modellen**: identificeert modellen waarvoor teruggehaald operationele Hallo afwijkingsdetectie detectie machine learning-experiment</span><span class="sxs-lookup"><span data-stu-id="b3c41-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="b3c41-376">We bekijken in de details van elk van deze metrische gegevens, Hallo</span><span class="sxs-lookup"><span data-stu-id="b3c41-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="b3c41-377">**Agressieve aangedreven patroon**</span><span class="sxs-lookup"><span data-stu-id="b3c41-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="b3c41-378">Hallo vehicle signalen gepartitioneerd en diagnostische gegevens worden verwerkt in de pijplijn Hallo met de naam 'AggresiveDrivingPatternPipeline' met behulp van Hive toodetermine Hallo modellen, locatie, vehicle, besturen voorwaarden en andere parameters die vertoont agressieve aangedreven patroon.</span><span class="sxs-lookup"><span data-stu-id="b3c41-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="b3c41-379">![Agressieve aangedreven patroon werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*figuur 18 – agressieve aangedreven patroon-werkstroom*</span><span class="sxs-lookup"><span data-stu-id="b3c41-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="b3c41-380">***Agressieve aangedreven patroon Hive-query***</span><span class="sxs-lookup"><span data-stu-id="b3c41-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="b3c41-381">Hallo Hive-script met de naam 'aggresivedriving.hql"gebruikt voor het analyseren van agressieve aangedreven voorwaarde patroon bevindt zich in de map '\demo\src\connectedcar\scripts' van Hallo gedownloade zip.</span><span class="sxs-lookup"><span data-stu-id="b3c41-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="b3c41-382">Hallo combinatie van drager van verzending tandwielpictogram positie, bedient vorm status en snelheid toodetect roekeloze/agressief gedrag op basis van het patroon met hoge snelheid remmen groot wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3c41-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="b3c41-383">Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="b3c41-385">*Afbeelding 19-AggressiveDrivingPatternPipeline uitvoer*</span><span class="sxs-lookup"><span data-stu-id="b3c41-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="b3c41-386">**Brandstof efficiënt aangedreven patroon**</span><span class="sxs-lookup"><span data-stu-id="b3c41-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="b3c41-387">Hallo vehicle signalen gepartitioneerd en diagnostische gegevens worden verwerkt in Hallo-pijplijn met de naam 'FuelEfficientDrivingPatternPipeline'.</span><span class="sxs-lookup"><span data-stu-id="b3c41-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="b3c41-388">Hive is gebruikte toodetermine Hallo modellen, locatie, vehicle, aangedreven voorwaarden en andere eigenschappen die brandstof efficiënt aangedreven patroon vertonen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Fuel-Efficient aangedreven patroon](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="b3c41-390">*Afbeelding 20 – Fuel-efficient aangedreven patroon-werkstroom*</span><span class="sxs-lookup"><span data-stu-id="b3c41-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="b3c41-391">***Brandstof efficiënt aangedreven patroon Hive-query***</span><span class="sxs-lookup"><span data-stu-id="b3c41-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="b3c41-392">Hallo Hive-script met de naam 'fuelefficientdriving.hql"gebruikt voor het analyseren van agressieve aangedreven voorwaarde patroon bevindt zich in de map '\demo\src\connectedcar\scripts' van Hallo gedownloade zip.</span><span class="sxs-lookup"><span data-stu-id="b3c41-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="b3c41-393">Hallo combinatie van de drager transmission tandwielpictogram positie, bedient vorm status snelheid en accelerator vorm positie toodetect brandstof efficiënt aangedreven gedrag op basis van versnelling, remmen, wordt gebruikt en patronen te versnellen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="b3c41-394">Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="b3c41-396">*Afbeelding 21 – FuelEfficientDrivingPatternPipeline uitvoer*</span><span class="sxs-lookup"><span data-stu-id="b3c41-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="b3c41-397">**Voorspellingen intrekken**</span><span class="sxs-lookup"><span data-stu-id="b3c41-397">**Recall Predictions**</span></span>

<span data-ttu-id="b3c41-398">Hallo machine learning-experiment worden ingericht en gepubliceerd als een webservice als onderdeel van Hallo-oplossing implementatie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="b3c41-399">Hallo score-eindpunt wordt gebruikt in deze werkstroom geregistreerd als een data factory gekoppelde service en geoperationaliseerd met behulp van data factory batch activiteit voor score berekenen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Machine Learning-eindpunt](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="b3c41-401">*Afbeelding 22 – Machine learning-eindpunt is geregistreerd als een gekoppelde service in de gegevensfactory*</span><span class="sxs-lookup"><span data-stu-id="b3c41-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="b3c41-402">Hallo wordt geregistreerde gekoppelde service gebruikt in Hallo DetectAnomalyPipeline tooscore Hallo gegevens met behulp van Hallo afwijkingsdetectie detectie model.</span><span class="sxs-lookup"><span data-stu-id="b3c41-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Machine Learning score activiteit in de gegevensfactory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="b3c41-404">*Afbeelding 23: Azure Machine Learning-Batchscoreberekening activiteit in de gegevensfactory*</span><span class="sxs-lookup"><span data-stu-id="b3c41-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="b3c41-405">Er zijn enkele stappen die worden uitgevoerd in deze pijplijn voor het voorbereiden van gegevens, zodat deze kan worden geoperationaliseerd met Hallo score-webservice.</span><span class="sxs-lookup"><span data-stu-id="b3c41-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline voor het voorspellen van voertuigen terughalen vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="b3c41-407">*Afbeelding 24 – DetectAnomalyPipeline voor het voorspellen van voertuigen terughalen vereisen*</span><span class="sxs-lookup"><span data-stu-id="b3c41-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="b3c41-408">***Afwijkingsdetectie detectie Hive-query***</span><span class="sxs-lookup"><span data-stu-id="b3c41-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="b3c41-409">Zodra Hallo score berekenen is voltooid, wordt een HDInsight-activiteit is gebruikte tooprocess en Hallo statistische gegevens die zijn aangemerkt als afwijkingen door Hallo-model met een kans score van 0,60 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b3c41-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="b3c41-410">Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.</span><span class="sxs-lookup"><span data-stu-id="b3c41-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![DetectAnomalyPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="b3c41-412">*Afbeelding 25 – DetectAnomalyPipeline uitvoer*</span><span class="sxs-lookup"><span data-stu-id="b3c41-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="b3c41-413">Publiceren</span><span class="sxs-lookup"><span data-stu-id="b3c41-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="b3c41-414">Realtime analyses</span><span class="sxs-lookup"><span data-stu-id="b3c41-414">Real-time analysis</span></span>
<span data-ttu-id="b3c41-415">Een van de Hallo query's in de Stream Analytics-taak Hallo Hallo gebeurtenissen tooan uitvoer publiceert Event Hub-instantie.</span><span class="sxs-lookup"><span data-stu-id="b3c41-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Stream Analytics-taak publiceert tooan uitvoer Event Hub-instantie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="b3c41-417">*Afbeelding 26 – Stream Analytics-taak publiceert tooan uitvoer Event Hub-instantie*</span><span class="sxs-lookup"><span data-stu-id="b3c41-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Stream Analytics query toopublish toohello uitvoer Event Hub-instantie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="b3c41-419">*Afbeelding 27 – Stream Analytics query toopublish toohello uitvoer Event Hub-instantie*</span><span class="sxs-lookup"><span data-stu-id="b3c41-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="b3c41-420">Deze stroom van gebeurtenissen wordt verbruikt door Hallo die realtimedashboardapp deel van Hallo-oplossing uitmaken.</span><span class="sxs-lookup"><span data-stu-id="b3c41-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="b3c41-421">Deze toepassing maakt gebruik van de webservice van Hallo Machine Learning-reactie op aanvragen voor score berekenen voor realtime en publiceert Hallo resulterende gegevens tooa Power BI gegevensset voor verbruik.</span><span class="sxs-lookup"><span data-stu-id="b3c41-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="b3c41-422">Batchanalyse</span><span class="sxs-lookup"><span data-stu-id="b3c41-422">Batch analysis</span></span>
<span data-ttu-id="b3c41-423">Hallo Hallo batch en realtime verwerking zijn gepubliceerde toohello Azure SQL Database-tabellen voor verbruik.</span><span class="sxs-lookup"><span data-stu-id="b3c41-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="b3c41-424">Hello Azure SQL-Server, Database en Hallo tabellen worden automatisch gemaakt als onderdeel van het installatiescript Hallo.</span><span class="sxs-lookup"><span data-stu-id="b3c41-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Batch verwerking resultaten kopiëren toodata datamart werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="b3c41-426">*Afbeelding 28 – batchverwerking resultaten kopiëren toodata datamart werkstroom*</span><span class="sxs-lookup"><span data-stu-id="b3c41-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Stream Analytics-taak publiceert toodata datamart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="b3c41-428">*Afbeelding 29 – Stream Analytics-taak publiceert toodata datamart*</span><span class="sxs-lookup"><span data-stu-id="b3c41-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Datamart-instelling van Data in Stream Analytics-taak](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="b3c41-430">*Afbeelding 30 – datamart instellen in Stream Analytics-taak*</span><span class="sxs-lookup"><span data-stu-id="b3c41-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="b3c41-431">Gebruiken</span><span class="sxs-lookup"><span data-stu-id="b3c41-431">Consume</span></span>
<span data-ttu-id="b3c41-432">Power BI biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="b3c41-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="b3c41-433">Klik hier voor gedetailleerde instructies over het instellen van Hallo Power BI-rapporten en het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b3c41-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="b3c41-434">Hallo laatste dashboard ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b3c41-434">hello final dashboard looks like this:</span></span>

![Power BI-dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="b3c41-436">*Afbeelding 31 - Power BI-Dashboard*</span><span class="sxs-lookup"><span data-stu-id="b3c41-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="b3c41-437">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b3c41-437">Summary</span></span>
<span data-ttu-id="b3c41-438">Dit document bevat een gedetailleerde inzoomen Hallo Vehicle telemetrie Analytics-oplossing.</span><span class="sxs-lookup"><span data-stu-id="b3c41-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="b3c41-439">Dit patroon met een lambda-architectuur voor gepresenteerd realtime en batch-analyses met voorspellingen en acties.</span><span class="sxs-lookup"><span data-stu-id="b3c41-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="b3c41-440">Dit patroon van toepassing is tooa breed scala aan gebruiksvoorbeelden waarvoor hot pad (real-time) en analyses van koude pad (batch).</span><span class="sxs-lookup"><span data-stu-id="b3c41-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

