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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="a295e-103">Notification Hubs implementeren en beheren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="a295e-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="a295e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a295e-104">Overview</span></span>
<span data-ttu-id="a295e-105">In dit artikel leest u hoe toouse maken en beheren van Azure Notification Hubs met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a295e-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="a295e-106">Hallo volgen algemene automatiseringstaken worden weergegeven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a295e-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="a295e-107">Een Notification Hub maken</span><span class="sxs-lookup"><span data-stu-id="a295e-107">Create a Notification Hub</span></span>
* <span data-ttu-id="a295e-108">Referenties instellen</span><span class="sxs-lookup"><span data-stu-id="a295e-108">Set Credentials</span></span>

<span data-ttu-id="a295e-109">Als u ook een nieuwe service bus-naamruimte toocreate voor uw notification hubs moet, Zie [Service Bus beheren met PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a295e-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="a295e-110">Het beheren van meldingen Hubs wordt rechtstreeks door Hallo-cmdlets die zijn opgenomen met Azure PowerShell niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a295e-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="a295e-111">Hallo aanbevolen aanpak van PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="a295e-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="a295e-112">Hallo-assembly is gedistribueerd met Hallo [Microsoft Azure Notification Hubs NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="a295e-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a295e-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a295e-113">Prerequisites</span></span>
<span data-ttu-id="a295e-114">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="a295e-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a295e-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a295e-115">An Azure subscription.</span></span> <span data-ttu-id="a295e-116">Azure is een platform op basis van abonnement.</span><span class="sxs-lookup"><span data-stu-id="a295e-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="a295e-117">Zie voor meer informatie over het verkrijgen van een abonnement [koopopties], [lid biedt], of [gratis proefversie].</span><span class="sxs-lookup"><span data-stu-id="a295e-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="a295e-118">Een computer met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a295e-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="a295e-119">Zie voor instructies [installeren en configureren van Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="a295e-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="a295e-120">Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a295e-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="a295e-121">Met inbegrip van een verwijzing toohello .NET-assembly voor Service Bus</span><span class="sxs-lookup"><span data-stu-id="a295e-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="a295e-122">Het beheren van Azure Notification Hubs is nog niet opgenomen in Hallo PowerShell-cmdlets in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a295e-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="a295e-123">tooprovision notification hubs, kunt u Hallo .NET client die wordt geleverd in Hallo [Microsoft Azure Notification Hubs NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="a295e-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="a295e-124">Controleer eerst of uw script kan vinden Hallo **Microsoft.Azure.NotificationHubs.dll** assembly die wordt geïnstalleerd als een NuGet-pakket in Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="a295e-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="a295e-125">In de volgorde toobe flexibele voert Hallo script deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a295e-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="a295e-126">Hiermee wordt bepaald Hallo pad waarop deze is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a295e-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="a295e-127">Traverses Hallo pad totdat er een map met de naam gevonden `packages`.</span><span class="sxs-lookup"><span data-stu-id="a295e-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="a295e-128">Deze map wordt gemaakt tijdens de installatie van NuGet-pakketten voor Visual Studio-projecten.</span><span class="sxs-lookup"><span data-stu-id="a295e-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="a295e-129">Recursief zoekopdrachten Hallo `packages` map voor een assembly met de naam **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="a295e-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="a295e-130">Verwijzingen Hallo assembly zodat Hallo-typen beschikbaar voor later gebruik zijn.</span><span class="sxs-lookup"><span data-stu-id="a295e-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="a295e-131">Hier ziet u hoe deze stappen worden geïmplementeerd in een PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="a295e-131">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="a295e-132">Hallo NamespaceManager klasse maken</span><span class="sxs-lookup"><span data-stu-id="a295e-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="a295e-133">tooprovision Notification Hubs, geen exemplaar maken van Hallo [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) klasse vanuit Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="a295e-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="a295e-134">U kunt Hallo [Get-AzureSBAuthorizationRule] cmdlet die deel uitmaakt van Azure PowerShell tooretrieve een autorisatieregel die tooprovide een verbindingsreeks is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a295e-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="a295e-135">Bewaren wij een verwijzing toohello `NamespaceManager` exemplaar in Hallo `$NamespaceManager` variabele.</span><span class="sxs-lookup"><span data-stu-id="a295e-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="a295e-136">We gebruiken `$NamespaceManager` tooprovision een notification hub.</span><span class="sxs-lookup"><span data-stu-id="a295e-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="a295e-137">Inrichting van een nieuwe Notification Hub</span><span class="sxs-lookup"><span data-stu-id="a295e-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="a295e-138">een nieuwe notification hub tooprovision gebruiken Hallo [.NET API voor Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a295e-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="a295e-139">In dit gedeelte van het script Hallo instellen u vier lokale variabelen.</span><span class="sxs-lookup"><span data-stu-id="a295e-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="a295e-140">`$Namespace`: Deze toohello naam instellen van de naamruimte Hallo waar u toocreate een notification hub.</span><span class="sxs-lookup"><span data-stu-id="a295e-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="a295e-141">`$Path`: Stel deze padnaam toohello van Hallo nieuwe notification hub.</span><span class="sxs-lookup"><span data-stu-id="a295e-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="a295e-142">Bijvoorbeeld 'MyHub'.</span><span class="sxs-lookup"><span data-stu-id="a295e-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="a295e-143">`$WnsPackageSid`: Het instellen van deze toohello pakket-SID voor u Windows-App vanuit de Hallo [Windows-ontwikkelaarscentrum](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a295e-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="a295e-144">`$WnsSecretkey`: Het instellen van de geheime sleutel van deze toohello voor u Windows-App vanuit de Hallo [Windows-ontwikkelaarscentrum](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a295e-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="a295e-145">Deze variabelen gebruikte tooconnect tooyour naamruimte zijn en maak een nieuwe Notification Hub geconfigureerd toohandle meldingen Windows Notification Services (WNS) met WNS-referenties voor een Windows-App.</span><span class="sxs-lookup"><span data-stu-id="a295e-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="a295e-146">Voor informatie over het verkrijgen van Hallo pakket-SID en de geheime sleutel Zie hello [aan de slag met Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a295e-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="a295e-147">Hallo script codefragment gebruikt Hallo `NamespaceManager` als Hallo Notification Hub wordt aangeduid met object-toocheck toosee `$Path` bestaat.</span><span class="sxs-lookup"><span data-stu-id="a295e-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="a295e-148">Als deze niet bestaat nog, Hallo script maakt een `NotificationHubDescription` referenties met WNS en doorgeven dat toohello `NamespaceManager` klasse `CreateNotificationHub` methode.</span><span class="sxs-lookup"><span data-stu-id="a295e-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="a295e-149">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="a295e-149">Additional Resources</span></span>
* [<span data-ttu-id="a295e-150">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="a295e-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="a295e-151">Hoe toocreate Service Bus-wachtrijen, onderwerpen en abonnementen op basis van een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="a295e-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="a295e-152">Hoe toocreate een Service Bus Namespace en een Event Hub met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="a295e-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="a295e-153">Er zijn ook enkele kant-en-scripts downloaden:</span><span class="sxs-lookup"><span data-stu-id="a295e-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="a295e-154">Service Bus PowerShell-Scripts</span><span class="sxs-lookup"><span data-stu-id="a295e-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[koopopties]: http://azure.microsoft.com/pricing/purchase-options/
[lid biedt]: http://azure.microsoft.com/pricing/member-offers/
[gratis proefversie]: http://azure.microsoft.com/pricing/free-trial/
[installeren en configureren van Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET API voor Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

