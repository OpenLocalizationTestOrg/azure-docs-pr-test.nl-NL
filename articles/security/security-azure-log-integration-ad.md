---
title: aaaAzure logboek integratie met Azure Active Directory-controlelogboeken | Microsoft Docs
description: Meer informatie over hoe tooinstall hello Azure Log Integration-service en de logboeken van Azure controlelogboeken integreren
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="89691-103">Integratie van Azure Active Directory-auditlogboeken</span><span class="sxs-lookup"><span data-stu-id="89691-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="89691-104">Controlegebeurtenissen van Azure Active Directory (Azure AD) kunnen u bepalen bevoorrechte acties die is opgetreden in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89691-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="89691-105">U kunt zien Hallo typen gebeurtenissen die u bijhouden aan de hand van kunt [Azure Active Directory-controlerapportgebeurtenissen](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="89691-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="89691-106">Voordat u de stappen in dit artikel hello, moet u Hallo doornemen [aan de slag](security-azure-log-integration-get-started.md) en voltooi er Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="89691-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="89691-107">Controlelogboeken stappen toointegrate Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="89691-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="89691-108">Open Hallo-opdrachtprompt en voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="89691-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="89691-109">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="89691-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="89691-110">Met deze opdracht wordt u gevraagd om uw Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89691-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="89691-111">Hallo opdracht maakt u een Azure Active Directory service-principal in hello Azure AD-tenants die als host fungeren hello Azure-abonnementen in welke Hallo aangemelde gebruiker een beheerder, CO-beheerder of een eigenaar is.</span><span class="sxs-lookup"><span data-stu-id="89691-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="89691-112">Hallo-opdracht mislukt als Hallo aangemelde gebruiker een gastgebruiker in hello Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="89691-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="89691-113">TooAzure verificatie wordt gedaan door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89691-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="89691-114">Maken van een service-principal voor Azure Log integratie maakt hello Azure AD identity die toegang tooread van Azure-abonnementen krijgt.</span><span class="sxs-lookup"><span data-stu-id="89691-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="89691-115">Voer Hallo opdracht tooprovide na uw tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="89691-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="89691-116">U moet lid van Hallo tenant admin rol toorun Hallo opdracht toobe.</span><span class="sxs-lookup"><span data-stu-id="89691-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="89691-117">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="89691-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="89691-118">Controleer Hallo na mappen tooconfirm die hello Azure Active Directory-audit log JSON-bestanden in deze zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="89691-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="89691-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="89691-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="89691-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="89691-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="89691-121">Hallo toont volgende video Hallo stappen die in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="89691-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="89691-122">Neem contact op met de leverancier van uw SIEM voor specifieke instructies voor het Hallo-informatie te brengen in Hallo JSON-bestanden in uw security information en event management (SIEM)-systeem.</span><span class="sxs-lookup"><span data-stu-id="89691-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="89691-123">Hulp is beschikbaar via Hallo [Azure Log integratie MSDN-Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="89691-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="89691-124">Dit forum kunt mensen in hello Azure Log integratie community toosupport elkaar met vragen, antwoorden, tips en slagen.</span><span class="sxs-lookup"><span data-stu-id="89691-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="89691-125">Bovendien hello Azure Log integratie team dit forum wordt bewaakt en helpt wanneer dat mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="89691-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="89691-126">U kunt ook openen een [ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="89691-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="89691-127">Selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="89691-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89691-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89691-128">Next steps</span></span>
<span data-ttu-id="89691-129">toolearn meer informatie over de integratie van Azure Log, Zie:</span><span class="sxs-lookup"><span data-stu-id="89691-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="89691-130">[Microsoft Azure Log-integratie voor Azure logboeken](https://www.microsoft.com/download/details.aspx?id=53324): deze Download Center-pagina geeft details, systeemvereisten en installatie-instructies voor de integratie van Azure-logboek.</span><span class="sxs-lookup"><span data-stu-id="89691-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="89691-131">[Inleiding tooAzure logboek integratie](security-azure-log-integration-overview.md): in dit artikel vindt u tooAzure logboek integratie, de belangrijkste mogelijkheden en hoe het werkt.</span><span class="sxs-lookup"><span data-stu-id="89691-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="89691-132">[Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): dit blogbericht leest u hoe tooconfigure Azure Log integratie toowork met partneroplossingen Splunk, HP ArcSight en IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="89691-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="89691-133">[Veelgestelde vragen over de Azure Log integratie](security-azure-log-integration-faq.md): in dit artikel antwoorden op vragen over Azure Log-integratie.</span><span class="sxs-lookup"><span data-stu-id="89691-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="89691-134">[Security Center waarschuwingen integreren met Azure Log integratie](../security-center/security-center-integrating-alerts-with-log-integration.md): dit artikel laat zien hoe toosync Security Center waarschuwingen, samen met de virtuele machine beveiligingsgebeurtenissen die is verzameld door Azure diagnoses en Azure controlelogboeken met uw logboekanalyse of SIEM-oplossing.</span><span class="sxs-lookup"><span data-stu-id="89691-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="89691-135">[Nieuwe functies voor Azure Diagnostics- en Azure controlelogboeken](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): vindt u in dit blogbericht tooAzure controlelogboeken en andere functies waarmee u inzicht in Hallo bewerkingen van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="89691-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
