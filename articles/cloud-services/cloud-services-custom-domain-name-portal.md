---
title: Een aangepaste domeinnaam configureren in Cloudservices | Microsoft Docs
description: Informatie over het weergeven van uw Azure-toepassing of de gegevens met het internet op een aangepast domein door DNS-instellingen configureren.  Deze voorbeelden worden de Azure portal gebruiken.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="94585-104">Een aangepaste domeinnaam voor een Azure-cloud-service configureren</span><span class="sxs-lookup"><span data-stu-id="94585-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94585-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94585-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="94585-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94585-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="94585-107">Wanneer u een Cloudservice maakt, Azure toegewezen aan een subdomein van **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="94585-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="94585-108">Bijvoorbeeld, als uw Cloudservice met de naam 'contoso', zich uw gebruikers toegang tot uw toepassing op een URL als http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="94585-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="94585-109">Azure wordt ook een virtueel IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="94585-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="94585-110">Echter, kan ook worden blootgesteld uw toepassing op uw eigen domeinnaam, zoals **contoso.com**. In dit artikel wordt uitgelegd hoe reserve of een aangepaste domeinnaam configureren voor Cloud Service-web-rollen.</span><span class="sxs-lookup"><span data-stu-id="94585-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="94585-111">U al begrijpen wat CNAME en A-records zijn?</span><span class="sxs-lookup"><span data-stu-id="94585-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="94585-112">[Korte inleiding voorbij de uitleg](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="94585-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="94585-113">De procedures in deze taak van toepassing op Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="94585-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="94585-114">Zie voor App-Services, [dit](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="94585-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="94585-115">Zie voor storage-accounts [dit](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="94585-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="94585-116">Aan de slag sneller--gebruik van de nieuwe Azure [scenario begeleide](http://support.microsoft.com/kb/2990804)!</span><span class="sxs-lookup"><span data-stu-id="94585-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="94585-117">Het maakt koppelen van een aangepaste domeinnaam en beveiligen van communicatie (SSL) met Azure Cloud Services of Azure Websites, een module.</span><span class="sxs-lookup"><span data-stu-id="94585-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="94585-118">Records CNAME en A begrijpen</span><span class="sxs-lookup"><span data-stu-id="94585-118">Understand CNAME and A records</span></span>
<span data-ttu-id="94585-119">CNAME (of aliasrecords) en een records kunnen u een domeinnaam koppelen aan een specifieke server (of service in dit geval) echter werken ze anders.</span><span class="sxs-lookup"><span data-stu-id="94585-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="94585-120">Er zijn ook enkele specifieke overwegingen bij het gebruik van A-records met Azure-Cloud-services die u overwegen moet voordat u besluit die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94585-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="94585-121">CNAME- of Alias-record</span><span class="sxs-lookup"><span data-stu-id="94585-121">CNAME or Alias record</span></span>
<span data-ttu-id="94585-122">Een CNAME-record verwijst een *specifieke* domein, zoals **contoso.com** of **www.contoso.com**, naar een canonieke domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="94585-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="94585-123">In dit geval de canonieke domeinnaam is de **[myapp] .cloudapp .net** domeinnaam van uw Azure gehoste toepassing.</span><span class="sxs-lookup"><span data-stu-id="94585-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="94585-124">Zodra gemaakt, CNAME maakt een alias voor de **[myapp] .cloudapp .net**.</span><span class="sxs-lookup"><span data-stu-id="94585-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="94585-125">De CNAME-vermelding wordt omgezet in het IP-adres van uw **[myapp] .cloudapp .net** service automatisch, zodat als het IP-adres van de cloudservice wordt gewijzigd, u hoeft geen actie te ondernemen.</span><span class="sxs-lookup"><span data-stu-id="94585-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="94585-126">Sommige registrars domein kunnen alleen u subdomeinen toewijzen wanneer u een CNAME-record, bijvoorbeeld www.contoso.com en geen basis-namen, zoals contoso.com. Zie voor meer informatie over de CNAME-records, de documentatie bij uw registrar [de vermelding Wikipedia (Engelstalig) op de CNAME-record](http://en.wikipedia.org/wiki/CNAME_record), of de [IETF domeinnamen - implementatie en specificatie](http://tools.ietf.org/html/rfc1035) document.</span><span class="sxs-lookup"><span data-stu-id="94585-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="94585-127">een record</span><span class="sxs-lookup"><span data-stu-id="94585-127">A record</span></span>
<span data-ttu-id="94585-128">Een *A* record wordt een domein, zoals toegewezen **contoso.com** of **www.contoso.com**, *of een jokertekendomein* zoals  **\*. contoso.com**, een IP-adres.</span><span class="sxs-lookup"><span data-stu-id="94585-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="94585-129">In het geval van een Azure Cloud Service, het virtuele IP-adres van de service.</span><span class="sxs-lookup"><span data-stu-id="94585-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="94585-130">Zodat het belangrijkste voordeel van een A-record via een CNAME-record is dat u kunt een vermelding die gebruikmaakt van een jokerteken, zoals \* **. contoso.com**, die zou staat aanvragen verwerken voor meerdere subdomeinen zoals **mail.contoso.com**, **login.contoso.com**, of **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="94585-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="94585-131">Omdat een A-record is toegewezen aan een statisch IP-adres, kan deze wijzigingen automatisch niet omzetten naar de IP-adres van uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="94585-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="94585-132">Het IP-adres wordt gebruikt door uw Cloud-Service is toegewezen de eerste keer dat u implementeert op een lege sleuf (productie of staging.) Als u de implementatie voor de site verwijdert, wordt het IP-adres wordt vrijgegeven door Azure en alle toekomstige implementaties in de sleuf kunnen een nieuw IP-adres worden gegeven.</span><span class="sxs-lookup"><span data-stu-id="94585-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="94585-133">Het IP-adres van een opgegeven implementatiesleuf (productie of staging) is gemakkelijk persistent bij het wisselen tussen fasering en productie-implementaties of het uitvoeren van een in-place upgrade van een bestaande implementatie.</span><span class="sxs-lookup"><span data-stu-id="94585-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="94585-134">Zie voor meer informatie over het uitvoeren van deze acties [cloudservices beheren](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="94585-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="94585-135">Voeg een CNAME-record voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="94585-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="94585-136">Als u wilt een CNAME-record maken, moet u een nieuwe vermelding in de DNS-tabel voor uw aangepaste domein toevoegen met behulp van de hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="94585-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="94585-137">Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een CNAME-record, maar de concepten zijn hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="94585-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="94585-138">Gebruik een van deze methoden om te zoeken naar de **. cloudapp.net** domeinnaam toegewezen aan uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="94585-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="94585-139">Meld u aan bij de [Azure-portal], selecteer uw cloudservice, kijkt u naar de **Essentials** sectie en gaat u naar de **Site-URL** vermelding.</span><span class="sxs-lookup"><span data-stu-id="94585-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![snelle weergave sectie URL van de site wordt weergegeven][csurl]
     
       <span data-ttu-id="94585-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="94585-141">**OR**</span></span>
   * <span data-ttu-id="94585-142">Installeer en configureer [Azure Powershell](/powershell/azure/overview), en gebruik vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="94585-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="94585-143">Sla de domeinnaam die is gebruikt in de URL die is geretourneerd door een van de methoden, zoals u deze hebt bij het maken van een CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="94585-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="94585-144">Meld u aan bij uw DNS-registratieservice website en Ga naar de pagina voor het beheren van DNS.</span><span class="sxs-lookup"><span data-stu-id="94585-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="94585-145">Zoek naar koppelingen of gebieden van de site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="94585-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="94585-146">Nu kunt u selecteren of invoeren van CNAME zoeken.</span><span class="sxs-lookup"><span data-stu-id="94585-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="94585-147">Mogelijk moet het recordtype in een vervolgkeuzelijst omlaag selecteren of Ga naar een pagina Geavanceerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="94585-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="94585-148">U ziet er voor de woorden **CNAME**, **Alias**, of **subdomeinen**.</span><span class="sxs-lookup"><span data-stu-id="94585-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="94585-149">U moet ook Geef het domein of subdomein alias voor de CNAME, zoals **www** als u wilt maken van een alias voor **www.customdomain.com**. Als u een alias maken voor het hoofddomein wilt, kan dit worden vermeld als de '**@**' symbool in DNS-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="94585-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="94585-150">Vervolgens moet u een canonieke hostnaam, uw toepassing is opgeven **cloudapp.net** domein in dit geval.</span><span class="sxs-lookup"><span data-stu-id="94585-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="94585-151">Bijvoorbeeld de volgende CNAME-record al het verkeer van stuurt **www.contoso.com** naar **contoso.cloudapp.net**, de aangepaste domeinnaam van uw geïmplementeerde toepassing:</span><span class="sxs-lookup"><span data-stu-id="94585-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="94585-152">Alias/Host-naam/subdomein</span><span class="sxs-lookup"><span data-stu-id="94585-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="94585-153">Canonieke domein</span><span class="sxs-lookup"><span data-stu-id="94585-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="94585-154">www</span><span class="sxs-lookup"><span data-stu-id="94585-154">www</span></span> |<span data-ttu-id="94585-155">Contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="94585-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="94585-156">Een bezoeker van **www.contoso.com** Zie nooit de waar host (contoso.cloudapp.net), zodat het proces doorsturen onzichtbaar voor de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="94585-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="94585-157">Het bovenstaande voorbeeld is alleen van toepassing op het verkeer bij de **www** subdomein.</span><span class="sxs-lookup"><span data-stu-id="94585-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="94585-158">Aangezien u kunt geen jokertekens CNAME-records gebruiken, moet u een CNAME voor elk domein/subdomein maken.</span><span class="sxs-lookup"><span data-stu-id="94585-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="94585-159">Als u wilt dat om verkeer te regelen van subdomeinen, zoals *. contoso.com naar uw adres cloudapp.net, kunt u een **Omleidings-URL** of **URL doorsturen** vermelding in uw DNS-instellingen, of maak een A-record.</span><span class="sxs-lookup"><span data-stu-id="94585-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="94585-160">Een A-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="94585-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="94585-161">Voor het maken van een A-record, moet u het virtuele IP-adres van uw cloudservice te zoeken.</span><span class="sxs-lookup"><span data-stu-id="94585-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="94585-162">Voeg een nieuwe vermelding in de DNS-tabel voor uw aangepaste domein met behulp van de hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="94585-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="94585-163">Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een A-record, maar de concepten zijn hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="94585-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="94585-164">Gebruik een van de volgende methoden om het IP-adres van uw cloudservice ophalen.</span><span class="sxs-lookup"><span data-stu-id="94585-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="94585-165">Meld u aan bij de [Azure-portal], selecteer uw cloudservice, kijkt u naar de **Essentials** sectie en gaat u naar de **openbare IP-adressen** vermelding.</span><span class="sxs-lookup"><span data-stu-id="94585-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![snelle weergave sectie waarin het VIP][vip]
     
       <span data-ttu-id="94585-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="94585-167">**OR**</span></span>
   * <span data-ttu-id="94585-168">Installeer en configureer [Azure Powershell](/powershell/azure/overview), en gebruik vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="94585-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="94585-169">Sla het IP-adres, zoals u deze hebt bij het maken van een A-record.</span><span class="sxs-lookup"><span data-stu-id="94585-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="94585-170">Meld u aan bij uw DNS-registratieservice website en Ga naar de pagina voor het beheren van DNS.</span><span class="sxs-lookup"><span data-stu-id="94585-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="94585-171">Zoek naar koppelingen of gebieden van de site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="94585-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="94585-172">Nu kunt u selecteren of invoeren van de record zoeken.</span><span class="sxs-lookup"><span data-stu-id="94585-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="94585-173">Mogelijk moet het recordtype in een vervolgkeuzelijst omlaag selecteren of Ga naar een pagina Geavanceerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="94585-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="94585-174">Selecteer of typ het domein of subdomein die door deze A-record wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94585-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="94585-175">Selecteer bijvoorbeeld **www** als u wilt maken van een alias voor **www.customdomain.com**. Als u maken van een vermelding jokerteken voor alle subdomeinen wilt, voert u ' ***'.</span><span class="sxs-lookup"><span data-stu-id="94585-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="94585-176">Hierin vindt u alle subdomeinen zoals **mail.customdomain.com**, **login.customdomain.com**, en **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="94585-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="94585-177">Als u maken van een A-record voor het hoofddomein wilt, kan dit worden vermeld als de '**@**' symbool in DNS-hulpprogramma's van uw registrar.</span><span class="sxs-lookup"><span data-stu-id="94585-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="94585-178">Geef het IP-adres van uw cloudservice in het opgegeven veld.</span><span class="sxs-lookup"><span data-stu-id="94585-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="94585-179">Hiermee wordt de domein-vermelding in de A-record met het IP-adres van uw cloud service-implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94585-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="94585-180">Bijvoorbeeld, het volgende een record al het verkeer van stuurt **contoso.com** naar **137.135.70.239**, het IP-adres van uw geïmplementeerde toepassing:</span><span class="sxs-lookup"><span data-stu-id="94585-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="94585-181">Host-naam/subdomein</span><span class="sxs-lookup"><span data-stu-id="94585-181">Host name/Subdomain</span></span> | <span data-ttu-id="94585-182">IP-adres</span><span class="sxs-lookup"><span data-stu-id="94585-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="94585-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="94585-183">137.135.70.239</span></span> |

<span data-ttu-id="94585-184">Dit voorbeeld wordt het maken van een A-record voor het hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="94585-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="94585-185">Als u maken van een vermelding jokertekens ten aanzien van alle subdomeinen wilt, voert u ' ***' als het subdomein.</span><span class="sxs-lookup"><span data-stu-id="94585-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="94585-186">IP-adressen in Azure zijn standaard dynamisch.</span><span class="sxs-lookup"><span data-stu-id="94585-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="94585-187">Wilt u waarschijnlijk gebruik van een [gereserveerd IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) om ervoor te zorgen dat uw IP-adres niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="94585-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="94585-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94585-188">Next steps</span></span>
* [<span data-ttu-id="94585-189">Cloud Services beheren</span><span class="sxs-lookup"><span data-stu-id="94585-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="94585-190">CDN-inhoud toewijzen aan een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="94585-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="94585-191">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94585-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="94585-192">Meer informatie over hoe [implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94585-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="94585-193">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94585-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure-portal]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
