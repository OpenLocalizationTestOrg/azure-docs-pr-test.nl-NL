---
title: aaaConfigure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="cc83b-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="cc83b-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cc83b-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="cc83b-104">Before you begin</span></span>
<span data-ttu-id="cc83b-105">Zorg ervoor dat u hebt voltooid [taak 2 - export Hallo beveiligde LDAP certificaat tooa. PFX-bestand](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="cc83b-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="cc83b-106">Kiezen of toouse Hallo preview-ervaring met Azure portal of hello Azure classic portal toocomplete deze taak.</span><span class="sxs-lookup"><span data-stu-id="cc83b-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="cc83b-107">**Azure-portal (Preview)**: [inschakelen secure LDAP hello Azure-portal gebruiken](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="cc83b-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="cc83b-108">**Klassieke Azure-portal**: [inschakelen met behulp van de klassieke Azure portal Hallo LDAP beveiligen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="cc83b-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="cc83b-109">Taak 3: beveiligde LDAP voor Hallo beheerde domein met de klassieke Azure portal Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="cc83b-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="cc83b-110">tooenable beveiligde LDAP, voert u Hallo configuratiestappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc83b-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="cc83b-111">Navigeer toohello  **[klassieke Azure-portal](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="cc83b-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="cc83b-112">Selecteer Hallo **Active Directory** knooppunt in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc83b-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="cc83b-113">Selecteer hello Azure AD-directory (ook waarnaar wordt verwezen tooas 'tenant'), waarvoor u Azure AD Domain Services hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc83b-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="cc83b-115">Klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cc83b-115">Click hello **Configure** tab.</span></span>

    ![Tabblad Configureren van directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="cc83b-117">Schuif omlaag in het gedeelte van toohello **domeinservices**.</span><span class="sxs-lookup"><span data-stu-id="cc83b-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="cc83b-118">U ziet een optie met de titel **beveiligde LDAP (LDAPS)** zoals weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc83b-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Configuratiesectie Domeinservices](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="cc83b-120">Klik op Hallo **certificaat configureren...**  knop toobring up Hallo **certificaat configureren voor Secure LDAP** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc83b-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Certificaat voor veilige LDAP configureren](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="cc83b-122">Klik op Hallo map pictogram volgende **PFX-bestand met certificaat** toospecify Hallo PFX-bestand dat u wenst dat toouse voor beveiligde LDAP toegang toohello Hallo-certificaat bevat beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="cc83b-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="cc83b-123">Ook Hallo wachtwoord die u hebt opgegeven bij het exporteren van Hallo toohello PFX-certificaatbestand invoeren.</span><span class="sxs-lookup"><span data-stu-id="cc83b-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="cc83b-124">Klik vervolgens op Hallo knop op Hallo onder gedaan.</span><span class="sxs-lookup"><span data-stu-id="cc83b-124">Then, click hello done button on hello bottom.</span></span>

    ![Beveiligde LDAP PFX-bestand en een wachtwoord opgeven](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="cc83b-126">Hallo **domeinservices** sectie Hallo **configureren** tabblad moet ophalen lichter gekleurd weergegeven en in Hallo **in behandeling...**  staat zijn voor een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="cc83b-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="cc83b-127">Tijdens deze periode Hallo LDAPS-certificaat is geverifieerd voor nauwkeurigheid en beveiligde LDAP is geconfigureerd voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="cc83b-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Beveiligde LDAP - status in behandeling](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="cc83b-129">Het duurt ongeveer 10 too15 minuten tooenable beveiligde LDAP voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="cc83b-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="cc83b-130">Hallo opgegeven beveiligde LDAP-certificaat komt niet overeen met Hallo vereist criteria, beveiligde LDAP is niet ingeschakeld voor uw directory als er een fout.</span><span class="sxs-lookup"><span data-stu-id="cc83b-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="cc83b-131">Bijvoorbeeld Hallo domeinnaam is onjuist, Hallo-certificaat is al verlopen of verloopt binnenkort.</span><span class="sxs-lookup"><span data-stu-id="cc83b-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="cc83b-132">Wanneer u beveiligde LDAP is ingeschakeld voor uw beheerde domein, Hallo **in behandeling...**  bericht verdwijnt.</span><span class="sxs-lookup"><span data-stu-id="cc83b-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="cc83b-133">U ziet Hallo vingerafdruk van certificaat dat Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cc83b-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="cc83b-135">Taak 4: het inschakelen van beveiligde LDAP toegang via Hallo internet</span><span class="sxs-lookup"><span data-stu-id="cc83b-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="cc83b-136">**Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.</span><span class="sxs-lookup"><span data-stu-id="cc83b-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="cc83b-137">Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="cc83b-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="cc83b-138">U ziet een optie te**Hallo inschakelen SECURE LDAP toegang via INTERNET** in Hallo **domeinservices** sectie Hallo **configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="cc83b-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="cc83b-139">Deze optie is ingesteld, te**Nee** standaard omdat internet toegang toohello beheerd domein via beveiligde LDAP is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc83b-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="cc83b-141">Wisselknop **Hallo inschakelen SECURE LDAP toegang via INTERNET** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="cc83b-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="cc83b-142">Klik op Hallo **opslaan** knop op Hallo onderpaneel.</span><span class="sxs-lookup"><span data-stu-id="cc83b-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="cc83b-143">![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="cc83b-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="cc83b-144">Hallo **domeinservices** sectie Hallo **configureren** tabblad moet ophalen lichter gekleurd weergegeven en in Hallo **in behandeling...**  staat zijn voor een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="cc83b-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="cc83b-145">Na enige tijd is toegang tooyour beheerde internetdomein via beveiligde LDAP ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc83b-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![Beveiligde LDAP - status in behandeling](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="cc83b-147">Het duurt ongeveer 10 minuten tooenable toegang tot internet via beveiligde LDAP voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="cc83b-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="cc83b-148">Wanneer beveiligde LDAP toegang tooyour beheerd domein via Hallo internet is ingeschakeld, Hallo **in behandeling...**  bericht verdwijnt.</span><span class="sxs-lookup"><span data-stu-id="cc83b-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="cc83b-149">U ziet Hallo extern IP-adres dat kan worden gebruikt tooaccess uw directory via LDAPS in Hallo veld **externe IP-adres voor LDAPS toegang**.</span><span class="sxs-lookup"><span data-stu-id="cc83b-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="cc83b-151">Taak 5: configureer DNS-tooaccess Hallo beheerde domein van Hallo internet</span><span class="sxs-lookup"><span data-stu-id="cc83b-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="cc83b-152">**Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.</span><span class="sxs-lookup"><span data-stu-id="cc83b-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="cc83b-153">Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="cc83b-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="cc83b-154">Wanneer u beveiligde LDAP toegang hebt ingeschakeld via internet Hallo voor uw beheerde domein, moet u tooupdate DNS zodat clientcomputers dit beheerde domein vindt.</span><span class="sxs-lookup"><span data-stu-id="cc83b-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="cc83b-155">Aan het einde van de Hallo van taak 4, een externe IP-adres wordt weergegeven op Hallo **configureren** tabblad **externe IP-adres voor LDAPS toegang**.</span><span class="sxs-lookup"><span data-stu-id="cc83b-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="cc83b-156">Uw externe DNS-provider configureren voor DNS-naam Hallo Hallo beheerd domein (bijvoorbeeld ' ldaps.contoso100.com') punten toothis externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="cc83b-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="cc83b-157">In ons voorbeeld moeten we toocreate Hallo DNS-vermelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc83b-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="cc83b-158">Dat is alles: u bent nu klaar tooconnect toohello beheerd domein met beveiligde LDAP via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc83b-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="cc83b-159">Houd er rekening mee dat clientcomputers is Hallo verlener van Hallo LDAPS certificaat toobe kunnen tooconnect moeten vertrouwen toohello beheerd domein LDAPS wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc83b-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="cc83b-160">Als u gebruikmaakt van een certificeringsinstantie voor ondernemingen of een openbaar vertrouwde certificeringsinstantie (CA), hoeft u niet toodo iets omdat deze certificaatverleners clientcomputers worden vertrouwd.</span><span class="sxs-lookup"><span data-stu-id="cc83b-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="cc83b-161">Als u een zelfondertekend certificaat gebruikt, moet u tooinstall Hallo openbare deel van de zelf-ondertekend certificaat Hallo in Hallo vertrouwde certificaatarchief op de clientcomputer Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc83b-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="cc83b-162">Vergrendeling LDAPS via Hallo tooyour beheerd domein toegang krijgen tot internet</span><span class="sxs-lookup"><span data-stu-id="cc83b-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="cc83b-163">**Optionele taak** : als u niet hebt ingeschakeld LDAPS toegang toohello beheerd domein meer dan internet hello, deze configuratietaak overslaan.</span><span class="sxs-lookup"><span data-stu-id="cc83b-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="cc83b-164">Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="cc83b-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="cc83b-165">Het blootstellen van uw beheerde domein voor LDAPS toegang via Hallo vertegenwoordigt internet een beveiligingsrisico.</span><span class="sxs-lookup"><span data-stu-id="cc83b-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="cc83b-166">Hallo beheerd domein is bereikbaar is vanaf Hallo internet op Hallo-poort die wordt gebruikt voor beveiligde LDAP (dat wil zeggen, poort 636).</span><span class="sxs-lookup"><span data-stu-id="cc83b-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="cc83b-167">U kunt daarom toorestrict toegang toohello beheerd domein toospecific bekende IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="cc83b-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="cc83b-168">Voor betere beveiliging, een netwerkbeveiligingsgroep (NSG) maken en deze koppelen aan Hallo subnet waar u Azure AD Domain Services hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc83b-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="cc83b-169">Hallo volgende tabel ziet u een voorbeeld van een NSG u configureren kunt, toolock omlaag beveiligde LDAP toegang via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="cc83b-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="cc83b-170">Hallo NSG bevat een reeks regels waarmee binnenkomende LDAPS toegang via TCP-poort 636 alleen uit een opgegeven set van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="cc83b-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="cc83b-171">Hallo 'DenyAll' standaardregel geldt tooall andere binnenkomend verkeer van Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="cc83b-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="cc83b-172">Hallo NSG regel tooallow LDAPS toegang via Hallo internet vanaf de opgegeven IP-adressen heeft een hogere prioriteit dan Hallo DenyAll NSG-regel.</span><span class="sxs-lookup"><span data-stu-id="cc83b-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Voorbeeld NSG toosecure LDAPS toegang via internet Hallo](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="cc83b-174">**Meer informatie** - [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cc83b-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="cc83b-175">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="cc83b-175">Related content</span></span>
* [<span data-ttu-id="cc83b-176">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="cc83b-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="cc83b-177">Een beheerd domein van Azure AD Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="cc83b-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="cc83b-178">Groepsbeleid voor een Azure AD Domain Services beheerd domein beheren</span><span class="sxs-lookup"><span data-stu-id="cc83b-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="cc83b-179">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="cc83b-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="cc83b-180">Een Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="cc83b-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
