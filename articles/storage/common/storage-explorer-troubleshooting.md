---
title: Azure Storage Explorer probleemoplossingsgids | Microsoft Docs
description: Overzicht van de twee foutopsporingsfunctie van Azure
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 470b2d87ffdc4769bb2963df7dea646901469e00
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="cbb77-103">Azure Storage Explorer probleemoplossingsgids</span><span class="sxs-lookup"><span data-stu-id="cbb77-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="cbb77-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="cbb77-104">Introduction</span></span>

<span data-ttu-id="cbb77-105">Microsoft Azure Opslagverkenner (Preview) is een zelfstandige app waardoor u eenvoudig werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="cbb77-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="cbb77-106">De app kan verbinding maken toStorage accounts die worden gehost op Azure, soevereine Clouds en Azure-Stack.</span><span class="sxs-lookup"><span data-stu-id="cbb77-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="cbb77-107">Deze handleiding bevat een overzicht van oplossingen voor algemene problemen gezien in Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="cbb77-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="cbb77-108">Problemen met aanmelden</span><span class="sxs-lookup"><span data-stu-id="cbb77-108">Sign in issues</span></span>

<span data-ttu-id="cbb77-109">Voordat u doorgaat, probeer uw toepassing opnieuw te starten en zien of de problemen te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="cbb77-109">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="cbb77-110">Fout: Zelf-ondertekend certificaat in de certificaatketen</span><span class="sxs-lookup"><span data-stu-id="cbb77-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="cbb77-111">Er zijn diverse redenen waarom u deze fout kan optreden, en de twee meest voorkomende redenen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="cbb77-111">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="cbb77-112">De app is verbonden via een transparante proxy-, wat betekent dat een server (zoals de bedrijfsserver van uw) onderscheppen HTTPS-verkeer, ontsleutelen van deze en vervolgens versleutelen met behulp van een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="cbb77-112">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="cbb77-113">U kunt een toepassing, zoals antivirussoftware, die is injecteren van een zelfondertekend SSL-certificaat in de HTTPS-berichten die u ontvangt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbb77-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="cbb77-114">Wanneer Opslagverkenner een van de problemen tegenkomt, kan het niet meer te weten of het ontvangen bericht voor HTTPS is geknoeid.</span><span class="sxs-lookup"><span data-stu-id="cbb77-114">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="cbb77-115">Als u een kopie van het zelfondertekend certificaat hebt, kunt u Opslagverkenner vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="cbb77-115">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="cbb77-116">Als u die het certificaat is injecteren weet, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="cbb77-116">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="cbb77-117">Open SSL installeren</span><span class="sxs-lookup"><span data-stu-id="cbb77-117">Install Open SSL</span></span>

    - <span data-ttu-id="cbb77-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (een van de lichte versies moet voldoende)</span><span class="sxs-lookup"><span data-stu-id="cbb77-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="cbb77-119">Mac- en Linux: moet worden opgenomen met het besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="cbb77-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="cbb77-120">Open SSL uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cbb77-120">Run Open SSL</span></span>

    - <span data-ttu-id="cbb77-121">Windows: open de map wilt installeren, klik op **/bin/**, en dubbelklik vervolgens op **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="cbb77-121">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="cbb77-122">Mac- en Linux: Voer **openssl** van een definitieve.</span><span class="sxs-lookup"><span data-stu-id="cbb77-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="cbb77-123">Uitvoeren van s_client - showcerts-microsoft.com:443 verbinding</span><span class="sxs-lookup"><span data-stu-id="cbb77-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="cbb77-124">Zoek naar de zelfondertekende certificaten.</span><span class="sxs-lookup"><span data-stu-id="cbb77-124">Look for self-signed certificates.</span></span> <span data-ttu-id="cbb77-125">Als u niet zeker dat zelf ondertekend weet, zoek naar elke locatie het onderwerp ('s:') en de verlener ('i') zijn hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="cbb77-125">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="cbb77-126">Wanneer u zelfondertekende certificaten hebt gevonden, voor elk adres kopieert en plakt u alles uit en inclusief **---BEGIN CERTIFICATE---** naar **---EINDCERTIFICAAT---** naar een nieuw .cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="cbb77-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="cbb77-127">Open Opslagverkenner, klik op **bewerken** > **SSL-certificaten** > **certificaten importeren**, en gebruik vervolgens de bestandskiezer om te zoeken, selecteert, en Open het cer-bestanden die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cbb77-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="cbb77-128">Als u geen zelfondertekende certificaten met behulp van de bovenstaande stappen niet kunt vinden, contact met ons opnemen via het hulpprogramma feedback voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cbb77-128">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="cbb77-129">Kan geen abonnementen ophalen</span><span class="sxs-lookup"><span data-stu-id="cbb77-129">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="cbb77-130">Als u niet ophalen van uw abonnementen, nadat u zich hebt aangemeld, volg deze stappen om dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="cbb77-130">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="cbb77-131">Controleer of dat uw account toegang tot de abonnementen heeft wanneer u zich aanmeldt bij de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cbb77-131">Verify that your account has access to the subscriptions by signing into the Azure Portal.</span></span>

- <span data-ttu-id="cbb77-132">Zorg ervoor dat u bent aangemeld met behulp van de juiste omgeving (Azure, Azure China, Duitse Azure, Azure US Government of aangepaste omgeving/Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="cbb77-132">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="cbb77-133">Als u zich achter een proxy, zorg er dan voor dat u de proxy Opslagverkenner juist hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cbb77-133">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="cbb77-134">Verwijder en readding van het account.</span><span class="sxs-lookup"><span data-stu-id="cbb77-134">Try removing and readding the account.</span></span>

- <span data-ttu-id="cbb77-135">Probeer een van de volgende bestanden worden verwijderd uit de hoofddirectory (dat wil zeggen, C:\Users\ContosoUser) en vervolgens opnieuw toe te voegen het account:</span><span class="sxs-lookup"><span data-stu-id="cbb77-135">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="cbb77-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="cbb77-136">.adalcache</span></span>

    - <span data-ttu-id="cbb77-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="cbb77-137">.devaccounts</span></span>

    - <span data-ttu-id="cbb77-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="cbb77-138">.extaccounts</span></span>

- <span data-ttu-id="cbb77-139">Bekijk de ontwikkelhulpprogramma's console (door op F12 wordt gedrukt) wanneer u voor eventuele foutberichten aanmeldt zich:</span><span class="sxs-lookup"><span data-stu-id="cbb77-139">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Hulpprogramma's voor ontwikkelaars](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="cbb77-141">Kan niet voor een overzicht van de verificatiepagina</span><span class="sxs-lookup"><span data-stu-id="cbb77-141">Unable to see the authentication page</span></span>

<span data-ttu-id="cbb77-142">Als u niet wilt weergeven van de verificatiepagina als volgt te werk om dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="cbb77-142">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="cbb77-143">Afhankelijk van de snelheid van uw verbinding duurt lang voordat de aanmeldingspagina te laden, wacht u minstens één minuut voordat u sluit het verificatiedialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cbb77-143">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="cbb77-144">Als u zich achter een proxy, zorg er dan voor dat u de proxy Opslagverkenner juist hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cbb77-144">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="cbb77-145">De developer-console weergeven door op de F12-toets te drukken.</span><span class="sxs-lookup"><span data-stu-id="cbb77-145">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="cbb77-146">Bekijk de antwoorden van de developer-console en ontdek of voor u een aanwijzing Waarom vindt verificatie werkt niet.</span><span class="sxs-lookup"><span data-stu-id="cbb77-146">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="cbb77-147">Kan account niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="cbb77-147">Cannot remove account</span></span>

<span data-ttu-id="cbb77-148">Als u niet om een account te verwijderen, of als de koppeling opnieuw verifiëren heeft geen invloed, volg deze stappen om dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="cbb77-148">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="cbb77-149">Probeer de volgende bestanden worden verwijderd uit de hoofddirectory en vervolgens readding het account:</span><span class="sxs-lookup"><span data-stu-id="cbb77-149">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="cbb77-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="cbb77-150">.adalcache</span></span>

    - <span data-ttu-id="cbb77-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="cbb77-151">.devaccounts</span></span>

    - <span data-ttu-id="cbb77-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="cbb77-152">.extaccounts</span></span>

- <span data-ttu-id="cbb77-153">Als u wilt verwijderen SAS opslagbronnen aangesloten, verwijdert u de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="cbb77-153">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="cbb77-154">De map %AppData%/StorageExplorer voor Windows</span><span class="sxs-lookup"><span data-stu-id="cbb77-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="cbb77-155">/Gebruikers/ < Uw_naam >/Library/Applicaiton ondersteuning/StorageExplorer voor Mac</span><span class="sxs-lookup"><span data-stu-id="cbb77-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="cbb77-156">~/.config/StorageExplorer voor Linux</span><span class="sxs-lookup"><span data-stu-id="cbb77-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="cbb77-157">U moet alle uw referenties opnieuw invoeren als u deze bestanden verwijdert.</span><span class="sxs-lookup"><span data-stu-id="cbb77-157">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="cbb77-158">Proxy-problemen</span><span class="sxs-lookup"><span data-stu-id="cbb77-158">Proxy issues</span></span>

<span data-ttu-id="cbb77-159">Controleer eerst of dat de volgende informatie die u hebt ingevoerd juist zijn:</span><span class="sxs-lookup"><span data-stu-id="cbb77-159">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="cbb77-160">De proxy-URL en het poortnummer</span><span class="sxs-lookup"><span data-stu-id="cbb77-160">The proxy URL and port number</span></span>

- <span data-ttu-id="cbb77-161">Gebruikersnaam en wachtwoord, indien vereist door de proxy</span><span class="sxs-lookup"><span data-stu-id="cbb77-161">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="cbb77-162">Algemene oplossingen</span><span class="sxs-lookup"><span data-stu-id="cbb77-162">Common solutions</span></span>

<span data-ttu-id="cbb77-163">Als u steeds problemen ondervindt nog, volg deze stappen voor het oplossen van deze:</span><span class="sxs-lookup"><span data-stu-id="cbb77-163">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="cbb77-164">Als u verbinding met Internet maken kunt zonder gebruik van uw proxyserver, moet u controleren of Opslagverkenner zonder proxyinstellingen zijn ingeschakeld werkt.</span><span class="sxs-lookup"><span data-stu-id="cbb77-164">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="cbb77-165">Als dit het geval is, is er mogelijk een probleem met uw proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="cbb77-165">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="cbb77-166">Werken met de proxy-beheerder om de problemen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="cbb77-166">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="cbb77-167">Controleer of andere toepassingen die gebruikmaken van de proxyserver werken zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="cbb77-167">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="cbb77-168">Controleer of u verbinding kunt maken voor de Microsoft Azure-portal met behulp van uw webbrowser</span><span class="sxs-lookup"><span data-stu-id="cbb77-168">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="cbb77-169">Controleer of u kunt reacties van uw service-eindpunten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="cbb77-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="cbb77-170">Voer een van de eindpunt-URL's in uw browser.</span><span class="sxs-lookup"><span data-stu-id="cbb77-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="cbb77-171">Als u verbinding maken kunt, ontvangt u een InvalidQueryParameterValue of een vergelijkbare XML-antwoord.</span><span class="sxs-lookup"><span data-stu-id="cbb77-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="cbb77-172">Als iemand anders Opslagverkenner ook met de proxyserver gebruikt, controleert u of dat ze verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="cbb77-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="cbb77-173">Als ze verbinding maken kunnen, hebt u mogelijk contact op met uw proxy-server.</span><span class="sxs-lookup"><span data-stu-id="cbb77-173">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="cbb77-174">Hulpprogramma's voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="cbb77-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="cbb77-175">Als u hulpprogramma's voor netwerken, zoals Fiddler voor Windows hebt, kunt u mogelijk problemen als volgt:</span><span class="sxs-lookup"><span data-stu-id="cbb77-175">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="cbb77-176">Als u om te werken via de proxy hebt, moet u wellicht uw netwerken hulpprogramma om verbinding via de proxy te configureren.</span><span class="sxs-lookup"><span data-stu-id="cbb77-176">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="cbb77-177">Controleer het poortnummer dat wordt gebruikt door uw netwerken hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="cbb77-177">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="cbb77-178">Voer de URL van de lokale host en het poortnummer van de netwerken hulpprogramma als proxy-instellingen in Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="cbb77-178">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="cbb77-179">Als deze isdone correct uw netwerken hulpprogramma start logging netwerkaanvragen door Opslagverkenner voor beheer en service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="cbb77-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="cbb77-180">Voer bijvoorbeeld https://cawablobgrs.blob.core.windows.net/ voor het eindpunt van de blob in een browser en ontvangt u een antwoord lijkt op het volgende voorbeeld, waarin wordt voorgesteld de bron bestaat, hoewel u geen toegang toe heeft.</span><span class="sxs-lookup"><span data-stu-id="cbb77-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![Voorbeeld van code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="cbb77-182">Neem contact op met de serverbeheerder proxy</span><span class="sxs-lookup"><span data-stu-id="cbb77-182">Contact proxy server admin</span></span>

<span data-ttu-id="cbb77-183">Als uw proxy-instellingen correct zijn, hebt u mogelijk contact opnemen met uw beheerder proxy-server en</span><span class="sxs-lookup"><span data-stu-id="cbb77-183">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="cbb77-184">Zorg ervoor dat uw proxy geen verkeer naar Azure management of de resource-eindpunten blokkeert.</span><span class="sxs-lookup"><span data-stu-id="cbb77-184">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="cbb77-185">Controleer of het verificatieprotocol dat wordt gebruikt door de proxyserver.</span><span class="sxs-lookup"><span data-stu-id="cbb77-185">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="cbb77-186">Opslagverkenner biedt momenteel geen ondersteuning voor NTLM-proxy's.</span><span class="sxs-lookup"><span data-stu-id="cbb77-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="cbb77-187">Foutbericht 'Kan niet naar onderliggende elementen ophalen'</span><span class="sxs-lookup"><span data-stu-id="cbb77-187">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="cbb77-188">Als u met Azure via een proxy verbonden bent, moet u controleren of de proxyinstellingen juist zijn.</span><span class="sxs-lookup"><span data-stu-id="cbb77-188">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="cbb77-189">Als u zijn toegang tot een resource verleend aan de eigenaar van het abonnement of account, Controleer of u hebt gelezen of lijst met machtigingen voor die bron.</span><span class="sxs-lookup"><span data-stu-id="cbb77-189">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="cbb77-190">Problemen met SAS-URL</span><span class="sxs-lookup"><span data-stu-id="cbb77-190">Issues with SAS URL</span></span>
<span data-ttu-id="cbb77-191">Als u verbinding met een service met behulp van een SAS-URL en deze fout optreedt maakt:</span><span class="sxs-lookup"><span data-stu-id="cbb77-191">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="cbb77-192">Controleer of dat de URL van de vereiste machtigingen voor lezen of lijst van bronnen biedt.</span><span class="sxs-lookup"><span data-stu-id="cbb77-192">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="cbb77-193">Controleer of de URL is niet verlopen.</span><span class="sxs-lookup"><span data-stu-id="cbb77-193">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="cbb77-194">Als de SAS-URL is gebaseerd op een toegangsbeleid, controleert u of het beleid voor toegang niet is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="cbb77-194">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb77-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cbb77-195">Next steps</span></span>

<span data-ttu-id="cbb77-196">Als geen van de oplossingen die voor u werken, Geef uw probleem via het hulpprogramma feedback met uw e-mailadres en zo veel meer informatie over het probleem dat is opgenomen als u kunnen, zodat we kunnen contact met u voor het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="cbb77-196">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="cbb77-197">Om dit te doen, klikt u op **Help** menu en klik vervolgens op **Feedback verzenden**.</span><span class="sxs-lookup"><span data-stu-id="cbb77-197">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Feedback](./media/storage-explorer-troubleshooting/4022503_en_1.png)
