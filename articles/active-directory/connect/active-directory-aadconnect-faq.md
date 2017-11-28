---
title: 'Azure Active Directory Connect: Veelgestelde vragen - | Microsoft Docs'
description: Deze pagina is Veelgestelde vragen over Azure AD Connect.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="d5df1-103">Veelgestelde vragen over Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="d5df1-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="d5df1-104">Algemene installatie</span><span class="sxs-lookup"><span data-stu-id="d5df1-104">General installation</span></span>
<span data-ttu-id="d5df1-105">**V: installatie werkt als hello Azure AD met globale beheerder 2FA ingeschakeld heeft?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="d5df1-106">Met de Hallo builds van februari 2016, wordt dit ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d5df1-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="d5df1-107">**V: is er een manier tooinstall Azure AD Connect zonder toezicht?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="d5df1-108">Alleen ondersteunde tooinstall Azure AD Connect is Hallo-installatiewizard gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5df1-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="d5df1-109">Een installatie zonder toezicht en de achtergrond wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d5df1-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="d5df1-110">**V: ik heb een forest waar één domein is niet bereikbaar. Hoe kan ik Azure AD Connect installeren?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="d5df1-111">Met de Hallo builds van februari 2016, wordt dit ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d5df1-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="d5df1-112">**V: Hallo AD DS health agent werkt op server core?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="d5df1-113">Ja.</span><span class="sxs-lookup"><span data-stu-id="d5df1-113">Yes.</span></span> <span data-ttu-id="d5df1-114">Nadat Hallo-agent is geïnstalleerd, kunt u Hallo registratieproces met behulp van de volgende PowerShell-cmdlet Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="d5df1-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="d5df1-115">Netwerk</span><span class="sxs-lookup"><span data-stu-id="d5df1-115">Network</span></span>
<span data-ttu-id="d5df1-116">**V: ik heb een firewall, netwerkapparaat of iets anders dat Hallo maximumtijd verbindingen beperkt geopend op mijn netwerk kunt blijven. Hoe lang mijn client side time-out drempelwaarde moet bij gebruik van Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="d5df1-117">Alle netwerksoftware, fysieke apparaten of iets anders dat limieten Hallo maximumtijd verbindingen kunnen open blijven een drempel van minstens 5 minuten (300 seconden) voor de verbinding tussen gebruiken moet Hallo server waarop hello Azure AD Connect-client is geïnstalleerd en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5df1-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="d5df1-118">Dit geldt ook hulpprogramma's voor eerder uitgebrachte tooall Microsoft Identity synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="d5df1-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="d5df1-119">**V: zijn niveaudomeinen (één Label domeinen) ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="d5df1-120">Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen met behulp van niveaudomeinen.</span><span class="sxs-lookup"><span data-stu-id="d5df1-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="d5df1-121">**V: zijn 'scheidingspunten' NetBios-naam ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="d5df1-122">Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen waar Hallo NetBIOS-naam een punt bevat '. ' Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="d5df1-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="d5df1-123">Federation</span><span class="sxs-lookup"><span data-stu-id="d5df1-123">Federation</span></span>
<span data-ttu-id="d5df1-124">**V: wat moet ik doen als ik een e-mailbericht ontvangen die vragen toorenew mijn Office 365-certificaat**</span><span class="sxs-lookup"><span data-stu-id="d5df1-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="d5df1-125">Gebruik Hallo richtlijnen die wordt beschreven in Hallo [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md) onderwerp op hoe toorenew Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="d5df1-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="d5df1-126">**V: ik heb 'Automatisch bijwerken relying party' instellen voor de relying party O365. Heb ik tootake geen acties als mijn voor token-ondertekening certificaat automatisch boven?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="d5df1-127">Gebruik Hallo richtlijnen die wordt beschreven in artikel Hallo [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="d5df1-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="d5df1-128">Omgeving</span><span class="sxs-lookup"><span data-stu-id="d5df1-128">Environment</span></span>
<span data-ttu-id="d5df1-129">**V: is it ondersteund toorename Hallo server nadat Azure AD Connect is geïnstalleerd?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="d5df1-130">Nee.</span><span class="sxs-lookup"><span data-stu-id="d5df1-130">No.</span></span> <span data-ttu-id="d5df1-131">Hallo-servernaam wijzigen oorzaak Hallo sync engine toonot worden kunnen tooconnect toohello SQL-database en Hallo service toostart kunnen niet worden.</span><span class="sxs-lookup"><span data-stu-id="d5df1-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="d5df1-132">Id-gegevens</span><span class="sxs-lookup"><span data-stu-id="d5df1-132">Identity data</span></span>
<span data-ttu-id="d5df1-133">**V: Hallo UPN (userPrincipalName)-kenmerk in Azure AD komt niet overeen met on-premises UPN - waarom Hallo?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="d5df1-134">Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="d5df1-134">See these articles:</span></span>

* [<span data-ttu-id="d5df1-135">Gebruikersnamen in Office 365, Azure of Intune komen niet overeen Hallo lokale UPN of alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="d5df1-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="d5df1-136">Wijzigingen zijn niet gesynchroniseerd door hello Azure Active Directory-synchronisatie nadat u Hallo UPN van een gebruiker account toouse een ander federatieve domein wijzigen</span><span class="sxs-lookup"><span data-stu-id="d5df1-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="d5df1-137">U kunt ook Azure AD tooallow Hallo sync engine tooupdate Hallo userPrincipalName configureren zoals beschreven in [functies van de service Azure AD Connect-synchronisatie](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="d5df1-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="d5df1-138">**V: is it ondersteund toosoft overeen lokale AD-groep/Contact-objecten met bestaande Azure AD-groep/Contact objecten?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="d5df1-139">Nee, dit wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d5df1-139">No, this is currently not supported.</span></span>

<span data-ttu-id="d5df1-140">**V: is it ondersteund toomanually onveranderbare id genoemd-kenmerk ingesteld op bestaande Azure AD-groep/contactpersoon objecten toohard hieraan tooon-premises AD-groep/Contact objecten?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="d5df1-141">Nee, dit wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d5df1-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="d5df1-142">Aangepaste configuratie</span><span class="sxs-lookup"><span data-stu-id="d5df1-142">Custom configuration</span></span>
<span data-ttu-id="d5df1-143">**V: waar zijn Hallo PowerShell-cmdlets voor Azure AD Connect beschreven?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="d5df1-144">Hallo, met uitzondering van Hallo-cmdlets beschreven op deze site worden andere gevonden in Azure AD Connect PowerShell-cmdlets niet ondersteund voor gebruik van de klant.</span><span class="sxs-lookup"><span data-stu-id="d5df1-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="d5df1-145">**V: kan ik gebruiken 'Server exportserver/importeren' gevonden in *Synchronization Service Manager* toomove configuratie tussen servers?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="d5df1-146">Nee.</span><span class="sxs-lookup"><span data-stu-id="d5df1-146">No.</span></span> <span data-ttu-id="d5df1-147">Deze optie worden alle configuratie-instellingen niet ophalen en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5df1-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="d5df1-148">U moet in plaats daarvan Hallo wizard toocreate Hallo basisconfiguratie op Hallo tweede server gebruiken en Hallo sync regel editor toogenerate PowerShell-scripts toomove een aangepaste regel tussen servers.</span><span class="sxs-lookup"><span data-stu-id="d5df1-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="d5df1-149">Zie [migratie bewegen](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="d5df1-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="d5df1-150">**V: kunnen wachtwoorden worden opgeslagen in de cache voor de pagina hello Azure aanmelden en kan dit worden voorkomen omdat het een wachtwoord invoerelement met Hallo automatisch aanvullen bevat = 'false' kenmerk?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="d5df1-151">Wordt momenteel niet ondersteund wijzigen Hallo HTML-kenmerken van het Hallo wachtwoord invoerveld, met inbegrip van Hallo automatisch aanvullen label.</span><span class="sxs-lookup"><span data-stu-id="d5df1-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="d5df1-152">We zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u tooadd elk kenmerkveld toohello-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d5df1-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="d5df1-153">Dit moet deel uitmaken beschikbaar hoger van 2017.</span><span class="sxs-lookup"><span data-stu-id="d5df1-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="d5df1-154">**V: op Hallo Azure-aanmeldingspagina, worden gebruikersnamen voor gebruikers die zich eerder hebt geregistreerd in met succes weergegeven.  U kunt dit gedrag uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="d5df1-155">Wordt momenteel niet ondersteund wijzigen Hallo HTML-kenmerken van de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5df1-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="d5df1-156">We zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u tooadd elk kenmerkveld toohello-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d5df1-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="d5df1-157">Dit moet deel uitmaken beschikbaar hoger van 2017.</span><span class="sxs-lookup"><span data-stu-id="d5df1-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="d5df1-158">**V: is er een manier tooprevent gelijktijdige sessies?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="d5df1-159">Nee.</span><span class="sxs-lookup"><span data-stu-id="d5df1-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="d5df1-160">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d5df1-160">Troubleshooting</span></span>
<span data-ttu-id="d5df1-161">**V: hoe vind ik meer informatie over Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d5df1-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="d5df1-162">Zoek Hallo Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="d5df1-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="d5df1-163">Zoek Hallo Microsoft Knowledge Base (KB) voor technische oplossingen toocommon schadevergoedings problemen over ondersteuning voor Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d5df1-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="d5df1-164">Microsoft Azure Active Directory-Forums</span><span class="sxs-lookup"><span data-stu-id="d5df1-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="d5df1-165">U kunt zoeken en bladeren voor technische vragen en uit Hallo community antwoorden of uw eigen vraag door te klikken op [hier](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="d5df1-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="d5df1-166">Ondersteuning van de klant Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d5df1-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="d5df1-167">Gebruik deze koppeling tooget ondersteuning via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5df1-167">Use this link tooget support through hello Azure portal.</span></span>

