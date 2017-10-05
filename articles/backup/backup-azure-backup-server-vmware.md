---
title: Maak een back-up van VMware-servers met Azure Backup-Server | Microsoft Docs
description: Azure Backup Server gebruiken om back-up van een VMware vCenter/ESXi-servers naar Azure of de schijf. In dit artikel wordt stap voor-stap instructies voor back-ups maken (of beveiligen) = uw VMware-werkbelastingen.
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
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="d3024-104">Back-up van een VMware-server naar Azure</span><span class="sxs-lookup"><span data-stu-id="d3024-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="d3024-105">In dit artikel wordt uitgelegd hoe Azure back-up-Server configureren om VMware server-werkbelasting beveiligen.</span><span class="sxs-lookup"><span data-stu-id="d3024-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="d3024-106">In dit artikel wordt ervan uitgegaan dat u hebt al Azure Backup-Server is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d3024-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="d3024-107">Als u geen Azure Backup-Server is geïnstalleerd, raadpleegt u [voorbereiden op back-up van werkbelastingen met Azure Backup-Server](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d3024-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="d3024-108">Azure Backup-Server kunnen back-up maken of te beschermen, VMware vCenter-serverversie 6.5, 6.0 en 5.5.</span><span class="sxs-lookup"><span data-stu-id="d3024-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="d3024-109">Maken van een beveiligde verbinding met de vCenter-Server</span><span class="sxs-lookup"><span data-stu-id="d3024-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="d3024-110">Standaard communiceert Azure Backup-Server met elk vCenter-Server via een HTTPS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="d3024-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="d3024-111">Als u wilt inschakelen op de beveiligde communicatie, wordt u aangeraden om het certificaat VMware certificeringsinstantie (CA) van de computer te installeren op Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="d3024-112">Als u geen veilige communicatie vereist en u gebruiken wilt om de vereiste HTTPS te schakelen, Zie [uitschakelen beveiligde communicatieprotocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="d3024-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="d3024-113">Importeer het vertrouwde certificaat op de Azure Backup-Server voor het maken van een beveiligde verbinding tussen Azure Backup-Server en de vCenter-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="d3024-114">Doorgaans kunt u een browser op de machine van Azure Backup-Server verbinding maken met de vCenter-Server via de vSphere webclient.</span><span class="sxs-lookup"><span data-stu-id="d3024-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="d3024-115">De eerste keer dat u de browser van de Azure Backup-Server gebruiken voor verbinding met de vCenter-Server, de verbinding is niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="d3024-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="d3024-116">De volgende afbeelding toont de niet-beveiligde verbinding.</span><span class="sxs-lookup"><span data-stu-id="d3024-116">The following image shows the unsecured connection.</span></span>

![Voorbeeld van een niet-beveiligde verbinding met de VMware-server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="d3024-118">U kunt dit probleem oplossen en een beveiligde verbinding maken, downloaden de vertrouwde basis-CA-certificaten.</span><span class="sxs-lookup"><span data-stu-id="d3024-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="d3024-119">Voer de URL naar de vSphere webclient in de browser op Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="d3024-120">De vSphere webclient-aanmeldingspagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-120">The vSphere Web Client login page appears.</span></span>

    ![vSphere webclient](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="d3024-122">Zoek aan de onderkant van de informatie voor beheerders en ontwikkelaars de **downloaden vertrouwde basis-CA-certificaten** koppeling.</span><span class="sxs-lookup"><span data-stu-id="d3024-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Koppeling voor het downloaden van de vertrouwde basis-CA-certificaten](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="d3024-124">Als u de aanmeldingspagina van vSphere webclient niet ziet, controleert u de proxy-instellingen van uw browser.</span><span class="sxs-lookup"><span data-stu-id="d3024-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="d3024-125">Klik op **downloaden vertrouwde basis-CA-certificaten**.</span><span class="sxs-lookup"><span data-stu-id="d3024-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="d3024-126">De vCenter-Server downloadt een bestand op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d3024-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="d3024-127">Naam van het bestand met de naam **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="d3024-127">The file's name is named **download**.</span></span> <span data-ttu-id="d3024-128">Afhankelijk van uw browser ontvangt u een bericht waarin wordt gevraagd of u wilt openen of opslaan van het bestand.</span><span class="sxs-lookup"><span data-stu-id="d3024-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![bericht downloaden wanneer certificaten worden gedownload.](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="d3024-130">Sla het bestand naar een locatie op de Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="d3024-131">Wanneer u het bestand opslaat, voeg de extensie .zip.</span><span class="sxs-lookup"><span data-stu-id="d3024-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="d3024-132">Het bestand is een ZIP-bestand met de informatie over certificaten.</span><span class="sxs-lookup"><span data-stu-id="d3024-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="d3024-133">U kunt de extractie-hulpprogramma's gebruiken met de extensie .zip.</span><span class="sxs-lookup"><span data-stu-id="d3024-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="d3024-134">Met de rechtermuisknop op **download.zip**, en selecteer vervolgens **Alles uitpakken** om de inhoud te extraheren.</span><span class="sxs-lookup"><span data-stu-id="d3024-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="d3024-135">Het ZIP-bestand extraheert inhoud naar een map met de naam ervan **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="d3024-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="d3024-136">Twee typen bestanden worden weergegeven in de map certificaten.</span><span class="sxs-lookup"><span data-stu-id="d3024-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="d3024-137">Het basiscertificaatbestand heeft een extensie die met een genummerde volgorde zoals.0 en.1 begint.</span><span class="sxs-lookup"><span data-stu-id="d3024-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="d3024-138">Het CRL-bestand heeft een extensie die met een reeks zoals .r0 of .r1 begint.</span><span class="sxs-lookup"><span data-stu-id="d3024-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="d3024-139">Het CRL-bestand is gekoppeld aan een certificaat.</span><span class="sxs-lookup"><span data-stu-id="d3024-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="d3024-140">Lokaal uitgepakt bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="d3024-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="d3024-141">In de **certificaten** map met de rechtermuisknop op het bestand voor het basiscertificaat en klik vervolgens op **naam**.</span><span class="sxs-lookup"><span data-stu-id="d3024-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="d3024-142">Wijzig de naam van basiscertificaat</span><span class="sxs-lookup"><span data-stu-id="d3024-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="d3024-143">Wijzig het basiscertificaat uitbreiding in .crt.</span><span class="sxs-lookup"><span data-stu-id="d3024-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="d3024-144">Als u wordt gevraagd als u zeker dat u wilt wijzigen van de extensie, klikt u op **Ja** of **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3024-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="d3024-145">Anders kunt u de juiste functie van het bestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d3024-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="d3024-146">Het pictogram voor het bestand is gewijzigd in een pictogram dat een basiscertificaat vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="d3024-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="d3024-147">Met de rechtermuisknop op het basiscertificaat en selecteer in het pop-upmenu **certificaat installeren**.</span><span class="sxs-lookup"><span data-stu-id="d3024-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="d3024-148">De **Wizard Certificaat importeren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="d3024-149">In de **Wizard Certificaat importeren** dialoogvenster, **lokale Machine** als bestemming voor het certificaat en klik vervolgens op **volgende** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="d3024-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="d3024-150">Certificaat bestemming opslagopties</span><span class="sxs-lookup"><span data-stu-id="d3024-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="d3024-151">Als u wordt gevraagd als u toestaan dat de computer gewijzigd wilt, klikt u op **Ja** of **OK**, naar alle wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d3024-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="d3024-152">Op de **certificaatarchief** pagina **alle certificaten in het onderstaande archief plaatsen**, en klik vervolgens op **Bladeren** kiezen van het certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="d3024-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Certificaten in een bepaalde opslag-positie plaatsen](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="d3024-154">De **certificaatarchief selecteren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Map van de certificaathiërarchie opslag](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="d3024-156">Selecteer **Trusted Root Certification Authorities** als doelmap voor de certificaten en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3024-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Certificaat-doelmap](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="d3024-158">De **Trusted Root Certification Authorities** map wordt bevestigd dat het certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="d3024-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="d3024-159">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-159">Click **Next**.</span></span>

    ![Archiefmap certificaat](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="d3024-161">Op de **de wizard Certificaat importeren** pagina, Controleer of het certificaat is in de gewenste map en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d3024-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Controleer of het certificaat bevindt zich in de juiste map](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="d3024-163">Een dialoogvenster wordt weergegeven, wordt bevestigd dat het importeren van het certificaat is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="d3024-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="d3024-164">Meld u aan de vCenter-Server om te bevestigen dat de verbinding beveiligd is.</span><span class="sxs-lookup"><span data-stu-id="d3024-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="d3024-165">Als het certificaat importeren niet geslaagd is en u geen beveiligde verbinding kan maken, raadpleegt u de VMware vSphere-documentatie op [servercertificaten](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="d3024-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="d3024-166">Als u beveiligde grenzen binnen uw organisatie hebben en niet wilt dat het HTTPS-protocol inschakelen, gebruikt u de volgende procedure uitschakelen van de beveiligde communicatie.</span><span class="sxs-lookup"><span data-stu-id="d3024-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="d3024-167">Beveiligde communicatieprotocol uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d3024-167">Disable secure communication protocol</span></span>

<span data-ttu-id="d3024-168">Als uw organisatie kan het HTTPS-protocol niet vereist, gebruik de volgende stappen uit om uit te schakelen van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3024-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="d3024-169">Schakel het standaardgedrag een registersleutel die het standaardgedrag negeert te maken.</span><span class="sxs-lookup"><span data-stu-id="d3024-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="d3024-170">Kopieer en plak de volgende tekst in een txt-bestand.</span><span class="sxs-lookup"><span data-stu-id="d3024-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="d3024-171">Sla het bestand op uw computer Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="d3024-172">Gebruik voor de bestandsnaam DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="d3024-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="d3024-173">Dubbelklik op het bestand voor het activeren van het register-item.</span><span class="sxs-lookup"><span data-stu-id="d3024-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="d3024-174">Een rol- en gebruikersaccount maakt op de vCenter-Server</span><span class="sxs-lookup"><span data-stu-id="d3024-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="d3024-175">Op de vCenter-Server is een rol een vooraf gedefinieerde set met rechten.</span><span class="sxs-lookup"><span data-stu-id="d3024-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="d3024-176">Een beheerder van de vCenter-Server maakt de rollen.</span><span class="sxs-lookup"><span data-stu-id="d3024-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="d3024-177">De beheerder paren als machtigingen wilt toewijzen, gebruikersaccounts met een rol.</span><span class="sxs-lookup"><span data-stu-id="d3024-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="d3024-178">Een gebruikersrol maakt met bevoegdheden om vast te stellen de benodigde gebruikersreferenties naar de back-up van de vCenter-Server-computer, en vervolgens het gebruikersaccount wilt koppelen aan de rol.</span><span class="sxs-lookup"><span data-stu-id="d3024-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="d3024-179">Azure Backup-Server gebruikt een gebruikersnaam en wachtwoord voor verificatie met de vCenter-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="d3024-180">Azure Backup-Server gebruikt deze referenties als verificatie voor alle back-upbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d3024-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="d3024-181">Een vCenter-Server-rol en de bevoegdheden voor een back-upadministrator toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d3024-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="d3024-182">Meld u aan met de vCenter-Server en vervolgens in de vCenter-Server **Navigator** -scherm, klikt u op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="d3024-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Beheeroptie in vCenter Server Navigator Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="d3024-184">In **beheer** Selecteer **rollen**, en klik vervolgens in de **rollen** Configuratiescherm klikt u op het pictogram van de rol toevoegen (het symbool +).</span><span class="sxs-lookup"><span data-stu-id="d3024-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Functie toevoegen](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="d3024-186">De **rol maken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-186">The **Create Role** dialog box appears.</span></span>

    ![Rol maken](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="d3024-188">In de **rol maken** het dialoogvenster de **rolnaam** Voer *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="d3024-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="d3024-189">De rolnaam kan niet wat u maar wilt, maar deze moet herkenbare voor doel van de rol.</span><span class="sxs-lookup"><span data-stu-id="d3024-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="d3024-190">Selecteer de bevoegdheden voor de juiste versie van vCenter en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3024-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="d3024-191">De volgende tabel bevat de vereiste machtigingen voor vCenter 6.0 en vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="d3024-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="d3024-192">Wanneer u de bevoegdheden selecteert, klikt u op het pictogram naast het bovenliggende label uitbreiden van de bovenliggende en onderliggende bevoegdheden weergeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="d3024-193">Schakel de bevoegdheden van de virtuele machine, moet u verschillende niveaus in de bovenliggende/onderliggende hiërarchie gaan.</span><span class="sxs-lookup"><span data-stu-id="d3024-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="d3024-194">U hoeft niet te selecteren van alle onderliggende bevoegdheden binnen een bovenliggende bevoegdheid.</span><span class="sxs-lookup"><span data-stu-id="d3024-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Bovenliggende/onderliggende hiërarchie bevoegdheden](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="d3024-196">Nadat u op **OK**, de nieuwe functie in de lijst in het deelvenster functies weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="d3024-197">Bevoegdheden voor vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="d3024-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="d3024-198">Bevoegdheden voor vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="d3024-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="d3024-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="d3024-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="d3024-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="d3024-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="d3024-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="d3024-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="d3024-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="d3024-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="d3024-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="d3024-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="d3024-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="d3024-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="d3024-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="d3024-205">Network.Assign</span></span> |
|<span data-ttu-id="d3024-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="d3024-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="d3024-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="d3024-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="d3024-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="d3024-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="d3024-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="d3024-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="d3024-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="d3024-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="d3024-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="d3024-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="d3024-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="d3024-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="d3024-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="d3024-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="d3024-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="d3024-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="d3024-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="d3024-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="d3024-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="d3024-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="d3024-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="d3024-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="d3024-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="d3024-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="d3024-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="d3024-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="d3024-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="d3024-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="d3024-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="d3024-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="d3024-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="d3024-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="d3024-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="d3024-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="d3024-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="d3024-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="d3024-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="d3024-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="d3024-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="d3024-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="d3024-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="d3024-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="d3024-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="d3024-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="d3024-229">Maak een gebruikersaccount van de vCenter-Server en machtigingen</span><span class="sxs-lookup"><span data-stu-id="d3024-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="d3024-230">Nadat de rol met bevoegdheden is ingesteld, moet u een gebruikersaccount maken.</span><span class="sxs-lookup"><span data-stu-id="d3024-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="d3024-231">Het gebruikersaccount heeft een naam en wachtwoord waarmee u de referenties die worden gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="d3024-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="d3024-232">Maken van een gebruikersaccount in de vCenter-Server **Navigator** -scherm, klikt u op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d3024-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Optie voor gebruikers en groepen](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="d3024-234">De **vCenter gebruikers en groepen** deelvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter gebruikers en groepen Configuratiescherm](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="d3024-236">In de **vCenter gebruikers en groepen** Configuratiescherm, selecteer de **gebruikers** tabblad en klik vervolgens op het pictogram van de gebruikers toevoegen (het symbool +).</span><span class="sxs-lookup"><span data-stu-id="d3024-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="d3024-237">De **nieuwe gebruiker** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="d3024-238">In de **nieuwe gebruiker** dialoogvenster vak, gegevens van de gebruiker toevoegen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3024-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="d3024-239">De gebruikersnaam is in deze procedure BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="d3024-239">In this procedure, the username is BackupAdmin.</span></span>

    ![Dialoogvenster Nieuwe gebruiker](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="d3024-241">Het nieuwe gebruikersaccount wordt weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="d3024-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="d3024-242">Het gebruikersaccount koppelen aan de rol, in de **Navigator** -scherm, klikt u op **algemene machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="d3024-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="d3024-243">In de **algemene machtigingen** Configuratiescherm, selecteer de **beheren** tabblad en klik vervolgens op het pictogram toevoegen (het symbool +).</span><span class="sxs-lookup"><span data-stu-id="d3024-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Globale machtigingen Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="d3024-245">De **globale machtigingen Root - machtiging toevoegen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="d3024-246">In de **globale machtiging Root - machtiging toevoegen** in het dialoogvenster, klikt u op **toevoegen** kiezen van de gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="d3024-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Gebruiker of groep kiezen](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="d3024-248">De **gebruikers/groepen selecteren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="d3024-249">In de **gebruikers/groepen selecteren** dialoogvenster Kies **BackupAdmin** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d3024-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="d3024-250">In **gebruikers**, wordt de *domein\gebruikersnaam* indeling wordt gebruikt voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="d3024-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="d3024-251">Als u gebruiken een ander domein wilt, kiest u uit de **domein** lijst.</span><span class="sxs-lookup"><span data-stu-id="d3024-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![BackupAdmin gebruiker toevoegen](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="d3024-253">Klik op **OK** de geselecteerde gebruikers toevoegen aan de **machtiging toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3024-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="d3024-254">Nu dat u hebt vastgesteld dat de gebruiker, wordt de gebruiker toewijzen aan de rol.</span><span class="sxs-lookup"><span data-stu-id="d3024-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="d3024-255">In **toegewezen rol**, selecteer in de vervolgkeuzelijst **BackupAdminRole**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3024-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Gebruiker toewijzen aan rol](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="d3024-257">Op de **beheren** tabblad de **algemene machtigingen** deelvenster, het nieuwe gebruikersaccount en de bijbehorende functieservices weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="d3024-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="d3024-258">Referenties van de vCenter-Server op Azure Backup-Server tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="d3024-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="d3024-259">Installeer voordat u de VMware-server aan Azure Backup-Server toevoegen, [Update 1 voor Azure Backup-Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="d3024-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="d3024-260">Om te openen in Azure Backup-Server, dubbelklikt u op het pictogram op het bureaublad van de Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Pictogram voor Azure Backup-Server](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="d3024-262">Als u het pictogram niet op het bureaublad vinden, opent u de Azure Backup-Server in de lijst met geïnstalleerde apps.</span><span class="sxs-lookup"><span data-stu-id="d3024-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="d3024-263">De naam van de app Azure Backup-Server, Microsoft Azure Backup wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="d3024-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="d3024-264">Klik in de console Azure Backup-Server op **Management**, klikt u op **productieservers**, en klik vervolgens op het lint op **beheren VMware**.</span><span class="sxs-lookup"><span data-stu-id="d3024-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Azure Backup-Server-console](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="d3024-266">De **referenties beheren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="d3024-268">In de **referenties beheren** in het dialoogvenster, klikt u op **toevoegen** openen de **referentie toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3024-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="d3024-269">In de **referentie toevoegen** dialoogvenster Voer een naam en beschrijving voor de nieuwe referentie.</span><span class="sxs-lookup"><span data-stu-id="d3024-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="d3024-270">Geef vervolgens de gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d3024-270">Then specify the username and password.</span></span> <span data-ttu-id="d3024-271">De naam van de *Contoso Vcenter referentie* wordt gebruikt voor het identificeren van de referentie in de volgende procedure.</span><span class="sxs-lookup"><span data-stu-id="d3024-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="d3024-272">Gebruik dezelfde gebruikersnaam en wachtwoord dat wordt gebruikt voor de vCenter-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="d3024-273">Als de vCenter-Server en de Azure Backup-Server zich niet in hetzelfde domein in **gebruikersnaam**, geef het domein.</span><span class="sxs-lookup"><span data-stu-id="d3024-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![In het dialoogvenster van Azure referentie van back-up-Server toevoegen](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="d3024-275">Klik op **toevoegen** nieuwe referentie toevoegen aan Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="d3024-276">De nieuwe referentie wordt weergegeven in de lijst in de **referenties beheren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3024-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="d3024-278">Sluiten de **referenties beheren** in het dialoogvenster, klikt u op de **X** in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="d3024-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="d3024-279">De vCenter-Server toevoegen aan Azure Backup-Server</span><span class="sxs-lookup"><span data-stu-id="d3024-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="d3024-280">Wizard voor toevoegen van productie-Server wordt gebruikt voor de vCenter-Server toevoegen aan Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="d3024-281">Productie-Server toevoegen om Wizard te openen, voert u de volgende procedure:</span><span class="sxs-lookup"><span data-stu-id="d3024-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="d3024-282">Klik in de console Azure Backup-Server op **Management**, klikt u op **productieservers**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d3024-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![De Wizard openen productie Server toevoegen](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="d3024-284">De **productie Server toevoeging Wizard** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Wizard voor productie-Server toevoegen](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="d3024-286">Op de **productieserver Selecteer type** pagina **VMware Servers**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="d3024-287">In **Server naam of het IP-adres**, geef de volledig gekwalificeerde domeinnaam (FQDN) of IP-adres van de VMware-server.</span><span class="sxs-lookup"><span data-stu-id="d3024-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="d3024-288">Als alle ESXi-servers worden beheerd met dezelfde vCenter, kunt u de vCenter-naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3024-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![VMware server FQDN of IP-adres opgeven](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="d3024-290">In **SSL-poort**, geef de poort die wordt gebruikt om te communiceren met de VMware-server.</span><span class="sxs-lookup"><span data-stu-id="d3024-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="d3024-291">Gebruik van poort 443, de standaardpoort, is tenzij u zeker weet dat een andere poort vereist is.</span><span class="sxs-lookup"><span data-stu-id="d3024-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="d3024-292">In **Geef referentie**, selecteert u de referenties die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3024-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Geef referenties](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="d3024-294">Klik op **toevoegen** VMware server toevoegen aan de lijst met **VMware-Servers toegevoegd**, en klik vervolgens op **volgende** verplaatsen naar de volgende pagina in de wizard.</span><span class="sxs-lookup"><span data-stu-id="d3024-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![VMWare-server en referentie toevoegen](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="d3024-296">In de **samenvatting** pagina, klikt u op **toevoegen** de opgegeven VMware-server toevoegen aan Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![VMware-server toevoegen aan Azure Backup-Server](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="d3024-298">De VMware-server back-up is een zonder agent back-up en de nieuwe server onmiddellijk wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d3024-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="d3024-299">De **voltooien** pagina ziet u de resultaten.</span><span class="sxs-lookup"><span data-stu-id="d3024-299">The **Finish** page shows you the results.</span></span>

  ![Voltooiingspagina](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="d3024-301">Herhaal de vorige stappen in deze sectie u meerdere exemplaren van de vCenter-Server toevoegen aan Azure Backup-Server door.</span><span class="sxs-lookup"><span data-stu-id="d3024-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="d3024-302">Nadat u de vCenter-Server aan Azure Backup-Server toevoegen, wordt de volgende stap is het maken van een beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="d3024-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="d3024-303">De beveiligingsgroep bevat de verschillende details voor de korte of lange bewaarperiode en waar u definiëren en de back-upbeleid van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="d3024-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="d3024-304">Het back-upbeleid is de planning voor wanneer de back-ups uitgevoerd en waarvan een back-is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3024-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="d3024-305">Configureer een beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="d3024-305">Configure a protection group</span></span>

<span data-ttu-id="d3024-306">Als u System Center Data Protection Manager of Azure Backup-Server voordat u niet hebt gebruikt, raadpleegt u [plannen voor back-ups van schijf](https://technet.microsoft.com/library/hh758026.aspx) voorbereiden van uw hardware-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d3024-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="d3024-307">Nadat u hebt gecontroleerd dat u de juiste opslag hebt, moet u de wizard nieuwe beveiligingsgroep maken gebruiken om toe te voegen virtuele VMware-machines.</span><span class="sxs-lookup"><span data-stu-id="d3024-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="d3024-308">Klik in de console Azure Backup-Server op **beveiliging**, en klik in het lint op **nieuw** om de wizard nieuwe beveiligingsgroep maken te openen.</span><span class="sxs-lookup"><span data-stu-id="d3024-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Open de wizard nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="d3024-310">De **nieuwe beveiligingsgroep maken** in het dialoogvenster wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Dialoogvenster voor wizard nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="d3024-312">Klik op **volgende** om door te gaan naar de **type beveiligingsgroep selecteren** pagina.</span><span class="sxs-lookup"><span data-stu-id="d3024-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="d3024-313">Op de **Selecteer type beveiligingsgroep** pagina **Servers** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="d3024-314">De **groepsleden selecteren** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="d3024-315">Op de **groepsleden selecteren** pagina, de beschikbare leden en de geselecteerde leden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3024-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="d3024-316">Selecteer de leden die u wilt beveiligen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="d3024-318">Wanneer u een lid, selecteert als u een map met andere mappen of virtuele machines selecteert, worden de mappen en virtuele machines ook geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d3024-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="d3024-319">Het opnemen van de mappen en virtuele machines in de bovenliggende map heet mapniveau beveiliging.</span><span class="sxs-lookup"><span data-stu-id="d3024-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="d3024-320">Schakel het selectievakje voor het verwijderen van een map of een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d3024-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="d3024-321">Als een virtuele machine of een map met een VM is al beveiligd naar Azure, niet worden geselecteerd die virtuele machine opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d3024-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="d3024-322">Dat wil zeggen, nadat een virtuele machine is beveiligd met Azure, worden niet beveiligd, waarmee wordt voorkomen dat dubbele herstelpunten worden gemaakt voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d3024-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="d3024-323">Als u zien welk exemplaar van Azure Backup-Server beveiligt al lid is wilt, wijst u het lid om te zien van de naam van de server beschermen.</span><span class="sxs-lookup"><span data-stu-id="d3024-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="d3024-324">Op de **methode voor gegevensbeveiliging selecteren** pagina, voer een naam voor de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="d3024-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="d3024-325">Beveiliging op korte termijn (naar schijf) en online beveiliging zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d3024-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="d3024-326">Als u wilt gebruiken van online beveiliging (naar Azure), moet u beveiliging op korte termijn op schijf.</span><span class="sxs-lookup"><span data-stu-id="d3024-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="d3024-327">Klik op **volgende** om door te gaan naar de korte termijn beveiliging bereik.</span><span class="sxs-lookup"><span data-stu-id="d3024-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="d3024-329">Op de **Kortetermijndoelen opgeven** pagina voor **bewaartermijn**, geef het aantal dagen dat u wilt bewaren herstelpunten die zijn *opgeslagen op schijf*.</span><span class="sxs-lookup"><span data-stu-id="d3024-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="d3024-330">Als u wilt wijzigen van de tijd en dagen wanneer herstelpunten worden gemaakt, klikt u op **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="d3024-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="d3024-331">De korte termijn herstelpunten zijn volledige back-ups.</span><span class="sxs-lookup"><span data-stu-id="d3024-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="d3024-332">Ze zijn geen incrementele back-ups.</span><span class="sxs-lookup"><span data-stu-id="d3024-332">They are not incremental backups.</span></span> <span data-ttu-id="d3024-333">Wanneer u tevreden met de korte-termijndoelstellingen bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="d3024-335">Op de **Schijftoewijzing controleren** controleert en wijzig indien nodig de schijfruimte voor de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d3024-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="d3024-336">De aanbevolen schijftoewijzingen zijn gebaseerd op de bewaartermijn die is opgegeven in de **Kortetermijndoelen opgeven** pagina, het type werkbelasting en de grootte van de beveiligde gegevens (aangeduid in stap 3).</span><span class="sxs-lookup"><span data-stu-id="d3024-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="d3024-337">**Gegevensgrootte:** grootte van de gegevens in de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="d3024-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="d3024-338">**Schijfruimte:** de aanbevolen hoeveelheid schijfruimte voor de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="d3024-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="d3024-339">Als u wilt om deze instelling te wijzigen, moet u de totale ruimte die groter is dan het bedrag in dat u een schatting maken van dat elke gegevensbron groeit toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d3024-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="d3024-340">**Gegevens plaatsen:** als u collocatie inschakelt, meerdere bronnen in de beveiliging aan een enkele replica en herstelpuntvolume toewijzen kunnen gegevenspuntvolume.</span><span class="sxs-lookup"><span data-stu-id="d3024-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="d3024-341">Collocatie wordt niet ondersteund voor alle werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="d3024-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="d3024-342">**Automatisch vergroten:** als u voor deze instelling inschakelt als gegevens in de groep beveiligde groter worden dan de aanvankelijke toewijzing, System Center Data Protection Manager wordt geprobeerd om de schijfgrootte met 25 procent.</span><span class="sxs-lookup"><span data-stu-id="d3024-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="d3024-343">**Opslaggroepdetails:** toont de status van de opslaggroep, waaronder de totale en resterende schijfgrootte.</span><span class="sxs-lookup"><span data-stu-id="d3024-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Schijftoewijzing controleren](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="d3024-345">Wanneer u tevreden bent met de toegewezen ruimte aan, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="d3024-346">Op de **methode voor maken van selecteren Replica** pagina, Geef op hoe u voor het genereren van de eerste kopie, of de replica van de beveiligde gegevens op Azure Backup-Server.</span><span class="sxs-lookup"><span data-stu-id="d3024-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="d3024-347">De standaardwaarde is **automatisch via het netwerk** en **nu**.</span><span class="sxs-lookup"><span data-stu-id="d3024-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="d3024-348">Als u de standaard gebruikt, raden wij aan dat u opgeeft dat een tijdstip buiten de piekuren.</span><span class="sxs-lookup"><span data-stu-id="d3024-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="d3024-349">Kies **Later** en geef een dag en tijd.</span><span class="sxs-lookup"><span data-stu-id="d3024-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="d3024-350">Voor grote hoeveelheden gegevens of minder dan optimale netwerkomstandigheden, kunt u de gegevens offline repliceren met behulp van verwijderbare media.</span><span class="sxs-lookup"><span data-stu-id="d3024-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="d3024-351">Nadat u uw keuzes hebt aangebracht, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-351">After you have made your choices, click **Next**.</span></span>

    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="d3024-353">Op de **opties voor consistentiecontrole** pagina, selecteer hoe en wanneer de consistentiecontroles automatiseren.</span><span class="sxs-lookup"><span data-stu-id="d3024-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="d3024-354">Wanneer de gerepliceerde gegevens inconsistent, of volgens een vooropgezet schema, kunt u consistentiecontroles uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d3024-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="d3024-355">Als u niet voor het configureren van automatische consistentiecontroles wilt, kunt u een handmatige controle uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d3024-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="d3024-356">In het gebied van de beveiliging van de back-upserver van Azure-console, met de rechtermuisknop op de beveiligingsgroep en selecteer vervolgens **consistentiecontrole uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="d3024-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="d3024-357">Klik op **volgende** verplaatsen naar de volgende pagina.</span><span class="sxs-lookup"><span data-stu-id="d3024-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="d3024-358">Op de **gegevens voor Online beveiliging opgeven** pagina, selecteer een of meer gegevensbronnen die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="d3024-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="d3024-359">U kunt de leden afzonderlijk selecteren of op **Alles selecteren** alle leden kiezen.</span><span class="sxs-lookup"><span data-stu-id="d3024-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="d3024-360">Nadat u ervoor de leden kiest, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-360">After you choose the members, click **Next**.</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="d3024-362">Op de **onlineback-upschema opgeven** pagina, geeft u de planning voor het genereren van herstelpunten van de back-up van schijf.</span><span class="sxs-lookup"><span data-stu-id="d3024-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="d3024-363">Nadat het herstelpunt dat is gegenereerd, wordt deze overgebracht naar de Recovery Services-kluis in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3024-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="d3024-364">Wanneer u tevreden met het online back-upschema bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="d3024-366">Op de **Online bewaarbeleid opgeven** pagina, geef aan hoe lang u wilt behouden van de back-upgegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3024-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="d3024-367">Nadat het beleid is gedefinieerd, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d3024-367">After the policy is defined, click **Next**.</span></span>

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="d3024-369">Er is geen tijdslimiet voor hoe lang van gegevens in Azure bewaren.</span><span class="sxs-lookup"><span data-stu-id="d3024-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="d3024-370">Wanneer u herstelpuntgegevens in Azure opslaat, is de enige limiet dat er meer dan 9999 herstelpunten per beveiligde exemplaar kan niet.</span><span class="sxs-lookup"><span data-stu-id="d3024-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="d3024-371">In dit voorbeeld is het beveiligde exemplaar de VMware-server.</span><span class="sxs-lookup"><span data-stu-id="d3024-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="d3024-372">Op de **samenvatting** pagina, Controleer de details voor de leden van de beveiligingsgroep en de instellingen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="d3024-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Een lid van beveiligingsgroep en samenvatting van de instelling](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="d3024-374">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3024-374">Next steps</span></span>
<span data-ttu-id="d3024-375">Als u Azure Backup-Server gebruikt om VMware workloads te beschermen, hebt u mogelijk geïnteresseerd in beveiligen met Azure Backup-Server een [Microsoft Exchange-server](./backup-azure-exchange-mabs.md), een [Microsoft SharePoint-farm](./backup-azure-backup-sharepoint-mabs.md), of een [SQL Server-database](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="d3024-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="d3024-376">Zie voor informatie over problemen met het registreren van de agent, configureert de beveiligingsgroep of back-ups van taken, [problemen met Azure Backup-Server](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d3024-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
