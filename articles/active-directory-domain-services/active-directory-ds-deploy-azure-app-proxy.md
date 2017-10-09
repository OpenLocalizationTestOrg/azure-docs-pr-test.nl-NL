---
title: 'Azure Active Directory Domain Services: Azure Active Directory-toepassingsproxy implementeren | Microsoft Docs'
description: Azure AD-toepassingsproxy gebruiken op de beheerde domeinen Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="c754c-103">Azure AD-toepassingsproxy op een beheerd domein van Azure AD Domain Services implementeren</span><span class="sxs-lookup"><span data-stu-id="c754c-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="c754c-104">Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van lokale toepassingen toobe toegankelijk is via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="c754c-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="c754c-105">U kunt nu lift-en-shift oudere toepassingen met lokale tooAzure Infrastructure Services met Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c754c-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises tooAzure Infrastructure Services.</span></span> <span data-ttu-id="c754c-106">Vervolgens kunt u deze toepassingen met behulp van hello Azure AD-toepassingsproxy, tooprovide veilige externe toegang toousers in uw organisatie publiceren.</span><span class="sxs-lookup"><span data-stu-id="c754c-106">You can then publish these applications using hello Azure AD Application Proxy, tooprovide secure remote access toousers in your organization.</span></span>

<span data-ttu-id="c754c-107">Als u nieuwe toohello Azure AD-toepassingsproxy, meer informatie over deze functie hello volgende artikel: [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c754c-107">If you're new toohello Azure AD Application Proxy, learn more about this feature with hello following article: [How tooprovide secure remote access tooon-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c754c-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c754c-108">Before you begin</span></span>
<span data-ttu-id="c754c-109">tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="c754c-109">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="c754c-110">Een geldige **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c754c-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="c754c-111">Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="c754c-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="c754c-112">Een **Azure AD Basic of Premium-licentie** is vereist toouse hello Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="c754c-112">An **Azure AD Basic or Premium license** is required toouse hello Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="c754c-113">**Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="c754c-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="c754c-114">Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c754c-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="c754c-115">Taak 1: toepassingsproxy van Azure AD inschakelen voor uw Azure AD-directory</span><span class="sxs-lookup"><span data-stu-id="c754c-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="c754c-116">Volgende stappen tooenable hello Azure AD-toepassingsproxy voor uw Azure AD-directory Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c754c-116">Perform hello following steps tooenable hello Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="c754c-117">Meld u aan als een beheerder in Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c754c-117">Sign in as an administrator in hello [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="c754c-118">Klik op **Azure Active Directory** toobring up overzicht Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c754c-118">Click **Azure Active Directory** toobring up hello directory overview.</span></span> <span data-ttu-id="c754c-119">Klik op **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c754c-119">Click **Enterprise applications**.</span></span>

    ![Azure AD-directory selecteren](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="c754c-121">Klik op **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="c754c-121">Click **Application proxy**.</span></span> <span data-ttu-id="c754c-122">Als u niet een Azure AD Basic of Azure AD Premium-abonnement hebt, ziet u een optie tooenable een proefversie.</span><span class="sxs-lookup"><span data-stu-id="c754c-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option tooenable a trial.</span></span> <span data-ttu-id="c754c-123">Wisselknop **toepassingsproxy inschakelen?** te**inschakelen** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c754c-123">Toggle **Enable Application Proxy?** too**Enable** and click **Save**.</span></span>

    ![Toepassingsproxy inschakelen](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="c754c-125">toodownload Hallo connector, klikt u op Hallo **Connector** knop.</span><span class="sxs-lookup"><span data-stu-id="c754c-125">toodownload hello connector, click hello **Connector** button.</span></span>

    ![Connector downloaden](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="c754c-127">Op de downloadpagina hello, accepteer Hallo licentievoorwaarden en privacyovereenkomst en klik op Hallo **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="c754c-127">On hello download page, accept hello license terms and privacy agreement and click hello **Download** button.</span></span>

    ![Download bevestigen](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="c754c-129">Taak 2 - inrichten domein Windows servers toodeploy hello Azure AD-toepassingsproxy-connector</span><span class="sxs-lookup"><span data-stu-id="c754c-129">Task 2 - Provision domain-joined Windows servers toodeploy hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="c754c-130">U moet lid zijn van het domein Windows Server virtuele machines waarop u hello Azure AD-toepassingsproxy connector kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="c754c-130">You need domain-joined Windows Server virtual machines on which you can install hello Azure AD Application Proxy connector.</span></span> <span data-ttu-id="c754c-131">Afhankelijk van de toepassingen hello wordt gepubliceerd, kunt u tooprovision meerdere servers waarop Hallo-connector is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c754c-131">Depending on hello applications being published, you may choose tooprovision multiple servers on which hello connector is installed.</span></span> <span data-ttu-id="c754c-132">Deze Implementatieoptie krijgt u groter beschikbaarheid en helpt bij het verwerken van zwaardere belastingen voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="c754c-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="c754c-133">Servers met de Hallo connector richten op Hallo van hetzelfde virtuele netwerk (of een virtueel netwerk met verbonden/brengen) in die u hebt ingeschakeld uw beheerde domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c754c-133">Provision hello connector servers on hello same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="c754c-134">Op deze manier Hallo-servers die als host fungeert voor Hallo-toepassingen die u via Hallo toepassingsproxy publiceert toobe geïnstalleerd op Hallo moeten hetzelfde virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="c754c-134">Similarly, hello servers hosting hello applications you publish via hello Application Proxy need toobe installed on hello same Azure virtual network.</span></span>

<span data-ttu-id="c754c-135">tooprovision Connectorservers, volg Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c754c-135">tooprovision connector servers, follow hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="c754c-136">Taak 3: Installeer en registreer hello Azure AD-Application Proxy Connector</span><span class="sxs-lookup"><span data-stu-id="c754c-136">Task 3 - Install and register hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="c754c-137">Eerder ingerichte van een virtuele machine van Windows Server en deze toohello beheerd domein toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c754c-137">Previously, you provisioned a Windows Server virtual machine and joined it toohello managed domain.</span></span> <span data-ttu-id="c754c-138">In deze taak kunt u hello Azure AD-toepassingsproxy connector wilt installeren op deze virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c754c-138">In this task, you will install hello Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="c754c-139">Kopieer Hallo connector installatie pakket toohello VM waarop u hello Azure AD Web Application Proxy connector installeert.</span><span class="sxs-lookup"><span data-stu-id="c754c-139">Copy hello connector installation package toohello VM on which you install hello Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="c754c-140">Voer **AADApplicationProxyConnectorInstaller.exe** op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c754c-140">Run **AADApplicationProxyConnectorInstaller.exe** on hello virtual machine.</span></span> <span data-ttu-id="c754c-141">Licentievoorwaarden Hallo-software accepteren.</span><span class="sxs-lookup"><span data-stu-id="c754c-141">Accept hello software license terms.</span></span>

    ![Accepteer de voorwaarden voor installatie](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="c754c-143">Tijdens de installatie bent u na vragen aan gebruiker tooregister Hallo connector met Hallo toepassingsproxy van uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="c754c-143">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="c754c-144">Geef uw **Azure AD-referenties globale beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c754c-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="c754c-145">De referenties van uw globale beheerderstenant kunnen afwijken van uw Microsoft Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="c754c-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="c754c-146">Hallo beheerder account gebruikt tooregister Hallo connector moet behoren toohello dezelfde map waarin u Hallo-service voor toepassingsproxy hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c754c-146">hello administrator account used tooregister hello connector must belong toohello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="c754c-147">Bijvoorbeeld, als Hallo tenant domein contoso.com is, Hallo beheerder moet admin@contoso.com of andere geldige alias in dat domein.</span><span class="sxs-lookup"><span data-stu-id="c754c-147">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="c754c-148">Als Verbeterde beveiliging van Internet Explorer is ingeschakeld voor Hallo server waarop u Hallo-connector installeert, kunt u Hallo registratiescherm mogelijk geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="c754c-148">If IE Enhanced Security Configuration is turned on for hello server where you are installing hello connector, hello registration screen might be blocked.</span></span> <span data-ttu-id="c754c-149">tooallow toegang, volg de instructies in Hallo in Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="c754c-149">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="c754c-150">Zorg ervoor dat de verbeterde beveiliging van Internet Explorer is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c754c-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="c754c-151">Zie [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md) (Engelstalig) als de registratie van de connector niet lukt.</span><span class="sxs-lookup"><span data-stu-id="c754c-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Connector is geïnstalleerd](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="c754c-153">tooensure hello connector werkt goed uitgevoerde hello Azure AD Application Proxy Connector probleemoplosser.</span><span class="sxs-lookup"><span data-stu-id="c754c-153">tooensure hello connector works properly, run hello Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="c754c-154">U ziet een geslaagde rapport na actieve Hallo probleemoplosser.</span><span class="sxs-lookup"><span data-stu-id="c754c-154">You should see a successful report after running hello troubleshooter.</span></span>

    ![Probleemoplosser geslaagd](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="c754c-156">U ziet Hallo onlangs geïnstalleerde connector vermeld op Hallo Application proxy pagina in uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="c754c-156">You should see hello newly installed connector listed on hello Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="c754c-157">U kunt tooguarantee hoge beschikbaarheid voor het verifiëren van toepassingen die zijn gepubliceerd via hello Azure AD-toepassingsproxy tooinstall connectors op meerdere servers.</span><span class="sxs-lookup"><span data-stu-id="c754c-157">You may choose tooinstall connectors on multiple servers tooguarantee high availability for authenticating applications published through hello Azure AD Application Proxy.</span></span> <span data-ttu-id="c754c-158">Hallo dezelfde stappen tooinstall Hallo connector op andere servers lid tooyour beheerde domeinen bovenstaande uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c754c-158">Perform hello same steps listed above tooinstall hello connector on other servers joined tooyour managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c754c-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c754c-159">Next Steps</span></span>
<span data-ttu-id="c754c-160">U hebt Azure AD-toepassingsproxy Hallo instellen en deze geïntegreerd met uw Azure AD Domain Services beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="c754c-160">You have set up hello Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="c754c-161">**Uw toepassingen tooAzure virtuele machines migreren:** kunt lift en shift uw toepassingen van lokale servers tooAzure virtuele machines lid tooyour beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="c754c-161">**Migrate your applications tooAzure virtual machines:** You can lift-and-shift your applications from on-premises servers tooAzure virtual machines joined tooyour managed domain.</span></span> <span data-ttu-id="c754c-162">In dat geval kunt u van kosten van de infrastructuur van het uitvoeren van servers lokale Hallo afvoeren.</span><span class="sxs-lookup"><span data-stu-id="c754c-162">Doing so helps you get rid of hello infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="c754c-163">**Toepassingen publiceren met Azure AD-toepassingsproxy:** publiceren van toepassingen die op uw virtuele machines in Azure met Azure AD-toepassingsproxy Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c754c-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using hello Azure AD Application Proxy.</span></span> <span data-ttu-id="c754c-164">Zie voor meer informatie [toepassingen publiceren met Azure AD-toepassingsproxy](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c754c-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="c754c-165">Opmerking van de implementatie - publiceren IWA (geïntegreerde Windows-verificatie)-toepassingen die gebruikmaken van Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="c754c-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="c754c-166">Eenmalige aanmelding tooyour-toepassingen die gebruikmaken van geïntegreerde Windows-verificatie (IWA) Application Proxy Connectors toestemming verleent tooimpersonate gebruikers, inschakelen en verzenden en ontvangen van tokens in hun naam.</span><span class="sxs-lookup"><span data-stu-id="c754c-166">Enable single sign-on tooyour applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission tooimpersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="c754c-167">Kerberos-beperkte delegatie (KCD) voor Hallo connector toogrant Hallo vereist machtigingen tooaccess bronnen op Hallo beheerd domein configureren.</span><span class="sxs-lookup"><span data-stu-id="c754c-167">Configure kerberos constrained delegation (KCD) for hello connector toogrant hello required permissions tooaccess resources on hello managed domain.</span></span> <span data-ttu-id="c754c-168">Gebruik Hallo resources gebaseerde KCD mechanisme op beheerde domeinen voor een betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="c754c-168">Use hello resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="c754c-169">Op basis van bronnen kerberos-beperkte overdracht voor hello Azure AD-toepassingsproxy connector inschakelen</span><span class="sxs-lookup"><span data-stu-id="c754c-169">Enable resource-based kerberos constrained delegation for hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="c754c-170">Hello Azure Application Proxy connector moet worden geconfigureerd voor kerberos-beperkte delegatie (KCD), zodat gebruikers kunnen worden geïmiteerd op Hallo beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="c754c-170">hello Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on hello managed domain.</span></span> <span data-ttu-id="c754c-171">Op een beheerd domein van Azure AD Domain Services er geen domeinadministratorrechten.</span><span class="sxs-lookup"><span data-stu-id="c754c-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="c754c-172">Daarom **traditionele account niveau KCD kan niet worden geconfigureerd op een beheerd domein**.</span><span class="sxs-lookup"><span data-stu-id="c754c-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="c754c-173">Gebruik KCD op basis van bronnen zoals beschreven in dit [artikel](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="c754c-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c754c-174">U moet toobe lid van Hallo ' AAD DC' beheerdersgroep tooadminister Hallo beheerd domein met AD PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c754c-174">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="c754c-175">Hallo Get-ADComputer PowerShell cmdlet tooretrieve Hallo instellingen gebruiken voor Hallo-computer op welke hello Azure AD-toepassingsproxy-connector is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c754c-175">Use hello Get-ADComputer PowerShell cmdlet tooretrieve hello settings for hello computer on which hello Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="c754c-176">Gebruik daarna Hallo Set-ADComputer cmdlet tooset up KCD op basis van een resource voor Hallo resource-server.</span><span class="sxs-lookup"><span data-stu-id="c754c-176">Thereafter, use hello Set-ADComputer cmdlet tooset up resource-based KCD for hello resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="c754c-177">Als u meerdere toepassingsproxy connectors voor uw beheerde domein hebt geïmplementeerd, moet u tooconfigure KCD voor elk dergelijke connector-exemplaar op basis van bronnen.</span><span class="sxs-lookup"><span data-stu-id="c754c-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need tooconfigure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="c754c-178">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="c754c-178">Related Content</span></span>
* [<span data-ttu-id="c754c-179">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="c754c-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c754c-180">Kerberos-beperkte overdracht configureren op een beheerd domein</span><span class="sxs-lookup"><span data-stu-id="c754c-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="c754c-181">Kerberos-beperkte overdracht overzicht</span><span class="sxs-lookup"><span data-stu-id="c754c-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
