---
title: Sessie-affiniteit met behulp van aaaEnable Hallo Azure Toolkit voor Eclipse
description: Meer informatie over hoe Azure-Toolkit voor Eclipse tooenable sessie affiniteit met Hallo.
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="b8f4c-103">Sessie-affiniteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="b8f4c-103">Enable Session Affinity</span></span>
<span data-ttu-id="b8f4c-104">Binnen hello Azure Toolkit voor Eclipse, kunt u de affiniteit van HTTP-sessie of 'een tijdelijke sessies', voor uw rollen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="b8f4c-105">Hallo volgende afbeelding toont Hallo **Load Balancing** eigenschappen dialoogvenster gebruikt tooenable Hallo sessie affiniteit functie:</span><span class="sxs-lookup"><span data-stu-id="b8f4c-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="b8f4c-106">sessie-affiniteit tooenable voor uw rol</span><span class="sxs-lookup"><span data-stu-id="b8f4c-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="b8f4c-107">Met de rechtermuisknop op het Hallo-rol in de Eclipse-Project Explorer, klikt u op **Azure**, en klik vervolgens op **Load Balancing**.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="b8f4c-108">In Hallo **eigenschappen WorkerRole1 Load Balancing** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="b8f4c-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="b8f4c-109">a.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-109">a.</span></span> <span data-ttu-id="b8f4c-110">Controleer **inschakelen HTTP-sessie affiniteit (een tijdelijke sessies) voor deze rol.**</span><span class="sxs-lookup"><span data-stu-id="b8f4c-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="b8f4c-111">b.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-111">b.</span></span> <span data-ttu-id="b8f4c-112">Voor **invoer eindpunt toouse**, selecteert u bijvoorbeeld een toouse invoereindpunt **http (openbare: 80, persoonlijke: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="b8f4c-113">Uw toepassing, moet dit eindpunt gebruiken als de HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="b8f4c-114">U kunt meerdere eindpunten inschakelen voor uw rol, maar kunt u slechts één van deze toosupport een tijdelijke sessies.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="b8f4c-115">c.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-115">c.</span></span> <span data-ttu-id="b8f4c-116">Uw toepassing opnieuw bouwt.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-116">Rebuild your application.</span></span>

<span data-ttu-id="b8f4c-117">Eenmaal is ingeschakeld, hebt u meer dan één rolexemplaar, HTTP-aanvragen die afkomstig zijn van een bepaalde client blijft wordt verwerkt door Hallo dezelfde rolinstantie.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="b8f4c-118">Hallo Eclipse Toolkit maakt dit mogelijk door een speciale IIS-module Application Request Routing (ARR) in elk van uw rolinstanties installeren.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="b8f4c-119">ARR wordt omgeleid toohello juiste rolinstantie voor HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="b8f4c-120">Hallo toolkit automatisch geselecteerd Hallo eindpunt opnieuw geconfigureerd zodat de binnenkomende HTTP-verkeer Hallo eerste gerouteerde toohello ARR software.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="b8f4c-121">Hallo toolkit maakt ook een nieuwe interne eindpunt dat uw Java-server is geconfigureerd toolisten aan.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="b8f4c-122">Hallo eindpunt dat wordt gebruikt door ARR tooreroute Hallo HTTP-verkeer toohello geschikte rolexemplaar is.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="b8f4c-123">Op deze manier fungeert elke rolinstantie in uw implementatie meerdere exemplaren als omgekeerde proxy voor alle andere exemplaren Hallo inschakelen van een tijdelijke sessies.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="b8f4c-124">Opmerkingen over de affiniteit van sessie</span><span class="sxs-lookup"><span data-stu-id="b8f4c-124">Notes about session affinity</span></span>
* <span data-ttu-id="b8f4c-125">Sessie-affiniteit werkt niet in Hallo rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="b8f4c-126">Hallo-instellingen kunnen worden toegepast in de rekenemulator Hallo geen conflicten ontstaan met uw buildproces of compute-emulator worden uitgevoerd, maar Hallo zelf functie werkt niet binnen het Hallo-rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="b8f4c-127">Inschakelen van sessie-affiniteit leidt tot een toename van Hallo en de hoeveelheid schijfruimte in beslag genomen door uw implementatie in Azure, zoals aanvullende software wordt gedownload en geïnstalleerd in uw rolinstanties wanneer uw service wordt gestart in hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="b8f4c-128">Hallo tijd tooinitialize die elke rol zal langer duren.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="b8f4c-129">Interne eindpunt, toofunction als een rerouter verkeer zoals hierboven vermeld, worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b8f4c-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="b8f4c-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b8f4c-130">See Also</span></span>
<span data-ttu-id="b8f4c-131">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8f4c-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="b8f4c-132">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8f4c-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="b8f4c-133">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8f4c-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="b8f4c-134">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b8f4c-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
