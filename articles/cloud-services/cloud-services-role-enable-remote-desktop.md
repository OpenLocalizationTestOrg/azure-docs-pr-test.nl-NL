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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen

> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klassieke Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

U kunt een verbinding met extern bureaublad in uw rol tijdens het ontwikkelen van inschakelen door Hallo extern bureaublad-modules in de servicedefinitie van de of u kunt tooenable extern bureaublad via Hallo uitbreidingsmodule Extern bureaublad. Hallo is gewenste aanpak toouse Hallo extern bureaublad-uitbreiding zoals u extern bureaublad inschakelen kunt, zelfs nadat de toepassing hello zonder tooredeploy uw toepassing wordt geïmplementeerd.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Extern bureaublad configureren via Hallo klassieke Azure-portal
Hallo klassieke Azure-portal gebruikt Hallo uitbreidingsmodule Extern bureaublad-benadering, zodat u extern bureaublad inschakelen kunt, zelfs nadat het Hallo-toepassing wordt geïmplementeerd. Hallo **configureren** voor uw cloudservice op de pagina kunt u tooenable extern bureaublad, wijziging Hallo lokale Administrator-account gebruikt tooconnect toohello virtuele machines, Hallo certificaat gebruikt bij de verificatie en Hallo instellen de vervaldatum.

1. Klik op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **configureren**.
2. Klik op Hallo **externe** knop Hallo onder aan.

    ![Externe cloudservices](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > Alle exemplaren van de functie wordt opnieuw gestart wanneer u eerst Extern bureaublad inschakelen en klik op OK (vinkje). tooprevent opnieuw worden opgestart, gebruikte tooencrypt Hallo-Hallo certificaatwachtwoord moet worden geïnstalleerd op Hallo-rol. tooprevent opnieuw is opgestart, [upload een certificaat voor de cloudservice hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) en ga daarna terug toothis dialoogvenster.

3. In **rollen**, selecteer Hallo rol of wilt u tooupdate Selecteer **alle** voor alle functies.
4. Breng een Hallo volgende wijzigingen aan:

   * Extern bureaublad, selecteer Hallo tooenable **extern bureaublad inschakelen** selectievakje. Extern bureaublad, schakel Hallo selectievakje toodisable.
   * Maken van een account toouse in extern bureaublad-verbindingen toohello rolinstanties.
   * Wachtwoord voor het bestaande account Hallo Hallo bijwerken.
   * Selecteer een toouse geüploade certificaat voor verificatie (uploaden Hallo certificaat gebruiken **uploaden** op Hallo **certificaten** pagina) of een nieuw certificaat maken.
   * Wijzig de vervaldatum Hallo Hallo configuratie van extern bureaublad.

5. Wanneer u klaar bent met de updates voor uw configuratie, klikt u op **OK** (vinkje).

## <a name="remote-into-role-instances"></a>De afstand in rolinstanties
Zodra de extern bureaublad is ingeschakeld op Hallo-functies kunt u externe in een rolinstantie via verschillende hulpprogramma's.

tooconnect tooa rolinstantie van Hallo klassieke Azure-portal:

1. Klik op **exemplaren** tooopen hello **exemplaren** pagina.
2. Selecteer een rolexemplaar met extern bureaublad die zijn geconfigureerd.
3. Klik op **Connect**, en volgt u Hallo instructies tooopen Hallo bureaublad.
4. Klik op **Open** en vervolgens **Connect** toostart Hallo extern bureaublad-verbinding.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Visual Studio tooremote gebruiken in een rolinstantie
In Visual Studio Server Explorer:

1. Vouw Hallo **Azure** > **Cloudservices** > **[cloudservicenaam]** knooppunt.
2. Vouw ofwel **fasering** of **productie**.
3. Vouw Hallo afzonderlijke rol.
4. Met de rechtermuisknop op een van de rolinstanties hello, klikt u op **verbinding maken met behulp van extern bureaublad...** , en voer vervolgens het Hallo-gebruikersnaam en wachtwoord.

![Server explorer extern bureaublad](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Gebruik PowerShell tooget Hallo RDP-bestand
U kunt Hallo [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve Hallo RDP-bestand. U kunt vervolgens Hallo RDP-bestand met verbinding met extern bureaublad tooaccess Hallo-cloudservice.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Hallo RDP-bestand via REST API van Opslagservicebeheer Hallo softwarematig downloaden
U kunt Hallo [RDP-bestand downloaden](https://msdn.microsoft.com/library/jj157183.aspx) REST bewerking toodownload Hallo RDP-bestand.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>Extern bureaublad in het servicedefinitiebestand hello tooconfigure
Deze methode kunt u tooenable extern bureaublad voor de toepassing hello tijdens de ontwikkeling. Deze methode moet de versleutelde wachtwoorden worden opgeslagen in de serviceconfiguratie bestands- en eventuele updates toohello configuratie van extern bureaublad vereist een nieuwe installatie van de toepassing hello. Als u tooavoid basis deze Hallo extern bureaublad-uitbreiding moet u de nadelen benadering die hierboven worden beschreven.  

U kunt Visual Studio te gebruiken[een verbinding met extern bureaublad inschakelen](../vs-azure-tools-remote-desktop-roles.md) met Hallo service definitie bestand benadering.  
Hallo stappen hieronder wordt beschreven Hallo wijzigingen nodig toohello service model-bestanden tooenable extern bureaublad. Visual Studio wordt automatisch deze wijzigingen aanbrengt bij het publiceren van.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Hallo-verbinding in het servicemodel Hallo instellen
Gebruik Hallo **invoer** element tooimport hello **RemoteAccess** module en Hallo **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) bestand.

Hallo servicedefinitiebestand moet vergelijkbaar toohello volgt Hello `<Imports>` element toegevoegd.

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
Hallo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) bestand moet worden vergelijkbare toohello voorbeeld te volgen, houd er rekening mee Hallo `<ConfigurationSettings>` en `<Certificates>` elementen. Hallo opgegeven certificaat moet [toohello cloudservice geüpload](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

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


## <a name="additional-resources"></a>Aanvullende resources
[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)
