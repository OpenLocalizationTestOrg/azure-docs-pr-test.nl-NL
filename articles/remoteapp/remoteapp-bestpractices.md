---
title: Aanbevolen procedures voor Azure RemoteApp | Microsoft Docs
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
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="8e9b3-103">Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8e9b3-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8e9b3-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8e9b3-105">Lees de [aankondiging](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="8e9b3-106">De volgende informatie kunt u configureren en gebruiken van Azure RemoteApp productief zijn.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="8e9b3-107">Connectiviteit</span><span class="sxs-lookup"><span data-stu-id="8e9b3-107">Connectivity</span></span>
* <span data-ttu-id="8e9b3-108">Gebruik altijd de meest recente clientversie.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-108">Always use the latest client version.</span></span> <span data-ttu-id="8e9b3-109">Met behulp van de oudere clients, kan dit leiden tot problemen met de netwerkverbinding en andere verslechterde ervaringen.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="8e9b3-110">Inschakelen van automatische toepassing van updates voor uw apparaat zorgt ervoor dat er altijd de nieuwste client is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="8e9b3-111">Gebruik altijd de meest stabiel en betrouwbaar internetverbinding beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="8e9b3-112">Proxyverbinding ondersteund gebruik alleen voor optimale connectiviteit met hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="8e9b3-113">De SOCKS-proxy wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="8e9b3-114">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="8e9b3-114">Applications</span></span>
* <span data-ttu-id="8e9b3-115">Opslaan en sluiten van RemoteApp-toepassingen wanneer u klaar bent met de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="8e9b3-116">De toepassing niet sluiten, kan dit leiden tot verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="8e9b3-117">Valideren van aangepaste toepassingen voordat u ze in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="8e9b3-118">Dit omvat zodat ze werken op een platform meerdere sessie en onnodige resources, zoals geheugen en CPU die mogelijk een andere gebruiker in dezelfde verzameling stilleggen niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="8e9b3-119">Download voor informatie en bekijk de [toepassing compatibiliteit met aanbevolen procedures voor extern bureaublad-Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="8e9b3-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="8e9b3-120">Configuratie en beheer</span><span class="sxs-lookup"><span data-stu-id="8e9b3-120">Configuration and management</span></span>
* <span data-ttu-id="8e9b3-121">Uw sjablooninstallatiekopieën up-to-date te houden, software-updates en andere kritieke updates installeren, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="8e9b3-122">Dit zorgt ervoor dat als Azure RemoteApp auto-schalen om te voldoen aan de capaciteit, elk exemplaar is een patch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="8e9b3-123">Zorg ervoor dat uw implementatie van Active Directory Federation Services (AD FS) is veilig en betrouwbaar.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="8e9b3-124">Anders mislukken client verificaties, voorkomen dat gebruikers toegang tot Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="8e9b3-125">Configureer sjablooninstallatiekopieën met geïnstalleerde toepassingen, functies of onderdelen zodanig in dat ze staatloze.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="8e9b3-126">Ze moeten niet afhankelijk van alle exemplaren van de virtuele machines in een RemoteApp-service wordt in een permanente status.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="8e9b3-127">Alle gebruikersgegevens opslaan in gebruikersprofielen of andere aan de service, externe opslaglocaties, zoals lokale bestand shares of OneDrive.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="8e9b3-128">Gedeelde gegevens opslaan in opslaglocaties buiten de service, zoals lokale bestand shares of OneDrive.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="8e9b3-129">Alle systeeminstellingen configureren in de sjablooninstallatiekopie in plaats van op afzonderlijke virtuele machines in een service.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="8e9b3-130">Schakel automatische software-updates voor gepubliceerde toepassingen - in plaats daarvan handmatig toepassen op de sjablooninstallatiekopie van de en te testen voordat u uit de sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="8e9b3-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

