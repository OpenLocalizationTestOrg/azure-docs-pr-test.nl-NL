---
title: aanbevolen procedures voor aaaAzure RemoteApp | Microsoft Docs
description: Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="eb44a-103">Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="eb44a-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eb44a-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="eb44a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="eb44a-105">Lees Hallo [aankondiging](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb44a-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="eb44a-106">Hallo volgende informatie kunt u configureren en gebruiken van Azure RemoteApp productief zijn.</span><span class="sxs-lookup"><span data-stu-id="eb44a-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="eb44a-107">Connectiviteit</span><span class="sxs-lookup"><span data-stu-id="eb44a-107">Connectivity</span></span>
* <span data-ttu-id="eb44a-108">Gebruik altijd de meest recente clientversie Hallo.</span><span class="sxs-lookup"><span data-stu-id="eb44a-108">Always use hello latest client version.</span></span> <span data-ttu-id="eb44a-109">Met behulp van de oudere clients, kan dit leiden tot problemen met de netwerkverbinding en andere verslechterde ervaringen.</span><span class="sxs-lookup"><span data-stu-id="eb44a-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="eb44a-110">Inschakelen van automatische toepassing van updates voor uw apparaat zorgt ervoor dat de meest recente client Hallo altijd is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="eb44a-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="eb44a-111">Gebruik altijd Hallo stabiel en meest betrouwbare internet verbinding beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="eb44a-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="eb44a-112">Proxyverbinding ondersteund gebruik alleen voor optimale connectiviteit met hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="eb44a-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="eb44a-113">Hallo SOCKS-proxy wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="eb44a-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="eb44a-114">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="eb44a-114">Applications</span></span>
* <span data-ttu-id="eb44a-115">Opslaan en sluiten van RemoteApp-toepassingen wanneer u klaar bent met de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="eb44a-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="eb44a-116">Niet sluiten Hallo toepassing kan leiden tot verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="eb44a-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="eb44a-117">Valideren van aangepaste toepassingen voordat u ze in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="eb44a-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="eb44a-118">Dit omvat zodat ze werken op een platform meerdere sessie en onnodige resources, zoals geheugen en CPU die mogelijk een andere gebruiker op Hallo stilleggen niet gebruiken dezelfde verzameling.</span><span class="sxs-lookup"><span data-stu-id="eb44a-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="eb44a-119">Voor meer informatie, downloaden en bekijken Hallo [toepassing compatibiliteit met aanbevolen procedures voor extern bureaublad-Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="eb44a-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="eb44a-120">Configuratie en beheer</span><span class="sxs-lookup"><span data-stu-id="eb44a-120">Configuration and management</span></span>
* <span data-ttu-id="eb44a-121">Houd uw sjablooninstallatiekopieën up toodate, software-updates en andere kritieke updates installeren, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="eb44a-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="eb44a-122">Dit zorgt ervoor dat als Azure RemoteApp auto-schalen toomeet uw capaciteit, elk exemplaar is hersteld.</span><span class="sxs-lookup"><span data-stu-id="eb44a-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="eb44a-123">Zorg ervoor dat uw implementatie van Active Directory Federation Services (AD FS) is veilig en betrouwbaar.</span><span class="sxs-lookup"><span data-stu-id="eb44a-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="eb44a-124">Anders mislukken client verificaties, voorkomen dat gebruikers toegang tot Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="eb44a-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="eb44a-125">Configureer sjablooninstallatiekopieën met geïnstalleerde toepassingen, functies of onderdelen zodanig in dat ze staatloze.</span><span class="sxs-lookup"><span data-stu-id="eb44a-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="eb44a-126">Ze moeten niet afhankelijk van alle exemplaren van Hallo virtuele machines in een RemoteApp-service wordt in een permanente status.</span><span class="sxs-lookup"><span data-stu-id="eb44a-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="eb44a-127">Alle gebruikersgegevens opslaan in gebruikersprofielen of andere locaties externe toohello opslagservice, zoals lokale bestand shares of OneDrive.</span><span class="sxs-lookup"><span data-stu-id="eb44a-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="eb44a-128">Gedeelde gegevens opslaan in opslagservice locaties externe toohello, zoals lokale bestand shares of OneDrive.</span><span class="sxs-lookup"><span data-stu-id="eb44a-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="eb44a-129">Configureer alle systeeminstellingen in Hallo-sjablooninstallatiekopie in plaats van op afzonderlijke virtuele machines in een service.</span><span class="sxs-lookup"><span data-stu-id="eb44a-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="eb44a-130">Schakel automatische software-updates voor gepubliceerde toepassingen - in plaats daarvan deze handmatig toepassen toohello sjablooninstallatiekopie en te testen voordat u met Hallo-sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="eb44a-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

