---
title: Maken van RemoteApp hybride verzamelingen oplossen | Microsoft Docs
description: Meer informatie over het oplossen van fouten bij RemoteApp hybride verzameling maken
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
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="9db7a-103">Problemen met het maken van hybride Azure RemoteApp-verzamelingen oplossen</span><span class="sxs-lookup"><span data-stu-id="9db7a-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9db7a-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="9db7a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9db7a-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9db7a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9db7a-106">Een hybride verzameling wordt gehost in en slaat gegevens op in de Azure-cloud, maar ook kiest, kunnen gebruikers toegang tot gegevens en resources die zijn opgeslagen op uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="9db7a-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="9db7a-107">Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9db7a-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="9db7a-108">U kunt een hybride verzameling die gebruikmaakt van een bestaand virtueel netwerk in Azure implementeren of u kunt een nieuw virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="9db7a-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="9db7a-109">U wordt aangeraden dat u maakt of gebruik een virtueel netwerksubnet met een CIDR-bereik groot genoeg zijn voor toekomstige groei van de verwachte voor Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9db7a-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="9db7a-110">Uw verzameling nog niet hebt worden gemaakt?</span><span class="sxs-lookup"><span data-stu-id="9db7a-110">Haven't created your collection yet?</span></span> <span data-ttu-id="9db7a-111">Zie [een hybride verzameling maken](remoteapp-create-hybrid-deployment.md) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="9db7a-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="9db7a-112">Als u problemen ondervindt bij het maken van de verzameling, of als de verzameling niet, de manier waarop werkt u denkt dat nodig is, controleert u de volgende informatie.</span><span class="sxs-lookup"><span data-stu-id="9db7a-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="9db7a-113">Uw installatiekopie is ongeldig</span><span class="sxs-lookup"><span data-stu-id="9db7a-113">Your image is invalid</span></span>
<span data-ttu-id="9db7a-114">Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure voor het inrichten van uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon voldoet niet aan de [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="9db7a-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="9db7a-115">Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer uw verzameling opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="9db7a-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="9db7a-116">Heeft uw VNET netwerkbeveiligingsgroepen die zijn gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="9db7a-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="9db7a-117">Als u netwerkbeveiligingsgroepen die zijn gedefinieerd op het subnet dat u voor uw verzameling gebruikt hebt, controleert u of deze [URL's en poorten](remoteapp-ports.md) toegankelijk vanuit het subnet zijn.</span><span class="sxs-lookup"><span data-stu-id="9db7a-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="9db7a-118">U kunt aanvullende netwerkbeveiligingsgroepen toevoegen aan de virtuele machines die door u geïmplementeerd in het subnet voor strikter besturingselement.</span><span class="sxs-lookup"><span data-stu-id="9db7a-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="9db7a-119">Gebruikt u uw eigen DNS-servers?</span><span class="sxs-lookup"><span data-stu-id="9db7a-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="9db7a-120">En zijn ze toegankelijk is vanaf uw VNET subnet?</span><span class="sxs-lookup"><span data-stu-id="9db7a-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="9db7a-121">U moet Controleer of dat de DNS-servers in uw VNET altijd actief zijn en altijd kunnen omzetten van de virtuele machines in het VNET.</span><span class="sxs-lookup"><span data-stu-id="9db7a-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="9db7a-122">Gebruik geen Google DNS voor deze.</span><span class="sxs-lookup"><span data-stu-id="9db7a-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="9db7a-123">Voor hybride verzamelingen gebruikt u uw eigen DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="9db7a-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="9db7a-124">U ze in uw network-configuratieschema of via de beheerportal bij het maken van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="9db7a-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="9db7a-125">DNS-servers worden gebruikt in de volgorde waarin ze worden opgegeven op een manier failover (in plaats van round-robin).</span><span class="sxs-lookup"><span data-stu-id="9db7a-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="9db7a-126">Raadpleeg [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) om te controleren of uw DNS-servers geconfigureerd correcly zijn.</span><span class="sxs-lookup"><span data-stu-id="9db7a-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="9db7a-127">Controleer of de DNS-servers voor uw verzameling toegankelijk zijn en beschikbaar is via het VNET subnet dat u hebt opgegeven voor deze verzameling.</span><span class="sxs-lookup"><span data-stu-id="9db7a-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="9db7a-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9db7a-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Uw DNS definiëren](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="9db7a-130">Gebruikt u een Active Directory-domeincontroller in uw verzameling?</span><span class="sxs-lookup"><span data-stu-id="9db7a-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="9db7a-131">Op dit moment slechts één Active Directory-domein gekoppeld aan Azure RemoteApp zijn.</span><span class="sxs-lookup"><span data-stu-id="9db7a-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="9db7a-132">De hybride verzameling ondersteunt alleen Azure Active Directory-accounts die zijn gesynchroniseerd met DirSync-hulpprogramma op een Windows Server Active Directory-implementatie; in het bijzonder hetzij gesynchroniseerd met de optie Wachtwoordsynchronisatie of gesynchroniseerd met Active Directory Federation Services (AD FS) federation geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9db7a-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="9db7a-133">U moet een aangepast domein die overeenkomt met het domein UPN-achtervoegsel voor uw lokale domein maken en instellen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="9db7a-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="9db7a-134">Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9db7a-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="9db7a-135">Zorg ervoor dat de details van het domein opgegeven geldig zijn en de domeincontroller bereikbaar is vanaf de virtuele machine gemaakt in het subnet dat wordt gebruikt voor Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9db7a-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="9db7a-136">Controleer ook of de service-account opgegeven referenties gemachtigd computers toevoegen aan het opgegeven domein en dat de opgegeven AD-naam omgezet vanaf de DNS-server die is opgegeven in het VNET worden kan.</span><span class="sxs-lookup"><span data-stu-id="9db7a-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="9db7a-137">Welke domeinnaam hebt u opgegeven tijdens het maken van uw verzameling?</span><span class="sxs-lookup"><span data-stu-id="9db7a-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="9db7a-138">De domeinnaam die u hebt gemaakt of toegevoegd, moet de naam van een interne domein (niet uw Azure AD domain name) en moet worden omgezet DNS-indeling (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="9db7a-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="9db7a-139">Bijvoorbeeld, hebt u een interne Active Directory-naam (contoso.local) en een Active Directory-UPN (contoso.com) - u moet de interne naam gebruiken bij het maken van uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="9db7a-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

