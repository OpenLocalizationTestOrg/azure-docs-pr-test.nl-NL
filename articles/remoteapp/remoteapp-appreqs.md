---
title: aaaApp vereisten voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over de vereisten van de Hallo voor apps die u wilt dat toouse in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="dae0c-103">App-vereisten</span><span class="sxs-lookup"><span data-stu-id="dae0c-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dae0c-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="dae0c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dae0c-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dae0c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dae0c-106">Azure RemoteApp biedt ondersteuning voor streaming 32-bits of 64-bits Windows-toepassingen van een installatiekopie van Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="dae0c-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="dae0c-107">De meeste bestaande 32-bits of 64-bits Windows-toepassingen uitvoeren 'als zodanig' in Azure RemoteApp (extern bureaublad-Services of voorheen bekend als Terminal Services) omgeving.</span><span class="sxs-lookup"><span data-stu-id="dae0c-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="dae0c-108">Echter, er is een verschil tussen uitgevoerd en goed - sommige toepassingen goed werken en ook niet uitvoeren terwijl andere niet.</span><span class="sxs-lookup"><span data-stu-id="dae0c-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="dae0c-109">Hallo volgende informatie bevat richtlijnen voor het ontwikkelen van toepassingen in een omgeving met extern bureaublad-Services en tooensure compatibiliteit testen.</span><span class="sxs-lookup"><span data-stu-id="dae0c-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="dae0c-110">Tip: Momenteel niets over het maken van voorbeelden werkt van apps voor u.</span><span class="sxs-lookup"><span data-stu-id="dae0c-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="dae0c-111">Hier ziet u nieuwe onderwerpen die betrekking hebben met behulp van Microsoft Access, QuickBooks en App-V in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="dae0c-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="dae0c-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dae0c-112">Requirements</span></span>
<span data-ttu-id="dae0c-113">Deze drie vereisten helpen als gevolgd, uw toepassing goed in RemoteApp worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="dae0c-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="dae0c-114">Toepassingen die voldoen aan alle [certificeringsvereisten voor Windows desktop-apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) en te voldoen[extern bureaublad-Services richtlijnen programming](https://msdn.microsoft.com/library/aa383490.aspx) heeft volledige compatibiliteit met RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="dae0c-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="dae0c-115">Toepassingen moeten nooit gegevens lokaal opslaan op Hallo afbeeldings- of RemoteApp-exemplaren die verloren kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="dae0c-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="dae0c-116">Nadat u een RemoteApp-collectie gemaakt, Hallo exemplaren worden gekloond en staatloze zijn en mag alleen toepassingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="dae0c-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="dae0c-117">Gegevens opslaan in een externe bron of binnen Hallo gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="dae0c-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="dae0c-118">Aangepaste installatiekopieën mag nooit bevatten gegevens die verbroken worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="dae0c-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="dae0c-119">Uw apps testen</span><span class="sxs-lookup"><span data-stu-id="dae0c-119">Testing your apps</span></span>
<span data-ttu-id="dae0c-120">Gebruik deze stappen tootesting toepassingen:</span><span class="sxs-lookup"><span data-stu-id="dae0c-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="dae0c-121">Windows Server 2012 R2 en uw toepassing geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="dae0c-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="dae0c-122">Extern bureaublad inschakelen</span><span class="sxs-lookup"><span data-stu-id="dae0c-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="dae0c-123">Maak twee gebruikersaccounts GebruikerA en gebruiker b, beide gebruiker accounts toohello extern bureaublad-beveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dae0c-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="dae0c-124">Meerdere sessie compatibiliteit controleren door het opstellen van twee gelijktijdige RDS sessies toohello PC tijdens het Hallo-toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="dae0c-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="dae0c-125">App-gedrag valideren</span><span class="sxs-lookup"><span data-stu-id="dae0c-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="dae0c-126">Richtlijnen voor het ontwikkelen van toepassing</span><span class="sxs-lookup"><span data-stu-id="dae0c-126">Application development guidelines</span></span>
<span data-ttu-id="dae0c-127">Hallo volgen richtlijnen voor het ontwikkelen van toepassingen voor RemoteApp gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dae0c-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="dae0c-128">Meerdere gebruikers</span><span class="sxs-lookup"><span data-stu-id="dae0c-128">Multiple users</span></span>
* <span data-ttu-id="dae0c-129">Installeren van een [toepassing voor één gebruiker ](https://msdn.microsoft.com/library/aa380661.aspx)problemen kunnen veroorzaken in een omgeving.</span><span class="sxs-lookup"><span data-stu-id="dae0c-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="dae0c-130">Toepassingen moeten [gebruikersspecifieke informatie opslaan](https://msdn.microsoft.com/library/aa383452.aspx) in gebruikersspecifieke locaties, afzonderlijk van globale gegevens die van toepassing is tooall gebruikers.</span><span class="sxs-lookup"><span data-stu-id="dae0c-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="dae0c-131">RemoteApp maakt gebruik van meerdere [naamruimten voor objecten van de kernel](https://msdn.microsoft.com/library/aa382954.aspx); een globale naamruimte wordt hoofdzakelijk gebruikt door services in de client/server-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dae0c-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="dae0c-132">Het is niet veilig tooassume die computernaam of het Hallo Hallo [IP-adres](https://msdn.microsoft.com/library/aa382942.aspx) toegewezen toohello computer zijn gekoppeld aan een enkele gebruiker omdat meerdere gebruikers kunnen worden geregistreerd op tegelijkertijd tooa Remote Desktop Session Host (extern bureaublad-sessie Host)-server.</span><span class="sxs-lookup"><span data-stu-id="dae0c-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="dae0c-133">Prestaties</span><span class="sxs-lookup"><span data-stu-id="dae0c-133">Performance</span></span>
* <span data-ttu-id="dae0c-134">Schakel [grafische effecten](https://msdn.microsoft.com/library/aa380822.aspx) voordat u uw app tooRemoteApp toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dae0c-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="dae0c-135">toomaximize CPU-beschikbaarheid voor alle gebruikers uitschakelen [taken op de achtergrond ](https://msdn.microsoft.com/library/aa380665.aspx) of maken van efficiënte achtergrondtaken die geen resource-intensief.</span><span class="sxs-lookup"><span data-stu-id="dae0c-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="dae0c-136">U moet afstemmen en saldo toepassing [gebruik thread](https://msdn.microsoft.com/library/aa383520.aspx) voor een omgeving met meerdere gebruikers, met meerdere processors.</span><span class="sxs-lookup"><span data-stu-id="dae0c-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="dae0c-137">toooptimize prestaties, het is raadzaam om voor toepassingen te[detecteren](https://msdn.microsoft.com/library/aa380798.aspx) of er in een clientsessie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dae0c-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

