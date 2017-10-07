---
title: aaaSet een Azure Service Fabric-cluster | Microsoft Docs
description: Quick Start - Maak een Service Fabric-cluster voor Windows of Linux in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Uw eerste Service Fabric-cluster maken in Azure
Een [Service Fabric-cluster](service-fabric-deploy-anywhere.md) is een met het netwerk verbonden reeks virtuele of fysieke machines waarop uw microservices worden geïmplementeerd en beheerd. Deze snelstartgids kunt u een cluster met vijf knooppunten, uitgevoerd op Windows of Linux, via Hallo toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) of [Azure-portal](http://portal.azure.com) over een paar minuten.  

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.


## <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal

Meld u bij toohello Azure-portal op [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Hallo-cluster maken

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.
2. Selecteer **Compute** van Hallo **nieuw** blade en selecteer vervolgens **Service Fabric-Cluster** van Hallo **Compute** blade.
3. Hallo Service Fabric invullen **basisbeginselen** formulier. Voor **besturingssysteem**, selecteer Hallo-versie van Windows of Linux die u wilt dat cluster knooppunten toorun Hallo. Hallo-gebruikersnaam en wachtwoord die u hier invoert is gebruikte toolog in toohello virtuele machine. Selecteer een **resourcegroep** of maak een nieuwe. Een resourcegroep is een logische container waarin Azure-resources worden gemaakt en waarin ze collectief worden beheerd. Na het voltooien klikt u op **OK**.

    ![Cluster-installatieuitvoer][cluster-setup-basics]

4. Hallo invullen **clusterconfiguratie** formulier.  Voer voor **Aantal knooppunttype** de waarde '1' in.

5. Selecteer **knooppunttype 1 (primair)** en invullen Hallo **type knooppuntconfiguratie** formulier.  Voer de naam van een knooppunt en stel Hallo [duurzaamheid laag](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) te 'Brons'.  Selecteer een VM-grootte.

    Knooppunttypen definiëren Hallo VM-grootte, het aantal virtuele machines, aangepaste eindpunten en andere instellingen voor virtuele machines van dat type Hallo. Elk knooppunttype gedefinieerd is ingesteld als een afzonderlijke virtuele-machineschaalset weergeven, die gebruikt toodeploy en beheerde virtuele machines als een set is. Elk knooppunttype kan onafhankelijk omhoog of omlaag worden geschaald, verschillende open poorten bevatten en verschillende capaciteitsstatistieken hebben.  Hallo eerste of primaire, knooppunttype is waar systeemservices Service Fabric worden gehost en vijf of meer virtuele machines moeten hebben.

    Bij elke implementatie voor productie is [capaciteitsplanning](service-fabric-cluster-capacity.md) van groot belang.  Voor deze Quick Start voert u echter geen toepassingen uit, dus selecteert u de VM-grootte *DS1_v2 Standard*.  Selecteer 'Silver' voor Hallo [betrouwbaarheidslaag](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) en een eerste virtuele-machineschaalset capaciteit van 5 instellen.  

    Aangepaste eindpunten openen van poorten in hello Azure load balancer zodat u verbinding kunt maken met toepassingen die worden uitgevoerd op Hallo-cluster.  Voer "80, 8172" tooopen up poorten 80 en 8172.

    Hallo niet controleren **geavanceerde instellingen configureren** vak dat wordt gebruikt voor het aanpassen van TCP/HTTP-eindpunten voor beheer, poortbereiken van toepassing, [plaatsingsbeperkingen](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), en [capaciteit eigenschappen](service-fabric-cluster-resource-manager-metrics.md).    

    Selecteer **OK**.

6. In Hallo **clusterconfiguratie** vormen, stelt u **Diagnostics** te**op**.  Voor deze snelstartgids, hoeft u niet tooenter ieder [fabric instelling](service-fabric-cluster-fabric-settings.md) eigenschappen.  In **Fabric-versie**, selecteer **automatische** upgrademodus zodat Microsoft hello versie van Hallo fabric code die wordt uitgevoerd Hallo cluster automatisch bijgewerkt.  Hallo-modus te instellen**handmatige** desgewenst te[kiest u een ondersteunde versie](service-fabric-cluster-upgrade.md) tooupgrade aan. 

    ![Configuratie van knooppunttypen][node-type-config]

    Selecteer **OK**.

7. Hallo invullen **beveiliging** formulier.  Voor deze Quick Start selecteert u **Onbeveiligd**.  U wordt ten zeerste aanbevolen toocreate een beveiligde cluster voor productieworkloads, echter, aangezien iedereen anoniem verbinding kunt tooan niet-beveiligde cluster en beheerbewerkingen uitvoeren.  

    Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen. Zie [Service Fabric-clusterbeveiligingsscenario's](service-fabric-cluster-security.md) voor meer informatie over hoe certificaten worden gebruikt in Service Fabric.  tooenable gebruikersverificatie met Azure Active Directory of tooset van certificaten voor Toepassingsbeveiliging, [een cluster maken van een Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md).

    Selecteer **OK**.

8. Controleer de hello samenvatting.  Als u wilt toodownload Resource Manager-sjabloon samengesteld uit Hallo-instellingen hebt ingevoerd, selecteert u **sjabloon en parameters downloaden**.  Selecteer **maken** toocreate Hallo-cluster.

    Voortgang van het Hallo maken in kennisgevingen hello, kunt u zien. (Klik op Hallo ' ' belpictogram bijna Hallo statusbalk Hallo rechterbovenhoek van het scherm). Als u hebt geklikt **pincode tooStartboard** tijdens het Hallo-cluster maken, ziet u **Service Fabric-Cluster implementeren** vastgemaakt toohello **Start** mededelingenbord.

### <a name="view-cluster-status"></a>De clusterstatus bekijken
Zodra het cluster is gemaakt, kunt u uw cluster in Hallo inspecteren **overzicht** blade in Hallo-portal. U ziet nu Hallo details van het cluster in Hallo-dashboard, met inbegrip van het cluster Hallo openbaar eindpunt en een koppeling tooService Fabric Explorer.

![De clusterstatus][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Hallo-cluster met Service Fabric explorer visualiseren
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een goed hulpmiddel om een cluster te visualiseren en toepassingen te beheren.  Service Fabric Explorer is een service die wordt uitgevoerd in Hallo-cluster.  Toegang tot dit met een webbrowser door te klikken op Hallo **Service Fabric Explorer** koppeling van Hallo cluster **overzicht** pagina in Hallo-portal.  U kunt ook Hallo adres invoeren rechtstreeks in de browser Hallo: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

Hallo cluster-dashboard biedt een overzicht van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status. Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster. Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Verbinding maken met behulp van PowerShell toohello-cluster
Controleer of dat Hallo-cluster wordt uitgevoerd door verbinding te maken met behulp van PowerShell.  Hallo ServiceFabric PowerShell-module is geïnstalleerd met Hallo [Service Fabric SDK](service-fabric-get-started.md).  Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stelt een verbinding toohello-cluster.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor andere voorbeelden van verbindende tooa cluster. Na het maken van verbinding toohello-cluster gebruiken Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet een lijst met knooppunten in het Hallo-cluster en de status van informatie voor elk knooppunt. **HealthState** moet *OK* zijn voor elk knooppunt.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Hallo-cluster verwijderen
Service Fabric-cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf. Zodat toocompletely verwijdert een Service Fabric-cluster moet u ook alle resources die wordt gemaakt van Hallo toodelete. Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep. Voor andere manieren toodelete een cluster of toodelete enkele (maar niet alle) Hallo-resources in een resourcegroep, Zie [een cluster verwijderen](service-fabric-cluster-delete.md)

Verwijderen van een resourcegroep in hello Azure-portal:
1. Navigeer toohello gewenste toodelete Service Fabric-cluster.
2. Klik op Hallo **resourcegroep** naam op Hallo cluster essentials pagina.
3. In Hallo **Resource groep Essentials** pagina, klikt u op **resourcegroep verwijderen** en volg Hallo-instructies op die pagina toocomplete Hallo verwijdering van de resourcegroep Hallo.
    ![Hallo-resourcegroep verwijderen][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Azure Powershell toodeploy een beveiligde cluster gebruiken
1. Hallo downloaden [Azure Powershell-moduleversie 4.0 of hoger](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) op uw computer.

2. Open een Windows PowerShell-venster uitvoeren Hallo opdracht te volgen. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    U ziet een uitvoer vergelijkbare toohello volgende.

    ![ps-list][ps-list]

3. Aanmelding tooAzure en selecteer Hallo abonnement toowhich u toocreate Hallo cluster wilt toevoegen

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Voer Hallo opdracht toonow na een beveiligde cluster maken. Vergeet niet toocustomize Hallo parameters. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    Hallo-opdracht kan duren 10 minuten too30 minuten toocomplete aan Hallo einde van het, krijgt u een vergelijkbare toohello volgende voor uitvoer. Hallo uitvoer bevat informatie over Hallo certificaat Hallo KeyVault waar deze is geüpload naar, en Hallo lokale map waarin Hallo-certificaat is gekopieerd. 

    ![ps-out][ps-out]

5. Kopieer de gehele uitvoer Hallo en tooa-tekstbestand opslaan als we toorefer tooit nodig. Maak een notitie van de volgende informatie uit de uitvoer Hallo Hallo. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Hallo-certificaat installeren op uw lokale computer
  
tooconnect toohello cluster, moet u tooinstall Hallo certificaat in archief van het persoonlijke (Mijn) van de huidige gebruiker Hallo Hallo. 

Hallo na PowerShell uitvoeren

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

U bent nu klaar tooconnect tooyour beveiligde cluster.

### <a name="connect-tooa-secure-cluster"></a>Verbinding maken met de beveiligde cluster tooa 

Hallo volgende PowerShell-opdracht tooconnect tooa beveiligde cluster worden uitgevoerd. Hallo certificaatdetails moeten overeenkomen met een certificaat dat gebruikt tooset Hallo-cluster is. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Hallo volgende voorbeeld toont Hallo voltooid parameters: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Voer Hallo na de opdracht toocheck dat u verbonden bent en Hallo-cluster is in orde.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publiceren van uw apps tooyour cluster vanuit Visual Studio

Nu dat u een Azure-cluster hebt ingesteld, kunt u uw tooit toepassingen vanuit Visual Studio door de volgende Hallo publiceren [publiceren tooan cluster](service-fabric-publish-app-remote-cluster.md) document. 

### <a name="remove-hello-cluster"></a>Hallo-cluster verwijderen
Een cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf. Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Volgende stappen
Nu u een ontwikkelcluster hebt ingesteld, proberen Hallo volgende:
* [Maken van een beveiligde cluster in Hallo-portal](service-fabric-cluster-creation-via-portal.md)
* [Een cluster maken op basis van een sjabloon](service-fabric-cluster-creation-via-arm.md) 
* [Apps implementeren met behulp van PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
