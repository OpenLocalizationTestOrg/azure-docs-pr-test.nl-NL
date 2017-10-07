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
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Azure Key Vault instellen met end-to-end sleutelrotatie en -controle
## <a name="introduction"></a>Inleiding
Na het maken van de sleutelkluis, kunt u zich kunt toostart die toostore kluis met behulp van uw sleutels en geheimen. Uw toepassingen niet langer toopersist uw sleutels of geheimen, maar in plaats daarvan wordt deze aanvragen op Hallo sleutelkluis indien nodig. Hiermee kunt u tooupdate sleutels en geheimen zonder Hallo gedrag van uw toepassing, wat een groot aantal mogelijkheden om uw sleutel en geheime management wordt geopend.

Dit artikel begeleidt bij een voorbeeld van het gebruik van Azure Sleutelkluis toostore een geheim, in dit geval een Azure Storage-Account-sleutel die is geopend door een toepassing. U ziet ook uitvoering van een geplande rotatie van de sleutel van die opslagaccount. Ten slotte wordt begeleid bij een demonstratie van hoe toomonitor Hallo sleutelkluis-logboeken voor controle en waarschuwingen genereren wanneer onverwachte aanvragen worden gedaan.

> [!NOTE]
> Deze zelfstudie is niet bedoeld tooexplain in detail Hallo eerste installatie van de sleutelkluis. Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie. Zie voor instructies platformoverschrijdende opdrachtregelinterface [Key Vault beheren met CLI](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Key Vault instellen
een toepassing tooretrieve een geheim tooenable uit Sleutelkluis, moet u eerst Hallo geheim maken en uploaden tooyour kluis. Dit kunt doen met Azure PowerShell-sessie starten en tooyour aanmelden met Azure-account met de volgende opdracht Hallo:

```powershell
Login-AzureRmAccount
```

In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord. PowerShell haalt alle abonnementen op Hallo die gekoppeld aan dit account zijn. Maakt gebruik van PowerShell Hallo eerste is standaard.

Als u meerdere abonnementen hebt, hebt u mogelijk toospecify Hallo die gebruikte toocreate is de sleutelkluis. Voer Hallo toosee Hallo abonnementen voor uw account te volgen:

```powershell
Get-AzureRmSubscription
```

toospecify hello abonnement dat is gekoppeld aan de sleutelkluis Hallo u logboekregistratie inschakelen wilt, voer:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Omdat dit artikel wordt beschreven voor het opslaan van de sleutel van een opslagaccount als een geheim, moet u die opslagaccountsleutel ophalen.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Bij het ophalen van het geheim (in dit geval wordt een sleutel van uw opslagaccount), moet u die beveiligde tekenreeks tooa converteren en vervolgens een geheim maken met de waarde in de sleutelkluis.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Haal vervolgens Hallo URI voor Hallo geheim die u hebt gemaakt. Dit wordt gebruikt in een latere stap wanneer u uw geheime Hallo sleutelkluis tooretrieve aanroepen. Hallo volgende PowerShell-opdracht uitvoeren en noteer Hallo-ID-waarde Hallo geheim URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Hallo-toepassing instellen
Nu dat u een geheim dat is opgeslagen hebt, kunt u code tooretrieve gebruiken en deze gebruiken. Er zijn een paar stappen vereist tooachieve dit. Hallo is eerste en belangrijkste stap het registreren van uw toepassing met Azure Active Directory en vervolgens melding Sleutelkluis de informatie over uw toepassing zodat deze aanvragen van uw toepassing.

> [!NOTE]
> Uw toepassing moet worden gemaakt op Hallo dezelfde Azure Active Directory-tenant als uw sleutelkluis.
>
>

Open het tabblad toepassingen Hallo van Azure Active Directory.

![Geopende toepassingen in Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Kies **toevoegen** tooadd een tooyour toepassing Azure Active Directory.

![Kies toevoegen](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Laat het toepassingstype Hallo als **WEBTOEPASSING en/of WEB-API** en geef een naam op voor uw toepassing.

![Naam Hallo-toepassing](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Geef de toepassing een **AANMELDINGS-URL** en een **APP ID URI**. Dit kunnen van alles die voor deze demo gewenste zijn en ze kunnen later worden gewijzigd indien nodig.

![Geef de vereiste URI 's](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Nadat de toepassing hello is tooAzure Active Directory worden toegevoegd, wordt u naar de pagina van de toepassing hello geopend. Klik op Hallo **configureren** tabblad en zoek vervolgens kopiëren Hallo **Client-ID** waarde. Noteer Hallo client-ID voor de volgende stappen.

Vervolgens wordt een sleutel genereren voor uw toepassing zodat deze met uw Azure Active Directory communiceren kan. U kunt dit onder Hallo maken **sleutels** sectie in Hallo **configuratie** tabblad. Let op Hallo zojuist gegenereerde sleutel van uw Azure Active Directory-toepassing voor gebruik in een latere stap.

![Sleutels voor Azure Active Directory-App](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Voordat er een aanroepen vanuit uw App in de sleutelkluis hello, moet u sleutelkluis Hallo Vertel over uw toepassing en de bijbehorende machtigingen. Hello volgende opdracht haalt de kluisnaam hello en Hallo client-ID van uw Azure Active Directory-app en verleent **ophalen** toegang tooyour sleutelkluis voor Hallo-toepassing.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

Op dit moment bent u klaar toostart bouwen van uw toepassing aanroepen. U moet in uw toepassing hello NuGet-pakketten vereist toointeract installeren met Azure Key Vault en Azure Active Directory. Voer Hallo opdrachten na van Hallo Visual Studio Package Manager-console. Huidige versie van Azure Active Directory-pakket Hallo Hallo is Hallo schrijven van dit artikel, 3.10.305231913, zodat u mogelijk tooconfirm Hallo meest recente versie wilt en dienovereenkomstig bijgewerkt.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

Maak een klasse toohold Hallo-methode voor uw Azure Active Directory-verificatie in uw toepassingscode. In dit voorbeeld die klasse wordt aangeroepen **Utils**. Voeg de volgende Hallo met de instructie:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Voeg vervolgens Hallo methode tooretrieve hello JWT-token van Azure Active Directory te volgen. Voor onderhoud kunt u toomove Hallo vastgelegde tekenreekswaarden in de configuratie van uw website of toepassing.

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

Hallo benodigde code toocall Sleutelkluis toevoegen en uw geheime waarde wordt opgehaald. Eerst moet u de volgende Hallo toevoegen met de instructie:

```csharp
using Microsoft.Azure.KeyVault;
```

Hallo-methode aanroepen tooinvoke Sleutelkluis toevoegen aan en ophalen van het geheim. In deze methode bieden u Hallo geheim URI die u hebt opgeslagen in de vorige stap. Houd er rekening mee Hallo gebruik van Hallo **GetToken** methode van Hallo **Utils** klasse eerder hebt gemaakt.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Wanneer u uw toepassing uitvoert, moet u nu worden verifiëren tooAzure Active Directory en vervolgens uw geheime waarde ophalen van Azure Sleutelkluis.

## <a name="key-rotation-using-azure-automation"></a>Sleutel rotatie met behulp van Azure Automation
Er zijn diverse opties voor het implementeren van een strategie worden gedraaid voor waarden die u als Azure Key Vault geheimen opslaan. Geheimen kunnen worden gedraaid als onderdeel van een handmatig proces, kan programmatisch met behulp van API-aanroepen worden gedraaid of ze in een automatiseringsscript kunnen worden gedraaid. Voor de toepassing hello van dit artikel, kunt u zich met Azure PowerShell in combinatie met Azure Automation toochange een toegangssleutel voor Azure Storage-Account. U wordt vervolgens een geheim sleutelkluis bijwerken met deze nieuwe sleutel.

tooallow Azure Automation tooset geheime waarden in de sleutelkluis, moet u Hallo client-ID ophalen voor Hallo verbinding met de naam AzureRunAsConnection die is gemaakt wanneer u uw exemplaar van Azure Automation tot stand gebracht. U kunt deze ID vinden door te kiezen **activa** van uw Azure Automation-exemplaar. Van daaruit, kiest u **verbindingen** en selecteer vervolgens Hallo **AzureRunAsConnection** principe service. Let op Hallo **toepassings-ID**.

![Azure Automation-client-ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

In **activa**, kies **Modules**. Van **Modules**, selecteer **galerie**, en zoek vervolgens naar en **importeren** bijgewerkte versies van elk van de volgende modules Hallo:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> Op Hallo schrijven van dit artikel, alleen hello toobe eerder is vermeld modules die nodig zijn bijgewerkt voor Hallo script te volgen. Als u merkt dat uw automation-taak is mislukt, moet u bevestigen dat u alle benodigde modules en de bijbehorende afhankelijkheden hebt geïmporteerd.
>
>

Nadat u hebt Hallo toepassings-ID opgehaald voor uw Azure Automation-verbinding, moet u de sleutelkluis zien dat deze toepassing toegang tooupdate geheimen in uw kluis heeft aan te geven. Dit kan worden bewerkstelligd met Hallo volgende PowerShell-opdracht:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Selecteer vervolgens **Runbooks** onder uw Azure Automation-instantie en selecteer vervolgens **een Runbook toevoegen**. Selecteer **Snelle invoer**. De naam van uw runbook en selecteer **PowerShell** als Hallo runbooktype. U hebt een beschrijving Hallo optie tooadd. Tot slot op **maken**.

![Runbook maken](./media/keyvault-keyrotation/Create_Runbook.png)

Plak de volgende PowerShell-script in Hallo editor deelvenster voor uw nieuwe runbook Hallo:

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

Kies in het deelvenster editor Hallo **testvenster** tootest uw script. Wanneer het Hallo-script wordt uitgevoerd zonder fouten, kunt u selecteren **publiceren**, en vervolgens kunt u een planning voor Hallo runbook weer in deelvenster Hallo runbook-configuratie toepassen.

## <a name="key-vault-auditing-pipeline"></a>Controle Sleutelkluis-pipeline
Wanneer u een sleutelkluis hebt ingesteld, kunt u toocollect controlelogboeken op toohello sleutelkluis toegangsaanvragen inschakelen. Deze logboeken worden opgeslagen in een aangewezen Azure Storage-account en kunnen worden opgevraagd, bewaakt en geanalyseerd. Hallo volgende scenario maakt gebruik van Azure functions, Azure logic apps en sleutelkluis audit logboeken toocreate een pijplijn toosend een e-mailbericht wanneer een app die overeenkomt met app-ID van de web-app Hallo Hallo geheimen uit Hallo kluis ophaalt.

Eerst moet u de sleutelkluis aanmelden inschakelen. U kunt dit doen via de volgende PowerShell-opdrachten hello (alle gegevens die kunnen worden weergegeven wanneer [sleutel kluis registreren](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Nadat dit is ingeschakeld, wordt de auditlogboeken start verzamelen in Hallo aangewezen storage-account. Deze logboeken bevatten gebeurtenissen over hoe en wanneer uw sleutelkluizen toegankelijk zijn en door wie.

> [!NOTE]
> U kunt uw logboekgegevens 10 minuten nadat de Hallo sleutelkluis opnieuw openen. Dit wordt meestal sneller worden.
>
>

de volgende stap Hallo is te[maken van een Azure Service Bus-wachtrij](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Dit is waar sleutelkluis controlelogboeken worden gepusht. Wanneer berichten voor het controlelogboek Hallo in de wachtrij hello zijn, wordt Hallo logische app ze opgehaald en op deze fungeert. Een servicebus Maak met Hallo stappen te volgen:

1. Maken van een Service Bus-naamruimte (als u al hebt die u wilt toouse hiervoor overslaan tooStep 2).
2. Blader toohello servicebus in hello Azure-portal en selecteer Hallo naamruimte die u wilt dat toocreate Hallo wachtrij in.
3. Selecteer **nieuw** en kies **Service Bus > wachtrij** en voer de details Hallo vereist.
4. Selecteer Hallo Service Bus-verbindingsinformatie Hallo naamruimte kiezen en op **verbindingsgegevens**. U moet deze informatie gebruiken voor de volgende sectie Hallo.

Vervolgens [maken van een Azure-functie](../azure-functions/functions-create-first-azure-function.md) toopoll sleutelkluis-logboeken binnen Hallo storage-account en nieuwe gebeurtenissen kunnen worden opgepikt. Dit is een functie die volgens een planning wordt geactiveerd.

een Azure-functie toocreate kiezen **Nieuw > functie-App** in hello Azure-portal. U kunt tijdens het maken van een bestaand abonnement hosting gebruiken of een nieuwe maken. U kunt ook kiezen voor het hosten van dynamische. Meer informatie over de functie opties host kunnen worden gevonden op [hoe tooscale Azure Functions](../azure-functions/functions-scale.md).

Wanneer hello Azure-functie is gemaakt, gaat u tooit en kiest u een timer functie en C\#. Klik vervolgens op **maken van deze functie**.

![Blade van Azure Functions starten](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Op Hallo **ontwikkelen** tabblad, vervangen door de volgende Hallo Hallo run.csx code:

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
> Zorg ervoor tooreplace Hallo variabelen in de voorgaande code toopoint tooyour opslagaccount waar Hallo sleutelkluis-logboeken worden geschreven, Hallo Hallo servicebus die u eerder hebt gemaakt, en Hallo specifiek pad toohello sleutelkluis-logboeken voor opslag.
>
>

Hallo functie Hallo nieuwste logboekbestand vanuit Hallo opslagaccount waar Hallo sleutelkluis-logboeken worden geschreven, grijpers Hallo meest recente gebeurtenissen van dat bestand opneemt en stuurt ze tooa Service Bus-wachtrij. Aangezien één enkel bestand meerdere gebeurtenissen hebben kan, moet u een sync.txt-bestand dat Hallo-functie wordt ook gezocht op toodetermine Hallo tijdstempel van Hallo laatste gebeurtenis die is opgehaald. Dit zorgt ervoor dat u push niet meerdere keren voor dezelfde gebeurtenis Hallo. Dit bestand sync.txt bevat een tijdstempel voor laatste aangetroffen Hallo-gebeurtenis. Hallo Logboeken, wanneer zijn geladen, hebben toobe gesorteerd op basis van Hallo tijdstempel tooensure ze correct zijn gerangschikt.

Voor deze functie, verwijzen we naar een aantal aanvullende bibliotheken die niet beschikbaar is buiten het Hallo-vak in Azure Functions. tooinclude, moeten we Azure Functions toopull ze met NuGet. Kies Hallo **bestanden weergeven** optie.

![Optie bestanden weergeven](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

En toevoegen van een bestand met de naam project.json met de volgende inhoud:

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
Bij **opslaan**, Azure Functions Hallo vereist binaire bestanden worden gedownload.

Overschakelen van toohello **integreren** tabblad en geef Hallo timer parameter een betekenisvolle naam toouse binnen Hallo-functie. Hallo voorafgaand aan code, het Hallo timer toobe aangeroepen verwacht *myTimer*. Geef een [CRON expressie](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) als volgt: 0 \* \* \* \* \* voor Hallo timer waardoor Hallo functie toorun minuut.

Hallo op dezelfde **integreren** tabblad, het toevoegen van de invoer van het type Hallo **Azure Blob Storage**. Dit verwijst toohello sync.txt-bestand met de Hallo tijdstempel van de laatste gebeurtenis Hallo bekeken door Hallo functie. Dit zijn beschikbaar binnen de functie Hallo door Hallo parameternaam. Hallo voorafgaand aan code, hello Azure Blob Storage invoer verwacht Hallo parameter name toobe *inputBlob*. Kies Hallo opslagaccount waarin Hallo sync.txt bestand wordt opgeslagen (kan de zijn dezelfde of een ander opslagaccount Hallo). Geef in het veld pad Hallo Hallo pad op waar Hallo bestand Hallo indeling {container-name}/path/to/sync.txt woont.

Toevoegen van de uitvoer van het type Hallo *Azure Blob Storage* uitvoer. Dit verwijst toohello sync.txt bestand die u hebt gedefinieerd in de invoer Hallo. Dit wordt gebruikt door Hallo functie toowrite Hallo tijdstempel van de laatste gebeurtenis Hallo bekeken. Hallo voorafgaande code verwacht deze parameter toobe aangeroepen *outputBlob*.

Hallo-functie is nu gereed. Zorg ervoor dat tooswitch back toohello **ontwikkelen** tabblad en Hallo-code op te slaan. Hallo uitvoervenster voor eventuele compileerfouten Controleer en corrigeer deze dienovereenkomstig. Als het Hallo-code wordt gecompileerd, Hallo-code moet nu worden controleren Hallo sleutelkluis-logboeken elke minuut en Service Bus-wachtrij pushen van alle nieuwe gebeurtenissen op Hallo gedefinieerd. U ziet logboekinformatie venster toohello-logboek schrijven telkens wanneer de functie hello wordt geactiveerd.

### <a name="azure-logic-app"></a>Azure logic app
Vervolgens moet u een Azure logic app die Hallo gebeurtenissen Hallo functie toohello Service Bus-wachtrij is gepusht opneemt, parseert Hallo inhoud en verzendt een e-mail op basis van een voorwaarde wordt aangepast maken.

[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) door te gaan**Nieuw > logische App**.

Zodra Hallo logische app is gemaakt, gaat u tooit en kies **bewerken**. Kies binnen Hallo logic app-editor **Service Bus-wachtrij** en voer uw referenties Service Bus tooconnect het toohello wachtrij.

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Kies vervolgens **een voorwaarde toevoegen**. In Hallo voorwaarde toohello geavanceerde editor switch en Voer Hallo code te volgen, APP_ID vervangen door een Hallo werkelijke APP_ID van uw web-app:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Deze expressie retourneert in wezen **false** als hello *appid* van Hallo inkomende gebeurtenis (dit is de instantie van Service Bus het Hallo-bericht Hallo) niet is Hallo *appid* Hallo App.

Maak nu een actie onder **zo Nee, niets doen**.

![Azure Logic App kiezen actie](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Hallo actie, kiest u **Office 365 - e-mailbericht verzenden**. Invullen Hallo velden toocreate een e-toosend wanneer Hallo gedefinieerd voorwaarde retourneert **false**. Als u geen Office 365 hebt, kunt u alternatieven bekijkt tooachieve Hallo dezelfde resultaten.

U hebt op dit moment een end-tooend pijplijn die naar de nieuwe sleutelkluis controlelogboeken minuut zoekt. Deze stuurt nieuwe logboeken vindt tooa service bus-wachtrij. Hallo logische app wordt geactiveerd wanneer een nieuw bericht in de wachtrij Hallo terechtkomt. Als hello *appid* binnen Hallo gebeurtenis komt niet overeen met Hallo app-ID van het aanroepen van de toepassing hello, zendt het een e-mailbericht.
