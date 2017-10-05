---
title: Problemen met Data Management Gateway | Microsoft Docs
description: Tips voor het oplossen van problemen met Data Management Gateway biedt.
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
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="d7c10-103">Problemen oplossen met behulp van Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="d7c10-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="d7c10-104">In dit artikel bevat informatie over het oplossen van problemen met het gebruik van Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c10-105">Zie de [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie over de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="d7c10-106">Zie de [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor een overzicht van de gegevens uit een on-premises SQL Server database verplaatsen naar Microsoft Azure Blob-opslag met behulp van de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="d7c10-107">Installatie mislukt of gateway registreren</span><span class="sxs-lookup"><span data-stu-id="d7c10-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="d7c10-108">1. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-108">1. Problem</span></span>
<span data-ttu-id="d7c10-109">U ziet dit foutbericht werd weergegeven bij het installeren en registreren van een gateway in het bijzonder tijdens het downloaden van het installatiebestand van de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="d7c10-110">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-110">Cause</span></span>
<span data-ttu-id="d7c10-111">De computer waarop u probeert te installeren van de gateway is mislukt voor het downloaden van het meest recente installatiebestand voor de gateway van het Downloadcentrum door een netwerkprobleem.</span><span class="sxs-lookup"><span data-stu-id="d7c10-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-112">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-112">Resolution</span></span>
<span data-ttu-id="d7c10-113">Controleer de instellingen van uw firewall proxy om te zien of de instellingen blokkeren met de netwerkverbinding van de computer naar de [Downloadcentrum](https://download.microsoft.com/), en werk de instellingen dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="d7c10-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="d7c10-114">U kunt ook downloaden van het installatiebestand voor de nieuwste gateway via de [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=39717) op andere computers die toegang heeft tot het download center.</span><span class="sxs-lookup"><span data-stu-id="d7c10-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="d7c10-115">U kunt het installer-bestand kopiëren naar de gateway-hostcomputer en deze handmatig te installeren en bijwerken van de gateway uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="d7c10-116">2. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-116">2. Problem</span></span>
<span data-ttu-id="d7c10-117">Deze fout te zien wanneer u probeert een gateway installeren door te klikken op **rechtstreeks op deze computer installeren** in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7c10-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="d7c10-118">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-118">Cause</span></span>
<span data-ttu-id="d7c10-119">Een gateway is al geïnstalleerd op de machine.</span><span class="sxs-lookup"><span data-stu-id="d7c10-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-120">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-120">Resolution</span></span>
<span data-ttu-id="d7c10-121">Verwijder de bestaande gateway op de machine en klik op de **rechtstreeks op deze computer installeren** opnieuw koppelen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="d7c10-122">3. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-122">3. Problem</span></span>
<span data-ttu-id="d7c10-123">U ziet deze fout bij het registreren van een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="d7c10-124">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-124">Cause</span></span>
<span data-ttu-id="d7c10-125">Dit bericht kan worden weergegeven voor een van de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="d7c10-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="d7c10-126">De indeling van de gatewaycode is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="d7c10-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="d7c10-127">De gatewaycode is ongeldig gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d7c10-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="d7c10-128">De gatewaycode is opnieuw vanuit de portal is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d7c10-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="d7c10-129">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-129">Resolution</span></span>
<span data-ttu-id="d7c10-130">Controleer of u de juiste gatewaycode via de portal.</span><span class="sxs-lookup"><span data-stu-id="d7c10-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="d7c10-131">Indien nodig, een sleutel opnieuw genereren en de sleutel gebruiken om de gateway te registreren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="d7c10-132">4. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-132">4. Problem</span></span>
<span data-ttu-id="d7c10-133">U ziet het volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Inhoud of de indeling van de sleutel is ongeldig](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-135">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-135">Cause</span></span>
<span data-ttu-id="d7c10-136">De inhoud of de indeling van de invoer gatewaycode is onjuist.</span><span class="sxs-lookup"><span data-stu-id="d7c10-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="d7c10-137">Een van de redenen kan zijn dat u slechts een deel van de sleutel hebt gekopieerd uit de portal of u een ongeldige sleutel.</span><span class="sxs-lookup"><span data-stu-id="d7c10-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-138">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-138">Resolution</span></span>
<span data-ttu-id="d7c10-139">Genereren van een gatewaysleutel in de portal en gebruik de knop kopiëren om te kopiëren van de gehele sleutel.</span><span class="sxs-lookup"><span data-stu-id="d7c10-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="d7c10-140">Plak deze in dit venster om de gateway te registreren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="d7c10-141">5. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-141">5. Problem</span></span>
<span data-ttu-id="d7c10-142">U ziet het volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-144">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-144">Cause</span></span>
<span data-ttu-id="d7c10-145">De gatewaycode is gegenereerd of de gateway is verwijderd in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7c10-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="d7c10-146">Het kan ook gebeuren als de installatie van Data Management Gateway geen laatste is.</span><span class="sxs-lookup"><span data-stu-id="d7c10-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-147">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-147">Resolution</span></span>
<span data-ttu-id="d7c10-148">Controleer als de installatie van Data Management Gateway de meest recente versie is, kunt u de meest recente versie vinden op de Microsoft [Downloadcentrum](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="d7c10-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="d7c10-149">Als setup is de huidige / nieuwste en gateway nog op de Portal bestaat, de gatewaysleutel in de Azure portal opnieuw genereren en gebruik de knop kopiëren om te kopiëren van de gehele sleutel en plak deze in dit venster om de gateway te registreren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="d7c10-150">Anders opnieuw maken van de gateway en begin opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d7c10-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="d7c10-151">6. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-151">6. Problem</span></span>
<span data-ttu-id="d7c10-152">U ziet het volgende foutbericht weergegeven wanneer u bij het registreren van een gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![Gatewaycode is ongeldig of leeg](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-154">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-154">Cause</span></span>
<span data-ttu-id="d7c10-155">Deze fout kan optreden omdat de gateway is verwijderd of de verbonden gatewaycode is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d7c10-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-156">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-156">Resolution</span></span>
<span data-ttu-id="d7c10-157">Als de gateway is verwijderd, opnieuw de gateway vanuit de portal maken, klikt u op **registreren**, Kopieer de sleutel van de portal, plakt u deze en probeert om de gateway te registreren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="d7c10-158">Als de gateway nog wel bestaat, maar de sleutel is gegenereerd, gebruikt u de nieuwe sleutel om de gateway te registreren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="d7c10-159">Als u de sleutel niet hebt, moet u de sleutel opnieuw vanuit de portal opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="d7c10-160">7. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-160">7. Problem</span></span>
<span data-ttu-id="d7c10-161">Wanneer u een gateway registreren wilt, moet u mogelijk pad en wachtwoord invoeren voor een certificaat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-163">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-163">Cause</span></span>
<span data-ttu-id="d7c10-164">De gateway is geregistreerd op andere computers voordat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="d7c10-165">Tijdens de initiële registratie van een gateway is een versleutelingscertificaat gekoppeld aan de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="d7c10-166">Het certificaat kan automatisch gegenereerd door de gateway of door de gebruiker opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d7c10-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="d7c10-167">Dit certificaat wordt gebruikt om de referenties van het gegevensarchief (gekoppelde service) te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Certificaat exporteren](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="d7c10-169">Bij het herstellen van de gateway op een andere hostmachine, wordt u gevraagd de registratiewizard voor dit certificaat voor het ontsleutelen van referenties die eerder werden gecodeerd met dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="d7c10-170">De referenties kunnen niet worden ontsleuteld door de nieuwe gateway en latere kopie activiteit uitvoeringen die zijn gekoppeld aan deze nieuwe gateway niet zonder dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="d7c10-171">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-171">Resolution</span></span>
<span data-ttu-id="d7c10-172">Als u de referenties van het certificaat van de oorspronkelijke computer met de gateway hebt geëxporteerd met behulp van de **exporteren** knop op de **instellingen** tabblad in Data Management Gateway Configuration Manager, gebruikt u het certificaat Hier.</span><span class="sxs-lookup"><span data-stu-id="d7c10-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="d7c10-173">U kunt deze fase niet overslaan tijdens het herstellen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="d7c10-174">Als het certificaat ontbreekt, moet u de gateway van de portal te verwijderen en opnieuw maken van een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="d7c10-175">Daarnaast werkt u alle gekoppelde services die zijn gerelateerd aan de gateway door hun referenties opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="d7c10-176">8. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-176">8. Problem</span></span>
<span data-ttu-id="d7c10-177">U ziet het volgende foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d7c10-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="d7c10-178">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-178">Cause</span></span>
<span data-ttu-id="d7c10-179">Deze fout treedt op wanneer uw gateway zich in een omgeving waarin een HTTP-proxy voor toegang tot internetbronnen, of het wachtwoord voor uw proxy-verificatie is gewijzigd, maar deze wordt niet dienovereenkomstig bijgewerkt in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-180">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-180">Resolution</span></span>
<span data-ttu-id="d7c10-181">Volg de instructies in de [overwegingen voor Proxy server](#proxy-server-considerations) sectie van dit artikel en proxy-instellingen configureren met Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d7c10-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="d7c10-182">Gateway is online via beperkte functionaliteit</span><span class="sxs-lookup"><span data-stu-id="d7c10-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="d7c10-183">1. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-183">1. Problem</span></span>
<span data-ttu-id="d7c10-184">U ziet de status van de gateway online met beperkte functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="d7c10-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="d7c10-185">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-185">Cause</span></span>
<span data-ttu-id="d7c10-186">U ziet de status van de gateway online met beperkte functionaliteit voor een van de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="d7c10-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="d7c10-187">Gateway kan geen verbinding maken met cloudservice via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d7c10-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="d7c10-188">Cloudservice kan geen verbinding met de gateway via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d7c10-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="d7c10-189">Wanneer de gateway online met beperkte functionaliteit is, kunt u mogelijk niet de Data Factory-Wizard kopiëren gebruiken om te maken van gegevenspijplijnen voor het kopiëren van gegevens naar of van on-premises gegevensopslagexemplaren.</span><span class="sxs-lookup"><span data-stu-id="d7c10-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="d7c10-190">Als tijdelijke oplossing kunt u Data Factory-Editor in de portal, Visual Studio of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7c10-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-191">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-191">Resolution</span></span>
<span data-ttu-id="d7c10-192">Oplossing voor dit probleem (online met beperkte functionaliteit) is gebaseerd op of de gateway kan geen verbinding met de cloudservice of de andere kant maken.</span><span class="sxs-lookup"><span data-stu-id="d7c10-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="d7c10-193">De volgende secties bevatten deze oplossingen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="d7c10-194">2. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-194">2. Problem</span></span>
<span data-ttu-id="d7c10-195">Ziet u de volgende fout.</span><span class="sxs-lookup"><span data-stu-id="d7c10-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![Gateway kan geen verbinding maken met cloudservice](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-197">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-197">Cause</span></span>
<span data-ttu-id="d7c10-198">Gateway kan geen verbinding maken met de cloudservice via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d7c10-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-199">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-199">Resolution</span></span>
<span data-ttu-id="d7c10-200">Volg deze stappen om de gateway weer online:</span><span class="sxs-lookup"><span data-stu-id="d7c10-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="d7c10-201">IP-adres uitgaande regels op de gatewaycomputer en de firewall van het bedrijf toestaan.</span><span class="sxs-lookup"><span data-stu-id="d7c10-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="d7c10-202">U kunt IP-adressen vinden via het Windows-gebeurtenislogboek (ID == 401): Er is een poging gedaan te krijgen tot een socket op een manier die volgens de toegangsmachtigingen XX is niet toegestaan. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="d7c10-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="d7c10-203">Proxy-instellingen configureren op de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="d7c10-204">Zie de [overwegingen voor Proxy server](#proxy-server-considerations) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d7c10-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="d7c10-205">Schakel de uitgaande poort 5671 en 9350-9354 op zowel de Windows Firewall op de gatewaycomputer en de firewall van het bedrijf.</span><span class="sxs-lookup"><span data-stu-id="d7c10-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="d7c10-206">Zie de [poorten en firewall](#ports-and-firewall) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d7c10-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="d7c10-207">Deze stap is optioneel, maar we raden aan voor prestaties overweging.</span><span class="sxs-lookup"><span data-stu-id="d7c10-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="d7c10-208">3. Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-208">3. Problem</span></span>
<span data-ttu-id="d7c10-209">Ziet u de volgende fout.</span><span class="sxs-lookup"><span data-stu-id="d7c10-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="d7c10-210">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-210">Cause</span></span>
<span data-ttu-id="d7c10-211">Een tijdelijke fout in verbinding met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="d7c10-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-212">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-212">Resolution</span></span>
<span data-ttu-id="d7c10-213">Volg deze stappen om de gateway weer online:</span><span class="sxs-lookup"><span data-stu-id="d7c10-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="d7c10-214">Wacht een paar minuten, de verbindingen worden automatisch hersteld wanneer de fout is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d7c10-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="d7c10-215">Als de fout zich blijft voordoen, start u de gateway-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d7c10-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="d7c10-216">Kan geen gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="d7c10-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="d7c10-217">Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-217">Problem</span></span>
<span data-ttu-id="d7c10-218">U kunt deze fout tegenkomen wanneer u probeert te Referentiebeheer in de portal te gebruiken referenties voor een nieuwe gekoppelde service invoeren of bijwerken van referenties voor een bestaande gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d7c10-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="d7c10-219">Wanneer u deze fout ziet, kan de instellingenpagina van Data Management Gateway Configuration Manager de volgende schermafbeelding eruitzien.</span><span class="sxs-lookup"><span data-stu-id="d7c10-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Database kan niet worden bereikt](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="d7c10-221">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-221">Cause</span></span>
<span data-ttu-id="d7c10-222">Het SSL-certificaat is mogelijk verloren gegaan op de gatewaycomputer.</span><span class="sxs-lookup"><span data-stu-id="d7c10-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="d7c10-223">Computer met de gateway kan het certificaat op dat moment die wordt gebruikt voor SSL-versleuteling niet laden.</span><span class="sxs-lookup"><span data-stu-id="d7c10-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="d7c10-224">U ziet ook een foutbericht weergegeven in het gebeurtenislogboek die vergelijkbaar is met het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="d7c10-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="d7c10-225">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-225">Resolution</span></span>
<span data-ttu-id="d7c10-226">Volg deze stappen om het probleem te verhelpen:</span><span class="sxs-lookup"><span data-stu-id="d7c10-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="d7c10-227">Start de Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d7c10-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="d7c10-228">Overschakelen naar de **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d7c10-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="d7c10-229">Klik op de **wijzigen** om te wijzigen van het SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![De knop certificaat wijzigen](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="d7c10-231">Selecteer een nieuw certificaat als het SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="d7c10-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="d7c10-232">U kunt een SSL-certificaat dat is gegenereerd door u of elke organisatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d7c10-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Certificaat opgeven](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="d7c10-234">Kopieeractiviteit mislukt</span><span class="sxs-lookup"><span data-stu-id="d7c10-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="d7c10-235">Probleem</span><span class="sxs-lookup"><span data-stu-id="d7c10-235">Problem</span></span>
<span data-ttu-id="d7c10-236">Ziet u mogelijk de volgende 'UserErrorFailedToConnectToSqlserver' fout na het instellen van een pijplijn in de portal.</span><span class="sxs-lookup"><span data-stu-id="d7c10-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="d7c10-237">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d7c10-237">Cause</span></span>
<span data-ttu-id="d7c10-238">Dit kan gebeuren om verschillende redenen en risicobeperking varieert dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="d7c10-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="d7c10-239">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d7c10-239">Resolution</span></span>
<span data-ttu-id="d7c10-240">Toestaan van uitgaande TCP-verbindingen via poort TCP 1433/aan de clientzijde Data Management Gateway voordat u verbinding maakt met een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="d7c10-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="d7c10-241">Als de doeldatabase een Azure SQL database is, controleert u de SQL Server firewall-instellingen voor Azure ook.</span><span class="sxs-lookup"><span data-stu-id="d7c10-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="d7c10-242">Zie de volgende sectie voor het testen van de verbinding met de on-premises gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="d7c10-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="d7c10-243">Gegevens opslaan verbinding of stuurprogramma gerelateerde fouten</span><span class="sxs-lookup"><span data-stu-id="d7c10-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="d7c10-244">Als u gegevens opslaan verbinding of stuurprogramma gerelateerde fouten ziet, kunt u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d7c10-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="d7c10-245">Start de Data Management Gateway Configuration Manager op de gatewaycomputer.</span><span class="sxs-lookup"><span data-stu-id="d7c10-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="d7c10-246">Overschakelen naar de **Diagnostics** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d7c10-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="d7c10-247">In **testverbinding**, voeg de waarden van de groep gateway toe.</span><span class="sxs-lookup"><span data-stu-id="d7c10-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="d7c10-248">Klik op **Test** om te zien als u verbinding met de lokale gegevensbron van het gateway-apparaat maken kunt met behulp van de verbindingsgegevens en referenties.</span><span class="sxs-lookup"><span data-stu-id="d7c10-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="d7c10-249">Als de testverbinding ook niet lukt nadat u een stuurprogramma hebt geïnstalleerd, start u de gateway opnieuw op om de meest recente wijziging op te halen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Testverbinding in tabblad Diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="d7c10-251">Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="d7c10-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="d7c10-252">Gateway-logboeken naar Microsoft verzenden</span><span class="sxs-lookup"><span data-stu-id="d7c10-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="d7c10-253">Wanneer u contact opneemt met Microsoft Support voor hulp bij het oplossen van problemen van de gateway, wordt u mogelijk gevraagd om te delen van uw gateway-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d7c10-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="d7c10-254">Met het uitbrengen van de gateway, kunt u logboeken met twee knop klikken in Data Management Gateway Configuration Manager vereist gateway delen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="d7c10-255">Overschakelen naar de **Diagnostics** tabblad in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d7c10-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Tabblad van Data Management Gateway diagnostische gegevens](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="d7c10-257">Klik op **logboeken verzenden** om te zien van het volgende dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d7c10-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Data Management Gateway verzenden Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="d7c10-259">(Optioneel) Klik op **logboeken bekijken** te bekijken in de event viewer registreert.</span><span class="sxs-lookup"><span data-stu-id="d7c10-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="d7c10-260">(Optioneel) Klik op **privacy** om te controleren van de privacyverklaring van Microsoft web services.</span><span class="sxs-lookup"><span data-stu-id="d7c10-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="d7c10-261">Wanneer u tevreden bent met wat u gaat uploaden, klikt u op **logboeken verzenden** daadwerkelijk de logboeken van de afgelopen zeven dagen naar Microsoft te verzenden voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="d7c10-262">U ziet de status van de bewerking send logboeken zoals weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="d7c10-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="d7c10-264">Nadat de bewerking voltooid is, ziet u een dialoogvenster, zoals wordt weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="d7c10-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Data Management Gateway verzenden logboeken status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="d7c10-266">Sla de **rapport ID** en delen met Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="d7c10-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="d7c10-267">De lijst-ID wordt gebruikt voor het vinden van de gateway-logboeken die u hebt geüpload voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="d7c10-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="d7c10-268">De lijst-ID wordt ook opgeslagen in de event viewer.</span><span class="sxs-lookup"><span data-stu-id="d7c10-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="d7c10-269">U kunt vinden door te kijken naar de gebeurtenis-ID '25', en controleer of de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="d7c10-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Data Management Gateway verzenden Logboeken lijst-ID](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="d7c10-271">Archief gateway-logboeken op de hostmachine gateway</span><span class="sxs-lookup"><span data-stu-id="d7c10-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="d7c10-272">Er zijn enkele scenario's waarbij u problemen met de gateway hebt en u gateway-logboeken rechtstreeks niet delen:</span><span class="sxs-lookup"><span data-stu-id="d7c10-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="d7c10-273">U handmatig installeren van de gateway en registreer de gateway.</span><span class="sxs-lookup"><span data-stu-id="d7c10-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="d7c10-274">U probeert te registreren van de gateway met een opnieuw gegenereerde sleutel in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d7c10-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="d7c10-275">U probeert om Logboeken te verzenden en de gateway-hostservice kan niet worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="d7c10-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="d7c10-276">Voor deze scenario's, kunt u de gateway-Logboeken als een zip-bestand opslaan en delen wanneer u contact opneemt met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d7c10-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="d7c10-277">Bijvoorbeeld, als er een fout opgetreden tijdens het registreren van de gateway als weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="d7c10-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Data Management Gateway-Registratiefout](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="d7c10-279">Klik op de **gateway-logboeken archiveren** koppeling voor het archiveren en Logboeken opslaan en vervolgens het zip-bestand delen met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d7c10-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Data Management Gateway archief Logboeken](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="d7c10-281">Naar de gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="d7c10-281">Locate gateway logs</span></span>
<span data-ttu-id="d7c10-282">U vindt gedetailleerde gateway logboekgegevens in de Windows-gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="d7c10-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="d7c10-283">Start Windows **logboeken**.</span><span class="sxs-lookup"><span data-stu-id="d7c10-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="d7c10-284">Ga naar Logboeken in de **toepassings- en servicelogboeken** > **Data Management Gateway** map.</span><span class="sxs-lookup"><span data-stu-id="d7c10-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="d7c10-285">Wanneer u bent het oplossen van problemen met de gateway, zoek naar niveau foutgebeurtenissen in de event viewer.</span><span class="sxs-lookup"><span data-stu-id="d7c10-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Data Management Gateway wordt geregistreerd in Logboeken](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
