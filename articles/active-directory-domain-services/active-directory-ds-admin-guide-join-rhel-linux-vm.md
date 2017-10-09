---
title: 'Azure Active Directory Domain Services: Deelnemen aan een beheerd domein van RHEL VM tooa | Microsoft Docs'
description: Virtuele machine met Red Hat Enterprise Linux toevoegen tooAzure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="b0174-103">Lid worden van een beheerd domein van Red Hat Enterprise Linux 7 virtuele machine tooa</span><span class="sxs-lookup"><span data-stu-id="b0174-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="b0174-104">Dit artikel laat zien hoe toojoin een Red Hat Enterprise Linux (RHEL) 7 virtuele machine tooan Azure AD Domain Services beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="b0174-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="b0174-105">Een Red Hat Enterprise Linux-machine inrichten</span><span class="sxs-lookup"><span data-stu-id="b0174-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="b0174-106">Volgende stappen tooprovision een RHEL 7 virtuele machine met behulp van Azure-portal Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b0174-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="b0174-107">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0174-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Azure-portaldashboard](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="b0174-109">Klik op **nieuw** op Hallo deelvenster en type **Red Hat** in de zoekbalk Hallo zoals weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0174-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="b0174-110">Vermeldingen voor Red Hat Enterprise Linux worden weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0174-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="b0174-111">Klik op **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="b0174-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="b0174-113">zoekresultaten in Hallo Hallo **Alles** deelvenster Hallo Red Hat Enterprise Linux 7.2 installatiekopie moet aanbieden.</span><span class="sxs-lookup"><span data-stu-id="b0174-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="b0174-114">Klik op **Red Hat Enterprise Linux 7.2** tooview meer informatie over de installatiekopie van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0174-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="b0174-116">In Hallo **Red Hat Enterprise Linux 7.2** deelvenster ziet u meer informatie over de installatiekopie van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0174-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="b0174-117">In Hallo **een implementatiemodel selecteren** vervolgkeuzelijst, selecteer **klassieke**.</span><span class="sxs-lookup"><span data-stu-id="b0174-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="b0174-118">Klik vervolgens op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="b0174-118">Then click hello **Create** button.</span></span>

    ![Details van de afbeelding weergeven](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="b0174-120">In Hallo **basisbeginselen** pagina Hallo **virtuele machine maken** wizard Voer Hallo **hostnaam** voor Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="b0174-121">Ook de gebruikersnaam van een lokale beheerder opgeven in Hallo **gebruikersnaam** veld en een **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b0174-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="b0174-122">U kunt desgewenst ook toouse gebruiker SSH sleutel tooauthenticate Hallo lokale beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0174-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="b0174-123">Selecteert u ook een **prijscategorie** voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![VM - basisbeginselen pagina maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="b0174-125">In Hallo **grootte** pagina Hallo **virtuele machine maken** grootte van de wizard, selecteer Hallo voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Maken van VM - grootte selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="b0174-127">In Hallo **instellingen** pagina Hallo **virtuele machine maken** wizard, selecteer Hallo storage-account voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="b0174-128">Klik op **virtueel netwerk** tooselect Hallo virtueel netwerk toowhich Hallo Linux VM moeten worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b0174-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="b0174-129">In Hallo **virtueel netwerk** blade, selecteer Hallo virtueel netwerk waarin Azure AD Domain Services beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="b0174-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="b0174-130">In dit voorbeeld kiest u Hallo 'MyPreviewVNet' virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="b0174-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Maken van VM - virtuele netwerk selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="b0174-132">Op Hallo **samenvatting** pagina Hallo **virtuele machine maken** wizard controleren en op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="b0174-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Maken van VM - virtuele netwerk zijn geselecteerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="b0174-134">Implementatie van Hallo nieuwe virtuele machine op basis van Hallo RHEL 7.2 afbeelding moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="b0174-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Maken van VM - implementatie is gestart](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="b0174-136">Na een paar minuten moet Hallo virtuele machine is geïmplementeerd en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="b0174-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Maken van VM - geïmplementeerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="b0174-138">Extern verbinding maken met toohello nieuw ingerichte virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="b0174-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="b0174-139">Hallo RHEL 7.2 virtuele machine is ingericht in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0174-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="b0174-140">de volgende taak Hallo tooconnect op afstand is toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="b0174-141">**Verbinding maken met toohello RHEL 7.2 virtuele machine** Hallo-instructies in Hallo artikel [hoe toolog op tooa virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0174-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b0174-142">Hallo rest Hallo stappen wordt ervan uitgegaan dat u Hallo PuTTY SSH client tooconnect toohello RHEL virtuele machine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0174-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="b0174-143">Zie voor meer informatie, Hallo [PuTTY-downloadpagina](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="b0174-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="b0174-144">Open Hallo PuTTY programma.</span><span class="sxs-lookup"><span data-stu-id="b0174-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="b0174-145">Voer Hallo **hostnaam** voor Hallo RHEL virtuele machine van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b0174-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="b0174-146">In dit voorbeeld is de virtuele machine Hallo host-naam 'contoso-rhel.cloudapp .net'.</span><span class="sxs-lookup"><span data-stu-id="b0174-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="b0174-147">Als u de hostnaam Hallo van uw virtuele machine niet weet, raadpleegt u toohello VM dashboard op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b0174-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![PuTTY verbinding maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="b0174-149">Meld u aan toohello virtuele machine met lokale beheerdersreferenties Hallo die u hebt opgegeven bij Hallo virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b0174-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="b0174-150">In dit voorbeeld hebben we Hallo lokale administrator-account 'mahesh' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0174-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![PuTTY-aanmelding](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="b0174-152">Installeert de vereiste pakketten op Hallo Linux virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b0174-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="b0174-153">Na het maken van verbinding toohello virtuele machine is de volgende taak Hallo tooinstall pakketten die zijn vereist voor domeinlidmaatschap op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="b0174-154">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0174-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="b0174-155">**Installeer realmd:** hello realmd pakket wordt gebruikt voor het domein.</span><span class="sxs-lookup"><span data-stu-id="b0174-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="b0174-156">Typ in de PuTTY terminal Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0174-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="b0174-157">sudo yum installeren realmd</span><span class="sxs-lookup"><span data-stu-id="b0174-157">sudo yum install realmd</span></span>

    ![Realmd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="b0174-159">Na een paar minuten moet Hallo realmd pakket ophalen geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="b0174-161">**Installeer sssd:** hello realmd pakket, is afhankelijk van sssd tooperform domain join-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b0174-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="b0174-162">Typ in de PuTTY terminal Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0174-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="b0174-163">sudo yum installeren sssd</span><span class="sxs-lookup"><span data-stu-id="b0174-163">sudo yum install sssd</span></span>

    ![Sssd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="b0174-165">Na een paar minuten moet Hallo sssd pakket ophalen geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="b0174-167">**Kerberos installeren:** Typ In de PuTTY terminal Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0174-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="b0174-168">sudo yum installeren krb5 werkstation krb5-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="b0174-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Kerberos installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="b0174-170">Na een paar minuten moet Hallo realmd pakket ophalen geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0174-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos is geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="b0174-172">Hallo Linux virtuele machine toohello beheerd domein koppelen</span><span class="sxs-lookup"><span data-stu-id="b0174-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="b0174-173">Nu vereist hello-pakketten op Hallo virtuele Linux-machine zijn geïnstalleerd, de volgende taak Hallo is toojoin Hallo virtuele machine toohello beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="b0174-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="b0174-174">Hallo AAD Domain Services beheerd domein detecteren.</span><span class="sxs-lookup"><span data-stu-id="b0174-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="b0174-175">Typ in de PuTTY terminal Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0174-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="b0174-176">sudo realm CONTOSO100.COM detecteren</span><span class="sxs-lookup"><span data-stu-id="b0174-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Realm detecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="b0174-178">Als **realm detecteren** niet kan toofind is uw beheerde domein, zorg ervoor dat domein Hallo bereikbaar is vanaf Hallo virtuele machine (probeer ping).</span><span class="sxs-lookup"><span data-stu-id="b0174-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="b0174-179">Zorg er ook voor dat de virtuele machine Hallo geïmplementeerde toohello inderdaad is hetzelfde virtuele netwerk in welke Hallo beheerde domein beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="b0174-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="b0174-180">Initialiseren van kerberos.</span><span class="sxs-lookup"><span data-stu-id="b0174-180">Initialize kerberos.</span></span> <span data-ttu-id="b0174-181">Typ in de PuTTY terminal Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="b0174-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="b0174-182">Zorg ervoor dat u opgeeft dat een gebruiker die lid is van toohello ' AAD DC' beheerdersgroep.</span><span class="sxs-lookup"><span data-stu-id="b0174-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="b0174-183">Alleen deze gebruikers kunnen computers toohello beheerd domein toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0174-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="b0174-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="b0174-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="b0174-186">Zorg dat u Hallo-domeinnaam opgeven in hoofdletters, anders kinit is mislukt.</span><span class="sxs-lookup"><span data-stu-id="b0174-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="b0174-187">Lid worden Hallo machine toohello domein.</span><span class="sxs-lookup"><span data-stu-id="b0174-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="b0174-188">Typ in de PuTTY terminal Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="b0174-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="b0174-189">Geef Hallo dezelfde gebruiker die u hebt opgegeven in de voorgaande stap (kinit) Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0174-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="b0174-190">sudo realm join--uitgebreide CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="b0174-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="b0174-192">U krijgt een bericht ('is ingeschreven machine in de realm') als Hallo machine neemt deel toohello beheerd domein is.</span><span class="sxs-lookup"><span data-stu-id="b0174-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="b0174-193">Controleer of aan domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0174-193">Verify domain join</span></span>
<span data-ttu-id="b0174-194">U kunt snel te controleren of Hallo machine neemt deel toohello beheerd domein is.</span><span class="sxs-lookup"><span data-stu-id="b0174-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="b0174-195">Verbinding maken met toohello nieuw domein RHEL VM die gebruikmaakt van SSH en een domeingebruikersaccount en vervolgens selectievakje toosee als gebruikersaccount Hallo correct is opgelost.</span><span class="sxs-lookup"><span data-stu-id="b0174-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="b0174-196">In uw terminal PuTTY type Hallo na opdracht tooconnect toohello nieuw domein RHEL virtuele machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="b0174-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="b0174-197">Een domeinaccount die deel uitmaakt van het beheerde domein toohello gebruiken (bijvoorbeeld 'bob@CONTOSO100.COM' in dit geval.)</span><span class="sxs-lookup"><span data-stu-id="b0174-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="b0174-198">SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b0174-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="b0174-199">Typ in de PuTTY terminal Hallo opdracht toosee volgen als basismap Hallo correct is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="b0174-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="b0174-200">pwd</span><span class="sxs-lookup"><span data-stu-id="b0174-200">pwd</span></span>
3. <span data-ttu-id="b0174-201">Typ in de PuTTY terminal Hallo opdracht toosee volgen als Hallo groepslidmaatschappen correct worden herleid.</span><span class="sxs-lookup"><span data-stu-id="b0174-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="b0174-202">id</span><span class="sxs-lookup"><span data-stu-id="b0174-202">id</span></span>

<span data-ttu-id="b0174-203">Hier volgt een voorbeeld van uitvoer van deze opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b0174-203">A sample output of these commands follows:</span></span>

![Controleer of aan domein toevoegen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="b0174-205">Het oplossen van problemen aan domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0174-205">Troubleshooting domain join</span></span>
<span data-ttu-id="b0174-206">Raadpleeg toohello [probleemoplossing domein](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artikel.</span><span class="sxs-lookup"><span data-stu-id="b0174-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="b0174-207">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="b0174-207">Related Content</span></span>
* [<span data-ttu-id="b0174-208">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="b0174-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="b0174-209">Deelnemen aan een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="b0174-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="b0174-210">[Hoe toolog op tooa virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0174-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="b0174-211">Kerberos installeren</span><span class="sxs-lookup"><span data-stu-id="b0174-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="b0174-212">Red Hat Enterprise Linux 7 - handleiding voor Windows-integratie</span><span class="sxs-lookup"><span data-stu-id="b0174-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
