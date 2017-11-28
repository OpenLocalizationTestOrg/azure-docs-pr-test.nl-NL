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
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2d9a2-103">Azure AD-toepassingsproxy op een beheerd domein van Azure AD Domain Services implementeren</span><span class="sxs-lookup"><span data-stu-id="2d9a2-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="2d9a2-104">Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van on-premises toepassingen via internet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="2d9a2-105">U kunt nu lift-en-shift oudere toepassingen met lokale naar Azure Infrastructure Services met Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="2d9a2-106">Vervolgens kunt u deze toepassingen de Azure AD-toepassingsproxy gebruiken voor veilige externe toegang tot gebruikers in uw organisatie publiceren.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="2d9a2-107">Als u geen ervaring met de Azure AD-toepassingsproxy, meer informatie over deze functie met het volgende artikel: [het verstrekken van veilige externe toegang tot on-premises toepassingen](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2d9a2-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="2d9a2-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2d9a2-108">Before you begin</span></span>
<span data-ttu-id="2d9a2-109">Als u wilt uitvoeren van de taken worden in dit artikel worden vermeld, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2d9a2-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="2d9a2-110">Een geldige **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="2d9a2-111">Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="2d9a2-112">Een **Azure AD Basic of Premium-licentie** is vereist voor het gebruik van de Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="2d9a2-113">**Azure AD Domain Services** moet zijn ingeschakeld voor de Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="2d9a2-114">Als u dit nog niet hebt gedaan, volgt u alle taken die worden beschreven in de [handleiding](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2d9a2-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="2d9a2-115">Taak 1: toepassingsproxy van Azure AD inschakelen voor uw Azure AD-directory</span><span class="sxs-lookup"><span data-stu-id="2d9a2-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="2d9a2-116">Voer de volgende stappen uit zodat de Azure AD-toepassingsproxy voor uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="2d9a2-117">Meld u aan als een beheerder in de [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d9a2-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="2d9a2-118">Klik op **Azure Active Directory** online zetten van een overzicht van de directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="2d9a2-119">Klik op **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-119">Click **Enterprise applications**.</span></span>

    ![Azure AD-directory selecteren](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="2d9a2-121">Klik op **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-121">Click **Application proxy**.</span></span> <span data-ttu-id="2d9a2-122">Als u niet een Azure AD Basic of Azure AD Premium-abonnement hebt, ziet u een optie voor het inschakelen van een evaluatieversie.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="2d9a2-123">Wisselknop **toepassingsproxy inschakelen?** naar **inschakelen** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![Toepassingsproxy inschakelen](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="2d9a2-125">De connector downloaden, klikt u op de **Connector** knop.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-125">To download the connector, click the **Connector** button.</span></span>

    ![Connector downloaden](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="2d9a2-127">Op de downloadpagina accepteer de licentievoorwaarden en privacyovereenkomst en klik op de **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![Download bevestigen](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2d9a2-129">Taak 2: het domein Windows-servers voor het implementeren van de Azure AD-toepassingsproxy connector richten</span><span class="sxs-lookup"><span data-stu-id="2d9a2-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2d9a2-130">U moet lid zijn van het domein Windows Server virtuele machines waarop u de Azure AD-toepassingsproxy-connector kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="2d9a2-131">Afhankelijk van de toepassingen die worden gepubliceerd, kunt u meerdere servers waarop de connector is geïnstalleerd inrichten.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="2d9a2-132">Deze Implementatieoptie krijgt u groter beschikbaarheid en helpt bij het verwerken van zwaardere belastingen voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="2d9a2-133">Richt de Connectorservers voor hetzelfde virtuele netwerk (of een virtueel netwerk met verbonden/peer is ingesteld), waarin u uw beheerde domein van Azure AD Domain Services hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="2d9a2-134">De servers die als host fungeert voor de toepassingen die u via de toepassingsproxy publiceert moeten op deze manier worden geïnstalleerd op dezelfde virtuele netwerk van Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="2d9a2-135">Voor het inrichten van Connectorservers, volgt u de taken die worden beschreven in het artikel [een virtuele Windows-computer toevoegen aan een beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2d9a2-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2d9a2-136">Taak 3: Installeer en registreer de Azure AD Application Proxy Connector</span><span class="sxs-lookup"><span data-stu-id="2d9a2-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="2d9a2-137">Eerder ingerichte van een virtuele machine van Windows Server en deze toegevoegd aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="2d9a2-138">In deze taak kunt u de Azure AD-toepassingsproxy-connector wilt installeren op deze virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="2d9a2-139">Kopieer het installatiepakket van de connector met de virtuele machine waarop u de Azure AD Web Application Proxy connector installeert.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="2d9a2-140">Voer **AADApplicationProxyConnectorInstaller.exe** op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="2d9a2-141">De gebruiksrechtovereenkomst accepteren.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-141">Accept the software license terms.</span></span>

    ![Accepteer de voorwaarden voor installatie](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="2d9a2-143">Tijdens de installatie wordt u gevraagd de connector te registreren bij de toepassingsproxy van uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="2d9a2-144">Geef uw **Azure AD-referenties globale beheerder**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="2d9a2-145">De referenties van uw globale beheerderstenant kunnen afwijken van uw Microsoft Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="2d9a2-146">Het administrator-account gebruikt voor het registreren van de connector moet behoren tot dezelfde map waarin u de service-toepassingsproxy hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="2d9a2-147">Bijvoorbeeld, als de tenant-domein contoso.com is, de beheerder moet admin@contoso.com of andere geldige alias in dat domein.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="2d9a2-148">Als Verbeterde beveiliging van Internet Explorer is ingeschakeld voor de server waarop u de connector installeert, is het registratiescherm mogelijk geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="2d9a2-149">Volg de instructies in het foutbericht voor toegang.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="2d9a2-150">Zorg ervoor dat de verbeterde beveiliging van Internet Explorer is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="2d9a2-151">Zie [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md) (Engelstalig) als de registratie van de connector niet lukt.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Connector is geïnstalleerd](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="2d9a2-153">Om te controleren of de connector worden werkt de Azure AD Application Proxy Connector probleemoplosser naar behoren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="2d9a2-154">U ziet een geslaagde rapport na het uitvoeren van de probleemoplosser.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-154">You should see a successful report after running the troubleshooter.</span></span>

    ![Probleemoplosser geslaagd](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="2d9a2-156">U ziet de nieuw geïnstalleerde weergegeven op de pagina Application proxy in uw Azure AD-directory-connector.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="2d9a2-157">U kunt om connectors te installeren op meerdere servers om bescherming te bieden hoge beschikbaarheid voor het verifiëren van toepassingen die zijn gepubliceerd via de Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="2d9a2-158">De hierboven beschreven voor het installeren van de connector op andere servers toegevoegd aan uw beheerde domein dezelfde stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2d9a2-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d9a2-159">Next Steps</span></span>
<span data-ttu-id="2d9a2-160">U hebt de Azure AD-toepassingsproxy instellen en deze geïntegreerd met uw Azure AD Domain Services beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="2d9a2-161">**Uw toepassingen met Azure virtuele machines migreren:** kunt u lift-en-shift uw toepassingen van lokale servers en virtuele machines in Azure die is gekoppeld aan uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="2d9a2-162">In dat geval kunt u de kosten van de infrastructuur van het uitvoeren van servers lokale weghalen.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="2d9a2-163">**Toepassingen publiceren met Azure AD-toepassingsproxy:** publiceren van toepassingen die worden uitgevoerd op uw virtuele machines in Azure met behulp van de Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="2d9a2-164">Zie voor meer informatie [toepassingen publiceren met Azure AD-toepassingsproxy](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2d9a2-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="2d9a2-165">Opmerking van de implementatie - publiceren IWA (geïntegreerde Windows-verificatie)-toepassingen die gebruikmaken van Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="2d9a2-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="2d9a2-166">Eenmalige aanmelding voor uw toepassingen met geïntegreerde Windows-verificatie (IWA) Application Proxy Connectors machtiging verlenen imiteren gebruikers, en verzenden en ontvangen van tokens namens hen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="2d9a2-167">Kerberos-beperkte delegatie (KCD) voor de connector voor het verlenen van de vereiste machtigingen voor toegang tot bronnen op het beheerde domein configureren.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="2d9a2-168">Gebruik het mechanisme KCD op basis van bronnen op de beheerde domeinen voor een betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2d9a2-169">Op basis van bronnen kerberos-beperkte overdracht voor de Azure AD-toepassingsproxy-connector inschakelen</span><span class="sxs-lookup"><span data-stu-id="2d9a2-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2d9a2-170">De Azure Application Proxy connector moet worden geconfigureerd voor kerberos-beperkte delegatie (KCD), zodat gebruikers kunnen worden geïmiteerd op het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="2d9a2-171">Op een beheerd domein van Azure AD Domain Services er geen domeinadministratorrechten.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="2d9a2-172">Daarom **traditionele account niveau KCD kan niet worden geconfigureerd op een beheerd domein**.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="2d9a2-173">Gebruik KCD op basis van bronnen zoals beschreven in dit [artikel](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="2d9a2-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2d9a2-174">U moet lid zijn van de groep 'AAD DC-beheerders' voor het beheer van het beheerde domein met AD PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="2d9a2-175">Gebruik de cmdlet Get-ADComputer PowerShell voor het ophalen van de instellingen voor de computer waarop de Azure AD-toepassingsproxy-connector is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="2d9a2-176">Daarna gebruikt u de cmdlet Set-ADComputer KCD op basis van een resource voor de resource-server instellen.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="2d9a2-177">Als u meerdere toepassingsproxy connectors voor uw beheerde domein hebt geïmplementeerd, moet u KCD op basis van bronnen voor elke keer dat deze connector configureert.</span><span class="sxs-lookup"><span data-stu-id="2d9a2-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="2d9a2-178">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="2d9a2-178">Related Content</span></span>
* [<span data-ttu-id="2d9a2-179">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="2d9a2-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2d9a2-180">Kerberos-beperkte overdracht configureren op een beheerd domein</span><span class="sxs-lookup"><span data-stu-id="2d9a2-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="2d9a2-181">Kerberos-beperkte overdracht overzicht</span><span class="sxs-lookup"><span data-stu-id="2d9a2-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
