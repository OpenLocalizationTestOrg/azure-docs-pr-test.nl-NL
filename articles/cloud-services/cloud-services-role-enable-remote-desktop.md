---
title: Extern bureaublad in een Azure Cloud Service aaaEnable | Microsoft Docs
description: Hoe tooconfigure uw azure cloud service-toepassing tooallow extern bureaublad-verbindingen
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="86b1c-103">Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen</span><span class="sxs-lookup"><span data-stu-id="86b1c-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="86b1c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="86b1c-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="86b1c-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="86b1c-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="86b1c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86b1c-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="86b1c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86b1c-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="86b1c-108">U kunt een verbinding met extern bureaublad in uw rol tijdens het ontwikkelen van inschakelen door Hallo extern bureaublad-modules in de servicedefinitie van de of u kunt tooenable extern bureaublad via Hallo uitbreidingsmodule Extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="86b1c-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="86b1c-109">Hallo is gewenste aanpak toouse Hallo extern bureaublad-uitbreiding zoals u extern bureaublad inschakelen kunt, zelfs nadat de toepassing hello zonder tooredeploy uw toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="86b1c-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="86b1c-110">Extern bureaublad configureren via Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="86b1c-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="86b1c-111">Hallo klassieke Azure-portal gebruikt Hallo uitbreidingsmodule Extern bureaublad-benadering, zodat u extern bureaublad inschakelen kunt, zelfs nadat het Hallo-toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="86b1c-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="86b1c-112">Hallo **configureren** voor uw cloudservice op de pagina kunt u tooenable extern bureaublad, wijziging Hallo lokale Administrator-account gebruikt tooconnect toohello virtuele machines, Hallo certificaat gebruikt bij de verificatie en Hallo instellen de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="86b1c-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="86b1c-113">Klik op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="86b1c-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="86b1c-114">Klik op Hallo **externe** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="86b1c-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Externe cloudservices](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="86b1c-116">Alle exemplaren van de functie wordt opnieuw gestart wanneer u eerst Extern bureaublad inschakelen en klik op OK (vinkje).</span><span class="sxs-lookup"><span data-stu-id="86b1c-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="86b1c-117">tooprevent opnieuw worden opgestart, gebruikte tooencrypt Hallo-Hallo certificaatwachtwoord moet worden geïnstalleerd op Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="86b1c-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="86b1c-118">tooprevent opnieuw is opgestart, [upload een certificaat voor de cloudservice hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) en ga daarna terug toothis dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86b1c-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="86b1c-119">In **rollen**, selecteer Hallo rol of wilt u tooupdate Selecteer **alle** voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="86b1c-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="86b1c-120">Breng een Hallo volgende wijzigingen aan:</span><span class="sxs-lookup"><span data-stu-id="86b1c-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="86b1c-121">Extern bureaublad, selecteer Hallo tooenable **extern bureaublad inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="86b1c-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="86b1c-122">Extern bureaublad, schakel Hallo selectievakje toodisable.</span><span class="sxs-lookup"><span data-stu-id="86b1c-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="86b1c-123">Maken van een account toouse in extern bureaublad-verbindingen toohello rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="86b1c-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="86b1c-124">Wachtwoord voor het bestaande account Hallo Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="86b1c-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="86b1c-125">Selecteer een toouse geüploade certificaat voor verificatie (uploaden Hallo certificaat gebruiken **uploaden** op Hallo **certificaten** pagina) of een nieuw certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="86b1c-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="86b1c-126">Wijzig de vervaldatum Hallo Hallo configuratie van extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="86b1c-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="86b1c-127">Wanneer u klaar bent met de updates voor uw configuratie, klikt u op **OK** (vinkje).</span><span class="sxs-lookup"><span data-stu-id="86b1c-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="86b1c-128">De afstand in rolinstanties</span><span class="sxs-lookup"><span data-stu-id="86b1c-128">Remote into role instances</span></span>
<span data-ttu-id="86b1c-129">Zodra de extern bureaublad is ingeschakeld op Hallo-functies kunt u externe in een rolinstantie via verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="86b1c-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="86b1c-130">tooconnect tooa rolinstantie van Hallo klassieke Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="86b1c-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="86b1c-131">Klik op **exemplaren** tooopen hello **exemplaren** pagina.</span><span class="sxs-lookup"><span data-stu-id="86b1c-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="86b1c-132">Selecteer een rolexemplaar met extern bureaublad die zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="86b1c-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="86b1c-133">Klik op **Connect**, en volgt u Hallo instructies tooopen Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="86b1c-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="86b1c-134">Klik op **Open** en vervolgens **Connect** toostart Hallo extern bureaublad-verbinding.</span><span class="sxs-lookup"><span data-stu-id="86b1c-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="86b1c-135">Visual Studio tooremote gebruiken in een rolinstantie</span><span class="sxs-lookup"><span data-stu-id="86b1c-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="86b1c-136">In Visual Studio Server Explorer:</span><span class="sxs-lookup"><span data-stu-id="86b1c-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="86b1c-137">Vouw Hallo **Azure** > **Cloudservices** > **[cloudservicenaam]** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="86b1c-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="86b1c-138">Vouw ofwel **fasering** of **productie**.</span><span class="sxs-lookup"><span data-stu-id="86b1c-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="86b1c-139">Vouw Hallo afzonderlijke rol.</span><span class="sxs-lookup"><span data-stu-id="86b1c-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="86b1c-140">Met de rechtermuisknop op een van de rolinstanties hello, klikt u op **verbinding maken met behulp van extern bureaublad...** , en voer vervolgens het Hallo-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="86b1c-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Server explorer extern bureaublad](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="86b1c-142">Gebruik PowerShell tooget Hallo RDP-bestand</span><span class="sxs-lookup"><span data-stu-id="86b1c-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="86b1c-143">U kunt Hallo [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve Hallo RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="86b1c-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="86b1c-144">U kunt vervolgens Hallo RDP-bestand met verbinding met extern bureaublad tooaccess Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="86b1c-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="86b1c-145">Hallo RDP-bestand via REST API van Opslagservicebeheer Hallo softwarematig downloaden</span><span class="sxs-lookup"><span data-stu-id="86b1c-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="86b1c-146">U kunt Hallo [RDP-bestand downloaden](https://msdn.microsoft.com/library/jj157183.aspx) REST bewerking toodownload Hallo RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="86b1c-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="86b1c-147">Extern bureaublad in het servicedefinitiebestand hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="86b1c-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="86b1c-148">Deze methode kunt u tooenable extern bureaublad voor de toepassing hello tijdens de ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="86b1c-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="86b1c-149">Deze methode moet de versleutelde wachtwoorden worden opgeslagen in de serviceconfiguratie bestands- en eventuele updates toohello configuratie van extern bureaublad vereist een nieuwe installatie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="86b1c-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="86b1c-150">Als u tooavoid basis deze Hallo extern bureaublad-uitbreiding moet u de nadelen benadering die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="86b1c-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="86b1c-151">U kunt Visual Studio te gebruiken[een verbinding met extern bureaublad inschakelen](../vs-azure-tools-remote-desktop-roles.md) met Hallo service definitie bestand benadering.</span><span class="sxs-lookup"><span data-stu-id="86b1c-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="86b1c-152">Hallo stappen hieronder wordt beschreven Hallo wijzigingen nodig toohello service model-bestanden tooenable extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="86b1c-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="86b1c-153">Visual Studio wordt automatisch deze wijzigingen aanbrengt bij het publiceren van.</span><span class="sxs-lookup"><span data-stu-id="86b1c-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="86b1c-154">Hallo-verbinding in het servicemodel Hallo instellen</span><span class="sxs-lookup"><span data-stu-id="86b1c-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="86b1c-155">Gebruik Hallo **invoer** element tooimport hello **RemoteAccess** module en Hallo **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) bestand.</span><span class="sxs-lookup"><span data-stu-id="86b1c-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="86b1c-156">Hallo servicedefinitiebestand moet vergelijkbaar toohello volgt Hello `<Imports>` element toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="86b1c-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="86b1c-157">Hallo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) bestand moet worden vergelijkbare toohello voorbeeld te volgen, houd er rekening mee Hallo `<ConfigurationSettings>` en `<Certificates>` elementen.</span><span class="sxs-lookup"><span data-stu-id="86b1c-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="86b1c-158">Hallo opgegeven certificaat moet [toohello cloudservice geüpload](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="86b1c-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="86b1c-159">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="86b1c-159">Additional Resources</span></span>
<span data-ttu-id="86b1c-160">[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="86b1c-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
