---
title: Azure Automation-account aaaManage | Microsoft Docs
description: Dit artikel wordt beschreven hoe toomanage Hallo configuratie van uw Automation-account zoals certificaatvernieuwing, verwijdering en onjuiste configuratie.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="7c94e-103">Azure Automation-account beheren</span><span class="sxs-lookup"><span data-stu-id="7c94e-103">Manage Azure Automation account</span></span>
<span data-ttu-id="7c94e-104">Op een bepaald moment voordat uw Automation-account is verlopen, moet u toorenew Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="7c94e-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="7c94e-105">Als u dat Hallo Run As-account er inbreuk is gemaakt denkt, kunt u deze kunt verwijderen en opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="7c94e-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="7c94e-106">Deze sectie wordt beschreven hoe tooperform deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="7c94e-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="7c94e-107">Zelfondertekend certificaat vernieuwen</span><span class="sxs-lookup"><span data-stu-id="7c94e-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="7c94e-108">Hallo zelfondertekend certificaat dat u hebt gemaakt voor Hallo Run As-account verloopt een jaar na de datum Hallo van maken.</span><span class="sxs-lookup"><span data-stu-id="7c94e-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="7c94e-109">U kunt het certificaat op elk gewenst moment vernieuwen voordat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="7c94e-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="7c94e-110">Als u deze vernieuwt, wordt Hallo huidige geldig certificaat terugkerende tooensure dat alle runbooks die in de wachtrij staan actief of actief actief, en die zich verifiëren met Hallo Run As-account, niet nadelig worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="7c94e-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="7c94e-111">Hallo-certificaat is geldig tot de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="7c94e-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="7c94e-112">Als u uw Automation Run As-account toouse een certificaat dat is uitgegeven door de certificeringsinstantie van uw onderneming hebt geconfigureerd en u deze optie gebruikt, wordt de Hallo enterprise-certificaat worden vervangen door een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="7c94e-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="7c94e-113">Hallo toorenew certificaat, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c94e-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="7c94e-114">Open in hello Azure-portal, Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="7c94e-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="7c94e-115">Op Hallo **Automation-Account** blade in Hallo **eigenschappen van Account** deelvenster onder **Accountinstellingen**, selecteer **Run As-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7c94e-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Eigenschappendeelvenster voor Automation-account](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="7c94e-117">Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of Hallo klassieke Run As-account die u wilt dat toorenew Hallo certificaat voor.</span><span class="sxs-lookup"><span data-stu-id="7c94e-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="7c94e-118">Op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **certificaat vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="7c94e-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Certificaat vernieuwen voor Uitvoeren als-account](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="7c94e-120">Tijdens het Hallo-certificaat wordt vernieuwd, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="7c94e-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="7c94e-121">Een Uitvoeren als- of klassiek Uitvoeren als-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="7c94e-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="7c94e-122">Deze sectie wordt beschreven hoe toodelete en opnieuw maken van een Run As- of klassieke Run As-account.</span><span class="sxs-lookup"><span data-stu-id="7c94e-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="7c94e-123">Wanneer u deze actie uitvoert, wordt Hallo Automation-account bewaard.</span><span class="sxs-lookup"><span data-stu-id="7c94e-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="7c94e-124">Nadat u een Run As- of klassieke Run As-account verwijdert, kunt u het opnieuw maken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7c94e-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="7c94e-125">Open in hello Azure-portal, Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="7c94e-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="7c94e-126">Op Hallo **Automation-account** blade in Hallo account eigenschappendeelvenster selecteert **Run As-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7c94e-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="7c94e-127">Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of klassieke Run As-account dat u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="7c94e-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="7c94e-128">Klik vervolgens op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7c94e-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Uitvoeren als-account verwijderen](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="7c94e-130">Tijdens het Hallo-account wordt verwijderd, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="7c94e-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="7c94e-131">Nadat het Hallo-account is verwijderd, kunt u opnieuw dit maken op Hallo **Run As-Accounts** eigenschappenblade door het selecteren van Hallo maken de optie **Azure uitvoeren als-Account**.</span><span class="sxs-lookup"><span data-stu-id="7c94e-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Hallo Automation Run As-account opnieuw maken](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="7c94e-133">Onjuiste configuratie</span><span class="sxs-lookup"><span data-stu-id="7c94e-133">Misconfiguration</span></span>
<span data-ttu-id="7c94e-134">Bepaalde configuratie-items die nodig zijn voor Hallo Run As- of klassieke Run As-account toofunction goed mogelijk is verwijderd of niet goed worden gemaakt tijdens de eerste configuratie.</span><span class="sxs-lookup"><span data-stu-id="7c94e-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="7c94e-135">Hallo-items omvatten:</span><span class="sxs-lookup"><span data-stu-id="7c94e-135">hello items include:</span></span>

* <span data-ttu-id="7c94e-136">Certificaatasset</span><span class="sxs-lookup"><span data-stu-id="7c94e-136">Certificate asset</span></span>
* <span data-ttu-id="7c94e-137">Verbindingsasset</span><span class="sxs-lookup"><span data-stu-id="7c94e-137">Connection asset</span></span>
* <span data-ttu-id="7c94e-138">Run As-account is verwijderd uit de rol Inzender Hallo</span><span class="sxs-lookup"><span data-stu-id="7c94e-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="7c94e-139">Service-principal of toepassing in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c94e-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="7c94e-140">In de voorgaande Hallo en andere exemplaren van onjuiste configuratie, detecteert Hallo Automation-account Hallo wijzigingen en een status weer van *onvolledig* op Hallo **Run As-Accounts** eigenschappenblade voor Hallo account.</span><span class="sxs-lookup"><span data-stu-id="7c94e-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Onvolledige Uitvoeren als-configuratiestatus](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="7c94e-142">Wanneer u Hallo Run As-account selecteert, Hallo account **eigenschappen** deelvenster Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7c94e-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Waarschuwingsbericht Onvolledige Uitvoeren als-configuratie](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="7c94e-144">.</span><span class="sxs-lookup"><span data-stu-id="7c94e-144">.</span></span>

<span data-ttu-id="7c94e-145">Deze problemen Run As-account kunt u snel oplossen door te verwijderen en opnieuw Hallo-account te maken.</span><span class="sxs-lookup"><span data-stu-id="7c94e-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c94e-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c94e-146">Next steps</span></span>
* <span data-ttu-id="7c94e-147">Voor meer informatie over Service-Principals te verwijzen[toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="7c94e-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="7c94e-148">Voor meer informatie over toegangsbeheer op basis van rollen in Azure Automation te verwijzen[toegangsbeheer op basis van rollen in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7c94e-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7c94e-149">Voor meer informatie over certificaten en Azure-services te verwijzen[certificaten voor Azure Cloud Services-overzicht](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="7c94e-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
