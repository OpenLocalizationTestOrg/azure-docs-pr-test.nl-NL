---
title: aaaProtect persoonlijke gegevens die onderweg met versleuteling in Azure | Microsoft Docs
description: Met behulp van versleuteling in Azure tooprotect persoonlijke gegevens
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="c9c33-103">Azure versleutelingstechnologieën: beveiligen van persoonlijke gegevens die onderweg met versleuteling</span><span class="sxs-lookup"><span data-stu-id="c9c33-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="c9c33-104">In dit artikel helpt u begrijpen en gebruiken van Azure versleuteling technologieën toosecure gegevens onderweg.</span><span class="sxs-lookup"><span data-stu-id="c9c33-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="c9c33-105">Beschermen Hallo privacy van persoonlijke gegevens is als ze via Hallo-netwerk een essentieel onderdeel van een meerlaagse defense-in-depth beveiligingsstrategie.</span><span class="sxs-lookup"><span data-stu-id="c9c33-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="c9c33-106">Versleuteling onderweg is ontworpen tooprevent een aanvaller die gegevensoverdrachten kunnen tooview of gebruik Hallo gegevens wordt onderschept.</span><span class="sxs-lookup"><span data-stu-id="c9c33-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="c9c33-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="c9c33-107">Scenario</span></span>

<span data-ttu-id="c9c33-108">Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="c9c33-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="c9c33-109">toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="c9c33-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="c9c33-110">Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c9c33-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="c9c33-111">Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase.</span><span class="sxs-lookup"><span data-stu-id="c9c33-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="c9c33-112">Dit omvat ook traditionele Human Resource informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="c9c33-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="c9c33-113">Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.</span><span class="sxs-lookup"><span data-stu-id="c9c33-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="c9c33-114">Persoonlijke gegevens van klanten wordt ingevoerd in de database Hallo uit van het bedrijf Hallo externe kantoren en reizen agents zich Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="c9c33-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="c9c33-115">Documenten met klantgegevens overgebracht over Hallo tooAzure netwerkopslag.</span><span class="sxs-lookup"><span data-stu-id="c9c33-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="c9c33-116">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="c9c33-116">Problem statement</span></span>

<span data-ttu-id="c9c33-117">Hallo bedrijf dient Hallo privacy van klanten te beschermen en persoonlijke gegevens van de werknemers terwijl het onderweg tooand van Azure-services is.</span><span class="sxs-lookup"><span data-stu-id="c9c33-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="c9c33-118">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="c9c33-118">Company goal</span></span>

<span data-ttu-id="c9c33-119">Hallo bedrijf doel tooensure dat persoonlijke gegevens van de harde schijf worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="c9c33-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="c9c33-120">Als niet-geautoriseerde personen Hallo uitschakelen schijf persoonlijke gegevens Intercept, moet deze in een formulier dat het onleesbaar verschijnt.</span><span class="sxs-lookup"><span data-stu-id="c9c33-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="c9c33-121">Versleuteling toepassen, moet eenvoudig of volledig transparant voor gebruikers en beheerders.</span><span class="sxs-lookup"><span data-stu-id="c9c33-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="c9c33-122">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="c9c33-122">Solutions</span></span>

<span data-ttu-id="c9c33-123">Azure-services bieden meerdere hulpprogramma's en technologieën toohelp beveiligen van persoonlijke gegevens die onderweg.</span><span class="sxs-lookup"><span data-stu-id="c9c33-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="c9c33-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c9c33-124">Azure Storage</span></span>

<span data-ttu-id="c9c33-125">Gegevens die zijn opgeslagen in de cloud Hallo moet getransporteerd van Hallo-client, die zich fysiek bevinden overal op kan Hallo wereld, toohello Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="c9c33-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="c9c33-126">Wanneer er gegevens worden opgehaald door gebruikers, overdracht opnieuw in Hallo tegengestelde richting.</span><span class="sxs-lookup"><span data-stu-id="c9c33-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="c9c33-127">Gegevens die onderweg via Hallo openbare Internet is altijd risico worden onderschept door kwaadwillende personen.</span><span class="sxs-lookup"><span data-stu-id="c9c33-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="c9c33-128">Het is belangrijk tooprotect Hallo privacy van persoonlijke gegevens met behulp van versleuteling transportniveau toosecure zoals deze tussen locaties verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c9c33-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="c9c33-129">Hallo HTTPS-protocol biedt een kanaal beveiligde, gecodeerde communicatie via Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c33-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="c9c33-130">HTTPS moet gebruikte tooaccess objecten in Azure Storage en bij het aanroepen van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="c9c33-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="c9c33-131">U gebruik van HTTPS-protocol Hallo afdwingen wanneer u [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure opslag-objecten.</span><span class="sxs-lookup"><span data-stu-id="c9c33-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="c9c33-132">Er zijn twee soorten SAS: Service-SAS en Account-SAS.</span><span class="sxs-lookup"><span data-stu-id="c9c33-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="c9c33-133">Hoe ik een Service-SAS maken?</span><span class="sxs-lookup"><span data-stu-id="c9c33-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="c9c33-134">Een Service-SAS gemachtigden toegang tooa resource in slechts één van de opslagservices hello (blob, queue, tabel of file-service).</span><span class="sxs-lookup"><span data-stu-id="c9c33-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="c9c33-135">een Service-SAS tooconstruct Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9c33-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="c9c33-136">Hallo ondertekend Versieveld opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="c9c33-137">Geef Hallo ondertekend Resource (Blob en alleen File-Service)</span><span class="sxs-lookup"><span data-stu-id="c9c33-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="c9c33-138">Geef de queryparameters tooOverride antwoordheaders (Blob-Service en alleen File-Service)</span><span class="sxs-lookup"><span data-stu-id="c9c33-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="c9c33-139">Geef Hallo tabelnaam (alleen tabel-Service)</span><span class="sxs-lookup"><span data-stu-id="c9c33-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="c9c33-140">Hallo toegangsbeleid opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="c9c33-141">Hallo handtekening geldigheidsinterval opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="c9c33-142">Machtigingen opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-142">Specify Permissions</span></span>

9. <span data-ttu-id="c9c33-143">IP-adres of IP-bereik opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="c9c33-144">Hallo HTTP-Protocol opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="c9c33-145">Tabel toegang adresbereiken opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="c9c33-146">Hallo ondertekend-id opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="c9c33-147">Hallo handtekening opgeven</span><span class="sxs-lookup"><span data-stu-id="c9c33-147">Specify hello Signature</span></span>

<span data-ttu-id="c9c33-148">Zie voor meer instructies, [samenstellen van een Service-SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="c9c33-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="c9c33-149">Hoe ik een SAS-Account maken?</span><span class="sxs-lookup"><span data-stu-id="c9c33-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="c9c33-150">Een Account-SAS delegeert toegang tooresources in een of meer van de opslagservices Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c33-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="c9c33-151">U kunt ook toegang tooread-, schrijf- en delete-bewerkingen op de blob-containers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan als een service-SAS delegeren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="c9c33-152">Bouw van een SAS-Account is vergelijkbaar toothat van een Service-SAS.</span><span class="sxs-lookup"><span data-stu-id="c9c33-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="c9c33-153">Zie voor gedetailleerde instructies [samenstellen van een SAS-Account.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="c9c33-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="c9c33-154">Hoe ik HTTPS afdwingen bij het aanroepen van REST-API's?</span><span class="sxs-lookup"><span data-stu-id="c9c33-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="c9c33-155">tooenforce hello gebruik van HTTPS bij het aanroepen van REST-API's tooaccess objecten in de storage-accounts, kunt u beveiligde overdracht vereist voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c9c33-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="c9c33-156">Selecteer in de Azure-portal Hallo, **Storage-Account maken**, of Selecteer voor een bestaand opslagaccount **instellingen** en vervolgens **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c9c33-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="c9c33-157">Onder **beveiligde overdracht vereist**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="c9c33-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Een opslagaccount maken](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="c9c33-159">Voor instructies gedetailleerde, inclusief hoe tooenable beveiligde overdracht vereist via een programma, Zie [vereisen Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="c9c33-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="c9c33-160">Versleutelen gegevens in Azure File Storage?</span><span class="sxs-lookup"><span data-stu-id="c9c33-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="c9c33-161">gegevens die onderweg met tooencrypt [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), kunt u SMB 3.x met Windows 8, 8.1 en 10 en Windows Server 2012 R2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c9c33-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="c9c33-162">Wanneer u hello Azure Files service gebruikt, wordt een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c9c33-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="c9c33-163">Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van het Hallo Linux SMB-client.</span><span class="sxs-lookup"><span data-stu-id="c9c33-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="c9c33-164">Azure-Client-side '-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c9c33-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="c9c33-165">Een andere optie voor het beveiligen van persoonlijke gegevens, terwijl deze wordt overgebracht tussen een client-toepassing en een Azure Storage is [clientzijde versleuteling](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="c9c33-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="c9c33-166">Hallo-gegevens worden versleuteld voordat ze worden overgedragen naar de Azure-opslag en wanneer u de Hallo-gegevens uit Azure Storage ophalen, Hallo gegevens worden ontsleuteld nadat het is ontvangen op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="c9c33-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="c9c33-167">Azure Site-naar-Site-VPN</span><span class="sxs-lookup"><span data-stu-id="c9c33-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="c9c33-168">Een effectieve manier tooprotect persoonlijke gegevens onderweg tussen een bedrijfsnetwerk of de gebruiker en het Hallo virtuele Azure-netwerk is toouse een [site-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) of [punt-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) virtuele particuliere netwerk (VPN).</span><span class="sxs-lookup"><span data-stu-id="c9c33-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="c9c33-169">Een VPN-verbinding wordt gemaakt van een beveiligde tunnel versleutelde via Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c33-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="c9c33-170">Hoe maak ik een site-naar-site VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="c9c33-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="c9c33-171">Een site-naar-site-VPN-verbinding maakt meerdere gebruikers op Hallo bedrijfsnetwerk tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c9c33-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="c9c33-172">een site-naar-site-verbinding in hello Azure-portal toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9c33-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="c9c33-173">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-173">Create a virtual network.</span></span>

2. <span data-ttu-id="c9c33-174">Geef een DNS-server.</span><span class="sxs-lookup"><span data-stu-id="c9c33-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="c9c33-175">Hallo gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="c9c33-176">Hallo VPN-gateway maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="c9c33-177">Hallo lokale netwerkgateway maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="c9c33-178">Configureer het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c9c33-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="c9c33-179">Hallo VPN-verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="c9c33-180">Hallo VPN-verbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="c9c33-181">Voor gedetailleerde instructies over hoe toocreate een site-naar-site-verbinding in hello Azure portal, Zie [maken van een Site-naar-Site-verbinding in hello Azure-Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="c9c33-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="c9c33-182">Hoe maak ik een punt-naar-site VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="c9c33-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="c9c33-183">Een punt-naar-Site VPN maakt een beveiligde verbinding van een individuele client computer tooa virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c9c33-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="c9c33-184">Dit is handig als u tooconnect tooAzure vanaf een externe locatie, zoals vanaf thuis of een hotel of conferentie center.</span><span class="sxs-lookup"><span data-stu-id="c9c33-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="c9c33-185">toocreate een punt-naar-site-verbinding in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c9c33-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="c9c33-186">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-186">Create a virtual network.</span></span>

2. <span data-ttu-id="c9c33-187">Voeg een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="c9c33-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="c9c33-188">Geef een DNS-server.</span><span class="sxs-lookup"><span data-stu-id="c9c33-188">Specify a DNS server.</span></span> <span data-ttu-id="c9c33-189">(optioneel)</span><span class="sxs-lookup"><span data-stu-id="c9c33-189">(optional)</span></span>

4. <span data-ttu-id="c9c33-190">Maak een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="c9c33-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="c9c33-191">Genereren van certificaten.</span><span class="sxs-lookup"><span data-stu-id="c9c33-191">Generate certificates.</span></span>

6. <span data-ttu-id="c9c33-192">Hallo-clientadresgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9c33-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="c9c33-193">Hallo root certificate openbaar certificaatgegevens uploaden.</span><span class="sxs-lookup"><span data-stu-id="c9c33-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="c9c33-194">Genereren en Hallo VPN-clientpakket configuratie installeren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="c9c33-195">Een geëxporteerde certificaat installeren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="c9c33-196">Verbinding maken met tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c9c33-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="c9c33-197">Controleer de verbinding.</span><span class="sxs-lookup"><span data-stu-id="c9c33-197">Verify your connection.</span></span>

<span data-ttu-id="c9c33-198">Zie voor meer instructies, [een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="c9c33-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="c9c33-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="c9c33-199">SSL/TLS</span></span>

<span data-ttu-id="c9c33-200">Microsoft raadt aan dat u altijd SSL/TLS-protocollen tooexchange gegevens op verschillende locaties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9c33-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="c9c33-201">Organisaties die ervoor toouse kiezen [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grote gegevenssets toegewezen snelle WAN-koppeling kunt Hallo gegevens op Hallo op toepassingsniveau met SSL/TLS- of andere protocollen voor extra beveiliging ook versleutelen.</span><span class="sxs-lookup"><span data-stu-id="c9c33-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="c9c33-202">Codering standaard</span><span class="sxs-lookup"><span data-stu-id="c9c33-202">Encryption by default</span></span>

<span data-ttu-id="c9c33-203">Microsoft gebruikt codering tooprotect gegevens onderweg tussen klanten en Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="c9c33-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="c9c33-204">Als u met Azure Storage via hello Azure Portal communiceert, worden alle transacties plaatsvinden via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c9c33-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="c9c33-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is dat Microsoft-datacenters toonegotiate met clientsystemen die verbinding met cloudservices tooMicrosoft zal proberen Hallo-protocol.</span><span class="sxs-lookup"><span data-stu-id="c9c33-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="c9c33-206">TLS bevat sterke verificatie, privacy van berichten en integriteit (schakelt u het detecteren van bericht knoeien, onderschept en kunnen worden vervalst), interoperabiliteit, algoritmeflexibiliteit, gebruiksgemak en gebruik.</span><span class="sxs-lookup"><span data-stu-id="c9c33-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="c9c33-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) wordt ook gebruikt zodat elke verbinding tussen clientsystemen klanten en cloudservices van Microsoft gebruiken unieke sleutels.</span><span class="sxs-lookup"><span data-stu-id="c9c33-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="c9c33-208">Verbindingen tooMicrosoft cloudservices ook te profiteren van op basis van RSA 2048-bits versleuteling sleutellengten.</span><span class="sxs-lookup"><span data-stu-id="c9c33-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="c9c33-209">Hallo combinatie van TLS, sleutellengtes RSA 2048-bits, en PFS maakt het moeilijker voor iemand toointercept en toegang tot gegevens die onderweg tussen Microsoft-cloudservices en -klanten.</span><span class="sxs-lookup"><span data-stu-id="c9c33-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="c9c33-210">Gegevens die onderweg is altijd versleuteld in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="c9c33-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="c9c33-211">Bovendien tooencrypting gegevens voorafgaande toostoring toopersistent media Hallo gegevens is ook altijd onderweg via HTTPS beveiligd.</span><span class="sxs-lookup"><span data-stu-id="c9c33-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="c9c33-212">HTTPS is alleen Hallo-protocol dat wordt ondersteund voor Hallo die Data Lake Store REST-interfaces.</span><span class="sxs-lookup"><span data-stu-id="c9c33-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="c9c33-213">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c9c33-213">Summary</span></span>

<span data-ttu-id="c9c33-214">Hallo bedrijf kan het doel van persoonlijke gegevens en Hallo privacy van dergelijke gegevens beveiligen met HTTPS-verbindingen tooAzure opslag afdwingen, met behulp van handtekeningen voor gedeelde toegang en inschakelen van beveiligde overdracht vereist op Hallo storage-accounts kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="c9c33-215">Ze kunnen ook persoonlijke gegevens beveiligen met behulp van SMB 3.0-verbindingen en clientzijde codering implementeren.</span><span class="sxs-lookup"><span data-stu-id="c9c33-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="c9c33-216">Site-naar-site VPN-verbindingen van Hallo bedrijfsnetwerk toohello virtuele Azure-netwerk en punt-naar-site VPN-verbindingen van afzonderlijke gebruikers maakt een beveiligde tunnel via welke persoonlijke gegevens kan veilig worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c9c33-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="c9c33-217">Microsoft standaard versleuteling procedures nog beter beschermd Hallo privacy van persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="c9c33-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c33-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9c33-218">Next steps</span></span>

- [<span data-ttu-id="c9c33-219">Best Practices voor beveiliging van gegevens van Azure en versleuteling</span><span class="sxs-lookup"><span data-stu-id="c9c33-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="c9c33-220">Planning en ontwerp voor VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="c9c33-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="c9c33-221">Veelgestelde vragen VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="c9c33-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="c9c33-222">Kopen en configureren van een SSL-certificaat voor uw Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c9c33-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
