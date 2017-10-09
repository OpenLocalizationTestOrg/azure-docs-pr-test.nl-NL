---
title: maken van RemoteApp hybride verzamelingen aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot RemoteApp hybride verzameling maken van fouten
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="ac3dd-103">Problemen met het maken van hybride Azure RemoteApp-verzamelingen oplossen</span><span class="sxs-lookup"><span data-stu-id="ac3dd-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac3dd-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ac3dd-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ac3dd-106">Een hybride verzameling wordt gehost in en slaat gegevens op in hello Azure-cloud, maar ook kiest, kunnen gebruikers toegang tot gegevens en resources die zijn opgeslagen op uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="ac3dd-107">Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="ac3dd-108">U kunt een hybride verzameling die gebruikmaakt van een bestaand virtueel netwerk in Azure implementeren of u kunt een nieuw virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="ac3dd-109">U wordt aangeraden dat u maakt of gebruik een virtueel netwerksubnet met een CIDR-bereik groot genoeg zijn voor toekomstige groei van de verwachte voor Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="ac3dd-110">Uw verzameling nog niet hebt worden gemaakt?</span><span class="sxs-lookup"><span data-stu-id="ac3dd-110">Haven't created your collection yet?</span></span> <span data-ttu-id="ac3dd-111">Zie [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) voor Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="ac3dd-112">Als u problemen ondervindt bij het maken van de verzameling, of als Hallo verzameling niet werkt, u denkt dat het Hallo-manier moet, Raadpleeg Hallo informatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="ac3dd-113">Uw installatiekopie is ongeldig</span><span class="sxs-lookup"><span data-stu-id="ac3dd-113">Your image is invalid</span></span>
<span data-ttu-id="ac3dd-114">Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure tooprovision uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon Hallo voldoet niet aan [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="ac3dd-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="ac3dd-115">Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer toocreate uw verzameling opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="ac3dd-116">Heeft uw VNET netwerkbeveiligingsgroepen die zijn gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ac3dd-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="ac3dd-117">Als u netwerkbeveiligingsgroepen die zijn gedefinieerd op Hallo subnet die u voor uw verzameling gebruikt hebt, controleert u of deze [URL's en poorten](remoteapp-ports.md) toegankelijk vanuit het subnet zijn.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="ac3dd-118">U kunt extra netwerk beveiliging groepen toohello VM's geïmplementeerd door u op Hallo-subnet voor meer controle toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="ac3dd-119">Gebruikt u uw eigen DNS-servers?</span><span class="sxs-lookup"><span data-stu-id="ac3dd-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="ac3dd-120">En zijn ze toegankelijk is vanaf uw VNET subnet?</span><span class="sxs-lookup"><span data-stu-id="ac3dd-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="ac3dd-121">U hebt ervoor toomake-Hallo DNS-servers in uw VNET altijd actief zijn en altijd kunnen tooresolve Hallo virtuele machines die worden gehost in Hallo VNET.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="ac3dd-122">Gebruik geen Google DNS voor deze.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="ac3dd-123">Voor hybride verzamelingen gebruikt u uw eigen DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="ac3dd-124">U ze in uw network-configuratieschema of via de beheerportal Hallo bij het maken van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="ac3dd-125">DNS-servers worden gebruikt in Hallo volgorde waarin ze worden opgegeven in een failover-manier (als tegengestelde tooround robin).</span><span class="sxs-lookup"><span data-stu-id="ac3dd-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="ac3dd-126">Raadpleeg het te[naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake ervoor dat uw DNS-servers zijn geconfigureerd correcly.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="ac3dd-127">Zorg ervoor dat Hallo DNS-servers voor uw verzameling zijn toegankelijk en beschikbaar vanuit Hallo VNET subnet dat u hebt opgegeven voor deze verzameling.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="ac3dd-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ac3dd-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Uw DNS definiëren](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="ac3dd-130">Gebruikt u een Active Directory-domeincontroller in uw verzameling?</span><span class="sxs-lookup"><span data-stu-id="ac3dd-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="ac3dd-131">Op dit moment slechts één Active Directory-domein gekoppeld aan Azure RemoteApp zijn.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="ac3dd-132">Hallo hybride verzameling ondersteunt alleen Azure Active Directory-accounts die zijn gesynchroniseerd met DirSync-hulpprogramma op een Windows Server Active Directory-implementatie; in het bijzonder hetzij gesynchroniseerd met de optie Wachtwoordsynchronisatie Hallo of gesynchroniseerd met Active Directory Federation Services (AD FS) federation geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="ac3dd-133">U moet een aangepast domein die overeenkomt met de Hallo UPN-achtervoegsel voor domein voor uw domein lokale toocreate en Active directory-integratie instellen.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="ac3dd-134">Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="ac3dd-135">Zorg ervoor dat Hallo domein details opgegeven geldig zijn en Hallo domeincontroller bereikbaar is vanaf Hallo die VM in Hallo subnet dat wordt gebruikt voor Azure RemoteApp gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="ac3dd-136">Controleer ook of Hallo service-account opgegeven referenties hebben machtigingen tooadd computers toohello opgegeven domein en dat de naam van de AD Hallo opgegeven kan worden opgelost van Hallo DNS in het Hallo VNET.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="ac3dd-137">Welke domeinnaam hebt u opgegeven tijdens het maken van uw verzameling?</span><span class="sxs-lookup"><span data-stu-id="ac3dd-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="ac3dd-138">Hallo domeinnaam u hebt gemaakt of toegevoegd moet een interne domeinnaam (niet uw Azure AD domain name) en moet worden omgezet DNS-indeling (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="ac3dd-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="ac3dd-139">Bijvoorbeeld: u hebt een interne Active Directory-naam (contoso.local) en een Active Directory-UPN (contoso.com) - u hebt toouse Hallo interne naam bij het maken van uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="ac3dd-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

