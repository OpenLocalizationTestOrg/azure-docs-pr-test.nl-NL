---
title: 'Azure AD Connect: Hallo SSL-certificaat bijwerken voor een farm met Active Directory Federation Services (AD FS) | Microsoft Docs'
description: Dit document details Hallo stappen tooupdate Hallo SSL-certificaat van een AD FS-farm met behulp van Azure AD Connect.
services: active-directory
keywords: Azure ad connect, AD FS ssl-update, adfs-certificaat updates, AD FS-certificaat wijzigen, nieuwe AD FS-certificaat, AD FS-certificaat, update AD FS ssl-certificaat en update ssl-certificaat adfs AD FS ssl-certificaat, AD FS, ssl, certificaat, AD FS-service configureren certificaat voor serviceberichten, update-federation, federatie configureren, aad connect
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="a6ead-104">Hallo SSL-certificaat voor een farm met Active Directory Federation Services (AD FS) bijwerken</span><span class="sxs-lookup"><span data-stu-id="a6ead-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="a6ead-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a6ead-105">Overview</span></span>
<span data-ttu-id="a6ead-106">Dit artikel wordt beschreven hoe u Azure AD Connect tooupdate Hallo SSL-certificaat voor een farm met Active Directory Federation Services (AD FS) kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6ead-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="a6ead-107">Zelfs als Hallo gebruiker aanmelden methode geselecteerd geen AD FS is, kunt u hello Azure AD Connect-hulpprogramma tooeasily update Hallo SSL-certificaat voor Hallo AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="a6ead-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="a6ead-108">U kunt de hele bewerking hello om SSL-certificaat voor Hallo AD FS-farm bij te werken voor alle federatieve en -servers voor Webtoepassingsproxy (WAP) in drie eenvoudige stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a6ead-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Drie stappen](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="a6ead-110">toolearn meer informatie over de certificaten die worden gebruikt door AD FS, Zie [Understanding-certificaten die worden gebruikt door AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6ead-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6ead-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a6ead-111">Prerequisites</span></span>

* <span data-ttu-id="a6ead-112">**AD FS-Farm**: Zorg ervoor dat uw AD FS-farm op basis van Windows Server 2012 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a6ead-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="a6ead-113">**Azure AD Connect**: Zorg ervoor dat Hallo versie van Azure AD Connect is 1.1.443.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a6ead-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="a6ead-114">U Hallo taak **Update AD FS SSL-certificaat**.</span><span class="sxs-lookup"><span data-stu-id="a6ead-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![SSL-taak bijwerken](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="a6ead-116">Stap 1: Geef informatie op AD FS-farm</span><span class="sxs-lookup"><span data-stu-id="a6ead-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="a6ead-117">Azure AD Connect probeert automatisch door tooobtain informatie over Hallo AD FS-farm:</span><span class="sxs-lookup"><span data-stu-id="a6ead-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="a6ead-118">Het uitvoeren van query's is Hallo Farmgegevens vanaf AD FS (WindowsServer 2016 of hoger).</span><span class="sxs-lookup"><span data-stu-id="a6ead-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="a6ead-119">Verwijzende Hallo-informatie uit de vorige wordt uitgevoerd, worden lokaal opgeslagen met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a6ead-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="a6ead-120">U kunt Hallo lijst met servers die worden weergegeven door het toevoegen of verwijderen van Hallo servers tooreflect Hallo huidige configuratie van Hallo AD FS-farm kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a6ead-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="a6ead-121">Zodra het Hallo-servergegevens is opgegeven, geeft Azure AD Connect Hallo connectiviteit en de huidige status van de SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="a6ead-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![AD FS-serverinformatie](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="a6ead-123">Als het Hallo-lijst bevat een server die niet langer deel uitmaakt van Hallo AD FS-farm, klikt u op **verwijderen** toodelete Hallo-server in de lijst Hallo van servers in uw AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="a6ead-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Offline-server in de lijst](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="a6ead-125">Een server verwijderen uit lijst Hallo van servers voor een AD FS-farm in Azure AD Connect is een lokale bewerking en updates Hallo-informatie voor Hallo AD FS-farm die lokaal wordt onderhouden door Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a6ead-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="a6ead-126">Azure AD Connect wijzigen niet Hallo configuratie van AD FS tooreflect Hallo wijziging.</span><span class="sxs-lookup"><span data-stu-id="a6ead-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="a6ead-127">Stap 2: Geef een nieuw SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="a6ead-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="a6ead-128">Nadat u hebt bevestigd Hallo informatie over AD FS-farm-servers, wordt u gevraagd Azure AD Connect voor Hallo nieuwe SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="a6ead-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="a6ead-129">Geef een wachtwoord beveiligde PFX toocontinue Hallo installatie van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="a6ead-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![SSL-certificaat](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="a6ead-131">Nadat u Hallo certificaat opgeeft, wordt Azure AD Connect gaat door een reeks vereisten.</span><span class="sxs-lookup"><span data-stu-id="a6ead-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="a6ead-132">Controleer of Hallo certificaat tooensure dat certificaat Hallo klopt voor Hallo AD FS-farm:</span><span class="sxs-lookup"><span data-stu-id="a6ead-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="a6ead-133">Hallo is onderwerp naam/alternatieve onderwerpnaam voor Hallo-certificaat dezelfde als de federatieve-servicenaam Hallo Hallo, of een jokertekencertificaat is.</span><span class="sxs-lookup"><span data-stu-id="a6ead-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="a6ead-134">Hallo-certificaat is geldig voor meer dan 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="a6ead-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="a6ead-135">vertrouwensketen Hallo-certificaat is geldig.</span><span class="sxs-lookup"><span data-stu-id="a6ead-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="a6ead-136">Hallo-certificaat is beveiligd met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a6ead-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="a6ead-137">Stap 3: Servers voor Hallo update selecteren</span><span class="sxs-lookup"><span data-stu-id="a6ead-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="a6ead-138">Selecteer in de volgende stap Hallo Hallo-servers die SSL-certificaat voor toohave Hallo is bijgewerkt moeten.</span><span class="sxs-lookup"><span data-stu-id="a6ead-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="a6ead-139">Servers die offline zijn, kunnen niet worden geselecteerd voor Hallo-update.</span><span class="sxs-lookup"><span data-stu-id="a6ead-139">Servers that are offline can't be selected for hello update.</span></span>

![Selecteer servers tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="a6ead-141">Nadat u Hallo configuratie hebt voltooid, geeft Azure AD Connect Hallo-bericht dat geeft de status Hallo van Hallo update en biedt een optie tooverify Hallo AD FS aanmelden.</span><span class="sxs-lookup"><span data-stu-id="a6ead-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Configuratie voltooien](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="a6ead-143">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a6ead-143">FAQs</span></span>

* <span data-ttu-id="a6ead-144">**Wat moet Hallo naam van Hallo-certificaat voor de nieuwe AD FS SSL-certificaat Hallo?**</span><span class="sxs-lookup"><span data-stu-id="a6ead-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="a6ead-145">Azure AD Connect wordt gecontroleerd of Hallo onderwerp naam/alternatieve naam van certificaat Hallo Hallo federatieve-servicenaam bevat.</span><span class="sxs-lookup"><span data-stu-id="a6ead-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="a6ead-146">Bijvoorbeeld, als de naam van uw federation service fs.contoso.com is, moet Hallo onderwerp naam/alternatieve onderwerpnaam fs.contoso.com.  Jokertekens-certificaten worden ook geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="a6ead-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="a6ead-147">**Waarom moet ik voor referenties opnieuw op pagina Hallo WAP-server?**</span><span class="sxs-lookup"><span data-stu-id="a6ead-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="a6ead-148">Als Hallo-referenties die u opgeeft voor het verbinden van tooAD FS-servers niet ook Hallo bevoegdheid toomanage Hallo WAP-servers hebt, klikt u vervolgens Azure AD Connect wordt gevraagd om referenties die u Administrator-bevoegdheden op Hallo WAP-servers hebt.</span><span class="sxs-lookup"><span data-stu-id="a6ead-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="a6ead-149">**Hallo-server wordt weergegeven als offline. Wat moet ik doen?**</span><span class="sxs-lookup"><span data-stu-id="a6ead-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="a6ead-150">Azure AD Connect kan een bewerking niet uitvoeren als Hallo server offline is.</span><span class="sxs-lookup"><span data-stu-id="a6ead-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="a6ead-151">Als Hallo server deel van Hallo AD FS-farm uitmaakt, moet u Hallo connectiviteit toohello server controleren.</span><span class="sxs-lookup"><span data-stu-id="a6ead-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="a6ead-152">Nadat u Hallo probleem hebt opgelost, drukt u op Hallo pictogram tooupdate hello vernieuwingsstatus in Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="a6ead-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="a6ead-153">Als Hallo server deel uitmaakte van Hallo farm eerder, maar nu niet meer bestaat, klikt u op **verwijderen** toodelete uit Hallo lijst met servers die Azure AD Connect houdt.</span><span class="sxs-lookup"><span data-stu-id="a6ead-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="a6ead-154">Verwijderen Hallo-server in de lijst Hallo in Azure AD Connect Hallo AD FS-configuratie zelf wordt niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a6ead-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="a6ead-155">Als u gebruikmaakt van AD FS in Windows Server 2016 of hoger, Hallo server blijft in Hallo configuratie-instellingen en worden weergegeven wordt opnieuw hello zodra hello taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6ead-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="a6ead-156">**Kan ik een subset van mijn webfarmservers met Hallo nieuwe SSL-certificaat bijwerken?**</span><span class="sxs-lookup"><span data-stu-id="a6ead-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="a6ead-157">Ja.</span><span class="sxs-lookup"><span data-stu-id="a6ead-157">Yes.</span></span> <span data-ttu-id="a6ead-158">U kunt altijd Hallo taak uitvoeren **SSL-certificaat bijwerken** opnieuw tooupdate Hallo resterende servers.</span><span class="sxs-lookup"><span data-stu-id="a6ead-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="a6ead-159">Op Hallo **geselecteerde servers voor het SSL-certificaat updates** pagina kunt u Hallo lijst met servers sorteren op **SSL vervaldatum** tooeasily-Hallo servers die nog niet zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a6ead-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="a6ead-160">**Ik Hallo-server in de vorige Hallo uitgevoerd verwijderd, maar deze wordt nog steeds wordt weergegeven als offline en vermelde op Hallo AD FS-Servers pagina. Waarom is Hallo offline server nog steeds er zelfs nadat ik verwijderd?**</span><span class="sxs-lookup"><span data-stu-id="a6ead-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="a6ead-161">Verwijderen Hallo-server in de lijst Hallo in Azure AD Connect verwijderen niet in Hallo AD FS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="a6ead-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="a6ead-162">Azure AD Connect verwijst naar AD FS (WindowsServer 2016 of hoger) voor informatie over het Hallo-farm.</span><span class="sxs-lookup"><span data-stu-id="a6ead-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="a6ead-163">Als het Hallo-server nog steeds aanwezig zijn in Hallo AD FS-configuratie, wordt het weergegeven terug in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6ead-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a6ead-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6ead-164">Next steps</span></span>

- [<span data-ttu-id="a6ead-165">Azure AD Connect en federatie</span><span class="sxs-lookup"><span data-stu-id="a6ead-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="a6ead-166">Active Directory Federation Services-beheer en aanpassingen met Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a6ead-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
