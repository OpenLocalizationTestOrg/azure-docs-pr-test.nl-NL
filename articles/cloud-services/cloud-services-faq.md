---
title: Azure Cloud Services-functies Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen over Azure Cloud Services. Antwoorden op enkele veelgestelde vragen over certificaten, webrollen en werkrollen.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="65ca3-104">Veelgestelde vragen over Cloud Services</span><span class="sxs-lookup"><span data-stu-id="65ca3-104">Cloud Services FAQ</span></span>
<span data-ttu-id="65ca3-105">Dit artikel worden enkele veelgestelde vragen over Microsoft Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="65ca3-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="65ca3-106">U kunt ook de [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure-prijzen en -ondersteuning voor informatie.</span><span class="sxs-lookup"><span data-stu-id="65ca3-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="65ca3-107">U kunt ook raadpleegt u de [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.</span><span class="sxs-lookup"><span data-stu-id="65ca3-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="65ca3-108">Certificaten</span><span class="sxs-lookup"><span data-stu-id="65ca3-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="65ca3-109">Waar moet ik mijn certificaat installeren?</span><span class="sxs-lookup"><span data-stu-id="65ca3-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="65ca3-110">**Mijn**</span><span class="sxs-lookup"><span data-stu-id="65ca3-110">**My**</span></span>  
  <span data-ttu-id="65ca3-111">Toepassingscertificaat met persoonlijke sleutel (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="65ca3-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="65ca3-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="65ca3-112">**CA**</span></span>  
  <span data-ttu-id="65ca3-113">Alle tussenliggende certificaten gaat u in dit archief (beleid en Sub-CA's).</span><span class="sxs-lookup"><span data-stu-id="65ca3-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="65ca3-114">**HOOFDMAP**</span><span class="sxs-lookup"><span data-stu-id="65ca3-114">**ROOT**</span></span>  
  <span data-ttu-id="65ca3-115">De basis-CA opslaan, zodat uw belangrijkste basis-CA-certificaat hier moet gaan.</span><span class="sxs-lookup"><span data-stu-id="65ca3-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="65ca3-116">Ik kan verlopen certificaat niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="65ca3-116">I can't remove expired certificate</span></span>
<span data-ttu-id="65ca3-117">Azure voorkomt u dat u een certificaat verwijderen terwijl deze gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="65ca3-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="65ca3-118">U moet aan de implementatie die gebruikmaakt van het certificaat te verwijderen of bijwerken van de implementatie met een andere of vernieuwd certificaat.</span><span class="sxs-lookup"><span data-stu-id="65ca3-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="65ca3-119">Een verlopen certificaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="65ca3-119">Delete an expired certificate</span></span>
<span data-ttu-id="65ca3-120">Zolang het certificaat niet gebruikt wordt, kunt u de [verwijderen AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell-cmdlet om te verwijderen van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="65ca3-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="65ca3-121">Ik zijn certificaten met de naam Windows Azure-servicebeheer voor uitbreidingen verlopen</span><span class="sxs-lookup"><span data-stu-id="65ca3-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="65ca3-122">Deze certificaten worden gemaakt wanneer een uitbreiding wordt toegevoegd aan de cloudservice, zoals de extern bureaublad-extensie.</span><span class="sxs-lookup"><span data-stu-id="65ca3-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="65ca3-123">Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van de persoonlijke configuratie van de extensie.</span><span class="sxs-lookup"><span data-stu-id="65ca3-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="65ca3-124">Het maakt niet uit als deze certificaten verlopen.</span><span class="sxs-lookup"><span data-stu-id="65ca3-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="65ca3-125">De verloopdatum is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="65ca3-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="65ca3-126">Certificaten die ik hebt verwijderd terugkomen</span><span class="sxs-lookup"><span data-stu-id="65ca3-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="65ca3-127">Deze terugkomen waarschijnlijk vanwege een hulpprogramma dat u gebruikt, zoals Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65ca3-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="65ca3-128">Wanneer u opnieuw verbinding met een hulpprogramma dat een certificaat gebruikt maken, wordt deze opnieuw worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="65ca3-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="65ca3-129">Mijn certificaten houden verdwijnen</span><span class="sxs-lookup"><span data-stu-id="65ca3-129">My certificates keep disappearing</span></span>
<span data-ttu-id="65ca3-130">Wanneer een exemplaar van de virtuele machine wordt gerecycled, gaan alle lokale wijzigingen verloren.</span><span class="sxs-lookup"><span data-stu-id="65ca3-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="65ca3-131">Gebruik een [opstarttaak](cloud-services-startup-tasks.md) om certificaten te installeren op de virtuele machine telkens wanneer de functie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="65ca3-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="65ca3-132">Ik kan mijn beheercertificaten niet vinden in de portal</span><span class="sxs-lookup"><span data-stu-id="65ca3-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="65ca3-133">[Certificaten voor](../azure-api-management-certs.md) zijn alleen beschikbaar in de klassieke Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="65ca3-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="65ca3-134">De huidige Azure-portal gebruikt geen beheercertificaten.</span><span class="sxs-lookup"><span data-stu-id="65ca3-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="65ca3-135">Hoe kan ik een beheercertificaat uitschakelen?</span><span class="sxs-lookup"><span data-stu-id="65ca3-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="65ca3-136">[Certificaten voor](../azure-api-management-certs.md) kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="65ca3-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="65ca3-137">U verwijdert deze via de klassieke Azure-Portal als u niet wilt dat meer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65ca3-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="65ca3-138">Hoe maak ik een SSL-certificaat voor een specifiek IP-adres</span><span class="sxs-lookup"><span data-stu-id="65ca3-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="65ca3-139">Volg de aanwijzingen in de [maken van een zelfstudie certificaat](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="65ca3-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="65ca3-140">Gebruik het IP-adres als de DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="65ca3-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="65ca3-141">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="65ca3-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="65ca3-142">SSL 3.0 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="65ca3-142">Disable SSL 3.0</span></span>
<span data-ttu-id="65ca3-143">Als u wilt uitschakelen, SSL 3.0 en TLS-beveiliging, op een opstarttaak maken die wordt beschreven in dit blogbericht: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="65ca3-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="65ca3-144">Voeg **nosniff** aan uw website</span><span class="sxs-lookup"><span data-stu-id="65ca3-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="65ca3-145">Voeg een instelling in om te voorkomen dat clients de MIME-typen voor het bewaken van netwerken voor uw *web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="65ca3-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="65ca3-146">U kunt dit ook toevoegen als een instelling in IIS.</span><span class="sxs-lookup"><span data-stu-id="65ca3-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="65ca3-147">Gebruik de volgende opdracht met de [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.</span><span class="sxs-lookup"><span data-stu-id="65ca3-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="65ca3-148">IIS voor een Webrol aanpassen</span><span class="sxs-lookup"><span data-stu-id="65ca3-148">Customize IIS for a web role</span></span>
<span data-ttu-id="65ca3-149">Het script voor het opstarten van IIS uit de [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.</span><span class="sxs-lookup"><span data-stu-id="65ca3-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="65ca3-150">Schalen</span><span class="sxs-lookup"><span data-stu-id="65ca3-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="65ca3-151">Ik kan niet worden uitgebreid dan X exemplaren</span><span class="sxs-lookup"><span data-stu-id="65ca3-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="65ca3-152">Uw Azure-abonnement heeft een limiet van het aantal kernen dat u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65ca3-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="65ca3-153">Schalen werkt niet als u de beschikbare kernen hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65ca3-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="65ca3-154">Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="65ca3-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="65ca3-155">Netwerken</span><span class="sxs-lookup"><span data-stu-id="65ca3-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="65ca3-156">Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's</span><span class="sxs-lookup"><span data-stu-id="65ca3-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="65ca3-157">Controleer eerst of de instantie van de virtuele machine die u probeert te reserveren van de IP voor is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="65ca3-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="65ca3-158">Controleer vervolgens of dat u gereserveerde IP-adressen voor bAndere de fasering en productie-implementaties.</span><span class="sxs-lookup"><span data-stu-id="65ca3-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="65ca3-159">**Geen** de instellingen niet wijzigen terwijl het upgraden van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="65ca3-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="65ca3-160">Extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="65ca3-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="65ca3-161">Hoe kan ik extern bureaublad wanneer ik een NSG hebben?</span><span class="sxs-lookup"><span data-stu-id="65ca3-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="65ca3-162">Regels toevoegen aan het NSG waarmee verkeer op poorten **3389** en **20000**.</span><span class="sxs-lookup"><span data-stu-id="65ca3-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="65ca3-163">Extern bureaublad maakt gebruik van poort **3389**.</span><span class="sxs-lookup"><span data-stu-id="65ca3-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="65ca3-164">Cloud Service-exemplaren worden verdeeld, zodat u direct welk exemplaar verbinding maken met kan niet bepalen.</span><span class="sxs-lookup"><span data-stu-id="65ca3-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="65ca3-165">De *RemoteForwarder* en *RemoteAccess* agents RDP-verkeer te beheren en dat de client verzenden van een cookie RDP en geeft u een afzonderlijk exemplaar verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="65ca3-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="65ca3-166">De *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.</span><span class="sxs-lookup"><span data-stu-id="65ca3-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
