---
title: Active Directory-Apparaatbeheer Veelgestelde vragen over aaaAzure | Microsoft Docs
description: Azure Active Directory Apparaatbeheer Veelgestelde vragen over.
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="54942-103">Veelgestelde vragen over Azure Active Directory device management</span><span class="sxs-lookup"><span data-stu-id="54942-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="54942-104">**V: ik onlangs Hallo apparaat geregistreerd. Waarom zie ik Hallo apparaat kan niet onder Mijn gebruikersgegevens in hello Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="54942-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="54942-105">**A:** Windows 10-apparaten die lid van een domein met automatische apparaatregistratie zijn worden niet weergegeven onder Hallo gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="54942-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="54942-106">U moet alle apparaten toouse PowerShell toosee.</span><span class="sxs-lookup"><span data-stu-id="54942-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="54942-107">Alleen worden hello volgende apparaten vermeld in Hallo gebruikersgegevens:</span><span class="sxs-lookup"><span data-stu-id="54942-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="54942-108">Alle persoonlijke apparaten die niet lid enterprise</span><span class="sxs-lookup"><span data-stu-id="54942-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="54942-109">Alle niet - Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="54942-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="54942-110">Alle niet-Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="54942-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="54942-111">**V: Waarom kan ik alle Hallo apparaten geregistreerd in Azure Active Directory hello Azure-portal niet zien?**</span><span class="sxs-lookup"><span data-stu-id="54942-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="54942-112">**A:** er is momenteel geen toosee manier alle geregistreerde apparaten in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="54942-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="54942-113">Alle apparaten, kunt u Azure PowerShell toofind gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54942-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="54942-114">Zie voor meer informatie, Hallo [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54942-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="54942-115">**V: hoe weet ik welke status Hallo apparaat registratie van de client Hallo is?**</span><span class="sxs-lookup"><span data-stu-id="54942-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="54942-116">**A:** afhankelijk van de apparaatstatus registratie Hallo:</span><span class="sxs-lookup"><span data-stu-id="54942-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="54942-117">Welke Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="54942-117">What hello device is</span></span>
- <span data-ttu-id="54942-118">Hoe het is geregistreerd</span><span class="sxs-lookup"><span data-stu-id="54942-118">How it was registered</span></span> 
- <span data-ttu-id="54942-119">Details tooit gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="54942-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="54942-120">**V: Waarom is een apparaat dat ik hebt verwijderd in hello Azure portal of met Windows PowerShell nog steeds vermeld als geregistreerd?**</span><span class="sxs-lookup"><span data-stu-id="54942-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="54942-121">**A:** dit is standaard.</span><span class="sxs-lookup"><span data-stu-id="54942-121">**A:** This is by design.</span></span> <span data-ttu-id="54942-122">Hallo-apparaat geen toegang tooresources in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="54942-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="54942-123">Als u wilt dat tooremove Hallo apparaat en opnieuw registreren, moet een handmatige actie toobe genomen op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="54942-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="54942-124">Voor Windows 10 en Windows Server 2016 met on-premises AD-domein:</span><span class="sxs-lookup"><span data-stu-id="54942-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="54942-125">Open Hallo-opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="54942-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="54942-126">Type`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="54942-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="54942-127">Meld u af en meld u aan tootrigger Hallo geplande taak die Hallo-apparaat opnieuw registreert.</span><span class="sxs-lookup"><span data-stu-id="54942-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="54942-128">Voor andere Windows-platforms die zich on-premises AD-domein:</span><span class="sxs-lookup"><span data-stu-id="54942-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="54942-129">Open Hallo-opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="54942-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="54942-130">Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="54942-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="54942-131">Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="54942-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="54942-132">**V: Waarom zie ik dubbele apparaatvermeldingen in Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="54942-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="54942-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="54942-133">**A:**</span></span>

-   <span data-ttu-id="54942-134">Voor Windows 10 en Windows Server 2016, als ze herhaalde pogingen toounjoin zijn en opnieuw aanmelden hello hetzelfde apparaat, kunnen er dubbele vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="54942-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="54942-135">Als u toevoegen werk of School-Account hebt gebruikt, elke windows-gebruiker die voegen werk- of Schoolaccount gebruikt een nieuwe apparaatrecord gemaakt met de Hallo dezelfde apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="54942-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="54942-136">Andere Windows-platforms die zich on-premises AD-domein met behulp van automatische registratie maakt een nieuwe apparaatrecord met Hallo dezelfde apparaatnaam voor elke domeingebruiker die zich bij Hallo-apparaat aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="54942-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="54942-137">Een AADJ-machine die is gewist, opnieuw geïnstalleerd en opnieuw toegevoegd met de Hallo dezelfde naam, wordt weergegeven als een andere record met Hallo dezelfde apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="54942-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="54942-138">**V: waarom een gebruiker nog steeds toegang tot bronnen vanaf een apparaat dat ik in hello Azure-portal hebt uitgeschakeld?**</span><span class="sxs-lookup"><span data-stu-id="54942-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="54942-139">**A:** een intrekken toobe toegepast tooan uur kan duren.</span><span class="sxs-lookup"><span data-stu-id="54942-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="54942-140">Verloren apparaten, wordt u aangeraden Hallo apparaat tooensure gebruikers geen toegang tot Hallo apparaat wissen.</span><span class="sxs-lookup"><span data-stu-id="54942-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="54942-141">Zie voor meer informatie [apparaten inschrijven voor beheer in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="54942-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="54942-142">**V: Waarom kunnen mijn gebruikers zien 'U geen toegang vanaf hier'?**</span><span class="sxs-lookup"><span data-stu-id="54942-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="54942-143">**A:** als u bepaalde regels toorequire voor voorwaardelijke toegang tot de status van een specifiek apparaat hebt geconfigureerd en Hallo-apparaat voldoet niet aan criteria hello, gebruikers worden geblokkeerd en dit bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="54942-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="54942-144">Voer Hallo regels evalueren en zorg ervoor dat het Hallo-apparaat kunnen toomeet Hallo criteria tooavoid dit bericht is.</span><span class="sxs-lookup"><span data-stu-id="54942-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="54942-145">**V: ik Zie Hallo apparaatrecord onder Hallo gebruikersgegevens in hello Azure-portal en Hallo status kunt zien zoals die is geregistreerd op Hallo-client. Kan dat ik een correct instellen voor het gebruik van voorwaardelijke toegang?**</span><span class="sxs-lookup"><span data-stu-id="54942-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="54942-146">**A:** Hallo record van apparaat (deviceID) en status op Hallo Azure-portal moeten overeenkomen met de Hallo-client en voldoen aan de evaluatiecriteria van een voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="54942-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="54942-147">Zie voor meer informatie [aan de slag met Azure Active Directory-apparaatregistratie](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="54942-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="54942-148">**V: Waarom krijg ik een bericht 'gebruikersnaam of wachtwoord is onjuist' voor een apparaat ik tooAzure AD zojuist hebt toegevoegd?**</span><span class="sxs-lookup"><span data-stu-id="54942-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="54942-149">**A:** veelvoorkomende redenen voor dit scenario zijn:</span><span class="sxs-lookup"><span data-stu-id="54942-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="54942-150">Uw referenties zijn niet langer geldig.</span><span class="sxs-lookup"><span data-stu-id="54942-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="54942-151">Kan geen toocommunicate met Azure Active Directory, is uw computer.</span><span class="sxs-lookup"><span data-stu-id="54942-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="54942-152">Controleer of eventuele problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="54942-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="54942-153">vereisten voor Azure AD Join van Hallo is niet voldaan aan.</span><span class="sxs-lookup"><span data-stu-id="54942-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="54942-154">Zorg ervoor dat u stappen voor het Hallo hebt gevolgd [cloud uitbreiden mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54942-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="54942-155">Federatieve aanmeldingen vereist uw federatieve server toosupport een actieve WS-Trust-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="54942-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="54942-156">**V: Waarom Zie Hallo ' Oops... is een fout opgetreden! "dialoogvenster wanneer ik probeer mijn PC toevoegen?**</span><span class="sxs-lookup"><span data-stu-id="54942-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="54942-157">**A:** dit is een resultaat van het instellen van Azure Active Directory-inschrijving met Intune.</span><span class="sxs-lookup"><span data-stu-id="54942-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="54942-158">Zie voor meer informatie [Windows Apparaatbeheer instellen](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="54942-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="54942-159">**V: Waarom is mijn poging toojoin een PC mislukken, maar ik heb informatie over de fout niet ontvangen?**</span><span class="sxs-lookup"><span data-stu-id="54942-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="54942-160">**A:** een waarschijnlijke oorzaak is dat Hallo-gebruiker is aangemeld met het ingebouwde beheerdersaccount Hallo toohello-apparaat.</span><span class="sxs-lookup"><span data-stu-id="54942-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="54942-161">Maak een andere lokale account voordat u Azure Active Directory Join toocomplete Hallo setup.</span><span class="sxs-lookup"><span data-stu-id="54942-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="54942-162">**V: waar vind ik instructies voor het Hallo-installatie van de automatische apparaatregistratie**</span><span class="sxs-lookup"><span data-stu-id="54942-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="54942-163">**A:** Zie voor gedetailleerde instructies [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="54942-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="54942-164">**V: waar vind ik het oplossen van informatie over automatische apparaatregistratie voor Hallo?**</span><span class="sxs-lookup"><span data-stu-id="54942-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="54942-165">**A:** voor informatie over probleemoplossing, Zie:</span><span class="sxs-lookup"><span data-stu-id="54942-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="54942-166">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="54942-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="54942-167">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD voor Windows downlevel-clients</span><span class="sxs-lookup"><span data-stu-id="54942-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

