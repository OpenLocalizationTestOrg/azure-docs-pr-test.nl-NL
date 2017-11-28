---
title: aaaBack van VMware-servers met Azure Backup-Server | Microsoft Docs
description: Gebruik Azure Backup-Server tooback u een VMware vCenter/ESXi-servers tooAzure of de schijf. In dit artikel wordt stap voor-stap instructies voor back-ups maken (of beveiligen) = uw VMware-werkbelastingen.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="bf2c7-104">Back-up van een VMware server tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf2c7-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="bf2c7-105">Dit artikel wordt uitgelegd hoe tooconfigure Azure Backup-Server toohelp VMware server-werkbelasting beveiligen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="bf2c7-106">In dit artikel wordt ervan uitgegaan dat u hebt al Azure Backup-Server is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="bf2c7-107">Als u geen Azure Backup-Server is geïnstalleerd, raadpleegt u [tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="bf2c7-108">Azure Backup-Server kunnen back-up maken of te beschermen, VMware vCenter-serverversie 6.5, 6.0 en 5.5.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="bf2c7-109">Maken van een beveiligde verbinding toohello vCenter-Server</span><span class="sxs-lookup"><span data-stu-id="bf2c7-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="bf2c7-110">Standaard communiceert Azure Backup-Server met elk vCenter-Server via een HTTPS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="bf2c7-111">tooturn op Hallo veilige communicatie, wordt aangeraden dat u Hallo VMware certificeringsinstantie (CA)-certificaat op Azure Backup-Server installeren.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="bf2c7-112">Als u geen veilige communicatie vereist en toodisable Hallo HTTPS vereiste wilt gebruiken, Zie [uitschakelen beveiligde communicatieprotocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="bf2c7-113">een beveiligde verbinding tussen Azure Backup-Server en Hallo vCenter-Server, toocreate importeren Hallo vertrouwd certificaat op de Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="bf2c7-114">Normaal, gebruikt u een browser op Hallo back-upserver van Azure machine tooconnect toohello vCenter-Server via Hallo vSphere webclient.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="bf2c7-115">Hallo wanneer u eerst hello Azure Backup-Server browser tooconnect toohello vCenter Server, Hallo-verbinding niet veilig.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="bf2c7-116">Hallo volgende afbeelding geeft Hallo onbeveiligde verbinding.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-116">hello following image shows hello unsecured connection.</span></span>

![Voorbeeld van een niet-beveiligde verbinding tooVMware server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="bf2c7-118">toofix dit probleem en een beveiligde verbinding maken, downloaden Hallo vertrouwde basis-CA-certificaten.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="bf2c7-119">Voer Hallo URL toohello vSphere webclient in Hallo-browser op Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="bf2c7-120">Hallo vSphere webclient-aanmeldingspagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere webclient](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="bf2c7-122">Aan de onderkant van de Hallo van Hallo-informatie voor beheerders en ontwikkelaars, zoek Hallo **downloaden vertrouwde basis-CA-certificaten** koppeling.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Koppeling toodownload Hallo vertrouwde basis-CA-certificaten](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="bf2c7-124">Als u Hallo vSphere webclient-aanmeldingspagina niet ziet, controleert u de proxy-instellingen van uw browser.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="bf2c7-125">Klik op **downloaden vertrouwde basis-CA-certificaten**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="bf2c7-126">Hallo vCenter-Server downloadt een bestand tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="bf2c7-127">Hallo bestandsnaam heet **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-127">hello file's name is named **download**.</span></span> <span data-ttu-id="bf2c7-128">Afhankelijk van uw browser die u ontvangt een bericht waarin wordt gevraagd of tooopen of Hallo bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![bericht downloaden wanneer certificaten worden gedownload.](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="bf2c7-130">Hallo tooa bestandslocatie op Azure Backup-Server opslaan.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="bf2c7-131">Wanneer u Hallo bestand opslaat, toevoegen Hallo .zip-extensie.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="bf2c7-132">Hallo-bestand is een ZIP-bestand dat Hallo informatie over Hallo certificaten bevat.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="bf2c7-133">U kunt met de extensie .zip hello, Hallo extractie-hulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="bf2c7-134">Met de rechtermuisknop op **download.zip**, en selecteer vervolgens **Alles uitpakken** tooextract Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="bf2c7-135">Hallo ZIP-bestand uitgepakt haar inhoud tooa map met de naam **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="bf2c7-136">Twee typen bestanden worden weergegeven in Hallo certificaten map.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="bf2c7-137">Hallo basiscertificaatbestand heeft een extensie die met een genummerde volgorde zoals.0 en.1 begint.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="bf2c7-138">Hallo CRL-bestand heeft een extensie die met een reeks zoals .r0 of .r1 begint.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="bf2c7-139">Hallo CRL-bestand is gekoppeld aan een certificaat.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="bf2c7-140">Lokaal uitgepakt bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="bf2c7-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="bf2c7-141">In Hallo **certificaten** map met de rechtermuisknop op Hallo basiscertificaatbestand en klik vervolgens op **naam**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="bf2c7-142">Wijzig de naam van basiscertificaat</span><span class="sxs-lookup"><span data-stu-id="bf2c7-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="bf2c7-143">Hallo-basiscertificaat van extensie too.crt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="bf2c7-144">Als u wordt gevraagd als u zeker dat u toochange Hallo extensie bent, klikt u op **Ja** of **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="bf2c7-145">Anders kunt u de juiste functie Hallo-bestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="bf2c7-146">Hallo-pictogram voor Hallo bestand wijzigingen tooan pictogram van een basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="bf2c7-147">Met de rechtermuisknop op het Hallo-basiscertificaat en selecteer in het pop-upmenu hello, **certificaat installeren**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="bf2c7-148">Hallo **Wizard Certificaat importeren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="bf2c7-149">In Hallo **Wizard Certificaat importeren** dialoogvenster, **lokale Machine** als bestemming voor Hallo-certificaat en klik vervolgens op Hallo **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="bf2c7-150">Certificaat bestemming opslagopties</span><span class="sxs-lookup"><span data-stu-id="bf2c7-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="bf2c7-151">Als u wordt gevraagd als u wilt dat tooallow wijzigingen toohello computer, klikt u op **Ja** of **OK**, tooall Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="bf2c7-152">Op Hallo **certificaatarchief** pagina **alle certificaten in Hallo volgende archief plaatsen**, en klik vervolgens op **Bladeren** toochoose Hallo-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Certificaten in een bepaalde opslag-positie plaatsen](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="bf2c7-154">Hallo **certificaatarchief selecteren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Map van de certificaathiërarchie opslag](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="bf2c7-156">Selecteer **Trusted Root Certification Authorities** als de doelmap Hallo voor Hallo certificaten en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Certificaat-doelmap](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="bf2c7-158">Hallo **Trusted Root Certification Authorities** map is bevestigd als Hallo-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="bf2c7-159">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-159">Click **Next**.</span></span>

    ![Archiefmap certificaat](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="bf2c7-161">Op Hallo **voltooien Hallo Wizard Certificaat importeren** pagina en klik vervolgens op controleren of dat Hallo-certificaat in de gewenste map Hallo **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Controleer of het certificaat bevindt zich in de juiste map Hallo](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="bf2c7-163">Er verschijnt een dialoogvenster, wordt Hallo geslaagde certificaat importeren bevestigd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="bf2c7-164">Meld u aan toohello vCenter Server tooconfirm dat de verbinding beveiligd is.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="bf2c7-165">Hallo certificaat importeren niet met succes is voltooid en u geen beveiligde verbinding kan maken, de documentatie als Hallo VMware vSphere op [servercertificaten](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="bf2c7-166">Als u beveiligde grenzen binnen uw organisatie hebben en tooturn op Hallo HTTPS-protocol niet wilt, gebruikt u hello te volgen procedure toodisable Hallo beveiligde communicatie.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="bf2c7-167">Beveiligde communicatieprotocol uitschakelen</span><span class="sxs-lookup"><span data-stu-id="bf2c7-167">Disable secure communication protocol</span></span>

<span data-ttu-id="bf2c7-168">Als uw organisatie niet Hallo HTTPS-protocol niet vereist, gebruik Hallo stappen toodisable HTTPS te volgen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="bf2c7-169">toodisable standaardgedrag hello, maakt u een registersleutel die Hallo standaardgedrag negeert.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="bf2c7-170">Kopieer en plak de volgende tekst in een txt-bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="bf2c7-171">Hallo bestand tooyour Azure Backup-Server computer opslaan.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="bf2c7-172">Gebruik voor Hallo bestandsnaam, DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="bf2c7-173">Dubbelklik op Hallo bestand tooactivate Hallo register-item.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="bf2c7-174">Een rol- en gebruikersaccount maakt op Hallo vCenter-Server</span><span class="sxs-lookup"><span data-stu-id="bf2c7-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="bf2c7-175">Hallo vcenter Server is een rol een vooraf gedefinieerde set met rechten.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="bf2c7-176">Een beheerder van de vCenter-Server maakt Hallo rollen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="bf2c7-177">tooassign machtigingen, Hallo beheerder paren gebruikersaccounts met een rol.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="bf2c7-178">tooestablish hello nodig gebruiker referenties tooback van Hallo vCenter Server-computer een rol maken met specifieke rechten, en vervolgens Hallo-gebruikersaccount te koppelen aan Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="bf2c7-179">Azure Backup-Server gebruikt een gebruikersnaam en wachtwoord tooauthenticate met Hallo vCenter-Server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="bf2c7-180">Azure Backup-Server gebruikt deze referenties als verificatie voor alle back-upbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="bf2c7-181">tooadd een vCenter Server-rol en de rechten voor de beheerder van een back-up:</span><span class="sxs-lookup"><span data-stu-id="bf2c7-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="bf2c7-182">Meld u aan in toohello vCenter-Server en klik vervolgens in Hallo vCenter-Server **Navigator** -scherm, klikt u op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Beheeroptie in vCenter Server Navigator Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="bf2c7-184">In **beheer** Selecteer **rollen**, en klik vervolgens in Hallo **rollen** Configuratiescherm klikt u op Hallo functiepictogram (symbool + Hallo) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Functie toevoegen](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="bf2c7-186">Hallo **rol maken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-186">hello **Create Role** dialog box appears.</span></span>

    ![Rol maken](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="bf2c7-188">In Hallo **rol maken** dialoogvenster in Hallo **rolnaam** Voer *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="bf2c7-189">Hallo rolnaam is wat u maar wilt, maar moet herkenbare voor doel Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="bf2c7-190">Hallo bevoegdheden voor de juiste versie van vCenter Hallo selecteren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="bf2c7-191">Hallo volgende tabel identificeert Hallo vereiste bevoegdheden voor vCenter 6.0 en vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="bf2c7-192">Wanneer u Hallo bevoegdheden selecteert, klikt u op Hallo pictogram volgende toohello bovenliggende label tooexpand Hallo bovenliggende en bekijkt hello onderliggende bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="bf2c7-193">tooselect hello VirtualMachine machtigingen beschikt, moet u toogo verschillende niveaus in Hallo bovenliggende/onderliggende hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="bf2c7-194">U hoeft niet tooselect alle onderliggende bevoegdheden binnen een bovenliggende-bevoegdheid.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Bovenliggende/onderliggende hiërarchie bevoegdheden](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="bf2c7-196">Nadat u op **OK**, Hallo nieuwe rol wordt weergegeven in de lijst Hallo op Hallo rollen Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="bf2c7-197">Bevoegdheden voor vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="bf2c7-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="bf2c7-198">Bevoegdheden voor vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="bf2c7-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="bf2c7-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="bf2c7-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="bf2c7-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="bf2c7-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="bf2c7-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="bf2c7-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="bf2c7-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="bf2c7-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="bf2c7-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="bf2c7-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="bf2c7-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="bf2c7-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="bf2c7-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="bf2c7-205">Network.Assign</span></span> |
|<span data-ttu-id="bf2c7-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="bf2c7-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="bf2c7-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="bf2c7-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="bf2c7-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="bf2c7-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="bf2c7-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="bf2c7-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="bf2c7-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="bf2c7-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="bf2c7-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="bf2c7-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="bf2c7-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="bf2c7-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="bf2c7-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="bf2c7-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="bf2c7-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="bf2c7-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="bf2c7-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="bf2c7-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="bf2c7-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="bf2c7-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="bf2c7-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="bf2c7-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="bf2c7-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="bf2c7-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="bf2c7-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="bf2c7-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="bf2c7-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="bf2c7-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="bf2c7-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="bf2c7-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="bf2c7-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="bf2c7-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="bf2c7-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="bf2c7-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="bf2c7-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="bf2c7-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="bf2c7-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="bf2c7-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="bf2c7-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="bf2c7-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="bf2c7-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="bf2c7-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="bf2c7-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="bf2c7-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="bf2c7-229">Maak een gebruikersaccount van de vCenter-Server en machtigingen</span><span class="sxs-lookup"><span data-stu-id="bf2c7-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="bf2c7-230">Nadat het Hallo-rol met bevoegdheden is ingesteld, moet u een gebruikersaccount maken.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="bf2c7-231">Hallo-gebruikersaccount heeft een naam en wachtwoord waarmee Hallo-referenties die worden gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="bf2c7-232">een gebruikersaccount in Hallo vCenter-Server toocreate **Navigator** -scherm, klikt u op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Optie voor gebruikers en groepen](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="bf2c7-234">Hallo **vCenter gebruikers en groepen** deelvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter gebruikers en groepen Configuratiescherm](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="bf2c7-236">In Hallo **vCenter gebruikers en groepen** Configuratiescherm, selecteer Hallo **gebruikers** tabblad en klik vervolgens op Hallo gebruikers-pictogram (symbool + Hallo) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="bf2c7-237">Hallo **nieuwe gebruiker** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="bf2c7-238">In Hallo **nieuwe gebruiker** dialoogvenster vak, Hallo gebruikersgegevens toevoegen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="bf2c7-239">In deze procedure is Hallo gebruikersnaam BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Dialoogvenster Nieuwe gebruiker](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="bf2c7-241">Hallo nieuwe gebruikersaccount wordt weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="bf2c7-242">tooassociate Hallo-gebruikersaccount met Hallo-rol, in Hallo **Navigator** -scherm, klikt u op **algemene machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="bf2c7-243">In Hallo **algemene machtigingen** Configuratiescherm, selecteer Hallo **beheren** tabblad en klik vervolgens op Hallo pictogram (symbool + Hallo) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Globale machtigingen Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="bf2c7-245">Hallo **globale machtigingen Root - machtiging toevoegen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="bf2c7-246">In Hallo **globale machtiging Root - machtiging toevoegen** in het dialoogvenster, klikt u op **toevoegen** toochoose Hallo gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Gebruiker of groep kiezen](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="bf2c7-248">Hallo **gebruikers/groepen selecteren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="bf2c7-249">In Hallo **gebruikers/groepen selecteren** dialoogvenster Kies **BackupAdmin** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="bf2c7-250">In **gebruikers**, Hallo *domein\gebruikersnaam* indeling wordt gebruikt voor het Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="bf2c7-251">Als u een ander domein toouse wilt, kiezen uit Hallo **domein** lijst.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![BackupAdmin gebruiker toevoegen](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="bf2c7-253">Klik op **OK** tooadd Hallo geselecteerd gebruikers toohello **machtiging toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="bf2c7-254">Nu dat u Hallo gebruiker hebt geïdentificeerd, toewijzen Hallo toohello gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="bf2c7-255">In **toegewezen rol**, selecteer in de vervolgkeuzelijst hello, **BackupAdminRole**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Gebruiker toorole toewijzen](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="bf2c7-257">Op Hallo **beheren** tabblad in Hallo **algemene machtigingen** deelvenster, Hallo nieuwe gebruikersaccount en Hallo gekoppeld rol wordt weergegeven in Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="bf2c7-258">Referenties van de vCenter-Server op Azure Backup-Server tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="bf2c7-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="bf2c7-259">Installeer voordat u Hallo VMware server tooAzure back-upserver toevoegt, [Update 1 voor Azure Backup-Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="bf2c7-260">tooopen Azure Backup-Server, dubbelklik op Hallo op Hallo Azure back-upserver bureaublad.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Pictogram voor Azure Backup-Server](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="bf2c7-262">Als u geen pictogram Hallo op Hallo bureaublad vinden, opent u Azure Backup-Server uit de lijst met geïnstalleerde apps Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="bf2c7-263">Hello Azure Backup-Server app-naam kan Microsoft Azure Backup wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="bf2c7-264">In de console hello Azure Backup-Server, klikt u op **Management**, klikt u op **productieservers**, en klik op het lint Hallo **beheren VMware**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Azure Backup-Server-console](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="bf2c7-266">Hallo **referenties beheren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="bf2c7-268">In Hallo **referenties beheren** in het dialoogvenster, klikt u op **toevoegen** tooopen hello **referentie toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="bf2c7-269">In Hallo **referentie toevoegen** dialoogvenster Voer een naam en beschrijving voor de nieuwe referentie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="bf2c7-270">Vervolgens Hallo gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-270">Then specify hello username and password.</span></span> <span data-ttu-id="bf2c7-271">Hallo-naam, *Contoso Vcenter referentie* wordt gebruikt tooidentify Hallo referentie in de volgende procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="bf2c7-272">Gebruik Hallo dezelfde gebruikersnaam en het wachtwoord dat wordt gebruikt voor Hallo vCenter-Server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="bf2c7-273">Als Hallo vCenter-Server en Azure Backup-Server zich niet in hetzelfde domein, Hallo **gebruikersnaam**, Hallo domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![In het dialoogvenster van Azure referentie van back-up-Server toevoegen](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="bf2c7-275">Klik op **toevoegen** tooadd Hallo nieuwe referentie tooAzure back-upserver.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="bf2c7-276">Hallo nieuwe referentie wordt weergegeven in de lijst Hallo in Hallo **referenties beheren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="bf2c7-278">Hallo tooclose **referenties beheren** dialoogvenster vak, klikt u op Hallo **X** in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="bf2c7-279">Hallo vCenter Server tooAzure back-upserver toevoegen</span><span class="sxs-lookup"><span data-stu-id="bf2c7-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="bf2c7-280">Wizard voor toevoegen van productie-Server is gebruikt tooadd hello vCenter Server tooAzure back-upserver.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="bf2c7-281">tooopen productie-Wizard voor het toevoegen van Server, volledige Hallo procedure te volgen:</span><span class="sxs-lookup"><span data-stu-id="bf2c7-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="bf2c7-282">Klik in hello Azure Backup-Server console **Management**, klikt u op **productieservers**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![De Wizard openen productie Server toevoegen](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="bf2c7-284">Hallo **productie Server toevoeging Wizard** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Wizard voor productie-Server toevoegen](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="bf2c7-286">Op Hallo **productieserver Selecteer type** pagina **VMware Servers**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="bf2c7-287">In **Server naam of het IP-adres**, Hallo volledig gekwalificeerde domeinnaam (FQDN) of IP-adres van Hallo VMware-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="bf2c7-288">Als alle Hallo ESXi-servers worden beheerd door Hallo dezelfde vCenter, kunt u Hallo vCenter naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![VMware server FQDN of IP-adres opgeven](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="bf2c7-290">In **SSL-poort**, Voer Hallo-poort die wordt gebruikt toocommunicate met Hallo VMware-server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="bf2c7-291">Gebruik van poort 443, de standaardpoort hello, is tenzij u zeker weet dat een andere poort vereist is.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="bf2c7-292">In **Geef referentie**, selecteer Hallo referentie die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Geef referenties](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="bf2c7-294">Klik op **toevoegen** tooadd Hallo VMware toohello lijst met servers van **VMware-Servers toegevoegd**, en klik vervolgens op **volgende** toomove toohello volgende pagina in Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![VMWare-server en referentie toevoegen](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="bf2c7-296">In Hallo **samenvatting** pagina, klikt u op **toevoegen** tooadd Hallo opgegeven VMware server tooAzure back-upserver.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![VMware server tooAzure back-upserver toevoegen](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="bf2c7-298">Hallo VMware server back-up is een zonder agent back-up en de nieuwe server Hallo onmiddellijk wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="bf2c7-299">Hallo **voltooien** pagina toont Hallo van resultaten.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-299">hello **Finish** page shows you hello results.</span></span>

  ![Voltooiingspagina](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="bf2c7-301">tooadd meerdere exemplaren van vCenter Server tooAzure back-upserver, herhaaldelijk Hallo vorige stappen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="bf2c7-302">Nadat u Hallo vCenter Server tooAzure back-upserver toevoegt, is de volgende stap Hallo toocreate een beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="bf2c7-303">Hallo-beveiligingsgroep geeft Hallo verschillende details voor de korte of lange bewaarperiode en waar u definiëren en toepassen van de back-upbeleid Hallo is.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="bf2c7-304">back-upbeleid Hallo is Hallo planning voor wanneer de back-ups uitgevoerd en waarvan een back-is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="bf2c7-305">Configureer een beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="bf2c7-305">Configure a protection group</span></span>

<span data-ttu-id="bf2c7-306">Als u System Center Data Protection Manager of Azure Backup-Server voordat u niet hebt gebruikt, raadpleegt u [plannen voor back-ups van schijf](https://technet.microsoft.com/library/hh758026.aspx) tooprepare uw hardware-omgeving.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="bf2c7-307">Nadat u hebt gecontroleerd dat u de juiste opslag hebt, gebruik Hallo nieuwe beveiligingsgroep maken wizard tooadd virtuele VMware-machines.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="bf2c7-308">In de console hello Azure Backup-Server, klikt u op **beveiliging**, en klik in het lint Hallo op **nieuw** tooopen Hallo nieuwe beveiligingsgroep maken wizard.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Wizard Open Hallo-nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="bf2c7-310">Hallo **nieuwe beveiligingsgroep maken** in het dialoogvenster wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Dialoogvenster voor wizard nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="bf2c7-312">Klik op **volgende** tooadvance toohello **type beveiligingsgroep selecteren** pagina.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="bf2c7-313">Op Hallo **Selecteer type beveiligingsgroep** pagina **Servers** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="bf2c7-314">Hallo **groepsleden selecteren** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="bf2c7-315">Op Hallo **groepsleden selecteren** pagina, de beschikbare leden Hallo en Hallo geselecteerde leden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="bf2c7-316">Selecteer Hallo leden wilt tooprotect en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="bf2c7-318">Wanneer u een lid, selecteert als u een map met andere mappen of virtuele machines selecteert, worden de mappen en virtuele machines ook geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="bf2c7-319">Hallo insluiting Hallo mappen en virtuele machines in Hallo bovenliggende map heet mapniveau beveiliging.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="bf2c7-320">tooremove een map of virtuele machine, wissen Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="bf2c7-321">Als een virtuele machine of een map met een VM al beveiligd tooAzure is, niet worden geselecteerd die virtuele machine opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="bf2c7-322">Dat wil zeggen, nadat een virtuele machine beveiligd tooAzure is, worden niet beveiligd, waarmee wordt voorkomen dat dubbele herstelpunten worden gemaakt voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="bf2c7-323">Als u wilt dat toosee beveiligt welk exemplaar van Azure Backup-Server al een lid, punt toohello toosee Hallo lidnaam Hallo server beveiligt.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="bf2c7-324">Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voer een naam voor de beveiligingsgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="bf2c7-325">Beveiliging op korte termijn (toodisk) en online beveiliging zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="bf2c7-326">Als u wilt toouse online beveiliging (tooAzure), moet u kortdurende beveiliging toodisk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="bf2c7-327">Klik op **volgende** tooproceed toohello kortdurende beveiliging bereik.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="bf2c7-329">Op Hallo **Kortetermijndoelen opgeven** pagina voor **bewaartermijn**, geef het aantal dagen dat u wilt tooretain herstelpunten Hallo zijn *toodisk opgeslagen*.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="bf2c7-330">Als u wilt dat toochange Hallo tijd en de dagen waarop herstelpunten worden gemaakt, klikt u op **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="bf2c7-331">Hallo op korte termijn herstelpunten zijn volledige back-ups.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="bf2c7-332">Ze zijn geen incrementele back-ups.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-332">They are not incremental backups.</span></span> <span data-ttu-id="bf2c7-333">Wanneer u tevreden met korte-termijndoelstellingen hello bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="bf2c7-335">Op Hallo **Schijftoewijzing controleren** controleert en wijzig indien nodig Hallo schijfruimte beschikbaar voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="bf2c7-336">Hallo aanbevolen schijftoewijzingen zijn gebaseerd op Hallo bewaartermijn die is opgegeven in Hallo **Kortetermijndoelen opgeven** pagina Hallo type werkbelasting en de grootte Hallo Hallo van beveiligde gegevens (aangeduid in stap 3).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="bf2c7-337">**Gegevensgrootte:** grootte van de gegevens in de beveiligingsgroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="bf2c7-338">**Schijfruimte:** Hallo aanbevolen hoeveelheid schijfruimte voor de beveiligingsgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="bf2c7-339">Als u deze instelling toomodify wilt, moet u de totale ruimte die groter is dan Hallo bedrag in dat u een schatting maken van dat elke gegevensbron groeit toewijzen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="bf2c7-340">**Gegevens plaatsen:** als u collocatie inschakelt, op meerdere gegevensbronnen Hallo beveiliging tooa één replica en herstelpuntvolume kunnen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="bf2c7-341">Collocatie wordt niet ondersteund voor alle werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="bf2c7-342">**Automatisch vergroten:** als u voor deze instelling inschakelt als gegevens in de groep beveiligde Hallo groter worden dan de aanvankelijke toewijzing hello, System Center Data Protection Manager tooincrease Hallo schijfgrootte probeert met 25 procent.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="bf2c7-343">**Opslaggroepdetails:** toont de status Hallo van Hallo opslaggroep aanwezig zijn, waaronder de totale en resterende schijfgrootte.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Schijftoewijzing controleren](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="bf2c7-345">Wanneer u tevreden met de ruimtetoewijzing hello bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="bf2c7-346">Op Hallo **methode voor maken van selecteren Replica** pagina, Geef op hoe u toogenerate Hallo eerste kopie of replica van Hallo beveiligde gegevens op Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="bf2c7-347">Hallo standaardwaarde is **automatisch via netwerk Hallo** en **nu**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="bf2c7-348">Als u Hallo standaard gebruikt, raden wij aan dat u een tijdstip buiten de piekuren opgeeft.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="bf2c7-349">Kies **Later** en geef een dag en tijd.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="bf2c7-350">Voor grote hoeveelheden gegevens of minder dan optimale netwerkomstandigheden, kunt u Hallo gegevens offline repliceren met behulp van verwijderbare media.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="bf2c7-351">Nadat u uw keuzes hebt aangebracht, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-351">After you have made your choices, click **Next**.</span></span>

    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="bf2c7-353">Op Hallo **opties voor consistentiecontrole** pagina hoe en wanneer tooautomate Hallo consistentiecontroles.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="bf2c7-354">Wanneer de gerepliceerde gegevens inconsistent, of volgens een vooropgezet schema, kunt u consistentiecontroles uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="bf2c7-355">Als u niet tooconfigure automatische consistentiecontroles wilt, kunt u een handmatige controle uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="bf2c7-356">Met de rechtermuisknop op de beveiligingsgroep Hallo in Hallo beveiliging gebied hello Azure Backup-Server-console, en selecteer vervolgens **consistentiecontrole uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="bf2c7-357">Klik op **volgende** toomove toohello volgende pagina.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="bf2c7-358">Op Hallo **gegevens voor Online beveiliging opgeven** pagina, selecteert u een of meer gegevensbronnen die u tooprotect wilt.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="bf2c7-359">Hallo leden afzonderlijk selecteren of klik op **Alles selecteren** toochoose alle leden.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="bf2c7-360">Nadat u ervoor Hallo leden kiest, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-360">After you choose hello members, click **Next**.</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="bf2c7-362">Op Hallo **onlineback-upschema opgeven** pagina, Hallo planning toogenerate herstelpunten Hallo schijfback-up opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="bf2c7-363">Nadat het Hallo herstelpunt dat is gegenereerd, is het overgebrachte toohello Recovery Services-kluis in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="bf2c7-364">Wanneer u tevreden met online back-upschema hello bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="bf2c7-366">Op Hallo **Online bewaarbeleid opgeven** pagina, geeft u aan hoe lang u tooretain Hallo back-upgegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="bf2c7-367">Nadat het Hallo-beleid is gedefinieerd, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-367">After hello policy is defined, click **Next**.</span></span>

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="bf2c7-369">Er is geen tijdslimiet voor hoe lang van gegevens in Azure bewaren.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="bf2c7-370">Wanneer u herstelpuntgegevens in Azure opslaat, hello alleen limiet is dat er geen meer dan 9999 herstelpunten per beveiligde exemplaar.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="bf2c7-371">In dit voorbeeld is het beveiligde exemplaar Hallo Hallo VMware-server.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="bf2c7-372">Op Hallo **samenvatting** pagina, Hallo details bekijken voor de leden van de beveiligingsgroep en de instellingen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="bf2c7-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Een lid van beveiligingsgroep en samenvatting van de instelling](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="bf2c7-374">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf2c7-374">Next steps</span></span>
<span data-ttu-id="bf2c7-375">Als u Azure Backup-Server tooprotect VMware werkbelastingen gebruikt, hebt u mogelijk geïnteresseerd in met behulp van Azure Backup-Server beveiligen toohelp een [Microsoft Exchange-server](./backup-azure-exchange-mabs.md), een [Microsoft SharePoint-farm](./backup-azure-backup-sharepoint-mabs.md), of een [SQL Server-database](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="bf2c7-376">Zie voor informatie over problemen met het Hallo-agent registreren, Hallo beveiligingsgroep configureert of back-ups van taken, [problemen met Azure Backup-Server](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="bf2c7-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
