---
title: aaaCreate aangepaste DNS-records voor een web-app | Microsoft Docs
description: Hoe toocreate aangepast domein-DNS-records voor web-app met Azure DNS.
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
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="68dac-103">DNS-records voor een web-app maken in een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="68dac-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="68dac-104">U kunt Azure DNS toohost een aangepast domein voor uw web-apps gebruiken.</span><span class="sxs-lookup"><span data-stu-id="68dac-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="68dac-105">Bijvoorbeeld, u een Azure-web-app maakt en u wilt dat uw gebruikers tooaccess deze door een van beide contoso.com of www.contoso.com als een FQDN-naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="68dac-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="68dac-106">toodo, hebt u twee records toocreate:</span><span class="sxs-lookup"><span data-stu-id="68dac-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="68dac-107">Een record aan wijzen toocontoso.com voor hoofdmap "A"</span><span class="sxs-lookup"><span data-stu-id="68dac-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="68dac-108">Een 'CNAME'-record voor Hallo www-naam die toohello verwijst een record</span><span class="sxs-lookup"><span data-stu-id="68dac-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="68dac-109">Houd er rekening mee dat als u een A-record voor een web-app in Azure maakt, Hallo Hallo die een record moet handmatig worden bijgewerkt als onderliggende IP-adres voor Hallo web appwijzigingen.</span><span class="sxs-lookup"><span data-stu-id="68dac-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="68dac-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="68dac-110">Before you begin</span></span>

<span data-ttu-id="68dac-111">Voordat u begint, moet u eerst een DNS-zone maken in Azure DNS en Hallo zone delegeren in uw registrar tooAzure DNS.</span><span class="sxs-lookup"><span data-stu-id="68dac-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="68dac-112">een DNS-zone toocreate Hallo stappen in [maken van een DNS-zone](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="68dac-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="68dac-113">toodelegate uw DNS-tooAzure DNS, stappen Hallo in [DNS-domeindelegering](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="68dac-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="68dac-114">Na het maken van een zone en het overdragen van tooAzure DNS, kunt u vervolgens records maken voor uw aangepaste domein.</span><span class="sxs-lookup"><span data-stu-id="68dac-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="68dac-115">1. Maak een A-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="68dac-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="68dac-116">Een A-record is gebruikte toomap een naam tooits IP-adres.</span><span class="sxs-lookup"><span data-stu-id="68dac-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="68dac-117">In het volgende voorbeeld Hallo wordt we @ toewijzen als een A-record tooan IPv4-adres:</span><span class="sxs-lookup"><span data-stu-id="68dac-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="68dac-118">Stap 1</span><span class="sxs-lookup"><span data-stu-id="68dac-118">Step 1</span></span>

<span data-ttu-id="68dac-119">Een A-record maken en toewijzen tooa variabele $rs</span><span class="sxs-lookup"><span data-stu-id="68dac-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="68dac-120">Stap 2</span><span class="sxs-lookup"><span data-stu-id="68dac-120">Step 2</span></span>

<span data-ttu-id="68dac-121">Toevoegen Hallo IPv4 waarde toohello eerder gemaakte recordset ' @ ' hello $rs variabele toegewezen.</span><span class="sxs-lookup"><span data-stu-id="68dac-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="68dac-122">Hallo IPv4-waarde die is toegewezen worden Hallo IP-adres voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="68dac-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="68dac-123">toofind hello IP-adres voor een web-app Hallo stappen in [een aangepaste domeinnaam configureren in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="68dac-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="68dac-124">Stap 3</span><span class="sxs-lookup"><span data-stu-id="68dac-124">Step 3</span></span>

<span data-ttu-id="68dac-125">Hallo toohello Recordset-wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="68dac-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="68dac-126">Gebruik `Set-AzureRMDnsRecordSet` tooupload hello toohello Recordset tooAzure DNS-wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="68dac-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="68dac-127">2. Maak een CNAME-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="68dac-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="68dac-128">Als uw domein wordt al beheerd door Azure DNS (Zie [DNS-domeindelegering](dns-domain-delegation.md), kunt u Hallo Hallo voorbeeld toocreate een CNAME-record voor contoso.azurewebsites.net te volgen.</span><span class="sxs-lookup"><span data-stu-id="68dac-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="68dac-129">Stap 1</span><span class="sxs-lookup"><span data-stu-id="68dac-129">Step 1</span></span>

<span data-ttu-id="68dac-130">Open PowerShell en een nieuwe CNAME-recordset maken en toewijzen tooa variabele $rs.</span><span class="sxs-lookup"><span data-stu-id="68dac-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="68dac-131">In dit voorbeeld maakt u een Recordset type CNAME met een 'uitvoeringstijd toolive' 600 seconden in DNS-zone met de naam 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="68dac-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="68dac-132">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="68dac-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="68dac-133">Stap 2</span><span class="sxs-lookup"><span data-stu-id="68dac-133">Step 2</span></span>

<span data-ttu-id="68dac-134">Zodra Hallo CNAME-recordset is gemaakt, moet u toocreate een aliaswaarde die verwijst toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="68dac-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="68dac-135">U kunt met behulp van de eerder toegewezen variabele '$rs' Hallo Hallo PowerShell-opdracht hieronder toocreate Hallo alias gebruiken voor Hallo web app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="68dac-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="68dac-136">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="68dac-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="68dac-137">Stap 3</span><span class="sxs-lookup"><span data-stu-id="68dac-137">Step 3</span></span>

<span data-ttu-id="68dac-138">Hallo wijzigingen met behulp van Hallo `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="68dac-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="68dac-139">U kunt valideren Hallo record correct is gemaakt door het uitvoeren van query's Hallo 'www.contoso.com' met nslookup, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="68dac-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="68dac-140">Maak een 'awverify'-record voor web-apps</span><span class="sxs-lookup"><span data-stu-id="68dac-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="68dac-141">Als u toouse een A-record voor uw web-app besluit, moet u gaan via een proces verificatie tooensure u eigen Hallo aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="68dac-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="68dac-142">Deze verificatiestap wordt gedaan door het maken van een speciale CNAME-record met de naam 'awverify'.</span><span class="sxs-lookup"><span data-stu-id="68dac-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="68dac-143">Deze sectie geldt alleen voor tooA records.</span><span class="sxs-lookup"><span data-stu-id="68dac-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="68dac-144">Stap 1</span><span class="sxs-lookup"><span data-stu-id="68dac-144">Step 1</span></span>

<span data-ttu-id="68dac-145">Hallo 'awverify'-record maken.</span><span class="sxs-lookup"><span data-stu-id="68dac-145">Create hello "awverify" record.</span></span> <span data-ttu-id="68dac-146">We gaan Hallo 'aweverify'-record voor contoso.com tooverify eigendom van het aangepaste domein Hallo maken in Hallo onderstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="68dac-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="68dac-147">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="68dac-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="68dac-148">Stap 2</span><span class="sxs-lookup"><span data-stu-id="68dac-148">Step 2</span></span>

<span data-ttu-id="68dac-149">Zodra de recordset 'awverify' hello is gemaakt, wijs Hallo CNAME-Recordset alias.</span><span class="sxs-lookup"><span data-stu-id="68dac-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="68dac-150">In onderstaande Hallo voorbeeld, wijst Hallo CNAME-Recordset alias tooawverify.contoso.azurewebsites.net toe.</span><span class="sxs-lookup"><span data-stu-id="68dac-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="68dac-151">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="68dac-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="68dac-152">Stap 3</span><span class="sxs-lookup"><span data-stu-id="68dac-152">Step 3</span></span>

<span data-ttu-id="68dac-153">Hallo wijzigingen met behulp van Hallo `Set-AzureRMDnsRecordSet cmdlet`, zoals weergegeven in onderstaande Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="68dac-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="68dac-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68dac-154">Next steps</span></span>

<span data-ttu-id="68dac-155">Volg de stappen Hallo in [configureren van een aangepaste domeinnaam voor App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure uw web-app toouse een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="68dac-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
