---
title: 'Azure Active Directory-rapportage: aan de slag | Microsoft Docs'
description: Bevat een lijst met de diverse beschikbare rapporten in Azure Active Directory-rapportage
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5cd1ae6196d9cd63f97dc9d302442280ece23e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="37ada-103">Aan de slag met Azure Active Directory-rapportage</span><span class="sxs-lookup"><span data-stu-id="37ada-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="37ada-104">Wat is het?</span><span class="sxs-lookup"><span data-stu-id="37ada-104">What it is</span></span>
<span data-ttu-id="37ada-105">Azure Active Directory (Azure AD) bevat beveiligings-, activiteits- en controlerapporten voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="37ada-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="37ada-106">Hierna volgt een lijst met de beschikbare rapporten:</span><span class="sxs-lookup"><span data-stu-id="37ada-106">Here's a list of the reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="37ada-107">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="37ada-107">Security reports</span></span>
* <span data-ttu-id="37ada-108">Aanmeldingen van onbekende bronnen</span><span class="sxs-lookup"><span data-stu-id="37ada-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="37ada-109">Aanmeldingen na meerdere mislukte pogingen</span><span class="sxs-lookup"><span data-stu-id="37ada-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="37ada-110">Aanmeldingen vanuit meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="37ada-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="37ada-111">Aanmeldingen van IP-adressen met verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="37ada-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="37ada-112">Onregelmatige aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="37ada-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="37ada-113">Aanmeldingen vanaf mogelijk geïnfecteerde apparaten</span><span class="sxs-lookup"><span data-stu-id="37ada-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="37ada-114">Gebruikers met afwijkende aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="37ada-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="37ada-115">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="37ada-115">Activity reports</span></span>
* <span data-ttu-id="37ada-116">Toepassingsgebruik: samenvatting</span><span class="sxs-lookup"><span data-stu-id="37ada-116">Application usage: summary</span></span>
* <span data-ttu-id="37ada-117">Toepassingsgebruik: gedetailleerd</span><span class="sxs-lookup"><span data-stu-id="37ada-117">Application usage: detailed</span></span>
* <span data-ttu-id="37ada-118">Toepassingsdashboard</span><span class="sxs-lookup"><span data-stu-id="37ada-118">Application dashboard</span></span>
* <span data-ttu-id="37ada-119">Fouten bij het inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="37ada-119">Account provisioning errors</span></span>
* <span data-ttu-id="37ada-120">Afzonderlijke gebruikersapparaten</span><span class="sxs-lookup"><span data-stu-id="37ada-120">Individual user devices</span></span>
* <span data-ttu-id="37ada-121">Afzonderlijke gebruikersactiviteiten</span><span class="sxs-lookup"><span data-stu-id="37ada-121">Individual user Activity</span></span>
* <span data-ttu-id="37ada-122">Rapport met groepsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="37ada-122">Groups activity report</span></span>
* <span data-ttu-id="37ada-123">Rapport voor de registratie van opnieuw ingestelde wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="37ada-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="37ada-124">Activiteit voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="37ada-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="37ada-125">Controlerapporten</span><span class="sxs-lookup"><span data-stu-id="37ada-125">Audit reports</span></span>
* <span data-ttu-id="37ada-126">Directorycontrolerapport</span><span class="sxs-lookup"><span data-stu-id="37ada-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="37ada-127">Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.</span><span class="sxs-lookup"><span data-stu-id="37ada-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="37ada-128">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="37ada-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="37ada-129">Rapportagepijplijn</span><span class="sxs-lookup"><span data-stu-id="37ada-129">Reporting pipeline</span></span>
<span data-ttu-id="37ada-130">De rapportagepijplijn bestaat uit drie hoofdstappen.</span><span class="sxs-lookup"><span data-stu-id="37ada-130">The reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="37ada-131">Elke keer wanneer een gebruiker zich aanmeldt of een verificatie wordt uitgevoerd, gebeurt het volgende:</span><span class="sxs-lookup"><span data-stu-id="37ada-131">Every time a user signs in, or an authentication is made, the following happens:</span></span>

* <span data-ttu-id="37ada-132">Eerst wordt de gebruiker geverifieerd (geslaagd of mislukt) en wordt het resultaat opgeslagen in de Azure Active Directory-servicedatabases.</span><span class="sxs-lookup"><span data-stu-id="37ada-132">First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.</span></span>
* <span data-ttu-id="37ada-133">Op vaste intervallen worden alle recente aanmeldingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="37ada-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="37ada-134">Op dit punt worden met onze algoritmen voor beveiliging en afwijkende activiteiten alle recente aanmeldingen doorzocht op verdachte activiteiten.</span><span class="sxs-lookup"><span data-stu-id="37ada-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="37ada-135">Na de verwerking worden de rapporten geschreven, in de cache opgeslagen en weergegeven in de klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="37ada-135">After processing, the reports are written, cached, and served in the Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="37ada-136">Tijden waarop rapporten worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="37ada-136">Report generation times</span></span>
<span data-ttu-id="37ada-137">Vanwege het grote aantal verificaties en aanmeldingen dat wordt verwerkt door het Azure AD-platform, zijn de meest recente verwerkte aanmeldingen gemiddeld een uur oud.</span><span class="sxs-lookup"><span data-stu-id="37ada-137">Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="37ada-138">Heel soms kan het acht uur duren voordat de meest recente aanmeldingen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="37ada-138">In rare cases, it may take up to 8 hours to process the most recent sign-ins.</span></span>

<span data-ttu-id="37ada-139">U vindt de meest recente verwerkte aanmelding in de Help-tekst boven aan elk rapport.</span><span class="sxs-lookup"><span data-stu-id="37ada-139">You can find the most recent processed sign-in by examining the help text at the top of each report.</span></span>

![Help-tekst boven aan elk rapport](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="37ada-141">Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.</span><span class="sxs-lookup"><span data-stu-id="37ada-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="37ada-142">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="37ada-142">Getting started</span></span>
### <a name="sign-into-the-azure-classic-portal"></a><span data-ttu-id="37ada-143">Aanmelden bij de klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="37ada-143">Sign into the Azure classic portal</span></span>
<span data-ttu-id="37ada-144">U moet u eerst aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com) als globale beheerder of compliancebeheerder.</span><span class="sxs-lookup"><span data-stu-id="37ada-144">First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="37ada-145">U moet ook een servicebeheerder of medebeheerder zijn van het Azure-abonnement of gebruikmaken van het Azure-abonnement Toegang tot Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37ada-145">You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.</span></span>

### <a name="navigate-to-reports"></a><span data-ttu-id="37ada-146">Navigeren naar rapporten</span><span class="sxs-lookup"><span data-stu-id="37ada-146">Navigate to Reports</span></span>
<span data-ttu-id="37ada-147">Als u rapporten wilt bekijken, gaat u naar het tabblad Rapporten boven aan uw directory.</span><span class="sxs-lookup"><span data-stu-id="37ada-147">To view Reports, navigate to the Reports tab at the top of your directory.</span></span>

<span data-ttu-id="37ada-148">Als dit de eerste keer is dat u de rapporten bekijkt, moet u akkoord gaan met de tekst in een dialoogvenster voordat u de rapporten kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="37ada-148">If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports.</span></span> <span data-ttu-id="37ada-149">Hiermee wordt gecontroleerd of beheerders in uw organisatie deze gegevens mogen bekijken omdat deze in sommige landen worden beschouwd als persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="37ada-149">This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.</span></span>

![Dialoogvenster](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="37ada-151">Elk rapport verkennen</span><span class="sxs-lookup"><span data-stu-id="37ada-151">Explore each report</span></span>
<span data-ttu-id="37ada-152">Navigeer in elk rapport om de verzamelde gegevens en verwerkte aanmeldingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="37ada-152">Navigate into each report to see the data being collected and the sign-ins processed.</span></span> <span data-ttu-id="37ada-153">U vindt [hier een lijst met alle rapporten](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="37ada-153">You can find a [list of all the reports here](active-directory-reporting-guide.md).</span></span>

![Alle rapporten](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a><span data-ttu-id="37ada-155">De rapporten downloaden als CSV</span><span class="sxs-lookup"><span data-stu-id="37ada-155">Download the reports as CSV</span></span>
<span data-ttu-id="37ada-156">Elk rapport kan worden gedownload als een CSV-bestand (door komma's gescheiden waarden).</span><span class="sxs-lookup"><span data-stu-id="37ada-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="37ada-157">U kunt deze bestanden gebruiken in Excel, Power BI of analyseprogramma's van derden om uw gegevens verder te analyseren.</span><span class="sxs-lookup"><span data-stu-id="37ada-157">You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.</span></span>

<span data-ttu-id="37ada-158">Als u een rapport wilt downloaden als CSV-bestand, gaat u naar het rapport en klikt u onderaan op Downloaden.</span><span class="sxs-lookup"><span data-stu-id="37ada-158">To download any report as a CSV, navigate to the report and click "Download" at the bottom.</span></span>

![Knop Downloaden](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="37ada-160">Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.</span><span class="sxs-lookup"><span data-stu-id="37ada-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="37ada-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37ada-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="37ada-162">Waarschuwingen voor afwijkende aanmeldingsactiviteiten aanpassen</span><span class="sxs-lookup"><span data-stu-id="37ada-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="37ada-163">Ga naar het tabblad Configureren van uw directory.</span><span class="sxs-lookup"><span data-stu-id="37ada-163">Navigate to the "Configure" tab of your directory.</span></span>

<span data-ttu-id="37ada-164">Ga naar de sectie Meldingen.</span><span class="sxs-lookup"><span data-stu-id="37ada-164">Scroll to the "Notifications" section.</span></span>

<span data-ttu-id="37ada-165">Schakel de sectie E-mailmeldingen van afwijkende aanmeldingen in of uit.</span><span class="sxs-lookup"><span data-stu-id="37ada-165">Enable or disable the "Email Notifications of Anomalous sign-ins" section.</span></span>

![De sectie Meldingen](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a><span data-ttu-id="37ada-167">Integreren met de rapportage-API van Azure AD</span><span class="sxs-lookup"><span data-stu-id="37ada-167">Integrate with the Azure AD Reporting API</span></span>
<span data-ttu-id="37ada-168">Zie [Aan de slag met de rapportage-API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="37ada-168">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="37ada-169">Multi-Factor Authentication inschakelen voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="37ada-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="37ada-170">Selecteer een gebruiker in een rapport.</span><span class="sxs-lookup"><span data-stu-id="37ada-170">Select a user in a report.</span></span>

<span data-ttu-id="37ada-171">Klik op de knop MFA inschakelen onder in het scherm.</span><span class="sxs-lookup"><span data-stu-id="37ada-171">Click the "Enable MFA" button at the bottom of the screen.</span></span>

![De knop Multi-Factor Authentication onder in het scherm](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="37ada-173">Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.</span><span class="sxs-lookup"><span data-stu-id="37ada-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="37ada-174">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="37ada-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="37ada-175">Controlegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="37ada-175">Audit events</span></span>
<span data-ttu-id="37ada-176">Lees meer over de gebeurtenissen die worden gecontroleerd in de directory in [Controlegebeurtenissen van Azure Active Directory-rapportage](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="37ada-176">Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="37ada-177">API-integratie</span><span class="sxs-lookup"><span data-stu-id="37ada-177">API Integration</span></span>
<span data-ttu-id="37ada-178">Zie [Aan de slag met de rapportage-API](active-directory-reporting-api-getting-started.md) en de [API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="37ada-178">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="37ada-179">Contact opnemen</span><span class="sxs-lookup"><span data-stu-id="37ada-179">Get in touch</span></span>
<span data-ttu-id="37ada-180">Stuur een e-mail naar [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) voor feedback, hulp of als u nog andere vragen hebt.</span><span class="sxs-lookup"><span data-stu-id="37ada-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="37ada-181">Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.</span><span class="sxs-lookup"><span data-stu-id="37ada-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

