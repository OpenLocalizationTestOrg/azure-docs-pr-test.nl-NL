---
title: Beveiligen van persoonlijke gegevens die onderweg met versleuteling in Azure | Microsoft Docs
description: Met behulp van versleuteling persoonlijke gegevens te beveiligen in Azure
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
ms.openlocfilehash: 99e40b8a09a2f151e7f83fbb58bdfc00ae4b1268
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="a85dd-103">Azure versleutelingstechnologieën: beveiligen van persoonlijke gegevens die onderweg met versleuteling</span><span class="sxs-lookup"><span data-stu-id="a85dd-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="a85dd-104">In dit artikel helpt u begrijpen en gebruiken van Azure versleutelingstechnologieën beveiligen van gegevens die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="a85dd-104">This article will help you understand and use Azure encryption technologies to secure data in transit.</span></span> 

<span data-ttu-id="a85dd-105">De privacy van persoonlijke gegevens te beveiligen als ze via het netwerk is een essentieel onderdeel van een meerlaagse beveiliging van defense-in-depth-strategie.</span><span class="sxs-lookup"><span data-stu-id="a85dd-105">Protecting the privacy of personal data as it travels across the network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="a85dd-106">Versleuteling onderweg is ontworpen om te voorkomen dat een aanvaller die gegevensoverdrachten te geven of de gegevens kunnen worden onderschept.</span><span class="sxs-lookup"><span data-stu-id="a85dd-106">Encryption in transit is designed to prevent an attacker who intercepts transmissions from being able to view or use the data.</span></span>

## <a name="scenario"></a><span data-ttu-id="a85dd-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="a85dd-107">Scenario</span></span>

<span data-ttu-id="a85dd-108">Een bedrijf grote cruise, gevestigd in de Verenigde Staten, aanvullende bewerkingen voor het bieden van routes in de Middellandse, Adriatische, Baltische veiligheid ook Florida.</span><span class="sxs-lookup"><span data-stu-id="a85dd-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="a85dd-109">Ter ondersteuning van deze inspanningen is die is verkregen meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en het Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="a85dd-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="a85dd-110">Het bedrijf gebruikmaakt van Microsoft Azure voor het opslaan van bedrijfsgegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="a85dd-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="a85dd-111">Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase.</span><span class="sxs-lookup"><span data-stu-id="a85dd-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="a85dd-112">Dit omvat ook traditionele Human Resource informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="a85dd-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="a85dd-113">De regel cruise onderhoudt ook een grote database van derden en loyaliteit programma leden met persoonlijke gegevens voor de relaties met de huidige en eerdere klanten bijhouden.</span><span class="sxs-lookup"><span data-stu-id="a85dd-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="a85dd-114">Persoonlijke gegevens van klanten is ingevoerd in de database uit van het bedrijf externe kantoren en reizen agents over de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="a85dd-114">Personal data of customers is entered in the database from the company’s remote offices and from travel agents located around the world.</span></span> <span data-ttu-id="a85dd-115">Documenten met klantgegevens worden overgebracht via het netwerk naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="a85dd-115">Documents containing customer information are transferred across the network to Azure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a85dd-116">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="a85dd-116">Problem statement</span></span>

<span data-ttu-id="a85dd-117">Het bedrijf moet de privacy van klanten en werknemers persoonlijke gegevens beveiligen terwijl het onderweg en naar Azure-services.</span><span class="sxs-lookup"><span data-stu-id="a85dd-117">The company must protect the privacy of customers’ and employees’ personal data while it is in transit to and from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a85dd-118">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="a85dd-118">Company goal</span></span>

<span data-ttu-id="a85dd-119">Het doel van het bedrijf om ervoor te zorgen dat de persoonlijke gegevens van de harde schijf worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="a85dd-119">The company goal to ensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="a85dd-120">Als niet-geautoriseerde personen de persoonlijke gegevens buiten de schijf Intercept, moet deze in een formulier dat het onleesbaar verschijnt.</span><span class="sxs-lookup"><span data-stu-id="a85dd-120">If unauthorized persons intercept the off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="a85dd-121">Versleuteling toepassen, moet eenvoudig of volledig transparant voor gebruikers en beheerders.</span><span class="sxs-lookup"><span data-stu-id="a85dd-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="a85dd-122">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="a85dd-122">Solutions</span></span>

<span data-ttu-id="a85dd-123">Azure-services bieden meerdere hulpprogramma's en technologieën voor het persoonlijke gegevens onderweg te beschermen.</span><span class="sxs-lookup"><span data-stu-id="a85dd-123">Azure services provide multiple tools and technologies to help you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="a85dd-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a85dd-124">Azure Storage</span></span>

<span data-ttu-id="a85dd-125">Gegevens die zijn opgeslagen in de cloud moet van de client, die zich fysiek overal ter wereld, naar het Azure Datacenter gaan.</span><span class="sxs-lookup"><span data-stu-id="a85dd-125">Data that is stored in the cloud must travel from the client, which can be physically located anywhere in the world, to the Azure data center.</span></span> <span data-ttu-id="a85dd-126">Wanneer er gegevens worden opgehaald door gebruikers, overdracht opnieuw in de tegengestelde richting.</span><span class="sxs-lookup"><span data-stu-id="a85dd-126">When that data is retrieved by users, it travels again, in the opposite direction.</span></span> <span data-ttu-id="a85dd-127">Gegevens die via het openbare Internet onderweg is altijd risico worden onderschept door kwaadwillende personen.</span><span class="sxs-lookup"><span data-stu-id="a85dd-127">Data that is in transit over the public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="a85dd-128">Het is belangrijk om de privacy van persoonlijke gegevens beschermen met behulp van transportniveau versleuteling te beveiligen als u deze verplaatst tussen locaties.</span><span class="sxs-lookup"><span data-stu-id="a85dd-128">It is important to protect the privacy of personal data by using transport-level encryption to secure it as it moves between locations.</span></span>

<span data-ttu-id="a85dd-129">Het HTTPS-protocol biedt een kanaal beveiligde, gecodeerde communicatie via Internet.</span><span class="sxs-lookup"><span data-stu-id="a85dd-129">The HTTPS protocol provides a secure, encrypted communications channel over the Internet.</span></span> <span data-ttu-id="a85dd-130">HTTPS moet worden gebruikt voor toegang tot objecten in Azure Storage en bij het aanroepen van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="a85dd-130">HTTPS should be used to access objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="a85dd-131">U gebruik van het HTTPS-protocol afdwingen wanneer u [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) te delegeren van toegang tot Azure Storage-objecten.</span><span class="sxs-lookup"><span data-stu-id="a85dd-131">You enforce use of the HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) to delegate access to Azure Storage objects.</span></span> <span data-ttu-id="a85dd-132">Er zijn twee soorten SAS: Service-SAS en Account-SAS.</span><span class="sxs-lookup"><span data-stu-id="a85dd-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="a85dd-133">Hoe ik een Service-SAS maken?</span><span class="sxs-lookup"><span data-stu-id="a85dd-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="a85dd-134">Een Service-SAS delegeert toegang tot een resource in slechts één van de storage-services (blob, queue, tabel of file-service).</span><span class="sxs-lookup"><span data-stu-id="a85dd-134">A Service SAS delegates access to a resource in just one of the storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="a85dd-135">Kan een Service-SAS, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a85dd-135">To construct a Service SAS, do the following:</span></span>

1. <span data-ttu-id="a85dd-136">Het veld ondertekende versie opgeven</span><span class="sxs-lookup"><span data-stu-id="a85dd-136">Specify the Signed Version Field</span></span>

2. <span data-ttu-id="a85dd-137">Geef de ondertekende Resource (Blob en File-Service)</span><span class="sxs-lookup"><span data-stu-id="a85dd-137">Specify the Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="a85dd-138">Geef queryparameters op om te overschrijven antwoordheaders (Blob-Service en File-Service)</span><span class="sxs-lookup"><span data-stu-id="a85dd-138">Specify Query Parameters to Override Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="a85dd-139">Geef de naam van de tabel (alleen voor Tabelservice)</span><span class="sxs-lookup"><span data-stu-id="a85dd-139">Specify the Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="a85dd-140">Geef het beleid voor toegang</span><span class="sxs-lookup"><span data-stu-id="a85dd-140">Specify the Access Policy</span></span>

6. <span data-ttu-id="a85dd-141">Geef het geldigheidsinterval van de handtekening</span><span class="sxs-lookup"><span data-stu-id="a85dd-141">Specify the Signature Validity Interval</span></span>

8. <span data-ttu-id="a85dd-142">Machtigingen opgeven</span><span class="sxs-lookup"><span data-stu-id="a85dd-142">Specify Permissions</span></span>

9. <span data-ttu-id="a85dd-143">IP-adres of IP-bereik opgeven</span><span class="sxs-lookup"><span data-stu-id="a85dd-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="a85dd-144">Geef de HTTP-Protocol</span><span class="sxs-lookup"><span data-stu-id="a85dd-144">Specify the HTTP Protocol</span></span>

11. <span data-ttu-id="a85dd-145">Tabel toegang adresbereiken opgeven</span><span class="sxs-lookup"><span data-stu-id="a85dd-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="a85dd-146">Hiermee geeft u de ondertekende id</span><span class="sxs-lookup"><span data-stu-id="a85dd-146">Specify the Signed Identifier</span></span>

13. <span data-ttu-id="a85dd-147">Geef de handtekening</span><span class="sxs-lookup"><span data-stu-id="a85dd-147">Specify the Signature</span></span>

<span data-ttu-id="a85dd-148">Zie voor meer instructies, [samenstellen van een Service-SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="a85dd-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="a85dd-149">Hoe ik een SAS-Account maken?</span><span class="sxs-lookup"><span data-stu-id="a85dd-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="a85dd-150">Een Account-SAS delegeert toegang tot bronnen in een of meer van de storage-services.</span><span class="sxs-lookup"><span data-stu-id="a85dd-150">An Account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="a85dd-151">U kunt ook toegang tot het lezen, schrijven en verwijderen van bewerkingen delegeren voor blobcontainers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan bij een service-SAS.</span><span class="sxs-lookup"><span data-stu-id="a85dd-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="a85dd-152">Bouw van een SAS-Account is vergelijkbaar met die van een Service-SAS.</span><span class="sxs-lookup"><span data-stu-id="a85dd-152">Construction of an Account SAS is similar to that of a Service SAS.</span></span> <span data-ttu-id="a85dd-153">Zie voor gedetailleerde instructies [samenstellen van een SAS-Account.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="a85dd-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="a85dd-154">Hoe ik HTTPS afdwingen bij het aanroepen van REST-API's?</span><span class="sxs-lookup"><span data-stu-id="a85dd-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="a85dd-155">Het gebruik van HTTPS afdwingen bij het aanroepen van REST-API's voor toegang tot objecten in de storage-accounts, kunt u beveiligde overdracht vereist voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a85dd-155">To enforce the use of HTTPS when calling REST APIs to access objects in storage accounts, you can enable Secure Transfer Required for the storage account.</span></span> 

1. <span data-ttu-id="a85dd-156">Selecteer in de Azure-portal **Storage-Account maken**, of Selecteer voor een bestaand opslagaccount **instellingen** en vervolgens **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="a85dd-156">In the Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="a85dd-157">Onder **beveiligde overdracht vereist**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="a85dd-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Een opslagaccount maken](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="a85dd-159">Voor instructies gedetailleerde, met inbegrip van beveiligde overdracht vereist programmatisch inschakelen, Raadpleeg [vereisen Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="a85dd-159">For more detailed instructions, including how to enable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="a85dd-160">Versleutelen gegevens in Azure File Storage?</span><span class="sxs-lookup"><span data-stu-id="a85dd-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="a85dd-161">Voor het versleutelen van gegevens tijdens de overdracht met [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), kunt u SMB 3.x met Windows 8, 8.1 en 10 en Windows Server 2012 R2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a85dd-161">To encrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="a85dd-162">Wanneer u de service Azure-bestanden gebruikt, wordt er een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a85dd-162">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="a85dd-163">Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van de Linux SMB-client.</span><span class="sxs-lookup"><span data-stu-id="a85dd-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="a85dd-164">Azure-Client-side '-versleuteling</span><span class="sxs-lookup"><span data-stu-id="a85dd-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="a85dd-165">Een andere optie voor het beveiligen van persoonlijke gegevens, terwijl deze wordt overgebracht tussen een client-toepassing en een Azure Storage is [clientzijde versleuteling](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="a85dd-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="a85dd-166">De gegevens worden versleuteld voordat ze worden overgedragen naar de Azure-opslag en wanneer u de gegevens uit Azure Storage ophaalt, de gegevens worden ontsleuteld nadat het is ontvangen op de client.</span><span class="sxs-lookup"><span data-stu-id="a85dd-166">The data is encrypted before being transferred into Azure Storage and when you retrieve the data from Azure Storage, the data is decrypted after it is received on the client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="a85dd-167">Azure Site-naar-Site-VPN</span><span class="sxs-lookup"><span data-stu-id="a85dd-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="a85dd-168">Een effectieve manier om persoonlijke gegevens onderweg tussen een bedrijfsnetwerk of de gebruiker en de virtuele Azure-netwerk te beveiligen is met een [site-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) of [punt-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) virtuele particuliere netwerk (VPN).</span><span class="sxs-lookup"><span data-stu-id="a85dd-168">An effective way to protect personal data in transit between a corporate network or user and the Azure virtual network is to use a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="a85dd-169">Een VPN-verbinding wordt gemaakt van een beveiligde tunnel versleutelde via Internet.</span><span class="sxs-lookup"><span data-stu-id="a85dd-169">A VPN connection creates a secure encrypted tunnel across the Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="a85dd-170">Hoe maak ik een site-naar-site VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="a85dd-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="a85dd-171">Meerdere gebruikers op het bedrijfsnetwerk verbinding een site-naar-site-VPN-met Azure.</span><span class="sxs-lookup"><span data-stu-id="a85dd-171">A site-to-site VPN connects multiple users on the corporate network to Azure.</span></span> <span data-ttu-id="a85dd-172">Een site-naar-site om verbinding te maken in de Azure portal, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a85dd-172">To create a site-to-site connection in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="a85dd-173">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="a85dd-173">Create a virtual network.</span></span>

2. <span data-ttu-id="a85dd-174">Geef een DNS-server.</span><span class="sxs-lookup"><span data-stu-id="a85dd-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="a85dd-175">Maak het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="a85dd-175">Create the gateway subnet.</span></span>

4. <span data-ttu-id="a85dd-176">Maak de VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="a85dd-176">Create the VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="a85dd-177">De lokale netwerkgateway maken.</span><span class="sxs-lookup"><span data-stu-id="a85dd-177">Create the local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="a85dd-178">Configureer het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a85dd-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="a85dd-179">Maak de VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="a85dd-179">Create the VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="a85dd-180">Controleer of de VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="a85dd-180">Verify the VPN connection.</span></span>

<span data-ttu-id="a85dd-181">Zie voor meer gedetailleerde instructies voor het maken van een site-naar-site-verbinding in de Azure portal [verbinding met Site-naar-Site in de Azure Portal maken]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a85dd-181">For more detailed instructions on how to create a site-to-site connection in the Azure portal, see [Create a Site-to-Site  connection in the Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="a85dd-182">Hoe maak ik een punt-naar-site VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="a85dd-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="a85dd-183">Een punt-naar-Site VPN maakt een beveiligde verbinding van een afzonderlijke clientcomputer met een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="a85dd-183">A Point-to-Site VPN creates a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="a85dd-184">Dit is handig als u verbinding maken met Azure vanaf een externe locatie wilt, zoals vanaf thuis of een hotel of conferentie center.</span><span class="sxs-lookup"><span data-stu-id="a85dd-184">This is useful when you  want to connect to Azure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="a85dd-185">Een punt-naar-site om verbinding te maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="a85dd-185">To create a point-to-site  connection in the Azure portal,</span></span>

1. <span data-ttu-id="a85dd-186">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="a85dd-186">Create a virtual network.</span></span>

2. <span data-ttu-id="a85dd-187">Voeg een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="a85dd-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="a85dd-188">Geef een DNS-server.</span><span class="sxs-lookup"><span data-stu-id="a85dd-188">Specify a DNS server.</span></span> <span data-ttu-id="a85dd-189">(optioneel)</span><span class="sxs-lookup"><span data-stu-id="a85dd-189">(optional)</span></span>

4. <span data-ttu-id="a85dd-190">Maak een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="a85dd-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="a85dd-191">Genereren van certificaten.</span><span class="sxs-lookup"><span data-stu-id="a85dd-191">Generate certificates.</span></span>

6. <span data-ttu-id="a85dd-192">Toevoegen van de client-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="a85dd-192">Add the client address pool.</span></span>

7. <span data-ttu-id="a85dd-193">De openbare certificaatgegevens van het root-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="a85dd-193">Upload the root certificate public certificate data.</span></span>

8. <span data-ttu-id="a85dd-194">Genereren en de configuratie van VPN-clientpakket installeren.</span><span class="sxs-lookup"><span data-stu-id="a85dd-194">Generate and install the VPN client configuration package.</span></span>

9. <span data-ttu-id="a85dd-195">Een geëxporteerde certificaat installeren.</span><span class="sxs-lookup"><span data-stu-id="a85dd-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="a85dd-196">Verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="a85dd-196">Connect to Azure.</span></span>

11. <span data-ttu-id="a85dd-197">Controleer de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a85dd-197">Verify your connection.</span></span>

<span data-ttu-id="a85dd-198">Zie voor meer instructies, [een punt-naar-Site-verbinding met een VNet met behulp van verificatie via certificaat configureren: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a85dd-198">For more detailed instructions, see [Configure a Point-to-Site connection to a VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="a85dd-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="a85dd-199">SSL/TLS</span></span>

<span data-ttu-id="a85dd-200">Microsoft raadt aan dat u altijd SSL/TLS-protocollen gebruiken voor het uitwisselen van gegevens op verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="a85dd-200">Microsoft recommends that you always use SSL/TLS protocols to exchange data across different locations.</span></span> <span data-ttu-id="a85dd-201">Organisaties die gebruiken [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) grote gegevenssets verplaatsen via een speciale snelle WAN koppeling ook de gegevens op toepassingsniveau kunt versleutelen met behulp van SSL/TLS- of andere protocollen voor extra beveiliging.</span><span class="sxs-lookup"><span data-stu-id="a85dd-201">Organizations that choose to use [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) to move large data sets over a dedicated high-speed WAN link can also encrypt the data at the application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="a85dd-202">Codering standaard</span><span class="sxs-lookup"><span data-stu-id="a85dd-202">Encryption by default</span></span>

<span data-ttu-id="a85dd-203">Microsoft maakt gebruik van versleuteling om gegevens onderweg tussen Azure-cloudservices en klanten te beschermen.</span><span class="sxs-lookup"><span data-stu-id="a85dd-203">Microsoft uses encryption to protect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="a85dd-204">Als u met Azure Storage via de Azure-Portal communiceert, worden alle transacties plaatsvinden via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a85dd-204">If you are interacting with Azure Storage through the Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="a85dd-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is het protocol dat Microsoft-datacenters probeert te onderhandelen met clientsystemen die verbinding met Microsoft-cloudservices maken.</span><span class="sxs-lookup"><span data-stu-id="a85dd-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is the protocol that Microsoft data centers will attempt to negotiate with client systems that connect to Microsoft cloud services.</span></span> <span data-ttu-id="a85dd-206">TLS bevat sterke verificatie, privacy van berichten en integriteit (schakelt u het detecteren van bericht knoeien, onderschept en kunnen worden vervalst), interoperabiliteit, algoritmeflexibiliteit, gebruiksgemak en gebruik.</span><span class="sxs-lookup"><span data-stu-id="a85dd-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="a85dd-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) wordt ook gebruikt zodat elke verbinding tussen clientsystemen klanten en cloudservices van Microsoft gebruiken unieke sleutels.</span><span class="sxs-lookup"><span data-stu-id="a85dd-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="a85dd-208">Verbindingen met Microsoft cloud-services ook te profiteren van op basis van RSA 2048-bits versleuteling sleutellengten.</span><span class="sxs-lookup"><span data-stu-id="a85dd-208">Connections to Microsoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="a85dd-209">De combinatie van TLS, sleutellengtes RSA 2048-bits, en PFS maakt het moeilijker voor iemand om te onderscheppen en toegang tot gegevens die onderweg tussen Microsoft-cloudservices en -klanten.</span><span class="sxs-lookup"><span data-stu-id="a85dd-209">The combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone to intercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="a85dd-210">Gegevens die onderweg is altijd versleuteld in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="a85dd-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="a85dd-211">Naast het versleutelen van gegevens voorafgaand aan het opslaan op permanente media, worden de gegevens tijdens overdracht ook altijd beveiligd met behulp van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a85dd-211">In addition to encrypting data prior to storing to persistent media, the data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="a85dd-212">HTTPS is het enige protocol dat wordt ondersteund voor de Data Lake Store REST-interfaces.</span><span class="sxs-lookup"><span data-stu-id="a85dd-212">HTTPS is the only protocol that is supported for the Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="a85dd-213">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a85dd-213">Summary</span></span>

<span data-ttu-id="a85dd-214">Het bedrijf kan het doel van persoonlijke gegevens en de privacy van dergelijke gegevens beveiligen met HTTPS-verbindingen naar Azure Storage afdwingen, met behulp van handtekeningen voor gedeelde toegang en inschakelen van beveiligde overdracht vereist op de storage-accounts kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a85dd-214">The company can accomplish its goal of protecting personal data and the privacy of such data by enforcing HTTPS connections to Azure Storage, using Shared Access Signatures and enabling Secure Transfer Required on the storage accounts.</span></span> <span data-ttu-id="a85dd-215">Ze kunnen ook persoonlijke gegevens beveiligen met behulp van SMB 3.0-verbindingen en clientzijde codering implementeren.</span><span class="sxs-lookup"><span data-stu-id="a85dd-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="a85dd-216">Site-naar-site VPN-verbindingen met het bedrijfsnetwerk naar het Azure-netwerk en punt-naar-site VPN-verbindingen van afzonderlijke gebruikers maakt een beveiligde tunnel via welke persoonlijke gegevens kan veilig worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="a85dd-216">Site-to-site VPN connections from the corporate network to the Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="a85dd-217">Procedures voor versleuteling van Microsoft-standaard wordt de privacy van persoonlijke gegevens verder beschermen.</span><span class="sxs-lookup"><span data-stu-id="a85dd-217">Microsoft’s default encryption practices will further protect the privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a85dd-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a85dd-218">Next steps</span></span>

- [<span data-ttu-id="a85dd-219">Best Practices voor beveiliging van gegevens van Azure en versleuteling</span><span class="sxs-lookup"><span data-stu-id="a85dd-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="a85dd-220">Planning en ontwerp voor VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="a85dd-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="a85dd-221">Veelgestelde vragen VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="a85dd-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="a85dd-222">Kopen en configureren van een SSL-certificaat voor uw Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a85dd-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
