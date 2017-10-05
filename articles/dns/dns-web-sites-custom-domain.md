---
title: Aangepaste DNS-records voor een web-app maken | Microsoft Docs
description: Het maken van aangepaste domein-DNS-records voor web-app met Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="58e69-103">DNS-records voor een web-app maken in een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="58e69-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="58e69-104">U kunt Azure DNS gebruiken voor het hosten van een aangepast domein voor uw web-apps.</span><span class="sxs-lookup"><span data-stu-id="58e69-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="58e69-105">Bijvoorbeeld, u een Azure-web-app maakt en u wilt dat gebruikers toegang tot het door u contoso.com of www.contoso.com als een FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="58e69-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="58e69-106">Hiervoor hebt u twee records maken:</span><span class="sxs-lookup"><span data-stu-id="58e69-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="58e69-107">Een hoofdmaprecord "A" verwijst naar contoso.com</span><span class="sxs-lookup"><span data-stu-id="58e69-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="58e69-108">Een 'CNAME'-record voor de www-naam die naar de A-record verwijst</span><span class="sxs-lookup"><span data-stu-id="58e69-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="58e69-109">Houd er rekening mee dat als u een A-record voor een web-app in Azure maakt, de A-record handmatig moet worden bijgewerkt als het onderliggende IP-adres voor de web-app-wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="58e69-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="58e69-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="58e69-110">Before you begin</span></span>

<span data-ttu-id="58e69-111">Voordat u begint, moet u eerst een DNS-zone maken in Azure DNS, en de zone in uw registrar naar Azure DNS overdragen.</span><span class="sxs-lookup"><span data-stu-id="58e69-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="58e69-112">Volg de stappen in voor het maken van een DNS-zone [maken van een DNS-zone](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="58e69-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="58e69-113">Als u wilt uw DNS naar Azure DNS overdragen, volg de stappen in [DNS-domeindelegering](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="58e69-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="58e69-114">Na het maken van een zone en deze te delegeren naar Azure DNS, kunt u vervolgens records maken voor uw aangepaste domein.</span><span class="sxs-lookup"><span data-stu-id="58e69-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="58e69-115">1. Maak een A-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="58e69-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="58e69-116">Een A-record wordt gebruikt om een naam toewijzen aan het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="58e69-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="58e69-117">In het volgende voorbeeld wordt we @ toewijzen als een A-record in een IPv4-adres:</span><span class="sxs-lookup"><span data-stu-id="58e69-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="58e69-118">Stap 1</span><span class="sxs-lookup"><span data-stu-id="58e69-118">Step 1</span></span>

<span data-ttu-id="58e69-119">Een A-record maken en toewijzen aan een variabele $rs</span><span class="sxs-lookup"><span data-stu-id="58e69-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="58e69-120">Stap 2</span><span class="sxs-lookup"><span data-stu-id="58e69-120">Step 2</span></span>

<span data-ttu-id="58e69-121">De IPv4-waarde toevoegen aan de eerder gemaakte recordset ' @ ' met behulp van de variabele $rs is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="58e69-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="58e69-122">De IPv4-waarde die is toegewezen, worden de IP-adres voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="58e69-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="58e69-123">Volg de stappen in het IP-adres voor een web-app vindt [een aangepaste domeinnaam configureren in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="58e69-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="58e69-124">Stap 3</span><span class="sxs-lookup"><span data-stu-id="58e69-124">Step 3</span></span>

<span data-ttu-id="58e69-125">De wijzigingen doorvoeren aan de recordset.</span><span class="sxs-lookup"><span data-stu-id="58e69-125">Commit the changes to the record set.</span></span> <span data-ttu-id="58e69-126">Gebruik `Set-AzureRMDnsRecordSet` voor het uploaden van de wijzigingen aan de recordset naar Azure DNS:</span><span class="sxs-lookup"><span data-stu-id="58e69-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="58e69-127">2. Maak een CNAME-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="58e69-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="58e69-128">Als uw domein wordt al beheerd door Azure DNS (Zie [DNS-domeindelegering](dns-domain-delegation.md), kunt u het volgende voorbeeld maakt u een CNAME-record voor contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="58e69-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="58e69-129">Stap 1</span><span class="sxs-lookup"><span data-stu-id="58e69-129">Step 1</span></span>

<span data-ttu-id="58e69-130">Open PowerShell en een nieuwe CNAME-recordset maken en toewijzen aan een variabele $rs.</span><span class="sxs-lookup"><span data-stu-id="58e69-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="58e69-131">In dit voorbeeld wordt een type recordset CNAME met een "time to live" maken van 600 seconden in DNS-zone met de naam 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="58e69-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="58e69-132">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="58e69-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="58e69-133">Stap 2</span><span class="sxs-lookup"><span data-stu-id="58e69-133">Step 2</span></span>

<span data-ttu-id="58e69-134">Zodra de CNAME-recordset is gemaakt, moet u de aliaswaarde van een die naar de web-app verwijst maken.</span><span class="sxs-lookup"><span data-stu-id="58e69-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="58e69-135">Met behulp van de eerder toegewezen variabele '$rs' kunt u de onderstaande PowerShell-opdracht voor het maken van de alias voor de web-app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="58e69-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="58e69-136">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="58e69-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="58e69-137">Stap 3</span><span class="sxs-lookup"><span data-stu-id="58e69-137">Step 3</span></span>

<span data-ttu-id="58e69-138">De wijzigingen met behulp van de `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="58e69-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="58e69-139">U kunt controleren of de record correct is gemaakt door het opvragen van de 'www.contoso.com' met nslookup, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="58e69-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="58e69-140">Maak een 'awverify'-record voor web-apps</span><span class="sxs-lookup"><span data-stu-id="58e69-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="58e69-141">Als u een A-record gebruiken voor uw web-app besluit, moet u een verificatieprocedure om te controleren of de eigenaar van het aangepaste domein doorlopen.</span><span class="sxs-lookup"><span data-stu-id="58e69-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="58e69-142">Deze verificatiestap wordt gedaan door het maken van een speciale CNAME-record met de naam 'awverify'.</span><span class="sxs-lookup"><span data-stu-id="58e69-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="58e69-143">Deze sectie geldt alleen een records.</span><span class="sxs-lookup"><span data-stu-id="58e69-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="58e69-144">Stap 1</span><span class="sxs-lookup"><span data-stu-id="58e69-144">Step 1</span></span>

<span data-ttu-id="58e69-145">De 'awverify'-record maken.</span><span class="sxs-lookup"><span data-stu-id="58e69-145">Create the "awverify" record.</span></span> <span data-ttu-id="58e69-146">We gaan de 'aweverify'-record voor contoso.com te verifiëren voor het aangepaste domein maken in het onderstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="58e69-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="58e69-147">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="58e69-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="58e69-148">Stap 2</span><span class="sxs-lookup"><span data-stu-id="58e69-148">Step 2</span></span>

<span data-ttu-id="58e69-149">Zodra de recordset 'awverify' is gemaakt, wijst u de CNAME-Recordset alias toe.</span><span class="sxs-lookup"><span data-stu-id="58e69-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="58e69-150">In het onderstaande voorbeeld wijst de alias wordt ingesteld op awverify.contoso.azurewebsites.net CNAMe-record toe.</span><span class="sxs-lookup"><span data-stu-id="58e69-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="58e69-151">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="58e69-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="58e69-152">Stap 3</span><span class="sxs-lookup"><span data-stu-id="58e69-152">Step 3</span></span>

<span data-ttu-id="58e69-153">De wijzigingen met behulp van de `Set-AzureRMDnsRecordSet cmdlet`, zoals wordt weergegeven in de onderstaande opdracht.</span><span class="sxs-lookup"><span data-stu-id="58e69-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="58e69-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58e69-154">Next steps</span></span>

<span data-ttu-id="58e69-155">Volg de stappen in [configureren van een aangepaste domeinnaam voor App Service](../app-service-web/web-sites-custom-domain-name.md) uw web-app voor het gebruik van een aangepast domein configureren.</span><span class="sxs-lookup"><span data-stu-id="58e69-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
