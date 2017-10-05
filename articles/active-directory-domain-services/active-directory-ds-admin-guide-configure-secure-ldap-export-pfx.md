---
title: Beveiligde LDAP (LDAPS) in Azure AD Domain Services configureren | Microsoft Docs
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="adc79-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="adc79-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="adc79-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="adc79-104">Before you begin</span></span>
<span data-ttu-id="adc79-105">Zorg ervoor dat u hebt voltooid [taak 1: een certificaat verkrijgen voor beveiligde LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="adc79-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="adc79-106">Taak 2: het beveiligde LDAP-certificaat te exporteren een. PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="adc79-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="adc79-107">Voordat u deze taak, zorg ervoor dat u het beveiligde LDAP-certificaat hebt verkregen van een openbare certificeringsinstantie (CA) of een zelfondertekend certificaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adc79-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="adc79-108">De volgende stappen uitvoeren, om te exporteren van het certificaat LDAPS naar een. PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="adc79-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="adc79-109">Druk op de **Start** knop en het type **R**. In de **uitvoeren** dialoogvenster, type **mmc** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="adc79-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![De MMC-console starten](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="adc79-111">Op de **User Account Control** gevraagd, klikt u op **Ja** MMC (Microsoft Management Console) als administrator te starten.</span><span class="sxs-lookup"><span data-stu-id="adc79-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="adc79-112">Van de **bestand** menu, klikt u op **module toevoegen/verwijderen...** .</span><span class="sxs-lookup"><span data-stu-id="adc79-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Module toevoegen aan MMC-console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="adc79-114">In de **toevoegen of verwijderen van modules** dialoogvenster, selecteer de **certificaten** -module en klikt u op de **toevoegen >** knop.</span><span class="sxs-lookup"><span data-stu-id="adc79-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Module Certificaten toevoegen aan MMC-console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="adc79-116">In de **-module Certificaten** wizard selecteert u **computeraccount** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="adc79-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Module Certificaten voor computeraccount toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="adc79-118">Op de **Computer selecteren** pagina **lokale computer: (de computer waarop deze console wordt uitgevoerd)** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="adc79-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Module Certificaten - Selecteer computer toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="adc79-120">In de **toevoegen of verwijderen van modules** dialoogvenster, klikt u op **OK** de module Certificaten toevoegen aan MMC.</span><span class="sxs-lookup"><span data-stu-id="adc79-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Module Certificaten toevoegen aan MMC - gedaan](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="adc79-122">Klik in het venster MMC om uit te breiden **consolebasis**.</span><span class="sxs-lookup"><span data-stu-id="adc79-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="adc79-123">U ziet de module Certificaten geladen.</span><span class="sxs-lookup"><span data-stu-id="adc79-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="adc79-124">Klik op **certificaten (lokale Computer)** uit te breiden.</span><span class="sxs-lookup"><span data-stu-id="adc79-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="adc79-125">Vouw de **persoonlijke** knooppunt, gevolgd door de **certificaten** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="adc79-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Archief met persoonlijke certificaten openen](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="adc79-127">U ziet het zelfondertekend certificaat gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adc79-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="adc79-128">Bekijk de eigenschappen van het certificaat om ervoor te zorgen die op de windows PowerShell gerapporteerd tijdens het maken van het certificaat komt overeen met de vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="adc79-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="adc79-129">Selecteer het zelfondertekend certificaat en **met de rechtermuisknop op**.</span><span class="sxs-lookup"><span data-stu-id="adc79-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="adc79-130">Selecteer in het snelmenu **alle taken** en selecteer **exporteren...** .</span><span class="sxs-lookup"><span data-stu-id="adc79-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="adc79-132">In de **Wizard Certificaat exporteren**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="adc79-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Certificaatwizard exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="adc79-134">Op de **persoonlijke sleutel exporteren** pagina **Ja, de persoonlijke sleutel exporteren**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="adc79-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![De persoonlijke certificaatsleutel exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="adc79-136">De persoonlijke sleutel samen met het certificaat, moet u exporteren.</span><span class="sxs-lookup"><span data-stu-id="adc79-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="adc79-137">Als u een PFX die de persoonlijke sleutel voor het certificaat niet bevat, mislukt beveiligde LDAP voor uw beheerde domein inschakelen.</span><span class="sxs-lookup"><span data-stu-id="adc79-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="adc79-138">Op de **bestandsindeling voor Export** pagina **Personal Information Exchange - PKCS #12 (. (PFX)** als de bestandsindeling voor het geëxporteerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="adc79-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Certificaat-bestandsindeling voor export](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="adc79-140">Alleen de. PFX-indeling wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="adc79-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="adc79-141">Het certificaat niet exporteren de. CER-bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="adc79-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="adc79-142">Op de **beveiliging** pagina de **wachtwoord** optie en typ een wachtwoord beveiligen de. PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="adc79-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="adc79-143">Onthoud dit wachtwoord omdat in de volgende taak vereist wel.</span><span class="sxs-lookup"><span data-stu-id="adc79-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="adc79-144">Klik op **volgende** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="adc79-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="adc79-145">Wachtwoord voor het exporteren van certificaat</span><span class="sxs-lookup"><span data-stu-id="adc79-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="adc79-146">Noteer dit wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="adc79-146">Make a note of this password.</span></span> <span data-ttu-id="adc79-147">U moet deze tijdens het inschakelen van beveiligde LDAP voor dit beheerde domein in [taak 3 - beveiligde LDAP voor het beheerde domein inschakelen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="adc79-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="adc79-148">Op de **te exporteren bestand** pagina, geef de bestandsnaam en de locatie waar u wilt het certificaat te exporteren.</span><span class="sxs-lookup"><span data-stu-id="adc79-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Pad voor het exporteren van certificaat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="adc79-150">Klik op de volgende pagina **voltooien** het certificaat te exporteren naar een PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="adc79-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="adc79-151">U ziet bevestigingsvenster wanneer het certificaat is geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="adc79-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Gedaan certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="adc79-153">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="adc79-153">Next step</span></span>
[<span data-ttu-id="adc79-154">Taak 3: beveiligde LDAP voor het beheerde domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="adc79-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
