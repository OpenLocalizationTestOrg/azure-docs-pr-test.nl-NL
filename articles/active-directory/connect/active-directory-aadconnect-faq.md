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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="15ecb-103">Veelgestelde vragen over Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="15ecb-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="15ecb-104">Algemene installatie</span><span class="sxs-lookup"><span data-stu-id="15ecb-104">General installation</span></span>
<span data-ttu-id="15ecb-105">**V: installatie werkt als de globale beheerder van Azure AD 2FA ingeschakeld heeft?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="15ecb-106">Met de opbouw van februari 2016, wordt dit ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ecb-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="15ecb-107">**V: is er een manier voor het installeren van Azure AD Connect zonder toezicht?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="15ecb-108">Alleen wordt ondersteund voor het installeren van Azure AD Connect met de installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="15ecb-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="15ecb-109">Een installatie zonder toezicht en de achtergrond wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ecb-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="15ecb-110">**V: ik heb een forest waar één domein is niet bereikbaar. Hoe kan ik Azure AD Connect installeren?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="15ecb-111">Met de opbouw van februari 2016, wordt dit ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ecb-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="15ecb-112">**V: de health-agent voor AD DS werkt op server core?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="15ecb-113">Ja.</span><span class="sxs-lookup"><span data-stu-id="15ecb-113">Yes.</span></span> <span data-ttu-id="15ecb-114">Nadat de agent is geïnstalleerd, kunt u het registratieproces met de volgende PowerShell-cmdlet uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="15ecb-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="15ecb-115">Netwerk</span><span class="sxs-lookup"><span data-stu-id="15ecb-115">Network</span></span>
<span data-ttu-id="15ecb-116">**V: ik heb een firewall, netwerkapparaat of iets anders dat de maximale tijd verbindingen beperkt geopend op mijn netwerk kunt blijven. Hoe lang mijn client side time-out drempelwaarde moet bij gebruik van Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="15ecb-117">Alle netwerksoftware, fysieke apparaten of iets anders dat de maximale tijd verbindingen kunnen open blijven beperkt moet een drempel van minstens 5 minuten (300 seconden) gebruiken voor verbindingen tussen de server waarop de Azure AD Connect-client is geïnstalleerd en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15ecb-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="15ecb-118">Dit geldt ook voor alle eerder uitgebrachte Microsoft Identity hulpprogramma's voor synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="15ecb-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="15ecb-119">**V: zijn niveaudomeinen (één Label domeinen) ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="15ecb-120">Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen met behulp van niveaudomeinen.</span><span class="sxs-lookup"><span data-stu-id="15ecb-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="15ecb-121">**V: zijn 'scheidingspunten' NetBios-naam ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="15ecb-122">Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen waar de NetBios-naam een punt bevat '. ' in de naam.</span><span class="sxs-lookup"><span data-stu-id="15ecb-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="15ecb-123">Federation</span><span class="sxs-lookup"><span data-stu-id="15ecb-123">Federation</span></span>
<span data-ttu-id="15ecb-124">**V: wat moet ik doen als ik een e-mailbericht ontvangen die vragen om mijn Office 365-certificaat te vernieuwen**</span><span class="sxs-lookup"><span data-stu-id="15ecb-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="15ecb-125">Gebruik de richtlijnen die wordt beschreven in de [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md) onderwerp over het vernieuwen van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="15ecb-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="15ecb-126">**V: ik heb 'Automatisch bijwerken relying party' instellen voor de relying party O365. Heb ik geen actie te ondernemen als mijn voor token-ondertekening certificaat automatisch boven?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="15ecb-127">Gebruik de richtlijnen die wordt beschreven in het artikel [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="15ecb-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="15ecb-128">Omgeving</span><span class="sxs-lookup"><span data-stu-id="15ecb-128">Environment</span></span>
<span data-ttu-id="15ecb-129">**V: is dit dan ondersteund als u wilt wijzigen van de server nadat Azure AD Connect is geïnstalleerd?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="15ecb-130">Nee.</span><span class="sxs-lookup"><span data-stu-id="15ecb-130">No.</span></span> <span data-ttu-id="15ecb-131">Naam van de server wijzigt, worden de synchronisatie-engine niet mogelijk om te verbinden met de SQL-database en de service kan niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="15ecb-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="15ecb-132">Id-gegevens</span><span class="sxs-lookup"><span data-stu-id="15ecb-132">Identity data</span></span>
<span data-ttu-id="15ecb-133">**V: in Azure AD-de UPN (userPrincipalName)-kenmerk niet overeenkomt met de on-premises UPN - waarom?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="15ecb-134">Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="15ecb-134">See these articles:</span></span>

* [<span data-ttu-id="15ecb-135">Gebruikersnamen in Office 365, Azure of Intune komen niet overeen met de lokale UPN of de alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="15ecb-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="15ecb-136">Wijzigingen zijn niet gesynchroniseerd door de Azure Active Directory-synchronisatie nadat u de UPN van een gebruikersaccount voor het gebruik van een ander federatieve domein wijzigen</span><span class="sxs-lookup"><span data-stu-id="15ecb-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="15ecb-137">U kunt ook configureren met Azure AD, zodat de synchronisatie-engine de userPrincipalName bijwerken zoals beschreven in [functies van de service Azure AD Connect-synchronisatie](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="15ecb-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="15ecb-138">**V: is het ondersteund op zachte overeenkomst met lokale AD-groep/Contact objecten met bestaande Azure AD-groep/Contact objecten?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="15ecb-139">Nee, dit wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ecb-139">No, this is currently not supported.</span></span>

<span data-ttu-id="15ecb-140">**V: is het handmatig instellen ondersteund onveranderbare id genoemd-kenmerk op bestaande Azure AD-groep/Contact objecten hard overeenkomen met het lokale AD-groep/Contact objecten?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="15ecb-141">Nee, dit wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ecb-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="15ecb-142">Aangepaste configuratie</span><span class="sxs-lookup"><span data-stu-id="15ecb-142">Custom configuration</span></span>
<span data-ttu-id="15ecb-143">**V: waar zijn de PowerShell-cmdlets voor Azure AD Connect beschreven?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="15ecb-144">Met uitzondering van de cmdlets beschreven op deze site, worden andere gevonden in Azure AD Connect PowerShell-cmdlets worden niet ondersteund voor gebruik van de klant.</span><span class="sxs-lookup"><span data-stu-id="15ecb-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="15ecb-145">**V: kan ik gebruiken 'Server exportserver/importeren' gevonden in *Synchronization Service Manager* configuratie verplaatsen tussen servers?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="15ecb-146">Nee.</span><span class="sxs-lookup"><span data-stu-id="15ecb-146">No.</span></span> <span data-ttu-id="15ecb-147">Deze optie worden alle configuratie-instellingen niet ophalen en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15ecb-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="15ecb-148">In plaats daarvan moet u de wizard gebruiken voor het maken van de basisconfiguratie op de tweede server en de regeleditor sync gebruiken voor het genereren van PowerShell-scripts voor het verplaatsen van een aangepaste regel tussen servers.</span><span class="sxs-lookup"><span data-stu-id="15ecb-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="15ecb-149">Zie [migratie bewegen](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="15ecb-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="15ecb-150">**V: kunnen wachtwoorden worden opgeslagen voor de Azure-aanmeldingspagina en kan dit worden voorkomen omdat het een wachtwoord invoerelement met automatisch aanvullen bevat = 'false' kenmerk?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="15ecb-151">Wordt momenteel niet ondersteund voor het wijzigen van de HTML-kenmerken van het invoerveld wachtwoord, met inbegrip van de tag automatisch aanvullen.</span><span class="sxs-lookup"><span data-stu-id="15ecb-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="15ecb-152">Er zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u een kenmerk toevoegen aan het wachtwoordveld.</span><span class="sxs-lookup"><span data-stu-id="15ecb-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="15ecb-153">Dit moet deel uitmaken beschikbaar hoger van 2017.</span><span class="sxs-lookup"><span data-stu-id="15ecb-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="15ecb-154">**V: op de Azure-aanmeldingspagina, worden gebruikersnamen voor gebruikers die zich eerder hebt geregistreerd in met succes weergegeven.  U kunt dit gedrag uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="15ecb-155">Wordt momenteel niet ondersteund voor het wijzigen van de HTML-kenmerken van de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="15ecb-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="15ecb-156">Er zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u een kenmerk toevoegen aan het wachtwoordveld.</span><span class="sxs-lookup"><span data-stu-id="15ecb-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="15ecb-157">Dit moet deel uitmaken beschikbaar hoger van 2017.</span><span class="sxs-lookup"><span data-stu-id="15ecb-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="15ecb-158">**V: is er een manier om te voorkomen dat gelijktijdige sessies?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="15ecb-159">Nee.</span><span class="sxs-lookup"><span data-stu-id="15ecb-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="15ecb-160">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="15ecb-160">Troubleshooting</span></span>
<span data-ttu-id="15ecb-161">**V: hoe vind ik meer informatie over Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="15ecb-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="15ecb-162">Zoeken in de Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="15ecb-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="15ecb-163">Zoek in de Microsoft Knowledge Base (KB) voor technische oplossingen voor problemen schadevergoedings over ondersteuning voor Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="15ecb-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="15ecb-164">Microsoft Azure Active Directory-Forums</span><span class="sxs-lookup"><span data-stu-id="15ecb-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="15ecb-165">U kunt zoeken en bladeren voor technische vragen en van de community antwoorden of uw eigen vraag door te klikken op [hier](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="15ecb-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="15ecb-166">Ondersteuning van de klant Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="15ecb-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="15ecb-167">Gebruik deze koppeling om ondersteuning te krijgen via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15ecb-167">Use this link to get support through the Azure portal.</span></span>

