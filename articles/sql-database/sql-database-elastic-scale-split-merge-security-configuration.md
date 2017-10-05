---
title: Gesplitste samenvoegen Beveiligingsconfiguratie | Microsoft Docs
description: Instellen van x409 certificaten voor versleuteling
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="6bba2-103">Gesplitste samenvoegen Beveiligingsconfiguratie</span><span class="sxs-lookup"><span data-stu-id="6bba2-103">Split-merge security configuration</span></span>
<span data-ttu-id="6bba2-104">Als u wilt de splitsing/Merge-service gebruikt, moet u correct beveiliging configureren.</span><span class="sxs-lookup"><span data-stu-id="6bba2-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="6bba2-105">De service maakt deel uit van de functie van de elastische Schaalfunctionaliteit van Microsoft Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6bba2-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="6bba2-106">Zie voor meer informatie [elastische Scale splitsen en Merge-zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="6bba2-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="6bba2-107">Configureren van certificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-107">Configuring certificates</span></span>
<span data-ttu-id="6bba2-108">Certificaten worden op twee manieren geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6bba2-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="6bba2-109">Het SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="6bba2-110">Voor het configureren van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="6bba2-111">Om certificaten te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="6bba2-111">To obtain certificates</span></span>
<span data-ttu-id="6bba2-112">Certificaten kunnen worden opgehaald van openbare certificeringsinstanties (CA's) of van de [Windows certificaatservice](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bba2-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="6bba2-113">Dit zijn de aanbevolen methoden om certificaten te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="6bba2-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="6bba2-114">Als u deze opties niet beschikbaar zijn, kunt u genereren **zelfondertekende certificaten**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="6bba2-115">Hulpprogramma's voor het genereren van certificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="6bba2-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="6bba2-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="6bba2-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="6bba2-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="6bba2-118">De hulpprogramma's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-118">To run the tools</span></span>
* <span data-ttu-id="6bba2-119">Zie van ontwikkelaars vanaf de opdrachtprompt voor Visual Studios [Visual Studio-opdrachtprompt](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="6bba2-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="6bba2-120">Als u hebt geïnstalleerd, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="6bba2-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="6bba2-121">Ophalen van de WDK van [Windows 8.1: Download kits en hulpprogramma's](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="6bba2-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="6bba2-122">Het SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-122">To configure the SSL certificate</span></span>
<span data-ttu-id="6bba2-123">Een SSL-certificaat is vereist voor het versleutelen van de communicatie en de server te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="6bba2-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="6bba2-124">Kies het meest van toepassing van de onderstaande drie scenario's en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="6bba2-125">Een nieuw zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="6bba2-126">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6bba2-127">PFX-bestand voor zelfondertekende SSL-certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6bba2-128">Cloud Service SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="6bba2-129">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="6bba2-130">SSL-certificeringsinstantie importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="6bba2-131">Een bestaand certificaat uit het certificaatarchief gebruiken</span><span class="sxs-lookup"><span data-stu-id="6bba2-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="6bba2-132">SSL-certificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="6bba2-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="6bba2-133">Cloud Service SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="6bba2-134">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6bba2-135">Een bestaand certificaat gebruiken in een PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="6bba2-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6bba2-136">Cloud Service SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="6bba2-137">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="6bba2-138">Voor het configureren van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-138">To configure client certificates</span></span>
<span data-ttu-id="6bba2-139">Clientcertificaten zijn vereist voor het verifiëren van aanvragen voor de service.</span><span class="sxs-lookup"><span data-stu-id="6bba2-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="6bba2-140">Kies het meest van toepassing van de onderstaande drie scenario's en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="6bba2-141">Clientcertificaten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6bba2-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="6bba2-142">Op basis van certificaten clientverificatie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6bba2-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="6bba2-143">Nieuwe zelfondertekende certificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="6bba2-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="6bba2-144">Een zelfondertekend certificeringsinstantie maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="6bba2-145">Uploaden van de CA-certificaat voor de Cloudservice</span><span class="sxs-lookup"><span data-stu-id="6bba2-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="6bba2-146">CA-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="6bba2-147">Clientcertificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="6bba2-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="6bba2-148">PFX-bestanden maken voor clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="6bba2-149">Client-certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="6bba2-150">Certificaatvingerafdrukken Client kopiëren</span><span class="sxs-lookup"><span data-stu-id="6bba2-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="6bba2-151">Toegestane Clients in het configuratiebestand van de Service configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="6bba2-152">Bestaande clientcertificaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="6bba2-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="6bba2-153">Vinden van openbare sleutel van CA</span><span class="sxs-lookup"><span data-stu-id="6bba2-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="6bba2-154">Uploaden van de CA-certificaat voor de Cloudservice</span><span class="sxs-lookup"><span data-stu-id="6bba2-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="6bba2-155">CA-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="6bba2-156">Certificaatvingerafdrukken Client kopiëren</span><span class="sxs-lookup"><span data-stu-id="6bba2-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="6bba2-157">Toegestane Clients in het configuratiebestand van de Service configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="6bba2-158">Controle van certificaatintrekking Client configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="6bba2-159">Toegestane IP-adressen</span><span class="sxs-lookup"><span data-stu-id="6bba2-159">Allowed IP addresses</span></span>
<span data-ttu-id="6bba2-160">Toegang tot de service-eindpunten kan worden beperkt tot specifieke bereiken van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="6bba2-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="6bba2-161">Versleuteling voor de store te configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-161">To configure encryption for the store</span></span>
<span data-ttu-id="6bba2-162">Een certificaat is vereist voor het versleutelen van de referenties die zijn opgeslagen in het metagegevensarchief met.</span><span class="sxs-lookup"><span data-stu-id="6bba2-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="6bba2-163">Kies het meest van toepassing van de onderstaande drie scenario's en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="6bba2-164">Een nieuw zelfondertekend certificaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="6bba2-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="6bba2-165">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6bba2-166">PFX-bestand voor het versleutelingscertificaat zelfondertekend maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6bba2-167">Versleutelingscertificaat cloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="6bba2-168">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="6bba2-169">Een bestaand certificaat uit het certificaatarchief gebruiken</span><span class="sxs-lookup"><span data-stu-id="6bba2-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="6bba2-170">Versleutelingscertificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="6bba2-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="6bba2-171">Versleutelingscertificaat cloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="6bba2-172">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6bba2-173">Een bestaand certificaat gebruiken in een PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="6bba2-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6bba2-174">Versleutelingscertificaat cloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="6bba2-175">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="6bba2-176">De standaardconfiguratie</span><span class="sxs-lookup"><span data-stu-id="6bba2-176">The default configuration</span></span>
<span data-ttu-id="6bba2-177">De standaardconfiguratie weigert alle toegang tot het HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="6bba2-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="6bba2-178">Dit is de aanbevolen instelling, aangezien de aanvragen voor deze eindpunten gevoelige informatie, zoals databasereferenties mag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6bba2-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="6bba2-179">De standaardconfiguratie kunt alle toegang tot het HTTPS-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="6bba2-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="6bba2-180">Deze instelling kan verder worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="6bba2-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="6bba2-181">Wijzigen van de configuratie</span><span class="sxs-lookup"><span data-stu-id="6bba2-181">Changing the Configuration</span></span>
<span data-ttu-id="6bba2-182">De groep toegangscontroleregels die gelden voor- en eindpunt zijn geconfigureerd in de  **<EndpointAcls>**  sectie het **serviceconfiguratiebestand**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="6bba2-183">De regels in een besturingselement toegangsgroep zijn geconfigureerd in een <AccessControl name=""> gedeelte van het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="6bba2-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="6bba2-184">De indeling wordt uitgelegd in de documentatie voor Network Access Control Lists.</span><span class="sxs-lookup"><span data-stu-id="6bba2-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="6bba2-185">Bijvoorbeeld, zodat alleen IP-adressen in het bereik 100.100.0.0-100.100.255.255 voor toegang tot het HTTPS-eindpunt eruit de regels als volgt:</span><span class="sxs-lookup"><span data-stu-id="6bba2-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="6bba2-186">Denial of service te voorkomen</span><span class="sxs-lookup"><span data-stu-id="6bba2-186">Denial of service prevention</span></span>
<span data-ttu-id="6bba2-187">Er zijn twee verschillende methoden die worden ondersteund om te detecteren en Denial of Service-aanvallen te voorkomen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="6bba2-188">Beperk het aantal gelijktijdige aanvragen per externe host (standaard uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="6bba2-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="6bba2-189">Snelheid van toegang per externe host beperken (op standaard)</span><span class="sxs-lookup"><span data-stu-id="6bba2-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="6bba2-190">Deze zijn gebaseerd op de functies die verder beschreven in de dynamische IP-beveiliging in IIS.</span><span class="sxs-lookup"><span data-stu-id="6bba2-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="6bba2-191">Wanneer deze configuratie wijzigen pas op de volgende factoren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="6bba2-192">Het gedrag van proxy's en apparaten via de externe hostinformatie Network Address Translation</span><span class="sxs-lookup"><span data-stu-id="6bba2-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="6bba2-193">Elke aanvraag naar een resource in de Webrol wordt beschouwd (bijvoorbeeld bij het laden van scripts, afbeeldingen, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="6bba2-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="6bba2-194">Het aantal gelijktijdige toegang beperken</span><span class="sxs-lookup"><span data-stu-id="6bba2-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="6bba2-195">De instellingen die voor het configureren van dit probleem zijn:</span><span class="sxs-lookup"><span data-stu-id="6bba2-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="6bba2-196">Wijzig DynamicIpRestrictionDenyByConcurrentRequests in waar deze beveiliging in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="6bba2-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="6bba2-197">Snelheid van de toegang beperken</span><span class="sxs-lookup"><span data-stu-id="6bba2-197">Restricting rate of access</span></span>
<span data-ttu-id="6bba2-198">De instellingen die voor het configureren van dit probleem zijn:</span><span class="sxs-lookup"><span data-stu-id="6bba2-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="6bba2-199">Het antwoord op een geweigerde aanvraag configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="6bba2-200">De volgende instelling configureert u het antwoord op een aanvraag afgewezen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="6bba2-201">Raadpleeg de documentatie voor dynamische IP-beveiliging in IIS voor andere ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="6bba2-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="6bba2-202">Bewerkingen voor het configureren van servicecertificaten</span><span class="sxs-lookup"><span data-stu-id="6bba2-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="6bba2-203">Dit onderwerp is alleen ter informatie.</span><span class="sxs-lookup"><span data-stu-id="6bba2-203">This topic is for reference only.</span></span> <span data-ttu-id="6bba2-204">Volg de configuratiestappen die worden beschreven in:</span><span class="sxs-lookup"><span data-stu-id="6bba2-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="6bba2-205">De SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="6bba2-206">Clientcertificaten configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="6bba2-207">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-207">Create a self-signed certificate</span></span>
<span data-ttu-id="6bba2-208">Uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="6bba2-209">Om aan te passen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-209">To customize:</span></span>

* <span data-ttu-id="6bba2-210">-n met de service-URL.</span><span class="sxs-lookup"><span data-stu-id="6bba2-210">-n with the service URL.</span></span> <span data-ttu-id="6bba2-211">Jokertekens ("CN = * .cloudapp .net ') en alternatieve namen (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net') worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6bba2-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="6bba2-212">e - met de vervaldatum van het certificaat een sterk wachtwoord maken en geef hem wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="6bba2-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="6bba2-213">PFX-bestand voor zelf-ondertekend SSL-certificaat maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="6bba2-214">Uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="6bba2-215">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6bba2-216">Ja, de persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-216">Yes, export the private key</span></span>
* <span data-ttu-id="6bba2-217">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="6bba2-218">SSL-certificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="6bba2-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="6bba2-219">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="6bba2-219">Find certificate</span></span>
* <span data-ttu-id="6bba2-220">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="6bba2-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6bba2-221">Exporteer het certificaat in een. PFX-bestand met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="6bba2-222">Ja, de persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-222">Yes, export the private key</span></span>
  * <span data-ttu-id="6bba2-223">Indien mogelijk exporteren met alle certificaten in het certificeringspad * alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="6bba2-224">SSL-certificaat uploaden naar cloudservice</span><span class="sxs-lookup"><span data-stu-id="6bba2-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="6bba2-225">Uploaden van het certificaat met de bestaande of gegenereerd. PFX-bestand met de SSL-sleutelpaar:</span><span class="sxs-lookup"><span data-stu-id="6bba2-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="6bba2-226">Voer het wachtwoord voor het beveiligen van gegevens van de persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="6bba2-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="6bba2-227">SSL-certificaat in het configuratiebestand van de service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="6bba2-228">Werk de vingerafdrukwaarde van de volgende instelling in het configuratiebestand van de service met de vingerafdruk van het certificaat dat is geüpload naar de cloudservice:</span><span class="sxs-lookup"><span data-stu-id="6bba2-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="6bba2-229">SSL-certificeringsinstantie importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-229">Import SSL certification authority</span></span>
<span data-ttu-id="6bba2-230">Volg deze stappen in alle account/machine die communiceert met de service:</span><span class="sxs-lookup"><span data-stu-id="6bba2-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="6bba2-231">Dubbelklik op de. CER-bestand in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="6bba2-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="6bba2-232">Klik in het dialoogvenster certificaat certificaat installeren...</span><span class="sxs-lookup"><span data-stu-id="6bba2-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="6bba2-233">Certificaat importeren in het archief Vertrouwde basiscertificeringsinstanties</span><span class="sxs-lookup"><span data-stu-id="6bba2-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="6bba2-234">Op basis van certificaten clientverificatie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6bba2-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="6bba2-235">Alleen op basis van certificaten clientverificatie wordt ondersteund en u dit uitschakelt wilt toestaan voor openbare toegang tot de service-eindpunten, tenzij andere beveiligingsmechanismen geïmplementeerd (zoals Microsoft Azure Virtual Network) zijn.</span><span class="sxs-lookup"><span data-stu-id="6bba2-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="6bba2-236">Deze instellingen wijzigen in false in het serviceconfiguratiebestand de functie om uit te schakelen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="6bba2-237">Kopieer de vingerafdruk van het hetzelfde als het SSL-certificaat in de instelling voor CA-certificaat:</span><span class="sxs-lookup"><span data-stu-id="6bba2-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="6bba2-238">Een zelfondertekend certificeringsinstantie maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="6bba2-239">De volgende stappen voor het maken van een zelfondertekend certificaat om te fungeren als een certificeringsinstantie worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6bba2-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="6bba2-240">Aanpassen</span><span class="sxs-lookup"><span data-stu-id="6bba2-240">To customize it</span></span>

* <span data-ttu-id="6bba2-241">e - met de vervaldatum van de certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="6bba2-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="6bba2-242">Vinden van openbare sleutel van CA</span><span class="sxs-lookup"><span data-stu-id="6bba2-242">Find CA public key</span></span>
<span data-ttu-id="6bba2-243">Alle clientcertificaten zijn uitgegeven door een certificeringsinstantie wordt vertrouwd door de service.</span><span class="sxs-lookup"><span data-stu-id="6bba2-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="6bba2-244">De openbare sleutel aan de certificeringsinstantie die certificaten de client die u gebruikt voor verificatie om te uploaden naar de cloudservice vinden.</span><span class="sxs-lookup"><span data-stu-id="6bba2-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="6bba2-245">Als het bestand met de openbare sleutel niet beschikbaar is, uit het certificaatarchief exporteren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="6bba2-246">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="6bba2-246">Find certificate</span></span>
  * <span data-ttu-id="6bba2-247">Zoeken naar een clientcertificaat dat is uitgegeven door de dezelfde certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="6bba2-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="6bba2-248">Dubbelklik op het certificaat.</span><span class="sxs-lookup"><span data-stu-id="6bba2-248">Double-click the certificate.</span></span>
* <span data-ttu-id="6bba2-249">Selecteer het tabblad certificeringspad in het dialoogvenster certificaat.</span><span class="sxs-lookup"><span data-stu-id="6bba2-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="6bba2-250">Dubbelklik op de CA-vermelding in het pad.</span><span class="sxs-lookup"><span data-stu-id="6bba2-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="6bba2-251">Notities van de eigenschappen voor certificaat.</span><span class="sxs-lookup"><span data-stu-id="6bba2-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="6bba2-252">Sluit de **certificaat** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6bba2-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="6bba2-253">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="6bba2-253">Find certificate</span></span>
  * <span data-ttu-id="6bba2-254">Zoeken naar de CA die hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="6bba2-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="6bba2-255">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="6bba2-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6bba2-256">Exporteer het certificaat in een. CER met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="6bba2-257">**Nee, de persoonlijke sleutel niet exporteren**</span><span class="sxs-lookup"><span data-stu-id="6bba2-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="6bba2-258">Indien mogelijk exporteren met alle certificaten in het certificeringspad.</span><span class="sxs-lookup"><span data-stu-id="6bba2-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="6bba2-259">Alle uitgebreide eigenschappen exporteren.</span><span class="sxs-lookup"><span data-stu-id="6bba2-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="6bba2-260">CA-certificaat uploaden naar cloudservice</span><span class="sxs-lookup"><span data-stu-id="6bba2-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="6bba2-261">Uploaden van het certificaat met de bestaande of gegenereerd. CER-bestand met de openbare sleutel van de CA.</span><span class="sxs-lookup"><span data-stu-id="6bba2-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="6bba2-262">Update-CA-certificaat in het configuratiebestand van de service</span><span class="sxs-lookup"><span data-stu-id="6bba2-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="6bba2-263">Werk de vingerafdrukwaarde van de volgende instelling in het configuratiebestand van de service met de vingerafdruk van het certificaat dat is geüpload naar de cloudservice:</span><span class="sxs-lookup"><span data-stu-id="6bba2-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="6bba2-264">Werk de waarde van de volgende instelling met dezelfde vingerafdruk:</span><span class="sxs-lookup"><span data-stu-id="6bba2-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="6bba2-265">Clientcertificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="6bba2-265">Issue client certificates</span></span>
<span data-ttu-id="6bba2-266">Elke gebruiker die toegang hebben tot de service moet een certificaat uitgegeven voor his/hers exclusieve gebruik hebben en his/hers eigenaar sterk wachtwoord op ter beveiliging van de persoonlijke sleutel moet kiezen.</span><span class="sxs-lookup"><span data-stu-id="6bba2-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="6bba2-267">De volgende stappen moeten worden uitgevoerd in dezelfde machine waar het zelfondertekende certificaat van de CA is gegenereerd en worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="6bba2-268">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-268">Customizing:</span></span>

* <span data-ttu-id="6bba2-269">-n met een ID voor het naar de client die met dit certificaat wordt geverifieerd</span><span class="sxs-lookup"><span data-stu-id="6bba2-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="6bba2-270">e - met de vervaldatum van certificaat</span><span class="sxs-lookup"><span data-stu-id="6bba2-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="6bba2-271">MyID.pvk en MyID.cer met unieke bestandsnamen voor dit clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="6bba2-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="6bba2-272">Met deze opdracht wordt gevraagd om een wachtwoord worden gemaakt en vervolgens één keer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bba2-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="6bba2-273">Gebruik een sterk wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="6bba2-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="6bba2-274">PFX-bestanden voor client-certificaten maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="6bba2-275">Voor elk certificaat gegenereerde client uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6bba2-276">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="6bba2-277">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6bba2-278">Ja, de persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-278">Yes, export the private key</span></span>
* <span data-ttu-id="6bba2-279">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-279">Export all extended properties</span></span>
* <span data-ttu-id="6bba2-280">De persoon aan wie dit certificaat wordt uitgegeven moet de export-wachtwoord kiezen</span><span class="sxs-lookup"><span data-stu-id="6bba2-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="6bba2-281">Client-certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-281">Import client certificate</span></span>
<span data-ttu-id="6bba2-282">Elke gebruiker voor wie een clientcertificaat is uitgegeven, moet het sleutelpaar in de machines die hij wordt gebruikt voor communicatie met de service importeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="6bba2-283">Dubbelklik op de. PFX-bestand in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="6bba2-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="6bba2-284">Importeren in het persoonlijk certificaatarchief met ten minste deze optie:</span><span class="sxs-lookup"><span data-stu-id="6bba2-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="6bba2-285">Alle uitgebreide eigenschappen ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="6bba2-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="6bba2-286">Certificaatvingerafdrukken client kopiëren</span><span class="sxs-lookup"><span data-stu-id="6bba2-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="6bba2-287">Elke gebruiker voor wie een clientcertificaat is uitgegeven, moet deze stappen volgen om te kunnen verkrijgen van de vingerafdruk van his/hers certificaat dat wordt toegevoegd aan het configuratiebestand van de service:</span><span class="sxs-lookup"><span data-stu-id="6bba2-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="6bba2-288">Certmgr.exe uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-288">Run certmgr.exe</span></span>
* <span data-ttu-id="6bba2-289">Selecteer het tabblad Persoonlijk</span><span class="sxs-lookup"><span data-stu-id="6bba2-289">Select the Personal tab</span></span>
* <span data-ttu-id="6bba2-290">Dubbelklik op het certificaat moet worden gebruikt voor verificatie</span><span class="sxs-lookup"><span data-stu-id="6bba2-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="6bba2-291">Selecteer het tabblad met Details in het dialoogvenster certificaat dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6bba2-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="6bba2-292">Controleer of dat weergeven alle wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="6bba2-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="6bba2-293">Selecteer het veld met de vingerafdruk van de naam in de lijst</span><span class="sxs-lookup"><span data-stu-id="6bba2-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="6bba2-294">Kopieer de waarde van de vingerafdruk van het ** verwijderen van niet-zichtbare Unicode-tekens voor het eerste cijfer ** verwijdert alle spaties</span><span class="sxs-lookup"><span data-stu-id="6bba2-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="6bba2-295">Toegestane clients in het configuratiebestand van de service configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="6bba2-296">Werk de waarde van de volgende instelling in het configuratiebestand van de service met een door komma's gescheiden lijst met de vingerafdrukken van de clientcertificaten die toegang hebben tot de service:</span><span class="sxs-lookup"><span data-stu-id="6bba2-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="6bba2-297">Controle van certificaatintrekking client configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="6bba2-298">De standaardinstelling wordt niet gecontroleerd met de certificeringsinstantie voor de clientstatus certificaat intrekken.</span><span class="sxs-lookup"><span data-stu-id="6bba2-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="6bba2-299">U schakelt de controles als de certificeringsinstantie die certificaten hebben verleend de client deze controles ondersteunt door de volgende instelling te wijzigen met een van de waarden die zijn gedefinieerd in de opsomming X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="6bba2-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="6bba2-300">PFX-bestand voor zelfondertekende versleutelingscertificaten maken</span><span class="sxs-lookup"><span data-stu-id="6bba2-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="6bba2-301">Voor een versleutelingscertificaat uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6bba2-302">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="6bba2-303">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6bba2-304">Ja, de persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-304">Yes, export the private key</span></span>
* <span data-ttu-id="6bba2-305">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-305">Export all extended properties</span></span>
* <span data-ttu-id="6bba2-306">U moet het wachtwoord tijdens het uploaden van het certificaat naar de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="6bba2-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="6bba2-307">Versleutelingscertificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="6bba2-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="6bba2-308">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="6bba2-308">Find certificate</span></span>
* <span data-ttu-id="6bba2-309">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="6bba2-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6bba2-310">Exporteer het certificaat in een. PFX-bestand met deze opties:</span><span class="sxs-lookup"><span data-stu-id="6bba2-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="6bba2-311">Ja, de persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-311">Yes, export the private key</span></span>
  * <span data-ttu-id="6bba2-312">Indien mogelijk exporteren met alle certificaten in het certificeringspad</span><span class="sxs-lookup"><span data-stu-id="6bba2-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="6bba2-313">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="6bba2-314">Versleutelingscertificaat uploaden naar cloudservice</span><span class="sxs-lookup"><span data-stu-id="6bba2-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="6bba2-315">Uploaden van het certificaat met de bestaande of gegenereerd. PFX-bestand met het sleutelpaar van versleuteling:</span><span class="sxs-lookup"><span data-stu-id="6bba2-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="6bba2-316">Voer het wachtwoord voor het beveiligen van gegevens van de persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="6bba2-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="6bba2-317">Versleutelingscertificaat in het configuratiebestand van de service bijwerken</span><span class="sxs-lookup"><span data-stu-id="6bba2-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="6bba2-318">Werk de vingerafdrukwaarde van de volgende instellingen in het configuratiebestand van de service met de vingerafdruk van het certificaat dat is geüpload naar de cloudservice:</span><span class="sxs-lookup"><span data-stu-id="6bba2-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="6bba2-319">Algemene bewerkingen van het certificaat</span><span class="sxs-lookup"><span data-stu-id="6bba2-319">Common certificate operations</span></span>
* <span data-ttu-id="6bba2-320">De SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="6bba2-321">Clientcertificaten configureren</span><span class="sxs-lookup"><span data-stu-id="6bba2-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="6bba2-322">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="6bba2-322">Find certificate</span></span>
<span data-ttu-id="6bba2-323">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="6bba2-323">Follow these steps:</span></span>

1. <span data-ttu-id="6bba2-324">Mmc.exe worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bba2-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="6bba2-325">File -> module toevoegen/verwijderen...</span><span class="sxs-lookup"><span data-stu-id="6bba2-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="6bba2-326">Selecteer **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="6bba2-327">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-327">Click **Add**.</span></span>
5. <span data-ttu-id="6bba2-328">Kies de locatie van certificaat store.</span><span class="sxs-lookup"><span data-stu-id="6bba2-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="6bba2-329">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-329">Click **Finish**.</span></span>
7. <span data-ttu-id="6bba2-330">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-330">Click **OK**.</span></span>
8. <span data-ttu-id="6bba2-331">Vouw **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="6bba2-332">Vouw het knooppunt van de store certificaat.</span><span class="sxs-lookup"><span data-stu-id="6bba2-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="6bba2-333">Vouw het knooppunt van de onderliggende certificaat.</span><span class="sxs-lookup"><span data-stu-id="6bba2-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="6bba2-334">Selecteer een certificaat in de lijst.</span><span class="sxs-lookup"><span data-stu-id="6bba2-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="6bba2-335">Certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="6bba2-335">Export certificate</span></span>
<span data-ttu-id="6bba2-336">In de **Export Wizard certificaat**:</span><span class="sxs-lookup"><span data-stu-id="6bba2-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="6bba2-337">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-337">Click **Next**.</span></span>
2. <span data-ttu-id="6bba2-338">Selecteer **Ja**, klikt u vervolgens **de persoonlijke sleutel exporteren**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="6bba2-339">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-339">Click **Next**.</span></span>
4. <span data-ttu-id="6bba2-340">Selecteer de gewenste uitvoer-bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="6bba2-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="6bba2-341">Controleer de gewenste opties.</span><span class="sxs-lookup"><span data-stu-id="6bba2-341">Check the desired options.</span></span>
6. <span data-ttu-id="6bba2-342">Controleer **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-342">Check **Password**.</span></span>
7. <span data-ttu-id="6bba2-343">Voer een sterk wachtwoord in en Bevestig het.</span><span class="sxs-lookup"><span data-stu-id="6bba2-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="6bba2-344">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-344">Click **Next**.</span></span>
9. <span data-ttu-id="6bba2-345">Typ of blader een bestandsnaam waar het certificaat wordt opgeslagen (gebruik een. PFX-extensie).</span><span class="sxs-lookup"><span data-stu-id="6bba2-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="6bba2-346">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-346">Click **Next**.</span></span>
11. <span data-ttu-id="6bba2-347">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-347">Click **Finish**.</span></span>
12. <span data-ttu-id="6bba2-348">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="6bba2-349">Certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-349">Import certificate</span></span>
<span data-ttu-id="6bba2-350">In de Wizard Certificaat importeren:</span><span class="sxs-lookup"><span data-stu-id="6bba2-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="6bba2-351">Selecteer de locatie van de store.</span><span class="sxs-lookup"><span data-stu-id="6bba2-351">Select the store location.</span></span>
   
   * <span data-ttu-id="6bba2-352">Selecteer **huidige gebruiker** als alleen de processen die worden uitgevoerd onder de huidige gebruiker heeft toegang tot de service</span><span class="sxs-lookup"><span data-stu-id="6bba2-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="6bba2-353">Selecteer **lokale Machine** als andere processen in deze computer toegang de service tot heeft</span><span class="sxs-lookup"><span data-stu-id="6bba2-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="6bba2-354">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-354">Click **Next**.</span></span>
3. <span data-ttu-id="6bba2-355">Als uit een bestand importeren, controleert u het bestandspad.</span><span class="sxs-lookup"><span data-stu-id="6bba2-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="6bba2-356">Als u deze importeert een. PFX-bestand:</span><span class="sxs-lookup"><span data-stu-id="6bba2-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="6bba2-357">Voer het wachtwoord voor het beveiligen van de persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="6bba2-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="6bba2-358">Selecteer opties voor importeren</span><span class="sxs-lookup"><span data-stu-id="6bba2-358">Select import options</span></span>
5. <span data-ttu-id="6bba2-359">Selecteer "Locatie" certificaten in het onderstaande archief opslaan</span><span class="sxs-lookup"><span data-stu-id="6bba2-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="6bba2-360">Klik op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-360">Click **Browse**.</span></span>
7. <span data-ttu-id="6bba2-361">Selecteer de gewenste winkel.</span><span class="sxs-lookup"><span data-stu-id="6bba2-361">Select the desired store.</span></span>
8. <span data-ttu-id="6bba2-362">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="6bba2-363">Als het archief Vertrouwde basiscertificeringsinstanties hebt gekozen, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="6bba2-364">Klik op **OK** op alle vensters van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6bba2-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="6bba2-365">Certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="6bba2-365">Upload certificate</span></span>
<span data-ttu-id="6bba2-366">In de [Azure-Portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6bba2-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="6bba2-367">Selecteer **Cloudservices**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="6bba2-368">Selecteer de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="6bba2-368">Select the cloud service.</span></span>
3. <span data-ttu-id="6bba2-369">Klik op het bovenste menu **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="6bba2-370">Klik op de balk onderaan **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="6bba2-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="6bba2-371">Selecteer het certificaatbestand.</span><span class="sxs-lookup"><span data-stu-id="6bba2-371">Select the certificate file.</span></span>
6. <span data-ttu-id="6bba2-372">Als het is een. PFX-bestand, typ het wachtwoord voor de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="6bba2-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="6bba2-373">Als voltooid, kopieert u de vingerafdruk van het certificaat van de nieuwe vermelding in de lijst.</span><span class="sxs-lookup"><span data-stu-id="6bba2-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="6bba2-374">Andere beveiligingsoverwegingen</span><span class="sxs-lookup"><span data-stu-id="6bba2-374">Other security considerations</span></span>
<span data-ttu-id="6bba2-375">De SSL-instellingen in dit document beschreven versleutelen van communicatie tussen de service en de clients wanneer het HTTPS-eindpunt wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bba2-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="6bba2-376">Dit is belangrijk omdat de referenties voor toegang tot de database en mogelijk andere vertrouwelijke informatie zijn opgenomen in de communicatie.</span><span class="sxs-lookup"><span data-stu-id="6bba2-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="6bba2-377">Let echter op dat de service zich blijft interne status voordoen, inclusief referenties, in de interne tabellen in de Microsoft Azure SQL-database die u hebt opgegeven voor de metagegevensopslag van in uw Microsoft Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6bba2-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="6bba2-378">Deze database is gedefinieerd als onderdeel van de volgende instelling in uw serviceconfiguratiebestand (. CSCFG-bestand):</span><span class="sxs-lookup"><span data-stu-id="6bba2-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="6bba2-379">In deze database opgeslagen referenties zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6bba2-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="6bba2-380">Echter, als een best practice, zorg ervoor dat web- en werkrollen rollen van uw service-implementaties actueel worden gehouden en veilig zijn als ze beide toegang tot de database met metagegevens en het certificaat dat wordt gebruikt voor versleuteling en ontsleuteling van opgeslagen referenties hebben.</span><span class="sxs-lookup"><span data-stu-id="6bba2-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

