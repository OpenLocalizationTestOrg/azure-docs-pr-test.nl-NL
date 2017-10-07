---
title: aaaSet van Azure Sleutelkluis met end-to-end sleutel worden gedraaid en controle | Microsoft Docs
description: Gebruik deze procedure-tootoohelp die u met de sleutel worden gedraaid en bewaking sleutelkluis-logboeken ophalen instellen.
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="ad2d3-103">Azure Key Vault instellen met end-to-end sleutelrotatie en -controle</span><span class="sxs-lookup"><span data-stu-id="ad2d3-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="ad2d3-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="ad2d3-104">Introduction</span></span>
<span data-ttu-id="ad2d3-105">Na het maken van de sleutelkluis, kunt u zich kunt toostart die toostore kluis met behulp van uw sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="ad2d3-106">Uw toepassingen niet langer toopersist uw sleutels of geheimen, maar in plaats daarvan wordt deze aanvragen op Hallo sleutelkluis indien nodig.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="ad2d3-107">Hiermee kunt u tooupdate sleutels en geheimen zonder Hallo gedrag van uw toepassing, wat een groot aantal mogelijkheden om uw sleutel en geheime management wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="ad2d3-108">Dit artikel begeleidt bij een voorbeeld van het gebruik van Azure Sleutelkluis toostore een geheim, in dit geval een Azure Storage-Account-sleutel die is geopend door een toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="ad2d3-109">U ziet ook uitvoering van een geplande rotatie van de sleutel van die opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="ad2d3-110">Ten slotte wordt begeleid bij een demonstratie van hoe toomonitor Hallo sleutelkluis-logboeken voor controle en waarschuwingen genereren wanneer onverwachte aanvragen worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2d3-111">Deze zelfstudie is niet bedoeld tooexplain in detail Hallo eerste installatie van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="ad2d3-112">Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="ad2d3-113">Zie voor instructies platformoverschrijdende opdrachtregelinterface [Key Vault beheren met CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="ad2d3-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="ad2d3-114">Key Vault instellen</span><span class="sxs-lookup"><span data-stu-id="ad2d3-114">Set up Key Vault</span></span>
<span data-ttu-id="ad2d3-115">een toepassing tooretrieve een geheim tooenable uit Sleutelkluis, moet u eerst Hallo geheim maken en uploaden tooyour kluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="ad2d3-116">Dit kunt doen met Azure PowerShell-sessie starten en tooyour aanmelden met Azure-account met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ad2d3-117">In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="ad2d3-118">PowerShell haalt alle abonnementen op Hallo die gekoppeld aan dit account zijn.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="ad2d3-119">Maakt gebruik van PowerShell Hallo eerste is standaard.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="ad2d3-120">Als u meerdere abonnementen hebt, hebt u mogelijk toospecify Hallo die gebruikte toocreate is de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="ad2d3-121">Voer Hallo toosee Hallo abonnementen voor uw account te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ad2d3-122">toospecify hello abonnement dat is gekoppeld aan de sleutelkluis Hallo u logboekregistratie inschakelen wilt, voer:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="ad2d3-123">Omdat dit artikel wordt beschreven voor het opslaan van de sleutel van een opslagaccount als een geheim, moet u die opslagaccountsleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="ad2d3-124">Bij het ophalen van het geheim (in dit geval wordt een sleutel van uw opslagaccount), moet u die beveiligde tekenreeks tooa converteren en vervolgens een geheim maken met de waarde in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="ad2d3-125">Haal vervolgens Hallo URI voor Hallo geheim die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="ad2d3-126">Dit wordt gebruikt in een latere stap wanneer u uw geheime Hallo sleutelkluis tooretrieve aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="ad2d3-127">Hallo volgende PowerShell-opdracht uitvoeren en noteer Hallo-ID-waarde Hallo geheim URI:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="ad2d3-128">Hallo-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="ad2d3-128">Set up hello application</span></span>
<span data-ttu-id="ad2d3-129">Nu dat u een geheim dat is opgeslagen hebt, kunt u code tooretrieve gebruiken en deze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="ad2d3-130">Er zijn een paar stappen vereist tooachieve dit.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="ad2d3-131">Hallo is eerste en belangrijkste stap het registreren van uw toepassing met Azure Active Directory en vervolgens melding Sleutelkluis de informatie over uw toepassing zodat deze aanvragen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2d3-132">Uw toepassing moet worden gemaakt op Hallo dezelfde Azure Active Directory-tenant als uw sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="ad2d3-133">Open het tabblad toepassingen Hallo van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-133">Open hello applications tab of Azure Active Directory.</span></span>

![Geopende toepassingen in Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="ad2d3-135">Kies **toevoegen** tooadd een tooyour toepassing Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Kies toevoegen](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="ad2d3-137">Laat het toepassingstype Hallo als **WEBTOEPASSING en/of WEB-API** en geef een naam op voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Naam Hallo-toepassing](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="ad2d3-139">Geef de toepassing een **AANMELDINGS-URL** en een **APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="ad2d3-140">Dit kunnen van alles die voor deze demo gewenste zijn en ze kunnen later worden gewijzigd indien nodig.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Geef de vereiste URI 's](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="ad2d3-142">Nadat de toepassing hello is tooAzure Active Directory worden toegevoegd, wordt u naar de pagina van de toepassing hello geopend.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="ad2d3-143">Klik op Hallo **configureren** tabblad en zoek vervolgens kopiëren Hallo **Client-ID** waarde.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="ad2d3-144">Noteer Hallo client-ID voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="ad2d3-145">Vervolgens wordt een sleutel genereren voor uw toepassing zodat deze met uw Azure Active Directory communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="ad2d3-146">U kunt dit onder Hallo maken **sleutels** sectie in Hallo **configuratie** tabblad. Let op Hallo zojuist gegenereerde sleutel van uw Azure Active Directory-toepassing voor gebruik in een latere stap.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Sleutels voor Azure Active Directory-App](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="ad2d3-148">Voordat er een aanroepen vanuit uw App in de sleutelkluis hello, moet u sleutelkluis Hallo Vertel over uw toepassing en de bijbehorende machtigingen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="ad2d3-149">Hello volgende opdracht haalt de kluisnaam hello en Hallo client-ID van uw Azure Active Directory-app en verleent **ophalen** toegang tooyour sleutelkluis voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="ad2d3-150">Op dit moment bent u klaar toostart bouwen van uw toepassing aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="ad2d3-151">U moet in uw toepassing hello NuGet-pakketten vereist toointeract installeren met Azure Key Vault en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="ad2d3-152">Voer Hallo opdrachten na van Hallo Visual Studio Package Manager-console.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="ad2d3-153">Huidige versie van Azure Active Directory-pakket Hallo Hallo is Hallo schrijven van dit artikel, 3.10.305231913, zodat u mogelijk tooconfirm Hallo meest recente versie wilt en dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="ad2d3-154">Maak een klasse toohold Hallo-methode voor uw Azure Active Directory-verificatie in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="ad2d3-155">In dit voorbeeld die klasse wordt aangeroepen **Utils**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="ad2d3-156">Voeg de volgende Hallo met de instructie:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ad2d3-157">Voeg vervolgens Hallo methode tooretrieve hello JWT-token van Azure Active Directory te volgen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="ad2d3-158">Voor onderhoud kunt u toomove Hallo vastgelegde tekenreekswaarden in de configuratie van uw website of toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="ad2d3-159">Hallo benodigde code toocall Sleutelkluis toevoegen en uw geheime waarde wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="ad2d3-160">Eerst moet u de volgende Hallo toevoegen met de instructie:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="ad2d3-161">Hallo-methode aanroepen tooinvoke Sleutelkluis toevoegen aan en ophalen van het geheim.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="ad2d3-162">In deze methode bieden u Hallo geheim URI die u hebt opgeslagen in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="ad2d3-163">Houd er rekening mee Hallo gebruik van Hallo **GetToken** methode van Hallo **Utils** klasse eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="ad2d3-164">Wanneer u uw toepassing uitvoert, moet u nu worden verifiëren tooAzure Active Directory en vervolgens uw geheime waarde ophalen van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="ad2d3-165">Sleutel rotatie met behulp van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ad2d3-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="ad2d3-166">Er zijn diverse opties voor het implementeren van een strategie worden gedraaid voor waarden die u als Azure Key Vault geheimen opslaan.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="ad2d3-167">Geheimen kunnen worden gedraaid als onderdeel van een handmatig proces, kan programmatisch met behulp van API-aanroepen worden gedraaid of ze in een automatiseringsscript kunnen worden gedraaid.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="ad2d3-168">Voor de toepassing hello van dit artikel, kunt u zich met Azure PowerShell in combinatie met Azure Automation toochange een toegangssleutel voor Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="ad2d3-169">U wordt vervolgens een geheim sleutelkluis bijwerken met deze nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="ad2d3-170">tooallow Azure Automation tooset geheime waarden in de sleutelkluis, moet u Hallo client-ID ophalen voor Hallo verbinding met de naam AzureRunAsConnection die is gemaakt wanneer u uw exemplaar van Azure Automation tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="ad2d3-171">U kunt deze ID vinden door te kiezen **activa** van uw Azure Automation-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="ad2d3-172">Van daaruit, kiest u **verbindingen** en selecteer vervolgens Hallo **AzureRunAsConnection** principe service.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="ad2d3-173">Let op Hallo **toepassings-ID**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-173">Take note of hello **Application ID**.</span></span>

![Azure Automation-client-ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="ad2d3-175">In **activa**, kies **Modules**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="ad2d3-176">Van **Modules**, selecteer **galerie**, en zoek vervolgens naar en **importeren** bijgewerkte versies van elk van de volgende modules Hallo:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="ad2d3-177">Op Hallo schrijven van dit artikel, alleen hello toobe eerder is vermeld modules die nodig zijn bijgewerkt voor Hallo script te volgen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="ad2d3-178">Als u merkt dat uw automation-taak is mislukt, moet u bevestigen dat u alle benodigde modules en de bijbehorende afhankelijkheden hebt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="ad2d3-179">Nadat u hebt Hallo toepassings-ID opgehaald voor uw Azure Automation-verbinding, moet u de sleutelkluis zien dat deze toepassing toegang tooupdate geheimen in uw kluis heeft aan te geven.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="ad2d3-180">Dit kan worden bewerkstelligd met Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="ad2d3-181">Selecteer vervolgens **Runbooks** onder uw Azure Automation-instantie en selecteer vervolgens **een Runbook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="ad2d3-182">Selecteer **Snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-182">Select **Quick Create**.</span></span> <span data-ttu-id="ad2d3-183">De naam van uw runbook en selecteer **PowerShell** als Hallo runbooktype.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="ad2d3-184">U hebt een beschrijving Hallo optie tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="ad2d3-185">Tot slot op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-185">Finally, click **Create**.</span></span>

![Runbook maken](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="ad2d3-187">Plak de volgende PowerShell-script in Hallo editor deelvenster voor uw nieuwe runbook Hallo:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="ad2d3-188">Kies in het deelvenster editor Hallo **testvenster** tootest uw script.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="ad2d3-189">Wanneer het Hallo-script wordt uitgevoerd zonder fouten, kunt u selecteren **publiceren**, en vervolgens kunt u een planning voor Hallo runbook weer in deelvenster Hallo runbook-configuratie toepassen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="ad2d3-190">Controle Sleutelkluis-pipeline</span><span class="sxs-lookup"><span data-stu-id="ad2d3-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="ad2d3-191">Wanneer u een sleutelkluis hebt ingesteld, kunt u toocollect controlelogboeken op toohello sleutelkluis toegangsaanvragen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="ad2d3-192">Deze logboeken worden opgeslagen in een aangewezen Azure Storage-account en kunnen worden opgevraagd, bewaakt en geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="ad2d3-193">Hallo volgende scenario maakt gebruik van Azure functions, Azure logic apps en sleutelkluis audit logboeken toocreate een pijplijn toosend een e-mailbericht wanneer een app die overeenkomt met app-ID van de web-app Hallo Hallo geheimen uit Hallo kluis ophaalt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="ad2d3-194">Eerst moet u de sleutelkluis aanmelden inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="ad2d3-195">U kunt dit doen via de volgende PowerShell-opdrachten hello (alle gegevens die kunnen worden weergegeven wanneer [sleutel kluis registreren](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="ad2d3-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="ad2d3-196">Nadat dit is ingeschakeld, wordt de auditlogboeken start verzamelen in Hallo aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="ad2d3-197">Deze logboeken bevatten gebeurtenissen over hoe en wanneer uw sleutelkluizen toegankelijk zijn en door wie.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2d3-198">U kunt uw logboekgegevens 10 minuten nadat de Hallo sleutelkluis opnieuw openen.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="ad2d3-199">Dit wordt meestal sneller worden.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="ad2d3-200">de volgende stap Hallo is te[maken van een Azure Service Bus-wachtrij](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ad2d3-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="ad2d3-201">Dit is waar sleutelkluis controlelogboeken worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="ad2d3-202">Wanneer berichten voor het controlelogboek Hallo in de wachtrij hello zijn, wordt Hallo logische app ze opgehaald en op deze fungeert.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="ad2d3-203">Een servicebus Maak met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="ad2d3-204">Maken van een Service Bus-naamruimte (als u al hebt die u wilt toouse hiervoor overslaan tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="ad2d3-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="ad2d3-205">Blader toohello servicebus in hello Azure-portal en selecteer Hallo naamruimte die u wilt dat toocreate Hallo wachtrij in.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="ad2d3-206">Selecteer **nieuw** en kies **Service Bus > wachtrij** en voer de details Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="ad2d3-207">Selecteer Hallo Service Bus-verbindingsinformatie Hallo naamruimte kiezen en op **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="ad2d3-208">U moet deze informatie gebruiken voor de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="ad2d3-209">Vervolgens [maken van een Azure-functie](../azure-functions/functions-create-first-azure-function.md) toopoll sleutelkluis-logboeken binnen Hallo storage-account en nieuwe gebeurtenissen kunnen worden opgepikt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="ad2d3-210">Dit is een functie die volgens een planning wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="ad2d3-211">een Azure-functie toocreate kiezen **Nieuw > functie-App** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="ad2d3-212">U kunt tijdens het maken van een bestaand abonnement hosting gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="ad2d3-213">U kunt ook kiezen voor het hosten van dynamische.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="ad2d3-214">Meer informatie over de functie opties host kunnen worden gevonden op [hoe tooscale Azure Functions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ad2d3-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="ad2d3-215">Wanneer hello Azure-functie is gemaakt, gaat u tooit en kiest u een timer functie en C\#.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="ad2d3-216">Klik vervolgens op **maken van deze functie**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-216">Then click **Create this function**.</span></span>

![Blade van Azure Functions starten](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="ad2d3-218">Op Hallo **ontwikkelen** tabblad, vervangen door de volgende Hallo Hallo run.csx code:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="ad2d3-219">Zorg ervoor tooreplace Hallo variabelen in de voorgaande code toopoint tooyour opslagaccount waar Hallo sleutelkluis-logboeken worden geschreven, Hallo Hallo servicebus die u eerder hebt gemaakt, en Hallo specifiek pad toohello sleutelkluis-logboeken voor opslag.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="ad2d3-220">Hallo functie Hallo nieuwste logboekbestand vanuit Hallo opslagaccount waar Hallo sleutelkluis-logboeken worden geschreven, grijpers Hallo meest recente gebeurtenissen van dat bestand opneemt en stuurt ze tooa Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="ad2d3-221">Aangezien één enkel bestand meerdere gebeurtenissen hebben kan, moet u een sync.txt-bestand dat Hallo-functie wordt ook gezocht op toodetermine Hallo tijdstempel van Hallo laatste gebeurtenis die is opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="ad2d3-222">Dit zorgt ervoor dat u push niet meerdere keren voor dezelfde gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="ad2d3-223">Dit bestand sync.txt bevat een tijdstempel voor laatste aangetroffen Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="ad2d3-224">Hallo Logboeken, wanneer zijn geladen, hebben toobe gesorteerd op basis van Hallo tijdstempel tooensure ze correct zijn gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="ad2d3-225">Voor deze functie, verwijzen we naar een aantal aanvullende bibliotheken die niet beschikbaar is buiten het Hallo-vak in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="ad2d3-226">tooinclude, moeten we Azure Functions toopull ze met NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="ad2d3-227">Kies Hallo **bestanden weergeven** optie.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-227">Choose hello **View Files** option.</span></span>

![Optie bestanden weergeven](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="ad2d3-229">En toevoegen van een bestand met de naam project.json met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="ad2d3-230">Bij **opslaan**, Azure Functions Hallo vereist binaire bestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="ad2d3-231">Overschakelen van toohello **integreren** tabblad en geef Hallo timer parameter een betekenisvolle naam toouse binnen Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="ad2d3-232">Hallo voorafgaand aan code, het Hallo timer toobe aangeroepen verwacht *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="ad2d3-233">Geef een [CRON expressie](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) als volgt: 0 \* \* \* \* \* voor Hallo timer waardoor Hallo functie toorun minuut.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="ad2d3-234">Hallo op dezelfde **integreren** tabblad, het toevoegen van de invoer van het type Hallo **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="ad2d3-235">Dit verwijst toohello sync.txt-bestand met de Hallo tijdstempel van de laatste gebeurtenis Hallo bekeken door Hallo functie.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="ad2d3-236">Dit zijn beschikbaar binnen de functie Hallo door Hallo parameternaam.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="ad2d3-237">Hallo voorafgaand aan code, hello Azure Blob Storage invoer verwacht Hallo parameter name toobe *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="ad2d3-238">Kies Hallo opslagaccount waarin Hallo sync.txt bestand wordt opgeslagen (kan de zijn dezelfde of een ander opslagaccount Hallo).</span><span class="sxs-lookup"><span data-stu-id="ad2d3-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="ad2d3-239">Geef in het veld pad Hallo Hallo pad op waar Hallo bestand Hallo indeling {container-name}/path/to/sync.txt woont.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="ad2d3-240">Toevoegen van de uitvoer van het type Hallo *Azure Blob Storage* uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="ad2d3-241">Dit verwijst toohello sync.txt bestand die u hebt gedefinieerd in de invoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="ad2d3-242">Dit wordt gebruikt door Hallo functie toowrite Hallo tijdstempel van de laatste gebeurtenis Hallo bekeken.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="ad2d3-243">Hallo voorafgaande code verwacht deze parameter toobe aangeroepen *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="ad2d3-244">Hallo-functie is nu gereed.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-244">At this point, hello function is ready.</span></span> <span data-ttu-id="ad2d3-245">Zorg ervoor dat tooswitch back toohello **ontwikkelen** tabblad en Hallo-code op te slaan.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="ad2d3-246">Hallo uitvoervenster voor eventuele compileerfouten Controleer en corrigeer deze dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="ad2d3-247">Als het Hallo-code wordt gecompileerd, Hallo-code moet nu worden controleren Hallo sleutelkluis-logboeken elke minuut en Service Bus-wachtrij pushen van alle nieuwe gebeurtenissen op Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="ad2d3-248">U ziet logboekinformatie venster toohello-logboek schrijven telkens wanneer de functie hello wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="ad2d3-249">Azure logic app</span><span class="sxs-lookup"><span data-stu-id="ad2d3-249">Azure logic app</span></span>
<span data-ttu-id="ad2d3-250">Vervolgens moet u een Azure logic app die Hallo gebeurtenissen Hallo functie toohello Service Bus-wachtrij is gepusht opneemt, parseert Hallo inhoud en verzendt een e-mail op basis van een voorwaarde wordt aangepast maken.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="ad2d3-251">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) door te gaan**Nieuw > logische App**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="ad2d3-252">Zodra Hallo logische app is gemaakt, gaat u tooit en kies **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="ad2d3-253">Kies binnen Hallo logic app-editor **Service Bus-wachtrij** en voer uw referenties Service Bus tooconnect het toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="ad2d3-255">Kies vervolgens **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="ad2d3-256">In Hallo voorwaarde toohello geavanceerde editor switch en Voer Hallo code te volgen, APP_ID vervangen door een Hallo werkelijke APP_ID van uw web-app:</span><span class="sxs-lookup"><span data-stu-id="ad2d3-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="ad2d3-257">Deze expressie retourneert in wezen **false** als hello *appid* van Hallo inkomende gebeurtenis (dit is de instantie van Service Bus het Hallo-bericht Hallo) niet is Hallo *appid* Hallo App.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="ad2d3-258">Maak nu een actie onder **zo Nee, niets doen**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure Logic App kiezen actie](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="ad2d3-260">Hallo actie, kiest u **Office 365 - e-mailbericht verzenden**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="ad2d3-261">Invullen Hallo velden toocreate een e-toosend wanneer Hallo gedefinieerd voorwaarde retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="ad2d3-262">Als u geen Office 365 hebt, kunt u alternatieven bekijkt tooachieve Hallo dezelfde resultaten.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="ad2d3-263">U hebt op dit moment een end-tooend pijplijn die naar de nieuwe sleutelkluis controlelogboeken minuut zoekt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="ad2d3-264">Deze stuurt nieuwe logboeken vindt tooa service bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="ad2d3-265">Hallo logische app wordt geactiveerd wanneer een nieuw bericht in de wachtrij Hallo terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="ad2d3-266">Als hello *appid* binnen Hallo gebeurtenis komt niet overeen met Hallo app-ID van het aanroepen van de toepassing hello, zendt het een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="ad2d3-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
