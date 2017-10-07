---
title: aaaAzure Opslagverkenner probleemoplossingsgids | Microsoft Docs
description: Overzicht van Hallo twee foutopsporingsfunctie van Azure
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
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="7a028-103">Azure Storage Explorer probleemoplossingsgids</span><span class="sxs-lookup"><span data-stu-id="7a028-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="7a028-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="7a028-104">Introduction</span></span>

<span data-ttu-id="7a028-105">Microsoft Azure Opslagverkenner (Preview) is een zelfstandige app waardoor u tooeasily werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="7a028-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="7a028-106">Hallo-app kunt verbinden toStorage accounts die worden gehost op Azure, soevereine Clouds en Azure-Stack.</span><span class="sxs-lookup"><span data-stu-id="7a028-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="7a028-107">Deze handleiding bevat een overzicht van oplossingen voor algemene problemen gezien in Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="7a028-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="7a028-108">Problemen met aanmelden</span><span class="sxs-lookup"><span data-stu-id="7a028-108">Sign in issues</span></span>

<span data-ttu-id="7a028-109">Voordat u doorgaat, probeer uw toepassing opnieuw te starten en Zie of Hallo problemen kunnen worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="7a028-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="7a028-110">Fout: Zelf-ondertekend certificaat in de certificaatketen</span><span class="sxs-lookup"><span data-stu-id="7a028-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="7a028-111">Er zijn diverse redenen waarom u deze fout kan optreden en de meest voorkomende twee redenen Hallo zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a028-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="7a028-112">Hallo-app is verbonden via een transparante proxy-, wat betekent dat een server (zoals de bedrijfsserver van uw) onderscheppen HTTPS-verkeer, ontsleutelen van deze en vervolgens versleutelen met behulp van een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="7a028-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="7a028-113">U kunt een toepassing, zoals antivirussoftware, die is injecteren van een zelfondertekend SSL-certificaat in Hallo HTTPS-berichten die u ontvangt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a028-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="7a028-114">Wanneer Opslagverkenner Hallo problemen tegenkomt, kan het niet meer te weten of Hallo ontvangen HTTPS-bericht is geknoeid.</span><span class="sxs-lookup"><span data-stu-id="7a028-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="7a028-115">Als u een kopie van Hallo zelf-ondertekend certificaat hebt, kunt u Opslagverkenner vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="7a028-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="7a028-116">Als u die is injecteren Hallo certificaat weet, volgt u deze stappen toofind het:</span><span class="sxs-lookup"><span data-stu-id="7a028-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="7a028-117">Open SSL installeren</span><span class="sxs-lookup"><span data-stu-id="7a028-117">Install Open SSL</span></span>

    - <span data-ttu-id="7a028-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (Hallo lichte versies moet voldoende)</span><span class="sxs-lookup"><span data-stu-id="7a028-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="7a028-119">Mac- en Linux: moet worden opgenomen met het besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="7a028-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="7a028-120">Open SSL uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7a028-120">Run Open SSL</span></span>

    - <span data-ttu-id="7a028-121">Windows: Hallo-installatiemap openen, klikt u op **/bin/**, en dubbelklik vervolgens op **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="7a028-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="7a028-122">Mac- en Linux: Voer **openssl** van een definitieve.</span><span class="sxs-lookup"><span data-stu-id="7a028-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="7a028-123">Uitvoeren van s_client - showcerts-microsoft.com:443 verbinding</span><span class="sxs-lookup"><span data-stu-id="7a028-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="7a028-124">Zoek naar de zelfondertekende certificaten.</span><span class="sxs-lookup"><span data-stu-id="7a028-124">Look for self-signed certificates.</span></span> <span data-ttu-id="7a028-125">Als u welke zijn zelf-ondertekend weet, zoek overal Hallo onderwerp ('s:') en verlener ('i') zijn dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a028-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="7a028-126">Wanneer u zelfondertekende certificaten hebt gevonden, voor elk adres kopieert en plakt u alles uit en inclusief **---BEGIN CERTIFICATE---** te**---EINDCERTIFICAAT---** tooa nieuwe cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a028-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="7a028-127">Open Opslagverkenner, klik op **bewerken** > **SSL-certificaten** > **certificaten importeren**, en vervolgens gebruik Hallo bestand objectkiezer toofind, selecteert, en open Hallo cer-bestanden die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a028-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="7a028-128">Als u geen zelfondertekende certificaten met behulp van Hallo bovenstaande stappen niet kunt vinden, contact met ons opnemen via Hallo feedbackprogramma voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7a028-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="7a028-129">Kan geen tooretrieve abonnementen</span><span class="sxs-lookup"><span data-stu-id="7a028-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="7a028-130">Als u tooretrieve uw abonnementen na het aanmelden, volg deze stappen tootroubleshoot dit probleem:</span><span class="sxs-lookup"><span data-stu-id="7a028-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="7a028-131">Controleer of uw account toegang toohello abonnementen door aanmeldt bij hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7a028-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="7a028-132">Zorg ervoor dat u bent aangemeld met behulp van de juiste omgeving hello (Azure, Azure China, Duitse Azure, Azure US Government of aangepaste omgeving/Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="7a028-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="7a028-133">Als u zich achter een proxy, zorg er dan voor dat Hallo Opslagverkenner proxy correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7a028-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="7a028-134">Verwijder en readding Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="7a028-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="7a028-135">Verwijder Hallo volgende bestanden uit de hoofddirectory (dat wil zeggen, C:\Users\ContosoUser) en vervolgens opnieuw toe te voegen Hallo-account:</span><span class="sxs-lookup"><span data-stu-id="7a028-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="7a028-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="7a028-136">.adalcache</span></span>

    - <span data-ttu-id="7a028-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="7a028-137">.devaccounts</span></span>

    - <span data-ttu-id="7a028-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="7a028-138">.extaccounts</span></span>

- <span data-ttu-id="7a028-139">Console voor controle Hallo developer's (door op F12 te drukken) wanneer u zich aanmeldt voor eventuele foutberichten:</span><span class="sxs-lookup"><span data-stu-id="7a028-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Hulpprogramma's voor ontwikkelaars](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="7a028-141">Kan geen toosee Hallo verificatiepagina</span><span class="sxs-lookup"><span data-stu-id="7a028-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="7a028-142">Als u pagina kan niet toosee Hallo-verificatie, volg deze stappen tootroubleshoot dit probleem:</span><span class="sxs-lookup"><span data-stu-id="7a028-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="7a028-143">Afhankelijk van Hallo snelheid van uw verbinding, kan het Hallo-aanmeldingspagina tooload even duren voordat, wacht ten minste één minuut voordat het dialoogvenster verificatie hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="7a028-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="7a028-144">Als u zich achter een proxy, zorg er dan voor dat Hallo Opslagverkenner proxy correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7a028-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="7a028-145">Weergave Hallo developer-console door Hallo F12-toets te drukken.</span><span class="sxs-lookup"><span data-stu-id="7a028-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="7a028-146">Hallo-antwoorden van Hallo developer-console te bekijken en zien of voor u een aanwijzing Waarom vindt verificatie werkt niet.</span><span class="sxs-lookup"><span data-stu-id="7a028-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="7a028-147">Kan account niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="7a028-147">Cannot remove account</span></span>

<span data-ttu-id="7a028-148">Volg deze stappen tootroubleshoot dit probleem als u tooremove een account of Hallo opnieuw verifiëren koppeling heeft geen invloed:</span><span class="sxs-lookup"><span data-stu-id="7a028-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="7a028-149">Verwijder Hallo volgende bestanden uit de hoofddirectory en vervolgens readding Hallo-account:</span><span class="sxs-lookup"><span data-stu-id="7a028-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="7a028-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="7a028-150">.adalcache</span></span>

    - <span data-ttu-id="7a028-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="7a028-151">.devaccounts</span></span>

    - <span data-ttu-id="7a028-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="7a028-152">.extaccounts</span></span>

- <span data-ttu-id="7a028-153">Als u tooremove SAS Storage-resources die zijn gekoppeld wilt, verwijder Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="7a028-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="7a028-154">De map %AppData%/StorageExplorer voor Windows</span><span class="sxs-lookup"><span data-stu-id="7a028-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="7a028-155">/Gebruikers/ < Uw_naam >/Library/Applicaiton ondersteuning/StorageExplorer voor Mac</span><span class="sxs-lookup"><span data-stu-id="7a028-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="7a028-156">~/.config/StorageExplorer voor Linux</span><span class="sxs-lookup"><span data-stu-id="7a028-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="7a028-157">U hebt tooreenter alle uw referenties als u deze bestanden verwijdert.</span><span class="sxs-lookup"><span data-stu-id="7a028-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="7a028-158">Proxy-problemen</span><span class="sxs-lookup"><span data-stu-id="7a028-158">Proxy issues</span></span>

<span data-ttu-id="7a028-159">Controleer eerst of die Hallo volgende informatie die u hebt ingevoerd juist zijn:</span><span class="sxs-lookup"><span data-stu-id="7a028-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="7a028-160">proxy-URL en poort Hallo getal</span><span class="sxs-lookup"><span data-stu-id="7a028-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="7a028-161">Gebruikersnaam en wachtwoord, indien vereist door het Hallo-proxy</span><span class="sxs-lookup"><span data-stu-id="7a028-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="7a028-162">Algemene oplossingen</span><span class="sxs-lookup"><span data-stu-id="7a028-162">Common solutions</span></span>

<span data-ttu-id="7a028-163">Als u steeds problemen ondervindt nog, volgt u deze stappen tootroubleshoot ze:</span><span class="sxs-lookup"><span data-stu-id="7a028-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="7a028-164">Als u verbinding van toohello Internet maken kunt zonder gebruik van uw proxyserver, moet u controleren of Opslagverkenner zonder proxyinstellingen zijn ingeschakeld werkt.</span><span class="sxs-lookup"><span data-stu-id="7a028-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="7a028-165">Als dit Hallo geval is, is er mogelijk een probleem met uw proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7a028-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="7a028-166">Werken met uw proxy-beheerder tooidentify Hallo problemen.</span><span class="sxs-lookup"><span data-stu-id="7a028-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="7a028-167">Controleer of andere toepassingen die gebruikmaken van de proxyserver Hallo werken zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="7a028-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="7a028-168">Controleer of u kunt verbinding maken toohello Microsoft Azure-portal met behulp van uw webbrowser</span><span class="sxs-lookup"><span data-stu-id="7a028-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="7a028-169">Controleer of u kunt reacties van uw service-eindpunten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7a028-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="7a028-170">Voer een van de eindpunt-URL's in uw browser.</span><span class="sxs-lookup"><span data-stu-id="7a028-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="7a028-171">Als u verbinding maken kunt, ontvangt u een InvalidQueryParameterValue of een vergelijkbare XML-antwoord.</span><span class="sxs-lookup"><span data-stu-id="7a028-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="7a028-172">Als iemand anders Opslagverkenner ook met de proxyserver gebruikt, controleert u of dat ze verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="7a028-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="7a028-173">Als ze verbinding maken kunnen, hebt u mogelijk toocontact uw proxy-server-beheerder.</span><span class="sxs-lookup"><span data-stu-id="7a028-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="7a028-174">Hulpprogramma's voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="7a028-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="7a028-175">Als u beschikt over hulpprogramma's voor netwerken, zoals Fiddler voor Windows, hebt u mogelijk kunnen toodiagnose Hallo problemen als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a028-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="7a028-176">Als u toowork via de proxy hebt, hebben uw netwerken hulpprogramma tooconnect via proxy Hallo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7a028-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="7a028-177">Controleer Hallo poortnummer dat wordt gebruikt door uw netwerken hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7a028-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="7a028-178">Hallo lokale host-URL en de netwerken van het hulpprogramma poortnummer als proxy-instellingen in Opslagverkenner Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="7a028-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="7a028-179">Als deze isdone correct uw netwerken hulpprogramma start logging netwerkaanvragen door Opslagverkenner toomanagement en service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="7a028-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="7a028-180">Voer bijvoorbeeld https://cawablobgrs.blob.core.windows.net/ voor het eindpunt van de blob in een browser en ontvangt u een antwoord lijkt op de volgende hello, die wordt voorgesteld Hallo resource bestaat, hoewel u geen toegang toe heeft.</span><span class="sxs-lookup"><span data-stu-id="7a028-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![Voorbeeld van code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="7a028-182">Neem contact op met de serverbeheerder proxy</span><span class="sxs-lookup"><span data-stu-id="7a028-182">Contact proxy server admin</span></span>

<span data-ttu-id="7a028-183">Als de proxy-instellingen correct zijn, hebt u mogelijk toocontact uw proxy-server-beheerder en</span><span class="sxs-lookup"><span data-stu-id="7a028-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="7a028-184">Zorg ervoor dat de proxy worden niet geblokkeerd verkeer tooAzure management of resource-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="7a028-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="7a028-185">Controleer of Hallo authenticatieprotocol dat wordt gebruikt door de proxyserver.</span><span class="sxs-lookup"><span data-stu-id="7a028-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="7a028-186">Opslagverkenner biedt momenteel geen ondersteuning voor NTLM-proxy's.</span><span class="sxs-lookup"><span data-stu-id="7a028-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="7a028-187">Het foutbericht 'Kan geen tooRetrieve kinderen'</span><span class="sxs-lookup"><span data-stu-id="7a028-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="7a028-188">Als u verbonden tooAzure via een proxy bent, moet u controleren of de proxyinstellingen juist zijn.</span><span class="sxs-lookup"><span data-stu-id="7a028-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="7a028-189">Als u toegang tooa resource zijn verleend van Hallo eigenaar van het Hallo-abonnement of account, Controleer of u hebt gelezen of lijst met machtigingen voor die bron.</span><span class="sxs-lookup"><span data-stu-id="7a028-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="7a028-190">Problemen met SAS-URL</span><span class="sxs-lookup"><span data-stu-id="7a028-190">Issues with SAS URL</span></span>
<span data-ttu-id="7a028-191">Als u verbinding tooa service met behulp van een SAS-URL en deze fout optreedt maakt:</span><span class="sxs-lookup"><span data-stu-id="7a028-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="7a028-192">Controleer of dat Hallo URL de benodigde machtigingen Hallo tooread of lijst met resources biedt.</span><span class="sxs-lookup"><span data-stu-id="7a028-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="7a028-193">Controleer of deze Hallo die URL niet is verlopen.</span><span class="sxs-lookup"><span data-stu-id="7a028-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="7a028-194">Als Hallo SAS-URL is gebaseerd op een toegangsbeleid, controleert u of Hallo-beleid niet is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="7a028-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a028-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a028-195">Next steps</span></span>

<span data-ttu-id="7a028-196">Als geen van de oplossingen Hallo werkt, Geef uw probleem via Hallo feedback hulpprogramma met uw e-mailadres en zoveel mogelijk details over Hallo probleem opgenomen als u kunnen, zodat we kunnen contact met u voor het oplossen van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="7a028-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="7a028-197">toodo, klikt u op **Help** menu en klik vervolgens op **Feedback verzenden**.</span><span class="sxs-lookup"><span data-stu-id="7a028-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Feedback](./media/storage-explorer-troubleshooting/4022503_en_1.png)
