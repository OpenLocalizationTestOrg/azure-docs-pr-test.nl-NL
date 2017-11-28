---
title: 'Azure Active Directory Domain Services: Azure Active Directory Domain Services inschakelen | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="f491a-103">Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="f491a-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="f491a-104">Taak 3: Azure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="f491a-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="f491a-105">In deze taak schakelt u Azure Active Directory Domain Services (Azure AD DS) voor uw directory Hallo volgende stappen uit als volgt:</span><span class="sxs-lookup"><span data-stu-id="f491a-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="f491a-106">Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f491a-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f491a-107">Selecteer in het linkerdeelvenster Hallo Hallo **Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="f491a-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="f491a-108">Hello Azure Active Directory (Azure AD) tenant (directory) waarvoor u tooenable Azure AD DS wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f491a-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="f491a-110">Op Hallo **preview directory** pagina, klikt u op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f491a-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Tabblad Configureren van directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="f491a-112">Onder **domeinservices**, Hallo wijzigen **domeinservices inschakelen voor deze map** te optie**Ja**.</span><span class="sxs-lookup"><span data-stu-id="f491a-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="f491a-113">Extra configuratieopties voor Azure Active Directory Domain Services weergegeven op Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="f491a-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Domain Services inschakelen](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="f491a-115">Wanneer u Azure Active Directory Domain Services voor uw tenant inschakelt, wordt Azure AD genereert en Hallo Kerberos en NTLM referentie-hashes die vereist zijn voor het verifiëren van gebruikers opslaat.</span><span class="sxs-lookup"><span data-stu-id="f491a-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="f491a-116">Geef Hallo **DNS-domeinnaam van domeinservices**.</span><span class="sxs-lookup"><span data-stu-id="f491a-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="f491a-117">Hallo standaarddomeinnaam van Hallo-map (met een **. onmicrosoft.com** achtervoegsel) is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f491a-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="f491a-118">Hallo lijst bevat alle domeinen die zijn geconfigureerd voor uw Azure AD-directory, waaronder zowel geverifieerd en niet-geverifieerde domeinen die u op Hallo configureert **domeinen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f491a-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="f491a-119">U kunt ook een aangepaste domeinnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="f491a-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="f491a-120">In dit voorbeeld wordt de aangepaste domeinnaam Hallo is *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="f491a-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="f491a-121">Hallo-voorvoegsel van de opgegeven domeinnaam (bijvoorbeeld *contoso100* in Hallo *contoso100.com* domeinnaam) moet 15 of minder tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="f491a-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="f491a-122">U kunt geen Azure Active Directory Domain Services-domein maken met een voorvoegsel van meer dan 15 tekens.</span><span class="sxs-lookup"><span data-stu-id="f491a-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="f491a-123">Zorg ervoor dat die Hallo DNS-domeinnaam die u hebt gekozen voor Hallo beheerd domein nog niet bestaat in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="f491a-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="f491a-124">In het bijzonder of toosee controleren:</span><span class="sxs-lookup"><span data-stu-id="f491a-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="f491a-125">U hebt al een domein met Hallo dezelfde DNS-domeinnaam op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f491a-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="f491a-126">Hallo virtueel netwerk dat u hebt geselecteerd heeft een VPN-verbinding met uw on-premises netwerk, en u een domein met Hallo dezelfde DNS-domeinnaam op uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="f491a-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="f491a-127">U hebt een bestaande cloudservice met die naam op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f491a-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="f491a-128">Selecteer een virtueel netwerk waarop u wilt dat Azure Active Directory Domain Services toobe beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f491a-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="f491a-129">Selecteer Hallo virtueel netwerk en u hebt gemaakt in Hallo-toegewezen subnet **Connect domain services-toothis virtueel netwerk** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f491a-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="f491a-130">Houd ook rekening Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f491a-130">Also consider hello following:</span></span>

   * <span data-ttu-id="f491a-131">Zorg ervoor dat Hallo virtuele netwerk dat u hebt opgegeven tooan Azure-regio die wordt ondersteund door Azure Active Directory Domain Services behoort.</span><span class="sxs-lookup"><span data-stu-id="f491a-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f491a-132">tooascertain Hallo Azure-regio's waar Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="f491a-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="f491a-133">Virtuele netwerken die deel uitmaken van tooa regio waar Azure Active Directory Domain Services niet wordt ondersteund, worden niet weergegeven in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="f491a-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="f491a-134">Gebruik een specifieke subnet in het virtuele netwerk Hallo voor Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f491a-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f491a-135">Voer *niet* Selecteer Hallo gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="f491a-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="f491a-136">Zie [Aandachtspunten voor netwerken](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="f491a-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="f491a-137">Virtuele netwerken die zijn gemaakt met behulp van Azure Resource Manager niet op dezelfde manier in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="f491a-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="f491a-138">Virtuele netwerken op basis van Resource Manager worden momenteel niet ondersteund door Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f491a-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="f491a-139">tooenable Azure Active Directory Domain Services in het taakvenster Hallo onderin Hallo Hallo pagina, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f491a-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="f491a-140">Terwijl de Azure Active Directory Domain Services is ingeschakeld voor uw directory, Hallo pagina een status weer van *in behandeling*.</span><span class="sxs-lookup"><span data-stu-id="f491a-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Het venster Domain Services inschakelen](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="f491a-142">Azure Active Directory Domain Services zorgt voor maximale beschikbaarheid voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="f491a-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="f491a-143">Nadat u Azure Active Directory Domain Services hebt ingeschakeld, zijn Hallo IP-adressen op welk domein services beschikbaar in het virtuele netwerk Hallo is weergegeven één voor één opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f491a-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="f491a-144">Hallo tweede IP-adres kort na Hallo eerst weergegeven, zoals snel Hallo maximale beschikbaarheid is ingeschakeld voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="f491a-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="f491a-145">Wanneer maximale beschikbaarheid is geconfigureerd en actief is voor uw domein, ziet u twee IP-adressen in Hallo **domeinservices** sectie Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f491a-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="f491a-146">Na ongeveer 20 too30 minuten Hallo eerste IP-adres op welk domein services beschikbaar in het virtuele netwerk in Hallo is **IP-adres** op Hallo **configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="f491a-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Het venster Domain Services met het eerste IP-adres dat is ingericht](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="f491a-148">Wanneer maximale beschikbaarheid ingeschakeld voor uw domein is, worden twee IP-adressen op Hallo pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f491a-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="f491a-149">Het beheerde domein is op deze twee IP-adressen beschikbaar in het geselecteerde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="f491a-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="f491a-150">Houd er rekening mee Hallo twee IP-adressen zodat u Hallo DNS-instellingen voor het virtuele netwerk bijwerken kunt.</span><span class="sxs-lookup"><span data-stu-id="f491a-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="f491a-151">In dat geval kunt virtuele machines op Hallo virtueel netwerk tooconnect toohello domein voor bewerkingen, zoals domeindeelname.</span><span class="sxs-lookup"><span data-stu-id="f491a-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Het venster Domain Services met beide ingerichte IP-adressen](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="f491a-153">Afhankelijk van de grootte van de Hallo van uw Azure AD-tenant (bijvoorbeeld Hallo aantal gebruikers of groepen) duurt synchronisatie tooyour beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="f491a-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="f491a-154">Dit synchronisatieproces wordt op de achtergrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="f491a-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="f491a-155">Voor grote tenants met tienduizenden objecten duurt het mogelijk een dag of twee voor alle gebruikers, groepslidmaatschappen en referenties toobe gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="f491a-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="f491a-156">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="f491a-156">Next step</span></span>
[<span data-ttu-id="f491a-157">Taak 4: Hallo DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="f491a-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
