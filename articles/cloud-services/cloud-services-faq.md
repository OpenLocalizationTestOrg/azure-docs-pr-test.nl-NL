---
title: aaaAzure Cloud Services-functies Veelgestelde vragen | Microsoft Docs
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="dcacb-104">Veelgestelde vragen over Cloud Services</span><span class="sxs-lookup"><span data-stu-id="dcacb-104">Cloud Services FAQ</span></span>
<span data-ttu-id="dcacb-105">Dit artikel worden enkele veelgestelde vragen over Microsoft Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="dcacb-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="dcacb-106">U kunt ook Hallo bezoeken [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure-prijzen en -ondersteuning voor informatie.</span><span class="sxs-lookup"><span data-stu-id="dcacb-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="dcacb-107">U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.</span><span class="sxs-lookup"><span data-stu-id="dcacb-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="dcacb-108">Certificaten</span><span class="sxs-lookup"><span data-stu-id="dcacb-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="dcacb-109">Waar moet ik mijn certificaat installeren?</span><span class="sxs-lookup"><span data-stu-id="dcacb-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="dcacb-110">**Mijn**</span><span class="sxs-lookup"><span data-stu-id="dcacb-110">**My**</span></span>  
  <span data-ttu-id="dcacb-111">Toepassingscertificaat met persoonlijke sleutel (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="dcacb-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="dcacb-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="dcacb-112">**CA**</span></span>  
  <span data-ttu-id="dcacb-113">Alle tussenliggende certificaten gaat u in dit archief (beleid en Sub-CA's).</span><span class="sxs-lookup"><span data-stu-id="dcacb-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="dcacb-114">**HOOFDMAP**</span><span class="sxs-lookup"><span data-stu-id="dcacb-114">**ROOT**</span></span>  
  <span data-ttu-id="dcacb-115">Hallo basis-CA opslaan, zodat uw belangrijkste basis-CA-certificaat hier moet gaan.</span><span class="sxs-lookup"><span data-stu-id="dcacb-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="dcacb-116">Ik kan verlopen certificaat niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="dcacb-116">I can't remove expired certificate</span></span>
<span data-ttu-id="dcacb-117">Azure voorkomt u dat u een certificaat verwijderen terwijl deze gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="dcacb-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="dcacb-118">U moet tooeither Hallo implementatie verwijderen die Hallo certificaat gebruikt of Hallo-update-implementatie met een certificaat verschillende of vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="dcacb-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="dcacb-119">Een verlopen certificaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="dcacb-119">Delete an expired certificate</span></span>
<span data-ttu-id="dcacb-120">Zolang het Hallo-certificaat niet wordt gebruikt, kunt u Hallo [verwijderen AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove een certificaat.</span><span class="sxs-lookup"><span data-stu-id="dcacb-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="dcacb-121">Ik zijn certificaten met de naam Windows Azure-servicebeheer voor uitbreidingen verlopen</span><span class="sxs-lookup"><span data-stu-id="dcacb-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="dcacb-122">Deze certificaten worden gemaakt wanneer een uitbreiding toohello-cloudservice, zoals Hallo extern bureaublad-extensie wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dcacb-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="dcacb-123">Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van de persoonlijke configuratie Hallo van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="dcacb-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="dcacb-124">Het maakt niet uit als deze certificaten verlopen.</span><span class="sxs-lookup"><span data-stu-id="dcacb-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="dcacb-125">Hallo-vervaldatum is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dcacb-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="dcacb-126">Certificaten die ik hebt verwijderd terugkomen</span><span class="sxs-lookup"><span data-stu-id="dcacb-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="dcacb-127">Deze terugkomen waarschijnlijk vanwege een hulpprogramma dat u gebruikt, zoals Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dcacb-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="dcacb-128">Wanneer u opnieuw verbinding met een hulpprogramma dat een certificaat gebruikt maken, wordt het geüploade tooAzure opnieuw zijn.</span><span class="sxs-lookup"><span data-stu-id="dcacb-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="dcacb-129">Mijn certificaten houden verdwijnen</span><span class="sxs-lookup"><span data-stu-id="dcacb-129">My certificates keep disappearing</span></span>
<span data-ttu-id="dcacb-130">Wanneer er wordt een exemplaar van de virtuele machine Hallo gerecycled, gaan alle lokale wijzigingen verloren.</span><span class="sxs-lookup"><span data-stu-id="dcacb-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="dcacb-131">Gebruik een [opstarttaak](cloud-services-startup-tasks.md) tooinstall certificaten toohello virtuele machine elke keer Hallo-rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="dcacb-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="dcacb-132">Ik kan mijn beheercertificaten niet vinden in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="dcacb-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="dcacb-133">[Certificaten voor](../azure-api-management-certs.md) zijn alleen beschikbaar in Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="dcacb-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="dcacb-134">Hallo huidige Azure-portal gebruikt geen beheercertificaten.</span><span class="sxs-lookup"><span data-stu-id="dcacb-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="dcacb-135">Hoe kan ik een beheercertificaat uitschakelen?</span><span class="sxs-lookup"><span data-stu-id="dcacb-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="dcacb-136">[Certificaten voor](../azure-api-management-certs.md) kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dcacb-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="dcacb-137">U verwijderen ze via de klassieke Azure-Portal Hallo wanneer u niet dat ze wilt toobe meer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dcacb-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="dcacb-138">Hoe maak ik een SSL-certificaat voor een specifiek IP-adres</span><span class="sxs-lookup"><span data-stu-id="dcacb-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="dcacb-139">Volg de aanwijzingen Hallo in Hallo [maken van een zelfstudie certificaat](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="dcacb-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="dcacb-140">Hallo IP-adres gebruiken zoals Hallo DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="dcacb-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="dcacb-141">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="dcacb-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="dcacb-142">SSL 3.0 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="dcacb-142">Disable SSL 3.0</span></span>
<span data-ttu-id="dcacb-143">toodisable SSL 3.0 en TLS-beveiliging gebruiken, op een opstarttaak maken die wordt beschreven in dit blogbericht: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="dcacb-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="dcacb-144">Voeg **nosniff** tooyour website</span><span class="sxs-lookup"><span data-stu-id="dcacb-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="dcacb-145">tooprevent-clients vanuit het bekijken van MIME-typen zijn hello, Voeg een instelling in uw *web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="dcacb-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="dcacb-146">U kunt dit ook toevoegen als een instelling in IIS.</span><span class="sxs-lookup"><span data-stu-id="dcacb-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="dcacb-147">Gebruik Hallo volgende opdracht Hello [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.</span><span class="sxs-lookup"><span data-stu-id="dcacb-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="dcacb-148">IIS voor een Webrol aanpassen</span><span class="sxs-lookup"><span data-stu-id="dcacb-148">Customize IIS for a web role</span></span>
<span data-ttu-id="dcacb-149">Gebruik Hallo IIS opstartscript van Hallo [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.</span><span class="sxs-lookup"><span data-stu-id="dcacb-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="dcacb-150">Schalen</span><span class="sxs-lookup"><span data-stu-id="dcacb-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="dcacb-151">Ik kan niet worden uitgebreid dan X exemplaren</span><span class="sxs-lookup"><span data-stu-id="dcacb-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="dcacb-152">Uw Azure-abonnement heeft een limiet op Hallo aantal kernen dat u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dcacb-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="dcacb-153">Schalen werkt niet als u alle Hallo kernen beschikbaar hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dcacb-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="dcacb-154">Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="dcacb-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="dcacb-155">Netwerken</span><span class="sxs-lookup"><span data-stu-id="dcacb-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="dcacb-156">Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's</span><span class="sxs-lookup"><span data-stu-id="dcacb-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="dcacb-157">Controleer eerst of de instantie van die Hallo-virtuele machine die u probeert tooreserve Hallo IP voor is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dcacb-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="dcacb-158">Controleer vervolgens of dat u gereserveerde IP-adressen voor bAndere Hallo fasering en productie-implementaties.</span><span class="sxs-lookup"><span data-stu-id="dcacb-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="dcacb-159">**Geen** Hallo-instellingen niet wijzigen terwijl het Hallo-implementatie worden geüpgraded.</span><span class="sxs-lookup"><span data-stu-id="dcacb-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="dcacb-160">Extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="dcacb-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="dcacb-161">Hoe kan ik extern bureaublad wanneer ik een NSG hebben?</span><span class="sxs-lookup"><span data-stu-id="dcacb-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="dcacb-162">Voeg regels toohello NSG waarmee verkeer op poorten **3389** en **20000**.</span><span class="sxs-lookup"><span data-stu-id="dcacb-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="dcacb-163">Extern bureaublad maakt gebruik van poort **3389**.</span><span class="sxs-lookup"><span data-stu-id="dcacb-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="dcacb-164">Cloud Service-exemplaren worden verdeeld, zodat u niet rechtstreeks welke tooconnect exemplaar om te controleren.</span><span class="sxs-lookup"><span data-stu-id="dcacb-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="dcacb-165">Hallo *RemoteForwarder* en *RemoteAccess* agents beheren van RDP-verkeer en Hallo client toosend een RDP-cookie toestaan en opgeven van een afzonderlijke instantie tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="dcacb-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="dcacb-166">Hallo *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.</span><span class="sxs-lookup"><span data-stu-id="dcacb-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
