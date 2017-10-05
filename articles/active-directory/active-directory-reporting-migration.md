---
title: Activiteitsrapporten vinden in de Azure portal | Microsoft Docs
description: Informatie over het vinden van rapporten voor Azure Active Directory-activiteiten in de Azure portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="e1f81-103">Activiteitsrapporten niet vinden in de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="e1f81-104">Als u van de klassieke Azure portal naar de Azure portal verplaatst, krijgt u een nieuwe kijken activiteitenlogboeken Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1f81-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="e1f81-105">In een recente [blogbericht](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we uitleggen hoe u kunt zien activiteit geregistreerd in de context van de resource die u in de Azure-portal op werkt.</span><span class="sxs-lookup"><span data-stu-id="e1f81-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="e1f81-106">In dit artikel wordt beschreven hoe rapporten die u gebruikt vinden in de klassieke Azure portal in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1f81-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="e1f81-107">Nieuwe functies</span><span class="sxs-lookup"><span data-stu-id="e1f81-107">What's new</span></span>

<span data-ttu-id="e1f81-108">Rapporten in de klassieke Azure portal zijn ingedeeld in categorieën:</span><span class="sxs-lookup"><span data-stu-id="e1f81-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="e1f81-109">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-109">Security reports</span></span>
2.  <span data-ttu-id="e1f81-110">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-110">Activity reports</span></span>
3.  <span data-ttu-id="e1f81-111">Geïntegreerde app-rapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="e1f81-112">Activiteit en geïntegreerde app-rapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-112">Activity and integrated app reports</span></span>

<span data-ttu-id="e1f81-113">Voor het context-rapporten in de Azure portal, worden bestaande rapporten samenvoegen in één weergave.</span><span class="sxs-lookup"><span data-stu-id="e1f81-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="e1f81-114">Één onderliggende API biedt de gegevens naar de weergave.</span><span class="sxs-lookup"><span data-stu-id="e1f81-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="e1f81-115">Voor deze weergave over de **Azure Active Directory** blade onder **activiteit**, selecteer **controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="e1f81-116">![Controlelogboeken](./media/active-directory-reporting-migration/482.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e1f81-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="e1f81-117">De volgende rapporten worden geconsolideerd in deze weergave:</span><span class="sxs-lookup"><span data-stu-id="e1f81-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="e1f81-118">Controlerapport</span><span class="sxs-lookup"><span data-stu-id="e1f81-118">Audit report</span></span>
-   <span data-ttu-id="e1f81-119">Activiteit voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e1f81-119">Password reset activity</span></span>
-   <span data-ttu-id="e1f81-120">Registratie-activiteit wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e1f81-120">Password reset registration activity</span></span>
-   <span data-ttu-id="e1f81-121">In activiteit</span><span class="sxs-lookup"><span data-stu-id="e1f81-121">Self-service groups activity</span></span>
-   <span data-ttu-id="e1f81-122">Wijzigingen in de groep Office365 naam</span><span class="sxs-lookup"><span data-stu-id="e1f81-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="e1f81-123">Inrichten van de activiteit van een account</span><span class="sxs-lookup"><span data-stu-id="e1f81-123">Account provisioning activity</span></span>
-   <span data-ttu-id="e1f81-124">Overschakeling van de status van het wachtwoord</span><span class="sxs-lookup"><span data-stu-id="e1f81-124">Password rollover status</span></span>
-   <span data-ttu-id="e1f81-125">Fouten bij het inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="e1f81-125">Account provisioning errors</span></span>


<span data-ttu-id="e1f81-126">Het gebruiksrapport van toepassing is uitgebreid en is opgenomen in de **aanmeldingen** weergeven.</span><span class="sxs-lookup"><span data-stu-id="e1f81-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="e1f81-127">Voor deze weergave over de **Azure Active Directory** blade onder **activiteit**, selecteer **aanmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="e1f81-128">![Aanmeldingen weergave](./media/active-directory-reporting-migration/483.png "aanmeldingen weergeven")</span><span class="sxs-lookup"><span data-stu-id="e1f81-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="e1f81-129">De **aanmeldingen** weergave bevat alle gebruikersaanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="e1f81-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="e1f81-130">U kunt deze informatie gebruiken om op te halen van informatie over het gebruik van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1f81-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="e1f81-131">Ook vindt u informatie over het gebruik van toepassing in de **bedrijfstoepassingen** overzicht, in de **beheren** sectie.</span><span class="sxs-lookup"><span data-stu-id="e1f81-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="e1f81-132">![Bedrijfstoepassingen](./media/active-directory-reporting-migration/484.png "bedrijfstoepassingen")</span><span class="sxs-lookup"><span data-stu-id="e1f81-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="e1f81-133">Toegang tot een specifiek rapport</span><span class="sxs-lookup"><span data-stu-id="e1f81-133">Access a specific report</span></span>

<span data-ttu-id="e1f81-134">Hoewel de Azure-portal één weergave biedt, kunt ook u bekijken bepaalde rapporten.</span><span class="sxs-lookup"><span data-stu-id="e1f81-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="e1f81-135">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="e1f81-135">Audit logs</span></span>

<span data-ttu-id="e1f81-136">Als reactie op feedback van klanten in de Azure portal kunt u geavanceerde filter voor toegang tot de gewenste gegevens.</span><span class="sxs-lookup"><span data-stu-id="e1f81-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="e1f81-137">Een filter kunt u een *activiteitscategorie*, die hier worden de verschillende typen activiteit geregistreerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1f81-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="e1f81-138">Als u wilt beperken resultaten als u zoekt, kunt u een categorie.</span><span class="sxs-lookup"><span data-stu-id="e1f81-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="e1f81-139">Bijvoorbeeld, als u alleen geïnteresseerd in activiteiten met betrekking tot selfservice wachtwoorden opnieuw ingesteld, kunt u de **Self-service wachtwoordbeheer** categorie.</span><span class="sxs-lookup"><span data-stu-id="e1f81-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="e1f81-140">De categorieën die u ziet zijn gebaseerd op de bron die u in werkt.</span><span class="sxs-lookup"><span data-stu-id="e1f81-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="e1f81-141">![Categorie-opties op de pagina Filter controlelogboeken](./media/active-directory-reporting-migration/06.png "categorie-opties op de pagina controlelogboeken Filter")</span><span class="sxs-lookup"><span data-stu-id="e1f81-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="e1f81-142">Categorieën voor activiteiten omvatten:</span><span class="sxs-lookup"><span data-stu-id="e1f81-142">Activity categories include:</span></span>

- <span data-ttu-id="e1f81-143">Hoofddirectory</span><span class="sxs-lookup"><span data-stu-id="e1f81-143">Core Directory</span></span>
- <span data-ttu-id="e1f81-144">Self-service voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="e1f81-144">Self-service Password Management</span></span>
- <span data-ttu-id="e1f81-145">Self-service voor groepsbeheer</span><span class="sxs-lookup"><span data-stu-id="e1f81-145">Self-service Group Management</span></span>
- <span data-ttu-id="e1f81-146">Account inrichten</span><span class="sxs-lookup"><span data-stu-id="e1f81-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="e1f81-147">Gebruik van de toepassing</span><span class="sxs-lookup"><span data-stu-id="e1f81-147">Application usage</span></span>

<span data-ttu-id="e1f81-148">Voor meer informatie over het gebruik van de toepassing voor alle apps of voor een enkele app onder **activiteit**, selecteer **aanmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="e1f81-149">U kunt de resultaten beperken, kunt u filteren op gebruikersnaam of toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1f81-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="e1f81-150">![Filter aanmelden gebeurtenissen pagina](./media/active-directory-reporting-migration/07.png "pagina aanmelden gebeurtenissen filteren")</span><span class="sxs-lookup"><span data-stu-id="e1f81-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="e1f81-151">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="e1f81-152">Azure AD afwijkende activiteit rapporten</span><span class="sxs-lookup"><span data-stu-id="e1f81-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="e1f81-153">Azure AD-beveiligingsgroep voor afwijkende activiteit rapporten vanuit de klassieke Azure portal om u te bieden met één centrale weergave zijn geconsolideerd.</span><span class="sxs-lookup"><span data-stu-id="e1f81-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="e1f81-154">Deze weergave toont alle risicogebeurtenissen die betrekking hebben op beveiliging dat Azure AD kunt detecteren en van rapporteren.</span><span class="sxs-lookup"><span data-stu-id="e1f81-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="e1f81-155">De volgende tabel afwijkende activiteit een lijst met de Azure AD beveiligingsrapporten en bijbehorende risico gebeurtenistypen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1f81-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="e1f81-156">Azure AD afwijkende activiteitenrapport</span><span class="sxs-lookup"><span data-stu-id="e1f81-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="e1f81-157">Identity protection risico gebeurtenistype</span><span class="sxs-lookup"><span data-stu-id="e1f81-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="e1f81-158">Gebruikers van wie de referenties zijn gelekt</span><span class="sxs-lookup"><span data-stu-id="e1f81-158">Users with leaked credentials</span></span> | <span data-ttu-id="e1f81-159">Gelekte aanmeldingsreferenties</span><span class="sxs-lookup"><span data-stu-id="e1f81-159">Leaked credentials</span></span> |
| <span data-ttu-id="e1f81-160">Onregelmatige aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="e1f81-160">Irregular sign-in activity</span></span> | <span data-ttu-id="e1f81-161">Onmogelijke reis naar ongewone locaties</span><span class="sxs-lookup"><span data-stu-id="e1f81-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="e1f81-162">Aanmeldingen vanaf mogelijk geïnfecteerde apparaten</span><span class="sxs-lookup"><span data-stu-id="e1f81-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="e1f81-163">Aanmeldingen vanaf geïnfecteerde apparaten</span><span class="sxs-lookup"><span data-stu-id="e1f81-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="e1f81-164">Aanmeldingen van onbekende bronnen</span><span class="sxs-lookup"><span data-stu-id="e1f81-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="e1f81-165">Aanmeldingen vanaf anonieme IP-adressen</span><span class="sxs-lookup"><span data-stu-id="e1f81-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="e1f81-166">Aanmeldingen van IP-adressen met verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="e1f81-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="e1f81-167">Aanmeldingen van IP-adressen met verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="e1f81-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="e1f81-168">Aanmeldingen vanaf onbekende locaties</span><span class="sxs-lookup"><span data-stu-id="e1f81-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="e1f81-169">De volgende Azure AD afwijkende activiteitsbeveiliging rapporten zijn niet opgenomen als risicogebeurtenissen in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="e1f81-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="e1f81-170">Aanmeldingen na meerdere mislukte pogingen</span><span class="sxs-lookup"><span data-stu-id="e1f81-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="e1f81-171">Aanmeldingen vanuit meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="e1f81-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="e1f81-172">Deze rapporten zijn nog steeds beschikbaar in de klassieke Azure portal, maar ze op een bepaald moment in de toekomst wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="e1f81-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="e1f81-173">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e1f81-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="e1f81-174">Gedetecteerde risico 's</span><span class="sxs-lookup"><span data-stu-id="e1f81-174">Detected risk events</span></span>

<span data-ttu-id="e1f81-175">In de Azure-portal, opent u rapporten over gedetecteerde risico's op de **Azure Active Directory** blade onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="e1f81-176">Gedetecteerde risicogebeurtenissen die worden bijgehouden in de volgende rapporten:</span><span class="sxs-lookup"><span data-stu-id="e1f81-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="e1f81-177">Gebruikers risico</span><span class="sxs-lookup"><span data-stu-id="e1f81-177">Users at Risk</span></span>
- <span data-ttu-id="e1f81-178">Riskante aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="e1f81-178">Risky Sign-ins</span></span>

<span data-ttu-id="e1f81-179">![Beveiligingsrapporten](./media/active-directory-reporting-migration/04.png "beveiligingsrapporten")</span><span class="sxs-lookup"><span data-stu-id="e1f81-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="e1f81-180">Zie voor meer informatie over beveiligingsrapporten:</span><span class="sxs-lookup"><span data-stu-id="e1f81-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="e1f81-181">Gebruikers op beveiligingsrapport risico's in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="e1f81-182">Riskant aanmeldingen rapport in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="e1f81-183">Activiteitsrapporten in de klassieke Azure portal vergeleken met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="e1f81-184">De tabel in deze sectie worden de bestaande rapporten in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1f81-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="e1f81-185">Ook wordt beschreven hoe u de dezelfde informatie kunt krijgen in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e1f81-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="e1f81-186">Alle controle om gegevens te bekijken, op de **Azure Active Directory** blade onder **activiteit**, gaat u naar **controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="e1f81-187">![Controlelogboeken](./media/active-directory-reporting-migration/61.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e1f81-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="e1f81-188">Klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-188">Azure classic portal</span></span>                 | <span data-ttu-id="e1f81-189">Om te zoeken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1f81-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="e1f81-190">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="e1f81-190">Audit logs</span></span>                           | <span data-ttu-id="e1f81-191">Voor **activiteitscategorie**, selecteer **Core Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="e1f81-192">Activiteit voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e1f81-192">Password reset activity</span></span>              | <span data-ttu-id="e1f81-193">Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="e1f81-194">Registratie-activiteit wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e1f81-194">Password reset registration activity</span></span> | <span data-ttu-id="e1f81-195">Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="e1f81-196">In activiteit</span><span class="sxs-lookup"><span data-stu-id="e1f81-196">Self-service groups activity</span></span>         | <span data-ttu-id="e1f81-197">Voor **activiteitscategorie**, selecteer **groepsbeheer met Self-service**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="e1f81-198">Inrichten van de activiteit van een account</span><span class="sxs-lookup"><span data-stu-id="e1f81-198">Account provisioning activity</span></span>        | <span data-ttu-id="e1f81-199">Voor **activiteitscategorie**, selecteer **Account gebruikersaanvragen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="e1f81-200">Overschakeling van de status van het wachtwoord</span><span class="sxs-lookup"><span data-stu-id="e1f81-200">Password rollover status</span></span>             | <span data-ttu-id="e1f81-201">Voor **activiteitscategorie**, selecteer **automatische overschakeling van de App-wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="e1f81-202">Fouten bij het inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="e1f81-202">Account provisioning errors</span></span>          | <span data-ttu-id="e1f81-203">Voor **activiteitscategorie**, selecteer **Account gebruikersaanvragen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="e1f81-204">Wijzigingen in de groep Office365 naam</span><span class="sxs-lookup"><span data-stu-id="e1f81-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="e1f81-205">Voor **activiteitscategorie**, selecteer **Self-service wachtwoordbeheer**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="e1f81-206">Voor **activiteit brontype**, selecteer **groep**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="e1f81-207">Voor **Activiteitbron**, selecteer **O365 groepen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="e1f81-208">Om weer te geven de **toepassingsgebruik** rapporteren op de **Azure Active Directory** blade onder **beheren**, selecteer **bedrijfstoepassingen**, en selecteer vervolgens **aanmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="e1f81-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="e1f81-209">![Enterprise toepassingen aanmeldingen rapport](./media/active-directory-reporting-migration/199.png "Enterprise toepassingen aanmeldingen rapport")</span><span class="sxs-lookup"><span data-stu-id="e1f81-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f81-210">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e1f81-210">Next steps</span></span>

<span data-ttu-id="e1f81-211">Zie [Azure Active Directory-rapportage](active-directory-reporting-azure-portal.md) voor een overzicht van de rapportage.</span><span class="sxs-lookup"><span data-stu-id="e1f81-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
