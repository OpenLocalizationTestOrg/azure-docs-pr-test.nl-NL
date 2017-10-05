---
title: Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen | Microsoft Docs
description: Bevat informatie over de basisprincipes voor het integreren van een on-premises SharePoint-server met Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="93f0b-103">Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="93f0b-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="93f0b-104">In dit artikel wordt beschreven hoe een on-premises SharePoint server integreren met Azure Active Directory (Azure AD) Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="93f0b-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="93f0b-105">Volg de secties in dit artikel stapsgewijze zodat externe toegang tot SharePoint met Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="93f0b-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93f0b-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="93f0b-106">Prerequisites</span></span>

<span data-ttu-id="93f0b-107">In dit artikel wordt ervan uitgegaan dat u SharePoint 2013 of nieuwer al in uw omgeving hebt.</span><span class="sxs-lookup"><span data-stu-id="93f0b-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="93f0b-108">Bovendien kunt u overwegen de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="93f0b-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="93f0b-109">SharePoint bevat systeemeigen ondersteuning van Kerberos.</span><span class="sxs-lookup"><span data-stu-id="93f0b-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="93f0b-110">Daarom gebruikers die toegang interne sites op afstand via Azure AD-toepassingsproxy tot kunnen wordt ervan uitgegaan dat een ervaring voor eenmalige aanmelding (SSO).</span><span class="sxs-lookup"><span data-stu-id="93f0b-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="93f0b-111">U moet enkele configuratiewijzigingen aanbrengen in uw SharePoint-server.</span><span class="sxs-lookup"><span data-stu-id="93f0b-111">You need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="93f0b-112">U wordt aangeraden met behulp van een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="93f0b-112">We recommend using a staging environment.</span></span> <span data-ttu-id="93f0b-113">Op deze manier u kunt updates eerst naar uw testserver maken en vervolgens een cyclus testen voordat u doorgaat naar de productie te vergemakkelijken.</span><span class="sxs-lookup"><span data-stu-id="93f0b-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="93f0b-114">Er wordt ervan uitgegaan dat u hebt al ingesteld SSL voor SharePoint, omdat SSL op de gepubliceerde URL is vereist.</span><span class="sxs-lookup"><span data-stu-id="93f0b-114">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="93f0b-115">U moet SSL is ingeschakeld op uw interne site, om ervoor te zorgen dat koppelingen verzonden/toegewezen correct zijn.</span><span class="sxs-lookup"><span data-stu-id="93f0b-115">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="93f0b-116">Als u dit nog niet hebt geconfigureerd dat SSL, Zie [SSL configureren voor SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="93f0b-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="93f0b-117">Zorg ervoor dat het certificaat dat u de opdracht wordt vertrouwd door de connector-machine.</span><span class="sxs-lookup"><span data-stu-id="93f0b-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="93f0b-118">(Het certificaat niet hoeft te openbaar worden uitgegeven.)</span><span class="sxs-lookup"><span data-stu-id="93f0b-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="93f0b-119">Stap 1: Instellen van eenmalige aanmelding tot SharePoint</span><span class="sxs-lookup"><span data-stu-id="93f0b-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="93f0b-120">Onze klanten willen in dit geval de beste SSO-ervaring voor hun back-end-toepassingen, SharePoint-server.</span><span class="sxs-lookup"><span data-stu-id="93f0b-120">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="93f0b-121">In dit veelvoorkomende scenario voor Azure AD, de gebruiker slechts één keer geverifieerd omdat ze niet gevraagd om het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="93f0b-121">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="93f0b-122">Voor on-premises toepassingen die vereisen of Windows-verificatie gebruiken, kunt u eenmalige aanmelding kunt bereiken met behulp van het Kerberos-protocol voor verificatie en Kerberos-beperkte delegatie (KCD) een functie.</span><span class="sxs-lookup"><span data-stu-id="93f0b-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="93f0b-123">KCD, wanneer geconfigureerd, kunt de connector voor toepassingsproxy verkrijgen van een windows-ticket/token voor een gebruiker, zelfs als de gebruiker nog niet aangemeld bij Windows rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="93f0b-123">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="93f0b-124">Zie voor meer informatie over KCD, [overzicht van Kerberos-beperkte overdracht](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="93f0b-124">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="93f0b-125">Als u KCD instelt voor een SharePoint-server, gebruik de procedures in de volgende sequentiële secties:</span><span class="sxs-lookup"><span data-stu-id="93f0b-125">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="93f0b-126">Controleer of SharePoint wordt uitgevoerd onder een serviceaccount</span><span class="sxs-lookup"><span data-stu-id="93f0b-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="93f0b-127">Controleer eerst of of SharePoint wordt uitgevoerd onder een gedefinieerde serviceaccount--niet lokaal systeem, lokale service of Netwerkservice.</span><span class="sxs-lookup"><span data-stu-id="93f0b-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="93f0b-128">Dit doen zodat u de service principal names (SPN's) aan een geldig account toevoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="93f0b-128">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="93f0b-129">SPN's zijn hoe het Kerberos-protocol verschillende services identificeert.</span><span class="sxs-lookup"><span data-stu-id="93f0b-129">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="93f0b-130">En u moet het account later naar de KCD configureren.</span><span class="sxs-lookup"><span data-stu-id="93f0b-130">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="93f0b-131">Om ervoor te zorgen dat uw sites onder een gedefinieerde serviceaccount worden uitgevoerd, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="93f0b-131">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="93f0b-132">Open de **Centraal beheer van SharePoint 2013** site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-132">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="93f0b-133">Ga naar **beveiliging** en selecteer **serviceaccounts configureren**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-133">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="93f0b-134">Selecteer **Web-groep van toepassingen - SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="93f0b-135">De opties mogelijk enigszins verschillen op basis van de naam van uw web-toepassingen, of als de webpool voor SSL standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="93f0b-135">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![Opties voor het configureren van een serviceaccount](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="93f0b-137">Als **Selecteer een account voor dit onderdeel** is **lokale Service** of **netwerkservice**, moet u een account maken.</span><span class="sxs-lookup"><span data-stu-id="93f0b-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="93f0b-138">Zo niet, u klaar bent en u kunt verplaatsen naar de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="93f0b-138">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="93f0b-139">Selecteer **nieuw beheerd account registreren**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-139">Select **Register new managed account**.</span></span> <span data-ttu-id="93f0b-140">Nadat u uw account is gemaakt, moet u instellen **toepassingen** voordat u het account kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="93f0b-140">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="93f0b-141">Moet u beschikken over een eerder gemaakte Azure AD-account voor de service.</span><span class="sxs-lookup"><span data-stu-id="93f0b-141">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="93f0b-142">Het is raadzaam dat u een automatische wachtwoordwijziging toestaan.</span><span class="sxs-lookup"><span data-stu-id="93f0b-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="93f0b-143">Zie voor meer informatie over de volledige set van stappen en het oplossen van problemen, [automatische wachtwoordwijziging configureren in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="93f0b-143">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="93f0b-144">SharePoint configureren voor Kerberos</span><span class="sxs-lookup"><span data-stu-id="93f0b-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="93f0b-145">Met KCD voeren eenmalige aanmelding met de SharePoint-server en dit werkt alleen met Kerberos.</span><span class="sxs-lookup"><span data-stu-id="93f0b-145">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="93f0b-146">De SharePoint-site voor Kerberos-verificatie configureren:</span><span class="sxs-lookup"><span data-stu-id="93f0b-146">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="93f0b-147">Open de **Centraal beheer van SharePoint 2013** site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-147">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="93f0b-148">Ga naar **Toepassingsbeheer**, selecteer **beheren van webtoepassingen**, en selecteert u de SharePoint-site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-148">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="93f0b-149">In dit voorbeeld is het **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-149">In this example, it is **SharePoint - 80**.</span></span>

  ![De SharePoint-site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="93f0b-151">Klik op **verificatieproviders** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="93f0b-151">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="93f0b-152">In de **verificatieproviders** Klik **standaardzone** om de instellingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="93f0b-152">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="93f0b-153">In de **Authentication bewerken** dialoogvenster vak, schuif omlaag totdat u ziet **typen claimverificatie** en zorg ervoor dat beide **Windows-verificatie inschakelen** en **geïntegreerde Windows-verificatie** zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-153">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="93f0b-154">Controleer of in de vervolgkeuzelijst **onderhandelen (Kerberos)** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-154">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Dialoogvenster Verificatie bewerken](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="93f0b-156">Aan de onderkant van de **Authentication bewerken** in het dialoogvenster, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-156">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="93f0b-157">Instellen van een service-principal-naam voor de SharePoint-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="93f0b-157">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="93f0b-158">Voordat u de KCD configureert, moet u het identificeren van de SharePoint-service wordt uitgevoerd als het serviceaccount dat u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-158">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="93f0b-159">U doen dit door een SPN instellen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-159">You do this by setting an SPN.</span></span> <span data-ttu-id="93f0b-160">Zie voor meer informatie [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span><span class="sxs-lookup"><span data-stu-id="93f0b-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="93f0b-161">De SPN-indeling is:</span><span class="sxs-lookup"><span data-stu-id="93f0b-161">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="93f0b-162">De SPN-indeling:</span><span class="sxs-lookup"><span data-stu-id="93f0b-162">In the SPN format:</span></span>

* <span data-ttu-id="93f0b-163">_Service-klasse_ is een unieke naam voor de service.</span><span class="sxs-lookup"><span data-stu-id="93f0b-163">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="93f0b-164">Voor SharePoint, gebruikt u **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="93f0b-165">_host_ is de FQDN- of NetBIOS-naam van de host die de service wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="93f0b-165">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="93f0b-166">Deze tekst mogelijk de URL van de site, afhankelijk van de versie van IIS die u voor een SharePoint-site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-166">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="93f0b-167">_poort_ is optioneel.</span><span class="sxs-lookup"><span data-stu-id="93f0b-167">_port_ is optional.</span></span>

<span data-ttu-id="93f0b-168">Als de FQDN van de SharePoint-server:</span><span class="sxs-lookup"><span data-stu-id="93f0b-168">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="93f0b-169">De SPN is dan:</span><span class="sxs-lookup"><span data-stu-id="93f0b-169">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="93f0b-170">Mogelijk moet u ook de SPN's instellen voor specifieke sites op uw server.</span><span class="sxs-lookup"><span data-stu-id="93f0b-170">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="93f0b-171">Zie voor meer informatie [Configureer Kerberos-verificatie](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="93f0b-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="93f0b-172">Aandacht besteedt aan de sectie 'Service Principal Names maken voor uw webtoepassingen Kerberos-verificatie gebruiken'.</span><span class="sxs-lookup"><span data-stu-id="93f0b-172">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="93f0b-173">De eenvoudigste manier voor het instellen van SPN's is de SPN-indelingen die al aanwezig om uw sites zijn mogelijk volgen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-173">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="93f0b-174">Kopieer de SPN-namen te registreren op basis van het serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="93f0b-174">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="93f0b-175">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="93f0b-175">To do this:</span></span>

1. <span data-ttu-id="93f0b-176">Blader naar de site met de SPN-naam van een andere computer.</span><span class="sxs-lookup"><span data-stu-id="93f0b-176">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="93f0b-177">Wanneer u dit doet, wordt de relevante reeks Kerberos-tickets in cache op de machine.</span><span class="sxs-lookup"><span data-stu-id="93f0b-177">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="93f0b-178">Deze tickets bevatten de SPN-naam van de doelsite die u hebt gebladerd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-178">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="93f0b-179">U kunt de SPN voor die site met een hulpprogramma aangeroepen pull- [Klist uit](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="93f0b-179">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="93f0b-180">Voer de volgende opdracht in een opdrachtvenster in de context als de gebruiker die toegang de site in de browser tot wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="93f0b-180">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="93f0b-181">Klist uit retourneert vervolgens de set van doel-SPN's.</span><span class="sxs-lookup"><span data-stu-id="93f0b-181">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="93f0b-182">De gemarkeerde waarde is in dit voorbeeld wordt de SPN-naam die nodig is:</span><span class="sxs-lookup"><span data-stu-id="93f0b-182">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Voorbeeld Klist uit resultaten](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="93f0b-184">Nu u de SPN hebt, moet u om ervoor te zorgen dat deze juist geconfigureerd op het serviceaccount dat u voor de webtoepassing eerder instellen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-184">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="93f0b-185">Voer de volgende opdracht vanaf de opdrachtprompt als beheerder van het domein:</span><span class="sxs-lookup"><span data-stu-id="93f0b-185">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="93f0b-186">Deze opdracht stelt u de SPN voor de SharePoint-serviceaccount wordt uitgevoerd als _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="93f0b-186">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="93f0b-187">Vervang _http/sharepoint.demo.o365identity.us_ met de SPN-naam voor uw server en _demo\sp_svc_ met het serviceaccount in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="93f0b-187">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="93f0b-188">De Setspn-opdracht wordt gezocht naar de SPN voordat deze wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-188">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="93f0b-189">In dit geval ziet u mogelijk een **dubbele SPN waarde** fout.</span><span class="sxs-lookup"><span data-stu-id="93f0b-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="93f0b-190">Als u deze fout ziet, zorg ervoor dat de waarde van de serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="93f0b-190">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="93f0b-191">U kunt controleren of de SPN-naam is toegevoegd door het uitvoeren van de Setspn-opdracht met de optie -l.</span><span class="sxs-lookup"><span data-stu-id="93f0b-191">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="93f0b-192">Zie voor meer informatie over deze opdracht, [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="93f0b-192">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="93f0b-193">Zorg ervoor dat de connector is ingesteld als een vertrouwde gemachtigde naar SharePoint</span><span class="sxs-lookup"><span data-stu-id="93f0b-193">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="93f0b-194">De KCD zodanig configureren dat de service Azure AD-toepassingsproxy gebruikersidentiteiten naar de SharePoint-service delegeren kunt.</span><span class="sxs-lookup"><span data-stu-id="93f0b-194">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="93f0b-195">U doen dit door de connector voor het ophalen van Kerberos-tickets voor uw gebruikers die zijn geverifieerd in Azure AD-toepassingsproxy in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-195">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="93f0b-196">Vervolgens die server context wordt doorgegeven aan de doeltoepassing of SharePoint in dit geval.</span><span class="sxs-lookup"><span data-stu-id="93f0b-196">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="93f0b-197">Herhaal de volgende stappen uit voor elke connector-machine voor het configureren van de KCD:</span><span class="sxs-lookup"><span data-stu-id="93f0b-197">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="93f0b-198">Meld u aan als domeinadministrator op een domeincontroller en open vervolgens **Active Directory: gebruikers en Computers**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-198">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="93f0b-199">De computer waarop de connector wordt uitgevoerd op vinden.</span><span class="sxs-lookup"><span data-stu-id="93f0b-199">Find the computer that the connector is running on.</span></span> <span data-ttu-id="93f0b-200">In dit voorbeeld is de dezelfde SharePoint-server.</span><span class="sxs-lookup"><span data-stu-id="93f0b-200">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="93f0b-201">Dubbelklik op de computer en klik vervolgens op de **delegering** tabblad.</span><span class="sxs-lookup"><span data-stu-id="93f0b-201">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="93f0b-202">Zorg ervoor dat de Overdrachtinstellingen zijn ingesteld op **deze computer mag alleen de opgegeven services delegeren**, en selecteer vervolgens **elk verificatieprotocol voor gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-202">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![Delegatie-instellingen](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="93f0b-204">Klik op de **toevoegen** klikken, klik op **gebruikers of Computers**, en zoek de serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="93f0b-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![De SPN voor de serviceaccount toevoegen](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="93f0b-206">Selecteer in de lijst van SPN's die u eerder hebt gemaakt voor het serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="93f0b-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="93f0b-207">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-207">Click **OK**.</span></span> <span data-ttu-id="93f0b-208">Klik op **OK** opnieuw de wijzigingen wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="93f0b-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="93f0b-209">Stap 2: Externe toegang voor SharePoint inschakelen</span><span class="sxs-lookup"><span data-stu-id="93f0b-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="93f0b-210">Nu u SharePoint hebt ingeschakeld voor Kerberos en geconfigureerde KCD, bent u klaar voor het instellen van eenmalige aanmelding tot SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93f0b-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="93f0b-211">Vervolgens kunt u de SharePoint-farm voor externe toegang via Azure AD-toepassingsproxy publiceren van de connector.</span><span class="sxs-lookup"><span data-stu-id="93f0b-211">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="93f0b-212">Als u wilt de volgende stappen uitvoert, moet u lid zijn van de globale beheerdersrol in uw organisatie Azure Active Directory-account.</span><span class="sxs-lookup"><span data-stu-id="93f0b-212">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="93f0b-213">Aanmelden bij de [Azure-portal](https://manage.windowsazure.com) en Ga naar uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="93f0b-213">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="93f0b-214">Klik op **toepassingen**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="93f0b-215">Selecteer **Een toepassing publiceren die toegankelijk is van buiten uw netwerk**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="93f0b-216">Als u deze optie niet ziet, zorg ervoor dat u Azure AD Basic hebt of Premium, in de tenant instellen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="93f0b-217">Elk van de opties als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="93f0b-217">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="93f0b-218">**Naam**: gebruik van elke waarde die u bijvoorbeeld wilt **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="93f0b-219">**Interne URL**: dit is de URL van de SharePoint-site intern, zoals **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-219">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="93f0b-220">Controleer of u in dit voorbeeld **https**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-220">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="93f0b-221">**Methode voor verificatie vooraf**: Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![Opties voor het toevoegen van een toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="93f0b-223">Nadat de app wordt gepubliceerd, klikt u op de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="93f0b-223">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="93f0b-224">Blader omlaag naar de optie **URL vertalen in Headers**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-224">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="93f0b-225">De standaardwaarde is **Ja**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-225">The default value is **YES**.</span></span> <span data-ttu-id="93f0b-226">Wijzig dit in **Nee**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-226">Change it to **NO**.</span></span>

 <span data-ttu-id="93f0b-227">SharePoint maakt gebruik van de _Host-Header_ waarde voor het opzoeken van de site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-227">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="93f0b-228">Koppelingen op basis van deze waarde wordt ook gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="93f0b-228">It also generates links based on this value.</span></span> <span data-ttu-id="93f0b-229">Het uiteindelijke resultaat is om ervoor te zorgen dat koppelingen die SharePoint genereert een gepubliceerde URL juist is ingesteld voor gebruik van de externe URL is.</span><span class="sxs-lookup"><span data-stu-id="93f0b-229">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="93f0b-230">De waarde instelt op **Ja** kunt u ook de connector voor het doorsturen van de aanvraag voor de back-end-toepassing.</span><span class="sxs-lookup"><span data-stu-id="93f0b-230">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="93f0b-231">Als u echter de waarde instelt op **Nee** betekent dit dat de connector wordt de interne hostnaam niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="93f0b-231">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="93f0b-232">In plaats daarvan verzendt de connector de host-header als de URL van de gepubliceerde naar de back-end-toepassing.</span><span class="sxs-lookup"><span data-stu-id="93f0b-232">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="93f0b-233">Om ervoor te zorgen dat SharePoint deze URL accepteert, moet u ook een meer configuratie op de SharePoint-server te voltooien.</span><span class="sxs-lookup"><span data-stu-id="93f0b-233">Also, to ensure that SharePoint accepts this URL, you need to complete one more configuration on the SharePoint server.</span></span> <span data-ttu-id="93f0b-234">U doet dat in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="93f0b-234">You'll do that in the next section.</span></span>

7. <span data-ttu-id="93f0b-235">Wijziging **interne verificatiemethode** naar **geïntegreerde Windows-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-235">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="93f0b-236">Als uw Azure AD-tenant gebruikmaakt van een UPN in de cloud die verschilt van de UPN-on-premises, houd er rekening mee te werken **overgedragen aanmelding identiteit** ook.</span><span class="sxs-lookup"><span data-stu-id="93f0b-236">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="93f0b-237">Stel **interne toepassing SPN** naar de waarde die u eerder hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="93f0b-237">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="93f0b-238">Bijvoorbeeld: **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="93f0b-239">De toepassing aan uw Doelgebruikers toewijzen.</span><span class="sxs-lookup"><span data-stu-id="93f0b-239">Assign the application to your target users.</span></span>

<span data-ttu-id="93f0b-240">Uw toepassing ziet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="93f0b-240">Your application should look similar to the following example:</span></span>

  ![Voltooide toepassing](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="93f0b-242">Stap 3: Zorg ervoor dat SharePoint op de hoogte van de externe URL</span><span class="sxs-lookup"><span data-stu-id="93f0b-242">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="93f0b-243">De laatste stap om ervoor te zorgen dat SharePoint de site op basis van de externe URL, vindt zodat deze koppelingen op basis van die externe URL worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="93f0b-243">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="93f0b-244">Hiervoor alternatieve toegangstoewijzingen voor de SharePoint-site configureren.</span><span class="sxs-lookup"><span data-stu-id="93f0b-244">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="93f0b-245">Open de **Centraal beheer van SharePoint 2013** site.</span><span class="sxs-lookup"><span data-stu-id="93f0b-245">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="93f0b-246">Onder **systeeminstellingen**, selecteer **alternatieve toegangstoewijzingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="93f0b-247">Hiermee opent u de **alternatieve toegangstoewijzingen** vak.</span><span class="sxs-lookup"><span data-stu-id="93f0b-247">This opens the **Alternate Access Mappings** box.</span></span>

  ![Alternatieve toegangstoewijzingen vak](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="93f0b-249">In de vervolgkeuzelijst naast **alternatieve toewijzing collectie**, selecteer **alternatieve toewijzing collectie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-249">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="93f0b-250">Selecteer uw site--bijvoorbeeld **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![Een site selecteren](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="93f0b-252">U kunt de gepubliceerde URL niet toevoegen als een interne URL of een openbare URL.</span><span class="sxs-lookup"><span data-stu-id="93f0b-252">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="93f0b-253">Dit voorbeeld wordt een openbare URL als het extranet.</span><span class="sxs-lookup"><span data-stu-id="93f0b-253">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="93f0b-254">Klik op **openbare URL's bewerken** in de **Extranet** pad, en voer vervolgens het pad voor de gepubliceerde toepassing, zoals in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="93f0b-254">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="93f0b-255">Voer bijvoorbeeld **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Het pad](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="93f0b-257">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93f0b-257">Click **Save**.</span></span>

 <span data-ttu-id="93f0b-258">U kunt nu toegang tot de SharePoint-site extern via Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="93f0b-258">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93f0b-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93f0b-259">Next steps</span></span>

- [<span data-ttu-id="93f0b-260">Het verstrekken van veilige externe toegang tot on-premises toepassingen</span><span class="sxs-lookup"><span data-stu-id="93f0b-260">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="93f0b-261">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="93f0b-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="93f0b-262">Publicatie van SharePoint 2016 en Office Online-Server met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="93f0b-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
