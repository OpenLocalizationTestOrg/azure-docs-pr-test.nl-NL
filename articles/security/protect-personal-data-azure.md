---
title: aaaProtect persoonlijke gegevens in Microsoft Azure | Microsoft Docs
description: Eerst artikel in een serie artikelen toohelp gebruikt u Azure tooprotect persoonlijke gegevens
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="8c4e5-103">Beveiligen van persoonlijke gegevens in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8c4e5-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="8c4e5-104">Dit artikel bevat een reeks van artikelen die u helpen bij gebruik van Azure-beveiliging technologieën en services tooprotect persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="8c4e5-105">Dit is een belangrijke vereiste voor vele zakelijke en bedrijfstak naleving en beheeracties initiatieven.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="8c4e5-106">Hallo-scenario, probleem-instructie en het bedrijf doelstellingen zijn opgenomen hier.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="8c4e5-107">Scenario en probleem vereisen</span><span class="sxs-lookup"><span data-stu-id="8c4e5-107">Scenario and problem statement</span></span>

<span data-ttu-id="8c4e5-108">Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="8c4e5-109">toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="8c4e5-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="8c4e5-110">Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="8c4e5-111">Dit kan werknemer en/of klantgegevens zoals omvatten:</span><span class="sxs-lookup"><span data-stu-id="8c4e5-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="8c4e5-112">adressen</span><span class="sxs-lookup"><span data-stu-id="8c4e5-112">addresses</span></span>
- <span data-ttu-id="8c4e5-113">telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="8c4e5-113">phone numbers</span></span>
- <span data-ttu-id="8c4e5-114">BTW-id 's</span><span class="sxs-lookup"><span data-stu-id="8c4e5-114">tax identification numbers</span></span>
- <span data-ttu-id="8c4e5-115">medische informatie</span><span class="sxs-lookup"><span data-stu-id="8c4e5-115">medical information</span></span>
- <span data-ttu-id="8c4e5-116">creditcardgegevens</span><span class="sxs-lookup"><span data-stu-id="8c4e5-116">credit card information</span></span>

<span data-ttu-id="8c4e5-117">Hallo bedrijf moet Hallo privacy van werknemers en klanten gegevens beveiligen tijdens het maken van gegevens toegankelijk toothose afdelingen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="8c4e5-118">(zoals salarissen en -reserveringen afdelingen)</span><span class="sxs-lookup"><span data-stu-id="8c4e5-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="8c4e5-119">Bedrijfsdoelstellingen</span><span class="sxs-lookup"><span data-stu-id="8c4e5-119">Company goals</span></span> 

- <span data-ttu-id="8c4e5-120">Gegevensbronnen met persoonlijke gegevens worden versleuteld wanneer die zich in de cloud-opslag.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="8c4e5-121">Persoonlijke gegevens die wordt overgebracht van één locatie tooanother tijdens in transit versleuteld.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="8c4e5-122">Dit is de waarde true wanneer Hallo gegevens via Hallo virtueel netwerk of via Internet Hallo onderweg tussen het bedrijfsdatacenter Hallo en hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="8c4e5-123">Vertrouwelijkheid en integriteit van persoonlijke gegevens wordt beschermd tegen onbevoegde toegang door sterke identiteits- en access control-technologieën.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="8c4e5-124">Persoonlijke gegevens beveiligd tegen blootstelling via inbreuk op de gegevens via bewaking voor beveiligingsproblemen en bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="8c4e5-125">Hallo beveiligingsstatus van de Azure-services die opslaan of persoonlijke gegevens verzenden wordt beoordeeld tooidentify verkoopkansen toobetter persoonlijke gegevens te beschermen.</span><span class="sxs-lookup"><span data-stu-id="8c4e5-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="8c4e5-126">Data protection richtlijnen</span><span class="sxs-lookup"><span data-stu-id="8c4e5-126">Data protection guidance</span></span>

<span data-ttu-id="8c4e5-127">Hallo volgende artikelen bevatten technische hoe-tooguidance waarmee u bereiken Hallo beveiliginsgdoelen op persoonlijke gegevens die hierboven worden genoemd:</span><span class="sxs-lookup"><span data-stu-id="8c4e5-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="8c4e5-128">Azure versleutelingstechnologieën</span><span class="sxs-lookup"><span data-stu-id="8c4e5-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="8c4e5-129">Azure versleutelingstechnologieën</span><span class="sxs-lookup"><span data-stu-id="8c4e5-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="8c4e5-130">Azure technologieën voor identiteits- en toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="8c4e5-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="8c4e5-131">Beveiligingstechnologieën Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="8c4e5-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="8c4e5-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8c4e5-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="8c4e5-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c4e5-133">Next steps</span></span>

- [<span data-ttu-id="8c4e5-134">Azure-beveiliging informatie Site</span><span class="sxs-lookup"><span data-stu-id="8c4e5-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="8c4e5-135">Microsoft Trust Center</span><span class="sxs-lookup"><span data-stu-id="8c4e5-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="8c4e5-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8c4e5-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="8c4e5-137">Blog van het Azure-beveiligingsteam</span><span class="sxs-lookup"><span data-stu-id="8c4e5-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="8c4e5-138">Azure.com Blog - beveiliging</span><span class="sxs-lookup"><span data-stu-id="8c4e5-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
