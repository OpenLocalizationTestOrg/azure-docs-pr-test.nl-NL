---
title: een Azure uitvoeren als-Account aaaConfigure | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo maken, testen en voorbeeld-gebruik van verificatie van de beveiligingsprincipal in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: naam van service-principal, setspn, azure-verificatie
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="5f5f1-104">Runbooks verifiëren met een Azure Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="5f5f1-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="5f5f1-105">Dit artikel laat zien hoe tooconfigure een Azure Automation-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="5f5f1-106">toodo dus u Hallo Run As-account functie tooauthenticate runbooks gebruiken voor het beheren van resources in Azure Resource Manager of Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="5f5f1-107">Wanneer u een Automation-account in hello Azure-portal maakt, maakt u automatisch twee accounts:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="5f5f1-108">Een Uitvoeren als-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-108">A Run As account.</span></span> <span data-ttu-id="5f5f1-109">Door dit account worden een service-principal in Azure Active Directory (Azure AD) en een certificaat gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="5f5f1-110">Hallo Inzender op rollen gebaseerde toegangsbeheer (RBAC), die Resource Manager-resources met behulp van runbooks beheert wijst ook toe.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="5f5f1-111">Een klassiek Uitvoeren als-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-111">A Classic Run As account.</span></span> <span data-ttu-id="5f5f1-112">Dit account een beheercertificaat dat is geüpload gebruikt toomanage Service Management of klassieke resources met behulp van runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="5f5f1-113">Maken van een account Hallo eenvoudiger voor u en helpt die u snel starten maken en implementeren van runbooks toosupport Automation uw automation moet.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="5f5f1-114">Met een Uitvoeren als- en een klassiek Uitvoeren als-account kunt u:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="5f5f1-115">Bieden een gestandaardiseerde manier tooauthenticate Azure bij het beheren van Resource Manager of de Service Management-resources van runbooks in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="5f5f1-116">Hallo-gebruik van globale runbooks die u in Azure waarschuwingen configureren kunt automatiseren.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="5f5f1-117">Hallo [Azure waarschuwing integratiefunctie](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) met Automation globale runbooks vereist een Automation-account dat geconfigureerd met Run As-account en een klassieke Run As-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="5f5f1-118">U kunt een automatiseringsaccount dat al is gedefinieerd uitvoeren als en klassieke Run As-accounts kunt selecteren, of u kunt toocreate een nieuw automatiseringsaccount.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="5f5f1-119">Dit artikel laat zien hoe toocreate een Automation-account van hello Azure-portal een Automation-account bijwerken met behulp van Azure PowerShell, Hallo-accountconfiguratie beheren en verifiëren in uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="5f5f1-120">Voordat u begint met het maken van een Automation-account, is een goed idee toounderstand en houd rekening met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="5f5f1-121">Een automatiseringsaccount maakt, heeft dit geen invloed op de Automation-accounts die kunt u al hebt gemaakt in de klassieke Hallo of Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="5f5f1-122">Hallo-proces werkt alleen voor Automation-accounts die u in hello Azure-portal maakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="5f5f1-123">Poging een account van de klassieke Azure-portal Hallo toocreate repliceert niet Hallo configuratie Run As-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="5f5f1-124">Als u al runbooks en activa (zoals planningen of variabelen) in plaats toomanage klassieke resources hebt en u wilt dat runbooks tooauthenticate met Hallo nieuwe klassieke Run As-account, gaat u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="5f5f1-125">toocreate klassieke Run As-account, volg Hallo-instructies in 'Uw Run As-account beheren' Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="5f5f1-126">tooupdate uw bestaande account, gebruik Hallo PowerShell script in 'Uw Automation-account bijwerken met behulp van PowerShell' Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="5f5f1-127">tooauthenticate met behulp van Hallo nieuwe Run As-account en klassieke uitvoeren als Automation-account, moet u uw bestaande runbooks met voorbeeldcode in de sectie Hallo Hallo toomodify [voorbeelden van verificatiecode](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="5f5f1-128">Hallo Run As-account is voor verificatie met een Resource Manager-resources met Hallo op basis van certificaten service-principal.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="5f5f1-129">Hallo klassieke Run As-account is voor verificatie ten opzichte van de Service Management-resources met een beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="5f5f1-130">Een Automation-account maken vanuit hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5f5f1-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="5f5f1-131">In deze sectie maakt u een Azure Automation-account van hello Azure portal, dat op zijn beurt zowel een Run As-account en een klassieke Run As-account maakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="5f5f1-132">toocreate een Automation-account, moet u lid zijn van Hallo serviceadministrators rol of medebeheerder van Hallo-abonnement dat is toohello-abonnement toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="5f5f1-133">U moet ook worden toegevoegd als een gebruiker toothat abonnement standaard Active Directory-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="5f5f1-134">Hallo account hoeft niet toobe een bevoorrechte rol toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="5f5f1-135">Als u niet lid zijn van de Active Directory-exemplaar van Hallo abonnement voordat u toohello mede beheerdersrol van Hallo abonnement worden toegevoegd, wordt u tooActive Directory toegevoegd als gast.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="5f5f1-136">In dit geval ontvangt u een "u hebt geen machtigingen toocreate..."</span><span class="sxs-lookup"><span data-stu-id="5f5f1-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="5f5f1-137">Waarschuwing voor Hallo **Automation-Account toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="5f5f1-138">Gebruikers die zijn toegevoegd toohello medebeheerder rol kan worden verwijderd uit Active Directory-exemplaar van het abonnement Hallo eerst en opnieuw toegevoegd toomake ze een volledige gebruiker in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="5f5f1-139">tooverify deze situatie Hallo **Azure Active Directory** deelvenster in hello Azure-portal door te selecteren **gebruikers en groepen**, selecteren **alle gebruikers** en, nadat u hebt geselecteerd specifieke gebruiker Hello, selecteren **profiel**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="5f5f1-140">waarde van Hallo Hallo **gebruikerstype** kenmerk onder Hallo gebruikersprofiel moet niet gelijk aan **Gast**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="5f5f1-141">Meld u aan toohello Azure-portal met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="5f5f1-142">Selecteer **Automation-accounts**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="5f5f1-143">Op Hallo **Automation-Accounts** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="5f5f1-144">Hallo **Automation-Account toevoegen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-144">hello **Add Automation Account** blade opens.</span></span>

 ![Hallo 'Automation-Account toevoegen' blade](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="5f5f1-146">Als uw account geen lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo abonnement is, Hallo volgende waarschuwing wordt weergegeven op Hallo **Automation-Account toevoegen** blade:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Waarschuwing bij Automation-account toevoegen](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="5f5f1-148">Op Hallo **Automation-Account toevoegen** blade in Hallo **naam** typt u een naam voor uw nieuwe Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="5f5f1-149">Als u meer dan één abonnement hebt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="5f5f1-150">a.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-150">a.</span></span> <span data-ttu-id="5f5f1-151">Onder **abonnement**, één voor de nieuwe account Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="5f5f1-152">b.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-152">b.</span></span> <span data-ttu-id="5f5f1-153">Klik onder **Resourcegroep** op **Nieuwe maken** of **Bestaande gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="5f5f1-154">c.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-154">c.</span></span> <span data-ttu-id="5f5f1-155">Geef onder **Locatie** een Azure-datacenter op.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="5f5f1-156">Selecteer onder **Een Uitvoeren als-account voor Azure maken** de optie **Ja** en klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5f5f1-157">Als u ervoor geen toocreate Hallo Run As-account door te selecteren kiest **Nee**, een waarschuwingsbericht weergegeven Hallo **Automation-Account toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="5f5f1-158">Hoewel het Hallo-account is gemaakt in hello Azure-portal, heeft deze geen overeenkomstige verificatie-id in de klassieke of Resource Manager abonnement directoryservice.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="5f5f1-159">Hallo-account heeft dus geen tooresources toegang in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="5f5f1-160">Met dit scenario wordt voorkomen dat runbooks die naar dit account verwijzen, taken verifiëren en uitvoeren met resources in die implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Waarschuwingsbericht op Hallo 'Automation-Account toevoegen' blade](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="5f5f1-162">Bovendien Hallo service-principal is niet gemaakt, omdat de is rol van Inzender Hallo niet toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="5f5f1-163">Terwijl Azure Hallo Automation-account maakt, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="5f5f1-164">Resources</span><span class="sxs-lookup"><span data-stu-id="5f5f1-164">Resources</span></span>
<span data-ttu-id="5f5f1-165">Als Hallo Automation-account is gemaakt, worden automatisch verschillende resources voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="5f5f1-166">Hallo resources worden samengevat in de volgende twee tabellen Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="5f5f1-167">Resources voor Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="5f5f1-167">Run As account resources</span></span>

| <span data-ttu-id="5f5f1-168">Resource</span><span class="sxs-lookup"><span data-stu-id="5f5f1-168">Resource</span></span> | <span data-ttu-id="5f5f1-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f5f1-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f5f1-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="5f5f1-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="5f5f1-171">Een grafische voorbeeldrunbook dat laat zien hoe tooauthenticate met behulp van Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="5f5f1-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="5f5f1-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="5f5f1-173">Een voorbeeldrunbook PowerShell die laat zien hoe tooauthenticate met behulp van Hallo Run As-account en alle Hallo Resource Manager-resources opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="5f5f1-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="5f5f1-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="5f5f1-175">Hallo-certificaatasset dat automatisch wordt gemaakt wanneer u een Automation-account maken of Hallo volgende PowerShell-script voor een bestaand account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="5f5f1-176">Hallo certificaat kunt u tooauthenticate met Azure zodat u Azure Resource Manager-resources van runbooks beheren kunt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="5f5f1-177">Hallo-certificaat heeft een één jaar geldig.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="5f5f1-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="5f5f1-178">AzureRunAsConnection</span></span> | <span data-ttu-id="5f5f1-179">Hallo-verbindingsasset dat automatisch wordt gemaakt wanneer u een Automation-account maken of Hallo PowerShell-script voor een bestaande account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="5f5f1-180">Resources voor klassiek Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="5f5f1-180">Classic Run As account resources</span></span>

| <span data-ttu-id="5f5f1-181">Resource</span><span class="sxs-lookup"><span data-stu-id="5f5f1-181">Resource</span></span> | <span data-ttu-id="5f5f1-182">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f5f1-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f5f1-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="5f5f1-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="5f5f1-184">Een grafische voorbeeldrunbook waarin alle Hallo VM's die zijn gemaakt met behulp van het klassieke implementatiemodel Hallo in een abonnement met behulp van Hallo klassieke Run As-account (certificaat), en vervolgens schrijft Hallo VM-naam en status worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="5f5f1-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="5f5f1-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="5f5f1-186">Een voorbeeld van de PowerShell-runbook die alle opgehaald Hallo klassieke virtuele machines in een abonnement met behulp van Hallo klassieke Run As-account (certificaat) en vervolgens schrijfbewerkingen Hallo VM-naam en de status.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="5f5f1-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="5f5f1-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="5f5f1-188">Hallo automatisch gemaakt certificaatasset tooauthenticate te gebruiken met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="5f5f1-189">Hallo-certificaat heeft een één jaar geldig.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="5f5f1-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="5f5f1-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="5f5f1-191">Hallo automatisch gemaakte verbindingsasset tooauthenticate te gebruiken met Azure zodat u de klassieke Azure-resources van runbooks beheren kunt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="5f5f1-192">Uitvoeren als-verificatie verifiëren</span><span class="sxs-lookup"><span data-stu-id="5f5f1-192">Verify Run As authentication</span></span>
<span data-ttu-id="5f5f1-193">Voer een kleine test tooconfirm die u verifiëren kunt met behulp van Hallo nieuwe Run As-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="5f5f1-194">Open in hello Azure-portal, Hallo Automation-account dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="5f5f1-195">Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="5f5f1-196">Selecteer Hallo **AzureAutomationTutorialScript** runbook, en klik vervolgens op **Start** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="5f5f1-197">Hallo volgende gebeurtenissen zich voordoen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-197">hello following events occur:</span></span>
 * <span data-ttu-id="5f5f1-198">Een [runbooktaak](automation-runbook-execution.md) is gemaakt, hello **taak** blade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht** tegel.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="5f5f1-199">Hallo taakstatus begint als **in de wachtrij geplaatst**, die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="5f5f1-200">Hallo-status wordt **starten** wanneer een werknemer Hallo taak claims.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="5f5f1-201">Hallo-status wordt **met** wanneer Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="5f5f1-202">Wanneer het Hallo-runbooktaak is voltooid, ziet u de status van **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="5f5f1-203">toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="5f5f1-204">Hallo **uitvoer** blade wordt weergegeven, met dat runbook Hallo heeft geverifieerd en een lijst met alle beschikbare resources in Hallo resourcegroep geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="5f5f1-205">Sluit Hallo **uitvoer** blade tooreturn toohello **taakoverzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="5f5f1-206">Sluit Hallo **taakoverzicht** blade en de bijbehorende van Hallo **AzureAutomationTutorialScript** runbookblade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="5f5f1-207">Klassieke Uitvoeren als-verificatie verifiëren</span><span class="sxs-lookup"><span data-stu-id="5f5f1-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="5f5f1-208">Uitvoeren van een vergelijkbare kleine tooconfirm die u verifiëren kunt met behulp van Hallo nieuwe klassieke Run As-account te testen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="5f5f1-209">Open in hello Azure-portal, Hallo Automation-account dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="5f5f1-210">Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="5f5f1-211">Selecteer Hallo **AzureClassicAutomationTutorialScript** runbook, en klik vervolgens op **Start** Hallo-runbook te starten.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="5f5f1-212">Hallo volgende gebeurtenissen zich voordoen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-212">hello following events occur:</span></span>

 * <span data-ttu-id="5f5f1-213">Een [runbooktaak](automation-runbook-execution.md) is gemaakt, hello **taak** blade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht** tegel.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="5f5f1-214">Hallo taakstatus begint als **in de wachtrij geplaatst**, die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="5f5f1-215">Hallo-status wordt **starten** wanneer een werknemer Hallo taak claims.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="5f5f1-216">Hallo-status wordt **met** wanneer Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="5f5f1-217">Wanneer het Hallo-runbooktaak is voltooid, ziet u de status van **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Runbooktest beveiligingsprincipal](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="5f5f1-219">toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="5f5f1-220">Hallo **uitvoer** blade wordt weergegeven, met dat runbook Hallo heeft geverifieerd en een lijst met alle klassieke VM's in Hallo abonnement geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="5f5f1-221">Sluit Hallo **uitvoer** blade tooreturn toohello **taakoverzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="5f5f1-222">Sluit Hallo **taakoverzicht** blade en de bijbehorende van Hallo **AzureAutomationTutorialScript** runbookblade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="5f5f1-223">Uw Uitvoeren als-account beheren</span><span class="sxs-lookup"><span data-stu-id="5f5f1-223">Managing your Run As account</span></span>
<span data-ttu-id="5f5f1-224">Op een bepaald moment voordat uw Automation-account is verlopen, moet u toorenew Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="5f5f1-225">Als u dat Hallo Run As-account er inbreuk is gemaakt denkt, kunt u deze kunt verwijderen en opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="5f5f1-226">Deze sectie wordt beschreven hoe tooperform deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="5f5f1-227">Zelfondertekend certificaat vernieuwen</span><span class="sxs-lookup"><span data-stu-id="5f5f1-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="5f5f1-228">Hallo zelfondertekend certificaat dat u hebt gemaakt voor Hallo Run As-account verloopt een jaar na de datum Hallo van maken.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="5f5f1-229">U kunt het certificaat op elk gewenst moment vernieuwen voordat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="5f5f1-230">Als u deze vernieuwt, wordt Hallo huidige geldig certificaat terugkerende tooensure dat alle runbooks die in de wachtrij staan actief of actief actief, en die zich verifiëren met Hallo Run As-account, niet nadelig worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="5f5f1-231">Hallo-certificaat is geldig tot de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="5f5f1-232">Als u uw Automation Run As-account toouse een certificaat dat is uitgegeven door de certificeringsinstantie van uw onderneming hebt geconfigureerd en u deze optie gebruikt, wordt de Hallo enterprise-certificaat worden vervangen door een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="5f5f1-233">Hallo toorenew certificaat, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="5f5f1-234">Open in hello Azure-portal, Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="5f5f1-235">Op Hallo **Automation-Account** blade in Hallo **eigenschappen van Account** deelvenster onder **Accountinstellingen**, selecteer **Run As-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Eigenschappendeelvenster voor Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="5f5f1-237">Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of Hallo klassieke Run As-account die u wilt dat toorenew Hallo certificaat voor.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="5f5f1-238">Op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **certificaat vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Certificaat vernieuwen voor Uitvoeren als-account](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="5f5f1-240">Tijdens het Hallo-certificaat wordt vernieuwd, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="5f5f1-241">Een Uitvoeren als- of klassiek Uitvoeren als-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="5f5f1-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="5f5f1-242">Deze sectie wordt beschreven hoe toodelete en opnieuw maken van een Run As- of klassieke Run As-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="5f5f1-243">Wanneer u deze actie uitvoert, wordt Hallo Automation-account bewaard.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="5f5f1-244">Nadat u een Run As- of klassieke Run As-account verwijdert, kunt u het opnieuw maken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="5f5f1-245">Open in hello Azure-portal, Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="5f5f1-246">Op Hallo **Automation-account** blade in Hallo account eigenschappendeelvenster selecteert **Run As-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="5f5f1-247">Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of klassieke Run As-account dat u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="5f5f1-248">Klik vervolgens op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Uitvoeren als-account verwijderen](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="5f5f1-250">Tijdens het Hallo-account wordt verwijderd, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="5f5f1-251">Nadat het Hallo-account is verwijderd, kunt u opnieuw dit maken op Hallo **Run As-Accounts** eigenschappenblade door het selecteren van Hallo maken de optie **Azure uitvoeren als-Account**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Hallo Automation Run As-account opnieuw maken](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="5f5f1-253">Onjuiste configuratie</span><span class="sxs-lookup"><span data-stu-id="5f5f1-253">Misconfiguration</span></span>
<span data-ttu-id="5f5f1-254">Bepaalde configuratie-items die nodig zijn voor Hallo Run As- of klassieke Run As-account toofunction goed mogelijk is verwijderd of niet goed worden gemaakt tijdens de eerste configuratie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="5f5f1-255">Hallo-items omvatten:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-255">hello items include:</span></span>

* <span data-ttu-id="5f5f1-256">Certificaatasset</span><span class="sxs-lookup"><span data-stu-id="5f5f1-256">Certificate asset</span></span>
* <span data-ttu-id="5f5f1-257">Verbindingsasset</span><span class="sxs-lookup"><span data-stu-id="5f5f1-257">Connection asset</span></span>
* <span data-ttu-id="5f5f1-258">Run As-account is verwijderd uit de rol Inzender Hallo</span><span class="sxs-lookup"><span data-stu-id="5f5f1-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="5f5f1-259">Service-principal of toepassing in Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5f1-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="5f5f1-260">In de voorgaande Hallo en andere exemplaren van onjuiste configuratie, detecteert Hallo Automation-account Hallo wijzigingen en een status weer van *onvolledig* op Hallo **Run As-Accounts** eigenschappenblade voor Hallo account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Onvolledige Uitvoeren als-configuratiestatus](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="5f5f1-262">Wanneer u Hallo Run As-account selecteert, Hallo account **eigenschappen** deelvenster Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Waarschuwingsbericht Onvolledige Uitvoeren als-configuratie](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="5f5f1-264">.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-264">.</span></span>

<span data-ttu-id="5f5f1-265">Deze problemen Run As-account kunt u snel oplossen door te verwijderen en opnieuw Hallo-account te maken.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="5f5f1-266">Uw Automation-account bijwerken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f5f1-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="5f5f1-267">U kunt PowerShell tooupdate uw bestaande Automation-account gebruiken als:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="5f5f1-268">U maakt een Automation-account maar weigeren toocreate Hallo Run As-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="5f5f1-269">U al een Automation-account toomanage Resource Manager-resources gebruikt en gewenste tooupdate Hallo account tooinclude Hallo Run As-account voor de runbook-verificatie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="5f5f1-270">U al een Automation-account toomanage klassieke resources gebruikt en u wilt tooupdate het toouse Hallo klassieke Run As-account in plaats van een nieuw account maken en uw runbooks en activa tooit migreren.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="5f5f1-271">Toocreate wilt u een Run As- en klassieke Run As-account met behulp van een certificaat zijn uitgegeven door uw enterprise-certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="5f5f1-272">Hallo-script heeft Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="5f5f1-273">Hallo-script kan alleen op Windows 10 en Windows Server 2016 met Azure Resource Manager-modules 2.01 en hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="5f5f1-274">Uitvoeren wordt niet ondersteund in eerdere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="5f5f1-275">Azure PowerShell 1.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="5f5f1-276">Zie voor meer informatie over Hallo PowerShell 1.0 release [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5f5f1-277">Een Automation-account waarnaar wordt verwezen als waarde voor Hallo Hallo *-AutomationAccountName* en *- ApplicationDisplayName* parameters in de volgende PowerShell-script Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="5f5f1-278">Hallo tooget waarden voor *SubscriptionID*, *ResourceGroup*, en *AutomationAccountName*, die de vereiste parameters voor Hallo scripts zijn, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="5f5f1-279">In Hallo Azure-portal, selecteert u uw Automation-account op Hallo **Automation-account** blade en selecteer vervolgens **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="5f5f1-280">Op Hallo **alle instellingen** blade onder **Accountinstellingen**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="5f5f1-281">Houd er rekening mee Hallo waarden op Hallo **eigenschappen** blade.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-281">Note hello values on hello **Properties** blade.</span></span>

![blade 'Eigenschappen' Hello Automation-account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="5f5f1-283">Een PowerShell-script voor Uitvoeren als-account maken</span><span class="sxs-lookup"><span data-stu-id="5f5f1-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="5f5f1-284">Deze PowerShell-script biedt ondersteuning voor Hallo volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="5f5f1-285">Een Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="5f5f1-286">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="5f5f1-287">Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="5f5f1-288">Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="5f5f1-289">Afhankelijk van Hallo configuratieoptie die u selecteert, maakt Hallo script Hallo volgende items.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="5f5f1-290">**Voor Uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="5f5f1-291">Hiermee maakt u een Azure AD-toepassing toobe geëxporteerd met een zelf-ondertekend Hallo of openbare sleutel voor de enterprise-certificaat, maakt u een account voor de service-principal voor de toepassing hello in Azure AD en wijst de rol van inzender voor Hallo-account in uw huidige Hallo abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="5f5f1-292">U kunt deze instelling tooOwner of een andere rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="5f5f1-293">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="5f5f1-294">Hiermee maakt u een Automation-certificaatasset met de naam *AzureRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5f5f1-295">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die wordt gebruikt door de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="5f5f1-296">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5f5f1-297">Hallo-verbindingsasset bevat Hallo applicationId, tenantId, subscriptionId en de vingerafdruk van certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="5f5f1-298">**Voor klassieke uitvoeren als-accounts:**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="5f5f1-299">Hiermee maakt u een Automation-certificaatasset met de naam *AzureClassicRunAsCertificate* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5f5f1-300">Hallo-certificaatasset bevat Hallo privésleutel voor certificaten die door het Hallo-beheercertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="5f5f1-301">Hiermee maakt u een Automation-verbindingsasset genaamd *AzureClassicRunAsConnection* in Hallo opgegeven Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5f5f1-302">Hallo-verbindingsasset bevat Hallo abonnementsnaam, abonnements-id en naam van certificaat asset.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="5f5f1-303">Als u de optie voor het maken van een klassieke Run As-account nadat Hallo-script is uitgevoerd is uploaden Hallo openbaar certificaat (.cer bestandsnaamextensie) toohello management opslaan voor Hallo-abonnement dat Hallo Automation-account gemaakt in.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="5f5f1-304">tooexecute Hallo script en Hallo-certificaat uploaden, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="5f5f1-305">Hallo script volgen op uw computer opslaan.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-305">Save hello following script on your computer.</span></span> <span data-ttu-id="5f5f1-306">Sla het bestand in dit voorbeeld met Hallo filename *nieuw RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="5f5f1-307">Klik op uw computer op **Start** en start vervolgens **Windows PowerShell** met verhoogde gebruikersrechten.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="5f5f1-308">Verhoogde van Hallo PowerShell opdrachtregel-shell Ga toohello map die u hebt gemaakt in stap 1 Hallo-script bevat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="5f5f1-309">Hallo-script uitvoeren met behulp van de parameterwaarden Hallo voor Hallo-configuratie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="5f5f1-310">**Een Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="5f5f1-311">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een zelfondertekend certificaat**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="5f5f1-312">**Een Uitvoeren als-account en een klassiek Uitvoeren als-account maken met een bedrijfscertificaat**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="5f5f1-313">**Een Run As-account en een klassieke Run As-account maken met behulp van een zelfondertekend certificaat in hello Azure Government cloud**</span><span class="sxs-lookup"><span data-stu-id="5f5f1-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="5f5f1-314">Nadat het Hallo-script is uitgevoerd, kunt u zich na vragen aan gebruiker tooauthenticate met Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="5f5f1-315">Aanmelden met een account dat lid is van Hallo abonnement beheerders rol en medebeheerder van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="5f5f1-316">Nadat het Hallo-script met succes is uitgevoerd, let u op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5f5f1-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="5f5f1-317">Als u een klassieke Run As-account hebt gemaakt met een zelf-ondertekend openbaar certificaat (.cer-bestand), Hallo script wordt gemaakt en slaat deze toohello map met tijdelijke bestanden op uw computer onder Hallo gebruikersprofiel *%USERPROFILE%\AppData\Local\Temp*, die u gebruikt tooexecute Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="5f5f1-318">Gebruik dit certificaat als u een klassiek Uitvoeren als-account hebt gemaakt met een openbaar certificaat (.cer-bestand).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="5f5f1-319">Volg de instructies Hallo voor [uploaden van een API management-certificaat toohello klassieke Azure-portal](../azure-api-management-certs.md), en vervolgens Hallo verwijzingsconfiguratie met Service Management-resources te valideren met behulp van Hallo [voorbeeldcode tooauthenticate met Service Management-Resources](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="5f5f1-320">Als u dit hebt gedaan *niet* klassieke Run As-account maken en verifiëren met Resource Manager-resources Hallo verwijzingsconfiguratie valideren met behulp van Hallo [voorbeeldcode voor verificatie met Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="5f5f1-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="5f5f1-321">Voorbeeld code tooauthenticate met Resource Manager-resources</span><span class="sxs-lookup"><span data-stu-id="5f5f1-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="5f5f1-322">Kunt u Hallo volgende bijgewerkt voorbeeldcode die afkomstig zijn uit Hallo *AzureAutomationTutorialScript* voorbeeldrunbook, tooauthenticate met behulp van Hallo Run As-account toomanage Resource Manager-resources met uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="5f5f1-323">toohelp u tooeasily tussen meerdere abonnementen werkt, Hallo script bevat twee extra regels met code die ondersteuning bieden voor die verwijzen naar de context van een abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="5f5f1-324">Een variabel asset met de naam *SubscriptionId* Hallo Hallo abonnement-ID bevat.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="5f5f1-325">Na het Hallo `Add-AzureRmAccount` instructie van de cmdlet Hallo [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet vermeld met de parameterset Hallo *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="5f5f1-326">Als de naam van variabele Hallo te algemeen is, kunt u herzien tooinclude een voorvoegsel of een andere naming convention toomake deze eenvoudiger tooidentify.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="5f5f1-327">U kunt ook kunt u de parameterset Hallo *- SubscriptionName* in plaats van *- SubscriptionId* met een bijbehorende variabeleasset.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="5f5f1-328">Hallo cmdlet die u kunt gebruiken voor verificatie in Hallo-runbook `Add-AzureRmAccount`, gebruikt Hallo *ServicePrincipalCertificate* parameterset.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="5f5f1-329">Hiermee verifieert met behulp van Hallo service principal certificaat niet Hallo gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="5f5f1-330">Voorbeeld code tooauthenticate met Service Management-resources</span><span class="sxs-lookup"><span data-stu-id="5f5f1-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="5f5f1-331">U kunt na de bijgewerkte voorbeeldcode die is genomen van Hallo Hallo *AzureClassicAutomationTutorialScript* voorbeeldrunbook, tooauthenticate met behulp van Hallo klassieke Run As-account toomanage klassieke resources met uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="5f5f1-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="5f5f1-332">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f5f1-332">Next steps</span></span>
* [<span data-ttu-id="5f5f1-333">Toepassings- en service-principalobjecten in Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5f1-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="5f5f1-334">Op rollen gebaseerd toegangsbeheer in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="5f5f1-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="5f5f1-335">Overzicht van certificaten voor Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="5f5f1-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
