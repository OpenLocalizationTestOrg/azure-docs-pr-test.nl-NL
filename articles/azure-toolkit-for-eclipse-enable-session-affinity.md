---
title: Sessie-affiniteit met de Azure-Toolkit voor Eclipse inschakelen
description: Informatie over het inschakelen van sessie-affiniteit met de Azure-Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="86318-103">Sessie-affiniteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="86318-103">Enable Session Affinity</span></span>
<span data-ttu-id="86318-104">Binnen de Azure-werkset voor Eclipse, kunt u de affiniteit van HTTP-sessie of 'een tijdelijke sessies', voor uw functies inschakelen.</span><span class="sxs-lookup"><span data-stu-id="86318-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="86318-105">De volgende afbeelding toont de **Load Balancing** eigenschappenvenster gebruikt voor het inschakelen van de functie van de affiniteit sessie:</span><span class="sxs-lookup"><span data-stu-id="86318-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="86318-106">Sessie-affiniteit voor uw rol inschakelen</span><span class="sxs-lookup"><span data-stu-id="86318-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="86318-107">Met de rechtermuisknop op de rol in de Eclipse-Project Explorer, klikt u op **Azure**, en klik vervolgens op **Load Balancing**.</span><span class="sxs-lookup"><span data-stu-id="86318-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="86318-108">In de **eigenschappen WorkerRole1 Load Balancing** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="86318-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="86318-109">a.</span><span class="sxs-lookup"><span data-stu-id="86318-109">a.</span></span> <span data-ttu-id="86318-110">Controleer **inschakelen HTTP-sessie affiniteit (een tijdelijke sessies) voor deze rol.**</span><span class="sxs-lookup"><span data-stu-id="86318-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="86318-111">b.</span><span class="sxs-lookup"><span data-stu-id="86318-111">b.</span></span> <span data-ttu-id="86318-112">Voor **invoer eindpunt te gebruiken**, selecteert u een invoereindpunt moet worden gebruikt, bijvoorbeeld **http (openbare: 80, persoonlijke: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="86318-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="86318-113">Uw toepassing, moet dit eindpunt gebruiken als de HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="86318-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="86318-114">U kunt meerdere eindpunten inschakelen voor uw rol, maar u kunt slechts één van deze ter ondersteuning van een tijdelijke sessies selecteren.</span><span class="sxs-lookup"><span data-stu-id="86318-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="86318-115">c.</span><span class="sxs-lookup"><span data-stu-id="86318-115">c.</span></span> <span data-ttu-id="86318-116">Uw toepassing opnieuw bouwt.</span><span class="sxs-lookup"><span data-stu-id="86318-116">Rebuild your application.</span></span>

<span data-ttu-id="86318-117">Eenmaal is ingeschakeld, hebt u meer dan één rolexemplaar, blijven HTTP-aanvragen die afkomstig zijn van een bepaalde client wordt verwerkt door dezelfde rolinstantie.</span><span class="sxs-lookup"><span data-stu-id="86318-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="86318-118">De Eclipse-Toolkit maakt dit mogelijk door een speciale IIS-module Application Request Routing (ARR) in elk van uw rolinstanties installeren.</span><span class="sxs-lookup"><span data-stu-id="86318-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="86318-119">ARR wordt omgeleid naar de juiste rolinstantie HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="86318-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="86318-120">De toolkit opnieuw automatisch geconfigureerd voor het geselecteerde eindpunt, zodat de binnenkomende HTTP-verkeer wordt eerst doorgestuurd naar de ARR-software.</span><span class="sxs-lookup"><span data-stu-id="86318-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="86318-121">De toolkit maakt ook een nieuwe interne eindpunt die uw Java-server is geconfigureerd om te luisteren naar.</span><span class="sxs-lookup"><span data-stu-id="86318-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="86318-122">Dit is het eindpunt dat wordt gebruikt door ARR de HTTP-verkeer naar de juiste instantie worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="86318-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="86318-123">Op deze manier elke rolinstantie in uw implementatie meerdere exemplaren fungeert als omgekeerde proxy voor alle andere gevallen belden inschakelen van een tijdelijke sessies.</span><span class="sxs-lookup"><span data-stu-id="86318-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="86318-124">Opmerkingen over de affiniteit van sessie</span><span class="sxs-lookup"><span data-stu-id="86318-124">Notes about session affinity</span></span>
* <span data-ttu-id="86318-125">Sessie-affiniteit werkt niet in de rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="86318-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="86318-126">De instellingen kunnen worden toegepast in de rekenemulator geen conflicten ontstaan met uw buildproces of compute-emulator worden uitgevoerd, maar de functie zelf werkt niet binnen de rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="86318-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="86318-127">Inschakelen van sessie-affiniteit leidt tot een toename van de hoeveelheid schijfruimte in beslag genomen door uw implementatie in Azure, zoals extra software worden gedownload en geïnstalleerd in uw rolinstanties wanneer uw service wordt gestart in de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="86318-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="86318-128">De tijd voor het initialiseren van elke rol zal langer duren.</span><span class="sxs-lookup"><span data-stu-id="86318-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="86318-129">Een interne eindpunt, zoals hierboven vermeld, worden gebruikt als een rerouter verkeer wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="86318-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="86318-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="86318-130">See Also</span></span>
<span data-ttu-id="86318-131">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="86318-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="86318-132">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="86318-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="86318-133">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="86318-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="86318-134">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="86318-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
