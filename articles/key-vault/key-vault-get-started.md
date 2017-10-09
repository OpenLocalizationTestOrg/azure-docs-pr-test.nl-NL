---
title: aaaGet de slag met Azure Sleutelkluis | Microsoft Docs
description: Gebruik van deze zelfstudie toohelp die u aan de slag met Azure Key Vault toocreate een geharde container in Azure, toostore en beheren van de cryptografische sleutels en geheimen in Azure.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Aan de slag met Azure Sleutelkluis
Azure Sleutelkluis is beschikbaar in de meeste regio's. Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Inleiding
Gebruik van deze zelfstudie toohelp die u aan de slag met Azure Key Vault toocreate een geharde container (een kluis) in Azure, toostore en beheren van de cryptografische sleutels en geheimen in Azure. Deze begeleidt u bij Hallo proces van het gebruik van Azure PowerShell toocreate een kluis die een sleutel of het wachtwoord dat u vervolgens met een Azure-toepassing gebruiken kunt bevat. Vervolgens wordt uitgelegd hoe een toepassing de sleutel of het wachtwoord kan gebruiken.

**Geschatte tijd toocomplete:** 20 minuten

> [!NOTE]
> Deze zelfstudie bevat geen instructies voor hoe toowrite hello Azure-toepassing die een Hallo stappen bevat, namelijk hoe tooauthorize een toouse toepassing een sleutel of geheim in de sleutel Hallo-kluis.
>
> In deze zelfstudie wordt Azure PowerShell gebruikt. Zie [deze equivalente zelfstudie](key-vault-manage-with-cli2.md) voor instructies om een platformonafhankelijke opdrachtregelinterface te maken.
>
>

Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie hebt u hello te volgen:

* Een abonnement tooMicrosoft Azure. Als u nog geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell, **minimaal versie 1.1.0 of hoger**. tooinstall Azure PowerShell en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Als u Azure PowerShell al hebt geïnstalleerd en het Hallo-versie van hello Azure PowerShell-console niet weet, typt u `(Get-Module azure -ListAvailable).Version`. Ook wanneer u een van de versies van Azure PowerShell versie 0.9.1 tot en met 0.9.8 hebt geïnstalleerd, kunt u deze zelfstudie gebruiken en zij er slechts enkele kleine wijzigingen van toepassing. Bijvoorbeeld, moet u Hallo `Switch-AzureMode AzureResourceManager` opdracht en bepaalde hello Azure Sleutelkluis-opdrachten zijn gewijzigd. Zie voor een lijst van Hallo Sleutelkluis-cmdlets voor versie 0.9.1 tot en met 0.9.8 [Azure Sleutelkluis-Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).
* Een toepassing die worden zal geconfigureerde toouse Hallo sleutel of het wachtwoord die u in deze zelfstudie maakt. Er is een voorbeeldtoepassing beschikbaar is via Hallo [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Zie voor instructies Hallo bijbehorende Leesmij-bestand.

Deze zelfstudie is ontworpen voor beginnende gebruikers van Azure PowerShell, maar er wordt vanuit gegaan dat u Hallo-basisconcepten, zoals modules, cmdlets en sessies begrijpt. Zie [Aan de slag met Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx) voor meer informatie.

tooget gedetailleerde help voor een cmdlet die u in deze zelfstudie gebruik Hallo ziet **Get-Help** cmdlet.

    Get-Help <cmdlet-name> -Detailed

Bijvoorbeeld, tooget help voor Hallo **Login-AzureRmAccount** cmdlet, type:

    Get-Help Login-AzureRmAccount -Detailed

U kunt ook de volgende zelfstudies tooget bekend met Azure Resource Manager in Azure PowerShell Hallo lezen:

* [Hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)
* [Azure PowerShell gebruiken met Resource Manager](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Verbinding maken met tooyour abonnementen
Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met de volgende opdracht Hallo:  

    Login-AzureRmAccount

Let op: als u een specifiek exemplaar van Azure, bijvoorbeeld Azure Government, gebruikt u Hallo - omgeving parameter met deze opdracht. Bijvoorbeeld: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord. Azure PowerShell haalt alle Hallo-abonnementen die gekoppeld aan dit account en standaard zijn, gebruikt de eerste Hallo.

Als u meerdere abonnementen hebt en wilt dat een specifieke één toouse toospecify voor Azure Sleutelkluis, typt u Hallo toosee Hallo abonnementen voor uw account te volgen:

    Get-AzureRmSubscription

Vervolgens toospecify Hallo abonnement toouse, type:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Zie voor meer informatie over het configureren van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Een nieuwe resourcegroep maken
Als u Azure Resource Manager gebruikt, worden alle gerelateerde resources gemaakt binnen een resourcegroep. In deze zelfstudie maken we de resourcegroep **ContosoResourceGroup**:

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Een sleutelkluis maken
Gebruik Hallo [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate een sleutelkluis. Deze cmdlet heeft drie verplichte parameters: een **Resourcegroepnaam**, een **sleutelkluisnaam**, en Hallo **geografische locatie**.

Bijvoorbeeld, als u Hallo kluisnaam **ContosoKeyVault**, Hallo Resourcegroepnaam **ContosoResourceGroup**, en de locatie van Hallo **Oost-Azië**, type:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

Hallo-uitvoer van deze cmdlet ziet u de eigenschappen van Hallo sleutelkluis die u zojuist hebt gemaakt. Hallo twee belangrijkste eigenschappen zijn:

* **Vault Name**: In Hallo voorbeeld is dit **ContosoKeyVault**. U gebruikt deze naam voor andere Sleutelkluis-cmdlets.
* **Vault URI**: In Hallo voorbeeld is dit https://contosokeyvault.vault.azure.net/. Toepassingen die via de REST API gebruikmaken van uw kluis, moeten deze URI gebruiken.

Uw Azure-account is nu geautoriseerde tooperform bewerkingen op deze sleutel kluis. Tot dusver is er nog niemand anders gemachtigd.

> [!NOTE]
> Als u Hallo fout ziet **Hallo-abonnement is niet geregistreerd toouse naamruimte 'Microsoft.KeyVault'** wanneer u toocreate de nieuwe sleutelkluis uitvoeren probeert `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` en voer vervolgens opdracht New-AzureRmKeyVault opnieuw uit. Zie [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) voor meer informatie.
>
>

## <a id="add"></a>Een sleutel of geheim toohello sleutelkluis toevoegen
Als u toocreate Azure Sleutelkluis een softwarematig beveiligde sleutel voor u wilt, gebruikt u Hallo [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet, en typ de volgende Hallo:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Echter, als er een bestaande softwarematig beveiligde sleutel in een. PFX-bestand opgeslagen tooyour C:\ station in een bestand met de naam softkey.pfx dat u wilt dat tooupload tooAzure Sleutelkluis, type Hallo na tooset Hallo variabele **securepfxpwd** voor het wachtwoord **123** voor Hallo. PFX-bestand:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Typ vervolgens de volgende tooimport Hallo sleutel uit Hallo Hallo. PFX-bestand, dat Hallo sleutel met software in Hallo Sleutelkluis-service beveiligt kan worden gebruikt:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


U kunt nu verwijzen naar deze sleutel die u hebt gemaakt of geüpload tooAzure Sleutelkluis, met behulp van de URI. Gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget deze specifieke versie.  

toodisplay hello URI voor deze sleutel, type:

    $Key.key.kid

tooadd een kluis geheime toohello, die een wachtwoord met de naam SQLPassword en Hallo waarde heeft van Pa$ $w0rd tooAzure Sleutelkluis, converteert u eerst Hallo-waarde van Pa$ $w0rd tooa beveiligde tekenreeks door Hallo volgende te typen:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Typ de volgende Hallo:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

U kunt nu verwijzen naar dit wachtwoord dat u met behulp van de URI tooAzure Sleutelkluis, toegevoegd. Gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget deze specifieke versie.

toodisplay hello URI voor dit geheim, type:

    $secret.Id

We bekijken Hallo sleutel of geheim dat u zojuist hebt gemaakt:

* tooview uw sleutel, type:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview uw geheime, type:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

De sleutelkluis en sleutel of geheim is nu gereed voor toepassingen toouse. U moet toepassingen toouse machtigt ze.  

## <a id="register"></a>Een toepassing registreren met Azure Active Directory
Deze stap wordt doorgaans uitgevoerd door een ontwikkelaar op een afzonderlijke computer. Is geen specifieke tooAzure Sleutelkluis, maar is hier opgenomen voor de volledigheid.

> [!IMPORTANT]
> toocomplete hello zelfstudie, uw account, Hallo kluis en Hallo-toepassing die u in deze stap registreren wilt moeten alle liggen Hallo dezelfde Azure-directory.
>
>

Toepassingen die gebruikmaken van een sleutelkluis moeten een token van Azure Active Directory gebruiken om zich te verifiëren. toodo deze, Hallo eigenaar van de toepassing hello moet Hallo-toepassing eerst registreren in Azure Active Directory. De eigenaar van de toepassing hello opgehaald Hallo na registratie Hallo volgende waarden:

* Een **toepassings-ID** (ook wel bekend als een Client-ID) en **verificatiesleutel** (ook wel bekend als Hallo gedeelde geheim genoemd). Hallo-toepassing moet beide deze waarden tooAzure Active Directory tooget bieden een token. Hoe de toepassing hello is dit afhankelijk van de toepassing hello toodo geconfigureerd. Voor Hallo voorbeeldtoepassing voor Sleutelkluis stelt u de eigenaar van de toepassing hello deze waarden in Hallo app.config-bestand.

tooregister hello toepassing in Azure Active Directory:

1. Meld u aan toohello klassieke Azure-portal.
2. Klik aan de linkerkant Hallo op **Active Directory**, en selecteer vervolgens Hallo directory waarin u uw toepassing wilt registreren. <br> <br> **Opmerking:** Hallo moet u dezelfde map waarin zich hello Azure-abonnement waarmee u de sleutelkluis hebt gemaakt. Als u niet welke directory dit weet is, klikt u op **instellingen**, identificeert Hallo-abonnement waarmee u de sleutelkluis hebt gemaakt en Opmerking Hallo-naam van Hallo-map weergegeven in de laatste kolom Hallo.
3. Klik op **TOEPASSINGEN**. Als u geen apps tooyour directory zijn toegevoegd, wordt op deze pagina alleen Hallo **een App toevoegen** koppeling. Klik op de koppeling Hallo of u kunt ook klikken op **toevoegen** op Hallo opdrachtbalk klikken.
4. In Hallo **toepassing toevoegen** wizard op Hallo **wat wilt u wilt dat toodo?** pagina, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.
5. Op Hallo **Vertel ons over uw toepassing** pagina, Geef een naam voor uw toepassing en selecteer vervolgens **WEBTOEPASSING en/of WEB-API** (Hallo standaard). Klik op Hallo **volgende** pictogram.
6. Op Hallo **App-eigenschappen** pagina, geeft u Hallo **AANMELDINGS-URL** en **APP ID URI** voor uw webtoepassing. Als uw toepassing deze waarden niet heeft, kunt u voor deze stap zelf iets verzinnen (u kunt voor beide vakken bijvoorbeeld http://test1.contoso.com opgeven). Het maakt niet uit of deze sites bestaan. Wat is het belangrijk is dat die Hallo app ID URI voor elke toepassing verschilt voor elke toepassing in uw directory. Hallo directory gebruikt deze tekenreeks tooidentify uw app.
7. Klik op Hallo **Complete** pictogram toosave uw wijzigingen in de wizard Hallo.
8. Op Hallo **Quick Start** pagina, klikt u op **configureren**.
9. Schuif toohello **sleutels** sectie, selecteer Hallo duur en klik vervolgens op **opslaan**. Hallo-pagina wordt vernieuwd en bevat nu een sleutelwaarde. U moet uw toepassing configureren met deze sleutelwaarde en Hallo **CLIENT-ID** waarde. (Instructies voor deze configuratie zijn toepassingsspecifiek.)
10. Kopieer Hallo client-id-waarde van deze pagina wordt gebruikt in Hallo volgende stap tooset machtigingen voor uw kluis.

## <a id="authorize"></a>Autoriseren hello toepassing toouse Hallo sleutel of geheim
tooauthorize hello toepassing tooaccess Hallo sleutel of geheim in Hallo kluis, gebruikt de [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.

Bijvoorbeeld, als uw kluisnaam **ContosoKeyVault** en gewenste tooauthorize client-ID van 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed heeft en u wilt dat tooauthorize Hallo toepassing toodecrypt en meld u met de sleutels in Hallo-toepassing uw kluis uit te voeren Hallo volgende:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Als u dat dezelfde toepassing tooread geheimen tooauthorize in uw kluis wilt, voert u Hallo volgende:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Als u wilt dat toouse een hardware security module (HSM)
U kunt voor de zekerheid importeren of genereren van sleutels in hardware security modules (HSM's) die Hallo HSM-grens nooit verlaten. Hallo HSM's zijn FIPS 140-2 Level 2-gevalideerde modules. Als deze vereiste niet van toepassing tooyou, kunt u deze sectie overslaan en gaat u te[hello sleutelkluis en de bijbehorende sleutels en geheimen verwijderen](#delete).

toocreate deze met HSM beveiligde sleutels, moet u Hallo [Azure Key Vault Premium service tier toosupport HSM beveiligde sleutels](https://azure.microsoft.com/pricing/free-trial/). Deze functionaliteit is niet beschikbaar voor Azure China.

Wanneer u de sleutelkluis Hallo maakt, voegt u Hallo **- SKU** parameter:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



U kunt softwarematige beveiligde sleutels (zoals hiervoor) en de HSM beveiligde sleutels toothis sleutelkluis toevoegen. toocreate een HSM beschermde sleutel set Hallo **-bestemming** parameter too'HSM':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

U kunt volgende opdracht tooimport Hallo een sleutel van een. PFX-bestand op uw computer. Deze opdracht wordt Hallo sleutel geïmporteerd in HSM's in Hallo Sleutelkluis-service:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


de volgende opdracht Hallo importeert u een 'bring your own key' (BYOK)-pakket. Dit scenario kunt u uw sleutel in uw lokale HSM genereren en overdragen tooHSMs in Hallo Sleutelkluis-service, zonder Hallo sleutel Hallo HSM-grens verlaat:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Voor instructies over het gedetailleerde toogenerate dit BYOK-pakket Zie [hoe toogenerate en de overdracht met HSM beveiligde sleutels voor Azure Sleutelkluis](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Hallo sleutelkluis en de bijbehorende sleutels en geheimen verwijderen
Als u niet langer Hallo sleutelkluis en sleutel Hallo of het geheim die deze bevat, kunt u Hallo sleutelkluis verwijderen met behulp van Hallo [verwijderen AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Of u kunt een volledige Azure-resourcegroep, waaronder Hallo sleutelkluis en alle andere resources die u hebt opgenomen in de groep verwijderen:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Overige Azure PowerShell-cmdlets
Overige opdrachten die handig kunnen zijn voor het beheren van Azure Sleutelkluis:

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: met deze opdracht worden alle sleutels en geselecteerde eigenschappen weergegeven in een tabel.
* `$Keys[0]`: Met deze opdracht geeft een volledige lijst met eigenschappen voor de opgegeven sleutel Hallo
* `Get-AzureKeyVaultSecret`: met deze opdracht worden alle geheime namen en geselecteerde eigenschappen weergegeven in een tabel.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Voorbeeld hoe tooremove een specifieke sleutel.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Voorbeeld hoe tooremove een specifiek geheim.

## <a id="next"></a>Volgende stappen
Zie [Azure Key Vault in een webtoepassing gebruiken](key-vault-use-from-web-application.md) voor een vervolgzelfstudie over het gebruik van Azure Key Vault in een webtoepassing.

toosee hoe uw sleutelkluis wordt gebruikt, Zie [logboekregistratie van Azure Sleutelkluis](key-vault-logging.md).

Zie voor een lijst met Hallo nieuwste Azure PowerShell-cmdlets voor Azure Sleutelkluis, [Azure Sleutelkluis-Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).

Zie voor het programmeren van verwijzingen [Hallo ontwikkelaarshandleiding Azure Key Vault](key-vault-developers-guide.md).
