---
title: aaaUsing omleiding in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooconfigure en gebruik omleiding in RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="62aa6-103">Met behulp van omleiding in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="62aa6-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="62aa6-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="62aa6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="62aa6-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="62aa6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="62aa6-106">Omleiding van apparaten kan uw gebruikers communiceren met externe apps met Hallo apparaten gekoppelde tootheir lokale computer, telefoon of tablet.</span><span class="sxs-lookup"><span data-stu-id="62aa6-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="62aa6-107">Als u Skype via Azure RemoteApp hebt opgegeven, moet de gebruiker Hallo camera op hun PC toowork met Skype geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="62aa6-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="62aa6-108">Dit geldt ook voor printers, luidsprekers, monitors en een bereik van USB-verbinding randapparatuur.</span><span class="sxs-lookup"><span data-stu-id="62aa6-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="62aa6-109">RemoteApp maakt gebruik van Hallo Remote Desktop Protocol (RDP) en RemoteFX tooprovide omleiding.</span><span class="sxs-lookup"><span data-stu-id="62aa6-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="62aa6-110">Welke omleiding is standaard ingeschakeld?</span><span class="sxs-lookup"><span data-stu-id="62aa6-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="62aa6-111">Wanneer u RemoteApp gebruikt, worden volgende omleidingen Hallo standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="62aa6-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="62aa6-112">Hallo informatie tussen haakjes weergegeven Hallo RDP-instelling.</span><span class="sxs-lookup"><span data-stu-id="62aa6-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="62aa6-113">Geluid afspelen op de lokale computer hello (**op deze computer afspelen**).</span><span class="sxs-lookup"><span data-stu-id="62aa6-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="62aa6-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="62aa6-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="62aa6-115">Geluid opnemen van de lokale computer Hallo en verzenden toohello externe computer (**Record van deze computer**).</span><span class="sxs-lookup"><span data-stu-id="62aa6-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="62aa6-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="62aa6-117">Afdrukken toolocal-printers (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="62aa6-118">COM-poorten (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="62aa6-119">Smartcard-apparaat (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="62aa6-120">Klembord (mogelijkheid toocopy en plakken) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="62aa6-121">Schakel type lettertype-aanpassing (lettertype-aanpassing toestaan: i:1)</span><span class="sxs-lookup"><span data-stu-id="62aa6-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="62aa6-122">Omleiden van alle ondersteunde Plug en Play-apparaten.</span><span class="sxs-lookup"><span data-stu-id="62aa6-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="62aa6-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="62aa6-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="62aa6-124">Welke andere omleiding is beschikbaar?</span><span class="sxs-lookup"><span data-stu-id="62aa6-124">What other redirection is available?</span></span>
<span data-ttu-id="62aa6-125">Er zijn twee opties voor Mapomleiding standaard uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="62aa6-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="62aa6-126">Stationsomleiding (stationstoewijzing): de lokale computer-stations worden toegewezen stations in de externe sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="62aa6-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="62aa6-127">Hiermee kunt u opslaat of geopende bestanden van de lokale vaste schijven terwijl u in de externe sessie Hallo werkt.</span><span class="sxs-lookup"><span data-stu-id="62aa6-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="62aa6-128">USB-omleiding: U kunt Hallo USB-apparaten gekoppelde tooyour lokale computer gebruiken in de externe sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="62aa6-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="62aa6-129">Wijzig de omleidingsinstellingen voor in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="62aa6-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="62aa6-130">U kunt Hallo apparaatinstellingen omleiding voor een verzameling wijzigen met behulp van Microsoft Azure PowerShell Hallo met SDK.</span><span class="sxs-lookup"><span data-stu-id="62aa6-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="62aa6-131">Nadat u Hallo nieuwe PowerShell- en SDK, moet u eerst toomanage uw abonnement als is beschreven in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62aa6-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="62aa6-132">Gebruik vervolgens een opdracht vergelijkbare toohello volgende tooset Hallo aangepaste RDP-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="62aa6-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="62aa6-133">(Houd er rekening mee dat  *\`n*  wordt gebruikt als scheidingsteken tussen de afzonderlijke eigenschappen.)</span><span class="sxs-lookup"><span data-stu-id="62aa6-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="62aa6-134">tooget een lijst met welke aangepaste RDP-eigenschappen zijn geconfigureerd, Hallo volgende cmdlet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="62aa6-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="62aa6-135">Houd er rekening mee dat alleen aangepaste eigenschappen worden weergegeven als de resultaten van de uitvoer en geen Hallo standaardeigenschappen:</span><span class="sxs-lookup"><span data-stu-id="62aa6-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="62aa6-136">Bij het instellen van aangepaste eigenschappen moet u alle aangepaste eigenschappen opgeven telkens; Hallo-instelling hersteld anders toodisabled.</span><span class="sxs-lookup"><span data-stu-id="62aa6-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="62aa6-137">Algemene voorbeelden</span><span class="sxs-lookup"><span data-stu-id="62aa6-137">Common examples</span></span>
<span data-ttu-id="62aa6-138">Hallo cmdlet tooenable stationsomleiding volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="62aa6-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="62aa6-139">Gebruik deze cmdlet tooenable omleiding van USB- en station:</span><span class="sxs-lookup"><span data-stu-id="62aa6-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="62aa6-140">Gebruik deze cmdlet toodisable Klembord delen:</span><span class="sxs-lookup"><span data-stu-id="62aa6-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="62aa6-141">Worden toocompletely ervoor dat alle gebruikers in de verzameling Hallo afmelden (en niet alleen verbreekt) voordat u gaat Hallo wijzigen testen.</span><span class="sxs-lookup"><span data-stu-id="62aa6-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="62aa6-142">tooensure zijn volledig afgemeld, Ga toohello **sessies** tabblad in de verzameling Hallo in hello Azure-portal en afmelden van gebruikers die zijn verbroken of aangemeld.</span><span class="sxs-lookup"><span data-stu-id="62aa6-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="62aa6-143">Soms kan het enkele seconden duren voor Hallo lokale stations tooshow in Verkenner binnen Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="62aa6-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="62aa6-144">Wijzig de instellingen van de USB-omleiding op uw Windows-client</span><span class="sxs-lookup"><span data-stu-id="62aa6-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="62aa6-145">Als u toouse USB-omleiding op een computer die verbinding tooRemoteApp wilt maakt, zijn er 2 acties die toohappen nodig.</span><span class="sxs-lookup"><span data-stu-id="62aa6-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="62aa6-146">1 - uw beheerder moet tooenable USB-omleiding op niveau van de verzameling Hallo met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62aa6-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="62aa6-147">2 - op elk apparaat waarop toouse USB-omleiding, moet u een groepsbeleid waarmee het tooenable.</span><span class="sxs-lookup"><span data-stu-id="62aa6-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="62aa6-148">Deze stap moet toobe gedaan voor elke gebruiker die wil toouse USB-omleiding.</span><span class="sxs-lookup"><span data-stu-id="62aa6-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="62aa6-149">USB-omleiding met Azure RemoteApp wordt alleen ondersteund voor Windows-computers.</span><span class="sxs-lookup"><span data-stu-id="62aa6-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="62aa6-150">USB-omleiding voor RemoteApp-collectie Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="62aa6-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="62aa6-151">Hallo cmdlet tooenable USB-omleiding op niveau van de verzameling Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="62aa6-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="62aa6-152">USB-omleiding voor Hallo client inschakelen</span><span class="sxs-lookup"><span data-stu-id="62aa6-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="62aa6-153">tooconfigure USB-instellingen voor mapomleiding op uw computer:</span><span class="sxs-lookup"><span data-stu-id="62aa6-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="62aa6-154">Open Hallo Editor voor lokaal groepsbeleid (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="62aa6-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="62aa6-155">(Gpedit.msc uitvoeren vanaf een opdrachtprompt.)</span><span class="sxs-lookup"><span data-stu-id="62aa6-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="62aa6-156">Open **Computer Configuration\Policies\Administrative Templates\Windows onderdelen\Extern Desktop Services\Remote bureaubladverbinding Client\RemoteFX USB-apparaatomleiding**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="62aa6-157">Dubbelklik op **toestaan RDP-omleiding van andere ondersteunde RemoteFX USB-apparaten van deze computer**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="62aa6-158">Selecteer **ingeschakeld**, en selecteer vervolgens **beheerders en gebruikers in Hallo RemoteFX USB-omleiding toegangsrechten**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="62aa6-159">Open een opdrachtprompt met beheerdersrechten en Voer Hallo volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="62aa6-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="62aa6-160">Hallo-computer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="62aa6-160">Restart hello computer.</span></span>

<span data-ttu-id="62aa6-161">U kunt ook Hallo Group Policy Management tool toocreate gebruiken en toepassen van Hallo USB-beleid voor omleiding voor alle computers in uw domein:</span><span class="sxs-lookup"><span data-stu-id="62aa6-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="62aa6-162">Meld u aan bij de domeincontroller Hallo als domeinbeheerder Hallo.</span><span class="sxs-lookup"><span data-stu-id="62aa6-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="62aa6-163">Open Hallo Group Policy Management Console.</span><span class="sxs-lookup"><span data-stu-id="62aa6-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="62aa6-164">(Klik op **Start > beheerprogramma's > Groepsbeleidsbeheer**.)</span><span class="sxs-lookup"><span data-stu-id="62aa6-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="62aa6-165">Toohello domein of organisatie-eenheid waarvoor u toocreate Hallo beleid wilt navigeren.</span><span class="sxs-lookup"><span data-stu-id="62aa6-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="62aa6-166">Met de rechtermuisknop op **standaarddomeinbeleid**, en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="62aa6-167">Open **Computer Configuration\Policies\Administrative Templates\Windows onderdelen\Extern Desktop Services\Remote bureaubladverbinding Client\RemoteFX USB-apparaatomleiding**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="62aa6-168">Dubbelklik op **toestaan RDP-omleiding van andere ondersteunde RemoteFX USB-apparaten van deze computer**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="62aa6-169">Selecteer **ingeschakeld**, en selecteer vervolgens **beheerders en gebruikers in Hallo RemoteFX USB-omleiding toegangsrechten**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="62aa6-170">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="62aa6-170">Click **OK**.</span></span>  

