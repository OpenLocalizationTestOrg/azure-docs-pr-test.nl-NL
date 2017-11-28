---
title: 'Azure Active Directory Domain Services: Een RHEL VM toevoegen aan een beheerd domein | Microsoft Docs'
description: Red Hat Enterprise Linux virtuele machine toevoegen aan Azure AD Domain Services
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="149f3-103">Een virtuele Red Hat Enterprise Linux 7-machine toevoegen aan een beheerd domein</span><span class="sxs-lookup"><span data-stu-id="149f3-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="149f3-104">In dit artikel laat zien hoe een virtuele machine met Red Hat Enterprise Linux (RHEL) 7 toevoegen aan een beheerd domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="149f3-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="149f3-105">Een Red Hat Enterprise Linux-machine inrichten</span><span class="sxs-lookup"><span data-stu-id="149f3-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="149f3-106">Voer de volgende stappen uit voor het inrichten van een RHEL 7 virtuele machine met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="149f3-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="149f3-107">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="149f3-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Azure-portaldashboard](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="149f3-109">Klik op **nieuw** in het linkerdeelvenster en typ **Red Hat** in de zoekbalk, zoals wordt weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="149f3-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="149f3-110">Vermeldingen voor Red Hat Enterprise Linux worden weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="149f3-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="149f3-111">Klik op **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="149f3-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="149f3-113">De zoekresultaten de **Alles** deelvenster moet de installatiekopie van het Red Hat Enterprise Linux 7.2 lijst.</span><span class="sxs-lookup"><span data-stu-id="149f3-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="149f3-114">Klik op **Red Hat Enterprise Linux 7.2** voor meer informatie over de installatiekopie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="149f3-116">In de **Red Hat Enterprise Linux 7.2** deelvenster ziet u meer informatie over de installatiekopie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="149f3-117">In de **een implementatiemodel selecteren** vervolgkeuzelijst, selecteer **klassieke**.</span><span class="sxs-lookup"><span data-stu-id="149f3-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="149f3-118">Klik vervolgens op de **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="149f3-118">Then click the **Create** button.</span></span>

    ![Details van de afbeelding weergeven](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="149f3-120">In de **basisbeginselen** pagina van de **virtuele machine maken** wizard voert de **hostnaam** voor de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="149f3-121">Geef ook de gebruikersnaam van een lokale beheerder in de **gebruikersnaam** veld en een **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="149f3-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="149f3-122">U kunt ook een SSH-sleutel gebruiken om te verifiëren van de lokale beheerder-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="149f3-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="149f3-123">Selecteert u ook een **prijscategorie** voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![VM - basisbeginselen pagina maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="149f3-125">In de **grootte** pagina van de **virtuele machine maken** wizard, selecteer de grootte voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Maken van VM - grootte selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="149f3-127">In de **instellingen** pagina van de **virtuele machine maken** wizard selecteert u de storage-account voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="149f3-128">Klik op **virtueel netwerk** selecteren van het virtuele netwerk waartoe de Linux-VM moeten worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="149f3-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="149f3-129">In de **virtueel netwerk** blade, selecteer het virtuele netwerk in welke Azure AD Domain Services beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="149f3-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="149f3-130">In dit voorbeeld kiest u het virtuele netwerk 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="149f3-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Maken van VM - virtuele netwerk selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="149f3-132">Op de **samenvatting** pagina van de **virtuele machine maken** wizard controleren en op de **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="149f3-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Maken van VM - virtuele netwerk zijn geselecteerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="149f3-134">Implementatie van de nieuwe virtuele machine op basis van de installatiekopie van het RHEL 7.2 moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="149f3-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Maken van VM - implementatie is gestart](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="149f3-136">Na een paar minuten, moeten de virtuele machine worden geïmplementeerd met succes en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="149f3-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Maken van VM - geïmplementeerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="149f3-138">Extern verbinding maken met de nieuw ingerichte virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="149f3-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="149f3-139">De RHEL 7.2 virtuele machine is ingericht in Azure.</span><span class="sxs-lookup"><span data-stu-id="149f3-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="149f3-140">De volgende taak is het op afstand verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="149f3-141">**Verbinding maken met de virtuele machine van RHEL 7.2** Volg de instructies in het artikel [aanmelden met een virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="149f3-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="149f3-142">De rest van de stappen wordt ervan uitgegaan dat u de PuTTY SSH-client verbinding maken met de RHEL virtuele machine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="149f3-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="149f3-143">Zie voor meer informatie de [PuTTY-downloadpagina](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="149f3-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="149f3-144">Open het PuTTY programma.</span><span class="sxs-lookup"><span data-stu-id="149f3-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="149f3-145">Voer de **hostnaam** voor de zojuist gemaakte RHEL virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="149f3-146">In dit voorbeeld is de virtuele machine de host-naam 'contoso-rhel.cloudapp .net'.</span><span class="sxs-lookup"><span data-stu-id="149f3-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="149f3-147">Als u de hostnaam van uw virtuele machine niet weet, raadpleegt u het VM-dashboard in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="149f3-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![PuTTY verbinding maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="149f3-149">Meld u bij de virtuele machine met de lokale administrator-referenties die u hebt opgegeven toen de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="149f3-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="149f3-150">In dit voorbeeld hebben we het lokale administrator-account 'mahesh' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="149f3-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![PuTTY-aanmelding](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="149f3-152">Installeert de vereiste pakketten op de virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="149f3-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="149f3-153">Nadat u verbinding maakt met de virtuele machine, is de volgende taak voor het installeren van pakketten die zijn vereist voor domeinlidmaatschap op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="149f3-154">De volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="149f3-154">Perform the following steps:</span></span>

1. <span data-ttu-id="149f3-155">**Installeer realmd:** het pakket realmd wordt gebruikt voor het domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="149f3-156">Typ de volgende opdracht in de PuTTY terminal:</span><span class="sxs-lookup"><span data-stu-id="149f3-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="149f3-157">sudo yum installeren realmd</span><span class="sxs-lookup"><span data-stu-id="149f3-157">sudo yum install realmd</span></span>

    ![Realmd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="149f3-159">Na een paar minuten moet het pakket realmd geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="149f3-161">**Installeer sssd:** het pakket realmd is afhankelijk van sssd domain join-bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="149f3-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="149f3-162">Typ de volgende opdracht in de PuTTY terminal:</span><span class="sxs-lookup"><span data-stu-id="149f3-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="149f3-163">sudo yum installeren sssd</span><span class="sxs-lookup"><span data-stu-id="149f3-163">sudo yum install sssd</span></span>

    ![Sssd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="149f3-165">Na een paar minuten moet het pakket sssd geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="149f3-167">**Kerberos installeren:** In uw terminal PuTTY, typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="149f3-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="149f3-168">sudo yum installeren krb5 werkstation krb5-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="149f3-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Kerberos installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="149f3-170">Na een paar minuten moet het pakket realmd geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="149f3-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos is geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="149f3-172">De virtuele Linux-machine toevoegen aan het beheerde domein</span><span class="sxs-lookup"><span data-stu-id="149f3-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="149f3-173">Nu de vereiste pakketten zijn geïnstalleerd op de virtuele Linux-machine, de volgende taak is de virtuele machine toevoegen aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="149f3-174">Ontdek het beheerde domein met AAD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="149f3-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="149f3-175">Typ de volgende opdracht in de PuTTY terminal:</span><span class="sxs-lookup"><span data-stu-id="149f3-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="149f3-176">sudo realm CONTOSO100.COM detecteren</span><span class="sxs-lookup"><span data-stu-id="149f3-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Realm detecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="149f3-178">Als **realm detecteren** kan niet zoeken naar uw beheerde domein, zorg ervoor dat het domein van de virtuele machine (probeer ping) bereikbaar is.</span><span class="sxs-lookup"><span data-stu-id="149f3-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="149f3-179">Zorg er ook voor dat de virtuele machine inderdaad is geïmplementeerd voor hetzelfde virtuele netwerk waarin het beheerde domein beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="149f3-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="149f3-180">Initialiseren van kerberos.</span><span class="sxs-lookup"><span data-stu-id="149f3-180">Initialize kerberos.</span></span> <span data-ttu-id="149f3-181">Typ de volgende opdracht in de PuTTY terminal.</span><span class="sxs-lookup"><span data-stu-id="149f3-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="149f3-182">Zorg ervoor dat u een gebruiker die lid is van de groep 'AAD DC Administrators' opgeven.</span><span class="sxs-lookup"><span data-stu-id="149f3-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="149f3-183">Alleen deze gebruikers kunnen computers toevoegen aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="149f3-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="149f3-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="149f3-186">Zorg dat u de domeinnaam in hoofdletters opgeven, anders kinit is mislukt.</span><span class="sxs-lookup"><span data-stu-id="149f3-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="149f3-187">De machine toevoegen aan het domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-187">Join the machine to the domain.</span></span> <span data-ttu-id="149f3-188">Typ de volgende opdracht in de PuTTY terminal.</span><span class="sxs-lookup"><span data-stu-id="149f3-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="149f3-189">Geef dezelfde gebruiker die u hebt opgegeven in de vorige stap (kinit).</span><span class="sxs-lookup"><span data-stu-id="149f3-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="149f3-190">sudo realm join--uitgebreide CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="149f3-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="149f3-192">U krijgt een bericht ('is ingeschreven machine in de realm') wanneer de computer met succes is toegevoegd aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="149f3-193">Controleer of aan domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="149f3-193">Verify domain join</span></span>
<span data-ttu-id="149f3-194">U kunt snel te controleren of de machine is toegevoegd aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="149f3-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="149f3-195">Verbinding maken met het nieuwe domein RHEL VM die gebruikmaakt van SSH en een domeingebruikersaccount en controleer om te zien of het gebruikersaccount correct is opgelost.</span><span class="sxs-lookup"><span data-stu-id="149f3-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="149f3-196">In de PuTTY terminal, typ de volgende opdracht verbinding maken met het nieuwe domein RHEL virtuele machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="149f3-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="149f3-197">Gebruik een domeinaccount die deel uitmaakt van het beheerde domein (bijvoorbeeld 'bob@CONTOSO100.COM' in dit geval.)</span><span class="sxs-lookup"><span data-stu-id="149f3-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="149f3-198">SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="149f3-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="149f3-199">Typ de volgende opdracht om te zien of de basismap correct is geïnitialiseerd in de PuTTY terminal.</span><span class="sxs-lookup"><span data-stu-id="149f3-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="149f3-200">pwd</span><span class="sxs-lookup"><span data-stu-id="149f3-200">pwd</span></span>
3. <span data-ttu-id="149f3-201">Typ de volgende opdracht om te zien als het groepslidmaatschap correct wordt opgelost in de PuTTY terminal.</span><span class="sxs-lookup"><span data-stu-id="149f3-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="149f3-202">id</span><span class="sxs-lookup"><span data-stu-id="149f3-202">id</span></span>

<span data-ttu-id="149f3-203">Hier volgt een voorbeeld van uitvoer van deze opdrachten:</span><span class="sxs-lookup"><span data-stu-id="149f3-203">A sample output of these commands follows:</span></span>

![Controleer of aan domein toevoegen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="149f3-205">Het oplossen van problemen aan domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="149f3-205">Troubleshooting domain join</span></span>
<span data-ttu-id="149f3-206">Raadpleeg de [probleemoplossing domein](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artikel.</span><span class="sxs-lookup"><span data-stu-id="149f3-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="149f3-207">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="149f3-207">Related Content</span></span>
* [<span data-ttu-id="149f3-208">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="149f3-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="149f3-209">Virtuele machine met Windows Server toevoegen aan een beheerd domein van Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="149f3-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="149f3-210">[Aanmelden met een virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="149f3-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="149f3-211">Kerberos installeren</span><span class="sxs-lookup"><span data-stu-id="149f3-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="149f3-212">Red Hat Enterprise Linux 7 - handleiding voor Windows-integratie</span><span class="sxs-lookup"><span data-stu-id="149f3-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
