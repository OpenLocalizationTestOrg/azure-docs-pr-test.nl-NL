---
title: aaaDeploy en beheren van Notification Hubs met behulp van PowerShell
description: Hoe tooCreate en beheren van Notification Hubs met behulp van PowerShell voor automatisering
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Notification Hubs implementeren en beheren met PowerShell
## <a name="overview"></a>Overzicht
In dit artikel leest u hoe toouse maken en beheren van Azure Notification Hubs met behulp van PowerShell. Hallo volgen algemene automatiseringstaken worden weergegeven in dit onderwerp.

* Een Notification Hub maken
* Referenties instellen

Als u ook een nieuwe service bus-naamruimte toocreate voor uw notification hubs moet, Zie [Service Bus beheren met PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Het beheren van meldingen Hubs wordt rechtstreeks door Hallo-cmdlets die zijn opgenomen met Azure PowerShell niet ondersteund. Hallo aanbevolen aanpak van PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly. Hallo-assembly is gedistribueerd met Hallo [Microsoft Azure Notification Hubs NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* Een Azure-abonnement. Azure is een platform op basis van abonnement. Zie voor meer informatie over het verkrijgen van een abonnement [koopopties], [lid biedt], of [gratis proefversie].
* Een computer met Azure PowerShell. Zie voor instructies [installeren en configureren van Azure PowerShell].
* Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Met inbegrip van een verwijzing toohello .NET-assembly voor Service Bus
Het beheren van Azure Notification Hubs is nog niet opgenomen in Hallo PowerShell-cmdlets in Azure PowerShell. tooprovision notification hubs, kunt u Hallo .NET client die wordt geleverd in Hallo [Microsoft Azure Notification Hubs NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Controleer eerst of uw script kan vinden Hallo **Microsoft.Azure.NotificationHubs.dll** assembly die wordt geïnstalleerd als een NuGet-pakket in Visual Studio-project. In de volgorde toobe flexibele voert Hallo script deze stappen uit:

1. Hiermee wordt bepaald Hallo pad waarop deze is aangeroepen.
2. Traverses Hallo pad totdat er een map met de naam gevonden `packages`. Deze map wordt gemaakt tijdens de installatie van NuGet-pakketten voor Visual Studio-projecten.
3. Recursief zoekopdrachten Hallo `packages` map voor een assembly met de naam **Microsoft.Azure.NotificationHubs.dll**.
4. Verwijzingen Hallo assembly zodat Hallo-typen beschikbaar voor later gebruik zijn.

Hier ziet u hoe deze stappen worden geïmplementeerd in een PowerShell-script:

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>Hallo NamespaceManager klasse maken
tooprovision Notification Hubs, geen exemplaar maken van Hallo [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) klasse vanuit Hallo SDK. 

U kunt Hallo [Get-AzureSBAuthorizationRule] cmdlet die deel uitmaakt van Azure PowerShell tooretrieve een autorisatieregel die tooprovide een verbindingsreeks is gebruikt. Bewaren wij een verwijzing toohello `NamespaceManager` exemplaar in Hallo `$NamespaceManager` variabele. We gebruiken `$NamespaceManager` tooprovision een notification hub.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Inrichting van een nieuwe Notification Hub
een nieuwe notification hub tooprovision gebruiken Hallo [.NET API voor Notification Hubs].

In dit gedeelte van het script Hallo instellen u vier lokale variabelen. 

1. `$Namespace`: Deze toohello naam instellen van de naamruimte Hallo waar u toocreate een notification hub.
2. `$Path`: Stel deze padnaam toohello van Hallo nieuwe notification hub.  Bijvoorbeeld 'MyHub'.    
3. `$WnsPackageSid`: Het instellen van deze toohello pakket-SID voor u Windows-App vanuit de Hallo [Windows-ontwikkelaarscentrum](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Het instellen van de geheime sleutel van deze toohello voor u Windows-App vanuit de Hallo [Windows-ontwikkelaarscentrum](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Deze variabelen gebruikte tooconnect tooyour naamruimte zijn en maak een nieuwe Notification Hub geconfigureerd toohandle meldingen Windows Notification Services (WNS) met WNS-referenties voor een Windows-App. Voor informatie over het verkrijgen van Hallo pakket-SID en de geheime sleutel Zie hello [aan de slag met Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) zelfstudie. 

* Hallo script codefragment gebruikt Hallo `NamespaceManager` als Hallo Notification Hub wordt aangeduid met object-toocheck toosee `$Path` bestaat.
* Als deze niet bestaat nog, Hallo script maakt een `NotificationHubDescription` referenties met WNS en doorgeven dat toohello `NamespaceManager` klasse `CreateNotificationHub` methode.

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Aanvullende resources
* [Servicebus met PowerShell beheren](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Hoe toocreate Service Bus-wachtrijen, onderwerpen en abonnementen op basis van een PowerShell-script](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Hoe toocreate een Service Bus Namespace en een Event Hub met een PowerShell-script](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Er zijn ook enkele kant-en-scripts downloaden:

* [Service Bus PowerShell-Scripts](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[koopopties]: http://azure.microsoft.com/pricing/purchase-options/
[lid biedt]: http://azure.microsoft.com/pricing/member-offers/
[gratis proefversie]: http://azure.microsoft.com/pricing/free-trial/
[installeren en configureren van Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET API voor Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

