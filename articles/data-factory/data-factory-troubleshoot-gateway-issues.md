---
title: problemen met Data Management Gateway aaaTroubleshoot | Microsoft Docs
description: Biedt tips tootroubleshoot problemen gerelateerde tooData Management Gateway.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="dad17-103">Problemen oplossen met behulp van Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="dad17-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="dad17-104">In dit artikel bevat informatie over het oplossen van problemen met het gebruik van Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dad17-105">Zie Hallo [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie over het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="dad17-106">Zie Hallo [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor een overzicht van het verplaatsen van gegevens vanuit een lokale SQL Server-database tooMicrosoft Azure Blob-opslag met behulp van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="dad17-107">Mislukte tooinstall of Registreer gateway</span><span class="sxs-lookup"><span data-stu-id="dad17-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="dad17-108">1. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-108">1. Problem</span></span>
<span data-ttu-id="dad17-109">U ziet dit foutbericht werd weergegeven bij het installeren en registreren van een gateway in het bijzonder tijdens het downloaden van Hallo gateway-installatiebestand.</span><span class="sxs-lookup"><span data-stu-id="dad17-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="dad17-110">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-110">Cause</span></span>
<span data-ttu-id="dad17-111">Hallo-machine waarop u tooinstall Hallo gateway probeert is toodownload Hallo nieuwste gateway-bestand voor installatie van Downloadcentrum Hallo vanwege tooa netwerkprobleem mislukt.</span><span class="sxs-lookup"><span data-stu-id="dad17-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-112">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-112">Resolution</span></span>
<span data-ttu-id="dad17-113">Controleer uw firewall proxy server instellingen toosee of Hallo instellingen Hallo netwerkverbinding van Hallo computer toohello blokkeren [Downloadcentrum](https://download.microsoft.com/), en het Hallo-instellingen bijwerken dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="dad17-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="dad17-114">U kunt ook Hallo-installatiebestand voor de nieuwste gateway Hallo downloaden van Hallo [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=39717) op andere computers die toegang heeft tot Hallo Downloadcentrum.</span><span class="sxs-lookup"><span data-stu-id="dad17-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="dad17-115">U kunt vervolgens kopiëren Hallo installer-bestand toohello gateway hostcomputer en voer deze handmatig tooinstall en update Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="dad17-116">2. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-116">2. Problem</span></span>
<span data-ttu-id="dad17-117">Deze fout te zien wanneer u een gateway tooinstall probeert door te klikken op **rechtstreeks op deze computer installeren** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dad17-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="dad17-118">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-118">Cause</span></span>
<span data-ttu-id="dad17-119">Een gateway is al geïnstalleerd op Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="dad17-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-120">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-120">Resolution</span></span>
<span data-ttu-id="dad17-121">Verwijderen van de bestaande gateway Hallo op Hallo machine en klik op Hallo **rechtstreeks op deze computer installeren** opnieuw koppelen.</span><span class="sxs-lookup"><span data-stu-id="dad17-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="dad17-122">3. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-122">3. Problem</span></span>
<span data-ttu-id="dad17-123">U ziet deze fout bij het registreren van een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="dad17-124">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-124">Cause</span></span>
<span data-ttu-id="dad17-125">U ziet dit bericht voor een van de volgende redenen Hallo:</span><span class="sxs-lookup"><span data-stu-id="dad17-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="dad17-126">Hallo-indeling van Hallo gatewaycode is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="dad17-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="dad17-127">Hallo gatewaycode is ongeldig gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dad17-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="dad17-128">Hallo gatewaycode is opnieuw vanuit de portal Hallo is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="dad17-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="dad17-129">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-129">Resolution</span></span>
<span data-ttu-id="dad17-130">Controleer of u Hallo rechts gatewaycode via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="dad17-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="dad17-131">Indien nodig, een sleutel opnieuw genereren en Hallo sleutel tooregister Hallo gateway gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dad17-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="dad17-132">4. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-132">4. Problem</span></span>
<span data-ttu-id="dad17-133">U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Inhoud of de indeling van de sleutel is ongeldig](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="dad17-135">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-135">Cause</span></span>
<span data-ttu-id="dad17-136">Hallo is inhoud of de indeling van de invoer gatewaycode Hallo onjuist.</span><span class="sxs-lookup"><span data-stu-id="dad17-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="dad17-137">Een van de redenen Hallo kan zijn dat u alleen een deel van de sleutel Hallo gekopieerd uit Hallo-portal of u een ongeldige sleutel.</span><span class="sxs-lookup"><span data-stu-id="dad17-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-138">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-138">Resolution</span></span>
<span data-ttu-id="dad17-139">Een gatewaysleutel genereren in Hallo-portal en Hallo kopie knop toocopy Hallo gehele sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dad17-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="dad17-140">Plak deze in dit venster tooregister Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="dad17-141">5. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-141">5. Problem</span></span>
<span data-ttu-id="dad17-142">U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="dad17-144">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-144">Cause</span></span>
<span data-ttu-id="dad17-145">Hallo gatewaycode is gegenereerd of Hallo gateway is verwijderd op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dad17-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="dad17-146">Het kan ook gebeuren als Hallo Data Management Gateway-installatie niet nieuwste is.</span><span class="sxs-lookup"><span data-stu-id="dad17-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-147">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-147">Resolution</span></span>
<span data-ttu-id="dad17-148">Controleer als Hallo Data Management Gateway-installatie de meest recente versie hello is, kunt u de meest recente versie Hallo vinden op Hallo Microsoft [Downloadcentrum](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="dad17-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="dad17-149">Als setup is de huidige / nieuwste en gateway nog op de Portal bestaat, lezensleutel Hallo gateway in hello Azure-portal en Hallo kopie knop toocopy Hallo gehele sleutel gebruiken en plak deze in dit venster tooregister Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="dad17-150">Anders Hallo-gateway opnieuw maken en begin opnieuw.</span><span class="sxs-lookup"><span data-stu-id="dad17-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="dad17-151">6. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-151">6. Problem</span></span>
<span data-ttu-id="dad17-152">U ziet Hallo volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="dad17-154">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-154">Cause</span></span>
<span data-ttu-id="dad17-155">Deze fout kan optreden omdat Hallo gateway is verwijderd of Hallo verbonden gatewaycode is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="dad17-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-156">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-156">Resolution</span></span>
<span data-ttu-id="dad17-157">Als het Hallo-gateway is verwijderd, Hallo gateway vanuit Hallo portal opnieuw te maken, klikt u op **registreren**, kopieer Hallo-sleutel van het Hallo-portal, plakt u deze en probeer tooregister Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="dad17-158">Als Hallo gateway nog bestaat, maar de sleutel is gegenereerd, gebruikt u Hallo nieuwe sleutel tooregister Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="dad17-159">Als er geen sleutel hello, Hallo-sleutel opnieuw vanuit het Hallo-portal opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="dad17-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="dad17-160">7. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-160">7. Problem</span></span>
<span data-ttu-id="dad17-161">Wanneer u een gateway registreren wilt, moet u mogelijk tooenter pad en het wachtwoord voor een certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="dad17-163">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-163">Cause</span></span>
<span data-ttu-id="dad17-164">Hallo-gateway is geregistreerd op andere computers voordat.</span><span class="sxs-lookup"><span data-stu-id="dad17-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="dad17-165">Tijdens de initiële registratie van een gateway Hallo is een versleutelingscertificaat gekoppeld aan het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="dad17-166">Hallo certificaat kan automatisch worden gegenereerd door Hallo gateway of opgegeven door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="dad17-167">Dit certificaat is gebruikte tooencrypt referenties van het gegevensarchief hello (gekoppelde service).</span><span class="sxs-lookup"><span data-stu-id="dad17-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Certificaat exporteren](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="dad17-169">Wanneer herstellen Hallo-gateway op een andere hostmachine, wordt u gevraagd de wizard Registratie Hallo voor dit certificaat toodecrypt eerder referenties gecodeerd met dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="dad17-170">Hallo referenties kunnen niet worden ontsleuteld door de nieuwe gateway Hallo en latere kopie activiteit uitvoeringen die zijn gekoppeld aan deze nieuwe gateway kunnen geen zonder dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="dad17-171">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-171">Resolution</span></span>
<span data-ttu-id="dad17-172">Als u Hallo referentiecertificaat hebt geëxporteerd uit de oorspronkelijke gatewaycomputer Hallo via Hallo **exporteren** knop op Hallo **instellingen** tabblad in Data Management Gateway Configuration Manager, gebruikt u Hallo Hier certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="dad17-173">U kunt deze fase niet overslaan tijdens het herstellen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="dad17-174">Als Hallo certificaat ontbreekt, u moet toodelete Hallo gateway vanuit Hallo-portal en opnieuw maken van een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="dad17-175">Daarnaast werkt u alle gekoppelde services die gerelateerd toohello gateway zijn door hun referenties opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="dad17-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="dad17-176">8. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-176">8. Problem</span></span>
<span data-ttu-id="dad17-177">U ziet Hallo volgende foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dad17-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="dad17-178">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-178">Cause</span></span>
<span data-ttu-id="dad17-179">Deze fout treedt op wanneer uw gateway in een omgeving die een HTTP-proxy tooaccess internetbronnen vereist is of uw Proxywachtwoord verificatie is gewijzigd, maar deze niet dienovereenkomstig bijgewerkt in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-180">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-180">Resolution</span></span>
<span data-ttu-id="dad17-181">Volg de instructies Hallo in Hallo [overwegingen voor Proxy server](#proxy-server-considerations) sectie van dit artikel en proxy-instellingen configureren met Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dad17-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="dad17-182">Gateway is online via beperkte functionaliteit</span><span class="sxs-lookup"><span data-stu-id="dad17-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="dad17-183">1. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-183">1. Problem</span></span>
<span data-ttu-id="dad17-184">Hallo-status van Hallo gateway worden weergegeven als online met beperkte functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="dad17-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="dad17-185">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-185">Cause</span></span>
<span data-ttu-id="dad17-186">Hallo-status van Hallo gateway die u met beperkte functionaliteit voor een van de volgende redenen Hallo als on line zien:</span><span class="sxs-lookup"><span data-stu-id="dad17-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="dad17-187">Gateway kan geen toocloud service verbinding via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dad17-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="dad17-188">Cloudservice kan geen toogateway verbinding via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dad17-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="dad17-189">Wanneer Hallo gateway online met beperkte functionaliteit is, mogelijk niet kunnen toouse Hallo Data Factory-Wizard kopiëren toocreate gegevenspijplijnen voor het kopiëren van gegevens tooor van on-premises gegevensopslagexemplaren.</span><span class="sxs-lookup"><span data-stu-id="dad17-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="dad17-190">Als tijdelijke oplossing kunt u Data Factory-Editor in Hallo portal voor Visual Studio of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dad17-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-191">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-191">Resolution</span></span>
<span data-ttu-id="dad17-192">Oplossing voor dit probleem (online met beperkte functionaliteit) is gebaseerd op of Hallo gateway kan geen verbinding maken met cloudservice toohello of Hallo andere manier.</span><span class="sxs-lookup"><span data-stu-id="dad17-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="dad17-193">Hallo volgende secties bieden deze oplossingen.</span><span class="sxs-lookup"><span data-stu-id="dad17-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="dad17-194">2. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-194">2. Problem</span></span>
<span data-ttu-id="dad17-195">U zien Hallo volgende fout.</span><span class="sxs-lookup"><span data-stu-id="dad17-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway kan geen toocloud-service verbinding](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="dad17-197">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-197">Cause</span></span>
<span data-ttu-id="dad17-198">Gateway kan geen verbinding met het maken van de cloudservice toohello via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dad17-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-199">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-199">Resolution</span></span>
<span data-ttu-id="dad17-200">Volg deze stappen tooget Hallo gateway weer online:</span><span class="sxs-lookup"><span data-stu-id="dad17-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="dad17-201">IP-adres uitgaande regels op de gatewaycomputer Hallo en Hallo bedrijfsfirewall toestaan.</span><span class="sxs-lookup"><span data-stu-id="dad17-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="dad17-202">Vindt u IP-adressen uit het gebeurtenislogboek van Windows hello (ID == 401): een poging is gedaan tooaccess een socket op een manier die volgens de toegangsmachtigingen XX is niet toegestaan. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="dad17-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="dad17-203">Proxy-instellingen configureren op Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="dad17-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="dad17-204">Zie Hallo [overwegingen voor Proxy server](#proxy-server-considerations) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dad17-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="dad17-205">Uitgaande poort 5671 en 9350-9354 op beide Hallo Windows Firewall op de gatewaycomputer Hallo en Hallo bedrijfsfirewall inschakelen.</span><span class="sxs-lookup"><span data-stu-id="dad17-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="dad17-206">Zie Hallo [poorten en firewall](#ports-and-firewall) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dad17-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="dad17-207">Deze stap is optioneel, maar we raden aan voor prestaties overweging.</span><span class="sxs-lookup"><span data-stu-id="dad17-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="dad17-208">3. Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-208">3. Problem</span></span>
<span data-ttu-id="dad17-209">U zien Hallo volgende fout.</span><span class="sxs-lookup"><span data-stu-id="dad17-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="dad17-210">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-210">Cause</span></span>
<span data-ttu-id="dad17-211">Een tijdelijke fout in verbinding met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="dad17-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-212">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-212">Resolution</span></span>
<span data-ttu-id="dad17-213">Volg deze stappen tooget Hallo gateway weer online:</span><span class="sxs-lookup"><span data-stu-id="dad17-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="dad17-214">Wacht een paar minuten, Hallo connectiviteit worden automatisch hersteld wanneer Hallo-fout is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="dad17-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="dad17-215">Als Hallo fout zich blijft voordoen, start u Hallo gateway-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="dad17-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="dad17-216">Mislukte tooauthor gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="dad17-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="dad17-217">Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-217">Problem</span></span>
<span data-ttu-id="dad17-218">U kunt deze fout tegenkomen wanneer u Referentiebeheer toouse Hallo portal tooinput referenties voor een nieuwe gekoppelde service probeert of referenties voor een bestaande gekoppelde service bijwerken.</span><span class="sxs-lookup"><span data-stu-id="dad17-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="dad17-219">Wanneer u deze fout ziet, Hallo instellingenpagina van Data Management Gateway Configuration Manager als volgt uitzien Hallo volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="dad17-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Database kan niet worden bereikt](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="dad17-221">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-221">Cause</span></span>
<span data-ttu-id="dad17-222">Hallo SSL-certificaat is mogelijk verloren gegaan op Hallo gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="dad17-223">Hallo gatewaycomputer kan Hallo certificaat momenteel dat wordt gebruikt voor SSL-versleuteling niet laden.</span><span class="sxs-lookup"><span data-stu-id="dad17-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="dad17-224">U ziet ook een foutbericht weergegeven in het Hallo-gebeurtenislogboek dat vergelijkbare toohello volgende bericht is.</span><span class="sxs-lookup"><span data-stu-id="dad17-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="dad17-225">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-225">Resolution</span></span>
<span data-ttu-id="dad17-226">Volg deze stappen toosolve Hallo probleem:</span><span class="sxs-lookup"><span data-stu-id="dad17-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="dad17-227">Start de Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dad17-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="dad17-228">Overschakelen van toohello **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="dad17-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="dad17-229">Klik op Hallo **wijziging** knop toochange Hallo SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![De knop certificaat wijzigen](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="dad17-231">Selecteer een nieuw certificaat als Hallo SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="dad17-232">U kunt een SSL-certificaat dat is gegenereerd door u of elke organisatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dad17-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="dad17-234">Kopieeractiviteit mislukt</span><span class="sxs-lookup"><span data-stu-id="dad17-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="dad17-235">Probleem</span><span class="sxs-lookup"><span data-stu-id="dad17-235">Problem</span></span>
<span data-ttu-id="dad17-236">Hallo na 'UserErrorFailedToConnectToSqlserver' fout na het instellen van een pijplijn in de portal hello, zult u merken.</span><span class="sxs-lookup"><span data-stu-id="dad17-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="dad17-237">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="dad17-237">Cause</span></span>
<span data-ttu-id="dad17-238">Dit kan gebeuren om verschillende redenen en risicobeperking varieert dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="dad17-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="dad17-239">Oplossing</span><span class="sxs-lookup"><span data-stu-id="dad17-239">Resolution</span></span>
<span data-ttu-id="dad17-240">Uitgaande TCP-verbindingen via TCP-poort/1433 op Hallo Data Management Gateway-clientzijde toestaan voordat u verbinding maakt tooan SQL-database.</span><span class="sxs-lookup"><span data-stu-id="dad17-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="dad17-241">Als de doeldatabase Hallo een Azure SQL database is, controleert u SQL Server firewall-instellingen voor Azure ook.</span><span class="sxs-lookup"><span data-stu-id="dad17-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="dad17-242">Zie de volgende sectie tootest Hallo verbinding toohello on-premises met gegevensopslag Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="dad17-243">Gegevens opslaan verbinding of stuurprogramma gerelateerde fouten</span><span class="sxs-lookup"><span data-stu-id="dad17-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="dad17-244">Als u gegevens opslaan verbinding of stuurprogramma gerelateerde fouten ziet, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dad17-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="dad17-245">Start de Data Management Gateway Configuration Manager op Hallo gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="dad17-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="dad17-246">Overschakelen van toohello **Diagnostics** tabblad.</span><span class="sxs-lookup"><span data-stu-id="dad17-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="dad17-247">In **testverbinding**, Hallo gateway groep waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dad17-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="dad17-248">Klik op **Test** toosee als u verbinding met toohello maken kunt on-premises gegevensbron uit de gatewaycomputer Hallo door met de verbindingsgegevens Hallo en referenties.</span><span class="sxs-lookup"><span data-stu-id="dad17-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="dad17-249">Als de testverbinding Hallo nog steeds niet na de installatie van een stuurprogramma, opnieuw opstarten hello gateway voor het toopick van laatste wijziging Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Testverbinding in tabblad Diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="dad17-251">Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="dad17-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="dad17-252">Gateway-logboeken tooMicrosoft verzenden</span><span class="sxs-lookup"><span data-stu-id="dad17-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="dad17-253">Wanneer u contact opneemt met Microsoft Support tooget hulp bij het oplossen van problemen met de gateway, wordt u mogelijk gevraagd tooshare uw gateway-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="dad17-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="dad17-254">Hallo-versie van gateway Hallo, kunt u logboeken met twee knop klikken in Data Management Gateway Configuration Manager vereist gateway delen.</span><span class="sxs-lookup"><span data-stu-id="dad17-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="dad17-255">Overschakelen van toohello **Diagnostics** tabblad in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dad17-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Tabblad van Data Management Gateway diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="dad17-257">Klik op **logboeken verzenden** toosee Hallo volgen in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dad17-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Data Management Gateway verzenden Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="dad17-259">(Optioneel) Klik op **logboeken bekijken** tooreview Logboeken in Logboeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="dad17-260">(Optioneel) Klik op **privacy** privacyverklaring tooreview Microsoft web services.</span><span class="sxs-lookup"><span data-stu-id="dad17-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="dad17-261">Wanneer u tevreden bent met wat u van tooupload zijn, klikt u op **logboeken verzenden** tooactually Hallo logboeken verzenden vanuit Hallo laatste zeven dagen tooMicrosoft voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="dad17-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="dad17-262">U ziet Hallo status van Hallo verzenden logboeken bewerking zoals weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="dad17-264">Nadat het Hallo-bewerking is voltooid, ziet u een dialoogvenster, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="dad17-266">Hallo opslaan **rapport ID** en delen met Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="dad17-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="dad17-267">Hallo rapport-ID is gebruikte toolocate Hallo gateway-logboeken die u hebt geüpload voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="dad17-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="dad17-268">Hallo lijst-ID wordt ook opgeslagen in de logboeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="dad17-269">U kunt vinden door te kijken naar Hallo gebeurtenis-ID '25', en controleren van Hallo datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="dad17-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Data Management Gateway verzenden Logboeken lijst-ID](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="dad17-271">Archief gateway-logboeken op de hostmachine gateway</span><span class="sxs-lookup"><span data-stu-id="dad17-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="dad17-272">Er zijn enkele scenario's waarbij u problemen met de gateway hebt en u gateway-logboeken rechtstreeks niet delen:</span><span class="sxs-lookup"><span data-stu-id="dad17-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="dad17-273">U handmatig Hallo gateway gateway installeren en registreren Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="dad17-274">U probeert tooregister Hallo gateway met een opnieuw gegenereerde sleutel in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dad17-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="dad17-275">U probeert toosend logboeken en Hallo gateway-hostservice kan niet worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="dad17-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="dad17-276">Voor deze scenario's, kunt u de gateway-Logboeken als een zip-bestand opslaan en delen wanneer u contact opneemt met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="dad17-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="dad17-277">Bijvoorbeeld als er een fout opgetreden tijdens het registreren van Hallo-gateway als weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="dad17-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Data Management Gateway-Registratiefout](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="dad17-279">Klik op Hallo **gateway-logboeken archiveren** tooarchive koppelen en Logboeken opslaan en vervolgens Hallo zip-bestand delen met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="dad17-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Data Management Gateway archief Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="dad17-281">Naar de gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="dad17-281">Locate gateway logs</span></span>
<span data-ttu-id="dad17-282">U vindt gedetailleerde gateway logboekgegevens in Hallo Windows-gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="dad17-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="dad17-283">Start Windows **logboeken**.</span><span class="sxs-lookup"><span data-stu-id="dad17-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="dad17-284">Logboeken niet vinden in Hallo **toepassings- en servicelogboeken** > **Data Management Gateway** map.</span><span class="sxs-lookup"><span data-stu-id="dad17-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="dad17-285">Wanneer u bent het oplossen van problemen met de gateway, zoek naar niveau foutgebeurtenissen in Hallo-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="dad17-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Data Management Gateway wordt geregistreerd in Logboeken](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
