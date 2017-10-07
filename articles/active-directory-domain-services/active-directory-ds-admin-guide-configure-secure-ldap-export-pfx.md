---
title: aaaConfigure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4d4d9-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="4d4d9-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4d4d9-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4d4d9-104">Before you begin</span></span>
<span data-ttu-id="4d4d9-105">Zorg ervoor dat u hebt voltooid [taak 1: een certificaat verkrijgen voor beveiligde LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="4d4d9-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="4d4d9-106">Taak 2: Hallo beveiligde LDAP certificaat tooa exporteren. PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="4d4d9-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="4d4d9-107">Voordat u deze taak, zorg ervoor dat u Hallo beveiligde LDAP-certificaat hebt verkregen van een openbare certificeringsinstantie (CA) of een zelfondertekend certificaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="4d4d9-108">Hallo stappen uitvoert, tooexport Hallo LDAPS tooa van het certificaat. PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="4d4d9-109">Druk op Hallo **Start** knop en het type **R**. In Hallo **uitvoeren** dialoogvenster, type **mmc** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Hallo MMC-console starten](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="4d4d9-111">Op Hallo **User Account Control** gevraagd, klikt u op **Ja** toolaunch MMC (Microsoft Management Console) als administrator.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="4d4d9-112">Van Hallo **bestand** menu, klikt u op **module toevoegen/verwijderen...** .</span><span class="sxs-lookup"><span data-stu-id="4d4d9-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Console-module tooMMC toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="4d4d9-114">In Hallo **toevoegen of verwijderen van modules** dialoogvenster, selecteer Hallo **certificaten** -module en klikt u op Hallo **toevoegen >** knop.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![De console tooMMC-module Certificaten toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="4d4d9-116">In Hallo **-module Certificaten** wizard selecteert u **computeraccount** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Module Certificaten voor computeraccount toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="4d4d9-118">Op Hallo **Computer selecteren** pagina **lokale computer: (Hallo-computer waarop deze console wordt uitgevoerd)** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Module Certificaten - Selecteer computer toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="4d4d9-120">In Hallo **toevoegen of verwijderen van modules** dialoogvenster, klikt u op **OK** tooadd Hallo certificaten module tooMMC.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Certificaten-module tooMMC - gedaan toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="4d4d9-122">Klik in de MMC-venster Hallo tooexpand **consolebasis**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="4d4d9-123">U ziet Hallo module Certificaten geladen.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="4d4d9-124">Klik op **certificaten (lokale Computer)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="4d4d9-125">Klik op tooexpand hello **persoonlijke** knooppunt, gevolgd door Hallo **certificaten** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Archief met persoonlijke certificaten openen](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="4d4d9-127">U ziet Hallo zelfondertekend certificaat gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="4d4d9-128">U kunt nagaan Hallo eigenschappen van Hallo certificaat tooensure Hallo vingerafdruk overeenkomt met die voor de PowerShell-vensters Hallo gerapporteerd tijdens het Hallo-certificaat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="4d4d9-129">Selecteer Hallo zelfondertekend certificaat en **met de rechtermuisknop op**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="4d4d9-130">Selecteer in het contextmenu hello, **alle taken** en selecteer **exporteren...** .</span><span class="sxs-lookup"><span data-stu-id="4d4d9-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="4d4d9-132">In Hallo **Wizard Certificaat exporteren**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Certificaatwizard exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="4d4d9-134">Op Hallo **persoonlijke sleutel exporteren** pagina **Ja, Hallo persoonlijke sleutel exporteren**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![De persoonlijke certificaatsleutel exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="4d4d9-136">De persoonlijke sleutel Hallo samen met de Hallo certificaat, moet u exporteren.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="4d4d9-137">Als u een PFX die bevat geen persoonlijke sleutel van de Hallo voor Hallo certificaat opgeeft, mislukt beveiligde LDAP voor uw beheerde domein inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="4d4d9-138">Op Hallo **bestandsindeling voor Export** pagina **Personal Information Exchange - PKCS #12 (. (PFX)** als Hallo-bestandsindeling voor Hallo certificaat geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Certificaat-bestandsindeling voor export](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="4d4d9-140">Alleen hello. PFX-indeling wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="4d4d9-141">Hallo certificaat toohello niet exporteren. CER-bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="4d4d9-142">Op Hallo **beveiliging** pagina, selecteer Hallo **wachtwoord** optie en typt u een wachtwoord tooprotect Hallo. PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="4d4d9-143">Onthoud dit wachtwoord omdat in de volgende taak Hallo wel vereist.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="4d4d9-144">Klik op **volgende** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="4d4d9-145">Wachtwoord voor het exporteren van certificaat</span><span class="sxs-lookup"><span data-stu-id="4d4d9-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="4d4d9-146">Noteer dit wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-146">Make a note of this password.</span></span> <span data-ttu-id="4d4d9-147">U moet deze tijdens het inschakelen van beveiligde LDAP voor dit beheerde domein in [taak 3 - beveiligde LDAP voor Hallo beheerde domein inschakelen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="4d4d9-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="4d4d9-148">Op Hallo **bestand tooExport** pagina, Hallo-bestandsnaam en locatie waar u tooexport Hallo certificaat wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Pad voor het exporteren van certificaat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="4d4d9-150">Klik op Hallo volgende pagina op **voltooien** tooexport hello tooa PFX-certificaatbestand.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="4d4d9-151">U ziet bevestigingsvenster wanneer Hallo-certificaat is geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="4d4d9-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Gedaan certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="4d4d9-153">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="4d4d9-153">Next step</span></span>
[<span data-ttu-id="4d4d9-154">Taak 3: het inschakelen van beveiligde LDAP voor Hallo beheerd domein</span><span class="sxs-lookup"><span data-stu-id="4d4d9-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
