---
title: 'Azure AD Connect: Bijwerken van het SSL-certificaat voor een farm met Active Directory Federation Services (AD FS) | Microsoft Docs'
description: De Documentdetails van dit van de stappen voor het bijwerken van het SSL-certificaat van een AD FS-farm met behulp van Azure AD Connect.
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
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="b7a96-104">Bijwerken van het SSL-certificaat voor een farm met Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="b7a96-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="b7a96-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b7a96-105">Overview</span></span>
<span data-ttu-id="b7a96-106">Dit artikel wordt beschreven hoe u Azure AD Connect kunt gebruiken voor het bijwerken van het SSL-certificaat voor een farm met Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="b7a96-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="b7a96-107">Het hulpprogramma Azure AD Connect kunt u eenvoudig de SSL-certificaat voor de AD FS-farm bijwerken, zelfs als de gebruiker aanmelden methode geselecteerd niet AD FS is.</span><span class="sxs-lookup"><span data-stu-id="b7a96-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="b7a96-108">U kunt de hele bewerking van het SSL-certificaat voor de AD FS-farm bijwerken voor alle federatieve en -servers voor Webtoepassingsproxy (WAP) in drie eenvoudige stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b7a96-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Drie stappen](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="b7a96-110">Zie voor meer informatie over certificaten die worden gebruikt door AD FS, [Understanding-certificaten die worden gebruikt door AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7a96-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a96-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7a96-111">Prerequisites</span></span>

* <span data-ttu-id="b7a96-112">**AD FS-Farm**: Zorg ervoor dat uw AD FS-farm op basis van Windows Server 2012 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b7a96-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="b7a96-113">**Azure AD Connect**: Zorg ervoor dat de versie van Azure AD Connect 1.1.443.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b7a96-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="b7a96-114">Gebruikt u de taak **Update AD FS SSL-certificaat**.</span><span class="sxs-lookup"><span data-stu-id="b7a96-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![SSL-taak bijwerken](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="b7a96-116">Stap 1: Geef informatie op AD FS-farm</span><span class="sxs-lookup"><span data-stu-id="b7a96-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="b7a96-117">Azure AD Connect probeert te verkrijgen van informatie over de AD FS-farm automatisch door:</span><span class="sxs-lookup"><span data-stu-id="b7a96-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="b7a96-118">Opvragen van de Farmgegevens van AD FS (WindowsServer 2016 of hoger).</span><span class="sxs-lookup"><span data-stu-id="b7a96-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="b7a96-119">Verwijst naar de informatie uit de vorige wordt uitgevoerd, die worden lokaal opgeslagen met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b7a96-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="b7a96-120">U kunt de lijst met servers die worden weergegeven door het toevoegen of verwijderen van de servers om de huidige configuratie van de AD FS-farm weer te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b7a96-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="b7a96-121">Zodra de server-informatie is opgegeven, geeft Azure AD Connect de connectiviteit en de huidige status van de SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b7a96-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![AD FS-serverinformatie](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="b7a96-123">Als de lijst een server die niet langer deel uitmaakt van de AD FS-farm bevat, klikt u op **verwijderen** server verwijderen uit de lijst met servers in uw AD FS-farm.</span><span class="sxs-lookup"><span data-stu-id="b7a96-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Offline-server in de lijst](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="b7a96-125">Een server verwijderen uit de lijst met servers voor een AD FS-farm in Azure AD Connect is een lokale bewerking en de gegevens voor de AD FS-farm die lokaal wordt onderhouden door Azure AD Connect-updates.</span><span class="sxs-lookup"><span data-stu-id="b7a96-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="b7a96-126">Azure AD Connect niet de configuratie op de AD FS in overeenstemming met de wijziging niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b7a96-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="b7a96-127">Stap 2: Geef een nieuw SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="b7a96-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="b7a96-128">Nadat u de informatie over AD FS-farm-servers hebt bevestigd, wordt u gevraagd Azure AD Connect voor het nieuwe SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b7a96-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="b7a96-129">Geef een PFX-certificaat wachtwoord om door te gaan met de installatie.</span><span class="sxs-lookup"><span data-stu-id="b7a96-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL-certificaat](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="b7a96-131">Nadat u het certificaat opgeeft, wordt Azure AD Connect gaat door een reeks vereisten.</span><span class="sxs-lookup"><span data-stu-id="b7a96-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="b7a96-132">Controleer of het certificaat om ervoor te zorgen dat het certificaat onjuist voor de AD FS-farm is:</span><span class="sxs-lookup"><span data-stu-id="b7a96-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="b7a96-133">De onderwerpnaam naam/alternatieve onderwerpnaam voor het certificaat is ofwel hetzelfde als de naam van de federation-service of een jokertekencertificaat is.</span><span class="sxs-lookup"><span data-stu-id="b7a96-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="b7a96-134">Het certificaat is geldig voor meer dan 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="b7a96-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="b7a96-135">De vertrouwensketen van het certificaat is geldig.</span><span class="sxs-lookup"><span data-stu-id="b7a96-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="b7a96-136">Het certificaat is beveiligd met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b7a96-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="b7a96-137">Stap 3: Servers voor de update selecteren</span><span class="sxs-lookup"><span data-stu-id="b7a96-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="b7a96-138">Selecteer de servers waarvoor Beveiligingsaanmelding moet het SSL-certificaat dat is bijgewerkt in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="b7a96-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="b7a96-139">Servers die offline zijn, kunnen niet worden geselecteerd voor de update.</span><span class="sxs-lookup"><span data-stu-id="b7a96-139">Servers that are offline can't be selected for the update.</span></span>

![Selecteer servers bijwerken](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="b7a96-141">Na het voltooien van de configuratie wordt het bericht geeft de status van de update en bevat een optie om te controleren of de AD FS-aanmeldingspagina weergegeven in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b7a96-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Configuratie voltooien](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="b7a96-143">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="b7a96-143">FAQs</span></span>

* <span data-ttu-id="b7a96-144">**Wat moet de onderwerpnaam van het certificaat voor de nieuwe AD FS SSL-certificaat?**</span><span class="sxs-lookup"><span data-stu-id="b7a96-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="b7a96-145">Azure AD Connect wordt gecontroleerd of de naam/alternatieve onderwerpnaam onderwerpnaam van het certificaat de naam van de federation-service bevat.</span><span class="sxs-lookup"><span data-stu-id="b7a96-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="b7a96-146">Bijvoorbeeld, als de naam van uw federation service fs.contoso.com is, moet de onderwerpnaam naam/alternatieve onderwerpnaam fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b7a96-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="b7a96-147">Jokertekens-certificaten worden ook geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="b7a96-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="b7a96-148">**Waarom moet ik voor referenties opnieuw op de pagina WAP-server?**</span><span class="sxs-lookup"><span data-stu-id="b7a96-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="b7a96-149">Als de referenties die u opgeeft voor de verbinding met AD FS-servers niet ook de bevoegdheid voor het beheren van de WAP-servers hebt, vervolgens Azure AD Connect wordt gevraagd om referenties die u Administrator-bevoegdheden op de WAP-servers hebt.</span><span class="sxs-lookup"><span data-stu-id="b7a96-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="b7a96-150">**De server wordt weergegeven als offline. Wat moet ik doen?**</span><span class="sxs-lookup"><span data-stu-id="b7a96-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="b7a96-151">Azure AD Connect kan een bewerking niet uitvoeren als de server offline is.</span><span class="sxs-lookup"><span data-stu-id="b7a96-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="b7a96-152">Als de server deel van de AD FS-farm uitmaakt, controleert u de verbinding met de server.</span><span class="sxs-lookup"><span data-stu-id="b7a96-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="b7a96-153">Nadat u het probleem hebt opgelost, drukt u op het pictogram Vernieuwen om de status in de wizard te werken.</span><span class="sxs-lookup"><span data-stu-id="b7a96-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="b7a96-154">Als de server is onderdeel van de farm eerder, maar nu niet meer bestaat, klikt u op **verwijderen** onderhoudt die Azure AD Connect verwijderen uit de lijst met servers.</span><span class="sxs-lookup"><span data-stu-id="b7a96-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="b7a96-155">De configuratie van de AD FS niet van invloed op de server verwijderen uit de lijst in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b7a96-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="b7a96-156">De taak wordt uitgevoerd als u gebruikmaakt van AD FS in Windows Server 2016 of hoger, de server blijft in de configuratie-instellingen en opnieuw in de volgende keer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b7a96-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="b7a96-157">**Kan ik een subset van mijn webfarmservers bijwerken met de nieuwe SSL-certificaat**</span><span class="sxs-lookup"><span data-stu-id="b7a96-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="b7a96-158">Ja.</span><span class="sxs-lookup"><span data-stu-id="b7a96-158">Yes.</span></span> <span data-ttu-id="b7a96-159">U kunt altijd de taak uitvoeren **SSL-certificaat bijwerken** opnieuw naar de resterende servers bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b7a96-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="b7a96-160">Op de **geselecteerde servers voor het SSL-certificaat updates** pagina kunt u de lijst met servers sorteren op **SSL vervaldatum** eenvoudig toegang tot de servers die nog niet zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b7a96-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="b7a96-161">**Ik heb de server in de vorige uitvoering verwijderd, maar deze nog steeds wordt weergegeven als offline en weergegeven op de pagina met AD FS-Servers. Waarom is de offline-server nog steeds er zelfs nadat ik verwijderd?**</span><span class="sxs-lookup"><span data-stu-id="b7a96-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="b7a96-162">De server verwijderen uit de lijst in Azure AD Connect verwijderen niet in de AD FS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="b7a96-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="b7a96-163">Azure AD Connect verwijst naar AD FS (WindowsServer 2016 of hoger) voor informatie over de farm.</span><span class="sxs-lookup"><span data-stu-id="b7a96-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="b7a96-164">Als de server nog steeds aanwezig zijn in de AD FS-configuratie, wordt het weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="b7a96-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b7a96-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b7a96-165">Next steps</span></span>

- [<span data-ttu-id="b7a96-166">Azure AD Connect en federatie</span><span class="sxs-lookup"><span data-stu-id="b7a96-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="b7a96-167">Active Directory Federation Services-beheer en aanpassingen met Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="b7a96-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
