---
title: Azure Active Directory automatische apparaatregistratie Veelgestelde vragen | Microsoft Docs
description: Automatische apparaatregistratie met Azure Active Directory-Veelgestelde vragen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="8bfd2-103">Veelgestelde vragen over de automatische apparaatregistratie van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bfd2-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="8bfd2-104">**V: ik het apparaat onlangs geregistreerd. Waarom zie ik het apparaat niet onder Mijn gebruikersgegevens in de Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="8bfd2-105">**A:** Windows 10-apparaten die lid van een domein met automatische apparaatregistratie zijn worden niet weergegeven onder de gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="8bfd2-106">U moet PowerShell gebruiken voor alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="8bfd2-107">Alleen de volgende apparaten worden vermeld in de gegevens van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="8bfd2-108">Alle persoonlijke apparaten die niet lid enterprise</span><span class="sxs-lookup"><span data-stu-id="8bfd2-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="8bfd2-109">Alle niet - Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8bfd2-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="8bfd2-110">Alle niet-Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="8bfd2-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="8bfd2-111">**V: Waarom kan ik de apparaten die zijn geregistreerd bij Azure Active Directory in de Azure portal niet zien?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="8bfd2-112">**A:** er is momenteel geen manier om te zien alle geregistreerde apparaten in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="8bfd2-113">Azure PowerShell kunt u alle apparaten zoeken.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="8bfd2-114">Zie voor meer informatie de [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="8bfd2-115">**V: hoe weet wat de status van het apparaat registratie van de client is?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="8bfd2-116">**A:** afhankelijk van de status van het apparaat registratie:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="8bfd2-117">Wat het apparaat is</span><span class="sxs-lookup"><span data-stu-id="8bfd2-117">What the device is</span></span>
- <span data-ttu-id="8bfd2-118">Hoe het is geregistreerd</span><span class="sxs-lookup"><span data-stu-id="8bfd2-118">How it was registered</span></span> 
- <span data-ttu-id="8bfd2-119">Gerelateerde details.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="8bfd2-120">**V: Waarom is een apparaat ik hebt verwijderd in de Azure portal of met Windows PowerShell nog steeds vermeld als geregistreerd?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="8bfd2-121">**A:** dit is standaard.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-121">**A:** This is by design.</span></span> <span data-ttu-id="8bfd2-122">Het apparaat geen toegang tot bronnen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="8bfd2-123">Als u wilt dat het apparaat te verwijderen en opnieuw te registreren, moet een handmatige actie moet worden uitgevoerd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="8bfd2-124">Voor Windows 10 en Windows Server 2016 met on-premises AD-domein:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="8bfd2-125">Open de opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="8bfd2-126">Type`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="8bfd2-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="8bfd2-127">Meld u af en meld u aan voor het activeren van de geplande taak die het apparaat opnieuw wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="8bfd2-128">Voor andere Windows-platforms die zich on-premises AD-domein:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="8bfd2-129">Open de opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="8bfd2-130">Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="8bfd2-131">Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="8bfd2-132">**V: Waarom zie ik dubbele apparaatvermeldingen in Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="8bfd2-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-133">**A:**</span></span>

-   <span data-ttu-id="8bfd2-134">Voor Windows 10 en Windows Server 2016 als ze herhaalde pogingen tot het loskoppelen van en opnieuw aanmelden voor hetzelfde apparaat, kunnen er dubbele vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="8bfd2-135">Als u toevoegen werk of School-Account hebt gebruikt, wordt elke windows-gebruiker die voegen werk- of Schoolaccount gebruikt een nieuwe apparaatrecord maken met dezelfde naam van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="8bfd2-136">Andere Windows-platforms die zich on-premises AD-domein met behulp van automatische registratie maakt een nieuwe record van apparaat met dezelfde naam voor elke domeingebruiker die zich bij het apparaat aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="8bfd2-137">Een AADJ-machine die is gewist, opnieuw geïnstalleerd en opnieuw toegevoegd met dezelfde naam wordt weergegeven als een andere record met dezelfde naam van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="8bfd2-138">**V: waarom een gebruiker nog steeds toegang tot bronnen vanaf een apparaat dat ik hebt uitgeschakeld in de Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="8bfd2-139">**A:** kan duren tot een uur voor een intrekken moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="8bfd2-140">Verloren apparaten, wordt u aangeraden het apparaat om ervoor te zorgen dat gebruikers geen toegang het apparaat tot wissen.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="8bfd2-141">Zie voor meer informatie [apparaten inschrijven voor beheer in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="8bfd2-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="8bfd2-142">**V: Waarom kunnen mijn gebruikers zien 'U geen toegang vanaf hier'?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="8bfd2-143">**A:** als u bepaalde regels voor voorwaardelijke toegang om ervoor te zorgen, de status van een specifiek apparaat hebt geconfigureerd en het apparaat niet aan de criteria voldoet, gebruikers worden geblokkeerd en dit bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="8bfd2-144">De regels evalueren en zorg ervoor dat het apparaat kunnen voldoen aan de criteria om te voorkomen dat dit bericht.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="8bfd2-145">**V: ik Zie apparaatrecord onder de gebruikersgegevens in de Azure portal en de status kunt zien, zoals die is geregistreerd op de client. Kan dat ik een correct instellen voor het gebruik van voorwaardelijke toegang?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="8bfd2-146">**A:** de record van apparaat (deviceID) en de status op de Azure-portal moeten overeenkomen met de client en voldoen aan de evaluatiecriteria van een voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="8bfd2-147">Zie voor meer informatie [aan de slag met Azure Active Directory-apparaatregistratie](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8bfd2-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="8bfd2-148">**V: Waarom krijg ik een bericht 'gebruikersnaam of wachtwoord is onjuist' voor een apparaat dat ik zojuist hebt toegevoegd aan Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="8bfd2-149">**A:** veelvoorkomende redenen voor dit scenario zijn:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="8bfd2-150">Uw referenties zijn niet langer geldig.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="8bfd2-151">Uw computer staat kan niet communiceren met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="8bfd2-152">Controleer of eventuele problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="8bfd2-153">Azure AD Join aan de vereisten is niet voldaan aan.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="8bfd2-154">Zorg ervoor dat u de stappen hebt gevolgd [cloudfuncties uitbreiden naar Windows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bfd2-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="8bfd2-155">Federatieve aanmeldingen vereist uw federatieserver ter ondersteuning van een actieve WS-Trust-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="8bfd2-156">**V: Waarom zie ik de "... Oops is een fout opgetreden!" dialoogvenster wanneer ik probeer mijn PC toevoegen?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="8bfd2-157">**A:** dit is een resultaat van het instellen van Azure Active Directory-inschrijving met Intune.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="8bfd2-158">Zie voor meer informatie [Windows Apparaatbeheer instellen](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="8bfd2-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="8bfd2-159">**V: waarom niet mijn poging om te nemen van een PC maar ik heb informatie over de fout niet ontvangen?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="8bfd2-160">**A:** een waarschijnlijke oorzaak is dat de gebruiker is aangemeld bij het apparaat met het ingebouwde administratoraccount.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="8bfd2-161">Maak een andere lokale account voordat u Azure Active Directory Join gebruikt om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8bfd2-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="8bfd2-162">**V: waar vind ik instructies voor het instellen van automatische apparaatregistratie**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="8bfd2-163">**A:** Zie voor gedetailleerde instructies [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="8bfd2-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="8bfd2-164">**V: waar vind ik het oplossen van informatie over de automatische apparaatregistratie?**</span><span class="sxs-lookup"><span data-stu-id="8bfd2-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="8bfd2-165">**A:** voor informatie over probleemoplossing, Zie:</span><span class="sxs-lookup"><span data-stu-id="8bfd2-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="8bfd2-166">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8bfd2-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="8bfd2-167">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. voor Windows downlevel-clients</span><span class="sxs-lookup"><span data-stu-id="8bfd2-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

