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
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="8e112-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="8e112-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8e112-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8e112-104">Before you begin</span></span>
<span data-ttu-id="8e112-105">Zorg ervoor dat u hebt voltooid [taak 2 - export Hallo beveiligde LDAP certificaat tooa. PFX-bestand](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="8e112-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="8e112-106">Kiezen of toouse Hallo preview-ervaring met Azure portal of hello Azure classic portal toocomplete deze taak.</span><span class="sxs-lookup"><span data-stu-id="8e112-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8e112-107">**Azure-portal (Preview)**: [inschakelen secure LDAP hello Azure-portal gebruiken](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="8e112-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="8e112-108">**Klassieke Azure-portal**: [inschakelen met behulp van de klassieke Azure portal Hallo LDAP beveiligen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="8e112-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="8e112-109">Taak 3: Schakel veilige LDAP voor Hallo beheerde domein met hello Azure-portal (Preview)</span><span class="sxs-lookup"><span data-stu-id="8e112-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="8e112-110">tooenable beveiligde LDAP, voert u Hallo configuratiestappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e112-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="8e112-111">Navigeer toohello  **[Azure-portal](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="8e112-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="8e112-112">Zoeken naar domain services in Hallo **zoeken bronnen** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="8e112-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="8e112-113">Selecteer **Azure AD Domain Services** van Hallo zoekresultaat.</span><span class="sxs-lookup"><span data-stu-id="8e112-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="8e112-114">Hallo **Azure AD Domain Services** blade geeft een lijst van uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="8e112-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Zoeken naar beheerde domein wordt ingericht](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="8e112-116">Klik op Hallo-naam van Hallo beheerd domein (bijvoorbeeld, contoso100.com') toosee meer informatie over het Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="8e112-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - status voor inrichten heeft](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="8e112-118">Klik op **beveiligde LDAP** op Hallo navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="8e112-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services - blade beveiligde LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="8e112-120">Beveiligde LDAP toegang tooyour beheerd domein is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8e112-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="8e112-121">Wisselknop **beveiligde LDAP** te**inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="8e112-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Beveiligde LDAP inschakelen](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="8e112-123">Standaard beheerde beveiligde LDAP toegang tooyour domein via Hallo die Internet is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8e112-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="8e112-124">Wisselknop **beveiligde LDAP-toegang toestaan via internet Hallo** te**inschakelen**, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="8e112-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="8e112-125">Klik op Hallo map pictogram volgende **. PFX-bestand met LDAP om certificaten veilig**.</span><span class="sxs-lookup"><span data-stu-id="8e112-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="8e112-126">Hallo pad toohello PFX-bestand met de Hallo-certificaat voor beveiligde LDAP toegang toohello beheerde domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="8e112-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="8e112-127">Geef Hallo **toodecrypt wachtwoord. PFX-bestand**.</span><span class="sxs-lookup"><span data-stu-id="8e112-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="8e112-128">Hallo bieden hetzelfde wachtwoord dat u hebt gebruikt bij het exporteren van Hallo toohello PFX-certificaatbestand.</span><span class="sxs-lookup"><span data-stu-id="8e112-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="8e112-129">Wanneer u klaar bent, klikt u op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8e112-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="8e112-130">U ziet een melding dat informeert u dat beveiligde LDAP wordt geconfigureerd voor Hallo beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="8e112-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="8e112-131">Totdat deze bewerking voltooid is, kunt u andere instellingen voor Hallo domein niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e112-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Beveiligde LDAP voor Hallo beheerde domein configureren](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="8e112-133">Het duurt ongeveer 10 too15 minuten tooenable beveiligde LDAP voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="8e112-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="8e112-134">Hallo opgegeven beveiligde LDAP-certificaat komt niet overeen met Hallo vereist criteria, beveiligde LDAP is niet ingeschakeld voor uw directory als er een fout.</span><span class="sxs-lookup"><span data-stu-id="8e112-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="8e112-135">Bijvoorbeeld Hallo domeinnaam is onjuist, Hallo-certificaat is al verlopen of verloopt binnenkort.</span><span class="sxs-lookup"><span data-stu-id="8e112-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="8e112-136">In dit geval, probeer het opnieuw met een geldig certificaat.</span><span class="sxs-lookup"><span data-stu-id="8e112-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="8e112-137">Taak 4: configureer DNS-tooaccess Hallo beheerde domein van Hallo internet</span><span class="sxs-lookup"><span data-stu-id="8e112-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="8e112-138">**Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.</span><span class="sxs-lookup"><span data-stu-id="8e112-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="8e112-139">Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="8e112-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="8e112-140">Wanneer u beveiligde LDAP toegang hebt ingeschakeld via internet Hallo voor uw beheerde domein, moet u tooupdate DNS zodat clientcomputers dit beheerde domein vindt.</span><span class="sxs-lookup"><span data-stu-id="8e112-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="8e112-141">Aan het einde van de Hallo van taak 3, een externe IP-adres wordt weergegeven op Hallo **eigenschappen** blade in **externe IP-adres voor LDAPS toegang**.</span><span class="sxs-lookup"><span data-stu-id="8e112-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="8e112-142">Uw externe DNS-provider configureren voor DNS-naam Hallo Hallo beheerd domein (bijvoorbeeld ' ldaps.contoso100.com') punten toothis externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8e112-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="8e112-143">In ons voorbeeld moeten we toocreate Hallo DNS-vermelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e112-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="8e112-144">Dat is alles: u bent nu klaar tooconnect toohello beheerd domein met beveiligde LDAP via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e112-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="8e112-145">Houd er rekening mee dat clientcomputers is Hallo verlener van Hallo LDAPS certificaat toobe kunnen tooconnect moeten vertrouwen toohello beheerd domein LDAPS wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e112-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="8e112-146">Als u een openbaar vertrouwde certificeringsinstantie (CA) gebruikt, hoeft u niet toodo iets omdat deze certificaatverleners clientcomputers worden vertrouwd.</span><span class="sxs-lookup"><span data-stu-id="8e112-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="8e112-147">Als u een zelfondertekend certificaat gebruikt, installeert u Hallo openbare deel van de zelf-ondertekend certificaat Hallo in Hallo vertrouwde certificaatarchief op de clientcomputer Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e112-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="8e112-148">Taak 5 - vergrendeling LDAPS tooyour beheerde toegang tot het domein via internet Hallo</span><span class="sxs-lookup"><span data-stu-id="8e112-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="8e112-149">**Optionele taak** : als u niet hebt ingeschakeld LDAPS toegang toohello beheerd domein meer dan internet hello, deze configuratietaak overslaan.</span><span class="sxs-lookup"><span data-stu-id="8e112-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="8e112-150">Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="8e112-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="8e112-151">Het blootstellen van uw beheerde domein voor LDAPS toegang via Hallo vertegenwoordigt internet een beveiligingsrisico.</span><span class="sxs-lookup"><span data-stu-id="8e112-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="8e112-152">Hallo beheerd domein is bereikbaar is vanaf Hallo internet op Hallo-poort die wordt gebruikt voor beveiligde LDAP (dat wil zeggen, poort 636).</span><span class="sxs-lookup"><span data-stu-id="8e112-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="8e112-153">U kunt daarom toorestrict toegang toohello beheerd domein toospecific bekende IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8e112-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="8e112-154">Voor betere beveiliging, een netwerkbeveiligingsgroep (NSG) maken en deze koppelen aan Hallo subnet waar u Azure AD Domain Services hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8e112-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="8e112-155">Hallo volgende tabel ziet u een voorbeeld van een NSG u configureren kunt, toolock omlaag beveiligde LDAP toegang via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="8e112-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="8e112-156">Hallo NSG bevat een reeks regels waarmee binnenkomende LDAPS toegang via TCP-poort 636 alleen uit een opgegeven set van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8e112-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="8e112-157">Hallo 'DenyAll' standaardregel geldt tooall andere binnenkomend verkeer van Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="8e112-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="8e112-158">Hallo NSG regel tooallow LDAPS toegang via Hallo internet vanaf de opgegeven IP-adressen heeft een hogere prioriteit dan Hallo DenyAll NSG-regel.</span><span class="sxs-lookup"><span data-stu-id="8e112-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Voorbeeld NSG toosecure LDAPS toegang via internet Hallo](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="8e112-160">**Meer informatie** - [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="8e112-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="8e112-161">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="8e112-161">Related content</span></span>
* [<span data-ttu-id="8e112-162">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="8e112-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="8e112-163">Een beheerd domein van Azure AD Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="8e112-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="8e112-164">Groepsbeleid voor een Azure AD Domain Services beheerd domein beheren</span><span class="sxs-lookup"><span data-stu-id="8e112-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="8e112-165">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="8e112-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8e112-166">Een Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="8e112-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
